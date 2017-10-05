---
title: "SendGrid 메일 서비스를 사용하는 방법(.NET) | Microsoft Docs"
description: "Azure에서 SendGrid 메일 서비스를 사용하여 메일을 보내는 방법을 알아봅니다. 코드 샘플은 C#으로 작성되었으며 .NET API를 사용합니다."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="941e2-104">Azure에서 SendGrid를 사용하여 전자 메일을 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="941e2-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="941e2-105">개요</span><span class="sxs-lookup"><span data-stu-id="941e2-105">Overview</span></span>
<span data-ttu-id="941e2-106">이 가이드에서는 Azure에서 SendGrid 전자 메일 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="941e2-107">샘플은 C\#으로 작성되었으며 .NET 표준 1.3을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="941e2-108">전자 메일 작성, 전자 메일 발송, 첨부 파일 추가 및 다양한 메일 및 추적 설정 사용 등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="941e2-109">SendGrid 및 전자 메일 보내기에 대한 자세한 내용은 [다음 단계][Next steps] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="941e2-110">SendGrid 전자 메일 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="941e2-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="941e2-111">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="941e2-112">일반적인 SendGrid 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="941e2-113">고객에게 영수증 또는 구매 확인을 자동으로 전송</span><span class="sxs-lookup"><span data-stu-id="941e2-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="941e2-114">고객에게 매달 전단지 및 홍보 메일을 보내는 메일 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="941e2-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="941e2-115">차단된 메일과 같은 작업에 대한 실시간 메트릭 및 고객 참여 수집</span><span class="sxs-lookup"><span data-stu-id="941e2-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="941e2-116">고객 질문 전달</span><span class="sxs-lookup"><span data-stu-id="941e2-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="941e2-117">수신 메일 처리</span><span class="sxs-lookup"><span data-stu-id="941e2-117">Processing incoming emails.</span></span>

<span data-ttu-id="941e2-118">자세한 내용은 [https://sendgrid.com](https://sendgrid.com) 또는 SendGrid의 [C# 라이브러리][sendgrid-csharp] GitHub 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="941e2-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="941e2-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="941e2-120">SendGrid.NET 클래스 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="941e2-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="941e2-121">[SendGrid NuGet 패키지](https://www.nuget.org/packages/Sendgrid) 는 SendGrid API를 가져오고 응용 프로그램에서 종속성을 모두 갖도록 구성하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="941e2-122">NuGet은 Microsoft Visual Studio 2015 이상에 포함된 Visual Studio 확장 프로그램으로서 라이브러리 및 도구를 쉽게 설치하고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="941e2-123">Visual Studio 2015보다 이전 버전의 Visual Studio를 실행 중인 경우 NuGet을 설치하려면 [http://www.nuget.org](http://www.nuget.org)로 이동하여 **Install NuGet** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="941e2-124">응용 프로그램에서 SendGrid NuGet 패키지를 설치하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="941e2-125">**새 프로젝트**를 클릭하고 **템플릿**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-125">Click on **New Project** and select a **Template**.</span></span>

   ![새 프로젝트 만들기][create-new-project]
2. <span data-ttu-id="941e2-127">**솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet 패키지][SendGrid-NuGet-package]
3. <span data-ttu-id="941e2-129">**SendGrid**를 검색하고 결과 목록에서 **SendGrid** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="941e2-130">이 문서에서 설명하는 개체 모델 및 API를 사용하려면 버전 드롭다운에서 안정적인 최신 버전의 Nuget 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![SendGrid 패키지][sendgrid-package]
5. <span data-ttu-id="941e2-132">**설치** 를 클릭하여 설치를 완료한 후 이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="941e2-133">SendGrid의 .NET 클래스 라이브러리는 **SendGrid**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="941e2-134">다음 네임스페이스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="941e2-135">**SendGrid**는 SendGrid API와 통신입니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="941e2-136">**SendGrid.Helpers.Mail**은 도우미 메서드가 전자 메일을 보내는 방법을 지정하는 SendGridMessage 개체를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="941e2-137">프로그래밍 방식으로 SendGrid 전자 메일 서비스에 액세스하려는 C# 파일의 맨 위에 다음과 같은 코드 네임스페이스 선언을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="941e2-138">방법: 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="941e2-138">How to: Create an Email</span></span>
<span data-ttu-id="941e2-139">**SendGridMessage** 개체를 사용하여 메일 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="941e2-140">일단 메시지 개체가 만들어지면 메일 보낸 사람, 메일 받는 사람, 메일 제목 및 본문을 포함하여 속성과 메서드를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="941e2-141">다음 예에서는 완전히 채워진 전자 메일 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="941e2-142">**SendGrid** 형식에서 지원하는 모든 속성 및 메서드에 대한 자세한 내용은 GitHub에서 [sendgrid-csharp][sendgrid-csharp]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="941e2-143">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="941e2-143">How to: Send an Email</span></span>
<span data-ttu-id="941e2-144">전자 메일 메시지를 만든 후에 SendGrid의 API를 사용하여 해당 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="941e2-145">또는 [.NET의 기본 제공 라이브러리][NET-library]를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="941e2-146">메일을 보내려면 SendGrid API 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="941e2-147">API 키를 구성하는 방법에 대한 세부 정보가 필요한 경우 SendGrid의 API 키 [설명서][documentation]를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="941e2-148">Azure Portal에서 응용 프로그램 설정을 클릭하고 앱 설정 아래에 키/값 쌍을 추가하여 이러한 자격 증명을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Azure 앱 설정][azure_app_settings]

 <span data-ttu-id="941e2-150">그러면 다음과 같이 자격 증명에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="941e2-151">다음 예제에서는 Web API를 사용하여 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-151">The following examples show how to send a message using the Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="941e2-152">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="941e2-152">How to: Add an attachment</span></span>
<span data-ttu-id="941e2-153">**AddAttachment** 메서드를 호출하고 최소한 첨부할 파일 이름과 Base64 인코딩 콘텐츠를 지정하여 첨부 파일을 메시지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="941e2-154">첨부할 파일마다 이 메서드를 한 번씩 호출하고 **AddAttachments** 메서드를 사용하여 여러 개의 첨부 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="941e2-155">다음 예에서는 메시지에 첨부 파일을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="941e2-156">방법: 메일 설정을 사용하여 바닥글, 추적 및 분석을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="941e2-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="941e2-157">SendGrid는 메일 설정 및 추적 설정을 사용하여 추가 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="941e2-158">클릭 추적, Google 분석, 구독 추적 등과 같은 특정 기능을 사용할 수 있도록 전자 메일 메시지에 이러한 설정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="941e2-159">앱의 전체 목록은 [설정 설명서][settings-documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="941e2-160">**SendGridMessage** 클래스의 일부로 구현되는 메서드를 사용하여 앱을 **SendGrid** 메일 메시지에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="941e2-161">다음 예에서는 바닥글 및 클릭 추적 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="941e2-162">다음 예에서는 바닥글 및 클릭 추적 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="941e2-163">바닥글 설정</span><span class="sxs-lookup"><span data-stu-id="941e2-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="941e2-164">클릭 추적</span><span class="sxs-lookup"><span data-stu-id="941e2-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="941e2-165">방법: 추가 SendGrid 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="941e2-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="941e2-166">SendGrid는 Azure 응용 프로그램 내에서 추가 기능을 활용하는 데 사용할 수 있는 여러 API 및 웹후크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="941e2-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="941e2-167">자세한 내용은 [SendGrid API 참조][SendGrid API documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941e2-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="941e2-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="941e2-168">Next steps</span></span>
<span data-ttu-id="941e2-169">SendGrid 전자 메일 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="941e2-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="941e2-170">SendGrid C\# 라이브러리 리포지토리: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="941e2-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="941e2-171">SendGrid API 설명서: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="941e2-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

<span data-ttu-id="941e2-172">[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="941e2-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="941e2-173">[트랜잭션 전자 메일 배달]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="941e2-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

