<template>
  <div>
      <p> 权限列表  </p>   
     <div class="MessageHeader">
       <div>
        
<el-button  size="small" type="primary" ><i class="iconfont icon-tianjia"></i>添加</el-button> 
   <el-button  size="small"  type="primary" >显示全部</el-button>
   <el-button  size="small"  type="warning" >批量删除</el-button></div>
   <el-button size="small" type="primary">刷新</el-button>
    
  </div>


    <p>会员列表</p>
      <el-table
    :data="tableData"
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
      label="oppo"
     
      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="APP应用"

      >
    </el-table-column>
    <el-table-column
      prop="state"
      label="其他（未知渠道）"
      
      >
    </el-table-column>
  </el-table>
   <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[5, 10, 15, 20]"
      :page-size="5"
      layout="total, sizes, prev, pager, next, jumper"
      :total="20">
    </el-pagination>
  </div>
  
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>
.MessageHeader{
  display:flex;
  align-items: center;
  justify-content:space-between;
  div{
    display:flex;
    align-items:center;
  }
 .refresh{
   margin-left:73%;
 }
 .el-button{
     margin-left:20px;
 }
 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}
</style>