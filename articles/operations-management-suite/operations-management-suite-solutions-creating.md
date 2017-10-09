---
title: "OMS의 관리 솔루션 aaaBuild | Microsoft Docs"
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
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>OMS(Operations Management Suite)에서 관리 솔루션 설계 및 만들기(미리 보기)
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.

[관리 솔루션](operations-management-suite-solutions.md) 패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)의 확장 고객 tootheir OMS 작업 영역을 추가할 수 있습니다.  이 문서는 것이 기본적인 프로세스 toodesign 수를 표시 하 고 적합 한 가장 일반적인 요구 사항에 대 한 관리 솔루션을 빌드합니다.  새 toobuilding 관리 솔루션의 경우 시작 지점으로이 프로세스를 사용 하 여 고 요구 사항을 발전 더 복잡 한 솔루션에 대 한 hello 개념을 활용할 수 있습니다.

## <a name="what-is-a-management-solution"></a>관리 솔루션이란?

OMS 및 특정 모니터링 시나리오 tooachieve 함께 작동 하는 Azure 리소스를 포함 하는 관리 솔루션입니다.  로 구현 될 [리소스 관리 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md) 방법에 대 한 세부 정보를 포함 하는 tooinstall hello 솔루션을 설치할 때 포함 된 리소스를 구성 합니다.

기본 전략 hello hello Azure 환경에서 개별 구성 요소를 작성 하 여 toostart 관리 솔루션은 합니다.  제대로 작동 하는 hello 기능을 사용할 수 있게 되 면 시작할 수 있습니다에 패키징하는 [관리 솔루션 파일](operations-management-suite-solutions-solution-file.md)합니다. 


## <a name="design-your-solution"></a>솔루션 디자인
관리 솔루션에 대 한 가장 일반적인 패턴 hello hello 다음 다이어그램에에서 표시 됩니다.  이 패턴의 hello 다른 구성 요소는 hello 아래에 설명 되어 있습니다.

![OMS 솔루션 개요](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>데이터 원본
솔루션을 디자인 hello 첫 번째 단계는 hello 로그 분석 저장소에서 필요로 하는 hello 데이터를 결정 합니다.  이 데이터를 수집할 수 있습니다는 [데이터 소스](../log-analytics/log-analytics-data-sources.md) 또는 [다른 솔루션](operations-management-suite-solutions.md), 솔루션 tooprovide hello 프로세스 toocollect 할 수 또는 것입니다.

다양 한 방법으로 데이터 원본에 설명 된 대로 hello 로그 분석 저장소에서 수집할 수 있는 없는 [로그 분석에서 데이터 원본을](../log-analytics/log-analytics-data-sources.md)합니다.  이 hello Windows 이벤트 로그에서에서 이벤트를 포함 하거나 의해 생성 된 Syslog 또한 tooperformance 카운터는 Windows 및 Linux 클라이언트에 대 한 합니다.  또한 Azure Monitor에서 수집한 Azure 리소스에서도 데이터를 수집할 수 있습니다.  

Hello 사용 가능한 데이터 원본 중 하나를 통해 액세스할 수 없는 데이터가 필요한 경우 hello를 사용할 수 있습니다 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md) toowrite 데이터 toohello 로그 분석 저장소는 REST를 호출할 수 있는 모든 클라이언트에서 수 있는 API입니다.  hello 가장 일반적인 방법은 관리 솔루션에 사용자 지정 데이터 컬렉션은 toocreate는 [Azure 자동화에서 runbook](../automation/automation-runbook-types.md) Azure 또는 외부 리소스에서 필요한 hello 데이터를 수집 하 고 사용 하 여 데이터 수집기 API toowrite hello toohello 리포지토리입니다.  

### <a name="log-searches"></a>로그 검색
[로그 검색](../log-analytics/log-analytics-log-searches.md) 사용 되는 tooextract 되며 hello 로그 분석 저장소에서 데이터를 분석 합니다.  보기 및 분석 중에 추가 tooallowing hello 사용자 tooperform 임시 hello 저장소에서 데이터의 경고에서 사용 됩니다.  

모든 뷰나 경고에서 사용 되지 않습니다 하는 경우에 도움이 toohello 사용자 수를 생각 하는 쿼리를 정의 해야 합니다.  이러한을 사용할 수 있는 toothem 저장 된 검색으로 hello 포털에서 되며에 포함할 수도 있습니다는 [쿼리 목록 시각화 부분](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) 사용자 지정 보기에 있습니다.

### <a name="alerts"></a>경고
[로그 분석에서 경고](../log-analytics/log-analytics-alerts.md) 를 통해 문제를 식별 [검색 로그](#log-searches) hello 리포지토리에 hello 데이터에 대 한 합니다.  Hello 사용자에 게 알리는 또는 자동으로 응답 작업을 실행 합니다. 응용 프로그램에 대한 다양한 경고 조건을 식별하고, 해당 경고 규칙을 솔루션 파일에 포함해야 합니다.

잠재적으로 프로세스를 자동화 hello 문제를 수정할 수, 하는 경우 다음 일반적으로 만들게 runbook tooperform Azure 자동화에서에서이 재구성 됩니다.  대부분의 Azure 서비스를 관리할 수 [cmdlet](/powershell/azure/overview) 는 hello runbook tooperform 이러한 기능을 활용 합니다.

솔루션 응답 tooan 경고의 외부 기능이 필요한 경우 사용할 수 있습니다는 [webhook 응답](../log-analytics/log-analytics-alerts-actions.md)합니다.  이렇게 하면 있습니다 toocall hello 경고에서 정보를 보내는 외부 웹 서비스.

### <a name="views"></a>뷰
로그 분석에는 뷰는 hello 로그 분석 저장소에서 사용 되는 toovisualize 데이터입니다.  각 솔루션에는 단일 뷰를 일반적으로 포함 합니다는 [타일](../log-analytics/log-analytics-view-designer-tiles.md) hello 사용자의 주 대시보드에 표시 되는 합니다.  hello 보기에는 개수에 관계 없이 포함 될 수 있습니다 [시각화 부분](../log-analytics/log-analytics-view-designer-parts.md) tooprovide hello 수집 된 데이터 toohello 사용자의 각기 다른 시각화 합니다.

하면 [hello 뷰 디자이너를 사용 하 여 사용자 지정 뷰 만들기](../log-analytics/log-analytics-view-designer.md) 있는 솔루션 파일에 포함 하기 위해 나중에 내보낼 수 있습니다.  


## <a name="create-solution-file"></a>솔루션 파일 만들기
구성 하 고 솔루션의 일부가 될 hello 구성 요소를 테스트 한, 후 [솔루션 파일을 만들](operations-management-suite-solutions-solution-file.md)합니다.  Hello 솔루션 구성 요소에서 구현 됩니다는 [리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md) 포함 하는 [솔루션 리소스](operations-management-suite-solutions-solution-file.md#solution-resource) 관계 toohello와 기타 리소스를 hello 파일입니다.  


## <a name="test-your-solution"></a>솔루션 테스트
솔루션을 개발 하는 동안 tooinstall 필요 하 고 작업 영역에 테스트 합니다.  이렇게 하려면 너무 hello 사용할 수 있는 방법 중 하나로[테스트 하 고 리소스 관리자 템플릿을 설치](../azure-resource-manager/resource-group-template-deploy.md)합니다.

## <a name="publish-your-solution"></a>솔루션 게시
완료 하 고 솔루션을 테스트 후 원본 hello 중 하나를 통해 사용할 수 있는 toocustomers를 만들 수 있습니다.

- **Azure 퀵 스타트 템플릿** -  [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/) GitHub 통해 hello 커뮤니티에서 제공 하는 리소스 관리자 템플릿 집합입니다.  사용할 수 있습니다 솔루션 hello에 다음 정보에 의해 [기여 가이드](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE)합니다.
- **Azure Marketplace** -  hello [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/) toodistribute 있으며 판매 솔루션 Isv tooother 개발자와 IT 전문가입니다.  학습할 수 있는 방법을 toopublish 사용자 솔루션 tooAzure Marketplace에서 [어떻게 toopublish hello Azure Marketplace에서에서 제공 하는 서비스를 관리 하 고](../marketplace-publishing/marketplace-publishing-getting-started.md)합니다.



## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[솔루션 파일을 만들](operations-management-suite-solutions-solution-file.md) 관리 솔루션에 대 한 합니다.
* 세부 사항을 hello [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.
* [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.