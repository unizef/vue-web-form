<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <!-- Input Fields -->
      <label for="">Email:</label>
      <input type="email" required v-model.trim="email" />

      <label for="">Password:</label>
      <input type="password" required v-model="password" />
      <div class="msg">{{ passwordError }}</div>

      <!-- Select Boxes -->
      <label for="">Role:</label>
      <select name="" id="" v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <!-- Keyup Input Field -->
      <label>Skill:</label>
      <input type="text" v-model.trim="tempSkill" @keyup.ctrl="addSkill" />
      <div
        v-for="skill in skills"
        :key="skill"
        @click="deleteSkill(skill)"
        class="pill"
      >
        {{ skill }}
      </div>

      <!-- Check Boxes -->
      <div class="terms">
        <input type="checkbox" v-model="terms" required />
        <label>Accept terms and conditions</label>
      </div>

      <!-- Submit Form -->
      <div class="submit">
        <button>Create Account</button>
      </div>
    </form>
  </div>
</template>

<script>
import "../assets/styles/global.css";
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
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
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit(e) {
      console.log(e);
      // validate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 chars long";
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

.msg {
  margin-top: 5px;
  color: firebrick;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background: dodgerblue;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

.submit {
  text-align: center;
}
</style>
