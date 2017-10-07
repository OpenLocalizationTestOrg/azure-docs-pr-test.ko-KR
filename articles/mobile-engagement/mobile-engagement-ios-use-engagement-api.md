---
title: "iOS에서 aaaHow tooUse hello Engagement API"
description: "최신 iOS SDK-iOS에서 tooUse Engagement API hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>IOS에서 tooUse Engagement API hello 하는 방법
이 문서는 추가 기능 toohello 문서 어떻게 iOS에서 Engagement tooIntegrate: 방법을 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.

유의 하려는 경우 Engagement tooreport 응용 프로그램의 세션, 활동, 충돌 및 기술 정보는 다음 hello 가장 간단한 방법은 toomake을 모든 사용자 지정은 `UIViewController` hello 해당 개체가 상속 `EngagementViewController` 클래스 .

예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementViewController` toouse hello 필요 클래스 API 계약입니다.

hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다. Hello를 호출 하 여이 클래스의 인스턴스를 검색할 수 있습니다 `[EngagementAgent shared]` 정적 메서드 (해당 hello 참고 `EngagementAgent` 반환 된 개체는 단일).

모든 API를 호출 하기 전에, hello `EngagementAgent` hello 메서드를 호출 하 여 개체를 초기화 합니다`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Engagement 개념
hello 다음과 같은 부분이 구체화 hello 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) hello iOS 플랫폼에 대 한 합니다.

### <a name="session-and-activity"></a>`Session` 및 `Activity`
*활동* toosay hello 된 hello 응용 프로그램의 한 화면은 주로 *활동* hello 화면에 표시 되 고 hello 화면을 닫으면이 중지 될 때 시작:이 hello 경우 hello Engagement SDK가 통합 hello를 사용 하 여 `EngagementViewController` 클래스입니다.

하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다. 이렇게 하면 toosplit 각된 화면에 대 한 자세한 내용은 hello 사용 현황 (예: tooknown 얼마나 자주 및이 화면 안에 대화 상자 사용 되는 시간)이 화면의 여러 하위 부분 tooget 있습니다.

## <a name="reporting-activities"></a>활동 보고
### <a name="user-starts-a-new-activity"></a>사용자가 새 활동을 시작함
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Toocall 필요한 `startActivity()` 각 시간 hello 사용자 동작을 변경 합니다. 첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.

### <a name="user-ends-his-current-activity"></a>사용자가 현재 활동을 종료함
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> 수행 해야 **NEVER** toosplit 여러 세션으로 응용 프로그램의 용도 중 하나를 원하는 경우를 제외 하 고이 함수를 직접 호출: toothis 함수 끝 호출 hello 현재 세션에 즉시 등에 대 한 순차적 호출 너무`startActivity()`새 세션을 시작 합니다. 이 함수는 응용 프로그램이 닫힐 때 hello SDK에서 자동으로 호출 됩니다.
> 
> 

## <a name="reporting-events"></a>이벤트 보고
### <a name="session-events"></a>세션 이벤트
세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.

**추가 데이터가 없는 예제:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**추가 데이터가 있는 예제:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>독립 실행형 이벤트
반대 toosession 이벤트, 독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 사용할 수 있습니다.

**예제:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>오류 보고
### <a name="session-errors"></a>세션 오류
세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.

**예제:**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>독립 실행형 오류
반대 toosession 오류, 독립 실행형 오류 세션의 hello 컨텍스트 외부에서 사용할 수 있습니다.

**예제:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>작업 보고
**예제:**

로그인 프로세스의 기간을 tooreport hello 일정 있다고 가정 합니다.

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>작업 중 오류 보고
오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.

**예제:**

로그인 프로세스 동안 tooreport 오류가 원하는 있다고 가정 합니다.

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>작업 중의 이벤트
이벤트 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.

**예제:**

소셜 네트워크는 한 작업 tooreport hello 총 시간 사용는 hello 하는 동안 사용자가 연결 된 toohello 서버 한다고 가정 합니다. hello 사용자 친구에서 메시지를 받을 수, 작업 이벤트입니다.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>extras 매개 변수
임의의 데이터에 연결 된 tooevents, 오류, 활동 및 작업 가능 합니다.

이 데이터는 구조화할 수 있으며 iOS의 NSDictionary 클래스를 사용합니다.

extras는`arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` 또는 기타 `NSDictionary` 인스턴스를 포함할 수 있습니다.

> [!NOTE]
> hello 추가 매개 변수는 직렬화 JSON. Hello 위에서 설명한 것 보다 toopass 서로 다른 개체를 원하는 경우 hello 메서드를 클래스에 다음을 구현 해야 합니다.
> 
> -(NSString*) JSONRepresentation;
> 
> hello 메서드는 개체의 JSON 표현을 반환 합니다.
> 
> 

### <a name="example"></a>예제
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello에 `NSDictionary` hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
추가 항목은 너무 제한**1024** (한 번 인코딩된 json에서 hello Engagement 에이전트에 의해) 호출당 문자입니다.

Hello 앞의 예제 JSON 전송 toohello 서버 hello 58 자입니다.

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>응용 프로그램 정보 보고
Hello를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 수동으로 보고할 수 있습니다 `sendAppInfo:` 함수입니다.

이러한 정보를 점진적으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다.

와 같은 이벤트 extras hello `NSDictionary` 클래스는 사용 되는 tooabstract 응용 프로그램 정보, 배열은 또는 하위 사전 플랫 문자열 (JSON serialization 사용)으로 처리 됩니다.

**예제:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello에 `NSDictionary` hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
응용 프로그램 정보는 너무 제한적**1024** (한 번 인코딩된 json에서 hello Engagement 에이전트에 의해) 호출당 문자입니다.

Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.

    {"birthdate":"1983-12-07","gender":"female"}
