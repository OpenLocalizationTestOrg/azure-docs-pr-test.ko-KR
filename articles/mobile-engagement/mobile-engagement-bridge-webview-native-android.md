---
title: "aaaBridge 네이티브 Mobile Engagement Android SDK와 Android 웹 보기"
description: "설명 방법을 toocreate WebView 사이의 다리 Javascript를 실행 하 고 네이티브 Mobile Engagement Android SDK hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="89e86-103">Android WebView와 네이티브 Mobile Engagement Android SDK 브리지</span><span class="sxs-lookup"><span data-stu-id="89e86-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89e86-104">Android 브리지</span><span class="sxs-lookup"><span data-stu-id="89e86-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="89e86-105">iOS 브리지</span><span class="sxs-lookup"><span data-stu-id="89e86-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="89e86-106">일부 모바일 응용 프로그램은 여기서 hello 응용 프로그램 자체가 네이티브 Android 개발을 사용 하 여 개발 된 되지만 일부 또는 모든 hello 화면 Android WebView 내에서 렌더링 되는 하이브리드 응용 프로그램으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="89e86-107">이 자습서에서는 설명 하 고 이러한 응용 프로그램 내에서 Mobile Engagement Android SDK를 계속 사용할 수 있습니다 어떻게 toogo이 작업을 수행 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="89e86-108">hello Android 설명서를 기반으로 하는 hello 샘플 코드 아래 [여기](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="89e86-109">문서화 된이 방법을 사용할 수 있습니다 어떻게 설명 Mobile Engagement Android SDK는 일반적으로 메서드를 사용 하는 하이브리드 응용 프로그램에서 Webview 시작할 수도 요청 tootrack 이벤트, 작업, 오류, 응용 프로그램 정보를 통해 파이핑 하는 동안 동일한 tooimplement hello Android SDK 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="89e86-110">통해 수행한 tooensure 해야 우선, 우리의 [시작 자습서](mobile-engagement-android-get-started.md) 하이브리드 앱에서 toointegrate hello Mobile Engagement Android SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="89e86-111">이렇게 하면 일단 프로그램 `OnCreate` 메서드 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="89e86-112">이제 하이브리드 앱에 WebView가 표시된 화면이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="89e86-113">hello에 대 한 코드 됩니다 비슷한 toohello 다음 로컬 HTML 파일을 로드는 म **Sample.html** hello에 hello Webview의에서 `onCreate` 화면 메서드.</span><span class="sxs-lookup"><span data-stu-id="89e86-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="89e86-114">이제 브리지 파일을 만들 **WebAppInterface** hello를 사용 하 여 Mobile Engagement Android SDK 메서드를 사용 하는 래퍼를 만드는 일부를 통해 일반적으로 `@JavascriptInterface` hello에 설명 된 방법을 [Android 설명서 ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="89e86-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="89e86-115">연결 파일 위에 hello 작성 했으면, tooensure 우리의 Webview에 연결 되어 있는지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="89e86-116">Tooedit 해야이 toohappen 프로그램 `SetWebview` 메서드 한다는 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="89e86-117">호출에서는 위의 조각 hello, `addJavascriptInterface` tooassociate 우리의 브리지 우리의 Webview 클래스와 호출 핸들을 만든 **EngagementJs** hello 브리지 파일에서 toocall hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="89e86-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="89e86-118">이제 hello 다음 호출 하는 파일을 만들 **Sample.html** 프로젝트 폴더의 호출 **자산** hello Webview에 로드 되 고 여기서 म hello 브리지 파일에서 hello 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="89e86-119">위의 hello HTML 파일에 대 한 참고 hello 다음 지점:</span><span class="sxs-lookup"><span data-stu-id="89e86-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="89e86-120">이벤트, 작업, 오류, AppInfo의 이름으로 사용 되는 데이터 toobe을 제공할 수 있는 입력란의 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="89e86-121">Hello 단추 다음 tooit 클릭할 때 toohello 결국 hello 브리지 파일 toopass에서 hello 메서드를 호출 toohello Mobile Engagement Android SDK이 호출 하는 Javascript 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="89e86-122">우리는 태그 지정에 몇 가지 추가 정보를 정적 toohello 이벤트, 작업 및 오류 toodemonstrate도 방법을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="89e86-123">Hello에서 보면이 추가 정보는 JSON 문자열을 전송 되 `WebAppInterface` 파일, 구문 분석 되 고에 Android `Bundle` 보내는 이벤트, 작업, 및 오류와 함께 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="89e86-124">Mobile Engagement 작업이 10 초 동안 실행 하 고 종료 hello 입력된 상자에 지정한 hello 이름으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="89e86-125">Mobile Engagement appinfo 또는 태그와 'customer_name' hello 정적 키와 입력 한 hello 입력에 hello 값으로 hello 태그에 대 한 hello 값 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="89e86-126">실행된 hello 앱 hello 다음에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="89e86-127">이제 다음 hello와 같은 테스트 이벤트에 대 한 몇 가지 이름을 제공 하 고 클릭 **보낼** 그 아래의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="89e86-128">이제 toohello 이동 **모니터** 앱과 검토의 탭 **이벤트 세부 정보->**, hello 정적 응용 프로그램 정보를 전송 하는 함께 표시 하는이 이벤트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e86-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
