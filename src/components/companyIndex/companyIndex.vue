<template>
  <div>
    <van-popup v-model="companyShow" style="width:100%;height:105%">
      <van-nav-bar class="navBarStyle" :title="detail.companyname" @click-left="companyShow=false">
        <div slot="left"><van-icon name="close" /></div>
      </van-nav-bar>
      <van-row>
        <van-field v-model="detail.enterprisestatusText"  label="交易状态"/>
        <van-field v-model="detail.importlevelText"  label="重要等级"/>
        <van-field v-model="detail.legalrepresentative"  label="法人"/>
        <van-field v-model="detail.cluesourceText"  label="企业来源"/>
        <van-field v-model="detail.followby"  label="跟进销售"/>
        <van-field v-model="detail.CompanyCreateDate"  label="创建时间"/>
        <van-field v-model="detail.createby"  label="创建人"/>
        <van-field label="工商信息"/>
        <van-field label="财务信息"/>
      </van-row>
    </van-popup>
  </div>
</template>

<script>
export default {
  data(){
    return {
      companyShow:false,
      detail:{
        companyname:"",
        enterprisestatusText:"",
        importlevelText:"",
        legalrepresentative:"",
        cluesourceText:"",
        followby:"",
        CompanyCreateDate:"",
        createby:""
      }
    }
  },
  created(){
    let _self = this
    this.$Bus.off("OPEN_COMPANY_INFO")
    this.$Bus.on("OPEN_COMPANY_INFO",(e)=>{
      _self.detail = e
      if(_self.detail.CompanyCreateDate){
        _self.detail.CompanyCreateDate = _self.detail.CompanyCreateDate.slice(0,10)
      }
      _self.companyShow = true
    })
  }
}
</script>
