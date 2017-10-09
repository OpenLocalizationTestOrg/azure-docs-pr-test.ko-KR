---
title: "aaaAzure 서비스 상태 개요 | Microsoft Docs"
description: "Azure 앱이 현재 및 향후 Azure 서비스 문제 및 유지 관리에 의해 어떤 영향을 받는지에 대한 개인 설정된 정보입니다."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Azure Service Health
Azure Service Health는 Azure 서비스의 문제가 사용 중인 서비스에 영향을 줄 때 시기적절하고 개인 설정된 정보를 제공합니다.  향후 계획된 유지 관리에 대해 준비하는 데도 도움이 됩니다.

## <a name="service-health-events"></a>Service Health 이벤트
Service Health는 리소스에 영향을 줄 수 있는 다음과 같은 세 가지 유형의 상태 이벤트를 추적합니다.
1. **서비스 문제** -문제 hello 지금 바로 영향을 주는 Azure 서비스입니다. 
2. **계획 된 유지 관리** -hello 나중에 서비스의 hello 가용성에 영향을 줄 수 있는 향후 유지 관리 합니다.  
3. **상태 자문** - 주의가 필요한 Azure 서비스의 변경 내용입니다. Azure 기능이 사용되지 않거나 사용 할당량을 초과하는 경우를 예로 들 수 있습니다.

    ![Service Health 이벤트](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Service Health 시작
toolaunch 서비스 상태 대시보드를 선택 hello 서비스 상태 대시보드에서 타일을 사용자 포털. 이전에 제거한 hello 타일 또는 사용자 지정 대시보드를 사용 하는 경우에 "더 많은 서비스" 서비스 상태 서비스에 대 한 검색 (동영상이 대시보드에서 왼쪽 아래).
![Service Health 시작](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>서비스에 영향을 주는 현재 문제 확인
hello **서비스 문제** 보기 리소스에 영향을 주지는 Azure 서비스에서 진행 중인 문제를 표시 합니다. Hello 문제 시작 되었을 때와 서비스 및 영역 영향을 이해할 수 있습니다. 읽을 수 있습니다 hello 가장 최근의 업데이트 toounderstand 어떤 Azure tooresolve hello 문제를 수행 하는 작업입니다. 
![서비스 문제 관리](./media/service-health-overview/azure-service-health-overview-2.png)

Hello 선택 **잠재적인 영향** 탭 toosee hello 특정 리소스 목록을 소유 하는 hello 문제의 영향을 받을 수 있습니다. 팀과 함께 이러한 리소스 tooshare CSV 목록이 다운로드할 수 있습니다.
![서비스 문제 관리 - 영향](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>링크 및 다운로드할 수 있는 설명 가져오기 
문제 관리 시스템에 문제가 toouse hello에 대 한 링크를 가져올 수 있습니다. PDF 및 경우에 따라 CSV 파일 tooshare 액세스 toohello Azure 포털에 없는 사용자를 다운로드할 수 있습니다.   
![서비스 문제 관리 - 문제 관리](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Microsoft에서 지원 받기
리소스는 잘못 된 상태로 남아 hello 해결 한 후에 지원을 문의 하십시오.  Hello 지원 링크를 사용 하 여 hello hello 페이지의 오른쪽에 있습니다.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>개인 설정 된 상태 맵 tooyour 대시보드 고정
비즈니스에 중요 한 구독, 지역 및 리소스 종류에는 서비스 상태 tooshow를 필터링 합니다. Hello 필터 및 개인 설정 된 상태 세계 지도 tooyour 포털 대시보드 pin를 저장 합니다. 
![개인 설정된 상태 지도 필터링](./media/service-health-overview/azure-service-health-overview-6a.png)
![개인 설정된 상태 지도 고정](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Service Health 경고 구성
Azure 서비스 상태와 통합 되어 Azure 모니터 tooalert 하면 전자 메일, 문자 메시지 및 webhook 알림을 통해 비즈니스에 중요 한 리소스의 영향을 받는 경우입니다. Hello 적절 한 서비스 상태 이벤트에 대 한 활동 로그 경고를 설정 합니다. 동작 그룹을 사용 하 여 조직에 적절 한 사람이 toohello 경고는 경로입니다. 자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.

# <a name="next-steps"></a>다음 단계
상태 문제 알림을 받도록 경고를 설정합니다. 자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요. 