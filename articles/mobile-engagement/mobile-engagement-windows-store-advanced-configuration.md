---
title: "구성에 대 한 Windows 유니버설 앱 Engagement SDK aaaAdvanced"
description: "Windows 유니버설 앱과 Azure Mobile Engagement 사용에 대한 고급 구성 옵션"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Windows 유니버설 앱 Engagement SDK에 대한 고급 구성
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

이 절차에서는 설명 방법을 tooconfigure Azure Mobile Engagement Android 앱에 대 한 다양 한 구성 옵션입니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>고급 구성
### <a name="disable-automatic-crash-reporting"></a>자동 작동 중단 보고를 사용하지 않도록 설정
Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다. 그러면 처리되지 않은 예외가 발생할 때 Engagement에서 아무 작업도 수행하지 않습니다.

> [!WARNING]
> 이 기능을 사용 하지 않도록 설정할 경우 Engagement hello 크래시를 보내지 않습니다 응용 프로그램에서 처리 되지 않은 충돌이 일어나면 **AND** hello 세션 및 작업 닫히지 않습니다.
> 
> 

toodisable 자동 충돌 보고를 선언한 hello 방식에 따라 구성을 사용자 지정:

#### <a name="from-engagementconfigurationxml-file"></a>`EngagementConfiguration.xml` 파일에서
보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>런타임에 `EngagementConfiguration` 개체에서
보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>실시간 보고 사용 안 함
기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다. 더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우를 표준 시간으로 한 번에 모두 있습니다. 이를 "버스트 모드"라고 합니다.

따라서 toodo hello 메서드를 호출 합니다.

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

hello 인수에는 **밀리초**합니다. Tooreactivate hello 실시간 로깅 원할 때마다 모든 매개 변수 없이 또는 hello 0 값을 가진 hello 메서드를 호출 합니다.

버스트 모드 약간 hello 배터리 수명 늘어나지만 hello Engagement 모니터에 영향을 주: 모든 세션 및 작업 기간 둥근된 toohello 버스트 임계값 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 됩니다. 30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다. 저장 된 로그는 제한 된 too300 항목입니다. 너무 길게 보내면 일부 로그가 손실될 수 있습니다.

> [!WARNING]
> 두 번째 hello 버스트 임계값은 1 보다 작은 구성된 tooa 기간 수 없습니다. 이렇게 하면 자동으로 toohello 기본값을 다시 0 초로 설정 및는 hello SDK hello 오류와 함께 추적을 보여 줍니다. 이 트리거 hello SDK tooreport hello 로그인 실시간 합니다.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
