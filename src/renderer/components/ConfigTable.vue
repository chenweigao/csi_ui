<template>
    <div>
        <h2>NIC Information Table</h2>
        <el-table
            :data="formList"
            stripe
            style="width: 100%"
        >
            <el-table-column type="expand">
                <template slot-scope="props">
                    <el-form
                        label-position="left"
                        inline
                        class="demo-table-expand"
                    >
                        <el-form-item label="txcm">
                            <span>{{ props.row.data.txcm }}</span>
                        </el-form-item>
                        <el-form-item label="rxcm">
                            <span>{{ props.row.data.rxcm }}</span>
                        </el-form-item>
                        <el-form-item label="ness">
                            <span>{{ props.row.data.ness }}</span>
                        </el-form-item>
                        <el-form-item label="pll">
                            <span>{{ props.row.data.pll }}</span>
                        </el-form-item>
                        <el-form-item label="policy">
                            <span>{{ props.row.data.policy }}</span>
                        </el-form-item>
                        <el-form-item label="repeat">
                            <span>{{ props.row.data.repeat }}</span>
                        </el-form-item>
                        <el-form-item label="delay">
                            <span>{{ props.row.data.delay }}</span>
                        </el-form-item>
                        <el-form-item label="cf">
                            <span>{{ props.row.data.cf }}</span>
                        </el-form-item><el-form-item label="sf">
                            <span>{{ props.row.data.sf }}</span>
                        </el-form-item><el-form-item label="delayed start">
                            <span>{{ props.row.data.delayedStart }}</span>
                        </el-form-item>
                    </el-form>
                </template>
            </el-table-column>
            <el-table-column
                label="NICId"
                prop="data.NICId"
            >
            </el-table-column>
            <el-table-column
                label="Mode"
                prop="data.mode"
            >
            </el-table-column>
            <el-table-column
                label="frequence"
                prop="data.freq"
            >
            </el-table-column>
        </el-table>
    </div>
</template>
<script>
import CardConfig from './CardConfig'
export default {
  components: { CardConfig },
  props: ['formList'],
  data () {
    return {
    }
  },
  methods: {
    sendConfig (config) {
      console.log('config is:' + config)
      this.formList = config
      console.log(this.formList)
    }
  }

}
</script>
<style>
  .demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
</style>