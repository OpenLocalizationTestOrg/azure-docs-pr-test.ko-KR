---
title: "Android WebView와 네이티브 Mobile Engagement Android SDK 브리지"
description: "Javascript를 실행하는 WebView와 네이티브 Mobile Engagement Android SDK 간의 브리지를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="9daf6-103">Android WebView와 네이티브 Mobile Engagement Android SDK 브리지</span><span class="sxs-lookup"><span data-stu-id="9daf6-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9daf6-104">Android 브리지</span><span class="sxs-lookup"><span data-stu-id="9daf6-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="9daf6-105">iOS 브리지</span><span class="sxs-lookup"><span data-stu-id="9daf6-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="9daf6-106">일부 모바일 앱은 앱 자체가 네이티브 Android 개발을 사용하여 개발되지만 화면의 일부 또는 전부가 Android WebView 내에서 렌더링되는 하이브리드 앱으로 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="9daf6-107">이러한 앱 내에서 Mobile Engagement Android SDK를 계속 사용할 수 있으며, 해당 작업 방법이 이 자습서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="9daf6-108">아래 샘플 코드는 Android 설명서( [여기](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript))를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="9daf6-109">Android 설명서에서는 하이브리드 앱의 Webview에서 Android SDK를 통해 파이프하는 동안 이벤트, 작업, 오류 및 앱 정보에 대한 추적 요청을 시작할 수 있도록 이 문서화된 접근 방식을 사용하여 Mobile Engagement Android SDK의 자주 사용되는 메서드에 대해 동일한 기능을 구현하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="9daf6-110">먼저 [시작 자습서](mobile-engagement-android-get-started.md) 에 따라 Mobile Engagement Android SDK를 하이브리드 앱에 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="9daf6-111">그러면 `OnCreate` 메서드가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="9daf6-112">이제 하이브리드 앱에 WebView가 표시된 화면이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="9daf6-113">코드는 화면의 `onCreate` 메서드에서 로컬 HTML 파일 **Sample.html**을 Webview에 로드하는 다음 코드와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="9daf6-114">이제 [Android 설명서](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)에 설명된 `@JavascriptInterface` 접근 방식을 사용하여 자주 사용되는 몇 가지 Mobile Engagement Android SDK 메서드에 래퍼를 만드는 **WebAppInterface**라는 브리지 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="9daf6-115">위 브리지 파일을 만든 후에는 이 파일이 Webview와 연결되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="9daf6-116">그러려면 `SetWebview` 메서드를 다음과 같이 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="9daf6-117">위 조각에서는 브리지 클래스를 Webview에 연결하기 위해 `addJavascriptInterface` 를 호출했으며, 브리지 파일에서 메서드를 호출하기 위해 **EngagementJs** 라는 핸들을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="9daf6-118">이제 **assets**이라는 폴더의 프로젝트에서 **Sample.html**이라는 파일을 만듭니다. Webview로 로드되는 이 브리지 파일에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="9daf6-119">위 HTML 파일에 대해 유의할 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="9daf6-120">이 파일은 이벤트, 작업, 오류, 앱 정보의 이름으로 사용할 데이터를 제공할 수 있는 입력 상자 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="9daf6-121">입력 상자 옆의 단추를 클릭하면 이 호출을 Mobile Engagement Android SDK로 전달하기 위해 브리지 파일에서 메서드를 호출하는 Javascript가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="9daf6-122">작업 방법을 보여 주기 위해 이벤트, 작업 및 오류의 몇 가지 정적 추가 정보에 대한 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="9daf6-123">이 추가 정보는 JSON 문자열로 전송됩니다. `WebAppInterface` 파일에서 구문 분석되어 Android `Bundle`에 배치된 후 전송되는 이벤트, 작업 및 오류와 함께 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="9daf6-124">Mobile Engagement 작업은 입력 상자에 지정한 이름으로 시작되며, 10초간 실행된 후 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="9daf6-125">Mobile Engagement 앱 정보 또는 태그는 입력 상자에 태그 값으로 입력한 값 및 정적 키로 'customer_name'과 함께 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="9daf6-126">앱을 실행하면 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-126">Run the app and you will see the following.</span></span> <span data-ttu-id="9daf6-127">이제 다음과 같은 테스트 이벤트의 이름을 제공하고 아래의 **Send** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="9daf6-128">이제 앱의 **모니터링** 탭으로 이동하면 **이벤트 -> 세부 정보** 아래에 전송한 정적 앱 정보와 함께 이 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9daf6-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
