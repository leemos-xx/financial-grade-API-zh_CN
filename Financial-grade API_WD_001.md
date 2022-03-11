# Financial-grade API - Part 1: Read-Only API Security Profile

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

金融科技是未来全球经济增长的领域之一，金融科技组织需要提升其运营安全性以及保护用户数据的能力。聚合服务普遍采用存储用户的密码，通过屏幕抓取的方式来捕获数据。这种脆弱、低效并且不安全的做法会导致安全漏洞，这就要求金融机构维持一个白名单，对白名单中的聚合商(译者注：不准确)放行，允许他们对应用进行类似自动攻击式的访问。本工作组提供的一个新的草案将使用具有结构化数据和令牌的API模型，如OAuth [RFC6749, RFC6750]。
> Fintech is an area of future economic growth around the world and Fintech organizations need to improve the security of their operations and protect customer data. It is common practice of aggregation services to use screen scraping as a method to capture data by storing users' passwords. This brittle, inefficient, and insecure practice creates security vulnerabilities which require financial institutions to allow what appears to be an automated attack against their applications and to maintain a whitelist of aggregators. A new draft standard, proposed by this workgroup would instead utilize an API model with structured data and a token model, such as OAuth [RFC6749, RFC6750].


金融级API旨在为线上的金融服务提供具体的实施指南，指导其开发一个由OAuth保障安全性的REST/JSON数据模型。金融级API安全规范可以适用于任何领域的线上服务，这将提供比标准的OAuth、或OpenID Connect更高的安全级别。
> The Financial-grade API aims to provide specific implementation guidelines for online financial services to adopt by developing a REST/JSON data model protected by a highly secured OAuth profile. The Financial-grade API security profile can be applied to online services in any market area that requires a higher level of security than provided by standard OAuth or OpenID Connect.


该文档是FAPI的第1部分，它描述了金融级API，并且提供一种OAuth的使用方式，以适用于访问只读类金融数据或类似案例的场景。
FAPI的第2部分提供更高的安全级别保障，适用于读写类的金融数据和其它风险等级更高的场景的访问。
> This document is Part 1 of FAPI that specifies the Financial-grade API and it provides a profile of OAuth that is suitable to be used in the access of read-only financial data and similar use cases.
> A higher level of security profile is provided in Part 2, suitable for read and write financial access APIs and other similar situations where the risk is higher.


尽管可以直接根据该规范去从零构建OpenID提供方和依赖方，但本规范的主要受众是已经实践了OpenID Connect并希望提升其安全级别的各方。我们鼓励实施者在从零开始构建前，先理解在7.6章节中描述的对安全的考量。
> Although it is possible to code an OpenID Provider and Relying Party from first principles using this specification, the main audience for this specification is parties who already have a certified implementation of OpenID Connect and want to achieve a higher level of security. Implementers are encouraged to understand the security considerations contained in section 7.6 before embarking on a 'from scratch' implementation.


### 符号约定

The key words "shall", "shall not",
"should", "should not", "may", and
"can" in this document are to be interpreted as described in
ISO Directive Part 2 [ISODIR2].
These key words are not used as dictionary terms such that
any occurrence of them shall be interpreted as key words
and are not to be interpreted with their natural language meanings.

# Financial-grade API - Part 1: Read-Only API Security Profile 

[TOC]

## 1. 范围

该文档定义了应用程序的如下行为:

- 以安全的方式获取OAuth令牌，用于对受保护数据的只读访问。
- 使用OpenID Connect(OIDC)来识别客户(用户)身份；以及
- 使用令牌从REST端点读取受保护的数据。

> This document specifies the method for an application to:
> - obtain OAuth tokens in a secure manner for read-only access to protected data;
> - use OpenID Connect (OIDC) to identify the customer (user); and
> - use tokens to read protected data from REST endpoints.


## 2. 参考文档

对本规范的实际应用而言，以下的参考规范必不可少。对标注日期的参考规范，仅引用的版本适用，而未标注日期的文档，其最新版本(包括所有修订)也适用本规范。
> The following referenced documents are indispensable for the application of this document. For dated references, only the edition cited applied. For undated references, the latest edition of the referenced document (including any amendments) applies.


[ISODIR2] - ISO/IEC Directives Part 2
[ISODIR2]: [https://www.iso.org/sites/directives/current/part2/index.xhtml](https://www.iso.org/sites/directives/current/part2/index.xhtml)

[RFC4122] A Universally Unique IDentifier (UUID) URN Namespace
[RFC4122]: [https://tools.ietf.org/html/rfc4122](https://tools.ietf.org/html/rfc4122)

[RFC6749] - The OAuth 2.0 Authorization Framework
[RFC6749]: [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749)

[RFC6750] - The OAuth 2.0 Authorization Framework: Bearer Token Usage
[RFC6750]: [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)

[RFC7636] - Proof Key for Code Exchange by OAuth Public Clients
[RFC7636]: [https://tools.ietf.org/html/rfc7636](https://tools.ietf.org/html/rfc7636)

[RFC6125] - Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security (TLS)
[RFC6125]: [https://tools.ietf.org/html/rfc6125](https://tools.ietf.org/html/rfc6125)

[BCP212] - OAuth 2.0 for Native Apps
[BCP212]: [https://tools.ietf.org/html/bcp212](https://tools.ietf.org/html/bcp212)

[RFC6819] - OAuth 2.0 Threat Model and Security Considerations
[RFC6819]: [https://tools.ietf.org/html/rfc6819](https://tools.ietf.org/html/rfc6819)

[BCP195] - Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS)
[BCP195]: [https://tools.ietf.org/html/bcp195](https://tools.ietf.org/html/bcp195)

[OIDC] - OpenID Connect Core 1.0 incorporating errata set 1
[OIDC]: [https://openid.net/specs/openid-connect-core-1_0.html](https://openid.net/specs/openid-connect-core-1_0.html)

[X.1254] - Entity authentication assurance framework
[X.1254]: [https://www.itu.int/rec/T-REC-X.1254](https://www.itu.int/rec/T-REC-X.1254)

[MTLS] - OAuth 2.0 Mutual TLS Client Authentication and Certificate Bound Access Tokens
[MTLS]: [https://tools.ietf.org/html/rfc8705](https://tools.ietf.org/html/rfc8705)

[RFC8414] - OAuth 2.0 Authorization Server Metadata
[RFC8414]: [https://tools.ietf.org/html/rfc8414](https://tools.ietf.org/html/rfc8414)

[OIDD] -  OpenID Connect Discovery 1.0 incorporating errata set 1
[OIDD]: [http://openid.net/specs/openid-connect-discovery-1_0.html](http://openid.net/specs/openid-connect-discovery-1_0.html)

## 3. 术语和定义

本规范而言，适用RFC6749、RFC6750、RFC7636、OpenID Connect Core中定义的术语。
> For the purpose of this document, the terms defined in [RFC6749], [RFC6750], [RFC7636], [OpenID Connect Core][OIDC] apply.


## 4. 缩略语

**API** – Application Programming Interface

**CSRF** - Cross Site Request Forgery

**FAPI** - Financial-grade API

**HTTP** – Hyper Text Transfer Protocol

**REST** – Representational State Transfer

**TLS** – Transport Layer Security

## 5. 只读API的安全总则

### 5.1 简介

OIDF定义的金融级API(FAPI)是一套提供JSON数据的REST API。这些API受OAuth 2.0授权框架的保护，该框架由[RFC6749]、[RFC6750]、[RFC7636]等规范组成。
> The OIDF Financial-grade API (FAPI) is a REST API that provides JSON data. These APIs are protected by the OAuth 2.0 Authorization Framework that consists of [RFC6749], [RFC6750], [RFC7636], and other specifications.


一般认为只读访问比写访问存在更低的安全风险，因此，对令牌的特性要求、获取方式也分开进行描述。
> Read-only access is generally viewed to pose a lower risk than the write access and as such, the characteristics required of the tokens are different and the methods to obtain tokens are explained separately.


### 5.2 只读API的安全规定

#### 5.2.1 简介

只读访问的安全风险比写访问更低，因此其安全保护级别也较低。
但考虑到FAPI可能提供潜在的敏感信息接口，因此它需要比基本的[RFC6749]更高的保护级别。
> Read-only access is a lower risk scenario compared to the write access; therefore the protection level can also be lower.
However, since the FAPI can provide potentially sensitive information, it requires more protection level than a basic [RFC6749] requires.

作为OAuth 2.0授权框架的配置实践，本文档对FAPI的只读API进行如下规定。
> As a profile of the OAuth 2.0 Authorization Framework, this document mandates the following to the read-only API of the FAPI.


#### 5.2.2 授权服务器

授权服务器

1. 应支持非公开的客户端；
1. 应该支持公开的客户端；
1. 如果使用基于对称密钥的验证方式(译者注：指client authentication中client_secret_jwt的模式)，应提供符合[OIDC]第16.19节要求的client secret；
1. 应使用下列方法之一对非公开客户端进行认证：
   1. 按照[MTLS]第2节描述的双向TLS，对OAuth客户端进行验证。
   1.  [OIDC]第9节中规定的client_secret_jwt或private_key_jwt。
5. 对RSA算法，应采用2048位或更大的密钥；
5. 对ECC算法，应采用160位或更大的密钥；
5. 应要求采用[RFC 7636](译者注：即PKCE)与S256作为code challenge的方法；
5. 重定向URI必须预先注册；
5. 授权请求中需要携带redirect_uri参数；
5. redirect_uri参数值必须与预先注册的重定向URI中的一个完全匹配；
5. 客户端代表用户进行数据访问前，需要用户进行认证，以授予其适当的访问范围；
5. 如果请求的作用域未被授权过，应要求用户明确的批准授权它；
5. 如果已经使用过某授权码([RFC6749]的1.3.1节)，则应拒绝再次使用；
5. 应返回符合[RFC6749]第4.1.4节的令牌响应；
5. 如果请求是从前端通道(译者注：不理解何为front channel)传入的，并且未受到完整性保护，则应返回已签发令牌相关联的授权域列表；
5. 应提供不透明的、不可被猜测的访问令牌、授权码和刷新令牌，应具备足够的熵，使攻击者猜测令牌的可能性在计算上不可行([RFC6749]第10.10节)；
5. 应按照[OIDC]第16.18条的规定，在授权过程中明确标明授予细节；以及
5. 应提供revoke机制，使最终用户能够按照[OIDC]第16.18条的规定，撤销授予客户端的访问令牌和刷新令牌；
5. 当进行客户端认证(多种客户端认证方式，如shared secret & jwt)时提供了不匹配的客户端标识符时，应返回[RFC6749]5.2中定义的invalid_client错误；
5. 应要求重定向URI使用https；
5. 应签发生命周期在10分钟以下的访问令牌，除非该令牌受发行人约束(译者注：不理解)；
5. 应支持[OIDD](译者注：OpenID Connect Discovery)，也可支持[RFC 8414](译者注：Authorization Server Metadata)；
5. 应仅通过[OIDD]和[RFC 8414]中规定的元数据文档来分发元数据(如授权端点)；
   - NOTE：要求使用刷新令牌来替代长时效的令牌，对公共或非公共客户端都适用；
   - NOTE：金融级API可以通过限制scope，来达到不实现某些API的目的；
   - NOTE：返回已授权的scope的列表，允许客户端检查何时授权请求被修改为包含不同的scope。当请求的scope与已授权的scope不同时，服务器仍然必须返回已授权的scope的列表；

> The authorization server
> 
> 1. shall support confidential clients;
> 1. should support public clients;
> 1. shall provide a client secret that adheres to the requirements in section 16.19 of [OIDC] if a symmetric key is used;
> 1. shall authenticate the confidential client using one of the following methods:
a. Mutual TLS for OAuth Client Authentication as specified in section 2 of [MTLS];
b. client_secret_jwt or private_key_jwt as specified in section 9 of [OIDC];
> 1. shall require and use a key of size 2048 bits or larger for RSA algorithms;
> 1. shall require and use a key of size 160 bits or larger for elliptic curve algorithms;
> 1. shall require [RFC7636] with S256 as the code challenge method;
> 1. shall require redirect URIs to be pre-registered;
> 1. shall require the redirect_uri parameter in the authorization request;
> 1. shall require the value of redirect_uri to exactly match one of the pre-registered redirect URIs;
> 1. shall require user authentication to an appropriate Level of Assurance for the operations the client will be authorized to perform on behalf of the user;
> 1. shall require explicit approval by the user to authorize the requested scope if it has not been previously authorized;
> 1. shall reject an authorization code (section 1.3.1 of [RFC6749]) if it has been previously used;
> 1. shall return token responses that conform to section 4.1.4 of [RFC6749];
> 1. shall return the list of granted scopes with the issued access token if the request was passed in the front channel and was not integrity protected;
> 1. shall provide opaque non-guessable access tokens, authorization codes, and refresh token
(where applicable), with sufficient entropy such that the probability of an attacker guessing
the generated token is computationally infeasible as per [RFC6749] section 10.10;
> 1. should clearly identify the details of the grant to the user during authorization as in 16.18 of [OIDC]; and
> 1. should provide a mechanism for the end-user to revoke access tokens and refresh tokens granted to a client as in 16.18 of [OIDC].
> 1. shall return an invalid_client error as defined in 5.2 of [RFC6749] when mis-matched client identifiers were provided through the client authentication methods that permits sending the client identifier in more than one way;
> 1. shall require redirect URIs to use the https scheme;
> 1. should issue access tokens with a lifetime of under 10 minutes unless the tokens are sender-constrained;
> 1. shall support [OIDD] and may support [RFC8414];
> 1. shall only distribute discovery metadata (such as the authorization endpoint) via the metadata document as specified in [OIDD] and [RFC8414].
NOTE: The use of refresh tokens instead of long-lived access tokens for both
public and confidential clients is recommended.
NOTE: The Financial-grade API server may limit the scopes for the purpose of not implementing certain APIs.
NOTE: The opaqueness requirement for the access token does not preclude the server to create a structured access token.
NOTE: The requirement to return the list of granted scopes allows clients to detect when the authorization request was modified to include different scopes. Servers must still return the granted scopes if they are different from those requested.


##### 5.2.2.1 返回已认证用户的标识

此外，如果希望在令牌响应中向客户端提供用户的标识符，则：

1. 应按照[OIDC]第3.1.2.1节的规定支持认证请求；
1. 应按照[OIDC]第3.1.2.2节的规定进行认证请求验证；
1. 应按照[OIDC]第3.1.2.2和3.1.2.3节的规定对用户进行认证；
1. 应按照[OIDC]第3.1.2.4节和3.1.2.5节所述，根据认证结果返回认证响应；
1. 应按照[OIDC]第3.1.3.2节执行令牌请求验证；以及
1. 当openid包含在请求的scope中时，如[OIDC]第3.1.3.3节所述，应在令牌响应中发出一个ID Token，其sub值对应经过认证的用户，并包含可选的acr值；

> Further, if it is desired to provide the authenticated user's identifier to the client in the token response, the authorization server:
> 1. shall support the authentication request as in Section 3.1.2.1 of [OIDC];
> 1. shall perform the authentication request verification as in Section 3.1.2.2 of [OIDC];
> 1. shall authenticate the user as in Section 3.1.2.2 and 3.1.2.3 of [OIDC];
> 1. shall provide the authentication response as in Section 3.1.2.4 and 3.1.2.5 of [OIDC] depending on the outcome of the authentication;
> 1. shall perform the token request verification as in Section 3.1.3.2 of [OIDC]; and
> 1. shall issue an ID Token in the token response when `openid` was included in the requested `scope`
as in Section 3.1.3.3 of [OIDC] with its `sub` value corresponding to the authenticated user
and optional `acr` value in ID Token.



##### 5.2.2.2 客户端请求openid域

如果客户端请求openid域，则授权服务器：

1. 应在认证请求中要求使用[OIDC]第3.1.2.1节中定义的nonce参数；

> If the client requests the openid scope, the authorization server
> 1. shall require the `nonce` parameter defined in Section 3.1.2.1 of [OIDC] in the authentication request.


##### 5.2.2.3 客户端未请求openid域

如果客户端未请求openid域，则授权服务器：

1. 应在请求中要求使用[RFC6749]第4.1.1节中定义的state参数；

> If the client does not requests the openid scope, the authorization server
> 1. shall require the `state` parameter defined in section 4.1.1 of [RFC6749].


#### 5.2.3 公开客户端

公开客户端

1. 应支持[RFC7636]；
1. 应使用S256作为[RFC7636]的code challenge方法；
1. 应对其产生交互的所有授权服务器都使用独立且不同的重定向URI；
1. 应将重定向URI的值存储在资源所有者的user-agents(如浏览器)会话中，并与收到授权响应的重定向URI进行对比，如果不匹配，客户端应以错误终止进程；
1. (已撤回)；
1. 应实现有效的CSRF防护，此外，如果希望获得已认证用户的持久性标识，则：
1. 应在scope中包含openid值，并且
1. 应在认证请求中包含[OIDC]第3.1.2.1节中定义的nonce参数，如果scope中不包含openid值，则：
1. 应包含 [RFC6749]第4.1.1节中定义的state参数；
1. 应验证令牌响应中收到的scope是否完全匹配，或者时认证请求中发送的scope的子集；
1. 应仅使用授权服务器在其well known端点发布的元数据，如[OIDD]or[RFC8414]所定义。
   - NOTE：遵守[RFC7636]意味着令牌请求中包含code_verifier参数；

> A public client
> - shall support [RFC7636];
> - shall use `S256` as the code challenge method for the [RFC7636];
> - shall use separate and distinct redirect URI for each authorization server that it talks to;
> - shall store the redirect URI value in the resource owner's user-agents (such as browser) session and compare it with the redirect URI that the authorization response was received at, where, if the URIs do not match, the client shall terminate the process with error;
> - (withdrawn);
> - shall implement an effective CSRF protection.
Further, if it is desired to obtain a persistent identifier of the authenticated user, then it
> - shall include `openid` in the `scope` value; and
> - shall include the `nonce` parameter defined in Section 3.1.2.1 of [OIDC] in the authentication request.
If `openid` is not in the `scope` value, then it
> - shall include the `state` parameter defined in section 4.1.1 of [RFC6749];
> - shall verify that the `scope` received in the token response is either an exact match,
or contains a subset of the `scope` sent in the authorization request;
> - shall only use Authorization Server metadata obtained from the metadata document published by the Authorization Server at its well known endpoint as defined in [OIDD] or [RFC8414].
**NOTE**: Adherence to [RFC7636] means that the token request includes `code_verifier` parameter in the request.


#### 5.2.4 非公开客户端

除对公开客户端的规定外，非公开客户端还需：

1. 应支持以下方法对令牌端点进行认证：
   1. 采用[MTLS]第2节规定的双向TLS进行OAuth客户端认证；
   1.  [OIDC]第9节中规定的client_secret_jwt或private_key_jwt；
2. 如果使用RSA加密方案，应使用最小2048位的RSA密钥；
2. 如果使用ECC加密方案，应使用至少160位的ECC密钥；以及
2. 如果使用对称密钥加密方案，应验证其client secret至少有128位；

> In addition to the provisions for a public client, a confidential client
> 1. shall support the following methods to authenticate against the token endpoint:
a. Mutual TLS for OAuth Client Authentication as specified in section 2 of [MTLS];
b. client_secret_jwt or private_key_jwt as specified in section 9 of [OIDC];
> 1. shall use RSA keys with a minimum 2048 bits if using RSA cryptography;
> 1. shall use elliptic curve keys with a minimum of 160 bits if using Elliptic Curve cryptography; and
> 1. shall verify that its client secret has a minimum of 128 bits if using symmetric key cryptography.


## 6. 访问受保护的资源

### 6.1 简介

FAPI的端点是受OAuth 2.0保护的资源端点，可返回所提交的访问令牌关联的资源所有者的受保护信息。
> The FAPI endpoints are OAuth 2.0 protected resource endpoints that return protected information for the resource owner associated with the submitted access token.


### 6.2 只读数据访问规范

#### 6.2.1 受保护资源的规定

包含FAPI端点的资源服务器：

1. 应支持使用[RFC7231]第4.3.1节中的HTTP GET方法；
1. 应按照[RFC6750]第2.1节的规定，在HTTP请求头中接受访问令牌；
1. 应按照[RFC6750]第2.3节的规定，不得接受在查询参数中的访问令牌；
1. 应校验访问令牌既未过期也未被撤销；
1. 应验证与访问令牌关联的scope是否授权读取当前资源；
1. 应识别访问令牌关联的实体；
1. 应只返回由访问中隐含的实体和授权范围共同标识的资源，否则应按照[RFC6750]的3.1节返回错误；
1. 如果适用，响应应采用UTF-8进行编码；
1. 如果适用，应发送Content-Type:application/json的HTTP请求头；
1. 应按照[RFC7231]第7.1.1.2节的规定，在HTTP Date头中发送服务器日期；
1. 应将x-fapi-interaction-id响应头设置未从FAPI客户端请求中接收到的值，如果请求中未携带该值来提供跟踪交互，则设置为[RFC4122]UUID值，例如，x-fapi-interaction-id：c770aef3-6784-41f7-8e0e-ff5f97bddb3a；以及：
1. 应在日志中记录x-fapi-interaction-id的值；
1. 不应该拒绝包含x-fapi-customer-ip-address请求头的请求，该头包含一个有效的IPv4或IPv6的地址；
   - NOTE：虽然本文档没有明确说明获取与访问令牌和授权范围相关联的实体的具体方法，受保护资源可以参考使用OAuth Token Introspection [RFC7662]；
14. 如果决定向基于JavaScript的客户端提供访问权限，需要支持跨域资源访问(CORS)或其它适当的方法；
   - NOTE：提供对JavaScript客户端的支持将带来其它的安全挑战，在支持这些客户端之前，请参考[RFC6819]；

> The resource server with the FAPI endpoints
> 1. shall support the use of the HTTP GET method as in Section 4.3.1 of [RFC7231];
> 1. shall accept access tokens in the HTTP header as in Section 2.1 of OAuth 2.0 Bearer Token Usage [RFC6750];
> 1. shall not accept access tokens in the query parameters stated in Section 2.3 of OAuth 2.0 Bearer Token Usage [RFC6750];
> 1. shall verify that the access token is neither expired nor revoked;
> 1. shall verify that the scope associated with the access token authorizes the reading of the resource it is representing;
> 1. shall identify the associated entity to the access token;
> 1. shall only return the resource identified by the combination of the entity implicit in the access and the granted scope and otherwise return errors as in section 3.1 of [RFC6750];
> 1. shall encode the response in UTF-8 if applicable;
> 1. shall send the `Content-type` HTTP header `Content-Type: application/json` if applicable;
> 1. shall send the server date in HTTP Date header as in section 7.1.1.2 of [RFC7231];
> 1. shall set the response header `x-fapi-interaction-id` to the value received from the corresponding fapi client request header or to a [RFC4122] UUID value if the request header was not provided to track the interaction, e.g., `x-fapi-interaction-id: c770aef3-6784-41f7-8e0e-ff5f97bddb3a`; and
> 1. shall log the value of `x-fapi-interaction-id` in the log entry;
> 1. shall not reject requests with a `x-fapi-customer-ip-address` header containing a
valid IPv4 or IPv6 address.
**NOTE**: While this document does not specify the exact method to obtain the entity associated with the
access token and the granted scope, the protected resource can use OAuth Token Introspection [RFC7662].
Further, it
> 1. should support the use of Cross Origin Resource Sharing (CORS) [CORS] and or other methods as appropriate to enable JavaScript clients to access the endpoint if it decides to provide access to JavaScript clients.
**NOTE**: Providing access to JavaScript clients has other security implications. Before supporting those clients [RFC6819] should be consulted.


#### 6.2.2 客户端规定

支持本文档的客户端应具备如下能力：

1. 应按照OAuth 2.0 Bearer Token Usage [RFC6750]第2.1节的规定，在HTTP请求头中发送访问令牌，并且
1. (已撤回)；
1. 可以在x-fapi-auth-date中发送最终用户最后一次登录客户端的时间，其中的值是[RFC7231]第7.1.1.1节中的HTTP-date来提供的，例如，x-fapi-auth-date: Tue, 11 Sep 2012 19:43:31 GMT；以及
1. 如果x-fapi-customer-ip-address中存在有效数据，则可以发送客户的IP地址。例如，x-fapi-customer-ip-address: 2001:DB8::1893:25c8:1946或x-fapi-customer-ip-address: 198.51.100.119；以及
1. 可以发送x-fapi-interaction-id请求头，值应该满足RFC4122 UUID约束，通过该头帮助客户端和服务器之间进行日志的关联，例如：x-fapi-interaction-id: c770aef3-6784-41f7-8e0e-ff5f97bddb3a；

> The client supporting this document
> 1. shall send access tokens in the HTTP header as in Section 2.1 of OAuth 2.0 Bearer Token Usage [RFC6750]; and
> 1. (withdrawn);
Further, the client
> 1. may send the last time the customer logged into the client in the x-fapi-auth-date header where the value is supplied as a HTTP-date as in section 7.1.1.1 of [RFC7231], e.g., x-fapi-auth-date: Tue, 11 Sep 2012 19:43:31 GMT; and
> 1. may send the customer’s IP address if this data is available in the x-fapi-customer-ip-address header, e.g., x-fapi-customer-ip-address: 2001:DB8::1893:25c8:1946 or  x-fapi-customer-ip-address: 198.51.100.119; and
> 1. may send the x-fapi-interaction-id request header, in which case the value shall be a
RFC4122 UUID to the server to help correlate log entries between client and server,
e.g., x-fapi-interaction-id: c770aef3-6784-41f7-8e0e-ff5f97bddb3a.


## 7. 安全考量

### 7.1 TLS和DNSSEC注意事项

由于正在交换隐私数据，因此所有的网络交互都应使用TLS加密(HTTPS)。
> As confidential information is being exchanged, all interactions shall be encrypted with TLS (HTTPS).


应遵循[BCP195]中关于安全使用TLS的建议，并附加以下要求：

1. 所有通信都应基于TSL 1.2或更高版本；
1. 根据[RFC6125]，应进行TLS服务器证书检查；

> The recommendations for Secure Use of Transport Layer Security in [BCP195] shall be followed, with the following additional requirements:
> - TLS version 1.2 or later shall be used for all communications.
> - A TLS server certificate check shall be performed, as per [RFC6125].


供web浏览器使用的端点应该提供机制来抵御TLS Stripping(HTTPS降级)攻击，可以使用预加载HTTP Strict Transport Security策略来达到这个目的[RFC6797]。一些顶级域名，如.bank和.insurance，已经设置了这样的策略，因此可以保护所有低于他们的二级域名。
> Endpoints for the use by web browsers should use mechanisms to ensure that connections cannot be downgraded using TLS Stripping attacks. A preloaded [preload] HTTP Strict Transport Security policy [RFC6797] can be used for this purpose. Some top-level domains, like `.bank` and `.insurance`, have set such a policy and therefore protect all second-level domains below them.


为了全面防范网络攻击，所有端点都应额外使用DNSSEC，以防止DNS欺诈，避免导致下发非法的TLS证书。
NOTE：即使端点使用的是OV或EV级别的TLS证书，非法的TLS证书仍然会导致端点冒用，以至出现中间人攻击。
> For a comprehensive protection against network attackers, all
> endpoints should additionally use DNSSEC to protect against DNS
> spoofing attacks that can lead to the issuance of rogue
> domain-validated TLS certificates. Note: Even if an endpoint uses only
> organization validated (OV) or extended validation (EV) TLS
> certificates, rogue domain-validated certificates can be used to
> impersonate the endpoints and conduct man-in-the-middle attacks.


### 7.2 消息源验证失败

授权请求或响应没有经过认证。
对于风险较高的场景，应该对它们进行认证。
参见第2部分，使用request object实现消息源认证。

> Authorization request and response are not authenticated.
> For higher risk scenarios, they should be authenticated.
> See Part 2, which uses request objects to achieve the message source authentication.


### 7.3 消息完整性验证失败

授权请求没有经过消息完整性保护，则可能出现被篡改和参数注入的情况。
如果需要这类保护，参考第2部分。

> The authorization request does not have message integrity protection and hence
> request tampering and parameter injection are possible.
> Where such protection is desired, Part 2 should be used.


授权端点返回ID Token时，消息响应则受完整性保护。
> The response is integrity protected when the ID Token is returned
> from the authorization endpoint.


### 7.4 消息遏制失败(信息泄露问题)

#### 7.4.1 授权请求和响应

在该文档中，授权请求未进行加密，当浏览器被入侵时，则可能导致信息泄露。
> In this document, the authorization request is not encrypted.
> Thus, it is possible to leak the information contained
> if the web browser is compromised.


授权响应可以和ID Token采取相同的加密策略。
> Authorization response can be encrypted as ID Token
> can be encrypted.


如果日志中记录了参数，且日志的访问权出现问题，则可能通过日志泄露信息。这种情况下应该严格控制日志的访问。
> It is possible to leak the information through the logs
> if the parameters were recorded in the logs and
> the access to the logs are compromised.
> Strict access control to the logs in such cases should be
> enforced.


#### 7.4.2 Token请求和响应

如果日志中记录了参数，且日志的访问权出现问题，则可能通过日志泄露信息。这种情况下应该严格控制日志的访问。
> It is possible to leak information through the logs
> if the parameters were recorded in the logs and
> the access to the logs are compromised.
> Strict access control to the logs in such cases should be
> enforced.


#### 7.4.3 资源请求和响应

应谨慎处理，以避免敏感数据通过关联方外泄。
> Care should be taken so that the sensitive data will not be leaked
> through the referrer.


如果访问令牌是不记名令牌，则可能出现令牌泄露的问题。由于访问令牌在多个URI端点使用，因此其泄露的可能性比刷新令牌大很多，因为刷新令牌仅在Token端点使用。关于访问令牌的和刷新令牌的寿命，参阅[OIDC]第16.18节。
> If the access token is a bearer token, it is possible to
> exercise the stolen token. Since the access token can be
> used against multiple URIs, the risk of leaking is
> much larger than the refresh token, which is used only
> against the token endpoint. Thus, the lifetime of
> the access token should be much shorter than that of
> the refresh token. Refer to section 16.18 of [OIDC] for
> more discussion on the lifetimes of access tokens and
> refresh tokens.


### 7.5 本地应用

当本地应用作为公共客户端、动态注册的非公共客户端，或者是为基于服务器的非公开客户端用于接收授权响应的用户代理，应遵循OAuth 2.0 for Native Apps [BCP212]。并附加如下要求：
> When native apps are used as either public clients, dynamically registered confidential clients or user-agents receiving the authorization response for a server based confidential client, the recommendations for OAuth 2.0 for Native Apps in [BCP212] shall be followed, with the following additional requirements:


当注册重定向URI时，授权服务器：

1. 不支持 "Private-Use URI Scheme Redirection"；
1. 不支持 "Loopback Interface Redirection"；

> When registering redirect URIs, authorization servers
> 1. shall not support "Private-Use URI Scheme Redirection";
> 1. shall not support "Loopback Interface Redirection";


这些要求意味着符合FAPI的实现只能通过使用"Claimed https Scheme URI Redirection"来支持本地应用。
> These requirements mean that FAPI compliant implementations can only
> support native apps through the use of "Claimed https Scheme URI Redirection".


NOTE：本文档没有禁止使用类似[https://localhost](https://localhost):port-number/callback这种固定URL的形式，因为这些URL在非生产系统或开发环境中特别有用，便于更快更方便的开发。
> Note: nothing in this document seeks to disallow fixed urls in the
> form [https://localhost](https://localhost):port-number/callback, as these are particularly
> useful in non-production systems or in clients used in development, to
> facilitate faster and easier development.


### 7.6 对规范不完整或错误的实现

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


### 7.7 发现&多品牌

需要在单一授权服务器的单一授权端点支持多"品牌"的组织，应为每个"品牌"使用独立的issure。这可以在域名级别(如：[https://brand-a.auth.example.com](https://brand-a.auth.example.com) 和 [https://brand-b.auth.example.com](https://brand-b.auth.example.com))或者通过不同的path(如：[https://auth.example.com/brand-a](https://auth.example.com/brand-a) 和 [https://auth.example.com/brand-b](https://auth.example.com/brand-b))实现。
> Organisations who need to support multiple "brands" with individual authorization endpoints
> from a single Authorization Server deployment shall use a separate `issuer` per brand.
> This can be achieved either at the domain level (e.g. `[https://brand-a.auth.example.com](https://brand-a.auth.example.com)`
> and  `[https://brand-b.auth.example.com](https://brand-b.auth.example.com)`) or with different paths (e.g. `[https://auth.example.com/brand-a](https://auth.example.com/brand-a)` and `[https://auth.example.com/brand-b](https://auth.example.com/brand-b)`)


如5.2.10中所述，客户端应仅使用通过[OIDD]中定义的元数据文件获得元数据值。通过其他方式(如通过电子邮件)传递元数据，可能会成为社会工程学的攻击向量。
> As stated in 5.2.10 Clients shall only use metadata values obtained via metadata documents
> as defined in [OIDD]. Communicating metadata through other means (e.g. via email), opens
> up a social engineering attack vector.


请注意，使用[OIDD]的要求不是支持动态客户端注册的要求。
> Note that the requirement to use [OIDD] is not a requirement to support Dynamic Client
> Registration.


## 8. 隐私考量

```
** NOTE ** The following only has a boilerplate text 
specifying the general principles. More specific text 
will be added towards the Final specification.
```

### 8.1 设计阶段的隐私考量

1. 应在系统设计的初始阶段进行隐私影响分析(PIA)。
1. 建议使用ISO/IEC 29134:2017隐私影响分析指南。
1. 供应商应建立管理体系，以协助尊重客户的隐私。

> 1. Privacy impact analysis (PIA) should be performed in the initial phase of the system planning.
> 1. Use of ISO/IEC 29134:2017 Guidelines for privacy impact analysis is recommended.
> 1. The provider should establish a management system to help respect privacy of customers.


### 8.2 遵循隐私原则

利益相关者应遵循ISO/IEC 29100的隐私原则。尤其是：

1. 同意和选择
1. 目的的合法性和规范性
1. 限制采集
1. 数据访问限制
1. 数据的使用、保留和披露限制
   1. 使用限制
   1. 保留限制：当数据不再使用，客户端应该在180天内从其系统中删除这些数据，但因法律限制而需要保留的情况除外
   1. 数据披露限制、
6. 准确性和质量
6. 公开性、透明度和通知
6. 个体参与和访问(译者注：不理解)
6. 问责制
6. 信息安全
6. 隐私条款


> Stakeholders should follow the privacy principles of ISO/IEC 29100. In particular:
> 1. Consent and choice
> 1. Purpose legitimacy and specification
> 1. Collection limitation
> 1. Data (access) limitation
> 1. Use, retention, and data disclosure limitation:
a. Use limitation:
b. Retention limitation: Where the data is no longer being used, clients should delete such data from their system within 180 days except for the cases where it needs to be retained due to legal restrictions;
c. Data disclosure limitation:
> 1. Accuracy and quality
> 1. Openness, transparency and notice
> 1. Individual participation and access
> 1. Accountability
> 1. Information security
> 1. Privacy compliance


1. 


## 9. 致谢

以下人员对本文档做出贡献：
> The following people contributed to this document:


- Nat Sakimura (Nomura Research Institute) -- Chair, Editor
- Anoop Saxana (Intuit) -- Co-chair, FS-ISAC Liaison
- Anthony Nadalin (Microsoft) -- Co-chair
- Edmund Jay (Illumila) -- Co-editor
- Dave Tonge (Moneyhub) -- Co-chair, UK Implementation Entity Liaison
- Sascha H. Preibisch (CA)
- Henrik Biering (Peercraft)
- Anton Taborszky (Deutsche Telecom)
- John Bradley (Yubico)
- Axel Nennker (Deutsche Telekom)
- Joseph Heenan (Authlete)
- Daniel Fett (yes.com)

## 10. 参考文献

- [ISODIR2] ISO/IEC Directives Part 2
- [RFC4122] A Universally Unique IDentifier (UUID) URN Namespace
- [RFC6749] The OAuth 2.0 Authorization Framework
- [RFC6750] The OAuth 2.0 Authorization Framework: Bearer Token Usage
- [RFC6797] HTTP Strict Transport Security (HSTS)
- [RFC7636] Proof Key for Code Exchange by OAuth Public Clients
- [RFC7662] OAuth 2.0 Token Introspection
- [RFC6125] Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security (TLS)
- [BCP212] OAuth 2.0 for Native Apps
- [RFC6819] OAuth 2.0 Threat Model and Security Considerations
- [RFC8414] OAuth 2.0 Authorization Server Metadata
- [OIDD] OpenID Connect Discovery 1.0 incorporating errata set 1
- [BCP195] Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS)
- [OIDC] OpenID Connect Core 1.0 incorporating errata set 1
- [X.1254] Entity authentication assurance framework
- [MTLS] OAuth 2.0 Mutual TLS Client Authentication and Certificate Bound Access Tokens
- [ISO29100] ISO/IEC 29100 Information technology -- Security techniques -- Privacy framework [http://standards.iso.org/ittf/PubliclyAvailableStandards/c045123_ISO_IEC_29100_2011.zip](http://standards.iso.org/ittf/PubliclyAvailableStandards/c045123_ISO_IEC_29100_2011.zip)
- [ISO29134] ISO/IEC 29134 Information technology -- Security techniques -- Privacy impact assessment -- Guidelines
- [preload] HSTS Preload List Submission [https://hstspreload.org/](https://hstspreload.org/)
