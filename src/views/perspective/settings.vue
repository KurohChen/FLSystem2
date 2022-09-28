<template>
  <div class="container" v-loading="loading">
    <div class="header">
      <el-steps :active="active" finish-status="success">
        <el-step title="网络参数配置"></el-step>
        <el-step title="基站参数配置"></el-step>
        <el-step title="信道参数配置"></el-step>
        <el-step title="运行日志配置"></el-step>
      </el-steps>
    </div>
    <div class="content">
      <div class="page" id="page1" v-show="active==0">
        <el-row :gutter="24">
          <el-col :span="10">
            <el-form ref="form" :model="form.input1" size="small" label-width="100px">
              <h1>gNB网络参数输入</h1>
              <el-form-item label="用户名">
                <el-input v-model="form.input1.username"></el-input>
              </el-form-item>
              <el-form-item label="密码">
                <el-input v-model="form.input1.password"></el-input>
              </el-form-item>
              <el-form-item label="ip">
                <el-input v-model="form.input1.ipaddress"></el-input>
              </el-form-item>
              <el-form-item label="端口">
                <el-input v-model="form.input1.port"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="10" :offset="2">
            <el-form ref="form" :model="form.input2" size="small" label-width="100px">
              <h1>UE网络参数输入</h1>
              <el-form-item label="用户名">
                <el-input v-model="form.input2.username"></el-input>
              </el-form-item>
              <el-form-item label="密码">
                <el-input v-model="form.input2.password"></el-input>
              </el-form-item>
              <el-form-item label="ip">
                <el-input v-model="form.input2.ipaddress"></el-input>
              </el-form-item>
              <el-form-item label="端口">
                <el-input v-model="form.input2.port"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-button type="primary" @click="reset" size="small" style="margin-top: 40px">重置</el-button>
      </div>
    </div>
    <div class="footer">
      <el-button style="margin-top: 12px;" @click="active--" :disabled='active==0'>上一步</el-button>
      <el-button style="margin-top: 12px;" @click="active++" :disabled='active==3'>下一步</el-button>
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
          input1: {
            username: '',
            password: '',
            ipaddress: '',
            port: ''
          },
          input2: {
            username: '',
            password: '',
            ipaddress: '',
            port: ''
          }
        }
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
      reset() {
        this.form = {
          input1: { username: '', password: '', ipaddress: '', port: '' },
          input2: { username: '', password: '', ipaddress: '', port: '' }
        }
      }
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
