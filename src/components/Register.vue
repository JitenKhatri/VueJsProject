<template>
  <div class="register-container">
    <h2>Register</h2>
    <form @submit.prevent="handleRegister">
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" v-model="username" id="username" required />
      </div>

      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" v-model="email" id="email" required />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" v-model="password" id="password" required />
      </div>

      <div class="form-group">
        <label for="confirmPassword">Confirm Password</label>
        <input
          type="password"
          v-model="confirmPassword"
          id="confirmPassword"
          required
        />
      </div>

      <div class="form-group">
        <label for="phone">Phone Number</label>
        <input type="tel" v-model="phone" id="phone" required />
      </div>

      <div class="form-group">
        <label for="storeLocation">Store Location</label>
        <input
          type="text"
          v-model="storeLocation"
          id="storeLocation"
          required
        />
      </div>

      <div class="form-group">
        <button type="submit">Register</button>
      </div>
    </form>
  </div>
</template>
  
  <script>
import apiClient from "../services/api";

export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
      confirmPassword: "",
      phone: "",
      storeLocation: "",
    };
  },
  methods: {
    async handleRegister() {
      if (this.password !== this.confirmPassword) {
        alert("Passwords do not match");
        return;
      }

      try {
        await apiClient.post("/auth/register", {
          username: this.username,
          email: this.email,
          password: this.password,
          phone: this.phone,
          storeLocation: this.storeLocation,
        });
        this.$router.push("/login"); // Redirect after successful registration
      } catch (error) {
        console.error("Registration failed", error);
        alert("Registration failed");
      }
    },
  },
};
</script>
  
  <style scoped>
/* Add basic styling for the registration form */
.register-container {
  width: 400px;
  margin: 50px auto;
}
.form-group {
  margin-bottom: 15px;
}
</style>