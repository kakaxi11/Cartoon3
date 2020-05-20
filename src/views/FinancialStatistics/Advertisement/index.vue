<template>
  <div>
      <p>投放回收统计列表</p>
        <div class="MessageHeader">
            <div>
        <el-date-picker
      v-model="value1"
      type="daterange"
      size="small"
      range-separator="至"
      start-placeholder="开始日期"
      value-format="yyyy-MM-dd"    
       end-placeholder="结束日期"
       @change="change"
       >
    </el-date-picker>
        <el-button type="primary" size="small"  @click="Search"> <i class="iconfont icon-sousuo"></i>查询日期</el-button>
            <el-button type="warning" size="small"  class="Excel" @click="exportExcel">导出Excel</el-button>
            </div>

   
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  								
  <el-table
    :data="LogList"
    border
   id="out-table"
  >
    <el-table-column
      prop="date"    
      label="日期"
     >
    </el-table-column>
    <el-table-column
      prop="count"
      label="当日所有新增用户数"
    >
    </el-table-column>
    <el-table-column
      prop="today"
      label="当天充值"
      max-width="90"
      >
      <!-- 作用域插槽 -->
    </el-table-column>
     <el-table-column
      prop="threeDay"
      label="3天累计充值"
      >
    </el-table-column>
    <el-table-column
      prop="fiveDay"
      label="5天累计充值"
   
      >
    </el-table-column>
    <el-table-column
      prop="sevenDay"
      label="7天累计充值"
    
      >
    </el-table-column>
     <el-table-column
      prop="fourteenDay"
      label="14天累计充值"
      >
      <!-- 作用域插槽 -->
      
    </el-table-column>
     <el-table-column
      prop="thirtyDay"
      label="30天累计充值"
      >
      
    </el-table-column>
     <el-table-column
      prop="now"
      label="至今累计充值"
      >
    </el-table-column>
  </el-table>

    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="logInfo.page"
      :page-sizes="[5, 10, 20, 30]"
      :page-size="this.logInfo.size"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>

  

  </div>
</template>

<script>
import FileSaver from "file-saver";
import XLSX from "xlsx";

export default {
data(){
        return{
           queryInfo:{
            type:1,
            page:1,
            size:10,
            key:''
          },
           logInfo:{
        page:1,
        size:10,
        start:'2020-3-1',
        end:'2020-3-30'
      },
      value1:[],
      total:null,
          CartoonList:[],
          LogList:[]
        }
    },
    created(){
      this.getList()
      this.getlogList()
    },
    methods:{
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
        this.getlogList()
      },
      change(){
      this.logInfo.start = this.value1[0]
      this.logInfo.end = this.value1[1]
      },
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
       getlogList(){
         this.$http.get('admin/new/user/recharge/info',{params:this.logInfo}
      ).then(res=>{
        this.LogList = res.data.data.list
        this.total =res.data.data.total
        console.log(this.LogList);
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
        this.logInfo.page = 1
        this.logInfo.size = newsize;
        this.getlogList()
      },
      handleCurrentChange(newpage){
        this.logInfo.page=newpage
        this.getlogList()
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

</style>