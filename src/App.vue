<template>
  <div id="app">
    <div>
      <el-button @click="linkWallet">连接钱包</el-button>
      pol:
      <div v-for="item in accounts.pol" :key="item.address">{{ item.address }}</div>
      eth:
      <div v-for="item in accounts.eth" :key="item">{{ item }}</div>
    </div>
    <div class="nav-bar">
      <el-radio-group v-model="tab" style="margin-bottom: 30px;">
        <el-radio-button label="exchange">兑换</el-radio-button>
        <el-radio-button label="account">账户</el-radio-button>
      </el-radio-group>
    </div>
    <Exchange v-show="tab==='exchange'"></Exchange>
    <Account v-show="tab==='account'"></Account>
  </div>
</template>

<script>
  import Exchange from './views/Exchange'
  import Account from './views/Account'

  import Web3 from 'web3'
  import { ApiPromise, WsProvider } from '@polkadot/api'
  import { web3Accounts, web3Enable, web3FromAddress } from '@polkadot/extension-dapp'

  export default {
    name: 'app',
    components: { Exchange, Account },
    data() {
      return {
        tab: 'exchange',
        injected: [],
        accounts: {
          eth: [],
          pol: [],
        },
        polApi: null,
        web3: null,
      }
    },
    methods: {
      async linkWallet() {
        this.enablePol()
        this.enableEth()
      },
      async enablePol() {
        this.injected = await web3Enable('Bandot')
        this.accounts.pol = await web3Accounts()

        const wsProvider = new WsProvider('ws://10.3.4.162:9944')
        this.polApi = await ApiPromise.create({ provider: wsProvider })
      },
      async enableEth() {
        if (typeof window.ethereum !== 'undefined') {
          this.web3 = new Web3(window.ethereum) // eslint-disable-line
          this.accounts.eth = await window.ethereum.enable()
        } else if (window.web3) {
          this.web3 = new Web3(window.web3.currentProvider)
        }
      },
      async transfer() {
        const injector = await web3FromAddress('5DTestUPts3kjeXSTMyerHihn1uwMfLj8vU8sqF7qYrFabHE')

        this.polApi.setSigner(injector.signer)

        this.polApi.tx.balances
            .transfer('5C5555yEXUcmEJ5kkcCMvdZjUo7NGJiQJMS7vZXEeoMhj3VQ', 123456)
            .signAndSend('5DTestUPts3kjeXSTMyerHihn1uwMfLj8vU8sqF7qYrFabHE', (status) => {

            })
      },
    },
  }
</script>

<style lang="scss">
  .nav-bar {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-top: 20px;
  }
</style>
