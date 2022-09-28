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
            <el-form ref="form" :model="form1.input1" size="small" label-width="100px">
              <h1>gNB网络参数输入</h1>
              <el-form-item label="用户名">
                <el-input v-model="form1.input1.username"></el-input>
              </el-form-item>
              <el-form-item label="密码">
                <el-input v-model="form1.input1.password"></el-input>
              </el-form-item>
              <el-form-item label="ip">
                <el-input v-model="form1.input1.ipaddress"></el-input>
              </el-form-item>
              <el-form-item label="端口">
                <el-input v-model="form1.input1.port"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="10" :offset="2">
            <el-form ref="form" :model="form1.input2" size="small" label-width="100px">
              <h1>UE网络参数输入</h1>
              <el-form-item label="用户名">
                <el-input v-model="form1.input2.username"></el-input>
              </el-form-item>
              <el-form-item label="密码">
                <el-input v-model="form1.input2.password"></el-input>
              </el-form-item>
              <el-form-item label="ip">
                <el-input v-model="form1.input2.ipaddress"></el-input>
              </el-form-item>
              <el-form-item label="端口">
                <el-input v-model="form1.input2.port"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-button type="primary" @click="reset(1)" size="small" style="margin-top: 40px">重置</el-button>
      </div>
      <div class="page" id="page2" v-show="active==1">
        <el-row :gutter="24">
          <el-col :span="24">
            <el-form ref="form" :model="form2" size="small" label-width="100px">
              <el-form-item label="配置方式">
                <el-radio v-model="form2.method" label="1">选择已有文件</el-radio>
                <el-radio v-model="form2.method" label="2">自行设置文件</el-radio>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-row :gutter="24">
          <el-col :span="12">
            <el-form ref="form" :model="form2" size="small" label-width="100px">
              <el-form-item label="选择文件" v-show="form2.method==1">
                <el-select v-model="form2.selectFile" placeholder="请选择">
                  <el-option
                    v-for="item in form2.files"
                    :key="item"
                    :label="item"
                    :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="配置文件名称" v-show="form2.method==2">
                <el-input v-model="form2.fileName"></el-input>
              </el-form-item>
              <el-form-item label="文件导入" v-show="form2.method==2">
                <el-upload
                  class="upload-demo"
                  ref="upload2"
                  action="/"
                  :on-preview="handlePreview"
                  :on-remove="handleRemove"
                  :file-list="form2.fileList"
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
          <el-col :span="12">
            <el-form ref="form" :model="form2" size="small" label-width="100px">
              <el-form-item label="serveraddr" v-show="form2.method==1">
                <el-input :disabled='form2.selectFile==""' v-model="form2.input.serveraddr"></el-input>
              </el-form-item>
              <el-form-item label="serverport" v-show="form2.method==1">
                <el-input :disabled='form2.selectFile==""' v-model="form2.input.serverport"></el-input>
              </el-form-item>
              <el-form-item label="option" v-show="form2.method==1">
                <el-input :disabled='form2.selectFile==""' v-model="form2.input.option"></el-input>
              </el-form-item>
              <el-form-item label="modelname" v-show="form2.method==1">
                <el-input :disabled='form2.selectFile==""' v-model="form2.input.modelname"></el-input>
              </el-form-item>
              <el-form-item label="IQfile" v-show="form2.method==1">
                <el-input :disabled='form2.selectFile==""' v-model="form2.input.IQfile"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-button  v-show="form2.method!=''" type="primary" @click="reset(2)" size="small" style="margin-top: 40px">重置</el-button>
      </div>
      <div class="page" id="page3" v-show="active==2">
        <el-row :gutter="24">
          <el-col :span="24">
            <el-form ref="form" :model="form3" size="small" label-width="100px">
              <el-form-item label="配置方式">
                <el-radio v-model="form3.method" label="1">选择已有文件</el-radio>
                <el-radio v-model="form3.method" label="2">自行设置文件</el-radio>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-row :gutter="24">
          <el-col :span="12">
            <el-form ref="form" :model="form3" size="small" label-width="100px">
              <el-form-item label="选择信道模型" v-show="form3.method==1">
                <el-select v-model="form3.selectFile" placeholder="请选择">
                  <el-option
                    v-for="item in form3.files"
                    :key="item"
                    :label="item"
                    :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="配置文件名称" v-show="form3.method==2">
                <el-input v-model="form3.fileName"></el-input>
              </el-form-item>
              <el-form-item label="文件导入" v-show="form3.method==2">
                <el-upload
                  class="upload-demo"
                  ref="upload2"
                  action="/"
                  :on-preview="handlePreview"
                  :on-remove="handleRemove"
                  :file-list="form3.fileList"
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
            <el-form ref="form" :model="form3" size="small" label-width="100px">
              <el-form-item label="nb_tx" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.nb_tx"></el-input>
              </el-form-item>
              <el-form-item label="nb_rx" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.nb_rx"></el-input>
              </el-form-item>
              <el-form-item label="nb_taps" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.nb_taps"></el-input>
              </el-form-item>
              <el-form-item label="channel_bandwidth" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.channel_bandwidth"></el-input>
              </el-form-item>
              <el-form-item label="sampling_rate" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.sampling_rate"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="8">
            <el-form ref="form" :model="form3" size="small" label-width="100px">
              <el-form-item label="max_Doppler" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.max_Doppler"></el-input>
              </el-form-item>
              <el-form-item label="amps" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.amps"></el-input>
              </el-form-item>
              <el-form-item label="delays" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.delays"></el-input>
              </el-form-item>
              <el-form-item label="channel_length" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.channel_length"></el-input>
              </el-form-item>
              <el-form-item label="Td" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.Td"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="8">
            <el-form ref="form" :model="form3" size="small" label-width="100px">
              <el-form-item label="sampling_rate" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.sampling_rate"></el-input>
              </el-form-item>
              <el-form-item label="aoa" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.aoa"></el-input>
              </el-form-item>
              <el-form-item label="ricean_factor" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.ricean_factor"></el-input>
              </el-form-item>
              <el-form-item label="path_loss_dB" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.path_loss_dB"></el-input>
              </el-form-item>
              <el-form-item label="nb_paths" v-show="form3.method==1">
                <el-input :disabled='form3.selectFile==""' v-model="form3.input.nb_paths"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-button  v-show="form3.method!=''" type="primary" @click="reset(3)" size="small" style="margin-top: 40px">重置</el-button>
      </div>
      <div class="page" id="page4" v-show="active==3">
        <el-row :gutter="24">
          <h1>设置日志打印级别</h1>
          <el-col :span="12">
            <el-form ref="form" :model="form4" size="small" label-width="150px">
              <el-form-item label="global_log_level">
                <el-radio v-model="form4.global_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.global_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.global_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.global_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="hw_log_level">
                <el-radio v-model="form4.hw_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.hw_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.hw_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.hw_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="phy_log_level">
                <el-radio v-model="form4.phy_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.phy_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.phy_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.phy_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="mac_log_level">
                <el-radio v-model="form4.mac_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.mac_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.mac_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.mac_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="rlc_log_level">
                <el-radio v-model="form4.rlc_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.rlc_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.rlc_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.rlc_log_level" label="3">debug</el-radio>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="12">
            <el-form ref="form" :model="form4" size="small" label-width="150px">
              <el-form-item label="pdcp_log_level">
                <el-radio v-model="form4.pdcp_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.pdcp_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.pdcp_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.pdcp_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="rrc_log_level">
                <el-radio v-model="form4.rrc_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.rrc_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.rrc_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.rrc_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="ngap_log_level">
                <el-radio v-model="form4.ngap_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.ngap_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.ngap_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.ngap_log_level" label="3">debug</el-radio>
              </el-form-item>
              <el-form-item label="f1ap_log_level">
                <el-radio v-model="form4.f1ap_log_level" label="0">不变</el-radio>
                <el-radio v-model="form4.f1ap_log_level" label="1">info</el-radio>
                <el-radio v-model="form4.f1ap_log_level" label="2">warming</el-radio>
                <el-radio v-model="form4.f1ap_log_level" label="3">debug</el-radio>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
        <el-button type="primary" @click="reset(4)" size="small">重置</el-button>
      </div>
    </div>
    <div class="footer">
      <el-button @click="active--" :disabled='active==0'>上一步</el-button>
      <el-button @click="active++" :disabled='active==3'>下一步</el-button>
      <!-- <el-button @click="submit" type="primary" v-show="active==3">保存配置</el-button> -->
    </div>
  </div>
</template>

<script>
  export default {
    name: "vueLC",
    data () {
      return {
        loading: false,
        active: 3,
        form1: {
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
        },
        form2: {
          method: '',
          files: [
            './gnb.band78.tm1.106PRB.usrpb210.conf',
            './gnb.band78.tm1.24PRB.usrpb210.conf',
            './gnb.sa.band78.f1.106PRB.usrpb210.conf',
            './gnb.sa.band41.f1.106PRB.usrpb210.conf',
          ],
          selectFile: '',
          input: {
            serveraddr: '',
            serverport: '',
            option: '',
            modelname: '',
            IQfile: '',
          },
          fileName: '',
          fileList: []
        },
        form3: {
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
        form4: {
          global_log_level: '0',
          hw_log_level: '0',
          phy_log_level: '0',
          mac_log_level: '0', 
          rlc_log_level: '0', 
          pdcp_log_level: '0',
          rrc_log_level: '0', 
          ngap_log_level: '0',
          f1ap_log_level: '0',
        }
      }
    },
    mounted() {
      this.loading = false;
    },
    methods:{
      reset(index) {
        if(index==1) {
          this.form1 = {
            input1: { username: '', password: '', ipaddress: '', port: '' },
            input2: { username: '', password: '', ipaddress: '', port: '' }
          }
        } else if(index==2) {
          this.form2 = {
            files: [
              './gnb.band78.tm1.106PRB.usrpb210.conf',
              './gnb.band78.tm1.24PRB.usrpb210.conf',
              './gnb.sa.band78.f1.106PRB.usrpb210.conf',
              './gnb.sa.band41.f1.106PRB.usrpb210.conf',
            ],
            selectFile: '',
            input: {
              serveraddr: '',
              serverport: '',
              option: '',
              modelname: '',
              IQfile: '',
            },
            fileName: '',
            fileList: []
          }
        } else if(index==3) {
          this.form3 = {
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
        } else if(index==4) {
          this.form4 = {
            global_log_level: '0',
            hw_log_level: '0',
            phy_log_level: '0',
            mac_log_level: '0', 
            rlc_log_level: '0', 
            pdcp_log_level: '0',
            rrc_log_level: '0', 
            ngap_log_level: '0',
            f1ap_log_level: '0',
          }
        }
      },
      // submitUpload() {
      //   this.$refs.upload.submit();
      // },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePreview(file) {
        console.log(file);
      },
      submit() {

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
