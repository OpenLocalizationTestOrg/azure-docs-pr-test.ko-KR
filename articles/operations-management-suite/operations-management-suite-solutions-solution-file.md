---
title: "Operations Management Suite (OMS)에서 aaaCreating 관리 솔루션 | Microsoft Docs"
description: "패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 관리 솔루션을 고객 tootheir OMS 작업 영역을 추가할 수 있습니다.  이 문서에서는 관리 솔루션 toobe를 만드는 방법에 대 한 내용은 사용자가 자신의 환경에서 사용 또는 사용 가능한 tooyour 고객을 제공 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 파일 만들기
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.  

OMS(Operations Management Suite)의 관리 솔루션은 [Resource Manager 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md)으로 구현됩니다.  hello 주 작업 tooauthor 관리 솔루션 너무 방법을 학습 하는 방법을 이해[템플릿으로 작성할](../azure-resource-manager/resource-group-authoring-templates.md)합니다.  이 문서에서는 사용 중인 솔루션에 대 한 서식 파일의 고유한 정보를 제공 하 고 어떻게 tooconfigure 일반적인 솔루션 리소스입니다.


## <a name="tools"></a>도구

모든 텍스트 편집기 toowork 솔루션 파일을 사용할 수 있지만 hello 다음 문서에에서 설명 된 대로 Visual Studio 또는 Visual Studio Code에서 제공 하는 hello 기능을 활용 하는 것이 좋습니다.

- [Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Visual Studio 코드에서 Azure Resource Manager 템플릿으로 작업](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>구조
hello 관리 솔루션 파일의 기본 구조는 동일 hello은 한 [리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md#template-format) 은 다음과 같습니다.  각 hello 섹션 아래 hello 최상위 수준 요소에 설명 하 고와 솔루션의 내용이 있습니다.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>매개 변수
[매개 변수](../azure-resource-manager/resource-group-authoring-templates.md#parameters) hello 관리 솔루션을 설치할 때 hello 사용자에서 필요로 하는 값입니다.  모든 솔루션에 포함될 표준 매개 변수가 있고, 특정 솔루션에 필요한 다른 매개 변수를 추가할 수 있습니다.  사용자에서는 어떻게 매개 변수 값 솔루션을 설치할 때 hello 특정 매개 변수 및 hello 솔루션이 설치 되는 방법에 따라 달라 집니다.

사용자가 hello 통해 관리 솔루션을 설치 하는 경우 [Azure 마켓플레이스](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 또는 [Azure 빠른 시작 템플릿](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 증명된 tooselect는는 [OMS 작업 영역 및 자동화 계정 ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  이들은 각각 hello 표준 매개 변수 사용 되는 toopopulate hello 값입니다.  hello 사용자에 게 묻지 않습니다 toodirectly hello 표준 매개 변수 값을 제공 하지만 모든 추가 매개 변수를 증명된 tooprovide 값입니다.

Hello 사용자 솔루션을 설치 하는 경우 [또 다른 방법은](operations-management-suite-solutions.md#finding-and-installing-management-solutions), 모든 표준 매개 변수 및 모든 추가 매개 변수 값을 입력 해야 합니다.

샘플 매개 변수는 다음과 같습니다.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

다음 표에서 hello 매개 변수의 hello 특성을 설명 합니다.

| 특성 | 설명 |
|:--- |:--- |
| type |Hello 매개 변수에 대 한 데이터 형식입니다. hello 사용자에 게 표시 하는 hello 입력된 컨트롤 hello 데이터 형식에 따라 달라 집니다.<br><br>bool - 드롭다운 상자<br>string - 텍스트 상자<br>int - 텍스트 상자<br>securestring - 암호 필드<br> |
| 카테고리 |Hello 매개 변수에 대 한 선택적 범주입니다.  매개 변수가 hello 같은 범주로 그룹화 됩니다. |
| control |string 매개 변수의 추가 기능입니다.<br><br>datetime - Datetime 컨트롤이 표시됩니다.<br>guid-Guid 값은 자동으로 생성 하 고 hello 매개 변수가 표시 되지 않습니다. |
| 설명 |Hello 매개 변수에 대 한 선택적 설명입니다.  정보 풍선이 다음 toohello 매개 변수에 표시 합니다. |

### <a name="standard-parameters"></a>표준 매개 변수
hello 다음 표에 모든 관리 솔루션에 대 한 표준 매개 변수 hello 있습니다.  Hello Azure 마켓플레이스 또는 퀵 스타트 서식 파일에서 솔루션을 설치할 때에 메시지를 표시 하는 대신 hello 사용자에 대 한 이러한 값은 채워집니다.  다른 방법으로 hello 솔루션이 설치 된 경우 hello 사용자에 대 한 값을 제공 해야 합니다.

> [!NOTE]
> hello Azure 마켓플레이스와 퀵 스타트 템플릿의 hello 사용자 인터페이스 hello 표에 hello 매개 변수 이름에 있어야 합니다.  다른 매개 변수 이름을 사용 하는 경우 다음 hello 묻는 고객을 위해 및은 자동으로 채워지지 않습니다.
>
>

| 매개 변수 | 형식 | 설명 |
|:--- |:--- |:--- |
| accountName |string |Azure Automation 계정 이름입니다. |
| pricingTier |string |Log Analytics 작업 영역 및 Azure Automation 계정의 가격 책정 계층입니다. |
| regionId |string |Azure 자동화 계정 hello의 지역입니다. |
| solutionName |string |Hello 솔루션의 이름입니다.  퀵 스타트 템플릿을 통해 솔루션을 배포 하는 경우 다음 정의 해야 solutionName 매개 변수로 대신 hello 사용자 toospecify 하나 필요로 하는 문자열을 정의할 수 있도록 합니다. |
| workspaceName |string |Log Analytics 작업 영역 이름입니다. |
| workspaceRegionId |string |지역 hello 로그 분석 작업 영역입니다. |


다음은 hello 구조를 복사 하 고 솔루션 파일에 붙여 넣을 수 있는 hello 표준 매개 변수입니다.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Hello 구문 사용 하 여 hello 솔루션의 다른 요소에서 tooparameter 값 참조 **매개 변수 ('parameter name')**합니다.  예를 들어 tooaccess hello 작업 영역 이름을, 사용 하 여 **parameters('workspaceName')**

## <a name="variables"></a>variables
[변수](../azure-resource-manager/resource-group-authoring-templates.md#variables) 은 hello 관리 솔루션의 나머지 hello에에서 사용할 수 있는 값입니다.  이러한 값이 노출된 toohello 사용자 hello 솔루션을 설치 합니다.  이들은 의도 한 tooprovide hello 작성자를 한 곳 hello 솔루션 전체의 여러 번 사용할 수 있는 값을 관리할 수 있습니다. 모든 값 특정 tooyour 솔루션에에서 넣어야 변수 hello에 코딩 하는 것과 반대로 toohard로 **리소스** 요소입니다.  쉽게 hello 코드를 더 쉽게 읽을 수 있고 있습니다 tooeasily 이후 버전에서 이러한 값을 변경 합니다.

다음은 솔루션에 일반적인 매개 변수를 사용한 **variables** 요소의 예입니다.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Hello 구문 사용 하 여 hello 솔루션을 통해 toovariable 값 참조 **변수 ('변수 이름')**합니다.  예를 들어 tooaccess hello SolutionName 변수를 사용 하 여 **variables('SolutionName')**합니다.

여러 값 집합이 있는 복잡한 변수를 정의할 수도 있습니다.  이러한 변수는 서로 다른 형식의 리소스에 대해 여러 속성을 정의하는 관리 솔루션에서 특히 유용합니다.  예를 들어 hello 솔루션 변수 toohello 다음 위에 표시 된 재구성 수 있습니다.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Hello 구문 사용 하 여 hello 솔루션을 통해 toovariable 값을 참조 하는 경우에 **variables('variable name').property**합니다.  예를 들어 tooaccess hello 솔루션 이름 변수, 사용 하 여 **variables('Solution') 합니다. 이름**합니다.

## <a name="resources"></a>리소스
[리소스](../azure-resource-manager/resource-group-authoring-templates.md#resources) 관리 솔루션 설치 및 구성 하는 hello 다른 리소스를 정의 합니다.  가장 큰 hello 및 hello 템플릿의 가장 복잡 한 부분 됩니다.  Hello 구조와 전체 설명은 리소스 요소를 가져올 수 있습니다 [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md#resources)합니다.  일반적으로 정의하는 여러 리소스는 이 설명서의 다른 문서에 자세히 설명되어 있습니다. 


### <a name="dependencies"></a>종속성
hello **dependsOn** 지정 하는 요소는 [종속성](../azure-resource-manager/resource-group-define-dependencies.md) 다른 리소스에 있습니다.  Hello 솔루션을 설치할 때 생성 된 모든 종속성 될 때까지 리소스가 만들어지지 않습니다.  예를 들어 솔루션이 [작업 리소스](operations-management-suite-solutions-resources-automation.md#automation-jobs)를 사용하여 설치될 경우 솔루션에서 [Runbook을 시작](operations-management-suite-solutions-resources-automation.md#runbooks)할 수 있습니다.  hello 작업 리소스 hello runbook 리소스 toomake hello 작업을 만들기 전에 해당 hello runbook을 만들 있는지 따라 달라 집니다.

### <a name="oms-workspace-and-automation-account"></a>OMS 작업 영역 및 Automation 계정
관리 솔루션을 필요로 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md) toocontain 뷰 및 [자동화 계정](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook 및 관련 리소스입니다.  이러한 hello hello 솔루션의 리소스 만들어지고 hello 솔루션 자체에 정의 되지 않아야 하기 전에 사용할 수 있어야 합니다.  hello 사용자는 [작업 영역 및 계정 지정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) 경우 여 솔루션을 배포 하지만 hello 작성자 hello 포인트 다음을 고려해 야 합니다.

## <a name="solution-resource"></a>솔루션 리소스
각 솔루션에 필요한 hello에 리소스 항목 **리소스** hello 솔루션 자체를 정의 하는 요소입니다.  유형의 아무런 **Microsoft.OperationsManagement/solutions** 있고 hello 구조를 수행 합니다. 여기에 [표준 매개 변수](#parameters) 및 [변수](#variables) 하는 hello 솔루션의 toodefine 일반적으로 사용 되는 속성입니다.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>종속성
hello 솔루션 리소스 있어야는 [종속성](../azure-resource-manager/resource-group-define-dependencies.md) 하므로 tooexist hello 솔루션 만들기 전에 hello 솔루션의 다른 모든 리소스에 있습니다.  Hello에 각 리소스에 대 한 항목을 추가 하 여이 작업을 수행 **dependsOn** 요소입니다.

### <a name="properties"></a>properties
hello 솔루션 리소스에는 다음 표에 hello에 hello 속성이 있습니다.  이 참조 하 고 hello 솔루션이 설치 된 후 hello 리소스 관리 되는 방식을 정의 하는 hello 솔루션에 포함 된 hello 리소스가 포함 됩니다.  어느 hello에 hello 솔루션의 각 리소스를 나열 해야 **referencedResources** 또는 hello **containedResources** 속성입니다.

| 속성 | 설명 |
|:--- |:--- |
| workspaceResourceId |hello 형태로 hello 로그 분석 작업 영역 ID  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<작업 영역 이름을\>*합니다. |
| referencedResources |Hello 솔루션을 제거할 때 제거 해야 하는 hello 솔루션의 리소스 목록입니다. |
| containedResources |Hello 솔루션을 제거할 때 제거 하는 hello 솔루션의 리소스 목록입니다. |

위의 hello 예제 runbook, 일정 및 보기를 포함 하는 솔루션입니다.  hello 일정 및 runbook은 *참조* hello에 **속성** 요소 하므로 hello 솔루션을 제거할 때 제거 되지 않습니다.  hello 보기는 *포함* 않았으므로 hello 솔루션을 제거할 때 제거 됩니다.

### <a name="plan"></a>계획
hello **계획** hello 솔루션 리소스의 엔터티에 포함 된 다음 표는 hello에 hello 속성입니다.

| 속성 | 설명 |
|:--- |:--- |
| name |Hello 솔루션의 이름입니다. |
| 버전 |Hello 작성자를 기준으로 hello 솔루션 버전입니다. |
| product |두 가지 범주인 tooidentify hello 솔루션입니다. |
| publisher |Hello 솔루션의 게시자입니다. |



## <a name="sample"></a>샘플
Hello 다음 위치에서 샘플 솔루션 리소스를 사용 하 여 솔루션 파일을 볼 수 있습니다.

- [Automation 리소스](operations-management-suite-solutions-resources-automation.md#sample)
- [검색 및 경고 리소스](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>다음 단계
* [저장 된 검색 및 알림 추가](operations-management-suite-solutions-resources-searches-alerts.md) tooyour 관리 솔루션입니다.
* [뷰 추가](operations-management-suite-solutions-resources-views.md) tooyour 관리 솔루션입니다.
* [Runbook 및 기타 자동화 리소스를 추가](operations-management-suite-solutions-resources-automation.md) tooyour 관리 솔루션입니다.
* 세부 사항을 hello [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.
* [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.
