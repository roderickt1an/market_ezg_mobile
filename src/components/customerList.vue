<template>
    <van-dialog
        v-model="name_open"
        :show-confirm-button="false"
        :close-on-click-overlay="true"
        >
        <form action="/">
            <van-search placeholder="请输入公司名称搜索" v-model="searchname" @click="search"/>
        </form>
        <van-radio-group v-model="select_customerid">
            <van-cell-group>
                <van-cell v-for="item in companyList" :key="item.customerid" clickable @click="choose(item)">
                    <van-col span="22"><div>{{item.name}}</div></van-col>
                    <van-col span="2"><van-radio :name="item.customerid" /></van-col>
                </van-cell>
            </van-cell-group>
        </van-radio-group>
    </van-dialog>
</template>

<script>
export default {
  data() {
    return {
      searchname: "",
      name_open: false,
      select_customerid: "",
      companyList: ""
    };
  },
  methods: {
    search() {
      let _self = this;
      let url = `api/legwork/apiQueryCompanyOrCustomerMsg`;
      let config = {
        params: {
          name: _self.searchname
        }
      };

      function success(res) {
        _self.companyList = res.data.data;
      }

      _self.$Get(url, config, success);
    },
    choose(e) {
      let _self = this;
      _self.select_customerid = e;
      _self.$Bus.emit("UPDATA_INFO", e);
      _self.name_open = false;
    }
  },
  created() {
    let _self = this;
    _self.$Bus.on("OPEN_NAME_LIST", e => {
      _self.name_open = true;
      _self.search();
    });
  },
  watch: {
    searchname: "search"
  }
};
</script>

<style>
.van-field__clear,
.van-field__icon {
  margin-right: 0px;
}
</style>
