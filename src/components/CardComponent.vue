<template>
  <div class="w-[1200px] p-5 bg-white border-radius-20">
    <FilterToolbar @filter-changed="handleFilterChange" />
    <TableComponent
        @filter-changed="handleFilterChange"
        @prev-page="prevPage"
        @next-page="nextPage"
        @go-to-page="goToPage"
        :tableData="filteredTableData"
        :page="page"
        :totalPages="totalPages"
    />
  </div>
</template>

<script>
import FilterToolbar from './FilterToolbar.vue';
import TableComponent from './TableComponent.vue';

export default {
  name: 'CardComponent',
  components: {
    FilterToolbar,
    TableComponent,
  },
  data() {
    return {
      tableData: [
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "1.png"
        },
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "2.png"
        },
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "3.png"
        },
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "4.png"
        },
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "5.png"
        },
        {
          company: "1. FC Locaboo München",
          contactPerson: "Lisa Eschen.-Hierl",
          email: "lisa.e-hierl@locaboo.com",
          phone: "+4915731482345",
          group: "Vereine",
          status: "Aktiv",
          img: "6.png"
        },
      ],
      page: 1,
      totalPages: 3,
      filteredTableData: [],
      searchQuery: '',
      selectedFilter: '',
      selectedStatus: [],
    };
  },
  created() {
    this.applyFilters();
  },
  methods: {
    handleFilterChange(filters) {
      this.searchQuery = filters.searchQuery;
      this.selectedStatus = filters.selectedStatus;
      this.applyFilters();
    },
    applyFilters() {
      this.filteredTableData = this.tableData.filter(item => {
        const matchesStatus = this.selectedStatus.length === 0 || this.selectedStatus.includes(item.status);
        const matchesQuery = this.searchQuery === '' || item.company.includes(this.searchQuery) || item.contactPerson.includes(this.searchQuery);
        return matchesStatus && matchesQuery;
      });
    },
    prevPage() {
      if (this.page > 1) {
        this.page--;
      }
    },
    nextPage() {
      if (this.page < this.totalPages) {
        this.page++;
      }
    },
    goToPage(pageNumber) {
      this.page = pageNumber;
    },
  },
};
</script>
