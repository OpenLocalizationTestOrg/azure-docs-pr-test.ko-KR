---
title: "aaaMonitor 가상 컴퓨터 변경-Azure 이벤트 표 형태 및 논리 앱 | Microsoft Docs"
description: "Azure Event Grid와 Logic Apps를 사용하여 VM(가상 컴퓨터)의 구성 변경 사항을 확인합니다."
keywords: "논리 앱, 이벤트 표, 가상 컴퓨터, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Azure Event Grid와 Logic Apps를 사용하여 가상 컴퓨터의 변경 사항 모니터링

Azure 리소스 또는 타사 리소스에서 특정 이벤트가 발생하는 경우 자동화된 [논리 앱 워크플로](../logic-apps/logic-apps-what-are-logic-apps.md)를 시작할 수 있습니다. 이러한 리소스는 해당 이벤트 tooan 게시할 수 [Azure 이벤트 표 형태](../event-grid/overview.md)합니다. 차례로 hello 이벤트 표 형태 푸시 webhook을 큐에 있는 해당 이벤트 toosubscribers 또는 [이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md) 끝점으로 합니다. 구독자 논리 앱 hello 이벤트 표 형태에서 이러한 이벤트에 대 한 모든 코드를 작성 하지 않고 tooperform 작업-자동화 된 워크플로 실행 하기 전에 대기할 수 있습니다.

예를 들어 다음은 게시자 toosubscribers hello 이벤트 표 형태 Azure 서비스를 통해 보낼 수 있음을 일부 이벤트입니다.

* 리소스를 만들고, 읽고, 업데이트하거나 삭제합니다. 예를 들어 Azure 구독에 요금이 부과되어 청구서에 영향을 줄 수 있는 변경 사항을 모니터링할 수 있습니다. 
* Azure 구독에서 사람을 추가하거나 제거합니다.
* 앱에서 특정 작업을 수행합니다.
* 새 메시지가 큐에 표시됩니다.

이 자습서에서는 변경 내용을 tooa 가상 컴퓨터를 모니터링 하 고 이러한 변경에 대 한 전자 메일을 전송 하는 논리 앱을 만듭니다. Azure 리소스에 대 한 이벤트 구독 사용 하 여 논리 앱을 만들 때 이벤트를 이벤트 표 형태 toohello 논리가 응용 프로그램을 통해 해당 리소스에서 배치 합니다. hello 자습서가 논리 앱을 구축 하는 과정을 설명 합니다.

![개요 - Event Grid와 논리 앱으로 가상 컴퓨터 모니터링](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Event Grid를 통해 이벤트를 모니터링하는 논리 앱을 만듭니다.
> * 특별히 가상 컴퓨터 변경 내용을 확인하는 조건을 추가합니다.
> * 가상 컴퓨터가 변경될 때 전자 메일을 보냅니다.

## <a name="prerequisites"></a>필수 조건

* 알림 전송을 위한 [Azure Logic Apps에서 지원하는 전자 메일 공급자](../connectors/apis-list.md)(예: Office 365 Outlook, Outlook.com 또는 Gmail)의 전자 메일 계정. 이 자습서에서는 Office 365 Outlook을 사용합니다.

* [가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines). 가상 컴퓨터가 아직 없는 경우 [VM 만들기 자습서](https://docs.microsoft.com/azure/virtual-machines/)를 통해 새로 만듭니다. toomake hello 가상 컴퓨터 이벤트를 게시 하면 [다른 무엇 toodo 필요 하지 않은](../event-grid/overview.md)합니다.

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Event Grid에서 이벤트를 모니터링하는 논리 앱을 만듭니다.

첫째, 논리 앱 만들고 hello 리소스 그룹에서 가상 컴퓨터에 대 한 모니터링 하는 이벤트 표 트리거를 추가 합니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 

2. Hello 왼쪽된 위 모서리의 hello 주 Azure 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **논리 앱**합니다.

   ![논리 앱 만들기](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. 다음 표에 hello에 지정 된 hello 설정을 사용 하 여 논리 앱을 만듭니다.

   ![논리 앱 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | 설정 | 제안 값 | 설명 | 
   | ------- | --------------- | ----------- | 
   | **Name** | *{your-logic-app-name}* | 고유한 논리 앱 이름을 제공합니다. | 
   | **구독** | *{your-Azure-subscription}* | 선택 hello이 자습서의 모든 서비스에 대해 동일한 Azure 구독. | 
   | **리소스 그룹** | *{your-Azure-resource-group}* | 선택이이 자습서의 모든 서비스에 대해 같은 Azure 리소스 그룹을 hello 합니다. | 
   | **위치**: | *{your-Azure-region}* | 선택이이 자습서의 모든 서비스에 대해 동일한 지역을 hello 합니다. | 
   | | | 

4. 준비 되 면 선택 **Pin toodashboard**, 선택 **만들기**합니다.

   이제 논리 앱에 대한 Azure 리소스를 만들었습니다. 
   Azure 논리 앱을 배포 후 hello 논리 앱 디자이너를 보면 일반적인 패턴에 대 한 템플릿을 더 빠르게 시작할 수 있도록 있습니다.

   > [!NOTE] 
   > 선택 하는 경우 **Pin toodashboard**, 논리 앱 논리 앱 디자이너에서 자동으로 열립니다. 그렇지 않으면 논리 앱을 수동으로 찾아 열 수 있습니다.

5. 이제 논리 앱 템플릿을 선택합니다. **템플릿** 아래에서 **비어 있는 논리 앱**을 선택하면 논리 앱을 처음부터 빌드할 수 있습니다.

   ![논리 앱 템플릿 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   이제 표시 hello 논리 앱 디자이너 [ *커넥터* ](../connectors/apis-list.md) 및 [ *트리거* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) 논리 앱과도 동작 toostart를 사용할 수 있는 트리거 tooperform 작업 후 추가할 수 있습니다. 트리거는 논리 앱 인스턴스를 만들고 논리 앱 워크플로를 시작하는 이벤트입니다. 
   논리 앱 hello 첫 번째 항목으로 트리거를 프로비저닝해야 합니다.

6. Hello 검색 상자에 필터로 "이벤트 표 형태"를 입력 합니다. **Azure Event Grid - On a resource event**(Azure Event Grid - 리소스 이벤트 시) 트리거를 선택합니다.

   !["Azure Event Grid - On a resource event"(Azure Event Grid - 리소스 이벤트 시) 트리거 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. 메시지가 표시 되 면 Azure 자격 증명으로 tooAzure 이벤트 표 형태에에서 로그인 합니다.

   ![Azure 자격 증명으로 로그인](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > 하는 경우 로그인 개인 Microsoft 계정으로 같은 @outlook.com 또는 @hotmail.com, hello 이벤트 표 형태 트리거가 제대로 나타나지 않을 수 있습니다. 이 문제를 해결 선택 [서비스 사용자와 연결](/azure-resource-manager/resource-group-create-service-principal-portal.md), hello 예를 들어 Azure 구독과 연결 된 Azure Active Directory의 멤버인 인증 또는 *사용자 이름* @emailoutlook.onmicrosoft.com.

8. 이제 논리 앱 toopublisher 이벤트를 구독 합니다. 다음 표에 hello에 지정 된 대로 이벤트 구독에 대 한 hello 세부 정보를 제공 합니다.

   ![이벤트 구독에 대한 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | 설정 | 제안 값 | 설명 | 
   | ------- | --------------- | ----------- | 
   | **구독** | *{virtual-machine-Azure-subscription}* | Hello 이벤트 게시자의 Azure 구독을 선택 합니다. 이 자습서에 대 한 hello 가상 컴퓨터에 대 한 Azure 구독을 선택 합니다. | 
   | **리소스 종류** | Microsoft.Resources.resourceGroups | Hello 이벤트 게시자의 리소스 종류를 선택 합니다. 이 자습서에 대 한 선택 논리 앱 리소스 그룹에만 모니터링 하도록 지정 된 값을 hello 합니다. | 
   | **리소스 이름** | *{virtual-machine-resource-group-name}* | Hello 게시자의 리소스 이름을 선택 합니다. 이 자습서에 대 한 가상 컴퓨터에 대 한 hello 리소스 그룹의 hello 이름을 선택 합니다. | 
   | 옵션 설정의 경우 **고급 옵션 표시**를 선택합니다. | *{see descriptions}* | * **접두사 필터**: 이 자습서에서는 이 설정을 비워 둡니다. hello 기본 동작은 모든 값 일치합니다. 그러나 접두사 문자열(예: 특정 리소스에 대한 경로 및 매개 변수)을 필터로 지정할 수 있습니다. <p>* **접미사 필터**: 이 자습서에서는 이 설정을 비워 둡니다. hello 기본 동작은 모든 값 일치합니다. 그러나 특정 파일 형식만 원하는 경우 접미사 문자열(예: 파일 이름 확장명)을 필터로 지정할 수 있습니다.<p>* **구독 이름**: 이벤트 구독에 대한 고유한 이름을 제공합니다. |
   | | | 

   완료되면 Event Grid 트리거가 다음 예와 유사하게 나타납니다.
   
   ![Event Grid 트리거 세부 정보의 예](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. 논리 앱을 저장합니다. Hello 디자이너 도구 모음에서 선택 **저장**합니다. toocollapse / 숨기기 논리 앱에서 동작의 세부 hello 액션의 제목 표시줄을 선택 합니다.

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   논리 앱 이벤트 표 트리거를 저장 하면 Azure 논리 앱 tooyour 선택한 리소스에 대 한 이벤트 구독을 자동으로 만듭니다. 따라서 hello 리소스 이벤트 toohello 이벤트 표 형태를 게시 하면 해당 이벤트 표 형태 hello 이벤트 tooyour 논리 앱을 자동으로 푸시합니다. 이 이벤트 트리거 논리 앱 다음 만들고 단계에서 정의 하는 hello 워크플로 인스턴스를 실행 합니다.

논리 앱 현재 라이브 및 tooevents hello 이벤트 표 형태에서 수신 대기 있지만 toohello 워크플로 작업을 추가할 때까지 아무런 동작이 수행 되지 합니다. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>가상 컴퓨터의 변경 사항을 확인하는 조건 추가

toorun 논리 앱 워크플로 특정 이벤트가 발생 하는 경우에 가상 컴퓨터에 대 한 "쓰기" 작업을 확인 하는 조건을 추가 합니다. 이 조건이 true 일 때 논리 앱 업데이트 hello 가상 컴퓨터에 대 한 세부 정보는 전자 메일로 보냅니다.

1. 논리가 응용 프로그램 디자이너에서 hello 이벤트 표 트리거 선택 **새 단계** > **조건 추가**합니다.

   ![조건 tooyour 논리 앱 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   hello 논리가 응용 프로그램 디자이너 hello 조건이 true 또는 false 인지를 기반으로 하는 작업 경로 toofollow를 포함 하는 빈 조건 tooyour 워크플로에 추가 합니다.

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. Hello에 **조건** 상자 **고급 모드에서 편집**합니다.
다음 식을 입력합니다.

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   이제 조건은 다음 예와 같습니다.

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   이 식은 hello 이벤트 확인 `body` 에 대 한는 `data` 여기서 hello 개체 `operationName` 속성은 hello `Microsoft.Compute/virtualMachines/write` 작업 합니다. 
   [Event Grid 이벤트 스키마](../event-grid/event-schema.md)에 대해 자세히 알아보세요.

3. tooprovide hello 조건에 대 한 설명을 선택 hello **줄임표** (**...** ) hello 조건 셰이프를 단추 한 다음 선택 **이름 바꾸기**합니다.

   > [!NOTE] 
   > hello이 자습서의 뒷부분에 나오는 예제 제공 hello 논리 앱 워크플로의 단계에 대해 설명 합니다.

4. 이제 선택할 **기본 모드에서 편집** hello 식 표시 된 것 처럼 자동으로 해결 되도록 합니다.

   ![논리 앱 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. 논리 앱을 저장합니다.

## <a name="send-email-when-your-virtual-machine-changes"></a>가상 컴퓨터가 변경될 때 전자 메일 보내기

이제 추가 [ *동작* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) hello를 지정 된 조건이 true 인 경우 전자 메일을 받을 수 있도록 합니다.

1. Hello 조건에 **True** 상자 **동작 추가**합니다.

   ![조건이 true인 경우의 작업 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Hello 검색 상자에 "email" 필터로 입력 합니다. 전자 메일 공급자에 따라를 찾기 되어 hello 일치 하는 커넥터를 선택 합니다. 커넥터에 대 한 hello "전자 메일 보내기" 작업을 선택 합니다. 예: 

   * Azure에 대 한 작업 또는 학교 계정이 선택 hello Office 365 Outlook 커넥터입니다. 
   * 개인 Microsoft 계정에 대 한 hello Outlook.com 커넥터를 선택 합니다. 
   * Gmail 계정에 대 한 hello Gmail 커넥터를 선택 합니다. 

   Hello Office 365 Outlook 커넥터와 함께 toocontinue를 하겠습니다. 
   다른 공급자를 사용 하는 경우 단계 상태를 유지 하는 hello hello 동일 하지만 UI 다르게 나타날 수 있습니다. 

   !["전자 메일 보내기" 작업 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. 전자 메일 공급자에 대 한 연결이 없는 경우 인증에 대 한 묻는 tooyour 전자 메일 계정에 로그인 합니다.

4. 다음 표에 hello에 지정 된 대로 hello 전자 메일에 대 한 세부 정보를 제공 합니다.

   ![빈 전자 메일 작업](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > 워크플로에서 사용할 수 있는 필드에서 tooselect 클릭 편집 상자에 있으므로 해당 hello **동적 콘텐츠** 열리고 나열 하거나 선택 **동적 콘텐츠를 추가할**합니다. 더 많은 필드에 대 한 선택 **더 보려면** hello 목록에서 각 섹션에 대 한 합니다. tooclose hello **동적 콘텐츠** 목록에서 선택 **동적 콘텐츠를 추가할**합니다.

   | 설정 | 제안 값 | 설명 | 
   | ------- | --------------- | ----------- | 
   | **To** | *{recipient-email-address}* |Hello 받는 사람의 전자 메일 주소를 입력 합니다. 자신의 이메일 주소를 사용하여 테스트할 수 있습니다. | 
   | **제목** | 업데이트된 리소스: **제목**| Hello 메일 제목에 대 한 hello 콘텐츠를 입력 합니다. 이 자습서에 대 한 입력 텍스트 및 선택 hello 이벤트 hello 제안 **주체** 필드입니다. 여기에서 메일 제목에는 업데이트 하는 hello 리소스 (가상 컴퓨터)에 대 한 hello 이름이 포함 됩니다. | 
   | **본문** | 리소스 그룹: **토픽** <p>이벤트 유형: **이벤트 유형**<p>이벤트 ID: **ID**<p>시간: **이벤트 시간** | Hello 메일의 본문에 대 한 hello 콘텐츠를 입력 합니다. 이 자습서에 대 한 입력 텍스트 및 선택 hello 이벤트 hello 제안 **항목**, **이벤트 유형을**, **ID**, 및 **이벤트 시간** 필드 있도록 사용자의 전자 메일 hello 리소스 그룹 이름, 이벤트 유형, 이벤트 타임 스탬프 및 hello 업데이트에 대 한 이벤트 ID를 포함합니다. <p>콘텐츠를에서 빈 줄 tooadd Shift + Enter를 누릅니다. | 
   | | | 

   > [!NOTE] 
   > 배열을 나타내는 필드 선택 hello 디자이너가 자동으로 추가 **각** hello 배열 참조 하는 hello 동작 주위 루프입니다. 그렇게 하면 논리 앱에서 각 배열 항목에 대한 해당 작업을 수행합니다.

   이제 전자 메일 작업이 다음 예와 같이 표시됩니다.

   ![전자 메일에서 출력 tooinclude를 선택 합니다.](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   완료된 논리 앱이 다음 예와 같이 표시됩니다.

   ![완료된 논리 앱](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. 논리 앱을 저장합니다. toocollapse / 숨기기 논리 앱에서 각 작업의 세부 hello 액션의 제목 표시줄을 선택 합니다.

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   논리 앱 현재 라이브가 있지만 작업을 수행 하기 전에 변경 내용 tooyour 가상 컴퓨터에 대 한 대기 합니다. 
   tootest 논리 앱 toohello 다음 섹션은 계속 진행 합니다.

## <a name="test-your-logic-app-workflow"></a>논리 앱 워크플로 테스트

1. 논리 앱 hello 하다는 toocheck 지정 된 이벤트, 가상 컴퓨터를 업데이트 합니다. 

   예를 들어 hello Azure 포털에서에서 가상 컴퓨터를 조정할 수 있습니다 또는 [Azure PowerShell을 사용한 VM의 크기를 조정](../virtual-machines/windows/resize-vm.md)합니다. 

   몇 분 후에 전자 메일을 받아야 합니다. 예:

   ![가상 컴퓨터 업데이트에 대한 전자 메일](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. tooreview hello를 실행 하 고 논리 앱 메뉴에서 논리 앱에 대 한 트리거 기록을 선택 **개요**합니다. 실행에 대 한 자세한 내용은 tooview 실행에 대 한 hello 행을 선택 합니다.

   ![논리 앱 실행 기록](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. tooview hello 입 / 출력 각 단계에 대 한 tooreview hello 단계를 확장 합니다. 이 정보는 논리 앱의 문제를 진단하고 디버깅하는 데 유용합니다.
 
   ![논리 앱 실행 기록 세부 정보](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

축하합니다! Event Grid를 통해 리소스 이벤트를 모니터링하고 이러한 이벤트가 발생하면 전자 메일을 보내는 논리 앱을 만들고 실행했습니다. 또한 프로세스를 자동화하고 시스템과 클라우드 서비스를 통합하는 워크플로를 쉽게 만들 수 있는 방법에 대해 알아보았습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서에서는 리소스를 사용하고 Azure 구독에 요금을 부과하는 작업을 수행합니다. 따라서 hello 자습서 및 테스트을 마친 경우 사용 하지 않도록 설정 하거나 tooincur 요금 않도록 하려는 모든 리소스를 삭제 하면 있는지 확인 합니다.

논리 앱을 실행 하 고 hello 앱을 삭제 하지 않고 전자 메일을 보내기에서 중지할 수 있습니다. 논리 앱 메뉴에서 **개요**를 선택합니다. Hello 도구 모음에서 선택 **사용 하지 않도록 설정**합니다.

![논리 앱 사용 해제](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>FAQ

**Q**: Event Grid 및 논리 앱으로 수행할 수 있는 다른 가상 컴퓨터 모니터링 작업은 무엇인가요? </br>
**A**: 다음과 같이 다른 구성 변경 내용을 모니터링할 수 있습니다.

* 가상 컴퓨터에서 RBAC(역할 기반 액세스 제어) 권한을 가져옵니다.
* 변경 내용이 tooa NSG 네트워크 보안 그룹 () (NIC) 네트워크 인터페이스에 적용 합니다.
* 가상 컴퓨터용 디스크가 추가되거나 제거되었습니다.
* 공용 IP 주소를 가상 컴퓨터 NIC. tooa 할당

## <a name="next-steps"></a>다음 단계

* [Event Grid 개요](../event-grid/overview.md)
* [Event Grid 개념](../event-grid/concepts.md)
* [빠른 시작: Event Grid로 사용자 지정 이벤트 만들기 및 라우팅](../event-grid/custom-event-quickstart.md)
* [Event Grid 이벤트 스키마](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [미리 정의된 템플릿을 사용하여 논리 앱 워크플로 만들기](../logic-apps/logic-apps-use-logic-app-templates.md)