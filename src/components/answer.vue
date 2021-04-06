<template>
  <div class="alert alert-success text-center">
    <h2>Correct Answer!!!</h2>
    <button class="btn btn-primary" @click="backQuestion">Question Again</button>
  </div>
</template>

<script>
export default {
  
  methods:{
    backQuestion(){
        this.$emit('confirmed');
    }
  },
};
</script>

<style scoped>

</style>