<template>
  <div>
      <p>充值统计图表</p>
        <div class="MessageHeader">
        <div>

          <el-date-picker
      v-model="value1"
      type="daterange"
      size="small"
      range-separator="至"
      start-placeholder="开始日期"
      value-format="yyyy-MM-dd"   
      end-placeholder="结束日期"
      @change="change"
      >
    </el-date-picker>

            <el-button type="primary" size="small" @click="Search"><i class="iconfont icon-sousuo"></i>查询日期</el-button>
        </div> 
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>


 <el-row :gutter="20">
   <!-- 使用昨日的日期作为参数然后渲染 -->
   <!-- 使用这个月的日期作为参数渲染到 -->
  <el-col :span="6"><div class="bg">昨日充值</div></el-col>
  <el-col :span="6"><div class="bg">今日充值</div></el-col>
  <el-col :span="6"><div class="bg">本月充值</div></el-col>
  <el-col :span="6"><div class="bg">总充值</div></el-col>
</el-row>

    <el-row :gutter="20">
  <el-col :span="6"><div class="grid-content bg-blue">
    
       <div >
<!-- 取消Lineheight -->
   <p>app充值</p>
    <!-- 请求时出现了报错的问题，把请求变为获取单个对象而不是嵌套对象时报错消失 -->
 <i>充值金额:</i> {{payTotal.sum}}
<i>完成订单数:</i>{{payTotal.count}}
   </div>
      </div></el-col>
  <el-col :span="6"><div class="grid-content bg-aqua">
         <div >
<!-- 取消Lineheight -->
   <p>app充值</p>
 <i>充值金额:</i> {{payTotal.sum}}
<i>完成订单数:</i>{{payTotal.count}}
   </div>
      </div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple">  
     <div >
<!-- 取消Lineheight -->
   <p>app充值</p>
 <i>充值金额:</i> {{payTotal.sum}}
<i>完成订单数:</i>{{payTotal.count}}
   </div></div></el-col>
  <el-col :span="6"><div class="grid-content bg-green">  
   <div >
<!-- 取消Lineheight -->
   <p>app充值</p>
 <i>充值金额:</i> {{payTotal.sum}}
<i>完成订单数:</i>{{payTotal.count}}
   </div></div></el-col>
</el-row>
  <el-row :gutter="20">
  <el-col :span="6"><div class="grid-content bg-blue">
   <div >
<!-- 取消Lineheight -->
   <p>快应用充值</p>
 <i>充值金额:</i> {{payTotal.sum}}
<i>完成订单数:</i>{{payTotal.count}}
   </div>
    </div></el-col>
  <el-col :span="6"><div class="grid-content bg-aqua">
     <div >
<!-- 取消Lineheight -->
   <p>快应用充值</p>
 <i>充值金额:</i>{{payTotal.sum}}
 <i>完成订单数:</i>{{payTotal.count}}
   </div>
    </div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple">
      <div >
<!-- 取消Lineheight -->
   <p>快应用充值</p>
 <i>充值金额:</i>{{payTotal.sum}}
 <i>完成订单数:</i>{{payTotal.count}}
   </div>
    </div></el-col>
  <el-col :span="6"><div class="grid-content bg-green">
   <div >
<!-- 取消Lineheight -->
   <p>快应用充值</p>
 <i>充值金额:</i> {{payTotal.sum}}
 <i>完成订单数:</i>{{payTotal.count}}
   </div>
      
    </div></el-col>
</el-row>
  
<lineChar></lineChar>
    

    <el-table
    :data="payList"
    border
    >
    <el-table-column
      prop="date"    
      label="日期"
     >
    </el-table-column>
    <el-table-column
      prop="allMoney"
      label="总充值金额"
     >
    </el-table-column>
    <el-table-column
      prop="allOrderNumber"
      label="总支付订单数"
      
      >
    </el-table-column>
     <el-table-column
      prop="state"
      label="app总充值"
     
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="app支付订单数"
      
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="快应用总充值"
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="快应用支付订单数"
      >
    </el-table-column>
    <el-table-column
      prop="wechatMoney"
      label="微信APP支付金额"
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="微信H5支付金额"
      >
    </el-table-column>
    <el-table-column
      prop="aliMoney"
      label="支付宝金额"
      >
    </el-table-column>
  </el-table>

     <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="queryInfo.page"
      :page-sizes="[5,10, 20, 30]"
       :page-size="queryInfo.size"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
 
 

  </div>
</template>

<script>
import lineChar from '@/components/Linechar.vue'
export default {
  name: 'hello',
  data () {
    return {
      queryInfo:{
        type:1,
        page:1,
        size:10,
        start:'2020-3-1',
        end:'2020-5-1'
      },
     
      total:null,
      payList:[],
      payTotal:{},
      //充值机录
       pickerOptions: {
          disabledDate(time) {
            return time.getTime() > Date.now();
          },
          shortcuts: [{
            text: '今天',
            onClick(picker) {
              picker.$emit('pick', new Date());
            }
          }, {
            text: '昨天',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit('pick', date);
            }
          }, {
            text: '一周前',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', date);
            }
          }]
        },
        value1:[],
    }
  },
  components:{
      lineChar
  },
  created(){
    this.getList()
  this.getFastappList()
  },
  mounted(){

    
    // this.drawLine();
  },
  methods: {
    Search(){
      this.getList()
    },
    change(){
      this.queryInfo.start = this.value1[0],
      this.queryInfo.end = this.value1[1]
    },
    getList(){
         this.$http.get('admin/recharge/info',{params:this.queryInfo}
      ).then(res=>{
        this.payList = res.data.data.list
        this.total = res.data.data.total
        // console.log(this.payList);
      })
    },
    //获取充值数据
    getFastappList(){
      this.$http.get('admin/recharge/log/get').then(res=>{
       this.payTotal = res.data.data.today
        console.log(this.payTotal);
        
      })
    },
     handleSizeChange(newsize){
        console.log(newsize);
        this.queryInfo.page = 1
        this.queryInfo.size = newsize;
        this.getList()
      },
      handleCurrentChange(newpage){
        this.queryInfo.page=newpage
        this.getList()
      },
//     drawLine(){
//         // 基于准备好的dom，初始化echarts实例
//         let myChart = this.$echarts.init(document.getElementById('myChart'))

// // this.testRes = res.responBody.map(item => {
// //      let jsonData = {}
// //      jsonData.name = item.adminArea
// //      jsonData.value = item.orgNum 
// //      jsonData.regCapital = item.regCapital 
    
// //      return jsonData
// // })

//         // 绘制图表
//         myChart.setOption({
//             title: { text: '用户折线图' },
//             tooltip: {
//     trigger: 'item',
//     formatter: function(a) {
//         //进行格式处理
//         return (
//             `${a['name']}</br>机构数量: ${a['value']} (${a['data'].orgNum}%)</br>注册资金: ${a['data'].regCapital} 亿元 (${a['data'].regCapitalPercent}%)</br>职工人数: ${a['data'].orgNum} (${a['data'].employeeNumPercent}%)`
//         )
//     }
// },

//             xAxis: {
//                 data: ["2020-05-06","2020-05-07","2020-05-08","2020-05-09","2020-05-06"]
//             },
//             yAxis: {},
//             //series用于设置多个折线图
//             series: [
//                 {
//                     type:'line',
//                     data:this.testRes
//                 },
//                 {
//                     type:'line',
//                     data:this.testLes
//                 }
//             ]
//         });
//     }
  }
}
</script>

<style lang="less" scoped>
.el-col{
  div{
  p{
    font-size:14px;
    margin-bottom:60px;
}
  font-size:27px;
  font-weight:600;
  i{
    font-size:14px;
    font-weight:500;
    margin:0 15px;
  }
}

}
.MessageHeader{
  display:flex;
  justify-content:space-between;
  div{
    display:flex;
    align-items: center;
  }
 .refresh{
   margin-left:73%;
 }
 .el-button{
   margin-left:5px;
 }
 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}
  .el-row {
    margin-bottom: 20px;
    margin-top:10px;
    color:white;
    text-align:center;

    &:last-child {
      margin-bottom: 0;
     
    }
  }
  .el-col {
    border-radius: 4px;
  
    
    
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: -webkit-gradient(linear, left bottom, left top, color-stop(0, #605ca8), color-stop(1, #9491c4)) !important;
  }
  .bg-green{
    background:  -webkit-gradient(linear, left bottom, left top, color-stop(0, #00a65a), color-stop(1, #00ca6d)) !important;
  }
  .bg-blue {
    background-color: #0073b7 !important;
}
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
    height:150px;
    line-height:150px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
    .bg{
        font-size:19px !important;
        font-weight:500 !important;
        color: rgb(66, 66, 66);
    }
    .bg-aqua{
        background: -webkit-gradient(linear, left bottom, left top, color-stop(0, #00c0ef), color-stop(1, #14d1ff)) !important;
    }
</style>