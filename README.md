# PumpFun - 基于solana完整逻辑的发射合约，支持Raydium,一键部署。（Solana Smart Contract Forked for Raydium）

**PumpFun Bonding Curve Protocol** 是基于 Raydium Dex 协议的 Solana 协议，旨在实现代币奖励、流动性管理和去中心化金融机制等高级功能。该项目旨在与 Solana 生态系统无缝集成，确保性能、可扩展性和安全性。


## 核心功能

### Bonding Curve Mechanism

The protocol implements a constant product bonding curve (x * y = k) with the following initial parameters:

- Initial Virtual Token Reserves: 1,073,000,191,000,000
- Initial Virtual SOL Reserves: 30,000,000,000
- Initial Real Token Reserves: 793,100,000,000,000
- Total Token Supply: 1,000,000,000,000,000

The bonding curve ensures price discovery and continuous liquidity for the token.


### 流动性管理（Automated Liquidity Management）

When the bonding curve accumulates 85 SOL:
1. X SOL is sent to the protocol multisig
2. Remaining SOL is used to seed a Raydium constant product liquidity pool
3. LP tokens are locked with claim authority assigned to the protocol multisig

## Administrative Roles

### 联合曲线（Curve Creator）
- Can initialize new bonding curves
- Sets initial parameters and optional whitelist
- Configures launch timing and initial purchases

### 配置（Admin）
- Can modify protocol parameters
- Manages fee settings
- Controls whitelist status

### Fee Recipients
- Protocol Multisig (``)
  - Receives trading fees
  - Has authority over locked LP tokens
  - Receives swapped USDC from liquidity migrations

## 创建联合曲线（Creating a Bonding Curve）

To create a new bonding curve:

1. Initialize curve parameters
2. Optional: Enable whitelist
3. Set launch timing
4. Configure initial purchases

Trading is enabled along the bonding curve until 85 SOL are raised and all 793,100,000 tokens are sold.

## 迁移（Migration）
Migration is a critical process that occurs once the bonding curve has completed and the tokens are empty. It involves:

1. Minting the remaining 206,900,000 tokens
2. Sending the experiment fee to the multisig wallet
3. A CPI (Cross-Program Invocation) call to create a Raydium Dynamic AMM (Automated Market Maker). It uses 206,900,000 matched with 85 SOL - migration fee

4. A separate instruction CPI call that locks the liquidity in the AMM and creates an escrow from which the multisig can claim trading fees.

## 🛠 安装

1. Get soucecode:

   ```
    联系 [@ghostkar](https://t.me/ghostkar)
   ```
2. Install dependencies:
   ```
    - anchor : v0.31.0
    - solana : v1.18.18
    - rustc : v1.75.0 
   ```
## 📂 项目结构

- `programs/pumpfun`: Contains the main smart contract code.
- `tests`: Automated test scripts for contract functionality.
- `migrations`: Deployment scripts for managing updates.
- `scripts`: Useful utilities for interacting with the contract.

## 🔧 配置

- Update the `Anchor.toml` file to set your Solana cluster (e.g., Devnet or Mainnet) and wallet details:

   ```
    [provider]
    cluster = "https://api.devnet.solana.com"
    wallet = "~/.config/solana/id.json"
   ```
- Ensure you have Solana CLI installed and configured:
   ```
    solana config set --url https://api.devnet.solana.com
   ```

## 📜 使用
- Interact with the smart contract: Use the provided scripts or integrate with a frontend to interact with the PumpFun smart contract.
- Testing: Run unit tests to validate the functionality 
- Deploy to Mainnet: Ensure all tests pass, and then update the deployment configuration to target the mainnet cluster.

## 🤝 问题、帮助 & 合作


如果您有任何疑问，请在 Telegram 中询问 [@ghostkar](https://t.me/ghostkar) 或者 QQ：3136710645





