<template>
  <div class="content-controls">
    <div class="content-controls-left">
      <div class="controls-left-lable">
        <p>Danh sách nhân viên</p>
      </div>
      <div class="controls-left-filter">
        <input
          class="search-input"
          type="text"
          placeholder="Tìm kiếm theo Mã, Tên hoặc Số điện thoại"
        />

        <base-combo-box
          ref="combobox-department"
          v-model="comboboxDepartmentValue"
          @clearComboboxValue="clearComboboxValue"
          @updateComboboxValue="updateComboboxValue"
          typeCombobox= "department"
        />

        <base-combo-box
          ref="combobox-position"
          v-model="comboboxPositionValue"
          @clearComboboxValue="clearComboboxValue"
          @updateComboboxValue="updateComboboxValue"
          typeCombobox="position"
        />
      </div>
    </div>
    <div class="content-controls-right">
      <div class="wrap-button">
        <button
          class="button button-delete"
          @click="deleteEmployees(listSelectedEmployees)"
          v-show="isShow"
        >
          <div class="btn-icon">
            <i class="far fa-trash-alt"></i>
          </div>
          <div class="btn-text">Xóa nhân viên</div>
        </button>
        <button class="button button-employee" @click="addEmployee">
          <div class="btn-icon btn-employee"></div>
          <div class="btn-text">Thêm nhân viên</div>
        </button>
      </div>

      <div class="controls-right-refresh" @click="loadTable"></div>
    </div>
  </div>
</template>

<style scoped>
@import url("../../css/layout/control.css");

</style>

<script>
import axios from "axios";
import { eventBus } from "../../main.js";
import BaseComboBox from '../../components/base/BaseComboBox.vue';

export default {
  name: "TheControl",
  components: {
    BaseComboBox
    
  },
  created() {
    eventBus.$on("showSelectedEmployees", (listSelectedEmployees) => {
      this.listSelectedEmployees = listSelectedEmployees;
      if (this.listSelectedEmployees.length > 0) {
        this.isShow = true;
      } else {
        this.isShow = false;
      }
    });
  },
  data() {
    return {
      employeeCode: "NV001",
      listSelectedEmployees: [],
      isShow: false,
      comboboxDepartmentValue: "",
      comboboxPositionValue: "",
    };
  },
  methods: {
    callAPINewEmployee: async () => {
      const response = await axios.get(
        `http://cukcuk.manhnv.net/v1/Employees/NewEmployeeCode`
      );
      return response.data;
    },
    async addEmployee() {
      let newEmployeeCode;
      newEmployeeCode = await this.callAPINewEmployee();
      this.$emit("addEmployee", newEmployeeCode);
    },
    /**
     * load lại dữ liệu trên bảng
     */
    loadTable() {
      this.$emit("loadTable");
    },
    /**
     * truyền dữ liệu chứa các khóa chính của nhân viên được xóa
     * @param {array} listSelectedEmployees : chứa các khóa chính của nhân viện được chọn
     
     
     */
    deleteEmployees(listSelectedEmployees) {
  //console.log(listSelectedEmployees);
      eventBus.$emit("deleteEmployees", listSelectedEmployees);
      this.$emit("showPopup");
    },
    /**
     * xóa dữ liệu ở ô input của combobox
     * @param {Int} type xác định loại combobox 1(deparment), 2(position)
     
     */
    clearComboboxValue(type) {
      if (type == "department") {
        this.comboboxDepartmentValue = "";
      }
      if (type == "position") {
        this.comboboxPositionValue = "";
      }
    },
    updateComboboxValue(type, selectedValue) {
      if (type == "department") {
        this.comboboxDepartmentValue = selectedValue;
      }
      if (type == "position") {
        
        this.comboboxPositionValue = selectedValue;
      }
    },
  },
};
</script>