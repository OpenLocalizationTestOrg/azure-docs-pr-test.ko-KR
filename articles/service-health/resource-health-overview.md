---
title: "aaaAzure 리소스 상태 개요 | Microsoft Docs"
description: "Azure 리소스 상태 개요"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Azure Resource Health 개요
 
Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다. 리소스의 hello 최신 및 이전 상태에 대해 알려 하 고 문제를 줄일 수 있습니다. Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.

반면 [Azure 상태](https://status.azure.com) 다양 한 Azure 고객 집합에 영향을 주는 서비스 문제에 대해 알려, 리소스 상태 리소스 hello 상태의 개인 설정 된 대시보드를 제공 합니다. 리소스 상태를 보면 리소스 hello에 사용할 수 없었습니다. hello 항상 기한이 지 남 tooAzure 서비스 문제입니다. 이렇게 하면 toounderstand 있습니다에 대 한 간단한 SLA 위반 된 경우. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>무엇이 리소스로 간주되고 리소스 상태에서는 리소스가 정상인지를 어떻게 결정하나요?
리소스는 가상 컴퓨터, 웹앱 또는 SQL Database처럼 Azure Resource Manager를 통해 Azure 서비스에서 제공하는 리소스 유형의 인스턴스입니다.

리소스 상태는 리소스의 정상 상태 경우 hello 서로 다른 Azure 서비스 tooassess에서 내보낸 신호에 의존 합니다. 리소스 상태가 정상이 아닌 경우 리소스 상태 hello 문제의 toodetermine hello 소스 추가 정보를 분석 합니다. 또한 Microsoft toofix hello 문제 또는 hello 문제의 원인을 tooaddress hello를 수행할 수 있는 작업에 소요 되는 동작을 식별 합니다. 

리소스 종류와 상태의 검토 hello 전체 목록은 체크 인할 [Azure 리소스 상태](resource-health-checks-resource-types.md) 상태 평가 하는 방법을 대 한 자세한 내용은 합니다.

## <a name="health-status-provided-by-resource-health"></a>리소스 상태에서 제공하는 상태
리소스의 hello 상태 hello 다음 상태 중 하나입니다.

### <a name="available"></a>사용 가능
hello 서비스가 hello 리소스의 hello 상태에 영향을 주지는 이벤트가 검색 되지 않습니다. 여기서 hello 리소스에서에서 복구 계획 되지 않은 가동 중지 시간 동안 hello 마지막 하는 경우에 표시 됩니다는 24 시간 동안 hello **최근 복구** 알림입니다.

![리소스 상태가 사용 가능한 가상 컴퓨터](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>사용할 수 없음
진행 중인 플랫폼 또는 플랫폼 비 이벤트 hello 리소스의 hello 상태에 영향을 주지 hello 검색 했습니다.

#### <a name="platform-events"></a>플랫폼 이벤트
이러한 이벤트는 hello Azure 인프라의 여러 구성 요소에 의해 트리거되는 및 계획 된 유지 관리와 같은 예약 된 작업 및 계획 되지 않은 호스트 재부팅와 같은 예기치 않은 문제를 모두 포함 합니다.

리소스 상태 이벤트 hello hello 복구 프로세스에 추가 세부 정보를 제공 하며 지원할 수 있도록 하면 toocontact는 활성 Microsoft 계약을 지원 해야 하는 경우에 합니다.

![Tooplatform 이벤트 인해 리소스 상태 사용할 수 없는 가상 컴퓨터](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>비-플랫폼 이벤트
이러한 이벤트는 사용자가 예를 들어 가상 컴퓨터를 중지 하거나 hello 연결 tooa Redis 캐시의 최대 수에 도달 하 여 수행 된 작업에 의해 트리거됩니다.

![Toonon 플랫폼 이벤트 인해 리소스 상태 사용할 수 없는 가상 컴퓨터](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>알 수 없음
이 상태 정보는 리소스 상태에서 10분 이상 이 리소스에 대한 정보를 수신하지 못했음을 나타냅니다. 이 상태 hello 상태의 hello 리소스의 명확한 표시 동안 hello 문제 해결 과정에에서는 중요 한 데이터 요소는:
* Hello 리소스 hello 리소스의 예상된 hello 상태와 실행 중인 경우 tooAvailable 몇 분 후 업데이트 됩니다.
* Hello 리소스에 문제가 발생 하는 경우 hello 알 수 없는 상태를 제안할 수 있습니다 hello 리소스 hello 플랫폼에서 이벤트에 의해 영향을 합니다.

![리소스 상태가 알 수 없음인 가상 컴퓨터](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>잘못된 상태 보고
클릭 하 여 알려 주십시오 수는 경우 언제 든 지 hello 현재 상태가 잘못 되었습니다., **잘못 된 상태를 보고**합니다. 여기서 Azure 문제로 인해 영향을 받는 경우 좋습니다 hello 리소스 상태 블레이드에서 toocontact 지원을. 

![리소스 상태에서 잘못된 상태 보고](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>기록 정보
클릭 하 여 too14 일 분량의 기록 상태 데이터를 액세스할 수 있습니다 **기록 보기** hello 리소스 상태 블레이드에서 합니다. 

![리소스 상태 보고 기록](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>시작
tooopen 한 리소스에 대 한 리소스 상태
1.  Azure 포털 hello에 로그인 합니다.
2.  Tooyour 리소스를 이동 합니다.
3.  Hello 왼쪽에 있는 hello 리소스 메뉴를 클릭 **리소스 상태**합니다.

![리소스 블레이드에서 리소스 상태 열기](./media/resource-health-overview/from-resource-blade.png)

리소스 상태를 클릭 하 여 액세스할 수도 있습니다 **더 많은 서비스**를 입력 하 고 **리소스 상태** 필터 텍스트 상자 tooopen hello에 **도움말 + 지원** 블레이드입니다. 마지막으로 [**리소스 상태**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth)를 클릭합니다.

![추가 서비스에서 리소스 상태 열기](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>다음 단계

이러한 리소스 toolearn 리소스 상태에 대해 자세히 확인해 보세요.
-  [Azure Resource Health에서 리소스 유형 및 상태 검사](resource-health-checks-resource-types.md)
-  [Azure Resource Health에 대한 질문과 대답](resource-health-faq.md)




