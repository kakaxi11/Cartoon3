<template>
  <div>
      <p>充值列表</p>
        <div class="MessageHeader">
        
     <el-input v-model="queryInfo.key" placeholder="用户名|ID 订单号" size="small" clearable></el-input>

   <el-select v-model="value" placeholder="支付状态" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>

<el-select v-model="value" placeholder="支付方式" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
  <el-select v-model="value" placeholder="充值类型" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>

  <el-select v-model="value" placeholder="应用" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
  
  <el-select v-model="value" placeholder="应用" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
    <el-date-picker
      v-model="value1"
      type="daterange"
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      size="small"
      >
    </el-date-picker>



    <el-button type="primary" size="small" @click="SeachKey"><i class="iconfont icon-sousuo"></i>搜索查询</el-button>
   
   <el-button type="primary" size="small" >显示全部</el-button>
   <el-button type="warning" size="small" >导出Excel</el-button>
      <el-button type="primary" size="small" class="refresh"><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  
  <el-table
    :data="payList"
    border
    
    >
    <el-table-column
      prop="id"    
      label="编号"
     >
    </el-table-column>
    <el-table-column
      prop="idnumber"
      label="用户id"
    >
    </el-table-column>
    <el-table-column
      prop="username"
      label="用户名称"    
      >
    </el-table-column>
     <el-table-column
      prop="createTime"
      label="用户注册时间"  
      >
      <template slot-scope="scope">
        {{scope.row.createTime | dateFormat}}
        <!-- 作用域插槽替换默认样式使用filter -->
        </template>
    </el-table-column>
    <el-table-column
      prop="channel"
      label="用户渠道"  
      >
    </el-table-column>
    <el-table-column
      prop="score"
      label="当前书币"    
      >
    </el-table-column>
    <el-table-column
      prop="orderChannel"
      label="充值应用"
      >
    </el-table-column>
    <el-table-column
      prop="orderSn"
      label="订单号"
      min-width="190"
      >
    </el-table-column>
       <el-table-column
      prop="orderBookId"
      label="充值漫画ID"
      >
    </el-table-column>
       <el-table-column
      prop="orderType"
      label="充值类型"
      >
      
    </el-table-column>
       <el-table-column
      prop="orderMoney"
      label="订单金额"
      >
    </el-table-column>
       <el-table-column
      prop="orderType"
      label="订单详情"
      >
    </el-table-column>
       <el-table-column
      prop="orderAddtime"
      label="提交时间"
      >
      <template slot-scope="scope">
        {{scope.row.orderAddtime | dateFormat}}        
      </template>
    </el-table-column>
       <el-table-column
      prop="orderPaytype"
      label="支付方式"
      >
      <template slot-scope="scope">
      <!-- 三元运算嵌套使用 -->
        {{scope.row.orderPaytype===1?"微信":scope.row.orderPaytype===2?"支付宝":"H5支付"}}
      </template>
    </el-table-column>
       <el-table-column
      prop="orderOvertime"
      label="支付时间"
      >
           <template slot-scope="scope">
        {{scope.row.orderOvertime | dateFormat}}        
      </template>
    </el-table-column>
       <el-table-column
      prop="orderState"
      label="订单状态"
      >
    </el-table-column>
  </el-table>

    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="queryInfo.page"
      :page-sizes="[5,10,20,30]"
      :page-size="this.queryInfo.size"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>

  </div>
</template>

<script>
export default {
    data(){
        return{
          total:null,
           queryInfo:{
            type:1,
            page:1,
            size:10,
            key:''     
          },
          payList:[],
           options: [{
          value: '选项1',
          label: '黄金糕'
        }, {
          value: '选项2',
          label: '双皮奶'
        }, {
          value: '选项3',
          label: '蚵仔煎'
        }, {
          value: '选项4',
          label: '龙须面'
        }, {
          value: '选项5',
          label: '北京烤鸭'
        }],
        value: '',
   pickerOptions: {
          shortcuts: [{
            text: '最近一周',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近一个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近三个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit('pick', [start, end]);
            }
          }]
        },
        
        // 开始日期与结束日期
        //转化为参数请求的时间格式,传入queryinfo进行请求。
        value1: '',
        value2: ''
        }
    },
    created(){
      this.getList()
    },
    methods:{
      getList(){
        this.$http.get('admin/order/info/list/get',{params:this.queryInfo}).then(res=>{
       this.payList = res.data.data.list
       this.total = res.data.data.total
       this.payList.forEach(item=>{
           switch(item.orderType){
                 case 1:item.orderType = "充值"; break;
                 case 2:item.orderType = "包月vip"; break;
                 case 3:item.orderType = "季度vip"; break;
                 case 4:item.orderType = "半年vip"; break;
                 case 5:item.orderType = "包年vip"; break;
               }             
       })
       console.log(this.payList);
        })
      },
      //通过页码器内置的方法更改请求参数并获取数据
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
    SeachKey(){
      console.log(this.value1);
      console.log(this.value2);
      
      this.getList()
    }
}
}
</script>
<style lang="less" scoped>
p{
    font-size:13px;
}
.MessageHeader{
  display:flex;
  justify-content:flex-start;
    .el-input{
        width:200px;
    }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
  .el-button{
      margin-left:15px;
  }
}
.el-select{
    width:140px;
    margin:0 3px
}
.refresh{
    margin:0 0 0 250px !important;
}



</style>