<template>
  <div class="small-wrapper">
    <riseFall :echartsData="echartsData" :width="width" :height="height"></riseFall>
  </div>
</template>

<script>
  import riseFall from 'pages/product/echarts/product-risefall';
  import {rightBarMixin} from 'assets/js/common.js'
  export default {
    name: 'risefall',
    data(){
      return {
        echartsData: {
          xdata: [],
          data: [],
        },
        width: '100%',
        height: '100%',
      }
    },
    mounted() {
      this.renderChart()
    },
    methods: {
      renderChart(){
        //  在这里修改数据
        // mock data
        /*let data1 = [{name: '北京', value: 0},
          {name: '山西', value: 0},
          {name: '陜西', value: 0},
          {name: '河南', value: 0},
          {name: '河北', value: 0},

        ]
        let data2 = [
          {name: '广州', value: 0},
          {name: '湖北', value: 0},
          {name: '山东', value: 0},
          {name: '湖南', value: 0},
          {name: '天津', value: 0},
        ]
        for (let i = 0; i < data1.length; i++) {
          data1[i].value = Math.round(Math.random() * 100)
        }
        for (let i = 0; i < data2.length; i++) {
          data2[i].value = Math.round(Math.random() * 100)
        }
        function sortRise(a,b){
          return a.value - b.value
        }
        function sortFall(a,b){
          return b.value - a.value
        }
        data2.sort(sortRise);
        data1.sort(sortFall);
        let newData =data1.concat(data2);
        newData.forEach((val, index)=>{
            this.echartsData.xdata.push(val.name);
            this.echartsData.data.push(val.value);
        });*/

        this.$xhr.get('apple/production/pAs?TIME_ID=2016&type=121689')
          .then((res)=>{
              this.echartsData.xdata = res.data.xdata
            this.echartsData.data = res.data.data
          })
          .catch((err)=>{
              console.log(err)
          })
      },
    },
    components: {
      riseFall
    }

  };
</script>

<style lang="scss" scoped>
  @import "./../../assets/css/_variable.scss";
  @import "./../../assets/css/_mixin.scss";

  .small-wrapper {
    height: 100%;
    padding: 0 0.2rem;
  }
</style>
