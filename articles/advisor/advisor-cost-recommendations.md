---
title: "aaaAzure Advisor 비용 권장 사항을 | Microsoft Docs"
description: "Azure 배포의 Azure 관리자 toooptimize hello 비용을 사용 합니다."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Advisor 비용 권장 사항

Advisor는 유휴 및 사용 미달 리소스를 식별하여 전체적인 Azure 사용을 최적화하고 줄이는 데 도움을 줍니다. Hello에서 권장 사항이 비용 얻을 수 있습니다 **비용** hello 관리자 대시보드에서 탭 합니다.

![Advisor 비용 탭](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>사용률이 낮은 인스턴스의 크기를 조정하여 가상 컴퓨터 소비 최적화 
특정 응용 프로그램 시나리오가 발생할 수도 있지만 사용률이 낮은의 설계, hello 크기와 수의 가상 컴퓨터를 관리 하 여 종종 비용을 절약할 수 있습니다. Advisor는 14일 동안 가상 컴퓨터 사용량을 모니터링하고 사용률이 낮은 가상 컴퓨터를 식별합니다. 4일 이상 CPU 사용률이 5% 이하이고 네트워크 사용량이 7MB 이하인 가상 컴퓨터는 사용률이 낮은 가상 컴퓨터로 간주됩니다.

Advisor tooshut 아래쪽 또는 크기를 조정할를 선택할 수 있도록 계속 toorun 가상 컴퓨터의 예상된 비용을 hello를 보여 줍니다.  

![가상 컴퓨터의 크기를 조정하기 위한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>여러 SQL 데이터베이스의 비용 효율적인 솔루션 toomanage 성능 목표를 사용 하 여
Advisor는 Elastic Database 풀을 만들 경우 도움이 되는 SQL Server 인스턴스를 식별합니다. 탄력적 데이터베이스 풀 사용 패턴을 다양 한 여러 데이터베이스의 성능 목표 hello 간단 하 고 비용 효율적인 솔루션 toomanage를 제공 합니다. Azure 탄력적 풀에 대한 자세한 내용은 [Azure 탄력적 풀이란?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)을 참조하세요.

![Elastic Database 풀에 대한 Advisor 비용 권장 사항](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Tooaccess는 Azure 관리자의 권장 사항을 비용 하는 방법

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.

3. Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.  
 hello 관리자 대시보드 표시 됩니다.

4. Hello 관리자 대시보드에서 hello 클릭 **비용** 탭 합니다.

5. Hello 구독 원하는 tooreceive 권장 사항를 클릭 한 다음 선택 **위한 권장 사항 보기**합니다.

> [!NOTE]
> 관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다. 구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다. 이 작업은 *한 번만* 수행하면 됩니다. Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.

## <a name="next-steps"></a>다음 단계

toolearn 관리자 권장 사항에 대해 자세히 알아보려면
* [소개 tooAdvisor](advisor-overview.md)
* [시작](advisor-get-started.md)
* [Advisor 성능 권장 사항](advisor-cost-recommendations.md)
* [Advisor 고가용성 권장 사항](advisor-cost-recommendations.md)
* [Advisor 보안 권장 사항](advisor-cost-recommendations.md)
