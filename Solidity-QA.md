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

## (5) What is an interface?

Interfaces are similar to abstract contracts, but they are limited to what the contract’s ABI can represent. In other words, you could convert an ABI into an interface, or vice versa, and no information would be lost. According to the Solidity docs they have a few additional restrictions. For instance:

- Interfaces cannot have any functions implemented
- Interfaces cannot inherit other contracts or interfaces (contracts can however inherit - interfaces just as they would inherit other contracts)
- Interfaces cannot define a constructor
- Interfaces cannot define variables
- Interfaces cannot define structs
- Interfaces cannot define enums


Interfaces are expressed using the interface keyword. Here’s an example:

```
pragma solidity ^0.4.24;

interface token {
function totalSupply() public view returns (uint256);
function balanceOf(address who) public view returns (uint256);
function transfer(address to, uint256 value) public returns (bool);
}
```

## (6) What is an abstract contract?

Contracts in Solidity are akin to classes in object-oriented languages. They include state variables that contain persistent data as well as functions that can manipulate the data in the state variables. Contracts are identified as abstract contracts when at least one of their functions lacks an implementation. As a result, they cannot be compiled. They can however be used as base contracts from which other contracts can inherit from.

Along with improved extensibility, abstract contracts provide better self-documentation, instill patterns (like the Template method), and eliminate code duplication.

Here’s an example:

```
pragma solidity ^0.4.24;

contract Person {
    function gender() public returns (bytes32);
}

contract Employee is Person {
    function gender() public returns (bytes32) { return "female"; }
}
```

## (7) When should you use an abstract contract instead of an interface?

Abstract contracts are particularly useful when you want to instill patterns — like the template method — into the dapp you’re building. They give you the ability to implement most of a contract yet you can still include abstract functions in it in order to define and self-document the skeleton of your dapp. Doing so facilitates extensibility, removes code duplication, and reduces overhead when you have multiple contracts that need to communicate with one another.

Additionally, **abstract contracts help with debugging**. Your compiler will report warnings and errors if it uncovers inconsistencies in your dapp’s patterns.

## (8) What is the difference between override and virtual in Solidity?

Virtual functions allow derived contracts to customize the functionality of a base contract, while override functions ensure that the derived contract has the same function signature as the virtual function it is overriding.

## (9) When should you use an interface instead of an abstract contract?

Interfaces are most useful when it comes to designing larger scale dapps prior to their comprehensive implementations. They make it easy to facilitate extensibility in your dapps without introducing added complexity. Many of their built in constraints (listed above) are what can ultimately be used to inform your decision as to whether or not to use an interface instead of an abstract contract.

**Takeaways**
When you’re building large, complex dapps, extensibility is key.
Abstract contracts are base contracts in which at least one of their functions lacks an implementation.

Other contracts can inherit from abstract contracts.

Interfaces are similar to abstract contracts in that they help foster extensibility, however, they cannot include any implemented functions.

Interfaces also cannot inherit from other contracts or interfaces, they cannot define constructors, they cannot define variables, they cannot define structs, and they cannot define enums.

Abstract contracts help to instill coding patterns into your dapps. They also define and self-document the structure of your dapps.

Interfaces are most useful in scenarios where your dapps require extensibility without introducing added complexity. Like abstract contracts they also help to remove code duplication and reduce overhead.

Abstract contracts and interfaces are similar, however, abstract contracts are better suited for situations where some heavy lifting is required. Conversely, interfaces are used strictly as representations.

## (10) What are Metamorphic contracts?

contracts that can be redeployed with new code to the same address. It does so by deploying the metamorphic contract with fixed, non-deterministic initialization code via the CREATE2 opcode. This initalization code clones a given implementation contract and optionally initializes it in one operation.

# Easy Questions

## (0) What is int and uint?

int is an abbreviation for int256, which has a range of -2 ** 255 to 2 ** 255 - 1.
uint is an abbreviation for uint256, which has a range of 0 to 2 \*\*256 - 1.

For example, uint8 has a range of 0 to 2 \*\* 8 -1.

## (1) What is the difference between private, internal, public, and external functions?

Access types:

**public** - can be used when contract was deployed, can be used in inherited contract

**external** can be used when contract was deployed, can NOT be used in inherited contract

**internal** - can NOT be used when contract was deployed, can be used in inherited contract

**private** - can NOT be used when contract was deployed, can NOT be used in inherited contract

**NOTE:** You cannot call a private or internal function in another contract.

Private functions can only be called from inside the contract, even the inherited contracts can't call them. Public functions can be called from anywhere. external :External functions are part of the contract interface, which means they can be called from other contracts and via transactions.

In a nutshell, public and external differs in terms of gas usage. **Public functions use more gas than External functions** when used with large arrays of data. This is due to the fact that **Solidity copies arguments to memory on a public function** while **external read from calldata** which is cheaper than memory allocation.

State variables cannot be marked as external. 

public − Public functions/ Variables can be used both externally and internally. 
For public state variable, Solidity automatically creates a getter function.

internal − Internal functions/Variables can only be used internally or by derived contracts.

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

In version 0.6.x, the fallback function was split into two separate functions:

receive() external payable — for empty calldata (and any value)
The receive() method is used as a fallback function if Ether are sent to the contract and no calldata are provided (no function is specified).

fallback() external payable — when no other function matches (not even the receive function). Optionally payable.

This separation provides an alternative to the fallback function for contracts that want to receive plain ether.

## (20) What is reentrancy?

Reentrancy is a programming technique in which a function execution is interrupted by an external function call. Within the the logic of the external function call are conditions that allow it to recursively call itself before the original function execution is able to complete.

## (21) As of the Shanghai upgrade, what is the gas limit per block?

## (22) What prevents infinite loops from running forever?

When view function is executed on-chain, i.e. within mined transaction, it consumes gas, and this protects node from infinite loop

## (23) What is the difference between tx.origin and msg.sender?

The difference between the two is fairly simple (as of early 2023); tx. origin is the address of the EOA (externally ownder account) that originated the transaction, and msg. sender is the address of whatever called the currently executing smart contract (could be an EOA or a smart contract).

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

View function declares that no state will be changed. Pure function declares that no state variable will be changed or **read**.

## (26) What is the difference between transferFrom and safeTransferFrom in ERC721?

safeTransfer just ensures that if the destination address is a contract that it has the ability to transfer the token again...essentially making sure that the token doesn't get locked by accident.

The safeTransferFrom functions are almost identical to transferFrom except that they check whether the recipient is a valid ERC721 receiver contract, and if it is, let you pass some data to that contract.

## (27) How can an ERC1155 token be made into a non-fungible token?

## (28) What is access control and why is it important?

Access control is an essential security measure when it comes to developing smart contracts in Solidity. Access control ensures that only authorized users can interact with sensitive data and functions within a smart contract, preventing attacks and ensuring the integrity of the blockchain ecosystem.

## (29) What does a modifier do?

Modifiers in Solidity are special functions that modify the behavior of other functions. They allow developers to add extra conditions or functionality without having to rewrite the entire function.

## (30) What is the largest value a uint256 can store?

2 \*\*256 - 1 (uint256, has a range of 0 to 2 \*\*256 - 1)

# Medium Questions

## (1) What is the difference between transfer and send? Why should they not be used?

## (2) How do you write a gas-efficient for loop in Solidity?

[read here](https://hackmd.io/@totomanov/gas-optimization-loops)

## (3) What is a storage collision in a proxy contract?

https://ethereum-blockchain-developer.com/110-upgrade-smart-contracts/06-storage-collisions/

## (4) What is the difference between abi.encode and abi.encodePacked?

abi.encode uses padding while abi.encodePacked does not. TBD

## (5) uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?

uint16, uint24, uint40, uint48... steps by 8 (byte size).

## (6) What changed with block.timestamp before and after proof of stake?

Under proof of work, the Ethereum block interval varied, but miners could modify the block timestamp by +/-15 seconds, as long as the modified value was greater than the parent timestamp, without the block getting rejected.

Under proof of stake, the Ethereum block interval is fixed at 12 seconds (or possibly a multiple of 12 seconds, in rare cases).

Validators (formerly miners) can still modify the block.timestamp. Before miners could manipulate the block.timestamp but if they were able to create the block. If they had 20 percent of hash power, they had a 20 percent of chance to create the block, so that their transaction will be confirmed. Even if they created the block, it is extra hard to pass the valid "timestamp".

## (7) What is frontrunning?

A front-running attack occurs when a malicious user observes a transaction after a user broadcasts it and it is waiting in the mempool. The attacker then sends their own transaction for the motive of gaining some profit with higher gas fees. This will lead to the attacker's transaction being executed before the users.

## (8) What is a commit-reveal scheme and when would you use it?

The commit-reveal scheme is a technique used in blockchain-based applications to ensure the fairness, transparency, and security of various activities such as voting, auctions, lotteries, quizzes, and gift exchanges. The scheme involves two steps: commit and reveal.

During the commit phase, users submit a commitment that contains the hash of their answer along with a random seed value. The smart contract stores this commitment on the blockchain. Later, during the reveal phase, the user reveals their answer and the seed value. The smart contract then checks that the revealed answer and the hash match, and that the seed value is the same as the one submitted earlier. If everything checks out, the contract accepts the answer as valid and rewards the user accordingly.

The commit-reveal scheme is essential in blockchain-based applications as it ensures that users cannot change their answers once they have submitted them, and prevents others from knowing the answer before the deadline. It also ensures that the process is fair and transparent, providing a secure and reliable way to conduct various activities on a blockchain-based platform.

Why should I use it ?
Not using the commit-reveal scheme in a blockchain-based application can undermine its fairness and transparency and leave the system vulnerable to various attacks such as :

Front-running attacks: In the absence of the commit-reveal scheme, an attacker can potentially front-run the transaction of a user and submit a transaction with a higher gas price to get their transaction processed first. This can give the attacker an unfair advantage in activities such as auctions or lotteries.

Replay attacks: In a blockchain-based application, a replay attack can happen when a user’s original transaction is replayed in a different context or environment. Without the commit-reveal scheme, an attacker can potentially replay a user’s transaction and manipulate the results in their favour.

Answer substitution attacks: In activities such as quizzes or voting, an attacker can potentially substitute the user’s answer with their own answer in the absence of the commit-reveal scheme. This can lead to an unfair advantage for the attacker and undermine the integrity of the activity.

Sybil attacks: In a blockchain-based application, a Sybil attack happens when an attacker creates multiple identities or accounts to manipulate the system’s results. Without the commit-reveal scheme, an attacker can potentially create multiple accounts and submit multiple answers, skewing the results in their favour.

Ref: [this](https://medium.com/coinmonks/commit-reveal-scheme-in-solidity-c06eba4091bb){:target="\_blank" rel="noopener"}

## (9) Under what circumstances could abi.encodePacked create a vulnerability?

https://medium.com/swlh/new-smart-contract-weakness-hash-collisions-with-multiple-variable-length-arguments-dc7b9c84e493

## (10) How does Ethereum determine the BASEFEE in EIP-1559?

## (11) What is the difference between a cold read and a warm read?

The **Storage** is one of the four data locations a solidity smart contract has (the others are : **memory**, **calldata** and **stack**).

## (12) How does an AMM price assets?

AMM use a mathematical formula to price assets based on liquidity, aka demand. 

Most AMMs use a **constant product** market maker model. The formula for this model is **X * Y = K** (K is a constant). 

A **constant sum AMM** can be considered a range-bound AMM with a very narrow range (good for stables) and uses the formula **X + Y = K**.

## (13) What is the effect on gas of making a function payable?

A Solidity function with a payable modifier means that the function is able to process transactions with more than or equal to zero Ether. TBD

## (14) What is a signature replay attack?

In the blockchain, a signature replay attack is an attack whereby a previously executed valid transaction is fraudulently or maliciously repeated on the same blockchain or a different blockchain.

One preventive technique is signing messages with a nonce and the address of the contract. Nonces, acronym for “number used only once”, would make each signed message unique. Also, by including the contract address in the signed message, the signature cannot be used to authenticate transactions for other contracts.

Bad: 

```
function transfer(address payable to, uint amount, bytes memory signature) external {
  bytes32 hashData = keccak256(abi.encodePacked(to, amount));
  address signer = hashData.toEthSignedMessageHash().recover(signature);
  require(signer == owner,"Signer is not owner");
  to.transfer(amount);
 }
```

Good: 

```
function transfer(address payable to, uint amount, bytes memory signature, uint nonce) external {
  require(nonce == currentNonce ++,"Invalid nonce");
  bytes32 hashData = keccak256(abi.encodePacked(to, amount,nonce));
  address signer = hashData.toEthSignedMessageHash().recover(signature);
  require(signer == owner,"Signer is not owner");
  currentNonce ++;
  to.transfer(amount);
 }
```
## (15) What is gas griefing?

A gas griefing attack happens when a user sends the amount of gas required to execute the target smart contract, but not its sub calls.

I'm really not very familiar with griefing attacks but based on the definition I'd say they can be profitable for the attacker. Not directly but indirectly.

My not-too-scientific analysis is based on the example given in the linked answer's references: https://consensys.github.io/smart-contract-best-practices/known_attacks/#insufficient-gas-griefing

This is not a perfect example but at least something: imagine a contract which is used for finding out whether anyone disagrees or agrees with some idea. So a maximum of one "yes" and a maximum of one "no" is enough for the contract. Now for some reason it needs to be called through such a Relayer contract. If the attacker performs a griefing attack on the "yes" or the "no" answer the answer doesn't get stored but nobody else can give that answer anymore as the Relayer has already blocked that answer. That way the attacker knows nobody can give an answer he doesn't like.

We might say that it's a type of "Lose-Lose game". That is, if I cannot win, I do not let nobody else wins.

A “Relayer” is an off-chain entity that pays for the gas of another user's transactions and the transaction is sent to a “Forwarder” contract.

https://www.rareskills.io/post/solidity-gasleft

## (16) How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?

https://coinsbench.com/solidity-smart-contract-for-rock-paper-scissors-6420f43d534d
TBD
## (17) What is the free memory pointer and where is it stored?

The free memory pointer (located at offset 0x40) is the most crucial part of the EVM memory. It must be handled with care, especially in assembly/Yul.

## (18) What function modifiers are valid for interfaces?

Only public and abstract modifiers are allowed for methods in interfaces.
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
