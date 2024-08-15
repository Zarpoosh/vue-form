<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <!-- ------------------------inputs------------------------------- -->
      <label for="email">email</label>
      <input type="email" required v-model="email" />
      <label for="password">password</label>
      <input type="password" required v-model="password" />
      <p class="err" v-if="passwordEror">{{ passwordEror }}</p>
      <!---------------------------- option----------------------------- -->
      <select v-model="role">
        <option value="developer">web developer</option>
        <option value="designer">web designer</option>
      </select>
      <!-- --------------------------skills------------------------------  -->
      <label>skills : </label>
      <input type="text" v-model="tempskills" @keyup.alt="addskill" />

      <div class="pill" v-for="skill in skills" :key="skill">
        <span @click="removeskill(skill)">{{ skill }}</span>
      </div>
      <!-- ---------------------checkbox------------------------------------ -->
      <div class="terms">
        <input type="checkbox" v-model="terms" required />
        <label>Accept trm & conditions </label>
      </div>
      <div class="terms">
        <input type="checkbox" v-model="names" value="minoo" required />
        <label>minoo</label>
      </div>
      <div class="terms">
        <input type="checkbox" v-model="names" value="amirmehdi" required />
        <label>amirmehdi </label>
      </div>
      <div class="terms">
        <input type="checkbox" v-model="names" value="kurosh" required />
        <label>kurosh </label>
      </div>

      <div class="submit">
        <button>create an account</button>
      </div>
    </form>
    <div class="result">
      <p>email : {{ email }}</p>
      <p>password : {{ password }}</p>
      <p>role : {{ role }}</p>
      <p>terms :{{ terms }}</p>
      <p>names: {{ names }}</p>
      <p>skills : {{ skills }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      names: [],
      tempskills: "",
      skills: [],
      passwordEror: "",
    };
  },
  methods: {
    addskill(e) {
      if (e.key === "," && this.tempskills) {
        if (!this.skills.includes(this.tempskills)) {
          this.skills.push(this.tempskills);
        }
        this.tempskills = "";
      }
    },
    removeskill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill != item;
      });
    },
    handleSubmit() {
      // console.log("form submit")
      if (this.password.length > 5) {
        this.passwordEror = "";
      } else {
        this.passwordEror = "password is not than more than 5 chars";
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
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  margin: 2px;
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #bbb;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
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
  background: rgb(22, 253, 176);
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: rgb(63, 63, 63);
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.err {
  color: red;
  margin-top: 10px;
  font-size: 0.8rem;
  font-weight: bold;
}
</style>
