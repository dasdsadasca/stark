| Term                        | Meaning                                                                                                                                                              |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **L1 (Layer 1)**            | Refers to the Ethereum mainnet, the primary blockchain where the main StarkGate bridge contracts are deployed and where users' original ERC20 assets reside.        |
| **L2 (Layer 2)**            | Refers to a StarkNet network, a separate blockchain that operates on top of L1, providing scalability and lower transaction costs.                                 |
| **ERC20**                   | A standard interface for fungible tokens on the Ethereum blockchain. The StarkGate bridge facilitates the transfer of these tokens to and from StarkNet.               |
| **StarkNet**                | A Validity Rollup (or ZK-Rollup) Layer 2 scaling solution for Ethereum.                                                                                              |
| **Bridge (StarkGate)**      | The collective term for the system of smart contracts and processes that facilitate the transfer of ERC20 tokens between L1 (Ethereum) and L2 (StarkNet).             |
| **`StarknetTokenBridge`**   | The primary L1 smart contract responsible for handling deposits and withdrawals of multiple ERC20 tokens for the modern StarkGate system.                              |
| **`LegacyBridge`**          | An L1 smart contract (inheriting from `StarknetTokenBridge`) designed to support specific ERC20 tokens that were bridged using an older version of the StarkGate system, ensuring backward compatibility. |
| **`StarknetERC20Bridge`**   | A concrete implementation of `LegacyBridge`, likely deployed for each individual legacy token requiring continued support.                                              |
| **Deposit**                 | The process of transferring ERC20 tokens from L1 to L2. Users lock tokens in the L1 bridge, and corresponding wrapped tokens are minted/credited on L2.                 |
| **Withdrawal**              | The process of transferring wrapped ERC20 tokens from L2 back to L1. Users burn/lock tokens on L2, and the original tokens are released from the L1 bridge.            |
| **Messaging Contract (`IStarknetMessaging`)** | The core StarkNet L1 contract that enables communication between L1 and L2. Used by the bridge to send deposit information to L2 and receive withdrawal information from L2. |
| **L2 Token Bridge**         | The counterpart smart contract on StarkNet (L2) for a specific bridged ERC20 token. It handles the minting/burning (or locking/unlocking) of wrapped tokens on L2.    |
| **`StarkgateManager`**      | An L1 administrative contract that governs the `StarknetTokenBridge`, manages token enrollment, deactivation, and interacts with the `StarkgateRegistry`.             |
| **`StarkgateRegistry`**     | An L1 contract that maintains a mapping of ERC20 tokens to the specific L1 bridge contracts responsible for them. Crucial for routing interactions to the correct bridge. |
| **Enrollment**              | The process of registering an ERC20 token with the `StarknetTokenBridge` to enable its transfer to and from StarkNet. Involves deploying its L2 token bridge counterpart. |
| **`StarknetTokenStorage`**  | An L1 abstract contract providing a standardized and upgrade-safe storage layout for bridge-related data, used by both `StarknetTokenBridge` and `LegacyBridge`. |
| **Selector**                | A unique identifier for a function in a smart contract. Used in messaging to specify which L2 function should process an L1 message (e.g., `HANDLE_TOKEN_DEPOSIT_SELECTOR`). |
| **Nonce**                   | A number used once. In the context of bridge messages, it helps identify and order messages, and is used in legacy deposit cancellation/reclaim.                     |
| **Payload**                 | The data content of a message sent between L1 and L2, containing details like token addresses, amounts, and recipients.                                              |
| **Wrapped Token**           | A token on L2 that represents an ERC20 token locked on L1. It is pegged to the value of the L1 token.                                                                |
| **Fee**                     | A charge paid by the user, typically in ETH, to cover the gas costs of L1 and L2 message processing for bridge operations like deposits or enrollments.                 |
| **`maxTotalBalance`**       | A security parameter on the L1 bridge that limits the total amount of a specific ERC20 token that can be locked in the bridge at any given time.                     |
| **Withdrawal Limit**        | A security feature (`WithdrawalLimit.sol` library) that can cap the amount of a token that can be withdrawn from the L1 bridge within a certain time period (intraday). |
| **NamedStorage**            | A library used by StarkWare contracts to define storage slots using string tags, facilitating upgradeability and avoiding storage collisions.                           |
| **Proxy Contract**          | A design pattern where a user interacts with a fixed-address proxy, while the underlying logic contract can be upgraded. Used by key StarkGate L1 contracts.          |
| **`onlyDepositor` modifier**| A modifier in `LegacyBridge` ensuring that only the original sender of a deposit can perform actions like cancellation or reclaim for that specific deposit.        |
| **Felt (felt252)**          | A field element in Cairo (StarkNet's native language). Solidity strings or addresses often need conversion to/from felts for L1-L2 communication.                    |
```
