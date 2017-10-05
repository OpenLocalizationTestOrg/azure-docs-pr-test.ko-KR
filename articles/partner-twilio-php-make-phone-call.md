---
title: "Twilio에서 전화를 거는 방법(PHP) | Microsoft Docs"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 샘플은 PHP 응용 프로그램용입니다."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: f35450ace02727ddf392dbbe857b934a45ee022a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="fc912-104">Azure의 PHP 응용 프로그램에서 Twilio를 사용하여 전화를 거는 방법</span><span class="sxs-lookup"><span data-stu-id="fc912-104">How to Make a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="fc912-105">다음 예제는 Azure에 호스트된 PHP 웹 페이지에서 Twilio를 사용하여 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-105">The following example shows you how you can use Twilio to make a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="fc912-106">다음 스크린샷에 표시된 것처럼 응용 프로그램에서 사용자에게 전화 통화 값을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-106">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Twilio 및 PHP를 사용하는 Azure 통화 양식][twilio_php]

<span data-ttu-id="fc912-108">이 항목에서 코드를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-108">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="fc912-109">[Twilio 콘솔][twilio_console]에서 Twilio 계정 및 인증 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="fc912-110">Twilio를 시작하려면 [http://www.twilio.com/pricing][twilio_pricing]에서 가격을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-110">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="fc912-111">[https://www.twilio.com/try-twilio][try_twilio]에서 체험 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="fc912-112">[PHP용 Twilio 라이브러리](https://github.com/twilio/twilio-php) 를 가져오거나 PEAR 패키지로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-112">Obtain the [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="fc912-113">자세한 내용은 [추가 정보 파일](https://github.com/twilio/twilio-php/blob/master/README.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-113">For more information, see the [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="fc912-114">PHP용 Azure SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-114">Install the Azure SDK for PHP.</span></span> <span data-ttu-id="fc912-115">SDK에 대한 개요 및 설치 지침은 [PHP용 Azure SDK 설정](app-service-web/web-sites-php-mysql-deploy-use-git.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-115">For an overview of the SDK and instructions on installing it, see [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="fc912-116">전화 걸기 웹 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="fc912-116">Create a web form for making a call</span></span>
<span data-ttu-id="fc912-117">다음 HTML 코드는 전화를 걸기 위해 사용자 데이터를 검색하는 웹 페이지(**callform.html**)를 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-117">The following HTML code shows how to build a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is the call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="fc912-118">코드를 만들어 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="fc912-118">Create the code to make the call</span></span>
<span data-ttu-id="fc912-119">다음 코드는 사용자가 **callform.html**에 의해 표시된 양식을 제출할 때 호출되는 **makecall.php**를 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-119">The following code shows how to build **makecall.php**, which is called when the user submits the form displayed by **callform.html**.</span></span> <span data-ttu-id="fc912-120">아래 표시된 코드는 통화 메시지를 만들고 통화를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-120">The code shown below creates the call message and generates the call.</span></span> <span data-ttu-id="fc912-121">또한 아래 코드에 있는 **$sid** 및 **$token**에 할당된 자리 표시자 값 대신 [Twilio 콘솔][twilio_console]에서 Twilio 계정 및 인증 토큰을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-121">Also, be sure to use your Twilio account and authentication token from the [Twilio Console][twilio_console] instead of the placeholder values assigned to **$sid** and **$token** in the code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="fc912-122">전화 걸기와 함께, **makecall.php**는 몇몇 통화 메타데이터를 아래 이미지에 표시된 대로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-122">In addition to making the call, **makecall.php** displays some call metadata, as is shown in the image below.</span></span> <span data-ttu-id="fc912-123">통화 메타데이터에 대한 자세한 내용은 [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Twilio 및 PHP를 사용하는 Azure 통화 응답][twilio_php_response]

## <a name="run-the-application"></a><span data-ttu-id="fc912-125">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="fc912-125">Run the application</span></span>
<span data-ttu-id="fc912-126">다음 단계는 Azure 웹 사이트에 응용 프로그램을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-126">The next step is to deploy your application to Azure Websites.</span></span> <span data-ttu-id="fc912-127">다음 문서에는 웹 사이트 생성 및 Git, FTP 또는 WebMatrix를 사용하여 코드 배포에 대한 정보가 들어 있습니다(각 문서의 일부 정보는 관련 없음).</span><span class="sxs-lookup"><span data-stu-id="fc912-127">The following articles contain the information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="fc912-128">PHP-MySQL Azure 웹 사이트 만들기 및 Git를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="fc912-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="fc912-129">PHP-MySQL Azure 웹 사이트 만들기 및 FTP를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="fc912-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="fc912-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc912-130">Next steps</span></span>
<span data-ttu-id="fc912-131">이 코드는 Azure의 PHP에서 Twilio를 사용하는 기본 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-131">This code was provided to show you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="fc912-132">Azure를 프로덕션에 배포하기 전에 더 많은 오류 처리 또는 기타 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-132">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="fc912-133">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-133">For example:</span></span>

* <span data-ttu-id="fc912-134">웹 양식을 사용하는 대신, Azure 저장소 Blob 또는 SQL 데이터베이스를 사용하여 전화 번호 및 통화 텍스트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-134">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="fc912-135">PHP에서 Azure Storage Blob 사용에 대한 내용은 [PHP 응용 프로그램에서 Azure Storage 사용][howto_blob_storage_php]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="fc912-136">PHP에서 SQL Database 사용에 대한 내용은 [PHP 응용 프로그램에서 SQL Database 사용][howto_sql_azure_php]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="fc912-137">**makecall.php** 코드는 Twilio 제공 URL([http://twimlets.com/message][twimlet_message_url])을 사용하여 Twilio에 통화를 진행하는 방법을 알리는 TwiML(Twilio Markup Language) 응답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-137">The **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) to provide a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="fc912-138">예를 들어 반환되는 TwiML에는 통화 수신자에게 말하는 텍스트에 나타나는 `<Say>` 동사가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-138">For example, the TwiML that is returned can contain a `<Say>` verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="fc912-139">Twilio 제공 URL을 사용하는 대신, 고유한 서비스를 빌드하여 Twilio의 요청에 응답할 수 있습니다. 자세한 내용은 [PHP에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법][howto_twilio_voice_sms_php]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-139">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="fc912-140">TwiML에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml][twiml]에서 확인할 수 있고, `<Say>` 및 기타 Twilio 동사에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml/say][twilio_say]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc912-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="fc912-141">[https://www.twilio.com/docs/security][twilio_docs_security]에서 Twilio 보안 지침을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-141">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="fc912-142">Twilio에 대한 자세한 내용은 [https://www.twilio.com/docs][twilio_docs]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc912-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="fc912-143">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fc912-143">See Also</span></span>
* [<span data-ttu-id="fc912-144">PHP에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="fc912-144">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
