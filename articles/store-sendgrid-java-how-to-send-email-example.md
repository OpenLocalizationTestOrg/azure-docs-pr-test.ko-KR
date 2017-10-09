---
title: aaastore-sendgrid-java-how-to-send-email-example
description: "Toosend 메일 Azure 배포의 Java에서 SendGrid를 사용 하는 방법"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="bfd41-103">어떻게 tooSend 전자 메일 Azure 배포의 Java에서 SendGrid를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bfd41-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="bfd41-104">hello 다음 예제에서는 하면 Azure에서 호스팅되는 웹 페이지에서 SendGrid toosend 보내는 전자 메일을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bfd41-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="bfd41-105">다음 스크린 샷에서 hello와 같이 hello 결과 응용 프로그램에 hello 사용자에 게 전자 메일 값 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![전자 메일 양식][emailform]

<span data-ttu-id="bfd41-107">전자 메일으로 인해 발생 하는 hello 스크린 샷 다음 비슷한 toohello 보입니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-107">hello resulting email will look similar toohello following screen shot.</span></span>

![전자 메일 메시지][emailsent]

<span data-ttu-id="bfd41-109">Toodo hello 다음 해야이 항목의 toouse hello 코드:</span><span class="sxs-lookup"><span data-stu-id="bfd41-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="bfd41-110">가져올에서 javax.mail Jar 예를 들어 hello <http://www.oracle.com/technetwork/java/javamail/index.html>합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="bfd41-111">Hello Jar tooyour Java 빌드 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="bfd41-112">Eclipse toocreate이 Java 응용 프로그램 사용 중인 경우에 Eclipse의 배포 어셈블리 기능을 사용 하 여 응용 프로그램 배포 파일 (WAR)에서 hello SendGrid 라이브러리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="bfd41-113">이 Java 응용 프로그램 Eclipse toocreate을 사용 하지 않는 경우 확인 hello 라이브러리 hello 내에 포함 됩니다. 응용 프로그램의 Java 응용 프로그램에서는, 및 추가 된 toohello 클래스 경로와 동일한 Azure 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="bfd41-114">사용자 고유의 SendGrid 사용자 이름 및 암호, toobe 수 toosend hello 전자 메일도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="bfd41-115">SendGrid, 시작 tooget 참조 [toosend Java에서 SendGrid를 사용 하 여 전자 메일 방법](store-sendgrid-java-how-to-send-email.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="bfd41-116">Hello에 대 한 정보를 익히는 또한 [Eclipse에서 Azure 용 Hello World 응용 프로그램을 만드는](http://msdn.microsoft.com/library/windowsazure/hh690944), 또는 Eclipse를 사용 하지 않는 경우 Azure에서 Java 응용 프로그램을 호스트에 대 한 다른 기술로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="bfd41-117">전자 메일을 보내기 위한 웹 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="bfd41-117">Create a web form for sending email</span></span>
<span data-ttu-id="bfd41-118">코드 다음 hello toocreate 웹 메일 전송을 위한 tooretrieve 사용자 데이터를 형성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="bfd41-119">이 콘텐츠를 위해 hello JSP 파일의 이름은 **emailform.jsp**합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="bfd41-120">Hello 코드 toosend hello 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="bfd41-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="bfd41-121">hello emailform.jsp에서 hello 양식을 완료 하면 라고 하는 다음 코드 hello 전자 메일 메시지를 만들고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="bfd41-122">이 콘텐츠를 위해 hello JSP 파일의 이름은 **sendemail.jsp**합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

<span data-ttu-id="bfd41-123">또한 toosending hello 전자 메일 emailform.jsp 제공 hello 사용자;에 대 한 결과 예는 다음 스크린 샷에서 hello:</span><span class="sxs-lookup"><span data-stu-id="bfd41-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![메일 보내기 결과][emailresult]

## <a name="next-steps"></a><span data-ttu-id="bfd41-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfd41-125">Next steps</span></span>
<span data-ttu-id="bfd41-126">배포 응용 프로그램 toohello 계산 에뮬레이터 및 hello 형태로 emailform.jsp를 실행 하는 브라우저 내에서 값을 입력, 클릭 **이 전자 메일을 보낼**, 다음 sendemail.jsp에서 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="bfd41-127">이 코드는 tooshow 제공한 있습니다 어떻게 toouse Azure에서 Java에서 SendGrid 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="bfd41-128">프로덕션 환경에서 tooAzure를 배포 하기 전에 tooadd 자세한 오류 처리 또는 다른 기능을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="bfd41-129">예:</span><span class="sxs-lookup"><span data-stu-id="bfd41-129">For example:</span></span> 

* <span data-ttu-id="bfd41-130">Web form을 사용 하는 대신 Azure 저장소 blob 또는 SQL 데이터베이스 toostore 전자 메일 주소 및 전자 메일 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="bfd41-131">Java에서 Azure 저장소 blob을 사용 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooUse hello Java에서 Blob 저장소 서비스](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="bfd41-132">Java에서 SQL 데이터베이스 사용에 대한 내용은 [Java에서 SQL 데이터베이스 사용](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="bfd41-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="bfd41-133">사용할 수 있습니다 `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid 사용자 이름 및 암호를 사용 하는 대신 배포의 구성 설정 로부터 웹 양식 tooretrieve 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="bfd41-134">Hello에 대 한 내용은 `RoleEnvironment` 클래스를 참조 하십시오. [JSP에서 Azure 서비스 런타임 라이브러리를 사용 하 여 hello](http://msdn.microsoft.com/library/windowsazure/hh690948) 및 hello Azure 서비스 런타임 패키지 설명서에서 <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="bfd41-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="bfd41-135">Java에서 SendGrid를 사용 하는 방법에 대 한 자세한 내용은 참조 [toosend Java에서 SendGrid를 사용 하 여 전자 메일 방법](store-sendgrid-java-how-to-send-email.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd41-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
