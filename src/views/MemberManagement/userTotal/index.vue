<template>
    <div>
       <div class="MessageHeader">
    <div>
         <el-button size="small" type="primary" >选择时间</el-button>
    <el-button  size="small" type="primary" ><i class="iconfont icon-sousuo"></i>查询</el-button>
    </div>
   
    <el-button type="primary" size="small" class="refresh"><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
    
    <el-card class="card-box">
        <h1>用户概况</h1>
    <div>
        <span>
            <p class="weight">{{userTotal.usersNumber}}</p>
            <p>总用户人数</p>
        </span>
        <span>
            <p class="weight">{{userTotal.usersNumber}}</p>
            <p>总用户人数</p>
        </span>
    </div>
    </el-card>
  <Linechar></Linechar>
   
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
      prop="name"
      label="总新增用户"
   >
    </el-table-column>
    <el-table-column
      prop="address"
      label="头条"

      >
    </el-table-column>
     <el-table-column
      prop="state"
      label="广点通"
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="oppo"
      >
    </el-table-column>
    <el-table-column
      prop="appNumber"
      label="APP应用"
      >
    </el-table-column>
     <el-table-column
      prop="state"
      label="其他(未知渠道)"
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
import Linechar from '@/components/Linechar.vue'
export default {
  name: 'hello',
  data () {
    return {
    //  testRes:[
    //       {
    //           name:"重庆",  //name点的名称
    //           value:369,   //value在y轴的位置高度
    //           orgNum:15485,
    //           regCapital:1907
    //       },  
    //       {
    //           name:"上海",
    //           value:276,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //         {
    //           name:"文档",
    //           value:563,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //         {
    //           name:"sss",
    //           value:613,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //        {
    //           name:"kss",
    //           value:513,
    //           orgNum:15485,
    //           regCapital:1907
    //       }
    //   ],
    //   testLes:[
    //       {
    //           name:"重庆",  //name点的名称
    //           value:249,   //value在y轴的位置高度
    //           orgNum:15485,
    //           regCapital:1907
    //       },  
    //       {
    //           name:"上海",
    //           value:336,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //         {
    //           name:"文档",
    //           value:453,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //         {
    //           name:"sss",
    //           value:343,
    //           orgNum:15485,
    //           regCapital:1907
    //       },
    //        {
    //           name:"kss",
    //           value:533,
    //           orgNum:15485,
    //           regCapital:1907
    //       }
    //   ],
      userTotal:[],
      queryInfo:{
        type:1,
        page:1,
        size:10,
        start:'2020-3-1',
        end:'2020-5-1'
      },
       total:null,
        payList:[],
    }
  },
  components:{
    Linechar
  },
   created(){
      this.$http.get('admin/index').then(res=>{
          console.log(res);
          this.userTotal = res.data.data
      })
     this.getList()
   },
  mounted(){
    this.drawLine();
  },
  methods: {
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
     getList(){
         this.$http.get('admin/index/register/detail'
      ).then(res=>{
        console.log(res);
        
        this.payList = res.data.data
        this.total = res.data.data.length
        console.log(this.payList);
      })
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
.MessageHeader{
  display:flex;
  justify-content:space-between;
  div{
    display:flex;
    align-items:center;
  }
 .refresh{
 }
  padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}
.card-box{
    margin-top:7px;
    height:130px;
    h1{
        transform:translateY(-30px);
        font-weight:500;
    }
    div{
         transform:translateY(-35px);
        display:flex;
        justify-content:space-around;
        font-size:14px;
        .weight{
            font-weight:600;
        }
    }
    margin-bottom:20px;
}
</style>