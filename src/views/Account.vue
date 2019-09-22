<template>
  <div class="home">
    <div class="card">
      <div>
        <span>我的资产</span>
      </div>
      <div class="table">
        <div class="row">
          <div class="col">资产</div>
          <div class="col">金额</div>
          <div class="col">锁仓金额</div>
          <div class="col">USDT 估值</div>
        </div>
        <div class="row" v-for="i of tableData">
          <div class="col">{{i.asset}}</div>
          <div class="col">{{i.amount}}</div>
          <div class="col">{{i.lockedAmount}}</div>
          <div class="col">{{i.value}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [{
          asset: 'ETH',
          amount: 123,
          lockedAmount: 0,
          value: 66,
        }, {
          asset: 'DOT',
          amount: 123,
          lockedAmount: 0,
          value: 66,
        }, {
          asset: 'USDT',
          amount: 123,
          lockedAmount: 0,
          value: 66,
        }],
      }
    },
  }

</script>


<style lang="scss" scoped>
  .card {
    margin: 20px auto 0;
    width: 600px;
    color: #ffffff;
    background: #2f2f38;
    border: 1px solid #2b2b33;
    box-shadow: 0 0 4px 1px rgba(0, 0, 0, .2);
    border-radius: 4px;
    padding: 20px 0;
  }

  .table {
    margin-top: 20px;

    .row {
      display: flex;
      flex-direction: row;
      padding: 10px 0;
      font-size: 14px;

      &:first-of-type {
        background: #ffffff11;
        font-size: 12px;
      }

      .col {
        width: 25%;
      }
    }
  }
</style>
