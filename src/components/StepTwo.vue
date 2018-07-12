<template>
   <div>
      <h1 class="title light">General Infomation</h1>
      <h3 class="subtitle light">Tell us who you are!</h3>
      <div class="form">
         <div class="label regular">Name</div>
         <el-input v-model="Name" placeholder="Example Name"></el-input>

         <div class="label regular">Birthday*</div>
         <el-date-picker v-model="birthday" type="date" placeholder="choose your date" @blur="blurBirthday" style="width: 100%;"></el-date-picker>
         <p class="warn birthday" v-if="birthdayInvalid">REQUIRED</p>
         <i class="el-icon-warning" v-if="birthdayInvalid"></i>
         <i class="el-icon-success" v-if="birthdaySuccess"></i>

         <div class="label regular">Phone*</div>
         <el-input v-model="phone" placeholder="type your password" @blur="blurPhone"></el-input>
         <p class="warn" :class="{birthday: phoneInvalidText === 'REQUIRED', number: phoneInvalidText === 'NUMBERS ONLY'}"  v-if="phoneInvalid">{{phoneInvalidText}}</p>
         <i class="el-icon-warning" v-if="phoneInvalid"></i>
         <i class="el-icon-success" v-if="phoneSuccess"></i>

         <el-button type="primary" style="width: 100%; margin-top: 30px;" class="light" @click="next">NEXT & SUBMIT</el-button>
      </div>
   </div>
</template>

<script>
export default {
  name: 'StepOne',
  data() {
    return {
      Name: '',
      birthday: '',
      phone: '',
      birthdayInvalid: false,
      birthdaySuccess: false,
      phoneInvalid: false,
      phoneInvalidText : '',
      phoneSuccess: false
    };
  },
  methods: {
    blurBirthday() {
      if (this.birthday !== '') {
        this.birthdayInvalid = false;
        this.birthdaySuccess = true;
      } else {
        this.birthdayInvalid = true;
        this.birthdaySuccess = false;
      }
    },
    blurPhone() {
      // eslint-disable-next-line
      const reg = /^[\d]+$/;
      if (this.phone !== '') {
        if (reg.test(this.phone)) {
          this.phoneInvalid = false;
          this.phoneSuccess = true;
        } else {
          this.phoneInvalid = true;
          this.phoneSuccess = false;
          this.phoneInvalidText = 'NUMBERS ONLY';
        }
      }
      else {
        this.phoneInvalid = true;
        this.phoneSuccess = false;
        this.phoneInvalidText = 'REQUIRED';
      }
    },
    next() {
      if (this.birthdaySuccess === true && this.phoneSuccess === true) {
        this.$emit('nextStep');
      }
      else {
        this.$message.error('Please complete your form!');
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.success {
  border: 1px solid #67c23a !important;
  border-radius: 4px;
}
i {
  position: absolute;
  margin-top: 12px;
  margin-left: -30px;
}
.el-icon-warning {
  color: #f56c6c;
}
.el-icon-success {
  color: #67c23a;
}
.warn {
  color: #f56c6c;
  position: absolute;
  font-size: 10px;
  margin-left: 325px;
  margin-top: -25px;
}
.birthday {
  margin-left: 350px;
}
.number {
  margin-left: 316px;
}
</style>
