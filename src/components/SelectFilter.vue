 <template>
  <div :class="className">

    <div class="filter-container">
      <div class="fliter-title" @click="filterShow">
        Filter
        <i class="fas fa-caret-down" :class=" { arrowUp: isActive }"></i>
      </div>
      <div class="search-box">
        <i class="fas fa-search"></i>
        <input type="text" v-model="search" placeholder="Search">
      </div>
    </div>

    <div v-if="filters" class="filters" :class=" { active: isActive }">
      <div v-for="(selectFilter, selectKey) in filters" :key="selectKey" class="select__container">
        <label :for="`select-filter-${selectKey}`">{{ selectFilter.label }}</label>
        <select
          class="select-box"
          :id="`select-filter-${selectKey}`"
          v-model="selectFilter.current"
        >
          <option
            v-for="(singleOption, optionKey) in selectFilter.options"
            :key="optionKey"
            v-bind:value="singleOption.value"
            class="'select-option'"
            :id="`select-option-${optionKey}`"
          >{{ singleOption.text }}</option>
        </select>
      </div>
    </div>

    <div v-if="showFilteredData" class="filtered-data">
      <table v-if="this.filteredData.length >= 1">
        <tr>
          <!-- <th v-for="(title, titleKey) in tableHeader"
          :key="titleKey">{{ title }}</th>-->
          <th>Username</th>
          <th>Role</th>
          <th>Fascia</th>
          <th>Services</th>
          <th>Actions</th>
        </tr>
        <tr v-for="(user, index) in filteredData" :key="index">
          <td>{{ user.username }}</td>
          <td>{{ user.role }}</td>
          <td>{{ user.fascias }}</td>
          <td>{{ user.services }}</td>
          <td>
            <div class="buttons-container">
              <button id="delete" class="users-list__buttons">
                <i class="fas fa-times-circle" title="remove user"></i>
              </button>
              <button id="edit" class="users-list__buttons">
                <i class="fas fa-check-circle" title="edit"></i>
              </button>
            </div>
          </td>
        </tr>
      </table>
      <p v-else class="filter-data__empty-message">{{ this.emptyMessage }}</p>
    </div>

  </div>
</template>

<script>
export default {
  name: "SelectFilter",

  props: {
    /**
     * The original data that will be filterd by the component
     */
    dataToFilter: {
      type: Array,
      default: () => [
        {
          username: "jhbjkbjh@test.com",
          role: "Admin",
          fascias: ["JDSPORTS", "JDSPORTS_BE"],
          services: ["Content Editor"]
        },
        {
          username: "bjhiiujb@test.com",
          role: "Edit",
          fascias: ["JDSPORTS"],
          services: ["Content Editor", "email_builder"]
        },
        {
          username: "opjjbvghc@test.com",
          role: "Admin",
          fascias: ["JDSPORTS_BE"],
          services: ["Raffle"]
        },
        {
          username: "dfxgvbbhj@test.com",
          role: "Manage",
          fascias: ["JDSPORTS"],
          services: ["Image"]
        }
      ]
    },

    /**
     * The select boxes used to filter the data
     */
    selectFilters: {
      type: Array,
      default: () => [
        {
          label: "Role",
          filterValue: "role",
          current: "",
          options: [
            {
              text: "All",
              value: ""
            },
            {
              text: "Admin",
              value: "admin"
            },
            {
              text: "Edit",
              value: "edit"
            },
            {
              text: "Manage",
              value: "manage"
            }
          ]
        },
        {
          label: "Fascia",
          filterValue: "fascias",
          current: "",
          options: [
            {
              text: "All",
              value: ""
            },
            {
              text: "JD Sports (GB)",
              value: "JDSPORTS"
            },
            {
              text: "JD Sports (IE)",
              value: "JDSPORTS_IE"
            },
            {
              text: "JD Sports (BE)",
              value: "JDSPORTS_BE"
            }
          ]
        },
        {
          label: "Service",
          filterValue: "services",
          current: "",
          options: [
            {
              text: "All",
              value: ""
            },
            {
              text: "Content Editor",
              value: "Content Editor"
            },
            {
              text: "Image",
              value: "image"
            },
            {
              text: "Raffle",
              value: "raffle"
            }
          ]
        }
      ]
    },

    /**
     * The message which appears if no data matches the filter criteria
     */
    emptyMessage: {
      type: String,
      default: "There are no results for the chosen filters."
    },

    /**
     * Toggle to show/hide the filtered data
     */
    showFilteredData: {
      type: Boolean,
      default: true
    }
  },

  data: () => ({
    isActive: false,
    search: "",
    className: "select-filter"
  //   tableHeader: ['Username', 'Role', 'Fascias', 'Services']
  }),

  computed: {
    filters() {
      return this.selectFilters;
    },

    filteredData() {

      console.log('HELLO')
      let filteredArray = this.dataToFilter;

     this.searchFilter = this.dataToFilter

      this.filters.forEach(filter => {
        filteredArray = this.filterByValue(
          filter.filterValue,
          this.getSelectedValue(filter.label),
          filteredArray);
      });

      this.searchFilter

      return filteredArray;
    }
  },

  methods: {
    searchFilter() {
      console.log('Hey')
    /*
     * NEED TO IMPLEMENT A SEARCH BOX FITLER
     */

    // const usernames = this.filteredData;

    // usernames.filter(username => username.match(this.search.toLowerCase()));

    // return this.search ? this.filteredData.filter(filtered => {
    //     for (let key in filtered) {
    //       if (filtered[key].toLowerCase().includes(this.search.toLowerCase())) {
    //           return true
    //         }
    //       }
    //     })
    //     : false;

      // return this.search ? this.items.filter(item => {
      //     let match = false
      //     for (let key in item) {
      //       console.log(item[key]);
      //       if (item[key].toLowerCase().includes(this.search.toLowerCase())) {
      //         return true
      //       }
      //     }
      //   })
      //   : this.items
    },
    filterShow() {
      if (this.isActive) {
        this.isActive = false;
      } else {
        this.isActive = true;
      }
    },

    getSelectedValue(value) {
      const toReturn = this.filters.filter(
        selectData => selectData.label === value
      );

      return toReturn[0].current;
    },

    filterByValue(key, currentValue, arrayToFilter) {
      let array = arrayToFilter;
      if (currentValue !== "") {
        array = arrayToFilter.filter(item => {
          if (Array.isArray(item[key])) {
            let checkSubArray = false;

            item[key].forEach(singleValue => {
              if (singleValue.toLowerCase() === currentValue.toLowerCase()) {
                checkSubArray = true;
                return true;
              }
              return false;
            });
            if (checkSubArray) {
              return item[key];
            }
          } else {
            return item[key].toLowerCase() === currentValue.toLowerCase();
          }

          return false;
        });
      }
      return array;
    }
  },
};
</script>

<style>
.filter-container {
  display: flex;
  color: #fff;
}
.fliter-title {
  color: #fff;
  cursor: pointer;
  margin-right: 1rem;
}
i.fas.fa-caret-down {
  padding-left: 0.3rem;
  cursor: pointer;
  align-items: center;
}
.filters {
  display: none;
  flex-flow: column wrap;
  transition: all 0.5s;
  flex-direction: row;
}

.filters .select__container {
  display: flex;
  flex-flow: row wrap;
  margin: 1rem 0;
  padding: 0.5rem;
  max-width: 100%;
  transition: all 0.5s;
  margin: 1rem;
  width: unset;
  color: #fff;
}
.filters label {
  flex: 1;
  font-size: 1rem;
  font-weight: 600;
}

.filters .select-box {
  border-radius: 20rem;
  font-size: 0.9rem;
  margin: 0 1rem;
  max-width: 100%;
  padding: 0 1rem;
  width: 15rem;
  border: 1px solid #fff;
  color: #fff;
  background: #a2cfec;
}

.filtered-data {
  margin: 1rem 0;
  display: flex;
  color: #fff;
}

.filtered-data .json {
  font-size: 0.8rem;
}
.search-box ::placeholder {
  color: #fff;
  font-size: 16px;
}

.active {
  display: flex !important;
}

i.fas.fa-caret-down.arrowUp {
  transform: rotate(-180deg);
  padding-right: 0.3rem;
  cursor: pointer;
  align-items: center;
  padding-left: 0;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  background-color: #fff;
}

td,
th {
  text-align: center;
  width: 20%;
  padding: 10px;
  font-weight: 600;
}

th {
  color: #a2cfec;
}

th:nth-child(even) {
  background-color: #f3f3f3;
}

tr:nth-child(even) {
  background-color: #a2cfec;
  color: #fff;
}

tr:nth-child(odd) {
  color: #a2cfec;
}

table tr:nth-child(odd) button {
  color: #a2cfec !important;
  background: #fff !important;
}
</style>
