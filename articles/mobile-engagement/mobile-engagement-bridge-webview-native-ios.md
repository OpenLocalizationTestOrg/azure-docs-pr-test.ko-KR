---
title: "네이티브 Mobile Engagement ios SDK aaaBridge iOS 웹 보기"
description: "설명 방법을 toocreate Javascript 및 hello 네이티브 Mobile Engagement iOS SDK를 실행 하는 웹 보기 간의 브리지"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>iOS WebView와 네이티브 Mobile Engagement iOS SDK 브리지
> [!div class="op_single_selector"]
> * [Android 브리지](mobile-engagement-bridge-webview-native-android.md)
> * [iOS 브리지](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

일부 모바일 응용 프로그램은 여기서 hello 응용 프로그램 자체가 Objective-c 네이티브 iOS 개발을 사용 하 여 개발 된 되지만 일부 또는 모든 hello 화면 웹 보기 iOS 내에서 렌더링 되는 하이브리드 응용 프로그램으로 설계 되었습니다. 이 자습서에서는 설명 하 고 이러한 응용 프로그램 내에서 Mobile Engagement iOS SDK 소비 될 수 있습니다 어떻게 toogo이 작업을 수행 하는 방법에 대 한 합니다. 

두 가지 접근 방식을 tooachieve이 있지만 둘 다 하지 문서화 된:

* 첫 번째 방식은 웹 보기에 `UIWebViewDelegate`를 등록하는 것과 관련된 이 [링크](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip)에 설명되어 있으며, Javascript에서 수행된 위치 변경을 catch하고 즉시 취소합니다. 
* 이에 따라 하나는 두 번째 [WWDC 2013 세션](https://developer.apple.com/videos/play/wwdc2013/615), 먼저 hello 보다 깔끔한 되 고이 가이드에 대 한 따라야 하는 방법입니다. 이 접근 방식은 iOS7 이상에서만 작동합니다. 

Hello iOS 브리지 샘플에 대 한 아래의 hello 단계를 수행 합니다.

1. 통해 수행한 tooensure 해야 우선, 우리의 [시작 자습서](mobile-engagement-ios-get-started.md) toointegrate hello 하이브리드 앱에서 Mobile Engagement iOS SDK입니다. 필요에 따라 테스트 hello 웹 보기에서 트리거할 것 처럼 hello SDK 메서드를 볼 수 있도록 다음과 같이 로깅을 설정할 수도 있습니다. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. 이제 하이브리드 앱에 WebView가 표시된 화면이 있는지 확인합니다. Toohello를 추가할 수 있습니다 `Main.storyboard` hello 응용 프로그램의 합니다. 
3. 이 웹 보기와 연결 하면 **ViewController** 클릭 하 고 hello webview hello 보기 컨트롤러 장면 toohello에서 끌어서 `ViewController.h` hello 바로 아래에 배치 하는 화면에서 편집 `@interface` 줄. 
4. 그러면 이름을 묻는 대화 상자가 나타납니다. 으로 hello 이름을 지정 **webView**합니다. 프로그램 `ViewController.h` 파일 hello 다음과 같습니다.
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Hello 업데이트할 것 `ViewController.m` 나중에 파일 있지만 먼저 SDK 메서드 일부 자주 사용 되는 Mobile Engagement iOS를 통해 래퍼를 생성 하는 hello 연결 파일을 만들겠습니다. 새 헤더 파일을 만들 **EngagementJsExports.h** hello를 사용 하 여 `JSExport` 앞에서 언급 한 hello에 설명 된 메커니즘 [세션](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello 네이티브 iOS 메서드. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. 다음 hello hello 연결 파일의 두 번째 부분을 만듭니다. 파일을 만들 **EngagementJsExports.m** 있는 hello 구현 hello Mobile Engagement iOS SDK 메서드를 호출 하 여 hello 실제 래퍼를 생성 합니다. Hello 구문 분석은 म 참고 또한 `extras` hello webview javascript에서 전달 되 고 해당 넣는 `NSMutableDictionary` 개체 toobe 호출 Engagement SDK 메서드 hello로 전달 합니다.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. 이제 우리 toohello 돌아와서 **ViewController.m** 코드 다음 hello로 업데이트: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Hello에 대 한 참고 hello 다음 가리키는 **ViewController.m** 파일:
   
   * Hello에 `loadWebView` 메서드, 우리를 로드 하는 이라는 로컬 HTML 파일 **LocalPage.html** 다음 검토할 코드입니다. 
   * Hello에 `webViewDidFinishLoad` 메서드를 hello를 끄는 것 `JsContext` 와 연관 래퍼 클래스입니다. 이렇게 우리의 래퍼의 hello 핸들을 사용 하는 SDK 메서드를 호출 하면 **EngagementJs** hello 웹 보기에서 합니다. 
9. 파일을 만들 **LocalPage.html** 코드 다음 hello로:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. 위의 hello HTML 파일에 대 한 참고 hello 다음 지점:
    
    * 이벤트, 작업, 오류, AppInfo의 이름으로 사용 되는 데이터 toobe을 제공할 수 있는 입력란의 집합을 포함 합니다. Hello 단추 다음 tooit 클릭할 때 toohello 결국 hello 브리지 파일 toopass에서 hello 메서드를 호출 toohello Mobile Engagement iOS SDK이 호출 하는 Javascript 호출 합니다. 
    * 우리는 태그 지정에 몇 가지 추가 정보를 정적 toohello 이벤트, 작업 및 오류 toodemonstrate도 방법을 수행할 수 있습니다. 이 추가 정보 보내집니다는 JSON 문자열 hello를 보면 `EngagementJsExports.m` 파일, 구문 분석 되 고 보내는 이벤트, 작업, 및 오류와 함께 전달 합니다. 
    * Mobile Engagement 작업이 10 초 동안 실행 하 고 종료 hello 입력된 상자에 지정한 hello 이름으로 시작 합니다. 
    * Mobile Engagement appinfo 또는 태그와 'customer_name' hello 정적 키와 입력 한 hello 입력에 hello 값으로 hello 태그에 대 한 hello 값 전달 됩니다. 
11. 실행된 hello 앱 hello 다음에 표시 됩니다. 이제 다음 hello와 같은 테스트 이벤트에 대 한 몇 가지 이름을 제공 하 고 클릭 **보낼** 다음 tooit 합니다. 
    
     ![][1]
12. 이제 toohello 이동 **모니터** 앱과 검토의 탭 **이벤트 세부 정보->**, hello 정적 응용 프로그램 정보를 전송 하는 함께 표시 하는이 이벤트가 표시 됩니다. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
