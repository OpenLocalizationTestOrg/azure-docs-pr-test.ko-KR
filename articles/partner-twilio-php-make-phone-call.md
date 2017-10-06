---
title: "Twilio (PHP)에서 전화 통화를 aaaHow toomake | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 샘플은 PHP 응용 프로그램용입니다."
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
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>어떻게 tooMake Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio
hello 다음 예제에 나와 사용 하는 방법을 Twilio toomake Azure에서 호스팅되는 PHP 웹 페이지 코드에서 호출 합니다. hello 다음 스크린 샷에서 같이 hello 결과 응용 프로그램에 전화 통화 값에 대 한 hello 사용자 라는 메시지가 나타납니다.

![Twilio 및 PHP를 사용하는 Azure 통화 양식][twilio_php]

Toodo hello 다음 해야이 항목의 toouse hello 코드:

1. [Twilio 콘솔][twilio_console]에서 Twilio 계정 및 인증 토큰을 가져옵니다. Twilio, 시작 tooget 평가에서 가격 책정 [http://www.twilio.com/pricing][twilio_pricing]합니다. [https://www.twilio.com/try-twilio][try_twilio]에서 체험 계정을 등록할 수 있습니다.
2. Hello 가져올 [PHP 용 Twilio 라이브러리](https://github.com/twilio/twilio-php) 하거나 배 패키지로 설치 합니다. 자세한 내용은 참조 hello [추가 정보 파일](https://github.com/twilio/twilio-php/blob/master/README.md)합니다.
3. PHP 용 hello Azure SDK를 설치 합니다. Hello SDK에 대 한 지침은 설치의 개요를 참조 하십시오. [hello Azure SDK for PHP 설정](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>전화 걸기 웹 양식 만들기
다음 HTML hello 코드 방법을 보여 줍니다 toobuild 웹 페이지 (**callform.html**)를 호출 하는 것에 대 한 사용자 데이터를 검색 하는:

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
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>Hello 코드 toomake hello 호출 만들기
코드에서 보여 주는 방법을 다음 hello toobuild **makecall.php**는 hello 사용자가 표시 하는 hello 양식을 전송 하면 호출 되 **callform.html**합니다. 아래 표시 된 hello 코드 hello 호출 메시지를 만들고 hello 호출을 생성 합니다. 또한 있는지 toouse hello에서 Twilio 계정 및 인증 토큰 될 [Twilio 콘솔] [ twilio_console] hello 자리 표시자 값이 너무 할당 하는 대신**$sid** 및 **$token** hello 코드 아래에 있습니다.

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

또한 toomaking hello 호출 **makecall.php** hello 이미지 아래에 표시 된 대로 일부 호출의 메타 데이터를 표시 합니다. 통화 메타데이터에 대한 자세한 내용은 [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties]를 참조하세요.

![Twilio 및 PHP를 사용하는 Azure 통화 응답][twilio_php_response]

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
hello 다음 단계는 toodeploy 프로그램 응용 프로그램 tooAzure 웹 사이트입니다. hello 다음 문서 hello에 대 한 정보가 웹 사이트를 만들고 (각 문서의 일부 정보는 적용 됨) 하는 경우 Git, FTP 또는 WebMatrix를 사용 하 여 코드를 배포 합니다.

* [PHP-MySQL Azure 웹 사이트 만들기 및 Git를 사용하여 배포](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [PHP-MySQL Azure 웹 사이트 만들기 및 FTP를 사용하여 배포](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>다음 단계
이 코드는 tooshow 제공한 하면 기본 기능 Twilio를 사용 하 여 Azure에서 php에서 합니다. 프로덕션 환경에서 tooAzure를 배포 하기 전에 tooadd 자세한 오류 처리 또는 다른 기능을 할 수 있습니다. 예:

* Web form을 사용 하는 대신 Azure 저장소 blob 나 SQL 데이터베이스 toostore 전화 번호를 사용 하 고 텍스트를 호출할 수 있습니다. PHP에서 Azure Storage Blob 사용에 대한 내용은 [PHP 응용 프로그램에서 Azure Storage 사용][howto_blob_storage_php]을 참조하세요. PHP에서 SQL Database 사용에 대한 내용은 [PHP 응용 프로그램에서 SQL Database 사용][howto_sql_azure_php]을 참조하세요.
* hello **makecall.php** Twilio 제공 URL을 사용 하는 코드 ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio 방법을 알려 주는 Twilio Markup Language (TwiML) 응답 hello 호출으로 tooproceed 합니다. 예를 들어 hello TwiML 반환 되는 포함 될 수 있습니다는 `<Say>` 텍스트 음성된 toohello 호출 받는 사람 중에 발생 하는 동사입니다. Hello Twilio 제공 URL을 사용 하는 대신 사용자 고유의 서비스 toorespond tooTwilio 요청을 작성할 수 있습니다. 자세한 내용은 참조 [어떻게 tooUse 음성 및 SMS 기능을 PHP Twilio][howto_twilio_voice_sms_php]합니다. TwiML에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml][twiml]에서 확인할 수 있고, `<Say>` 및 기타 Twilio 동사에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml/say][twilio_say]에서 확인할 수 있습니다.
* hello Twilio 보안 지침을 읽고 [https://www.twilio.com/docs/security][twilio_docs_security]합니다.

Twilio에 대한 자세한 내용은 [https://www.twilio.com/docs][twilio_docs]를 참조하세요.

## <a name="see-also"></a>참고 항목
* [어떻게 tooUse Twilio 음성 및 SMS 기능 PHP에 대 한](partner-twilio-php-how-to-use-voice-sms.md)

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
