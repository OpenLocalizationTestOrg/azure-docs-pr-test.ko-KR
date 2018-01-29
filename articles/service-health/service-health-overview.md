---
title: "Azure Service Health 개요 | Microsoft Docs"
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
ms.openlocfilehash: c463479b7eaee5a0548c8891dd3a20ef070dd39b
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="azure-service-health"></a>Azure Service Health
Azure Service Health는 Azure 서비스의 문제가 사용 중인 서비스에 영향을 줄 때 시기적절하고 개인 설정된 정보를 제공합니다.  향후 계획된 유지 관리에 대해 준비하는 데도 도움이 됩니다.

## <a name="service-health-events"></a>Service Health 이벤트
Service Health는 리소스에 영향을 줄 수 있는 다음과 같은 세 가지 유형의 상태 이벤트를 추적합니다.
1. **서비스 문제** - 즉시 사용자에게 영향을 주는 Azure 서비스의 문제입니다. 
2. **계획된 유지 관리** - 나중에 서비스의 가용성에 영향을 줄 수 있는 예정된 유지 관리입니다.  
3. **상태 자문** - 주의가 필요한 Azure 서비스의 변경 내용입니다. Azure 기능이 사용되지 않거나 사용 할당량을 초과하는 경우를 예로 들 수 있습니다.

    ![Service Health 이벤트](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Service Health 시작
Service Health 대시보드를 시작하려면 포털 대시보드에서 Service Health 타일을 선택합니다. 이전에 타일을 제거했거나 사용자 지정 대시보드를 사용 중인 경우 “추가 서비스”(대시보드의 왼쪽 아래)에서 Service Health 서비스를 검색합니다.
![Service Health 시작](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>서비스에 영향을 주는 현재 문제 확인
**서비스 문제** 보기에는 리소스에 영향을 주고 있는 Azure 서비스의 진행 중인 문제가 표시됩니다. 문제가 시작된 시점 및 영향을 받는 서비스 및 지역을 파악할 수 있습니다. 또한 최신 업데이트를 읽어 문제를 해결하기 위해 Azure에서 수행 중인 내용을 파악할 수 있습니다. 
![서비스 문제 관리](./media/service-health-overview/azure-service-health-overview-2.png)

**잠재적 영향** 탭을 선택하여 소유한 리소스 중에서 문제의 영향을 받을 수 있는 특정 리소스 목록을 확인할 수 있습니다. 이러한 리소스의 CSV 목록을 다운로드하여 팀과 공유할 수 있습니다.
![서비스 문제 관리 - 영향](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>링크 및 다운로드할 수 있는 설명 가져오기 
문제 관리 시스템에서 사용할 문제의 링크를 가져올 수 있습니다. PDF 및 경우에 따라 CSV 파일을 다운로드하여 Azure Portal에 액세스할 수 없는 사용자와 공유할 수 있습니다.   
![서비스 문제 관리 - 문제 관리](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Microsoft에서 지원 받기
문제가 해결된 후에도 리소스가 잘못된 상태로 남아 있는 경우 지원에 문의하세요.  페이지 오른쪽에 있는 지원 링크를 사용하세요.  

## <a name="pin-a-personalized-health-map-to-your-dashboard"></a>대시보드에 개인 설정된 상태 지도 고정
Service Health를 필터링하여 업무상 중요한 구독, 지역 및 리소스 종류를 표시합니다. 필터를 저장하고 개인 설정된 상태 세계 지도를 포털 대시보드에 고정합니다. 
![개인 설정된 상태 지도 필터링](./media/service-health-overview/azure-service-health-overview-6a.png)
![개인 설정된 상태 지도 고정](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Service Health 경고 구성
Azure Service Health는 Azure Monitor와 통합되어 업무상 중요한 리소스가 영향을 받는 경우 메일, 문자 메시지 및 웹후크 알림을 통해 경고합니다. 적절한 Service Health 이벤트에 대한 활동 로그 경고를 설정합니다. 작업 그룹을 사용하여 조직 내의 해당하는 사람들에게 해당 경고를 라우팅합니다. 자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.

 
