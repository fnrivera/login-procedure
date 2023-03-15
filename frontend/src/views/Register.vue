<script>
export default {
  name: 'Register',
  data() {
    return {
      email: '',
      password: '',
      role: '',
      error: ''
    }
  },
  methods: {
    async authorize() {
      try {
        const response = await this.axios.post('/api/authorize')
        this.$router.push('/')
      } catch (error) {
        // user is logged out, nothing
      }
    },
    async doRegister() {
      try {
        if (!this.validateEmail()) {
          // alert('Invalid email')
          this.error = 'Invalid Email'
          return
        }
        const response = await this.axios.post('/api/register', { email: this.email, password: this.password, role: this.role })
        this.$router.push('/')
      } catch (error) {
        // alert(error.response.data.message)
        this.error = 'Error While Registering'
        console.log('Error on Register.vue > doRegister()', error.response.data.message)
      }
    },
    validateEmail() {
      return (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.email))
    }
  },
  async mounted() {
    await this.authorize()
  }
}
</script>
<template>
  <div class="row justify-content-center align-items-center m-0 p-0">
    <form class="col-10 col-md-5 col-lg-3 shadow form p-4" @submit.prevent>
      <h1 class="text-center mt-2">Register</h1>
      <div class="d-flex flex-column">
        <div class="btn-group my-5">
          <a class="btn" href="/login">Login</a>
          <a class="btn text-white current" href="/register">Register</a>
        </div>
      </div>
      <div class="">
        <div class="form-group mb-3">
          <input placeholder="Email" class="form-control py-2" v-model="email" type="text">
        </div>
        <div class="form-group mb-3">
          <input placeholder="Password" class="form-control py-2" v-model="password" type="password">
        </div>
        <div class="form-group mb-3">
          <select class="form-select py-2" v-model="role">
            <option value="" selected disabled>--Select Role--</option>
            <option value="role1">Admin</option>
            <option value="role2">Student</option>
            <option value="role3">Faculty</option>
            <option value="role4">Staff</option>
          </select>
        </div>
        <small v-if="error" class="text-danger d-block mt-3">{{ error }}</small>
      </div>
      <div class="d-flex flex-column align-items-stretch">
        <button class="btn login" @click="doRegister">Register</button>
        <span class="d-block align-self-center mt-4">Already have an account? <a href="/login" class="login-link">Login Now</a></span>
      </div>
    </form>
  </div>
</template>

<style scoped>
h1 {
  font-weight: bold;
}

a, small {
  font-weight: 600;
}

.form {
  background: #FCFEFB;
  height: 60%;
  border-radius: 12px;
  box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
}

.current {
  background: rgb(10, 53, 104);
  background: linear-gradient(270deg, rgba(10, 53, 104, 1) 0%, rgba(23, 110, 216, 1) 100%);
  font-weight: bold;
}

.btn-group {
  border: 1px solid #CCC;
}

.login {
  background: linear-gradient(90deg, rgba(10, 53, 104, 1) 0%, rgba(23, 110, 216, 1) 100%);
  font-weight: bold;
  color: #FFF;
}

.login-link {
  text-decoration: none;
}
</style>
