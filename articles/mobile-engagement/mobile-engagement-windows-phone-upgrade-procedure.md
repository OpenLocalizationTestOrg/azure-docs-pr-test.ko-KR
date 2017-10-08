---
title: "aaaWindows Phone Silverlight SDK 업그레이드 절차"
description: "Azure Mobile Engagement용 Windows Phone Silverlight SDK 업그레이드 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Windows Phone Silverlight SDK 업그레이드 절차
통합 한 경우 이미이 SDK의 이전 버전 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다. 예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.

## <a name="from-200-too330"></a>2.0.0에서 too3.3.0
### <a name="test-logs"></a>테스트 로그
Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다. toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>1.1.1에서 too2.0.0
hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다. 

> [!IMPORTANT]
> Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다. Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.
> 
> 

이전 버전에서 마이그레이션하려는 경우 하십시오 hello Capptain 웹 사이트 toomigrate too1.1.1를 먼저 참조 다음 절차를 수행 하는 hello를 적용 합니다.

### <a name="nuget-package"></a>NuGet 패키지
**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.

### <a name="applying-mobile-engagement"></a>Mobile Engagement 적용
hello SDK hello 단어를 사용 하 여 `Engagement`합니다. Tooupdate 프로젝트 toomatch 해야이 변경 합니다.

Toouninstall 현재 Capptain nuget 패키지를 해야합니다. Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다. Tookeep 하려는 경우 해당 파일의 복사본을 확인 합니다.

그 후 hello 새 Microsoft Azure Engagement nuget 패키지를 프로젝트에 설치 합니다. 해당 패키지는 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)에서 직접 찾을 수 있습니다. 프로젝트 참조를 Engagement에서 사용 되는 및 hello 새 Engagement DLL tooyour 추가 하는 모든 리소스 파일에이 작업으로 바꿉니다.

해야 tooclean 프로젝트 참조 Capptain DLL 참조를 삭제 하 여 합니다. 이 적용 하지 않을 경우 hello 버전 Capptain의 충돌 하는 및 오류가 발생 합니다.

Capptain 리소스를 사용자 지정한 경우 이전 파일 내용을 복사한 hello 새 Engagement 파일에 붙여 넣습니다. Xaml 및 cs 파일을 모두 업데이트 toobe 한지 note 하십시오.

이러한 단계가 완료 되 면 hello 새 Engagement 참조에 의해 tooreplace 이전 Capptain 참조가 있습니다.

1. 모든 Capptain 네임 스페이스 업데이트 toobe가 있어야 합니다.
   
    마이그레이션 전:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    마이그레이션 후:
   
        using Microsoft.Azure.Engagement;
2. "Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.
   
    마이그레이션 전:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    마이그레이션 후:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.
   
    마이그레이션 전:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    마이그레이션 후:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Hello Capptain 그림 등의 다른 리소스에 대 한,이 또한 있다가 이름이 바뀐된 toouse "계약" 점에 유의 하십시오.

### <a name="application-id--sdk-key"></a>응용 프로그램 ID/SDK 키
Engagement에서는 연결 문자열을 사용합니다. 응용 프로그램 ID 및 Mobile Engagement와 SDK 키 toospecify 없는, 하기만 하면 toospecify 연결 문자열입니다. EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.

hello Engagement 구성에서 설정할 수 있습니다 프로그램 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.

이 파일 toospecify를 편집 합니다.

* `<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열

런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에에서 표시 됩니다.

### <a name="items-name-change"></a>항목 이름 변경
*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다. 마찬가지로 *Capptain* 너무*Engagement*합니다.

일반적으로 사용되는 Capptain 항목의 예제:

* CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.
* CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.
* CapptainReach의 이름은 EngagementReach로 바뀌었습니다.
* CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.
* GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.

이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.

