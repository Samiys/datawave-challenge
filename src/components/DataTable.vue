<template>
  <div class="w-full bg-white p-4 rounded-md">
    <!-- Table with filters and pagination -->
    <div class="flex items-center justify-between mb-4">
      <!-- Search and Filter buttons -->
      <div class="flex space-x-4">
        <input
            type="text"
            placeholder="Suche"
            class="border px-4 py-2 rounded-full w-64"
        />
        <button class="px-4 py-2 rounded-full bg-gray-100">Kunde</button>
        <button class="px-4 py-2 rounded-full bg-gray-100">Ansprechpartner</button>
        <button class="px-4 py-2 rounded-full bg-gray-100">Kundengruppe</button>
        <button class="px-4 py-2 rounded-full bg-gray-100">Weitere Filter</button>
      </div>
    </div>

    <table class="table-auto w-full text-left border-separate">
      <thead>
      <tr class="text-gray-500 text-sm">
        <th class="w-[252px] h-[60px]">Firmenname</th>
        <th class="w-[164px] h-[60px]">Ansprechpartner</th>
        <th class="w-[208px] h-[60px]">E-Mail Adresse</th>
        <th class="w-[153px] h-[60px]">Telefon</th>
        <th class="w-[114px] h-[60px]">K-Gruppe</th>
        <th class="w-[103px] h-[60px]">Status</th>
        <th class="w-[50px] h-[60px]"></th> <!-- For the options icon -->
      </tr>
      </thead>
      <tbody>
      <tr
          v-for="(row, index) in tableData"
          :key="index"
          class="border-b hover:bg-gray-50"
      >
        <!-- Firmenname with image -->
        <td class="flex items-center space-x-3 py-4">
          <img :src="'/src/assets/' + row.img" alt="Logo" class="w-10 h-10 rounded-full" />
          <span>{{ row.company }}</span>
        </td>
        <td>{{ row.contactPerson }}</td>
        <td class="text-blue-600">{{ row.email }}</td>
        <td>{{ row.phone }}</td>
        <td>
          <span class="tag">{{ row.group }}</span>
        </td>
        <td>
          <span class="status">{{ row.status }}</span>
        </td>
        <td>
          <!-- Options button with three dots -->
          <button class="text-gray-400 hover:text-gray-600">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="2"
                stroke="currentColor"
                class="w-6 h-6"
            >
              <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 6v.01M12 12v.01M12 18v.01"
              />
            </svg>
          </button>
        </td>
      </tr>
      </tbody>
    </table>

    <!-- Pagination -->
    <div class="flex items-center justify-between mt-4">
      <div class="text-sm text-gray-600">10 pro Seite</div>
      <div class="flex space-x-2">
        <button
            class="px-3 py-1 border rounded-md bg-white hover:bg-gray-100"
            :disabled="page === 1"
            @click="prevPage"
        >
          &lt;
        </button>
        <button
            v-for="pageNumber in totalPages"
            :key="pageNumber"
            class="px-3 py-1 border rounded-md bg-white hover:bg-gray-100"
            @click="goToPage(pageNumber)"
        >
          {{ pageNumber }}
        </button>
        <button
            class="px-3 py-1 border rounded-md bg-white hover:bg-gray-100"
            :disabled="page === totalPages"
            @click="nextPage"
        >
          &gt;
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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
    };
  },
  methods: {
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

<style scoped>
.tag {
  @apply px-2 py-1 rounded-full bg-purple-100 text-purple-800 text-sm;
}

.status {
  @apply px-2 py-1 rounded-full bg-green-100 text-green-800 text-sm;
}
</style>
