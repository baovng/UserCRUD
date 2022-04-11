<template>
    <div class="container">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">User Management</h5>
          <button type="button" class="btn btn-success" @click="showUsers()">
            Show All Users
          </button>
          <AddUserBtn @addUser="addUser" />
        </div>
      </div>
      <table class="table" id="userTable" :key="users.length">
        <thead>
          <tr>
            <th scope="col">Index</th>
            <th scope="col">Name</th>
            <th scope="col">isActive</th>
            <th scope="col">Salary</th>
            <th scope="col">Company</th>
            <th scope="col">Operations</th>
          </tr>
        </thead>
        <tbody id="userTableBody">
          <UserItem
           v-for="(user, index) in users"
           :key="index"
           :user="user"
           @delete="deleteUser(index)"
           @update="s => updateSalary(s, index)"
          />
        </tbody>
      </table>
    </div>
</template>

<script>
import users from './data/users.json'

import AddUserBtn from './components/AddUserBtn.vue'
import UserItem from './components/UserItem.vue'


export default {
  components: {
    AddUserBtn,
    UserItem
  },
  data: () => ({
    users: [],
    lastIndex: users.length + 1
  }),
  methods: {
    showUsers(){
      this.users = users
    },
    deleteUser(index){
      this.users.splice(index, 1)
    },
    updateSalary(salary, index){
      this.users[index].salary = salary
    },
    addUser(data){
      this.showUsers()
      this.users.push({
        ...data,
        index: this.generateUserIndex(),
        isActive: false,
        _id: this.generateUserId()
      })
    },
    generateUserId() {
      let timestamp = ((new Date().getTime() / 1000) | 0).toString(16);
      return (
        timestamp +
        'xxxxxxxxxxxxxxxx'
          .replace(/[x]/g, function () {
            return ((Math.random() * 16) | 0).toString(16);
          })
          .toLowerCase()
      )
    },
    generateUserIndex() {
      return this.lastIndex++
    }
  }
}
</script>

<style>
button {
  margin-right: 10px;
}

.card {
  margin-top: 10px;
}
</style>
