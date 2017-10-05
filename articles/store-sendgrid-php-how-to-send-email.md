---
title: "SendGrid 메일 서비스를 사용하는 방법(PHP) | Microsoft Docs"
description: "Azure에서 SendGrid 메일 서비스를 사용하여 메일을 보내는 방법을 알아봅니다. 코드 샘플은 PHP로 작성되었습니다."
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
ms.openlocfilehash: 523b986f66a2e48685e9707903194856f0dcf4a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-sendgrid-email-service-from-php"></a><span data-ttu-id="5aa3c-104">PHP에서 SendGrid 메일 서비스를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="5aa3c-104">How to Use the SendGrid Email Service from PHP</span></span>
<span data-ttu-id="5aa3c-105">이 가이드에서는 Azure에서 SendGrid 전자 메일 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="5aa3c-106">샘플은 PHP로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-106">The samples are written in PHP.</span></span>
<span data-ttu-id="5aa3c-107">**전자 메일 작성**, **전자 메일 보내기**, **첨부 파일 추가** 등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="5aa3c-108">SendGrid 및 전자 메일 보내기에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="5aa3c-109">SendGrid 전자 메일 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="5aa3c-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="5aa3c-110">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 발송], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="5aa3c-111">일반적인 SendGrid 사용 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="5aa3c-112">고객에게 확인 메일 자동으로 보내기</span><span class="sxs-lookup"><span data-stu-id="5aa3c-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="5aa3c-113">월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리</span><span class="sxs-lookup"><span data-stu-id="5aa3c-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="5aa3c-114">차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="5aa3c-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="5aa3c-115">경향을 식별하는 데 도움이 되도록 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="5aa3c-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="5aa3c-116">고객 문의 전달</span><span class="sxs-lookup"><span data-stu-id="5aa3c-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="5aa3c-117">응용 프로그램의 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="5aa3c-117">Email notifications from your application</span></span>

<span data-ttu-id="5aa3c-118">자세한 내용은 [https://sendgrid.com][https://sendgrid.com]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="5aa3c-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="5aa3c-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="5aa3c-120">PHP 응용 프로그램에서 SendGrid 사용</span><span class="sxs-lookup"><span data-stu-id="5aa3c-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="5aa3c-121">Azure PHP 응용 프로그램에서 SendGrid를 사용하기 위해 특별한 구성이 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="5aa3c-122">SendGrid는 서비스이므로, 온-프레미스 응용 프로그램에서 액세스하는 것과 동일한 방법으로 클라우드 응용 프로그램에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="5aa3c-123">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="5aa3c-123">How to: Send an Email</span></span>
<span data-ttu-id="5aa3c-124">SendGrid에서 제공하는 SMTP 또는 웹 API를 사용하여 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-124">You can send email using either SMTP or the Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="5aa3c-125">SMTP API</span><span class="sxs-lookup"><span data-stu-id="5aa3c-125">SMTP API</span></span>
<span data-ttu-id="5aa3c-126">SendGrid SMTP API를 사용하여 메일을 보내려면 PHP 응용 프로그램에서 메일을 보내기 위한 구성 요소 기반 라이브러리인 *Swift Mailer*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="5aa3c-127">[http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0에서 *Swift Mailer* 라이브러리를 다운로드할 수 있습니다([Composer]를 사용하여 Swift Mailer 설치).</span><span class="sxs-lookup"><span data-stu-id="5aa3c-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span></span> <span data-ttu-id="5aa3c-128">라이브러리를 사용하여 전자 메일 보내기에는<span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span> 및 <span class="auto-style2">Swift\_Message</span> 클래스의 인스턴스 생성, 적절한 속성 설정 및 <span class="auto-style2">Swift\_Mailer::send</span> 메서드 호출이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the receiver is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');
     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="5aa3c-129">웹 API</span><span class="sxs-lookup"><span data-stu-id="5aa3c-129">Web API</span></span>
<span data-ttu-id="5aa3c-130">PHP의 [curl 함수][curl function] 를 사용하여 SendGrid 웹 API를 사용하여 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span></span>

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

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="5aa3c-131">SendGrid의 웹 API는 REST API와 매우 유사하지만 대부분의 호출에서 GET 및 POST 동사를 상호 교환 가능한 방식으로 사용할 수 있으므로 진정한 의미에서 RESTful API는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="5aa3c-132">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="5aa3c-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="5aa3c-133">SMTP API</span><span class="sxs-lookup"><span data-stu-id="5aa3c-133">SMTP API</span></span>
<span data-ttu-id="5aa3c-134">SMTP API를 사용하여 첨부 파일을 보내는 프로세스에는 Swift Mailer를 사용하여 메일을 보내기 위한 예제 스크립트에 대한 추가 코드 줄이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the reciever is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');

     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="5aa3c-135">추가 코드 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-135">The additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="5aa3c-136">이 코드 줄은 <span class="auto-style2">Swift\_Message</span> 개체에서 첨부 메서드를 호출하고 <span class="auto-style2">Swift\_Attachment</span> 클래스의 정적 <span class="auto-style2">fromPath</span> 메서드를 사용하여 파일을 가져와서 메시지에 첨부합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span></span>

### <a name="web-api"></a><span data-ttu-id="5aa3c-137">웹 API</span><span class="sxs-lookup"><span data-stu-id="5aa3c-137">Web API</span></span>
<span data-ttu-id="5aa3c-138">웹 API를 사용한 첨부 파일 보내기는 웹 API를 사용하여 메일 보내기와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span></span> <span data-ttu-id="5aa3c-139">그러나 다음 예제에서 매개 변수 배열은 이 요소를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-139">However, note that in the example that follows, the parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="5aa3c-140">예제:</span><span class="sxs-lookup"><span data-stu-id="5aa3c-140">Example:</span></span>

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
         'html' => '<p> the HTML </p>',
         'text' => 'the plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="5aa3c-141">방법: 필터를 사용하여 바닥글, 추적 및 분석을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5aa3c-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="5aa3c-142">SendGrid는 '필터' 사용을 통해 추가 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-142">SendGrid provides additional email functionality through the use of 'filters'.</span></span> <span data-ttu-id="5aa3c-143">클릭 추적, Google 분석, 구독 추적 등을 사용하도록 설정하는 것과 같이 특정 기능을 사용하도록 설정하기 위해 전자 메일 메시지에 추가할 수 있는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="5aa3c-144">필터는 filters 속성을 사용하여 메시지에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-144">Filters can be applied to a message by using the filters property.</span></span> <span data-ttu-id="5aa3c-145">각 필터는 필터별 설정을 포함하는 해시에 의해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="5aa3c-146">다음 예제에서는 바닥글 필터를 사용하도록 설정하고 메일 메시지의 맨 아래에 추가할 텍스트 메시지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span></span>
<span data-ttu-id="5aa3c-147">이 예제의 경우 [sendgrid-php 라이브러리]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="5aa3c-148">라이브러리를 설치하려면 [Composer]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-148">Use [Composer] to install library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="5aa3c-149">예제:</span><span class="sxs-lookup"><span data-stu-id="5aa3c-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // The list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request to SendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify the names of the recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of the above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled the footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // The subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy the user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $to = 'john@contoso.com';

     # Create the body of the message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of the email
     # if the receiver is able to view html emails then only the html
     # email will be displayed

     /*
      * Note the variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment to call you at -time- EST to discuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     to call you at -time- EST to discuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach the body of the email
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

## <a name="next-steps"></a><span data-ttu-id="5aa3c-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5aa3c-150">Next Steps</span></span>
<span data-ttu-id="5aa3c-151">SendGrid 전자 메일 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="5aa3c-152">SendGrid 설명서: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="5aa3c-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="5aa3c-153">SendGrid PHP 라이브러리: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="5aa3c-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="5aa3c-154">Azure 고객을 위한 SendGrid 특가 제공: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="5aa3c-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="5aa3c-155">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aa3c-155">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
<span data-ttu-id="5aa3c-156">[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="5aa3c-156">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="5aa3c-157">[트랜잭션 전자 메일 발송]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="5aa3c-157">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
<span data-ttu-id="5aa3c-158">[sendgrid-php 라이브러리]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span><span class="sxs-lookup"><span data-stu-id="5aa3c-158">[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span></span>
<span data-ttu-id="5aa3c-159">[Composer]: https://getcomposer.org/download/</span><span class="sxs-lookup"><span data-stu-id="5aa3c-159">[Composer]: https://getcomposer.org/download/</span></span>
