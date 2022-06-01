<template>
  <div>
    <div class="container">
      <button @click="flag = 1"><strong>Form</strong></button>
      <button @click="flag = 2"><strong>Admin</strong></button>
      <button @click="flag = 3"><strong>Student</strong></button>
      <br><br>
    </div> 
    <form @submit.prevent="formHandle" v-if="flag == 1">
      <div>
        <label for="name"><strong>Name</strong></label
        ><br />
        <input
          type="text"
          placeholder="Enter your name"
          name="name"
          required
          v-model.trim="formValues.name"
        /><br />
        <label for="age"><strong>Age</strong></label
        ><br />
        <input
          type="text"
          placeholder="Enter your Age"
          name="age"
          required
          v-model.number.trim="formValues.age"
        /><br />
        <label for="city"><strong>City</strong></label
        ><br />
        <input
          type="text"
          placeholder="Enter your city"
          name="city"
          required
          v-model.trim="formValues.city"
        />
      </div>
      <br />
      <div class="role">
        <input
          type="radio"
          value="student"
          id="student"
          name="role"
          required
          v-model="formValues.picked"
        />
        <label for="student" class="radio">Student</label>
        <input
          type="radio"
          value="admin"
          id="admin"
          name="role"
          required
          v-model="formValues.picked"
        />
        <label for="admin" class="radio">Admin</label>
      </div>
      <br />
      <button type="submit"><strong>Add User</strong></button>
    </form>
    <adminApp v-if="flag == 2" :role="role.filter(e=>e.picked==='admin')" @delete="reset"/>
    <studentApp v-if="flag == 3" :role="role.filter(e=>e.picked==='student')" @delete="reset"/>
  </div>
</template>

<script>
import adminApp from "./admin.vue";
import studentApp from "./student.vue";
export default {
  name: "formApp",
  components: {
    adminApp,
    studentApp,
  },
  data() {
    return {
      formValues: {
        name: "",
        age: "",
        city: "",
        picked: "",
      },
      flag:1,
      role:[],
    };
  },
  methods: {
    formHandle(e) {
      e.preventDefault();
      this.role.push(this.formValues);
      console.log(this.formValues);
    },
    reset(index) {
        this.role.splice(index,1);
    }
  },
};
</script>

<style >
  
  button {
      width: 10%;
      padding: 10px 0;
      margin: 10px;
      border-radius: 5px; 
      border: none;
      background: #8ebf42; 
      font-size: 14px;
      font-weight: 600;
      color: #fff;
      }
      input[type=text] {
      width: 50%;
      padding: 16px 8px;
      margin: 8px 0;
      display: inline-block;
      border: 1px solid #ccc;
      box-sizing: border-box;
      font-size:medium;
      }
      input[type=radio]{
      /* width: 30%; */
      padding: 10px 5px;
      margin: 10px 15px;
      display: inline-block;
      }
</style>