<template>
  <div>
      <p>充值配置</p>
        <div class="MessageHeader">
    <el-button type="primary" size="small" plain><i class="iconfont icon-tianjia"></i>添加</el-button>
   
   <el-button type="primary" size="small" ><i class="iconfont icon-shuaxin"></i>刷新</el-button>
  </div>
  
  <el-table
    :data="paylist"
    border
  >
    <el-table-column
      prop="id"    
      label="编号"
      >
    </el-table-column>
    <el-table-column
      prop="money"
      label="充值金额"
      >
    </el-table-column>
    <el-table-column
      prop="type"
      label="类型"
      >
    </el-table-column>
    <el-table-column
      prop="coin"
      label="书币"    
      >
    </el-table-column>
    <el-table-column
      prop="giveCoin"
      label="赠送" 
      >
    </el-table-column>
    <el-table-column
      prop="content"
      label="套餐描述"
      >
      </el-table-column>
      <el-table-column
      prop="saleDesc"
      label="标签"
      >
      </el-table-column>
      <el-table-column
      prop="isGive"
      label="是否赠送"
      >
       <template slot-scope="scope">
        {{scope.row.isGive===0?'是':'否'}}
      </template>
    </el-table-column>
    <el-table-column
      prop="isSale"
      label="是否打折"
      >
       <template slot-scope="scope">
        {{scope.row.isSale===0?'是':'否'}}
      </template>
    </el-table-column>
    <el-table-column
      prop="isDisplay"
      label="是否展示"
      >
      <template slot-scope="scope">
        {{scope.row.isDisplay===0?'是':'否'}}
      </template>
    </el-table-column>
    <el-table-column
      prop=""
      label="编辑"
      >
    </el-table-column>
  </el-table>

    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="queryInfo.page"
      :page-sizes="[10, 20, 30, 40]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>

  </div>
</template>

<script>
export default {
    data(){
      return{
        paylist:[],
        queryInfo:{
          page:1,
          size:10
        }
      }
    },
  created(){
    this.getList()
  },
  methods:{
    getList(){
this.$http.get('user/recharge/package/get').then(res=>{
      this.paylist = res.data.data
      this.total = res.data.data.length
    })
    },
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
 .refresh{
   margin-left:73%;
 }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
}

</style>