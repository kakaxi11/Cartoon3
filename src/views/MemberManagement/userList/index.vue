<template>
  <div>
    <p>会员列表</p>
      <el-table
    :data="userList"
    border
  >
    <el-table-column
      prop="date"    
      label="uid"
     >
    </el-table-column>
    <el-table-column
      prop="userType"
      label="注册来源"
     >
    </el-table-column>
    <el-table-column
      prop="isYk"
      label="注册方式" 
      >
    </el-table-column>
     <el-table-column
      prop="idnumber"
      label="IDnum" 
      >
    </el-table-column>
    <el-table-column
      prop="username"
      label="昵称"
    
      >
    </el-table-column>
    <el-table-column
      prop="score"
      label="书币"
      >
    </el-table-column>
    <el-table-column
      prop="userType"
      label="注册渠道"
      >
    </el-table-column>
    <el-table-column
      prop="userface"
      label="头像"
      >
    </el-table-column>
    <el-table-column
      prop="sex"
      label="性别"
      >
    </el-table-column>
    <el-table-column
      prop="mobile"
      label="手机号"
      >
    </el-table-column>
    <el-table-column
      prop="isvip"
      label="vip"
      >
    </el-table-column>
    <el-table-column
      prop="createTime"
      label="注册时间"
      >
      <template slot-scope="scope">
        {{scope.row.createTime | dateFormat}}
        <!-- 作用于插槽替换默认样式使用filter -->
        </template>
    </el-table-column>
    <el-table-column
      prop="lastLoginTime"
      label="最后登录时间"
      >
       <template slot-scope="scope">
        {{scope.row.lastLoginTime | dateFormat}}
        <!-- 作用于插槽替换默认样式使用filter -->
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
      :current-page="queryInfo.page"
      :page-sizes="[10, 20, 30, 40]"
      :page-size="10"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
  </div>
  
</template>

<script>
export default {
   data(){
     return{
          userList:[],
          queryInfo:{
            page:1,
            size:10
          },
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
      getList(){
         this.$http.get('admin/index/user/list/get',
      {
        params: this.queryInfo
      }
      ).then(res=>{
        this.userList = res.data.data.list
        this.total = res.data.data.total
         this.userList.forEach(item=>      
       {
          item.isYk = item.isYK===1?'游客用户':'注册住户'
          item.userType = item.userType===1?'APP':'快应用'
          item.sex = item.sex===1?'男':'女'
          switch(item.isvip){
                 case 1:item.isvip = "普通"; break;
                 case 2:item.isvip = "包月"; break;
                 case 3:item.isvip = "季度"; break;
                 case 4:item.isvip = "半年"; break;
                 case 5:item.isvip = "包年"; break;
               }                          
               return 
       } 
        )
        
        
      })
      }

   },
   created(){
     this.getList()
   }




}
</script>

<style>

</style>