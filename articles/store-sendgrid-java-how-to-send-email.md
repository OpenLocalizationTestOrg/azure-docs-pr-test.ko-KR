---
title: "SendGrid 메일 서비스를 사용하는 방법(Java) | Microsoft Docs"
description: "Azure에서 SendGrid 메일 서비스를 사용하여 메일을 보내는 방법을 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="cea8a-104">Java의 SendGrid를 사용하여 메일을 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="cea8a-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="cea8a-105">이 가이드에서는 Azure에서 SendGrid 전자 메일 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="cea8a-106">샘플은 Java로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-106">The samples are written in Java.</span></span> <span data-ttu-id="cea8a-107">**전자 메일 생성**, **전자 메일 보내기**, **첨부 파일 추가**, **필터 사용**, **속성 업데이트** 등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="cea8a-108">SendGrid 및 전자 메일 보내기에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cea8a-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="cea8a-109">SendGrid 전자 메일 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="cea8a-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="cea8a-110">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 발송], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="cea8a-111">일반적인 SendGrid 사용 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="cea8a-112">고객에게 확인 메일 자동으로 보내기</span><span class="sxs-lookup"><span data-stu-id="cea8a-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="cea8a-113">월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리</span><span class="sxs-lookup"><span data-stu-id="cea8a-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="cea8a-114">차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="cea8a-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="cea8a-115">경향을 식별하는 데 도움이 되도록 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="cea8a-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="cea8a-116">고객 문의 전달</span><span class="sxs-lookup"><span data-stu-id="cea8a-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="cea8a-117">응용 프로그램의 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="cea8a-117">Email notifications from your application</span></span>

<span data-ttu-id="cea8a-118">자세한 내용은 <http://sendgrid.com>(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cea8a-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="cea8a-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cea8a-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="cea8a-120">방법: javax.mail 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="cea8a-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="cea8a-121">예를 들어 javax.mail 라이브러리를 <http://www.oracle.com/technetwork/java/javamail>(영문)에서 얻어 코드로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="cea8a-122">상위 수준에서, javax.mail 라이브러리를 사용하여 SMTP를 통해 전자 메일을 보내는 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="cea8a-123">SMTP 서버를 포함한 SMTP 값을 지정합니다. SendGrid는 smtp.sendgrid.net입니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="cea8a-124">*javax.mail.Authenticator* 클래스를 확장하고 *getPasswordAuthentication* 메서드 구현에서 SendGrid 사용자 이름 및 암호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="cea8a-125">*javax.mail.Session* 개체를 통해 인증된 전자 메일 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="cea8a-126">메시지를 만들고 **받는 사람**, **보낸 사람**, **제목** 및 내용 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="cea8a-127">[방법: 전자 메일 만들기](#how-to-create-an-email) 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="cea8a-128">*javax.mail.Transport* 개체를 통해 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="cea8a-129">[방법: 전자 메일 보내기][방법: 전자 메일 보내기] 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="cea8a-130">방법: 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="cea8a-130">How to: Create an email</span></span>
<span data-ttu-id="cea8a-131">다음은 메일 값을 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-131">The following shows how to specify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="cea8a-132">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="cea8a-132">How to: Send an email</span></span>
<span data-ttu-id="cea8a-133">다음은 메일을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="cea8a-134">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="cea8a-134">How to: Add an attachment</span></span>
<span data-ttu-id="cea8a-135">다음 코드는 첨부 파일을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="cea8a-136">방법: 필터를 사용하여 바닥글, 추적 및 분석을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="cea8a-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="cea8a-137">SendGrid는 *필터*사용을 통해 추가 전자 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="cea8a-138">클릭 추적, Google 분석, 구독 추적 등을 사용하도록 설정하는 것과 같이 특정 기능을 사용하도록 설정하기 위해 전자 메일 메시지에 추가할 수 있는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="cea8a-139">전체 필터 목록은 [필터 설정][Filter Settings](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cea8a-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="cea8a-140">다음은 보내는 전자 메일 아래쪽에 HTML 텍스트가 표시되도록 하는 바닥글 필터 삽입 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="cea8a-141">필터에 대한 또 다른 예제는 클릭 추적입니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="cea8a-142">전자 메일 텍스트에 다음과 같은 하이퍼링크가 포함되어 있고 클릭률을 추적하려 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="cea8a-143">클릭 추적을 사용하도록 설정하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="cea8a-144">방법: 전자 메일 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="cea8a-144">How to: Update email properties</span></span>
<span data-ttu-id="cea8a-145">사용 하 여 일부 전자 메일 속성을 덮어쓸 수  **설정*속성** *를 사용 하 여 추가 또는  **추가*속성** *입니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="cea8a-146">예를 들어 **ReplyTo** 주소를 지정하려면 다음을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="cea8a-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="cea8a-147">**참조** 받는 사람을 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="cea8a-148">방법: 추가 SendGrid 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="cea8a-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="cea8a-149">SendGrid는 Azure 응용 프로그램에서 추가 SendGrid 기능을 활용하는 데 사용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cea8a-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="cea8a-150">자세한 내용은 [SendGrid API 설명서][SendGrid API documentation](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cea8a-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea8a-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cea8a-151">Next steps</span></span>
<span data-ttu-id="cea8a-152">SendGrid 메일 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="cea8a-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="cea8a-153">Azure 배포에서 SendGrid를 사용하는 방법을 보여 주는 샘플: [Azure 배포에서 Java의 SendGrid를 사용하여 전자 메일을 보내는 방법](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="cea8a-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="cea8a-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="cea8a-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="cea8a-155">SendGrid API 설명서: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="cea8a-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="cea8a-156">Azure 고객을 위한 SendGrid 특가 제공: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="cea8a-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="cea8a-157">[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="cea8a-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="cea8a-158">[트랜잭션 전자 메일 발송]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="cea8a-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
