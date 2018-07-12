<template>
  <div id="app">
    <div class="line"></div>
    <div style="width: 300px; margin-top: 30px; margin-right: auto; margin-left: auto;">
      <el-steps :active="step" align-center>
        <el-step></el-step>
        <el-step></el-step>
        <el-step></el-step>
      </el-steps>
    </div>
    <StepOne v-on:nextStep="onNextStep" v-if="step === '1'"/>
    <StepTwo v-on:nextStep="onNextStep" v-if="step === '2'"/>
    <Finish v-if="step === '3'"/>
    
  </div>
</template>

<script>
import StepOne from './components/StepOne';
import StepTwo from './components/StepTwo';
import Finish from './components/Finish';

export default {
  name: 'app',
  data() {
    return {
      step: '1'
    }
  },
  components: {
    StepOne,
    StepTwo,
    Finish
  },
  methods: {
    onNextStep() {
      if (this.step === '1') {
        this.step = '2';
      }
      else {
        this.step = '3';
      }
    }
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400');
.line {
  margin-left: auto;
  margin-right: auto;
  width: 416px;
  height: 3px;
  background-color: #409eff;
}
.light {
  font-family: 'Roboto';
  font-weight: 300;
}
.regular {
  font-family: 'Roboto';
  font-weight: 400;
}
.title {
  font-size: 48px;
  text-align: center;
  margin-top: 40px;
  line-height: 57px;
  color: #303133;
}
.subtitle {
  font-size: 24px;
  text-align: center;
  line-height: 28px;
  color: #303133;
}
.form {
  width: 450px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
}
.label {
  font-size: 16px;
  color: #606266;
  margin-bottom: 8px;
  margin-left: 5px;
  margin-top: 20px;
}
</style>
