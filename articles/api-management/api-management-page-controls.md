---
title: "API 관리 페이지 컨트롤 aaaAzure | Microsoft Docs"
description: "Azure API 관리에서 개발자 포털 서식 파일에서 사용 하기 위해 사용할 수 있는 hello 페이지 컨트롤에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Azure API Management 페이지 컨트롤
Azure API 관리 hello 다음 hello 개발자 포털 서식 파일에서 사용 하기 위해 컨트롤을 제공 합니다.  
  
 toouse 컨트롤을 위치에 배치할 원하는 hello hello 개발자 포털 서식 파일에 있습니다. Hello 같은 일부 컨트롤 [앱 작업](#app-actions) hello 다음 예제에에서 나와 있는 것 처럼 매개 변수가 있습니다.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 hello 매개 변수에 대 한 hello 값 hello 서식 파일에 대 한 hello 데이터 모델의 일부로 전달 됩니다. 대부분의 경우에서에 붙여 넣기만 하면 hello 예제 각 컨트롤에 제공 toowork 올바르게 합니다. Hello 매개 변수 값에 대 한 자세한 내용은 hello 컨트롤을 사용할 수 있는 각 템플릿에 대 한 모델 섹션에 데이터를 볼 수 있습니다.  
  
 서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.  
  
## <a name="developer-portal-template-page-controls"></a>개발자 포털 템플릿 페이지 컨트롤  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [providers](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 hello `app-actions` 컨트롤 hello 사용자 프로필 페이지 hello 개발자 포털에서 응용 프로그램 상호 작용 하기 위한 사용자 인터페이스를 제공 합니다.  
  
 ![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|appId|hello 응용 프로그램의 hello id입니다.|  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `app-actions` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [응용 프로그램](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>basic-signin  
 hello `basic-signin` hello에 대 한 정보 수집 사용자 로그인 페이지 hello 개발자 포털에 로그인에 대 한 컨트롤은 컨트롤을 제공 합니다.  
  
 ![basic&#45;signin 컨트롤](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `basic-signin` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [로그인](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 hello `paging-control` 항목의 목록을 표시 하는 포털 페이지 개발자에서 페이징 기능을 제공 합니다.  
  
 ![페이징 컨트롤](./media/api-management-page-controls/APIM-paging-control.png "APIM 페이징 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `paging-control` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [API 목록](api-management-api-templates.md#APIList)  
  
-   [문제 목록](api-management-issue-templates.md#IssueList)  
  
-   [제품 목록](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> 공급자  
 hello `providers` 컨트롤 hello 로그인 hello 개발자 포털에서 페이지의 인증 공급자 선택에 대 한 컨트롤을 제공 합니다.  
  
 ![공급자 컨트롤](./media/api-management-page-controls/APIM-providers-control.png "APIM 공급자 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `providers` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [로그인](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 hello `search-control` 포털 페이지 항목의 목록을 표시 하는 개발자에 검색 기능을 제공 합니다.  
  
 ![검색 컨트롤](./media/api-management-page-controls/APIM-search-control.png "APIM 검색 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `search-control` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [API 목록](api-management-api-templates.md#APIList)  
  
-   [제품 목록](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 hello `sign-up` 컨트롤 hello 등록 hello 개발자 포털에서 페이지에서에서 사용자 프로필 정보를 수집 하기 위한 컨트롤을 제공 합니다.  
  
 ![등록&#45;컨트롤](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 등록 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `sign-up` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [등록](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 hello `subscribe-button` 사용자 tooa 제품을 구독에 대 한 컨트롤을 제공 합니다.  
  
 ![subscribe&#45;button 컨트롤](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>매개 변수  
 없음.  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `subscribe-button` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [제품](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 hello `subscription-cancel` 컨트롤의 hello 사용자 프로필 페이지 hello 개발자 포털에서 구독 tooa 제품을 취소 하는 것에 대 한 컨트롤을 제공 합니다.  
  
 ![subscription&#45;cancel 컨트롤](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 컨트롤")  
  
### <a name="usage"></a>사용 현황  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|subscriptionId|hello 구독 toocancel의 hello id입니다.|  
|cancelUrl|hello 구독 URL을 취소 합니다.|  
  
### <a name="developer-portal-templates"></a>개발자 포털 템플릿  
 hello `subscription-cancel` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.  
  
-   [제품](api-management-product-templates.md#Product)

## <a name="next-steps"></a>다음 단계
서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.
