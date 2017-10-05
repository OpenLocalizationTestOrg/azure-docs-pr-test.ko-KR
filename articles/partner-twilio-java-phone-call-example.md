---
title: "Twilio에서 전화를 거는 방법(Java) | Microsoft Docs"
description: "Azure의 Java 응용 프로그램에서 Twilio를 사용하여 웹 페이지에서 전화를 거는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="895eb-103">Azure의 Java 응용 프로그램에서 Twilio를 사용하여 전화를 거는 방법</span><span class="sxs-lookup"><span data-stu-id="895eb-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="895eb-104">다음 예제는 Azure에 호스트된 웹 페이지에서 Twilio를 사용하여 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="895eb-105">다음 스크린샷에 표시된 것처럼 응용 프로그램에서 사용자에게 전화 통화 값을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Twilio 및 Java를 사용하는 Azure 통화 양식][twilio_java]

<span data-ttu-id="895eb-107">이 항목에서 코드를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="895eb-108">Twilio 계정 및 인증 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="895eb-109">Twilio를 시작하려면 [http://www.twilio.com/pricing][twilio_pricing]에서 가격을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="895eb-110">에 등록할 수 있습니다 [https://www.twilio.com/try-twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="895eb-111">Twilio에서 제공 하는 API에 대 한 정보를 참조 하십시오. [http://www.twilio.com/api][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="895eb-112">Twilio JAR를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="895eb-113">[https://github.com/twilio/twilio-java][twilio_java_github]에서 GitHub 원본을 다운로드한 후 고유한 JAR을 만들거나 종속성 포함 여부에 관계없이 미리 빌드된 JAR을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="895eb-114">이 항목의 코드는 미리 빌드된 TwilioJava-3.3.8-with-dependencies JAR을 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="895eb-115">Java 빌드 경로에 JAR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="895eb-116">Eclipse를 사용하여 이 Java 응용 프로그램을 만드는 경우, Eclipse의 배포 어셈블리 기능을 사용하여 응용 프로그램 배포 파일(WAR)에 Twilio JAR을 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="895eb-117">Eclipse를 사용하지 않고 이 Java 응용 프로그램을 만드는 경우, 같은 Azure 역할 내에 Twilio JAR이 Java 응용 프로그램으로 포함되어 있으며 응용 프로그램의 클래스 경로에 추가되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="895eb-118">cacerts keystore에 MD5 지문이 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4인 Equifax Secure Certificate Authority 인증서가 포함되어 있는지 확인합니다(일련 번호는 35:DE:F4:CF이고 SHA1 지문은 D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A임).</span><span class="sxs-lookup"><span data-stu-id="895eb-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="895eb-119">이 인증서는 Twilio API를 사용할 때 호출되는 [https://api.twilio.com][twilio_api_service] 서비스에 대한 CA(인증 기관) 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="895eb-120">이 CA 인증서를 JDK의 cacert 저장소에 추가 하는 방법에 대 한 정보를 참조 하십시오. [Java CA 인증서 저장소에 인증서 추가][add_ca_cert]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="895eb-121">또한 경험에 대 한 정보를 [Eclipse 용 Azure 도구 키트는 Hello World 응용 프로그램 사용 하 여 만드는][azure_java_eclipse_hello_world], 나는 경우 Azure에서 Java 응용 프로그램을 호스트 하는 것에 대 한 다른 기술로 Eclipse를 사용 하지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="895eb-122">전화 걸기 웹 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="895eb-122">Create a web form for making a call</span></span>
<span data-ttu-id="895eb-123">다음 코드는 전화를 걸기 위해 웹 양식을 만들고 사용자 데이터를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="895eb-124">이 예제에서는 **TwilioCloud**라는 새 동적 웹 프로젝트가 생성되고 **callform.jsp**가 JSP 파일로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
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

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="895eb-125">코드를 만들어 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="895eb-125">Create the code to make the call</span></span>
<span data-ttu-id="895eb-126">사용자가 callform.jsp에 의해 표시되는 양식을 다 작성하면 호출되는 다음 코드는 통화 메시지를 만들고 통화를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="895eb-127">이 예제에서는 JSP 파일이 **makecall.jsp**로 이름이 지정되고 **TwilioCloud** 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="895eb-128">(아래 코드에서 **accountSID** 및 **authToken**에 할당된 자리 표시자 값 대신 Twilio 계정 및 인증 토큰을 사용하십시오.)</span><span class="sxs-lookup"><span data-stu-id="895eb-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

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
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
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

<span data-ttu-id="895eb-129">전화 걸기와 함께, makecall.jsp는 Twilio 끝점, API 버전 및 통화 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="895eb-130">다음 스크린샷에 예가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-130">An example is the following screen shot:</span></span>

![Twilio 및 Java를 사용하는 Azure 통화 응답][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="895eb-132">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="895eb-132">Run the application</span></span>
<span data-ttu-id="895eb-133">다음은; 응용 프로그램을 실행 하는 개략적인 단계 다음이 단계를 찾을 수 있습니다 세부 [Eclipse 용 Azure 도구 키트는 Hello World 응용 프로그램 사용 하 여 만드는][azure_java_eclipse_hello_world]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="895eb-134">TwilioCloud WAR을 Azure **approot** 폴더로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="895eb-135">**startup.cmd** 를 수정하여 TwilioCloud WAR의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="895eb-136">계산 에뮬레이터에 대해 응용 프로그램을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="895eb-137">계산 에뮬레이터에서 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="895eb-138">브라우저를 열고 **http://localhost:8080/TwilioCloud/callform.jsp**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="895eb-139">양식에 값을 입력하고 **Make this call**을 클릭한 다음 makecall.jsp의 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="895eb-140">Azure에 배포할 준비가 되면 클라우드에 배포에 대해 다시 컴파일하고 Azure에 배포한 다음 브라우저에서 http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp를 실행합니다(*your_hosted_name*의 값 대체).</span><span class="sxs-lookup"><span data-stu-id="895eb-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="895eb-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="895eb-141">Next steps</span></span>
<span data-ttu-id="895eb-142">이 코드는 Azure의 Java에서 Twilio를 사용하는 기본 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="895eb-143">Azure를 프로덕션에 배포하기 전에 더 많은 오류 처리 또는 기타 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="895eb-144">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-144">For example:</span></span>

* <span data-ttu-id="895eb-145">웹 양식을 사용하는 대신, Azure 저장소 Blob 또는 SQL 데이터베이스를 사용하여 전화 번호 및 통화 텍스트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="895eb-146">Java에서 Azure 저장소 blob을 사용 하는 방법에 대 한 정보를 참조 하십시오. [Java에서 Blob 저장소 서비스를 사용 하는 방법을][howto_blob_storage_java]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="895eb-147">Java에서 SQL 데이터베이스를 사용 하는 방법에 대 한 정보를 참조 하십시오. [Java에서 SQL 데이터베이스를 사용 하 여][howto_sql_azure_java]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="895eb-148">makecall.jsp에서 값을 하드 코딩하는 대신, **RoleEnvironment.getConfigurationSettings** 를 사용하여 배포 구성 설정에서 Twilio 계정 ID 및 인증 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="895eb-149">에 대 한 내용은 **RoleEnvironment** 클래스를 참조 하십시오. [JSP에서 Azure 서비스 런타임 라이브러리를 사용 하 여] [ azure_runtime_jsp] 및 에Azure서비스런타임패키지설명서[http://dl.windowsazure.com/javadoc][azure_javadoc]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="895eb-150">Makecall.jsp 코드 Twilio 제공 URL 할당 [http://twimlets.com/message][twimlet_message_url]을 **Url** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="895eb-151">이 URL은 Twilio에 통화를 진행하는 방법을 알리는 TwiML(Twilio Markup Language) 응답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="895eb-152">예를 들어, 반환되는 TwiML에는 통화 수신자에게 말하는 텍스트에 나타나는 **&lt;Say&gt;** 동사가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="895eb-153">Twilio 제공 URL을 사용 하는 대신 Twilio의 요청에 응답 하도록 사용자 고유의 서비스를 작성할 수 있습니다. 자세한 내용은 참조 [음성 및 SMS 기능 Java에서 사용 하 여 Twilio 하는 방법을][howto_twilio_voice_sms_java]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="895eb-154">TwiML에 대 한 자세한 정보를 찾을 수 있습니다 [http://www.twilio.com/docs/api/twiml][twiml], 및에 대 한 자세한 내용은  **&lt;의견을 언급 해서도&gt;**  및 다른 Twilio 동사를 찾을 수 있습니다 [http://www.twilio.com/docs/api/twiml/say][twilio_say]합니다.</span><span class="sxs-lookup"><span data-stu-id="895eb-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="895eb-155">[https://www.twilio.com/docs/security][twilio_docs_security]에서 Twilio 보안 지침을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="895eb-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="895eb-156">Twilio에 대한 자세한 내용은 [https://www.twilio.com/docs][twilio_docs]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="895eb-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="895eb-157">참고 항목</span><span class="sxs-lookup"><span data-stu-id="895eb-157">See Also</span></span>
* <span data-ttu-id="895eb-158">[음성 및 SMS 기능 Java에서 위해 Twilio를 사용 하는 방법][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="895eb-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="895eb-159">[Java CA 인증서 저장소에 인증서 추가][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="895eb-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

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
