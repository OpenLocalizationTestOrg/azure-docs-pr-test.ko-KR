---
title: "Azure 자동화에서 첫 번째 그래픽 runbook aaaMy | Microsoft Docs"
description: "Hello 개발, 테스트 하 고 간단한 그래픽 runbook의 게시 하는 과정을 안내 하는 자습서입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, runbook 템플릿, runbook 자동화, azure runbook"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>내 첫 번째 그래픽 Runbook

> [!div class="op_single_selector"]
> * [그래픽](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell 워크플로](automation-first-runbook-textual.md)
> 
> 

이 자습서에서는 hello 만드는 과정을 [그래픽 runbook](automation-runbook-types.md#graphical-runbooks) Azure 자동화에서 합니다.  테스트 하 고 tootrack hello runbook 작업의 상태를 hello 하는 방법을 설명 하는 동안 게시 하는 단순한 runbook으로 시작 합니다.  다음 hello runbook을 수정 했습니다 tooactually이 경우에 Azure 가상 컴퓨터를 시작 하는 Azure 리소스를 관리 합니다.  그러면 hello 자습서 runbook 매개 변수 및 조건부 링크를 추가 하 여 hello runbook 보다 강력한 하 여 완료 합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 필요 합니다.

* 동작합니다.  계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.
* [Azure 자동화 계정](automation-sec-configure-azure-runas-account.md) toohold runbook hello 및 tooAzure 리소스를 인증 합니다.  이 계정은 권한 toostart 있고 hello 가상 컴퓨터를 중지 해야 합니다.
* Azure 가상 컴퓨터.  프로덕션이 되지 않게하기 위해 이 가상 컴퓨터를 중지하고 시작합니다.

## <a name="step-1---create-runbook"></a>1단계 - Runbook 만들기
Hello 텍스트를 출력 하는 단순한 runbook을 만들어 시작 *Hello World*합니다.

1. Hello Azure 포털에서에서 자동화 계정을 엽니다.  
   hello 자동화 계정 페이지에서이 계정을 hello 리소스의 빠른 보기를 제공합니다.  사용자는 일부 자산이 이미 있어야 합니다.  그 중 대부분은 hello 모듈 새 자동화 계정에 자동으로 포함 됩니다.  Hello에 나와 있는 hello 자격 증명 자산 있어야 [필수 구성 요소](#prerequisites)합니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.<br> ![Runbook 컨트롤](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Hello를 클릭 하 여 새 runbook을 만들려면 **runbook을 추가할** 단추 차례로 **새 runbook을 만들**합니다.
4. Runbook hello 이름을 hello *MyFirstRunbook 그래픽*합니다.
5. 이 예에서 여기 toocreate는 [그래픽 runbook](automation-graphical-authoring-intro.md) 선택 **그래픽** 에 대 한 **Runbook 형식**합니다.<br> ![새 runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. 클릭 **만들기** toocreate hello runbook 및 열기 hello 그래픽 편집기입니다.

## <a name="step-2---add-activities-toohello-runbook"></a>2 단계-활동 toohello runbook 추가
hello hello hello 편집기의 왼쪽에는 라이브러리 제어 tooselect 활동 tooadd tooyour runbook을 허용 합니다.  Tooadd 여기는 **Write-output** hello runbook에서 cmdlet toooutput 텍스트입니다.

1. Hello 검색 텍스트 상자 및 형식 라이브러리 제어 hello 클릭 **Write-output**합니다.  hello 검색 결과 아래 표시 됩니다. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Toohello hello 목록 맨 아래로 스크롤하십시오.  오른쪽 단추로 클릭 하면 **Write-output** 선택 **toocanvas 추가** hello 타원 다음 toohello cmdlet을 클릭 한 다음 선택 또는 **toocanvas 추가**합니다.
3. Hello 클릭 **Write-output** hello 캔버스에서 작업 합니다.  Tooconfigure hello 활동 수 있는 hello 구성 제어 블레이드가 열립니다.
4. hello **레이블** toohello hello cmdlet 이름 기본값만 toosomething 더 친숙 한 변경할 수 있습니다. 속성을 변경할*Hello World 쓰기 toooutput*합니다.
5. 클릭 **매개 변수** tooprovide hello cmdlet의 매개 변수 값입니다.  
   일부 cmdlet 여러 매개 변수 집합 있는데이 하 한 toouse tooselect 필요 합니다. 이 경우 **Write-output** tooselect 하나 필요 하지 하나의 매개 변수를 설정 했습니다. <br> ![쓰기 출력 속성](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. 선택 hello **InputObject** 매개 변수입니다.  Hello 텍스트 toosend toohello 출력 스트림에 지정 hello 매개 변수입니다.
7. Hello에 **데이터 소스** 드롭다운 **PowerShell 식을**합니다.  hello **데이터 원본** 드롭다운 여러 원본을 제공 toopopulate 매개 변수 값을 사용 하 여 합니다.  
   다른 활동, 자동화 자산, 혹은 Power Shell식 같은 특정 소스들로부터 출력을 사용할 수 있습니다.  이 경우 원하는 toooutput hello 텍스트 *Hello World*합니다. PowerShell 식을 사용하고 문자열을 지정할 수 있습니다.
8. Hello에 **식** 상자에서 입력 *"Hello World"* 클릭 하 고 **확인** tooreturn toohello 캔버스에 두 번입니다.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. 클릭 하 여 hello runbook을 저장 **저장**합니다.<br> ![Runbook을 저장 합니다.](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>3 단계-hello runbook 테스트
Hello runbook toomake를 게시 하기 전에 것 tootest 원하는 프로덕션 환경에서 사용할 수 있는 것 toomake 제대로 작동 합니다.  Runbook을 테스트할 때 **초안** 버전을 실행하고 해당 출력을 대화형으로 봅니다.

1. 클릭 **테스트 창** tooopen hello 테스트 블레이드입니다.<br> ![테스트 창](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. 클릭 **시작** toostart hello 테스트 합니다.  이 경우에 사용할 수는 hello 옵션 이어야 합니다.
3. A [runbook 작업](automation-runbook-execution.md) 만들어집니다 및 서버 인스턴스의 상태 hello 창에 표시 합니다.  
   작업 상태 hello로 시작 *큐 대기* hello 클라우드 toobecome 사용할 수 있는에 runbook worker를 대기 하 고 있음을 나타내는입니다.  그런 다음 이동 너무*시작* 작업자 hello 작업 요구 한 경우 다음 *실행* hello runbook 실제로 실행을 시작한 경우.  
4. Hello runbook 작업이 완료 되 면 해당 출력이 표시 됩니다. 여기서는 *Hello World*할 수 있습니다.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Hello 테스트 블레이드 tooreturn toohello 캔버스를 닫습니다.

## <a name="step-4---publish-and-start-hello-runbook"></a>4 단계-게시 하 고 hello runbook을 시작
만든 hello runbook 초안 모드입니다. Toopublish 필요 전에 프로덕션 환경에서 실행할 수 있습니다.  Runbook을 게시 하는 경우 hello 초안 버전으로 hello 기존의 게시 된 버전을 덮어씁니다.  경우에에서는 없는 게시 됨 버전 hello runbook 방금 만든 때문에 있습니다.

1. 클릭 **게시** toopublish hello runbook 차례로 **예** 대화 상자가 나타나면 합니다.<br> ![게시](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Hello에 왼쪽된 tooview hello runbook 스크롤하면 **Runbook** 블레이드를 표시 한 **작성 상태** 의 **게시 됨**합니다.
3. 에 대 한 스크롤 백 toohello 오른쪽 tooview hello 블레이드 **MyFirstRunbook**합니다.  
   hello hello 위쪽 옵션 toostart hello runbook 수 있도록 허용 hello 미래에 toostart 예약 하거나, 한 [webhook](automation-webhooks.md) 시작 될 수 있도록 HTTP 호출을 통해.
4. Toostart hello runbook 원하는 이므로 클릭 **시작** 차례로 **예** 대화 상자가 나타나면 합니다.<br> ![Runbook 시작](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. 만든 hello runbook 작업에 대 한 작업 블레이드가 열립니다.  이 블레이드를 닫을 수 있습니다 하지만 경우에서는 열어 둔 채로 म hello 작업의 진행 상황을 볼 수 있도록.
6. hello 작업 상태에 표시 되어 **작업 요약** 및 일치 hello 상태는 hello runbook을 테스트 했습니다에 대해 살펴보았습니다.<br> ![작업 요약](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. 한 번 runbook 상태 표시를 hello *Completed*, 클릭 **출력**합니다. hello **출력** 블레이드가 열리며 볼 수 있습니다이 *Hello World* hello 창에서.<br> ![작업 요약](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. 닫기 hello 출력 블레이드입니다.
9. 클릭 **모든 로그** tooopen hello 스트림 블레이드 hello runbook 작업에 대 한 합니다.  에서는 행만 볼 *Hello World* hello 출력에서 스트림에 하지만이 표시할 수 있습니다 Verbose 및 오류와 같은 runbook 작업에 대 한 다른 스트림을 hello runbook toothem에 씁니다.<br> ![작업 요약](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. 모든 로그 블레이드 hello 및 hello 작업 블레이드 tooreturn toohello MyFirstRunbook 블레이드를 닫습니다.
11. 클릭 **작업** tooopen hello 작업 블레이드가이 runbook에 대 한 합니다.  이 runbook에서 만든 모든 hello 작업을 나열 합니다. म만 했습니다 hello 작업이 한 번 나열 되는 하나의 작업만 나타나야 합니다.<br> ![작업](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. 이 작업을 클릭할 수 있는 tooopen hello hello runbook을 시작 했습니다. 있을 때 볼에서는 동일한 작업 창.  이렇게 하면 있습니다 toogo 다시 특정 runbook에 대해 만들어진 모든 작업의 시간과 보기 hello 세부 있습니다.

## <a name="step-5---create-variable-assets"></a>5 단계 - 변수 자산 만들기
지금까지 runbook을 테스트 하고 게시했지만, 딱히 유용하지는 않습니다. Azure 리소스를 관리 하는 toohave 주시기 바랍니다.  Hello runbook tooauthenticate를 구성 하기 전에 변수 toohold hello 구독 ID를 만든 하 아래 6 단계에서 hello 활동 tooauthenticate을 설정 하 여 후 참조.  참조 toohello 구독 컨텍스트를 비롯 한 여러 구독 간에 tooeasily 작업이 있습니다.  계속 하기 전에 hello 구독 옵션을 해제 hello 탐색 창에서에서 구독 ID를 복사 합니다.  

1. Hello 자동화 계정을 블레이드에서 hello 클릭 **자산** 타일 및 hello **자산** 블레이드가 열립니다.
2. Hello 자산 블레이드에서 hello 클릭 **변수** 바둑판식으로 배열입니다.
3. Hello 변수 블레이드에서 클릭 **변수 추가**합니다.<br>![자동화 변수](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. Hello 새 변수 블레이드에서 hello에 **이름** 상자에 입력 **AzureSubscriptionId** 및 hello **값** 상자 구독 ID를 입력  유지 *문자열* hello에 대 한 **형식** 및 hello에 대 한 기본값 **암호화**합니다.  
5. 클릭 **만들기** toocreate hello 변수입니다.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>6 단계-인증 toomanage 추가 Azure 리소스
우리의 구독 ID 변수 toohold을 만들었으므로 이제 해당 구성 하 여 우리의 runbook tooauthenticate hello 계정으로 실행 되는 자격 증명 참조 tooin hello와 [필수 구성 요소](#prerequisites)합니다.  Hello Azure 계정으로 실행 연결을 추가 하 여 할까요 **자산** 및 **추가 AzureRMAccount** cmdlet toohello 캔버스입니다.  

1. 클릭 하 여 그래픽 편집기 열기 hello **편집** hello MyFirstRunbook 블레이드에서 합니다.<br> ![Runbook 편집](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Hello 필요 하지 않으므로 **작성 하는 Hello World toooutput** 더 이상 이므로 마우스 선택 **삭제**합니다.
3. Hello 라이브러리 컨트롤, 확장 **연결** 추가 **AzureRunAsConnection** 선택 하 여 toohello 캔버스 **toocanvas 추가**합니다.
4. Hello 캔버스에서 선택 **AzureRunAsConnection** hello 구성 컨트롤 창에서 입력 **실행으로 연결 가져오기** hello에 **레이블** 텍스트 상자에 붙여넣습니다.  이 hello 연결
5. Hello 라이브러리 컨트롤에에서 입력 **추가 AzureRmAccount** hello 검색 텍스트 상자에 있습니다.
6. 추가 **추가 AzureRmAccount** toohello 캔버스입니다.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. 위로 마우스를 가져가고 **실행으로 연결 가져오기** 원 hello hello 셰이프의 하단에 나타날 때까지 합니다. Hello 원을 클릭 하 고 너무 hello 화살표를 끌어**추가 AzureRmAccount**합니다.  만든 hello 화살표는는 *링크*합니다.  hello runbook에서 시작 **실행으로 연결 가져오기** 후 실행 **추가 AzureRmAccount**합니다.<br> ![활동 간 링크 만들기](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Hello 캔버스에서 선택 **추가 AzureRmAccount** hello 구성 제어 창 유형 및 **로그인 tooAzure** hello에 **레이블** 텍스트 상자에 붙여넣습니다.
9. 클릭 **매개 변수** hello 작업 매개 변수 구성 블레이드 나타납니다.
10. **추가 AzureRmAccount** 여러 매개 변수 집합에는 매개 변수 값이 제공 수 전에 하나 tooselect 필요 없으므로 합니다.  클릭 **매개 변수 설정** 선택한 후 hello **ServicePrincipalCertificatewithSubscriptionId** 매개 변수 집합입니다.
11. Hello 매개 변수 집합을 선택 하면 hello 작업 매개 변수 구성 블레이드에서 hello 매개 변수가 표시 됩니다.  **APPLICATIONID**를 클릭합니다.<br> ![Azure RM 계정 매개 변수 추가](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Hello 매개 변수 값 블레이드에서 선택 **활동 출력** hello에 대 한 **데이터 소스** 선택 **실행으로 연결 가져오기** hello 목록 hello에서 **필드 경로** textbox 형식 **ApplicationId**, 클릭 하 고 **확인**합니다.  Hello 활동 여러 속성을 가진 개체를 출력 하기 때문에 hello 필드 경로 대 한 hello 속성의 hello 이름을 지정 하는 것입니다.
13. 클릭 **CERTIFICATETHUMBPRINT**, hello 매개 변수 값 블레이드에서 선택 **활동 출력** hello에 대 한 **데이터 소스**합니다.  선택 **실행으로 연결 가져오기** hello 목록 hello에서 **필드 경로** textbox 형식 **CertificateThumbprint**, 클릭 하 고 **확인**합니다.
14. 클릭 **SERVICEPRINCIPAL**, hello 매개 변수 값 블레이드에서 선택 **ConstantValue** hello에 대 한 **데이터 소스**, hello 옵션을 클릭 **True**, 클릭 하 고 **확인**합니다.
15. 클릭 **TENANTID**, hello 매개 변수 값 블레이드에서 선택 **활동 출력** hello에 대 한 **데이터 소스**합니다.  선택 **실행으로 연결 가져오기** hello 목록 hello에서 **필드 경로** textbox 형식 **TenantId**, 클릭 하 고 **확인** 두 번입니다.  
16. Hello 라이브러리 컨트롤에에서 입력 **집합 AzureRmContext** hello 검색 텍스트 상자에 있습니다.
17. 추가 **집합 AzureRmContext** toohello 캔버스입니다.
18. Hello 캔버스에서 선택 **집합 AzureRmContext** hello 구성 제어 창 유형 및 **구독 Id를 지정** hello에 **레이블** 텍스트 상자에 붙여넣습니다.
19. 클릭 **매개 변수** hello 작업 매개 변수 구성 블레이드 나타납니다.
20. **집합 AzureRmContext** 여러 매개 변수 집합에는 매개 변수 값이 제공 수 전에 하나 tooselect 필요 없으므로 합니다.  클릭 **매개 변수 설정** 선택한 후 hello **SubscriptionId** 매개 변수 집합입니다.  
21. Hello 매개 변수 집합을 선택 하면 hello 작업 매개 변수 구성 블레이드에서 hello 매개 변수가 표시 됩니다.  **SubscriptionID**
22. Hello 매개 변수 값 블레이드에서 선택 **변수 자산** hello에 대 한 **데이터 소스** 선택 **AzureSubscriptionId** hello 목록에서 **확인**  두 번입니다.   
23. 위로 마우스를 가져가고 **로그인 tooAzure** 원 hello hello 셰이프의 하단에 나타날 때까지 합니다. Hello 원을 클릭 하 고 너무 hello 화살표를 끌어**구독 Id를 지정**합니다.

Runbook은 hello이 시점에서 다음 같이 표시 됩니다. <br>![Runbook 인증 구성](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>7 단계-활동 toostart 가상 컴퓨터를 추가 합니다.
추가 여기는 **시작 AzureRmVM** 활동 toostart 가상 컴퓨터.  선택 하면 모든 가상 컴퓨터 및 Azure 구독에서 이제 hello cmdlet에 이름을 지정 하는 하드 코드.

1. Hello 라이브러리 컨트롤에에서 입력 **시작 AzureRm** hello 검색 텍스트 상자에 있습니다.
2. 추가 **시작 AzureRmVM** toohello 캔버스 다음 클릭 하 고 아래 창으로 놓습니다 **구독 Id를 지정**합니다.
3. 위로 마우스를 가져가고 **구독 Id를 지정** 원 hello hello 셰이프의 하단에 나타날 때까지 합니다.  Hello 원을 클릭 하 고 너무 hello 화살표를 끌어**시작 AzureRmVM**합니다.
4. **Start-AzureRmVM**을 선택합니다.  클릭 **매개 변수** 차례로 **매개 변수 설정** tooview hello에 대 한 설정 **시작 AzureRmVM**합니다.  선택 hello **ResourceGroupNameParameterSetName** 매개 변수 집합입니다. **ResourceGroupName** 및 **이름** 옆에는 느낌표가 있습니다.  이것은 매개 변수가 필요하다는 것을 나타냅니다.  또한, 양 쪽 모두에 문자열 값이 필요합니다.
5. **Name**을 선택합니다.  선택 **PowerShell 식을** hello에 대 한 **데이터 소스** 가장 먼저이 runbook 큰따옴표로 hello 가상 컴퓨터의 hello 이름 입력 합니다.  **확인**을 클릭합니다.<br>![Start-AzureRmVM 이름 매개 변수 값](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. **ResourceGroupName**을 선택합니다. 사용 하 여 **PowerShell 식을** hello에 대 한 **데이터 소스** 큰따옴표로 hello 리소스 그룹의 hello 이름 입력 합니다.  **확인**을 클릭합니다.<br> ![Start-AzureRmVM 매개 변수](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. 테스트 창을 클릭 하 여 hello runbook을 테스트할 수 있습니다.
8. 클릭 **시작** toostart hello 테스트 합니다.  완료 되 면 해당 hello 가상 컴퓨터가 시작 된 확인 합니다.

Runbook은 hello이 시점에서 다음 같이 표시 됩니다. <br>![Runbook 인증 구성](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>8 단계-toohello runbook 추가 입력된 매개 변수를 추가 합니다.
이 runbook hello에 지정한 기 hello 리소스 그룹에 현재 hello 가상 컴퓨터를 시작 **시작 AzureRmVM** cmdlet.  이 runbook은 더 경우 유용할 수 hello runbook이 시작 될 때 둘 다 지정할 수 있습니다.  입력된 매개 변수 toohello runbook tooprovide 기능을 하는 지금 추가합니다.

1. 클릭 하 여 그래픽 편집기 열기 hello **편집** hello에 **MyFirstRunbook** 창.
2. 클릭 **입력 및 출력** 차례로 **입력 추가** tooopen hello Runbook 입력 매개 변수 창.<br> ![Runbook 입력 및 출력](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. 지정 *VMName* hello에 대 한 **이름**합니다.  유지 *문자열* hello에 대 한 **형식**을 변경 하지만 **필수** 너무*예*합니다.  **확인**을 클릭합니다.
4. 라는 두 번째 필수 입력된 매개 변수를 만들 *ResourceGroupName* 클릭 하 고 **확인** tooclose hello **입력 및 출력** 창.<br> ![Runbook 입력 매개 변수](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. 선택 hello **시작 AzureRmVM** 활동과 클릭 **매개 변수**합니다.
6. 변경 hello **데이터 소스** 에 대 한 **이름** 너무**Runbook 입력** 선택한 후 **VMName**합니다.<br>
7. 변경 hello **데이터 소스** 에 대 한 **ResourceGroupName** 너무**Runbook 입력** 선택한 후 **ResourceGroupName**합니다.<br> ![Start-azurevm 매개 변수](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Hello runbook을 저장 하 고 hello 테스트 창을 엽니다.  Note 이제를 제공할 수 있습니다 값 hello에 대 한 hello 테스트에서 사용 하는 두 개의 입력된 변수입니다.
9. 닫기 hello 테스트 창입니다.
10. 클릭 **게시** toopublish hello hello runbook의 새 버전입니다.
11. Hello 이전 단계에서 시작 하는 hello 가상 컴퓨터를 중지 합니다.
12. 클릭 **시작** toostart hello runbook입니다.  Hello 입력 **VMName** 및 **ResourceGroupName** toostart 거 hello 가상 컴퓨터에 대 한 합니다.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Hello runbook이 완료 되 면 해당 hello 가상 컴퓨터가 시작 된 확인 합니다.

## <a name="step-9---create-a-conditional-link"></a>9 단계 - 조건부 링크 만들기
에서는 아직 시작 되지 않은 경우 toostart hello 가상 컴퓨터만 시도 되도록 hello runbook 지금 수정 합니다.  추가 하 여이 작업을 수행는 **Get AzureRmVM** cmdlet toohello runbook이 hello hello 가상 컴퓨터의 인스턴스 수준 상태를 가져옵니다. 다음 호출 하는 PowerShell 워크플로 코드 모듈 추가 **상태 가져오기** hello 가상 컴퓨터 상태는 실행 또는 중지 하는 경우 코드 toodetermine powershell 코드 조각을 사용 합니다.  Hello에서 조건부 링크 **상태 가져오기** 모듈에만 실행 **시작 AzureRmVM** hello 현재 실행 상태를 중지 합니다.  마지막으로, PowerShell Write-output cmdlet hello VM 성공적으로 시작 되었거나 사용 하지 여부 hello 메시지 tooinform을 출력 했습니다.

1. 열기 **MyFirstRunbook** hello 그래픽 편집기에서.
2. 사이의 hello 연결 제거 **구독 Id를 지정** 및 **시작 AzureRmVM** 클릭 하 고 다음 hello 키를 눌러 *삭제* 키입니다.
3. Hello 라이브러리 컨트롤에에서 입력 **Get AzureRm** hello 검색 텍스트 상자에 있습니다.
4. 추가 **Get AzureRmVM** toohello 캔버스입니다.
5. 선택 **Get AzureRmVM** 차례로 **매개 변수 설정** tooview hello에 대 한 설정 **Get AzureRmVM**합니다.  선택 hello **GetVirtualMachineInResourceGroupNameParamSet** 매개 변수 집합입니다.  **ResourceGroupName** 및 **이름** 옆에는 느낌표가 있습니다.  이것은 매개 변수가 필요하다는 것을 나타냅니다.  또한, 양 쪽 모두에 문자열 값이 필요합니다.
6. **이름**에 대한 **데이터 원본**에서 **Runbook 입력**을 선택한 다음 **VMName**을 선택합니다.  **확인**을 클릭합니다.
7. **ResourceGroupName**에 대한 **데이터 원본**에서 **Runbook 입력**을 선택한 다음 **ResourceGroupName**을 선택합니다.  **확인**을 클릭합니다.
8. **상태**에 대한 **데이터 원본**에서 **상수 값**을 선택한 다음 **True**를 클릭합니다.  **확인**을 클릭합니다.  
9. 링크를 만들 **구독 Id를 지정** 너무**Get AzureRmVM**합니다.
10. Hello 라이브러리 제어 확장 **Runbook 컨트롤** 추가 **코드** toohello 캔버스입니다.  
11. 링크를 만들 **Get AzureRmVM** 너무**코드**합니다.  
12. 클릭 **코드** hello 구성 창에서 변경 레이블 너무**상태 가져오기**합니다.
13. 선택 **코드** 매개 변수 및 hello **코드 편집기** 블레이드 나타납니다.  
14. Hello 코드 편집기에서 다음 코드 조각 hello를 붙여 넣습니다.
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. 링크를 만들 **상태 가져오기** 너무**시작 AzureRmVM**합니다.<br> ![코드 모듈과 Runbook](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Hello 링크를 선택 하 고 hello 구성 창에서 변경 **조건을 적용** 너무**예**합니다.   참고 hello 링크는 hello 대상 활동 hello 상황이 tootrue 해결 하는 경우에 실행을 나타내는 tooa 파선 선으로를 바뀝니다.  
17. Hello에 대 한 **식 조건**, 형식 *$ActivityOutput [' 상태 가져오기 ']-eq "Stopped"*합니다.  **시작 AzureRmVM** hello 가상 컴퓨터가 중지 된 경우 이제만 실행 합니다.
18. Hello 라이브러리 컨트롤, 확장 **Cmdlet** 차례로 **Microsoft.PowerShell.Utility**합니다.
19. 추가 **Write-output** toohello 캔버스를 두 번입니다.<br> ![쓰기 출력으로 Runbook](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Hello에 첫 번째 **Write-output** 컨트롤을 클릭 하 여 **매개 변수** hello 변경 **레이블** 너무 값*VM 시작 알릴*합니다.
21. 에 대 한 **InputObject**, 변경 **데이터 소스** 너무**PowerShell 식을** hello 식 입력 *"$VMName 성공적으로 시작 합니다."* .
22. Hello에 두 번째 **Write-output** 컨트롤을 클릭 하 여 **매개 변수** hello 변경 **레이블** 너무 값*알림 VM을 시작 하지 못했습니다.*
23. 에 대 한 **InputObject**, 변경 **데이터 소스** 너무**PowerShell 식을** hello 식 입력 *"$VMName 시작 하지 못했습니다."* .
24. 링크를 만듭니다 **시작 AzureRmVM** 너무**VM 시작 알릴** 및 **알림 VM을 시작 하지 못했습니다**합니다.
25. 너무 hello 링크를 선택**VM 시작 알릴** 변경 **조건을 적용** 너무**True**합니다.
26. Hello에 대 한 **식 조건**, 형식 *$ActivityOutput ['AzureRmVM 시작 ']. IsSuccessStatusCode-eq $true*합니다.  이 Write-output hello 가상 컴퓨터가 성공적으로 시작 하는 경우 이제 실행을 제어 합니다.
27. 너무 hello 링크를 선택**알림 VM을 시작 하지 못했습니다** 변경 **조건을 적용** 너무**True**합니다.
28. Hello에 대 한 **식 조건**, 형식 *$ActivityOutput ['AzureRmVM 시작 ']. IsSuccessStatusCode-ne $true*합니다.  이 쓰기 출력 제어 hello 가상 컴퓨터가 성공적으로 시작 되지 않은 경우 실행만 사용 합니다.
29. Hello runbook을 저장 하 고 hello 테스트 창을 엽니다.
30. Hello 가상 컴퓨터 중지와 hello runbook을 시작 하 고 시작 해야 합니다.

## <a name="next-steps"></a>다음 단계
* 그래픽 작성에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)
* PowerShell runbook 시작 tooget 참조 [내 첫 번째 PowerShell runbook](automation-first-runbook-textual-powershell.md)
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)

