# 💠 GRT Token Whitepaper
### Version 1.0 | October 2025

---

## Executive Summary

**GRT Token** представляет собой утилитарный токен стандарта **ERC-20**, интегрированный с экосистемой GiranTrade для обеспечения бесшовной конвертации **фиат ↔ USDT ↔ GRT**. Токен служит мостом между традиционной финансовой системой и децентрализованной экономикой, предоставляя пользователям доступ к:

- Fee-sharing и вознаграждениям от комиссий платформы
- Staking с фиксированными APY (до 40%)
- Governance правам в DAO
- Liquidity mining программам
- Скидкам на торговые комиссии

**Ключевое отличие**: В отличие от обычных utility токенов, GRT напрямую интегрирован с работающим P2P обменником, что обеспечивает реальный use case с первого дня.

---

## 1. Introduction

### 1.1 Background

Криптовалютный рынок страдает от фрагментации между фиатными и криптовалютными сервисами. Пользователи вынуждены использовать множество платформ для:
- Покупки криптовалюты за фиат
- P2P обмена
- Стейкинга и yield farming
- Управления ликвидностью

GRT Token решает эту проблему, объединяя все функции в единой экосистеме с прозрачной экономической моделью.

### 1.2 Vision

Создать самодостаточную экономику, где токен служит:
1. **Средством обмена** внутри платформы
2. **Инструментом управления** через DAO
3. **Источником пассивного дохода** через стейкинг
4. **Механизмом лояльности** для активных пользователей

---

## 2. Technical Specifications

### 2.1 Blockchain Platform

**Primary Network**: Ethereum Mainnet
- Причина выбора: максимальная децентрализация и безопасность
- Широкая поддержка кошельков и бирж
- Наибольшая ликвидность для DeFi

**Future Expansion**:
- Layer-2 (Arbitrum/Optimism) для снижения gas fees
- Bridge на TRON для интеграции с существующим escrow
- Возможное развертывание на BNB Chain для азиатского рынка

### 2.2 Token Standard

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";

contract GRTToken is ERC20, Ownable, Pausable {
    uint256 public constant MAX_SUPPLY = 100_000_000 * 10**18;
    
    constructor() ERC20("GiranTrade Token", "GRT") {
        _mint(msg.sender, MAX_SUPPLY);
    }
    
    function pause() external onlyOwner {
        _pause();
    }
    
    function unpause() external onlyOwner {
        _unpause();
    }
    
    function _beforeTokenTransfer(
        address from,
        address to,
        uint256 amount
    ) internal override whenNotPaused {
        super._beforeTokenTransfer(from, to, amount);
    }
}
```

---

## 3. Tokenomics

### 3.1 Token Parameters

| Parameter           | Value                |
|---------------------|----------------------|
| Token Name          | GiranTrade Token     |
| Symbol              | GRT                  |
| Standard            | ERC-20               |
| Total Supply        | 100,000,000 GRT      |
| Initial Circulation | 25,000,000 GRT (25%) |
| Decimals            | 18                   |
| Contract Ownership  | Multi-sig (3/5)      |
| Mintable            | No                   |
| Burnable            | Yes                  |

### 3.2 Token Distribution

```
┌─────────────────────────────────────────────────────────────┐
│              TOKEN ALLOCATION (100M GRT)                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🌊 Liquidity Pool          35%  (35,000,000 GRT)           │
│     ├─ DEX Liquidity        20%  (20,000,000 GRT)           │
│     ├─ CEX Listings         10%  (10,000,000 GRT)           │
│     └─ Internal Pool         5%  (5,000,000 GRT)            │
│                                                             │
│  🎁 Community Incentives    25%  (25,000,000 GRT)           │
│     ├─ Staking Rewards      15%  (15,000,000 GRT)           │
│     ├─ Referral Program      5%  (5,000,000 GRT)            │
│     ├─ Airdrops & Events     3%  (3,000,000 GRT)            │
│     └─ Bug Bounty            2%  (2,000,000 GRT)            │
│                                                             │
│  🔧 Development Fund        20%  (20,000,000 GRT)           │
│     ├─ Product Dev          10%  (10,000,000 GRT)           │
│     ├─ Marketing             6%  (6,000,000 GRT)            │
│     └─ Partnerships          4%  (4,000,000 GRT)            │
│                                                             │
│  👥 Team & Advisors         15%  (15,000,000 GRT)           │
│     ├─ Core Team            10%  (10,000,000 GRT)           │
│     └─ Advisors              5%  (5,000,000 GRT)            │
│     Vesting: 12-month cliff, 36-month linear                │
│                                                             │
│  🏦 Reserve Fund             5%  (5,000,000 GRT)            │
│     └─ Emergency/Migration                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 3.3 Vesting Schedule

```
TEAM & ADVISORS VESTING (15M GRT)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Month 0-12:     0% released (cliff period)
Month 13:       2.78% released
Month 14-48:    2.78% monthly (linear vesting)
Month 48:       100% fully vested

Example for 1M GRT allocation:
├─ Month 0-12:  0 GRT
├─ Month 13:    27,800 GRT
├─ Month 14:    27,800 GRT
└─ Month 48:    1,000,000 GRT total
```

### 3.4 Token Release Schedule

| Quarter | Released Tokens | Circulating Supply | % of Total |
|---------|-----------------|-------------------|-------------|
| Q4 2025 | 25,000,000      | 25,000,000        | 25%         |
| Q1 2026 | 10,000,000      | 35,000,000        | 35%         |
| Q2 2026 | 8,000,000       | 43,000,000        | 43%         |
| Q3 2026 | 7,000,000       | 50,000,000        | 50%         |
| Q4 2026 | 5,000,000       | 55,000,000        | 55%         |
| 2027+   | 45,000,000      | 100,000,000       | 100%        |

---

## 4. System Architecture

### 4.1 High-Level Overview

```
╔═══════════════════════════════════════════════════════════════╗
║                    GRT TOKEN ECOSYSTEM                        ║
╚═══════════════════════════════════════════════════════════════╝


┌─────────────────┐
│                 │
│  FIAT GATEWAY   │  User deposits UAH/USD/EUR
│  (Payment APIs) │  ├─ Monobank
│                 │  ├─ PrivatBank
└────────┬────────┘  └─ Wise/SEPA
         │
         │ 1. Fiat → USDT conversion
         ▼
┌─────────────────┐
│                 │
│ EXCHANGE ENGINE │  Internal P2P + DEX integration
│  (USDT ↔ GRT)   │  ├─ Uniswap V3
│                 │  ├─ Curve Finance
└────────┬────────┘  └─ Internal Pool
         │
         │ 2. USDT → GRT swap
         ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│               ETHEREUM MAINNET                          │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────┐    │
│  │              │  │              │  │             │    │
│  │  GRT Token   │  │   Staking    │  │  Governance │    │
│  │  Contract    │  │   Module     │  │     DAO     │    │
│  │              │  │              │  │             │    │
│  └──────┬───────┘  └──────┬───────┘  └──────┬──────┘    │
│         │                 │                 │           │
└─────────┼─────────────────┼─────────────────┼───────────┘
          │                 │                 │
          │ 3. Token distribution
          ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│                 USER WALLETS                            │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────┐    │
│  │              │  │              │  │             │    │
│  │  MetaMask    │  │ WalletConnect│  │  Ledger     │    │
│  │              │  │              │  │             │    │
│  └──────────────┘  └──────────────┘  └─────────────┘    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 4.2 Smart Contract Layer

```
┌─────────────────────────────────────────────────────────┐
│               SMART CONTRACT ARCHITECTURE               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌────────────────────────────────────────────────┐     │
│  │          GRTToken.sol (ERC-20)                 │     │
│  │  ├─ totalSupply()                              │     │
│  │  ├─ balanceOf(address)                         │     │
│  │  ├─ transfer(address, uint256)                 │     │
│  │  ├─ approve(address, uint256)                  │     │
│  │  └─ transferFrom(address, address, uint256)    │     │
│  └────────────────────────────────────────────────┘     │
│                       │                                 │
│          ┌────────────┼────────────┐                    │
│          │            │            │                    │
│          ▼            ▼            ▼                    │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐               │
│  │          │  │          │  │          │               │
│  │ Staking  │  │Liquidity │  │   Fee    │               │
│  │ Module   │  │ Manager  │  │Distributor│              │
│  │          │  │          │  │          │               │
│  └──────────┘  └──────────┘  └──────────┘               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 5. Core Modules

### 5.1 Staking Module

```solidity
contract StakingModule {
    struct Stake {
        uint256 amount;
        uint256 startTime;
        uint256 lockPeriod;
        uint256 apy;
        bool withdrawn;
    }
    
    mapping(address => Stake[]) public stakes;
    
    // Lock periods & APY
    uint256[4] public LOCK_PERIODS = [30 days, 90 days, 180 days, 360 days];
    uint256[4] public APY_RATES = [5, 10, 18, 30]; // percentage
    
    function stake(uint256 amount, uint8 periodIndex) external {
        require(amount > 0, "Amount must be > 0");
        require(periodIndex < 4, "Invalid period");
        
        token.transferFrom(msg.sender, address(this), amount);
        
        stakes[msg.sender].push(Stake({
            amount: amount,
            startTime: block.timestamp,
            lockPeriod: LOCK_PERIODS[periodIndex],
            apy: APY_RATES[periodIndex],
            withdrawn: false
        }));
    }
    
    function withdraw(uint256 stakeIndex) external {
        Stake storage userStake = stakes[msg.sender][stakeIndex];
        require(!userStake.withdrawn, "Already withdrawn");
        require(
            block.timestamp >= userStake.startTime + userStake.lockPeriod,
            "Lock period not ended"
        );
        
        uint256 reward = calculateReward(userStake);
        uint256 total = userStake.amount + reward;
        
        userStake.withdrawn = true;
        token.transfer(msg.sender, total);
    }
}
```

### 5.2 Liquidity Manager

Управляет внутренним пулом ликвидности для обмена USDT ↔ GRT:

```solidity
contract LiquidityManager {
    uint256 public constant FEE_PERCENTAGE = 30; // 0.3%
    
    IERC20 public grtToken;
    IERC20 public usdtToken;
    
    function swapUSDTforGRT(uint256 usdtAmount) external returns (uint256) {
        uint256 grtAmount = getGRTAmount(usdtAmount);
        uint256 fee = (grtAmount * FEE_PERCENTAGE) / 10000;
        uint256 amountAfterFee = grtAmount - fee;
        
        usdtToken.transferFrom(msg.sender, address(this), usdtAmount);
        grtToken.transfer(msg.sender, amountAfterFee);
        
        return amountAfterFee;
    }
    
    function swapGRTforUSDT(uint256 grtAmount) external returns (uint256) {
        uint256 usdtAmount = getUSDTAmount(grtAmount);
        uint256 fee = (usdtAmount * FEE_PERCENTAGE) / 10000;
        uint256 amountAfterFee = usdtAmount - fee;
        
        grtToken.transferFrom(msg.sender, address(this), grtAmount);
        usdtToken.transfer(msg.sender, amountAfterFee);
        
        return amountAfterFee;
    }
}
```

### 5.3 Fee Distributor

Автоматическое распределение торговых комиссий:

```solidity
contract FeeDistributor {
    // Distribution percentages
    uint256 public constant STAKERS_SHARE = 40;  // 40%
    uint256 public constant LIQUIDITY_SHARE = 30; // 30%
    uint256 public constant TREASURY_SHARE = 20;  // 20%
    uint256 public constant BURN_SHARE = 10;      // 10%
    
    function distributefees(uint256 totalFees) external onlyOwner {
        uint256 stakersAmount = (totalFees * STAKERS_SHARE) / 100;
        uint256 liquidityAmount = (totalFees * LIQUIDITY_SHARE) / 100;
        uint256 treasuryAmount = (totalFees * TREASURY_SHARE) / 100;
        uint256 burnAmount = (totalFees * BURN_SHARE) / 100;
        
        stakingModule.distributeFees(stakersAmount);
        liquidityManager.addLiquidity(liquidityAmount);
        treasury.deposit(treasuryAmount);
        grtToken.burn(burnAmount);
    }
}
```

---

## 6. Exchange Integration

### 6.1 Fiat → USDT → GRT Flow

```
┌─────────────────────────────────────────────────────────────┐
│              DEPOSIT FLOW (Fiat → GRT)                      │
└─────────────────────────────────────────────────────────────┘

┌──────────┐
│   USER   │  1. Initiates deposit: 10,000 UAH
└────┬─────┘
     │
     ▼
┌──────────────────┐
│ Payment Gateway  │  2. Processes payment
│  (Monobank API)  │     ├─ Validates user
└────┬─────────────┘     ├─ Checks limits
     │                   └─ Confirms transaction
     │
     │ 3. Webhook notification
     ▼
┌──────────────────┐
│  GiranTrade API  │  4. Converts UAH → USDT
│                  │     Rate: 41.5 UAH/USDT
└────┬─────────────┘     Result: 241 USDT
     │
     │ 5. Query GRT price
     ▼
┌──────────────────┐
│ Liquidity Pool   │  6. Calculate GRT amount
│  (USDT/GRT)      │     Current rate: 1 USDT = 10 GRT
└────┬─────────────┘     Result: 2,410 GRT
     │
     │ 7. Execute swap
     ▼
┌──────────────────┐
│  Smart Contract  │  8. Transfer GRT to user
│  (Ethereum)      │     ├─ Deduct 0.3% fee (7.23 GRT)
└────┬─────────────┘     └─ Net: 2,402.77 GRT
     │
     │ 9. Tokens delivered
     ▼
┌──────────┐
│   USER   │  10. Receives GRT in wallet
│  WALLET  │      Balance: 2,402.77 GRT
└──────────┘
```

### 6.2 GRT → Fiat Exit Flow

```
┌─────────────────────────────────────────────────────────────┐
│              WITHDRAWAL FLOW (GRT → Fiat)                   │
└─────────────────────────────────────────────────────────────┘

┌──────────┐
│   USER   │  1. Initiates withdrawal: 1,000 GRT
└────┬─────┘
     │
     ▼
┌──────────────────┐
│  Smart Contract  │  2. Burn GRT or swap to USDT
│                  │     ├─ Option A: Direct burn
└────┬─────────────┘     └─ Option B: Swap to USDT
     │
     │ 3. Convert GRT → USDT
     ▼
┌──────────────────┐
│ Liquidity Pool   │  4. Calculate USDT amount
│  (GRT/USDT)      │     Rate: 10 GRT = 1 USDT
└────┬─────────────┘     Result: 100 USDT
     │
     │ 5. Request fiat conversion
     ▼
┌──────────────────┐
│  GiranTrade API  │  6. Convert USDT → UAH
│                  │     Rate: 41.5 UAH/USDT
└────┬─────────────┘     Result: 4,150 UAH
     │
     │ 7. Initiate bank transfer
     ▼
┌──────────────────┐
│ Payment Gateway  │  8. Process payout
│  (Bank API)      │     ├─ KYC check
└────┬─────────────┘     ├─ AML screening
     │                   └─ Fee: 1% (41.5 UAH)
     │
     │ 9. Fiat delivered
     ▼
┌──────────┐
│   USER   │  10. Receives 4,108.5 UAH
│   BANK   │      to bank account
└──────────┘
```

---

## 7. Use Cases

### 7.1 Fee Reduction

```
┌─────────────────────────────────────────────────────────┐
│            TRADING FEE STRUCTURE                        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  GRT Holdings         │  P2P Fee  │  Swap Fee           │
│  ─────────────────────┼───────────┼────────────         │
│  0 GRT                │   0.5%    │   0.3%              │
│  500+ GRT             │   0.4%    │   0.25%             │
│  5,000+ GRT           │   0.25%   │   0.2%              │
│  10,000+ GRT          │   0.1%    │   0.15%             │
│  50,000+ GRT (VIP)    │   0%      │   0.1%              │
│                                                         │
│  Example: 1,000 USDT trade                              │
│  ├─ No GRT:     5 USDT fee                              │
│  └─ 5,000 GRT:  2.5 USDT fee (50% savings)              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 7.2 Staking Rewards

```
┌─────────────────────────────────────────────────────────┐
│              STAKING CALCULATOR                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Stake: 10,000 GRT                                      │
│  Period: 360 days                                       │
│  APY: 30%                                               │
│                                                         │
│  Daily reward:  8.22 GRT                                │
│  Monthly reward: 250 GRT                                │
│  Yearly reward: 3,000 GRT                               │
│                                                         │
│  Total after 1 year: 13,000 GRT                         │
│                                                         │
│  If GRT price = $0.5:                                   │
│  Investment: $5,000                                     │
│  Returns: $6,500                                        │
│  Profit: $1,500 (30% APY)                               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 7.3 Liquidity Mining

```
Provide liquidity to USDT/GRT pool:

1. Deposit equal value:
   ├─ 1,000 USDT
   └─ 10,000 GRT (at 1:10 rate)

2. Receive LP tokens:
   └─ USDT-GRT-LP

3. Stake LP tokens:
   └─ Earn 15% APY in GRT

4. Additional bonuses:
   ├─ Trading fee share: 0.3% of all swaps
   ├─ Impermanent loss protection
   └─ Early LPs bonus: +5% APY for first 3 months
```

### 7.4 DAO Governance

```
Voting Power Calculation:

Base voting power = GRT holdings
Boosted power = Staked GRT × 1.5
Time multiplier = (stake duration in days / 365) + 1

Example:
├─ User holds: 5,000 GRT
├─ Staked: 3,000 GRT for 180 days
└─ Voting power:
    (5,000) + (3,000 × 1.5) + (3,000 × 0.49)
    = 5,000 + 4,500 + 1,470
    = 10,970 votes
```

### 7.5 Loyalty Program

```
┌─────────────────────────────────────────────────────────┐
│              TIER-BASED REWARDS                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Tier        │ GRT Required │ Benefits                  │
│  ────────────┼──────────────┼─────────────────────      │
│  Bronze      │ 100          │ 1% cashback               │
│  Silver      │ 1,000        │ 2% cashback + NFT badge   │
│  Gold        │ 5,000        │ 3% cashback + priority    │
│  Platinum    │ 10,000       │ 5% cashback + VIP         │
│  Diamond     │ 50,000       │ 10% cashback + premium    │
│                                                         │
│  Cashback paid in GRT monthly                           │
│  Tier status reviewed quarterly                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 8. Economic Model

### 8.1 Fee Distribution

```
┌─────────────────────────────────────────────────────────┐
│         PLATFORM FEE ALLOCATION                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Total fees collected: 100%                             │
│  │                                                      │
│  ├─ 40% → Stakers (proportional distribution)           │
│  │         ├─ Distributed weekly                        │
│  │         └─ Auto-compound option available            │
│  │                                                      │
│  ├─ 30% → Liquidity Providers                           │
│  │         ├─ Added to USDT/GRT pool                    │
│  │         └─ Increases pool depth                      │
│  │                                                      │
│  ├─ 20% → Treasury (DAO controlled)                     │
│  │         ├─ Development funding                       │
│  │         ├─ Marketing campaigns                       │
│  │         └─ Strategic partnerships                    │
│  │                                                      │
│  └─ 10% → Token Burn (deflationary mechanism)           │
│            ├─ Permanently removes from circulation      │
│            └─ Increases scarcity over time              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 8.2 Token Burn Mechanism

```
Quarterly Burn Events:

Q1 2026: Burn 1,000,000 GRT (1% of supply)
Q2 2026: Burn based on trading volume
Q3 2026: Burn 10% of collected fees
Q4 2026: Burn based on DAO vote

Burn triggers:
├─ Automatic: 10% of all trading fees
├─ Manual: DAO governance proposals
└─ Milestone: 25% of tokens when TVL hits $10M

Total projected burn over 5 years: 15-20M GRT
```

### 8.3 Value Accrual

```
Token value increases through:

1. Decreased Supply:
   └─ Continuous burns → scarcity

2. Increased Demand:
   ├─ More users need GRT for fee discounts
   ├─ Staking locks up circulating supply
   └─ Liquidity mining incentivizes holding

3. Revenue Sharing:
   └─ Stakers earn from platform profits

4. Utility Expansion:
   ├─ New features require GRT
   ├─ Cross-platform integrations
   └─ NFT marketplace access
```

---

## 9. Roadmap

### ✅ In Progress