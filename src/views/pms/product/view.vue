<template>
  <div>
    <el-card class="form-container" shadow="never">

      <div slot="header" class="clearfix">
        <span style="font-size:20px">{{ productDetail.product.name }}详情信息：</span>
        <el-button style="float: right; padding: 3px 0" @click="handleEdit" type="text">编辑</el-button>
      </div>
      <el-row>
        <el-col :span="24" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">物料信息:</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">物料编码:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.code }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">物料名称:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.name }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">类型:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">
            {{ productTypeList[productDetail.product.type1]}}>{{productDetail.product.type2==null?"":productTypeList[productDetail.product.type2] }}
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">单位:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productUtilList[productDetail.product.unit] }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">规格:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.specifications }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">标准</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.standard }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">价格</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.price }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">供应商</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">
            {{ productDetail.product.supplierId | filterSupplierName }}
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">创建人</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{memberList[productDetail.product.createOn] }}</div>
        </el-col>

      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">时间</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.product.createTime }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">发布状态</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">
            {{ productDetail.product.status == 1 ? "已发布" : "未发布" }}
          </div>
        </el-col>
      </el-row>

      <!--库存信息-->
      <el-col :span="24" align="center" style="line-height: 20px;">
        <div ></div>
      </el-col>
      <el-col :span="24" align="center" style="line-height: 20px;">
        <div class="grid-content bg-table-head">库存信息:</div>
      </el-col>
      <el-row>
        <el-col :span="9" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">上月数量:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.stock.lastMonthQuantity }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9" align="center" style="line-height: 20px;">
          <div class="grid-content bg-table-head">现有库存:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">
            {{ productDetail.stock.onHandInventory }}
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">本月提报数量:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.stock.reportedQuantity }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">安全库存 :</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.stock.safetyStock }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">生产线人数 :</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ productDetail.stock.prodLineMembers  }}</div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="9">
          <div class="grid-content bg-table-head">采购方式:</div>
        </el-col>
        <el-col :span="15">
          <div class="grid-content bg-purple">{{ purchaseMethodList[productDetail.stock.purchaseMethod] }}</div>
        </el-col>
      </el-row>
    </el-card>

  </div>
</template>
<script>
  import ProductDetail from "./components/ProductDetail";

  let than;
  import {fetchaAllList as getAllSupplier} from "@/api/supplier";
  import {fetchAllList as getAllProductUtil } from "@/api/productUtil";
  import {fetchList as getAllPurchaseMethod} from "@/api/purchaseMethod";
  import {fetchAllList as getAllProductType} from "@/api/productType";
  import {fetchAllList as getAllMember} from "@/api/login";


  import {getProduct} from "@/api/product";



  export default {
    name: "viewProduct",

    data() {
      than = this;
      return {
        productDetail: null,
        supplierList: [],
        productId: null,
        product:{},
        productUtilList:[],
        productTypeList:[],
        purchaseMethodList:[],
        memberList:[],
      };
    },
    created() {
      this.productId = this.$route.query.id;
      //查询
      this.getProductDetil();
      this.getProductUtil();
      this.getProductType();
      this.getPurchaseMethod();
      this.getAllSupplierList();
      this.getMember();
    },
    methods: {
      handleEdit(){
        this.$router.push({path: '/pms/updateProduct', query: {id: this.productDetail.product.id}});
      },
      getMember() {
        getAllMember().then(response => {
          response.data.forEach(item=>{this.memberList[item.id]=item.username})
        })
      },
      getPurchaseMethod() {
        getAllPurchaseMethod().then(response => {
          response.data.list.forEach(item=>{this.purchaseMethodList[item.id]=item.name})
        })
      },
      getProductType() {
        getAllProductType(0).then(response => {
          response.data.forEach(item=>{this.productTypeList[item.id]=item.typeName})
        })
      },
      getProductUtil() {
        getAllProductUtil().then(response => {
           response.data.forEach(item=>{this.productUtilList[item.id]=item.utilName})
        })
      },
      getProductDetil() {
        getProduct(this.productId).then(response => {
          this.productDetail = response.data
        })
      },
      //获取供应商
      getAllSupplierList() {
        getAllSupplier().then((response) => {
          this.supplierList = response.data;
        });
      },
    },
    filters: {
      filterSupplierName(ids) {
        let res = "";
        ids && ids.split(",").forEach(id => {
          than.supplierList.forEach(item => {
            if (item.id == id) {
              res += item.name + ",";
            }
          })

        });
        return res.substring(0, res.length - 1);
      }
    },

  };
</script>
<style scoped>


  .el-row {
    /*margin-bottom: 20px;*/
  }

  .bg-table-head {
    color: white;
    background-color: cadetblue;
    font-size: 18px;
  }

  .el-col {
    border-radius: 4px;
  }

  .bg-purple-dark {
    /*background: #99a9bf;*/
  }

  .bg-purple {
    background: #d3dce6;
  }

  .bg-purple-light {
    /*background: #e5e9f2;*/
  }

  .grid-content {
    text-align: center;
    line-height: 30px;
    min-height: 30px;
    border: #f2f2f2 solid 1px;
  }

  .row-bg {
    padding: 10px 0;
    /*background-color: #f9fafc;*/
  }

  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  el-col div {
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }

  .clearfix:after {
    clear: both;
  }

  .box-card {
    width: 480px;
  }
</style>
