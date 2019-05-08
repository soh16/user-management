<template>
  <div class="table-container">

      <div class="filter-container">
        <div class="filter-section">
          <div class="fliter-title">
            Filter
          <i class="fas fa-sort-down" :class=" { arrowUp: isActive }"></i></div>
          <label>Role:</label>
          <select v-model="selectedRole">
            <option value="All">All</option>
            <option value="Admin">Admin</option>
            <option value="Edit">Edit</option>
            <option value="Manage">Manage</option>
          </select>
          <label>Fascia:</label>
          <select v-model="selectedFascia">
            <option value="All">All</option>
            <option value="JDSPORTS">JDSPORTS</option>
            <option value="JDSPORTS_IE">JDSPORTS_IE</option>
            <option value="JDSPORTS_BE">JDSPORTS_BE</option>
          </select>
          <label>Services</label>
          <select v-model="selectedServices">
            <option value="All">All</option>
            <option value="Content Editor">Content Editor</option>
            <option value="Image">Image</option>
            <option value="Raffle">Raffle</option>
          </select>
        </div>
        <div class="search-box">
          <i class="fas fa-search"></i>
          <input type="text" v-model="search" placeholder="Search">
        </div>
      </div>

      <div>
      <table>
        <tr>
          <th>Username</th>
          <th>Role</th>
          <th>Fascia</th>
          <th>Services</th>
          <th>Actions</th>
        </tr>
        <tr v-for="(user, index) in matches" :key="index">
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
    </div>

    <!-- <div class="filter-container">
      <div class="fliter-title" @click="filterShow">
        Filter
        <i class="fas fa-caret-down" :class=" { arrowUp: isActive }"></i>
      </div>
      <div class="search-box">
        <i class="fas fa-search"></i>
        <input type="text" v-model="search" placeholder="Search">
      </div>
    </div> -->
<!--
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

    </div> -->

          <!-- <label>Role:</label>
          <select v-model="selectedRole">
            <option value="Admin">Admin</option>
            <option value="Edit">Edit</option>
            <option value="Manage">Manage</option>
          </select>

          <label>Fascia:</label>
          <select v-model="selectedFascia">
            <option value="JDSPORTS">JDSPORTS</option>
            <option value="JDSPORTS_IE">JDSPORTS_IE</option>
            <option value="JDSPORTS_BE">JDSPORTS_BE</option>
          </select>

          <label>Services</label>
          <select v-model="selectedServices">
            <option value="Content Editor">Content Editor</option>
            <option value="Image">Image</option>
            <option value="Raffle">Raffle</option>
          </select>
        </div> -->
<!--
        <div class="search-box">
          <i class="fas fa-search"></i>
          <input type="text" v-model="search" placeholder="Search">
        </div> -->

  </div>
</template>

<script>
export default {
  name: 'UsersTable',

   components: {
  },

  data() {
    return {
      isActive: false,
      search: '',
      selectedRole: '',
      selectedFascia: '',
      selectedServices: '',
      filteredResults: [],
      items: [{
        username: 'first.last@jdplc.com',
        role: 'Edit',
        fascias: 'JDSPORTS',
        services: 'Content Editor',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Manage',
        fascias: 'JDSPORTS',
        services: 'Image',
      },
      {
        username: 'ste.last@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS, JDSPORTS_IE, JDSPORTS_BE',
        services: 'Content Editor',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS_BE',
        services: 'Raffle',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Edit',
        fascias: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'ste.bloggs@jdplc.com',
        role: 'Manage',
        fascias: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'DELETE.ME@jdplc.com',
        role: 'Manage',
        fascias: 'JDSPORTS_BE',
        services: 'Raffle',
      },
      {
        username: 'DELETbjhbE.ME@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS',
        services: 'Content Editor',
      },
      {
        username: 'ikhnjkbjkbjkbjk.ME@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS',
        services: 'Content Editor',
      },
      {
        username: 'jkbjkbjkb.ME@jdplc.com',
        role: 'Admin',
        fascias: 'JDSPORTS_IE',
        services: 'Content Editor',
      }],
      label: "Role",
      filterValue: "role",
      current: "",
      selectFilters: [
        {
          label: 'Role',
          filterValue: 'role',
          current: '',
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
    }
  },

  computed: {
     matches() {

      let filterRole= this.selectedRole,
          filterFascia = this.selectedFascia,
          filterServices = this.selectedServices

          
			// if(filterRole === "All") {
      //   return item.role
      // }

      return this.items.filter(item => {
       let userList = item.username.toLowerCase().match(this.search.toLowerCase());
			
        if(filterRole && filterRole.length > 1){
          userList = item.role == filterRole
        }
        if(userList){
          if(filterFascia && filterFascia.length > 1){
            userList = item.fascia == filterFascia
          }
        }
        if(userList){
          if(filterServices && filterServices.length > 1){
            userList = item.services == filterServices
          }
        }
        return userList
      })

    },
  },

  methods: {
    // filterShow() {
    //   if (this.isActive) {
    //     this.isActive = false;
    //   } else {
    //     this.isActive = true;
    //   }
    // },
  }

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
    margin-bottom: 0;
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

  .filter-section select {
    border-radius: 20rem;
    font-size: 0.9rem;
    margin: 0 1rem;
    padding: 0 1rem;
    border: 1px solid #fff;
    color: #fff;
    background: #a2cfec;
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
    margin-top: 1rem;
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
