<template>
  <div class="employee-list">
    <the-control @addEmployee="addEmployee" @loadTable="loadTable" @showPopup="showPopup"/>
    <!-- <the-top-of-list/> -->
    <base-table
      :key = "tableKey"
      :urlAPI="employeesAPI"
      :tableHeaders="tableEmployeeHeader"
      @editEmployee = "editEmployee"
    />
    <the-footer/>
  </div>
</template>

<style scoped>
@import url("../../css/layout/employee-list.css");
</style>

<script>
//import TheTopOfList from "../../components/layout/TheTopOfList.vue"
import TheFooter from "../../components/layout/TheFooter.vue"
 import TheControl from "../common/TheControl.vue";
import BaseTable from "../../components/base/BaseTable.vue";

//import ThePaging from "../common/ThePaging.vue";
export default {
  name: "EmployeeList",
  components: {
    TheControl,
    BaseTable,
    TheFooter,
    
  },
  data() {
    return {
      employeesAPI: "http://cukcuk.manhnv.net/v1/Employees",
      tableKey:false,
      tableEmployeeHeader: [
        { EmployeeCode: "Mã nhân viên", type: "0" },
        { FullName: "Họ và tên", type: "0" },
        { GenderName: "Giới tính", type: "0" },
        { DateOfBirth: "Ngày sinh", type: "1" },
        { PhoneNumber: "Điện thoại", type: "0" },
        { Email: "Email", type: "0" },
        { PositionName: "Chức vụ", type: "0" },
        { DepartmentName: "Phòng ban", type: "0" },
        { Salary: "Mức lương cơ bản", type: "2" },
        { WorkStatus: "Tình trạng công việc", type: "0" },
      ],
    };
  },
  methods: {
    
    addEmployee(employeeCode){
      this.$emit("addEmployee", employeeCode);
    },
    
    editEmployee(employeeData){
      this.$emit("editEmployee", employeeData);
    },
    loadTable(){
      this.tableKey = !this.tableKey;
    },
    showPopup(){
      this.$emit("showPopup");
    }
  },
  
};
</script>