<template>
  <div>
    <button class="gbtn" @click="getallDepartment">GetDept</button>
  </div>

  <table>
    <tr>
      <th>DepartmentId</th>
      <th>DepartmentName</th>
      <th>Additional Information</th>
      <th>Manage</th>
    </tr>
    <tr v-for="dept in departments" :key="dept.id">
      <td>{{ dept.id }}</td>
      <td>{{ dept.departmentName }}</td>
      <td>{{ dept.additionalInformation }}</td>
      <td>
        <button class="editbtn" @click="editdept(dept.id)">Edit</button>
        <button class="deletebtn" @click="deleteDept(dept.id)">Delete</button>
      </td>
    </tr>
  </table>

  <!--add department component -->
  <div>
    <adddept :rerender="getallDepartment" />
  </div>

  <!--edit component incomplete-->
  <form action="" id="editform">
    <label>Dept Name:</label><br />
    <input type="text"  v-model="test"  required  />
    <br />
    <label>addtional info:</label><br />
    <input type="text"  v-model="test"   required />
    <div class="submit">
      <button class="eddept" @click="finaledit(dept)">edit department</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
import adddept from "./AddDepartment.vue";

export default {
  name: "department",
  components: {
    adddept,
  },
  data() {
    return {
      departments: []
    };
  },
  methods: {
    async getallDepartment() {
      try {
        let baseurl = "https://localhost:5001/api/Department";
        const deptserverdata = await axios.get(baseurl);
        this.departments = deptserverdata.data;
      } catch (e) {
        console.log(e);
      }
    },

    async deleteDept(id) {
      axios.delete("https://localhost:5001/api/Department/" + id).then(() => {
        alert("deletion successfull");
        this.getallDepartment();
      });
    },

    async editdept(id){
      console.log(`editing department with id ${id} `)
    },

    async finaleditdepartment(dept){
      console.log(`editing department with id ${id} `)
    }
  }
};
</script>


<style >
body {
  color: #999;
  background: #f3f3f3;
  font-family: "Roboto", sans-serif;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 60%;
  margin-bottom: 0px;
  margin-left: 40px;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

.gbtn {
  background-color: rgb(100, 201, 241);
  display: inline-block;
  padding: 0.3em 1.2em;
  border: 0.16em solid rgba(255, 255, 255, 0);
  box-sizing: border-box;
  text-decoration: none;
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  color: #ffffff;
  text-shadow: 0 0.04em 0.04em rgba(0, 0, 0, 0.35);
  text-align: center;
  transition: all 0.2s;
  margin-right: 1400px;
  margin-left: 40px;
  margin-bottom: 15px;
}

.editbtn {
  margin-left: 4px;
  margin-top: 2px;
  margin-bottom: 2px;
  background-color: rgb(164, 231, 76);
}

.deletebtn {
  margin-left: 4px;
  margin-top: 2px;
  margin-bottom: 2px;
  background-color: rgb(226, 115, 115);
}

#editform {
  max-width: 420px;
  margin: 30px 500px 30px 40px;
  background: white;
  text-align: left;
  padding: 20px;
  border-radius: 10px;
  position: relative;
  left: 500px;
  bottom: 300px;
}

.eddept {
  background: rgb(150, 150, 231);
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  margin-right: 220px;
  color: white;
  border-radius: 20px;
}
</style>
