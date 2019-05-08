<template>
  <main>    
    <div class="users-list">
      <div class="top-bar">
        <i class="far fa-bell"></i>
        <div class="username">
          <i class="fas fa-user-circle"></i>
          <p>Joe Bloggs</p>
        </div>
      </div>
      <header>
        <h1 class="users-list__header">User Management</h1>
        <button id="add" class="users-list__buttons">
          <i class="fas fa-user-plus"></i>
        </button>
      </header>

      <UserTable />
      <!-- <div class="search_container">
        <div class="filter-section">
          <div class="filter">Filter<i class="fas fa-sort-down"></i></div>
          <label>Role:</label>
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
        </div>
        <div class="search-box">
          <i class="fas fa-search"></i>
          <input type="text" v-model="search" placeholder="Search">
        </div>
      </div> -->

      <!-- <table>
        <tr>
          <th>Username</th>
          <th>Role</th>
          <th>Fascia</th>
          <th>Services</th>
          <th>Actions</th>
        </tr>
        <tr v-for="(item, index) in matches" :key="index">
          <td>{{ item.username }}</td>
          <td>{{ item.role }}</td>
          <td>{{ item.fascia }}</td>
          <td>{{ item.services }}</td>
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
      </table> -->

      
    <!-- <h1 class="title">Select Filter</h1>
    <SelectFilter :dataToFilter="selectFilterData" /> -->

      <div class="pages">
        <span>1</span>
        <span>2</span>
        <span>3</span>
      </div>
    </div>
  </main>
</template>

<script>
import UserTable from '@/components/UserTable.vue';
import SelectFilter from '@/components/SelectFilter.vue';

export default {
  name: 'Users',
  
  components: {
    UserTable,
    SelectFilter,
  },

  data() {
    return {
      search: '',
      selectedRole: '',
      selectedFascia: '',
      selectedServices: '',
      items: [{
        username: 'first.last@jdplc.com',
        role: 'Edit',
        fascia: 'JDSPORTS',
        services: 'Content Editor',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Manage',
        fascia: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'ste.last@jdplc.com',
        role: 'Admin',
        fascia: 'JDSPORTS, JDSPORTS_IE, JDSPORTS_BE',
        services: 'Content Editor',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Admin',
        fascia: 'JDSPORTS, JDSPORTS_IE, JDSPORTS_BE',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Edit',
        fascia: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'ste.bloggs@jdplc.com',
        role: 'Manage',
        fascia: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      },
      {
        username: 'joe.bloggs@jdplc.com',
        role: 'Admin',
        fascia: 'JDSPORTS',
        services: 'Content Editor, Image, Email, Raffle',
      }]
    }
  },
  computed: {
    matches() {
      let filterRole= this.selectedRole,
          filterFascia = this.selectedFascia,
          filterServices = this.selectedServices
      return this.items.filter(item => {
        let filtered = true
        if(filterRole && filterRole.length > 0){
          filtered = item.role == filterRole
        }
        if(filtered){
          if(filterFascia && filterFascia.length > 0){
            filtered = item.fascia == filterFascia
          }
        }
        if(filtered){
          if(filterServices && filterServices.length > 0){
            filtered = item.services == filterServices
          }
        }
        return filtered
      })

      return this.search ? this.items.filter(item => {
          for (let key in item) {
            if (item[key].toLowerCase().includes(this.search.toLowerCase())) {
              return true
            }
          }
        })
        : this.items
    }
  }

};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=PT+Sans+Caption');
main {
    background: #7cc5ef;
}
.top-bar {
  display: flex;
  justify-content: flex-end;
  border-bottom: solid 0.5px #f3f3f3;
  padding-bottom: 1.5rem;
}

.top-bar .username {
  display: flex;
}

.top-bar i.far.fa-bell {
  color: #fff;
  font-size: 30px;
  display: flex;
  align-items: center;
  margin-right: 1.5rem;
}

.top-bar i.fas.fa-user-circle {
  color: #f3f3f3;
  background: #00b5ff;
  font-size: 24px;
  justify-content: center;
  display: flex;
  align-items: center;
  padding: .3rem .5rem;
}

.top-bar p {
  font-size: 19px;
  font-weight: bold;
  line-height: 1.26;
  color: #595959;
  background: #fff;
  padding: .5rem 1.5rem .5rem 1rem;
  margin: 0;
}

.buttons-container {
  display: flex;
  justify-content: center;
}

.users-list {
  width: 100%;
  height: 100%;
  position: relative;
}

.users-list header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.users-list__header {
  display: block;
  margin: 2rem 0;
  color: #fff;
  font-size: 39px;
}

.search_container {
  display: flex;
  padding: 1rem 0 2rem 0;
  color: #fff;
}

.search_container .filter {
  display: flex;
  margin-right: 1rem;
  cursor: pointer;
}

.filter-section select {
  background-color: #a2cfec;
  border: 1px solid #fff;
  margin: 0 .5rem;
}

.filter-section {
  display: flex;
  margin-right:  1rem;
}

.search_container i.fas.fa-sort-down {
   padding-left: .3rem;
   cursor: pointer;
}

.search_container .search-box ::placeholder {
  color: #fff;
  font-size: 16px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  background-color: #fff;
}

td, th {
  text-align: center;
  width: 20%;
  padding: 10px;
  font-weight: 600;
}

th {
  color:#a2cfec;
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
  color: #a2cfec!important;
  background:#fff!important;
}


.users-list__buttons {
  color: #f3f3f3;
  margin: 0 .2rem;
  border-radius: 50px;
}

.users-list__buttons .fas {
  font-size: 18px;
}

.buttons {
  width:  100%;
  display:  flex;
  justify-content: flex-end;
  /* margin-bottom:  1.5rem; */
}

.buttons button {
  margin: 0 1rem;
  border: none;
}

#add {
  background-color: #fff;
  color: #595959;
  padding: .6rem;
  border-radius: 50px;

}

#delete {
  background-color: #a2cfec;
}

#edit {
  background-color: #a2cfec;
  color: #fff;
  margin-right: 0;
}

.pages {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-top: 1.5rem;
}

.pages span {
    background:  #f3f3f3;
    color: #a2cfec;
    padding: .5rem 1rem;
    margin: 0 .3rem;
    border-radius: 3px;
}

</style>
