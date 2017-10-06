---
title: "Operations Management Suite (OMS) 관리 솔루션에 aaaViews | Microsoft Docs"
description: "Operations Management Suite (OMS)에서 관리 솔루션에는 하나 이상의 보기 toovisualize 데이터 일반적으로 포함 됩니다.  이 문서 방법을 tooexport 뷰를 만들 hello 뷰 디자이너에서 설명 하 고 관리 솔루션에 포함 합니다. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>OMS(Operations Management Suite) 관리 솔루션의 보기(Preview)
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.    
>
>

[Operations Management Suite (OMS)에서 관리 솔루션](operations-management-suite-solutions.md) 는 일반적으로 하나 이상의 보기 toovisualize 데이터를 포함 합니다.  이 문서에서 설명 하는 방법을 tooexport 뷰를 만들 hello 여 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md) 관리 솔루션에 포함 합니다.  

> [!NOTE]
> hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>필수 조건
이 문서에서는 하 이미 방법을 잘 알고 너무 가정[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md) 및 솔루션 파일의 hello 구조입니다.

## <a name="overview"></a>개요
만들 tooinclude 관리 솔루션에는 보기는 **리소스** hello에 대 한 [솔루션 파일](operations-management-suite-solutions-creating.md)합니다.  hello hello 보기의 세부 구성을 나타내는 JSON은 일반적으로 복잡 하지만 및 문제가 되지 일반적인 솔루션 작성자 수 toocreate 수동으로 수 있다고 합니다.  hello 가장 일반적인 방법은 hello를 사용 하 여 toocreate hello 뷰 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md), 내보내고 해당 자세한 구성 toohello 솔루션을 추가 합니다.

hello 기본 단계 tooadd 보기 tooa 솔루션은 다음과 같습니다.  각 단계는 아래 hello 섹션에서 더 자세히 설명 되어 있습니다.

1. Hello 보기 tooa 파일을 내보냅니다.
2. Hello 솔루션의 hello 보기 리소스를 만듭니다.
3. Hello 세부 정보 보기를 추가 합니다.

## <a name="export-hello-view-tooa-file"></a>Hello 보기 tooa 파일 내보내기
Hello 지침에 따라 [로그 분석 뷰 디자이너](../log-analytics/log-analytics-view-designer.md) tooexport 뷰 tooa 파일입니다.  hello 내보낸된 파일은 될 JSON 형식으로 hello 동일 [hello 솔루션 파일로 요소](operations-management-suite-solutions-solution-file.md)합니다.  

hello **리소스** hello 보기 파일의 요소는 유형의 사용 하 여 리소스를 갖게 됩니다 **Microsoft.OperationalInsights/workspaces** 나타내는 hello OMS 작업 영역을 합니다.  이 요소에는의 형식과 subelement 포함 될 **뷰** 하는 자세한 구성을 포함 하 hello 보기를 나타냅니다.  이 요소의 hello 세부 정보 복사한 다음 솔루션에 복사 합니다.

## <a name="create-hello-view-resource-in-hello-solution"></a>Hello 솔루션에서 hello 보기 리소스 만들기
다음 보기 리소스 toohello hello 추가 **리소스** 솔루션 파일의 요소입니다.  이 작업에는 아래 설명된, 추가해야 하는 변수가 사용됩니다.  해당 hello 참고 **대시보드** 및 **OverviewTile** 속성 하는 자리 표시자 hello hello 내보낸된 보기 파일에서 해당 속성을 덮어씁니다.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Hello 솔루션 파일의 변수 toohello 변수 요소 다음에 오는 hello를 추가 하 고 솔루션에 대 한 hello 값 toothose 바꿉니다.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


참고 내보낸된 보기 파일 에서만 hello 전체 보기 리소스를 복사할 수 toowork 솔루션에서 toomake hello에 대 한 변경 내용을 수행 해야 합니다.  

* hello **형식** hello 보기에 대 한 리소스에서 변경 toobe이 필요한 **뷰** 너무**Microsoft.OperationalInsights/workspaces**합니다.
* hello **이름** hello 보기 리소스에 대 한 속성 변경 toobe tooinclude hello 작업 영역 이름이 필요 합니다.
* hello 작업 영역에 대 한 hello 종속성 toobe hello 작업 공간 리소스 hello 솔루션에 정의 되어 있지 이후 제거 해야 합니다.
* **DisplayName** 속성 요구 toobe toohello 보기를 추가 합니다.  hello **Id**, **이름**, 및 **DisplayName** 모두 일치 해야 합니다.
* 매개 변수 이름을 변경 해야 toomatch hello 매개 변수 집합이 필요 합니다.
* 변수는 hello 솔루션에 정의 하 고 hello 적절 한 속성에 사용 해야 합니다.

## <a name="add-hello-view-details"></a>Hello 뷰 세부 정보 추가
hello 보기 리소스 hello에 내보낸 파일은 hello에 두 개의 요소를 포함 하는 보기 **속성** 라는 요소 **대시보드** 및 **OverviewTile** hello를 포함 하는 hello 보기의 자세한 구성 합니다.  이 두 요소 및 해당 내용을 hello에 복사한 **속성** 솔루션 파일에 hello 보기 리소스의 요소입니다.

## <a name="example"></a>예제
예를 들어 다음 예제는 hello는 보기를 통해 간단한 솔루션 파일을 보여 줍니다.  줄임표 (...) hello에 대 한 표시 **대시보드** 및 **OverviewTile** 공간 원인에 대 한 콘텐츠입니다.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>다음 단계
* [관리 솔루션](operations-management-suite-solutions-creating.md)을 만드는 방법에 대한 자세한 내용을 알아보세요.
* [관리 솔루션에 Automation runbook](operations-management-suite-solutions-resources-automation.md)을 포함합니다.
