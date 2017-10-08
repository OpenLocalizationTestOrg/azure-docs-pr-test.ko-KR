---
title: "aaaRegister hello 현재 사용자에 게 웹 API를 사용 하 여 푸시 알림 | Microsoft Docs"
description: "어떻게 toorequest 푸시 알림 등록에 Azure 알림 허브를 사용 하 여 iOS 앱에 ASP.NET Web API에서 등록을 수행할 때에 대해 알아봅니다."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>ASP.NET을 사용 하 여 hello 현재 사용자에 게 푸시 알림 등록
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>개요
이 항목에서는 방법을 toorequest 푸시 알림 등록에 Azure 알림 허브와 ASP.NET Web API에서 등록을 수행할 때를 보여 줍니다. 이 항목 확장 hello 자습서 [알림 허브와 사용자에 게 알림]합니다. 이미 완료 해야 해당 자습서 toocreate hello 인증 모바일 서비스에 필요한 hello 단계입니다. Hello에 대 한 자세한 내용은 알림 사용자 시나리오, 참조 [알림 허브와 사용자에 게 알림]합니다.

## <a name="update-your-app"></a>앱 업데이트
1. 프로그램 MainStoryboard_iPhone.storyboard hello 개체 라이브러리에서 다음과 같은 구성 요소가 hello를 추가 합니다.
   
   * **레이블**: "푸시 알림 허브와 tooUser"
   * **레이블**: "InstallationId"
   * **레이블**: "User"
   * **텍스트 필드**: "User"
   * **레이블**: "Password"
   * **텍스트 필드**: "Password"
   * **단추**: "Login"
     
     이 시점에서 스토리 보드 hello 다음과 같습니다.
     
      ![][0]
2. Hello 도우미 편집기에서 모든 전환 hello 컨트롤에 대 한 콘센트 및 전화할 hello 뷰-컨트롤러 (대리자)를 사용 하 여 hello 텍스트 필드를 연결 만들고 만들기는 **동작** hello에 대 한 **로그인** 단추입니다.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. 이라는 클래스를 만들 **DeviceInfo**, 복사 hello hello 파일 DeviceInfo.h의 hello 인터페이스 섹션에 코드를 다음 및:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Hello 코드 hello DeviceInfo.m 파일의 hello 구현 섹션에서 다음을 복사 합니다.
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. PushToUserAppDelegate.h에서 다음 속성 singleton hello를 추가 합니다.
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Hello에 **didFinishLaunchingWithOptions** PushToUserAppDelegate.m에 메서드 추가 코드 다음 hello:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    첫 번째 줄 hello를 hello 초기화 **DeviceInfo** singleton입니다. hello 두 번째 줄 시작 hello 등록 푸시 알림이 표시 되어 있는 hello를 이미 완료 했다고 [알림 허브 시작] 자습서입니다.
7. PushToUserAppDelegate.m, hello 메서드를 구현 **didRegisterForRemoteNotificationsWithDeviceToken** 프로그램 AppDelegate에서 코드 다음 hello 추가:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Hello 요청에 대 한 hello 장치 토큰을 설정합니다.
   
   > [!NOTE]
   > 이때 이 메서드에 다른 코드가 있어서는 안 됩니다. 호출 toohello 이미 있는 경우 **registerNativeWithDeviceToken** hello 완료 되 면 추가 된 메서드가 [알림 허브 시작](/manage/services/notification-hubs/get-started-notification-hubs-ios/) 주석 아웃 하거나 제거 해야 하는 자습서 호출 합니다.
   > 
   > 
8. Hello PushToUserAppDelegate.m 파일에서 처리기 메서드를 다음 hello를 추가 합니다.
   
   * 응용 프로그램 (void):(UIApplication *) 응용 프로그램 didReceiveRemoteNotification:(NSDictionary *) 사용자 정보 {NSLog (@"% @", 사용자 정보);   UIAlertView * 경고 = [[UIAlertView alloc] initWithTitle:@"Notification" 메시지: [사용자 정보 objectForKey:@"inAppMessage"] 대리자: nil cancelButtonTitle: @"확인" otherButtonTitles:nil, nil];   [경고 표시]; }
   
   이 메서드는 실행 중인 앱에서 알림을 수신 하는 경우 hello UI에서에서 경고를 표시 합니다.
9. Hello 다음 구현에에서 hello PushToUserViewController.m 파일과 반환 hello 키보드를 엽니다.
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Hello에 **viewDidLoad** 메서드 hello PushToUserViewController.m 파일에서 다음과 같이 hello installationId 레이블을 초기화 합니다.
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Hello 다음과 같은 PushToUserViewController.m 인터페이스에서 속성을 추가 합니다.
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. 그런 다음 구현에 따라 hello를 추가 합니다.
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. 복사 hello 다음 hello에 코드 **로그인** XCode에서 만든 처리기 메서드:
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    이 메서드는 설치 ID와 채널에 대 한 푸시 알림을 가져오고 hello 장치 유형 함께 보냅니다, 그리고 toohello 웹 API를 만드는 메서드를 등록 하는 알림 허브에 인증 합니다. 이 웹 API는 [알림 허브와 사용자에 게 알림]에서 정의했습니다.

Hello 클라이언트 응용 프로그램 업데이트 했으므로 반환 toohello [알림 허브와 사용자에 게 알림] 알림 허브를 사용 하 여 hello 모바일 서비스 toosend 알림을 업데이트 합니다.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[알림 허브와 사용자에 게 알림]: /manage/services/notification-hubs/notify-users-aspnet

[알림 허브 시작]: /manage/services/notification-hubs/get-started-notification-hubs-ios
