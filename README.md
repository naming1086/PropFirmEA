# PropFirm EA Fleet Project

> Système automatisé d'Expert Advisors optimisé pour les prop firms (FTMO, E8 Markets, Funding Pips, The5ers)

---

## Objectif

Créer et gérer une flotte de comptes prop firm générant **10-15% mensuel** de manière automatisée et respectant toutes les règles des différentes prop firms.

**Nouveau: Scalper V8** - EA haute fréquence conçu pour passer les challenges rapidement.

---

## Quick Start

### 1. Prérequis

- MetaTrader 5 (ou MT4)
- VPS avec latence <20ms vers broker
- Capital initial pour challenges (~$1,000-2,000)
- Connaissances de base en trading

### 2. Installation

```bash
# 1. Copier les fichiers EA
cp EA/MQL5/*.mq5 /path/to/MT5/MQL5/Experts/
cp EA/MQL5/Include/*.mqh /path/to/MT5/MQL5/Include/

# 2. Copier les configurations
cp config/profiles/*.set /path/to/MT5/MQL5/Presets/

# 3. Compiler l'EA dans MetaEditor
# Ouvrir PropFirm_Scalper_v8.mq5 et compiler (F7)
```

### 3. Configuration (Scalper V8)

1. Ouvrir MT5
2. Attacher l'EA au graphique **M5** (EURUSD recommandé)
3. Charger le preset correspondant à votre prop firm:
   - `Scalper_FTMO_Challenge.set` pour FTMO
   - `Scalper_E8_OneStep.set` pour E8 Markets
   - `Scalper_FundingPips_1Step.set` pour Funding Pips
   - `Scalper_The5ers_Bootcamp.set` pour The5ers
4. Activer l'AutoTrading
5. L'EA trade automatiquement pendant les sessions London/NY

---

## Structure du Projet

```
PropFirmEA_Project/
├── CLAUDE.md                    # Directives du projet
├── README.md                    # Ce fichier
│
├── docs/
│   ├── PROP_FIRMS_RULES.md     # Règles détaillées par prop firm
│   ├── RISK_MANAGEMENT.md      # Guide de gestion du risque
│   └── FLEET_SCALING_STRATEGY.md # Stratégie de scaling
│
├── strategies/
│   ├── SMC_ICT_Strategy.md     # Stratégie principale (Smart Money)
│   ├── Session_Breakout.md     # Stratégie secondaire
│   └── RSI_Divergence.md       # Stratégie tertiaire
│
├── EA/
│   ├── MQL5/
│   │   └── PropFirm_SMC_EA_v1.mq5  # EA principal MT5
│   └── MQL4/
│       └── (à venir)
│
├── config/
│   └── profiles/
│       ├── FTMO_Normal_Challenge.set
│       ├── FTMO_Normal_Funded.set
│       ├── E8_One_Step.set
│       ├── FundingPips_1Step.set
│       └── The5ers_Bootcamp.set
│
├── backtests/                   # Résultats de backtests
├── monitoring/                  # Scripts de monitoring
└── risk_management/             # Outils additionnels
```

---

## Stratégies Incluses

### 1. Scalper V8 (RECOMMANDE pour Challenges)

Scalping haute fréquence multi-paires:
- 4 types d'entrées: Momentum, Breakout, Pullback, Reversal
- 12-15 trades/jour
- Compounding agressif (+25% après 3 wins)
- Mode Turbo si retard sur challenge
- Dashboard compact et lisible

**Paires**: EURUSD, GBPUSD, USDJPY, XAUUSD
**Performance cible**: WR 52-55%, PF 1.3+, **12-15% mensuel**

### 2. SMC/ICT Institutional

Stratégie basée sur les Smart Money Concepts:
- Order Blocks
- Fair Value Gaps
- Liquidity Sweeps
- Break of Structure / Change of Character

**Performance cible**: WR 55-62%, PF 1.6-2.2

### 3. Session Breakout (v1-v7)

Exploitation des breakouts de range (versions précédentes):
- Range Asian/London
- Multiple timeframes
- Scoring de qualité

**Note**: Remplacé par Scalper V8 pour meilleure performance

---

## Prop Firms Supportées

| Prop Firm | DD Max | DD Daily | Profit Split | Scaling |
|-----------|--------|----------|--------------|---------|
| FTMO | 10% | 5% | 80-90% | $2M max |
| E8 Markets | 6-10% | 5% | 80-100% | $1M max |
| Funding Pips | 6-10% | 4-5% | 80-100% | Variable |
| The5ers | 5-10% | 3-5% | 50-100% | $4M max |

---

## Workflow Recommandé

```
PHASE 1 (Mois 1-2): Validation
├── Backtest 5 ans minimum
├── Forward test démo 3 mois
├── Passer 2 premiers challenges
└── Budget: ~$1,500

PHASE 2 (Mois 3-4): Expansion
├── Atteindre 5 comptes funded
├── Premiers payouts
└── Revenus: ~$20,000/mois

PHASE 3 (Mois 5-6): Consolidation
├── Atteindre 8-10 comptes
├── Système automatisé stable
└── Revenus: ~$40,000/mois

PHASE 4 (Mois 7+): Scaling
├── Scaling interne prop firms
├── Expansion horizontale
└── Objectif: $1M+ sous gestion
```

---

## Gestion du Risque

### Circuit Breakers

```
Niveau 1 @ -1.5% jour: Réduire risk 50%
Niveau 2 @ -2.5% jour: Stop 4 heures
Niveau 3 @ -3.5% jour: Stop journée
Niveau 4 @ -4.5% jour: EA OFF
```

### Paramètres par Mode (Scalper V8)

| Paramètre | Challenge | Funded |
|-----------|-----------|--------|
| Risk/Trade | 0.6% | 0.4% |
| Max DD Daily | 4.5% | 4.0% |
| Max Trades/Jour | 15 | 10 |
| RR Cible | 1.2 | 1.5 |
| Compounding | Agressif | Modéré |
| Mode Turbo | Activé | Désactivé |

---

## Backtesting

### Commande

```bash
# Via terminal MT5 ou script
mt5_backtest --ea=PropFirm_SMC_EA_v1 \
             --symbol=EURUSD \
             --period=M15 \
             --from=2019.01.01 \
             --to=2024.12.01 \
             --deposit=100000 \
             --leverage=100
```

### Métriques Cibles

| Métrique | Minimum | Optimal |
|----------|---------|---------|
| Net Profit | >50% | >100% |
| Profit Factor | >1.5 | >2.0 |
| Win Rate | >50% | >55% |
| Max Drawdown | <10% | <6% |
| Recovery Factor | >3 | >5 |

---

## Monitoring

### Dashboard EA

L'EA affiche en temps réel:
- P&L journalier / total
- Drawdown utilisé vs max
- Trades du jour
- Status des filtres
- Structure de marché

### Alertes

- Push notifications sur mobile
- Email pour alertes critiques
- Logs détaillés dans fichier

---

## FAQ

### Quel capital pour commencer?

~$1,000-1,500 pour 2 premiers challenges.

### Combien de temps pour être rentable?

3-6 mois pour valider et avoir des revenus stables.

### Risque de breach?

~10-15% des comptes/an avec bonne gestion du risque.

### Peut-on utiliser sur plusieurs brokers?

Oui, l'EA est compatible avec tout broker MT5.

### Support?

Documentation complète dans /docs/

---

## Roadmap

- [x] EA principal MQL5 (SMC)
- [x] Profiles prop firms
- [x] Documentation stratégies
- [x] Guide risk management
- [x] **Scalper V8 haute fréquence**
- [x] **Dashboard compact V2**
- [x] **Multi-paires (4 paires)**
- [x] **Mode Turbo adaptatif**
- [ ] Backtester V8 sur 6-12 mois
- [ ] Dashboard web monitoring
- [ ] API intégration news
- [ ] Multi-compte manager

---

## Avertissement

Le trading comporte des risques. Les performances passées ne garantissent pas les résultats futurs. Ce projet est fourni à titre éducatif. Utilisez-le à vos propres risques.

---

## Licence

Usage personnel uniquement. Ne pas redistribuer sans autorisation.

---

## Contact

Pour questions ou suggestions, ouvrir une issue dans ce repository.

# 资管公司 EA 集群项目（PropFirm EA Fleet Project）

> 
> 专为挑战资管交易平台（FTMO、E8 Markets、Funding Pips、The5ers）打造的自动化 EA 专家交易系统

---

## 项目目标

搭建并运维一套资管平台账户集群，**自动化实现月收益 10%-15%**，严格遵守各资管平台交易规则。
**新增：Scalper V8** — 高频剥头皮 EA，用于快速通过平台考核阶段。

## 快速上手

### 1. 前置条件

- MetaTrader 5（也可使用 MT4）
- VPS 服务器，到经纪商延迟＜20ms
- 考核阶段初始资金（约 1000–2000 美元）
- 基础交易知识

### 2. 安装步骤

```
# 1. 复制EA源码文件
cp EA/MQL5/*.mq5 /path/to/MT5/MQL5/Experts/
cp EA/MQL5/Include/*.mqh /path/to/MT5/MQL5/Include/
# 2. 复制配置文件
cp config/profiles/*.set /path/to/MT5/MQL5/Presets/
# 3. 在MetaEditor编译EA
# 打开 PropFirm_Scalper_v8.mq5，按F7编译
```

### 3. Scalper V8 配置

1. 打开 MT5
2. 将 EA 挂载到**M5（5 分钟）**图表，推荐品种：EURUSD
3. 加载对应资管平台预设文件：
   - `Scalper_FTMO_Challenge.set` → FTMO 考核账户
   - `Scalper_E8_OneStep.set` → E8 Markets 一步式考核
   - `Scalper_FundingPips_1Step.set` → Funding Pips 一步考核
   - `Scalper_The5ers_Bootcamp.set` → The5ers 训练营账户
4. 开启自动交易（AutoTrading）
5. EA 将在伦敦盘 + 纽约盘时段自动执行交易

## 项目目录结构

```
PropFirmEA_Project/
├── CLAUDE.md                    # 项目开发规范
├── README.md                    # 本说明文档
│
├── docs/
│   ├── PROP_FIRMS_RULES.md     # 各资管平台详细规则
│   ├── RISK_MANAGEMENT.md      # 风险管理手册
│   └── FLEET_SCALING_STRATEGY.md # 账户扩容策略
│
├── strategies/
│   ├── SMC_ICT_Strategy.md     # 核心策略：聪明资金概念
│   ├── Session_Breakout.md     # 次级策略：时段突破
│   └── RSI_Divergence.md       # 第三策略：RSI背离
│
├── EA/
│   ├── MQL5/
│   │   └── PropFirm_SMC_EA_v1.mq5  # MT5主EA程序
│   └── MQL4/
│       └── (待开发)
│
├── config/
│   └── profiles/
│       ├── FTMO_Normal_Challenge.set
│       ├── FTMO_Normal_Funded.set
│       ├── E8_One_Step.set
│       ├── FundingPips_1Step.set
│       └── The5ers_Bootcamp.set
│
├── backtests/                   # 回测结果存放目录
├── monitoring/                  # 监控脚本
└── risk_management/             # 附加风控工具
```

## 内置交易策略

### 1. Scalper V8（**考核阶段首选**）

多品种高频剥头皮策略

- 4 种入场模型：动量入场、突破入场、回调入场、反转入场
- 每日交易 12–15 笔
- 激进复利机制：连续盈利 3 单后仓位 + 25%
- 进度落后考核目标时可开启 Turbo 加速模式
- 内置精简可视化面板
**适用品种**：EURUSD、GBPUSD、USDJPY、XAUUSD
**目标绩效**：胜率 52–55%，盈亏因子 PF≥1.3，**月收益 12–15%**

### 2. SMC/ICT 机构交易策略

基于聪明资金概念（Smart Money Concepts）

- 订单块 Order Blocks
- 公平价值缺口 FVG
- 流动性清扫 Liquidity Sweeps
- 结构突破 / 结构转换 BOS/CHoCH
**目标绩效**：胜率 55–62%，盈亏因子 PF 1.6–2.2

### 3. 时段突破策略（v1-v7 旧版）

区间突破策略（旧版本）

- 亚盘 / 伦敦盘区间交易
- 多时间框架分析
- 交易质量打分机制

> 
> 备注：考核场景已由 Scalper V8 替代，性能更优

## 支持的资管平台

表格

| 资管平台 | 最大总回撤 | 单日最大回撤 | 收益分成 | 账户扩容上限 |
| --- | --- | --- | --- | --- |
| FTMO | 10% | 5% | 80%-90% | 最高 200 万美金 |
| E8 Markets | 6%-10% | 5% | 80%-100% | 最高 100 万美金 |
| Funding Pips | 6%-10% | 4%-5% | 80%-100% | 浮动 |
| The5ers | 5%-10% | 3%-5% | 50%-100% | 最高 400 万美金 |

## 推荐执行流程

```
阶段1（第1–2月）：验证期
├── 至少5年历史数据回测
├── 模拟盘实盘前置测试3个月
├── 通过前2个平台考核
└── 预算：约1500美元

阶段2（第3–4月）：扩张期
├── 落地5个实盘资金账户
├── 开始提取盈利
└── 预期收入：约20000美元/月

阶段3（第5–6月）：稳定期
├── 账户数量达到8–10个
├── 自动化系统稳定运行
└── 预期收入：约40000美元/月

阶段4（第7月起）：规模化
├── 使用资管平台内置扩容机制
├── 横向新增更多账户
└── 长期目标：管理资金规模100万美金+
```

## 风险管理机制

### 熔断保护机制

```
1级：当日亏损达 -1.5% → 风险减半
2级：当日亏损达 -2.5% → 暂停交易4小时
3级：当日亏损达 -3.5% → 当日停止交易
4级：当日亏损达 -4.5% → EA直接关闭
```

### Scalper V8 参数区分（考核账户 / 实盘资金账户）

表格

| 参数 | 考核账户 | 已通过考核实盘 |
| --- | --- | --- |
| 单笔风险 | 0.6% | 0.4% |
| 单日最大回撤 | 4.5% | 4.0% |
| 每日最大交易笔数 | 15 | 10 |
| 目标盈亏比 | 1.2 | 1.5 |
| 复利模式 | 激进 | 温和 |
| Turbo 加速模式 | 开启 | 关闭 |

## 回测说明

### 回测执行命令

```
# MT5终端或脚本执行
mt5_backtest --ea=PropFirm_SMC_EA_v1 \
             --symbol=EURUSD \
             --period=M15 \
             --from=2019.01.01 \
             --to=2024.12.01 \
             --deposit=100000 \
             --leverage=100
```

### 绩效指标目标

表格

| 指标 | 最低标准 | 理想目标 |
| --- | --- | --- |
| 净利润 | >50% | >100% |
| 盈亏因子 PF | >1.5 | >2.0 |
| 胜率 | >50% | >55% |
| 最大回撤 | <10% | <6% |
| 恢复因子 | >3 | >5 |

## 监控系统

### EA 内置面板

实时展示：

- 当日 / 总盈亏
- 已占用回撤 vs 最大允许回撤
- 当日交易记录
- 过滤器状态
- 市场结构信息

### 告警通知

- 手机推送通知
- 重大风险邮件告警
- 完整本地日志文件

## 常见问题 FAQ

### 启动需要多少资金？

约 1000–1500 美元，用于前两个平台考核。

### 需要多久实现稳定盈利？

3–6 个月完成验证，获取稳定收益。

### 触发平台违规（爆考核）概率？

风控执行到位的前提下，每年约 10–15% 账户失败。

### 是否可以在多个经纪商使用？

可以，EA 兼容所有 MT5 经纪商。

### 技术支持？

完整文档存放于 `/docs/` 目录。

## 开发路线图

- MQL5 主 EA（SMC 策略）
- 各资管平台预设配置文件
- 策略文档
- 风险管理指南
- **高频 Scalper V8 剥头皮 EA**
- **V2 精简仪表盘**
- **4 品种多标的交易**
- **自适应 Turbo 模式**
- Scalper V8 6–12 个月回测验证
- Web 网页监控面板
- 新闻事件 API 接入
- 多账户统一管理器

## 风险提示

交易存在高风险。历史绩效不能代表未来收益。本项目仅用于学习教育用途，使用本系统所有风险由使用者自行承担。

## 许可证

仅限个人使用。未经授权禁止二次分发。

## 联系方式

如有问题或建议，在仓库提交 Issue。


