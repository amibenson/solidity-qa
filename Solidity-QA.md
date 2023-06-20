# https://www.rareskills.io/post/solidity-interview-questions

# Easy Questions

## (1) What is the difference between private, internal, public, and external functions?

Access types:

public - can be used when contract was deployed, can be used in inherited contract

external can be used when contract was deployed , can NOT be used in inherited contract

internal - can NOT be used when contract was deployed , can be used in inherited contract

private - can NOT be used when contract was deployed, can NOT be used in inherited contract

Private functions can only be called from inside the contract, even the inherited contracts can't call them ?????. Public functions can be called from anywhere. external :External functions are part of the contract interface, which means they can be called from other contracts and via transactions.

In a nutshell, public and external differs in terms of gas usage. The former use more than the latter when used with large arrays of data. This is due to the fact that Solidity copies arguments to memory on a public function while external read from calldata which is cheaper than memory allocation.

State variables cannot be marked as external. public − Public functions/ Variables can be used both externally and internally. For public state variable, Solidity automatically creates a getter function. internal − Internal functions/ Variables can only be used internally or by derived contracts.

## (2) Approximately, how large can a smart contract be?

Another limitation of smart contracts is the maximum contract size. A smart contract can be a maximum of 24KB or it will run out of gas. This can be circumnavigated by using The Diamond Pattern (ERC-2535)

## (3) What is the difference between create and create2?

An important difference lies in how the address of the new contract is determined. With CREATE the address is determined by the factory contract's nonce. Everytime CREATE is called in the factory, its nonce is increased by 1. With CREATE2, the address is determined by an arbitrary salt value and the init_code.

## (4) What major change with arithmetic happened with Solidity 0.8.0?

Arithmetic operations revert on underflow and overflow, but not for type casting.

## (5) What special CALL is required for proxies to work?

A `delegatecall` is used to execute functions at a delegate in the context of the proxy structure. This means that `msg.data` is forwarded (function identifier in the first 4 bytes). After being forwarded, in order to be executed and trigger the forwarding mechanism for every function call, it is placed in the proxy contract’s fallback function. However, the `delegatecall` only returns a boolean, telling us whether the execution was successful or not.

To solve this limitation, inline assembly is used. This allows for more granular control over the stack wit a language similar to the one used by the EVM. Using inline assembly we can dissect the return value of the `delegatecall` and return the result to the caller.

```
How do they work? In Solidity, a proxy is a smart contract that allows for the execution of another contract's code. It acts as an intermediary, forwarding calls and transactions to the intended contract while also allowing for additional functionality, such as access control or logging.
```

## (6) Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?

## (7) What are the challenges of creating a random number on the blockchain?

## (8) What is the difference between a Dutch Auction and an English Auction?

English auction is a type of auction where the bid starts from the lower value and reaches the highest value. In contrast, in a Dutch auction, the bidding starts from the highest value and reaches the lower value but not less than the minimum amount set.

An advantage of a Dutch auction is that it tends to result in higher payments being made to an issuer than what is derived from the more traditional initial public offering approach. It also tends to shift share purchases away from investment banks and toward smaller investors.

## (9) What is the difference between transfer and transferFrom in ERC20?

## (10) Which is better to use for an address allowlist: a mapping or an array? Why?

## (11) Why shouldn’t tx.origin be used for authentication?

The tx.origin variable can be manipulated in certain scenarios where malicious actors use phishing attacks to trick users into conducting authenticated tasks on vulnerable contracts that rely on tx.origin for user authentication and access control.

## (12) What hash function does Ethereum primarily use?

Keccak256 can be used in many different ways in Solidity, depending on your needs. Some common use cases include:

#### Generating random numbers: You can use Keccak256 to generate random numbers by hashing a seed value with a block timestamp or block hash.

#### Verifying digital signatures: You can use Keccak256 to verify digital signatures by hashing the signed message and comparing it to the expected hash value.

#### Creating unique identifiers: You can use Keccak256 to create unique identifiers for entities in your smart contract, such as tokens or accounts.

## (13) How much is 1 gwei of Ether?

Specifically, a unit of Gwei is defined as one-billionth (one Nano) of an Ether. So 1 Gwei equals 0.000000001 or 10-9 ETH.

## (14) How much is 1 wei of Ether?

The smallest unit of ETH is called a wei, which is equivalent to 10^-18 ETH. In other words, one ETH is equal to 1,000,000,000,000,000,000 wei — or one wei is equal to
0.000000000000000001 ETH

## (15) What is the difference between assert and require?

## (16) What is a flash loan?

## (17) What is the check-effects pattern?

## (18) What is the minimum amount of Ether required to run a solo staking node?

For solo staking, the minimum deposit required is 32 ETH, which is the amount required to run a validator node on the Ethereum network.

## (19) What is the difference between fallback and receive?

## (20) What is reentrancy?

## (21) As of the Shanghai upgrade, what is the gas limit per block?

## (22) What prevents infinite loops from running forever?

When view function is executed on-chain, i.e. within mined transaction, it consumes gas, and this protects node from infinite loop

## (23) What is the difference between tx.origin and msg.sender?

## (24) How do you send Ether to a contract that does not have payable functions, or a receive or fallback?

a contract just with a payable function can receive ether，but why does the contract need to be add a receive()function to receive ether?

is there different between obtained ether via payable function and obtained ether via receive()?

We can transfer ETH to smart contracts without calling a payable function.

To handle these scenarios when someone sends ETH directly to a contract we use receive and fallback functions.

If someone sends ETH to a smart contract without passing calldata and there is a receive() function, the receive() function is executed. If there is no receive() function, then the fallback() is executed (and if there is no receive nor fallback, then the transaction reverts).

If ETH are sent to smart contracts with calldata's and the function selector doesn't match any existing function in the contract, the fallback() function is executed (again, if no fallback is implemented, the transaction reverts).

receive() is for receiving ether without calling data.

```
e.g address.call{value : 1 ether}();
```

payable function is for receiving ether with data

```
e.g address.call{value : 1 ether}(abi.encodeWithSignature('function()')
```

## (25) What is the difference between view and pure?

View function declares that no state will be changed. Pure function declares that no state variable will be changed or _read_.

## (26) What is the difference between transferFrom and safeTransferFrom in ERC721?

## (27) How can an ERC1155 token be made into a non-fungible token?

## (28) What is access control and why is it important?

## (29) What does a modifier do?

## (30) What is the largest value a uint256 can store?

# Medium Questions

## (1) What is the difference between transfer and send? Why should they not be used?

## (2) How do you write a gas-efficient for loop in Solidity?

## (3) What is a storage collision in a proxy contract?

## (4) What is the difference between abi.encode and abi.encodePacked?

## (5) uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?

## (6) What changed with block.timestamp before and after proof of stake?

## (7) What is frontrunning?

## (8) What is a commit-reveal scheme and when would you use it?

## (9) Under what circumstances could abi.encodePacked create a vulnerability?

## (10) How does Ethereum determine the BASEFEE in EIP-1559?

## (11)

## (12)

## (13)

## (14)

## (15)

## (16)

## (17)

## (18)

## (19)

## (20)

## (21)

## (22)

# High Questions
