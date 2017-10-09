---
title: "유사한 다른 Azure 서비스와 함께 Azure Mobile Engagement aaaComparing"
description: "Azure Mobile Engagement와 기타 유사한 Azure 서비스(HockeyApp, AppInsights, 알림 허브) 비교"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f114775-3a9a-4dd4-8d59-b10d1da9a68b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0859ae9980d0fa96ffbc0edfbd795ccc58d2c843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-azure-mobile-engagement-with-other-similar-azure-services"></a>Azure Mobile Engagement와 기타 유사한 Azure 서비스 비교
hello Microsoft Azure에서 제공 하는 서비스 목록이 현재까지 확장 되 고 때때로 궁금할 방금 읽기 또는 알려야 하는이 서비스와 다른 Azure Mobile Engagement 어떤가요. 이 문서는 tooclear hello 혼동을 시도 하 고 사용량에 대 한 가장 적합 한 Azure Mobile Engagement toochoose를 보냅니다. 

Azure Mobile Engagement는 구체적으로 대상 서비스 **디지털 마케팅/CMOs에 대 한** 하나에서 사용할 수 있지만 **모바일 앱 소유자 또는 게시자** tooincrease hello 사용, 보존 싶은 사람이 누가 및 가 모바일 앱의 경제적 가치 창출 합니다. 

*데이터 기반 통찰력을 앱 사용, 실시간 사용자 구분에 제공하고 컨텍스트 인식 푸시 알림 및 앱 내 메시징을 가능하게 하는 SaaS(Software-as-a-Service) 사용자 참여 플랫폼입니다.* 

해당 고유 가치 제안을 강조 표시 hello 주요 특성에 따라이 정의 분할 해야 합니다.

1. **컨텍스트 인식 푸시 알림 및 앱 내 메시징**
   
   이 hello 제품의 핵심 포커스 hello-대상 및 개인 설정 된 푸시 알림을 수행 합니다. 및이 toohappen에 대 한 풍부한 동작 분석 데이터를 수집 했습니다. 
2. **앱 사용에 대한 데이터 기반 통찰력**
   
   크로스 플랫폼 Sdk toocollect hello 동작 분석 hello 응용 프로그램 사용자에 대 한 제공합니다. Hello 앱 사용자가 hello 앱을 사용 하는 방법에 대해 살펴볼 때문에 (성능 분석)에 대해 hello 용어 동작 분석을 note 합니다. 오류, 충돌 등 하지만 즉 hello 제품의 핵심 초점을 hello에 대 한 기본 성능 분석 데이터는 수집지 않습니다. 
3. **실시간 사용자 구분**
   
   응용 프로그램 사용자 동작 분석 데이터를 수집한 후 허용 toosegment 다양 한 매개 변수를 기반으로 대상 그룹 및 수집 된 데이터 tooenable 있습니다 toorun 대상 푸시 캠페인입니다. 
4. **SaaS(Software-as-a-Service):**
   
   최적화 된 toointeract hello Azure 관리 포털에서 포털 따로 및 hello 앱 사용자에 대 한 풍부한 동작 분석을 보고 마케팅 푸시 캠페인을 실행 합니다. hello 제품은 tooget 순식간에 알아볼 수 넓히려는!   

이 손 모양에 차이점이이 집합으로 다음은 겉보기에 비슷한 다른 Azure 제품-에 대 한 비교 방법을 해당 hello 문서 기능 수준 비교를 수행 하지 있지만 제품에 가장 적합 한 더 많은 기반 시나리오 접근 방식을 toodefine 사용:

1. [HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello Microsoft 모바일 DevOps 솔루션입니다. 빌드 toobeta 테스터를 배포할 충돌 데이터를 수집 하며 사용자 피드백을 받을 수 있습니다. 또한 Visual Studio Team Services와 통합되어 있기 때문에 손쉬운 빌드 배포 및 작업 항목 통합이 가능합니다. 
   
   hello 여기 초점은 DevOps 및 hello 모바일 앱에 대 한 성능 분석 데이터를 수집 합니다. 두 HockeyApps 통합로 끝날 수도 있습니다 및 hello 수집 된 데이터의 일부 겹치는 경우에 hello 제품의 hello 코어 포커스가 다른 있고이 달성 하는 데 다른 때문에 Mobile Engagement 응용 프로그램에서 비정상적인 되지 않습니다. 사용자에 대 한 목표입니다.  
2. [Application Insights](../application-insights/app-insights-overview.md) 모바일 응용 프로그램에 서버 쪽 다음 응용 프로그램의 Application Insights toomonitor hello 웹 서버 쪽을 사용 하 여 이지만 hello 클라이언트 쪽 모바일 앱을 HockeyApp을 사용 해야 하는 경우. 
3. [알림 허브](https://azure.microsoft.com/services/notification-hubs/) hello 의미는 hello 모바일 앱에 통합 하는 SDK 필요 하지 않습니다 및 모바일 앱의 모든 권한을 가질 수 있으며 기본 태그 설정 기능을 사용 하 여 푸시 알림을 보낼 수 있습니다에서 간단한 서비스를 제공 합니다. 이 보내기/통신 정보에 대 한 더 작고 대상으로 하는 방법에 대 한 관심이 있는 모든 응용 프로그램 소유자에 대 한 훌륭한 즉시 tootheir 응용 프로그램 사용자 (브로드캐스트 tooa 큰 채우기). 
   
   기본 분할 기능을 매우 빠르게 알림을 보내는 방법에 hello 포커스를 여기 note 합니다. 

몇 가지 시나리오를 살펴보겠습니다.

1. Tim에는 사용자 용 모바일 앱을 게시 하는 Adventure Works 매장에서 hello 디지털 마케팅 팀의 일부입니다. Tim의 목표는 hello 사용자가 모바일 앱을 다운로드 하는 계속 toouse tooensure 것 자주 있습니다. 이 뿐 아니라 높아집니다. 브랜드를 사용한 연결 hello 응용 프로그램 사용자 뿐만 아니라 증가 경제적 가치 창출 hello 응용 프로그램 사용자 hello 모바일 앱을 사용 하 여 구매를 확인 하는 경우. 이 Tim 필요 대상 toosend 알림 toohello 응용 프로그램 사용자에 대 한 것이 유용할 수 있는, tooencourage 해당 tooopen 앱 hello tooit 자주 방문 하 여 합니다. 이 경우 Tim은 Mobile Engagement가 유용하다는 것을 알게 됩니다. 
2. Joann은 hello의 hello 개발 팀의 Adventure Works에서 모바일 응용 프로그램 및 예외, 충돌 하는 방법에 대 한 제품 toolog 세부 정보를 찾고 이며 응용 프로그램에서 성능 원격 분석을 가져오세요. 이 경우 Joann는 HockeyApp이 유용하다는 것을 알게 됩니다. Joann 통합을 만들 수 모두 HockeyApp 그녀의 개발자 포커스가 있는 시나리오 및 Azure Mobile Engagement tim의 hello에 대 한 최고 모두 동일한 앱 tooget hello 합니다. 
3. 로빈은 hello Contoso 뉴스 네트워크 및 hello 뉴스 경고가 트리거될으로 많은 조각화 없는 뉴스 경고 tooall 사용자 주요 아웃 toosend는 원하는 모든 모바일 앱의 hello 개발 팀의 일부입니다. 이 경우 Robin은 알림 허브가 유용하다는 것을 알게 됩니다. 
   그러나이 시나리오에서는 있기 hello 모바일 앱 완성 되어 감에 한지 요구 사항 toodo hello 응용 프로그램 사용자의 동작에 대 한 보다 다양 한 조각화 및 get 세부 정보. 이때 로빈 tooevaluate Azure Mobile Engagement 갖습니다. 

toorecap, hello Mobile Engagement의 목적은 하지 방금 toocollect 분석 되지 않습니다.-"Microsoft의 또 다른 분석 제품"입니다. 대상된 푸시 알림을 보내는 방법에 대 한 및 동작 분석 데이터를 수집한이 대상 지정에 대 한 이지만 hello 포커스가 스팸으로 상태가 되지 않으면 있도록 hello 대부분 의미 toohello 응용 프로그램의 사용자가 하도록 하는 푸시 알림을 보내는 방법에 유지 됩니다. 

자세한 내용은 Mobile Engagement에 대해 간단하게 설명하는 이 [짧은 비디오](mobile-engagement-overview.md) 를 살펴보세요. 

