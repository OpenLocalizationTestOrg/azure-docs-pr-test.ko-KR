---
title: "Mobile Engagement Windows 유니버설 SDK 통합 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement의 Windows 유니버설 SDK 통합"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Azure Mobile Engagement의 Windows 유니버설 SDK 통합
이 문서에서는 일부 hello 통합 및 구성 옵션을 사용할 hello Azure Mobile Engagement Windows 유니버설 SDK에 대 한 설명입니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에 먼저 [15분 자습서](mobile-engagement-windows-store-dotnet-get-started.md)를 완료해야 합니다.

## <a name="advanced-features"></a>고급 기능
### <a name="reporting-features"></a>보고 기능
이러한 기능을 추가할 수 있습니다.

1. [고급 보고 옵션](mobile-engagement-windows-store-advanced-reporting.md)
2. [고급 구성 옵션](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>알림
[어떻게 Windows 유니버설 앱에서 toointegrate Reach (알림)](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>태그 계획 구현:
[어떻게 toouse hello 고급 Mobile Engagement API Windows 유니버설 앱에 태그 지정](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>릴리스 정보
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* 안정성 향상

이전 버전에 대 한 참조 hello [릴리스 정보를 완료 합니다.](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>업그레이드 절차
통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow를 할 수 있습니다. 참조 hello 완료 [업그레이드 절차](mobile-engagement-windows-store-upgrade-procedure.md)합니다. 예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.

### <a name="from-330-too340"></a>3.3.0에서 too3.4.0
#### <a name="test-logs"></a>테스트 로그
Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다. toocustomize, hello 속성 업데이트 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값 tooone `EngagementTestLogLevel` 열거형 예를 들어:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>리소스
hello Reach 오버레이 향상 되었습니다. Hello SDK NuGet 패키지 리소스의 일부인 것입니다.

Toohello hello SDK의 새 버전을 업그레이드 하는 동안 여부 hello에서 기존 파일의 리소스 폴더를 오버레이 tookeep 할지 여부를 선택할 수 있습니다.

* Hello 이전 오버레이를 작동 하거나 hello를 통합 하는 경우 `WebView` 요소를 수동으로 다음 결정할 수 있습니다 tookeep 종료 프로그램 파일, 계속 작동 합니다.
* tooupdate toohello 새 오버레이가 전체 바꾸기 hello `overlay` hello SDK 패키지에서 새 hello로 리소스에서 폴더 (UWP 앱: hello 업그레이드 후 hello 새 오버레이 폴더 % USERPROFILE %에서 얻을 수 있습니다\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)입니다.

> [!WARNING]
> Hello 새 오버레이 사용 하 여 hello 이전 버전에서 적용 된 모든 사용자 지정을 덮어씁니다.
> 
> 

### <a name="upgrade-from-older-versions"></a>이전 버전에서 업그레이드
[Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)

