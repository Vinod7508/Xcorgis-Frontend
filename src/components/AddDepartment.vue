<template>
  
  <form action="">
  <label>Dept Name:</label><br>
    <input type="text" v-model="newdept.departmentName"  required>
    <br>
    <label>addtional info:</label><br>
    <input type="text" v-model="newdept.additionalInformation" required>

    <!-- <div class="terms">
      <input type="checkbox" v-model="newdept.isActive" required>
      <label>isActive</label>
    </div> -->
    
     <div class="submit">
      <button class="addept" @click="Addept">Add department</button>
    </div>
  </form>

</template>

<script>

import axios from "axios";

export default {
  name: "adddept",
  data(){
    return{
      newdept:{
          departmentName: "",
          additionalInformation: ""
         }
    }
  },
  methods:{
     Addept(){
       try {
        console.log("adding department")
         this.$emit('rerender');
         axios.post("https://localhost:5001/api/Department", this.newdept)
         alert("department added succesfully to microsoft sql server database")
         this.$emit('rerender');
      }
       catch (e) {
        console.log(e);
      }
   }
}
}
</script>

<style>

form {
    max-width: 420px;
    margin:30px 900px 30px 40px;
    background: white;
    text-align: left;
    padding: 20px;
    border-radius: 10px;
  }

  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }

  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }

.addept {
    background: rgb(134, 204, 134);
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    margin-right: 220px;
    color: white;
    border-radius: 20px;
  }
  .submit {
    text-align: center;
  }
</style>