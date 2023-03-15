<script>
export default {
  name: 'Home',
  data() {
    return {
      user: {}
    }
  },
  methods: {
    async authorize() {
      try {
        const response = await this.axios.post('/api/authorize')
        this.user = response.data
      } catch (error) {
        // alert('Error')
        console.log('Error on Home.vue > authorize()', error.response.data.message)
        this.$router.push('/login')
      }
    },
    async doLogout() {
      try {
        const response = await this.axios.post('/api/logout')
        this.$router.push('/login')
      } catch (error) {
        // alert('Error')
        console.log('Error on Home.vue > doLogout()', error.respone.data.message)
      }
    }
  },
  async mounted() {
    await this.authorize()
  }
}
</script>
<template>
  <div class="row justify-content-center align-items-center m-0 p-0">
    <main class="col-10 col-md-5 col-lg-3 shadow main p-5">
      <h2>Welcome</h2>
      <h1>{{ user.username }}, <span class="role">{{ user.role }}</span></h1>
      <button class="btn w-100 logout mt-3" @click="doLogout">Logout</button>
    </main>
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

main {
  background: #FCFEFB;
  border-radius: 12px;
  box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 5px 4px 12px 0px rgba(0, 0, 0, 0.75);
}


.logout {
  background: linear-gradient(90deg, rgba(103, 10, 104, 1) 0%, rgba(216, 23, 43, 1) 100%);
  color: #FFF;
  font-weight: bold;
  text-transform: uppercase;
}

.role {
  color: #AAA;
  font-weight: 600;
  font-size: 1.5rem;
  text-transform: uppercase;
}
</style>
