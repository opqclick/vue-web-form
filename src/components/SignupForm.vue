<template>
  <div class="signup-form">
    <form @submit.prevent="handleSubmit" class="">
      <h2>Register</h2>
      <p class="hint-text">
        Create your account. It's free and only takes a minute.
      </p>

      <div class="form-group">
        <label class="my-1 mr-2" for="email">Email</label>
        <input
          type="email"
          class="form-control"
          name="email"
          placeholder="Email"
          required="required"
          v-model="email"
        />
      </div>
      <div class="form-group">
        <label class="my-1 mr-2" for="password">Password</label>
        <input
          type="password"
          class="form-control"
          name="password"
          placeholder="Password"
          required="required"
          v-model="password"
        />
        <div v-if="passwordError" class="text-danger">
          <span class="">{{ passwordError }}</span>
        </div>
      </div>
      <div class="form-group">
        <label class="my-1 mr-2" for="role">Role</label>
        <select class="custom-select my-1 mr-sm-2" id="role" v-model="role">
          <option selected>Select...</option>
          <option value="web_designer">Web Designer</option>
          <option value="web_developer">Web Developer</option>
        </select>
      </div>
      <div class="form-group">
        <label class="my-1 mr-2" for="password">Select skills</label>
        <input
          type="text"
          class="form-control"
          v-model="tempSkill"
          placeholder="Enter your skill and press enter"
          @keyup="addSkill"
        />
        <ul v-for="skill in skills" :key="skill" class="list-group">
          <li class="list-group-item">
            <span class="badge badge-success">{{ skill }}</span>
            <button
              class="btn-danger btn-xs pull-right remove-item"
              @click="deleteSkill(skill)"
            >
              <i class="fa fa-remove"></i>
            </button>
          </li>
        </ul>
      </div>
      <div class="form-group">
        <label class="form-check-label">
          <input type="checkbox" required="required" v-model="terms" /> I accept
          the <a href="#">Terms of Use</a> &amp;
          <a href="#">Privacy Policy</a>
        </label>
      </div>
      <hr />
      <div class="form-group">
        <button type="submit" class="btn btn-success btn-lg btn-block">
          Register Now
        </button>
      </div>
    </form>
    <div class="text-center">
      Already have an account? <a href="#">Sign in</a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "web_developer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        console.log(this.skills);
        let input = this.tempSkill.replace(",", "").toUpperCase();
        if (!this.skills.includes(input)) {
          this.skills.push(input);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill != item;
      });
    },
    handleSubmit() {
      //validate password
      this.passwordError =
        this.password.length > 5 ? "" : "Password must be a 6 chars long";
      if (!this.passwordError) {
        if (typeof Storage !== "undefined") {
          // Code for localStorage/sessionStorage.
          localStorage.setItem("email", this.email);
          localStorage.setItem("password", this.password);
          localStorage.setItem("role", this.role);
          localStorage.setItem("skills", this.skills);
          localStorage.setItem("terms", this.terms);
          console.log(localStorage);
        } else {
          // Sorry! No Web Storage support..
        }
      }
    },
  },
};
</script>

<style></style>
