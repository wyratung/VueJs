<template>
  <div style="display: flex">
    <the-menu/>
    <employee-list  
      @addEmployee="addEmployee"
      @editEmployee="editEmployee"
      ref="employeeList"
      @showPopup="showPopup"
    />  
    
    <employee-detail
      :key="focusKey"
      :class="{ 'formstaff--hide': isHide }"
      @closeFormStaff="closeFormStaff"
      :employeeData="employeeData"
      :mode="mode"
      @loadTable="loadTable"
    />
    
    <base-popup
      :apiUrl="baseEmployeeApi"
      :listData="listSelectedEmployees"
      :class="{ 'popup--show': popupShow }"
      @loadTable="loadTable"
      @closePopup="closePopup"
    />
    
  </div>
</template>

<script>

import TheMenu from "../layout/TheMenu.vue";
import EmployeeList from "../../views/employee/EmployeeList.vue";
import EmployeeDetail from "../../views/employee/EmployeeDetail.vue";
import BasePopup from "../../components/base/BasePopup.vue";
import { eventBus } from "../../main.js";


export default {
  name: "theWrapper",

  components: {
    EmployeeList,
    EmployeeDetail,
    BasePopup,
    TheMenu,
    
  },
  created() {
    eventBus.$on("deleteEmployees", (listSelectedEmployees) => {
      this.listSelectedEmployees = listSelectedEmployees;
    });
  },
  data() {
    return {
      isHide: true,
      show: "",
      employeeData: {},
      focusKey: false,
      mode: "1",
      listSelectedEmployees: [],
      baseEmployeeApi: "http://cukcuk.manhnv.net/v1/Employees/",
      popupShow: false,
    };
  },
  methods: {
    /**
     * hiển thị form thêm nhân viên
     * @param {Object} employeeCode chứa mã code nhân viên mới
   
     
     */
    addEmployee(employeeCode) {
      this.isHide = false;
      this.focusKey = !this.focusKey;
      this.employeeData = { EmployeeCode: employeeCode };
      this.mode = "1";
    },
    
    closeFormStaff() {
      this.isHide = true;
    },
    /**
     * hiển thị form thông tin nhân viên và cho phép chỉnh sửa
     * @param {Object} employeeData chứa thông tin nhân viên hiển thị
   
     */
    editEmployee(employeeData) {
      this.isHide = false;
      this.mode = "2";
      this.focusKey = !this.focusKey;
      this.employeeData = employeeData;
    },
    /**
     * load lại dữ liệu trong bảng
     
     */
    loadTable() {
      this.$refs.employeeList.loadTable();
    },

    closePopup() {
      this.popupShow = false;
    },

    showPopup() {
      this.popupShow = true;
    },
  },
};
</script>

<style>
</style>