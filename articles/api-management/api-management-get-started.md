---
title: "aaaManage Azure API 관리에서 첫 번째 API | Microsoft Docs"
description: "Toocreate Api, 작업을 추가 하 고 API 관리 시작 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Azure API 관리에서 첫 번째 API 관리
## <a name="overview"> </a>개요
이 가이드에는 tooquickly Azure API 관리를 사용 하 여 시작 하 고 첫 번째 API 호출을 확인 하는 방법을 보여줍니다.

## <a name="concepts"> </a>Azure API 관리란?
Azure API 관리 tootake 원하는 백 엔드를 사용할 수 있으며 그에 따라 기능을 갖춘 API 프로그램을 시작.

일반적인 시나리오는 다음과 같습니다.

* **모바일 인프라 보안** 
* **ISV 파트너 에코 시스템을 사용 하도록 설정** hello 개발자 통해 빠른 파트너 온 보 딩을 제공 하 여 포털 하는 API 외관 toodecouple 구현 내부에서 작성 되며 없습니다 서식 파일을 파트너 소비 합니다.
* **내부 API 프로그램을 실행** hello 가용성 및 최신 버전에 대 한 hello 조직 toocommunicate tooAPIs 변경에 대 한 중앙된 위치를 제공 하 여 조직 계정 기반 액세스 제어 모두 기반 간의 보안된 채널 hello API 게이트웨이 및 hello 백 엔드를 제공 합니다.

hello 시스템 hello 다음과 같은 구성 요소가 구성 됩니다.

* hello **API 게이트웨이** 는 hello 끝점입니다.
  
  * API를 호출 하 고 라우팅하 tooyour 백 엔드를 허용 합니다.
  * API 키, JWT 토큰, 인증서 및 기타 자격 증명을 확인합니다.
  * 사용 할당량 및 속도 제한을 적용합니다.
  * 코드를 수정 하지 않고 hello 즉석에서 API를 변형합니다.
  * 설정된 위치에 백 엔드 응답을 캐시합니다.
  * 분석용으로 호출 메타데이터를 기록합니다.
* hello **게시자 포털** API 프로그램을 설정한 hello 관리 인터페이스입니다. 다음 작업을 수행하는 데 사용합니다.
  
  * API 스키마를 정의하거나 가져옵니다.
  * 제품에 API를 패키징합니다.
  * 할당량 또는 hello Api에 대 한 변형 같은 정책을 설정 합니다.
  * 분석의 정보를 활용합니다.
  * 사용자를 관리합니다.
* hello **개발자 포털** 역할을 hello 기본 웹 사이트는 개발자를 위한 수 있습니다.
  
  * API 설명서를 읽습니다.
  * Hello 대화형 콘솔을 통해 API를 사용해 봅니다.
  * 계정을 만들고 tooget API 키를 구독 합니다.
  * 자신의 사용량에 대한 분석에 액세스합니다.

## <a name="create-service-instance"> </a>API 관리 인스턴스 만들기
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][Azure Free Trial]을 참조하세요.
> 
> 

hello 첫 번째 작업의 단계에서는 API 관리 toocreate 서비스 인스턴스는 합니다. Toohello 로그인 [Azure 포털] [ Azure Portal] 클릭 **새로**, **웹 + 모바일**, **API 관리**합니다.

![API 관리 새 인스턴스][api-management-create-instance-menu]

에 대 한 **이름**, hello 서비스 URL에 대 한 고유한 하위 도메인 이름을 toouse를 지정 합니다.

원하는 hello 선택 **구독**, **리소스 그룹** 및 **위치** 서비스 인스턴스에 대 한 합니다.

입력 **Contoso ltd.** hello에 대 한 **조직 이름**, hello에 전자 메일 주소를 입력 하 고 **관리자 전자 메일** 필드입니다.

> [!NOTE]
> 이 전자 메일 주소는 hello API 관리 시스템에서에서 알림에 사용 됩니다. 자세한 내용은 참조 [어떻게 tooconfigure 알림 하 고 Azure API 관리에서 서식 파일을 전자 메일로][How tooconfigure notifications and email templates in Azure API Management]합니다.
> 
> 

![새 API 관리 서비스][api-management-create-instance-step1]

API 관리 서비스 인스턴스는 Developer, Standard, Premium의 세 가지 계층으로 제공됩니다.

> [!NOTE]
> hello 개발자 계층 개발, 테스트 및 파일럿 API 프로그램 고가용성은 문제가 되지입니다. Hello 표준 및 프리미엄 계층에서는 예약된 단위 개수 toohandle 더 많은 트래픽을 확장할 수 있습니다. 대부분의 처리 능력 및 성능을 hello Standard 및 Premium 계층 hello 사용 하 여 API 관리 서비스를 제공합니다. 임의 계층을 사용하여 이 자습서를 완료할 수 있습니다. API Management 계층에 대한 자세한 내용은 [API Management 가격][API Management pricing]을 참조하세요.
> 
> 

클릭 **만들기** toostart 서비스 인스턴스를 프로 비전 합니다.

![새 API 관리 서비스][api-management-instance-created]

Hello 서비스 인스턴스를 만든 후 hello 다음 단계는 toocreate 가져오거나 API.

## <a name="create-api"> </a>API 가져오기
API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다. API 작업은 웹 서비스 프록시 tooexisting입니다.

API를 만들고 작업을 수동으로 추가하거나 API를 가져올 수 있습니다. 이 자습서에서는 Microsoft에서 제공 하 고 Azure에서 호스팅되는 샘플 계산기 웹 서비스에 대 한 API hello를 가져옵니다.

> [!NOTE]
> API를 만들고 수동으로 추가 하는 작업에 대 한 지침을 참조 하십시오. [어떻게 toocreate Api](api-management-howto-create-apis.md) 및 [어떻게 tooadd 작업 tooan API](api-management-howto-add-operations.md)합니다.
> 
> 

Api는 hello 게시자 포털에서 구성 됩니다. tooreach, 클릭 **게시자 포털** hello 서비스 도구 모음에서 합니다.

![게시자 포털][api-management-management-console]

tooimport hello 계산기 API 클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **가져오기 API**합니다.

![API 가져오기 단추][api-management-import-api]

Hello 단계 tooconfigure hello 계산기 API 다음을 수행 합니다.

1. 클릭 **From URL**, 입력 **http://calcapi.cloudapp.net/calcapi.json** hello에 **사양 문서 URL** 텍스트 상자, 한 hello 클릭 **Swagger**  라디오 단추입니다.
2. 형식 **calc** hello에 **웹 API URL 접미사** 입력란.
3. Hello에 클릭 **(선택 사항) 제품** 확인란을 선택한 **스타터**합니다.
4. 클릭 **저장** tooimport hello API입니다.

![새 API 추가][api-management-import-new-api]

> [!NOTE]
> **API 관리**는 현재 가져오기에 대한 Swagger 문서의 1.2 및 2.0 버전을 지원합니다. [Swagger 2.0 사양](http://swagger.io/specification)에서 `host`, `basePath` 및 `schemes` 속성이 선택 사항이라고 선언하더라도 Swagger 2.0 문서는 해당 속성을 **반드시** 포함해야 합니다. 그렇지 않으면 가져오지 않습니다. 
> 
> 

가져온 hello API는 hello hello API에 대 한 요약 페이지에에서 표시 됩니다 hello 게시자 포털.

![API 요약][api-management-imported-api-summary]

hello API 섹션에 여러 탭이 있습니다. hello **요약** 기본 메트릭 및 hello API에 대 한 정보 탭에 표시 됩니다. hello [설정을](api-management-howto-create-apis.md#configure-api-settings) 탭은 API에 대 한 사용 되는 tooview 및 편집 hello 구성 합니다. hello [작업](api-management-howto-add-operations.md) 탭은 사용 되는 toomanage hello API의 작업으로 나타납니다. hello **보안** 탭은 기본 인증을 사용 하 여 hello 백 엔드 서버에 대 한 사용된 tooconfigure 게이트웨이 인증 수 또는 [상호 인증서 인증](api-management-howto-mutual-certificates.md), 및 tooconfigure [ OAuth 2.0을 사용 하 여 사용자 권한 부여](api-management-howto-oauth2.md)합니다.  hello **문제** 탭은 Api를 사용 하는 hello 개발자 보고 사용 하는 tooview 문제입니다. hello **제품** 탭은이 API를 포함 하는 사용 되는 tooconfigure hello 제품입니다.

기본적으로 각 API 관리 인스턴스는 두 개의 샘플 제품과 함께 제공됩니다.

* **Starter**
* **무제한**

이 자습서에서는 API hello를 가져올 때 기본 계산기 API hello toohello Starter 제품에 추가 되었습니다.

순서 toomake 호출 tooan api에서 개발자가 access tooit을 제공 하는 tooa 제품 먼저 구독 해야 합니다. 개발자는 tooproducts hello 개발자 포털에서 구독할 수 있습니다 또는 관리자가 개발자 tooproducts hello 게시자 포털에 등록할 수 있습니다. Hello API 관리 인스턴스 hello에서 이전 단계에서에서 만든 hello 자습서 하므로 기본적으로 구독 된 tooevery 제품은 이미 하기 때문에 관리자를 않습니다.

## <a name="call-operation"></a>Hello 개발자 포털에서 작업 호출
작업 편리 tooview 제공 하는 hello 개발자 포털에서 직접 호출할 수 있습니다 및 API의 hello 작동을 테스트 합니다. 이 자습서 단계에서는 hello 기본 계산기 API를 호출 합니다 **정수 두 개를 추가** 작업 합니다. 클릭 **개발자 포털** hello에 hello 메뉴에서 hello 게시자 포털의 오른쪽 위에 있습니다.

![개발자 포털][api-management-developer-portal-menu]

클릭 **Api** hello 상단 메뉴에서 **기본 계산기** toosee hello 사용 가능한 작업 합니다.

![개발자 포털][api-management-developer-portal-calc-api]

Note hello 샘플 설명과 함께 hello API 및이 작업을 사용 하는 hello 개발자에 대 한 설명서를 제공 하는 작업을 가져온 매개 변수입니다. 작업을 수동으로 추가하는 경우 이러한 설명을 추가할 수도 있습니다.

toocall hello **정수 두 개를 추가** 작업을 클릭 하 여 **실습**합니다.

![시도][api-management-developer-portal-calc-api-console]

Hello 매개 변수에 대 한 일부 값을 입력 하 또는 hello 기본값을 유지 하 고 클릭 수 **보낼**합니다.

![HTTP Get][api-management-invoke-get]

작업이 호출 hello 개발자 포털 hello 표시 **응답 상태**, hello **응답 헤더**, 임의의 **응답 콘텐츠**합니다.

![응답][api-management-invoke-get-response]

## <a name="view-analytics"> </a>분석 보기
기본 계산기를 선택 하 여 스위치 백 toohello 게시자 포털에 대 한 tooview 분석 **관리** hello에 hello 메뉴에서 hello 개발자 포털의 오른쪽 위에 있습니다.

![관리][api-management-manage-menu]

hello hello 게시자 포털에 대 한 기본 보기는 hello **대시보드**, 해당 API 관리 인스턴스에 대 한 개요를 제공 하는 합니다.

![대시보드][api-management-dashboard]

에 대 한 hello 차트 위로 hello 마우스 호버 **기본 계산기** toosee hello 특정 메트릭을의 지정 된 기간에 대 한 API hello hello 사용에 대 한 합니다.

> [!NOTE]
> 모든 줄 보이지 않으면 차트에서 뒤로 toohello 개발자 포털 및 API hello 일부 호출, 몇 분 정도 전환한 다음 돌아와서 toohello 대시보드 합니다.
> 
> 

클릭 **세부 정보 보기** tooview hello 요약 페이지 API 표시 하는 hello 메트릭 중 더 큰 버전을 포함 하 여 hello에 대 한 합니다.

![분석][api-management-mouse-over]

![요약][api-management-api-summary-metrics]

자세한 메트릭 및 보고서에 대 한 클릭 **분석** hello에서 **API 관리** hello 왼쪽 메뉴.

![개요][api-management-analytics-overview]

hello **분석** 섹션에 다음 4 개의 탭 hello:

* **한 눈에** 뿐만 아니라 상위 개발자, 상위 제품, 상위 Api 및 상위 작업 hello 전반적인 사용 현황 및 상태 메트릭을 제공 합니다.
* **사용량** 에서는 지리적 표현을 포함하여 API 호출 및 대역폭을 심도 있게 확인할 수 있습니다.
* **상태** 에서는 상태 코드, 캐시 성공률, 응답 시간, API 및 서비스 응답 시간을 위주로 보여 줍니다.
* **활동** hello 개발자, 제품, API 및 작업에서 특정 활동에 드릴 다운 하는 보고서를 제공 합니다.

## <a name="next-steps"> </a>다음 단계
* 너무 방법에 대해 알아봅니다[속도 제한 된 API 보호](api-management-howto-product-with-rules.md)합니다.

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
