---
title: "OMS 솔루션의 aaaAzure 자동화 리소스 | Microsoft Docs"
description: "OMS의 솔루션에서 수집 하 고 모니터링 데이터를 처리 하는 등의 Azure 자동화 tooautomate 프로세스 runbook 일반적으로 포함 됩니다.  이 문서에서는 설명 방법을 tooinclude runbook 및 관련된 해당 리소스에는 솔루션입니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Azure 자동화 리소스 tooan OMS 관리 솔루션 (미리 보기) 추가
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.   


[OMS의 관리 솔루션](operations-management-suite-solutions.md) 수집 하 고 모니터링 데이터를 처리 하는 등의 Azure 자동화 tooautomate 프로세스에는 일반적으로 runbook을 포함 합니다.  또한 toorunbooks, 자동화 계정을 사용 하는 hello runbook hello 솔루션에서 지원 되는 일정 및 변수와 같은 자산을 포함 합니다.  이 문서에서는 설명 방법을 tooinclude runbook 및 관련된 해당 리소스에는 솔루션입니다.

> [!NOTE]
> hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>필수 조건
이 문서는 익숙한 이미 hello 다음 정보를 가정 합니다.

- 어떻게 너무[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md)합니다.
- hello의 구조는 [솔루션 파일](operations-management-suite-solutions-solution-file.md)합니다.
- 어떻게 너무[리소스 관리자 템플릿을 작성](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Automation 계정
Azure Automation의 모든 리소스는 [Automation 계정](../automation/automation-security-overview.md#automation-account-overview)에 포함됩니다.  에 설명 된 대로 [OMS 작업 영역 및 자동화 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello 자동화 계정 hello 관리 솔루션에 포함 되어 있지 않지만 hello 솔루션을 설치 하기 전에 존재 해야 합니다.  사용할 수 없으면 hello 솔루션 설치 실패 합니다.

각 자동화 리소스의 hello 이름에는 자동화 계정 hello 이름이 포함합니다.  Hello 사용 하 여 hello 솔루션에서 이렇게 **accountName** hello 다음 runbook 리소스의 예제에서와 같이 매개 변수입니다.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbook
Hello 솔루션을 설치할 때 만들어질 수 있도록 hello 솔루션 파일에 hello 솔루션에서 사용 하는 모든 runbook을 포함 해야 합니다.  Hello runbook tooa 공용 위치 솔루션을 설치 하는 모든 사용자가 액세스할 수 있는 게시 해야 하므로 하지만 hello 서식 파일에서 hello runbook의 hello 본문을 포함할 수 없습니다.

[Azure 자동화 runbook](../automation/automation-runbook-types.md) 리소스 유형의 **Microsoft.Automation/automationAccounts/runbooks** 있고 hello 구조를 수행 합니다. 여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


runbook에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.

| 속성 | 설명 |
|:--- |:--- |
| runbookType |Hello runbook의 hello 유형을 지정합니다. <br><br> Script - PowerShell 스크립트 <br>PowerShell - PowerShell 워크플로 <br> GraphPowerShell - 그래픽 PowerShell 스크립트 runbook <br> GraphPowerShellWorkflow - 그래픽 PowerShell 워크플로 runbook |
| logProgress |지정 하는지 여부를 [진행률 레코드](../automation/automation-runbook-output-and-messages.md) hello runbook에 대 한 생성 해야 합니다. |
| logVerbose |지정 하는지 여부를 [상세 레코드](../automation/automation-runbook-output-and-messages.md) hello runbook에 대 한 생성 해야 합니다. |
| 설명 |Hello runbook에 대 한 선택적 설명입니다. |
| publishContentLink |Hello runbook의 hello 콘텐츠를 지정합니다. <br><br>uri-hello runbook의 Uri toohello 콘텐츠입니다.  이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.  <br> 버전-고유한 추적에 대 한 hello runbook의 버전입니다. |


## <a name="automation-jobs"></a>Automation 작업
Azure Automation에서 Runbook을 시작하면 자동화 작업이 만들어집니다.  Hello 관리 솔루션을 설치할 때 runbook 자동화 작업 리소스 tooyour 솔루션 tooautomatically 시작을 추가할 수 있습니다.  이 방법은 hello 솔루션의 초기 구성에 사용 되는 일반적으로 사용 되는 toostart runbook에 설명 합니다.  toostart 정기적으로 runbook 만들기는 [일정](#schedules) 및 [작업 일정](#job-schedules)

작업 리소스에는 형식이 **Microsoft.Automation/automationAccounts/jobs** 있고 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

다음 표에 hello 자동화 작업에 대 한 hello 속성 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| runbook |Hello runbook toostart의 hello 이름의 단일 이름 엔터티. |
| 매개 변수 |Hello runbook에 필요한 각 매개 변수 값에 대 한 엔터티. |

hello runbook 이름 및 toohello runbook 보낸 모든 매개 변수 값 toobe hello 작업에 포함 되어 있습니다.  hello 작업 해야 [의존](operations-management-suite-solutions-solution-file.md#resources) hello runbook부터 시작 하는 hello runbook hello 작업 보다 먼저 만들어야 합니다.  시작해야 하는 Runbook이 여러 개 있는 경우 작업을 먼저 실행해야 하는 다른 작업에 종속되게 하여 순서를 정의 할 수 있습니다.

작업 리소스의 hello 이름 매개 변수를 통해 일반적으로 할당 된 GUID를 포함 해야 합니다.  GUID 매개 변수에 대한 자세한 내용은 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-solution-file.md#parameters)를 참조하세요.  


## <a name="certificates"></a>인증서
[Azure 자동화 자격 증명](../automation/automation-certificates.md) 유형의 **Microsoft.Automation/automationAccounts/certificates** 있고 hello 구조를 수행 합니다. 여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



다음 표에 hello 인증서 리소스에 대 한 hello 속성 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| base64Value |Hello 인증서에 대 한 base 64 값입니다. |
| thumbprint |Hello 인증서에 대 한 지문입니다. |



## <a name="credentials"></a>자격 증명
[Azure 자동화 자격 증명](../automation/automation-credentials.md) 유형의 **Microsoft.Automation/automationAccounts/credentials** 있고 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

자격 증명 리소스에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.

| 속성 | 설명 |
|:--- |:--- |
| userName |Hello 자격 증명에 대 한 사용자 이름입니다. |
| 암호 |Hello 자격 증명에 대 한 암호입니다. |


## <a name="schedules"></a>일정
[Azure 자동화 일정](../automation/automation-schedules.md) 유형의 **Microsoft.Automation/automationAccounts/schedules** 있고 hello hello 구조를 수행 합니다. 여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

다음 표에 hello 일정 리소스에 대 한 hello 속성 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 설명 |Hello 일정에 대 한 선택적 설명입니다. |
| startTime |일정의 hello 시작 시간을 DateTime 개체로 지정합니다. 변환 된 tooa 수 있으면 문자열을 제공할 수 있습니다 유효한 날짜/시간입니다. |
| isEnabled |Hello 일정이 사용 되는지 여부를 지정 합니다. |
| interval |hello 형식 hello 일정에 대 한 간격입니다.<br><br>일<br>시간 |
| frequency |Hello 일정 빈도 (일) 또는 시간에 발생 해야 합니다. |

일정 시작 시간을 hello 보다 큰 값으로 현재 시간 여야 합니다.  진행 중인 toobe 설치 되었을 때를 알 수 없습니다 없으므로 변수로이 값을 제공할 수 없습니다.

Hello 솔루션의 일정 리소스를 사용할 때 두 가지 전략을 다음 중 하나를 사용 합니다.

- Hello 일정의 시작 시간 hello에 대 한 매개 변수를 사용 합니다.  Hello 솔루션을 설치할 때이 라는 hello 사용자 tooprovide 값 표시 됩니다.  일정이 여러 개 있는 경우 둘 이상의 일정에 단일 매개 변수 값을 사용할 수 있습니다.
- Hello 솔루션이 설치 될 때 시작 하는 runbook을 사용 하 여 hello 일정을 만듭니다.  이렇게 하면 한 번 하지만 포함할 수 없습니다 hello 사용자 toospecify의 hello 요구 사항이 제거 hello 일정 솔루션 hello 솔루션을 제거할 때 제거 됩니다.


### <a name="job-schedules"></a>작업 일정
작업 일정 리소스는 Runbook과 일정을 연결합니다.  형식이 **Microsoft.Automation/automationAccounts/jobSchedules** 있고 hello hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


작업 일정에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.

| 속성 | 설명 |
|:--- |:--- |
| 일정 이름 |단일 **이름** hello 일정의 hello 이름의 엔터티가 있습니다. |
| Runbook 이름  |단일 **이름** hello runbook의 hello 이름의 엔터티가 있습니다.  |



## <a name="variables"></a>variables
[Azure 자동화 변수](../automation/automation-variables.md) 유형의 **Microsoft.Automation/automationAccounts/variables** 있고 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

다음 표에 hello 변수 리소스에 대 한 hello 속성 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 설명 | Hello 변수에 대 한 선택적 설명입니다. |
| isEncrypted | Hello 변수를 암호화 해야 하는지 여부를 지정 합니다. |
| type | 이 속성은 현재 적용되지 않습니다.  hello 변수의 데이터 형식은 hello hello 초기 값으로 결정 됩니다. |
| 값 | Hello 변수에 대 한 값입니다. |

> [!NOTE]
> hello **형식** 현재 속성이 만들려는 hello 변수에 적용 되지 않습니다.  hello 변수의 데이터 형식은 hello hello 값으로 결정 됩니다.  

Hello hello 변수의 초기 값을 설정 하는 경우에 hello 올바른 데이터 형식으로 구성 되어야 합니다.  다음 표에서 hello hello 서로 다른 데이터 형식을 허용 및 구문을 제공 합니다.  JSON 값이 예상된 tooalways 되었음을 참고 hello 따옴표 안에 특수 문자를 따옴표로 묶어야 합니다.  Hello 문자열 따옴표로로 문자열 값을 지정할 수는 예를 들어 (hello 이스케이프 문자를 사용 하 여 (\\)) 동안 하나의 집합만 따옴표는 숫자 값이 지정 됩니다.

| 데이터 형식 | 설명 | 예제 | 너무 확인|
|:--|:--|:--|:--|
| string   | 값을 큰따옴표로 묶습니다.  | "\"Hello world\"" | "Hello world" |
| numeric  | 작은따옴표가 있는 숫자 값| "64" | 64 |
| 부울  | 따옴표로 묶은 **true** 또는 **false**.  이 값은 소문자여야 합니다. | "true" | true |
| Datetime | 직렬화된 날짜 값.<br>특정 날짜에 대 한 PowerShell toogenerate hello Convertto-json cmdlet이이 값을 사용할 수 있습니다.<br>예제: get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>모듈
관리 솔루션에 toodefine 않아도 [전역 모듈](../automation/automation-integration-modules.md) 가 항상 자동화 계정에서 사용할 수 있으므로 runbook으로 사용 됩니다.  Runbook에서 사용 하는 다른 모듈에 대 한 리소스 tooinclude가 필요가 있습니다.

[통합 모듈](../automation/automation-integration-modules.md) 유형의 **Microsoft.Automation/automationAccounts/modules** 있고 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


리소스 모듈에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.

| 속성 | 설명 |
|:--- |:--- |
| contentLink |Hello 모듈의 hello 내용을 지정합니다. <br><br>uri-hello 모듈의 Uri toohello 콘텐츠입니다.  이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.  <br> 버전-고유한 추적에 대 한 hello 모듈의 버전입니다. |

hello runbook hello runbook 하기 전에 만든 hello 모듈 리소스 tooensure에 의존 해야 합니다.

### <a name="updating-modules"></a>모듈 업데이트
일정을 사용 하는 runbook을 포함 하는 관리 솔루션을 업데이트 하는 경우 솔루션의 hello 새 버전에 해당 runbook에서 사용 하는 새 모듈 hello 이전 버전의 hello 모듈이 hello runbook에 사용할 수 있습니다.  Hello runbook 솔루션에서 다음을 포함 하 고 만들 작업 toorun 해야 다른 runbook 하기 전에 해당 합니다.  이렇게 하면 모든 모듈을 runbook은 사용 하기 전에 필요한 hello로 업데이트 됩니다.

* [업데이트 ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) 은 hello 최신 버전의 모든 솔루션에는 runbook에서 사용 하는 hello 모듈 되는지 확인 합니다.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) hello 일정 리소스 tooensure hello runbook을 사용 하 여 hello 최신 모듈로 toothem 연결 되어 있는 모든는 다시 등록 합니다.




## <a name="sample"></a>샘플
다음은 hello 다음 리소스를 포함 하는 포함 하는 솔루션의 샘플입니다.

- Runbook -  공용 GitHub 리포지토리에 저장된 샘플 Runbook입니다.
- Hello 솔루션을 설치할 때 hello runbook을 시작 하는 자동화 작업
- 일정 및 작업 일정 한 간격 toostart hello runbook을 예약합니다.
- 인증서
- 자격 증명
- 변수
- 모듈 -  이 hello [OMSIngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) 데이터 tooLog 분석을 작성 합니다. 

샘플 사용 하 여 hello [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 와 솔루션에 일반적으로 사용 되는 변수 hello 리소스 정의에서 toohardcoding 값을 반대로 합니다.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>다음 단계
* [보기 tooyour 솔루션 추가](operations-management-suite-solutions-resources-views.md) toovisualize 데이터를 수집 합니다.
