<template>
  <div>
      <p>意见反馈列表</p>
        <div class="MessageHeader">
    <el-button type="warning" size="small">批量删除</el-button>
   
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  
  <el-table
    :data="suggestionList"
    border
 >

							

    <el-table-column
      prop="id"    
      label="编号"
     >
    </el-table-column>
    <el-table-column
      prop="idnumber"
      label="IDnumber"
      >
    </el-table-column>
    <el-table-column
      prop="username"
      label="昵称" 
      >
    </el-table-column>
     <el-table-column
      prop="contact"
      label="联系方式"
      >
    </el-table-column>
    <el-table-column
      prop="content"
      label="反馈内容"  
      >
    </el-table-column>
    <el-table-column
      prop="type"
      label="来源"
      >
    </el-table-column>
      <el-table-column
      prop="addtime"
      label="添加时间"
      >
      <template slot-scope="scope">
        {{scope.row.addtime | dateFormat}}
      </template>
    </el-table-column>
      <el-table-column
      prop="state"
      label="操作"
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
    data(){
        return{
           queryInfo:{
            page:1,
            size:5
          },
          suggestionList:[]
        }
    },
    created(){
      this.$http.get('admin/user/feedback',{params:this.queryInfo}).then(res=>{
       this.suggestionList = res.data.data.list
      })

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
 .refresh{
   margin-left:73%;
 }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}

</style>