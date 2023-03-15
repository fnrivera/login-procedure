<script>
export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
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
    async doLogin() {
      try {
        if (!this.validateEmail()) {
          // alert('Invalid email')
          this.error = "Invalid Email";
          return
        }
        const response = await this.axios.post('/api/login', { email: this.email, password: this.password })
        this.$router.push('/')
      } catch (error) {
        // alert('Error')
        this.error = 'Invalid User Credentials';
        console.log('Error on Login.vue > doLogin()', error.response.data.message)
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
      <h1 class="text-center mt-2">Login</h1>
      <div class="d-flex flex-column">
        <div class="btn-group my-5">
          <a class="btn text-white current" href="/login">Login</a>
          <a class="btn" href="/register">Register</a>
        </div>
      </div>
      <div class="">
        <div class="form-group mb-3">
          <input placeholder="Email" class="form-control py-2" v-model="email" type="text">
        </div>
        <div class="form-group mb-3">
          <input placeholder="Password" class="form-control py-2 mb-1" v-model="password" type="password">
        </div>
        <small v-if="error" class="text-danger d-block my-2">{{ error }}</small>
      </div>
      <div class="d-flex flex-column align-items-stretch">
        <button class="btn login" @click="doLogin">Login</button>
        <span class="d-block align-self-center mt-4">Don't have an account? <a href="/register"
            class="register-link">Register
            now</a></span>
      </div>
    </form>
  </div>
</template>
<style scoped>
h1 {
  font-weight: bold;
}

a,
small {
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
  background: linear-gradient(90deg, rgba(10, 53, 104, 1) 0%, rgba(23, 110, 216, 1) 100%);
  font-weight: bold;
}

.btn-group {
  border: 1px solid #CCC;
}

.login {
  background: linear-gradient(270deg, rgba(10, 53, 104, 1) 0%, rgba(23, 110, 216, 1) 100%);
  font-weight: bold;
  color: #FFF;
}

.forgot-password {
  text-decoration: none;
}

.register-link {
  text-decoration: none;
}
</style>
