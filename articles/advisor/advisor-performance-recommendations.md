---
title: "aaaAzure 관리자 성능 권장 사항 | Microsoft Docs"
description: "Azure 배포의 관리자 toooptimize hello 성능을 사용 합니다."
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
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Advisor 성능 권장 사항

Azure 관리자 성능 권장 사항 hello 속도 및 비즈니스에 중요 한 응용 프로그램의 응답성 향상에 도움이. Hello에 성능 권장 사항 관리자에서 얻을 수 있습니다 **성능** hello 관리자 대시보드 탭 합니다.

![Advisor 성능 탭](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>SQL DB Advisor로 데이터베이스 성능 개선

Advisor는 모든 Azure 리소스에 대한 권장 사항을 일관되고 통합된 보기로 표시합니다. 와 통합 SQL 데이터베이스 관리자 toobring 하면 SQL Azure 데이터베이스의 hello 성능 개선을 위한 권장 사항입니다. SQL 데이터베이스 관리자 사용 기록 분석 하 여 SQL Azure 데이터베이스의 hello 성능을 평가 합니다. 그런 다음 hello 데이터베이스의 일반 워크 로드를 실행 하는 데 가장 적합 한 권장 사항을 제공 합니다. 

> [!NOTE]
> tooget 권장 사항, 데이터베이스 약 1 주, 사용이 있어야 하며 해당 주 있어야 일부 일관 된 동작 합니다. SQL Database Advisor는 일관성 있는 쿼리 패턴을 임의 활동 버스트보다 더욱 쉽게 최적화할 수 있습니다.

SQL Database Advisor에 대한 자세한 내용은 [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/)를 참조하세요.

![SQL Database 권장 사항](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Redis Cache 성능 및 안정성 향상

Advisor는 높은 메모리 사용량, 서버 부하, 네트워크 대역폭 또는 많은 수의 클라이언트 연결이 성능이 부정적인 영향을 미칠 수 있는 Redis Cache 인스턴스를 식별합니다. 관리자에서 제공 하 모범 사례 권장 사항 toohelp 잠재적 문제를 방지 합니다. Redis Cache 권장 사항에 대한 자세한 내용은 [r](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor)를 참조하세요.


## <a name="improve-app-service-performance-and-reliability"></a>App Service 성능 및 안정성 향상

Azure Advisor는 App Services 환경을 개선하고 관련 플랫폼 기능을 검색하기 위한 모범 사례 권장 사항을 통합합니다. App Services 권장 사항 예제:
* 완화 옵션을 사용하여 메모리나 CPU 리소스가 앱 런타임에서 소모되는 인스턴스 검색
* Web Apps 및 데이터베이스를 함께 배치할 때 성능을 향상시키고 비용을 절감할 수 있는 인스턴스 검색 

App Services 권장 사항에 대한 자세한 내용은 [Azure App Service에 대한 모범 사례](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/)를 참조하세요.
![App Services 권장 사항](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>어떻게 tooaccess 관리자에서 성능 권장 사항

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.

3. Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.  
 hello 관리자 대시보드 표시 됩니다.

4. Hello 관리자 대시보드에서 hello 클릭 **성능** 탭 합니다.

5. Hello 구독 원하는 tooreceive 권장 사항를 클릭 한 다음 선택 **위한 권장 사항 보기**합니다.

> [!NOTE]
> 관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다. 구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다. 이 작업은 *한 번만* 수행하면 됩니다. Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.

## <a name="next-steps"></a>다음 단계

toolearn 관리자 권장 사항에 대해 자세히 알아보려면

* [소개 tooAdvisor](advisor-overview.md)
* [Advisor 시작](advisor-get-started.md)
* [Advisor 비용 권장 사항](advisor-performance-recommendations.md)
* [Advisor 고가용성 권장 사항](advisor-high-availability-recommendations.md)
* [Advisor 보안 권장 사항](advisor-security-recommendations.md)

