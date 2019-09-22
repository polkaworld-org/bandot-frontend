<template>
  <div class="home">
    <div class="card">
      <div>
        <span>实时兑换</span>
      </div>
      <div class="stats">
        <el-row :gutter="20">
          <el-col :span="12" class="item">
            <div class="title">基准汇率</div>
            <div v-if="rate===null">
              <i class="el-icon-loading"></i>
            </div>
            <div class="value" v-else>{{rate}}</div>
          </el-col>
          <el-col :span="12" class="item">
            <div class="title">参考费率</div>
            <div v-if="fee===null">
              <i class="el-icon-loading"></i>
            </div>
            <div class="value" v-else>{{fee}}</div>
          </el-col>
        </el-row>
      </div>
      <div class="cols">
        <div class="col">
          <div class="border">
            <img src="../assets/usdt.svg" alt="">
            <div class="balance">0 USDT</div>
          </div>
          <input value="" placeholder="接收金额"></input>
        </div>
        <div>
          <img src="../assets/exchange.svg" alt="" style="margin-bottom: 50px">
        </div>
        <div class="col">
          <div class="border">
            <img src="../assets/bdt.svg" alt="">
            <div class="balance">0 BDT</div>
          </div>
          <input value="" placeholder="金额"></input>
        </div>
      </div>
      <el-button class="button" type="primary">提交</el-button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        rate: null,
        fee: null,
      }
    },
    mounted() {
      setTimeout(() => {
        this.rate = (1 + Math.random() * 0.1).toFixed(4)
      }, (1 + Math.floor(Math.random() * 2)) * 1000)
      setTimeout(() => {
        this.fee = `${(0.01 + Math.random() * 0.01).toFixed(4)}%`
      }, (2 + Math.floor(Math.random() * 5)) * 1000)
    },
  }
</script>


<style lang="scss" scoped>
  .card {
    margin: 20px auto 0;
    width: 400px;
    color: #ffffff;
    background: #2f2f38;
    border: 1px solid #2b2b33;
    box-shadow: 0 0 4px 1px rgba(0, 0, 0, .2);
    border-radius: 4px;
    padding: 20px;
  }

  .stats {
    margin-top: 20px;
    width: calc(100% - 40px);
    border: 1px solid #58585f;
    border-radius: .325rem;
    padding: 10px 15px;
    font-size: 12px;
    line-height: 25px;

    .item {
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      .title {
        color: #828287;
      }

      i {
        color: #f91586;
        font-weight: bold;
      }

      .value {
        color: #ffffffcc;
      }
    }
  }

  .cols {
    margin: 20px 50px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;

    .col {
      width: 35%;
      display: flex;
      flex-direction: column;
      align-items: center;

      .balance {
        font-size: 14px;
        opacity: 0.7;
      }

      .border {
        width: 100%;
        border: 1px solid #58585f;
        border-radius: .325rem;
        cursor: pointer;
        padding: 20px 0;
        display: flex;
        flex-direction: column;
        align-items: center;
      }

      img {
        width: 40%;
        margin-bottom: 10px;
      }

      input {
        width: 100%;
        border: 1px solid #58585f;
        border-radius: .125rem;
        text-align: center;
        background: none;
        margin-top: 20px;
        line-height: 30px;
        height: 30px;
        font-size: 16px;

        &:focus {
          border: 1px #e3137a solid;
        }
      }
    }
  }

  .button {
    width: 100%;
  }
</style>
