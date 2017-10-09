---
title: "aaaIntroduction tooAzure 관리자 | Microsoft Docs"
description: "Azure 관리자 toooptimize Azure 배포를 사용 합니다."
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
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>소개 tooAzure 관리자

Azure 관리자 및 해당 주요 기능에 대해 알아보고 질문과 대답 toofrequently를 확인 합니다.

## <a name="what-is-advisor"></a>Advisor란?
관리자는 개인 설정 된 클라우드 컨설턴트 때 도움이 되는 모범 사례 toooptimize Azure 배포를 수행 합니다. 리소스 구성 및 사용 원격 분석을 분석 하 고 수 있는 솔루션 높일 hello 비용 효율성, 성능, 고가용성 및 Azure 리소스의 보안을 권장 합니다.

Advisor를 사용하면 다음과 같은 작업을 수행할 수 있습니다.
* 사전 대응이 가능하고, 실행 가능하고, 개인화된 모범 사례 권장 사항 
* 전체 Azure 지출 기회 tooreduce 확인할 경우 hello 성능, 보안 및 사용자 리소스의 고가용성을 향상 합니다.
* 온라인으로 작업이 제안되는 권장 사항 가져오기

Hello를 통해 관리자에 액세스할 수 있습니다 [Azure 포털](https://aka.ms/azureadvisordashboard)합니다. Toohello에 로그인 [포털](https://portal.azure.com)선택, **찾아보기**, 한 다음 너무 스크롤하여**Azure 관리자**합니다. hello 관리자 대시보드에 선택한 구독에 대 한 개인 설정 된 권장 사항 표시 됩니다. 

hello 권장 사항은 네 가지 범주로 구분 됩니다. 

* **고가용성**: tooensure 고 업무에 중요 한 응용 프로그램의 hello 연속성을 개선 합니다. 자세한 내용은 [Advisor 고가용성 권장 사항](advisor-high-availability-recommendations.md)을 참조하세요.

* **보안**: toodetect 위협 요소 및 취약성 toosecurity 위반을 발생 시킬 수 있는 합니다. 자세한 내용은 [Advisor 보안 권장 사항](advisor-security-recommendations.md)을 참조하세요.

* **성능**: 응용 프로그램의 tooimprove hello 속도입니다. 자세한 내용은 [Advisor 성능 권장 사항](advisor-performance-recommendations.md)을 참조하세요.

* **비용**: toooptimize 줄이고 전반적인 Azure 지출 합니다. 자세한 내용은 [Advisor 비용 권장 사항](advisor-cost-recommendations.md)을 참조하세요.

  ![Advisor 권장 사항 유형](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> 관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다. 구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다. 이 작업은 *한 번만* 수행하면 됩니다. Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.

항목에 대 한 자세한 권장 사항을 toolearn는 클릭할 수 있습니다. Tootake 활용 하는 기회를 수행 하거나 문제를 해결할 수 있는 작업에 대해 알 수 있습니다. 

Advisor는 인라인 작업 또는 설명서 링크가 있는 권장 사항을 제공합니다. 인라인 작업을 클릭 하면 "안내 사용자 여행" tooimplement를 통해 이동 것입니다. 설명서 링크를 클릭 하면 toodocumentation toomanually hello 동작을 구현 하는 방법을 설명 하는 링크 합니다. 

Advisor는 시간별로 권장 사항을 업데이트합니다. 권장 사항을에 tootake 즉각적인 조치 않으려는 경우 지정 된 시간 동안 다시 알림 하거나 닫을 수도 있습니다. 

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="how-do-i-access-advisor"></a>Advisor에 액세스하려면 어떻게 해야 하나요?
Hello를 통해 관리자에 액세스할 수 있습니다 [Azure 포털](https://aka.ms/azureadvisordashboard)합니다. Toohello에 로그인 [포털](https://portal.azure.com)선택, **찾아보기**, 한 다음 너무 스크롤하여**Azure 관리자**합니다. hello 관리자 대시보드에 선택한 구독에 대 한 개인 설정 된 권장 사항 표시 됩니다. 

또한 hello 가상 컴퓨터 리소스 블레이드를 통해 관리자 권장 구성을 볼 수 있습니다. 가상 컴퓨터를 선택 하 고 hello 메뉴의 tooAdvisor 권장 사항을 스크롤하십시오. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>사용 권한 수행할 tooaccess Advisor 필요 합니까?

관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다. 구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다. 이 작업은 *한 번만* 수행하면 됩니다. Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.

### <a name="how-often-are-advisor-recommendations-updated"></a>Advisor 권장 사항은 얼마나 자주 업데이트되나요?

Advisor 권장 사항은 시간별로 업데이트됩니다.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Advisor는 어떤 리소스에 대해 권장 사항을 제공하나요?

Advisor는 가상 컴퓨터, 가용성 집합, Application Gateway, App Services, SQL Server, SQL Database 및 Redis Cache에 대한 권장 사항을 제공합니다.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>권장 사항을 다시 알리거나 해제할 수 있나요?

toosnooze 또는 권장 구성을 해제, hello 클릭 **다시 알림** 단추 또는 링크입니다. 기간 선택 하거나 선택 알림을 시간을 지정할 수 **Never** toodismiss hello 권장 합니다.

## <a name="next-steps"></a>다음 단계

toolearn 관리자 권장 사항에 대해 자세히 알아보려면

* [Advisor 시작](advisor-get-started.md)
* [Advisor 고가용성 권장 사항](advisor-high-availability-recommendations.md)
* [Advisor 보안 권장 사항](advisor-security-recommendations.md)
* [Advisor 성능 권장 사항](advisor-performance-recommendations.md)
* [Advisor 비용 권장 사항](advisor-cost-recommendations.md)
