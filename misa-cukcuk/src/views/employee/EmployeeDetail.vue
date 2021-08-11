<template>
  <div class="formstaff-overlay">
    <div class="formstaff">
      <div class="formstaff-header">
        <div class="formstaff-header__label">THÔNG TIN NHÂN VIÊN</div>
        <button class="close btn-exit"  @click="closeFormStaff"> <i class="fas fa-times"></i></button>
      </div>
      <div class="formstaff-body">
        <div class="formstaff-avatar">
          <div class="formstaff-avatar__img"></div>
          <span class="formstaff-avatar__required"
            >(Vui lòng chọn ảnh có định dạng <br />
            <b>.jpg, .jpeg, .png, .gif.</b>)
          </span>
        </div>
        <div class="formstaff-infor">
          <div class="formstaff-infor__title">
            <div>A. THÔNG TIN CHUNG:</div>
            <div class="under-line"></div>
          </div>
          <div class="inline-block">
            <div class="form-block">
              <base-input
                label="Mã nhân viên"
                tabIndex="1"
                ref="employeeCodeInput"
                :required="true"
                v-model="employeeDetailData['EmployeeCode']"
                :inputCheck="inputCheck"
              />
            </div>
            <div class="form-block">
              <base-input
                label="Họ và tên"
                tabIndex="2"
                v-model="employeeDetailData['FullName']"
                :required="true"
                :inputCheck="inputCheck"
              />
            </div>
          </div>

          <div class="inline-block">
            <div class="form-block">
              <base-input label="Ngày sinh" tabIndex="3" type="date" v-model="employeeDetailData['DateOfBirth'] "/>
            </div>
            <div class="form-block">
              <base-input label="Giới tính" tabIndex="4" />
            </div>
          </div>
          <div class="inline-block">
            <div class="form-block">
              <base-input
                label="Số CMTND/Căn cước"
                type="text"
                tabIndex="5"
                :required="true"
                v-model="employeeDetailData['IdentityNumber']"
                :inputCheck="inputCheck"
              />
            </div>
            <div class="form-block">
              <base-input label="Ngày cấp" type="date" tabIndex="6" />
            </div>
          </div>
          <div id="staff-place" style="width: 285.5px">
            <base-input
              label="Nơi cấp"
              type="text"
              tabIndex="7"
              v-model="employeeDetailData['IdentityPlace']"
            />
          </div>
          <div class="inline-block">
            <div class="form-block">
              <base-input
                label="Email"
                type="text"
                tabIndex="8"
                :required="true"
                v-model="employeeDetailData['Email']"
                :inputCheck="inputCheck"
              />
            </div>
            <div class="form-block">
              <base-input
                label="Điện thoại"
                type="text"
                tabIndex="9"
                :required="true"
                v-model="employeeDetailData['PhoneNumber']"
                :inputCheck="inputCheck"
              />
            </div>
          </div>
          <div class="formstaff-infor__title">
            <div>B. THÔNG TIN CÔNG VIỆC:</div>
            <div class="under-line"></div>
          </div>
          <div class="inline-block">
            <div class="form-block">
              <!-- <base-combobox label="Vị trí"  /> -->
              <base-input
                label="Vị trí"
                type="text"
                tabIndex="12"
                v-model="employeeDetailData['PositionName']"
              />
            </div>
            <div class="form-block">
              <!-- <base-combobox label="Phòng ban" /> -->
              <base-input
                label="Phòng ban"
                type="text"
                tabIndex="12"
                v-model="employeeDetailData['DepartmentName']"
              />
            </div>
          </div>
          <div class="inline-block">
            <div class="form-block">
              <base-input
                label="Mã số thuế cá nhân"
                type="text"
                tabIndex="12"
                v-model="employeeDetailData['PersonalTaxCode']"
              />
            </div>
            <div class="form-block block-salary">
              <base-input label="Mức lương cơ bản" type="text" tabIndex="13" v-model="employeeDetailData['Salary']"/>
            </div>
          </div>
          <div class="inline-block">
            <div class="form-block">
              <base-input
                label="Ngày gia nhập công ty"
                type="date"
                tabIndex="14"
              />
            </div>
            <div class="form-block">
              <base-input
                label="Tình trạng công việc"
                type="text"
                tabIndex="15"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="formstaff-footer">
        <button class=" button-cancel button button-short button">Hủy</button>
        <button class="button button-save " @click="saveEmployeeData">
          <div class="btn-icon btn-save"></div>
          <div class="btn-text">Lưu</div>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("../../css/layout/employee-detail.css");
</style>

<script>
import BaseInput from "../../components/base/BaseInput.vue";
//  import CommonMethods from "../../mixins/CommonMethods.js";
import Vue from "vue";
import axios from "axios";
export default {
  name: "EmployeeDetail",
  // mixins: [CommonMethods],
  components: {
    BaseInput,
  },
  // mounted() {
  //   this.$refs.employeeCodeInput.focusInput();
  // },
  props: {
    employeeData: {
      type: Object,
      default() {
        return {};
      },
    },
    mode: {
      type: String,
      default() {
        return "1";
      },
    },
  },
  data() {
    return {
      employeeDetailData: Vue.util.extend({}, this.employeeData),
    };
  },
  methods: {
    async postEmployee(requestMode, employeeData) {
      try {
        let response;
        if (requestMode == "POST") {
          response = await axios.post(
            "http://cukcuk.manhnv.net/v1/Employees",
            employeeData
          );
        }
        if (requestMode == "PUT") {
          response = await axios.put(
            `http://cukcuk.manhnv.net/v1/Employees/` +
              employeeData["EmployeeId"],
            employeeData
          );
        }
        console.log(response);
        return response;
      } catch (error) {
        if (error.response.status == "404") {
          console.log("Not found API url");
        }else{
          console.log(error);
        }
      }
    },
    
    loadTable() {
      this.$emit("loadTable");
    },
    
    closeFormStaff() {
      this.$emit("closeFormStaff");
    },
    /**
     * thêm mới hoặc sửa thông tin nhân viên
     */
    async saveEmployeeData() {
      if (this.mode == "1") {
        //thêm mới nhân viên
        console.log(this.employeeDetailData);
        await this.postEmployee("POST", this.employeeDetailData);
      }
      if (this.mode == "2") {
        //sửa nhân viên
        console.log("sửa");
        await this.postEmployee("PUT", this.employeeDetailData);
      }
      //Hiện thông báo thêm thành công
      //Close form
      this.closeFormStaff();
      //load lại table
      this.loadTable();
      console.log(this.employeeDetailData["EmployeeCode"]);
    },
  },
};
</script>