---
title: "Azure 모바일 앱과 iOS에서 aaaAdd 인증"
description: "자세한 방법을 다양 한 AAD, Google, Facebook, Twitter 및 Microsoft를 포함 하 여 id 공급자를 통해 iOS 앱의 toouse Azure 모바일 앱 tooauthenticate 사용자입니다."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>인증 tooyour iOS 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

이 자습서에서는 인증 toohello 추가한 [iOS 빠른 시작] 지원 되는 id 공급자를 사용 하 여 프로젝트. 이 자습서는 hello 기반 [iOS 빠른 시작] 자습서 먼저 완료 해야 합니다.

## <a name="register"></a>인증에 대 한 앱을 등록 하 고 hello 응용 프로그램 서비스 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가

보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.  Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.  이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.  그러나 선택한 어떤 URL 체계도 사용 가능합니다.  고유 tooyour 모바일 응용 프로그램 이어야 합니다.  th 서버 쪽에서 tooenable hello 리디렉션:

1. Hello에 [Azure 포털], 응용 프로그램 서비스를 선택 합니다.

2. Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.

3. 클릭 **Azure Active Directory** hello에서 **인증 공급자** 섹션.

4. 집합 hello **관리 모드** 너무**고급**합니다.

5. Hello에 **외부 리디렉션 Url 허용**, 입력 `appname://easyauth.callback`합니다.  hello _appname_ 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.  이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).  Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.

6. **확인**을 클릭합니다.

7. **Save**를 클릭합니다.

## <a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Xcode에서 눌러 **실행** toostart hello 앱. Hello 앱 tooaccess 인증 되지 않은 사용자로 백 엔드를 시도 하기 때문에 예외가 발생 하지만 hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.

## <a name="add-authentication"></a>인증 tooapp 추가
**Objective-C**:

1. Mac에서 열고 *QSTodoListViewController.m* Xcode에서 hello 다음 메서드 추가:

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    변경 *google* 너무*microsoftaccount*, *twitter*, *facebook*, 또는 *windowsazureactivedirectory* Google을 id 공급자로 사용 하지 않는 경우. Facebook을 사용하는 경우 [앱에서 Facebook 도메인을 허용 목록에 추가해야 합니다][1].

    Hello 대체 **urlScheme** 응용 프로그램에 대 한 고유한 이름을 사용 합니다.  hello urlScheme 해야 수 hello 동일 hello에 지정 된 URL 체계가 프로토콜 hello로 **외부 리디렉션 Url 허용** hello Azure 포털의. 인증 요청이 완료 된 후 hello urlScheme hello 인증 콜백 tooswitch 백 tooyour 응용 프로그램에서 사용 됩니다.

2. 대체 `[self refresh]` 에 `viewDidLoad` 에 *QSTodoListViewController.m* 코드 다음 hello로:

    ```Objective-C
    [self loginAndGetData];
    ```

3. 열기 hello `QSAppDelegate.h` 파일 및 코드 다음 hello 추가:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. 열기 hello `QSAppDelegate.m` 파일 및 코드 다음 hello 추가:

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   직접 hello 줄 읽기 전에이 코드를 추가 `#pragma mark - Core Data stack`합니다.  대체는 _appname_ 작동이 hello urlScheme 값 1 단계에서 사용한 것입니다.

5. 열기 hello `AppName-Info.plist` (응용 프로그램의 hello 이름으로 교체 AppName) 파일을 찾아 hello 코드 다음에 추가 합니다.

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    이 코드는 hello 안에 배치 해야 `<dict>` 요소입니다.  Hello 대체 _appname_ 문자열 (배열 내에서 **CFBundleURLSchemes**) 1 단계에서 선택한 hello 응용 프로그램 이름으로 합니다.  또한이 변경을 수행할 수 있습니다 이러한 hello plist에 편집기-hello 클릭 `AppName-Info.plist` XCode tooopen hello plist 편집기에서 파일입니다.

    Hello 대체 `com.microsoft.azure.zumo` 에 대 한 문자열 **CFBundleURLName** 프로그램 apple 번들 식별자입니다.

6. 키를 눌러 *실행* toostart 응용 프로그램에서는 hello 및 다음에 로그인 합니다. 로그인 할 때 수 tooview hello 할 일 목록 이어야 하 고 업데이트 해야 합니다.

**Swift**:

1. Mac에서 열고 *ToDoTableViewController.swift* Xcode에서 hello 다음 메서드 추가:

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    변경 *google* 너무*microsoftaccount*, *twitter*, *facebook*, 또는 *windowsazureactivedirectory* Google을 id 공급자로 사용 하지 않는 경우. Facebook을 사용하는 경우 [앱에서 Facebook 도메인을 허용 목록에 추가해야 합니다][1].

    Hello 대체 **urlScheme** 응용 프로그램에 대 한 고유한 이름을 사용 합니다.  hello urlScheme 해야 수 hello 동일 hello에 지정 된 URL 체계가 프로토콜 hello로 **외부 리디렉션 Url 허용** hello Azure 포털의. 인증 요청이 완료 된 후 hello urlScheme hello 인증 콜백 tooswitch 백 tooyour 응용 프로그램에서 사용 됩니다.

2. Hello 줄을 제거 `self.refreshControl?.beginRefreshing()` 및 `self.onRefresh(self.refreshControl)` 끝날 때 `viewDidLoad()` 에 *ToDoTableViewController.swift*합니다. 호출을 너무 추가`loginAndGetData()` 그 자리에:

    ```swift
    loginAndGetData()
    ```

3. 열기 hello `AppDelegate.swift` 파일을 다음 줄 toohello hello 추가 `AppDelegate` 클래스:

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    Hello 대체 _appname_ 작동이 hello urlScheme 값 1 단계에서 사용한 것입니다.

4. 열기 hello `AppName-Info.plist` (응용 프로그램의 hello 이름으로 교체 AppName) 파일을 찾아 hello 코드 다음에 추가 합니다.

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    이 코드는 hello 안에 배치 해야 `<dict>` 요소입니다.  Hello 대체 _appname_ 문자열 (배열 내에서 **CFBundleURLSchemes**) 1 단계에서 선택한 hello 응용 프로그램 이름으로 합니다.  또한이 변경을 수행할 수 있습니다 이러한 hello plist에 편집기-hello 클릭 `AppName-Info.plist` XCode tooopen hello plist 편집기에서 파일입니다.

    Hello 대체 `com.microsoft.azure.zumo` 에 대 한 문자열 **CFBundleURLName** 프로그램 apple 번들 식별자입니다.

5. 키를 눌러 *실행* toostart 응용 프로그램에서는 hello 및 다음에 로그인 합니다. 로그인 할 때 수 tooview hello 할 일 목록 이어야 하 고 업데이트 해야 합니다.

App Service 인증은 Apples Inter-App Communication을 사용합니다.  이 주제에 대 한 자세한 내용은 참조 toohello [Apple 설명서][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure 포털]: https://portal.azure.com

[iOS 빠른 시작]: app-service-mobile-ios-get-started.md

