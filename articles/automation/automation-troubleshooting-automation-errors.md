---
title: "일반적인 Azure 자동화 발급 aaaTroubleshooting | Microsoft Docs"
description: "이 문서에서는 설명 toohelp 문제를 해결 하 고 일반적인 Azure 자동화 오류를 해결 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "자동화 오류, 문제 해결, 문제"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Azure Automation이 일반적인 문제 해결 
이 문서에서는 Azure 자동화에서 발생할 수 있습니다 및 가능한 해결 방법을 tooresolve 제안 하는 일반적인 오류 문제 해결 도움말을 제공 하 합니다.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Azure 자동화 Runbook을 사용할 때 인증 오류
### <a name="scenario-sign-in-tooazure-account-failed"></a>시나리오: tooAzure 하지 못했습니다. 계정에 로그인
**오류:** 때 오류가 발생 hello "Unknown_user_type:: 알 수 없는 사용자 유형" hello Add-azureaccount 또는 로그인 AzureRmAccount cmdlet 작업.

**Hello 오류에 대 한 이유:** hello 자격 증명 자산 이름은 유효 하지 않거나 경우 hello 사용자 이름 및 암호 toosetup hello 자동화 자격 증명 자산을 사용 하는 유효 하지 않음 경우이 오류가 발생 합니다.

**문제 해결 팁:** 에 무엇이 잘못 toodetermine 순서, hello 다음 단계를 수행 합니다.  

1. Hello 등의 특수 문자가 없는지 확인  **@**  tooconnect tooAzure를 사용 하는 hello 자동화 자격 증명 자산 이름에 문자입니다.  
2. Hello 사용자 이름 및 암호 로컬 PowerShell ISE 편집기에서 hello Azure 자동화 자격 증명에 저장 된 사용할 수 있는지 확인 합니다. Hello cmdlet hello PowerShell ISE에서에서 다음을 실행 하 여이 수행할 수 있습니다.  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. 인증이 로컬에서 실패하면 Azure Active Directory 자격 증명을 올바르게 설정하지 않았다는 뜻입니다. 너무 참조[tooAzure Azure Active Directory를 사용 하 여 인증](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) 블로그 게시물 tooget hello Azure Active Directory 계정 정확 하 게 설정 합니다.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>시나리오: 수 없습니다 toofind hello Azure 구독
**오류:** hello 오류 "라는 구독 hello ``<subscription name>`` 찾을 수 없습니다" hello Select-azuresubscription 또는 선택 AzureRmSubscription cmdlet을 사용 합니다.

**Hello 오류에 대 한 이유:** hello 구독 이름이 올바르지 않거나 hello Azure Active Directory 사용자에 게 tooget hello 구독 세부 정보 hello 구독 관리자로 구성 되지 않은 경우이 오류가 발생 합니다.

**문제 해결 팁:** 순서로 toodetermine tooAzure 제대로 인증 된 액세스 toohello 구독 tooselect, 고치려는 있는 경우 수행할 단계를 수행 하는 hello:  

1. Hello 실행 **Add-azureaccount** hello를 실행 하기 전에 **Select-azuresubscription** cmdlet.  
2. 이 오류 메시지가 계속 나타나면 hello를 추가 하 여 코드를 수정 **Get-azuresubscription** hello 다음 cmdlet **Add-azureaccount** cmdlet 후 hello 코드를 실행 합니다.  이제 Get-azuresubscription의 hello 출력 구독 정보를 포함 하는 경우를 확인 합니다.  

   * Hello 출력에 대 한 구독 세부 정보 표시 되지 않으면, 즉, hello 구독이 아직 초기화 되지 않습니다.  
   * Hello 출력에 hello 구독 세부 정보를 표시 되 면 hello 올바른 구독 이름 또는 ID hello로 사용 하는 확인 **Select-azuresubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>시나리오: 인증 tooAzure 다단계 인증을 사용 하기 때문에 실패 했습니다.
**오류:** hello 오류가 나타나면 "Add-azureaccount: AADSTS50079: 강력한 인증 등록 (증명 접속)가 필요" tooAzure Azure 사용자 이름과 암호로 인증할 때.

**Hello 오류에 대 한 이유:** Azure 계정에서 다단계 인증을 설정한 경우 Azure Active Directory 사용자 tooauthenticate tooAzure 사용할 수 없습니다.  대신, 인증서 또는 서비스 보안 주체 tooauthenticate tooAzure toouse 필요 합니다.

**문제 해결 팁:** toouse hello Azure 서비스 관리 cmdlet으로 인증서 참조 너무[만들고 추가 인증서 toomanage Azure 서비스입니다.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) Azure 리소스 관리자 cmdlet이 포함 된 서비스 사용자 toouse 너무 참조[주 Azure 포털을 사용 하 여 서비스를 만드는](../azure-resource-manager/resource-group-create-service-principal-portal.md) 및 [Azure 리소스 관리자와 서비스 사용자를 인증 합니다.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Runbook을 사용할 때 발생하는 일반적인 오류
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>시나리오: hello runbook 작업 시작을 세 번 시도 했습니다 하지만 toostart 때마다 실패
**오류:** runbook "" hello 작업이 세 번 시도 했지만 실패."hello 오류와 함께 실패

**Hello 오류에 대 한 이유:** hello 이유를 수행 하 여이 오류가 발생할 수 있습니다.  

1. 메모리 제한.  샌드박스 tooa 할당할 메모리 양을 제한 문서화 해야 우리 [자동화 서비스 제한](../azure-subscription-service-limits.md#automation-limits) 되므로 작업 400MB 개 이상의 메모리를 사용 하는 경우이 실패할 수 있습니다. 

2. 모듈이 호환되지 않음.  이는 모듈 종속성이 올바르지 않은 경우에 발생할 수 있으며 그렇지 않은 경우 일반적으로 Runbook은 "명령을 찾을 수 없습니다." 또는 "매개 변수를 바인드할 수 없습니다." 메시지를 반환합니다. 

**문제 해결 팁:** hello 문제가 해결 됩니다 hello 솔루션을 다음 중 하나:  

* 방법이 제안된 toowork hello 메모리 한도 내에서 여러 runbook 간에 toosplit hello 작업 부하는, 메모리, 불필요 한 출력에서 runbook toowrite에에서 많은 데이터를 처리 하지 또는 여 PowerShell에 쓸 수 검사점을 고려 워크플로 runbook입니다.  

* Hello 단계에 따라 tooupdate Azure 모듈 필요한 [어떻게 Azure 자동화에서 Azure PowerShell 모듈 tooupdate](automation-update-azure-modules.md)합니다.  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>시나리오: 역직렬화된 개체로 인해 Runbook 실패
**오류:** runbook hello 오류와 함께 실패 "매개 변수를 바인딩할 수 없습니다 ``<ParameterName>``합니다. Hello를 변환할 수 없습니다 ``<ParameterType>`` Deserialized 형식의 값 ``<ParameterType>`` tootype ``<ParameterType>``"입니다.

**Hello 오류에 대 한 이유:** PowerShell 워크플로 runbook을 사용 하는 경우 복잡 한 개체에에서 저장 순서 toopersist에서 역직렬화 된 형식 runbook 상태 hello 워크플로가 일시 중단 하는 경우.  

**문제 해결 팁:**  
이 문제가 해결 됩니다 hello 세 가지 솔루션이 다음 중 하나:

1. 하나의 cmdlet tooanother에서 복잡 한 개체를 파이프 하는 경우는 InlineScript의 이러한 cmdlet을 래핑하십시오.  
2. Hello hello 전체 개체를 전달 하는 대신 복잡 한 개체에서 필요한 hello 이름 또는 값을 전달 합니다.  
3. PowerShell 워크플로 Runbook 대신 PowerShell Runbook을 사용합니다.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>시나리오: Runbook 작업 hello 할당 할당량을 초과 하기 때문에 실패 했습니다.
**오류:** "hello 월간 총 작업 실행 시간에 대 한 hello 할당량에 도달 했습니다.이 구독에 대 한" runbook 작업 hello 오류와 함께 실패 합니다.

**Hello 오류에 대 한 이유:** 경우이 오류가 발생 hello 작업 실행 계정에 대 한 hello 500 분 무료 할당량을 초과 합니다. 이 할당량은 tooall 유형의 등의 작업을 테스트 hello 포털에서 작업을 시작 하거나 hello Azure 포털을 사용 하 여 또는 작업 tooexecute 일정 예약 및 webhook을 사용 하 여 작업을 실행 데이터 센터에서 작업 실행 태스크에 적용 됩니다. 자동화에 대 한 가격 책정에 대 한 자세한 참조 toolearn [자동화 가격 책정](https://azure.microsoft.com/pricing/details/automation/)합니다.

**문제 해결 팁:** 원하면 toouse 이상 500 분의 경우 구독 hello 무료 계층 toohello 기본 계층에서 한 달 toochange 해야 처리 합니다. 라인 hello 단계를 수행 하 여 toohello 기본 계층을 업그레이드할 수 있습니다.  

1. Azure 구독 tooyour에 로그인  
2. Tooupgrade 원하는 hello 자동화 계정을 선택 합니다.  
3. **설정** > **가격 책정 계층 및 사용 현황** > **가격 책정 계층**을 클릭합니다.  
4. Hello에 **가격 책정 계층 선택** 블레이드를 **기본**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>시나리오: Runbook을 실행해도 cmdlet이 인식되지 않음
**오류:** hello 오류로 인해 runbook 작업 실패 "``<cmdlet name>``: hello 용어 ``<cmdlet name>`` cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 hello 이름으로 인식 되지 않습니다."

**Hello 오류에 대 한 이유:** 이 오류는 hello PowerShell 엔진 runbook에서 사용 하는 hello cmdlet을 찾을 수 없을 때 발생 합니다.  Hello cmdlet을 포함 하는 hello 모듈 hello 계정에서 runbook 이름을 사용할 경우 이름이 충돌 하는 또는 hello cmdlet도 다른 모듈에 존재 하 고 자동화 hello 이름을 확인할 수 없는 때문일 수 있습니다.

**문제 해결 팁:** hello 문제가 해결 됩니다 hello 솔루션을 다음 중 하나:  

* Hello cmdlet 이름을 올바르게 입력 했는지 확인 합니다.  
* Hello cmdlet 자동화 계정에 존재 하며 충돌 되어 있는지 확인 합니다. hello cmdlet을 사용할 수 있으면 tooverify 편집 모드 hello cmdlet toofind hello 라이브러리에서 또는 실행에 대 한 검색에서 runbook을 열고 **Get-command ``<CommandName>``** 합니다.  Hello cmdlet 유효성 검사는 사용할 수 있는 toohello 계정이 고, 하 고 다른 cmdlet 이나 runbook와 이름이 충돌 하지 toohello 캔버스 추가 하 고 runbook에 설정 된 유효한 매개 변수를 사용 하 고 있는지 확인 합니다.  
* 이름 충돌이 있는 경우 hello cmdlet은 두 개의 서로 다른 모듈에서 사용할 수 있는 hello hello cmdlet에 대 한 정규화 된 이름을 사용 하 여이 해결할 수 있습니다. 예를 들어 **ModuleName\CmdletName**을 사용할 수 있습니다.  
* Hello runbook 온-프레미스 hybrid worker 그룹에서 실행 되는 다음 해당 hello 있는지 확인 하면 모듈/cmdlet hello 하이브리드 작업자를 호스팅하는 hello 컴퓨터에 설치 됩니다.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>시나리오: 장기 실행 runbook hello 예외와 함께 지속적으로 실패: "hello 작업 hello에서 반복적으로 제거 하기 때문에 실행을 계속할 수 없습니다 같은 검사점"입니다.
**Hello 오류에 대 한 이유:** 3 시간 보다 오래 실행 되는 경우 runbook를 자동으로 일시 중단 하는 Azure 자동화를 내에서 프로세스의 toohello "공평 분배" 모니터링 인해 의도 된 동작입니다. 그러나 반환 된 오류 메시지 "다음"을 제공 하지 않습니다 hello 옵션입니다. runbook은 다양한 이유로 일시 중단될 수 있습니다. 일시 중단을 발생 due tooerrors 대부분 합니다. 예를 들어, runbook, 네트워크 오류 또는 충돌을 확인할 수 없는 예외가 hello hello runbook을 실행 하는 Runbook Worker, 모든 hello runbook toobe 일시 중단 되며, 마지막 검사점 다시 시작 될 때 시작 합니다.

**문제 해결 팁:** hello 문서화 솔루션 tooavoid이이 문제는 워크플로의 toouse 검사점입니다.  너무 참조 더 toolearn[학습 PowerShell 워크플로](automation-powershell-workflow.md#checkpoints)합니다.  "공평 분배" 및 검사점에 대한 자세한 설명은 [Runbook에서 검사점 사용](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/) 블로그 문서에서 확인 수 있습니다.

## <a name="common-errors-when-importing-modules"></a>모듈을 가져올 때 발생하는 일반적인 오류
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>시나리오: 모듈이 실패할 tooimport 또는 가져온 다음 cmdlet을 실행할 수 없습니다.
**오류:** 모듈 tooimport 실패 하거나, 성공적으로 가져오는 있지만 cmdlet이 없어 추출 됩니다.

**Hello 오류에 대 한 이유:** 몇 가지 일반적인 이유는 모듈을 가져올 수 없습니다 성공적으로 tooAzure 자동화 됩니다.  

* hello 구조 hello 구조와 일치 하지 않기를 자동화 해야 하는 것에 toobe 합니다.  
* hello 모듈 배포 tooyour 자동화 계정이 되지 않은 다른 모듈에 종속 됩니다.  
* hello 모듈 hello 폴더에 종속성이 없습니다.  
* hello **새로 AzureRmAutomationModule** cmdlet를 사용 하는 tooupload hello 모듈 되 고 hello 전체 저장소 경로 제공 되지 않은 또는 공개적으로 액세스할 수 있는 URL을 사용 하 여 hello 모듈을 로드 되지 않았습니다.  

**문제 해결 팁:**  
Hello 문제가 해결 됩니다 hello 솔루션을 다음 중 하나:  

* 해당 hello 모듈 형식에 따라 hello 따르는지 확인 합니다.  
  ModuleName.Zip **->** 모듈 이름 또는 버전 번호 **->** (ModuleName.psm1, ModuleName.psd1)
* Hello.psd1 파일을 열고 hello 모듈 종속성에 있는지 확인 합니다.  그렇지 않으면 이러한 모듈 toohello 자동화 계정을 업로드 합니다.  
* 참조 된 모든.dll이 hello 모듈 폴더에 존재 하는지 확인 합니다.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>DSC(필요한 상태 구성)으로 작업하는 경우 일반적인 오류 문제
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>시나리오: 노드는 "찾을 수 없음" 오류로 실패한 상태
**오류:** hello 노드에 있는 보고서는 **실패** 상태 hello 오류를 포함 하 고 "hello 서버 https://에서 시도 tooget hello 작업``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction 때문에 실패 했습니다. 올바른 구성 ``<guid>`` 찾을 수 없습니다. "

**Hello 오류에 대 한 이유:** 이 일반적으로이 오류 발생 때 hello 노드가 tooa 구성 이름 (예: ABC) 노드 구성 이름 (예: ABC 대신 할당. 웹 서버)입니다.  

**문제 해결 팁:**  

* "노드 구성 이름은" hello "구성 이름이 아니라"와 hello 노드를 할당 하려는 있는지 확인 합니다.  
* Azure 포털 또는 PowerShell cmdlet을 사용 하 여 노드 구성 tooa 노드를 지정할 수 있습니다.

  * Azure 포털을 사용 하 여 노드 구성 tooa 노드 tooassign 주문에서 hello를 열고 **DSC 노드** 블레이드에서 다음 노드를 선택 하 고 클릭 **할당 노드 구성** 단추입니다.  
  * PowerShell cmdlet을 사용 하 여 노드 구성 tooa 노드 tooassign 순서에서 사용 하 여 **집합 AzureRmAutomationDscNode** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>시나리오: 구성이 컴파일될 때 생성된 노드 구성(mof 파일)이 없음
**오류:** hello 오류로 DSC 컴파일 작업을 일시 중단: "컴파일 완료 되었지만 없는 노드 구성.mofs 생성 되었습니다"입니다.

**Hello 오류에 대 한 이유:** hello 다음에 나오는 식을 때는 hello **노드** hello DSC 구성에 키워드 너무 계산 노드 구성이 만들어지지 것입니다. 그런 다음 $null입니다.    

**문제 해결 팁:**  
Hello 문제가 해결 됩니다 hello 솔루션을 다음 중 하나:  

* 해당 hello 식 다음 toohello 있는지 확인 **노드** 키워드 hello 구성 정의를 너무 평가 하지 않는 $null입니다.  
* Hello 예상 값을 전달 하 고 있는지 확인 ConfigurationData hello 구성을 컴파일할 때 전달 하는 경우 해당 hello 구성에서 필요한 [ConfigurationData](automation-dsc-compile.md#configurationdata)합니다.

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>시나리오: hello DSC 노드 보고서 "진행 중" 상태인 빠질
**오류:** DSC 에이전트는 "주어진 속성 값으로 인스턴스를 찾을 수 없음"을 출력합니다.

**Hello 오류에 대 한 이유:** WMF 버전 업그레이드 하 고 WMI가 손상 것 같습니다.  

**문제 해결 팁:** hello 지침 hello에 따라 [알려진 문제 및 제한 하는 DSC](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix hello 문제입니다.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>시나리오: 수 없습니다 toouse DSC 구성에서 자격 증명
**오류:** hello 오류로 일시 중단 된 DSC 컴파일 작업: "System.InvalidOperationException 오류 처리 '자격 증명' 형식의 속성 ``<some resource name>``: 변환 및 암호화 된 암호를 저장 하는 경우에 허용 되는 일반 텍스트 PSDscAllowPlainTextPassword 설정은 tootrue "합니다.

**Hello 오류에 대 한 이유:** 구성에서 자격 증명을 사용 했지만 적절 한 제공 하지 않았기 **ConfigurationData** tooset **PSDscAllowPlainTextPassword** 각 노드에 대해 tootrue 구성입니다.  

**문제 해결 팁:**  

* 적절 한 hello에 있는지 toopass 확인 **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue hello 구성에서 언급 한 각 노드의 구성에 대 한 합니다. 자세한 내용은 참조 너무[Azure 자동화 DSC에서 자산](automation-dsc-compile.md#assets)합니다.

## <a name="next-steps"></a>다음 단계
문제 해결 단계 위의 hello 따랐는지 hello 답변을 찾을 수 없습니다 하는 경우 아래 hello 추가 지원 옵션을 검토할 수 있습니다.

* Azure 전문가에게 도움을 받으세요. 문제 toohello 제출 [스택 오버플로 또는 Azure MSDN 포럼.](https://azure.microsoft.com/support/forums/)합니다.
* Azure 지원 인시던트 제출 Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 클릭 **지원을 받는** 아래 **기술 및 대금 청구 지원**합니다.
* Azure 자동화 Runbook 솔루션 또는 통합 모듈을 찾고 있는 경우 [스크립트 센터](https://azure.microsoft.com/documentation/scripts/) 에 스크립트 요청을 게시하세요.
* Azure 자동화에 대한 의견이나 기능 요청이 있으면 [사용자 의견](https://feedback.azure.com/forums/34192--general-feedback)에 게시하세요.
