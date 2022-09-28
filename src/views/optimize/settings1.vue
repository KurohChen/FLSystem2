<template>
  <div class="container" v-loading="loading">
    <div class="content">
      <div class="page">
        <el-row :gutter="24">
          <el-col :span="12">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="minislot配置">
                <el-checkbox v-model="form.checkbox1[0]">基于微时隙配置</el-checkbox>
                <el-checkbox v-model="form.checkbox1[1]">基于时隙配置</el-checkbox>
              </el-form-item>
              <el-form-item label="k0">
                <el-input v-model="form.k0"></el-input>
              </el-form-item>
              <el-form-item label="k2">
                <el-input v-model="form.k2"></el-input>
              </el-form-item>
              <el-form-item label="typeA">
                <el-input v-model="form.typeA"></el-input>
              </el-form-item>
              <el-form-item label="typeB">
                <el-input v-model="form.typeB"></el-input>
              </el-form-item>
              <el-form-item label="SLIV">
                <el-input v-model="form.SLIV"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="12">
            <el-form ref="form" :model="form" size="small" label-width="150px">
              <el-form-item label="子载波配置">
                <el-checkbox v-model="form.checkbox2[0]">30kHz</el-checkbox>
                <el-checkbox v-model="form.checkbox2[1]">120kHz</el-checkbox>
              </el-form-item>
              <el-form-item label="nrofDownlinkSlots">
                <el-input v-model="form.nrofDownlinkSlots"></el-input>
              </el-form-item>
              <el-form-item label="nrofDownlinkSymbols">
                <el-input v-model="form.nrofDownlinkSymbols"></el-input>
              </el-form-item>
              <el-form-item label="nrofUplinkSlots">
                <el-input v-model="form.nrofUplinkSlots"></el-input>
              </el-form-item>
              <el-form-item label="nrofUplinkSymbols">
                <el-input v-model="form.nrofUplinkSymbols"></el-input>
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
