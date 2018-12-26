<template>
    <div>
        <Layout>
            <Layout>
                <Sider hide-trigger :style="{background: '#fff'}">
                    <Menu active-name="1-2" theme="light" width="auto" :open-names="['1']">
                         <Submenu name="1">
                    <template slot="title">
                        <Icon type="ios-paper" />
                        {{PrjInfos}}
                    </template>
                    <MenuItem  v-for="(item,index) in NameItmes" :name="indexnames(index)">{{item.name}}</MenuItem>
                </Submenu>
                    </Menu>
                </Sider>
                <Layout :style="{padding: '0 24px 24px'}">
                    <Content :style="contstyle">
                        <!-- <Button @click="loadfile()">上传</Button>
                        <Input search enter-button="Send" placeholder="Enter something..." /> -->
                        <Steps :current="current">
                        <Step title="需求背景"></Step>
                        <Step title="功能测试分析"></Step>
                        <Step title="专项测试分析"></Step>
                        <Step title="用户场景分析"></Step>
                        <Step title="完成"></Step>
                        </Steps>
                        <Input v-model="TextValue" type="textarea" placeholder="需求背景描述" />
                        <Button type="primary" @click="next">{{ButtonName}}</Button>
                    </Content>
                </Layout>
            </Layout>
        </Layout>
    </div>
</template>

<script>
  import fs from 'fs'
  // import nedb from 'nedb'
  export default {
    data () {
      return {
        NameItmes: '',
        PrjInfos: '',
        contstyle: {padding: '2px', minHeight: '500px', background: '#fff', position: ''},
        current: 0,
        ButtonName: '下一步',
        TextValue: '',
        TextList: []
      }
    },
    methods: {
      loadfile () {
        this.$electron.ipcRenderer.send('loadfile')
        const _this = this
        this.$electron.ipcRenderer.on('filepath', function (event, arg) {
          console.log(arg[0])
          let filejson = JSON.parse(fs.readFileSync(arg[0], 'utf-8'))
          _this.NameItmes = filejson.item
          _this.PrjInfos = filejson.info.name
        })
      },
      indexnames: function (index) {
        return '1' + String(index + 1)
      },
      next () {
        if (this.current === 3) {
          this.current += 1
          this.ButtonName = '提交'
        } else if (this.current === 5) {

        } else {
          this.TextList[this.current] = this.TextValue
          this.TextValue = ''
          this.current += 1
          console.log(this.TextList)
        }
      }
    }
  }
</script>

<style scoped>
.header {
    position: relative;
    width: 1200px;
    height: 100px
}

</style>