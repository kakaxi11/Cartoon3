<template>
  <div>
      <p>全局弹窗设置</p>
        <div class="MessageHeader">
          <div>
   <el-select v-model="value" placeholder="支付状态" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
<el-select v-model="value" placeholder="支付方式" size="small">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
<el-button type="primary" size="small"  plain >推广时间</el-button>
    <el-button type="primary" size="small" >
<i class="iconfont icon-sousuo"></i>搜索</el-button>
   <el-button type="primary" size="small" plain>显示全部</el-button>  
   </div>
      <el-button type="primary" size="small" class="refresh">
<i class="iconfont icon-shuaxin"></i>刷新</el-button>
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
      label="总新增用户">
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
    data(){
        return{
             options: [{
          value: '选项1',
          label: '黄金糕'
        }, {
          value: '选项2',
          label: '双皮奶'
        }, {
          value: '选项3',
          label: '蚵仔煎'
        }, {
          value: '选项4',
          label: '龙须面'
        }, {
          value: '选项5',
          label: '北京烤鸭'
        }],
        value: ''
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
  }
    .el-input{
        width:160px;
    }

 padding:0 10px 10px 0px;
  border-bottom: 2px solid #ccc;
  .el-button{
      margin-left:10px;
  }
}
.el-select{
    // width:140px;
    margin:0 3px
}

</style>