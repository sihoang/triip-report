# TIIMToken Smart Contracts - Round 2 - Commit Id 389cf69
- Hoang Nguyen - 04/01/2019
- This is the report on the second round of TIIMToken's audit. The [contract code](https://gist.github.com/sihoang/a330215404ca75cb6447c8953fc891a5) is copied from the original repo at commit id [389cf69](https://github.com/triipme/triip-smart-contract/tree/389cf6941760b5b6f1cb347849a5d4b7b9470b9d).


### 1. Background

TIIMToken contract is an Ethereum token contract, which aims to comply with the ERC-20 standard.  It is based on the openzeppelin-solidity ERC-20 StandardToken version [1.12.0](https://github.com/OpenZeppelin/openzeppelin-solidity/releases/tag/v1.12.0) and also has these extra functionalities:
* `Pausable` allows the contract owner to block all the transfer calls.
* `releaseTeamTokens` and `releaseFounderTokens` issue new TIIMToken to team and founder according to a pre-defined schedule.
* `transferAndCall` allows this tokens to be transferred to other contracts which implements `onTokenTransfer` and have the receiving contract trigger logic for how to respond to receiving tokens within a single transaction. This follows the current ERC-677 specifications. Note: Because the ERC-677 specifications are not finalized, this implementation may or may not comply with the future final ERC-677.


### 2. Issues that have been resolved

Please refer to the original audit [result](https://github.com/sihoang/triip-report/blob/master/TIIMToken.md) for the issue numbers.
* 3.1.2, 3.1.3, 3.1.4, 3.1.5
* 3.2.1 3.2.2
* 3.3.1, 3.3.2, 3.3.3
* 3.4.1, 3.4.2, 3.4.3, 3.4.4
* 3.5
* 3.6


### 3. Current issues

#### 3.1. Unclear behaviors
Line [30](https://gist.github.com/sihoang/a330215404ca75cb6447c8953fc891a5#file-tiimtoken-389cf69-L30): `TIIMTeamAllocation` is not being used. Even if it's consumed by other contracts, the value is not consistent with the variable `teamAllocation`.


#### 3.2. Correctness
Even though the total supply is hardcoded to be 500 millions, there are 90 million tokens unallocated. The current contract does not reflect how 90 million tokens will be minted. According to the whitepaper, the `TIIMTokenSaleAllocation` should be 75M + 90M = 165M which is 33 percent of the total supply.


### 4. Test coverage
The `solidity-coverage` is used for evaluating the test coverage. As the result, `TIIMToken` has the coverage of 57.14 percent branches, 50 percent functions and 77.19 percent lines. 


### 5. Recommendation
Please revisit the Correctness issue (i.e. item 3.2 in this report) to make sure that the total supply is actually 500 millions.


### 6. Disclosure
The scope of our review is limited to a review of Solidity code and only the source code we note as being within the scope
of our review within this report. Cryptographic tokens are emergent technologies and carry with them high levels of
technical risk and uncertainty. The Solidity language itself remains under development and is subject to unknown risks and
flaws. The review does not extend to the compiler layer, or any other areas beyond Solidity that could present security
risks.

The report is not an endorsement or indictment of any particular project or team, and the report does not guarantee the
security of any particular project. This report does not consider, and should not be interpreted as considering or having
any bearing on, the potential economics of a token, token sale or any other product, service or other asset.
No third party should rely on the reports in any way, including for the purpose of making any decisions to buy or sell any
token, product, service or other asset. Specifically, for the avoidance of doubt, this report does not constitute investment
advice, is not intended to be relied upon as investment advice, is not an endorsement of this project or team, and it is not a
guarantee as to the absolute security of the project.
