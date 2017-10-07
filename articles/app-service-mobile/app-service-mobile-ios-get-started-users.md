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
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="82cb7-103">인증 tooyour iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="82cb7-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="82cb7-104">이 자습서에서는 인증 toohello 추가한 [iOS 빠른 시작] 지원 되는 id 공급자를 사용 하 여 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="82cb7-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="82cb7-105">이 자습서는 hello 기반 [iOS 빠른 시작] 자습서 먼저 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="82cb7-106"><a name="register"></a>인증에 대 한 앱을 등록 하 고 hello 응용 프로그램 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="82cb7-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="82cb7-107"><a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가</span><span class="sxs-lookup"><span data-stu-id="82cb7-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="82cb7-108">보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="82cb7-109">Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="82cb7-110">이 자습서에서는 전체적으로 URL 체계 _appname_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="82cb7-111">그러나 선택한 어떤 URL 체계도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="82cb7-112">고유 tooyour 모바일 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="82cb7-113">th 서버 쪽에서 tooenable hello 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="82cb7-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="82cb7-114">Hello에 [Azure 포털], 응용 프로그램 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="82cb7-115">Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="82cb7-116">클릭 **Azure Active Directory** hello에서 **인증 공급자** 섹션.</span><span class="sxs-lookup"><span data-stu-id="82cb7-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="82cb7-117">집합 hello **관리 모드** 너무**고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="82cb7-118">Hello에 **외부 리디렉션 Url 허용**, 입력 `appname://easyauth.callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="82cb7-119">hello _appname_ 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="82cb7-120">이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).</span><span class="sxs-lookup"><span data-stu-id="82cb7-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="82cb7-121">Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="82cb7-122">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-122">Click **OK**.</span></span>

7. <span data-ttu-id="82cb7-123">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-123">Click **Save**.</span></span>

## <span data-ttu-id="82cb7-124"><a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한</span><span class="sxs-lookup"><span data-stu-id="82cb7-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="82cb7-125">Xcode에서 눌러 **실행** toostart hello 앱.</span><span class="sxs-lookup"><span data-stu-id="82cb7-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="82cb7-126">Hello 앱 tooaccess 인증 되지 않은 사용자로 백 엔드를 시도 하기 때문에 예외가 발생 하지만 hello *TodoItem* 테이블에는 이제 인증이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="82cb7-127"><a name="add-authentication"></a>인증 tooapp 추가</span><span class="sxs-lookup"><span data-stu-id="82cb7-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="82cb7-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="82cb7-128">**Objective-C**:</span></span>

1. <span data-ttu-id="82cb7-129">Mac에서 열고 *QSTodoListViewController.m* Xcode에서 hello 다음 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="82cb7-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="82cb7-130">변경 *google* 너무*microsoftaccount*, *twitter*, *facebook*, 또는 *windowsazureactivedirectory* Google을 id 공급자로 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="82cb7-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="82cb7-131">Facebook을 사용하는 경우 [앱에서 Facebook 도메인을 허용 목록에 추가해야 합니다][1].</span><span class="sxs-lookup"><span data-stu-id="82cb7-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="82cb7-132">Hello 대체 **urlScheme** 응용 프로그램에 대 한 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="82cb7-133">hello urlScheme 해야 수 hello 동일 hello에 지정 된 URL 체계가 프로토콜 hello로 **외부 리디렉션 Url 허용** hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="82cb7-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="82cb7-134">인증 요청이 완료 된 후 hello urlScheme hello 인증 콜백 tooswitch 백 tooyour 응용 프로그램에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="82cb7-135">대체 `[self refresh]` 에 `viewDidLoad` 에 *QSTodoListViewController.m* 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="82cb7-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="82cb7-136">열기 hello `QSAppDelegate.h` 파일 및 코드 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="82cb7-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="82cb7-137">열기 hello `QSAppDelegate.m` 파일 및 코드 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="82cb7-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="82cb7-138">직접 hello 줄 읽기 전에이 코드를 추가 `#pragma mark - Core Data stack`합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="82cb7-139">대체는 _appname_ 작동이 hello urlScheme 값 1 단계에서 사용한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="82cb7-140">열기 hello `AppName-Info.plist` (응용 프로그램의 hello 이름으로 교체 AppName) 파일을 찾아 hello 코드 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="82cb7-141">이 코드는 hello 안에 배치 해야 `<dict>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="82cb7-142">Hello 대체 _appname_ 문자열 (배열 내에서 **CFBundleURLSchemes**) 1 단계에서 선택한 hello 응용 프로그램 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="82cb7-143">또한이 변경을 수행할 수 있습니다 이러한 hello plist에 편집기-hello 클릭 `AppName-Info.plist` XCode tooopen hello plist 편집기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="82cb7-144">Hello 대체 `com.microsoft.azure.zumo` 에 대 한 문자열 **CFBundleURLName** 프로그램 apple 번들 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="82cb7-145">키를 눌러 *실행* toostart 응용 프로그램에서는 hello 및 다음에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="82cb7-146">로그인 할 때 수 tooview hello 할 일 목록 이어야 하 고 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="82cb7-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="82cb7-147">**Swift**:</span></span>

1. <span data-ttu-id="82cb7-148">Mac에서 열고 *ToDoTableViewController.swift* Xcode에서 hello 다음 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="82cb7-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="82cb7-149">변경 *google* 너무*microsoftaccount*, *twitter*, *facebook*, 또는 *windowsazureactivedirectory* Google을 id 공급자로 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="82cb7-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="82cb7-150">Facebook을 사용하는 경우 [앱에서 Facebook 도메인을 허용 목록에 추가해야 합니다][1].</span><span class="sxs-lookup"><span data-stu-id="82cb7-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="82cb7-151">Hello 대체 **urlScheme** 응용 프로그램에 대 한 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="82cb7-152">hello urlScheme 해야 수 hello 동일 hello에 지정 된 URL 체계가 프로토콜 hello로 **외부 리디렉션 Url 허용** hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="82cb7-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="82cb7-153">인증 요청이 완료 된 후 hello urlScheme hello 인증 콜백 tooswitch 백 tooyour 응용 프로그램에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="82cb7-154">Hello 줄을 제거 `self.refreshControl?.beginRefreshing()` 및 `self.onRefresh(self.refreshControl)` 끝날 때 `viewDidLoad()` 에 *ToDoTableViewController.swift*합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="82cb7-155">호출을 너무 추가`loginAndGetData()` 그 자리에:</span><span class="sxs-lookup"><span data-stu-id="82cb7-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="82cb7-156">열기 hello `AppDelegate.swift` 파일을 다음 줄 toohello hello 추가 `AppDelegate` 클래스:</span><span class="sxs-lookup"><span data-stu-id="82cb7-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="82cb7-157">Hello 대체 _appname_ 작동이 hello urlScheme 값 1 단계에서 사용한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="82cb7-158">열기 hello `AppName-Info.plist` (응용 프로그램의 hello 이름으로 교체 AppName) 파일을 찾아 hello 코드 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="82cb7-159">이 코드는 hello 안에 배치 해야 `<dict>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="82cb7-160">Hello 대체 _appname_ 문자열 (배열 내에서 **CFBundleURLSchemes**) 1 단계에서 선택한 hello 응용 프로그램 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="82cb7-161">또한이 변경을 수행할 수 있습니다 이러한 hello plist에 편집기-hello 클릭 `AppName-Info.plist` XCode tooopen hello plist 편집기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="82cb7-162">Hello 대체 `com.microsoft.azure.zumo` 에 대 한 문자열 **CFBundleURLName** 프로그램 apple 번들 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="82cb7-163">키를 눌러 *실행* toostart 응용 프로그램에서는 hello 및 다음에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="82cb7-164">로그인 할 때 수 tooview hello 할 일 목록 이어야 하 고 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="82cb7-165">App Service 인증은 Apples Inter-App Communication을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82cb7-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="82cb7-166">이 주제에 대 한 자세한 내용은 참조 toohello [Apple 설명서][2]</span><span class="sxs-lookup"><span data-stu-id="82cb7-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure 포털]: https://portal.azure.com

[iOS 빠른 시작]: app-service-mobile-ios-get-started.md

