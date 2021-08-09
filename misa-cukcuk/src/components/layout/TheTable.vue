<template>
  <div class="wrapper-data">
    <div class="grid" id="grid">
      <table>
        <thead>
          <tr class="employees-title">
            <th>#</th>
            <th>Mã nhân viên</th>
            <th>Họ và tên</th>
            <th>Giới tính</th>
            <th>Ngày sinh</th>
            <th>Điện thoại</th>
            <th>Email</th>
            <th>Chức vụ</th>
            <th>Phòng ban</th>
            <th class="align-item-money">Mức lương cơ bản</th>
            <th>Tình trạng công việc</th>
          </tr>
        </thead>

        <tbody id="listDataEmployee">
          <tr
            v-for="(item, index) in employees"
            v-bind:key="index"
            v-on:click="clicktableRow($event)"        
           :employeeId="item.EmployeeId"
          >
            
            <td>
              <input type="checkbox" name="employeeId" value="" />
              <label for=""></label>
            </td>
            <td>{{ item.EmployeeCode }}</td>
            <td>{{ item.FullName }}</td>
            <td>{{ item.GenderName }}</td>
            <td>{{ item.DateOfBirth }}</td>
            <td>{{ item.PhoneNumber }}</td>
            <td>{{ item.Email }}</td>
            <td>{{ item.PositionName }}</td>
            <td>{{ item.DepartmentName }}</td>
            <td class="align-item-money">{{ item.Salary }}</td>
            <td>{{ item.WorkStatus }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <the-pop-up
      v-bind:employeeInfor="employeeInfor"
      v-on:closeIn4OfEmployee="closeIn4OfEmployee"
      v-bind:in4Employee="in4Employee"
      
    />
  </div>
</template>

<script>
import axios from "axios";
import ThePopUp from "./ThePopUp.vue";
export default {
  components: { ThePopUp },
  data() {
    return {
      employees: [],
      in4Employee: false,
      tableRowId:'',
      employeeInfor:{},
    };
  },
  methods: {
    closeIn4OfEmployee() {
      this.in4Employee = false;
    },
    clicktableRow(event) {
      this.tableRowId = event.target.parentElement.getAttribute('employeeId');
      this.in4Employee = true;
      axios      
      .get(`http://cukcuk.manhnv.net/v1/Employees/${this.tableRowId}`)
      .then((res) => {
        console.log(res.data);
        this.employeeInfor = res.data;
        
      })
      .catch(() => {});
      console.log(this.tableRowId);
    },
  },
  created() {
    
    axios
      .get("http://cukcuk.manhnv.net/v1/Employees")
      .then((res) => {
        this.employees = res.data;
        
      })
      .catch(() => {});
  },
};
</script>

<style>
</style>