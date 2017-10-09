---
title: "Azure 논리 앱 aaaValidate XML-| Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello를 사용 하 여 Azure 논리 앱 및 B2B 시나리오에 대 한 스키마와 XML 유효성 검사"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>엔터프라이즈 통합에 대한 XML 유효성 검사

종종 B2B 시나리오에서 hello 파트너 규약에서 hello 메시지를 교환 하는 유효한 데이터 처리를 시작할 수 있는지 확인 해야 합니다. Hello 엔터프라이즈 통합 팩의에서 커넥터 hello 사용 hello XML 유효성 검사를 사용 하 여 미리 정의 된 스키마에 대 한 문서를 확인할 수 있습니다.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Hello XML 유효성 검사 커넥터와 함께 문서 유효성 검사

1. 논리 앱 만들기 및 [hello 앱 toohello 통합 계정 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 통합 계정 tooa 논리 앱에 알아봅니다") hello 스키마 toouse XML 데이터 유효성 검사에 사용할 수 있는 합니다.

2. 추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. tooadd hello **XML 유효성 검사** 동작을 선택 **동작 추가**합니다.

4. 원하는 하나 작업 toohello hello 모든 toofilter 입력 *xml* hello 검색 상자에 있습니다. **XML 유효성 검사**를 선택합니다.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. toospecify hello toovalidate, 원하는 XML 콘텐츠 선택 **콘텐츠**합니다.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Hello toovalidate 원하는 내용으로 hello body 태그를 선택 합니다.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. toouse hello 이전 유효성 검사에 대 한 원하는 toospecify hello 스키마 *콘텐츠* 입력, 선택 **스키마 이름**합니다.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. 작업을 저장합니다.  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

이제 유효성 검사 커넥터 설정이 끝났습니다. 실제 응용 프로그램에서 SalesForce와 같은 기간 업무 (LOB) 응용 프로그램에서 유효성을 검사 하는 hello 데이터 toostore 할 수 있습니다. toosend는 유효성이 검사 된 출력 tooSalesforce hello, 작업을 추가 합니다.

tootest 유효성 검사 동작을 요청 toohello HTTP 끝점을 확인 합니다.

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 통합 팩 hello에 대 한 자세한](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")   

