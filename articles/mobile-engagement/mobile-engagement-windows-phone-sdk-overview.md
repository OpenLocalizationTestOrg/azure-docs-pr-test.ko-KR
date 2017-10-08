---
title: "aaaAzure Mobile Engagement Windows Phone Silverlight SDK 개요 | Microsoft Docs"
description: "Hello Azure Mobile Engagement에 대 한 Windows Phone Silverlight SDK의 개요"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Azure Mobile Engagement의 Windows Phone Silverlight SDK 개요
방법에 tooget hello 세부 정보를 여기서 시작 toointegrate는 Windows Phone Silverlight 앱에 Azure Mobile Engagement 합니다. Toogive 원하는 경우 완료 될 때 try 했는지 먼저 확인 해야 하면 우리의 [15 분 자습서](mobile-engagement-windows-phone-get-started.md)합니다.

Toosee hello 클릭 [SDK 콘텐츠](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>통합 절차
1. 여기에서 시작: [방법을 Windows Phone Silverlight 앱에서 Mobile Engagement toointegrate](mobile-engagement-windows-phone-integrate-engagement.md)
2. 알림: [방법을 Windows Phone Silverlight 앱에서 toointegrate Reach (알림)](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. 계획 구현 태그: [어떻게 toouse hello 고급 Mobile Engagement API Windows Phone Silverlight 앱에 태그 지정](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>릴리스 정보
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Hello의 일부 *MicrosoftAzure.MobileEngagement* Nuget 패키지 **v3.4.1**

* 안정성 향상

이전 버전에 대 한 hello를 참조 하십시오 [릴리스 정보를 완료 합니다.](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>업그레이드 절차
통합 한 경우 이미이 SDK의 이전 버전 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다. 참조 hello 완료 [업그레이드 절차](mobile-engagement-windows-phone-upgrade-procedure.md)합니다. 예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.

### <a name="from-200-too330"></a>2.0.0에서 too3.3.0
#### <a name="test-logs"></a>테스트 로그
Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다. toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>이전 버전에서 업그레이드
[Upgrade Procedures](mobile-engagement-windows-phone-upgrade-procedure.md)

