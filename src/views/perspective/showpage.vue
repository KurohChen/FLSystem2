<template>
  <div class="container" v-loading="loading">
    <el-empty description="暂未开发"></el-empty>
  </div>
</template>

<script>
  export default {
    name: "vueLC",
    data () {
      return {
        loading: false
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
    }
  }
</script>

<style>
  .el-main {
    padding: 10px 20px;
  }
</style>

<style scoped>
  .container {
    position: relative;
  }
  .pagination {
    position: absolute;
    right: 20px;
  }
</style>
