---
title: "리소스 상태 FAQ aaaAzure | Microsoft Docs"
description: "Azure Resource Health 개요"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Azure Resource Health FAQ
Hello Azure 리소스 상태에 대 한 toocommon 질문에 답변에 대해 알아봅니다.

## <a name="what-is-azure-resource-health"></a>Azure Resource Health란?
Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다. 리소스의 hello 최신 및 이전 상태에 대해 알려 하 고 문제를 줄일 수 있습니다. Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.  

## <a name="what-is-hello-resource-health-intended-for"></a>리소스 상태를 위한 hello 이란?
리소스에 문제가 감지 되 면 리소스 상태 hello 근본 원인을 진단 하는 데 유용 합니다. Azure 서비스 문제에 도움이 필요한 경우 도움말 toomitigate hello 문제 및 기술 지원을 제공 합니다.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Resource Health에서 어떤 상태 검사를 수행하나요?
Hello에 따라 다양 한 검사를 수행 하는 리소스 상태 [리소스 종류](resource-health-checks-resource-types.md)합니다. 이러한 검사는 세 가지 유형의 문제를 설계 된 tooimplement: 
- 계획되지 않은 이벤트(예: 예기치 않은 호스트 재부팅)
- 계획된 이벤트(예약된 호스트 OS 업데이트)
- 사용자 작업으로 트리거된 이벤트(예: 사용자가 가상 컴퓨터를 다시 부팅)

## <a name="what-does-each-of-hello-health-status-mean"></a>어떤 hello 상태의 각 의미 입니까?
3가지 상태가 있습니다.
- 사용 가능한 공간: 알려진된 문제가 없습니다 hello이이 리소스에 미치는 영향 수 있는 Azure 플랫폼에서
- 사용할 수 없음: 리소스 상태 요소가 hello 리소스 영향을 미치는 문제
- : 알 수 없는 리소스 상태가 확인할 수 없습니다 리소스의 hello 상태 항목에 대 한 정보를 받아 중지 했습니다. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>알 수 없는 상태 평균 hello는 무엇입니까? 내 리소스에 문제가 있나요?
hello 상태는 리소스 상태 특정 리소스에 대 한 정보 수신이 중지 될 때 toounknown을 설정 됩니다. 이 상태가 되어 있지 않지만 문제가 발생 하는 경우에 hello 리소스의 hello 상태의 최종 표시를 Azure 문제가 나타낼 수 있습니다.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>사용할 수 없는 리소스에 대한 도움을 받으려면 어떻게 하나요?
Hello 리소스 상태 블레이드에서 지원 요청을 제출할 수 있습니다. Hello 리소스를 사용할 수 없는 경우 Microsoft tooopen 요청에 대 한 지원 계약 불필요 때문에 플랫폼 이벤트입니다.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Resource Health에서는 플랫폼 문제로 인한 사용 불가와 사용자가 의도한 사용 불가가 구분되나요?
예, 리소스를 사용할 수 없는 경우 리소스 상태에 이러한 범주 중 하나 내 hello 근본 원인을 식별 합니다. 
-   사용자가 시작한 작업
-   계획된 이벤트 
-   계획되지 않은 이벤트

Hello 포털에서 사용자가 시작한 작업 계획 되거나 계획 되지 않은 이벤트 빨간색 경고 아이콘이 사용 하 여 표시 되어 파란색 알림 아이콘을 사용 하 여 표시 됩니다. 자세한 내용은 hello에서 제공 됩니다 [리소스 상태 개요](Resource-health-overview.md)합니다.  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Resource Health를 내 모니터링 도구에 통합할 수 있나요?
리소스 상태를 진단 하 고 리소스에 영향을 주는 Azure 서비스 문제를 완화 설계 된 서비스 toohelp 합니다. 사용할 수 있지만, hello 리소스 상태 API tooprogrammatically hello 상태를 가져와서 메트릭 toomonitor 리소스를 사용 하는 것이 좋습니다. 리소스 상태 hello 근본 원인을 확인할 수 있습니다 및 작업 tooaddress 과정을 안내해 문제가 감지 되 면 해당 합니다. 방문 [Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn 사용 하는 방법을 메트릭 toocheck 리소스에 대 한 자세한 합니다.

## <a name="where-do-i-find-resource-health"></a>Resource Health는 어디서 찾을 수 있나요?
Toohello Azure 포털에에서 로그인 한 후 여러 가지 방법으로 리소스 상태에 액세스할 수 있습니다.
- Tooyour 리소스를 이동 합니다. Hello 왼쪽 탐색에서 선택 **리소스 상태**
- Toohello Azure 모니터 블레이드로 이동 합니다.  Hello 왼쪽 탐색에서 선택 **리소스 상태**합니다.
- 열기 hello **도움말 + 지원** 블레이드에서 다음을 선택 하 고 hello 포털의 hello 상단 오른쪽 모서리에 hello 매개 변수를 선택 하 여 **도움말 + 지원**합니다. Hello 블레이드가 열리고 되 면 선택 **리소스 상태**

Hello 리소스 상태 API tooobtain 정보의 hello 상태에 대 한 리소스를 사용할 수 있습니다.

## <a name="is-resource-health-available-for-all-resource-types"></a>모든 리소스 유형에 Resource Health를 사용할 수 있나요?
hello 상태 검사 및 리소스 상태를 통해 지원 되는 리소스 형식 목록이 있습니다 [여기](resource-health-checks-resource-types.md)합니다.

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>내 리소스가 사용 가능으로 표시되지만 그렇지 않다고 생각되면 어떻게 해야 하나요?
리소스의 hello 상태를 확인할 때 바로 아래 hello 상태에서 클릭할 수 있는 **잘못 된 상태를 보고**합니다. Hello 보고서를 전송 하기 전에 hello 현재 상태가 잘못 되었습니다. 생각 이유에서 추가 세부 정보를 제공 하는 중 hello 선택할을 수 있습니다.

## <a name="is-resource-health-available-for-all-azure-regions"></a>모든 Azure 지역에서 Resource Health가 제공되나요? 
Hello 다음 영역을 제외한 모든 Azure geos에서 리소스 상태에서 제공 됩니다.
- 미국 정부 버지니아
- 미국 정부 아이오와
- 미국 국방부 동부
- 미국 국방부 중부
- 독일 중부
- 독일 북동부
- 중국 동부
- 중국 북부

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>리소스 상태 hello 서비스 상태 대시보드 또는 hello Azure 포털 서비스 알림와 어떻게 다릅니까?
리소스 상태에서 제공 하는 hello 정보 hello Azure 서비스 상태 대시보드에서 제공 하는 보다 구체적인입니다.

반면 [Azure 상태](https://status.azure.com) 및 hello 포털 서비스 알림 광범위 한 고객 (예: Azure 지역)에 영향을 주는 서비스 문제에 대 한 사용자에 게 알립니다만 관련이 있는 보다 세부적인 이벤트를 노출 하는 리소스 상태 toohello 특정 리소스입니다. 예를 들어 호스트가 예기치 않게 재부팅되는 경우 Resource Health는 가상 컴퓨터가 해당 호스트에서 실행 중인 고객에게만 경고합니다.

중요 한 toonotice에서는 리소스를 표면 이벤트 알림 서비스에에서도 게시 하는 리소스 상태에 영향을 주지 이벤트의 표시 여부를 완료 하면 해당 tooprovide 사용 되며 서비스 상태 대시보드에서 hello 합니다.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>각 리소스에 대 한 리소스 상태 tooactivate 필요 합니까?
아니요, 상태 정보는 Resource Health를 통해 제공되는 모든 리소스 유형에 대해 사용 가능합니다. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>내 조직에 대 한 리소스 상태 tooenable 필요한 무엇입니까?
아니요.  Azure 리소스 상태를 hello를 설치할 필요 없이 Azure 포털 내에서 액세스할 수 있습니다.

## <a name="is-resource-health-available-free-of-charge"></a>Resource Health는 비용 없이 제공되나요?
예.  Azure Resource Health에는 비용이 없습니다.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>리소스 상태를 제공 하는 hello 권장 사항은 무엇입니까?
Hello 상태에 따라, 리소스 상태를 제공 돌려받을 문제 해결 권장 사항을 hello 시간을 줄이는 hello 목표와 합니다. 사용 가능한 리소스에 대 한 hello 권장 사항을 toosolve hello 가장 일반적인 문제 고객 발생 하는 방법에 집중 합니다. Hello 리소스 인해 사용할 수 없는 경우 Azure의 계획 되지 않은 이벤트 tooan hello 포커스에 포함 될 동안과 그 후 hello 복구 과정을 지원 합니다. 

## <a name="next-steps"></a>다음 단계

Resource Health에 대해 알아봅니다.
-  [Azure Resource Health 개요](Resource-health-overview.md)
-  [Azure Resource Health를 통해 사용할 수 있는 리소스 유형 및 상태 검사](resource-health-checks-resource-types.md)
