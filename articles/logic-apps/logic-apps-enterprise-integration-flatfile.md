---
title: "aaaEncode Azure 논리 앱에 있는 플랫 파일 디코딩 또는 | Microsoft Docs"
description: "파일 파일 인코더 또는 디코더가 논리 앱에 엔터프라이즈 통합 팩 hello에 toouse hello 하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>플랫 파일을 사용한 엔터프라이즈 통합 개요

기업 (B2B) 시나리오에서 tooa 비즈니스 파트너를 보내기 전에 XML tooencode를 콘텐츠 할 수 있습니다. 논리 앱에서는이 커넥터 toodo 인코딩 hello 플랫 파일을 사용할 수 있습니다. hello 만드는 논리 앱 콘텐츠를 볼 수는 XML에서 다양 한 소스를 포함 하 여 HTTP 요청 트리거, 다른 응용 프로그램 또는 hello 중 하나 에서도 많은 [커넥터](../connectors/apis-list.md)합니다. 논리 앱에 대 한 자세한 내용은 참조 hello [논리 앱 설명서](logic-apps-what-are-logic-apps.md "논리 앱에 대 한 자세한")합니다.  

## <a name="create-hello-flat-file-encoding-connector"></a>Hello 플랫 파일 인코딩 커넥터 만들기
이러한 단계 tooadd를 플랫 파일 인코딩 커넥터 tooyour 논리 앱을 따릅니다.

1. 논리 앱 만들기 및 [tooyour 통합 계정 연결](logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다")합니다. 이 계정은 tooencode hello XML 데이터를 사용 하 여 hello 스키마를 포함 합니다.  
2. 추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.  
   ![트리거 tooselect의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. 작업을 다음과 같이 인코딩 hello 플랫 파일을 추가 합니다.
   
    a. 선택 hello **플러스** 기호입니다.
   
    b. 선택 hello **동작 추가** 링크 (hello 더하기 기호를 선택한 후 표시 됨).
   
    c. Hello 검색 상자에 입력 *플랫* toofilter toouse 되도록 하나 작업 toohello hello 모든 합니다.
   
    d. 선택 hello **플랫 파일 인코딩** hello 목록에서 옵션입니다.   
   ![플랫 파일 인코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Hello에 **플랫 파일 인코딩** 대화 상자, 선택 hello **콘텐츠** 입력란.  
   ![텍스트 상자 콘텐츠의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Hello tooencode 원하는 내용으로 hello body 태그를 선택 합니다. hello body 태그는 hello 콘텐츠 필드를 채웁니다.     
   ![본문 태그의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. 선택 hello **스키마 이름** 목록 상자 및 toouse tooencode hello hello 스키마 입력 콘텐츠를 선택 합니다.    
   ![스키마 이름 목록 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. 작업을 저장합니다.   
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

이 시점에서 플랫 파일 인코딩 커넥터의 설정이 완료됩니다. 실제 응용 프로그램에서 Salesforce와 같은 기간 업무 응용 프로그램에서는 hello로 인코딩된 데이터 toostore 수도 있습니다. 또는 해당 인코딩된 데이터 tooa 거래 업체를 보낼 수 있습니다. 쉽게 제공 하는 다른 커넥터 hello hello 중 하나를 사용 하 여 인코딩 작업 tooSalesforce 또는 tooyour 거래 업체의 작업 toosend hello 결과 추가할 수 있습니다.

이제 요청 toohello HTTP 끝점을 만들고이 hello hello 요청 본문에 hello XML 콘텐츠를 포함 하 여 커넥터를 테스트할 수 있습니다.  

## <a name="create-hello-flat-file-decoding-connector"></a>Hello 플랫 파일 디코딩 커넥터 만들기

> [!NOTE]
> 이 단계는 toocomplete, toohave 스키마 파일을 이미 통합 계정에 업로드 해야 합니다.

1. 추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.  
   ![트리거 tooselect의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. 다음과 같이 작업을 디코딩 hello 플랫 파일을 추가 합니다.
   
    a. 선택 hello **플러스** 기호입니다.
   
    b. 선택 hello **동작 추가** 링크 (hello 더하기 기호를 선택한 후 표시 됨).
   
    c. Hello 검색 상자에 입력 *플랫* toofilter toouse 되도록 하나 작업 toohello hello 모든 합니다.
   
    d. 선택 hello **플랫 파일 디코딩** hello 목록에서 옵션입니다.   
   ![플랫 파일 디코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. 선택 hello **콘텐츠** 제어 합니다. Hello 콘텐츠의 콘텐츠 toodecode hello로 사용할 수 있는 이전 단계에서 목록이 생성 됩니다. 해당 hello 확인 *본문* hello에서 들어오는 HTTP 요청은 사용할 수 있는 toobe 콘텐츠 toodecode hello로 사용 합니다. Hello 콘텐츠 toodecode hello에 직접 입력할 수도 있습니다 **콘텐츠** 제어 합니다.     
4. 선택 hello *본문* 태그입니다. 이제 알림 hello body 태그는 hello에 **콘텐츠** 제어 합니다.
5. Toouse toodecode hello 콘텐츠 hello 스키마의 hello 이름을 선택 합니다. hello 다음 스크린샷에서 *OrderFile* hello 선택한 스키마 이름입니다. 이 스키마 이름은 hello 통합 계정에 이전에 업로드 했습니다.
   
   ![플랫 파일 디코딩 대화 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. 작업을 저장합니다.  
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

이 시점에서 플랫 파일 디코딩 커넥터의 설정이 완료됩니다. 실제 응용 프로그램에서 Salesforce와 같은 기간 업무 응용 프로그램에서 toostore hello 디코딩할 데이터 수도 있습니다. hello 동작 tooSalesforce 디코딩 작업 toosend hello 결과 쉽게 추가할 수 있습니다.

이제 요청 toohello HTTP 끝점을 하 여 커넥터를 테스트할 수 있습니다 및 hello XML 내용을 포함 하 여 hello hello 요청 본문에 toodecode 합니다.  

## <a name="next-steps"></a>다음 단계
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")합니다.  

