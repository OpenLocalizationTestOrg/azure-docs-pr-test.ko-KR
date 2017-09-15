---
title: "Azure AD v2 iOS 시작 - 사용 | Microsoft Docs"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="25a03-103">MSAL(Microsoft 인증 라이브러리)를 사용하여 Microsoft Graph API에 대한 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="25a03-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="25a03-104">`ViewController.swift`를 열고 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="25a03-105">추가 정보</span><span class="sxs-lookup"><span data-stu-id="25a03-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="25a03-106">대화형으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="25a03-106">Getting a user token interactively</span></span>
<span data-ttu-id="25a03-107">`acquireToken` 메서드를 호출하면 사용자에게 로그인하라는 브라우저 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="25a03-108">사용자가 처음으로 보호되는 리소스에 액세스해야 하거나 토큰 획득을 위한 자동 작업에 실패한 경우(예: 사용자의 암호 만료) 일반적으로 사용자는 응용 프로그램에서 대화식으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="25a03-109">자동으로 사용자 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="25a03-109">Getting a user token silently</span></span>
<span data-ttu-id="25a03-110">`acquireTokenSilent` 메서드는 사용자 개입 없이 토큰 획득 및 갱신을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="25a03-111">`acquireToken`이 처음으로 실행된 후 일반적으로 `acquireTokenSilent` 메서드를 사용하여 후속 호출 시 보호되는 리소스에 액세스하는 데 사용되는 토큰을 가져옵니다. 즉, 토큰을 요청하거나 갱신하기 위한 호출이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="25a03-112">결국 `acquireTokenSilent`에 실패합니다(예: 사용자 로그아웃 또는 다른 장치에서 사용자가 암호 변경).</span><span class="sxs-lookup"><span data-stu-id="25a03-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="25a03-113">MSAL이 대화형 작업을 요구해 이 문제를 해결할 수 있다고 감지하면 `MSALErrorCode.interactionRequired` 예외를 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="25a03-114">응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="25a03-115">즉시 `acquireToken`에 대한 호출을 수행합니다. 그러면 사용자에게 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="25a03-116">이 패턴은 응용 프로그램에 사용자가 사용할 수 있는 오프라인 콘텐츠가 없는 온라인 응용 프로그램에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="25a03-117">이 단계별 설치에 따라 생성된 샘플 응용 프로그램은 이 패턴을 사용합니다. 이 패턴은 응용 프로그램을 처음 실행할 때 작동되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="25a03-118">이 응용 프로그램을 사용한 사용자가 없으므로 `applicationContext.users().first`에는 null 값이 포함되며 ` MSALErrorCode.interactionRequired ` 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="25a03-119">샘플의 코드는 `acquireToken`를 호출해 예외를 처리하며, 사용자에게 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="25a03-120">또한 응용 프로그램에서는 대화형 로그인이 필요하다는 시각적 표시를 사용자에게 보여줍니다. 따라서 사용자가 로그인할 적절한 시간을 선택하거나 이후에 응용 프로그램이 `acquireTokenSilent`를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="25a03-121">이는 사용자가 중단 없이 응용 프로그램의 기능을 사용할 수 있는 경우(예: 응용 프로그램에 사용 가능한 오프라인 콘텐츠가 있는 경우) 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="25a03-122">이 경우 사용자가 보호되는 리소스에 액세스하거나 오래된 정보를 새로 고치기 위해 로그인할 시점을 결정하거나 응용 프로그램이 일시적으로 사용할 수 없게 된 후 네트워크가 복원된 경우 `acquireTokenSilent`를 다시 시도하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="25a03-123">방금 가져온 토큰을 사용하여 Microsoft Graph API 호출</span><span class="sxs-lookup"><span data-stu-id="25a03-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="25a03-124">`ViewController.swift`에 아래의 새 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="25a03-125">이 메서드는 *HTTP 인증 헤더*를 사용하여 Microsoft Graph API에 대해 `GET` 요청을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="25a03-126">보호되는 API에 대해 REST 호출 수행</span><span class="sxs-lookup"><span data-stu-id="25a03-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="25a03-127">이 샘플 응용 프로그램에서 `getContentWithToken()` 메서드는 토큰이 필요한 보호되는 리소스에 대한 HTTP `GET` 요청을 실행한 다음 호출자에게 콘텐츠를 반환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="25a03-128">이 메서드는 *HTTP 인증 헤더*에 획득된 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="25a03-129">이 샘플에서 리소스는 사용자 프로필 정보를 표시하는 Microsoft Graph API *me* 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="25a03-130">로그아웃 설정</span><span class="sxs-lookup"><span data-stu-id="25a03-130">Set up sign-out</span></span>

<span data-ttu-id="25a03-131">`ViewController.swift`에 다음 메서드를 추가하면 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="25a03-132">로그아웃에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="25a03-132">More info on sign-out</span></span>

<span data-ttu-id="25a03-133">`signoutButton` 메서드는 MSAL 사용자 캐시에서 사용자를 제거하여 MSAL에 현재 사용자를 잊으라고 효율적으로 전달합니다. 따라서 대화식으로 수행되는 경우에만 토큰 획득을 위한 이후 요청에 성공하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="25a03-134">이 샘플의 응용 프로그램이 단일 사용자를 지원하더라도 MSAL은 동시에 여러 계정에 로그인할 수 있는 시나리오를 지원합니다(예: 사용자 한 명이 여러 계정을 가질 수 있는 메일 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="25a03-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="25a03-135">콜백 등록</span><span class="sxs-lookup"><span data-stu-id="25a03-135">Register the callback</span></span>

<span data-ttu-id="25a03-136">사용자가 인증되면 브라우저는 사용자를 응용 프로그램으로 다시 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="25a03-137">아래 단계에 따라 이 콜백을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="25a03-138">`AppDelegate.swift`를 열고 MSAL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="25a03-139"><code>AppDelegate</code> 클래스에 다음 메서드를 추가하여 콜백을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="25a03-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

