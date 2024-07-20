<template>
  <div class="w-full flex items-center justify-center gap-3">
    <v-card class="mx-auto my-12" max-width="374">
      <template slot="progress">
        <v-progress-linear color="deep-purple" height="10" indeterminate></v-progress-linear>
      </template>
      <v-img height="250"
        src="https://static.vecteezy.com/system/resources/previews/006/912/004/non_2x/secure-login-and-sign-up-concept-illustration-vector.jpg"></v-img>
      <v-card-title>User Login</v-card-title>
      <v-card-text class="w-full">
        <form @submit.prevent="login" class="">
          <v-text-field v-model="username" label="Username" placeholder="Username" type="text" outlined
            dense></v-text-field>
          <v-text-field v-model="password" label="Password" placeholder="Password" type="password" outlined
            dense></v-text-field>
          <v-btn type="submit" class="w-full" color="primary lighten-2 w-full" width="100%">
            Login
          </v-btn>
        </form>
      </v-card-text>
      <v-divider class="mt-4"></v-divider>
      <v-card-actions>
        <a href="/admin/login">for Admin login</a>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    login() {
      if (this.username === 'admin' && this.password === '123') {
        this.$router.push('/user/dashboard');
      } else {
        alert('Invalid credentials');
      }
    }
  }
};
</script>