<template>
  <div>
      <p>漫画充值统计</p>
        <div class="MessageHeader">
           全局搜索
          <el-input v-model="queryInfo.key" placeholder="漫画ID|漫画名称" size="small" clearable>
          </el-input>
         
          
    <el-button  size="small" type="primary" @click="SeachKey" ><i class="iconfont icon-sousuo" ></i>搜索</el-button>
    <el-button  size="small" type="info" @click="Reset" >重置</el-button>

  </div>
  
  <el-table
    :data="CartoonList"
    border
    height="733"
  >
    <el-table-column
      prop="id"    
      label="id"
     >
    </el-table-column>
    <el-table-column
      prop="name"
      label="漫画名称"
    >
    </el-table-column>
    <el-table-column
      prop="image"
      label="漫画封面"
      max-width="90"
      >
      <!-- 作用域插槽 -->
      <template slot-scope="scope">
       <img :src="scope.row.image" alt="" style="width:60%;height:100px;">
        </template>
    </el-table-column>
     <el-table-column
      prop="typeName"
      label="漫画分类"
      >
    </el-table-column>
    <el-table-column
      prop="view"
      label="点击量"
   
      >
    </el-table-column>
    <el-table-column
      prop="isend"
      label="漫画状态"
    
      >
    </el-table-column>
     <el-table-column
      prop="today"
      label="今日充值"
      >
      <!-- 作用域插槽 -->
      <template slot-scope="scope">
        <p>充值金额:￥{{scope.row.today.sum}}</p>
        <p>充值笔数:{{scope.row.today.count}}</p>
        <p>消费书币:{{scope.row.today.score}}</p>
        </template>
    </el-table-column>
     <el-table-column
      prop="yesterday"
      label="昨日充值"
      >
      <template slot-scope="scope">
          <p>充值金额:￥{{scope.row.yesterday.sum}}</p>
        <p>充值笔数:{{scope.row.yesterday.count}}</p>
        <p>消费书币:{{scope.row.yesterday.score}}</p>
        </template>
    </el-table-column>
     <el-table-column
      prop="all"
      label="累计充值"
      >
      <template slot-scope="scope">
         <p>充值金额:￥{{scope.row.all.sum}}</p>
        <p>充值笔数:{{scope.row.all.count}}</p>
        <p>消费书币:{{scope.row.all.score}}</p>
        </template>
    </el-table-column>
  </el-table>

    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="queryInfo.page"
      :page-sizes="[5, 10, 20, 30]"
      :page-size="queryInfo.size"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>

  </div>
</template>

<script>
export default {
  data(){
        return{
           queryInfo:{
            type:1,
            page:1,
            size:10,
            key:''
          },
          CartoonList:[]
        }
    },
    created(){
      this.getList()
    },
    methods:{
      getList(){
        this.$http.get('admin/cartoon/recharge/info',{params:this.queryInfo}).then(res=>{
       this.CartoonList = res.data.data.list
       console.log(this.CartoonList);
       this.CartoonList.forEach(item=>      
       {
               item.isend = item.isend===1?'完结':'连载中'  
               if(item.isend===3){
                 item="暂停"
               }                     
               return 
       } 
        )
      })
      },
      SeachKey(){
        this.getList()
      },
      Reset(){
        this.queryInfo={
          type:1,
          page:1,
          size:10,
          key:''
        }
        this.getList()
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
  align-items: center;
  
 .refresh{
   margin-left:73%;
 }
 .el-input{
   width:300px;
   margin:0 20px;
 }
 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}
.el-table{
  p{
    color: rgb(236, 111, 111);
    font-size:14px;
    font-weight:600;
    padding:0;
    margin:0;
  }
}

</style>