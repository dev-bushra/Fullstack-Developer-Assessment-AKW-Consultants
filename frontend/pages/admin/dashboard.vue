<template>
    <v-row class="">
      <v-col cols="12" class="text-center mt-5" align-center>
      <h1>Admin Dashboard</h1>
      <a href="/admin/login">LogOut</a>
    </v-col>
    <v-col cols="12" class="text-center" align-center>
      <v-row>
        <v-col cols="12" v-for="user in users" :key="user.username" class="flex items-center">
          <v-divider class="mb-5" max-width="50%"></v-divider>
          <div class="list-wrapper">
            <b class="mr-5 text-3xl">{{ user.username }}</b>
            <label>
              <input type="checkbox" v-model="user.permissions.canEdit" class="mr-2" />
              <span>Can Edit</span>
            </label>
            <label>
              <input type="checkbox" v-model="user.permissions.canDelete" class="mr-2" />
              <span>Can Delete</span>
            </label>
            <label>
              <input type="checkbox" v-model="user.permissions.canView" class="mr-2" />
              <span>Can View</span>
            </label>
            <label>
              <input type="checkbox" v-model="user.permissions.canViewAll" class="mr-2" />
              <span>Can View All</span>
            </label>
          </div>
          <v-divider class="mt-5" max-width="50%"></v-divider>
        </v-col>
      </v-row>
    </v-col>
    </v-row>
  </template>
  
  <script>
  export default {
    data() {
      return {
        users: [
          {
            username: 'user1',
            permissions: {
              canEdit: true,
              canDelete: true,
              canView: true,
              canViewAll: false
            }
          },
          {
            username: 'user2',
            permissions: {
              canEdit: false,
              canDelete: false,
              canView: true,
              canViewAll: true
            }
          }
        ]
      };
    },
    watch: {
      users: {
        handler(val) {
          // Save the updated permissions to local storage or any persistence layer
          localStorage.setItem('users', JSON.stringify(val));
        },
        deep: true
      }
    },
    mounted() {
      const storedUsers = localStorage.getItem('users');
      if (storedUsers) {
        this.users = JSON.parse(storedUsers);
      }
    }
  };
  </script>
  
  <style lang="scss" scoped>
  h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
}
.list-wrapper{
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 3rem;
  padding-left: 3rem;
}
  </style>
  