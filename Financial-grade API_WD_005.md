# Financial Services – Financial-grade API - Part 5: Protected Data API and Schema - Read and Write

## 警告

该文档不是OIDF(OpenID Foundation)的国际标准，公布该规范的目的是供大家审阅与评价。因此如果该规范出现变更，恕不另行通知，并且也不允许称其为国际标准。
> This document is not an OIDF International Standard. It is distributed for review and comment. It is subject to change without notice and may not be referred to as an International Standard.


我们邀请本草案的接受者提出意见，并且如果觉察到我们存在侵犯相关专利的情况，请告知我们并提供相关的证明材料。
> Recipients of this draft are invited to submit, with their comments, notification of any relevant patent rights of which they are aware and to provide supporting documentation.


## 版权声明和许可

对任何贡献者、开发者、实现者或其他有兴趣的相关方，OpenID基金会(OIDF)都授以非独占性、免版税以及全球范围内的版权许可，可用以复制、衍生、分发、实践或展示该规范。
本草案或最终规范仅用于以下目的：

1. 进一步完善规范；
1. 根据此类文件实践本草案或最终规范；

必须注明资料来源为OIDF，但该类注明并不表示获得OIDF的背书。
> The OpenID Foundation (OIDF) grants to any Contributor, developer, implementer, or other interested party a non-exclusive, royalty free, worldwide copyright license to reproduce, prepare derivative works from, distribute, perform and display, this Implementers Draft or Final Specification solely for the purposes of (i) developing specifications, and (ii) implementing Implementers Drafts and Final Specifications based on such documents, provided that attribution be made to the OIDF as the source of the material, but that such attribution does not indicate an endorsement by the OIDF.


该规范中描述的技术由多个来源方贡献，其中包含OpenID基金会或其他第三方。虽然OpenID基金会已经采取一些步骤以保障这些技术的可用性，但对于与本文档中所描述的技术实现或使用有关的任何知识产权问题，基金会不持任何立场。OpenID基金会和本规范的贡献者不做(并在此明确声明不做任何) 保证(明示、暗示或其他)，包括与本规范相关的可销售性、非侵权性、对特定用途的适用性或所有权的保证，实现本规范的全部风险由实现者承担。OpenID知识产权策略要求贡献者提供专利承诺，不对其他贡献者和实现者提出某些专利要求。OpenID 基金会期望任何有兴趣的相关方，需要注意在实践该规范时用到的技术可能涉及到的任何版权、专利、专利申请问题。
> The technology described in this specification was made available from contributions from various sources, including members of the OpenID Foundation and others. Although the OpenID Foundation has taken steps to help ensure that the technology is available for distribution, it takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the implementation or use of the technology described in this specification or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any independent effort to identify any such rights. The OpenID Foundation and the contributors to this specification make no (and hereby expressly disclaim any) warranties (express, implied, or otherwise), including implied warranties of merchantability, non-infringement, fitness for a particular purpose, or title, related to this specification, and the entire risk as to implementing this specification is assumed by the implementer. The OpenID Intellectual Property Rights policy requires contributors to offer a patent promise not to assert certain patent claims against other contributors and against implementers. The OpenID Foundation invites any interested party to bring to its attention any copyrights, patents, patent applications, or other proprietary rights that may cover technology that may be required to practice this specification.


## 序言

OIDF (OpenID Foundation)是一个国际化标准机构，由160多个参与实体组成。编制国际标准的工作是OIDF工作组根据OpenID Process进行的，对已成立工作组感兴趣的参与方都有权利加入工作组。国际组织，包括政府和非政府组织，在与OIDF的联络下，也参与到该工作中来，OIDF与相关领域的其他标准化机构保持紧密合作关系。
> The OpenID Foundation (OIDF) promotes, protects and nurtures the OpenID community and technologies. As a non-profit international standardizing body, it is comprised by over 160 participating entities (workgroup participants). The work of preparing implementer drafts and final international standards is carried out through OIDF workgroups in accordance with the OpenID Process. Participants interested in a subject for which a workgroup has been established has the right to be represented in that workgroup. International organizations, governmental and non-governmental, in liaison with OIDF, also take part in the work. OIDF collaborates closely with other standardizing bodies in the related fields.


OpenID基金会的标准是根据OpenID Process中给出的规则起草的。
> OpenID Foundation standards are drafted in accordance with the rules given in the OpenID Process.


工作组的主要任务是起草实施者草案以及最终草案。最终草案需要公开发布，供公众审查60天，也供OIDF成员进行表决，至少需要50%以上的成员批准才能作为OIDF标准发布。
> The main task of work group is to prepare Implementers Draft and Final Draft. Final Draft adopted by the Work Group through consensus are circulated publicly for the public review for 60 days and for the OIDF members for voting. Publication as an OIDF Standard requires approval by at least 50 % of the members casting a vote.


请注意，该文档的某些内容可能涉及专利权相关问题，OIDF对识别此类专利权不负任何责任。
> Attention is drawn to the possibility that some of the elements of this document may be the subject of patent rights. OIDF shall not be held responsible for identifying any or all such patent rights.


Financial API - Part 4: Protected Data API and Schema - Read only was prepared by OpenID Foundation Financial API Work Group.

Financial API由以下几个部分组成，其父标题为Financial Services — Financial API:

- 1：只读操作相关接口的安全总则
- 2：读写操作相关接口的安全总则
- 3：开放数据接口
- 4：受保护数据的API和结构 - 只读
- 5：受保护数据的API和结构 - 读写

> Financial API consists of the following parts, under the general title Financial Services — Financial API:
> - Part 1: Read Only API Security Profile
> - Part 2: Read and Write API Security Profile
> - Part 3: Open Data API
> - Part 4: Protected Data API and Schema - Read only
> - Part 5: Protected Data API and Schema - Read and Write


本部分旨在与[RFC6749]、[RFC6750]、[RFC7636]和[OIDC]配合使用。
> This part is intended to be used with [RFC6749], [RFC6750], [RFC7636], and [OIDC].


## 简介

在很多情况下，聚合服务等金融科技服务都会使用"screen craping"和存储用户密码的方式，这种模式既脆弱又不安全。为应对脆弱性，应使用结构化数据的API模型，而为应对安全性，则应该利用OAuth[RFC6749，RFC6750]等token模型。
> In many cases, Fintech services such as aggregation services uses screen scraping and stores user passwords. This model is both brittle and insecure. To cope with the brittleness, it should utilize an API model with structured data and to cope with insecurity, it should utilize a token model such as OAuth [RFC6749, RFC6750].


该工作组旨在通过开发一个受OAuth保护的REST/JSON模型来改善这种情况，具体来说，FAPI WG旨在提供JSON数据结构、安全和隐私要求以及协议，以便：

- 使应用程序能够使用金融账户的数据；
- 使应用程序能够与金融账户交互，并且
- 使用户能控制安全和隐私设置；

> This working group aims to rectify the situation by developing a REST/JSON model protected by OAuth. Specifically, the FAPI WG aims to provide JSON data schemas, security and privacy recommendations and protocols to:
> - enable applications to utilize the data stored in the financial account,
> - enable applications to interact with the financial account, and
> - enable users to control the security and privacy settings.


既要考虑商业和投资银行账户，也要考虑保险、信用卡账户。
> Both commercial and investment banking accounts as well as insurance, and credit card accounts are to be considered.


# Financial Services – Financial API - Part 5: Protected Data API and Schema - Read and Write 

[TOC]

## 1. 范围

本文档声明了如下方法：

- 应用以适当的方式获取OAuth令牌，用户金融数据的访问；
- 应用程序利用OpenID Connect来识别客户；
- 以JSON格式来传递金融数据；
- 使用令牌与提供金融数据的REST端点交互；以及
- 使用户能够控制安全和隐私设置；

> This document specifies the method of
> - applications to obtain the OAuth tokens in an appropriately secure manner for the financial data access;
> - application to utilize OpenID Connect to identify the customer;
> - representing financial data in JSON format;
> - using the tokens to interact with the REST endpoints that provides financial data; and
> - enabling users to control the security and privacy settings.


本文档既适用于商业和投资银行账户，也适用于保险和信用卡账户。
> This document is applicable to both commercial and investment banking accounts as well as insurance, and credit card accounts are to be considered.


## 2. 参考文档

对本规范的实际应用而言，以下的参考规范必不可少。对标注日期的参考规范，仅引用的版本适用，而未标注日期的文档，其最新版本(包括所有修订)也适用本规范。
> The following referenced documents are indispensable for the application of this document. For dated references, only the edition cited applied. For undated references, the latest edition of the referenced document (including any amendments) applies.


[RFC7230] -  Hypertext Transfer Protocol -- HTTP/1.1
[RFC7230]: [https://tools.ietf.org/html/rfc7230](https://tools.ietf.org/html/rfc7230)

[RFC6749] - The OAuth 2.0 Authorization Framework
[RFC6749]: [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749)

[RFC6750] - The OAuth 2.0 Authorization Framework: Bearer Token Usage
[RFC6750]: [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)

[RFC7636] - Proof Key for Code Exchange by OAuth Public Clients
[RFC7636]: [https://tools.ietf.org/html/rfc7636](https://tools.ietf.org/html/rfc7636)

[RFC5246] - The Transport Layer Security (TLS) Protocol Version 1.2
[RFC5246]: [https://tools.ietf.org/html/rfc5246](https://tools.ietf.org/html/rfc5246)

[RFC7525] - Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS)
[RFC7525]: [https://tools.ietf.org/html/rfc7525](https://tools.ietf.org/html/rfc7525)

[RFC6125] - Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security (TLS)
[RFC6125]: [https://tools.ietf.org/html/rfc6125](https://tools.ietf.org/html/rfc6125)

BCP NAPPS - [OAuth 2.0 for Native Apps](https://tools.ietf.org/html/draft-ietf-oauth-native-apps-03)

[OIDC] - OpenID Connect Core 1.0 incorporating errata set 1
[OIDC]: [http://openid.net/specs/openid-connect-core-1_0.html](http://openid.net/specs/openid-connect-core-1_0.html)

[OIDD] -  OpenID Connect Discovery 1.0 incorporating errata set 1
[OIDD]: [http://openid.net/specs/openid-connect-discovery-1_0.html](http://openid.net/specs/openid-connect-discovery-1_0.html)

[OIDM] -  OAuth 2.0 Multiple Response Type Encoding Practices
[OIDM]: [http://openid.net/specs/oauth-v2-multiple-response-types-1_0.html](http://openid.net/specs/oauth-v2-multiple-response-types-1_0.html)

[X.1254] - Entity authentication assurance framework
[X.1254]: [https://www.itu.int/rec/T-REC-X.1254](https://www.itu.int/rec/T-REC-X.1254)

## 3. 术语和定义

本规范而言，适用RFC6749、RFC6750、RFC7636、OpenID Connect Core中定义的术语。
> For the purpose of this standard, the terms defined in [RFC6749], [RFC6750], [RFC7636], [OpenID Connect Core][OIDC] apply.

## 4. 缩略语

**API** – Application Programming Interface

**CSRF** - Cross Site Request Forgery

**FAPI** - Financial API

**FI** – Financial Institution

**HTTP** – Hyper Text Transfer Protocol

**REST** – Representational State Transfer

**TLS** – Transport Layer Security

## 5.资源APIs

### 5.1 简介

FAPI文档定义了两种资源类型：

- 开放访问的资源；
- 受保护的资源；

> Financial API document specifies resources in two categories:
> - open access resources;
> - protected resources;


开放访问的资源不需要授权就可以读取。
> Open access resources does not require authorization to read them out.


受保护的资源需要访问令牌来读取。受保护的资源又分为只读访问和读写访问。
> Protected resources require an access token to read them out.Protected resources are further divided into Read Only access and Read and Write access.


本文档定义资源和数据的读写访问权限。
> This document defines the resources and data schema for Read and Write access.


定义了如下资源的读写访问：

- 转账

> The following protected Read and Write resources are defined:
> - transfer


### 5.2 OAuth Scope

为请求受保护资源的读写权限，客户端需要使用Financial API - Part 4: Protected Data API and Schema - Read only第5.2节的scope范围，表1定义了额外的范围：

| 资源 | 允许的操作 | Scope value |
| --- | --- | --- |
| Transfer | 账户间的转账操作 | wTransfer |

Table 1 - Financial API Write Scopes

> To request read and write authorization to access the protected resource in question, the client uses the OAuth scope values defined in clause 5.2 of Financial API - Part 4: Protected Data API and Schema - Read only. Additional scopes in Table 1 are defined.
> 
| Resource | Allowed Actions | Scope value |
| --- | --- | --- |
| Transfer | Transfer of money between accounts | wTransfer |

> 
> Table 1 - Financial API Write Scopes


### 5.3 受保护资源

#### 5.3.1 转账

**转账**代表将资产从一个账户转移到另一个账户。
> A **transfer** represents a transfer of assets from one account to another.


如下是非规范性的转账请求案例：
> Following is a non-normative example of the transfer request.


```
POST /transfer HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/json

{
  "Transfer" : {
    "TransferId" : "111222333444555",
    "FromAccountId" : "1357902468",
    "ToAccountId" : "3216540987",
    "Amount" : 50.00,
    "Memo" : "For Check #1234",
  }
}
```

如下是非规范性的转账响应案例：
> Following is a non-normative example of the transfer response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/transfer" },
       "fapi.transferstatus": {
          "href": "/transfer/status{?transferId}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true}
  },
  "TransferStatus": {
    "TransferId" : "111222333444555",
    "ReferenceId" : "8453935582",
    "Status" : "PENDING",
    "TransferDate" : "2015-02-01Z",
  }
}
```

## 6. API-ID's

### 6.1 简介

本文档中使用的API-IDs同Financial API - Part 4: Protected Data API and Schema - Read only第6节定义的一致。
> This document uses API-IDs as specified in clause 6 of Financial API - Part 4: Protected Data API and Schema - Read only.


### 6.2 List of API-ID's

本文档规定了如下附加的api-id：
> This document specifies the following additional API-IDs:

| api | api-id | description |
| --- | --- | --- |
| /transfer | 40000 | 400XXX indicates transfer related API's |


## 7. API Errors

### 7.1 简介

本文档对错误响应的声明与Financial API - Part 4: Protected Data API and Schema - Read only第7节一致。
> This API specified by this document uses error responses as specified in clause 7 of Financial API - Part 4: Protected Data API and Schema - Read only.


### 7.2 错误清单

## 8. 安全考量

## 9. 隐私考量

## 10. 致谢

(Fill in the names)

## 11. 参考文献

- [OFX2.2] Open Financial Exchange 2.2
- [HTML4.01] “HTML 4.01 Specification,” World Wide Web Consortium Recommendation REC-html401-19991224, December 1999
- [RFC7662] OAuth 2.0 Token Introspection
- [DDA] Durable Data API, (2015), FS-ISAC

## 附录A Financial Data API Level 1 (Normative)

- [fapi.yml]
