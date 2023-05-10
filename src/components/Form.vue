<template>
  <form @submit.prevent="createAcc">
    <div class="">
      <label>Email</label>
      <input type="email" v-model="email" />
      <small v-if="emailErrorMsg">{{ emailErrorMsg }}</small>
    </div>

    <div class="">
      <label>Password</label>
      <input type="password" v-model="password" />
      <small v-if="passwordErrorMsg">{{ passwordErrorMsg }}</small>
    </div>

    <div class="">
      <label>Roles:</label>
      <select name="" id="" v-model="developer">
        <option value="">Choose::</option>
        <option value="Web Developer">Web Developer</option>
        <option value="Web Designer">Web Designer</option>
        <option value="React Js Developer">React Js Developer</option>
      </select>
      <small v-if="roleErrorMsg">{{ roleErrorMsg }}</small>
    </div>

    <div class="">
      <label>Skills:</label>
      <input type="text" @keyup.alt="addSkill" v-model="skill" />
    </div>
    <div class="skill" v-for="skill in skills" :key="skill">
      <p>
        {{ skill }}
        <i class="fa-solid fa-xmark" @click="deleteSkill(skill)"></i>
      </p>
    </div>

    <div class="">
      <input type="checkbox" v-model="accept" />
      <label>Accept terms and conditions</label>
      <div class="">
        <small v-if="acceptErrorMsg">{{ acceptErrorMsg }}</small>
      </div>
    </div>

    <div class="align">
      <button class="create">Create</button>
    </div>
    <!-- <label for="">Choose Gender:</label>

            <input type="radio" value="Male" v-model="gender"/>
            <label for="">Male</label>

            <input type="radio" value="Female" v-model="gender"/>
            <label for="">Female</label> -->
    <!-- <div class="">
        <label for="">Choose Names:</label>
        <div class="">
            <input type="checkbox" value="kei" v-model="names"/>
            <label for="">Kei</label>
        </div>
        <div class="">
            <input type="checkbox" value="horikita" v-model="names"/>
            <label for="">Horikita</label>
        </div>
        <div class="">
            <input type="checkbox" value="oni" v-model="names"/>
            <label for="">Oni</label>
        </div>
        <div class="">
            <input type="checkbox" value="yuu" v-model="names"/>
            <label for="">Yuu</label>
        </div>
    </div> -->
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      developer: "",
      accept: false,
      names: [],
      gender: "",
      skill: "",
      skills: [],
      passwordErrorMsg: "",
      emailErrorMsg: "",
      acceptErrorMsg: "",
      roleErrorMsg: "",
      createId: 0,
      users: [],
      checkValidation: true,
    };
  },
  methods: {
    addSkill(e) {
      if (e.key == ",") {
        this.skills.push(this.skill);
        this.skill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((loopSkill) => {
        return loopSkill != skill;
      });
      // console.log(this.skills)
    },
    createAcc() {
        if (this.password == "" || this.password == null) {
          this.passwordErrorMsg = "You need to enter Password";
        } else if (this.password.length < 8) {
          this.passwordErrorMsg = "Password must be atleast 8 characters";
        }

        if (this.email == "" || this.email == null) {
          this.emailErrorMsg = "You need to enter Email address";
        }

        if (this.accept == false) {
          this.acceptErrorMsg = "You need to accept our terms and conditions";
        }

        if (this.developer == null || this.developer == "") {
          this.roleErrorMsg = "You need to choose roles";
        }

        
    },
  },
};
</script>

<style>
form {
  background-color: white;
  max-width: 420px;
  margin: 30px auto;
  border-radius: 10px;
  padding: 40px;
  text-align: left;
}
label {
  display: inline-block;
  color: #2c3e50;
  text-transform: uppercase;
  margin: 35px 0 15px;
  font-size: 0.6rem;
  font-weight: bold;
  letter-spacing: 1px;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #2c3e50;
  color: #2c3e50;
}
select {
  background-color: #add0f3;
  border: 1px solid #2c3e50;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.skill {
  display: inline-block;
}
.skill p {
  background-color: #2c3e50;
  color: white;
  padding: 5px;
  margin-left: 5px;
  text-align: center;
  border-radius: 5px;
}
.skill p i {
  color: red;
  margin-right: 5px;
  font-size: large;
  cursor: pointer;
}
.align {
  text-align: center;
  margin: 20px 0 0 0;
}
.create {
  background-color: blue;
  padding: 10px 20px;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
small {
  color: red;
}
</style>
