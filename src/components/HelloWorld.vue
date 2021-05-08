<template xmlns="http://www.w3.org/1999/html">
  <hr/>
  <p>
    <b>ETH</b>:
    <span class="balance">{{ state.total.eth.usd }}</span> USD |
    <span class="balance">{{ state.total.eth.pln }}</span> PLN
  </p>
  <p>
    <b>BSC</b>:
    <span class="balance">{{ state.total.bsc.usd }}</span> USD |
    <span class="balance">{{ state.total.bsc.pln }}</span> PLN
  </p>
  <p>
    <b>Total</b>:
    <span class="balance">{{ state.total.total.usd }}</span> USD |
    <span class="balance">{{ state.total.total.pln }}</span> PLN
  </p>
  <hr/>
  <p>
    <b>Ether</b>: {{ state.eth.balance }} ETH |
    <span class="rate">{{ state.eth.usdRate }}</span> USD |
    <span class="change">{{ state.eth.change7 }}%</span> 7d |
    <span class="change">{{ state.eth.change24 }}%</span> 24h |
    <span class="balance">{{ state.eth.usdBalance }}</span> USD |
    <span class="balance">{{ state.eth.plnBalance }}</span> PLN
  </p>
  <p>
    <b>BNB</b>: {{ state.bnb.balance }} BNB |
    <span class="rate">{{ state.bnb.usdRate }}</span> USD |
    <span class="change">{{ state.bnb.change7 }}%</span> 7d |
    <span class="change">{{ state.bnb.change24 }}%</span> 24h |
    <span class="balance">{{ state.bnb.usdBalance }}</span> USD |
    <span class="balance">{{ state.bnb.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Pancake</b>:
    {{ state.cake.balance }} CAKE +
    {{ state.cakeLp.balance }} CAKE LP |
    <span class="yield">{{ state.cake.stakeV2 }}</span> CAKE +
    <span class="yield">{{ state.cake.earnedV2 }}</span> CAKE |
    <span class="rate">{{ state.cake.usdRate }}</span> USD |
    <span class="change">{{ state.cake.change7 }}%</span> 7d |
    <span class="change">{{ state.cake.change24 }}%</span> 24h |
    <span class="balance">{{ state.cake.usdBalance }}</span> USD |
    <span class="balance">{{ state.cake.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Bunny</b>:
    {{ state.bunny.balance }} BUNNY |
    <span class="yield">{{ state.bunny.cake }}</span> CAKE +
    <span class="yield">{{ state.bunny.cakeLp }}</span> CAKE LP |
    <span class="rate">{{ state.bunny.usdRate }}</span> USD |
    <span class="change">{{ state.bunny.change7 }}%</span> 7d |
    <span class="change">{{ state.bunny.change24 }}%</span> 24h |
    <span class="balance">{{ state.bunny.usdBalance }}</span> USD |
    <span class="balance">{{ state.bunny.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Auto</b>:
    {{ state.auto.balance }} AUTO |
    <span class="yield">{{ state.auto.cake }}</span> CAKE +
    <span class="yield">{{ state.auto.earned }}</span> AUTO |
    <span class="rate">{{ state.auto.usdRate }}</span> USD |
    <span class="change">{{ state.auto.change7 }}%</span> 7d |
    <span class="change">{{ state.auto.change24 }}%</span> 24h |
    <span class="balance">{{ state.auto.usdBalance }}</span> USD |
    <span class="balance">{{ state.auto.plnBalance }}</span> PLN
  </p>
  <p>
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

function get_tickers(coinId) {
  return axios.get(`https://api.coingecko.com/api/v3/coins/${coinId}`)
}

function formatCrypto(crypto, digits=4) {
  return parseFloat(
    ethers.utils.formatEther(crypto)
  ).toFixed(digits)
}

function formatUsd(response, key) {
  return parseFloat(
    response.data[key]['usd']
  ).toFixed(2)
}

function formatPercentage(percentage) {
  return parseFloat(percentage).toFixed(2)
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
  else {
    throw type;
  }

  state.total.total.usd = sumUsd(state.total.total.usd, usd)
  state.total.total.pln = mulPln(state.total.total.usd)
}

function recalculateCake() {
  let total = (
      parseFloat(state.cake.balance) +
      parseFloat(state.cake.stakeV2) +
      parseFloat(state.cake.earnedV2) +
      parseFloat(state.auto.cake) +
      parseFloat(state.bunny.cake)
  )
  if (!isNaN(total)) {
    state.cake.usdBalance = mulUsd(total, state.cake.usdRate)
    state.cake.plnBalance = mulPln(state.cake.usdBalance)

    recalculateTotal(state.cake.usdBalance)
  }
}

const provider = new ethers.providers.JsonRpcProvider(
  'https://bsc-dataseed1.binance.org:443',
)

const accountAddress = '0xF7DE62B65768a169279be74b12FaA65a22FB38D3'
const erc20Abi = ['function balanceOf(address) view returns (uint)']

const cakeAddress = '0x0e09fabb73bd3ade0a17ecc321fd13a19e81ce82'
const cakeAbi = erc20Abi
// const cakeStakeAddress = '0x73feaa1ee314f8c655e354234017be2193c9e24e'
// const cakeStakeAbi = ['function userInfo(uint, address) view returns (uint)', 'function pendingCake(uint, address) view returns (uint)']
const cakeStakeV2Address = '0xa80240eb5d7e05d3f250cf000eec0891d00b51cc'
const cakeStakeV2Abi = ['function userInfo(address) view returns (uint, uint, uint, uint)', 'function getPricePerFullShare() view returns (uint)']

const cakeLpAddress = '0x0ed7e52944161450477ee417de9cd3a859b14fd0'
const cakeLpAbi = erc20Abi

const autoAddress = '0xa184088a740c695e156f91f5cc086a06bb78b827'
const autoAbi = erc20Abi
const autoCakeAddress = '0x0895196562c7868c5be92459fae7f877ed450452'
const autoCakeAbi = ['function stakedWantTokens(uint, address) view returns (uint)', 'function pendingAUTO(uint, address) view returns (uint)']

const bunnyAddress = '0xc9849e6fdb743d08faee3e34dd2d1bc69ea11a51'
const bunnyAbi = erc20Abi
const bunnyCakeAddress = '0xEDfcB78e73f7bA6aD2D829bf5D462a0924da28eD'
const bunnyCakeAbi = ['function principalOf(address) view returns (uint)']
const bunnyCakeLpAddress = '0x203Ee29ba85BbDfA23bFaE5D77620AeFDaf92cB1'
const bunnyCakeLpAbi = ['function principalOf(address) view returns (uint)']

const cakeContract = new ethers.Contract(cakeAddress, cakeAbi, provider)
// const cakeStakeContract = new ethers.Contract(cakeStakeAddress, cakeStakeAbi, provider)
const cakeStakeV2Contract = new ethers.Contract(cakeStakeV2Address, cakeStakeV2Abi, provider)
const cakeLPContract = new ethers.Contract(cakeLpAddress, cakeLpAbi, provider)

const autoContract = new ethers.Contract(autoAddress, autoAbi, provider)
const autoCakeContract = new ethers.Contract(autoCakeAddress, autoCakeAbi, provider)

const bunnyContract = new ethers.Contract(bunnyAddress, bunnyAbi, provider)
const bunnyCakeContract = new ethers.Contract(bunnyCakeAddress, bunnyCakeAbi, provider)
const bunnyCakeLpContract = new ethers.Contract(bunnyCakeLpAddress, bunnyCakeLpAbi, provider)

const state = reactive({
  total: {
    eth: {
      usd: 0.00,
      pln: 0.00,
    },
    bsc: {
      usd: 0.00,
      pln: 0.00,
    },
    total: {
      usd: 0.00,
      pln: 0.00,
    }
  },
  eth: {
    balance: '0.1239',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: 0.00,
    plnBalance: 0.00,
  },
  bnb: {
    balance: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: 0.00,
    plnBalance: 0.00,
  },
  cake: {
    balance: '',
    stakeV2: '',
    earnedV2: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: 0.00,
    plnBalance: 0.00,
  },
  cakeLp: {
    balance: '',
  },
  auto: {
    balance: '',
    cake: '',
    earned: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: 0.00,
    plnBalance: 0.00,
  },
  bunny: {
    balance: '',
    cake: '',
    cakeLp: '',
    earned: {
      cake: '',
      cakeLp: '',
    },
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: 0.00,
    plnBalance: 0.00,
  }
})

get_price('ethereum').then((response) => {
  state.eth.usdRate = formatUsd(response, 'ethereum')
  state.eth.usdBalance = mulUsd(state.eth.balance, state.eth.usdRate)
  state.eth.plnBalance = mulPln(state.eth.usdBalance)

  recalculateTotal(state.eth.usdBalance, 'eth')

  get_tickers('ethereum').then((response) => {
    let market_data = response.data['market_data']
    state.eth.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.eth.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})

get_price('binancecoin').then((response) => {
  state.bnb.usdRate = formatUsd(response, 'binancecoin')

  provider.getBalance(accountAddress).then(
    (result) => {
      state.bnb.balance = formatCrypto(result)

      state.bnb.usdBalance = mulUsd(state.bnb.balance, state.bnb.usdRate)
      state.bnb.plnBalance = mulPln(state.bnb.usdBalance)

      recalculateTotal(state.bnb.usdBalance)
    }
  )

  get_tickers('binancecoin').then((response) => {
    let market_data = response.data['market_data']
    state.bnb.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.bnb.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})

get_price('pancakeswap-token').then((response) => {
  state.cake.usdRate = formatUsd(response, 'pancakeswap-token')

  cakeContract.balanceOf(accountAddress).then(
    (result) => {
      state.cake.balance = formatCrypto(result)
      recalculateCake()
    }
  )

  cakeStakeV2Contract.userInfo(accountAddress).then(
    (result) => {
      let shares = result[0]
      state.cake.stakeV2 = formatCrypto(result[2])

      cakeStakeV2Contract.getPricePerFullShare().then(
        (result) => {
          let stakedPlusShares = ((
            ethers.BigNumber.from(shares) * ethers.BigNumber.from(result) / 10**18
          ) / 10**18).toFixed(4)
          state.cake.earnedV2 = (
            parseFloat(stakedPlusShares) - parseFloat(state.cake.stakeV2)
          ).toFixed(4)
          recalculateCake()
        }
      )
    }
  )

  autoCakeContract.stakedWantTokens(7, accountAddress).then(
    (result) => {
      state.auto.cake = formatCrypto(result)
      recalculateCake()
    }
  )

  bunnyCakeContract.principalOf(accountAddress).then(
    (result) => {
      state.bunny.cake = formatCrypto(result)
      recalculateCake()
    }
  )

  get_tickers('pancakeswap-token').then((response) => {
    let market_data = response.data['market_data']
    state.cake.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.cake.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})

cakeLPContract.balanceOf(accountAddress).then(
  (result) => {
    state.cakeLp.balance = formatCrypto(result)

    bunnyCakeLpContract.principalOf(accountAddress).then(
      (result) => {
        state.bunny.cakeLp = formatCrypto(result)
      }
    )
  }
)

get_price('auto').then((response) => {
  state.auto.usdRate = formatUsd(response, 'auto')

  autoContract.balanceOf(accountAddress).then(
    (result) => {
      state.auto.balance = formatCrypto(result)

      autoCakeContract.pendingAUTO(7, accountAddress).then(
        (result) => {
          state.auto.earned = formatCrypto(result, 6)
          state.auto.usdBalance = mulUsd(
            (parseFloat(state.auto.balance) + parseFloat(state.auto.earned)),
            state.auto.usdRate,
          )
          state.auto.plnBalance = mulPln(state.auto.usdBalance)

          recalculateTotal(state.auto.usdBalance)
        }
      )
    }
  )

  get_tickers('auto').then((response) => {
    let market_data = response.data['market_data']
    state.auto.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.auto.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})

get_price('pancake-bunny').then((response) => {
  state.bunny.usdRate = formatUsd(response, 'pancake-bunny')

  bunnyContract.balanceOf(accountAddress).then(
    (result) => {
      state.bunny.balance = formatCrypto(result)

      state.bunny.usdBalance = mulUsd(state.bunny.balance, state.bunny.usdRate)
      state.bunny.plnBalance = mulPln(state.bunny.usdBalance)

      recalculateTotal(state.bunny.usdBalance)
    }
  )

  get_tickers('pancake-bunny').then((response) => {
    let market_data = response.data['market_data']
    state.bunny.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.bunny.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})
</script>

<style scoped>
.yield {
  color: orange;
}

.change {
  color: red;
}

.balance {
  color: green;
}

.rate {
  color: blue;
}
</style>
