<template class="wrapper">
  <div class="w-full flex items-center justify-center gap-3">
    <v-card class="mx-auto my-12" max-width="374">
      <template slot="progress">
        <v-progress-linear color="deep-purple" height="10" indeterminate></v-progress-linear>
      </template>
      <v-img height="250"
        src="https://static.vecteezy.com/system/resources/thumbnails/003/689/228/small_2x/online-registration-or-sign-up-login-for-account-on-smartphone-app-user-interface-with-secure-password-mobile-application-for-ui-web-banner-access-cartoon-people-illustration-vector.jpg"></v-img>
      <v-card-title>Admin Login</v-card-title>
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
        <a href="/user/login">for User login</a>
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
        this.$router.push('/admin/dashboard');
      } else {
        alert('Invalid credentials');
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  background-color: #dbdbdb;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  gap: 1rem;
}

.submit {
  background-color: #ff0000;
  padding: 4rem;
  color: #000000;
}
</style>