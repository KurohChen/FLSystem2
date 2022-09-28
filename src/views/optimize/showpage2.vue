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
        <el-collapse-item title="mcs编码表配置性能展示" name="1">
          <div class="imgBox">
            <div class="imgStarmap" id="textbox">
              {{ text }}
            </div>
            <div class="imgStarmap">
              <img src="../../assets/imgs/kekaoxing1.png" alt="">
            </div>
          </div>
        </el-collapse-item>
        <el-collapse-item title="编码可靠性配置性能展示" name="2">
          <div class="imgBox">
            <div class="imgStarmap">
              <img src="../../assets/imgs/kekaoxing2.png" alt="">
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
        text: 'SNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \nSNR 26.400000: Channel BLER 8.200000e-03 \n SNR 26.600000: Channel BLER 8.00000e-03\n SNR 26.800000: Channel BLER 5.900000e-03\n SNR 27.000000: Channel BLER 4.900000e-03\nSNR 27.200000: Channel BLER 3.900000e-03\n SNR 27.400000: Channel BLER 2.500000e-03\n SNR 27.600000: Channel BLER 1.700000e-03\n......\nSNR 29.000000: Channel BLER 6.000000e-04'
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
    height: 20vw;
    margin-left: 10px;
  }
  .imgStarmap img {
    width: 100%;
    max-height: 100%;
  }
  #textbox {
    white-space: pre;
    overflow-y: auto;
  }
</style>
