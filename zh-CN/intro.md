# Nervos AppChain 概览 {docsify-ignore-all}


「Nervos AppChain」是一套开源的**应用公链**解决方案。它主要为B端用户解决「搭建区块链困难」和「开发区块链应用困难」这两个问题。我们在市场痛点调研中发现，很多行业或企业联盟有商业资源，具备一定传统应用系统的开发能力，也有意愿搭建一条自己的区块链，但当前市场并没有一个完整的的技术方案来支撑开发。同时，许多的应用开发者们想要开发一些酷炫的区块链应用，但他们常常被以太坊的低性能所拖累。而我们尝试通过推出一套产品，即 Nervos AppChain，来解决这个问题。

## Nervos AppChain 组件


#### CITA | 区块链内核

[![](https://img.shields.io/badge/CITA-Documents-green.svg)](https://cryptape.github.io/cita/)
[![](https://img.shields.io/badge/CITA-GitHub-lightgrey.svg)](https://github.com/cryptape/cita)

Nervos AppChain 的核心组件是采用微服务架构的底层区块链内核 CITA。作为区块链内核，它可以配置成许可链也可以配置成公有链。前者作为成熟产品在过去两年中成功地支撑了多家银行和金融机构的区块链创新业务。后者则专门针对各类商业应用做了改进，包括支持灵活的激励机制（原生代币经济模型）和治理机制（通过智能合约进行记账节点配置、权重分配等）。公有链模式下的CITA由强力节点作为记账节点，其他节点作为同步节点共同维护一个高性能的区块链生态。

CITA 将一个区块链节点的共识、网络、计算、RPC 等功能进行了微服务化拆分，每一个微服务又可以有多个实例，最终这些实例共同完成一个节点的记账功能。这样，我们将区块链性能的扩展问题转化成了节点的扩展问题，当性能不足时，插入一台服务器，分担节点的工作压力即可。同时，我们将共识机制、底层逻辑进行了深度优化，例如采用Rust语言架构所有代码等。最终实现了目前*开源可实证*区块链系统的顶级性能。这是一组实测数据：由4核8G云主机构成的AppChain的性能可达到每秒2900笔简单交易；32核64G云主机组成的AppChain的性能则超过了每秒1.5万笔简单交易。而采用集群构建节点的AppChain性能则更高。这样的性能已经足以应付绝大多数应用场景。

#### Neuron | DApp 钱包

[![](https://img.shields.io/badge/Neuron-Documents-green.svg)](https://cryptape.github.io/neuron-android/)
[![](https://img.shields.io/badge/Neuron-GitHub-lightgrey.svg)](https://github.com/cryptape/neuron-android/)

Neuron 是 Nervos AppChain 产品中的一个核心组件。它提供了现实世界的用户访问区块链世界的入口。Neuron 一方面是 Nervos Network（也兼容以太坊）上用户私钥和各类数字资产、私有产权和私有数据的管理工具，更重要的，它作为一个 DApp 的运行平台，可以允许各种区块链应用以小程序的方式在用户终端直接运行。

设想一个 AppChain 上的区块链游戏开发者，他只需要完成智能合约的核心开发和 DApp 的访问网站开发即可，复杂的私钥管理和数字资产管理业务都由开源的Neuron接管。用户只需要输入 DApp 的 URL 甚至扫码即可访问 DApp 并完成游戏操作。开发者也可以利用流行的支付服务整合到操作页面中，例如使用微信充值购买区块链上的游戏道具。而第三方开发者也可以制作新的 DApp（游戏副本等）与原DApp在智能合约层面交互、实现去中心化协作，共同为用户创造价值。

AppChain 的运营者或者 DApp 开发者也可以选择重构开源的 Neuron 代码，为用户提供更加专业和针对性的服务。相信这将大大降低开发者的门槛，也降低用户的学习难度。

#### Microscope | 区块链浏览器

[![](https://img.shields.io/badge/Microscope-GitHub-lightgrey.svg)](https://github.com/cryptape/microscope/)

Microscope 的目标是打造一个类似 etherscan 的区块链数据访问平台。它提供对区块数据、交易数据、账号地址数据以及智能合约的访问等必备功能。Microscope 支持多链访问，只要给出对应 AppChain 的 RPC 服务地址，即可接入这条区块链并提供数据浏览服务。AppChain 运营方可以部署一个自己的专用浏览器，也可以将访问接口提供给其他浏览器。

未来 Microscope 将增加数字资产访问、结构化数据展示等功能。对应地，我们将提供一个链上 KV 数据自动转换为本地关系型数据的中间件，以方便 DApp 的开发。开发者可以通过中间件快速索引业务数据，为用户提供更加友好的服务。

#### ReBirth | 区块缓存服务器

[![](https://img.shields.io/badge/ReBirth-GitHub-lightgrey.svg)](https://github.com/cryptape/re-birth/)

ReBirth 是一个提供区块链数据缓存服务的服务器端组件。它通过在服务器本地缓存 AppChain 上的数据，为 Microscope 和 Neuron 提供所需的数据缓存和查询服务，加快查询区块数据的速度，提升软件的使用体验。

#### Nervos AppChain SDK | 软件开发工具包

[![](https://img.shields.io/badge/nervos.js-GitHub-lightgrey.svg)](https://github.com/cryptape/nervos.js/)
[![](https://img.shields.io/badge/nervosj-Documents-green.svg)](https://cryptape.github.io/nervosj/)
[![](https://img.shields.io/badge/nervosj-GitHub-lightgrey.svg)](https://github.com/cryptape/nervosj/)

考虑到签名、报文拼装，abi调用等复杂操作，区块链操作对于绝大多数开发者来说都有不小的难度。为此，我们提供了多平台SDK进一步降低开发门槛。目前正在维护的开源SDK包括 JavaScript、Java、Android、Swift 等多个版本，方便开发者使用。（目前我们已经上线了 JavaScript 版本和 Java 版本的 SDK：nervos.js 和 nervosj）

以 JavaScript 版本的 @nervos/chain 为例，DApp 前端在 Neuron 中运行可以自动获得区块链访问接口，并通过该接口请求用户对区块链交易进行数字签名。SDK提供完整的环境检测、区块信息查询、交易信息查询等接口，开发者只需要调用交易接口，其余工作完全由SDK来处理，大大简化开发流程。用户也可以同时使用以太坊的web3 SDK，使得同一个DApp前端同时支持以太坊网络和 Nervos AppChain 网络的业务操作。


## AppChain 特点

#### 灵活部署

AppChain 是完全免费和开放的，任何开发者或运营者都可以下载源代码自己部署一条链，并在自己的链上构建完整的应用生态。开发者和运营方在构建自己的生态时，可以设计并实现自己的经济生态，且不需要购买或提前获得Nervos AppChain 的基础代币。因此，AppChain 的发布和运行完全是由开发者自主主导的。

作为开源产品，开发者可以随时从 GitHub 下载最新版本的 Nervos AppChain 源代码自行编译部署。为了方便开发者更加简单地部署，我们除了提供 docker 这种开发者友好的部署方案之外，还将与华为云等多家云服务商合作，提供一键部署服务。开发者在这些云服务商的网站上选择一键部署 Nervos AppChain 服务，接着输入节点数、原生代币信息等几个必备的参数即可生成一条应用公链。考虑到区块链的去中心化特性，后续加入的节点可以不受限于同一个云服务商的主机。

我们还将与万云等多家BaaS服务商合作，提供 Nervos AppChain 的环境实例，开发者可以直接在万云运维的一条 AppChain 上免费部署 DApp 并向用户发布。这将进一步降低开发门槛。

#### 多链协议

区块链的根本价值在于其形成的链上共识。显然，并不是所有的共识都需要在全球范围内达成一致。例如一个玩家社区、一个供应链金融服务以及一个校友会，他们内部的互动是不需要在全球范围内达成共识的。如果强行要求所有的区块链应用都在同一个环境下达成共识，其结果一定就是 Cryptokitties 这种只有少数人使用的服务会时不时地将以太坊这种定位在全球共识的基础设施服务搞垮。由此可以得出一个非常自然的结论：既然共识是有范围的，区块链本身也应该是有层级和范围的。Nervos AppChain专注于提供特定范围内的应用公链服务，任何应用或行业都可以搭建自己的 AppChain 并构建自己的生态。

在我们的愿景中，未来将会有数百条甚至数万条 AppChain 在并行运行。通过一个开放的多链协议，用户的DApp钱包可以访问任何一条链上的任何 DApp，并同时管理各条链上的资产。对于终端用户来讲，多链之间的切换完全是透明的，其信息交互完全由 Neuron 处理。不论用户使用哪条链，他的地址都是一致的。因此，用户在自己的账户（区块链地址）下可以统一管理各条 AppChain 上的资产，甚至无需知道这个资产在哪条链上。

在这样的设计理念下，不论是DApp开发者还是终端用户，他可以不用关心具体的链信息，而是将所有的AppChain统一看作一个虚拟的 Nervos Network。用户打开 DApp 操作时，基础设施会自动将其定位到 Nervos Network 上的某个具体的 AppChain，执行访问智能合约并发送交易等操作。这也意味着 AppChain 将单一区块链的性能大幅提升后，多链协议将 Nervos Network 作为整体，使得区块链的性能和吞吐率获得了矩阵式的提升。

#### 安全与跨链

熟悉区块链技术走向的开发者可能马上会提出疑问：Nervos AppChain 这样的多链架构是否会带来记账节点作恶的风险，以及如何实现跨链资产流转等功能。如前所述，Nervos Network中除了 Nervos AppChain 多链外，还包含一个重要的基础公链，Nervos CKB（Common Knowledge Base）。CKB 将为所有的 AppChain 提供跨链价值流转与安全性保障。

具体来说，作为应用公链，使用者往往对运营方存在着一定的信任。例如某游戏公司运营一条 AppChain 并将自己的游戏业务逻辑以智能合约的形式在链上执行，或者某核心企业运营一条 AppChain 并将应收账款、商业票据的金融资产数字化上链交易。这些链的使用者对运营方是天然信任的。但即便如此，作为信任基石的区块链仍然需要有“最终仲裁人”，以便在作恶行为出现时能够对作恶者做出惩罚。CKB就是 Nervos Network 中最终仲裁人的角色，一旦 AppChain 的记账人出现作恶行为，例如双花、错误交易打包、忽略出块等等，用户就可以提交相应的数学证明到 CKB 上，罚没这些记账节点在 CKB 上的押金。而CKB本身作为全球基础公链，其安全性由开放竞争的共识协议和全球节点共同保障。当然，作为一个开放的生态，CKB的监督完全是可选的。如果 AppChain 的用户对运营方足够信任，也可以选择由链外机制进行仲裁。我们还将提供跨链交易功能，用户在不同的 AppChain 上锁定资产，可通过第三条 AppChain 或者 CKB 进行去中心化资产交换。



## DApp解决方案

传统上，我们将实现特定业务功能的智能合约集合称为 DApp（Decentralized Application）。DApp的业务逻辑和执行过程都是分布式存储和操作的。不过智能合约作为区块链上的代码块，本身还需前端UI进行访问和操作。因此一个DApp应用除了去中心化的部分之外，还需要部分中心化的服务来提供额外的功能，例如数字资产对应的图片展示等。因此，现在一般认为一个 DApp 包含智能合约、前端访问UI以及后端服务等部分。

### 前端UI
DApp 本质上需要满足为客户提供价值的基本要求。区块链和智能合约只是提供价值的平台和手段。作为与用户直接接触的前端 UI，仍然是应用方开发的重中之重。

开发者可以使用 HTML 在 PC 或移动端为用户提供服务，也可以采用Native程序为用户提供服务。通过开源的 Neuron DApp Wallet（或开发者在其基础上二次开发），开发者只需要开发H5页面，即可为用户提供便捷的 DApp 前端。AppChain 也提供 java/swift/rust 等多种 SDK，方便开发者开发 Native 的应用程序。

### 后端服务
考虑到区块链的RPC接口只能提供kv数据，不宜检索关系型数据，且无法提供区块链之外的扩展信息，因此一般来说DApp 需要一个后端服务来提供支持。例如用户持有的数字资产的虚拟外观、战斗画面等等。

AppChain 提供一个数据缓存层组件，用来将区块链上开发者感兴趣的 kv 数据转换成关系型数据保存下来，并在需要的时候提供检索信息。

### 业务合约

考虑到 AppChain 具有高吞吐量和高性能等特性，我们建议开发者将业务的核心逻辑和资产发行与流转用智能合约实现。在这种情况下，同一个核心业务甚至可以由不同的开发者提供前端UI来访问。并且第三方开发者可以开发新的合约与原核心逻辑合约交互。最终，围绕着一个核心业务逻辑将生产一个生态，它的自由度和用户粘性将远远超过目前常见的开放平台。