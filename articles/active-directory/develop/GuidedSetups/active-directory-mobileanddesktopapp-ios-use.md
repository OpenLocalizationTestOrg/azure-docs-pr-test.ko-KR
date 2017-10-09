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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hello Microsoft 인증 라이브러리 (MSAL) tooget 토큰을 사용 하 여 hello Microsoft Graph API에 대 한

열기 `ViewController.swift` hello 코드와 바꿉니다.

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
### <a name="more-information"></a>추가 정보
#### <a name="getting-a-user-token-interactively"></a>대화형으로 사용자 토큰 가져오기
호출 hello `acquireToken` 라는 브라우저 창에서 메서드 결과에 대 한 사용자 toosign hello 합니다. 응용 프로그램 일반적으로 필요에 대화형으로 hello 사용자 toosign tooaccess 필요한 처음으로 보호 된 리소스 되거나 자동 작업 tooacquire 토큰 실패 (예: hello 사용자의 암호 만료 됨).

#### <a name="getting-a-user-token-silently"></a>자동으로 사용자 토큰 가져오기
hello `acquireTokenSilent` 토큰 획득 및 갱신 사용자 상호 작용 없이 처리 합니다. 후 `acquireToken` 처음으로 hello에 대 한 실행 `acquireTokenSilent` hello 일반적으로 사용 되는 방법 tooobtain 사용 되는 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.

결국 `acquireTokenSilent` 못합니다-예: hello 사용자가 로그 아웃 또는 다른 장치에서 암호 변경 되었습니다. MSAL 탐지 대화형 작업을 요구 하 여 hello 문제 해결을 발생 시킬는 `MSALErrorCode.interactionRequired` 예외입니다. 응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.

1.  에 대 한 호출 `acquireToken` 즉시 메시지를 표시에서 발생 하는 hello에 대 한 사용자 toosign 합니다. 이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 되는 오프 라인 콘텐츠 hello 응용 프로그램의 hello 사용자에 대해 사용할 수 있습니다. 이 패턴을 사용 하 여이 단계별된 설치 프로그램에서 생성 된 hello 샘플 응용 프로그램: 나타나면 작업 hello에 처음으로 hello 응용 프로그램을 실행 합니다. 사용자 없음 hello 응용 프로그램을 사용 하기 때문에 `applicationContext.users().first` null 값이 포함 됩니다는 및 ` MSALErrorCode.interactionRequired ` 예외가 throw 됩니다. 핸들 예외를 호출 하 여 hello 다음 hello 샘플의 코드를 hello `acquireToken` 그 결과에서 사용자 toosign hello 메시지를 표시 합니다.

2.  응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `acquireTokenSilent` 나중에 있습니다. 이 일반적으로 hello 사용자 중단 되지 않고 hello 응용 프로그램의 다른 기능을 사용할 수 있습니다-예를 들어 콘텐츠가 오프 라인 hello 응용 프로그램에서 사용할 수 있는 경우에 사용 됩니다. 때 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보를 오래 된 항목 또는 응용 프로그램 tooretry를 결정할 수 hello 사용자 결정할 수는 경우 `acquireTokenSilent` 네트워크 일시적으로 사용할 수 없게 후 복원 된 경우.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.

아래 새 메서드의 hello 너무 추가`ViewController.swift`합니다. 이 메서드는 사용 되는 toomake는 `GET` hello Microsoft Graph API를 사용 하 여에 대 한 요청 된 *HTTP 권한 부여 헤더*:

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
### <a name="making-a-rest-call-against-a-protected-api"></a>보호되는 API에 대해 REST 호출 수행

이 샘플 응용 프로그램에서는 hello `getContentWithToken()` 메서드는 사용 되는 toomake HTTP `GET` 토큰 한 후 hello 콘텐츠 toohello 호출자를 요구 하는 보호 된 리소스에 대 한 요청입니다. 이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다. 이 샘플에 대 한 hello 리소스는 Microsoft Graph API hello *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>로그아웃 설정

메서드를 너무 뒤 hello 추가`ViewController.swift` toosign hello 사용자:

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
### <a name="more-info-on-sign-out"></a>로그아웃에 대한 자세한 정보

hello `signoutButton` 메서드 hello MSAL 사용자 캐시-에서 hello 사용자를 제거 합니다.이 쿼리 효과적으로 확인할 MSAL tooforget hello에 대 한 현재 사용자 후속 요청 tooacquire 만들어진 경우 toobe 대화형 토큰 성공만 됩니다.

MSAL 여기서 여러 계정을 로그인 할 수 hello에 시나리오를 지원 hello 응용 프로그램에서이 샘플에서는 단일 사용자를 지원 하지만 동일한 시간-예로 전자 메일 응용 프로그램 사용자가 계정을 여러 개 있습니다.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Hello 콜백을 등록합니다

Hello 사용자가 인증 되 면 hello 브라우저 hello 사용자 백 toohello 응용 프로그램을 리디렉션합니다. 이 콜백은 tooregister 아래 hello 단계를 수행 합니다.

1.  `AppDelegate.swift`를 열고 MSAL을 가져옵니다.

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
다음 메서드 tooyour hello 추가 <code>AppDelegate</code> toohandle 콜백 클래스.
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

