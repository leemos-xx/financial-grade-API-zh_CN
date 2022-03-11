# Financial-grade API - Part 2: Read and Write API Security Profile

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

OIDF (OpenID Foundation)是一个国际化标准机构，由160多个参与实体组成。编制国际标准的工作是OIDF工作组根据OpenID Process进行的，对已成立工作组感兴趣的参与方都有权利加入工作组。国际组织，包括政府和非政府组织，在与OIDF的联络下，也参与到该工作中来，OIDF与相关领域的其他标准化机构保持紧密合作关系。
> The OpenID Foundation (OIDF) promotes, protects and nurtures the OpenID community and technologies. As a non-profit international standardizing body, it is comprised by over 160 participating entities (workgroup participants). The work of preparing implementer drafts and final international standards is carried out through OIDF workgroups in accordance with the OpenID Process. Participants interested in a subject for which a workgroup has been established has the right to be represented in that workgroup. International organizations, governmental and non-governmental, in liaison with OIDF, also take part in the work. OIDF collaborates closely with other standardizing bodies in the related fields.


金融级API由以下部分组成：

- 1：只读操作相关接口的安全总则
- 2：读写操作相关接口的安全总则
- 金融级API：客户端初始化时的后端认证规范
- 金融级API：基于JWT的OAuth2.0安全授权响应机制(JARM)
- 金融级API：实施和部署建议

> Financial-grade API consists of the following parts:
> - Part 1: Read-Only API Security Profile
> - Part 2: Read and Write API Security Profile
> - Financial-grade API: Client Initiated Backchannel Authentication Profile
> - Financial-grade API: JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)
> - Financial-grade API: Implementation and Deployment Advice


后续部分将持续更新。
> Future parts may follow.


金融级API的组成部分应与[RFC6749], [RFC6750]、[RFC7636]和[OIDC]配合使用。
> These parts are intended to be used with [RFC6749], [RFC6750], [RFC7636], and [OIDC].



## 说明

金融科技是未来全球经济增长的领域之一，金融科技组织需要提升其运营安全性以及保护用户数据的能力。聚合服务普遍采用存储用户的密码，通过屏幕抓取的方式来捕获数据。这种脆弱、低效并且不安全的做法会导致安全漏洞，这就要求金融机构维持一个白名单，对白名单中的聚合商(译者注：不准确)允许他们对应用进行类似自动攻击式的访问。本工作组提供的一个新的草案将使用一个具有结构化数据和令牌的API模型，如OAuth [RFC6749, RFC6750]。
> Fintech is an area of future economic growth around the world and Fintech organizations need to improve the security of their operations and protect customer data. It is common practice of aggregation services to use screen scraping as a method to capture data by storing users' passwords. This brittle, inefficient, and insecure practice creates security vulnerabilities which require financial institutions to allow what appears to be an automated attack against their applications and to maintain a whitelist of aggregators. A new draft standard, proposed by this workgroup would instead utilize an API model with structured data and a token model, such as OAuth [RFC6749, RFC6750].


金融级API旨在为线上的金融服务提供具体的实施指南，通过开发一个通过OAuth保护的REST/JSON数据模型，供其采用。金融级API安全规范可以适用于任何领域的线上服务，这将提供比标准的OAuth、或OpenID Connect更高的安全级别。
> The Financial-grade API aims to provide specific implementation guidelines for online financial services to adopt by developing a REST/JSON data model protected by a highly secured OAuth profile. The Financial-grade API security profile can be applied to online services in any market area that requires a higher level of security than provided by standard OAuth or OpenID Connect.


该文档是FAPI的第1部分，它描述了金融级API，并提供一种OAuth的使用方式，用于解决更高风险等级情况下的访问问题(读或写)，如，对高度敏感数据的读访问或者对金融数据的写访问(也就是发起支付)。本文档规约了对如下攻击的控制策略，如：授权请求篡改、授权响应篡改，包括代码注入、状态注入(译者注：不理解)和token请求钓鱼。更多细节可参考安全考量部分。
> This document is Part 2 of FAPI that specifies the Financial-grade API and it provides a profile of OAuth that is suitable to be used for high risk access (read or write), for example, read access to highly sensitive data or write access to financial data (also known as payment initiation). This document specifies the controls against attacks such as: authorization request tampering, authorization response tampering including code injection, state injection, and token request phishing. Additional details are available in the security considerations section.


尽管可以直接根据该规范去从零构建OpenID提供方和依赖方，但本规范的主要受众是已经实践了OpenID Connect并希望提升其安全级别的各方。我们鼓励实施者在从零开始构建前，先理解在8.7章节中描述的对安全的考量。
> Although it is possible to code an OpenID Provider and Relying Party from first principles using this specification, the main audience for this specification is parties who already have a certified implementation of OpenID Connect and want to achieve a higher level of security. Implementers are encouraged to understand the security considerations contained in section 8.7 before embarking on a 'from scratch' implementation.

### 

### 符号约定
The keywords "shall", "shall not",
"should", "should not", "may", and
"can" in this document are to be interpreted as described in
ISO Directive Part 2 [ISODIR2].
These keywords are not used as dictionary terms such that
any occurrence of them shall be interpreted as keywords
and are not to be interpreted with their natural language meanings.

# Financial-grade API - Part 2: Read and Write API Security Profile 

[TOC]

## 1. 范围

该文档定义了应用程序的如下行为:

- 应用程序以适当且安全的方式获取OAuth令牌，用于更高安全级别的数据访问；
- 使用OpenID Connect来识别客户，并且
- 使用令牌与REST端点交互受保护的数据；

> This part of the document specifies the method of
> - applications to obtain the OAuth tokens in an appropriately secure manner for higher risk access to data;
> - applications to use OpenID Connect to identify the customer; and
> - using tokens to interact with the REST endpoints that provides protected data;


本文档适用于风险较高的场景用例，包括商业和投资银行以及其它类似行业。
> This document is applicable to higher risk use cases which includes commercial and investment banking and other similar industries.


## 2. 参考文档

对本规范的实际应用而言，以下的参考规范必不可少。对标注日期的参考规范，仅引用的版本适用，而未标注日期的文档，其最新版本(包括所有修订)也适用本规范。
> The following referenced documents are indispensable for the application of this document. For dated references, only the edition cited applied. For undated references, the latest edition of the referenced document (including any amendments) applies.


[ISODIR2] - ISO/IEC Directives Part 2
[ISODIR2]: [http://www.iso.org/sites/directives/2016/part2/index.xhtml](http://www.iso.org/sites/directives/2016/part2/index.xhtml)

[RFC6749] - The OAuth 2.0 Authorization Framework
[RFC6749]: [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749)

[RFC6750] - The OAuth 2.0 Authorization Framework: Bearer Token Usage
[RFC6750]: [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)

[RFC7636] - Proof Key for Code Exchange by OAuth Public Clients
[RFC7636]: [https://tools.ietf.org/html/rfc7636](https://tools.ietf.org/html/rfc7636)

[RFC6819] - OAuth 2.0 Threat Model and Security Considerations
[RFC6819]: [https://tools.ietf.org/html/rfc6819](https://tools.ietf.org/html/rfc6819)

[RFC7519] - JSON Web Token (JWT)
[RFC7519]:[https://tools.ietf.org/html/rfc7519](https://tools.ietf.org/html/rfc7519)

[RFC7591] - OAuth 2.0 Dynamic Client Registration Protocol
[RFC7591]:[https://tools.ietf.org/html/rfc7591](https://tools.ietf.org/html/rfc7591)

[RFC7592] - OAuth 2.0 Dynamic Client Registration Management Protocol
[RFC7592]:[https://tools.ietf.org/html/rfc7592](https://tools.ietf.org/html/rfc7592)

[OIDC] - OpenID Connect Core 1.0 incorporating errata set 1
[OIDC]: [http://openid.net/specs/openid-connect-core-1_0.html](http://openid.net/specs/openid-connect-core-1_0.html)

[OIDD] -  OpenID Connect Discovery 1.0 incorporating errata set 1
[OIDD]: [http://openid.net/specs/openid-connect-discovery-1_0.html](http://openid.net/specs/openid-connect-discovery-1_0.html)

[MTLS] - OAuth 2.0 Mutual TLS Client Authentication and Certificate Bound Access Tokens
[MTLS]: [https://tools.ietf.org/html/rfc8705](https://tools.ietf.org/html/rfc8705)

[JARM] - Financial Services – Financial-grade API: JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)
[JARM]: [https://bitbucket.org/openid/fapi/src/master/Financial_API_JWT_Secured_Authorization_Response_Mode.md](https://bitbucket.org/openid/fapi/src/master/Financial_API_JWT_Secured_Authorization_Response_Mode.md)

[PAR] - OAuth 2.0 Pushed Authorization Requests
[PAR]: [https://tools.ietf.org/html/draft-ietf-oauth-par](https://tools.ietf.org/html/draft-ietf-oauth-par)

[JAR] - OAuth 2.0 JWT Secured Authorization Request
[JAR]: [https://tools.ietf.org/html/draft-ietf-oauth-jwsreq](https://tools.ietf.org/html/draft-ietf-oauth-jwsreq)

## 3. 术语和定义

本规范而言，适用RFC6749、RFC6750、RFC7636、OpenID Connect Core和ISO29100中定义的术语。
> For the purpose of this document, the terms defined in [RFC6749], [RFC6750], [RFC7636], [OpenID Connect Core][OIDC] and [ISO29100] apply.


## 4. 缩略语

**API** – Application Programming Interface

**CSRF** - Cross Site Request Forgery

**FAPI** - Financial-grade API

**HTTP** – Hyper Text Transfer Protocol

**OIDF** - OpenID Foundation

**REST** – Representational State Transfer

**TLS** – Transport Layer Security

## 5. 读写API的安全总则

### 5.1 简介

OIDF定义的金融级API(FAPI)是一套提供JSON数据(高风险)的REST API，这些API受由[RFC6749]、[RFC6750]、[RFC7636]和其它规范组成的OAuth授权框架的保护。
> The OIDF Financial-grade API (FAPI) is a REST API that provides JSON data representing
> higher risk data. These APIs are protected by the
> OAuth 2.0 Authorization Framework that consists of [RFC6749], [RFC6750],
> [RFC7636], and other specifications.


访问这些API会带来不同安全级别的风险。
如，具备读写操作的API的访问比只读的API访问存在更高的金融风险。因此，保护这些API的授权框架的安全策略也就不尽相同。
> There are different levels of risks associated with access to these APIs.
> For example, read and write access to a bank API has a higher financial risk than read-only access. As
> such, the security profiles of the authorization framework protecting these
> APIs are also different.


该策略为金融级API的客户端和服务端描述了一些安全规约，其中定义了一些机制用以减轻：

- 利用端点弱绑定进行的攻击[RFC6749](如：恶意端点攻击、IdP混淆攻击)，
- 篡改未受保护的授权请求和响应的攻击 [RFC6749]

> This profile describes security provisions for the server and client that are appropriate for Financial-grade APIs by defining the measures to mitigate:
> - attacks that leverage the weak binding of endpoints in [RFC6749] (e.g. malicious endpoint attacks, IdP mix-up attacks),
> - attacks that modify authorization requests and responses unprotected in [RFC6749]


该策略不支持公开客户端。
> This profile does not support public clients.


以下是应对授权响应篡改的方法：实施者可以如OpenID Connect's Hybrid Flow所述，在授权响应中返回ID Token，也可以使用JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)，通过JWT来保护授权响应中的所有参数。
> The following ways are specified to cope with modifications of authorization responses: Implementations can leverage OpenID Connect's Hybrid Flow that returns an ID Token in the authorization response or they can utilize the JWT Secured Authorization Response Mode for OAuth 2.0 (JARM) that returns and protects all authorization response parameters in a JWT.


#### 5.1.1 作为分离式签名的ID Token

虽然ID Token( OpenID Connect Hybrid Flow所使用的)的名称给我们的印象是提供资源所有者(subject)的标识，但不全是如此，比如通过issuer也可以标识授权服务器，同时有一个短暂的subject标识资源所有者也是没有问题的。
基于此种情况，ID Token可以作为授权服务器对授权响应的分离式签名，而且OpenID Connect Core的这种设计是非常明智的。
> While the name ID Token (as used in the OpenID Connect Hybrid Flow) suggests that it is something that provides the identity of the resource owner (subject), it is not necessarily so. While it does identify the authorization server by including the issuer identifier,
> it is perfectly fine to have an ephemeral subject identifier. In this case, the ID Token acts as a detached signature of the issuer to the authorization response and it was an explicit design decision of OpenID Connect Core to make the ID Token act as a detached signature.


本文档基于这一事实，通过在ID Token中包含未受保护的响应参数来保护授权响应(如state和code)。
> This document leverages this fact and protects the authorization response by including the hash of all of the unprotected response parameters, e.g. `code` and `state`, in the ID Token.


虽然[OIDC]中定义了code的哈希，但没有定义state的哈希。
因此，本文档对其定义如下：
> While the hash of the `code` is defined in [OIDC], the hash of the `state` is not defined.
> Thus this document defines it as follows.


**s_hash**

State哈希值。其值是state值的ASCII码的八进制形式下的最左半部分的hash值，再进行base64url编码。其哈希算法是ID Token的JOSE头的alg参数中标注的哈希算法。例如，如果alg是HS512，通过SHA-512对state的值进行hash，然后取其最左半部分的256bits，并进行base64url编码。
s_hash值大小写敏感。

> State hash value. Its value is the base64url encoding of the left-most half of the hash of the octets of the ASCII representation
> of the `state` value, where the hash algorithm used is the hash algorithm used
> in the `alg` header parameter of the ID Token's JOSE header. For instance,
> if the `alg` is `HS512`, hash the state value with SHA-512, then take the left-most 256 bits and base64url encode them.
> The `s_hash` value is a case sensitive string.


#### 5.1.2 JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)

授权服务器可以通过使用"JWT Secured Authorization Response Mode" [JARM]来保护对客户端的授权响应。
> An authorization server may protect authorization responses to clients using the "JWT Secured Authorization Response Mode" [JARM].


[JARM]允许授权服务器将授权响应(任何响应类型)编码在JWT中返回给客户端，它是利用ID Token作为分离式签名，来为授权响应提供金融级安全的一种方法，可以与普通的OAuth共用。
> The [JARM] allows a client to request that an authorization server encodes the authorization response (of any response type) in a JWT. It is an alternative to utilizing ID Tokens as detached signatures for providing financial-grade security on authorization responses and can be used with plain OAuth.


本规范可以使[JARM]与code类型的响应更容易的结合使用。
> This specification facilitates use of [JARM] in conjunction with the response type `code`.


NOTE: [JARM]可以用来保护OpenID Connect的授权响应。在这种情况下，OpenID RP应该使用值为code的response_type、值为jwt的response_mode并在scope中包含openid域，这种设置意味着令牌端点将通过[JARM]来保护授权响应，同时返回包含End-User Claims的ID Token。这更有利于隐私保护，因为没有通过前端通道发送End-User Claims。它还提供对消息保护和身份维持的解耦，因为客户端(或RP)可以使用[JARM]来保护所有授权响应，并在需要时才开启OpenID以获得用户身份(如登录用户)。
> Note: [JARM] can be used to protect OpenID Connect authentication responses. In this case, the OpenID RP would use response type `code`, response mode `jwt` and scope `openid`. This means [JARM] protects the authentication response (instead of the ID Token) and the ID Token containing End-User Claims is obtained from the token endpoint. This facilitates privacy since no End-User Claims are sent through the front channel. It also provides decoupling of
> message protection and identity providing since a client (or RP) can basically use [JARM] to protect all
> authorization responses and turn on OpenID if needed (e.g. to log the user in).


### 5.2 读写类型API的安全规约

#### 5.2.1 简介

读写访问带来更高的安全风险，因此其所需的保护级别高于只读访问。
> Read and write access carries higher risk; therefore the protection level required is higher than read-only access.


作为OAuth2.0授权框架的策略， 本文档为FAPI的读写类API规定了如下内容。
> As a profile of The OAuth 2.0 Authorization Framework, this document mandates the following for the read and write API of the FAPI.


#### 5.2.2 授权服务器

授权服务器应支持Financial-grade API - Part 1: Read-Only API Security Profile第5.2.2条的规定，但对5.2.2.7(执行[RFC7636])不做要求。
> The authorization server shall support the provisions specified in clause 5.2.2 of
> Financial-grade API - Part 1: Read-Only API Security Profile, with the exception
> that section 5.2.2.7 (enforcement of [RFC7636]) is not required.


此外，授权服务器

1. 应要求按照[OIDC]第6条的规定，使用request或request_uri参数，将请求参数作为JWT进行传递；
1. 应要求
   1. response_type值为code id_token，或
   1. response_type值为code和response_mode值为jwt；
3. (迁移到5.2.2.1)；
3. 应该只签发发送者受限的访问令牌；
3. 应支持[MTLS]作为约束访问令牌合法发送者的机制；
3. (已撤回)；
3. (迁移到5.2.2.1)；
3. (迁移到5.2.2.1)；
3. 应仅使用签名对象中传递的参数(签名前的request或request_uri参数)；
3. 可支持[PAR](译者注：OAuth 2.0 Pushed Authorization Requests，进行中的草案)中描述的推送授权请求端点；
3. (已撤回)；
3. 应要求request object包含exp claim，其寿命为nbf claim之后的60分钟内，并且
3. 应使用以下方法之一验证非公开客户端(优先于FAPI第一部分的5.2.2.4条)：
   1. 如[MTLS]第2节规定的OAuth客户端认证的双向TLS；
   1. [OIDC]第9条规定的private_key_jwt；
14. 应要求request object中的aud claim是、或者是包含OP's Issuer Identifier URL的数组；
14. 不应该支持公共客户端(译者注：只读API并无此要求)；
14. 应要求request object中的nbf claim的值不超过过去的60分钟(译者注：nbf配合exp确定其寿命)；以及
14. 应要求[PAR]请求(如果支持)，使用PKCE([RFC7636])和S256作为code chanllenge；

> In addition, the authorization server
> 1. shall require the `request` or `request_uri` parameter to be passed as a JWS signed JWT as in clause 6 of [OIDC];
> 1. shall require
>    1. the `response_type` value `code id_token` or
>    1. the `response_type` value `code` in conjunction with the `response_mode` value `jwt`;
> 3. (moved to 5.2.2.1)
> 3. shall only issue sender-constrained access tokens;
> 3. shall support [MTLS] as mechanism for constraining the legitimate senders of access tokens;
> 3. (withdrawn);
> 3. (moved to 5.2.2.1);
> 3. (moved to 5.2.2.1);
> 3. shall only use the parameters included in the signed request object passed in the `request` or `request_uri` parameter;
> 3. may support the pushed authorization request endpoint as described in [PAR];
> 3. (withdrawn);
> 3. shall require the request object to contain an `exp` claim that has a lifetime of no longer than 60 minutes after the `nbf` claim; and
> 3. shall authenticate the confidential client using one of the following methods (this overrides FAPI part 1 clause 5.2.2.4):
>    1. Mutual TLS for OAuth Client Authentication as specified in section 2 of [MTLS];
>    1. `private_key_jwt` as specified in section 9 of [OIDC];
> 14. shall require the aud claim in the request object to be, or to be an array containing, the OP's Issuer Identifier URL;
> 14. shall not support public clients;
> 14. shall require the request object to contain an `nbf` claim that is no longer than 60 minutes in the past; and
> 14. shall require [PAR] requests, if supported, to use PKCE ([RFC7636]) with `S256` as the code challenge method.


NOTE：MTLS是目前唯一被广泛使用的实现发送者受限的访问令牌的机制。本规范的未来版本很可能允许其他机制用于实现发送者受限的访问令牌(译者注：上述第4点提到只能签发sender-constrained的访问令牌，此处又描述MTLS是目前唯一广泛使用的实现sender-constrained的机制，那上述13点提到的两种验证非公开客户端的方式，private_key_jwt方式是否还可用？)。
> **NOTE:** MTLS is currently the only mechanism for sender-constrained access tokens that has been widely deployed. Future versions of this specification are likely to allow other mechanisms for sender-constrained access tokens.


NOTE：[PAR]并没有任何需要使用PKCE的额外的安全问题-在其它情况下不需要PKCE的原因是为了保证本规范的早期版本的向后兼容性。**
> **NOTE** [PAR] does not present any additional security concerns that necessitated the requirement to use PKCE - the reason PKCE is not required in other cases is merely to be backwards compatible with earlier drafts of this standard.


#### 5.2.2.1 作为分离式签名的ID Token

此外，如果response_type值为code id_token，则授权服务器：

1. 应支持[OIDC]；
1. 应支持有签名的ID Token；
1. 应支持经过签名和加密的ID Token；
1. 应在授权响应中将ID Token作为分离式签名返回；
1. 如果客户端提供了state，应在ID Token中包含state的hash，即s_hash，以保护state值。如果s_hash已经在授权端点返回的ID Token存在，则从令牌端点返回的ID Token中的s_hash可以忽略。
1. 如果在授权响应的ID Token中包含敏感的个人身份信息，则应该对ID Token进行签名和加密；
1. 如果不加密ID Token，则不应在授权响应中返回个人敏感信息；

> In addition, if the `response_type` value `code id_token` is used, the authorization server
> 1. shall support [OIDC]
> 1. shall support signed ID Tokens;
> 1. should support signed and encrypted ID Tokens;
> 1. shall return ID Token as a detached signature to the authorization response;
> 1. shall include state hash, `s_hash`, in the ID Token to protect the `state` value if the client supplied a value for `state`. `s_hash` may be omitted from the ID Token returned from the Token Endpoint when `s_hash` is present in the ID Token returned from the Authorization Endpoint;
> 1. if returning any sensitive personally identifiable information (PII) in the ID Token in the authorization response, should sign and encrypt the ID Token;
> 1. if not encrypting the ID Token, should not return sensitive personally identifiable information (PII) in the ID Token in the authorization response


NOTE：授权服务器中令牌端点返回的ID Token携带的claims可能会比授权响应中的ID Token更多。
> **NOTE:** The authorization server may return more claims in the ID Token from the token endpoint than in the one from the authorization response


#### 5.2.2.2 JARM

此外，如果采用response_type为code和response_mode为jwt的组合方式，则授权服务器：

1. 应按照[JARM]第4.3节的规定，创建JWT-secured授权响应；

> In addition, if the `response_type` value `code` is used in conjunction with the `response_mode` value `jwt`, the authorization server
> 1. shall create JWT-secured authorization responses as specified in [JARM], section 4.3;



#### 5.2.3 非公开客户端

非公开客户端除[RFC7636]外，还应支持Financial-grade API - Part 1: Read-Only API Security Profile中5.2.3和5.2.4的规定。
> A confidential client shall support the provisions specified in clause 5.2.3 and 5.2.4 of Financial-grade API - Part 1: Read-Only API Security Profile, except for [RFC7636] support.


此外，非公开客户端：

1. 应支持[MTLS]作为限制访问令牌发送者的机制；
1. 在认证请求中，应包括[OIDC]第6节所定义的request或request_uri参数；
1. 应确保授权服务器对用户进行了适当级别的认证，以满足客户端的预期需求；
1. (迁移到5.2.3.1)；
1. (已撤回)；
1. (已撤回)；
1. (迁移到5.2.3.1)；
1. 应发送授权请求签名对象中包含的所有参数；
1. 如果不使用[PAR]，则应按照OpenID Connect规范第6.1节的要求，使用OAuth 2.0请求语法发送response_type、client_id和scope参数/值的副本
1. 应在request object中发送aud claim，作为OP的签发这标识URL；
1. 应在request object中发送exp claim，其值不超过60分钟；
1. (迁移到5.2.3.1)；
1. (迁移到5.2.3.1)；
1. 应在request object中发送nbf claim；
1. 如果使用[PAR]，应使用[RFC7636]和S256作为code chanllenge；
1. 如果使用[PAR]，应按照[JAR]第5节的要求，另外使用OAuth 2.0请求语法向授权端点发送client_id参数/值的副本；

> In addition, the confidential client
> 1. shall support [MTLS] as mechanism for sender-constrained access tokens;
> 1. shall include the `request` or `request_uri` parameter as defined in Section 6 of [OIDC] in the authentication request;
> 1. shall ensure the Authorization Server has authenticated the user to an appropriate Level of Assurance for the client's intended purpose;
> 1. (moved to 5.2.3.1);
> 1. (withdrawn);
> 1. (withdrawn);
> 1. (moved 5.2.3.1);
> 1. shall send all parameters inside the authorization request's signed request object;
> 1. shall additionally send duplicates of the `response_type`, `client_id`, and `scope` parameters/values using the OAuth 2.0 request syntax as required by section 6.1 of the OpenID Connect specification if not using [PAR];
> 1. shall send the `aud` claim in the request object as the OP's Issuer Identifier URL;
> 1. shall send an `exp` claim in the request object that has a lifetime of no longer than 60 minutes;
> 1. (moved to 5.2.3.1);
> 1. (moved to 5.2.3.1);
> 1. shall send a `nbf' claim in the request object;
> 1. shall use [RFC7636] with `S256` as the code challenge method if using [PAR];
> 1. shall additionally send a duplicate of the `client_id` parameter/value using the OAuth 2.0 request syntax to the authorization endpoint, as required by section 5 of [JAR], if using [PAR];


#### 5.2.3.1 作为分离式签名的ID Token

此外，如果采用response_type值为code id_token的方式，则客户端：

1. 应在scope参数中加入openid域，以激活OIDC支持；
1. 应要求端点返回经过JWS签名的ID Token；
1. 使用ID Token作为分离的签名来验证授权响应没有被篡改；
1. 除[OIDC]3.3.2.12的所有要求外，还应该验证授权响应中返回的state值计算后是否等于s_hash。NOTE：这使得客户端可以通过作为分离签名的ID Token，去验证授权响应是否被篡改；
1. 应同时支持签名和签名&加密的ID Token；

> In addition, if the `response_type` value `code id_token` is used, the client
> 1. shall include the value `openid` into the `scope` parameter in order to activate [OIDC] support
> 1. shall require JWS signed ID Token be returned from endpoints;
> 1. shall verify that the authorization response was not tampered using ID Token as the detached signature
> 1. shall verify that `s_hash` value is equal to the value calculated from the `state` value in the authorization response in addition to all the requirements in 3.3.2.12 of [OIDC]. Note: this enables the client to verify that the authorization response was not tampered with, using the ID Token as a detached signature.
> 1. shall support both signed and signed & encrypted ID Tokens


#### 5.2.3.2 JARM

此外，如果采用response_type为code和response_mode为jwt的组合方式，则授权服务器：

1. 应按照[JARM]第4.4节的规定，创建JWT-secured授权响应；

> In addition, if the `response_type` value `code` is used in conjunction with the `response_mode` value `jwt`, the client
> 1. shall verify the authorization responses as specified in [JARM], section 4.4;


#### 5.2.4 (已撤回)

#### 5.2.5 (已撤回)

## 6. 访问受保护的资源(使用tokens)

### 6.1 简介

FAPI的端点是受OAuth 2.0保护的端点，可以返回与提交的访问令牌相关联的资源所有者的受保护信息。
> The FAPI endpoints are OAuth 2.0 protected resource endpoints that return protected information for the resource owner associated with the submitted access token.


### 6.2 读写访问的规范

#### 6.2.1 受保护资源的规范

支持本文档的受保护资源：

1. 应支持Financial-grade API - Part 1: Read Only API Security Profile第6.2.1节的规范；
1. 应遵守[MTLS]的要求；

> The protected resources supporting this document
> 1. shall support the provisions specified in clause 6.2.1 Financial-grade API - Part 1: Read Only API Security Profile;
> 1. shall adhere to the requirements in [MTLS].


#### 6.2.2 客户端规范

支持本文档的客户端应满足Financial-grade API - Part 1: Read-Only API Security Profile第6.2.2节的规范。
> The client supporting this document shall support the provisions specified in clause 6.2.2 of Financial-grade API - Part 1: Read-Only API Security Profile.


## 8. 安全考量

### 8.1 简介

作为OAuth 2.0授权框架的策略，本规范参考了[RFC6749]第10节中定义的安全考虑因素，以及[RFC6819]--OAuth 2.0 Threat Model and Security Considerations，其中详细介绍了各种威胁和缓解措施。
> As a profile of the OAuth 2.0 Authorization Framework, this specification references the security considerations defined in section 10 of [RFC6749], as well as [RFC6819] - OAuth 2.0 Threat Model and Security Considerations, which details various threats and mitigations.


### 8.2 资源服务器处理访问令牌的不确定性

客户端无法明确访问令牌是不记名令牌还是sender-constrained令牌。
两者在风险特征上有所差异，客户端可能希望区分它们。
符合本文档的受保护资源对它们进行了区分。
符合本文档的受保护资源不应接收不记名访问令牌。
他们应只支持通过[MTLS]实现的sender-constrained访问令牌。
> There is no way that the client can find out whether the resource access was granted for a bearer or sender-constrained access token.
> The two differ in the risk profile and the client may want to differentiate them.
> The protected resources that conform to this doc differentiate them.
> The protected resources that conform to this document shall not accept a bearer access token.
> They shall only support sender-constrained access tokens via [MTLS].


### 8.3 利用授权服务器端点弱绑定进行攻击
#### 
#### 8.3.1 简介

在[RFC6749]和[RFC6750]中，授权服务器提供的端点并没有紧密的绑定在一起，没有授权服务器标识符的概念(issuer标识符)，除非客户端为每个授权服务器使用不同的重定向URI，否则它不会在授权响应中显示出来。但这(使用不同的redirect_uri)在OAuth模型中是假定的，没有明确的写出来，因此许多客户端对不同授权服务器仍然使用相同的重定向URI，这暴露了新的攻击面。目前已经发现了几种攻击，在[RFC6819]中详细解释了这些威胁。
> In [RFC6749] and [RFC6750], the endpoints that the authorization server offers are not tightly bound together.
> There is no notion of authorization server identifier (issuer identifier) and it is not indicated in
> the authorization response unless the client uses different redirection URI per authorization server.
> While it is assumed in the OAuth model, it is not explicitly spelled out and thus many clients
> use the same redirection URI for different authorization servers exposing an attack surface.
> Several attacks have been identified and the threats are explained in detail in [RFC6819].


#### 8.3.2 在令牌端点对客户凭证和授权码实施钓鱼攻击

在此类攻击中，客户端开发人员因受社会工程学攻击的影响，相信令牌端点已经修改为被攻击者控制的URL，结果，客户端错误的将授权码和client secret发送给攻击者，随后攻击者可进行重播攻击。
> In this attack, the client developer is socially engineered into believing that the token endpoint has changed
> to the URL that is controlled by the attacker. As a result, the client sends the `code` and the client secret to
> the attacker, which will be replayed subsequently.


当FAPI客户端使用[MTLS]时，客户端的私钥(TLS对应的私钥)不会暴露给攻击者，因此攻击者无法向授权服务器的端点发起认证。
> When the FAPI client uses [MTLS], the client's secret (the private key corresponding to its TLS certificate) is
> not exposed to the attacker, which therefore cannot authenticate towards the token endpoint of the authorization server.


#### 8.3.3 身份提供者(IdP - Identity provicder)混淆攻击

在此类攻击中，客户端注册了多个IdP，其中有一个为恶意IdP，它返回与其中一个正常IdP相同的client_id。当用户点击恶意链接或被入侵的网站时，授权请求会被发送到恶意IdP。
恶意Idp就会将客户端重定向到拥有相同client_id的正常IdP，如果用户已经在正常的IdP登录过，那么认证可能会被跳过，并且正常Idp会生成授权码并发挥给客户端，由于客户端正在与恶意IdP交互，因此该授权码会被发送到恶意IdP的令牌端点，此时，攻击者就能获取到一个有效的授权码，并可以在正常IdP处换取访问令牌。
> In this attack, the client has registered multiple IdPs and one of them is a rogue IdP that returns the same `client_id`
> that belongs to one of the honest IdPs. When a user clicks on a malicious link or visits a compromised site,
> an authorization request is sent to the rogue IdP.
> The rogue IdP then redirects the client to the honest IdP that has the same `client_id`.
> If the user is already logged on at the honest IdP,
> then the authentication may be skipped and a code is generated and returned to the client.
> Since the client was interacting with the rogue IdP, the code is sent to the rogue IdP's token endpoint.
> At the point, the attacker has a valid code that can be exchanged for an access token at the honest IdP.


这可以通过OpenID Connect Hybrid Flow来缓解，其中正常IdP的issuer标识会被包含到iss中，或者通过[JARM]放到响应JWT中。在收到授权响应时，客户端将响应中的iss值与它发送授权请求的IdP(恶意IdP)的issuer URL进行对比，当出现冲突时则中止交易。
> This is mitigated by the use of OpenID Connect Hybrid Flow in which the honest IdP's issuer identifier is included as the value of `iss` or [JARM]
> where the `iss` included in the response JWT. On receiving the authorization response, the client compares the `iss` value from the response with the
> issuer URL of the IdP it sent the authorization request to (the rogue IdP). The client detects the conflicting issuer values and aborts the transaction.


#### 8.3.4 (removed)

#### 8.3.5 访问令牌钓鱼攻击

当FAPI客户端使用[MTLS]时，访问令牌会绑定在客户端的TLS证书上，由于被钓鱼的访问令牌无法使用，因此具有防钓鱼的功能。
> When the FAPI client uses [MTLS], the access token is bound to the client's TLS certificate, it is access token phishing resistant as the phished access tokens cannot be used.


### 8.4 修改授权请求和响应的攻击

#### 8.4.1 简介

在[RFC6749]中，授权请求和响应不受完整性保护，因此，攻击者可以修改它们。
> In [RFC6749] the authorization request and responses are not integrity protected.
> Thus, an attacker can modify them.


#### 8.4.2 对授权请求参数的注入攻击

在[RFC6749]中，授权请求是以query parameter形式发送的。
虽然[RFC6749]规定使用TLS，但TLS是在浏览器中卸载的，在浏览器中并不受保护；因此，攻击者可以篡改授权请求并插入任何参数值。
> In [RFC6749], the authorization request is sent as a query parameter.
> Although [RFC6749] mandates the use of TLS, the TLS is terminated in the browser and thus not protected within the browser; as a result an attacker can tamper the authorization request and insert any parameter values.


在授权请求中使用request object或request_uri将阻止请求参数的篡改。
> The use of a `request` object or `request_uri` in the authorization request will prevent tampering with the request parameters.


SoK: Single Sign-On Security - An Evaluation of OpenID Connect中披露的IdP混淆攻击就是这种攻击的一个例子。
> The IdP confusion attack reported in [SoK: Single Sign-On Security – An Evaluation of OpenID Connect](https://www.nds.rub.de/media/ei/veroeffentlichungen/2017/01/30/oidc-security.pdf) is an example of this kind of attack.


#### 8.4.3 对授权响应参数的注入攻击

这种攻击发生在攻击者和受害者使用同一个客户端时，攻击者可以从受害者的授权响应中获取授权码和状态，并在自己的授权响应中使用它们。
> This attack occurs when the victim and attacker use the same relying party client. The attacker is somehow able to
> capture the authorization code and state from the victim's authorization response and uses them in his own
> authorization response.


这可以通过使用OpenID Connect Hybrid Flow来缓解，其中c_hash、at_hash和s_hash可以用来验证授权码、访问令牌和state参数。也可以使用[JARM]，通过验证授权响应JWT的完整性来缓解。
> This can be mitigated by using OpenID Connect Hybrid Flow where the `c_hash`, `at_hash`,
> and `s_hash` can be used to verify the validity of the authorization code, access token,
> and state parameters. It can also be mitigated using [JARM] by verifying the integrity of the authorization response JWT.


服务器可以校验state是否与发送授权请求时浏览器会话中存储的state一致。
> The server can verify that the state is the same as what was stored in the browser session at the time of the authorization request.


### 8.5 TLS注意事项

由于正在交换私密信息，因此所有交互都必须通过TLS加密(HTTPS)。
> As confidential information is being exchanged, all interactions shall be encrypted with TLS (HTTPS).


应实现Financial-grade API - Part 1: Read Only API Security Profile第7.1章节，以及如下附加要求：

1. 对于1.3以下的TLS版本，只允许使用以下4种密码套件
   - TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
   - TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
   - TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
   - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
2. 对授权端点，如有必要，授权服务器可以使用最新版本的[BCP195]所允许的额外密码套件，以便与用户的web浏览器有更好的交互；
2. 当使用TLS_DHE_RSA_WITH_AES_128_GCM_SHA256或TLS_DHE_RSA_WITH_AES_256_GCM_SHA384密码套件时，其密钥长度至少为2048位；

> Section 7.1 of Financial-grade API - Part 1: Read Only API Security Profile shall apply, with the following additional requirements:
> 1. For TLS versions below 1.3, only the following 4 cipher suites shall be permitted:
>    - `TLS_DHE_RSA_WITH_AES_128_GCM_SHA256`
>    - `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`
>    - `TLS_DHE_RSA_WITH_AES_256_GCM_SHA384`
>    - `TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384`
> 2. For the `authorization_endpoint`, the authorization server MAY allow additional cipher suites that are permitted by the latest version of [BCP195], if necessary to allow sufficient interoperability with users' web browsers.
> 2. When using the `TLS_DHE_RSA_WITH_AES_128_GCM_SHA256` or `TLS_DHE_RSA_WITH_AES_256_GCM_SHA384` cipher suites, key lengths of at least 2048 bits are required.


### 8.6 算法注意事项

对JWS，客户端和授权服务器：

1. 应使用PS256或ES256算法；
1. 不应该使用RSASSA-PKCS1-v1_5类算法(如：RS256)；
1. 不得使用none；

> For JWS, both clients and authorization servers:
> 1. shall use `PS256` or `ES256` algorithms;
> 1. should not use algorithms that use RSASSA-PKCS1-v1_5 (e.g. `RS256`);
> 1. shall not use `none`;


### 8.6.1 加密算法的注意事项

对JWE，客户端和授权服务器：

1. 不应该使用RSA1_5算法；

> For JWE, both clients and authorization servers
> 1. shall not use the `RSA1_5` algorithm.


### 8.7 对规范不完整或错误的实现

为实现全量的安全保障，对本规范以及底层的OpenID Connect和OAuth规范的完整和正确的实现都非常重要。
> To achieve the full security benefits, it is important the implementation of this specification, and the underlying OpenID Connect and OAuth specifications, are both complete and correct.


OpenID基金会提供了一些工具，可以用来检验一个实现是否正确。
> The OpenID Foundation provides tools that can be used to confirm that an implementation is correct:


[https://openid.net/certification/](https://openid.net/certification/)

OpenID基金会维护着一份经过认证的实现清单：
> The OpenID Foundation maintains a list of certified implementations:


[https://openid.net/developers/certified/](https://openid.net/developers/certified/)

基于本规范的部署方，应采用认证过的实现。
> Deployments that use this specification should use a certified implementation.


### 8.8 会话固定攻击

攻击者可以准备一个授权请求的URL，并欺骗受害者授权访问所请求的资源，例如，通过电子邮件发送该URL，或在假网站上使用它。
> An attacker could prepare an authorization request URL and trick a victim
> into authorizing access to the requested resources, e.g. by sending the URL
> via e-Mail or utilizing it on a fake site.


OAuth 2.0可以防止这种攻击，因为获取访问令牌的过程(授权码交换、CSRF保护等)被设计成只要攻击者无法控制受害者的浏览器，就无法获取和使用令牌。
> OAuth 2.0 prevents this kind of attack since the process for obtaining the
> access token (code exchange, CSRF protection etc.) is designed in a way that the
> attacker will be unable to obtain and use the token as long as it does not
> control the victim's browser.


然而，如果API允许在授权过程中、在访问令牌签发前执行任何特权操作，这些控制就会失效。因此，本规范的实践者应确保所有操作都是使用授权过程中发出的访问令牌执行的。
> However, if the API allows execution of any privileged action in the course of
> the authorization process before the access token is issued, these controls are
> rendered ineffective. Implementers of this specification therefore shall ensure
> any action is executed using the access token issued by the authorization
> process.


例如，支付动作不应在授权过程中执行，而应在客户端将授权码交换为访问令牌之后，并向受保护端点发送携带访问令牌的"执行支付"请求后执行。
> For example, payments shall not be executed in the authorization process but
> after the Client has exchanged the authorization code for a token and sent an
> "execute payment" request with the access token to a protected endpoint.


### 8.9 JWKS URIs

该策略要求客户端和授权服务器都要用对方的密钥验证payloads。AS需验证request object和private_key_jwt断言，客户端验证ID Token和授权响应的JWT。对于AS来说，本规范强烈建议使用JWKS URI端点来分发公钥，对于客户端，本规范建议使用 JWKS URI 端点，或者结合[RFC7591]和[RFC7592]使用jwks参数。
> This profile requires both Clients and Authorization Servers to verify payloads
> with keys from the other party. The AS verifies request objects and `private_key_jwt`
> assertions. The Client verifies ID Tokens and authorization response JWTs. For AS's
> this profile strongly recommends the use of JWKS URI endpoints to distribute
> public keys. For Clients this profile recommends either the use of JWKS URI endpoints
> or the use of the `jwks` parameter in combination with [RFC7591]
> and [RFC7592].


AS jwks_uri的定义可以在[RFC8414]中找到，而客户端jwks_uri的定义可以在[RFC7591]中找到。
> The definition of the AS jwks_uri can be found in [RFC8414], while the definition
> of the Client jwks_uri can be found in [RFC7591].


此外，该策略：

1. 要求jwks_uri端点应通过TLS提供服务；
1. 建议不要使用x5u和jku的JOSE头；
1. 建议JWK集不包含相同的多个密钥；

> In addition, this profile
> 1. requires that jwks_uri endpoints shall be served over TLS;
> 1. recommends that JOSE headers for x5u and jku should not be used;
> 1. recommends that the JWK set does not contain multiple keys with the same `kid`.


### 8.10 多客户端共享密钥

使用[MTLS]来进行客户端认证和sender-constrained访问令牌，比使用共享密钥有显著的安全优势。然而，在某些情况下，[MTLS]所使用的证书是由机构级而非客户端级的证书颁发机构颁发的。在这种情况下，拥有多个客户端的组织可能会在客户端使用相同的证书(或具有相同DN的证书)。实施者应该意识到，这种共享意味着，任何一个客户机受到损害，都会导致所有共享同一密钥的客户机受到损害。
> The use of [MTLS] for client authentication and sender constraining access tokens brings
> significant security benefits over the use of shared secrets. However in some deployments
> the certificates used for [MTLS] are issued by a Certificate Authority at an organisation
> level rather than a client level. In such situations it may be common for an organisation
> with multiple clients to use the same certificates (or certificates with the same DN)
> across clients. Implementers should be aware that such sharing means that a compromise
> of any one client, would result in a compromise of all clients sharing the same key.


### 8.11 重复的密钥标识

JWK集不应该包括位多个密钥使用相同的kid，但是，为提高多个密钥使用相同kid的交互性，验证方可以考虑当特定的JWS消息选择密钥时使用其它JWK属性，如kty、use、alg等。例如，在选择使用哪个密钥来验证消息签名时，可以使用如下方法：

1. 查找与JOSE头中kid相匹配的密钥；
1. 如果找到唯一的密钥，则使用该密钥；
1. 如果找多多个密钥，那么验证方应该遍历这些密钥，直到找到一个与被验证信息的alg、use、kty或crv属性都匹配的密钥；


> JWK sets should not contain multiple keys with the same `kid`. However, to increase
> interoperability when there are multiple keys with the same `kid`,  the verifier shall
> consider other JWK attributes, such as kty, use, alg, etc., when selecting the
> verification key for the particular JWS message. For example, the following algorithm
> could be used in selecting which key to use to verify a message signature:
> 
> 1. Find keys with a `kid` that matches the `kid` in the JOSE header;
> 1. If a single key is found, use that key;
> 1. If multiple keys are found, then the verifier should iterate through the keys until a key is found that has a matching `alg`, `use`, `kty`, or `crv` that corresponds to the message being verified.


## 9. 隐私考量

### 9.1 简介

在实践本文档时，在隐私方面有很多因素需要考量。但是，由于本文档是对OAuth和OpenID Connect的介绍，所有这些因素都是通用的，适用于OAuth或OpenID Connect，并非针对本文档。建议实施者进行全面的隐私影响评估，并适当管理已识别的风险。
> There are many factors to be considered in terms of privacy
> when implementing this document. However, since this document
> is a profile of OAuth and OpenID Connect, all of them
> are generic and applies to OAuth or OpenID Connect and
> not specific to this document. Implementers are advised to
> perform a thorough privacy impact assessment and and manage identified risks appropriately.


NOTE：实施者可以参考[ISO29100]和[ISO29134]等文件来实现这一目的。
> NOTE: Implementers can consult documents like
> [ISO29100] and [ISO29134] for this purpose.


OAuth和OpenID Connect实施过程的隐私风险包括以下几点：

- (不恰当的隐私声明)在policy_url处或通过其他方式提供的隐私声明可能是不适当的。
- (选项不充分)在没有充分选项的情况下，提供的"用户同意"并不构成同意。
- (滥用数据)AS、RS或客户有可能不按照约定的目的使用数据。
- (违反收集最小化原则)客户要求提供的数据超过了为达到目的所需的绝对数量，这违反了收集最小化原则。
- (资源方主动提供的个人数据)一些不良的资源服务器实现可能会返回比请求的数据更多的数据。如果这些数据是个人数据，那么这将违反隐私原则。
- (违反数据最小化原则)任何一个处理数据的程序如果处理超过它所需要的数据，这就违反了数据最小化原则。
- (AS/OP对RP的跟踪)AS/OP识别正向哪个Client/RP提供哪些数据。
- (RP跟踪用户)两个或以上RP通过关联访问令牌或ID令牌来跟踪用户。
- (AS导致用户对RP的误认)由于AS的授权页面对RP的表述混乱，用户误解了RP是谁。
- (用户的理解或RP向用户显示的内容与实际的授权请求不匹配)为了提高生态系统的信任度，最佳实践是AS要明确授权请求中包括哪些内容(例如，哪些数据将被发布给RP)。
- (攻击者观察授权请求中的个人数据) 授权请求可能包含个人数据。这可以被攻击者观察到。
- (攻击者在授权端点响应中观察个人数据) 在一些框架中，甚至状态也被视为个人数据，这可以被攻击者通过各种手段观察到。
- (AS的数据泄露)AS存储了个人数据。如果AS存在泄露问题，这些数据就会泄露或被修改。
- (来自RS的数据泄露)一些资源服务器(RS)存储着个人数据。如果RS被入侵，这些数据可能会被泄露或被修改。
- (来自客户端的数据泄漏)一些客户端存储了个人数据，如果客户端被入侵，这些数据就会泄漏或被修改。

> Privacy threats to OAuth and OpenID Connect implementations include the following:
> 
> - (Inappropriate privacy notice) A privacy notice provided at a `policy_url` or by other means can be inappropriate.
> - (Inadequate choice) Providing a consent screen without adequate choices does not form consent.
> - (Misuse of data) An AS, RS or Client can potentially use the data not according to the purpose that was agreed.
> - (Collection minimization violation) Clients asking for more data than it absolutely needs to fulfil the purpose is violating the collection minimization principle.
> - (Unsolicited personal data from the Resource) Some bad resource server implementations may return more data than was requested. If the data is personal data, then this would be a  violation of privacy principles.
> - (Data minimization violation) Any process that is processing more data than it needs is violating the data minimization principle.
> - (RP tracking by AS/OP) AS/OP identifying what data is being provided to which Client/RP.
> - (User tracking by RPs) Two or more RPs correlating access tokens or ID Tokens to track users.
> - (RP misidentification by User at AS) User misunderstands who the RP is due to a confusing representation of the RP at
the AS's authorization page.
> - (Mismatch between User’s understanding or what RP is displaying to a user and the actual authorization request). To enhance
the trust of the ecosystem, best practice is for the AS to make clear what is included in the authorisation request (for example,
what data will be released to the RP).
> - (Attacker observing personal data in authorization request) Authorization request might contain personal data. This can be observed by an attacker.
> - (Attacker observing personal data in authorization endpoint response) In some frameworks, even state is deemed personal data.
This can be observed by an attacker through various means.
> - (Data leak from AS) AS stores personal data. If AS is compromised, these data can leak or be modified.
> - (Data leak from Resource) Some resource servers (RS) store personal data. If a RS is compromised, these data can leak or be modified.
> - (Data leak from Clients) Some clients store personal data. If the client is compromised, these data can leak or be modified.


这些问题可以通过选择OAuth或OpenID中合适的选项，或引入一些操作规则来缓解。
例如"攻击者观察授权请求中的个人数据"问题，可以通过使用request_uri引用授权请求或加密request object来缓解。
同样的，"攻击者在授权端点响应中观察个人数据"问题，可以通过加密ID Token或JARM响应来缓解。
> These can be mitigated by choosing appropriate options in OAuth or OpenID, or by introducing some operational rules.
> For example, "Attacker observing personal data in authorization request" can be mitigated by either using authorization request by reference
> using `request_uri` or by encrypting the request object.
> Similarly, "Attacker observing personal data in authorization endpoint response" can be mitigated by encrypting the ID Token or JARM response.


## 10. 致谢

The following people contributed to this document:

- Nat Sakimura (NAT Consulting) -- Chair, Editor
- Anoop Saxana (Intuit) -- Co-chair, FS-ISAC Liaison
- Anthony Nadalin (Microsoft) -- Co-chair, SC 27 Liaison
- Edmund Jay (Illumila) -- Co-editor
- Dave Tonge (Moneyhub) -- Co-chair, UK Implementation Entity Liaison
- Paul A. Grassi (NIST) -- X9 Liaison
- Joseph Heenan (Authlete)
- Sascha H. Preibisch (CA)
- John Bradley (Yubico)
- Henrik Biering (Peercraft)
- Tom Jones (Independent)
- Axel Nennker (Deutsche Telekom)
- Torsten Lodderstedt (yes.com)
- Ralph Bragg (Raidiam)
- Brian Campbell (Ping Identity)
- Dima Postnikov (Independent)
- Stuart Low (Biza.io)

## 11. 参考文献

- [ISODIR2] ISO/IEC Directives Part 2
- [ISO29100] ISO/IEC 29100 Information technology — Security techniques — Privacy framework
- [ISO29134] ISO/IEC 29134 Information technology — Security techniques — Guidelines for privacy impact assessment
- [ISO29184] ISO/IEC 29184 Information technology — Online privacy notices and consent
- [RFC6749] The OAuth 2.0 Authorization Framework
- [RFC6750] The OAuth 2.0 Authorization Framework: Bearer Token Usage
- [RFC7636] Proof Key for Code Exchange by OAuth Public Clients
- [RFC6819] OAuth 2.0 Threat Model and Security Considerations
- [RFC7519] JSON Web Token (JWT)
- [RFC7591] OAuth 2.0 Dynamic Client Registration Protocol
- [RFC7592] OAuth 2.0 Dynamic Client Registration Management Protocol
- [OIDC] OpenID Connect Core 1.0 incorporating errata set 1
- [OIDD] OpenID Connect Discovery 1.0 incorporating errata set 1
- [MTLS] OAuth 2.0 Mutual TLS Client Authentication and Certificate Bound Access Tokens
- [JARM] Financial Services – Financial-grade API: JWT Secured Authorization Response Mode for OAuth 2.0
- [SoK] Mainka, C., Mladenov, V., Schwenk, J., and T. Wich: SoK: Single Sign-On Security – An Evaluation of OpenID Connect

## 12. IANA注意事项

### 12.1 Additions to JWT Claims Registry

本规范向[RFC7519]发布的"JSON Web Token Claims"中增加了部分值。
> This specification adds the following values to the "JSON Web Token Claims" registry
> established by [RFC7519].


#### 12.1.1. Registry Contents

- Claim name: s_hash
- Claim Description: State hash value
- Change Controller: OpenID Foundation Financial-Grade API Working Group - [openid-specs-fapi@lists.openid.net](mailto:openid-specs-fapi@lists.openid.net)
- Reference: Section 5 of [[ this specification ]]

## 附录A. 案例

以下时符合本规范的多种对象的非规范性示例，仅用作展示目的。
> The following are non-normative examples of various objects compliant with this specification, with line wraps within values for display purposes only.


The examples signed by the client may be verified with the following JWK:

```
{
  "kty": "RSA",
  "e": "AQAB",
  "use": "sig",
  "kid": "client-2020-08-28",
  "alg": "PS256",
  "n": "i0Ybm4TJyErnD5FIs-6sgAdtP6fG631FXbe5gcOGYgn9aC2BS2h9Ah5cRGQpr3aLLVKCRWU6
HRfnGseUBOejo57vI-kgab2YsQJSwedAxvtKrIrJlgKn1gTXMNsz-NQd1LyLSV50qJVEy5l9RtsdDzOV
8_kLCbzroEL3rc00iqVZBcQiYm8Bx4z0G8LYZ4oMJAG462Mf_znJkKXsuSIH735xnSmx74CC8TOe6G-V
0Wi_wVSJ9bHPphSki_kWUtjVGcnyjYuQVE0LRj3qrGPAX9bsVKSqs8T9AM41TB9oV5Sjz5YhggwICvvC
CGwil9qhUoQRkeXtWuGCfvCSeTdawQ"
}
```

The examples signed by the server may be verified with the following JWK:

```
{
  "kty": "RSA",
  "e": "AQAB",
  "use": "sig",
  "kid": "server-2020-08-28",
  "alg": "PS256",
  "n": "pz6g0h7Cu63SHE8_Ib4l3hft8XuptZ-Or7v_j1EkCboyAEn_ZCuBrQOmpUIoPKrA0JNWK_fF
eZ2q1_26Gvn3E4dQlcOWpiWkKmxAhYCWnNDv3urVgldDp_kw0Dx2H8yn9tmFW28E_WvrZRwHEF5Czigb
xlmFIrkniMHRzjyYQTHRU0gW3DRV9MrQQrmP71McvfLPeMBPPgsHgLo7KmUBDoUjsgnwgycEOWPm8MWJ
13dpTsVnoWNIFQqVNz1L5pRU3Uoknl0MGoE6v0M9lfgQgzxIX9gSB1VGp5zZRcsnZGU3MFpwBhOWwiCU
wqztoX0H5P0g7OWocspHrDn6YOgxHw"
}
```

The code that generated these examples can be found here:

[https://gitlab.com/emobix/fapi-examples](https://gitlab.com/emobix/fapi-examples)

### A.1 Example request object

```
eyJraWQiOiJjbGllbnQtMjAyMC0wOC0yOCIsImFsZyI6IlBTMjU2In0.eyJhdWQiOiJodHRwczpcL1wv
ZmFwaS1hcy5leGFtcGxlLmNvbVwvIiwic2NvcGUiOiJvcGVuaWQgcGF5bWVudHMiLCJpc3MiOiI1MjQ4
MDc1NDA1MyIsInJlc3BvbnNlX3R5cGUiOiJjb2RlIGlkX3Rva2VuIiwicmVkaXJlY3RfdXJpIjoiaHR0
cHM6XC9cL2ZhcGktY2xpZW50LmV4YW1wbGUub3JnXC9mYXBpLWFzLWNhbGxiYWNrIiwic3RhdGUiOiJW
Z1NVSUVuZmxuRHhUZTF2QXRyNTRvIiwiZXhwIjoxNTk0MTQwMzkwLCJub25jZSI6Ijd4RENIdml1UE1T
WEpJaWdrSE9jRGkiLCJjbGllbnRfaWQiOiI1MjQ4MDc1NDA1MyJ9.aGqQcWpsvGpzNi8H1CMcV3uC3Ng
gAGvMTkwV9Ttci5Pci-dIU2E9FvumcNXO6T4ScEdv1WeY_qC-B8ULgd7ui53t-Yhe_3rUuv4pIso5iql
NlufQlaLvaJ7WPmz3DEqkjJwEAK1fi-PTFFjp-DF3cbbbAFptcchVcXkKM0VoUueTHiq8BAysLJ3WEev
pn9GVq9W3TAjL1nB3rPv-hKfJhUNCpbTT7eIzHpznRu_JBzCvcvC_q1oD1hUlPLV-Isy20lROSB7VS-e
Cap-pgoyjDIkYW0U3BxapM13vqZ29HRWui8NdNvbAqBglrQ_g97DMFuZmnyaOYaUyk_8J5JLwZw
```

which when decoded has the following body:

```
{
  "aud": "https://fapi-as.example.com/",
  "scope": "openid payments",
  "iss": "52480754053",
  "response_type": "code id_token",
  "redirect_uri": "https://fapi-client.example.org/fapi-as-callback",
  "state": "VgSUIEnflnDxTe1vAtr54o",
  "exp": 1594140390,
  "nonce": "7xDCHviuPMSXJIigkHOcDi",
  "client_id": "52480754053"
}
```

### A.2 Example signed id_token for authorization endpoint response

```
eyJraWQiOiJzZXJ2ZXItMjAyMC0wOC0yOCIsImFsZyI6IlBTMjU2In0.eyJzdWIiOiIxMDAxIiwiYXVk
IjoiNTI0ODA3NTQwNTMiLCJjX2hhc2giOiJRUjJ6dWNmWVpraUxyYktCS0RWcGdRIiwic19oYXNoIjoi
OXM2Q0JiT3hpS0U2NWQ5LVFyMFFJUSIsImF1dGhfdGltZSI6MTU5NDE0MDA5MCwiaXNzIjoiaHR0cHM6
XC9cL2ZhcGktYXMuZXhhbXBsZS5jb21cLyIsImV4cCI6MTU5NDE0MDM5MCwiaWF0IjoxNTk0MTQwMDkw
LCJub25jZSI6Ijd4RENIdml1UE1TWEpJaWdrSE9jRGkifQ.Z-LpQRuYoiTqEBfVfctn-e6bLwSMqi8wA
3TuARGW6GyD05gPF6TVlUwHgJnSUlhETrzhEUAKKiyGDxGspuBU0OAnB4qepgrEBizk980NjCEVXNkog
v0ANv9VX_01Lcl0d_6_c-AUjwDSuKY8rDfvggKSJFzRilbQuB8b1drAIAZpc6kMObY3PcQZ_vKTMsQ8l
HCuXXRuAo__0xRE6l_iiRCos_940GrJr0Sih9uTQpnCWBoEab1dC0l-vUp4lP0TQRKNpDoPoMOj10KJA
8T8pKhjZ8TKM-wo9A4qH2LBgUIYJyjd8bWfKTZxCNmLRzRr-_JBG7fF_fpOUhGT_DhzMw
```

which when decoded has the following body:

```
{
  "sub": "1001",
  "aud": [
    "52480754053"
  ],
  "c_hash": "QR2zucfYZkiLrbKBKDVpgQ",
  "s_hash": "9s6CBbOxiKE65d9-Qr0QIQ",
  "auth_time": 1594140090,
  "iss": "https://fapi-as.example.com/",
  "exp": 1594140390,
  "iat": 1594140090,
  "nonce": "7xDCHviuPMSXJIigkHOcDi"
}
```

### A.3 Example signed and encrypted id_token for authorization endpoint response

```
eyJraWQiOiJjbGllbnQtZW5jLTIwMjAtMDgtMjgiLCJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwi
YWxnIjoiUlNBLU9BRVAtMjU2In0.LFvxFCzJ-1NRl48pXTUs8f2axm5MRe9Cv0dgV6sXTRKwkT3nC2SJ
QlutOol36VARLd3uaIoj4Z7LVV_MrdIYYvDci2WLlKSlI_NRgR3qJ25N3S6fCqNEYRgDDbNzSr15MDRc
WQR5Jdl3VP8g748cowD_2gaopaCzZWTa3r_J2VOEETfcBAIMX0NbtVA3hHW-rQ0aCC7UIbP0_oEB2YF0
u6qAXCXuC02nO6coMSpSHTDZwkqkmFiFEKERM_Gayz3lVddlgfcPR2k76bCUjWy934-rOrOBGcLyS1Ww
aTIqMUS3WEIsAwCDr1Jt4pAioryRLZfLmWNff4QZSBxWejRqpw.uRANzseIWYB9YeAW.sJGqF2ERkMEE
jm8h62tUA4UeZIBqvVRpkQqjTuae7-4ac-4sSth0A3zeERvlyC5GcP0W2tj7uxMi0I4gpN33OfAOR-tA
9E_47oCHXrOH-7cpLgVIxxWZFx43dhxUh5QHuBfli4nHErMVUsFq6CzQj8Z5SHvBD2Qx3suPEeCNo_M2
woohCprwjOKhE-Q_VkWUJb-Elrq9HxJcBtadw0spolqgYYTIWvV4fcKmbtGANYLac29oKWd5-jyDAsSF
FZrSCNxv-BtJUiUVWUn5eVufjJYCx62Ju-MZ8vsPNTE-_I5em9RTBja6ylcivjzhW9Ncl6yKVfnB0XJN
cSSHQSFhc6Gvy7oYMBXx1C5G31OsiklkKQX2gsAZlxFQ_X25AXpMoV8-5xsUwdMdTaPxIIsccbrK2dfA
aP0rUruSV8zrlrbsN3ftjTJSka2XGG3kra76EPAlzSwxy6XdFVtEV31hirV3f9g04Gj_e-Q7J7HR62eY
3_09WyARShQL3DVXWOcK_8YrLr58JjNAbm0s5dAUq-zt9cMv8rl05t_dE59Gi6Hnl2YAiRdYG6B71FxJ
CE2Uqciy2jLe6mCDFDfqkog4G5R9FzNz5VzhVpmZVm3OJkug-UzayN7nwZ7jsmxQ2ucCM03xq-0MLdsk
H-cleahkFw5S-W40cn5hLrRXSqUoYfKmVSd9RltOZ6T0VrYpw2LaF2uUYEO9w9bMmg2zzfxft4WHsEbD
OlJVb5SE8mUjzBBZAcgaHYSv0Wii70lEJvLSdnVI1r9kuu9ae_j1Tu08RVyFGfgixYjI9z2L_sc8uOoO
HJ-Tq1iuncL3lCQJBuwBFoxyINlFgz4YV2AgreNsX8bDfE9XbRB9TnfvSd6rmes9lO0-3VQFlsC0C5dx
VXgp5o05E8nisPwuLmlGO5BTtBzCQ3tIH2SuTLTG-gohTEUVn4fACwIiyuXdPXcF4GxJNRNgNOH7xwxx
55qEM0xl2GuSseV59FiZR-WKMMs.kScy0JLB4XECklDAwTIVNA
```

which when decrypted using the following key:

```
{
    "kty": "RSA",
    "d": "OjDe8EkZXgvB-Gy5A4EdU8fBuAjdHLMyHKAtMaS_W_joEJHDvZRhIYbh1jAyHYoR3kFMXu
tCIYpRjDrsUEhjYuVKLm90CVtysoRjjkiXyupcEW3o--X_HBJhKm1Y-0I7LQ-cA7CotJpTVMR2fRTqP1
T4FsORAjg9l-fbdpVmeDiZBRbL2zCWmKWhtDpHyy7vbSCRghntihz_M5Hrchk7r8ito_K3dFrV9IZSF9
RoEY7kyK5bL36Kpgai44PYCzqOzqP2fteO_rZ9fn-uK59pI3ySo_PgSbJ55n14Nd9Z8m70zE9Z4aIeND
EFspZUhavngRwc7MuJ7f_hVGQ9RFbbkQ",
    "e": "AQAB",
    "use": "enc",
    "kid": "client-enc-2020-08-28",
    "n": "jVc92j0ntTV0V1nwZ3mpGaV2bME4d6AMS2SRrJBM0fLehaTEqDNzGu0warz2SC9bhcBOB5
_q3mYBFjmTwWzSbsk6RYETnAgViXg67PgH7Vkx2NCtwgQW3cNdnUZWRNYHsoevkx_Ta1X6Vi9ulebU_B
CKjrF-6CjVcGgEsO_S5DKcukGHdf81WlQOq3zGQg4h7MLArrbPSTHHORDsu_87qY9m2EhiYSOBSF5rHs
fDo7zWI5FWNG-_HO-CBM005bykIIS1aXCXx1jOW1OrKcp5xv3e-BR6MJTxncZJ4o1GtynJI8kLXRgltL
ArSOkbzNEr9GjU9lnSSxKLMtRLKkG2Ow"
}
```

has the following body:

```
{
  "sub": "1001",
  "aud": "2334382354153498",
  "acr": "urn:cds.au:cdr:2",
  "c_hash": "BLfy9hvQUZTDq6_KmF4kDQ",
  "s_hash": "9s6CBbOxiKE65d9-Qr0QIQ",
  "auth_time": 1595827190,
  "iss": "https://fapi-as.example.com/",
  "exp": 1595827490,
  "iat": 1595827190,
  "nonce": "7xDCHviuPMSXJIigkHOcDi"
}
```

### A.4 Example JARM response

```
eyJraWQiOiJzZXJ2ZXItMjAyMC0wOC0yOCIsImFsZyI6IlBTMjU2In0.eyJhdWQiOiI0NjkxODA2NDgw
MzkwNTEiLCJjb2RlIjoiendrR2FjOWp1TFg4RjhmcmFwRElTaTNLMkZ3bG40cXh3eWZOSUkzQ2p6MCIs
ImlzcyI6Imh0dHBzOlwvXC9mYXBpLWFzLmV4YW1wbGUuY29tXC8iLCJzdGF0ZSI6IlZnU1VJRW5mbG5E
eFRlMXZBdHI1NG8iLCJleHAiOjE1OTQxNDEwOTB9.k_3df0dIDX6watKxQkzAHOLgf4FBi_xIPN-n8aT
5hMX3gaBbeDqdUA5NR764L4ugdDgXyQm8dNcZrZldKIPfSfRcjBTtSx9PEdiffn_xUkwnS18YNAfEoq0
HjvkOQ59F21ImKn113kon00uC2dqBGByRrZcaUYOnvW2DdHCVA0VTW2je5nzbI02z9csLa8uGGGwjWRP
Ec9j9bvR1Adc2m2Z-o0QCRIBl81sZz6_AnE-wPTw-KZFQBs3FgS-r0FDYOzE7FHIMgDBSKAg1J5tWY3J
wRuIv_oAbYdSlxdYzrbFQ9grX4MA0p7pk5lS-kwnN845GZ2k1_yaOLtYYyvRFrw
```

which when decoded has the following body:

```
{
  "aud": "469180648039051",
  "code": "zwkGac9juLX8F8frapDISi3K2Fwln4qxwyfNII3Cjz0",
  "iss": "https://fapi-as.example.com/",
  "state": "VgSUIEnflnDxTe1vAtr54o",
  "exp": 1594141090
}
```

### A.5 Example private_key_jwt client assertion

```
eyJraWQiOiJjbGllbnQtMjAyMC0wOC0yOCIsImFsZyI6IlBTMjU2In0.eyJzdWIiOiI1MjQ4MDc1NDA1
MyIsImF1ZCI6Imh0dHBzOlwvXC9mYXBpLWFzLmV4YW1wbGUuY29tXC9hcGlcL3Rva2VuIiwiaXNzIjoi
NTI0ODA3NTQwNTMiLCJleHAiOjE1OTQxNDAxNTEsImlhdCI6MTU5NDE0MDA5MSwianRpIjoiNHZCY3RN
U2tLNHdmdU91aTlDeWMifQ.h3i0k2DWc7V6WEiinHAsse-pOFiWxe5kD4KetdGX65Q03orj0Fh6EWfdE
AntCrOodUsypKjM1ia3evbQmsSkhIb4YK5s53hYYtEbJC_eG9jFnVc4ki7Qc5O-1K-D80w7WT1UI--Ih
Ku-i22Ai_nMed-71UWLHcPi7W20SCroPHXfaLiFj_TOsr7I8h7VNsoa7P3-coHlXT5q4cMjIA7t8cRag
sGtKlIgwdFYySlimtSESDM0U-_NUPperTgnF8FVn7SqtizBJneZNAWwSLJD9AVsnMOH6kOeNLtpopsru
Dcs54S_aIlroP-BdiHw9R1qRTIVSoX3k_EStvoWSf8NcQ
```

which when decoded has the following body:

```
{
  "sub": "52480754053",
  "aud": "https://fapi-as.example.com/api/token",
  "iss": "52480754053",
  "exp": 1594140151,
  "iat": 1594140091,
  "jti": "4vBctMSkK4wfuOui9Cyc"
}
```
