<template>
  <div>
      <p>充值配置</p>
        <div class="MessageHeader">
    <el-button type="primary" size="small"   @click="dialogFormVisible = true"><i class="iconfont icon-tianjia"></i>添加</el-button>
   <el-button type="primary" size="small"><i class="iconfont icon-shuaxin"></i>刷新</el-button>


   <el-dialog title="档位添加" :visible.sync="dialogFormVisible" width="510px" top="10vh">
  <el-form :model="form" label-width="80px">
      <el-form-item label="档位类型" >
      <el-select v-model="form.type" placeholder="请选择档位类型" size="small" style="width:260px" >
        <el-option label="书币充值" value="书币充值"></el-option>
        <el-option label="包月会员" value="包月会员"></el-option>
        <el-option label="季度会员" value="季度会员"></el-option>
        <el-option label="半年会员" value="半年会员"></el-option>
        <el-option label="包年会员" value="包年会员"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="充值金额" >
      <el-input v-model="form.money" style="width:260px" size="small"></el-input>
    </el-form-item>
     <el-form-item label="书币" >
      <el-input v-model="form.coin" style="width:260px" size="small"></el-input>
    </el-form-item>
     <el-form-item label="赠送" >
      <el-input v-model="form.giveCoin" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="套餐描述" >
      <el-input v-model="form.content" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="活动折扣" >
      <el-input v-model="form.saleDesc" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="是否赠送" >
        <el-radio v-model="form.isGive" label="0">是</el-radio>
        <el-radio v-model="form.isGive" label="1">否</el-radio>
    </el-form-item>
    <el-form-item label="是否打折" >
        <el-radio v-model="form.isSale" label="0">是</el-radio>
        <el-radio v-model="form.isSale" label="1">否</el-radio>
    </el-form-item>
    <el-form-item label="是否展示" >
        <el-radio v-model="form.isDisplay" label="0">是</el-radio>
        <el-radio v-model="form.isDisplay" label="1">否</el-radio>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogClose">确 定</el-button>
  </div>
</el-dialog>

   <el-dialog title="档位修改" :visible.sync="EditdialogFormVisible" width="510px" top="10vh">
  <el-form :model="editForm" label-width="80px">
      <el-form-item label="档位类型" >
      <el-select v-model="editForm.type" placeholder="请选择档位类型" size="small" style="width:260px" >
        <el-option label="书币充值" value="书币充值"></el-option>
        <el-option label="包月会员" value="包月会员"></el-option>
        <el-option label="季度会员" value="季度会员"></el-option>
        <el-option label="半年会员" value="半年会员"></el-option>
        <el-option label="包年会员" value="包年会员"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="充值金额" >
      <el-input v-model="editForm.money" style="width:260px" size="small"></el-input>
    </el-form-item>
     <el-form-item label="书币" >
      <el-input v-model="editForm.coin" style="width:260px" size="small"></el-input>
    </el-form-item>
     <el-form-item label="赠送" >
      <el-input v-model="editForm.giveCoin" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="套餐描述" >
      <el-input v-model="editForm.content" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="活动折扣" >
      <el-input v-model="editForm.saleDesc" style="width:260px" size="small"></el-input>
    </el-form-item>
    <el-form-item label="是否赠送" >
        <el-radio v-model="editForm.isGive" :label="0">是</el-radio>
        <el-radio v-model="editForm.isGive" :label="1">否</el-radio>
    </el-form-item>
    <el-form-item label="是否打折" >
        <el-radio v-model="editForm.isSale" :label="0">是</el-radio>
        <el-radio v-model="editForm.isSale" :label="1">否</el-radio>
    </el-form-item>
    <el-form-item label="是否展示" >
        <el-radio v-model="editForm.isDisplay" :label="0">是</el-radio>
        <el-radio v-model="editForm.isDisplay" :label="1">否</el-radio>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="EditdialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="editdialogClose">确 定</el-button>
  </div>
</el-dialog>

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
      <template slot-scope="scope">
        {{'￥'+scope.row.money/100}}
        </template>
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
      label="活动折扣"
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
    <template slot-scope="scope">
        <el-button size="mini" type="primary" icon="el-icon-edit" @click="edit(scope.row.id)"></el-button>
      <el-button size="mini" type="danger" icon="el-icon-delete" @click="remove(scope.row.id)"></el-button>
    </template>
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
        //档位添加框开关
        dialogFormVisible:false,

        //档位修改框开关
        EditdialogFormVisible:false,
        paylist:[],
        total:null,
        //修改数据对象
        editForm:{},
        queryInfo:{
          page:1,
          size:10
        },
        form:{
        type:null,
        money:null,
        coin:null,  
        giveCoin:null,
        content:'',
        saleDesc:'',
        saleMoney:0,
        // 单选框数据
        isGive:null,
        isSale:null,
        isDisplay:null,
        // id:null,
        giveDesc:'',
        },
      }
    },
  created(){
    this.getList()
  },
  methods:{
    edit(id){
      this.EditdialogFormVisible=true
      console.log(id);
      // 通过数组方法寻找该id的第一个下标并获取到  
      // findIndex  数据绑定 到diaLog
       const index = this.paylist.findIndex(item=>{
       return item.id === id
      })
        this.editForm=this.paylist[index]
    },
      // 删除数据
    remove(id){
       this.$http.delete(`admin/recharge/package/delete?id=${id}`).then(res=>{
          console.log(res);
           this.getList()
      })
    },
     //修改数据并提交
    editdialogClose(){
     
      console.log(this.editForm);
      this.EditdialogFormVisible = false
      this.$http.put('admin/recharge/package/update',this.editForm).then(res=>{
        console.log(res);
      })
    },
    //修改数据格式并添加套餐数据
    dialogClose(){
           switch(this.form.type){
                 case "书币充值":this.form.type = 0; break;
                 case "包月会员":this.form.type = 1; break;
                 case "季度会员":this.form.type = 2; break;
                case "半年会员":this.form.type = 3; break;
                case "包年会员":this.form.type = 4; break;
               }             
      // this.form.id = this.paylist[this.paylist.length-1].id+1
      console.log(this.form);
      this.dialogFormVisible = false
      console.log(this.form);
       this.$http.post('admin/recharge/package/add',this.form).then(res=>{
        console.log(res);
          this.getList()
      })
    },
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
.el-form-item {
  margin:7px 0px;
  .el-radio{
    margin:0 10px 0 40px;
  }
}
.el-table-column{
  .el-button{
    height: 30px !important;
  }
}
</style>