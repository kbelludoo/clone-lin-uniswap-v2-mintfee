# clone-lin-uniswap-v2-mintfee

Experimental LIN clone of Uniswap V2 `UniswapV2Pair._mintFee` / `Math.sqrt` (uint64-scale, bounded Babylonian 80 steps, 128-bit floor `(a*b)/d`, fail-closed if the quotient does not fit uint64).

- **Upstream:** [Uniswap/v2-core](https://github.com/Uniswap/v2-core) `contracts/UniswapV2Pair.sol` + `contracts/libraries/Math.sol` + `contracts/libraries/SafeMath.sol` tag `v1.0.1` commit `4dd59067c76dea4a0e8e4bfdda41877a6b16dedc` (GPL-3.0-or-later). This repository does **not** vendor the Solidity source. Hashes only: Pair sha256 `43a5421b31415868367b62bfa161ca10bcee03778873faad905f5a3e2cce9cbd` blob `f87a1db262fba132862eae377d8cdaef74c79f97`; Math sha256 `e4a9d451964a0689be2b244322a353de143ca4248d8736d91aca4ffadca4325f` blob `1cab10d2628630dfad34a0810f4fd56282208366`; SafeMath sha256 `4b1c95ff75de7342e0fadff58064820a4eb7c2fcb422a75b4994980ce8e216ae` blob `f2fbe164ffb143bc1c7116674654edd9113cbc54`.
- **LIN kernel:** [`src/lin_uniswap_v2_mintfee.lin`](src/lin_uniswap_v2_mintfee.lin) (sha256 `2cd6f4e7174fdeed632b7dd4dbfb3ba6f85ef2946b035fcaaccfe37c7858a734`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/uniswap_v2_mintfee_c11.c`](test/oracles/uniswap_v2_mintfee_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/uniswap_v2_mintfee/` and `python3 test/prove_uniswap_v2_mintfee_external.py` (23 PASS / 0 FAIL / 1 SKIP JIT this run)
- **Class:** EXPERIMENTAL. Not Ethereum Uniswap V2 uint256/uint112. Not a production pair replacement. Not a TVL claim.

Named goldens: `sqrt(0)=0`, `sqrt(4)=2`, `sqrt(1e18)=1e9`; mintFee no-growth `1000/1000` vs `kLast=1e6` → **0**; `1100/1100` → **15**; `2000/2000` → **90**; `feeOn=0` → **0**; `1e9/1e9` vs `kLast=1e12` supply `1e9` → **199760047**; naive i64 `7e18*3e18` wraps to **-5389669316318724096**.
