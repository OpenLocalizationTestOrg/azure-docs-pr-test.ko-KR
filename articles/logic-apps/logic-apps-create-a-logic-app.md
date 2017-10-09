---
title: "aaaCreate 클라우드 앱 및 클라우드 서비스-Azure 논리 앱 간에 첫 번째 워크플로 | Microsoft Docs"
description: "Azure Logic Apps에서 워크플로를 만들고 실행하여 시스템 통합 및 EAI(Enterprise Application Integration) 시나리오에 대한 비즈니스 프로세스 자동화"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "워크플로, 클라우드 앱, 클라우드 서비스, 비즈니스 프로세스, 시스템 통합, Enterprise Application Integration, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>첫 번째 논리 앱 클라우드 앱 및 클라우드 서비스 간에 tooautomate 프로세스 워크플로 만들기

[Azure Logic Apps](logic-apps-what-are-logic-apps.md)를 사용하여 워크플로를 만들고 실행하는 경우 코드를 작성하지 않고도 비즈니스 프로세스를 쉽고 신속하게 자동화할 수 있습니다. 이 첫 번째 예제에서는 방법을 toocreate RSS를 확인 하는 기본 논리 앱 워크플로 피드 새로운 콘텐츠는 웹 사이트를 보여 줍니다. Hello 웹 사이트 피드에 새 항목이 표시 되 면 hello 논리 앱 Outlook 또는 Gmail 계정에서 전자 메일을 보냅니다.

toocreate 및 실행 논리 앱 이러한 항목이 필요합니다.

* Azure 구독. 구독이 없는 경우 [Azure 계정을 사용하여 시작](https://azure.microsoft.com/free/)할 수 있습니다. 그렇지 않으면 [종량제 구독에 등록](https://azure.microsoft.com/pricing/purchase-options/)할 수 있습니다.

  Azure 구독은 논리 앱 사용 요금을 청구하는 데 사용됩니다. Azure Logic Apps에서 [사용 계량](../logic-apps/logic-apps-pricing.md) 및 [가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)의 작동 방식에 대해 알아봅니다.

또한 이 예제에는 다음과 같은 항목이 필요합니다.

* Outlook.com, Office 365 Outlook 또는 Gmail 계정

    > [!TIP]
    > 개인 [Microsoft 계정](https://account.microsoft.com/account)이 있는 경우 Outlook.com 계정이 있습니다. 그렇지 않은 경우 Azure 직장 또는 학교 계정이 있으면 **Office 365 Outlook** 계정이 있습니다.

* 웹 사이트의 RSS 피드 링크 tooa입니다. 이 예에서는 hello [RSS hello CNN.com 웹 사이트에서 상위 스토리에 대 한 피드](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>워크플로를 시작하는 트리거 추가

A [ *트리거* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) 논리 앱 워크플로 시작 하는 이벤트 이며 논리 앱 필요한 hello 첫 번째 항목입니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.

2. Hello 왼쪽된 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **논리 앱** 다음과 같이 합니다.

     ![Azure Portal, New, 엔터프라이즈 통합, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > 선택할 수도 있습니다 **새로**, hello 검색 상자에 입력 한 다음 `logic app`, Enter 키를 누릅니다. 그런 다음 **Logic App** > **만들기**를 선택합니다.

3. 논리 앱의 이름을 지정하고 Azure 구독을 선택합니다. 이제 Azure 리소스 그룹을 만들거나 선택합니다. 이를 통해 관련 Azure 리소스를 구성하고 관리할 수 있습니다. 마지막으로, 논리 앱을 호스트에 대 한 hello 데이터 센터 위치를 선택 합니다. 준비 되 면 선택 **Pin toodashboard** 차례로 **만들기**합니다.

     ![논리 앱 세부 정보](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > 선택 하는 경우 **Pin toodashboard**, 논리 앱 배포 후 Azure 대시보드 hello에 표시 되 고 자동으로 열립니다. 논리 앱 hello에 hello 대시보드에 표시 되지 않습니다 **모든 리소스** 타일에서 선택 **참조 더**, 논리 앱을 선택 합니다. Hello 왼쪽된 메뉴에서 선택 하거나 **더 많은 서비스**합니다. **엔터프라이즈 통합** 아래에서 **Logic Apps**을 선택하고 논리 앱을 선택합니다.

4. Hello에 대 한 논리 앱을 처음 열 때 hello 논리가 응용 프로그램 디자이너 템플릿을 보여줍니다 tooget 시작을 사용할 수 있습니다. 이제 **빈 Logic App**을 선택하여 처음부터 논리 앱을 빌드할 수 있습니다.

    hello 논리 앱 디자이너가 열리고 사용 가능한 서비스를 표시 하 고 *트리거* 논리 앱에서 사용할 수 있는 합니다.

5. Hello 검색 상자에 입력 `RSS`,이 트리거를 선택 하 고: **-RSS 피드 항목은 게시 된 경우** 

    ![RSS 트리거](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Hello 링크 tootrack 원하는 hello 웹 사이트의 RSS 피드를 입력 합니다. 

     **주파수** 및 **간격**을 변경할 수도 있습니다. 
     이러한 설정은 논리 앱이 새 항목을 확인하는 빈도를 결정하고 시간 범위 동안 찾은 모든 항목을 반환합니다.

     이 예에서는 상위 스토리에 대 한 매일 toohello 만우절 웹 사이트 게시 확인해 보겠습니다.

     ![RSS 피드, 빈도 및 간격을 사용하여 트리거 설정](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. 이제 작업을 저장합니다. (Hello 디자이너 명령 모음에서 **저장**.)

   ![논리 앱 저장](media/logic-apps-create-a-logic-app/save-logic-app.png)

   저장 하면 논리 앱 문제, 하지만 새 항목에 대 한 논리 앱만 확인 현재 hello RSS 피드를 지정 합니다. 
   toomake 보다 유용한 추가 논리가 응용 프로그램의 사용자의 트리거 후 실행 하는 작업이 예제를 발생 시킵니다.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Tooyour 트리거가 응답 하는 작업 추가

[*작업*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)은 논리 앱 워크플로에서 수행하는 태스크입니다. 트리거 tooyour 논리 앱을 추가 하면 해당 트리거에 의해 생성 된 데이터와 작업 tooperform 작업을 추가할 수 있습니다. 이 예에서는 이제 hello 웹 사이트의 RSS 피드에 새 항목이 표시 되 면 전자 메일을 보내는 작업을 추가 합니다.

1. 트리거를 아래 hello 디자이너에서 선택 **새 단계** > **동작 추가** 다음과 같이:

   ![작업 추가](media/logic-apps-create-a-logic-app/add-new-action.png)

   디자이너에서는 hello [사용할 커넥터](../connectors/apis-list.md) 트리거가 발생할 때 작업 tooperform를 선택할 수 있도록 합니다.

2. 에 따라 전자 메일 계정을 수행 hello 단계 Outlook 또는 Gmail에 대 한 합니다.

   * hello 검색 상자에, Outlook 계정에서 전자 메일 toosend 입력 `outlook`합니다. **서비스** 아래에서 개인 Microsoft 계정에 **Outlook.com**을 선택하거나 Azure 회사 또는 학교 계정에 **Office 365 Outlook**을 선택합니다. 
   **작업** 아래에서 **전자 메일 보내기**를 선택합니다.

       ![Outlook "전자 메일 보내기" 작업 선택](media/logic-apps-create-a-logic-app/actions.png)

   * hello 검색 상자에, Gmail 계정에서 전자 메일 toosend 입력 `gmail`합니다. 
   **작업** 아래에서 **전자 메일 보내기**를 선택합니다.

       !["Gmail - 전자 메일 보내기" 선택](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. 전자 메일 계정에 대 한 자격 증명에 대 한 메시지가 면 hello 사용자 이름 및 암호를 사용 하 여 로그인 합니다. 

4. Hello 대상 전자 메일 주소 처럼이 작업에 대 한 hello 세부 정보를 제공 하 고 예를 들어 hello 전자 메일로 데이터 tooinclude hello에 대 한 hello 매개 변수를 선택 합니다.

   ![전자 메일로 데이터 tooinclude 선택](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    따라서 Outlook을 선택한 경우 논리 앱은 다음 예제와 같습니다.

    ![완료된 논리 앱](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  변경 내용을 저장합니다. (Hello 디자이너 명령 모음에서 **저장**.)

6. 이제 테스트하기 위해 논리 앱을 수동으로 실행할 수 있습니다. Hello 디자이너 명령 모음에서 **실행**합니다. 그렇지 않으면 논리 앱을 설정 하는 hello 일정에 따라 RSS 피드를 지정 하는 hello 확인 하도록 할 수 있습니다.

   논리 앱은 새 항목을 찾는 경우 hello 논리 앱 선택한 데이터를 포함 된 전자 메일을 보냅니다. 
   새 항목을 찾지 논리 앱 전자 메일을 보내는 hello 동작을 건너뜁니다.

7. 논리 앱의 실행 하 고 트리거 논리 앱 메뉴에서 기록을 확인 하 고 toomonitor 선택 **개요**합니다.

   ![논리 앱 실행 및 트리거 기록 모니터링 및 보기](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Hello 명령 모음에서 예상 하는 hello 데이터를 찾을 수 없는 경우을 선택 해 보십시오 **새로 고침**합니다.

   논리 앱의 상태에 대 한 자세한 toolearn 또는 실행 하 고 기록 또는 toodiagnose 논리 앱 트리거, 참조 [논리 앱의 문제를 해결](logic-apps-diagnosing-failures.md)합니다.

      > [!NOTE]
      > 논리 앱은 앱을 해제할 때까지 계속 실행합니다. 지금은 논리 앱 메뉴에서 응용 프로그램 해제 tooturn 선택 **개요**합니다. Hello 명령 모음에서 **사용 하지 않도록 설정**합니다.

축하드립니다. 첫 번째 기본 논리 앱을 설정하고 실행했습니다. 또한 코드 없이 프로세스를 자동화하는 워크플로를 쉽게 만들고 클라우드 앱 및 클라우드 서비스를 통합하는 방법에 대해 알아보았습니다.

## <a name="manage-your-logic-app"></a>논리 앱 관리

toomanage 응용 프로그램을 hello 상태를 확인, 편집, 기록 보기, 해제 또는 논리 앱을 삭제 하는 등의 작업을 수행할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.

2. Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다. **엔터프라이즈 통합** 아래에서 **논리 앱**을 선택합니다. 논리 앱을 선택합니다. 

   Hello 논리 앱 메뉴에서 이러한 논리 앱 관리 작업을 찾을 수 있습니다.

   |작업|단계| 
   |:---|:---| 
   | 앱의 상태, 실행 기록 및 일반 정보 보기| **개요**를 선택합니다.| 
   | 앱 편집 | **Logic App Designer**를 선택합니다. | 
   | 앱의 워크플로 JSON 정의 보기 | **Logic App 코드 보기**를 선택합니다. | 
   | 논리 앱에 수행된 작업 보기 | **활동 로그**를 선택합니다. | 
   | 논리 앱의 이전 버전 보기 | **버전**을 선택합니다. | 
   | 일시적으로 앱 해제 | 선택 **개요**, hello 명령 모음에서 선택 합니다 **사용 하지 않도록 설정**합니다. | 
   | 앱 삭제 | 선택 **개요**, hello 명령 모음에서 선택 합니다 **삭제**합니다. 논리 앱의 이름을 입력하고 **삭제**를 선택합니다. | 

## <a name="get-help"></a>도움말 보기

tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

*  [조건 추가 및 워크플로 실행](../logic-apps/logic-apps-use-logic-app-features.md)
*    [논리 앱 템플릿](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Azure Resource Manager 템플릿에서 논리 앱 만들기](../logic-apps/logic-apps-arm-provision.md)
