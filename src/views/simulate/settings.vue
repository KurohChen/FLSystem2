<template>
  <div class="container" v-loading="loading">
    <div class="content">
      <div class="page">
        <el-row :gutter="24">
          <el-col :span="24">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="配置方式">
                <el-radio v-model="form.method" label="1">选择已有文件</el-radio>
                <el-radio v-model="form.method" label="2">自行设置文件</el-radio>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-row :gutter="24">
          <el-col :span="12">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="选择信道模型" v-show="form.method==1">
                <el-select v-model="form.selectFile" placeholder="请选择">
                  <el-option
                    v-for="item in form.files"
                    :key="item"
                    :label="item"
                    :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="配置文件名称" v-show="form.method==2">
                <el-input v-model="form.fileName"></el-input>
              </el-form-item>
              <el-form-item label="文件导入" v-show="form.method==2">
                <el-upload
                  class="upload-demo"
                  ref="upload2"
                  action="/"
                  :on-preview="handlePreview"
                  :on-remove="handleRemove"
                  :file-list="form.fileList"
                  :auto-upload="false"
                  :limit=1
                  :multiple='false'>
                  <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
                  <!-- <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button> -->
                  <!-- <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div> -->
                </el-upload>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-row :gutter="24">
          <el-col :span="8">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="nb_tx" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.nb_tx"></el-input>
              </el-form-item>
              <el-form-item label="nb_rx" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.nb_rx"></el-input>
              </el-form-item>
              <el-form-item label="nb_taps" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.nb_taps"></el-input>
              </el-form-item>
              <el-form-item label="channel_bandwidth" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.channel_bandwidth"></el-input>
              </el-form-item>
              <el-form-item label="sampling_rate" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.sampling_rate"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="8">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="max_Doppler" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.max_Doppler"></el-input>
              </el-form-item>
              <el-form-item label="amps" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.amps"></el-input>
              </el-form-item>
              <el-form-item label="delays" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.delays"></el-input>
              </el-form-item>
              <el-form-item label="channel_length" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.channel_length"></el-input>
              </el-form-item>
              <el-form-item label="Td" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.Td"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="8">
            <el-form ref="form" :model="form" size="small" label-width="100px">
              <el-form-item label="sampling_rate" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.sampling_rate"></el-input>
              </el-form-item>
              <el-form-item label="aoa" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.aoa"></el-input>
              </el-form-item>
              <el-form-item label="ricean_factor" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.ricean_factor"></el-input>
              </el-form-item>
              <el-form-item label="path_loss_dB" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.path_loss_dB"></el-input>
              </el-form-item>
              <el-form-item label="nb_paths" v-show="form.method==1">
                <el-input :disabled='form.selectFile==""' v-model="form.input.nb_paths"></el-input>
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
          method: '',
          files: [
            'AWGN信道',
            '瑞利信道',
            '莱斯信道',
          ],
          selectFile: '',
          input: {
            nb_tx: '',
            nb_rx: '',
            nb_taps: '',
            channel_bandwidth: '',
            sampling_rate: '',
            max_Doppler: '',
            amps: '',
            delays: '',
            channel_length: ''
          },
          fileName: '',
          fileList: []
        },
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
      reset() {
        this.form = {
          files: [
            'AWGN信道',
            '瑞利信道',
            '莱斯信道',
          ],
          selectFile: '',
          input: {
            nb_tx: '',
            nb_rx: '',
            nb_taps: '',
            channel_bandwidth: '',
            sampling_rate: '',
            max_Doppler: '',
            amps: '',
            delays: '',
            channel_length: ''
          },
          fileName: '',
          fileList: []
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
