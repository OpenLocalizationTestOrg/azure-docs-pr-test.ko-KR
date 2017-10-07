---
title: "aaaAzure API 관리 템플릿 데이터 모델이 참조 | Microsoft Docs"
description: "Azure API 관리에서 개발자 포털 템플릿 hello에 대 한 hello 데이터 모델에 사용 되는 공통 항목에 대 한 hello 엔터티 및 유형 표현에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Azure API Management 템플릿 데이터 모델 참조
이 항목에서는 Azure API 관리에서 개발자 포털 템플릿 hello에 대 한 hello 데이터 모델에 사용 되는 공통 항목에 대 한 hello 엔터티 및 유형 표현을 설명 합니다.  
  
 서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.  
  
-   [API](#API)  
-   [API 요약](#APISummary)  
-   [응용 프로그램](#Application)  
-   [첨부 파일](#Attachment)  
-   [코드 샘플](#Sample)  
-   [Comment](#Comment)  
-   [필터링](#Filtering)  
-   [머리글](#Header)  
-   [HTTP 요청](#HTTPRequest)  
-   [HTTP 응답](#HTTPResponse)  
-   [문제](#Issue)  
-   [작업](#Operation)  
-   [작업 메뉴](#Menu)  
-   [작업 메뉴 항목](#MenuItem)  
-   [페이징](#Paging)  
-   [매개 변수](#Parameter)  
-   [제품](#Product)  
-   [공급자](#Provider)  
-   [표현](#Representation)  
-   [구독](#Subscription)  
-   [구독 요약](#SubscriptionSummary)  
-   [사용자 계정 정보](#UserAccountInfo)  
-   [사용자 로그인](#UseSignIn)  
-   [사용자 등록](#UserSignUp)  
  
##  <a name="API"></a> API  
 hello `API` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|id|string|리소스 식별자. Hello API hello 현재 API 관리 서비스 인스턴스 내에서 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `apis/{id}` 여기서 `{id}` 는 API id입니다. 이 속성은 읽기 전용입니다.|  
|name|string|Hello API의 이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|description|string|Hello API의 설명입니다. 비어 있지 않아야 합니다. HTML 서식 지정 태그를 포함할 수 있습니다. 최대 길이는 1000자입니다.|  
|serviceUrl|string|이 API를 구현 하는 hello 백 엔드 서비스의 절대 URL입니다.|  
|path|string|이 API 및 모든 hello API 관리 서비스 인스턴스 내의 해당 리소스 경로 고유 하 게 식별 하는 상대 URL입니다. 추가이 API에 대 한 공용 URL hello 서비스 인스턴스 만들기 tooform 하는 동안 지정한 toohello API 끝점 기준 URL입니다.|  
|프로토콜|숫자의 배열|이 API의 작업 호출할 수 있는 프로토콜 hello에 설명 합니다. 허용되는 값은 `1 - http` 및 `2 - https` 또는 둘 다입니다.|  
|authenticationSettings|[권한 부여 서버 인증 설정](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|이 API에 포함된 인증 설정의 컬렉션입니다.|  
|subscriptionKeyParameterNames|object|Hello 구독 키가 포함 된 쿼리 및/또는 헤더 매개 변수에 대 한 사용자 지정 이름을 사용 하는 toospecify 일 수 있는 선택적 속성입니다. 이 속성은 현재 다음 hello 두 속성 중 하나 이상을 포함 해야 합니다.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a> API 요약  
 hello `API summary` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|id|string|리소스 식별자. Hello API hello 현재 API 관리 서비스 인스턴스 내에서 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `apis/{id}` 여기서 `{id}` 는 API id입니다. 이 속성은 읽기 전용입니다.|  
|name|string|Hello API의 이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|description|string|Hello API의 설명입니다. 비어 있지 않아야 합니다. HTML 서식 지정 태그를 포함할 수 있습니다. 최대 길이는 1000자입니다.|  
  
##  <a name="Application"></a> 응용 프로그램  
 hello `application` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|hello hello 응용 프로그램의 고유 식별자입니다.|  
|제목|string|hello 응용 프로그램의 hello 제목입니다.|  
|설명|string|hello 응용 프로그램의 hello 설명입니다.|  
|Url|URI|hello 응용 프로그램에 대 한 URI 번호입니다.|  
|버전|string|Hello 응용 프로그램에 대 한 버전 정보입니다.|  
|요구 사항|string|Hello 응용 프로그램에 대 한 요구 사항에 대 한 설명|  
|시스템 상태|number|hello hello 응용 프로그램의 현재 상태입니다.<br /><br /> - 0 - 등록됨<br /><br /> - 1 - 제출됨<br /><br /> - 2 - 게시됨<br /><br /> - 3 - 거부됨<br /><br /> - 4 - 게시 취소됨|  
|RegistrationDate|DateTime|hello 날짜 및 시간 hello 응용 프로그램 등록 되었습니다.|  
|CategoryId|number|hello 응용 프로그램 (재무, 엔터테인먼트 등)의 hello 범주|  
|DeveloperId|string|hello hello 응용 프로그램을 제출 하는 hello 개발자의 고유 식별자입니다.|  
|첨부 파일|[첨부 파일](#Attachment) 엔터티의 컬렉션입니다.|Hello 또는 같은 응용 프로그램 스크린 샷 아이콘에 대 한 모든 첨부 파일입니다.|  
|아이콘|[첨부 파일](#Attachment)|hello hello 응용 프로그램에 대 한 아이콘 번호입니다.|  
  
##  <a name="Attachment"></a> 첨부 파일  
 hello `attachment` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|UniqueId|string|hello hello 첨부 파일에 대 한 고유 식별자입니다.|  
|Url|string|hello 리소스의 hello URL입니다.|  
|형식|string|첨부 파일의 hello 형식입니다.|  
|ContentType|string|hello 미디어 hello 첨부 파일의 유형입니다.|  
  
##  <a name="Sample"></a> 코드 샘플  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|title|string|hello 연산의 hello 이름입니다.|  
|snippet|string|이 속성은 사용되지 않으며 사용할 수 없습니다.|  
|brush|string|코드 구문 색 템플릿 toobe hello 코드 샘플을 표시할 때 사용 합니다. 허용되는 값은 `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` 및 `csharp`입니다.|  
|template|string|이 코드 예제 서식 파일의 hello 이름입니다.|  
|body|string|Hello 조각의 hello 코드 샘플 부분에 대 한 자리 표시자입니다.|  
|메서드|string|hello hello 작업의 HTTP 메서드입니다.|  
|scheme|string|hello hello 작업 요청에 대 한 프로토콜 toouse 합니다.|  
|path|string|hello 연산의 hello 경로입니다.|  
|쿼리|string|정의된 매개 변수가 있는 쿼리 문자열 예제입니다.|  
|host|string|이 작업을 포함 하는 API hello에 대 한 hello API 관리 서비스 게이트웨이의 hello URL입니다.|  
|headers|[헤더](#Header) 엔터티의 컬렉션입니다.|이 작업에 대한 헤더입니다.|  
|매개 변수|[매개 변수](#Parameter) 엔터티의 컬렉션입니다.|이 작업에 대해 정의된 매개 변수입니다.|  
  
##  <a name="Comment"></a> 주석  
 hello `API` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|number|hello 주석의 hello id입니다.|  
|CommentText|string|hello 주석의 hello 본문입니다. HTML을 포함할 수 있습니다.|  
|DeveloperCompany|string|hello 개발자의 hello 회사 이름입니다.|  
|PostedOn|DateTime|hello 날짜 및 시간 hello 주석을 게시 했습니다.|  
  
##  <a name="Issue"></a> 문제  
 hello `issue` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|hello hello 문제에 대 한 고유 식별자입니다.|  
|ApiID|string|이 문제를 보고 된 hello API에 대 한 hello id입니다.|  
|제목|string|Hello 문제의 제목입니다.|  
|설명|string|Hello 문제에 대 한 설명입니다.|  
|SubscriptionDeveloperName|string|Hello 문제를 보고 하는 hello 개발자의 이름입니다.|  
|IssueState|string|hello hello 문제의 현재 상태입니다. 가능한 값은 Proposed, Opened, Closed입니다.|  
|ReportedOn|DateTime|hello 날짜 및 시간 hello 문제 보고 되었습니다.|  
|설명|[주석](#Comment) 엔터티의 컬렉션입니다.|이 문제에 대한 주석입니다.|  
|첨부 파일|[첨부 파일](api-management-template-data-model-reference.md#Attachment) 엔터티의 컬렉션입니다.|모든 첨부 파일 toohello 문제가 발생 했습니다.|  
|Services|[API](#API) 엔터티의 컬렉션입니다.|hello Api hello 문제를 신고 tooby hello 사용자를 구독 합니다.|  
  
##  <a name="Filtering"></a> 필터링  
 hello `filtering` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|패턴|string|검색 단어를 현재 hello; 또는 `null` 검색 단어가 없는 경우.|  
|Placeholder|string|지정 된 검색 단어가 없는 경우 hello 검색 상자에 텍스트 toodisplay를 hello 합니다.|  
  
##  <a name="Header"></a> 헤더  
 이 섹션에서는 hello 설명 `parameter` 표현 합니다.  
  
|속성|설명|유형|  
|--------------|-----------------|----------|  
|name|string|매개 변수 이름입니다.|  
|description|string|매개 변수 설명입니다.|  
|값|string|헤더 값입니다.|  
|typeName|string|헤더 값의 데이터 형식입니다.|  
|options|string|옵션입니다.|  
|필수|부울|여부 hello 헤더가 필요 합니다.|  
|readOnly|부울|여부 hello 헤더는 읽기 전용입니다.|  
  
##  <a name="HTTPRequest"></a> HTTP 요청  
 이 섹션에서는 hello 설명 `request` 표현 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|description|string|작업 요청 설명입니다.|  
|헤더|[헤더](#Header) 엔터티의 배열입니다.|요청 헤더입니다.|  
|매개 변수|[매개 변수](#Parameter)의 배열|작업 요청 매개 변수의 컬렉션입니다.|  
|표현|[표현](#Representation)의 배열|작업 요청 표현의 컬렉션입니다.|  
  
##  <a name="HTTPResponse"></a> HTTP 응답  
 이 섹션에서는 hello 설명 `response` 표현 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|statusCode|양의 정수|작업 응답 상태 코드입니다.|  
|description|string|작업 응답 설명입니다.|  
|표현|[표현](#Representation)의 배열|작업 응답 표현의 컬렉션입니다.|  
  
##  <a name="Operation"></a> 작업  
 hello `operation` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|id|string|리소스 식별자. Hello 작업 hello 현재 API 관리 서비스 인스턴스 내에서 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `apis/{aid}/operations/{id}` 여기서 `{aid}` 는 API id 및 `{id}` 작업 식별자입니다. 이 속성은 읽기 전용입니다.|  
|name|string|Hello 작업의 이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|description|string|Hello 작업의 설명입니다. 비어 있지 않아야 합니다. HTML 서식 지정 태그를 포함할 수 있습니다. 최대 길이는 1000자입니다.|  
|scheme|string|이 API의 작업 호출할 수 있는 프로토콜 hello에 설명 합니다. 허용되는 값은 `http`, `https` 또는 `http` 및 `https` 모두입니다.|  
|uriTemplate|string|이 작업에 대 한 hello 대상 리소스를 식별 합니다. 상대 URL 템플릿. 매개 변수를 포함할 수 있습니다. 예제: `customers/{cid}/orders/{oid}/?date={date}`|  
|host|string|hello API를 호스팅하는 hello API 관리 게이트웨이 URL입니다.|  
|httpMethod|string|작업 HTTP 메서드입니다.|  
|request|[HTTP 요청](#HTTPRequest)|요청 세부 정보를 포함하는 엔터티입니다.|  
|응답|[HTTP 응답](#HTTPResponse)의 배열|작업 [HTTP 응답](#HTTPResponse) 엔터티의 배열입니다.|  
  
##  <a name="Menu"></a> 작업 메뉴  
 hello `operation menu` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|ApiId|string|hello 현재 API의 hello id입니다.|  
|CurrentOperationId|string|hello 현재 작업의 hello id입니다.|  
|동작|string|hello 메뉴 형식입니다.|  
|MenuItems|[작업 메뉴 항목](#MenuItem) 엔터티의 컬렉션입니다.|현재 API hello에 대 한 hello 작업입니다.|  
  
##  <a name="MenuItem"></a> 작업 메뉴 항목  
 hello `operation menu item` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|hello 연산의 hello id입니다.|  
|제목|string|hello 연산의 hello 설명입니다.|  
|HttpMethod|string|hello hello 작업의 Http 메서드입니다.|  
  
##  <a name="Paging"></a> 페이징  
 hello `paging` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Page|number|hello 현재 페이지 번호입니다.|  
|PageSize|number|hello 최대 결과 toobe 단일 페이지에 표시 됩니다.|  
|TotalItemCount|number|표시할 항목 hello 수입니다.|  
|ShowAll|부울|여부 toosho 모든 단일 페이지에 발생 합니다.|  
|PageCount|number|페이지 결과의 개수는 hello입니다.|  
  
##  <a name="Parameter"></a> 매개 변수  
 이 섹션에서는 hello 설명 `parameter` 표현 합니다.  
  
|속성|설명|유형|  
|--------------|-----------------|----------|  
|name|string|매개 변수 이름입니다.|  
|description|string|매개 변수 설명입니다.|  
|값|string|매개 변수 값입니다.|  
|options|문자열의 배열|쿼리 매개 변수 값에 대해 정의된 값입니다.|  
|필수|부울|매개 변수가 필요한지 여부를 지정합니다.|  
|kind|number|이 매개 변수가 경로 매개 변수(1) 또는 쿼리 문자열 매개 변수(2)인지 여부입니다.|  
|typeName|string|매개 변수 유형입니다.|  
  
##  <a name="Product"></a> 제품  
 hello `product` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|리소스 식별자. Hello 현재 API 관리 서비스 인스턴스 내의 hello 제품을 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `products/{pid}` 여기서 `{pid}` 는 제품 id입니다. 이 속성은 읽기 전용입니다.|  
|제목|string|Hello 제품의 이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|설명|string|Hello 제품의 설명입니다. 비어 있지 않아야 합니다. HTML 서식 지정 태그를 포함할 수 있습니다. 최대 길이는 1000자입니다.|  
|용어|string|제품 사용 약관입니다. Toosubscribe toohello 제품을 시도 하는 개발자가 표시 되 고 tooaccept hello 등록 프로세스를 완료 하기 전에 이러한 용어 필요 합니다.|  
|ProductState|number|Hello 제품이 게시 되었는지 여부를 지정 합니다. 게시 된 제품은 개발자가 hello 개발자 포털에서 검색할 수 있습니다. 게시 되지 않은 제품은 tooadministrators 표시 됩니다.<br /><br /> 제품 상태에 대 한 hello 값 허용 됩니다.<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|부울|사용자가 hello에 여러 개의 구독 toothis 제품을 가질 수 있는지 여부를 지정 동시 합니다.|  
|MultipleSubscriptionsCount|number|hello 현재 사용자가 구독 toothis 제품 hello 수입니다.|  
  
##  <a name="Provider"></a> 공급자  
 hello `provider` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|속성|문자열 사전|이 인증 공급자에 대한 속성입니다.|  
|AuthenticationType|string|hello 공급자 유형입니다. (Azure Active Directory, Facebook 로그인, Google 계정, Microsoft 계정, Twitter).|  
|Caption|string|Hello 공급자의 표시 이름입니다.|  
  
##  <a name="Representation"></a> 표현  
 이 섹션에서는 `representation`을 설명합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|contentType|string|이 표현에 대한 등록된 또는 사용자 지정 콘텐츠 형식을 지정합니다(예: `application/xml`).|  
|샘플|string|Hello 표현의 예입니다.|  
  
##  <a name="Subscription"></a> 구독  
 hello `subscription` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|리소스 식별자. Hello 현재 API 관리 서비스 인스턴스 내의 hello 구독을 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `subscriptions/{sid}` 여기서 `{sid}` 는 구독 id입니다. 이 속성은 읽기 전용입니다.|  
|ProductId|string|hello의 hello 제품 리소스 식별자는 제품을 구독합니다. hello 값은 hello 형식의 유효한 상대 URL `products/{pid}` 여기서 `{pid}` 는 제품 id입니다.|  
|ProductTitle|string|Hello 제품의 이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|ProductDescription|string|Hello 제품의 설명입니다. 비어 있지 않아야 합니다. HTML 서식 지정 태그를 포함할 수 있습니다. 최대 길이는 1000자입니다.|  
|ProductDetailsUrl|string|상대 URL toohello 제품 세부 정보입니다.|  
|state|string|hello 구독의 hello 상태입니다. 가능한 상태는 다음과 같습니다.<br /><br /> - `0 - suspended`– hello 구독이 차단 되 고 hello 구독자 hello 제품의 Api를 호출할 수 없습니다.<br /><br /> - `1 - active`– hello 구독이 활성화 되어 있습니다.<br /><br /> - `2 - expired`– hello 구독 만료 날짜에 도달 하 고 비활성화 합니다.<br /><br /> - `3 - submitted`– hello 구독 요청이 hello 개발자가 이루어졌을 하지만 아직 승인 또는 거부 합니다.<br /><br /> - `4 - rejected`– 관리자가 hello 구독 요청이 거부 되었습니다.<br /><br /> - `5 - cancelled`– hello 개발자 또는 관리자가 hello 구독을 취소 했습니다.|  
|displayName|string|Hello 구독의 표시 이름입니다.|  
|CreatedDate|datetime|hello 날짜 hello 구독이 생성 된 ISO 8601 형식에서: `2014-06-24T16:25:00Z`합니다.|  
|CanBeCancelled|부울|여부 hello 현재 사용자가 hello 구독을 취소할 수 있습니다.|  
|IsAwaitingApproval|부울|여부 hello 구독 승인 대기 중입니다.|  
|StartDate|datetime|ISO 8601 형식에서 hello 시작 hello 구독에 대 한 날짜: `2014-06-24T16:25:00Z`합니다.|  
|ExpirationDate|datetime|ISO 8601 형식에서 hello 구독에 대 한 hello 만료 날짜: `2014-06-24T16:25:00Z`합니다.|  
|NotificationDate|datetime|ISO 8601 형식에서 hello 구독에 대 한 hello 알림 날짜: `2014-06-24T16:25:00Z`합니다.|  
|primaryKey|string|hello 기본 구독 키입니다. 최대 길이는 256자입니다.|  
|secondaryKey|string|hello 보조 구독 키입니다. 최대 길이는 256자입니다.|  
|CanBeRenewed|부울|여부 hello 현재 사용자가 hello 구독을 갱신할 수 있습니다.|  
|HasExpired|부울|여부 hello 구독이 만료 되었습니다.|  
|IsRejected|부울|여부 hello 구독 요청이 거부 되었습니다.|  
|CancelUrl|string|hello 상대 Url toocancel hello 구독입니다.|  
|RenewUrl|string|hello 상대 Url toorenew hello 구독입니다.|  
  
##  <a name="SubscriptionSummary"></a> 구독 요약  
 hello `subscription summary` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Id|string|리소스 식별자. Hello 현재 API 관리 서비스 인스턴스 내의 hello 구독을 고유 하 게 식별 합니다. hello 값은 hello 형식의 유효한 상대 URL `subscriptions/{sid}` 여기서 `{sid}` 는 구독 id입니다. 이 속성은 읽기 전용입니다.|  
|DisplayName|string|hello 표시 이름 hello 구독입니다.|  
  
##  <a name="UserAccountInfo"></a> 사용자 계정 정보  
 hello `user account info` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|FirstName|string|이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|LastName|string|성입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|Email|string|메일 주소입니다. 비어 있지 않아야 하 고 hello 서비스 인스턴스 내에서 고유 해야 합니다. 최대 길이는 254자입니다.|  
|암호|string|사용자 계정 암호입니다.|  
|NameIdentifier|string|계정 식별자를 hello hello 사용자 전자 메일와 동일 합니다.|  
|ProviderName|string|인증 공급자 이름입니다.|  
|IsBasicAccount|부울|이 계정은 전자 메일 및 암호를 사용 하 여 등록 된 경우 true입니다. hello 계정 공급자를 사용 하 여 등록 된 경우 false입니다.|  
  
##  <a name="UseSignIn"></a> 사용자 로그인  
 hello `user sign in` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|Email|string|메일 주소입니다. 비어 있지 않아야 하 고 hello 서비스 인스턴스 내에서 고유 해야 합니다. 최대 길이는 254자입니다.|  
|암호|string|사용자 계정 암호입니다.|  
|ReturnUrl|string|hello 사용자 로그인을 클릭 한 위치의 hello 페이지의 hello URL입니다.|  
|RememberMe|부울|여부 toosave hello 현재 사용자의 정보입니다.|  
|RegistrationEnabled|부울|등록이 활성화되어 있는지 여부입니다.|  
|DelegationEnabled|부울|위임된 로그인이 활성화되어 있는지 여부입니다.|  
|DelegationUrl|string|hello 사용 하도록 설정한 경우 로그인 url 위임 합니다.|  
|SsoSignUpUrl|string|단일 hello 있는 경우 URL에 hello 사용자에 대 한 로그인 합니다.|  
|AuxServiceUrl|string|Hello 현재 사용자가 관리자 인 경우이 hello Azure 클래식 포털의에서 링크 toohello 서비스 인스턴스입니다.|  
|공급자|[공급자](#Provider) 엔터티의 컬렉션|이 사용자에 대 한 hello 인증 공급자입니다.|  
|UserRegistrationTerms|string|사용자 로그인 toobefore 동의 해야 하는 조건입니다.|  
|UserRegistrationTermsEnabled|부울|약관이 활성화되었는지 여부입니다.|  
  
##  <a name="UserSignUp"></a> 사용자 등록  
 hello `user sign up` 엔터티에 hello 다음과 같은 속성을 포함 합니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|PasswordConfirm|부울|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up)등록 제어 합니다.|  
|암호|string|사용자 계정 암호입니다.|  
|PasswordVerdictLevel|number|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up)등록 제어 합니다.|  
|UserRegistrationTerms|string|사용자 로그인 toobefore 동의 해야 하는 조건입니다.|  
|UserRegistrationTermsOptions|number|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up)등록 제어 합니다.|  
|ConsentAccepted|부울|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up)등록 제어 합니다.|  
|Email|string|메일 주소입니다. 비어 있지 않아야 하 고 hello 서비스 인스턴스 내에서 고유 해야 합니다. 최대 길이는 254자입니다.|  
|FirstName|string|이름입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|LastName|string|성입니다. 비어 있지 않아야 합니다. 최대 길이는 100자입니다.|  
|UserData|string|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up) 제어 합니다.|  
|NameIdentifier|string|Hello 사용 되는 [등록](api-management-page-controls.md#sign-up)등록 제어 합니다.|  
|ProviderName|string|인증 공급자 이름입니다.|

## <a name="next-steps"></a>다음 단계
서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.
