<template>
  <div class="flex items-center justify-between mb-4">
    <div class="flex space-x-4">
      <!-- Search Input with applied styles -->
      <div class="search-container">
        <div class="search-icon"></div>
        <input
            type="text"
            placeholder="Suche"
            class="search-input"
            v-model="searchQuery"
            @input="emitFilterChange"
        />
      </div>
      <!-- Filter Buttons -->
      <button class="filter-button button-kunde" @click="applyFilter('Kunde')">Kunde</button>
      <button class="filter-button button-ansprechpartner" @click="applyFilter('Ansprechpartner')">Ansprechpartner</button>
      <button class="filter-button button-kundengruppe" @click="applyFilter('Kundengruppe')">Kundengruppe</button>

      <!-- Dropdown for Status Filter -->
      <div class="filter-dropdown-wrapper relative" ref="dropdown">
        <button
            @click="toggleDropdown"
            :class="{'bg-black text-white': selectedStatus.length, 'filter-button button-status': true}"
            class="flex items-center"
        >
          Status
          <span v-if="selectedStatus.length" class="filter-count ml-1 text-white">
              • {{ selectedStatus.length }}
              <svg
                  @click.stop="clearFilters"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                  stroke="currentColor"
                  class="w-4 h-4 clear-icon"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </span>
          </button>
        <div v-if="isDropdownOpen" class="absolute z-10 mt-2 w-44 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
          <div class="py-1" role="menu" aria-orientation="vertical">
            <label v-for="(option, index) in options" :key="index" class="flex items-center px-4 py-2 text-sm text-gray-700 cursor-pointer hover:bg-gray-100">
              <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" v-model="selectedStatus" :value="option" @change="emitFilterChange">
              <span class="ml-2 option-color">{{ option }}</span>
            </label>
          </div>
        </div>
      </div>
      <button class="filter-button button-filter" @click="applyFilter('Weitere Filter')">Weitere Filter</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FilterToolbar',
  data() {
    return {
      searchQuery: '',
      selectedStatus: [],
      selectedFilter: '',
      isDropdownOpen: false,
      options: ["Aktiv", "InAktiv", "Gast", "Registriert"],
    };
  },
  methods: {
    applyFilter(filter) {
      this.selectedFilter = filter;
      this.emitFilterChange();
    },
    emitFilterChange() {
      this.$emit('filter-changed', {
        searchQuery: this.searchQuery,
        selectedStatus: this.selectedStatus,
        selectedFilter: this.selectedFilter
      });
    },
    toggleDropdown() {
      this.isDropdownOpen = !this.isDropdownOpen;
    },
    clearFilters() {
      this.selectedStatus = [];
      this.closeDropdown();
      this.emitFilterChange();
    },
    closeDropdown() {
      this.isDropdownOpen = false;
    },
    handleClickOutside(event) {
      const dropdown = this.$refs.dropdown;
      if (dropdown && !dropdown.contains(event.target)) {
        this.closeDropdown();
      }
    }
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
  },
  beforeDestroy() {
    document.removeEventListener('click', this.handleClickOutside);
  }
};
</script>
