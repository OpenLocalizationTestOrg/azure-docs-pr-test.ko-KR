---
title: "Azure에서 음성, VoIP 및 SMS 메시징을 위해 Twilio 사용"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 Node.js로 작성되었습니다."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="28af6-104">Azure에서 음성, VoIP 및 SMS 메시징을 위해 Twilio 사용</span><span class="sxs-lookup"><span data-stu-id="28af6-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="28af6-105">이 가이드에서는 Azure에서 Twilio 및 node.js와 통신하는 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="28af6-106">Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="28af6-106">What is Twilio?</span></span>
<span data-ttu-id="28af6-107">Twilio는 개발자가 전화 통화를 걸고 받고, 문자 메시지를 보내고 받고, VoIP 호출을 브라우저 기반 및 네이티브 모바일 응용 프로그램에 포함하는 작업을 쉽게 수행할 수 있게 해주는 API 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="28af6-108">깊이 있게 설명하기 전에 이러한 내용을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="28af6-109">전화 및 문자 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="28af6-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="28af6-110">Twilio를 통해 개발자는 전화 및 문자 메시지를 보내고 받는 데 모두 사용할 수 있는 [프로그램 가능 전화 번호를 구매][purchase_phone]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="28af6-111">Twilio 번호가 인바운드 전화 또는 문자를 받으면 Twilio는 웹 응용 프로그램에 HTTP POST 또는 GET 요청을 보내 전화 또는 문자를 처리하는 방법에 대한 지침을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="28af6-112">서버는 전화 또는 문자를 처리하는 방법에 대한 지침이 포함된 간단한 XML 태그 집합인 [TwiML][twiml]을 통해 Twilio의 HTTP 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="28af6-113">잠시 후에 TwiML 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="28af6-114">전화 걸기 및 문자 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="28af6-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="28af6-115">개발자는 Twilio 웹 서비스 API에 대한 HTTP 요청을 만들어 문자 메시지를 보내거나 아웃바운드 전화 통화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="28af6-116">아웃바운드 전화의 경우 개발자는 아웃바운드 전화가 연결된 후 해당 전화를 처리하는 방법에 대한 TwiML 지침을 반환하는 URL도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="28af6-117">UI 코드(JavaScript, iOS 또는 Android)에 VoIP 기능 포함</span><span class="sxs-lookup"><span data-stu-id="28af6-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="28af6-118">Twilio는 모든 데스크톱 웹 브라우저, iOS 앱 또는 Android 앱을 VoIP 전화로 변환할 수 있는 클라이언트 쪽 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="28af6-119">이 문서에서는 브라우저에서 VoIP 호출을 사용하는 방법을 집중적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="28af6-120">브라우저에서 실행되는 *Twilio JavaScript SDK* 외에 서버 쪽 응용 프로그램(node.js 응용 프로그램)을 사용하여 "기능 토큰"을 JavaScript 클라이언트에 발급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="28af6-121">node.js에 VoIP를 사용하는 방법에 대한 자세한 내용은 [Twilio 개발자 블로그][voipnode]에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="28af6-122">Twilio 등록(Microsoft 할인)</span><span class="sxs-lookup"><span data-stu-id="28af6-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="28af6-123">Twilio 서비스를 사용하기 전에 먼저 [계정을 등록][signup]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="28af6-124">Microsoft Azure 고객은 특별 할인을 받습니다. [반드시 여기서 등록하셔야 합니다][signup]!</span><span class="sxs-lookup"><span data-stu-id="28af6-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="28af6-125">node.js Azure 웹 사이트 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="28af6-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="28af6-126">이제 Azure에서 실행되는 node.js 웹 사이트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="28af6-127">[이 작업을 수행하는 공식 설명서가 여기에 있습니다][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="28af6-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="28af6-128">높은 수준에서 봤을 때 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="28af6-129">Azure 계정 등록(아직 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="28af6-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="28af6-130">Azure 관리 콘솔을 사용하여 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="28af6-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="28af6-131">소스 제어 지원 추가(git를 사용했다고 가정함)</span><span class="sxs-lookup"><span data-stu-id="28af6-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="28af6-132">간단한 node.js 웹 응용 프로그램을 사용하여 파일 `server.js` 만들기</span><span class="sxs-lookup"><span data-stu-id="28af6-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="28af6-133">이 간단한 응용 프로그램을 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="28af6-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="28af6-134">Twilio 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="28af6-134">Configure the Twilio Module</span></span>
<span data-ttu-id="28af6-135">이제 Twilio API를 사용하는 간단한 node.js 응응 프로그램 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="28af6-136">시작하기 전에 Twilio 계정 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="28af6-137">시스템 환경 변수에서 Twilio 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="28af6-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="28af6-138">Twilio 백 엔드에 대해 인증된 요청을 만들려면 Twilio 계정에 대해 사용자 이름 및 암호 집합 역할을 하는 계정 SID 및 인증 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="28af6-139">Azure에서 노드 모듈에 사용하기 위해 이를 구성하는 가장 안전한 방법은 시스템 환경 변수를 사용하는 것입니다. 시스템 환경 변수는 Azure 관리 콘솔에서 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="28af6-140">node.js 웹 사이트를 선택하고 "구성" 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="28af6-141">아래로 조금 스크롤하면 응용 프로그램의 구성 속성을 설정할 수 있는 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="28af6-142">표시된 것처럼 Twilio 계정 자격 증명([Twilio 콘솔에서 찾을 수 있음][twilio_console])을 입력합니다. 이름을 각각 `TWILIO_ACCOUNT_SID` 및 `TWILIO_AUTH_TOKEN`으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure 관리 콘솔][azure-admin-console]

<span data-ttu-id="28af6-144">이러한 변수를 구성하고 나서 Azure 콘솔에서 응용 프로그램을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="28af6-145">package.json에서 Twilio 모듈 선언</span><span class="sxs-lookup"><span data-stu-id="28af6-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="28af6-146">이제 [npm]을 통해 노드 모듈 종속성을 관리하기 위한 package.json을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="28af6-147">*Azure/node.js* 자습서에서 만든 `server.js` 파일과 같은 수준에서 `package.json`이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="28af6-148">이 파일 내에 다음을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-148">Inside this file, place the following:</span></span>

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

<span data-ttu-id="28af6-149">그러면 널리 사용되는 [Express 웹 프레임워크][express] 및 EJS 템플릿 엔진뿐만 아니라 종속성으로 twilio 모듈이 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="28af6-150">이제 모두 준비되었으니 코드를 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="28af6-151">아웃바운드 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="28af6-151">Make an Outbound Call</span></span>
<span data-ttu-id="28af6-152">선택한 번호로 전화하는 간단한 양식을 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="28af6-153">`server.js`를 열고 다음 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="28af6-154">"CHANGE_ME"라고 표시된 곳에 Azure 웹 사이트의 이름을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

<span data-ttu-id="28af6-155">이제 `views`라는 디렉터리를 만들고 이 디렉터리 내에 다음 내용이 포함된 `index.ejs`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="28af6-156">이제 웹 사이트를 Azure에 배포하고 홈을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="28af6-157">텍스트 필드에 전화 번호를 입력하고 Twilio 번호로부터 전화를 받을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="28af6-158">SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="28af6-158">Send an SMS Message</span></span>
<span data-ttu-id="28af6-159">이제 사용자 인터페이스 및 양식 처리 논리를 설정하여 문자 메시지를 보내겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="28af6-160">`server.js`를 열고 `app.post`에 대한 마지막 호출 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="28af6-161">`views/index.ejs`에서 첫 번째 양식 아래에 다른 양식을 추가하여 번호 및 문자 메시지를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="28af6-162">응용 프로그램을 Azure에 다시 배포하고 나면 이제 해당 양식을 제출하고 자신(또는 가까운 친구)에게 문자 메시지를 보낼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="28af6-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28af6-163">Next Steps</span></span>
<span data-ttu-id="28af6-164">이제 node.js 및 Twilio를 사용하여 통신하는 앱을 빌드하는 방법에 대한 기본 사항을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="28af6-165">그러나 이러한 예제는 Twilio 및 node.js를 사용하여 수행할 수 있는 작업의 극히 일부에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="28af6-166">Twilio와 node.js 사용에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="28af6-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="28af6-167">[공식 모듈 문서][docs]</span><span class="sxs-lookup"><span data-stu-id="28af6-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="28af6-168">[node.js 응용 프로그램에 VoIP 사용 자습서][voipnode]</span><span class="sxs-lookup"><span data-stu-id="28af6-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="28af6-169">[Votr - node.js 및 CouchDB를 사용한 실시간 SMS 투표 응용 프로그램(세 부분으로 구성되어 있음)][votr]</span><span class="sxs-lookup"><span data-stu-id="28af6-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="28af6-170">[node.js를 사용한 브라우저에서의 쌍 프로그래밍][pair]</span><span class="sxs-lookup"><span data-stu-id="28af6-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="28af6-171">Azure에서 node.js와 Twilio 해킹을 즐기시기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="28af6-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="28af6-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="28af6-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
