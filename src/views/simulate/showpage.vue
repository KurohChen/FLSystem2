<template>
  <div class="container" v-loading="loading">
    <div class="page" id="page1" v-show="state!=3">
      <el-button type="primary" v-show="state==0" @click="start">开始仿真</el-button>
      <span v-show="state==1">正在仿真中，请等待...</span>
      <el-button type="success" v-show="state==2" @click="showdetail">仿真回放</el-button>
    </div>
    <div class="page" id="page2" v-show="state==3">
      <el-button type="primary" @click="state=0" style="margin-bottom: 20px">结束仿真</el-button>
      <el-collapse v-model="activeName" accordion>
        <el-collapse-item title="gNB和UE星座图" name="1">
          <div class="imgBox">
            <div class="imgStarmap">
              <img src="../../assets/imgs/gNB.png" alt="">
            </div>
            <div class="imgStarmap">
              <img src="../../assets/imgs/UE.png" alt="">
            </div>
          </div>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>

<script>
  export default {
    name: "vueLC",
    data () {
      return {
        loading: false,
        state: 0,
        activeName: '1',
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
      start() {
        this.state = 1;
        setTimeout(() => {
          this.state = 2;
        }, 2000);
      },
      showdetail() {
        this.state = 3;
      }
    }
  }
</script>

<style>
</style>

<style scoped>
  .container {
    position: relative;
    width: 100%;
    height: 100%;
  }
  .page {
    position: relative;
    width: 100%;
    height: 100%;
  }
  #page1 {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .imgBox {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
  }
  .imgStarmap {
    position: relative;
    width: 30vw;
    height: 30vw;
    margin-left: 10px;
  }
  .imgStarmap img {
    width: 100%;
    height: 100%;
  }
</style>
