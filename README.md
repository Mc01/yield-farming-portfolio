# Yield Farming Portfolio
:tractor: Yield Farming dashboard for BSC, CAKE, AUTO and BUNNY

## Used contracts

BSC addresses
```
const cakeAddress = '0x0e09fabb73bd3ade0a17ecc321fd13a19e81ce82'
const cakeLpAddress = '0x0ed7e52944161450477ee417de9cd3a859b14fd0'
const cakeStakeV2Address = '0xa80240eb5d7e05d3f250cf000eec0891d00b51cc'

const autoAddress = '0xa184088a740c695e156f91f5cc086a06bb78b827'
const autoCakeAddress = '0x0895196562c7868c5be92459fae7f877ed450452'

const bunnyAddress = '0xc9849e6fdb743d08faee3e34dd2d1bc69ea11a51'
const bunnyCakeAddress = '0xEDfcB78e73f7bA6aD2D829bf5D462a0924da28eD'
const bunnyCakeLpAddress = '0x203Ee29ba85BbDfA23bFaE5D77620AeFDaf92cB1'
```

Contract ABIs
```
const cakeAbi = ['function balanceOf(address) view returns (uint)']
const cakeLpAbi = ['function balanceOf(address) view returns (uint)']
const cakeStakeV2Abi = ['function userInfo(address) view returns (uint, uint, uint, uint)', 'function getPricePerFullShare() view returns (uint)']

const autoAbi = ['function balanceOf(address) view returns (uint)']
const autoCakeAbi = ['function stakedWantTokens(uint, address) view returns (uint)', 'function pendingAUTO(uint, address) view returns (uint)']

const bunnyAbi = ['function balanceOf(address) view returns (uint)']
const bunnyCakeAbi = ['function principalOf(address) view returns (uint)']
const bunnyCakeLpAbi = ['function principalOf(address) view returns (uint)']
```
