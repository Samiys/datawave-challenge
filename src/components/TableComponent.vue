<template>
  <div>
    <table class="table-auto w-full text-left border-separate">
      <thead>
      <tr class="text-sm table-head">
        <th class="w-[252px] h-[60px]">Firmenname</th>
        <th class="w-[164px] h-[60px]">Ansprechpartner</th>
        <th class="w-[208px] h-[60px]">
          <div class="flex items-center space-x-2">
            <span>E-Mail Adresse</span>
            <svg class="cursor-pointer" width="11" height="12" viewBox="0 0 11 12" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3.85015 7.65007L5.50015 9.30007L7.15015 7.65007M7.15015 4.35007L5.50015 2.70007L3.85015 4.35007" stroke="#222222" stroke-width="0.916667" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
        </th>
        <th class="w-[153px] h-[60px]">Telefon</th>
        <th class="w-[114px] h-[60px]">K-Gruppe</th>
        <th class="w-[103px] h-[60px]">Status</th>
        <th class="w-[50px] h-[60px]"></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(row, index) in tableData" :key="index" class="border-b hover:bg-gray-50">
        <td class="flex items-center space-x-3 py-3">
          <img :src="'/src/assets/' + row.img" alt="Logo" class="w-10 h-10 rounded-full" />
          <span class="company-style">{{ row.company }}</span>
        </td>
        <td class="text-style">{{ row.contactPerson }}</td>
        <td class="text-blue-600 text-style">{{ row.email }}</td>
        <td class="text-style">{{ row.phone }}</td>
        <td><span class="tag">{{ row.group }}</span></td>
        <td>
          <span class="status">
            <span class="dot"></span>
            {{ row.status }}
          </span>
        </td>
        <td>
          <button class="text-gray-400 hover:text-gray-600">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-6 h-6">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v.01M12 12v.01M12 18v.01" />
            </svg>
          </button>
        </td>
      </tr>
      </tbody>
    </table>

    <div class="pagination-container">
      <div class="pagination-controls">
        <button class="pagination-button" :disabled="page === 1" @click="prevPage">
          <svg class="icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        <button v-for="pageNumber in totalPages" :key="pageNumber" class="pagination-button" :class="{'active': pageNumber === page}" @click="goToPage(pageNumber)">
          {{ pageNumber }}
        </button>
        <button class="pagination-button" :disabled="page === totalPages" @click="nextPage">
          <svg class="icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>
      <div class="rows-per-page">
        <span>{{ tableData.length }} pro Seite</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TableComponent',
  props: {
    tableData: Array,
    page: Number,
    totalPages: Number,
  },
  methods: {
    prevPage() {
      this.$emit('prev-page');
    },
    nextPage() {
      this.$emit('next-page');
    },
    goToPage(pageNumber) {
      this.$emit('go-to-page', pageNumber);
    },
  },
};
</script>
