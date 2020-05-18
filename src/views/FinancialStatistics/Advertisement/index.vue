<template>
  <div>
      <p>投放回收统计列表</p>
        <div class="MessageHeader">
            <div>
    <el-button type="primary" size="small" plain>选择时间</el-button>
        <el-button type="primary" size="small" plain> <i class="iconfont icon-sousuo"></i>查询</el-button>
            <el-button type="warning" size="small"  class="Excel">导出Excel</el-button>
            </div>

   
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  								
  <el-table
    :data="CartoonList"
    border
    height="733"
  >
    <el-table-column
      prop="id"    
      label="日期"
     >
    </el-table-column>
    <el-table-column
      prop="name"
      label="当日所有新增用户数"
    >
    </el-table-column>
    <el-table-column
      prop="image"
      label="当天充值"
      max-width="90"
      >
      <!-- 作用域插槽 -->
    </el-table-column>
     <el-table-column
      prop="typeName"
      label="3天累计充值"
      >
    </el-table-column>
    <el-table-column
      prop="view"
      label="5天累计充值"
   
      >
    </el-table-column>
    <el-table-column
      prop="isend"
      label="7天累计充值"
    
      >
    </el-table-column>
     <el-table-column
      prop="today"
      label="14天累计充值"
      >
      <!-- 作用域插槽 -->
      
    </el-table-column>
     <el-table-column
      prop="yesterday"
      label="30天累计充值"
      >
      
    </el-table-column>
     <el-table-column
      prop="all"
      label="至今累计充值"
      >
    </el-table-column>
  </el-table>

    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
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
  justify-content:space-between;
  
  div{
     display:flex;
  
  align-items:center;
  }
 .refresh{
   margin-left:73%;
 }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}

</style>