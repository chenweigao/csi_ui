<template>
    <div>
        <el-card
            class="box-card"
            v-for="(form, index) in formList"
            :form="form"
            :key="index"
        >

            <el-form
                ref="form"
                :model="form.data"
                label-width="100px"
                :inline="true"
            >
                <el-button type="info">Command No.{{ index }} </el-button>

                <!-- <el-form-item>

                    <p>{{ index }} : {{ form.data }}</p>
                </el-form-item> -->

                <el-form-item label="Mode">
                    <el-select
                        v-model="form.data.mode"
                        placeholder="mode"
                    >
                        <el-option
                            label="logger"
                            value="logger"
                        ></el-option>
                        <el-option
                            label="injector"
                            value="injector"
                        ></el-option>
                        <el-option
                            label="responder"
                            value="responder"
                        ></el-option>
                        <el-option
                            label="initiator"
                            value="initiator"
                        ></el-option>
                    </el-select>
                </el-form-item>
                <el-button type="default" style="float:right;" icon="el-icon-delete" circle @click="deleteCommand(index)"></el-button>
            </el-form>
            <el-form
                ref="form"
                :model="form.data"
                label-width="100px"
                :inline="true"
                label-position="top"
            >

                <el-form-item label="freq">
                    <el-input v-model="form.data.freq"></el-input>
                </el-form-item>

                <el-form-item
                    label="txcm"
                    v-if="form.data.mode !='logger'"
                >
                    <el-input-number
                        v-model="form.data.txcm"
                        :min="1"
                        :max="7"
                        label="txcm"
                    ></el-input-number>
                </el-form-item>
                <el-form-item label="rxcm">
                    <el-input-number
                        v-model="form.data.rxcm"
                        :min="1"
                        :max="7"
                        label="rxcm"
                    ></el-input-number>
                </el-form-item>
                <el-form-item
                    label="ness"
                    v-if="form.data.mode !='logger'"
                >
                    <el-input-number
                        v-model="form.data.ness"
                        :min="0"
                        :max="2"
                        label="rxcm"
                    ></el-input-number>
                </el-form-item>

                <el-form-item label="pll">
                    <el-input v-model="form.data.pll"></el-input>
                </el-form-item>

                <el-form-item
                    label="Policy"
                    v-if="form.data.mode !='logger'"
                >
                    <el-select
                        v-model="form.data.region"
                        placeholder="Policy"
                    >
                        <el-option
                            label="chansel"
                            value="chansel"
                        ></el-option>
                        <el-option
                            label="fastcc"
                            value="fastcc"
                        ></el-option>
                        <el-option
                            label="reset"
                            value="reset"
                        ></el-option>
                        <el-option
                            label="default"
                            value="default"
                        ></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item
                    label="repeat"
                    v-if="form.data.mode =='injector' || form.data.mode == 'initiator'"
                >
                    <el-input v-model="form.data.repeat"></el-input>
                </el-form-item>
                <el-form-item
                    label="delay"
                    v-if="form.data.mode =='injector' || form.data.mode == 'initiator'"
                >
                    <el-input v-model="form.data.delay"></el-input>
                </el-form-item>
                <el-form-item
                    label="cf"
                    v-if="form.data.mode =='injector' || form.data.mode == 'initiator'"
                >
                    <el-input v-model="form.data.cf"></el-input>
                </el-form-item>
                <el-form-item
                    label="sf"
                    v-if="form.data.mode =='injector' || form.data.mode == 'initiator'"
                >
                    <el-input v-model="form.data.sf"></el-input>
                </el-form-item>
                <el-form-item
                    label="delayed start"
                    v-if="form.data.mode =='injector' || form.mode == 'initiator'"
                >
                    <el-input v-model="form.delayedStart"></el-input>
                </el-form-item>
            </el-form>

            <el-form
                ref="form"
                :model="form.data"
                label-width="100px"
                :inline="true"
                label-position="top"
            >
                <el-form-item>
                    <el-button
                        @click="submit"
                        type="primary"
                        plain
                    >Commit</el-button>
                    <!-- weigao chen built for free in 2019 -->
                </el-form-item>
            </el-form>
        </el-card>
        <el-row>
            <el-col :span="24">
                <el-button id = "addbtn"
                    @click="addCommand"
                    type="success"
                >
                    Add Command
                </el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script>
/* eslint-disable */
// var Form = function(){
//     return {
//         data: {
//           NICId: '',
//           freq: '',
//           txcm: 7,
//           rxcm: 7,
//           ness: 0,
//           pll: '',
//           policy: '',
//           repeat: '',
//           delay: '',
//           cf: '',
//           sf: '',
//           delayedStart: ''
//         }
//       }
// }
/* eslint-enable */
export default {
  data: function () {
    return {
      formList: [],
      form: {
        data: {
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
          delayedStart: ''
        }
      }
    }
  },
  methods: {

    addCommand () {
      //   this.form.commandId = this.formList.length
      //   var form = new Form()

      this.formList.push(JSON.parse(JSON.stringify(this.form)))
      console.log(this.formList)
    },
    submit () {
      console.log('submit' + JSON.stringify(this.formList))
    },
    deleteCommand (index) {
      this.formList.splice(index, 1)
      console.log(JSON.stringify(this.formList))
    }
  }
}
</script>

<style>
.el-col {
  margin-bottom: 20px;
  margin-top: 20px;
}

#addbtn{
    float: right;
}

/* .el-col {
    border-radius: 4px;
  } */
   .item {
      margin: 4px;
    }
</style>
