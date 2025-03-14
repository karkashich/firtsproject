<template>
  <div className="form">
    <input type="text" v-model="userName" placeholder="Логин">
    <input type="password" v-model="userPass" placeholder="Пароль">
    <input type="email" v-model="userEmail" placeholder="Email">
    <p className="error">{{ error }}</p>
    <button @click="sendData()">Отправить</button>
    
    <div v-if="users.length == 0" className="user">
      <h3>Пользователей пока нет</h3>
    </div>
    <div v-else-if="users.length == 1" className="user">
      <h3>Всего один пользователь</h3>
    </div>
    <div v-else className="user">
      <h3>В базе {{ users.length }} пользовател(ей/я)</h3>
    </div>
    
    <div className="user" v-for="(el, index) in users" :key="index">
      <h3>{{ el.name }}</h3>
      <p>{{ el.email }} - <b>{{ el.pass }}</b></p>

    </div>
  </div>
</template>

<script>
 export default{
    data(){
      return {
          users: [],
          error: '',
          userName: '',
          userPass: '',
          userEmail: '',
      }
    },
    methods:{
        sendData(){
            if(this.userName == '') {
              this.error = 'Имя не введено';
              return;
            } else if(this.userPass == '') {
              this.error = 'Пароль не задан';
              return;
            } else if(this.userEmail == '') {
              this.error = 'Емейл не введен';
              return;
            }
            
            this.error = '';

            this.users.push({
              name: this.userName,
              pass: this.userPass,
              email: this.userEmail
            })
        }
    }
 }
</script>

<style scoped>
   .form{
    justify-content: center;
    align-items: center;
    display: flex;
    flex-direction: column;
    font-size: 150px;
   }
   input{
    width: 300px;
    margin-top: 15px;
    padding: 15px;
    border-radius: 15px;
    font-size: 20px;
   }
   button{
    margin-top: 15px;
    width: 330px;
    padding: 15px;
    border-radius: 15px;
    font-size: 20px;
   }
   p, h3{
    font-size: 15px;
   }
   .user{
    background-color: #333;
    border-radius: 15px;
    color: aliceblue;
    width: 300px;
    height: auto;
    padding: 15px;
    margin-top: 15px
   }
</style>

