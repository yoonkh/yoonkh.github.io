---
layout: post
title:  "블록체인기술의 개념(O'reilly-blockchain)"
date:   2017-12-19
author: Yoonkh
categories: Blockchain
tags:   Blockchain
comments: True
---


**[원문]**
# We may be at the dawn of a new revolution. 

This revolution started with a new fringe economy on the Internet, 
an alternative currency called Bitcoin that was issued and backed not by a central authority, 
but by automated consensus among networked users. 
Its true uniqueness, however, lay in the fact that it did not require the users to trust each other. 
Through algorithmic self-policing, any malicious attempt to defraud the system would be rejected. 
In a precise and technical definition, Bitcoin is digital cash that is transacted via the Internet in a decentralized trustless system using a public ledger called the blockchain. 
It is a new form of money that combines BitTorrent peer-to-peer file sharing1 with public key cryptography.
2 Since its launch in 2009, Bitcoin has spawned a group of imitators—alternative currencies using the same general approach but with different optimizations and tweaks. 
More important, blockchain technology could become the seamless embedded economic layer the Web has never had, 
serving as the technological underlay for payments, decentralized exchange, token earning and spending, digital asset invocation and transfer, 
and smart contract issuance and execution. Bitcoin and blockchain technology, as a mode of decentralization, could be the next major disruptive technology 
and worldwide computing paradigm (following the mainframe, PC, Internet, and social networking/mobile phones), with the potential for reconfiguring all human activity as pervasively as did the Web.


**[번역]**
- 우리는 새로운 혁명의 새벽에 있을지도 모릅니다. 

이 혁명은 중앙 권위가 아니라 네트워크 사용자 간의 자동 합의에 의해 발행되고지지 된 Bitcoin이라는 대체 통화 인 인터넷에서 새로운 프린지 경제로 시작되었습니다. 
그러나 진정한 독창성은 사용자가 서로 신뢰하지 않아도된다는 사실에있었습니다. 
알고리즘 자체 폴링을 통해 악의적 인 시스템 사기 시도가 거부됩니다. 정확하고 기술적 인 정의에서, 
Bitcoin은 블록 체인이라는 공공 장부를 사용하여 분산 된 트러스트리스 시스템에서 인터넷을 통해 거래되는 디지털 현금입니다. 
BitTorrent 피어 투 피어 파일 공유 1과 공개 키 암호화 2를 결합한 새로운 형태의 돈입니다.
2 Bitcoin은 2009 년 출시 이후 동일한 일반적인 접근법을 사용하지만 최적화와 조정이 다른 모방 자 그룹을 탄생 시켰습니다. 
더 중요한 것은 블록 체인 기술은 지불, 분산 형 교환, 토큰 획득 및 지출, 디지털 자산 호출 및 전송, 스마트 계약 체결 및 실행을위한 기술적 인 기반 역할을하는 웹이 없었던 매끄러운 임베디드 경제 계층이 될 수 있습니다. 
분권화 모드 인 Bitcoin 및 블록 체인 기술은 다음과 같은 주요 파괴적인 기술 및 전 세계 컴퓨팅 패러다임 (메인 프레임, PC, 인터넷 및 소셜 네트워킹 / 휴대폰에 이어)으로서 모든 인간 활동을 다음과 같이 광범위하게 재구성 할 수 있습니다.
<br>
<br>
<br>

**[원문]**
# What Is Bitcoin?

Bitcoin is digital cash. 

It is a digital currency and online payment system in which encryption techniques are used to regulate the generation of units of currency and verify the transfer of funds, operating independently of a central bank. 
The terminology can be confusing because the words Bitcoin and blockchain may be used to refer to any three parts of the concept: 
the underlying blockchain technology, the protocol and client through which transactions are effected, and the actual cryptocurrency (money); 
or also more broadly to refer to the whole concept of cryptocurrencies. 
It is as if PayPal had called the Internet “PayPal,” upon which the PayPal protocol was run, to transfer the PayPal currency. 
The blockchain industry is using these terms interchangeably sometimes because it is still in the process of shaping itself into what could likely become established layers in a technology stack.


**[번역]**
- Bitcoin은 무엇인가?

Bitcoin은 디지털 현금입니다. 

이것은 디지털 통화 및 온라인 지불 시스템으로 암호화 기술을 사용하여 통화 단위 생성을 규제하고 중앙 은행과 독립적으로 운영되는 자금의 이체를 확인합니다. 
Bitcoin과 blockchain이라는 단어가 개념의 세 부분, 즉 기본 블록 체인 기술, 트랜잭션이 수행되는 프로토콜과 클라이언트, 실제 암호 화 (돈)를 언급하기 위해 사용되기 때문에 전문 용어가 혼란 스러울 수 있습니다. 
cryptocurrencies의 전체 개념을 언급하는 데 더 광범위하게 사용됩니다. 
마치 PayPal이 PayPal 통화를 전송하기 위해 PayPal 프로토콜이 실행 된 인터넷 "PayPal"을 호출 한 것과 같습니다. 
블록 체인 업계는 때때로 기술 스택에서 확립 된 레이어가 될 수 있는 요소를 형성하는 과정에 있기 때문에 이러한 용어를 서로 바꾸어 사용합니다.
<br>
<br>
<br>

**[원문]**

Bitcoin was created in 2009 (released on January 9, 20096) by an unknown person or entity using the name Satoshi Nakamoto. 
The concept and operational details are described in a concise and readable white paper, 
“Bitcoin: A Peer-to-Peer Electronic Cash System.”7 Payments using the decentralized virtual currency are recorded in a public ledger that is stored on many—potentially all—Bitcoin users’ computers, and continuously viewable on the Internet. 
Bitcoin is the first and largest decentralized cryptocurrency. 
There are hundreds of other “altcoin” (alternative coin) cryptocurrencies, like Litecoin and Dogecoin, but Bitcoin comprises 90 percent of the market capitalization of all cryptocurrencies and is the de facto standard. 
Bitcoin is pseudonymous (not anonymous) in the sense that public key addresses (27–32 alphanumeric character strings; similar in function to an email address) are used to send and receive Bitcoins and record transactions, as opposed to personally identifying information.

Bitcoins are created as a reward for computational processing work, known as mining, 
in which users offer their computing power to verify and record payments into the public ledger. 
Individuals or companies engage in mining in exchange for transaction fees and newly created Bitcoins. 
Besides mining, Bitcoins can, like any currency, be obtained in exchange for fiat money, products, and services. 
Users can send and receive Bitcoins electronically for an optional transaction fee using wallet software on a personal computer, mobile device, or web application.

**[번역]**
- Bitcoin은 2009 년 1 월 9 일에 발표 된 나카 모토 사토시 (Satoshi Nakamoto)라는 이름을 사용하여 알려지지 않은 사람이나 단체에 의해 작성되었습니다. 
개념 및 운영 세부 사항은 간결하고 읽기 쉬운 백서 "Bitcoin : 피어 - 투 - 피어 전자 현금 시스템"에 설명되어 있습니다. 
7 분산 가상 화폐를 사용하는 지급은 잠재적으로 모두에 저장된 공공 장부에 기록됩니다 -Bitcoin 사용자의 컴퓨터 및 인터넷에서 지속적으로 볼 수 있습니다. 
비트 코인 (Bitcoin)은 최초이자 가장 큰 분산 형 크립토 커 런시 (cryptocurrency)입니다. 
Litecoin과 Dogecoin 같은 다른 "altcoin"(대체 동전) cryptocurrencies가 있지만 Bitcoin은 모든 cryptocurrencies의 시가 총액의 90 %를 차지하며 사실상의 표준입니다. 
Bitcoin은 개인 식별 정보가 아니라 공개 키 주소 (전자 메일 주소와 기능면에서 27-32 자의 영숫자 문자열)가 Bitcoins을 보내고 수신하는 데 사용된다는 의미에서 익명입니다 (익명은 아닙니다). 


- Bitcoins은 광업으로 알려진 전산 처리 작업에 대한 보상으로 만들어지며, 사용자가 계산을 통해 공공 장부에 지불을 확인하고 기록합니다. 
개인이나 회사는 거래 수수료 및 새로 생성 된 Bitcoins과 교환하여 광업에 종사합니다. 
광업 외에도 Bitcoins는 통화와 마찬가지로 현금, 제품 및 서비스와 교환 할 수 있습니다. 사용자는 개인용 컴퓨터, 모바일 장치 또는 웹 응용 프로그램에서 Wallet 소프트웨어를 사용하여 선택적 거래 수수료로 Bitcoins을 전자적으로 보내고받을 수 있습니다.
<br>
<br>
<br>

**[원문]**
# What Is the Blockchain?

The blockchain is the public ledger of all Bitcoin transactions that have ever been executed. 
It is constantly growing as miners add new blocks to it (every 10 minutes) to record the most recent transactions. 
The blocks are added to the blockchain in a linear, chronological order. 
Each full node (i.e., every computer connected to the Bitcoin network using a client that performs the task of validating and relaying transactions) has a copy of the blockchain, which is downloaded automatically when the miner joins the Bitcoin network. 
The blockchain has complete information about addresses and balances from the genesis block (the very first transactions ever executed) to the most recently completed block. 
The blockchain as a public ledger means that it is easy to query any block explorer (such as https://blockchain.info/) for transactions associated with a particular Bitcoin address—for example, you can look up your own wallet address to see the transaction in which you received your first Bitcoin.


**[번역]**
- 블록 체인은 지금까지 실행 된 모든 Bitcoin 트랜잭션의 공용 원장입니다. 
광부들이 가장 최근의 거래를 기록하기 위해 매 10 분마다 새로운 블록을 추가함에 따라 지속적으로 증가하고 있습니다. 
블록은 선형, 연대순으로 블록 체인에 추가됩니다. 
모든 전체 노드 (즉, 거래의 유효성을 확인하고 릴레이하는 작업을 수행하는 클라이언트를 사용하여 Bitcoin 네트워크에 연결된 모든 컴퓨터)에는 광부가 Bitcoin 네트워크에 가입 할 때 자동으로 다운로드되는 블록 체인 복사본이 있습니다. 
Blockchain은 창세기 블록 (실행 된 첫 번째 트랜잭션)에서 가장 최근에 완료된 블록까지의 주소 및 잔액에 대한 완전한 정보를 가지고 있습니다. 
공용 장부로서의 블록 체인은 특정 Bitcoin 주소와 관련된 트랜잭션에 대해 블록 탐색기 (예 : https://blockchain.info/)를 쿼리하는 것이 쉽다는 것을 의미합니다. 
예를 들어 자신의 지갑 주소를 조회하여 첫 번째 Bitcoin을받은 거래.
<br>
<br>
<br>


**[원문]**

The blockchain is seen as the main technological innovation of Bitcoin because it stands as a “trustless” proof mechanism of all the transactions on the network. 
Users can trust the system of the public ledger stored worldwide on many different decentralized nodes maintained by “miner-accountants,” as opposed to having to establish and maintain trust with the transaction counterparty (another person) or a third-party intermediary (like a bank). 
The blockchain as the architecture for a new system of decentralized trustless transactions is the key innovation. 
The blockchain allows the disintermediation and decentralization of all transactions of any type between all parties on a global basis.


**[번역]**
- Blockchain은 Bitcoin의 주요 기술 혁신으로 간주됩니다. 
BitCin은 네트워크상의 모든 트랜잭션을 "신뢰할 수없는"증명 메커니즘으로 간주하기 때문입니다. 
사용자는 거래 상대방 (타인) 또는 제 3 자 중개자 (예 : 거래 상대방)와의 신뢰를 쌓고 유지해야하는 것과 달리 "광부 - 회계사"가 관리하는 여러 분산 된 노드에 전 세계에 저장된 공공 장부 시스템을 신뢰할 수 있습니다. 
은행). 분산 된 트러스트없는 트랜잭션의 새로운 시스템을위한 아키텍처 인 블록 체인은 핵심 혁신입니다. 
블록 체인은 모든 유형의 모든 거래를 글로벌 차원에서 모든 당사자간에 분산 및 분권화 할 수 있습니다.
<br>
<br>
<br>


**[원문]**

The blockchain is like another application layer to run on the existing stack of Internet protocols, 
adding an entire new tier to the Internet to enable economic transactions, both immediate digital currency payments (in a universally usable cryptocurrency) and longer-term, more complicated financial contracts. 
Any currency, financial contract, or hard or soft asset may be transacted with a system like a blockchain. 
Further, the blockchain may be used not just for transactions, but also as a registry and inventory system for the recording, tracking, monitoring, and transacting of all assets. 
A blockchain is quite literally like a giant spreadsheet for registering all assets, and an accounting system for transacting them on a global scale that can include all forms of assets held by all parties worldwide. 
Thus, the blockchain can be used for any form of asset registry, inventory, and exchange, including every area of finance, economics, and money; hard assets (physical property); and intangible assets (votes, ideas, reputation, intention, health data, etc.).


**[번역]**
- 블록 체인은 기존의 인터넷 프로토콜 스택에서 실행되는 또 다른 응용 프로그램 계층과 같으며 인터넷에 전체 계층을 추가하여 경제 거래 (즉각적인 디지털 통화 지불 (보편적으로 사용 가능한 cryptocurrency에서)와 장기적이고 복잡한 재무 관리 계약. 
모든 통화, 금융 계약 또는 하드 또는 소프트 자산은 블록 체인과 같은 시스템으로 거래 될 수 있습니다. 
또한 블록 체인은 트랜잭션뿐만 아니라 모든 자산의 기록, 추적, 모니터링 및 트랜잭션을위한 레지스트리 및 재고 시스템으로도 사용될 수 있습니다. 
블록 체인은 말 그대로 모든 자산을 등록하는 거대한 스프레드 시트와 같으며 전 세계 모든 당사자가 보유한 모든 형태의 자산을 포함 할 수있는 글로벌 규모로 거래하는 회계 시스템입니다. 
따라서 블록 체인은 금융, 경제 및 자금의 모든 영역을 포함하여 자산 등록, 재고 및 교환의 형태로 사용될 수 있습니다. 
딱딱한 자산 (물적 재산); 무형 자산 (투표, 아이디어, 평판, 의도, 건강 데이터 등).
<br>
<br>
<br>


**[원문]**
# The Connected World and Blockchain: The Fifth Disruptive Computing Paradigm

One model of understanding the modern world is through computing paradigms, 
with a new paradigm arising on the order of one per decade (Figure P-1). 
First, there were the mainframe and PC (personal computer) paradigms, and then the Internet revolutionized everything. 
Mobile and social networking was the most recent paradigm. 
The current emerging paradigm for this decade could be the connected world of computing relying on blockchain cryptography. 
The connected world could usefully include blockchain technology as the economic overlay to what is increasingly becoming a seamlessly connected world of multidevice computing that includes wearable computing, Internet-of-Things (IoT) sensors, smartphones, tablets, laptops, quantified self-tracking devices (i.e., Fitbit), smart home, smart car, and smart city. 
The economy that the blockchain enables is not merely the movement of money, however; it is the transfer of information and the effective allocation of resources that money has enabled in the human- and corporate-scale economy.


**[번역]**
- 현대 세계를 이해하는 한 가지 모델은 컴퓨팅 패러다임을 통해 이루어지며 새로운 패러다임은 10 년에 한 번씩 발생합니다 (그림 P-1). 
첫째, 메인 프레임과 PC (개인용 컴퓨터) 패러다임이 있었고 인터넷은 모든 것을 혁명적으로 변화 시켰습니다. 
모바일 및 소셜 네트워킹이 가장 최근의 패러다임이었습니다. 이 10 년 동안 현재 떠오르는 패러다임은 블록 체인 (blockchain) 암호화에 의존하는 컴퓨팅의 연결 된 세계 일 수 있습니다. 
연결된 세계는 웨어러블 컴퓨팅, IoT (Internet-of-Things) 센서, 스마트 폰, 태블릿, 랩톱, 수량화 된 자체 추적 장치를 포함하는 멀티 장치 컴퓨팅의 끊임없이 연결된 세상이되고있는 것에 대한 경제적 인 오버레이로서 블록 체인 기술을 유용하게 포함 할 수 있습니다 
(즉, Fitbit), 스마트 홈, 스마트 카, 똑똑한 도시. 블록 체인이 가능하게하는 경제는 단순한 돈의 이동이 아닙니다. 
이는 정보의 이전과 인간 및 기업 규모의 경제에서 돈이 가능하게 한 자원의 효과적인 배분입니다.

**[원문]**

With revolutionary potential equal to that of the Internet, blockchain technology could be deployed and adopted much more quickly than the Internet was, given the network effects of current widespread global Internet and cellular connectivity.

**[번역]**
- 인터넷과 동등한 혁명적 인 잠재력을 지닌 블록 체인 기술은 현재 널리 보급 된 전세계 인터넷 및 셀룰러 연결의 네트워크 효과를 고려할 때 인터넷보다 훨씬 빠르게 배치되고 채택 될 수 있습니다.
<br>
<br>
<br>


**[원문]**

Just as the social-mobile functionality of Paradigm 4 has become an expected feature of technology properties, with mobile apps for everything and sociality as a website property (liking, commenting, friending, forum participation), so too could the blockchain of Paradigm 5 bring the pervasive expectation of value exchange functionality. 
Paradigm 5 functionality could be the experience of a continuously connected, seamless, physical-world, multidevice computing layer, with a blockchain technology overlay for payments—not just basic payments, but micropayments, decentralized exchange, token earning and spending, digital asset invocation and transfer, and smart contract issuance and execution—as the economic layer the Web never had. 
The world is already being prepared for more pervasive Internet-based money: Apple Pay (Apple’s token-based ewallet mobile app) and its competitors could be a critical intermediary step in moving to a full-fledged cryptocurrency world in which the blockchain becomes the seamless economic layer of the Web.


**[번역]**
- Paradigm 4의 소셜 - 모바일 기능이 기술 속성의 기대되는 기능이되고, 모든 것을위한 모바일 앱과 웹 사이트 속성 (좋아하는 것, 댓글 달기, friending, 포럼 참여)으로 된 것처럼, 
Paradigm 5의 블록 체인은 가치 교환 기능에 대한 전반적인 기대. 
Paradigm 5 기능은 지불에 대한 블록 체인 기술 오버레이 (기본 지불뿐 아니라 소액 결제, 분산 된 교환, 토큰 적립 및 지출, 디지털 자산 호출 및 기타 기능)을 통해 끊임없이 연결되고 끊김없는 물리적 세계 멀티 컴퓨터 컴퓨팅 계층의 경험 일 수 있습니다. 
이전, 스마트 계약 체결 및 실행 - 웹에서 결코 볼 수 없었던 경제적 계층. Apple Pay (Apple의 토큰 기반 ewallet 모바일 앱) 및 그 경쟁자는 블록 체인이 완벽 해지는 본격적인 cryptocurrency 세계로 이동하는 중요한 중개 단계가 될 수 있습니다 경제 계층.

![](https://yoonkh.github.io/assets/blockchain.png)
