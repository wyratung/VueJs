<template>
  <div class="base-input">
    <label class="base-input__label">
      {{ label }} <span v-if="required">(<b class="text--red">*</b>)</span>
    </label>

    <div
      class="base-input__input"
      :class="{ 'base-input__input--error': isError }"
    >
      <input
        ref="input"
        v-bind="$attrs"
        v-bind:value="value"        
        :tabindex="tabIndex"
        v-on="inputListeners"
        
        
      />
    </div>
    <div class="text--red" style="margin-top: 2px">{{ errors }}</div>
    <!-- </ValidationProvider> -->
  </div>
</template>

<script>
export default {
  name: "BaseInput",
  inheritAttrs: false,
  data() {
    return {
      errors: "",
      isError: false,
      
    };
  },
  props: {
    label: {
      type: String,
      default() {
        return "";
      },
    },
    value: {
      type: [Number,String],
      default() {
        return "";
      },
    },
    tabIndex: {
      type: String,
      default() {
        return "";
      },
    },
    
    // rules: {
    //   type: String,
    //   default() {
    //     return "";
    //   },
    // },
    required: {
      type: Boolean,
      default() {
        return false;
      },
    },
    inputCheck: {
      type: Boolean,
      default() {
        return false;
      },
    },
  },
  methods: {
    /**
     * focus input từ parent
     */
    focusInput() {
      this.$nextTick(() => {
        this.$refs.input.focus();
      });
    },
    /**
     * validate email đúng định dạng
     * @param {String} email xâu email người dùng nhập vào
     * @returns {Boolean} true nếu đúng định dạng
     
     */
    validEmail: function (email) {
      var re =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    validateInput(self) {
      
      if (self.required && (self.value === null || self.value === "")) {  
        self.errors = "Trường này bắt buộc nhập";
        self.isError = true;
      }
      if (self.$refs.input.type == "email" && self.value != null) {
        if (!self.validEmail(self.value)) {
          self.errors = "Sai định dạng email";
          self.isError = true;
        }
      }
    },
  },
  computed: {
    inputListeners: function () {
      
      var vm = this
      // `Object.assign` merges objects together to form a new object
      return Object.assign({},
        // We add all the listeners from the parent
        this.$listeners,
        // Then we can add custom listeners or override the
        // behavior of some listeners.
        {
          // This ensures that the component works with v-model
          input: function (event) {
            vm.$emit('input', event.target.value)
          }
        }
      )
    }
  },
  watch: {
    inputCheck: function () {
      this.validateInput(this);
    },
  },
};
</script>

<style scoped>
@import url("../../css/common/input.css");
</style>