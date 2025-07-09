<script setup>
import { onMounted, ref, computed, watch } from 'vue';
import PageTitle from './components/PageTitle.vue';
import DropDown from './components/DropDown.vue';
import TextField from './components/TextField.vue';
import BranchesTable from './components/BranchesTable.vue';

const storeData = ref([]);
const selectedArea = ref('');
const selectedCity = ref('');
const searchQuery = ref('');

// ✅ All unique areas
const areas = computed(() =>
  [...new Set(storeData.value.map(store => store.store_region))]
);

// ✅ Cities based on selected area
const cities = computed(() =>
  [...new Set(
    storeData.value
      .filter(store => !selectedArea.value || store.store_region === selectedArea.value)
      .map(store => store.city)
  )]
);


watch(searchQuery, () => {
  if (searchQuery.value.trim().length > 0) {
    selectedArea.value = '';
    selectedCity.value = '';
  }
});

watch(selectedArea, () => {
  if (selectedArea.value) {
    selectedCity.value = '';
  }
});

// ✅ Filtered branches (stores)
const filteredStores = computed(() =>
  storeData.value.filter(store => {
    const matchesArea = !selectedArea.value || store.store_region === selectedArea.value;
    const matchesCity = !selectedCity.value || store.city === selectedCity.value;
    const matchesSearch = !searchQuery.value || store.store_title.toLowerCase().includes(searchQuery.value.toLowerCase());
    return matchesArea && matchesCity && matchesSearch;
  })
);

const resetFilters = () => {
  selectedArea.value = '';
  selectedCity.value = '';
  searchQuery.value = '';
};
// ✅ Fetch store data
onMounted(async () => {
  try {
    const response = await fetch('/data.json');
    const data = await response.json();
    storeData.value = data.map(store => ({
      ...store,
      city: store.city.trim(),
    }));
  } catch (error) {
    console.error('Error fetching store data:', error);
  }
});
</script>

<template>
  <PageTitle title="סניפי מקדונלד'ס בישראל" />

  <div class="filters">
    <DropDown
      v-model="selectedArea"
      :options="areas"
      placeholder="בחר אזור"
    />

    <DropDown
      v-model="selectedCity"
      :options="cities"
      placeholder="בחר עיר"
    />

    <TextField
      v-model="searchQuery"
      label="חפש סניף לפי שם"
      placeholder="הכנס שם סניף לחיפוש"
      id="searchField"
    />
    <button class="reset-btn" @click="resetFilters">איפוס סינון</button>
  </div>

  <BranchesTable :branches="filteredStores" />
</template>

<style scoped>
.filters {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}
.reset-btn {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border-radius: 8px;
  border: none;
  background-color: #f44336;
  color: white;
  cursor: pointer;
}
</style>
