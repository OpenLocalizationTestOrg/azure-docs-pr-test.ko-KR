---
title: "Windows Phone Silverlight에서 Engagement API aaaHow tooUse hello"
description: "TooUse는 Windows Phone Silverlight에서 Engagement API hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>TooUse는 Windows Phone Silverlight에서 Engagement API hello 하는 방법
이 문서는 추가 기능 toohello 문서 [방법을 Windows Phone Silverlight 앱에서 Mobile Engagement toointegrate](mobile-engagement-windows-phone-integrate-engagement.md)합니다. 어떻게 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.

응용 프로그램의 세션, 활동, 충돌 및 기술 정보 Engagement tooreport 원하는 경우 가장 간단한 hello toomake 모든를 방식으로 프로그램 `PhoneApplicationPage` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.

예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementPage` toouse hello 필요 클래스 API 계약입니다.

hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다. 통해 toothose 메서드에 액세스할 수 있습니다 `EngagementAgent.Instance`합니다.

Hello 에이전트 모듈 초기화 되지 않은 경우에에 각 호출 toohello API 지연 되 고 hello 에이전트를 사용할 수 있는 경우 다시 실행 됩니다.

## <a name="engagement-concepts"></a>Engagement 개념
다음 부분 hello hello Windows Phone 플랫폼에 대 한 hello Mobile Engagement 개념을 구체화 합니다.

### <a name="session-and-activity"></a>`Session` 및 `Activity`
*활동* toosay hello 된 hello 응용 프로그램의 한 페이지는 주로 *활동* hello 페이지가 표시 되 고 hello 페이지를 닫을 때 중지 될 때 시작: hello 좋다고 때 hello SDK 서비스는 hello를 사용 하 여 통합 된 `EngagementPage` 클래스입니다.

하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다. 이렇게 하면 toosplit 지정한 페이지에 대 한 자세한 내용은 hello 사용 현황 (예: tooknown 얼마나 자주 및이 페이지 안에 대화 상자 사용 되는 시간)이이 페이지의 여러 하위 부분 tooget 있습니다.

## <a name="reporting-activities"></a>활동 보고
### <a name="user-starts-a-new-activity"></a>사용자가 새 활동을 시작함
#### <a name="reference"></a>참조
            void StartActivity(string name, Dictionary<object, object> extras = null)

Toocall 필요한 `StartActivity()` 각 시간 hello 사용자 동작을 변경 합니다. 첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.

> [!IMPORTANT]
> hello SDK hello 응용 프로그램이 닫힐 때 자동으로 hello EndActivity 메서드를 호출 합니다. 따라서 좋습니다 toocall hello StartActivity 메서드 hello 사용자 변경 및 hello이이 메서드를 호출 하는 이후 EndActivity 메서드 강제로 hello 현재 세션 toobe tooNEVER 호출의 hello 작업이 종료 될 때마다 합니다.
> 
> 

#### <a name="example"></a>예제
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>사용자가 현재 활동을 종료함
#### <a name="reference"></a>참조
            void EndActivity()

Toocall 필요한 `EndActivity()` hello 사용자 자신의 마지막 활동을 완료 하는 때 한 번 이상. 이 hello Engagement SDK hello 사용자가 현재 유휴 및 hello 사용자 세션에 필요 하며 toobe 닫힌 hello 세션 시간 제한 한 번 만료 됩니다를 통해 알립니다 (호출 하는 경우 `StartActivity()` hello 세션 계속 단순히 hello 세션 제한 시간 만료 되기 전에).

#### <a name="example"></a>예제
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>작업 보고
### <a name="start-a-job"></a>작업 시작
#### <a name="reference"></a>참조
            void StartJob(string name, Dictionary<object, object> extras = null)

시간 동안 hello 작업 tootrack의 작업을 사용할 수 있습니다.

#### <a name="example"></a>예제
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>작업 종료
#### <a name="reference"></a>참조
            void EndJob(string name)

추적 작업에 의해 작업이 종료 되는 즉시 hello 작업 이름을 제공 하 여이 작업에 대 한 hello 작업 끝 메서드를 호출 해야 합니다.

#### <a name="example"></a>예제
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>이벤트 보고
이벤트에는 다음의 세 가지 유형이 있습니다.

* 독립 실행형 이벤트
* 세션 이벤트
* 작업 이벤트

### <a name="standalone-events"></a>독립 실행형 이벤트
#### <a name="reference"></a>참조
            void SendEvent(string name, Dictionary<object, object> extras = null)

독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 발생할 수 있습니다.

#### <a name="example"></a>예제
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>세션 이벤트
#### <a name="reference"></a>참조
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.

#### <a name="example"></a>예제
**데이터 제외:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**데이터 포함:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>작업 이벤트
#### <a name="reference"></a>참조
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

작업 이벤트는 일반적으로 사용 되는 tooreport hello 동작 하는 동안 사용자가 수행 합니다.

#### <a name="example"></a>예제
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>오류 보고
오류에는 다음의 세 가지 유형이 있습니다.

* 독립 실행형 오류
* 세션 오류
* 작업 오류

### <a name="standalone-errors"></a>독립 실행형 오류
#### <a name="reference"></a>참조
            void SendError(string name, Dictionary<object, object> extras = null)

반대 toosession 오류 세션의 hello 컨텍스트 외부에서 독립 실행형 오류가 발생할 수 있습니다.

#### <a name="example"></a>예제
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>세션 오류
#### <a name="reference"></a>참조
            void SendSessionError(string name, Dictionary<object, object> extras = null)

세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.

#### <a name="example"></a>예제
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>작업 오류
#### <a name="reference"></a>참조
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.

#### <a name="example"></a>예제
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>작동 중단 보고
hello 에이전트 충돌와 두 개의 메서드 toodeal를 제공합니다.

### <a name="send-an-exception"></a>예외 보내기
#### <a name="reference"></a>참조
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>예
언제든지 다음을 호출하여 예외를 보낼 수 있습니다.

            EngagementAgent.Instance.SendCrash(aCatchedException);

Hello에 대 한 선택적 매개 변수 tooterminate hello engagement 세션을 사용할 수도 있습니다 동시 hello 크래시를 보내는 것 보다 합니다. toodo를 호출 합니다.

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

이렇게 하면 hello 세션 및 작업 닫힙니다 hello 크래시 보내는 직후 합니다.

### <a name="send-an-unhandled-exception"></a>처리되지 않은 예외 보내기
#### <a name="reference"></a>참조
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

또한 engagement 메서드 toosend 처리 되지 않은 예외를 제공합니다. Hello silverlight UnhandledException 이벤트 처리기 내에서 사용할 때 특히 유용 합니다.

이 방법은 **항상** 호출 된 후 hello engagement 세션 및 작업을 종료 합니다.

#### <a name="example"></a>예제
Tooimplement를 사용할 수 있습니다 (특히 경우 hello 자동 충돌 보고 서비스의 기능을 사용 하지 않도록 설정한) 자신만 UnhandledException 처리기입니다. 예를 들어 hello에에서 `Application_UnhandledException` hello 방식의 `App.xaml.cs` 파일:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>참조
            void OnActivated(ActivatedEventArgs e)

Hello 사용자 컨트롤에서 벗어나면 앞으로 응용 프로그램 hello Deactivated 이벤트 발생 한 후 hello 운영 체제는 유휴 상태가 tooput hello 응용 프로그램을 시도 합니다. 그런 다음 hello 응용 프로그램 삭제 표시 됩니다. 이 프로세스에서 응용 프로그램 종료 되지만 hello 상태 hello 응용 프로그램과 hello hello 응용 프로그램 내에서 개별 페이지에 대 한 일부 데이터 보존 됩니다.

Tooinsert 있는 `EngagementAgent.Instance.OnActivated(e)` hello에 `Application_Activated` hello App.xaml.cs 파일 tooreset hello hello 응용 프로그램 삭제 표시 됨으로 되었을 때 Engagement 에이전트에서에서 메서드.

### <a name="example"></a>예제
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>장치 ID
            String GetDeviceId()

이 메서드를 호출 하 여 hello engagement 장치 id를 얻을 수 있습니다.

## <a name="extras-parameters"></a>extras 매개 변수
임의의 데이터에 연결 된 tooan 이벤트, 오류, 작업 또는 작업 가능 합니다. 사전을 사용하여 이러한 데이터를 구조화할 수 있습니다. 모든 형식의 키와 값을 사용할 수 있습니다.

기타 데이터 tooinsert 추가 기능에서 사용자 정의 형식을 선택 해야 하므로 tooadd이이 형식에 대 한 데이터 계약 직렬화 됩니다.

### <a name="example"></a>예제
아래 예제에서는 "Person"이라는 새 클래스를 만듭니다.

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

그런 다음 추가 됩니다 한 `Person` 인스턴스 tooan 추가 합니다.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> 다른 형식의 개체를 두면 해당 tostring () 메서드 구현된 tooreturn 사람이 읽을 수 있는 문자열 인지 확인 합니다.
> 
> 

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*$`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
추가 항목은 너무 제한**1024** 호출당 문자.

## <a name="reporting-application-information"></a>응용 프로그램 정보 보고
### <a name="reference"></a>참조
            void SendAppInfo(Dictionary<object, object> appInfos)

수동으로 hello SendAppInfo() 함수를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 보고할 수 있습니다.

이러한 정보를 점진적으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다. 이벤트, 기타 같이 사전을 사용 하 여\<개체, 개체\> tooattach 내용은 합니다.

### <a name="example"></a>예제
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*$`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
응용 프로그램 정보는 너무 제한적**1024** 호출당 문자.

Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>로깅
### <a name="enable-logging"></a>로깅 사용
hello SDK hello IDE 콘솔에서 구성 된 tooproduce 테스트 로그 수 있습니다.
이러한 로그는 기본적으로 활성화되지 않습니다. toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
