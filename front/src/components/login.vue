<template>
  <Layout>
    <div class="main-wrapper">
      <div class="form-wrap">
        <div class="nammm">
          <h2>SIGN IN </h2>
        </div>
        <form class="double-wrap" @submit.prevent="register">
          <div class="inp-wrap">
            <label for="inp3">E-mail</label>
            <input id="inp3" v-model="formData.email" type="email" required>
            <p v-if="errors.email.length">{{ errors.email }}</p>
            <label for="inp4">Password"</label>
            <input id="inp4" required v-model="formData.password" :type="show2 ? 'text' : 'password'">
            <p v-if="errors.password.length">{{ errors.password }}</p>
          </div>
          <div class="show">
            <input @change="show2 = !show2" class="chinp" type="checkbox">
            <label>Show password</label>
          </div>
          <div class="btn-wrap">
            <button class="btn1">sign in</button>
            <div class="exx">
              <button class="btn2"> <img src="../assets/google-icon.svg" alt="logo of google "> Continue with
                google</button>
            </div>
          </div>
          <div class="rout">
            <router-link class="okk" to="/input">SIGN UP </router-link>
          </div>
        </form>
      </div>
    </div>
  </Layout>
</template>

<script>
import Layout from "@/layout/Layout.vue";

export default {
  components: {Layout},
  data() {
    return {
      show2: false,
      formData: {
        email: '',
        password: '',
        returnSecureToken: true
      },
      errors: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    async register() {
      console.log(this.formData)
      const URL = `http://localhost:8000/users/sessions`
      const OPTIONS = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.formData)
      }
      const response = await fetch(URL, OPTIONS)
      const data = await response.json()
      if (response.ok) {
        localStorage.setItem('user', data)
        this.$router.push({ path: '/home' })
      } else {
        if (data.error === "Username not found"){
          this.errors.email = "Username not found"
        }else{
          this.errors.password = "Passsword is wrong"
        }
        // switch (data.errors.email.message) {
        //   case 'INVALID_EMAIL':
        //     this.errors.email = 'Неверный email'
        //     break
        //   case 'EMAIL_EXISTS':
        //     this.errors.email = 'Такой email уже есть'
        //     break
        //   case 'WEAK_PASSWORD : Password should be at least 6 characters':
        //     this.errors.password = 'Пароль должен превышать 6 символов'
        //     break
        //   default:
        //     this.$notify({
        //       title: data.error.message,
        //       type: 'error'
        //     });
        // }
      }
    }
  }
}
</script>

<style scoped>
form {
  width: 100%;
}

.okk {
  position: relative;
}

.okk::before {
  content: '';
  position: absolute;
  top: -2px;
  left: 0;
  right: 0;
  height: 2px;
  background-color: #985ACE;
  transform-origin: bottom right;
  transform: scaleX(0);
  transition: transform 0.5s ease;
}

.double-wrap {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.okk:hover::before {
  transform-origin: bottom left;
  transform: scaleX(1);
}

.rout a {
  text-decoration: none;
  color: black;
  text-transform: uppercase;
  font-family: "Gill Sans", sans-serif;
}

.rout {
  padding-top: 10px;
}

.exx {
  width: 100%;
}

.btn-wrap {
  width: 70%;
  border-bottom: 1px solid black;
  margin: 15px 0;
}

.btn2 {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  background: none;
  border: 1px solid #985ACE;
}

.btn1 {
  background: #985ACE;
  color: var(--vt-c-black);
  text-transform: uppercase;
  font-family: "Gill Sans", sans-serif;
  font-weight: 350;
  border-bottom: 1px solid black;
  border: 1px solid #985ACE;
}

.btn2 img {
  width: 20px;
}

.btn1,
.btn2 {
  /* border: none ; */
  width: 100%;
  padding: 10px 0;
  margin-bottom: 10px;
  border-radius: 4px;
  background: var(--vt-c-black-mute);
  color: white;
}

.inp-wrap input {
  height: 32px;
  padding: 0 10px;
  border: none;
  background: #F8F1FF;
  margin-bottom: 10px;
  border-radius: 6px;
}

.inp-wrap {
  display: flex;
  flex-direction: column;
  width: 70%;
}
.inp-wrap p{
  color: red;
}
.main-wrapper {
  background: var(--vt-c-black);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-wrap {
  background: white;
  height: 55%;
  width: 30%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  border-radius: 20px;
  -webkit-box-shadow: 29px -31px 87px 0px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 29px -31px 87px 0px rgba(34, 60, 80, 0.2);
  box-shadow: 29px -31px 87px 0px rgba(34, 60, 80, 0.2);
}

label {
  color: rgba(0, 0, 0, 0.567);
}

.nammm {
  padding: 30px 0 25px 0;
}

.nammm h2 {
  text-transform: uppercase;
  font-family: "Gill Sans", sans-serif;
  font-weight: 600;
  color: var(--vt-c-black);

}</style>
