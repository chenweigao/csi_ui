<template>
    <div>
        <el-form
            :inline="true"
            :model="formInline"
            class="demo-form-inline"
        >
            <el-form-item label="array_prepare">
                <el-input
                    v-model="formInline.card"
                    placeholder="array id"
                ></el-input>
            </el-form-item>

            <el-form-item label="channel parameter">
                <el-input
                    v-model="formInline.cardString"
                    placeholder="parameter"
                    value="jskjasdjk"
                ></el-input>
            </el-form-item>

            <el-form-item>
                <el-button
                    type="primary"
                    @click="onSubmit"
                >Add</el-button>
            </el-form-item>
        </el-form>

        <el-card class="box-card">
            Card Parameter:
            <h3>{{ nicInfo.parameter }}</h3>
            Card Information List:
            <h3></h3>

            <h3
                v-for="nic in nicInfo.ids"
                :key="nic.index"
                class="text item"
            >
                {{ nic }}
                <!-- <el-button icon="el-icon-delete" circle></el-button> -->
                <i
                    class="el-icon-delete"
                    @click="deleteCard(nic.index)"
                    style="float:right"
                ></i>
            </h3>
        </el-card>
        <card-config></card-config>
        <el-card class="box-card">
            <div
                slot="header"
                class="clearfix"
            >
                <span>Config Json:</span>
                <el-button
                    style="float: right; padding: 3px 0"
                    type="text"
                    @click="fetchState"
                >Send</el-button>
            </div>
            <div>
                {{ configResult }}
            </div>
        </el-card>

    </div>
</template>
<script>
import CardConfig from './CardConfig'
var dgram = require('dgram')
var udpClient = dgram.createSocket('udp4')
export default {
  components: { CardConfig },
  data () {
    return {
      fromList: [1, 2, 3],
      formInline: {
        card: '',
        cardString: ''
      },
      nicInfo: {
        ids: [],
        parameter: ''
      },
      modes: ['logger', 'injector', 'responder', 'initiator'],
      selectedCard: '',
      selectedMode: 'responder',
      selectedPolicy: '',
      selectedNicID: '',
      form: {
        NICId: '',
        freq: '',
        txcm: 7,
        rxcm: 7,
        ness: 0,
        pll: '',
        policy: '',
        repeat: '',
        delay: '',
        cf: '',
        sf: '',
        delayedStart: '',
        mode: ''
      },
      configResult: []
    }
  },
  methods: {
    onSubmit () {
      this.nicInfo.ids.push(this.formInline.card)
      this.nicInfo.parameter = this.formInline.cardString
      console.log(this.nicInfo)
    },
    deleteCard (index) {
      this.nicInfo.ids.splice(index, 1)
      console.log(this.nicInfo.ids)
    },
    configCard () {
      this.form.mode = this.selectedMode
      this.form.NICId = this.formInline.card
      for (var key in this.form) {
        if (this.form[key] === '') {
          delete this.form[key]
        }
      }
      this.configResult.push(this.form)
      console.log(this.configResult)
      //   var SendBuff = JSON.stringify(this.configResult)
      //   var SendLen = SendBuff.length
      //   udpClient.send(SendBuff, 0, SendLen, 7788, '127.0.0.1')
    },
    fetchState () {
      var SendBuff = JSON.stringify(this.configResult)
      var SendLen = SendBuff.length
      udpClient.send(SendBuff, 0, SendLen, 7788, '127.0.0.1')
    }

  },
  created () {
    var self = this
    udpClient.on('message', function (msg, rinfo) {
      try {
        var data = JSON.parse(msg)
        if (data) {
          self.processList = data
        }
      } catch (e) { }
      console.log(
        `receive message from ${rinfo.address}:${rinfo.port}：${msg}`
      )
    })
    // window.setInterval(self.fetchState, 1000)
  }
}
</script>