<template>
   <div>
      <h1 class="title light">Congratulations</h1>
      <h3 class="subtitle light">Now you’re one of us! </h3>
      <div class="icon"><i class="fas fa-smile"></i></div>
      <p>Redirected to homepage after 5 seconds…</p>
   </div>
</template>

<script>
export default {
  name: 'Finish',
  data() {
    return {

    };
  },
  methods: {
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.icon {
  font-size: 220px;
  color: #BEE1FF;
  text-align: center;
  margin-right: auto;
  margin-left: auto;
  margin-top: 20px;
}
p {
  text-align: center;
  margin-top: 50px;
  color: #409EFF;
}
</style>
