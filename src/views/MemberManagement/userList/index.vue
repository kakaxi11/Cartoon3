<template>
  <div>
    <p>会员列表</p>
      <div class="MessageHeader">
            <div>
      <el-input size="small" style="width:230px" placeholder="用户ID | IDnumber |昵称|手机号" v-model="queryInfo.Key" clearable></el-input>

        <el-button type="primary" size="small"  @click="Search"> <i class="iconfont icon-sousuo"></i>查询</el-button>
            <el-button type="warning" size="small"  class="Excel" @click="exportExcel">导出Excel</el-button>
            </div>
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
      <el-table
    :data="userList"
    border
    id="out-table"
  >
    <el-table-column
      prop="uid"    
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
      <template slot-scope="scope">
        <img :src="scope.row.userface" alt="" style="width:65%">
      </template>
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
      min-width="140"
      >
      <template slot-scope="scope">
        {{scope.row.createTime*1000 | dateFormat}}
        <!-- 作用于插槽替换默认样式使用filter -->
        </template>
    </el-table-column>
    <el-table-column
      prop="lastLoginTime"
      label="最后登录时间"
      min-width="140"
      >
       <template slot-scope="scope">
        {{scope.row.lastLoginTime | dateFormat}}
        <!-- 作用于插槽替换默认样式使用filter -->
        </template>
    </el-table-column>
    <el-table-column
      prop="state"
      label="操作"
      min-width="100"
      >
       <template slot-scope="scope">
        <el-button size="mini" type="primary" icon="el-icon-view" @click="view(scope.row.id)"></el-button>
      <el-button size="mini" type="danger" icon="el-icon-delete" @click="remove(scope.row.id)"></el-button>
    </template>
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
    <el-dialog
  title="用户明细"
  :visible.sync="dialogVisible"
  width="60%"
  :before-close="handleClose">
  <el-table :data="gridData" title="充值明细">
        <el-table-column label="充值明细">
          <el-table-column property="date" label="日期" width="150"></el-table-column>
    <el-table-column property="name" label="姓名" width="200"></el-table-column>
    <el-table-column property="address" label="地址"></el-table-column>
   </el-table-column>
  </el-table>
  <el-table :data="signList">
<el-table-column property="date" label="签到明细" width="150">
     <el-table-column property="day" label="日期" width="150"></el-table-column>
    <el-table-column property="coupon" label="签到" width="200"></el-table-column>
    <el-table-column property="status" label="地址">
      <template slot-scope="scope">
        {{scope.row.status===true?'是':'否'}} 
      </template>
    </el-table-column>
</el-table-column>
  </el-table>
  <el-table :data="gridData">
<el-table-column property="date" label="章节明细" width="150">
     <el-table-column property="date" label="日期" width="150"></el-table-column>
    <el-table-column property="name" label="姓名" width="200"></el-table-column>
    <el-table-column property="address" label="地址">
    </el-table-column>
</el-table-column>
  </el-table>
  <el-table :data="gridData">
<el-table-column property="date" label="签到明细" width="150">
     <el-table-column property="date" label="日期" width="150"></el-table-column>
    <el-table-column property="name" label="姓名" width="200"></el-table-column>
    <el-table-column property="address" label="地址"></el-table-column>
</el-table-column>
  </el-table>
  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
</el-dialog>
  </div>
</template>
<script>
import FileSaver from "file-saver";
import XLSX from "xlsx";

export default {
   data(){
     return{
       dialogVisible:false,
          userList:[],
          queryInfo:{
            page:1,
            size:10,
            Key:''
          },
          signList:[],
          total:null

      


     }
   },
   methods:{
     view(){
       this.dialogVisible = true
       this.$http.get('user/sign/detail/get').then(res=>{
         console.log(res);
         this.signList = res.data.data.list
       }
      )
     },
       exportExcel() {
        /* 从表生成工作簿对象 */
        var wb = XLSX.utils.table_to_book(document.querySelector("#out-table"));
        /* 获取二进制字符串作为输出 */
        var wbout = XLSX.write(wb, {
            bookType: "xlsx",
            bookSST: true,
            type: "array"
        });
        try {
            FileSaver.saveAs(
            //Blob 对象表示一个不可变、原始数据的类文件对象。
            //Blob 表示的不一定是JavaScript原生格式的数据。
            //File 接口基于Blob，继承了 blob 的功能并将其扩展使其支持用户系统上的文件。
            //返回一个新创建的 Blob 对象，其内容由参数中给定的数组串联组成。
            new Blob([wbout], { type: "application/octet-stream" }),
            //设置导出文件名称
            "sheetjs.xlsx"
            );
        } catch (e) {
            if (typeof console !== "undefined") console.log(e, wbout);
        }
        return wbout;
        },

        
     Search(){
       this.getList()
     },
     handleSizeChange(newsize){
        console.log(newsize);
        this.queryInfo.page = 1;
        this.queryInfo.size = newsize;
        this.getList()
      },
      handleCurrentChange(newpage){
        this.queryInfo.page=newpage;
        this.getList();
      },
      //数据请求api
      getList(){
         this.$http.get('admin/index/user/list/get',
      {
        params: this.queryInfo
      }
      ).then(res=>{
        this.userList = res.data.data.list;
        this.total = res.data.data.total;
         this.userList.forEach(item=>      
       {
          item.isYk = item.isYK===1?'游客用户':'注册用户'
          item.userType = item.userType===1?'APP':'快应用'
          item.sex = item.sex===1?'男':'女'
          //转化参数的数据格式
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

<style lang="less" scoped>
p{
    font-size:13px;
}
.MessageHeader{
  display:flex;
  justify-content:space-between;
  .el-button{
    margin-left:5px;
  }
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
.el-dialog{
  .el-table{
    margin:0 0 20px 0;
  border-radius:7px;
}
}



</style>