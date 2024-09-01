<template>
  <div class="login-container">
    <h2>Login</h2>
    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" v-model="username" id="username" required />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" v-model="password" id="password" required />
      </div>
      <div class="form-group">
        <button type="submit">Login</button>
      </div>
    </form>
  </div>
</template>
<script>
import apiClient from "@/services/api";

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async handleLogin() {
      try {
        const response = await apiClient.post("/auth/login", {
          username: this.username,
          password: this.password,
        });
        const token = response.data.token;
        localStorage.setItem("jwt", token);
        this.$router.push("/dashboard"); // redirect after successful login
      } catch (error) {
        console.log("Login failed", error);
        alert("Invalid username or password");
      }
    },
  },
};
</script>

<style scoped>
/* Add basic styling for the login form */
.login-container {
  width: 300px;
  margin: 50px auto;
}
.form-group {
  margin-bottom: 15px;
}
</style>