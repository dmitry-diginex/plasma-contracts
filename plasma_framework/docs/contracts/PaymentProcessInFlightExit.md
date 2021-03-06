# PaymentProcessInFlightExit.sol

View Source: [contracts/src/exits/payment/controllers/PaymentProcessInFlightExit.sol](../../contracts/src/exits/payment/controllers/PaymentProcessInFlightExit.sol)

**PaymentProcessInFlightExit**

## Structs
### Controller

```js
struct Controller {
 contract PlasmaFramework framework,
 contract EthVault ethVault,
 contract Erc20Vault erc20Vault,
 uint256 safeGasStipend
}
```

**Events**

```js
event InFlightExitOmitted(uint168 indexed exitId, address  token);
event InFlightExitOutputWithdrawn(uint168 indexed exitId, uint16  outputIndex);
event InFlightExitInputWithdrawn(uint168 indexed exitId, uint16  inputIndex);
event InFlightBondReturnFailed(address indexed receiver, uint256  amount);
event InFlightBountyReturnFailed(address indexed receiver, uint256  amount);
```

## Functions

- [run(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExitMap exitMap, uint168 exitId, address token, address payable processExitInitiator)](#run)
- [isAnyInputFinalizedByOtherExit(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, uint168 exitId)](#isanyinputfinalizedbyotherexit)
- [shouldWithdrawInput(struct PaymentProcessInFlightExit.Controller controller, struct PaymentExitDataModel.InFlightExit exit, struct PaymentExitDataModel.WithdrawData withdrawal, address token, uint16 index)](#shouldwithdrawinput)
- [shouldWithdrawOutput(struct PaymentProcessInFlightExit.Controller controller, struct PaymentExitDataModel.InFlightExit exit, struct PaymentExitDataModel.WithdrawData withdrawal, address token, uint16 index)](#shouldwithdrawoutput)
- [withdrawFromVault(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.WithdrawData withdrawal)](#withdrawfromvault)
- [flagOutputsWhenNonCanonical(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, address token, uint168 exitId)](#flagoutputswhennoncanonical)
- [flagOutputsWhenCanonical(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, address token, uint168 exitId)](#flagoutputswhencanonical)
- [returnInputPiggybackBonds(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExit exit, address token, address payable processExitInitiator)](#returninputpiggybackbonds)
- [returnOutputPiggybackBonds(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExit exit, address token, address payable processExitInitiator)](#returnoutputpiggybackbonds)
- [clearPiggybackInputFlag(struct PaymentExitDataModel.InFlightExit exit, address token)](#clearpiggybackinputflag)
- [clearPiggybackOutputFlag(struct PaymentExitDataModel.InFlightExit exit, address token)](#clearpiggybackoutputflag)
- [allPiggybacksCleared(struct PaymentExitDataModel.InFlightExit exit)](#allpiggybackscleared)

### run

Main logic function to process in-flight exit

```js
function run(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExitMap exitMap, uint168 exitId, address token, address payable processExitInitiator) public nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| self | struct PaymentProcessInFlightExit.Controller | The controller struct | 
| exitMap | struct PaymentExitDataModel.InFlightExitMap | The storage of all in-flight exit data | 
| exitId | uint168 | The exitId of the in-flight exit | 
| token | address | The ERC20 token address of the exit; uses address(0) to represent ETH | 
| processExitInitiator | address payable | The processExits() initiator | 

### isAnyInputFinalizedByOtherExit

```js
function isAnyInputFinalizedByOtherExit(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, uint168 exitId) private view
returns(bool)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| framework | PlasmaFramework |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| exitId | uint168 |  | 

### shouldWithdrawInput

```js
function shouldWithdrawInput(struct PaymentProcessInFlightExit.Controller controller, struct PaymentExitDataModel.InFlightExit exit, struct PaymentExitDataModel.WithdrawData withdrawal, address token, uint16 index) private view
returns(bool)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| controller | struct PaymentProcessInFlightExit.Controller |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| withdrawal | struct PaymentExitDataModel.WithdrawData |  | 
| token | address |  | 
| index | uint16 |  | 

### shouldWithdrawOutput

```js
function shouldWithdrawOutput(struct PaymentProcessInFlightExit.Controller controller, struct PaymentExitDataModel.InFlightExit exit, struct PaymentExitDataModel.WithdrawData withdrawal, address token, uint16 index) private view
returns(bool)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| controller | struct PaymentProcessInFlightExit.Controller |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| withdrawal | struct PaymentExitDataModel.WithdrawData |  | 
| token | address |  | 
| index | uint16 |  | 

### withdrawFromVault

```js
function withdrawFromVault(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.WithdrawData withdrawal) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| self | struct PaymentProcessInFlightExit.Controller |  | 
| withdrawal | struct PaymentExitDataModel.WithdrawData |  | 

### flagOutputsWhenNonCanonical

```js
function flagOutputsWhenNonCanonical(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, address token, uint168 exitId) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| framework | PlasmaFramework |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 
| exitId | uint168 |  | 

### flagOutputsWhenCanonical

```js
function flagOutputsWhenCanonical(PlasmaFramework framework, struct PaymentExitDataModel.InFlightExit exit, address token, uint168 exitId) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| framework | PlasmaFramework |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 
| exitId | uint168 |  | 

### returnInputPiggybackBonds

```js
function returnInputPiggybackBonds(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExit exit, address token, address payable processExitInitiator) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| self | struct PaymentProcessInFlightExit.Controller |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 
| processExitInitiator | address payable |  | 

### returnOutputPiggybackBonds

```js
function returnOutputPiggybackBonds(struct PaymentProcessInFlightExit.Controller self, struct PaymentExitDataModel.InFlightExit exit, address token, address payable processExitInitiator) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| self | struct PaymentProcessInFlightExit.Controller |  | 
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 
| processExitInitiator | address payable |  | 

### clearPiggybackInputFlag

```js
function clearPiggybackInputFlag(struct PaymentExitDataModel.InFlightExit exit, address token) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 

### clearPiggybackOutputFlag

```js
function clearPiggybackOutputFlag(struct PaymentExitDataModel.InFlightExit exit, address token) private nonpayable
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| exit | struct PaymentExitDataModel.InFlightExit |  | 
| token | address |  | 

### allPiggybacksCleared

```js
function allPiggybacksCleared(struct PaymentExitDataModel.InFlightExit exit) private pure
returns(bool)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| exit | struct PaymentExitDataModel.InFlightExit |  | 

## Contracts

* [Address](Address.md)
* [Bits](Bits.md)
* [BlockController](BlockController.md)
* [BlockModel](BlockModel.md)
* [BondSize](BondSize.md)
* [ECDSA](ECDSA.md)
* [Erc20DepositVerifier](Erc20DepositVerifier.md)
* [Erc20Vault](Erc20Vault.md)
* [EthDepositVerifier](EthDepositVerifier.md)
* [EthVault](EthVault.md)
* [ExitableTimestamp](ExitableTimestamp.md)
* [ExitGameController](ExitGameController.md)
* [ExitGameRegistry](ExitGameRegistry.md)
* [ExitId](ExitId.md)
* [ExitPriority](ExitPriority.md)
* [FailFastReentrancyGuard](FailFastReentrancyGuard.md)
* [FeeClaimOutputToPaymentTxCondition](FeeClaimOutputToPaymentTxCondition.md)
* [FeeExitGame](FeeExitGame.md)
* [FungibleTokenOutputModel](FungibleTokenOutputModel.md)
* [GenericTransaction](GenericTransaction.md)
* [IERC20](IERC20.md)
* [IErc20DepositVerifier](IErc20DepositVerifier.md)
* [IEthDepositVerifier](IEthDepositVerifier.md)
* [IExitProcessor](IExitProcessor.md)
* [ISpendingCondition](ISpendingCondition.md)
* [IStateTransitionVerifier](IStateTransitionVerifier.md)
* [Math](Math.md)
* [Merkle](Merkle.md)
* [Migrations](Migrations.md)
* [MoreVpFinalization](MoreVpFinalization.md)
* [OnlyFromAddress](OnlyFromAddress.md)
* [OnlyWithValue](OnlyWithValue.md)
* [OutputId](OutputId.md)
* [Ownable](Ownable.md)
* [PaymentChallengeIFEInputSpent](PaymentChallengeIFEInputSpent.md)
* [PaymentChallengeIFENotCanonical](PaymentChallengeIFENotCanonical.md)
* [PaymentChallengeIFEOutputSpent](PaymentChallengeIFEOutputSpent.md)
* [PaymentChallengeStandardExit](PaymentChallengeStandardExit.md)
* [PaymentDeleteInFlightExit](PaymentDeleteInFlightExit.md)
* [PaymentEip712Lib](PaymentEip712Lib.md)
* [PaymentExitDataModel](PaymentExitDataModel.md)
* [PaymentExitGame](PaymentExitGame.md)
* [PaymentExitGameArgs](PaymentExitGameArgs.md)
* [PaymentInFlightExitModelUtils](PaymentInFlightExitModelUtils.md)
* [PaymentInFlightExitRouter](PaymentInFlightExitRouter.md)
* [PaymentInFlightExitRouterArgs](PaymentInFlightExitRouterArgs.md)
* [PaymentOutputToPaymentTxCondition](PaymentOutputToPaymentTxCondition.md)
* [PaymentPiggybackInFlightExit](PaymentPiggybackInFlightExit.md)
* [PaymentProcessInFlightExit](PaymentProcessInFlightExit.md)
* [PaymentProcessStandardExit](PaymentProcessStandardExit.md)
* [PaymentStandardExitRouter](PaymentStandardExitRouter.md)
* [PaymentStandardExitRouterArgs](PaymentStandardExitRouterArgs.md)
* [PaymentStartInFlightExit](PaymentStartInFlightExit.md)
* [PaymentStartStandardExit](PaymentStartStandardExit.md)
* [PaymentTransactionModel](PaymentTransactionModel.md)
* [PaymentTransactionStateTransitionVerifier](PaymentTransactionStateTransitionVerifier.md)
* [PlasmaFramework](PlasmaFramework.md)
* [PosLib](PosLib.md)
* [PriorityQueue](PriorityQueue.md)
* [Protocol](Protocol.md)
* [Quarantine](Quarantine.md)
* [RLPReader](RLPReader.md)
* [SafeERC20](SafeERC20.md)
* [SafeEthTransfer](SafeEthTransfer.md)
* [SafeMath](SafeMath.md)
* [SpendingConditionRegistry](SpendingConditionRegistry.md)
* [Vault](Vault.md)
* [VaultRegistry](VaultRegistry.md)
