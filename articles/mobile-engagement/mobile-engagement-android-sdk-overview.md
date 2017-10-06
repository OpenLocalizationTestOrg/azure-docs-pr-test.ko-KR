---
title: "Azure Mobile Engagement에 대 한 SDK 통합 aaaAndroid"
description: "설명 방법을 Android 앱에서 Azure Mobile Engagement SDK toointegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Azure Mobile Engagement용 Android SDK 통합
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

이 문서에서는 일부 hello 통합 및 구성 옵션을 사용할 Azure Mobile Engagement Android SDK에 대 한 설명입니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>고급 기능
### <a name="reporting-features"></a>보고 기능
이러한 기능을 추가할 수 있습니다.

1. [고급 보고 옵션](mobile-engagement-android-advanced-reporting.md)
2. [위치 보고 옵션](mobile-engagement-android-location-reporting.md)
3. [고급 구성 옵션](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>알림:
[어떻게 Android 앱에서 toointegrate Reach (알림)](mobile-engagement-android-integrate-engagement-reach.md)

1. Google 클라우드 메시징 (GCM): [어떻게 tooIntegrate Mobile Engagement와 GCM](mobile-engagement-android-gcm-integrate.md)
2. Amazon 장치 메시징 (ADM): [어떻게 tooIntegrate Mobile Engagement와 ADM](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>태그 계획 구현:
[어떻게 toouse hello 고급 Mobile Engagement Android 앱의 API를 태그 지정](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>릴리스 정보

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* 호출할 때 거의 발생할 수 있는 충돌을 해결 `EngagementAgentUtils.isInDedicatedEngagementProcess`, hello에서 사용 되는 `EngagementApplication` 클래스입니다.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 지원 (이전 버전의 hello SDK는 Android 8에서 작동 하지 것입니다).
* 지원 라이브러리에 대한 종속성이 더 이상 없습니다.
* `EngagementFragmentActivity` 클래스를 제거합니다.
* 기한 너무[배경 실행 제한](https://developer.android.com/preview/features/background.html) Android 8에서 백그라운드로 로그 지연 될 수 있습니다 hello 사용자 hello 장치 상호 작용할 때까지, 푸시 캠페인에 영향을 미치게 됩니다이 **Delivered** 및 **시스템 알림 표시** 통계 hello 장치 중지 된 경우 지연 되 고 (hello 알림이 표시 됩니다, 링 되며 문제 없이 실시간으로 진동).
* 기한 너무[배경 위치 제한](https://developer.android.com/preview/features/background-location-limits.html), Android 8 hello 실시간으로 위치 백그라운드에서 자주 업데이트 되지 것입니다.

모든 버전에 대 한 참조 hello [릴리스 정보 완료](mobile-engagement-android-release-notes.md)합니다.

## <a name="upgrade-procedures"></a>업그레이드 절차
이전 버전의 SDK를 응용 프로그램에 이미 통합한 경우에는 [업그레이드 절차](mobile-engagement-android-upgrade-procedure.md)를 참조하세요.

