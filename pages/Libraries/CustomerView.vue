<template>

    <div class="bg-white">
        <header class="py-8 px-4 md:px-16">
          <div class="container mx-auto flex justify-between items-center">
            <img src="../../img/LendCash_Logo-removebg-preview.png" class="w-20" alt="logo" />
          </div>
        </header>
      </div>
    
      <div class="max-w-screen-xl mx-auto px-4 md:px-8">
        <div class="items-start justify-between md:flex">
          <div class="max-w-lg">
            <h3 class="text-gray-800 text-xl font-bold sm:text-2xl">Customers</h3>
          </div>
          <div class="mt-3 md:mt-0 flex flex-col items-start gap-y-4">
            <a href="javascript:void(0)" class="inline-block px-4 py-2 text-white duration-150 font-medium bg-indigo-600 rounded-lg hover:bg-indigo-500 active:bg-indigo-700 md:text-sm">
              Add Customer
            </a>
            <!-- Search Bar -->
            <div class="mb-4 flex justify-center">
            <input
              type="text"
              placeholder="Search customers"
              class="px-4 py-2 border border-gray-300 rounded-lg"
            />
          </div>
          </div>
        </div>
        <div class="mt-12 shadow-sm border rounded-lg overflow-x-auto">
          <table class="w-full table-auto text-sm text-left">
            <thead class="bg-gray-50 text-gray-600 font-medium border-b">
              <tr>
                <th class="py-3 px-6">Customer ID</th>
                <th class="py-3 px-6">Name</th>
                <th class="py-3 px-6">group ID</th>
                <th class="py-3 px-6">Passbook Number</th>
                <th class="py-3 px-6">Loan count</th>
                <th class="py-3 px-6">Mortuary Coverage start</th>
                <th class="py-3 px-6">Mortuary Coverage end</th>
                <th class="py-3 px-6"></th>
              </tr>
            </thead>
            <tbody class="text-gray-600 divide-y">
              <tr v-for="(item, idx) in filteredTableItems" :key="idx">
                <td class="px-6 py-4 whitespace-nowrap">{{ item.customerId }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.name }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.groupId }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.passbookNumber }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.loanCount }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.mortuaryCoverageStart }}</td>
                <td class="px-6 py-4 whitespace-nowrap">{{ item.mortuaryCoverageEnd }}</td>
                <td class="text-right px-6 whitespace-nowrap">
                  <button @click="editMember(item)" class="py-2 px-3 font-medium text-indigo-600 hover:text-indigo-500 duration-150 hover:bg-gray-50 rounded-lg">
                    Edit
                  </button>
                </td>
              </tr>
              <tr v-if="filteredTableItems.length === 0">
                <td colspan="8" class="text-center py-4 text-gray-600">No data found</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </template>
    
    <script>
    export default {
      data() {
        return {
          searchQuery: '',
          tableItems: [] // Table items left blank
        }
      },
      computed: {
        filteredTableItems() {
          return this.tableItems.filter(item => {
            return Object.values(item).some(value =>
              value.toLowerCase().includes(this.searchQuery.toLowerCase())
            );
          });
        }
      },
      methods: {
        editMember(item) {
          console.log('Editing member:', item);
        }
      }
    }
    </script>
    
    <style scoped>
    button {
      padding: 8px 12px;
      font-size: 0.875rem;
      text-align: center;
    }
    </style>
    