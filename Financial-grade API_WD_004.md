# Financial Services – Financial-grade API - Part 4: Protected Data API and Schema - Read only

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


# Financial Services – Financial API - Part 4: Protected Data API and Schema - Read only 

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

## 5. 资源APIs

### 5.1 简介

FAPI文档定义了两种资源类型：

- 开放访问的资源；
- 受保护的资源；

> Financial API document specifies resources in two categories:
> - open access resources;
> - protected resources;


开放访问的资源不需要授权就可以读取。
> Open access resources does not require authorization to read them out.


受保护的资源需要访问令牌来读取。
> Protected resources require an access token to read them out.


本文档定义资源和数据的只读访问权限。
> This document defines the resources and data schema for Read Only access.


定义了如下类型的只读资源：

- 客户
- 账户
- 交易
- 转账
- 转账状态
- 对账单
- 其它

> The following protected Read Only resources are defined:
> - customer
> - account
> - transaction
> - transfer
> - transfer status
> - statement
> - etc.


### 5.2 OAuth Scope

作为OAuth授权框架的策略，授权请求需要向授权服务器传递scope值，FAPI在表1中定义了对只读资源的scope的值列表。

| 资源 | 允许的操作 | Scope value |
| --- | --- | --- |
| Account | 对账户摘要信息的只读操作 | rAccount |
| Customer | 对客户信息的只读操作，包括隐私信息 | rCustomer |
| Image | 对交易图片的只读权限 | rImage |
| Statement | 对对账单图片的只读权限 | rStatement |
| Transaction | 对交易信息的只读权限 | rTransaction |

Table 1 - Financial API Scopes

> As a profile of The OAuth 2.0 Authorization Framework, the authorization request to the Authorization Server requires `scope` values. Finacial API defines the scope values in Table 1 for read only access to Financial API protected resources.
> 
> | Resource | Allowed Actions | Scope value |
| --- | --- | --- |
| Account | Read only Access to summary account information | rAccount |
| Customer | Read only Access to customer information, including PII | rCustomer |
| Image | Read only Access to transaction images (checks and receipts) | rImage |
| Statement | Read only Access to statement image | rStatement |
| Transaction | Read only Access to transaction information | rTransaction |

> Table 1 - Financial API Scopes


本文档也定义了聚合的范围FinancialInformation，等同于rAccount + rCustomer + rImage + rStatement + rTransaction。
> This document also defines an aggregated scope `FinancialInformation`, which equates to
> `rAccount` + `rCustomer` + `rImage` + `rStatement` + `rTransaction`.


### 5.3 受保护的资源

#### 5.3.1 客户

**客户**是受OAuth保护的资源，它代表了访问令牌所关联的客户。
该资源被表示为URI，可以通过该URI的GET请求获得实际的JSON资源。
客户端只被允许获取授权范围内的数据。

> A **customer** is an OAuth protected resource that represents the customer referred to by the access token presented.
> It is represented as a URI from which the client can GET the JSON representation.
> The client is only allowed to obtain the data within the granted scope.


```java
Editor's Note: The DDA seems to be quite particular not to use customerId
but the "surrogate identity (identifier)", which is the access token.
However, the token endpoint returns customer_id and this is represented in
the HTTP header all the time. Need to find out what it is trying to achieve.
```

该对象的详细细节可以在附录A中参考Swagger格式的数据。
> The detail of this object is defined in Appendix A as a swagger.


如下是非规范性的资源请求案例：
> Following is a non-normative example of the resource request.


```
GET /customer HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
User-Agent: Intuit/1.2.3 Mint/4.3.1
Accept-Charset: UTF-8
```

如下是非规范性的资源响应的案例：
> Following is a non-normative example of the resource response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/customer" }
  },
  "Customer": {
    "name": {
      "first": "Michael",
      "middle": "J",
      "last": "Smith",
      "company": "Acme"
    },
    "taxId": "144-27-7471",
    "customerID": a237cb74-61c9-4319-9fc5-ff5812778d6b
  }
}
```

注意：这和OIDC定义的UserInfo端点类似。
> **NOTE**: It is similar to the UserInfo endpoint of [OIDC].


#### 5.3.2. 账户信息列表

账户信息列表是受OAuth保护的资源，它标识与所提供访问令牌相关的账户信息列表，即账户的元数据信息，这与具体的客户相关。
> An account descriptor list is an OAuth protected resource that represents the list of account descriptors, the metadata about the account, associated with the provided access token, which is related to the customer in question.


该对象的详细细节可以在附录A中参考Swagger格式的数据。
> The detail of this object is defined in Appendix A as a swagger.


如下是非规范性的资源请求案例：
> Following is a non-normative example of the resource request.


```
GET /accountDescriptorList HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
```

如下是非规范性的资源响应案例：
> Following is a non-normative example of the resource response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accountDescriptorList" },
       "fapi.account": {
          "href": "/accounts{?accountId}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true}
  },
  "AccountDescriptorList" : [
    {
      "AccountId" : "1357902468",
      "AccountType" : "SAVINGS",
      "DisplayName" : "Savings Account",
      "Status" : "OPEN",
      "Description" : "Savings Account",
    },
    {
      "AccountId" : "3216540987",
      "AccountType" : "CHECKING",
      "DisplayName" : "Checking Account",
      "Status" : "OPEN",
      "Description" : "Checking Account",
    }
  ]
}
```

```
 Editor's Note:  /me/accountDescriptorList might look more REST like.
```

#### 5.3.3 账户

**账户**是受OAuth保护的资源，代表相关客户的账户资源。
该资源被表示为URI，客户端可以通过该URI获取实际的JSON数据。
它可能是增强的HAL。
客户端仅被允许访问授权范围内的数据。
对签发组织而言，它有唯一的标识符accountId。
> An **account** is an OAuth protected resource that represents the account of the customer in question.
> It is represented as a URI from which the client can obtain the JSON representation.
> It may be HAL+ enhanced.
> The client is only allowed to obtain the data within the granted scope.
> It has an identifier unique to the issuing organization called `accountId`.


由于访问令牌仅标识用户，而用户可能拥有多个账户，因此需要提供账户的唯一标识符accountId。
> Since the access token only identifies the customer and the customer might have multiple accounts, account identifier, `accountId`, which is provided in the account descriptor needs to be provided.


该对象的详细细节可以在附录A中参考Swagger格式的数据。
> The detail of this object is defined in Appendix A as a swagger.


如下是非标准型的资源请求案例：
> Following is a non-normative example of the resource request.


```
POST /account HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1357902468
```

如下是非标准型的资源响应案例：
> Following is a non-normative example of the resource request.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accounts/?accountId=1357902468" },
       "fapi.statements": {
          "href": "/statements{?accountId,startTime,endTime}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true},
       "fapi.transactions": {
          "href": "/account/transactions"},
  },
  "DepositAccount" : {
    "AccountId" : "1357902468",
    "AccountType" : "SAVINGS",
    "DisplayName" : "Savings Account",
    "Status" : "OPEN",
    "Description" : "Savings Account",
    "ParentAccountId" : "2468135790",
    "Nickname" : "My Savings Account A",
    "AccountNumber" : "4561237890",
    "InterestRate" : 3.0,
    "InterestRateType" : "FIXED",
    "MicrNumber" : "9753108642",
    "BalanceAsOf" : "2015-01-01Z",
    "CurrentBalance" : 1000.00,
  }
}
```

尽管使用GET方式会更符合REST风格，但在上述案例中仍然采用POST方式，因此accountId将不会暴露到path中，这也就不会出现通过referrer和历史记录泄露accountId的问题。
> While GET is more REST like, in the above example, POST is used
> so that the accountId is not exposed as a path / query,
> which may expose the accountId through referrer and history.


#### 5.3.4 账户不可用

5.3.3节中描述的账户可能暂时不可用或不存在，那API将不会返回账户消息，而是返回提示该账户不存在或没有可用信息的消息。
> An **account** as described in 5.3.3 may not be available temporarily or does not exist. In that case the API will not
> return account info but a message indicating that it either does not exist or has no available information at the moment.


如下是非规范性的资源请求的案例：
> Following is a non-normative examples of the resource request.


```java
POST /account HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1357902468
```

如下是非规范性的资源请求案例，其中账号处在暂时不可用的状态。
> Following is a non-normative example of the resource request with an account being temporarily unavailable.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accounts/?accountId=1357902468" },
       "fapi.statements": {
          "href": "/statements{?accountId,startTime,endTime}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true},
       "fapi.transactions": {
          "href": "/account/transactions"},
  },
  "DepositAccount" : {
    "AccountId" : "1357902468",
    "Error" : {
        "Code":"700",
        "Description":"Account information temporarily not available"
    }
  }
}
```

如下是非规范性的资源请求案例，其中账号并不存在。
> Following is a non-normative example of the resource request with a non existing account.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accounts/?accountId=1357902468" },
       "fapi.statements": {
          "href": "/statements{?accountId,startTime,endTime}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true},
       "fapi.transactions": {
          "href": "/account/transactions"},
  },
  "DepositAccount" : {
    "AccountId" : "1357902468",
    "Error" : {
        "Code":"701",
        "Description":"Account does not exist"
    }
  }
}
```

#### 5.3.5 对账单

返回给定账户的对账单列表。
> Gets a list of statements for the given account.


```
POST /account/statements HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1357902468&startTime=2015-01-01Z&endTime=2015-02-01Z&page=1
```

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accounts/statements?accountId=1357902468" },
       "fapi.statement": {
          "href": "/statement/{?accountId,statementId}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true}
  },
  "Statements" : {
    "Total" : "1",
    "TotalPages" : "1",
    "Page" : "1",
    "Statement" : [
      {
        "AccountId" : "1357902468",
        "StatementId" : "ST875376081768363584636",
        "StatementDate" : "2015-01-01Z",
        "Description" : "Statement for 2015-01-01",
      },
      {
        "AccountId" : "1357902468",
        "StatementId" : "ST962558772885635484949",
        "StatementDate" : "2015-02-01Z",
        "Description" : "Statement for 2015-02-01",
      }
    ]
  }
}
```

```
Editor's Note: Is StatementId unique to the org or to the AccountId?
```

#### 5.3.6 对账单图片

**对账单**代表对账单图片，可能包含如下格式：

- application/pdf
- image/gif
- image/jpeg
- image/png
- image/tiff

> A **statement** represents an image of an account statement. It can be one of the following formats:
> - application/pdf
> - image/gif
> - image/jpeg
> - image/png
> - image/tiff


```
POST /account/statement HTTP/1.1
Host: example.com
Accept: application/pdf
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1&statementId=1
```

```
HTTP/1.1 200 OK
Content-Type: application/pdf

Binary data
```

#### 5.3.7 交易

**交易**代表给定账号的交易列表。
> **Transactions** represents a list of transactions for the given account.


```
POST /account/transactions HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1357902468&startTime=2015-01-01Z&endTime=2015-02-01Z&page=1
```

响应案例：
> Response example.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/accounts/transactions?accountId=1357902468&startTime=2015-01-01Z&endTime=2015-02-01Z&page=1" },
       "fapi.transaction": {
          "href": "/transaction{?accountId,transactionId}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true},
       "fapi.transactionImages": {
          "href": "/transaction/images/{?accountId,transactionId}",
          "Authorize":"Bearer {access_token}",
          "Method":"POST",
          "templated":true},
  },
  "Transactions" : {
    "Total" : "1",
    "TotalPages" : "1",
    "Page" : "1",
    "DepositTransaction" : [
      {
        "AccountId" : "1357902468",
        "TransactionId" : "111222333444555",
        "TransactionTimestamp" : "2015-02-01Z",
        "Description" : "Transfer",
        "Status" : "POSTED",
        "Amount" : -50.00,
        "TransactionType" : "TRANSFER",
        "Payee" : "3216540987",
      },
      {
        "AccountId" : "1357902468",
        "TransactionId" : "111222333444588",
        "TransactionTimestamp" : "2015-02-01Z",
        "Description" : "Transfer",
        "Status" : "POSTED",
        "Amount" : 150.00,
        "TransactionType" : "TRANSFER",
        "Payee" : "3216540987",
      }
    ]
  }
}
```

#### 5.3.8 交易图片

**交易图片**代表交易信息的图片，比如扫描的支票或者存款提款单。
它可以是如下格式之一：

- application/pdf
- image/gif
- image/jpeg
- image/png
- image/tiff

> A **transaction image** represents an image of a transaction such as a scanned check or deposit/withdrawal slip. It can be one of the following formats:
> - application/pdf
> - image/gif
> - image/jpeg
> - image/png
> - image/tiff


```
POST /account/transaction/image HTTP/1.1
Host: example.com
Accept: application/pdf
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/x-www-form-urlencoded

accountId=1&imageId=101&startTime=2015-01-01Z&endTime=2015-02-01Z
```

```
HTTP/1.1 200 OK
Content-Type: application/pdf

Binary data
```

#### 5.3.9 转账状态

**转账状态**代表对某笔转账交易请求的执行状态。
> A **transfer status** represents the status of a transfer request.


如下是非规范性的转账状态请求案例：
> Following is a non-normative example of the transfer request.


```
POST /transfer/status HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer w0mcJylzCn-AfvuGdqkty2-KP48=
Content-Type: application/json

transferId=111222333444555
```

如下是非规范性的转账状态响应的案例：
> Following is a non-normative example of the transfer status response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/transfer/status" }
  },
  "TransferStatus": {
    "TransferId" : "111222333444555",
    "ReferenceId" : "8453935582",
    "Status" : "SUCCESS",
    "TransferDate" : "2015-02-01Z",
  }
}
```

## 6. API-ID's

### 6.1 定义

为每个资源端点指定一个api-id，api-id是唯一的5位数字。
为资源端点分配api-id的好处如下：
(译者注：该版本的规范没有完成，不好翻译，请可自行阅读如下原文)

> For each resource endpoint an api-id is specified. Api-id’s are unique and are represented as a 5-digit integer value.
> Assigning an API-ID to a protected resource endpoint (API) has several advantages:
> 1. Due to internal regulations within FAPI provider systems FAPI endpoints may have to be implemented with different URL path components
> 1. Due to overlapping URL's within FAPI provider systems FAPI endpoints may have to be implemented with different URL path components
> 1. API-ID's identify a FAPI endpoint independently of the actual URL which


### 6.2 List of API-ID's

FAPI中的受保护资源端点都有api-id，应按照如下列表中分配：
> All protected resource endpoints in FAPI have an API-ID. The API-ID's shall be assigned as listed below:

| api | api-id | description |
| --- | --- | --- |
| /account | 10000 | 100XX indicates account related API's |
| /account/statement | 10010 |  |
| /account/statements | 10011 |  |
| /account/transaction | 10020 |  |
| /account/transactions | 10021 |  |
| /account/transaction/image | 10022 |  |
| /accountList | 10030 |  |
| /accountDetails | 10040 |  |
| /availability | 20010 | 200XXX indicates api-health related API's |
| /capability | 20020 |  |
| /customer | 30000 | 300XXX indicates customer related API's |
| /transfer | 40000 | 400XXX indicates transfer related API's |
| /transfer/status | 40010 |  |
| /atm/countries | 50010 | 500XXX indicates atm related API's |
| /atm/provinces | 50020 |  |
| /atm/locations | 50030 |  |
| /products | 60000 | 600XXX indicates product related API's |


每当API发生错误时就会返回api-id，api-id会与错误码结合，客户端可以通过HTTP header中的api-id来识别失败的API。
> API-ID's are returned whenever an error on that API occurs. The api-id will be combined with an error code. Clients are able to identify the failing API by reading the api-id which is returned in an HTTP header.


## 7. API Errors

### 7.1 简介

资源端点可能会返回代表错误的响应，在这种情况下，应结合错误信息给与适当的HTTP状态码，但即便HTTP状态码定义的很好，也不总能明确的传达错误信息。资源端点也会返回错误信息，但这些信息必须由客户端解析，以提取有关错误信息的原因。
> Resource endpoints may respond with an error. In those cases an appropriate HTTP status is returned in conjunction with an error message. HTTP status codes are well defined but do not always indicate the exact cause for an error. Resource endpoints will also include an error message but these have to be parsed by clients to extract the information about the error cause.


要求客户端解析错误信息有以下缺点：

1. 客户端以来文本信息，但这些信息可以会随时间改变；
1. 客户端需要能解析本地化的错误信息(译者注：应该是指国际化)；
1. 由于FAPI提供方系统的内部规约，错误信息可能与本文档中定义的不一致；

> Requiring a client to parse the error message has several drawbacks:
> - Clients depend on a text message which may change over time
> - Clients need to be able to parse localized error messages
> - Due to internal regulations within FAPI provider systems error messages may not match the ones specified in this document


### 7.2 错误码

每种类型的错误都会指定一个错误码，错误码是3位的整数。
> For each type of error an error code is specified. Error codes are specified as a 3-digit integer value.


### 7.4 Error响应头

x-fapi-err应包含一个通过"-"来连接api-id和错误码的值。
该值使客户端能识别导致错误的端点和错误类型，无需解析消息主体。
> A HTTP header named `x-fapi-err` shall contain a value constructed by concatenating the API-ID value and the error code with "-" (0x2D).
> The value shall enable a client to identify the error causing protected resource endpoint and the type of error without parsing the message body.


### 7.5 Error响应

错误响应应该包括HTTP错误响应头和错误信息，提供错误响应头有如下好处：

1. 无需解析错误信息就可以访问HTTP的头；
1. 错误信息的content-type可以被忽略；
1. 本地化的错误信息不需要客户端有额外的特殊处理；
1. 客户端即便是进行过封装，可以在某封装后的方法向不同端点执行多个请求，也可以识别出导致错误的资源端点；

> Error responses shall include the HTTP error header and an error message. Providing the error header has several advantages:
> 1. HTTP headers are accessible without parsing the error message
> 1. The content type of the error message can be ignored
> 1. Localized error messages do not require special handling by the client
> 1. The error causing protected resource can be identified even if client libraries are used that execute multiple requests to different endpoints in an encapsulating manner


### 7.6 错误清单

RFC 6749 (OAuth 2.0)没有指定受保护资源端点的错误响应，但它提供了错误响应框架(第8.5节)，并指定了错误名称和描述。按照此模式，FAPI为如下几类指明了错误：

1. 一般的服务端错误
1. 无效的请求参数
1. 请求受限
1. 无效的access_token

> RFC 6749 (OAuth 2.0) does not specify error responses for protected resource endpoints. It provides an error response framework (Section 8.5) and specifies a pattern for error names and descriptions. Following that pattern FAPI specifies errors for several categories:
> 1. General server side errors
> 1. Invalid request parameters
> 1. General limitations
> 1. Invalid access_token


#### 7.6.1 一般的服务端错误

服务端可能出现意外的内部错误，这些类型的错误应该引起系统管理员的注意。

| 错误码 | 错误 | 错误描述 | http status |
| --- | --- | --- | --- |
| 000 | invalid | 未知异常 | 500 |


> It is possible that servers have internal errors that occur unexpected. These types of errors will likely require system administrators attention.
> 
| error code | error | error description | http status |
| --- | --- | --- | --- |
| 000 | invalid | The request failed due some unknown reason | 500 |



#### 7.6.2 无效的请求参数

受保护资源端点可能会要求参数和请求头满足一定的格式。

| 错误码 | 错误 | 错误描述 | http status |
| --- | --- | --- | --- |
| 100 | invalid_request | 缺失或重复的参数 | 400 |
| 101 | invalid_request | 缺失或重复的请求头 | 400 |


> Protected resource endpoints may require parameters and headers and have limitations on how they can be provided.
> 
| error code | error | error description | http status |
| --- | --- | --- | --- |
| 100 | invalid_request | Missing or duplicate parameters | 400 |
| 101 | invalid_request | Missing or duplicate headers | 400 |



#### 7.6.3 API访问限制

受保护的资源端点可能存在访问限制导致请求失效。

| 错误码 | 错误 | 错误描述 | http status |
| --- | --- | --- | --- |
| 200 | invalid_request | 超过了允许的请求数量 | 400 |
| 201 | invalid_request | 不支持的Content-Type | 400 |
| 202 | invalid_request | 请求消息超出最大限制 | 400 |


> Protected resource endpoints may have restrictions that fail otherwise valid requests.
> 
| error code | error | error description | http status |
| --- | --- | --- | --- |
| 200 | invalid_request | The number of permitted requests has been exceeded | 400 |
| 201 | invalid_request | The request messages Content-Type is not supported | 400 |
| 202 | invalid_request | The request message exceeds max. message size | 400 |



#### 9.6.4 无效的access_token

访问受保护资源端点总是需要携带access_token，但是该token可能验证失败。

| 错误码 | 错误 | 错误描述 | http status |
| --- | --- | --- | --- |
| 990 | invalid_request | token已过期 | 401 |
| 991 | invalid_request | token无该scope访问权限 | 401 |
| 992 | invalid_request | token不存在或者已经使用过 | 401 |
| 993 | invalid_request | 该token被禁用 | 401 |
| 994 | invalid_Request | 该token是通过不支持的grant_type获取的 | 401 |
| 995 | invalid_Request | 该token是向不支持的客户类型签发的 | 401 |
| 996 | invalid_Request | 该token类型不受支持 | 401 |


> Protected resource endpoints always require an access_token but the token may not pass validations.
> 
| error code | error | error description | http status |
| --- | --- | --- | --- |
| 990 | invalid_request | The token has expired | 401 |
| 991 | invalid_request | The token misses permissions (SCOPE) | 401 |
| 992 | invalid_request | The token is missing or it has been provided more than once | 401 |
| 993 | invalid_request | The token is disabled | 401 |
| 994 | invalid_Request | The token was retrieved via an unsupported grant_type | 401 |
| 995 | invalid_Request | The token was issued to an unsupported client type | 401 |
| 996 | invalid_Request | The token type is not supported | 401 |



### 7.7 错误响应案例

假设请求被发送到一个受保护的端点，如/account，该端点的api-id为10000。在发送请求时，没有输入所需的参数accountId，此时错误类型为"缺失或重复的参数"，错误码为100。
则错误响应可能如下：

> Assuming a request was send to a protected endpoint such as **/account**. That endpoint has been specified with **api-id=10000**. A request is sent without the required parameter **accountId**. The error type _Missing or duplicate parameters_ has been specified with **error-code=100**.
> An error response may look as follows:


```
HTTP/1.1 400 Bad Request
Content-Type: application/json; charset=utf-8
x-fapi-err: 10000-100:

{
    "error":"invalid_request",
    "error_description":"Missing or duplicate parameters"
}
```

客户端可以通过处理响应头来识别失败的端点和错误类型，即使错误消息已经本地化。解析错误消息是可选的，可以用作展示目的。
> The client can identify the failing endpoint and the error by processing the error header even if the error message had been localized. Parsing the error message is optional and may be used for display purposes only.


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
- 

