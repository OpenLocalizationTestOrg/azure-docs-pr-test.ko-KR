---
title: "논리 앱에서 aaaAdd hello Office 365 Outlook 커넥터 | Microsoft Docs"
description: "Office 365와 Office 365 커넥터 tooenable 상호 작용을 통해 논리 앱을 만듭니다. 예: 연락처 및 일정 항목 만들기, 편집 및 업데이트."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Hello Office 365 Outlook 커넥터와 함께 시작.
hello Office 365 Outlook 커넥터를 사용 하면 Office 365 용 Outlook의에서 상호 작용 합니다. 사용이 커넥터 toocreate, 편집 및 업데이트 연락처 및 일정 항목 및 또한 가져오기, 보내기, 및 tooemail 회신 합니다.

Office 365 Outlook을 사용하여 다음을 수행합니다.

* Office 365 내에서 hello 전자 메일 및 일정 기능을 사용 하 여 워크플로 작성 합니다. 
* 사용 하 여 있으면 새 전자 메일, 일정 항목이 업데이트 될 때 워크플로 및 기타 toostart를 트리거합니다.
* 만들 새 일정 이벤트를 작업 toosend 전자 메일을 사용 합니다. 예를 들어 Salesforce (트리거)에 새 개체가 있을 때 전자 메일 보내기 tooyour Office 365 Outlook (작업). 

이 항목에서는 방법을 toouse hello 논리 앱에 Office 365 Outlook 커넥터 및 트리거 및 작업 그룹의 hello도 합니다.

> [!NOTE]
> 이 버전의 hello 문서 tooLogic 앱 GA (일반 공급)를 적용합니다.
> 
> 

논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="connect-toooffice-365"></a>TooOffice 365 연결
논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다. 연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다. 예를 들어 tooconnect tooOffice 365 Outlook, 먼저 Office 365 *연결*합니다. toocreate 연결을 일반적으로 tooconnect를 원하는 tooaccess hello 서비스를 사용 하는 hello 자격 증명을 입력 합니다. 따라서 Office 365 outlook hello 자격 증명 tooyour Office 365 계정 toocreate hello 연결을 입력 합니다.

## <a name="create-hello-connection"></a>Hello 연결 만들기
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. 트리거 "서비스를 폴링하기" hello 간격 및 원하는 빈도 합니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

1. Hello 논리 앱에서 "office 365" tooget hello 트리거 목록을 입력 합니다.  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. **Office 365 Outlook - 예정된 이벤트가 곧 시작될 때**를 선택합니다. 연결이 이미 존재 하는 경우 일정 hello 드롭 다운 목록에서 선택 합니다.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    증명된 toosign 인 경우 hello 로그인 세부 정보 toocreate hello 연결에을 입력 합니다. [Hello 연결을 만들](connectors-create-api-office365-outlook.md#create-the-connection) 이 항목의 hello 단계를 소개 합니다. 
   
   > [!NOTE]
   > 이 예제에서는 hello 논리 앱 일정 이벤트 업데이트 될 때 실행 됩니다. 이 트리거의 toosee hello 결과 텍스트 메시지를 보내는 다른 작업을 추가 합니다. 예를 들어 hello Twilio 추가 *메시지 보내기* 때 hello 달력 이벤트 텍스트의 15 분 내에 시작 하는 작업입니다. 
   > 
   > 
3. 선택 hello **편집** 단추 및 hello 설정 **주파수** 및 **간격** 값입니다. 예를 들어 15 분 마다 hello 트리거 toopoll 하려는 경우 다음 설정 hello **주파수** 너무**분**, 및 집합 hello **간격** 너무**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리). 논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.

## <a name="use-an-action"></a>작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

1. Hello 더하기 기호를 선택 합니다. 여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. **작업 추가**를 선택합니다.
3. Hello 텍스트 상자에 "office 365" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. 이 예제에서는 **Office 365 Outlook - 연락처 만들기**를 선택했습니다. 연결이 이미 존재 하는 경우 다음 hello 선택 **폴더 ID**, **지정 된 이름**, 및 기타 속성:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다. [Hello 연결을 만들](connectors-create-api-office365-outlook.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다. 
   
   > [!NOTE]
   > 이 예제에서는 Office 365 Outlook에 새 연락처를 만듭니다. 다른 트리거 toocreate hello 연락처의 출력을 사용할 수 있습니다. 예를 들어 SalesForce hello 추가 *개체를 만들 때* 트리거. 그런 다음 Office 365 Outlook hello 추가 *연락처 만들기* SalesForce hello를 사용 하 여 작업 필드 toocreate hello 새 새 연락처 Office 365의 합니다. 
   > 
   > 
5. **저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리). 논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/office365connector/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

