# Financial Services – Financial-grade API - Part 3: Open Data API

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


OpenID基金会的标准是根据OpenID Process中给出的规则起草的。
> OpenID Foundation standards are drafted in accordance with the rules given in the OpenID Process.


工作组的主要任务是起草实施者草案以及最终草案。最终草案需要公开发布，供公众审查60天，也供OIDF成员进行表决，至少需要50%以上的成员批准才能作为OIDF标准发布。
> The main task of work group is to prepare Implementers Draft and Final Draft. Final Draft adopted by the Work Group through consensus are circulated publicly for the public review for 60 days and for the OIDF members for voting. Publication as an OIDF Standard requires approval by at least 50 % of the members casting a vote.


请注意，该文档的某些内容可能涉及专利权相关问题，OIDF对识别此类专利权不负任何责任。
> Attention is drawn to the possibility that some of the elements of this document may be the subject of patent rights. OIDF shall not be held responsible for identifying any or all such patent rights.


Financial API - Part 3: Open Data API was prepared by OpenID Foundation Financial API Work Group.

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

在很多情况下，聚合服务等金融科技服务都会使用"screen scraping"和存储用户密码的方式，这种模式既脆弱又不安全。为应对脆弱性，应使用结构化数据的API模型，而为应对安全性，则应该利用OAuth[RFC6749，RFC6750]等token模型。
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


# Financial Services – Financial API - Part 3: Open Data API 

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


该文档定义了开放访问的资源和数据格式。
> This document defines the open access resources and data schema.


定义了如下了类型的开放访问的资源：

- 网点地址
- ATM地址
- 产品列表
- 产品信息
- API服务的可用性
- API服务能力
- API端点发现
- 其它

> The following open access resources are defined:
> - Branch location
> - ATM location
> - Offered products list
> - Offered product
> - API service availability
> - API service capability
> - API endpoint discovery
> - etc.


### 5.2 端点发现

```java
Editor's Note: In the following, we are currently citing OpenID Connect Discovery but
once OAuth Server Metadata is done, it should be changed to it.
```

该文档定义了发现各种资源端点的机制，以请求用户的金融数据。它定义了两种方式：

- 服务端元数据文档；
- 增强的HAL；

> This document defines a mechanism for discovering the various resources endpoints for requesting the user's financial data. It defines two ways of doing it i.e.,
> - server metadata document;
> - Enhanced HAL;


服务器元数据文档建立在OpenID Connect Discovery 1.0中描述的Discovery机制之上。本文档定义了表2中定义的OpenID Discovery响应的参数。
> Server metadata document builds upon the discovery mechanism described in OpenID Connect Discovery 1.0. This document defines the parameters defined in Table 2 to the OpenID Discovery response.


在使用HAL的情况下，描述链接的JSON将作为被返回的资源的一部分。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `fapi` _optional_ | Array | JSON对象，包含API资源端点的集合和对应的URL地址 |


> In case of using HAL, JSON describing the link is returned as a part of the resource being returned.
> 
| Parameter | Type | Description |
| --- | --- | --- |
| `fapi` _optional_ | Array | JSON object containing a collection of the API resources endpoints and their URL locations |



fapi参数包含以下值

| Rel | 参数 | 类型 | 描述 |
| --- | --- | --- | --- |
| fapi.account | account _optional_ | String | 获取账号信息 |
| fapi.accountlist | accountlist _optional_ | String | 获取账号列表 |
| fapi.accountdetails | accountdetails _optional_ | String | 获取账号详细信息 |
| fapi.statement | statement _optional_ | String | 获取对账单文档 |
| fapi.statementlist | statementlist _optional_ | String | 获取对账单列表 |
| fapi.transaction | transaction _optional_ | String | 获取交易文档 |
| fapi.transactionlist | transactionlist _optional_ | String | 获取交易列表 |
| fapi.availability | availability _optional_ | String | 获取API可用性的文档 |
| fapi.capability | capability _optional_ | String | 获取API能力的文档 |
| fapi.customer | customer _optional_ | String | 获取授权范围内客户端信息 |
| fapi.transfer | transfer _optional_ | String | 用于转账 |
| fapi.transferstatus | transferstatus _optional_ | String | 用于查询转账状态 |

Table 2 -- Link relations and the JSON parameters.

> The `fapi` parameter contains the following parameters:
> 
| Rel | Parameter | Type | Description |
| --- | --- | --- | --- |
| fapi.account | account _optional_ | String | URL for getting account information |
| fapi.accountlist | accountlist _optional_ | String | URL for getting list of accounts |
| fapi.accountdetails | accountdetails _optional_ | String | URL for getting account information (details & transactions) for the current token |
| fapi.statement | statement _optional_ | String | URL for retrieving a statement document |
| fapi.statementlist | statementlist _optional_ | String | URL for getting list of statements |
| fapi.transaction | transaction _optional_ | String | URL for getting a transaction document |
| fapi.transactionlist | transactionlist _optional_ | String | URL for getting list of transactions |
| fapi.availability | availability _optional_ | String | URL for getting information about this API's availability |
| fapi.capability | capability _optional_ | String | URL for getting information about this API's capabilities |
| fapi.customer | customer _optional_ | String | URL for getting about the customer within the authorization scope |
| fapi.transfer | transfer _optional_ | String | URL for creating a transfer between accounts |
| fapi.transferstatus | transferstatus _optional_ | String | URL for getting the status of a transfer between accounts |

> Table 2 -- Link relations and the JSON parameters.


```
Editor's note:
An example should be added.
```

以下使非规范性的discovery的例子。
> Following is a non-normative example of the discovery request.


```
GET /.well-known/openid-configuration HTTP/1.1
Host: example.com
Accept: application/json
Accept-Charset: UTF-8
```

以下是非规范性的资源响应的例子。
> Following is a non-normative example of the resource response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
 	"issuer": "https://example.com",
 	"authorization_endpoint": "https://example.com/connect/authorize",
 	"token_endpoint": "https://example.com/connect/token",
 	"jwks_uri": "https://example.com/jwks.json",
 	"scopes_supported": ["openid", "profile", "email", "address",
 		"phone", "offline_access"
 	],
 	"response_types_supported": ["code", "code id_token", "id_token", "token id_token"],
 	"subject_types_supported": ["pairwise"],
 	"id_token_signing_alg_values_supported": ["RS256", "ES256", "HS256"],
 	"fapi" : {
 	    "account" : "https://example.com/account",
 	    "statement" : "https://example.com/account/statement",
 	    "statementlist" : "https://example.com/account/statements",
 	    "transaction" : "https://example.com/account/transaction/image",
 	    "transactionlist" : "https://example.com/account/transactions",
 	    "accountlist" : "https://example.com/accountlist",
 	    "accountdetails" : "https://example.com/accountdetail",
 	    "availability" : "https://example.com/availability",
 	    "capability" : "https://example.com/capability",
 	    "customer" : "https://example.com/customer",
 	    "transfer" : "https://example.com/transfer",
 	    "transferstatus" : "https://example.com/transfer/status",
 	}
}
```

### 5.3 开放访问的资源

#### 5.3.1 ATM地址

##### 5.3.1.1 简介

ATM地址API已经 ...
> ATM locations APIs has ...


##### 5.3.1.2 ATM所属国列表

AIM所属国代理AIM所在国家列表的资源，该API不接受任何参数，返回国家信息的数组，该数组有以下成员：

- 名称：国家名称；
- 代码：ISO 3166-1 Alpha-3代码；
- Geocoding：地理编码。表示该国是否有地理编码的布尔值。

> ATM countries are the resource that represents the list of countries
> that the ATM are located. The API does not take any parameters and
> returns the array of country information which has the following
> members:
> - Name: Country name;
> - Code: ISO 3166-1 Alpha-3 code;
> - Geocoding: Boolean that represents whether the geocoding is available for the country or not.


请求案例：
> Request example:


```
GET /countries HTTP/1.1
Host: example.com
Accept: application/json
```

响应案例：
> Response example:


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "_links": {
       "self": { "href": "/countries" }
  },
  "Countries":  [
      {
        "Name": "Japan",
        "Code": "JPN",
        "Geocoding": FALSE
      },
      {
        "Name": "United States of America",
        "Code": "USA",
        "Geocoding": FALSE
      }
   ]
}
```

##### 5.3.1.3 ATM所属省列表

AIM所属省代表国家分区，如州、省、县等有AIM的地方。
> ATM provinces represents country subdivisions such as states, provinces, prefectures etc. that have ATM locations.


请求案例：
> Request example:


```
GET /atms/provinces?country=CAN HTTP/1.1
Host: example.com
Accept: application/json
```

响应案例：
> Response example:


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "_links": {
       "self": { "href": "/atms/provinces?country=CAN" }
  },
  "CountrySubdivisions":  [
    {
      "Name": "ALBERTA",
      "Code": "AB"
     },
    {
      "Name": "BRITISH COLUMBIA",
      "Code": "BC"
    }
  ]
}
```

##### 5.3.1.4 ATM位置

AIM位置表示ATM的地理位置，它以国家、省份、城市和经纬度作为参数。
> ATM locations represents the Geolocation of the ATMs.
> It takes Country, Province, City, latitude, and longitude as parameter.


详情参考附录A的Swagger格式文档。
> Details are defined in Swagger format in Appendix A.


请求案例：
> Request example:


```
GET /atms?country=CAN&province=BC HTTP/1.1
Host: example.com
Accept: application/json
```

响应案例：
> Response example:


```
{
  "atms":[
    {
      "id":"24242-3b13",
      "name":"RMD01",
      "address":{
        "line_1":" 1221 Granville St",
        "line_2":"",
        "line_3":"",
        "city":"Vancouver",
        "province":"BC",
        "postcode":"V6Z 1M6",
        "country":"CAN"
      },
     "location":{
        "latitude":49.2634,
        "longitude":-123.1241
      }
    }
  ]
}
```

#### 5.3.2 提供的产品

##### 5.3.2.1 简介

##### 5.3.2.2 提供的产品列表

产品列表代表金融机构提供的产品和服务清单。
> Offered product list represents the products and services offered by a financial institution.


详情参考附录A中Swagger格式文档。
> Details are defined in Swagger format in Appendix A.


请求案例：
> Request example:


```
GET /products HTTP/1.1
Host: example.com
Accept: application/json
```

响应案例：
> Response example:


```
{
  "Products": [{
    "Code": "BPC05001161",
    "Name": "Premiere Savings Account",
    "Category": "Savings",
    "Family": "Banking",
    "SuperFamily": "Financial",
    "MoreInfUrl": "https:example.com/products/BPC05001161",
    }, {
    "Code": "BCP11118372",
    "Name": "Retirement Account",
    "Category": "Retirement",
    "Family": "Investing",
    "SuperFamily": "Financial",
    "MoreInfoUrl": "https://example.com/products/BCP11118372",
  }]
}
```

##### 5.3.2.3 提供的产品

#### 5.3.4 可用性

可用性代表API服务的可用性。
> **Availability** represents the availability of the API service.


如下是非规范性的可用性求的例子：
> Following is a non-normative example of availability request.


```
GET /availability HTTP/1.1
Host: example.com
Accept: application/json
```

如下是非规范性的可用性响应的例子：
> Following is a non-normative example of the availability response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/availability" }
  },
  "Availability" : {
    "CurrentStatus" : "Operational",
    "CurrentStatusDesc" : "All systems working with no problems",
    "PlannedAvailability" : [
      {
        "Status" : "Maintenance",
        "StatusShortDesc" : "Monthly Maintenance Downtime",
        "StatusStartDate" : "2015-01-01T03:00:00.000Z",
        "StatusEndDate" : "2015-01-01T04:00:00.000Z",
      },
      {
        "Status" : "Maintenance",
        "StatusShortDesc" : "Monthly Maintenance Downtime",
        "StatusStartDate" : "2015-02-01T03:00:00.000Z",
        "StatusEndDate" : "2015-02-01T04:00:00.000Z",
      },
    ],
  }
}
```

#### 5.3.5 服务能力

服务能力标识API服务提供的能力和支持的特性。
> **Capability** represents the capabilities and supported features of the API service.


如下是非规范性的服务能力请求的例子：
> Following is a non-normative example of capability request.


```
GET /capability HTTP/1.1
Host: example.com
Accept: application/json
```

如下是非规范性的服务能力响应的例子：
> Following is a non-normative example of the capability response.


```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
  "_links": {
       "self": { "href": "/capability" }
  },
  "Capability": {
    "allowedConnections": 10,
    "supportsCustomer": true,
    "supportsAccounts": true,
    "supportsTransactions": true,
    "supportsImage": true,
  }
}
```

## 6. 安全考量

## 7. 隐私考量

## 8. 致谢

(Fill in the names)

## 9. 参考文献

- [OFX2.2] Open Financial Exchange 2.2
- [HTML4.01] “HTML 4.01 Specification,” World Wide Web Consortium Recommendation REC-html401-19991224, December 1999
- [RFC7662] OAuth 2.0 Token Introspection
- [DDA] Durable Data API, (2015), FS-ISAC

## 附录 A Financial Data API Level 1 (Normative)

- [fapi.yml]
- 

