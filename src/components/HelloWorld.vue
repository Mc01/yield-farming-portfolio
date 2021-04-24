<template>
  <hr/>
  <p>
    <b>ETH</b>:
    {{ state.total.eth.usd }} USD |
    {{ state.total.eth.pln }} PLN
  </p>
  <p>
    <b>BSC</b>:
    {{ state.total.bsc.usd }} USD |
    {{ state.total.bsc.pln }} PLN
  </p>
  <p>
    <b>BN1</b>:
    {{ state.total.bn1.usd }} USD |
    {{ state.total.bn1.pln }} PLN
  </p>
  <p>
    <b>BN2</b>:
    {{ state.total.bn2.usd }} USD |
    {{ state.total.bn2.pln }} PLN
  </p>
  <p>
    <b>Total</b>:
    {{ state.total.total.usd }} USD |
    {{ state.total.total.pln }} PLN
  </p>
  <hr/>
  <p>
    <b>Ether</b>: {{ state.eth.balance }} ETH |
    {{ state.eth.usdRate }} USD |
    {{ state.eth.usdBalance }} USD |
    {{ state.eth.plnBalance }} PLN
  </p>
  <p>
    <b>BNB</b>: {{ state.bnb.balance }} BNB |
    {{ state.bnb.usdRate }} USD |
    {{ state.bnb.usdBalance }} USD |
    {{ state.bnb.plnBalance }} PLN
  </p>
  <p>
    <b>Cake</b>: {{ state.cake.balance }} CAKE + {{ state.cake.stake }} CAKE + {{ state.cake.earned }} CAKE |
    {{ state.cake.usdRate }} USD |
    {{ state.cake.usdBalance }} USD |
    {{ state.cake.plnBalance }} PLN
  </p>
  <p>
    <b>Horizon</b>: {{ state.hzn.balance }} HZN + {{ state.hzn.earned }} HZN |
    {{ state.hzn.usdRate }} USD |
    {{ state.hzn.usdBalance }} USD |
    {{ state.hzn.plnBalance }} PLN
  </p>
  <hr/>
  <p>
    <b>Atom</b>: {{ state.atom.balance }} ATOM + {{ state.atom.earned }} ATOM |
    {{ state.atom.usdRate }} USD |
    {{ state.atom.usdBalance }} USD |
    {{ state.atom.plnBalance }} PLN
  </p>
  <p>
    <b>Dot BN1</b>: {{ state.dot.balance }} DOT + {{ state.dot.earned }} DOT |
    {{ state.dot.usdRate }} USD |
    {{ state.dot.usdBalance }} USD |
    {{ state.dot.plnBalance }} PLN
  </p>
  <p>
    <b>Dot BN2</b>: {{ state.dot.extra.balance }} DOT + {{ state.dot.extra.earned }} DOT |
    {{ state.dot.usdRate }} USD |
    {{ state.dot.extra.usdBalance }} USD |
    {{ state.dot.extra.plnBalance }} PLN
  </p>
</template>

<script setup>
import { reactive } from 'vue'
import { ethers } from 'ethers'
import axios from 'axios'

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

function formatCrypto(crypto) {
  return parseFloat(
    ethers.utils.formatEther(crypto)
  ).toFixed(4)
}

function formatUsd(response, key) {
  return parseFloat(
    response.data[key]['usd']
  ).toFixed(2)
}

function mulUsd(left, right) {
  return (
    parseFloat(left) * parseFloat(right)
  ).toFixed(2)
}

function sumUsd(left, right) {
  return (
    parseFloat(left) + parseFloat(right)
  ).toFixed(2)
}

function mulPln(usd) {
  const usdPln = 3.77
  return (parseFloat(usd) * usdPln).toFixed(2)
}

function recalculateTotal(usd, type='bsc') {
  if (type === 'eth') {
    state.total.eth.usd = sumUsd(state.total.eth.usd, usd)
    state.total.eth.pln = mulPln(state.total.eth.usd)
  }
  else if (type === 'bsc') {
    state.total.bsc.usd = sumUsd(state.total.bsc.usd, usd)
    state.total.bsc.pln = mulPln(state.total.bsc.usd)
  }
  else if (type === 'bn1') {
    state.total.bn1.usd = sumUsd(state.total.bn1.usd, usd)
    state.total.bn1.pln = mulPln(state.total.bn1.usd)
  }
  else if (type === 'bn2') {
    state.total.bn2.usd = sumUsd(state.total.bn2.usd, usd)
    state.total.bn2.pln = mulPln(state.total.bn2.usd)
  }
  else {
    throw type;
  }

  state.total.total.usd = sumUsd(state.total.total.usd, usd)
  state.total.total.pln = mulPln(state.total.total.usd)
}

const provider = new ethers.providers.JsonRpcProvider(
  'https://bsc-dataseed1.binance.org:443',
)

const accountAddress = '0xF7DE62B65768a169279be74b12FaA65a22FB38D3'
const cakeAddress = '0x0e09fabb73bd3ade0a17ecc321fd13a19e81ce82'
const cakeAbi = ['function balanceOf(address) view returns (uint)']
const cakeStakeAddress = '0x73feaa1ee314f8c655e354234017be2193c9e24e'
const cakeStakeAbi = ['function userInfo(uint, address) view returns (uint)', 'function pendingCake(uint, address) view returns (uint)']
const hznAddress = '0x67D5a94F444DF4bBA254645065a4137fc665Bf98'
const hznAbi = ['function balanceOf(address) view returns (uint)', 'function earned(address) view returns (uint)']

const cakeContract = new ethers.Contract(cakeAddress, cakeAbi, provider)
const cakeStakeContract = new ethers.Contract(cakeStakeAddress, cakeStakeAbi, provider)
const hznContract = new ethers.Contract(hznAddress, hznAbi, provider)

const state = reactive({
  total: {
    eth: {
      usd: 0,
      pln: 0,
    },
    bsc: {
      usd: 0,
      pln: 0,
    },
    bn1: {
      usd: 0,
      pln: 0,
    },
    bn2: {
      usd: 0,
      pln: 0,
    },
    total: {
      usd: 0,
      pln: 0,
    }
  },
  eth: {
    balance: '0.1239',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
  },
  bnb: {
    balance: '',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
  },
  cake: {
    balance: '',
    stake: '',
    earned: '',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
  },
  hzn: {
    balance: '',
    earned: '',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
  },
  atom: {
    balance: '10.0',
    earned: '0.0903',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
  },
  dot: {
    balance: '8.6272',
    earned: '0.1071',
    usdRate: '',
    usdBalance: '',
    plnBalance: '',
    extra: {
      balance: '21.2986',
      earned: '0.4054',
      usdBalance: '',
      plnBalance: '',
    }
  },
})

get_price('ethereum').then((response) => {
  state.eth.usdRate = formatUsd(response, 'ethereum')
  state.eth.usdBalance = mulUsd(state.eth.balance, state.eth.usdRate)
  state.eth.plnBalance = mulPln(state.eth.usdBalance)

  recalculateTotal(state.eth.usdBalance, 'eth')
})

provider.getBalance(accountAddress).then(
  (result) => {
    state.bnb.balance = formatCrypto(result)

    get_price('binancecoin').then((response) => {
      state.bnb.usdRate = formatUsd(response, 'binancecoin')
      state.bnb.usdBalance = mulUsd(state.bnb.balance, state.bnb.usdRate)
      state.bnb.plnBalance = mulPln(state.bnb.usdBalance)

      recalculateTotal(state.bnb.usdBalance)
    })
  }
)

cakeContract.balanceOf(accountAddress).then(
  (result) => {
    state.cake.balance = formatCrypto(result)

    cakeStakeContract.userInfo(0, accountAddress).then(
        (result) => {
          state.cake.stake = formatCrypto(result)

          cakeStakeContract.pendingCake(0, accountAddress).then(
              (result) => {
                state.cake.earned = formatCrypto(result)

                get_price('pancakeswap-token').then((response) => {
                  state.cake.usdRate = formatUsd(response, 'pancakeswap-token')
                  state.cake.usdBalance = mulUsd(
                      (
                          parseFloat(state.cake.balance) +
                          parseFloat(state.cake.stake) +
                          parseFloat(state.cake.earned)
                      ),
                      state.cake.usdRate,
                  )
                  state.cake.plnBalance = mulPln(state.cake.usdBalance)

                  recalculateTotal(state.cake.usdBalance)
                })
              }
          )
        }
    )
  }
)

hznContract.balanceOf(accountAddress).then(
  (result) => {
    state.hzn.balance = formatCrypto(result)

    hznContract.earned(accountAddress).then(
      (result) => {
        state.hzn.earned = formatCrypto(result)

        get_price('horizon-protocol').then((response) => {
          state.hzn.usdRate = formatUsd(response, 'horizon-protocol')
          state.hzn.usdBalance = mulUsd(
              parseFloat(state.hzn.balance) + parseFloat(state.hzn.earned),
              state.hzn.usdRate,
          )
          state.hzn.plnBalance = mulPln(state.hzn.usdBalance)

          recalculateTotal(state.hzn.usdBalance)
        })
      }
    )
  }
)

get_price('cosmos').then((response) => {
  state.atom.usdRate = formatUsd(response, 'cosmos')
  state.atom.usdBalance = mulUsd(
      parseFloat(state.atom.balance) + parseFloat(state.atom.earned),
      state.atom.usdRate,
  )
  state.atom.plnBalance = mulPln(state.atom.usdBalance)

  recalculateTotal(state.atom.usdBalance, 'bn1')
})

get_price('polkadot').then((response) => {
  state.dot.usdRate = formatUsd(response, 'polkadot')
  state.dot.usdBalance = mulUsd(
      parseFloat(state.dot.balance) + parseFloat(state.dot.earned),
      state.dot.usdRate,
  )
  state.dot.plnBalance = mulPln(state.dot.usdBalance)
  state.dot.extra.usdBalance = mulUsd(
      parseFloat(state.dot.extra.balance) + parseFloat(state.dot.extra.earned),
      state.dot.usdRate,
  )
  state.dot.extra.plnBalance = mulPln(state.dot.extra.usdBalance)

  recalculateTotal(state.dot.usdBalance, 'bn1')
  recalculateTotal(state.dot.extra.usdBalance, 'bn2')
})
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
