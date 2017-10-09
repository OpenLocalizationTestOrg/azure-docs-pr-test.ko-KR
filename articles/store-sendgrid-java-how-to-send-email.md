---
title: "aaaHow toouse hello SendGrid 전자 메일 서비스 (Java) | Microsoft Docs"
description: "자세한 내용은 Azure에서 SendGrid 전자 메일 서비스 hello로 전자 메일을 보내려면 어떻게 합니다. 코드 샘플은 Java로 작성되었습니다."
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
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a>어떻게 tooSend 전자 메일 Java에서 SendGrid를 사용 하 여
이 가이드에서는 tooperform 일반적인 프로그래밍 작업 SendGrid Azure에서 서비스 메일 하는 방법을 보여 줍니다. hello 샘플 Java로 작성 됩니다. hello 가이드에서 다루는 시나리오 포함 **전자 메일 구성**, **메일을 보내는**, **첨부 파일 추가**, **필터를 사용 하 여**, 및 **속성 업데이트**합니다. SendGrid 및 전자 메일에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

## <a name="what-is-hello-sendgrid-email-service"></a>Hello SendGrid 전자 메일 서비스는 무엇입니까?
SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다. 일반적인 SendGrid 사용 시나리오는 다음과 같습니다.

* 자동으로 확인 메일 toocustomers 보내기
* 월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리
* 차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집
* Toohelp 추세를 파악 하는 보고서 생성
* 고객 문의 전달
* 응용 프로그램의 전자 메일 알림

자세한 내용은 <http://sendgrid.com>(영문)을 참조하세요.

## <a name="create-a-sendgrid-account"></a>SendGrid 계정 만들기
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>방법: hello javax.mail 라이브러리 사용
예를 들어 hello javax.mail 라이브러리를 가져올 <http://www.oracle.com/technetwork/java/javamail> 코드도 가져옵니다. 상위 수준에서 hello SMTP를 사용 하 여 hello javax.mail 라이브러리 toosend 메일을 사용 하기 위한 프로세스는 toodo hello 다음:

1. 즉 SendGrid 용 smtp.sendgrid.net hello SMTP 서버를 포함 하 여 hello SMTP 값을 지정 합니다.

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

1. Hello 확장 *javax.mail.Authenticator* 클래스를 구현에서 하 고는 *getPasswordAuthentication* 메서드를 SendGrid 사용자 이름과 암호를 반환 합니다.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. *javax.mail.Session* 개체를 통해 인증된 전자 메일 세션을 만듭니다.  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. 메시지를 만들고 **받는 사람**, **보낸 사람**, **제목** 및 내용 값을 할당합니다. 이 hello에 나와 [How To: 전자 메일 만들기](#how-to-create-an-email) 섹션.
4. 통해 hello 메시지를 보내기는 *javax.mail.Transport* 개체입니다. 이 hello에 나와 [How To: 전자 메일 보내기] [하는 방법: 전자 메일 보내기] 섹션.

## <a name="how-to-create-an-email"></a>방법: 전자 메일 만들기
hello 다음 toospecify 전자 메일에 대 한 값 하는 방법을 보여 줍니다.

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

## <a name="how-to-send-an-email"></a>방법: 전자 메일 보내기
표시 방법을 따르는 hello toosend 전자 메일입니다.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>방법: 첨부 파일 추가
hello 다음 코드에서는 tooadd 첨부 합니다.

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>방법: tooenable 바닥글, 추적 및 분석을 사용 하 여 필터링
SendGrid hello 사용을 통해 추가 전자 메일 기능을 제공 *필터*합니다. 이 클릭 추적, Google 분석, 추적, 구독을 설정 하는 등 특정 기능을 사용 하도록 설정 하려면 tooan 전자 메일 메시지를 추가할 수 있는 설정 등입니다. 전체 필터 목록은 [필터 설정][Filter Settings](영문)을 참조하십시오.

* hello 다음 tooinsert 바닥글 hello hello 전자 메일이 전송 되 고 맨 아래에 나타나는 HTML 텍스트에 해당 결과 필터링 하는 방법을 보여 줍니다.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* 필터에 대한 또 다른 예제는 클릭 추적입니다. 전자 메일 텍스트에 하이퍼링크, tootrack hello 빈도 클릭 hello 다음 하려는 같은 경우를 가정해 보십시오.

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello 추적을 사용 하 여 hello 코드 다음를 클릭 합니다.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>방법: 전자 메일 속성 업데이트
사용 하 여 일부 전자 메일 속성을 덮어쓸 수  **설정*속성** *를 사용 하 여 추가 또는  **추가*속성** *입니다.

예를 들어 toospecify **ReplyTo** 주소를 사용 하 여 hello 다음:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd는 **Cc** 받는 사람을 사용 하 여 hello 다음:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>방법: 추가 SendGrid 서비스 사용
SendGrid 웹 기반 Api 제공 tooleverage 추가 SendGrid 기능을 Azure 응용 프로그램에서 사용할 수 있습니다. 전체 세부 정보에 대 한 참조 hello [SendGrid API 설명서][SendGrid API documentation]합니다.

## <a name="next-steps"></a>다음 단계
Hello SendGrid 전자 메일 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* SendGrid를 사용 하 여 Azure 배포에서를 보여 주는 샘플: [toosend 메일 Azure 배포의 Java에서 SendGrid를 사용 하는 방법](store-sendgrid-java-how-to-send-email-example.md)
* SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html>
* SendGrid API 설명서: <https://sendgrid.com/docs/API_Reference/index.html>
* Azure 고객을 위한 SendGrid 특가 제공: <https://sendgrid.com/windowsazure.html>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions
[트랜잭션 전자 메일 배달]: https://sendgrid.com/transactional-email
