# 移动 App 广告联盟：市场、玩家与 SDK 能力全景

> 版本：v0.1 ｜ 更新：2026-10-21 ｜ 定位：移动应用广告变现的行业研究，不构成投放或投资建议。
>
> 口径说明：本文把“广告联盟”限定为 **ADN（Ad Network）+ 聚合层（Mediation）**；SSP/DSP 只在解释处提及。平台规模数字多为公司官方口径，未经独立审计；市场数据来自不同机构，定义不同，不能相加。未披露的数字标注“未披露”，不做估算。

## 一页纸结论

1. **“广告联盟”要分三层看，混在一起会得出错误结论。**  
   - **ADN/联盟**：自己有广告主需求，也聚合开发者流量，如 AdMob、Meta Audience Network、AppLovin、Unity、Mintegral、Pangle、穿山甲、优量汇、快手联盟。  
   - **聚合平台（Mediation）**：把多个 ADN 接进一个 SDK 统一竞价，如 MAX、LevelPlay、AdMob Mediation、GroMore、TopOn、TradPlus。  
   - **程序化交易/SSP**：AdX、PubMatic、Magnite 等，偏库存交易，不是通常说的“联盟”。

2. **市场盘子：全球应用内广告约 3,320 亿美元，但独立广告技术层只有约 790 亿美元。**  
   Altman Solon 测算 2025 年全球应用内广告支出约 **3,320 亿美元**，2030 年约 **6,170 亿美元**，CAGR 约 **13.2%**；其中“独立广告技术平台”的可服务市场（SAM）2025 年约 **790 亿美元**，2030 年约 **1,360 亿美元**。大部分预算仍在 Google、Meta、字节等自有生态内。

3. **中国：2025 年互联网广告约 7,930.8 亿元，增速已降到中个位数；但“广告联盟”没有权威单列口径。**  
   QuestMobile 口径 2025 年中国互联网广告 **7,930.8 亿元，同比 +4.6%**；艾瑞“网络广告（媒体收入，含电商）”口径 2025 年预计 **13,711 亿元**。两者差近一倍，因为统计范围不同。穿山甲、优量汇、快手联盟的收入分别并表在字节、腾讯、快手，未单独披露。

4. **格局：全球 AdMob 覆盖最广，AppLovin 游戏变现最强，Mintegral/Pangle 上升最快；Unity LevelPlay 仍是主流聚合层，但 ironSource Ads 直客需求已于 2026-04-30 停止。**  
   AppLovin 2025 年收入 **54.8 亿美元，同比 +70%**；Mintegral **19.6 亿美元，同比 +35.9%**；Google Network **297.9 亿美元，同比 -1.9%**（AdSense 下降、AdMob 增长）；Unity Grow **12.3 亿美元，同比 +2.4%**。

5. **SDK 能力已经高度同质化，真正拉开差距的是六件事：需求质量与填充率、竞价公平性、归因与数据能力、隐私合规、SDK 性能与跨平台、商业条款。**  
   主流联盟都支持激励、插屏、原生、Banner、Bidding+Waterfall、SSV、ILRD、SKAN/AAK、隐私同意、报表 API；差异在“能不能稳定拿到高价预算”和“是否透明”。

---

## 1. 口径与边界

### 1.1 三层结构

```
广告主 / DSP / 电商 / 游戏发行
        │
        ▼
ADN / 广告联盟：AdMob、Meta、AppLovin、Unity、Mintegral、Pangle、穿山甲、优量汇、快手…
        │
        ▼
聚合层：MAX、LevelPlay、AdMob Mediation、GroMore、TopOn、TradPlus
        │
        ▼
App / 游戏 / 工具 / 内容（流量主）
```

| 概念 | 谁在做 | 收入模式 | 典型代表 |
|---|---|---|---|
| ADN/联盟 | 自有或代理广告主需求，向开发者买量 | 广告差价/分成 | AdMob、Meta、AppLovin、穿山甲 |
| 聚合平台 | 把多个 ADN 接进一个 SDK，统一竞价 | 服务费/差价/自有需求 | MAX、LevelPlay、TopOn、TradPlus |
| SSP/Exchange | 把库存程序化卖出 | 交易费 | AdX、PubMatic、Magnite |
| DSP | 帮广告主实时买量 | 服务费/差价 | DV360、The Trade Desk |
| MMP | 归因与测量 | SaaS 订阅 | AppsFlyer、Adjust、Branch |

**关键区别：**

- **广告支出 ≠ 开发者收入。** 3,320 亿美元是广告主支出；开发者到手还要扣除联盟分成、聚合服务费、无效流量扣款。
- **ADN 收入 ≠ 聚合收入 ≠ 程序化收入。** 公司财报里的“收入”有毛/净口径差异，不能直接相加或排名。
- **投放侧排名 ≠ 变现侧份额。** AppsFlyer 排的是买量/安装，不是 eCPM 或收入份额。

### 1.2 市场规模不是一件事

同一个“中国广告市场”，至少有三种常见口径：

| 口径 | 典型来源 | 大致范围 | 说明 |
|---|---|---:|---|
| 互联网广告 | QuestMobile | 约 7,900 亿元（2025） | 偏互联网广告整体 |
| 网络广告（媒体收入） | 艾瑞咨询 | 约 1.37 万亿元（2025E） | 含电商平台广告，媒体收入口径 |
| 移动广告 | 第三方移动广告报告 | 约 4,800–4,900 亿元 | 更窄的移动端口径 |
| 广告联盟 | 无权威单列 | — | 通常只统计 ADN/聚合层，难以独立核算 |

**结论：** 任何给出精确“中国广告联盟市场规模”的报告，都要先看它是否把 ADN、聚合、程序化、媒体收入混在一起。本文不采用单一“联盟市场规模”数字，而是用 **全球应用内广告支出 + 中国互联网广告大盘 + 可验证的网络侧收入** 三个层次来描述。

---

## 2. 市场盘子

### 2.1 全球：应用内广告 3,320 亿美元，独立层 790 亿美元

| 指标 | 2025 | 2030 | 增速/说明 |
|---|---:|---:|---|
| 全球应用内广告支出 | 约 3,320 亿美元 | 约 6,170 亿美元 | CAGR 约 13.2% |
| 独立广告技术平台 SAM | 约 790 亿美元 | 约 1,360 亿美元 | CAGR 约 11% |
| 非游戏品类 | — | — | CAGR 约 14%，高于游戏 |

来源：Altman Solon 2025 年 11 月研究，转引自 SEC EX-23.3。这里的“独立广告技术平台”指不依赖 Google/Meta/字节自有生态的广告技术层，接近“联盟/聚合”的可服务盘子，但 **SAM 不等于实际收入**。

**怎么读这个数：**

- 3,320 亿美元是**广告主支出**，不是开发者到手收入。
- 790 亿美元是**独立广告技术平台的可服务市场**，不是这些平台的实际营收；它说明大部分应用内广告预算仍在 walled garden（围墙花园）内。
- 非游戏增速高于游戏，电商、短剧、工具、AI 应用是主要增量。

### 2.2 中国：三个口径，差近一倍

| 来源 | 口径 | 2025 规模 | 增长 |
|---|---|---:|---|
| QuestMobile | 中国互联网广告 | **7,930.8 亿元** | 同比 +4.6% |
| 艾瑞咨询 | 网络广告（媒体收入，含电商） | **13,711 亿元（预测）** | 2023–2026 CAGR 9.7% |
| 广告联盟 | 无权威单列 | — | — |

- QuestMobile 预计 2026/2027 年分别 **8,362.6 / 8,847.6 亿元**，增速约 5%–6%。
- 按 QuestMobile 数据推算，PC 广告仅约 2%，OTT/智能硬件约 9.1%，移动端占约 **89%**。
- 艾瑞的 13,711 亿元含电商平台广告，很多并不通过第三方联盟 SDK 变现，所以 **不能当作“广告联盟市场规模”**。
- 穿山甲、优量汇、快手联盟均未单独披露联盟收入；市面上精确到“中国广告联盟 1,200 亿元”之类的数字，大多缺少可核验的一手来源。

### 2.3 可验证的网络侧收入（2025 财年）

| 平台 | 2025 收入 | 同比 | 口径/备注 |
|---|---:|---:|---|
| Google Network（AdMob/AdSense/Ad Manager） | **297.92 亿美元** | **-1.9%** | 毛收入，含 TAC；AdSense 下降、AdMob 增长 |
| AppLovin | **54.81 亿美元** | **+70.0%** | 公司总收入，以 Axon Ads Manager 为主；高毛利平台型收入 |
| Mintegral | **19.61 亿美元** | **+35.9%** | 占汇量科技总收入 95.8%；游戏占 74.6%；平台毛收入 |
| Unity Grow | **12.28 亿美元** | **+2.4%** | 含 Unity Vector/LevelPlay；Q4 约 3.38 亿美元 |
| Meta Audience Network | 未披露 | — | 含在 Meta 广告收入中 |
| Pangle/穿山甲 | 未披露 | — | 含在字节广告收入中 |
| 优量汇 | 未披露 | — | 含在腾讯营销服务中 |
| 快手联盟 | 未披露 | — | 含在快手线上营销中 |

**不要直接比较这张表：**

- Google Network 是毛收入，TAC（流量获取成本）计入成本；AppLovin 是高毛利平台型收入；Mintegral 毛利率约 21%；Unity Grow 还包含非联盟业务。
- 看趋势可以，排名不可以；更不能用它推算“市场份额”。

### 2.4 投放侧排名：AppsFlyer Performance Index 2025

| 类别 | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| iOS 游戏 | Apple Ads | AppLovin | Google Ads | Moloco | Mintegral |
| Android 游戏 | Google Ads | AppLovin | Mintegral | Unity Ads | Meta Ads |
| iOS 非游戏 | Apple Ads | Meta Ads | TikTok for Business | Google Ads | Snapchat |
| Android 非游戏 | Google Ads | Meta Ads | TikTok for Business | Google Marketing Platform | Snapchat |

这是**买量侧**排名，不是变现侧收入份额。AppLovin 在 iOS 游戏与 Apple 的差距在缩小；Mintegral 升至 Android 游戏第 3；非游戏仍是 Google/Meta/TikTok 的主场。

### 2.5 SDK 覆盖率：差异极大，别当市场份额

第三方监测（42matters、Insightrackr、Pixalate）给出的覆盖率差异很大：

- 按 App 数，AdMob 约 **70%–80%**；Unity/AppLovin 约 **15%–55%**。
- 按展示量加权，AppLovin、Meta、Unity 的排名会明显上升。
- 差异来自“按 App 数还是按展示量、Android 还是 iOS、是否含聚合 adapter”。

**不要把单一百分比当成市场份额。** 如果要评估竞争格局，至少同时看：安装量份额、展示量份额、收入份额、SDK 覆盖率，四者结论会不同。

---

## 3. 全球玩家与能力

### 3.1 主要平台对比

| 平台 | 类型 | 需求来源 | 核心能力 | 主要限制 | 适合场景 |
|---|---|---|---|---|---|
| **Google AdMob** | ADN + 聚合 | Google Ads/AdX；全球品牌+效果 | 开屏/App Open、激励、激励插屏、插屏、原生、Banner；官方列 24 个聚合源；Bidding+Waterfall；UMP；ILRD；Firebase/BigQuery；app-ads.txt | 聚合对 Google 需求有天然倾斜；政策严格；游戏 eCPM 不一定最高；中国弱 | 出海基线、非游戏、长尾 App |
| **Meta Audience Network** | ADN | Meta 广告主；社交/再营销 | 激励视频、插屏、原生、Banner、Playable；Bidding-only；通过 MAX/LevelPlay/AdMob 等聚合接入 | 无自有聚合；ATT 后效果波动；格式较少；中国不可用 | Tier-1 非游戏/游戏、再营销 |
| **AppLovin MAX** | 聚合 + ADN | Axon Ads Manager + 25+ 广告网络 + ALX DSP | App Open、Banner、插屏、MREC、原生、激励；统一竞价；ILRD；A/B；流量分组；Adjust | 审核门槛；自有需求参与竞价；集成复杂；小团队不友好 | 规模化游戏、iOS、UA 与变现闭环 |
| **Unity LevelPlay** | 聚合 + ADN | Unity Ads/Vector + iSX + 官方列 27 个网络 | 激励、插屏、Banner/MREC、原生；Bidding/非 Bidding/混合；Unity 引擎集成；A/B | ironSource Ads 直客需求 2026-04-30 停止；格式较少；过渡期不确定性 | Unity 游戏、混合竞价 |
| **Mintegral** | ADN + 变现 | 程序化广告主；游戏/非游戏 | Banner/MREC、插屏、激励、原生、Playable；Bidding+Waterfall；智能出价收入占比 >80%；全球 | 品牌需求较小；非游戏占比低；规模小于巨头 | 游戏、Playable、APAC、iOS |
| **Pangle** | ADN | TikTok for Business；全球/APAC | 激励、插屏、原生、App Open（Beta）、Banner、Playable；RTB；中国穿山甲/GroMore | 部分市场品牌安全/合规更敏感；需求集中；中国与海外分开 | APAC、游戏、短剧、新兴市场 |
| **Liftoff** | ADN | 游戏/性能广告主 | 激励、插屏、Banner、原生、Playable；创意自动化；程序化 | 规模较小；品牌需求有限 | 游戏视频/Playable |
| **InMobi / Moloco / DT Exchange / Amazon Ads** | ADN/区域/垂直 | InMobi：印度/APAC；Moloco：ML/电商；DT：OEM/运营商；Amazon：零售意图 | 全形式/程序化/OEM 预装/零售数据 | 区域或场景集中；规模较小 | 印度/APAC、电商、OEM、零售 |

### 3.2 重点平台画像

**Google AdMob**

需求最广、接入最简单、测量与合规模块最完整，适合做“出海基线”。官方文档列出 24 个聚合源，支持 Bidding + Waterfall、UMP、ILRD、Open Measurement、app-ads.txt、Ad Inspector。缺点是游戏 eCPM 不一定最高，聚合对 Google 需求有倾斜，政策封禁不手软；中国境内基本不用它做主力。

**Meta Audience Network**

社交/品牌/再营销需求强，Bidding-only，通过聚合接入，没有自有聚合。ATT 之后效果波动大，但 Tier-1 的激励和插屏仍值得测试。适合已经有 Meta 买量、需要再营销或品牌溢价的 App；不适合把全部变现押在它上面。

**AppLovin MAX**

本质是“聚合 + Axon 需求”，游戏变现和 UA 闭环最强；ILRD、A/B、流量分组完整。官方 SDK 支持 App Open、Banner、插屏、MREC、原生、激励，没有独立的 Rewarded Interstitial。缺点是审核门槛高、自有需求参与竞价、对小团队不友好；适合已经有规模、需要把 eCPM 和 LTV 打通的游戏团队。

**Unity LevelPlay**

Unity 生态里的默认聚合层，混合竞价成熟；官方文档列出的网络覆盖激励、插屏、Banner/MREC、原生。ironSource Ads 直客需求于 2026-04-30 停止，iSX 程序化需求和 LevelPlay 聚合继续，但需要重新评估填充和 eCPM。适合 Unity 游戏、希望用一个聚合层管理多家 ADN 的团队。

**Mintegral**

游戏程序化 + Playable 创意 + 智能出价。2025 年收入 19.61 亿美元，同比 +35.9%，占汇量科技总收入 95.8%；游戏占 74.6%，非游戏占 23.7%；智能出价产品收入占比超过 80%；官方称日均广告请求接近 4,000 亿次，接入 SDK 的应用接近 12 万款。适合游戏、Playable、APAC、iOS。

**Pangle**

TikTok 需求 + 全广告形式 + 新兴市场。官方支持激励、插屏、原生、App Open（Beta）、Banner、Playable；中国穿山甲官方称 10 万+ 合作 App、8 亿+ DAU、620 亿+ 日请求。适合 APAC、游戏、短剧；部分市场对品牌安全和合规更敏感，需要 blocklist 和素材审核。

**其他区域/垂直平台**

- **Liftoff（Vungle）**：游戏视频、Playable、创意自动化。
- **InMobi**：印度/APAC、电信合作、Glance。
- **Moloco**：机器学习出价、电商/游戏、iOS 表现较强。
- **DT Exchange（原 Fyber）**：OEM/运营商、预装、替代分发。
- **Amazon Ads**：零售购买意图、高 CPM，但区域和库存有限。
- **Yandex Ads**：俄罗斯/CIS。
- **BIGO Ads**：新兴市场、自有流量。
- **adjoe**：激励/Playtime，欧洲团队。
- **Chartboost**：游戏、Playable、直客。

### 3.3 已整合/边缘化的历史品牌

选型时容易看到过期名单，注意这些品牌已经或正在被整合：

- **AdColony** → 并入 Digital Turbine，独立品牌存在感下降。
- **Tapjoy** → 被 ironSource 收购，后随 Unity 整合，主打 Offerwall。
- **Vungle** → 与 Liftoff 合并，现为 **Liftoff Monetize**。
- **Fyber** → 被 Digital Turbine 收购，现为 **DT Exchange**。
- **Smaato** → 被 Verve 收购。
- **Chartboost** → 被 Zynga 收购，随 Take-Two 体系。
- **MoPub** → 2022 年关闭，聚合业务被 AppLovin MAX 接手。

接入前确认“当前法律实体、SDK 生命周期、是否还在一线竞价”，不要按旧文章的名录接。

---

## 4. 中国玩家与能力

### 4.1 主要平台对比

| 平台 | 类型 | 预算来源 | 广告形式 | 竞价/聚合 | 适合 |
|---|---|---|---|---|---|
| **穿山甲** | ADN + GroMore | 字节/抖音电商/117 个行业 | 开屏、激励、插屏、全屏、信息流/原生、Banner、Draw | Bidding+Waterfall；GroMore；SSV；风控 | 国内 IAA 游戏、工具、短剧 |
| **优量汇** | ADN | 腾讯系/直客 | 开屏、激励、原生、插屏、Banner、模板信息流 | Bidding；聚合 adapter；SSV | 国内非游戏、品牌 |
| **快手联盟** | ADN | 快手短视频/直播电商 | 开屏、激励、全屏、信息流、Draw、原生、插屏 | Bidding+Waterfall；SSV；SKAN/ATT | 下沉市场、短剧、游戏 |
| **百度联盟/百青藤** | ADN | 百度搜索/信息流/中小广告主 | 开屏、激励、信息流、插屏、Banner、全屏 | Bidding+Waterfall；SSV | 工具、内容、长尾 |
| **华为 Petal Ads** | OEM/ADN | 华为生态/品牌 | Banner、原生、激励、插屏、开屏、贴片 | HMS Ads Kit；Bidding | 华为设备、海外 HMS |
| **OPPO 联盟** | OEM/ADN | OPPO/一加设备；官方称 4.2 亿 DAU | 开屏、激励、信息流/原生、插屏、Banner、互推盒子、悬浮球 | C2S/S2S Bidding；OpenRTB 2.5；SDK/API/ADS | 国内 Android、预装、IAA |
| **vivo 联盟** | OEM/ADN | vivo 设备；官方称 2.5 亿+ DAU | 开屏、激励、信息流/原生、Banner、插屏 | SDK；样式优选；聚合支持 | 国内 Android、OEM |
| **小米米盟** | OEM/ADN | 小米设备 | 开屏、激励、信息流/原生、Banner、插屏 | SDK/聚合 SDK；Flutter；Unity 通过 JNI | 小米设备、IAA |
| **GroMore** | 聚合 | 穿山甲/优量汇/快手/百度/Sigmob + Mintegral/Klevin | 全形式 | Bidding+Waterfall；SSV；预加载；多进程；鸿蒙 | 国内聚合（穿山甲系） |
| **TopOn** | 聚合 | 30+ 全球网络 | 全形式 | C2S/S2S Bidding；A/B；Open API；官方称 300 亿日请求 | 出海/国内中性聚合 |
| **TradPlus** | 聚合 | 40+ 网络 | 全形式 | Bidding+Waterfall；漏斗分析；交叉推广；LTV | 出海/国内中性聚合 |

### 4.2 重点平台画像

**穿山甲**

国内应用内变现最大的一极，字节/抖音电商预算 + 全广告形式 + GroMore。官方称 10 万+ 合作 App、10.5 万+ 活跃客户、8 亿+ DAU、620 亿+ 日请求，覆盖 117 个行业预算。适合国内 IAA 游戏、工具、短剧；注意政策与广告质量，不要把所有流量押在一家。

**优量汇**

腾讯系预算，开屏/激励/原生/插屏/Banner 齐全，适合国内非游戏和品牌广告主；eCPM 稳定性一般，需要和穿山甲/快手做组合。它的优势是腾讯生态的直客和品牌预算，不是“最高 eCPM”。

**快手联盟**

短视频/直播电商预算，激励、信息流、开屏强；下沉市场和短剧场景有优势。官方 SDK 支持开屏、激励、全屏、信息流、Draw、原生、插屏，支持 SSV、SKAN/ATT。适合短剧、游戏、内容类 App。

**百度联盟/百青藤**

搜索/信息流预算，长尾开发者覆盖好；eCPM 通常低于字节/腾讯，但填充稳定。适合工具、内容、长尾 App，以及需要补填充的国内聚合。

**华为/OPPO/vivo/小米**

本质是“设备厂商联盟”，卖的是系统级入口和自有设备流量。适合预装、系统应用、IAA 游戏；只能覆盖对应品牌设备。华为海外用 Petal Ads，支持 Banner、原生、激励、插屏、开屏、贴片六种形式，适合 HMS 生态和海外华为设备。

**GroMore/TopOn/TradPlus**

聚合层。GroMore 绑定穿山甲生态，支持穿山甲/优量汇/快手/百度/Sigmob，以及 Mintegral/Klevin 等 adapter；TopOn/TradPlus 更强调中立和多网络。选聚合时，**中立性、竞价方式（C2S/S2S）、数据能力、服务费**比“接了多少家”更重要。

> 注意：MAX、LevelPlay、AdMob Mediation、GroMore 都有自有需求，不是完全中立；TopOn、TradPlus 相对更中立，但也要看它们的 exchange/服务费结构。

---

## 5. SDK 能力拆解

### 5.1 七层能力模型

| 能力层 | 具体能力 | 选型判断 |
|---|---|---|
| **广告形式** | 开屏/App Open、激励视频、激励插屏、插屏、原生/信息流、Banner/自适应/可折叠、MREC、Playable、Offerwall、Draw | 核心四件套（激励、插屏、原生、Banner）已标配；开屏/App Open、Playable、Offerwall 是差异化；不是所有联盟全支持 |
| **聚合与竞价** | Waterfall、C2S Bidding、S2S Bidding、Hybrid、统一拍卖、底价、流量分组、A/B、预加载、频次控制 | 问清是“真竞价”还是“瀑布流+比价”；是否支持 S2S；聚合是否偏向自有需求；看 auction log/loss notification |
| **定向与出价** | 地域、设备、OS、运营商、语言、上下文、人群、再营销、Lookalike、排除；CPI/CPA/ROAS/tROAS；PMP/OpenRTB | SDK 通常不做定向；定向在需求侧。SDK 负责传递上下文、同意和标识，不要把投放能力当成变现能力 |
| **测量与归因** | MMP、SKAN/AAK、ATT、Postback、Conversion Value、ILRD、SSV、OM SDK、Viewability、LTV/Cohort、Reporting API | ILRD 是 MAX/LevelPlay 的核心价值；SSV 是激励视频防作弊必备；SKAN/AAK 下确定性下降，需校准 |
| **隐私与合规** | GDPR/CCPA/COPPA/PIPL、TCF v2.2、UMP/CMP、Consent Mode、Age Gate、数据最小化、Privacy Manifest、app-ads.txt/sellers.json | 合规是开发者+联盟+MMP 三方责任；SDK 初始化必须在用户同意之后；儿童/未成年人要单独配置 |
| **工程质量** | 包体、初始化耗时、崩溃/ANR、内存/电量、预加载/缓存、超时/重试、多进程/线程、跨平台、Adapter 版本 | SDK 数量越多，包体/ANR/隐私披露风险越高；优先用聚合 adapter，控制直接集成 SDK 数 |
| **商业运营** | 填充保底、eCPM 底价、结算周期、直客/PMP、专属 AM、政策支持、交叉推广、Offerwall、报表 | eCPM 不是净收入；问清分成、结算、税费、保底、独家条款；看 invalid traffic 扣款规则 |

### 5.2 主流 SDK 的能力覆盖

| 平台 | 广告形式 | 聚合/竞价 | 测量/归因 | 隐私/合规 | 跨平台 |
|---|---|---|---|---|---|
| **AdMob** | 6 种，最全 | 24 个聚合源；Bidding+Waterfall | ILRD、Firebase、BigQuery、OM SDK、app-ads.txt | UMP、TCF、COPPA、美国州隐私 | Android/iOS/Unity/Flutter |
| **MAX** | 6 种，无独立激励插屏 | 25+ 网络；统一竞价；A/B；流量分组 | ILRD、Adjust、报表 API | Consent、隐私清单 | Android/iOS/Unity/Flutter |
| **LevelPlay** | 4 种 | 27 个网络；Bidding/非 Bidding/混合 | ILRD、A/B、报表 | Consent、GDPR | Unity/Android/iOS |
| **Mintegral** | 5 种 | Bidding+Waterfall；智能出价 | ILRD、SSV、报表 | GDPR/CCPA | Android/iOS/Unity/Flutter |
| **Pangle** | 6 种 | RTB；GroMore（中国） | SSV、归因、报表 | 区域合规 | Android/iOS/Unity/Flutter |
| **Meta** | 5 种 | Bidding-only | Meta 归因、MMP | ATT、CCPA | 通过聚合 adapter |
| **穿山甲** | 7 种 | Bidding+Waterfall；GroMore | SSV、归因、报表 | PIPL、OAID、隐私合规 | Android/iOS/鸿蒙 |
| **优量汇** | 6 种 | Bidding；聚合适配 | SSV、报表 | PIPL、隐私合规 | Android/iOS |
| **快手联盟** | 7 种 | Bidding+Waterfall | SSV、SKAN/ATT、报表 | PIPL、隐私合规 | Android/iOS |
| **OEM 联盟** | 5–7 种 | C2S/S2S Bidding | 厂商报表/归因 | PIPL、设备权限 | Android/鸿蒙/Flutter |

### 5.3 广告形式的适用场景

| 形式 | 适用场景 | 关键指标 | 注意 |
|---|---|---|---|
| **开屏/App Open** | App 启动、游戏冷启动 | 展示率、点击率、跳过率 | 国内开屏是刚需；海外 App Open 要避免误触和频繁打扰 |
| **激励视频** | 游戏复活/道具、工具解锁、内容奖励 | 完播率、SSV、eCPM | 奖励必须与广告一致；服务端验证防作弊 |
| **激励插屏** | 中重度游戏、关卡结束 | eCPM、体验 | 不是所有联盟支持；频次要控制 |
| **插屏** | 关卡切换、页面跳转 | 展示率、跳过率 | 避免打断核心流程；注意关闭按钮合规 |
| **原生/信息流** | 内容、电商、工具列表 | CTR、CVR、渲染质量 | 模板渲染 vs 自渲染；素材下载与缓存 |
| **Banner/MREC** | 常驻页面、工具类 | 填充率、Viewability | 自适应/可折叠；不要遮挡内容 |
| **Playable** | 游戏买量、试玩 | 试玩转化、加载时长 | 素材体积大；需要预加载 |
| **Offerwall** | 游戏、工具 | 完成率、ARPU | 用户体验与奖励规则要设计好 |
| **Draw/竖版视频** | 国内信息流 | eCPM、停留时长 | 快手/穿山甲等国内平台常见 |

### 5.4 选型时最容易踩的五个坑

1. **只看 eCPM，不看填充率和净收入。** 高 eCPM + 低填充，ARPDAU 可能更低；还要扣分成、无效流量和聚合服务费。
2. **把聚合平台当中立。** MAX/LevelPlay/GroMore 都有自有需求；TopOn/TradPlus 相对更中立。看 auction log、loss notification、底价规则。
3. **SDK 接得越多越好。** 每多一个 SDK，包体、ANR、隐私披露、合规审查都增加；优先用聚合 adapter，直接集成的 SDK 控制在少数几家。
4. **忽略归因与测量。** iOS ATT/SKAN/AAK 下，平台报表和 MMP 对不上是常态；没有 ILRD/SSV/Postback，优化就是盲人摸象。
5. **合规后置。** SDK 初始化必须在用户同意隐私政策之后；儿童/未成年人、COPPA、PIPL、GDPR 都要单独配置，不能等上线再补。

---

## 6. 选型方法

### 6.1 按场景给组合

| 场景 | 推荐组合 | 说明 |
|---|---|---|
| **国内 IAA 游戏** | 穿山甲 + 优量汇 + 快手联盟；GroMore 或 TopOn 聚合；补 OEM | 预算来源分散，降低单一联盟依赖；OEM 补设备入口 |
| **国内非游戏/工具** | 优量汇 + 穿山甲 + 百度联盟；TopOn/TradPlus | 腾讯/字节/百度预算；OEM 补充 |
| **出海游戏** | MAX 或 LevelPlay + AdMob + AppLovin + Unity Ads + Mintegral + Pangle；Meta 作为 bidder | 一个聚合 + 多个 ADN；不要同时上两个聚合 |
| **出海非游戏** | AdMob Mediation + Meta + TikTok/Pangle + AppLovin；电商加 Moloco/Amazon | AdMob 做基线；Meta/TikTok 做品牌+效果 |
| **小团队/首款 App** | AdMob 单接；到量后再上 MAX/LevelPlay | 降低集成、合规、运维成本 |
| **合规敏感/儿童向** | AdMob + UMP；COPPA/年龄门控；少接 SDK | 先合规，再谈 eCPM |

### 6.2 十个选型问题

1. 目标市场是哪里？中国、出海、还是全球？
2. 品类是什么？游戏、非游戏、电商、工具、短剧？
3. 变现模式是 IAA、IAP 还是混合？
4. DAU/日请求量够不够联盟门槛？
5. 用哪个聚合？是否中立？是否支持 S2S bidding？
6. 是否支持 ILRD、SSV、Postback、报表 API？
7. MMP 用哪家？SKAN/AAK 怎么配？
8. 隐私合规要求是什么？GDPR/COPPA/PIPL/未成年人？
9. SDK 包体、初始化耗时、ANR、跨平台/鸿蒙支持如何？
10. 商业条款：分成、结算周期、保底、独家、无效流量扣款？

### 6.3 评价指标

| 指标 | 说明 | 注意 |
|---|---|---|
| **Fill rate** | 请求中成功返回广告的比例 | 高填充不等于高收入；看有效展示 |
| **eCPM** | 每千次展示收入 | 毛/净口径不同；不同国家/形式不可直接比 |
| **ARPDAU** | 日活用户平均广告收入 | 比 eCPM 更接近业务结果 |
| **Ad LTV** | 用户生命周期广告价值 | 需要 ILRD/ cohort |
| **Retention** | 留存 | 广告频次过高会伤留存 |
| **Latency** | 广告加载/竞价延迟 | 影响用户体验和展示率 |
| **Crash/ANR** | SDK 稳定性 | 多 SDK 集成时重点看 |
| **SDK size** | 包体增量 | 对新兴市场下载转化有影响 |
| **Policy risk** | 封号/合规/广告质量 | 比短期 eCPM 更重要 |
| **Net revenue** | 扣除分成、无效流量后的收入 | 最终看这个 |

---

## 7. 趋势与风险

### 7.1 五个正在发生的变化

1. **非游戏增速高于游戏。** Altman Solon 预计非游戏品类 2025–2030 CAGR 约 14%，高于游戏；电商、短剧、工具、AI 应用是增量。
2. **头部集中与整合继续。** AppLovin 2025 年 +70%、Mintegral +35.9%，而 Google Network -1.9%、Unity Grow +2.4%；Unity 已停止 ironSource Ads 直客需求，行业在“少而大”的方向整合。
3. **AI 进入出价、创意和聚合。** AppLovin Axon、Unity Vector、Mintegral 智能出价（收入占比 >80%）、Playturbo 等，把竞争从“接多少家”转向“模型效率”。
4. **隐私与测量持续收紧。** ATT、SKAN/AdAttributionKit、CMP/UMP、Consent Mode 让确定性归因下降；平台报表、MMP、增量实验要交叉校准。
5. **中国：增速放缓、结构分化。** 互联网广告增速降到中个位数；电商内循环、短剧、小游戏、鸿蒙是结构性机会；合规（PIPL、广告法、未成年人）是硬约束。

### 7.2 主要风险

- **聚合中立性**：自有需求优先、底价不透明、auction log 不完整。
- **广告质量/欺诈**：IVT、点击欺诈、误导性素材、品牌安全。
- **政策/封号**：Google/Meta 政策严格，国内联盟也会因合规/质量处罚。
- **预算波动**：电商大促、游戏发行周期、宏观经济。
- **SDK 供应链**：第三方 SDK 漏洞、权限过度、隐私清单缺失。
- **结算风险**：账期、无效流量扣款、汇率/税费。

---

## 8. 术语表

| 缩写 | 全称 | 一句话解释 |
|---|---|---|
| **ADN** | Ad Network | 广告网络/联盟，聚合供给并用自己的需求售卖 |
| **SSP** | Supply-Side Platform | 供给方平台，代表媒体管理库存和需求 |
| **DSP** | Demand-Side Platform | 需求方平台，帮广告主实时买量 |
| **Mediation** | — | App 内聚合多个广告网络，统一瀑布流/竞价 |
| **RTB** | Real-Time Bidding | 实时竞价 |
| **C2S / S2S Bidding** | Client/Server to Server | 客户端/服务端竞价；S2S 通常更安全、延迟更低 |
| **Waterfall** | — | 按历史 eCPM 顺序请求，逐层降级 |
| **Hybrid** | — | Bidding + Waterfall 混合 |
| **ILRD** | Impression-Level Revenue Data | 展示级收入数据，用于 LTV/ROAS 优化 |
| **SSV** | Server-Side Verification | 激励视频服务端验证，防作弊 |
| **MMP** | Mobile Measurement Partner | 移动测量合作伙伴，如 AppsFlyer、Adjust |
| **SKAN** | SKAdNetwork | Apple 的隐私保护归因框架 |
| **AAK** | AdAttributionKit | Apple 新一代归因框架，与 SKAN 并存 |
| **ATT** | App Tracking Transparency | iOS 跟踪授权 |
| **CMP / UMP** | Consent Management Platform / User Messaging Platform | 同意管理平台；UMP 是 Google 的方案 |
| **TCF** | Transparency and Consent Framework | IAB Europe 的同意框架 |
| **PMP** | Private Marketplace | 私有交易市场 |
| **OpenRTB** | Open Real-Time Bidding | IAB 的程序化竞价协议 |
| **OAID** | Open Anonymous Device Identifier | 中国移动安全联盟的匿名设备标识 |
| **GAID / IDFA** | Google/Apple Advertising ID | Android/iOS 广告标识 |
| **eCPM** | Effective Cost Per Mille | 每千次展示有效收入 |
| **ARPDAU** | Average Revenue Per Daily Active User | 日活用户平均收入 |
| **LTV** | Lifetime Value | 用户生命周期价值 |
| **ROAS / tROAS** | Return on Ad Spend / target ROAS | 广告支出回报/目标回报 |
| **IVT** | Invalid Traffic | 无效流量 |
| **OM SDK** | Open Measurement SDK | 可见性测量 SDK |

---

## 9. 参考资料

### 市场与财报

- Altman Solon《Global in-app advertising study》（2025-11），转引自 SEC EX-23.3：[链接](https://content-archive.fast-edgar.com/20260113/A32LDG2CZC2RIZZ2222A2ZYLHGKNZZ22D282/iron-ex23_3.htm)
- Alphabet 2025 Form 10-K（Google Network 收入）：[SEC](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm)
- AppLovin 2025 Form 10-K：[SEC](https://www.sec.gov/Archives/edgar/data/1751008/000175100826000010/app-20251231.htm)
- Unity 2025 Form 10-K：[SEC](https://www.sec.gov/Archives/edgar/data/1810806/000181080626000011/unity-20251231.htm)
- 汇量科技 2025 年度业绩公告（2026-03-11）：[Mobvista IR](https://www.mobvista.com/)
- QuestMobile《2025 年中国营销市场年度报告》（2026-03-24）：[报告页](https://www.questmobile.com.cn/research/report/2036335887177060354)
- 艾瑞咨询《2025 年中国互联网营销市场研究报告》（2025-03）：[iResearch](https://www.iresearch.com.cn/)
- AppsFlyer Performance Index 2025：[报告页](https://www.appsflyer.com/resources/reports/performance-index/)

### 平台与 SDK 文档

- Google AdMob 快速接入（广告形式/平台）：[文档](https://developers.google.com/admob/android/quick-start)
- AdMob Mediation 聚合源：[文档](https://developers.google.com/admob/android/mediation)
- Unity LevelPlay 聚合网络矩阵：[文档](https://docs.unity.com/en-us/grow/levelplay/platform/fundamentals/mediated-networks)
- Unity ironSource Ads 直客需求停止说明：[FAQ](https://unity.com/products/ironsource-ads-sunset)
- AppLovin MAX Android SDK（格式/网络）：[GitHub](https://github.com/AppLovin/AppLovin-MAX-SDK-Android)
- Pangle 全球：[官网](https://www.pangleglobal.com/)
- 穿山甲（中国）：[官网](https://www.csjplatform.com/)
- Mintegral：[官网](https://www.mintegral.com/en/)
- Meta Audience Network：[官网](https://www.facebook.com/audiencenetwork/)
- 优量汇：[官网](https://e.qq.com/)
- 快手联盟：[官网](https://u.kuaishou.com/)
- 百度联盟：[官网](https://union.baidu.com/)
- 华为 Ads Kit/Petal Ads：[文档](https://developer.huawei.com/consumer/cn/doc/hiai-guides/ads-kit-introduction)
- OPPO 联盟：[官网](https://u.oppomobile.com/)
- vivo 联盟：[开发者页](https://dev.vivo.com.cn/promote/adSense)
- 小米米盟：[文档](https://dev.mi.com/xiaomihyperos/documentation/detail?pId=2089)
- TopOn（300 亿日请求/30+ 网络）：[官方帮助中心](https://help.toponad.net/docs/mSI16D)
- TradPlus（40+ 网络）：[文档](https://docs.tradplusad.com/)
- GroMore 第三方网络：[官方文档](https://www.csjplatform.com/supportcenter/5848)

### 口径说明

- 本文把“广告联盟”限定为 **ADN + 聚合层**；SSP/DSP 只在解释处提及。
- 未披露的数字标注“未披露”，不做估算；厂商规模数据为官方口径，未经审计。
- 市场数据来自不同机构，定义不同，不能相加；投放侧排名、SDK 覆盖率、收入份额是三种不同指标，不能混用。
- 数据截至 2026 年 10 月；接入前请以各平台最新官方文档和政策为准。
- 本文件由 `sync.sh` 自动同步至 GitHub 仓库 `jiangjinfeng/rta-advertising-notes`。
