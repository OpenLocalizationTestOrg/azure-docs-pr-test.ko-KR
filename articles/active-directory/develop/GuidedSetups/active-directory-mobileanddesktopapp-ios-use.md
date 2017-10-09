---
title: "AD aaaAzure v2 iOS 시작-사용 | Microsoft Docs"
description: "iOS(Swift) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="6ba9d-103">Hello Microsoft 인증 라이브러리 (MSAL) tooget 토큰을 사용 하 여 hello Microsoft Graph API에 대 한</span><span class="sxs-lookup"><span data-stu-id="6ba9d-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="6ba9d-104">열기 `ViewController.swift` hello 코드와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-104">Open `ViewController.swift` and replace hello code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6ba9d-105">추가 정보</span><span class="sxs-lookup"><span data-stu-id="6ba9d-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="6ba9d-106">대화형으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ba9d-106">Getting a user token interactively</span></span>
<span data-ttu-id="6ba9d-107">호출 hello `acquireToken` 라는 브라우저 창에서 메서드 결과에 대 한 사용자 toosign hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="6ba9d-108">응용 프로그램 일반적으로 필요에 대화형으로 hello 사용자 toosign tooaccess 필요한 처음으로 보호 된 리소스 되거나 자동 작업 tooacquire 토큰 실패 (예: hello 사용자의 암호 만료 됨).</span><span class="sxs-lookup"><span data-stu-id="6ba9d-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="6ba9d-109">자동으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ba9d-109">Getting a user token silently</span></span>
<span data-ttu-id="6ba9d-110">hello `acquireTokenSilent` 토큰 획득 및 갱신 사용자 상호 작용 없이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="6ba9d-111">후 `acquireToken` 처음으로 hello에 대 한 실행 `acquireTokenSilent` hello 일반적으로 사용 되는 방법 tooobtain 사용 되는 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="6ba9d-112">결국 `acquireTokenSilent` 못합니다-예: hello 사용자가 로그 아웃 또는 다른 장치에서 암호 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="6ba9d-113">MSAL 탐지 대화형 작업을 요구 하 여 hello 문제 해결을 발생 시킬는 `MSALErrorCode.interactionRequired` 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="6ba9d-114">응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="6ba9d-115">에 대 한 호출 `acquireToken` 즉시 메시지를 표시에서 발생 하는 hello에 대 한 사용자 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="6ba9d-116">이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 되는 오프 라인 콘텐츠 hello 응용 프로그램의 hello 사용자에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="6ba9d-117">이 패턴을 사용 하 여이 단계별된 설치 프로그램에서 생성 된 hello 샘플 응용 프로그램: 나타나면 작업 hello에 처음으로 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="6ba9d-118">사용자 없음 hello 응용 프로그램을 사용 하기 때문에 `applicationContext.users().first` null 값이 포함 됩니다는 및 ` MSALErrorCode.interactionRequired ` 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="6ba9d-119">핸들 예외를 호출 하 여 hello 다음 hello 샘플의 코드를 hello `acquireToken` 그 결과에서 사용자 toosign hello 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="6ba9d-120">응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `acquireTokenSilent` 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="6ba9d-121">이 일반적으로 hello 사용자 중단 되지 않고 hello 응용 프로그램의 다른 기능을 사용할 수 있습니다-예를 들어 콘텐츠가 오프 라인 hello 응용 프로그램에서 사용할 수 있는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="6ba9d-122">때 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보를 오래 된 항목 또는 응용 프로그램 tooretry를 결정할 수 hello 사용자 결정할 수는 경우 `acquireTokenSilent` 네트워크 일시적으로 사용할 수 없게 후 복원 된 경우.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="6ba9d-123">얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="6ba9d-124">아래 새 메서드의 hello 너무 추가`ViewController.swift`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="6ba9d-125">이 메서드는 사용 되는 toomake는 `GET` hello Microsoft Graph API를 사용 하 여에 대 한 요청 된 *HTTP 권한 부여 헤더*:</span><span class="sxs-lookup"><span data-stu-id="6ba9d-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="6ba9d-126">보호되는 API에 대해 REST 호출 수행</span><span class="sxs-lookup"><span data-stu-id="6ba9d-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="6ba9d-127">이 샘플 응용 프로그램에서는 hello `getContentWithToken()` 메서드는 사용 되는 toomake HTTP `GET` 토큰 한 후 hello 콘텐츠 toohello 호출자를 요구 하는 보호 된 리소스에 대 한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="6ba9d-128">이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="6ba9d-129">이 샘플에 대 한 hello 리소스는 Microsoft Graph API hello *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="6ba9d-130">로그아웃 설정</span><span class="sxs-lookup"><span data-stu-id="6ba9d-130">Set up sign-out</span></span>

<span data-ttu-id="6ba9d-131">메서드를 너무 뒤 hello 추가`ViewController.swift` toosign hello 사용자:</span><span class="sxs-lookup"><span data-stu-id="6ba9d-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="6ba9d-132">로그아웃에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6ba9d-132">More info on sign-out</span></span>

<span data-ttu-id="6ba9d-133">hello `signoutButton` 메서드 hello MSAL 사용자 캐시-에서 hello 사용자를 제거 합니다.이 쿼리 효과적으로 확인할 MSAL tooforget hello에 대 한 현재 사용자 후속 요청 tooacquire 만들어진 경우 toobe 대화형 토큰 성공만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="6ba9d-134">MSAL 여기서 여러 계정을 로그인 할 수 hello에 시나리오를 지원 hello 응용 프로그램에서이 샘플에서는 단일 사용자를 지원 하지만 동일한 시간-예로 전자 메일 응용 프로그램 사용자가 계정을 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="6ba9d-135">Hello 콜백을 등록합니다</span><span class="sxs-lookup"><span data-stu-id="6ba9d-135">Register hello callback</span></span>

<span data-ttu-id="6ba9d-136">Hello 사용자가 인증 되 면 hello 브라우저 hello 사용자 백 toohello 응용 프로그램을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="6ba9d-137">이 콜백은 tooregister 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="6ba9d-138">`AppDelegate.swift`를 열고 MSAL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="6ba9d-139">다음 메서드 tooyour hello 추가 <code>AppDelegate</code> toohandle 콜백 클래스.</span><span class="sxs-lookup"><span data-stu-id="6ba9d-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

