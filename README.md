# DefiFund-Core
core of defi fund

Introduction
Getting acquainted with the TTTdefi Fund protocol.
TTTdefi Fund is an advanced timelock for ETH and ERC-20 assets. Using TTTdefi Fund, you can lock in the time value of your assets. 
Features
0% Fees
Though this may be subject to change, TTTdefi Fund does not plan to charge any fees to use the service whatsoever.
Non-Custodial
Funds are 100% held by smart contracts. We couldn’t touch them even if we tried.
Unlimited Funds
Easily manage as many funds as you like with several beneficiaries.
Lock Period Increases
If you decide you want to keep your funds locked for longer, you can always increase the time until expiration as much as you’d like.
Beneficiary Management
As the owner of a TTTdefi Fund, you have the ability to change the beneficiary at any time, so you never have to worry about your beneficiary losing their private key. Alternatively, you have the option to renounce ownership of the fund, to completely revoke access to beneficiary controls.
In The Pipeline
TTTdefi Fund is excited to explore the possibilities of time-locked assets. In v2 we look forward to experimenting with things like: preset portfolio allocations, fund balancing, and trading of locked assets.
Use Cases
The extent of the novel applications of time-locked assets is yet to be explored, but here are a few examples.
Gifts
Want to show friends and family the time-value of crypto-assets? Lock up tokens as a birthday gift so they can get a nice surprise for the next birthday.
Savings
Saving up for something? Lock up some interest bearing tokens so you can’t cheat.
Speculation
Think your portfolio will rise astronomically in the next 10 years? Lock up your tokens to prevent your weak hands from getting the best of you. You can always add to your fund or increase the expiration date anytime.
Earning
Want to earn passive income on interest bearing tokens? Lock up some rDai and have the interest paid directly to your wallet.
Vesting
Want to hold your employees accountable? Lock up funds to give them the rights to assets over time.
Smart Contracts
TTTdefi Fund consists of two primary smart contracts: TTTdefiFund.sol and TTTdefiFundFactory.sol.
TTTdefiFundFactory.sol
Factory to deploy new TTTdefiFund contracts.
function getFund(uint _id) public view returns(address)
Given an id, return the corresponding fund address.
Parameter	Type	Description
_id	uint	The id of the fund.
Returns	Description
address	The address of the corresponding fund.

function getUserFunds(address _user) public view returns(address[] memory) 
Given a user address, return all owned funds.
Parameter	Type	Description
_user	address	The address of the user.
Returns	Description
uint[]	Array of user's funds.

function createFund(uint _expiration, address _beneficiary) public payable
Deploy a TTTdefiFund contract.
Parameter	Type	Description
_expiration	uint	Date time in seconds when timelock expires.
_beneficiary	address	Address permitted to withdraw funds after unlock.

TTTdefiFund.sol
Contract for individual funds.
function deposit(uint _amount, address _token) public payable
Allows a user to deposit ETH or an ERC20 into the contract. If _token is 0 address, deposit ETH.
Parameter	Type	Description
_amount	uint	The amount to deposit.
_token	address	The token to deposit.

function withdraw(uint _amount, address _token) public isExpired() onlyBeneficiary()
Withdraw funds to msg.sender, but only if the timelock is expired and msg.sender is the beneficiary. If _token is 0 address, withdraw ETH.
Parameter	Type	Description
_amount	uint	The amount to withdraw.
_token	address	The token to withdraw.

function increaseTime(uint _newExpiration) public onlyOwner()
Increase the time until expiration. Only the owner can perform this. This feature can be disabled if the owner renounces ownership.
Parameter	Type	Description
_newExpiration	uint	New date time in seconds when timelock expires.

function updateBeneficiary(address _newBeneficiary) public onlyOwner()
Update the beneficiary address. Only the owner can perform this. This feature can be disabled if the owner renounces ownership.
Parameter	Type	Description
_newBeneficiary	address	New beneficiary address.

function renounceOwnership() public onlyOwner 
Renounce ownership of fund. Will no longer be possible to call increaseTime or updateBeneficiary.

