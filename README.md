# reward-pools

1. Configure [the demo contract](/contracts/DemoRewardPool.sol)'s constructor arguments and modifiers (example below)
2. Deploy and fund the contract
3. Eligible addresses can now claim rewards, part of which is sent to their referrer

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "./sdk/RewardPool.sol";

contract DemoRewardPool is RewardPool(
    REWARD_TOKEN,
    REWARD_AMOUNT,
    REFERRAL_FEE,
    DID_REGISTRY_ADDRESS,
    CREDENTIAL_ISSUER_ADDRESS
)
{
    function claimReward(
        address referrer,
        bytes calldata signedCredential
    ) external override
        requiresDIDInList("KYC")
        requiresDIDInList("AML")
        requiresValidCredential("not US resident", signedCredential)
    {
        _claimReward(referrer);
    }
}
```
