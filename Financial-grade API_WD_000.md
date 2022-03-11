# Financial Services – Financial-grade API
## 警告

该文档不是OIDF(OpenID Foundation)的国际标准，发布该文档的目的是供大家审阅与评价。因此，如果该文档出现变更，恕不另行通知。此外，也不允许称其为国际标准。
> This document is not an OIDF International Standard. It is distributed for review and comment. It is subject to change without notice and may not be referred to as an International Standard.


我们邀请本草案的受益方给予宝贵意见，并且如果觉察到我们存在侵犯相关专利的情况，请告知我们，并提供相关的证明材料。
> Recipients of this draft are invited to submit, with their comments, notification of any relevant patent rights of which they are aware and to provide supporting documentation.


## 版权声明

对任何贡献者、开发者、实现者或其他有兴趣的相关方，OpenID基金会(OIDF)都授以非独占性、免版税以及全球范围内的版权许可，可用于复制、衍生、分发、实践或展示该规范。
本草案或最终规范仅用于以下目的：

1. 进一步完善规范；
1. 根据这些文档实践本草案或最终规范；

必须注明资料来源为OIDF，但该类注明并不表示获得OIDF的背书。
> The OpenID Foundation (OIDF) grants to any Contributor, developer, implementer, or other interested party a non-exclusive, royalty free, worldwide copyright license to reproduce, prepare derivative works from, distribute, perform and display, this Implementers Draft or Final Specification solely for the purposes of (i) developing specifications, and (ii) implementing Implementers Drafts and Final Specifications based on such documents, provided that attribution be made to the OIDF as the source of the material, but that such attribution does not indicate an endorsement by the OIDF.


该规范中描述的技术由多个来源方贡献，其中包含OpenID基金会或其他第三方。虽然OpenID基金会已经采取一些方法以保障这些技术的可用性，但对于与本文档中所描述的技术实现或使用有关的任何知识产权问题，OpenID基金会不持任何立场。OpenID基金会和本规范的贡献者不做(并在此明确声明不做任何)保证(明示、暗示或其他)，包括与本规范相关的可销售性、非侵权性、对特定用途的适用性或所有权，实践本规范的全部风险由实现者承担。OpenID知识产权策略要求贡献者提供专利承诺，不对其他贡献者和实现者提出某些专利要求。OpenID基金会期望任何有兴趣的相关方，需要注意在实践该规范时用到的技术可能涉及到的任何版权、专利、专利申请问题。
> The technology described in this specification was made available from contributions from various sources, including members of the OpenID Foundation and others. Although the OpenID Foundation has taken steps to help ensure that the technology is available for distribution, it takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the implementation or use of the technology described in this specification or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any independent effort to identify any such rights. The OpenID Foundation and the contributors to this specification make no (and hereby expressly disclaim any) warranties (express, implied, or otherwise), including implied warranties of merchantability, non-infringement, fitness for a particular purpose, or title, related to this specification, and the entire risk as to implementing this specification is assumed by the implementer. The OpenID Intellectual Property Rights policy requires contributors to offer a patent promise not to assert certain patent claims against other contributors and against implementers. The OpenID Foundation invites any interested party to bring to its attention any copyrights, patents, patent applications, or other proprietary rights that may cover technology that may be required to practice this specification.


## 序言

OIDF (OpenID Foundation)是一个国际化标准机构，由160多个参与实体组成。编制国际标准的工作是OIDF工作组根据OpenID Process进行的，对已成立工作组感兴趣的参与方都有权利加入工作组。国际组织，包括政府和非政府组织，在与OIDF的联络下，也参与到该工作中来。OIDF持续与相关领域的其他标准化机构保持紧密合作关系。
> OIDF (OpenID Foundation) is an international standardizing body comprised by over 160 participating entities (working group participants). The work of preparing international standards is carried out through OIDF working groups according to OpenID Process. Each participants interested in a subject for which a working group has been established has the right to be represented on that working group. International organizations, governmental and non-governmental, in liaison with OIDF, also take part in the work. OIDF collaborates closely with other standardizing bodies in the related fields.


国际标准是根据OpenID Process中给出的规则起草的。
> International standards are drafted in accordance with the rules given in the OpenID Process.


工作组的主要任务是起草实施者草案以及最终草案。最终草案的通过需要OIDF成员进行表决，至少需要50%以上的成员批准才能作为OIDF标准发布。
> The main task of working group is to prepare Implementers Draft and Final Draft. Final Draft adopted by the Working Group through consensus are circulated to the OIDF members for voting. Publication as an OIDF Standard requires approval by at least 50 % of the member bodies casting a vote.


请注意，该文档的某些内容可能涉及专利权相关问题，OIDF对识别此类专利权不负任何责任。
> Attention is drawn to the possibility that some of the elements of this document may be the subject of patent rights. OIDF shall not be held responsible for identifying any or all such patent rights.


Financial API由以下几个部分组成，其父标题为Financial Services — Financial API:

- 1：只读接口的安全总则
- 2：读写接口的安全总则
- 3：开放数据接口
- 4：只读接口
- 5：读写接口
> Financial API consists of the following parts, under the general title Financial Services — Financial API:
> - Part 1: Read Only API Security Profile
> - Part 2: Read & Write API Security Profile
> - Part 3: Open Data API
> - Part 4: Read Only API
> - Part 5: Read & write API


## 简介

Financial API的目标是提供安全总则和建议、JSON数据模板和REST API，用于实现：

- 使用金融机构账户相关数据的应用
- 使用金融机构账户进行交易的应用(如发起付款或添加收款人)
> The goal of the Financial API is to provide security profiles & recommendations, JSON data schemas and a REST API to enable:
> - applications to utilize the data relating to a financial account,
> - applications to interact with the financial account (for example to initiate a payment or add a payee)


该规范主要有两类用例：

1. 金融机构或服务提供方将该规范用于自己的应用程序和服务
1. 金融机构或服务提供方将该规范用于开放自己的接口，以供第三方应用程序和服务使用
> There are two main use cases for this standard:
> 1. A Financial Institution or Service Provider uses the standard for it’s own applications and services.
> 1. A Financial Institution or Service Provider uses the standard to expose an API for third party applications and services to use.


第二类用例将使市场从目前脆弱且不安全的"screen scraping"(译者注：关于屏幕抓取技术，可以了解如[https://www.uipath.com.cn/product/studiox/](https://www.uipath.com.cn/product/studiox/))实践，转变为具有结构化数据和强大安全模型的健壮API。
> The second use case will allow the market to transition from the current practice of “screen scraping”, which is brittle and insecure, to a robust API with structured data and a strong security model.


该规范分为五个部分，实施者可以根据自己的实际情况选择要实现的部分。
> The standard has been split into 5 parts to enable implementers to select the appropriate part(s) of the standard for their use-case.


# Financial Services – Financial API

## 范围

该规范的范围：

- 包含只读操作的金融级接口的安全总则和建议
- 包含读写操作的金融级接口的安全总则和建议
- 开放数据相关接口的JSON数据模型和REST规范，如ATM位置或产品信息等数据
- 读取金融机构账户数据相关接口的JSON数据模型和REST规范
- 金融机构账务交易相关接口的JSON数据模型和REST规范

> The scope of the standard is:
> - Security profile and recommendations for read-only financial APIs
> - Security profile and recommendations for read & write financial APIs
> - JSON data schemas and REST specifications for open data such as ATM locations or product information
> - JSON data schemas and REST specifications for reading financial data relating to financial accounts.
> - JSON data schemas and REST specifications for interacting with financial accounts.


Web Payments不在此规范的描述范围内。
> Web Payments are out of scope of this standard.


## 规范引用

对本文档而言，以下的规范必不可少。对标注日期的规范，仅引用的版本适用，而未标注日期的文档，其最新版本(包括所有修订)也适用本规范。
> The following referenced documents are indispensable for the application of this document. For dated references, only the edition cited applied. For undated references, the latest edition of the referenced document (including any amendments) applies.


- RFC 6749 - The OAuth 2.0 Authorization Framework
- RFC 7636 - Proof Key for Code Exchange by OAuth Public Clients
- RFC 5246 - The Transport Layer Security (TLS) Protocol Version 1.2
- RFC 7525 - Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS)
- RFC 6125 - Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security (TLS)
- OpenID Connect Core 1.0 incorporating errata set 1
- OpenID Connect Discovery 1.0 incorporating errata set 1
- OAuth 2.0 Multiple Response Type Encoding Practices
- Open Financial Exchange 2.2
- “HTML 4.01 Specification,” World Wide Web Consortium Recommendation REC-html401-19991224, December 1999

## 术语和定义

就本规范而言，适用RFC6749、RFC6750、RFC7636、OpenID Connect Core中定义的术语。
> For the purpose of this standard, the terms defined in RFC6749, RFC6750, RFC7636, OpenID Connect Core applies.


## 缩略语

API – Application Programming Interface

FI – Financial Institution

HTTP – Hyper Text Transfer Protocol

REST – Representational State Transfer

TLS – Transport Layer Security

## API概览
### 消息传输
Financial API要求使用HTTP，这是一种可靠的同步且无状态的消息传输协议。推荐REST风格，因为它可以将消息语法本身和传输相关的关注点进行解耦(译者注：翻译不准确。猜测可能指REST将资源定位、资源操作和资源操作状态分离到HTTP协议来承载，所以消息语法本身可以只关注数据)，REST支持内容类型协商、条件获取和压缩。
> Financial API requires the use of HTTP, which is a reliable synchronous stateless message protocol. REST is preferred because it decouples the message syntax from the transport concerns. REST supports content type negotiation, conditional fetches, and compression.


由于正在交换私密信息，因此必须根据RFC 7525中的建议，使用TLS/SSL(HTTPS)对所有交互进行加密。在撰写本文时，TLS 1.2版是最新版本。
> Since confidential information is being exchanged, all interactions must be encrypted with TLS/SSL (HTTPS) in accordance with the recommendations in RFC 7525. At the time of this writing, TLS version 1.2 is the most recent version.


为了防止信息泄露和篡改，必须使用带有密码套件(非对称、对称及消息摘要算法)的TLS来提供机密性和完整性保障。
> To protect against information disclosure and tampering, confidentiality protection MUST be applied using TLS with a cipher suite that provides confidentiality and integrity protection.


无论何时使用TLS，都必须根据RFC 6125进行TLS服务器证书检查。
> Whenever TLS is used, a TLS server certificate check MUST be performed, per RFC 6125.


## 服务的交付能力要求
Financial API服务端必须在请求到达的30秒内响应客户端。服务端应该使用HTTP 100或200状态码来延长大型数据集的响应时间。服务端响应应该在120秒内完成，以避免长事务。
> The Financial API server response to requests must start within 30 seconds. The server may use HTTP 100 continue or 200 chunked encoding response to extend the response time for large data sets. Server responses should not last longer than 120 seconds to prevent long running transactions.


## 消息语法
Financial API支持JSON格式的语法。
> Financial API supports the JSON syntax.


## 安全
### 模型

Financial API使用OpenID Connect 1.0协议进行身份认证和授权。
> Financial API uses the OpenID Connect 1.0 protocol for authentication and authorization.


OpenID Connect Core 1.0的3.1.3节，详细介绍Financial API客户端如何获取OAuth访问令牌的流程。
> The details of how a Financial API client obtain an OAuth access token are covered in Section 3.1.3 of OpenID Connect Core 1.0.


Financial API客户端必须持有以下信息，才能成功与Financial API服务器进行交互：

1. OAuth授权服务器
   1. 授权端点，如：[https://oauth.example.com/authorization](https://oauth.example.com/authorization)
   1. 客户端标识，如：intuit.com
   1. 请求的授权范围("accounts", "customer", "images", "transfer", "transactions")
   1. 重定向端点，如：[https://oauth.intuit.com/client](https://oauth.intuit.com/client)
   1. Token端点，如：[https://oauth.example.com/token](https://oauth.example.com/token)(译者注：此处链接做了修改，fapi原文应该存在笔误)
   1. 客户端身份认证方法以及支持Client credentials模式
   1. (可选的)客户端身份认证证书
   1. 授权服务器的证书信任链
2. Financial API服务器(OAuth资源服务器)
   1. 资源服务端点，如：[https://data.example.com](https://data.example.com)
   1. 客户端授权(Bearer or MAC token)
   1. (可选) 客户端认证证书。除访问和刷新令牌外，可使用双向认证进行客户端代理身份验证
   1. 资源服务器的证书信任链，客户端需要确保服务器的SSL证书位于其信任库中
> The Financial API client must have the following information to successfully interact with a Financial API server:
> 1. OAuth Authorization Server
a. Authorization endpoint, e.g. [https://oauth.example.com/authorization](https://oauth.example.com/authorization)
b. Client identifier, e.g. intuit.com
c. Requested scope ("accounts", "customer", "images", "transfer", "transactions")
d. Redirection Endpoint, e.g. [https://oauth.intuit.com/client](https://oauth.intuit.com/client)
e. Token endpoint, e.g. [https://oauth.example.com/authorization](https://oauth.example.com/authorization)
f. Client Authenciation Method and Client credentials (JWT or shared secret)
g. Optional client authentication certificate
h. Authorization Server Certifying Authority public key chain
> 1. Financial API Service (OAuth resource server)
a. Endpoint, e.g. [https://data.example.com](https://data.example.com)
b. client authorization (Bearer or MAC token)
c. (Optional) client authentication certificate. Use mutual authentication for access by the client agents in addition to the refresh or access token.
d. Resource Server Certifying Authority public key chain. Client will need to make sure server SSL certificate CA is in their trust store.


金融机构的授权服务器必须支持RFC 6749的4.1章节中定义的授权码模式，并且强烈建议其支持OAuth2.0多种响应类型(OAuth 2.0 Multiple Response Type)中定义的"code id_token"类型。
> The FI's Authorization Server MUST support Authorization Code Grant OAuth as defined in section 4.1 of RFC6749 with PKCE [RFC7636] extension, and highly RECOMMENDED to support "code id_token" response type as defined in OAuth 2.0 Multiple Response Type Encoding Practices.


授权服务器应该根据OpenID Connect Discovery中第4章节定义的机制去发布信息。
> Authorization Server SHOULD publish this information through a discovery file defined in section 4 of OpenID Connect Discovery.


### 客户端认证

推荐使用网络层的双向认证以及OAuth 2.0定义的授权码模式和Bearer Token模型来保障客户端和金融机构的通信安全。
> The recommended approach to securely communicate between a client and FI is through use of both network transport mutual authentication and message security as defined by the use of the OAuth 2.0 Authorization Code Grant and Bearer Token model. Alternative supported methods are outlined below.


网络层的认证基于双向TLS/SSL连接实现，用于客户端和金融机构间的所有Web服务调用，如OAuth令牌服务和数据获取操作。X.509证书必须由授权的证书颁发机构签发和验证，这将在客户端和金融机构之间提供数据来源认证，保障数据完整性和数据机密性。
> Network transport mutual authentication will consist of a two way TLS/SSL network connection used for all web service calls made between the client and FI for both OAuth token and data acquisition operations. The X.509 certificates must be issued and validated by an authorized certificate authority. This will provide data origin authentication, data integrity, and data confidentiality between the client and FI.


客户端系统必须能保证每个金融机构凭证(译者注：应该指Bearer Token或MAC Token)的机密性(比如，在安全的服务器上部署客户端，且对客户端凭证仅具有受限的访问权限)。
> The client system must be capable of maintaining the confidentiality of their credentials for each FI (e.g. client implemented on a secure server with restricted access to the client credentials).


X = Recommended x = Alternatives supported

//TODO

(译者注：不理解该表含义，该表似乎未完成？)
// Table 6.2

| Network Transport TLS/SSL | Client Authentication | Token Type |
| --- | --- | :---: |
| Server Side               Mutual Authentication      Authentication | Shared Secret         JWT | Bearer         Mac |
| X | X | X |
| X | X | X |
| X | X | X |


服务端认证 - 仅进行服务端认证，用于在网络传输过程中向客户端证明其身份。
> Server Side Authentication – Only the Server authenticates itself, assuring its identity to the client across the network transport.


双向认证 - 服务端和客户端双向认证，在网络传输过程中可以确保彼此的身份。
> Mutual Authentication – Enables both Client and Server to authenticate to each other, assuring each other's identity across the network transport.


符合FFIEC(联邦金融机构检查委员会)对身份认证的指南，用于减轻安全风险。
> In line with FFIEC (Federal Financial Institutions Examination Council) guidance on Authentication to mitigate security risks.


当调用金融机构的Financial API数据服务时，Financial API客户端将根据协商好的编码处理访问令牌，并置于HTTP的Authorization头中。
> When invoking the FI's Financial API data service, the Financial API client will provide an Authorization header with the access tokens encoded per the agreed encoding.


支持多个授权服务器的客户端，必须为每个授权服务器分配唯一的redirect_uri，这将缓解因混淆ID Token签发方和授权服务器所导致的安全问题。
> Clients that support multiple Authorization Servers MUST use a unique _redirect_uri_ for each Authorization Server.  This will mitigate security issues where there is a mix-up of the issuer of the ID Token and Authorization Server.


在移动设备上运行的客户端，必须如RFC 7636章节4所描述的，开启PKCE机制。
> Clients running on “mobile devices” MUST send PKCE enabled authorization and token endpoint requests as described in section 4 of RFC 7636.


### 令牌域

当用户离线时，Financial API也允许访问用户的个人金融信息。为了获取用户离线时也能维持用户同意和授权的、有效的访问令牌，授权请求的scope参数中必须包含openid和offline_access域，此时如OpenID Connect Core 1.0章节12所描述的，授权请求的响应中将包含刷新令牌，用于换取访问令牌。
> The Financial API allows access to the user's private financial information while the user is offline. To obtain consent and authorization for an access token that  can be used while the user is offline, the authorization request MUST contain the _openid_ and _offline_access_ values in the _scope_ parameter. A refresh token will be returned in the authorization response that can be exchanged for an access token as described in Section 12 of OpenID Connect Core 1.0.


当请求获取访问令牌时，Financial API客户端需要明确所需的授权范围，Financial API数据服务定义了以下范围：

| 主体 | 授权的操作 | 范围 |
| --- | --- | --- |
| Account | 对账户摘要信息的只读操作 | FinancialInformation |
| Customer | 对用户信息的只读操作，包含个人验证信息 | FinancialInformation |
| Image | 对交易图像的只读操作(支票或收据) | FinancialInformation |
| Statement | 对对账单图像的只读操作 | FinancialInformation |
| Transfer | 转账操作 | Transfer |
| Transaction | 交易信息的只读操作 | FinancialInformation |


> The Financial API client application will include a list of desired scopes when requesting an authorization token. The following scopes are defined for Financial API data service.
> 
| Primary Entity | Allowed Actions | Token Scope |
| --- | --- | --- |
| Account | Read only Access to summary account information | FinancialInformation |
| Customer | Read only Access to customer information, including PII | FinancialInformation |
| Image | Read only Access to transaction images (checks and receipts) | FinancialInformation |
| Statement | Read only Access to statement image | FinancialInformation |
| Transfer | Transfer of money between accounts | Transfer |
| Transaction | Read only Access to transaction information | FinancialInformation |



Financial API服务器会通过签发授权令牌的方式返回允许访问的域的列表。
> The Financial API server will return the list of allowed scopes with the issued authorization token.


Financial API服务端可以通过限制域的范围，来达到不实现某些API的目的。
> The Financial API server may limit the scopes for the purpose of not implementing certain APIs.


最终用户登录后，Financial API服务器还可以在"用户同意"页面显示范围，明确每个帐户的访问权限。
> The Financial API server may also present scopes in the access confirmation page after end user login to have them determine each account(s) access for the requesting application.


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1848672/1601639469758-4ae1d8c5-fd00-4829-81c3-0acc8ccbcfd2.png#align=left&display=inline&height=398&margin=%5Bobject%20Object%5D&name=image.png&originHeight=796&originWidth=1068&size=426327&status=done&style=none&width=534)

## 业务数据模型

Financial API最终将包含多个金融数据域，此时，需要实体和消息来支持个人金融数据的聚合。业务数据模型由用户、登录、帐户、交易明细、对帐单和图像实体组成。
> Financial API will eventually encompass multiple financial data domains. At this point, entities and messages are required to support the aggregation of personal financial data. The logical data model consists of User, Login, Account, Transaction, Detail, Statement and Image entities.


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1848672/1601639500973-56d93b3b-2b06-4403-b99b-2ca9f4de5949.png#align=left&display=inline&height=409&margin=%5Bobject%20Object%5D&name=image.png&originHeight=818&originWidth=1466&size=406154&status=done&style=none&width=733)

### 实体标识

Financial API消息中不表示User实体。
Login实体有一个对其所属机构而言独一无二的标识符。
Login实体的标识符通常是用户名/密码登录的用户名部分。
Login实体的替代标识符是从金融机构获得的OAuth令牌。
Account实体的标识符对所属机构来说是唯一的。
Transaction实体具有一个标识符，该标识符对于关联Account实体是唯一的，并且通常对于所属机构也是唯一的。
> The User entity is not expressed in Financial API messages.
> The Login entity has an identifier unique to its owning Institution.
> The Login identifier is usually the username part of a username / password login.
> The Login surrogate identifier is the OAuth token obtained from the Financial Institution.
> The Account entity has an identifier that is unique to the owning Institution.
> The Transaction entity has an identifier that is unique to the owning Account and is usually unique to the owning Institution.


传输实体时，实体标识符(或替代标识符)是必需的，并用于关联实体。
Financial API标识符最多包含32个字符。
(IBAN帐户标识符为31个字符，
ACH有9位数字作为路由，另有17位数字为账号，
OFX 2.0允许<FITID>最多包含255个字符，但建议使用32个或更少的字符)。
> The entity identifier (or surrogate identifier) is required when transmitting the entities and is used to relate the entities.
> Financial API identifier properties have a maximum of 32 characters.
> (IBAN account identifiers are 31 characters,
> ACH has 9 digits for routing and 17 digits for account number,
> OFX 2.0 allowed <FITID> with up to 255 characters but recommended 32 or fewer).


### 替代标识符(Access Token)
OAuth为Login实体创建替代标识符 - 
Financial API服务器不会公开金融机构Login实体的标识符。
为了限制公开个人身份信息，Financial API服务器传输的其他标识符应该是替代标识符。
替代标识必须对实体关系提供如上所述相同的唯一性约束。
任何替代标识符必须长期保持不变(译者注：替代标识符是Access Token的情况下，如何保持长期不变？)。
> OAuth creates a surrogate identifier for a Login –
> a Financial API server does not expose the financial institution’s principal identifier of the Login.
> To limit the exposure of personally identifiable information,
> the other identifiers transmitted by the Financial API server should be a surrogate identifier.
> Surrogates must provide the same uniqueness constraints on the entity relationships as described above.
> Any surrogate identities must be long term persistent.


```java
Editor's Note: 
The clause's meaning is not entirely sure. 
See [#20](https://bitbucket.org/openid/fapi/issues/20/) for more details.
```

### 获取替代标识符(Access Token)

```
Editor's Note: 
This clause is newly created. It does not exist in DDA.
```

以下步骤总结了如何从金融机构的授权服务器获取Access Token的方式以及其用法。

1. 最终用户在Web端或者设备端启动客户端应用程序。
1. 客户端应用程序对最终用户进行身份验证。
1. 客户端应用程序提示最终用户提供关于金融机构的信息。
1. 客户端应用程序可以选择通过OpenID Connect Discovery 1.0进行配置发现，以获取金融机构的授权、令牌和资源端点(如果它们是未知的)。
1. 客户端向金融机构的授权端点发起授权请求，授权请求参数的细节在OpenID Connect 1.0的3.1.2.1和3.3.2.1节中有描述。
   1. response_type参数必须设置为code(授权码流程)。但是，如果授权服务器支持的话，建议将response_type参数设置为code id_token(混合流程)，这样可以确保授权码与金融机构授权服务器的最终用户相关联，前提是ID Token验证和授权码验证的功能已按照OpenID Connect 1.0的3.3.2.9和3.3.2.10节所描述的进行实现(译者注：c_hash & s_hash)。
   1. scope参数必须包含openid和offline_access。
   1. 建议prompt参数包含login值，以确保提示最终用户执行身份验证。prompt参数必须包含consent值，以提示最终用户必须明确的授予客户端应用程序访问金融信息的权限。
   1. 建议设置state和nonce参数。
   1. 建议将acr_values参数设置为授权服务器支持的值(按首选项排序)。
6. 客户端携带请求参数，将最终用户重定向到授权端点。
6. 授权服务器对最终用户进行认证，并从最终用户那里获得客户端应用的授权(译者注：不太理解)。
6. 授权服务器将授权结果反馈到客户端定义的redirect_uri端点。
6. 如果使用授权码流程，客户端根据OpenID Connect 1.0的3.1.2.7节验证响应。如果使用混合流程，则根据3.3.2.8进行验证。
6. 客户端从授权响应中提取授权代码和ID Token(如果需要)。
6. 如果使用混合流程，则按照OpenID Connect 1.0 的 3.3.2.9 和 3.3.2.10章节进行授权码验证和ID Token 验证。
6. 为了获得访问令牌，需要按照OpenID Connect 1.0 的 3.1.3节所述，将授权码提交给授权服务器的令牌端点。
   1. 客户端必须使用OpenID Connect 1.0第9节中描述的认证方法向Token端点进行自认证。不支持none方法。认证方法必须由授权服务器支持，并在客户端注册或创建期间达成一致。
13. 客户端必须按照OpenID Connect 1.0的3.1.3.5节所述验证令牌响应。
13. 使用访问令牌来访问受保护的Financial API端点。
13. 存储刷新令牌，以便在访问令牌过期时获取新的访问令牌。

> The following steps summarizes the methods on how to obtain an access token from a Financial Institution Authorization Server and its usage.
> 1. The end user starts a Client application on the web or on a device.
> 1. The client application authenticates the end user.
> 1. The client application prompts the end user for information regarding the Financial Institution.
> 1. The client application may optionally perform discovery via OpenID Connect Discovery 1.0 to otain the Financial Instituion's authorization, token, and resource endpoints if they are unknown.
> 1. The client constructs an Authorization request to the Financial Institution's Authorization Endpoint. The details of the Authorization request parameters are described in section 3.1.2.1 and 3.3.2.1 of OpenID Connect 1.0.
>    1. The _response_type_ parameter MUST be set to _code_ (Code flow).  However, it is RECOMMENDED to set the _response_type_ parameter to _code id_token_ (Hybrid Flow) if it is supported by the Authorization Server. This ensures that the authorization code correlates to the end user at the Financial Institution's Authorization Server provided that ID Token validation and authorization code validation are performed as described in section 3.3.2.9 and 3.3.2.10 of OpenID Connect 1.0.
>    1. The _scope_ parameter MUST contain the values _openid_ and _offline_access_.
>    1. It is RECOMMENDED that the _prompt_ parameter contains the values _login_ to ensure that the end user is prompted to perform authentication. The _prompt_ parameter MUST contain the value _consent_ to prompt the end user for explicit authorization for the client application to obtain financial information.
>    1. It is RECOMMENDED to set values for the _state_ and _nonce_ parameters.
>    1. It is RECOMMENDED to set the _acr_values_ parameter to values supported by the Authorization Server, ordered by preference.
> 6. The client redirects the end user to the Authorization Endpoint with the request parameters.
> 6. The Authorization Server authenticates the end user and obtains authorization from the end user for the client application.
> 6. The Authorization Server sends the authorization response back to the client's _redirect_uri_ endpoint.
> 6. The client validates the response according to section 3.1.2.7 of OpenID Connect 1.0 if using Code Flow. If Hybrid flow was used, validation is done according 3.3.2.8.
> 6. The client extracts the authorization code and if requested, the ID Token from the authorization response.
> 6. If Hybrid flow was used, authorization code validation and ID Token validation is performed according to 3.3.2.9 and 3.3.2.10 of OpenID Connect 1.0.
> 6. To obtain an Access Token, the authorization code is submitted to Authorization Server's Token Endpoint as described in section 3.1.3 of OpenID Connect 1.0.
>    1. The client MUST authenticate itself to the Token Endpoint using an authentication method as described in section 9 of OpenID Connect 1.0. The _none_ method is not supported. The authentication method MUST be supported by the Authorization Server and agreed upon during client registration or creation.
> 13. The client MUST validate the token response as described in section 3.1.3.5 of OpenID Connect 1.0.
> 13. Use Access Token to access protected Financial API endpoints.
> 13. Store the Refresh Token for fetching a new Access Token once the current Access Token expires.


## 冗余数据

冗余数据定义为不再使用的数据，例如，如果一个帐户已关闭，聚合方(译者注：不准确)应在180天内从其系统中删除相关冗余数据。
> Residual data is defined as data that is no longer being used, for example if an account has been closed. Aggregators should delete residual data from their systems within 180 days.


## 协议

```java
Editor's Note: 
This section, while titled "Protocol", seems to be talking about 
the protected resource access per RFC6750. 
It is probably redundant and should be removed.
```

Financial API客户端使用HTTP GET和POST方法请求数据。
> The Financial API client requests data using HTTP GET and POST methods.


```
Editor's Note: 
Why not PUT and PATCH as well?
```

请求应当包含合适的Request-URI。
请求必须在Authorization头中包含OAuth访问令牌。
以下是一个案例，代表HTTP请求中典型的请求头。
> The request includes an appropriate Request-URI.
> Requests must include an OAuth access token in the authorization header.
> The following is a sample of the headers provided in a typical request.


```
GET /accounts HTTP/1.1
Host: example.com
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Accept: application/json
Accept-Charset: UTF-8
Accept-Encoding: gzip
```

### 消息序列化

```java
Editor's Note: 
This section is not in DDA. It needs to be explained somewhere, 
but this location seems to be out-of-place.
```

消息采用如下的方式进行序列化：

1. Query String Serialization
1. Form Serialization
1. JSON Serialization
> Messages are serialized using one of the following methods:
> - Query String Serialization
> - Form Serialization
> - JSON Serialization


#### Query String Serialization

为了使用Query String Serialization对参数进行序列化，客户端通过使用HTML 4.01规范定义的application/x-www-form-urlencoded格式，将参数和值添加到URL的queryString中来构造最终字符串。
Query String Serialization通常用于HTTP GET请求中，将参数添加到URL的Fragment(译者注：scheme:[//[user:password@]host[:port]][/]path[?query][#fragmet]，即location.hash)时，通常也使用相同的序列化方法。
> In order to serialize the parameters using the Query String Serialization, the client constructs the string by adding the parameters and values to the query component of a URL using the application/x-www-form-urlencoded format as defined by the HTML 4.01 specification. Query String Serialization is typically used in HTTP GET requests. The same serialization method is also used when adding parameters to the fragment component of a URL.


#### Form Serialization

通过使用HTML 4.01规范定义的application/x-www-form-urlencoded格式，将参数和值添加到HTTP请求的请求体中，Form Serialization通常用于HTTP POST请求中。
> Parameters and their values are Form Serialized by adding the parameter names and values to the entity body of the HTTP request using the application/x-www-form-urlencoded format as defined by the HTML 4.01 specification. Form Serialization is typically used in HTTP POST requests.


#### JSON Serialization

通过在JSON的最高级逐项添加每个参数，可以将这些参数序列化为JSON对象结构。参数名和字符串值表示为JSON字符串，数字值表示为JSON数字，布尔类型值表示为JSON布尔值。
除非另有说明，否则应从对象中删除忽略的参数项及值为空的参数项，并且不以JSON的空值表示。参数可以使用JSON对象或JSON数组作为其值(译者注：指复杂层级结构)。
> The parameters are serialized into a JSON object structure by adding each parameter at the highest structure level. Parameter names and string values are represented as JSON strings. Numerical values are represented as JSON numbers. Boolean values are represented as JSON booleans. Omitted parameters and parameters with no value SHOULD be omitted from the object and not represented by a JSON null value, unless otherwise specified. A parameter MAY have a JSON object or a JSON array as its value.


### 请求头

#### 传输安全

```
Editor's note: 
It should be moved to TLS consideration in Security Consideration. 
Also, requirling TLS client auth is unrealistic for mobile apps etc.
```

必须使用SSL/TLS保护所有Financial API的通信，以避免网络嗅探攻击。使用TLS可以确保包括所有请求头在内的整个HTTP请求和HTTP响应的安全。我们建议Financial API客户端和服务器都使用证书。此外，Financial API服务器响应头中应包括Cache-Control标头，以防止对响应进行任何缓存或存储。
> All Financial API communication must be secured from network sniffing with SSL/TLS. Using TLS will secure the entire request and response including any headers. We recommend that both the Financial API client and server use certificates. Additionally, Financial API server responses should include Cache-Control headers to prevent any caching or storing of the response.


```java
Cache-Control: no-cache, no-store
```

#### 请求授权

```java
Editor's note: 
The title is misleading. This clause is talking about Protected Resource access 
so it should be titled "Protected Resource Access Authorization" or something instead.
```

Financial API客户端不会在Financial API服务器进行用户识别，而是通过OAuth令牌来代表用户在在金融机构的身份(译者注：identify的动作通过授权服务器完成，此处所指的Financial API服务器只作为资源服务器)。
> The Financial API client does not identify a User to the Financial API server. Instead, the User’s financial institution Login is implied via an OAuth token.


```java
Editor's note: 
Access Token and Refresh Token is opaque to the client by definition. 
The above paragraph is redundant.
```

任何Financial API请求返回的数据，都应受限于已登录用户能访问的内容，并且进一步受OAuth令牌范围的限制。
> The data returned by any Financial API request is limited to what the User could see using his/her Login and further limited by the scope of the OAuth token.


```java
Editor's note: 
This is vague. Perhaps it meant that the access tokens are more narrowly scoped than 
the access entitlement than the person who is authorizing the access has. 
It may be too limiting when we consider about delegation etc.
```

Financial API客户端的Authorization请求头中，应携带Bearer或MAC令牌。
建议使用Bearer令牌，尽管如果客户端支持，服务器也可以选择签发MAC令牌作为替代方案。
安全相关的模型部分中详细介绍了如何获取此令牌。

> The Financial API client uses the Authorization request header with a Bearer or MAC token.
Bearer tokens are recommended although the server has option to issue MAC tokens as an alternative if the client supports it.How to obtain this token was detailed in the Security Model section.

```
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=

Editor's Note: 
Was there a MAC token in OAuth 2.0? 
Token Binding or PoP Token sounds better.
```

#### 内容协商

```
Editor's Note: 
FAPI only supports JSON. 
Rest of the clause is something handled by web server, so we probably do not need to 
state them as a protocol spec.
```

Financial API客户端和服务器使用标准的HTTP头来协商传输配置选项。
Financial API客户端使用Accept请求头来标明其期望的语法，服务器必须使用其请求的语法之一进行响应，或返回406(Not Acceptable)状态码。本文档定义了以下格式：
> Financial API clients and servers use standard HTTP headers to negotiate transport options.
The Financial API client uses the Accept request header to ask for its preferred syntax. The server must respond with one of the requested syntaxes or with a 406 status code. The following formats are defined by this document:

- application/json

默认情况下返回application/json格式。
> The application/json format is returned by default.


```
Accept: application/json, application/xml;q=0.5
```

Financial API客户端使用Accept-Charset请求头来标明其期望的字符集。服务器必须使用其请求的字符集之一中编码方式进行响应，或返回406(Not Acceptable)状态码。
> The Financial API client uses the Accept-Charset request header to ask for its preferred character set. The server must respond with the body encoded in one of the requested character sets or with a 406 status code.


```
Accept-Charset: UTF-8
```

Financial API服务器使用Content-Type响应头，告知客户端其响应语法和字符集。
> The Financial API server uses the Content-Type response header to inform the client of the response syntax and charset.


```
Content-Type: application/json; charset=UTF-8
```

Financial API客户端使用Accept-Encoding请求头来标明其期望的压缩算法，服务器必须以其请求的压缩算法之一进行压缩，或者以未压缩的主体作为响应。
> The Financial API client uses the Accept-Encoding request header to ask for its preferred compression encoding. The server must either respond with the body compressed with one of the requested compressions, or with the body not compressed.


```
Accept-Encoding: compress, gzip
```

Financial API服务器使用Content-Encoding响应头通知客户端其响应编码。
> The Financial API server uses the Content-Encoding response header to inform the client of the response encoding.


```
Content-Encoding: gzip
```

对于查询类请求，客户端通过If-Modified-Since请求头指定日期，仅当该日期之后数据存在变更的情况下，服务端才会给予响应数据。如果服务器支持此请求头，且在指定日期后并未修改数据，则将向客户端返回304(Not modified)响应码。
> For queries, the Financial API client may use the If-Modified-Since request header to ask for a data response only if the data has been modified since the given date. If the server supports this header and the data has not been modified, a 304 HTTP response code will be returned to the client.


```
If-Modified-Since: Wed, 12 Sep 2012 06:00:00 GMT
```

#### 服务器环境

Financial API服务端的每个响应都包含Date响应头。
> The Financial API server returns a Date header with every response.


```
Date: Tue, 11 Sep 2012 19:43:31 GMT
```

#### Host

Host请求头字段指定所请求资源所在服务器的主机地址和端口号。没有指明任何端口信息的Host请求头表示使用默认端口(例如，HTTP默认为80端口)
> The Host request header field specifies the Internet host and port number of the resource being requested. A Host header without any trailing port information implies the default port for the service requested (e.g. "80" for an HTTP URL).


```
Host: example.com
```

#### 客户端标识

```
Editor's Note: 
Is the below "shall" or "should"? Too vague.
```

Financial API客户端的每个请求都包含User-Agent请求，此请求头不会影响响应的内容。User-Agent请求头仅设计用于Financial API的数据服务去收集有关产品的统计信息。该请求头的第一段标识符是厂商和厂商版本，第二段标识符是产品和产品版本(译者注：不准确，可参考规范文档对User-Agent的定义，但目前很多浏览器为保障兼容性，其实现并不标准)。
> The Financial API client supplies a User-Agent header with every request. This header should not be used to change the content of the response. This header is designed to only collect statistics on the products using the Financial API data service. The first token is the aggregator and aggregator version. The second token is the product and product version.


```java
User-Agent: Intuit/1.2.3 Mint/4.3.1
```

#### 客户标识

Financial API客户端可以选择在请求头中添加DDA-CustomerId，作为客户的标识符。
此请求头的值是为其颁发OAuth 2.0令牌的用户。
DDA-CustomerId的值必须与OAuth 2.0响应返回的user_id参数，以及客户实体中CustomerId字段的值相同(如果Financial API服务器实现了客户操作)。
> The Financial API client can optionally supply a customer identifier with request header `DDA-CustomerId`.
> This value identifies the user for whom the OAuth 2.0 token was issued.
> The value of DDA-CustomerId must be the same as the the `user_id` parameter returned by the OAuth 2.0 response and the value of the CustomerId field in the Customer Entity (if the Financial API server implements the customer operations).


```
DDA-CustomerId: a237cb74-61c9-4319-9fc5-ff5812778d6b

Editor's Note: 
Where is user¥_id defined? 
See issue #22 (https://bitbucket.org/openid/fapi/issues/22/)
```

#### 客户的最后登录时间

如果存在此数据，则Financial API客户端可以选择支持DDA-CustomerLastLoggedTime请求头，以指明客户的最后登录时间。
> The Financial API client can optionally supply the last time the customer logged into the aggregator product if this data is available.


```java
DDA-CustomerLastLoggedTime: Tue, 11 Sep 2012 19:43:31 GMT
```

#### 客户IP地址

如果此数据可用，则Financial API客户端可以选择通过DDA-CustomerIPAddress请求头提供客户的IP地址。
> The Financial API client optionally can supply the customer’s IP address if this data is available or applicable.


```java
DDA-CustomerIPAddress: 0.0.0.0

Editor's Note: 
"customer's IP" is too vague. Clarify.
```

#### 日志追踪

Financial API客户端可以将DDA-InteractionId请求头发送到服务器，以辅助关联客户端和服务器之间的日志条目。 例：
> The Financial API client may send the DDA-InteractionId request header to the server to help correlate log entries between client and server. Example:


```
DDA-InteractionId: c770aef3-6784-41f7-8e0e-ff5f97bddb3a
```

Financial API服务器必须在其日志条目中包含此请求头的值。Financial API服务器还必须将DDA-InteractionId作为响应头返还给客户端，其值等于客户端发送的值，或者如果客户端未发送DDA-InteractionId，服务器则会生成唯一值。
> The Financial API server must include the value of this header in its log entries. The Financial API server must also send `DDA-InteractionId` as a response header with value equal to the value sent by the client, or a unique value generated by the server if the client did not send `DDA-InteractionId`.


#### 金融机构标识

如果Financial API服务由服务商提供，该服务商对多个金融机构使用相同的端点，则Financial API客户端必须提供请求头，以指明所需的金融机构，由服务商定义此值。例如，通常是金融机构的转帐号码(RTN)。
> If the Financial API service is provided by a service bureau which uses the same end point for multiple institutions, the Financial API client must provide a header the identifies the desired financial institution. The service bureau defines this value. For example, it is often the financial institution’s routing number (RTN).


```
DDA-FinancialId: 123456789

Editor's Note: 
This is "Hacky". Is there a real example like this?
```

### 错误

当Financial API服务器无法完成请求时，它们应该发送恰当的HTTP状态码以及错误实体作为响应。错误消息应仅包含足够的信息，在不影响安全性的情况下，告知最终用户发生了什么问题。
> When Financial API servers are unable to fulfill a request, they should send Error Entity as the response payload along with an appropriate HTTP Status Code. Error messages should contain just enough information for an end user to understand what went wrong without compromising security.

| Error Code | Error Message | HTTP Status Code |
| --- | --- | --- |
| 601 | Customer not found | 404 |
| 602 | Customer not authorized | 401 |
| 701 | Account not found | 404 |
| 702 | Invalid start or end date | 400 |
| 703 | Invalid date range | 400 |
| 901 | Source account not found | 404 |
| 902 | Source account closed | 404 |
| 903 | Source account not authorized for transfer | 401 |
| 904 | Destination account not found | 404 |
| 905 | Destination account closed | 404 |
| 906 | Destination account not authorized for transfer | 401 |
| 907 | Invalid amount | 404 |
| 908 | Duplicate transfer request | 409 |
| 909 | Transfer not available due to end of day processing | 503 |
| 910 | Insufficient funds | 400 |
| 911 | Transaction limit exceeded | 400 |
| 950 | Transfer not found | 404 |


### 资源

在实践Financial API时，客户端和服务器维护者必须在数据服务端点上达成一致。
所有资源URI都可以以基本URI作为前缀，例如：[https://example.com/dda/1.0](https://example.com/dda/1.0)。
基本URI应包含服务器实现的Financial API的版本。

> When implementing Financial API, the client and server maintainers must agree on the data service endpoint.
> All resource URIs may be prefixed by a base URI, for example [https://example.com/dda/1.0](https://example.com/dda/1.0).
The base URI should include the version of Financial API that the server implements.

出于安全原因，标识符不应成为URI的一部分，而应成为HTTP body的一分部，以防止在服务器审核日志中无意间泄露信息。
> For security reasons identifiers should not be part of the URI and should be part of the HTTP body to prevent in inadvertent information disclosure in server audit logs.


```
Editor's Note: 
What Identifier?
```

也因为如此，某些请求被实现为POST而非GET，其参数以application/x-www-form-urlencoded格式化作为表单数据放到请求体中。
> For this reason some requests are implemented as POST rather than GET with parameters sent in the body as form data in application/x-www-form-urlencoded format.


### 资源端点发现

```
Editor's note: 
This clause is new. 
DDA does not define how to discover the endpoints.
```

本文档定义了一种机制，用于发现各种资源端点，以请求用户的数据。
基于OpenID Connect Discovery 1.0中描述的发现机制，本文档为OpenID Discovery的响应定义了以下参数：
> This document defines a mechanism for discovering the various resources endpoints for requesting the user's financial data.
Building upon the discovery mechanism described in OpenID Connect Discovery 1.0,this document defines the following parameters to the OpenID Discovery response:
| Parameter | Type | Description |
| --- | --- | --- |
| ofx _optional_ | Array | JSON object containing a collection of the API resources endpoints and their URL locations |


ofx参数包含以下参数值：
> The ofx parameter contains the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| account_endpoint _optional_ | String | URL for getting account information |
| statement_endpoint _optional_ | String | URL for retrieving a statement document |
| statement_list_endpoint _optional_ | String | URL for getting list of statements |
| transaction_document_endpoint _optional_ | String | URL for getting a transaction document |
| transaction_list_endpoint _optional_ | String | URL for getting list of transactions |
| account_list_endpoint _optional_ | String | URL for getting list of accounts |
| account_details_endpoint _optional_ | String | URL for getting account information (details & transactions) for the current token |
| availability_endpoint _optional_ | String | URL for getting information about this API's availability |
| capability_endpoint _optional_ | String | URL for getting informtion about this API's capabilities |
| customer_endpoint _optional_ | String | URL for getting about the customer within the authorization scope |
| transfer_endpoint _optional_ | String | URL for creating a transfer between accounts |
| transfer_status_endpoint _optional_ | String | URL for getting the status of a transfer between accounts |


```
Editor's note: 
An example should be added.
```
