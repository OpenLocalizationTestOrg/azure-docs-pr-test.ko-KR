---
title: "Twilio (Java)의 통화 aaaHow tooMake | Microsoft Docs"
description: "휴대폰 toomake Twilio를 사용 하 여 Azure에서 Java 응용 프로그램에서 웹 페이지에서 호출 하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>어떻게 tooMake Azure에서 Java 응용 프로그램에서 전화 통화를 사용 하 여 Twilio
hello 다음 예제에 나와 사용 하는 방법을 Twilio toomake Azure에서 호스팅되는 웹 페이지 코드에서 호출 합니다. hello 다음 스크린 샷에서 같이 hello 결과 응용 프로그램에 전화 통화 값에 대 한 hello 사용자 라는 메시지가 나타납니다.

![Twilio 및 Java를 사용하는 Azure 통화 양식][twilio_java]

Toodo hello 다음 해야이 항목의 toouse hello 코드:

1. Twilio 계정 및 인증 토큰을 받습니다. Twilio, 시작 tooget 평가에서 가격 책정 [http://www.twilio.com/pricing][twilio_pricing]합니다. 에 등록할 수 있습니다 [https://www.twilio.com/try-twilio][try_twilio]합니다. Hello Twilio에서 제공 하는 API에 대 한 정보를 참조 하십시오. [http://www.twilio.com/api][twilio_api]합니다.
2. Twilio JAR hello를 가져옵니다. [https://github.com/twilio/twilio-java][twilio_java_github], hello GitHub 소스를 다운로드 하 고 사용자 고유의 JAR 작성 하거나 (종속성이 없는 또는) 미리 작성 된 JAR 다운로드 수 있습니다.
   이 항목의 hello 코드 종속성으로 TwilioJava 3.3.8 JAR 미리 만들어진 hello를 사용 하 여 작성 되었습니다.
3. Hello JAR tooyour Java 빌드 경로 추가 합니다.
4. Eclipse toocreate이 Java 응용 프로그램을 사용할 경우 Eclipse의 배포 어셈블리 기능을 사용 하 여 응용 프로그램 배포 파일 (WAR)에 Twilio JAR hello를 포함 합니다. 이 Java 응용 프로그램 Eclipse toocreate을 사용 하지 않는 경우 확인 Twilio JAR hello hello 내에 포함 된 응용 프로그램의 Java 응용 프로그램에서는, 및 추가 된 toohello 클래스 경로와 동일한 Azure 역할을 합니다.
5. MD5 지문 67:CB:9 D와 hello Equifax 보안 인증 기관 인증서를 포함 하는 cacerts keystore 확인: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello 번호 35:DE:F4:CF 이며 hello SHA1 지문 D2:32:09:AD:23:D 직렬 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). 이 hello에 대 한 인증 기관 (CA) 인증서 hello [https://api.twilio.com] [ twilio_api_service] Twilio Api를 사용 하는 경우 호출 되는 서비스입니다. 이 CA 인증서 tooyour JDK의 cacert 저장소를 추가 하는 방법에 대 한 정보를 참조 하십시오. [Java CA 인증서 저장소 인증서 toohello 추가][add_ca_cert]합니다.

Hello에 대 한 정보를 익히는 또한 [Eclipse 용 Azure 도구 키트를 사용 하 여 Hello World 응용 프로그램 hello 만드는][azure_java_eclipse_hello_world], 또는 Azure에서 Java 응용 프로그램을 호스트 하는 것에 대 한 다른 기술로 있습니다 Eclipse를 사용 하지 않는, 것이 좋습니다.

## <a name="create-a-web-form-for-making-a-call"></a>전화 걸기 웹 양식 만들기
코드 다음 hello toocreate 웹 전화 걸기 tooretrieve 사용자 데이터를 형성 하는 방법을 보여 줍니다. 이 예제에서는 **TwilioCloud**라는 새 동적 웹 프로젝트가 생성되고 **callform.jsp**가 JSP 파일로 추가되었습니다.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Hello 코드 toomake hello 호출 만들기
hello hello 사용자 callform.jsp 하 여 표시 된 hello 폼 완료 되 면 라고 하는 다음 코드 hello 호출 메시지를 만들고 hello 호출을 생성 합니다. 이 예제에 대 한 hello JSP 파일의 이름은 **makecall.jsp** 있어서 toohello 추가 **TwilioCloud** 프로젝트. (너무 할당 hello 자리 표시자 값 대신 Twilio 계정 및 인증 토큰을 사용 하 여**accountSID** 및 **authToken** hello 코드 아래에 있습니다.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

또한 toomaking hello 호출, makecall.jsp hello Twilio 끝점, API 버전 및 hello 호출 상태를 표시 합니다. 예는 다음 스크린 샷에서 hello:

![Twilio 및 Java를 사용하는 Azure 통화 응답][twilio_java_response]

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
다음과 같은 개략적인 단계 toorun; 응용 프로그램 hello 됩니다. 다음이 단계를 찾을 수 있습니다에 대 한 세부 정보 [Eclipse 용 Azure 도구 키트를 사용 하 여 Hello World 응용 프로그램 hello 만드는][azure_java_eclipse_hello_world]합니다.

1. 프로그램 TwilioCloud WAR toohello Azure 내보내기 **approot** 폴더입니다. 
2. 수정 **startup.cmd** toounzip TwilioCloud WAR 합니다.
3. Hello 계산 에뮬레이터에 대 한 응용을 프로그램을 컴파일하십시오.
4. Hello 계산 에뮬레이터에서 배포를 시작 합니다.
5. 브라우저를 열고 **http://localhost:8080/TwilioCloud/callform.jsp**를 실행합니다.
6. Hello 형식으로 값을 입력, 클릭 **이 메서드를 호출**, 다음 makecall.jsp hello 결과 표시 합니다.

준비 toodeploy tooAzure 러 우면 toohello 클라우드 배포에 대 한 다시 컴파일해야, tooAzure, 배포 하 고 http:// 실행*your_hosted_name*hello 브라우저에서.cloudapp.net/TwilioCloud/callform.jsp ( 에대한값으로대체*your_hosted_name*).

## <a name="next-steps"></a>다음 단계
이 코드는 tooshow 제공한 하면 기본 기능을 Java Twilio를 사용 하 여 Azure에서. 프로덕션 환경에서 tooAzure를 배포 하기 전에 tooadd 자세한 오류 처리 또는 다른 기능을 할 수 있습니다. 예:

* Web form을 사용 하는 대신 Azure 저장소 blob 나 SQL 데이터베이스 toostore 전화 번호를 사용 하 고 텍스트를 호출할 수 있습니다. Java에서 Azure 저장소 blob을 사용 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooUse hello Java에서 Blob 저장소 서비스][howto_blob_storage_java]합니다. Java에서 SQL 데이터베이스를 사용 하는 방법에 대 한 정보를 참조 하십시오. [Java에서 SQL 데이터베이스를 사용 하 여][howto_sql_azure_java]합니다.
* 사용할 수 있습니다 **RoleEnvironment.getConfigurationSettings** makecall.jsp에서 하드 코딩 hello 값이 아닌 배포의 구성 설정에서 tooretrieve hello Twilio 계정 ID 및 인증 토큰입니다. Hello에 대 한 내용은 **RoleEnvironment** 클래스를 참조 하십시오. [JSP에서 Azure 서비스 런타임 라이브러리를 사용 하 여 hello] [ azure_runtime_jsp] 및 hello Azure 서비스 런타임 패키지 설명서에서 [http://dl.windowsazure.com/javadoc][azure_javadoc]합니다.
* Twilio 제공 URL을 할당 하는 hello makecall.jsp 코드 [http://twimlets.com/message][twimlet_message_url], toohello **Url** 변수입니다. 이 URL Twilio tooproceed hello로 호출 하는 방법을 알려 주는 Twilio Markup Language (TwiML) 응답을 제공 합니다. 예를 들어 hello TwiML 반환 되는 포함 될 수 있습니다는  **&lt;의견을 언급 해서도&gt;**  텍스트 음성된 toohello 호출 받는 사람 중에 발생 하는 동사입니다. Hello Twilio 제공 URL을 사용 하는 대신 사용자 고유의 서비스 toorespond tooTwilio 요청을 작성할 수 있습니다. 자세한 내용은 참조 [어떻게 tooUse 음성 및 SMS 기능 java에서 Twilio][howto_twilio_voice_sms_java]합니다. TwiML에 대 한 자세한 정보를 찾을 수 있습니다 [http://www.twilio.com/docs/api/twiml][twiml], 및에 대 한 자세한 내용은  **&lt;의견을 언급 해서도&gt;**  및 다른 Twilio 동사를 찾을 수 있습니다 [http://www.twilio.com/docs/api/twiml/say][twilio_say]합니다.
* hello Twilio 보안 지침을 읽고 [https://www.twilio.com/docs/security][twilio_docs_security]합니다.

Twilio에 대한 자세한 내용은 [https://www.twilio.com/docs][twilio_docs]를 참조하세요.

## <a name="see-also"></a>참고 항목
* [어떻게 tooUse 음성 및 SMS 기능 java에서 Twilio][howto_twilio_voice_sms_java]
* [인증서 toohello Java CA 인증서 저장소를 추가합니다.][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
