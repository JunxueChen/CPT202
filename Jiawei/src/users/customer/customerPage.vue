<script>

import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
import axios from "axios";
import Navigate from "@/users/navigatebar/navigateBar.vue";


// document.getElementById('avatar-dropdown').addEventListener('click', function() {
//   var dropdownMenu = document.getElementById('dropdown-menu');
//   if (dropdownMenu.style.display === 'block') {
//     dropdownMenu.style.display = 'none';
//   } else {
//     dropdownMenu.style.display = 'block';
//   }
// });

export default {
  components: {Navigate, VueDatePicker },
  data() {
    return {
      date: null,
      trainer:null,
      showdrop: false,
    };
  },
  methods:{
    toaccount(){
      this.$router.push("/account")
    },
    toview(){
      this.$router.push("/viewappointment")
    },
    submitForm(){
      const formData= new FormData();
      formData.append("trainer", this.trainer);
      formData.append("data",this.date)
      axios.post("http://example.com/api/appointment", formData)
          .then(response =>{
            console.log("appointment successful", response.data);
          })
          .catch(error =>{
            console.log("error",error);
          })
    },
    toggleDropdown() {
      this.showdrop = !this.showdrop;
      }
  }
}
</script>

<template>

  <Navigate/>

<div class="appoint">
  <h1>Appointment now!</h1>


  <form @submit.prevent="submitForm">
    <div id="choosertrainer">
    Trainer:<select id="trainer" v-model="trainer">
        <option value="trainer1">trainer1</option>
      <option value="trainer2">trainer2</option>
      <option value="trainer3">trainer3</option>
    </select>
    </div>

    <br>
    <div id="selecttime">
    <VueDatePicker v-model="date"></VueDatePicker>
    </div>
    <div>
      <button id="submit" type="submit">Appointment</button>
    </div>

  </form>

</div>


  <div id="right">
  <div id="account1"  @click="toggleDropdown">
   <img src="../../assets/img.png" alt="avatar">
  </div>
  <div class="dropdown-menu" v-show="showdrop">
    <ul id="ul1">
      <li >退出登录</li>
      <li @click="toview">view appointment</li>
      <li @click="toaccount">Account info</li>

      <!-- 其他选项 -->
    </ul>
  </div>
  </div>
</template>

<style>
/* Style for the main container */
#appointment-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

/* Style for the title */
h1 {
  font-size: 24px;
  margin-bottom: 20px;
  text-align: center;
}

/* Style for the form */
form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* Style for the select dropdown */
#trainers select {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

/* Style for the date picker */
#selecttime {
  width: 50%;
  margin-bottom: 20px;
}

/* Style for the appointment button */
#submit {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  text-align: center;
  width: auto;
}

/* Hover effect for the appointment button */
#submit:hover {
  background-color: #0056b3;
}
.appoint{
  margin-top: 200px;
   background: yellow;
  width: 75%;
  position: relative;
  left: 10%;
}
#account1{
  position: fixed;
  top: 40px;
  right: 40px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: 10px;
}
img{
  width: auto;
  height: auto;
  max-width: 100%;
  max-height: 100%;
}
.dropdown-menu{
  position: absolute;
  top: -335px;
  right: 40px;
 background: #2c3e50;
  color: #131212;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  z-index: 1000;


}
#ul1{
  list-style: none;
  padding: 0;
}

#ul1 li{
  text-align: center;
  background: #f0f0f0;
  margin: 2px;
}
#ul1 li:hover{
  cursor: pointer;
  background-color: #f0f0f0;
}
#right{

  z-index: 20;
  position: relative;
}
</style>