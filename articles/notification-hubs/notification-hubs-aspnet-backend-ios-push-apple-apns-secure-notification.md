---
title: "알림 허브 푸시 Secure aaaAzure"
description: "보안 toosend Azure에서 알림을 tooan iOS 앱을 강제 하는 방법을 알아봅니다. 코드 샘플은 Objective-C 및 C#으로 작성되었습니다."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure 알림 허브 보안 푸시
> [!div class="op_single_selector"]
> * [Windows 범용](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>개요
Microsoft Azure에서 푸시 알림 지원을 사용 하면 tooaccess 크게 간소화 됩니다. 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에서 푸시 알림의 hello 구현 하는 사용 하기 쉬운, 다중 플랫폼, 수평 확장 된 푸시 인프라 플랫폼입니다.

때로는 tooregulatory 또는 보안 제약 조건 때문 응용 프로그램에서 hello 표준 푸시 알림 인프라를 통해 전송 될 수 없는 hello 알림 tooinclude를 할 수도 있습니다. 이 자습서에서는 tooachieve hello 클라이언트 장치 및 앱 백 엔드에서 hello 간에 안전 하 고 인증 된 연결을 통해 중요 한 정보를 전송 하 여 동일한 환경을 hello 하는 방법을 설명 합니다.

상위 수준 hello 흐름은 다음과 같습니다.

1. hello 앱 백 엔드에서:
   * 백 엔드 데이터베이스에 보안 페이로드를 저장합니다.
   * 이 알림 toohello 장치 (보안 정보 없음 전송 됨)의 hello ID를 전송 합니다.
2. 응용 프로그램에 액세스 hello 알림을 받은 경우 hello 장치 hello:
   * hello 장치가 hello 백 엔드에서 요청 hello 보안 페이로드를 연결합니다.
   * hello 앱 hello 장치에 대 한 알림으로 hello 페이로드를 표시할 수 있습니다.

hello 사용자가 로그인 한 후 toonote 하의 hello 흐름 이전 (및이 자습서에서는) 가정 hello 장치 로컬 저장소에 인증 토큰을 저장 합니다. 이 hello 장치는이 토큰을 사용 하 여 hello 알림 보안 페이로드를 검색할 수 있는 완전히 원활한 환경을 보장 합니다. 응용 프로그램에서 hello 장치에서 인증 토큰을 저장 하지 않으면 이러한 토큰을 만료 될 수 있습니다를 hello hello 알림을 받으면 장치 응용 프로그램 해야 표시 제네릭 알림을 hello 사용자 toolaunch hello 앱 메시지를 표시 합니다. 그런 다음 hello 앱 hello 사용자를 인증 하 고 hello 알림 페이로드를 보여 줍니다.

이 보안 밀어넣기 자습서에서는 어떻게 toosend 푸시 알림 안전 하 게 합니다. hello을 기반으로 하는 hello 자습서 [사용자에 게 알림](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 자습서에서는 하므로 먼저 해당 자습서의 hello 단계를 완료 해야 합니다.

> [!NOTE]
> 이 자습서에서는 [알림 허브 시작(iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Hello iOS 프로젝트를 수정 합니다.
앱 백 엔드에서 toosend 정당한 hello 수정 했으므로 *id* 는 알림의 있는 toochange 프로그램 iOS 앱 toohandle 알림과 콜백을 백 엔드 tooretrieve hello 보안 메시지 toobe 표시 합니다.

tooachieve toowrite hello 논리 tooretrieve hello 보안의 콘텐츠를 앱 백 엔드에서 hello 했으므로이 목표입니다.

1. **AppDelegate.m**, hello 백 엔드에서 전송 hello 알림 id를 처리 하므로 자동 알림에 대 한 hello 앱 레지스터 있는지 확인 합니다. Hello 추가 **UIRemoteNotificationTypeNewsstandContentAvailability** didFinishLaunchingWithOptions 옵션:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. 사용자 **AppDelegate.m** 선언 뒤 hello로 구현 섹션이 hello 위쪽에 추가 합니다.
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. 그런 다음 hello 구현 섹션 hello hello 자리 표시자를 대체, 코드 다음에 추가 `{back-end endpoint}` 이전에 얻은 백 엔드에 대 한 hello 끝점과:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. 이제 toohandle hello 수신 알림을 했으며 tooretrieve hello 콘텐츠 toodisplay 위에 hello 메서드를 사용 합니다. 첫째, 했으므로 tooenable iOS 앱 toorun hello 백그라운드에서 푸시 알림의 받을 때입니다. **XCode**hello 왼쪽된 패널에 응용 프로그램 프로젝트를 선택한 다음 클릭 hello에 기본 응용 프로그램 대상 **대상** hello 가운데 창에서 섹션.
2. 클릭 한 다음 프로그램 **기능** hello 최상위 중앙 창에서 탭 하 고 hello 확인 **원격 알림** 확인란을 선택 합니다.
   
    ![][IOS1]
3. **AppDelegate.m** hello 다음 메서드 toohandle 푸시 알림 추가:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    누락 된 인증 헤더 속성 또는 hello 백 엔드가 거부 된 것이 좋습니다 toohandle hello 경우 인지 note 합니다. 대상 사용자 경험에 대부분의이 경우 hello 특정 처리에 따라 달라 집니다. 한 가지 방법은 toodisplay hello 사용자 tooauthenticate tooretrieve hello 실제 알림에 대 한 제네릭 프롬프트로 알림입니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
toorun hello 응용 프로그램, 다음 hello지 않습니다.

1. XCode에서 실제 iOS 장치 (푸시 알림이 hello 시뮬레이터에서 작동 하지 것입니다) hello 앱을 실행 합니다.
2. Hello iOS 앱 UI 사용자 이름 및 암호를 입력 합니다. 모든 문자열을 지정할 수 있습니다 이러한 있지만 해야만 해당 hello 동일한 값입니다.
3. Hello iOS 앱 UI의에서 클릭 **로그인**합니다. 그리고 나서 **푸시 보내기**를 클릭합니다. 알림 센터에 표시 되는 hello 보안 알림을 표시 되어야 합니다.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
