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

      <!-- <SelectFilter :dataToFilter="items" /> -->
      <UserTable />

      <div class="pages">
        <span>1</span>
        <span>2</span>
        <span>3</span>
      </div>
    </div>
  </main>
</template>

<script>
// import SelectFilter from '@/components/SelectFilter.vue';
import UserTable from '@/components/UserTable.vue';
export default {
  name: 'Users',

   components: {
    // SelectFilter,
    UserTable,
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
        services: 'Content Editor, Image, Email, Raffle',
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
        fascias: 'JDSPORTS, JDSPORTS_IE, JDSPORTS_BE',
        services: 'Content Editor, Image, Email, Raffle',
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
      },
      ]
    }
  },
  // computed: {
  //   matches() {
  //     // return this.items;


  //     // return this.search ? this.items.filter(item => {
  //     //     let match = false
  //     //     for (let key in item) {
  //     //       console.log(item[key]);
  //     //       if (item[key].toLowerCase().includes(this.search.toLowerCase())) {
  //     //         return true
  //     //       }
  //     //     }
  //     //   })
  //     //   : this.items
  //   },
  // },

  methods: {
    filterShow() {
       if(this.isActive){
         this.isActive = false;
       }else{
         this.isActive = true;
       }
    },

    filterByType(itemKey, currentValue) {
      return this.items.filter(item => {
        if (currentValue !== "") {
          return item[itemKey] === currentValue;
        }
        return item;
      });
    },
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=PT+Sans+Caption');
main {
  background: #a2cfec;
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

.active{
  display: flex!important;
}

.filter-section select {
  background-color: #a2cfec;
  border: 1px solid #fff;
  margin: 0 .5rem;
}

.filter-section {
  display: none;
  margin-right:  1rem;
}

.search_container i.fas.fa-caret-right {
   padding-left: .3rem;
   cursor: pointer;
   display: flex;
   align-items: center;
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
