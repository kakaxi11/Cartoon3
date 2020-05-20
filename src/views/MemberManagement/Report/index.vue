<template>
  <div>
      <p>举报用户列表</p>
        <div class="MessageHeader">
    
   
   <el-button type="primary" size="small"><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  
  <el-table
    :data="ReportList"
    border
   >
    <el-table-column
      prop="id"    
      label="编号"
     >
    </el-table-column>
    <el-table-column
      prop="username"
      label="举报者"
   >
    </el-table-column>
    <el-table-column
      prop="reportName"
      label="被举报用户"
     
      >
    </el-table-column>
     <el-table-column
      prop="reportImage"
      label="被举报用户头像"
      >
      <template slot-scope="scope">
        <img :src="scope.row.reportImage" alt="" >
      </template>
    </el-table-column>
    <el-table-column
      prop="reportTypeName"
      label="举报类型"
      >
    </el-table-column>
    <el-table-column
      prop="content"
      label="举报内容"
      >
    </el-table-column>
    <el-table-column
      prop="createTime"
      label="添加时间"
      min-width="140"
      >
      <!-- 作用域插槽 -->
      <template slot-scope="scope">
        <!-- {{scope.row.createTime | dateFormat}} -->
        {{scope.row.createTime | dateFormat}}
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
      :total="total">
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
      ReportList:[],
      total:null
    }
  },
  methods:{
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
  },
  created(){
      this.$http.get('admin/report/get',{params:this.queryInfo}).then(res=>{
       this.ReportList = res.data.data.list
       this.total = res.data.data.total
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
  justify-content:flex-end;
 .refresh{
   margin-left:73%;
 }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}

</style>