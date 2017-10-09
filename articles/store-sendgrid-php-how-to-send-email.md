---
title: "aaaHow toouse hello SendGrid 전자 메일 서비스 (PHP) | Microsoft Docs"
description: "자세한 내용은 Azure에서 SendGrid 전자 메일 서비스 hello로 전자 메일을 보내려면 어떻게 합니다. 코드 샘플은 PHP로 작성되었습니다."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>TooUse는 PHP에서 SendGrid 전자 메일 서비스를 hello 하는 방법
이 가이드에서는 tooperform SendGrid hello로 일반적인 프로그래밍 작업 Azure에서 서비스를 메일 하는 방법을 보여 줍니다. hello 샘플 PHP로 작성 됩니다.
hello 가이드에서 다루는 시나리오 포함 **전자 메일 구성**, **메일을 보내는**, 및 **첨부 파일 추가**합니다. SendGrid 및 전자 메일에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

## <a name="what-is-hello-sendgrid-email-service"></a>Hello SendGrid 전자 메일 서비스는 무엇입니까?
SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다. 일반적인 SendGrid 사용 시나리오는 다음과 같습니다.

* 자동으로 확인 메일 toocustomers 보내기
* 월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리
* 차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집
* Toohelp 추세를 파악 하는 보고서 생성
* 고객 문의 전달
* 응용 프로그램의 전자 메일 알림

자세한 내용은 [https://sendgrid.com][https://sendgrid.com]을 참조하세요.

## <a name="create-a-sendgrid-account"></a>SendGrid 계정 만들기
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>PHP 응용 프로그램에서 SendGrid 사용
Azure PHP 응용 프로그램에서 SendGrid를 사용하기 위해 특별한 구성이 필요하지는 않습니다. SendGrid 서비스 때문에 정확 하 게 hello에서 액세스할 수 있습니다 그대로 클라우드 응용 프로그램에서 같은 방식으로 온-프레미스 응용 프로그램에서 수 있습니다.

## <a name="how-to-send-an-email"></a>방법: 전자 메일 보내기
SMTP 또는 hello SendGrid에서 제공 하는 웹 API를 사용 하 여 메일을 보낼 수 있습니다.

### <a name="smtp-api"></a>SMTP API
SendGrid SMTP API를 사용 하 여 hello를 사용 하 여 toosend 메일 *Swift 메일러*, PHP 응용 프로그램에서 전자 메일을 보내기 위한 구성 요소 기반 라이브러리입니다. Hello를 다운로드할 수 있습니다 *Swift 메일러* 에서 라이브러리 [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (사용 하 여 [작성기] tooinstall Swift Mailer)입니다. 인스턴스를 만드는 과정이 포함 되어 hello 라이브러리와 전자 메일을 보내기는 <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, 및 <span class="auto-style2">Swift\_메시지 </span> 클래스, 적절 한 속성을 설정 하 고 호출에서 <span class="auto-style2">Swift\_Mailer::send</span> 메서드.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>Web API
PHP의를 사용 하 여 [함수 curl] [ curl function] SendGrid 웹 API hello toosend 전자 메일을 사용 합니다.

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

SendGrid의 웹 API 되지 않은 경우에 실제로 RESTful API 대부분 호출에 둘 다가 GET 및 POST 동사를 교대로 사용 될 수 있으므로 매우 유사한 tooa REST API입니다.

## <a name="how-to-add-an-attachment"></a>방법: 첨부 파일 추가
### <a name="smtp-api"></a>SMTP API
Hello SMTP API를 사용 하 여 첨부 파일 보내기 Swift 메일러 전자 메일을 보내기 위한 코드 toohello 예제 스크립트의 한 줄 포함 됩니다.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

hello 추가 코드 줄은 다음과 같습니다.

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

이 줄의 코드 호출 hello 연결 방법을 <span class="auto-style2">Swift\_메시지</span> 개체 및 정적 메서드를 사용 하 여 <span class="auto-style2">fromPath</span> 에 <span class="auto-style2">Swift\_첨부</span>tooget 클래스 및 파일 tooa 메시지를 연결 합니다.

### <a name="web-api"></a>Web API
Hello 웹 API를 사용 하 여 첨부 파일은 매우 유사한 toosending 보내는 웹 API hello 사용 하 여 전자 메일입니다. 그러나 뒤에 오는 hello 예제 hello 매개 변수 배열에 해야이 요소 포함 표시 note:

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

예제:

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>방법: 사용 하 여 필터 tooEnable 바닥글, 추적 및 분석
SendGrid '필터' hello 사용을 통해 추가 전자 메일 기능을 제공합니다. 이 클릭 추적, Google 분석, 추적, 구독을 설정 하는 등 특정 기능을 사용 하도록 설정 하려면 tooan 전자 메일 메시지를 추가할 수 있는 설정 등입니다.

필터는 hello 필터 속성을 사용 하 여 적용 된 tooa 메시지를 수 있습니다. 각 필터는 필터별 설정을 포함하는 해시에 의해 지정됩니다. 다음 예에서는 hello 바닥글 필터를 사용 하도록 설정 하 고 수 있는 문자 메시지 추가 toohello 맨 hello 전자 메일 메시지를 지정 합니다.
이 예제의 경우 [sendgrid-php 라이브러리]를 사용합니다.
사용 하 여 [작성기] tooinstall 라이브러리:

    php composer.phar require sendgrid/sendgrid 2.1.1

예제:    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>다음 단계
Hello SendGrid 전자 메일 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* SendGrid 설명서: <https://sendgrid.com/docs>
* SendGrid PHP 라이브러리: <https://github.com/sendgrid/sendgrid-php>
* Azure 고객을 위한 SendGrid 특가 제공: <https://sendgrid.com/windowsazure.html>

자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions
[트랜잭션 전자 메일 배달]: https://sendgrid.com/transactional-email
[sendgrid-php 라이브러리]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[작성기]: https://getcomposer.org/download/
