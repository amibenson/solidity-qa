#

https://www.youtube.com/watch?v=Zf1tWIQ2vh8

https://www.youtube.com/watch?v=Zf1tWIQ2vh8&t=21:00

Questions are based on [this](https://www.rareskills.io/post/solidity-interview-questions){:target="\_blank" rel="noopener"}

# More questions

## (1) What is Solidity Visual Editor for VSCode?

https://marketplace.visualstudio.com/items?itemName=tintinweb.solidity-visual-auditor

## (2) External calls - why marking them? What so bad about them?

https://www.youtube.com/watch?v=Zf1tWIQ2vh8&t=21:00

## (3) What is issue with ++ increment and -- decreament ?

## (4) What are bot races in Code4Arena ?

## (4) What are bot races in Code4Arena ?

You can submit output of your bot in first hour.

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

## (11) What is the difference between a cold read and a warm read?

## (12) How does an AMM price assets?

## (13) What is the effect on gas of making a function payable?

## (14) What is a signature replay attack?

## (15) What is gas griefing?

## (16) ow would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?

## (17) What is the free memory pointer and where is it stored?

The free memory pointer (located at offset 0x40) is the most crucial part of the EVM memory. It must be handled with care, especially in assembly/Yul.

## (18) What function modifiers are valid for interfaces?

## (19) What is the difference between memory and calldata in a function argument?

## (20) Describe the three types of storage gas costs.

## (21) Why shouldn’t upgradeable contracts use the constructor?

## (22) What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?

## (23) What danger do ERC777 tokens pose?

## (24) What is a bonding curve?

## (25) How does safeMint differ from mint in the OpenZeppelin ERC721 implementation?

## (26) What keywords are provided in Solidity to measure time?

## (27) What is a sandwich attack?

## (28) What is a gas efficient alternative to multiplying and dividing by a multiple of two?

## (29) How large a uint can be packed with an address in one slot?

## (30) Which operations give a partial refund of gas?

## (31) What is ERC165 used for?

## (32) What is a slippage parameter useful for?

## (33) What does ERC721A do to reduce mint costs? What is the tradeoff?

## (34) Why doesn't Solidity support floating point arithmetic?

Solidity does not support floating point values there are many reasons but the most important is that solidity deals with real money and as we all know while division we lose some minor point values when we convert the value back to an integer due to that solidity does not support it.

# High Questions

## (1) How does fixed point arithmetic represent numbers?

## (2) What is an ERC20 approval frontrunning attack?

## (3) What opcode accomplishes address(this).balance?

## (4) How many arguments can a solidity event have?

## (5) What is an anonymous Solidity event?

## (6) Under what circumstances can a function receive a mapping as an argument?

## (7) What is an inflation attack in ERC4626

## (8) How many arguments can a solidity function have?

## (9) How many storage slots does this use? uint64[] x = [1,2,3,4,5]? Does it differ from memory?

## (10) Prior to the Shanghai upgrade, under what circumstances is returndatasize() more efficient than push zero?

## (11) Why does the compiler insert the INVALID op code?

## (12) What is the difference between how a custom error and a require with error string is encoded at the EVM level?

## (13) What is the kink parameter in the Compound DeFi formula?

## (14) How can the name of a function affect its gas cost, if at all?

## (15) What is a common vulnerability with ecrecover?

## (16) What is the difference between an optimistic rollup and a zk-rollup?

## (17) How does EIP1967 pick the storage slots, how many are there, and what do they represent?

## (18) How much is one Sazbo of ether?

## (19) Under what circumstances would a smart contract that works on Etheruem not work on Polygon or Optimism? (Assume no dependencies on external contracts)

## (20) How can a smart contract change its bytecode without changing its address?

## (21) What is the danger of putting msg.value inside of a loop?

## (22) Describe the calldata of a function that takes a dynamic length array of uint128 when uint128[1,2,3,4] is passed as an argument

## (23) Why is strict inequality comparisons more gas efficient than ≤ or ≥? What extra opcode(s) are added?

## (24) What is the relationship between variable scope and stack depth?

## (25) What is an access list transaction?

## (26) How can you halt an execution with the mload opcode?

## (27) Why is it necessary to take a snapshot of balances before conducting a governance vote?

## (28) How can a transaction be executed without a user paying for gas?

## (29) In solidity, without assembly, how do you get the function selector of the calldata?

## (30) How is an Ethereum address derived?

## (31) What is the metaproxy standard?

## (32) Under what circumstances do vanity addresses (leading zero addresses) save gas?

## (33) Why do a significant number of contract bytecodes begin with 6080604052? What does that bytecode sequence do?

## (34) How does Uniswap V3 determine the boundaries of liquidity intervals?

# Advanced Questions

## (1) What addresses to the ethereum precompiles live at?

## (2) How does Solidity manage the function selectors when there are more than 4 functions?

## (3) How does ABI encoding vary between calldata and memory, if at all?

## (4) What is the difference between how a uint64 and uint256 are abi-encoded in calldata?

## (5) What is read-only reentrancy?

## (6) If you deploy an empty Solidity contract, what bytecode will be present on the blockchain, if any?

## (7) How does the EVM price memory usage?

## (8) What is stored in the metadata section of a smart contract?

## (9) What is the uncle-block attack from an MEV perspective?

## (10) How do you conduct a signature malleability attack?

## (11) Under what circumstances do addresses with leading zeros save gas and why?

## (12) What is the difference between payable(msg.sender).call{value: value}(””) and msg.sender.call{value: value}(””)?

## (13) How many storage slots does a string take up?

## (14) How does the --via-ir functionality in the Solidity compiler work?

## (15) Are function modifiers called from right to left or left to right, or is it non-deterministic?

## (16) If you do a delegatecall to a contract and the opcode CODESIZE executes, which contract size will be returned?

## (17) Why is it important to ECDSA sign a hash rather than an arbitrary bytes32?

## (18) Describe how symbolic manipulation testing works.

## (19) What is the most efficient way to copy regions of memory?

## (20) How can you validate on-chain that another smart contract emitted an event, without using an oracle?

## (21) When selfdestruct is called, at what point is the Ether transferred? At what point is the smart contract's bytecode erased?

## (22) Why did Solidity deprecate the "years" keyword?

Try to use days instead, so now + 365 days. it has been deprecated because not every year is composed by 365 days.

## (23) What does the verbatim keyword do, and where can it be used?

## (24) How much gas can be forwarded in a call to another smart contract?

In order to prevent over-reservation of the smart contract services, the gas credited back relative to the reservation will be limited to at most 20% of the reservation amount. From a different perspective, the amount of gas charged to a user based on the reservation will be a minimum of 80% of the reservation.

## (25) What does an int256 variable that stores -1 look like in hex?

## (26) What is the use of the signextend opcode?

## (27) Why do negative numbers in calldata cost more gas?

## (28) What is a zk-friendly hash function and how does it differ from a non-zk-friendly hash function?

## (29) What is a nullifier in the context of zero knowledge, and what is it used for?
