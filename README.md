# Yield Farming Portfolio
:tractor: Yield Farming dashboard for BSC, CAKE, Autofarm and HZN

## Used contracts

BSC addresses
```
const cakeAddress = '0x0e09fabb73bd3ade0a17ecc321fd13a19e81ce82'
const cakeStakeAddress = '0x73feaa1ee314f8c655e354234017be2193c9e24e'
const cakeStakeV2Address = '0xa80240eb5d7e05d3f250cf000eec0891d00b51cc'
const autoAddress = '0x0895196562c7868c5be92459fae7f877ed450452'
const hznAddress = '0x67D5a94F444DF4bBA254645065a4137fc665Bf98'
```

Contract ABIs
```
const cakeAbi = ['function balanceOf(address) view returns (uint)']
const cakeStakeAbi = ['function userInfo(uint, address) view returns (uint)', 'function pendingCake(uint, address) view returns (uint)']
const cakeStakeV2Abi = ['function userInfo(address) view returns (uint, uint, uint, uint)', 'function getPricePerFullShare() view returns (uint)']
const autoAbi = ['function stakedWantTokens(uint, address) view returns (uint)', 'function pendingAUTO(uint, address) view returns (uint)']
const hznAbi = ['function balanceOf(address) view returns (uint)', 'function earned(address) view returns (uint)']
```
