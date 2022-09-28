<template>
  <div class="container" v-loading="loading">
    <div class="content">
      <div class="page">
        <el-row :gutter="24">
          <el-col :span="12">
            <h1>mcs编码表配置</h1>
            <el-form ref="form" :model="form" size="small" label-width="150px">
              <el-form-item label="mcs编码表">
                <el-checkbox v-model="form.checkbox1[0]">64 QAM 表</el-checkbox>
                <el-checkbox v-model="form.checkbox1[1]">256 QAM 表</el-checkbox>
                <el-checkbox v-model="form.checkbox1[2]">低频谱效率 64 QAM 表</el-checkbox>
              </el-form-item>
              <el-form-item label="采样数据">
                <el-input v-model="form.k0"></el-input>
              </el-form-item>
              <el-form-item label="起始SNR值">
                <el-input v-model="form.k2"></el-input>
              </el-form-item>
              <el-form-item label="SNR变化间隔">
                <el-input v-model="form.typeA"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="12">
            <h1>编码可靠性配置</h1>
            <el-form ref="form" :model="form" size="small" label-width="150px">
              <el-form-item label="编码模式选择" style="font-weight: bolder">
                <el-checkbox v-model="form.checkbox2[0]">SISO【无编码】</el-checkbox>
                <el-checkbox v-model="form.checkbox2[1]">2×1Alamouti编码</el-checkbox>
                <el-checkbox v-model="form.checkbox2[2]">3×1STBC编码</el-checkbox>
                <el-checkbox v-model="form.checkbox2[3]">4×1STBC编码</el-checkbox>
              </el-form-item>
              <el-form-item label="控制参数设置" style="font-weight: bolder">
              </el-form-item>
              <el-form-item label="发射功率" :inline='true'>
                <el-row :gutter="12">
                  <el-col :span="5"><el-input v-model="form.nrofDownlinkSlots"><i slot="suffix">dBm</i></el-input></el-col>
                  <el-col :span="2">—</el-col>
                  <el-col :span="5"><el-input v-model="form.nrofDownlinkSlots"><i slot="suffix">dBm</i></el-input></el-col>
                </el-row>
              </el-form-item>
              <el-form-item label="信道带宽">
                <el-input v-model="form.nrofDownlinkSymbols"><i slot="suffix">kHz</i></el-input>
              </el-form-item>
              <el-form-item label="基站-用户距离">
                <el-input v-model="form.nrofUplinkSlots"><i slot="suffix">m</i></el-input>
              </el-form-item>
              <el-form-item label="载波频率">
                <el-input v-model="form.nrofUplinkSymbols"><i slot="suffix">GHz</i></el-input>
              </el-form-item>
              <el-form-item label="仿真参数设置" style="font-weight: bolder">
              </el-form-item>
              <el-form-item label="传输符号量">
                <el-input v-model="form.nrofDownlinkSlots"><i slot="suffix">个</i></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
      </div>
    </div>
    <div class="footer">
      <el-button style="margin-top: 12px;" type="primary" @click="reset">重置</el-button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "vueLC",
    data () {
      return {
        loading: false,
        active: 0,
        form: {
          checkbox1: [false,false,false],
          checkbox2: [false,false],
          
          k0: '',
          k1: '',
          typeA: '',
          typeB: '',
          SLIV: '',

          nrofDownlinkSlots: '',
          nrofDownlinkSymbols: '',
          nrofUplinkSlots: '',
          nrofUplinkSymbols: '',
        },
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
      reset() {
        this.form = {
          checkbox1: [false,false],
          checkbox2: [false,false],
          
          k0: '',
          k1: '',
          typeA: '',
          typeB: '',
          SLIV: '',

          nrofDownlinkSlots: '',
          nrofDownlinkSymbols: '',
          nrofUplinkSlots: '',
          nrofUplinkSymbols: '',
        }
      },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePreview(file) {
        console.log(file);
      },
    }
  }
</script>

<style scoped>
  .container {
    padding: 20px 80px;
    position: relative;
    display: flex;
    flex-direction: column;
    height: 100%;
  }
  .container .header {
    height: 80px;
    width: 100%;
  }
  .container .content {
    position: relative;
    width: 100%;
    flex: 1;
  }
  .container .footer {
    height: 60px;
    width: 100%;
  }
</style>
