<template>
  <div>
    <h1>父组件：{{content1}}</h1>
    <h1>父组件：{{content2}}</h1>
    <el-button @click="toChild">父组件传参子组件</el-button>
    <child-comp :content1="content1" @getParamFromChild="getFromChild"></child-comp>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: "test",
    data() {
      return {
        content1: "",
        content2: ""
      }
    },
    created() {
      //console.log(this.info)
    },
    mounted() {
      //axios.get('https://api.coindesk.com/v1/bpi/currentprice.json').then(response => (this.info = response))
    },
    methods: {
      toChild() {
        this.content1 = "父组件的参数"
      },
      getFromChild(param){
        this.content2 = param.title
      }
    },
    components: {
      "child-comp":
        {
          props: ['content1'],
          methods:{
            toFather(){
              this.$emit("getParamFromChild",this.content2)
            }
          },
          data(){
            return {
              content2:{
                title:"子组件多参数",
                pageNum:1,
                pageSize:5
              }
            }
          },
          template: "<div>" +
            "<h1>子组件：{{content1}}</h1>" +
            "<h1>子组件：{{content2.title}}{{content2.pageNum}}</h1>" +
            "<el-button @click='toFather'>子组件传参父组件</el-button>" +
            "</div>"
        }
    }
  }
</script>

<style scoped>

</style>
