---
title: "aaaManage 통합 계정 아티팩트 메타 데이터-Azure 논리 앱 | Microsoft Docs"
description: "Azure Logic Apps에 대한 통합 계정에서 아티팩트 메타데이터 추가 또는 검색"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Logic Apps에 대한 통합 계정에서 아티팩트 메타데이터 관리

통합 계정에서 아티팩트에 대한 사용자 지정 메타데이터를 정의하고 논리 앱에 대한 런타임 동안 해당 메타데이터를 검색할 수 있습니다. 예를 들어 파트너, 규약, 스키마 및 맵 등의 아티팩트에 대해 메타데이터를 지정할 수 있습니다. 모두 키-값 쌍을 사용해서 메타데이터를 저장합니다. 현재 아티팩트 UI 통해 메타 데이터를 만들 수는 없지만 REST Api toocreate 메타 데이터를 사용할 수 있습니다. 만들거나 hello Azure 포털에서에서 파트너, 계약 또는 스키마를 선택할 때 tooadd 메타 데이터 선택 **JSON으로 편집**합니다. 논리 앱에서 tooretrieve 아티팩트 메타 데이터를 hello 통합 계정 아티팩트 조회 기능을 사용할 수 있습니다.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>메타 데이터 tooartifacts 통합 계정 그룹에 추가

1. [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)을 만듭니다.

2. 예를 들어 아티팩트 tooyour 통합 계정을 추가, [파트너](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [계약](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), 또는 [스키마](logic-apps-enterprise-integration-schemas.md)합니다.

3.  Hello 아티팩트 선택, 선택 **JSON으로 편집**, 메타 데이터 정보를 입력 하 고 있습니다.

    ![메타데이터 입력](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Logic Apps에 대한 아티팩트에서 메타데이터 검색

1. [논리 앱](logic-apps-create-a-logic-app.md)을 만듭니다.

2. 만들기는 [논리 앱 tooyour 통합 계정에서 링크](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app)합니다. 

3. 같은 트리거를 추가 논리가 응용 프로그램 디자이너에서 *요청* 또는 *HTTP* tooyour 논리 앱.

4.  **다음 단계** > **작업 추가**를 선택합니다. *통합*을 검색합니다. 그러면 **통합 계정 - 통합 계정 아티팩트 조회**를 찾아서 선택할 수 있습니다.

    ![통합 계정 아티팩트 조회 선택](media/logic-apps-enterprise-integration-metadata/image2.png)

5. 선택 hello **아티팩트 유형**, hello 설명과 **아티팩트 이름**합니다.

    ![아티팩트 유형 선택 및 아티팩트 이름 제공](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>예제: 파트너 메타데이터 검색

파트너 메타데이터는 다음과 같은 세 가지 `routingUrl` 세부 정보를 포함합니다.

![파트너 "routingURL" 메타데이터 찾기](media/logic-apps-enterprise-integration-metadata/image6.png)

1. 논리 앱에서 트리거, 파트너에 대한 **통합 계정 - 통합계정 아티팩트 조회** 작업 및 **HTTP**를 추가합니다.

    ![트리거, 아티팩트 조회 및 "HTTP" tooyour 논리 앱 추가](media/logic-apps-enterprise-integration-metadata/image4.png)

2. tooretrieve hello URI, 논리 앱에 대 한 보기 tooCode 이동 합니다. 논리 앱 정의가 다음 예제와 같이 표시됩니다.

    ![검색 조회](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>다음 단계
* [규약에 대해 자세히 알아보기](logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  
