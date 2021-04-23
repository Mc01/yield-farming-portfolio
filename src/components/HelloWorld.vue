<template>
  <p>
    <b>Total</b>:
    {{ state.totalUsd }} USD |
    {{ state.totalPln }} PLN
  </p>
  <p>
    <b>Balance</b>: {{ state.bnbBalance }} BNB |
    {{ state.bnbUsdBalance }} USD |
    {{ state.bnbUsdRate }} USD
  </p>
  <p>
    <b>Cake</b>: {{ state.cakeBalance }} CAKE |
    {{ state.cakeUsdBalance }} USD |
    {{ state.cakeUsdRate }} USD
  </p>
  <p>
    <b>Horizon</b>: {{ state.hznBalance }} HZN + {{ state.hznEarned }} HZN |
    {{ state.hznUsdBalance }} USD |
    {{ state.hznUsdRate }} USD
  </p>
</template>

<script setup>
import { reactive } from 'vue'
import { ethers } from 'ethers'
import axios from "axios"

function get_price(coinId, base='usd') {
  return axios.get(
    'https://api.coingecko.com/api/v3/simple/price',
    {
      params: {
        ids: coinId,
        vs_currencies: base,
      },
    }
  )
}

const provider = new ethers.providers.JsonRpcProvider(
  'https://bsc-dataseed1.binance.org:443',
)

const accountAddress = '0xF7DE62B65768a169279be74b12FaA65a22FB38D3'
const cakeAddress = '0x0e09fabb73bd3ade0a17ecc321fd13a19e81ce82'
const cakeAbi = ['function balanceOf(address) view returns (uint)']
const hznAddress = '0x67D5a94F444DF4bBA254645065a4137fc665Bf98'
const hznAbi = ['function balanceOf(address) view returns (uint)', 'function earned(address) view returns (uint)']

const cakeContract = new ethers.Contract(cakeAddress, cakeAbi, provider)
const hznContract = new ethers.Contract(hznAddress, hznAbi, provider)

const state = reactive({
  accountAddress: accountAddress,
  totalUsd: 0,
  totalPln: 0,
  bnbBalance: '',
  bnbUsdBalance: '',
  bnbUsdRate: '',
  cakeBalance: '',
  cakeUsdBalance: '',
  cakeUsdRate: '',
  hznBalance: '',
  hznEarned: '',
})

let usdPln = 3.77

provider.getBalance(accountAddress).then(
  (result) => {
    state.bnbBalance = parseFloat(
      ethers.utils.formatEther(result)
    ).toFixed(4)

    get_price('binancecoin').then((response) => {
      state.bnbUsdRate = response.data['binancecoin']['usd']
      state.bnbUsdBalance = (
        parseFloat(state.bnbBalance) * parseFloat(state.bnbUsdRate)
      ).toFixed(2)

      state.totalUsd = (
        parseFloat(state.totalUsd) + parseFloat(state.bnbUsdBalance)
      ).toFixed(2)
      state.totalPln = parseFloat(
        state.totalUsd * usdPln
      ).toFixed(2)
    })
  }
)

cakeContract.balanceOf(accountAddress).then(
  (result) => {
    state.cakeBalance = parseFloat(
      ethers.utils.formatEther(result)
    ).toFixed(4)

    get_price('pancakeswap-token').then((response) => {
      state.cakeUsdRate = response.data['pancakeswap-token']['usd']
      state.cakeUsdBalance = (
        parseFloat(state.cakeBalance) * parseFloat(state.cakeUsdRate)
      ).toFixed(2)

      state.totalUsd = (
        parseFloat(state.totalUsd) + parseFloat(state.cakeUsdBalance)
      ).toFixed(2)
      state.totalPln = parseFloat(
        state.totalUsd * usdPln
      ).toFixed(2)
    })
  }
)

hznContract.balanceOf(accountAddress).then(
  (result) => {
    state.hznBalance = parseFloat(
      ethers.utils.formatEther(result)
    ).toFixed(4)

    hznContract.earned(accountAddress).then(
      (result) => {
        state.hznEarned = parseFloat(
          ethers.utils.formatEther(result)
        ).toFixed(4)

        get_price('horizon-protocol').then((response) => {
          state.hznUsdRate = parseFloat(response.data['horizon-protocol']['usd']).toFixed(2)
          state.hznUsdBalance = (
            (
                parseFloat(state.hznBalance) + parseFloat(state.hznEarned)
            ) * parseFloat(state.hznUsdRate)
          ).toFixed(2)

          state.totalUsd = (
            parseFloat(state.totalUsd) + parseFloat(state.hznUsdBalance)
          ).toFixed(2)
          state.totalPln = parseFloat(
            state.totalUsd * usdPln
          ).toFixed(2)
        })
      }
    )
  }
)
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
