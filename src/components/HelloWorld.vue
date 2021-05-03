<template>
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
    <b>BN1</b>:
    <span class="balance">{{ state.total.bn1.usd }}</span> USD |
    <span class="balance">{{ state.total.bn1.pln }}</span> PLN
  </p>
  <p>
    <b>BN2</b>:
    <span class="balance">{{ state.total.bn2.usd }}</span> USD |
    <span class="balance">{{ state.total.bn2.pln }}</span> PLN
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
    <b>Cake V2</b>: {{ state.cake.balance }} CAKE + {{ state.cake.stakeV2 }} CAKE + {{ state.cake.earnedV2 }} CAKE |
    <span class="rate">{{ state.cake.usdRate }}</span> USD |
    <span class="change">{{ state.cake.change7 }}%</span> 7d |
    <span class="change">{{ state.cake.change24 }}%</span> 24h |
    <span class="balance">{{ state.cake.usdBalance }}</span> USD |
    <span class="balance">{{ state.cake.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Cake V1</b>: {{ state.cake.stake }} CAKE + {{ state.cake.earned }} CAKE |
    <span class="rate">{{ state.cake.usdRate }}</span> USD |
    <span class="change">{{ state.cake.change7 }}%</span> 7d |
    <span class="change">{{ state.cake.change24 }}%</span> 24h |
    <span class="balance">{{ state.cake.usdBalanceV1 }}</span> USD |
    <span class="balance">{{ state.cake.plnBalanceV1 }}</span> PLN
  </p>
  <p>
    <b>Auto</b>: {{ state.auto.cake }} CAKE + {{ state.auto.earned }} AUTO |
    <span class="rate">{{ state.auto.usdRate }}</span> USD |
    <span class="change">{{ state.auto.change7 }}%</span> 7d |
    <span class="change">{{ state.auto.change24 }}%</span> 24h |
    <span class="balance">{{ state.auto.usdBalance }}</span> USD |
    <span class="balance">{{ state.auto.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Horizon</b>: {{ state.hzn.balance }} HZN + {{ state.hzn.earned }} HZN |
    <span class="rate">{{ state.hzn.usdRate }}</span> USD |
    <span class="change">{{ state.hzn.change7 }}%</span> 7d |
    <span class="change">{{ state.hzn.change24 }}%</span> 24h |
    <span class="balance">{{ state.hzn.usdBalance }}</span> USD |
    <span class="balance">{{ state.hzn.plnBalance }}</span> PLN
  </p>
  <hr/>
  <p>
    <b>Atom BN</b>: {{ state.atom.balance }} ATOM + {{ state.atom.earned }} ATOM |
    <span class="rate">{{ state.atom.usdRate }}</span> USD |
    <span class="change">{{ state.atom.change7 }}%</span> 7d |
    <span class="change">{{ state.atom.change24 }}%</span> 24h |
    <span class="balance">{{ state.atom.usdBalance }}</span> USD |
    <span class="balance">{{ state.atom.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Dot BN1</b>: {{ state.dot.balance }} DOT + {{ state.dot.earned }} DOT |
    <span class="rate">{{ state.dot.usdRate }}</span> USD |
    <span class="change">{{ state.dot.change7 }}%</span> 7d |
    <span class="change">{{ state.dot.change24 }}%</span> 24h |
    <span class="balance">{{ state.dot.usdBalance }}</span> USD |
    <span class="balance">{{ state.dot.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Dot BN2</b>: {{ state.dot.extra.balance }} DOT + {{ state.dot.extra.earned }} DOT |
    <span class="rate">{{ state.dot.usdRate }}</span> USD |
    <span class="change">{{ state.dot.change7 }}%</span> 7d |
    <span class="change">{{ state.dot.change24 }}%</span> 24h |
    <span class="balance">{{ state.dot.extra.usdBalance }}</span> USD |
    <span class="balance">{{ state.dot.extra.plnBalance }}</span> PLN
  </p>
  <p>
    <b>Cake BN</b>: {{ state.cake.extra.balance }} CAKE |
    <span class="rate">{{ state.cake.usdRate }}</span> USD |
    <span class="change">{{ state.cake.change7 }}%</span> 7d |
    <span class="change">{{ state.cake.change24 }}%</span> 24h |
    <span class="balance">{{ state.cake.extra.usdBalance }}</span> USD |
    <span class="balance">{{ state.cake.extra.plnBalance }}</span> PLN
  </p>
  <p>
    <b>0x BN</b>: {{ state.zrx.balance }} ZRX |
    <span class="rate">{{ state.zrx.usdRate }}</span> USD |
    <span class="change">{{ state.zrx.change7 }}%</span> 7d |
    <span class="change">{{ state.zrx.change24 }}%</span> 24h |
    <span class="balance">{{ state.zrx.usdBalance }}</span> USD |
    <span class="balance">{{ state.zrx.plnBalance }}</span> PLN
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
const cakeStakeV2Address = '0xa80240eb5d7e05d3f250cf000eec0891d00b51cc'
const cakeStakeV2Abi = ['function userInfo(address) view returns (uint, uint, uint, uint)', 'function getPricePerFullShare() view returns (uint)']
const autoAddress = '0x0895196562c7868c5be92459fae7f877ed450452'
const autoAbi = ['function stakedWantTokens(uint, address) view returns (uint)', 'function pendingAUTO(uint, address) view returns (uint)']
const hznAddress = '0x67D5a94F444DF4bBA254645065a4137fc665Bf98'
const hznAbi = ['function balanceOf(address) view returns (uint)', 'function earned(address) view returns (uint)']

const cakeContract = new ethers.Contract(cakeAddress, cakeAbi, provider)
const cakeStakeContract = new ethers.Contract(cakeStakeAddress, cakeStakeAbi, provider)
const cakeStakeV2Contract = new ethers.Contract(cakeStakeV2Address, cakeStakeV2Abi, provider)
const autoContract = new ethers.Contract(autoAddress, autoAbi, provider)
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
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
  bnb: {
    balance: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
  cake: {
    balance: '',
    stake: '',
    stakeV2: '',
    earned: '',
    earnedV2: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
    usdBalanceV1: '',
    plnBalanceV1: '',
    extra: {
      balance: '4.2167',
      usdBalance: '',
      plnBalance: '',
    }
  },
  auto: {
    cake: '',
    earned: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
  hzn: {
    balance: '',
    earned: '',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
  atom: {
    balance: '0',
    earned: '0',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
  dot: {
    balance: '0',
    earned: '0',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
    extra: {
      balance: '21.2986',
      earned: '0.4975',
      usdBalance: '',
      plnBalance: '',
    }
  },
  zrx: {
    balance: '78.7012',
    usdRate: '',
    change7: '',
    change24: '',
    usdBalance: '',
    plnBalance: '',
  },
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

provider.getBalance(accountAddress).then(
  (result) => {
    state.bnb.balance = formatCrypto(result)

    get_price('binancecoin').then((response) => {
      state.bnb.usdRate = formatUsd(response, 'binancecoin')
      state.bnb.usdBalance = mulUsd(state.bnb.balance, state.bnb.usdRate)
      state.bnb.plnBalance = mulPln(state.bnb.usdBalance)

      recalculateTotal(state.bnb.usdBalance)
    })

    get_tickers('binancecoin').then((response) => {
      let market_data = response.data['market_data']
      state.bnb.change7 = formatPercentage(market_data['price_change_percentage_7d'])
      state.bnb.change24 = formatPercentage(market_data['price_change_percentage_24h'])
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

            autoContract.stakedWantTokens(7, accountAddress).then(
              (result) => {
                state.auto.cake = formatCrypto(result)

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

                        get_price('pancakeswap-token').then(
                          (response) => {
                            state.cake.usdRate = formatUsd(response, 'pancakeswap-token')

                            // Token + V2
                            state.cake.usdBalance = mulUsd(
                                (
                                    parseFloat(state.cake.balance) +
                                    parseFloat(state.cake.stakeV2) +
                                    parseFloat(state.cake.earnedV2) +
                                    parseFloat(state.auto.cake)
                                ),
                                state.cake.usdRate,
                            )
                            state.cake.plnBalance = mulPln(state.cake.usdBalance)

                            // V1
                            state.cake.usdBalanceV1 = mulUsd(
                                (
                                    parseFloat(state.cake.stake) +
                                    parseFloat(state.cake.earned)
                                ),
                                state.cake.usdRate,
                            )
                            state.cake.plnBalanceV1 = mulPln(state.cake.usdBalanceV1)

                            // Binance
                            state.cake.extra.usdBalance = mulUsd(
                                state.cake.extra.balance,
                                state.cake.usdRate,
                            )
                            state.cake.extra.plnBalance = mulPln(state.cake.extra.usdBalance)

                            recalculateTotal(state.cake.usdBalance)
                            recalculateTotal(state.cake.usdBalanceV1)
                            recalculateTotal(state.cake.extra.usdBalance, 'bn2')

                            get_tickers('pancakeswap-token').then((response) => {
                              let market_data = response.data['market_data']
                              state.cake.change7 = formatPercentage(market_data['price_change_percentage_7d'])
                              state.cake.change24 = formatPercentage(market_data['price_change_percentage_24h'])
                            })
                          }
                        )
                      }
                    )
                  }
                )
              }
            )
          }
        )
      }
    )
  }
)

autoContract.pendingAUTO(7, accountAddress).then(
  (result) => {
    state.auto.earned = formatCrypto(result, 6)

    get_price('auto').then((response) => {
      state.auto.usdRate = formatUsd(response, 'auto')
      state.auto.usdBalance = mulUsd(state.auto.earned, state.auto.usdRate)
      state.auto.plnBalance = mulPln(state.auto.usdBalance)

      recalculateTotal(state.auto.usdBalance)

      get_tickers('binancecoin').then((response) => {
        let market_data = response.data['market_data']
        state.auto.change7 = formatPercentage(market_data['price_change_percentage_7d'])
        state.auto.change24 = formatPercentage(market_data['price_change_percentage_24h'])
      })
    })
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

          get_tickers('horizon-protocol').then((response) => {
            let market_data = response.data['market_data']
            state.hzn.change7 = formatPercentage(market_data['price_change_percentage_7d'])
            state.hzn.change24 = formatPercentage(market_data['price_change_percentage_24h'])
          })
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

  get_tickers('cosmos').then((response) => {
    let market_data = response.data['market_data']
    state.atom.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.atom.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
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

  get_tickers('polkadot').then((response) => {
    let market_data = response.data['market_data']
    state.dot.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.dot.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})

get_price('0x').then((response) => {
  state.zrx.usdRate = formatUsd(response, '0x')
  state.zrx.usdBalance = mulUsd(
      state.zrx.balance,
      state.zrx.usdRate,
  )
  state.zrx.plnBalance = mulPln(state.zrx.usdBalance)

  recalculateTotal(state.zrx.usdBalance, 'bn2')

  get_tickers('0x').then((response) => {
    let market_data = response.data['market_data']
    state.zrx.change7 = formatPercentage(market_data['price_change_percentage_7d'])
    state.zrx.change24 = formatPercentage(market_data['price_change_percentage_24h'])
  })
})
</script>

<style scoped>
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
