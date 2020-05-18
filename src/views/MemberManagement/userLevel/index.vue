<template>
  <div>
      <p>会员等级列表</p>
        <div class="MessageHeader">
            <div>
<el-button type="primary" size="small" >显示全部</el-button>
    <el-button type="primary" size="small" ><i class="iconfont icon-tianjia"></i>添加</el-button>
     <el-button type="warning" size="small" >批量删除</el-button>
            </div>
   <el-button type="primary" size="small"><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  
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
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>

  </div>
</template>

<script>
export default {

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