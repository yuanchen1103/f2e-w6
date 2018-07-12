<template>
   <div>
      <h1 class="title light">Create Account</h1>
      <h3 class="subtitle light">Glad to see you here!</h3>
      <div class="form">
         <div class="label regular">Account*</div>
         <el-input v-model="account" placeholder="example@email.com" @blur="blurAccount"></el-input>
         <p class="warn" v-if="accountInvalid">INVALID EMAIL</p>
         <i class="el-icon-warning" v-if="accountInvalid"></i>
         <i class="el-icon-success" v-if="accountSuccess"></i>

         <div class="label regular">Password*</div>
         <el-input v-model="password" type="password" placeholder="type your password" @blur="blurPassword"></el-input>
         <p class="warn password" v-if="passwordInvalid">MINIMUM 8 CHARACTERS</p>
         <i class="el-icon-warning" v-if="passwordInvalid"></i>
         <i class="el-icon-success" v-if="passwordSuccess"></i>

         <div class="label regular">Comfirm Password*</div>
         <el-input v-model="passwordAgain" type="password" placeholder="type your password again!" @blur="blurPasswordAgain"></el-input>
         <p class="warn password-again" v-if="passwordAgainInvalid">NOT MATCH</p>
         <i class="el-icon-warning" v-if="passwordAgainInvalid"></i>
         <i class="el-icon-success" v-if="passwordAgainSuccess"></i>

         <el-button type="primary" style="width: 100%; margin-top: 30px;" class="light" @click="next">NEXT & SUBMIT</el-button>
      </div>
   </div>
</template>

<script>
export default {
  name: 'StepOne',
  data() {
    return {
      account: '',
      password: '',
      passwordAgain: '',
      accountInvalid: false,
      accountSuccess: false,
      passwordInvalid: false,
      passwordSuccess: false,
      passwordAgainInvalid: false,
      passwordAgainSuccess: false
    };
  },
  methods: {
    blurAccount() {
      // eslint-disable-next-line
      const emailRule = /^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z]+$/;
      if (this.account.search(emailRule) != -1) {
        this.accountInvalid = false;
        this.accountSuccess = true;
      } else {
        this.accountInvalid = true;
        this.accountSuccess = false;
      }
    },
    blurPassword() {
      if (this.password.length >= 8) {
        this.passwordInvalid = false;
        this.passwordSuccess = true;
      } else {
        this.passwordInvalid = true;
        this.passwordSuccess = false;
      }
    },
    blurPasswordAgain() {
      if (this.passwordAgain !== '' && this.passwordSuccess === true) {
        if (this.passwordAgain === this.password) {
          this.passwordAgainInvalid = false;
          this.passwordAgainSuccess = true;
        } else {
          this.passwordAgainInvalid = true;
          this.passwordAgainSuccess = false;
        }
      }
    },
    next() {
      if (this.accountSuccess === true && this.passwordSuccess === true && this.passwordAgainSuccess === true) {
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
.password {
  margin-left: 262px;
}
.password-again {
  margin-left: 340px;
}
</style>
