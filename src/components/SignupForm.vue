<template>
  <div>
    <form>
      <!-- Input Fields -->
      <label for="">Email:</label>
      <input type="email" required v-model="email" />

      <label for="">Password:</label>
      <input type="password" required v-model="password" />

      <!-- Select Boxes -->
      <label for="">Role:</label>
      <select name="" id="" v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <!-- Keyup Input Field -->
      <label>Skill:</label>
      <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill" />
      <div v-for="skill in skills" :key="skill" class="pill">
        {{ skill }}
      </div>

      <!-- Check Boxes -->
      <div class="terms">
        <input type="checkbox" v-model="terms" required />
        <label>Accept terms and conditions</label>
      </div>
    </form>

    <p>Your Email: {{ email }}</p>
    <p>Your Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms: {{ terms }}</p>
    <p>Names: {{ names }}</p>
    <p>Skills: {{ skills }}</p>
  </div>
</template>

<script>
import "../assets/styles/global.css";
export default {
  data() {
    return {
      email: "",
      password: "secred123",
      role: "",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," || (e.key === ";" && this.tempSkill)) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 3px;
}
</style>
