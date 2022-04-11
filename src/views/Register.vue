<template>
  <div>
    <section class="breadcrumbs">
      <h1>REGISTER</h1>
      <p>
        <router-link to="/"><span>Home</span></router-link>
        <img src="../assets/right.svg" alt="" />
        <router-link to="/login"><span>Login</span></router-link>
        <img src="../assets/right.svg" alt="" />
        <span>Register</span>
      </p>
      <div>
        <hr>
      </div>
    </section>
    <section class="register-form">
      <div class="register-page">
        <h3>Register</h3>
        <p v-if="err" class = 'error-mgs'>{{err}}</p>
        <div class="register-container">
          <form @submit.prevent="registerAccount">
            <label for="email">Email</label>
            <input
              type="email"
              name="email"
              pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
              required
              placeholder="example@email.com"
              v-model="register.email"
            />
            <label for="name">Name</label>
            <input
              type="text"
              name="name"
              placeholder="Firstname Lastname"
              pattern="[a-zA-Z]{2,16}\s[a-zA-Z]{2,16}" required
              minlength="5"
              maxlength="33"
              v-model="register.name"
            />
            <label for="password">Password</label>
            <input
              type="password"
              name="password"
              pattern=".{8,}"
              required
              placeholder="Password 8 or more letters/symbols"
              v-model="register.password"
            />
            <label for="validation">Confirm password</label>
            <input
              type="password"
              name="validation"
              pattern=".{8,}"
              required
              placeholder="Re-type your password"
              v-model="validation.password"
            />

            <div class="check-box">
              <label><input type="checkbox" />By creating an account you agree to our</label>
              <a href="#"> conditions</a>
            </div>
            <button>Register</button>
          </form>
          <hr class="solid" />
          <div class="sign">
            <p>Already have an account?</p>
            <a
              href="#"
              @click="click"
            >Login here</a>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      register: {
        email: "",
        password: "",
        role: "",
        name: "",
        address: {
          city: "",
          street: "",
          zip: "",
        },
      },
      validation: {
        password: "",
      },
    };
  },

computed:{
  err(){
    return this.$store.state.errors 
  }
},

  methods: {
   async registerAccount() {
      try{
        if (
        this.register.email !== "" &&
        this.register.name !== "" &&
        this.register.password !== "" &&
        this.register.password === this.validation.password
      ) {
       await  this.$store.dispatch("signup", this.register)
        await  this.$router.push("/login");
        
        // Found issue here in prev version (issue: this.register.validation.password)
      }else if (this.register.password !== this.validation.password) {
        throw new Error("Password is not matching!");
      } else {
        throw new Error("Required info missing!");
      }
      }catch(error){
       await await this.$store.dispatch("catchErr", error);
        }
       
    },

    click() {
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped lang="scss">
.top {
  width: 100%;
  height: 80px;
  background-color: #aaa;
  // font-family: "Times New Roman", Times, serif;
  h1,
  p {
    display: flex;
    margin: 0;
    padding: 5px 2rem;
    color: white;
  }
  h1 {
    color: black;
  }
  a {
    text-decoration: none;
  }
}
.register-page{
  margin: 5rem 0 11rem 0;
  h3 {
    font-size: 2rem;
  }
  .error-mgs{
    color: red;
  }
}
.login-container {
  width: 400px;
  margin: auto;
  border-radius: 5px;
  padding: 20px;
}
label {
  display: flex;
}
input[type="text"],
select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
  background-color: #f5f5f5;
}
input[type="password"],
select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  // margin-bottom: 16px;
  resize: vertical;
  background-color: #f5f5f5;
}
a {
  display: flex;
  justify-content: flex-end;
}
button {
  width: 400px;
  height: 40px;
  margin: 2rem auto;
  background-color: #2091f9;
  border-radius: 5px;
  border: none;
  font-size: 1.2rem;
  color: white;
  cursor: pointer;
  &:hover {
    background-color: #45a049;
    transition: 0.5s;
  }
}
hr.solid {
  border-top: 1px solid #bbb;
  width: 400px;
}
.face-book {
  display: flex;
  justify-content: center;
  background-color: #2091f9;
  color: white;
  width: 400px;
  margin: auto;
  border-radius: 5px;
  cursor: pointer;
  h4 {
    margin: 1rem;
  }
}
.sign {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 400px;
  margin: auto;
  a {
    font-size: 1.2rem;
    margin: 1rem;
    text-decoration: none;
    font-weight: 900;
    color: #2091f9;
  }
}

.register-form {
  h3 {
    font-size: 2rem;
  }
}
.register-container {
  width: 400px;
  margin: auto;
  border-radius: 5px;
  padding: 20px;
}
label {
  display: flex;
}
input[type="text"],
input[type="email"],
select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  // margin-bottom: 16px;
  resize: vertical;
  background-color: #f5f5f5;
}
input[type="password"],
select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
  background-color: #f5f5f5;
}
a {
  display: flex;
  justify-content: flex-end;
}
button {
  width: 400px;
  height: 40px;
  margin: 2rem 0 auto;
  background-color: #2091f9;
  border-radius: 5px;
  border: none;
  font-size: 1.2rem;
  color: white;
  cursor: pointer;
  &:hover {
    background-color: #45a049;
    transition: 0.5s;
  }
}
.check-box {
  display: flex;
  width: 400px;
  margin: auto;
  a {
    color: #2091f9;
    text-decoration: none;
    // font-size: 1.2rem;
    font-weight: 900;
    margin-left: 10px;
  }
}
</style>