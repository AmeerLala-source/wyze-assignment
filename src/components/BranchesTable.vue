<script setup>
const props = defineProps({
  branches: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <section class="branches-table-wrapper">
    <h2>רשימת סניפים</h2>

    <table class="branches-table">
      <thead>
        <tr>
          <th>מזהה</th>
          <th>שם הסניף</th>
          <th>כתובת</th>
          <th>עיר</th>
          <th>אזור</th>
          <th>ניווט</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="branch in branches" :key="branch.store_id">
          <td>{{ branch.store_id }}</td>
          <td>{{ branch.store_title }}</td>
          <td>{{ branch.store_address }}</td>
          <td>{{ branch.city.trim() }}</td>
          <td>{{ branch.store_region }}</td>
          <td>
            <a
              :href="`https://www.google.com/maps?q=${branch.gps_location}`"
              target="_blank"
              rel="noopener noreferrer"
            >
              פתח במפות
            </a>
          </td>
        </tr>
      </tbody>
    </table>

    <p v-if="branches.length === 0">לא נמצאו סניפים.</p>
  </section>
</template>

<style scoped>
.branches-table-wrapper {
  direction: rtl;
  text-align: right;
  padding: 1rem;
  font-family: 'Arial', sans-serif;
}

h2 {
  margin-bottom: 1rem;
  color: #333;
}

.branches-table {
  width: 100%;
  border-collapse: collapse;
  background-color: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.branches-table th,
.branches-table td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid #ddd;
}

.branches-table th {
  background-color: #f1f1f1;
  font-weight: bold;
}

.branches-table td a {
  color: #0d6efd;
  text-decoration: underline;
}

.branches-table tr:last-child td {
  border-bottom: none;
}
</style>
