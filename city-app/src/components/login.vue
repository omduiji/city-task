<template>
  <form>
    <h1>Welcome to cities app, please login</h1>
    <div class="input-wrapper">
      <label for="email">Email:</label>
      <input type="email" name="email" v-model="userData.Email" required>
    </div>
    <div class="input-wrapper">
      <label for="userPassword">Password:</label>
      <input type="password" name="userPassword" v-model="userData.Password" required>
    </div>
    <button @click.prevent="submitForm(userData)" :disabled="(userData.Email == '') || (userData.Password == '')" >Submit</button>
    <div class="errorDiv" v-if="errorDiv">
      <p>{{errorMsg}}</p>
    </div>
  </form>
</template>

<script>
export default {
  name: 'login',
  data() {
    return {
      userData: {
        Email: null,
        Password: null
      },
      errorMsg: '',
      errorDiv: false
    }
  },
  methods: {
    submitForm(credientials) {
      //small validation
      this.errorDiv = false
      if(Object.values(credientials).length < 2) {
        this.errorMsg = "Please fill all form fields"
        this.errorDiv = true
        return
      }
      this.loginRequest(credientials)
    },
    async loginRequest(credientials) {
      let req = await fetch('https://taskfrontendapi.azurewebsites.net/api/user/login', {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(credientials)
      })
      if(req.status === 200) {
        
      }
      let res = await req.json()
      console.log(res, 'ss')
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
form {
  border: 1px solid #ccc;
  padding: 1em .75em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
}
h1 {
  font-size: 1rem;
  color: rgb(87, 86, 86);
}

.input-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: .5em .25em;
}


.input-wrapper label {
  max-width: 30ch;
  min-width: 10ch;
  color: rgb(87, 86, 86);
}

.input-wrapper input {
  flex-grow: 1;
  padding: .5em .25em;
  outline: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  color: rgb(87, 86, 86);
}

.input-wrapper input:focus {
  
  outline: none;
  border-color:rgb(87, 86, 86) ;
}

form button {
  outline: none;
  padding: .5em .75em;
  background: transparent;
  border: 1px solid #ccc;
  color: rgb(87, 86, 86);
  border-radius: 4px;
  cursor: pointer;
  transition: 450ms all ease-out;

}

form button:hover {
  background-color: rgb(87, 86, 86);
  color: white;
}

form button:disabled {
  cursor: not-allowed;

}

.errorDiv {
  padding: .5em 1em;
  border: 2px solid rgb(187, 88, 88);
  color: white;
}
</style>
