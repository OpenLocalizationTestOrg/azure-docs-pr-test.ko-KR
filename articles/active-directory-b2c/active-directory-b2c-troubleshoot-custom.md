---
title: "응용 프로그램 통찰력 tootroubleshoot 사용자 지정 정책-Azure AD B2C | Microsoft Docs"
description: "어떻게 toosetup Application Insights tootrace hello 사용자 지정 정책 실행"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: 로그 수집

이 문서에서는 사용자 지정 정책을 사용하여 문제를 진단할 수 있도록 Azure AD B2C에서 로그를 수집하는 단계를 설명합니다.

>[!NOTE]
>현재 hello 여기에 설명 된 자세한 활동 로그 만들어진 **전용** tooaid 사용자 지정 정책 개발에서 합니다. 프로덕션에서 개발 모드를 사용하지 않습니다.  로그를 개발 하는 동안 tooand hello id 공급자에서 보내는 클레임을 모두 수집 합니다.  프로덕션 환경에서 사용 하는 경우 hello 개발자는 각자 소유한 hello App Insights 로그에서 수집 된 PII (개인적으로 식별이 가능한 정보)에 대 한 책임을 가정 합니다.  Hello 정책에 배치 되 면 이러한 자세한 로그만 수집 됩니다 **개발 모드**합니다.


## <a name="use-application-insights"></a>Application Insights 사용

Azure AD B2C 데이터 tooApplication Insights 보내기 위한 기능을 지원 합니다.  Application Insights 방법을 toodiagnose 예외를 제공 하 고 응용 프로그램 성능 문제를 시각화 합니다.

### <a name="setup-application-insights"></a>Application Insights 설정

1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다. 사용자가 hello 테 넌 트의 Azure 구독 (하지 Azure AD B2C 테 넌 트)를 확인 합니다.
1. 클릭 **+ 새로 만들기** hello 왼쪽 탐색 메뉴에 있습니다.
1. **Application Insights**를 검색하고 선택한 다음 **만들기**를 클릭합니다.
1. Hello 양식을 작성 하 고 클릭 **만들기**합니다. 선택 **일반** hello에 대 한 **응용 프로그램 종류**합니다.
1. Hello 리소스를 만든 후에 hello Application Insights 리소스를 엽니다.
1. 찾을 **속성** hello 왼쪽 메뉴에서 항목을 클릭 합니다.
1. 복사 hello **계측 키** hello 다음 섹션에 저장 합니다.

### <a name="set-up-hello-custom-policy"></a>Hello 사용자 지정 정책 설정

1. Hello RP 파일 (예를 들어 SignUpOrSignin.xml)을 엽니다.
1. 다음 특성 toohello hello 추가 `<TrustFrameworkPolicy>` 요소:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. 이미 존재 하지 않으면 자식 노드를 추가 `<UserJourneyBehaviors>` toohello `<RelyingParty>` 노드. Hello 직후 위치 여야 합니다.`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Hello 노드 다음에 오는 hello의 자식으로 추가 `<UserJourneyBehaviors>` 요소입니다. 있는지 tooreplace 확인 `{Your Application Insights Key}` hello로 **계측 키** hello 이전 섹션에서 Application Insights에서 가져온 합니다.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`양호 하지만 높은 볼륨에서 제한 된 개발에 대 한 hello 처리 파이프라인을 통해 ApplicationInsights tooexpedite hello 원격 분석을 지시합니다.
  * `ClientEnabled="true"`페이지 보기 및 클라이언트 쪽 오류 (필요 없음)을 추적 하기 위한 hello ApplicationInsights 클라이언트 쪽 스크립트를 보냅니다.
  * `ServerEnabled="true"`사용자 지정 이벤트 tooApplication 통찰력으로 기존 UserJourneyRecorder JSON hello 하는 보냅니다.
샘플:

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. Hello 정책을 업로드 합니다.

### <a name="see-hello-logs-in-application-insights"></a>Hello Application Insights에서 로그를 참조 하십시오.

>[!NOTE]
> Application Insights에서 새 로그가 표시되기까지 짧은 지연 시간이 발생합니다(5분 미만).

1. Hello에서 만든 hello Application Insights 리소스를 열고 [Azure 포털](https://portal.azure.com)합니다.
1. Hello에 **개요** 메뉴를 클릭 **분석**합니다.
1. Application Insights에서 새 탭을 엽니다.
1. 다음은 toosee hello 로그를 사용할 수 있습니다 쿼리 목록

| 쿼리 | 설명 |
|---------------------|--------------------|
traces | 모든 Azure AD B2C에 의해 생성 된 hello 로그 참조 |
traces \| where timestamp > ago(1d) | 참조 하는 모든 hello 로그에서 생성 된 Azure AD B2C hello에 대 한 마지막 날

hello 항목 걸릴 수 있습니다.  자세히 보기에 대 한 tooCSV 내보냅니다.

Hello 분석 도구에 대 한 자세히 알아볼 수 있습니다 [여기](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)합니다.

>[!NOTE]
>hello 커뮤니티에는 사용자의 여행 뷰어 toohelp identity 개발자가 개발 했습니다.  Microsoft에서 지원되지 않고 엄격하게 그대로 사용할 수 없습니다.  Application Insights 인스턴스에서 읽고 hello 사용자 여행 이벤트의 올바른 구조 보기를 제공 합니다.  Hello 소스 코드를 받으며 사용자 고유의 솔루션에 배포 합니다.

>[!NOTE]
>현재 hello 여기에 설명 된 자세한 활동 로그 만들어진 **전용** tooaid 사용자 지정 정책 개발에서 합니다. 프로덕션에서 개발 모드를 사용하지 않습니다.  로그를 개발 하는 동안 tooand hello id 공급자에서 보내는 클레임을 모두 수집 합니다.  프로덕션 환경에서 사용 하는 경우 hello 개발자는 각자 소유한 hello App Insights 로그에서 수집 된 PII (개인적으로 식별이 가능한 정보)에 대 한 책임을 가정 합니다.  Hello 정책에 배치 되 면 이러한 자세한 로그만 수집 됩니다 **개발 모드**합니다.

[지원되지 않는 사용자 지정 정책 샘플 및 관련된 도구에 대한 GitHub 리포지토리](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>다음 단계

Hello 데이터를 이해 하는 Application Insights toohelp 탐색 방법을 toodeliver 고유한 identity 환경을 작동 하는 기본 B2C Id 경험 프레임 워크를 hello 합니다.
