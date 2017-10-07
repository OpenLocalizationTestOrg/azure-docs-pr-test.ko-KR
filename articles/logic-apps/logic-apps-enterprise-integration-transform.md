---
title: "Azure 논리 앱-변환 사용 하 여 XML 데이터 aaaConvert | Microsoft Docs"
description: "변환 또는 mapps hello 엔터프라이즈 통합 SDK를 사용 하 여 논리 앱에 대 한 형식 간에 tooconvert XML 데이터 만들기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>XML 변환과 엔터프라이즈 통합
## <a name="overview"></a>개요
hello 엔터프라이즈 통합 변환 커넥터 형식 tooanother 형식 으로부터 데이터를 변환합니다. 예를 들어 hello hello YearMonthDay 형식의 현재 날짜를 포함 하는 들어오는 메시지를 할 수 있습니다. 변환 tooreformat hello 날짜 toobe hello MonthDayYear 형식으로 사용할 수 있습니다.

## <a name="what-does-a-transform-do"></a>변환의 기능은 무엇인가요?
지도 라고도 변환을 소스 XML 스키마 (입력 hello)와 대상 XML 스키마 (hello 출력)으로 구성 됩니다. 도 루프 구문 및 문자열 조작, 조건부 할당, 산술 식, 날짜 시간 포맷터를 포함 하 여 서로 다른 기본 제공 함수 toohelp 조작 하거나 컨트롤 hello 데이터를 사용할 수 있습니다.

## <a name="how-toocreate-a-transform"></a>어떻게 toocreate 변환?
변환/매핑 hello Visual Studio를 사용 하 여 만들 수 있습니다 [엔터프라이즈 통합 SDK](https://aka.ms/vsmapsandschemas)합니다. 완료를 만들고 테스트 hello 변환 되 면 통합 계정에 hello 변환을 업로드 합니다. 

## <a name="how-toouse-a-transform"></a>어떻게 toouse 변환
Hello 변환/매핑을 통합 계정에 업로드 한 후 논리 앱 toocreate를 사용할 수 있습니다. hello 논리 앱 hello 논리 앱 (트리거되고 toobe 변환 해야 하는 입력 콘텐츠가) 될 때마다 변환을 실행 합니다.

**같습니다. hello 단계 toouse 변환을**:

### <a name="prerequisites"></a>필수 조건

* 통합 계정을 만들고 지도 tooit 추가  

이제 hello 필수 구성 요소 처리 한 있습니다,입니다 시간 toocreate 논리 앱:  

1. 논리 앱 만들기 및 [tooyour 통합 계정 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다") hello 맵을 포함 하는 합니다.
2. 추가 **요청** 트리거 tooyour 논리 앱  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. 추가 hello **XML 변환** 먼저 선택 하 여 작업 **동작 추가**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Hello 단어를 입력 *변환* toouse 되도록 하나 작업 toohello를 모든 hello hello 검색 상자 toofilter  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. 선택 hello **XML 변환** 동작   
6. Hello XML 추가 **콘텐츠** 변환입니다. Hello hello HTTP 요청에 수신 하는 XML 데이터를 사용할 수 있습니다 **콘텐츠**합니다. 이 예에서는 hello hello 논리 앱을 트리거한 hello HTTP 요청 본문을 선택 합니다.
7. Hello의 선택 hello 이름을 **지도** toouse tooperform hello 변환 한다고 합니다. hello 지도 통합 계정에 이미 있어야 합니다. 이전 단계에서 이미 제공한 맵이 포함 된 논리 앱 액세스 tooyour 통합 계정.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. 작업을 저장합니다.  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

이 시점에서 맵의 설정이 완료됩니다. 실제 응용 프로그램에서 SalesForce와 같은 LOB 응용 프로그램의 toostore 변환 hello 데이터 수도 있습니다. TooSalesforce hello의 동작 toosend hello 출력으로 쉽게 변형할 수 있습니다. 

이제 요청 toohello HTTP 끝점을 만들어서 변환을 테스트할 수 있습니다.  

## <a name="features-and-use-cases"></a>기능 및 사용 사례
* 지도에서 만든 hello 변환에서 하나의 문서 tooanother 이름 및 주소를 복사 하는 등의 간단한 될 수 있습니다. 또는 hello의 기본 매핑 작업을 사용 하 여 보다 복잡 한 변환을 만들 수 있습니다.  
* 문자열, 날짜 시간 함수 등 여러 맵 작업이나 함수를 바로 사용할 수 있습니다.  
* Hello 스키마 간에 직접 데이터 복사를 수행할 수 있습니다. Hello hello SDK에에서 포함 된 맵 편집기, hello 소스 스키마의 hello 요소 hello 대상 스키마의 해당 항목을 연결 하는 선을 그리기 단순하게입니다.  
* 지도 만들 때 모든 hello 관계를 보여 주는 hello 맵 및 생성 하는 링크의 그래픽 표현을 보려면 합니다.
* Hello 맵 테스트 기능 tooadd 샘플 XML 메시지를 사용 합니다. 간단한 클릭으로 hello 맵 생성 및 hello 생성 된 출력을 테스트할 수 있습니다.  
* 기존 데이터 업로드  
* Hello XML 형식에 대 한 지원이 포함 되어 있습니다.

## <a name="learn-more"></a>자세한 정보
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  
* [맵에 대해 자세히 알아보기](../logic-apps/logic-apps-enterprise-integration-maps.md "엔터프라이즈 통합 맵에 대해 알아보기")  

