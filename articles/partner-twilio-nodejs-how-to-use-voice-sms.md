---
title: "음성, VoIP 및 Azure에서 SMS 메시징에 대 한 Twilio aaaUsing"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 Node.js로 작성되었습니다."
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
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="61c38-104">Azure에서 음성, VoIP 및 SMS 메시징을 위해 Twilio 사용</span><span class="sxs-lookup"><span data-stu-id="61c38-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="61c38-105">이 가이드에서는 방법을 toobuild 앱 통신 하는 Twilio와 Azure에서 node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="61c38-106">Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="61c38-106">What is Twilio?</span></span>
<span data-ttu-id="61c38-107">Twilio는 개발자 toomake 손쉽게 및 전화 통화를 수신, 송신 및 문자 메시지를 받 및 브라우저 기반 및 네이티브 모바일 응용 프로그램에 대 한 VoIP 전화를 포함 하는 API 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="61c38-108">깊이 있게 설명하기 전에 이러한 내용을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="61c38-109">전화 및 문자 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="61c38-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="61c38-110">Twilio 너무 개발자가 사용할 수[프로그래밍 가능한 전화 번호를 구입] [ purchase_phone] 보내고 통화 및 문자 메시지를 받을 tooboth 사용된 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="61c38-111">Twilio 번호는 인바운드 통화 나 문자를 받을 경우 Twilio 송신할 웹 응용 프로그램 HTTP POST 또는 GET 요청 통화 나 문자 toohandle hello 하는 방법에 대 한 지침은 묻는 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="61c38-112">서버는 HTTP 요청에 tooTwilio의 응답 [TwiML][twiml]는 간단한 방법에 대 한 지침을 포함 하는 XML 태그 집합이 toohandle 통화 나 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="61c38-113">잠시 후에 TwiML 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="61c38-114">전화 걸기 및 문자 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="61c38-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="61c38-115">개발자가 HTTP 요청 toohello Twilio 웹 서비스 API를 늘려 문자 메시지를 보낼 하거나 아웃 바운드 전화 통화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="61c38-116">아웃 바운드 호출에 대 한 hello 개발자 TwiML 지침 toohandle hello 아웃 바운드 연결 되 면를 호출 하는 방법을을 반환 하는 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="61c38-117">UI 코드(JavaScript, iOS 또는 Android)에 VoIP 기능 포함</span><span class="sxs-lookup"><span data-stu-id="61c38-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="61c38-118">Twilio는 모든 데스크톱 웹 브라우저, iOS 앱 또는 Android 앱을 VoIP 전화로 변환할 수 있는 클라이언트 쪽 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="61c38-119">이 문서에 대해 살펴볼 것 방법 toouse VoIP hello 브라우저에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="61c38-120">또한 toohello에서 *Twilio JavaScript SDK* hello 브라우저에서 실행, 서버 쪽 응용 프로그램 (node.js 응용 프로그램) 이어야 합니다 "기능 토큰" toohello JavaScript 클라이언트 사용된 tooissue 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="61c38-121">자세한 내용은 VoIP node.js와 함께 사용 하는 방법에 대 한 [hello Twilio 개발자 블로그][voipnode]합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="61c38-122">Twilio 등록(Microsoft 할인)</span><span class="sxs-lookup"><span data-stu-id="61c38-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="61c38-123">Twilio 서비스를 사용하기 전에 먼저 [계정을 등록][signup]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="61c38-124">Microsoft Azure 고객과 특별 할인 가격-수신 [여기 있는지 toosign 수][signup]!</span><span class="sxs-lookup"><span data-stu-id="61c38-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="61c38-125">node.js Azure 웹 사이트 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="61c38-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="61c38-126">다음으로, 해야 toocreate Azure에서 실행 되는 node.js 웹 사이트.</span><span class="sxs-lookup"><span data-stu-id="61c38-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="61c38-127">[이 작업을 수행 하는 것에 대 한 공식 설명서 hello은 여기에서 찾을][azure_new_site]합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="61c38-128">상위 수준 hello 다음 수행:</span><span class="sxs-lookup"><span data-stu-id="61c38-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="61c38-129">Azure 계정 등록(아직 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="61c38-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="61c38-130">Hello Azure 관리 콘솔 toocreate 새 웹 사이트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="61c38-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="61c38-131">소스 제어 지원 추가(git를 사용했다고 가정함)</span><span class="sxs-lookup"><span data-stu-id="61c38-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="61c38-132">간단한 node.js 웹 응용 프로그램을 사용하여 파일 `server.js` 만들기</span><span class="sxs-lookup"><span data-stu-id="61c38-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="61c38-133">이 간단한 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="61c38-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="61c38-134">Hello Twilio 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="61c38-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="61c38-135">다음으로, toowrite hello Twilio API의 낮추는 간단한 node.js 응용 프로그램을 사용 하기 시작할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="61c38-136">시작 하기 전에 tooconfigure 우리의 Twilio 계정 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="61c38-137">시스템 환경 변수에서 Twilio 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="61c38-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="61c38-138">Hello Twilio 백 엔드에 대 한 주문 toomake 인증 요청에 우리의 계정 SID 및 인증 토큰을 hello 사용자 이름 및 암호가 Twilio 계좌에 대 한 설정으로 어떤 함수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="61c38-139">가장 안전한 방법은 tooconfigure hello Azure의 hello 노드 모듈 사용에 대 한 이러한 hello Azure 관리 콘솔에서 직접 설정할 수 있는 시스템 환경 변수를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="61c38-140">Node.js 웹 사이트를 선택 하 고 hello "구성" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="61c38-141">아래로 조금 스크롤하면 응용 프로그램의 구성 속성을 설정할 수 있는 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="61c38-142">Twilio 계정 자격 증명을 입력 ([Twilio 콘솔에][twilio_console])-표시 된 것 처럼 확인 되었는지 tooname 해당 `TWILIO_ACCOUNT_SID` 및 `TWILIO_AUTH_TOKEN`각각:</span><span class="sxs-lookup"><span data-stu-id="61c38-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure 관리 콘솔][azure-admin-console]

<span data-ttu-id="61c38-144">이러한 변수를 구성한 경우 hello Azure 콘솔에서에서 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="61c38-145">Package.json의 hello Twilio 모듈 선언</span><span class="sxs-lookup"><span data-stu-id="61c38-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="61c38-146">다음으로 필요한 toocreate package.json toomanage 우리의 노드 모듈 종속성을 통해 [npm]합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="61c38-147">Hello 동일 수준으로 hello `server.js` hello에서 만든 파일을 *Azure/node.js* 자습서 라는 파일을 만들어 `package.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="61c38-148">이 파일을 내부 hello 다음을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="61c38-149">이 선언 hello twilio 모듈은 종속성으로 hello 인기 있는 [웹 프레임 워크 Express] [ express] 및 hello EJS 템플릿 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="61c38-150">이제 모두 준비되었으니 코드를 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="61c38-151">아웃바운드 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="61c38-151">Make an Outbound Call</span></span>
<span data-ttu-id="61c38-152">선택한 호출 tooa 숫자 정렬은 하는 단순 폼을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="61c38-153">열고 `server.js`, hello 코드 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="61c38-154">"CHANGE_ME"-azure 웹 사이트의 hello 이름을 대시보드에 배치한 것 라고 표시 된 부분 note:</span><span class="sxs-lookup"><span data-stu-id="61c38-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
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

<span data-ttu-id="61c38-155">다음으로 라는 디렉터리를 만듭니다 `views` -이 디렉터리 내 라는 파일을 만들어 `index.ejs` 내용을 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="61c38-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="61c38-156">이제 웹 사이트 tooAzure를 배포 하 고 홈을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="61c38-157">수 tooenter hello 텍스트 필드에 전화 번호 고 해야 Twilio 번호에서 전화를 받을!</span><span class="sxs-lookup"><span data-stu-id="61c38-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="61c38-158">SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="61c38-158">Send an SMS Message</span></span>
<span data-ttu-id="61c38-159">이제, 문자 메시지를 사용자 인터페이스 및 양식 논리 toosend 처리를 보겠습니다 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="61c38-160">열고 `server.js`, hello 너무 hello 마지막 호출 후 코드를 다음 추가`app.post`:</span><span class="sxs-lookup"><span data-stu-id="61c38-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="61c38-161">`views/index.ejs`, 숫자 및 문자 메시지를 다른 양식에서 첫 번째 toosubmit hello 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="61c38-162">응용 프로그램 tooAzure 프로그램을 다시 배포 하 고 형성 하 고 직접 (또는 가장 가까운 친구 모든) 문자 메시지를 보낼 수 toosubmit 수 있어야!</span><span class="sxs-lookup"><span data-stu-id="61c38-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="61c38-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61c38-163">Next Steps</span></span>
<span data-ttu-id="61c38-164">Node.js와 통신 하는 Twilio toobuild 응용 프로그램을 사용 하 여의 hello 기본 사항을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="61c38-165">하지만 이러한 예제에는 거의 Twilio 및 node.js로 가능한의 hello 화면 스크래치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="61c38-166">Node.js와 함께 Twilio를 사용 하 여 자세한 내용은 다음 리소스는 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="61c38-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="61c38-167">[공식 모듈 문서][docs]</span><span class="sxs-lookup"><span data-stu-id="61c38-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="61c38-168">[node.js 응용 프로그램에 VoIP 사용 자습서][voipnode]</span><span class="sxs-lookup"><span data-stu-id="61c38-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="61c38-169">[Votr - node.js 및 CouchDB를 사용한 실시간 SMS 투표 응용 프로그램(세 부분으로 구성되어 있음)][votr]</span><span class="sxs-lookup"><span data-stu-id="61c38-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="61c38-170">[Node.js 사용 하 여 hello 브라우저의 쌍 프로그래밍][pair]</span><span class="sxs-lookup"><span data-stu-id="61c38-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="61c38-171">Azure에서 node.js와 Twilio 해킹을 즐기시기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="61c38-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
