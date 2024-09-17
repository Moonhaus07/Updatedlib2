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
        </div>
      </div>
  
      <!-- Search Bar - Centered and Spaced Above Table -->
      <div class="flex justify-center mt-8 mb-6">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search customer"
          class="px-4 py-2 border border-gray-300 rounded-lg"
        />
      </div>
  
      <!-- Customer Table -->
      <div class="mt-12 shadow-sm border rounded-lg overflow-x-auto">
        <table class="w-full table-auto text-sm text-left">
          <thead class="bg-gray-50 text-gray-600 font-medium border-b">
            <tr>
              <th class="py-3 px-6">
                <input
                  type="checkbox"
                  v-model="selectAll"
                  @change="toggleSelectAll"
                  class="form-checkbox"
                />
              </th>
              <th class="py-3 px-6">Employee ID</th>
            <th class="py-3 px-6">Name</th>
            <th class="py-3 px-6">Email</th>
            <th class="py-3 px-6">Telephone#</th>
            <th class="py-3 px-6">Birthday</th>
            <th class="py-3 px-6">Gender</th>
            <th class="py-3 px-6">Civil Status</th>
            <th class="py-3 px-6">Group Name</th>
            <th class="py-3 px-6">House Street</th>
            <th class="py-3 px-6">Purok Zone</th>
            <th class="py-3 px-6">postal Code</th>
            <th class="py-3 px-6">Pesonality Status</th>
            <th class="py-3 px-6">Barangay</th>
            <th class="py-3 px-6">City</th>
            <th class="py-3 px-6">Country</th>
            <th class="py-3 px-6">Province</th>
            <th class="py-3 px-6">Credit Status</th>
            <th class="py-3 px-6">Date Created</th>
            <th class="py-3 px-6">Date Last Modified</th>
            <th class="py-3 px-6">Passbook Number</th>
            <th class="py-3 px-6">Loan Count</th>
            <th class="py-3 px-6">Mortuary Status</th>
            <th class="py-3 px-6">Mortuary Coverage Start</th>
            <th class="py-3 px-6">Mortuary Coverage End</th>
            <th class="py-3 px-6">Notes</th>
              <th class="py-3 px-6"></th>
            </tr>
          </thead>
          <tbody class="text-gray-600 divide-y">
            <tr v-for="(item, idx) in filteredTableItems" :key="idx">
              <td class="px-6 py-4 whitespace-nowrap">
                <input
                  type="checkbox"
                  v-model="selectedItems"
                  :value="item.employeeId"
                  class="form-checkbox"
                />
              </td>
              <td class="px-6 py-4 whitespace-nowrap">{{ item.employeeId }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.name }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.email }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.telephoneNumber }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.birthday }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.gender }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.civilStatus }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.groupName }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.houseStreet }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.purokZone }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.postalCode }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.personalityStatus }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.Barangay }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.city }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.country }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.province }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.creditStatus }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.dateCreated }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.dateLastModified }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.passbookNumber }}</td>
            <td class="px-6 py-4 whitespace-nowrap">{{ item.loanCount }}</td>
              <!-- Display Mortuary Status with Color Indicator -->
              <td class="px-6 py-4 whitespace-nowrap">
                <span :class="{'bg-green-500': item.mortuaryStatus, 'bg-red-500': !item.mortuaryStatus}" class="inline-block w-3 h-3 rounded-full"></span>
                {{ item.mortuaryStatus ? 'Enabled' : 'Disabled' }}
              </td>
              <td class="px-6 py-4 whitespace-nowrap">{{ item.mortuaryCoverageStart }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ item.mortuaryCoverageEnd }}</td>
              <td class="text-right px-6 whitespace-nowrap">
                <button @click="editMember(item)" class="py-1.5 px-3 bg-blue-200 hover:bg-blue-300 rounded">
                  <a href="CustomerEditComponent">Edit</a>
                </button>
              </td>
            </tr>
            <tr v-if="filteredTableItems.length === 0">
              <td colspan="12" class="text-center py-4 text-gray-600">No data found</td>
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
        tableItems: [
          //{ employeeId: "001", name: "Liam James", email: "liam@example.com", phoneNumber: "123456789", groupName: "Group A", passbookNumber: "PB001", loanCount: 2, mortuaryStatus: true, mortuaryCoverageStart: "2021-01-01", mortuaryCoverageEnd: "2023-12-31" },
          //{ employeeId: "002", name: "Emma Olivia", email: "emma@example.com", phoneNumber: "987654321", groupName: "Group B", passbookNumber: "PB002", loanCount: 3, mortuaryStatus: false, mortuaryCoverageStart: "2020-05-01", mortuaryCoverageEnd: "2023-05-01" }
        ],
        selectedItems: [],
        selectAll: false
      };
    },
    computed: {
      filteredTableItems() {
        return this.tableItems.filter(item => {
          return Object.values(item).some(value =>
            String(value).toLowerCase().includes(this.searchQuery.toLowerCase())
          );
        });
      }
    },
    methods: {
      editMember(item) {
        // Redirect or navigate to edit view with item ID
        this.$router.push({ name: 'EditCustomer', params: { id: item.employeeId } });
      },
      toggleSelectAll() {
        if (this.selectAll) {
          this.selectedItems = this.filteredTableItems.map(item => item.employeeId);
        } else {
          this.selectedItems = [];
        }
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
  
  input[type="text"] {
    width: 50%;
  }
  
  /* Color Indicator Styles */
  .inline-block {
    display: inline-block;
  }
  </style>
  