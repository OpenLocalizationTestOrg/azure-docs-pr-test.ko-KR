---
title: ".NET 백 엔드와 iOS 용 aaaAzure 알림 허브 사용자에 게 알림"
description: "Azure에서 toosend 알림 toousers 강제 하는 방법에 대해 알아봅니다. Objective C 및 hello 백 엔드에 대 한 hello.NET API로 작성 된 코드 샘플입니다."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>.NET 백 엔드를 통한 Azure 알림 허브의 iOS 사용자 알림
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>개요
Azure의 푸시 알림 지원을 사용 하면 tooaccess는 사용 하기 쉬운, 다중 플랫폼, 및 수평 확장형 푸시 인프라를 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에 대 한 푸시 알림 hello 구현이 크게 간소화 플랫폼입니다. 이 자습서에서는 toouse Azure 알림 허브 toosend 특정 장치에서 알림을 tooa 특정 응용 프로그램 사용자를 강제 하는 방법을 보여 줍니다. ASP.NET WebAPI 백 엔드는 사용 되는 tooauthenticate 클라이언트 및 toogenerate 알림 hello 지침 항목에 나와 있는 것 처럼 [앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)합니다.

> [!NOTE]
> 이 자습서에서는 [알림 허브 시작(iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다 이 자습서는 또한 hello 필수 toohello [(iOS) 푸시 Secure](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) 자습서입니다.
> 백 엔드 서비스로 toouse 모바일 앱을 원하는 경우 참조 hello [모바일 앱 시작 푸시](../app-service-mobile/app-service-mobile-ios-get-started-push.md)합니다.
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>iOS 앱 수정
1. 열기 hello 단일 페이지 앱 보기 hello에서 만든 [알림 허브 (iOS) 시작](notification-hubs-ios-apple-push-notification-apns-get-started.md) 자습서입니다.
   
   > [!NOTE]
   > 이 섹션에서는 빈 조직 이름을 사용하여 프로젝트를 구성했다고 가정합니다. 그렇지 않으면 tooprepend 사용자 조직의 이름 tooall 클래스 이름이 필요 합니다.
   > 
   > 
2. 프로그램 Main.storyboard hello 개체 라이브러리에서 아래 hello 스크린 샷에 표시 된 hello 구성 요소를 추가 합니다.
   
    ![][1]
   
   * **사용자 이름**: 자리 표시자 텍스트와 A UITextField *사용자 이름 입력*, 즉시 hello 아래에 결과 레이블 및 제한 된 toohello 왼쪽 및 오른쪽 여백을 보내고 hello 아래에 결과 레이블 보냅니다.
   * **암호**: 자리 표시자 텍스트와 A UITextField *암호 입력*, 즉시 아래 hello 사용자 이름 텍스트 필드 및 제한 된 toohello 왼쪽 및 오른쪽 여백 및 hello 사용자 이름 텍스트 필드 아래에 있습니다. Hello 확인 **텍스트 입력 보안** hello 특성 검사기에서에서 아래 옵션 *반환 키*합니다.
   * **로그인**: A UIButton hello 암호 텍스트 필드 아래에 즉시 레이블이 지정 되며이 hello의 선택을 취소 **Enabled** hello 특성 검사기에서에서 아래 옵션 *콘텐츠 컨트롤*
   * **WNS**: 레이블과 스위치 tooenable 보내는 hello Windows 알림 서비스 알림 경과 했는데도 문제가 있다면 hello 허브에서 설치 하는 경우. Hello 참조 [Windows 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 자습서입니다.
   * **GCM**: 레이블과 스위치 tooenable 보내는 hello Cloud Messaging 알림 tooGoogle 경과 했는데도 문제가 있다면 hello 허브에서 설치 하는 경우. [Android 시작](notification-hubs-android-push-notification-google-gcm-get-started.md) 자습서를 참조하세요.
   * **APNS**: 레이블과 스위치 tooenable 보내는 hello 알림 toohello Apple 플랫폼 알림 서비스.
   * **Recipent 사용자 이름**: 자리 표시자 텍스트와 A UITextField *받는 사용자 이름 태그*즉시 hello GCM 아래에 레이블을 표시 하 고 제한 된 toohello 왼쪽 및 오른쪽 여백 및 레이블을 GCM hello 아래에 있습니다.

    일부 구성 요소는 hello에 추가 된 [알림 허브 (iOS) 시작](notification-hubs-ios-apple-push-notification-apns-get-started.md) 자습서입니다.

1. **Ctrl** hello 보기 tooViewController.h hello 구성 요소에서 끌어서 이러한 새 콘센트에 추가 합니다.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. Hello 다음 추가 ViewController.h에서 `#define` import 문을 바로 아래 합니다. 대체 hello *< 백 엔드 끝점 입력\>*  hello hello 이전 단원의 toodeploy 앱 백 사용 하는 대상 URL로 자리 표시자입니다. 예: *http://you_backend.azurewebsites.net*
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. 프로젝트에서 만드는 새 **Cocoa 터치 클래스** 라는 **RegisterClient** 만든 ASP.NET 백 엔드 hello로 toointerface 합니다. Hello 클래스에서 상속 만들기 `NSObject`합니다. Hello 코드 hello RegisterClient.h에서에서 다음을 추가 합니다.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Hello RegisterClient.m 업데이트 hello `@interface` 섹션:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Hello 대체 `@implementation` hello RegisterClient.m 코드 다음 hello로의 섹션입니다.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    hello 지침 문서에서 설명 하는 hello 논리를 구현 하는 위의 hello 코드 [앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) tooyour 앱 백 엔드 및 NSUserDefaults toolocally 저장소 hello tooperform REST 호출 NSURLSession를 사용 하 여 registrationId hello 알림 허브에서 반환 합니다.

    이 클래스의 속성을 필요로 하는 참고 **authorizationHeader** toobe 제대로 순서 toowork에 설정 합니다. 이 속성은 hello **ViewController** hello 로그인 후 클래스입니다.

1. ViewController.h에서 RegisterClient.h에 대한 `#import` 문을 추가합니다. 그런 다음 장치 토큰 hello에 대 한 선언을 추가 하 고 tooa 참조 `RegisterClient` hello에 대 한 인스턴스 `@interface` 섹션:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. ViewController.m에서 hello에 private 메서드 선언을 추가 `@interface` 섹션:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> hello 다음 코드 조각은 아닙니다. 보안 인증 체계의 hello hello 구현을 바꿔야 **createAndSetAuthenticationHeaderWithUsername:AndPassword:** 특정 인증 메커니즘 hello 레지스터 클라이언트 클래스, 예: OAuth Active Directory에서 사용 하는 인증 토큰 toobe를 생성 됩니다.
> 
> 

1. 그런 다음 hello `@implementation` ViewController.m 섹션 hello 설정 hello 장치 토큰 및 인증 헤더에 대 한 hello 구현을 추가 하는 코드를 다음 추가 합니다.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    설정을 hello 장치 토큰 hello 로그인 단추를 사용 하는 방법을 note 합니다. Hello 로그인 동작의 일부로 hello 뷰-컨트롤러와 hello 앱 백 엔드에서 푸시 알림에 등록 때문입니다. 따라서 바람직하지 작업 toobe 로그에 액세스할 수 있는 hello 장치 토큰을 제대로 설정한 때까지 합니다. 후자의 hello 하기 전에 발생 하는 hello 이전으로 hello 푸시 등록에서 로그인 hello를 분리할 수 있습니다.
2. ViewController.m에서 hello에 대 한 조각 tooimplement hello 동작 메서드를 다음을 사용 하 여 프로그램 **로그인** 단추와 toosend hello 알림 메시지 사용 하는 메서드는 ASP.NET 백 엔드 hello 합니다.
   
       - (IBAction) LogInAction: 보낸 사람 (id) {/ 인증 헤더 생성 및 레지스터 클라이언트 NSString * 사용자 이름에 설정 / 자체 = 합니다. UsernameField.text;   NSString 암호 자체 = 합니다. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie 자체; =   [self.registerClient registerWithDeviceToken:self.deviceToken 태그: nil andCompletion:^(NSError* error) {경우 (! 오류) {dispatch_async(dispatch_get_main_queue(), ^ {selfie 합니다. SendNotificationButton.enabled = YES;               [자체 MessageBox:@"Success" message:@"Registered 했습니다!"];을 (를));}}];을 (를)

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Hello pns와 사용자 이름이 태그를 hello REST URL toohello ASP.NET 백 엔드 NSURL * requestURL와 매개 변수로 전달 = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            NSMutableURLRequest 요청 [NSMutableURLRequest requestWithURL:requestURL] =;    [요청 setHTTPMethod:@"POST"];

            Hello 모의 authenticationheader 클라이언트에서에서 가져올 hello 레지스터 NSString authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [요청 setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            Hello 알림 메시지 본문을 추가 [setValue:@"application/json;charset=utf-8 요청" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody 요청: [dataUsingEncoding:NSUTF8StringEncoding 메시지]];

            Hello ASP.NET 백 엔드 NSURLSessionDataTask * dataTask에서 hello 알림 보내기 REST API를 실행 합니다. [세션 dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *= 오류) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) 응답;        경우 (오류 | | httpResponse.statusCode! = 200) {NSString* 상태 = [%에 대 한 상태 NSString stringWithFormat:@"Error @: %d\nError: %@\n", pns httpResponse.statusCode, 오류];            dispatch_async(dispatch_get_main_queue(), ^ {/ / 모든 3 PNS 호출 수 정보 tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status] 수도 있기 때문에 텍스트 추가];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Hello에 대 한 hello 작업 업데이트 **알림 보내기** toouse hello ASP.NET 백 엔드 단추 보내고 tooany PNS에 스위치 사용 하도록 설정 합니다.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. 함수에서 **ViewDidLoad**, hello tooinstantiate hello RegisterClient 인스턴스 뒤에 추가 하 고 텍스트 필드에 대 한 hello 대리자를 설정 합니다.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. 이제 **AppDelegate.m**, hello 메서드의 모든 hello 콘텐츠 제거 **응용 프로그램: didRegisterForPushNotificationWithDeviceToken:** 및 보기 hello 있는지 toomake 다음 hello로 바꾸기 컨트롤러는 APNs에서 검색 된 hello 최신 장치 토큰을 포함 되어 있습니다.
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. 마지막에 **AppDelegate.m**, hello 메서드 뒤에 있는지 확인 합니다.
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>테스트 hello 응용 프로그램
1. XCode에서 실제 iOS 장치 (푸시 알림이 hello 시뮬레이터에서 작동 하지 것입니다) hello 앱을 실행 합니다.
2. Hello iOS 앱 UI 사용자 이름 및 암호를 입력 합니다. 이러한 모든 문자열 수 있지만 둘 다 있어야 hello 동일한 문자열 값입니다. 그런 다음 **Log In**을 클릭합니다.
   
    ![][2]
3. 등록 성공을 알리는 팝업이 표시됩니다. **확인**을 클릭합니다.
   
    ![][3]
4. Hello에 **받는 사용자 이름 태그* 텍스트 필드에 다른 장치에서 hello 등록에 사용 되는 hello 사용자 이름 태그를 입력 합니다.
5. 알림 메시지를 입력하고 **알림 보내기**를 클릭합니다.  Hello 받는 사람 사용자 이름 태그로 등록 hello 장치만 hello 알림 메시지가 표시 됩니다.  Toothose 사용자만 전송 됩니다.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
