---
title: "aaaHow toouse hello SendGrid 전자 메일 서비스 (.NET) | Microsoft Docs"
description: "자세한 내용은 Azure에서 SendGrid 전자 메일 서비스 hello로 전자 메일을 보내려면 어떻게 합니다. C# 및 사용 하 여 hello.NET API로 작성 된 코드 샘플입니다."
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
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="34f51-104">어떻게 tooSend Azure와 함께 사용 하 여 SendGrid 전자 메일</span><span class="sxs-lookup"><span data-stu-id="34f51-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="34f51-105">개요</span><span class="sxs-lookup"><span data-stu-id="34f51-105">Overview</span></span>
<span data-ttu-id="34f51-106">이 가이드에서는 tooperform 일반적인 프로그래밍 작업 SendGrid Azure에서 서비스 메일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="34f51-107">hello 샘플은 C로 작성 된\# .NET 표준 1.3을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="34f51-108">가이드에서 다루는 hello 시나리오에는 전자 메일을 구성, 전자 메일을 보내기, 첨부 파일을 추가 하 고 다양 한 메일 활성화 및 추적 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="34f51-109">SendGrid 및 전자 메일에 대 한 자세한 내용은 참조 hello [다음 단계] [ Next steps] 섹션.</span><span class="sxs-lookup"><span data-stu-id="34f51-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="34f51-110">Hello SendGrid 전자 메일 서비스는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="34f51-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="34f51-111">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="34f51-112">일반적인 SendGrid 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="34f51-113">수신 확인 또는 구매 확인 toocustomers 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="34f51-114">고객에게 매달 전단지 및 홍보 메일을 보내는 메일 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="34f51-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="34f51-115">차단된 메일과 같은 작업에 대한 실시간 메트릭 및 고객 참여 수집</span><span class="sxs-lookup"><span data-stu-id="34f51-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="34f51-116">고객 질문 전달</span><span class="sxs-lookup"><span data-stu-id="34f51-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="34f51-117">수신 메일 처리</span><span class="sxs-lookup"><span data-stu-id="34f51-117">Processing incoming emails.</span></span>

<span data-ttu-id="34f51-118">자세한 내용은 [https://sendgrid.com](https://sendgrid.com) 또는 SendGrid의 [C# 라이브러리][sendgrid-csharp] GitHub 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="34f51-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="34f51-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="34f51-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="34f51-120">Hello SendGrid.NET 클래스 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="34f51-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="34f51-121">hello [SendGrid NuGet 패키지](https://www.nuget.org/packages/Sendgrid) hello 가장 쉬운 방법은 tooget hello SendGrid API 및 tooconfigure 모든 종속성이 있는 응용 프로그램은 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="34f51-122">NuGet은 Visual Studio 확장 발견 된 Microsoft Visual Studio 2015와 함께 그 이상 사용 하면 쉽게 tooinstall 및 update 라이브러리 및 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="34f51-123">tooinstall NuGet Visual Studio 2015 이전 버전의 Visual Studio를 실행 하는 경우 방문 [http://www.nuget.org](http://www.nuget.org), hello를 클릭 하 고 **NuGet 설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="34f51-124">tooinstall hello 응용 프로그램에서 SendGrid NuGet 패키지는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="34f51-125">**새 프로젝트**를 클릭하고 **템플릿**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-125">Click on **New Project** and select a **Template**.</span></span>

   ![새 프로젝트 만들기][create-new-project]
2. <span data-ttu-id="34f51-127">**솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet 패키지][SendGrid-NuGet-package]
3. <span data-ttu-id="34f51-129">검색할 **SendGrid** 및 선택 hello **SendGrid** 결과 목록에서 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="34f51-130">Hello 버전 드롭다운 toobe 수 toowork hello 개체 모델 및이 문서에서 설명 하는 Api와에서 hello 안정적인 최신 버전의 hello Nuget 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![SendGrid 패키지][sendgrid-package]
5. <span data-ttu-id="34f51-132">클릭 **설치** toocomplete hello 설치를 한 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="34f51-133">SendGrid의 .NET 클래스 라이브러리는 **SendGrid**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="34f51-134">다음 네임 스페이스 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="34f51-135">**SendGrid**는 SendGrid API와 통신입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="34f51-136">**SendGrid.Helpers.Mail** 도우미에 대 한 메서드 tooeasily SendGridMessage는 개체를 만들어 toosend 메일이 전송 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="34f51-137">코드 네임 스페이스 선언을 toohello 위쪽 tooprogrammatically 액세스 hello SendGrid 전자 메일 서비스를 원하는 경우는 C# 파일의 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="34f51-138">방법: 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="34f51-138">How to: Create an Email</span></span>
<span data-ttu-id="34f51-139">사용 하 여 hello **SendGridMessage** toocreate 전자 메일 메시지 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="34f51-140">Hello 메시지 개체를 만든 후에 속성과 메서드를 hello 전자 메일 보낸 사람, hello 전자 메일 받는 사람 및 hello 제목과 hello 전자 메일의 본문을 포함 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="34f51-141">hello 다음 예제에서는 어떻게 toocreate 완전히 채워진된 전자 메일 개체:</span><span class="sxs-lookup"><span data-stu-id="34f51-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="34f51-142">**SendGrid** 형식에서 지원하는 모든 속성 및 메서드에 대한 자세한 내용은 GitHub에서 [sendgrid-csharp][sendgrid-csharp]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34f51-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="34f51-143">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="34f51-143">How to: Send an Email</span></span>
<span data-ttu-id="34f51-144">전자 메일 메시지를 만든 후에 SendGrid의 API를 사용하여 해당 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="34f51-145">또는 [.NET의 기본 제공 라이브러리][NET-library]를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="34f51-146">메일을 보내려면 SendGrid API 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="34f51-147">방법에 대 한 세부 정보를 해야 할 경우 tooconfigure API 키를 방문 하세요. SendGrid의 API 키 [설명서][documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="34f51-148">클릭 하 여 응용 프로그램 설정 및 응용 프로그램 설정에서 hello 키/값 쌍을 추가 하 여 Azure 포털을 통해 이러한 자격 증명을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Azure 앱 설정][azure_app_settings]

 <span data-ttu-id="34f51-150">그러면 다음과 같이 자격 증명에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="34f51-151">다음 예제는 hello 방법을 사용 하 여 메시지 toosend hello 웹 API를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-151">hello following examples show how toosend a message using hello Web API.</span></span>

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
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="34f51-152">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="34f51-152">How to: Add an attachment</span></span>
<span data-ttu-id="34f51-153">첨부 파일 호출 hello 여 tooa 메시지 추가할 수 있습니다 **AddAttachment** 원하는 tooattach 메서드 및 최소 hello 파일 이름 및 Base64 인코딩 콘텐츠를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="34f51-154">원하는 tooattach 각 파일에 대 한 면이 메서드를 호출 하 여 또는 hello를 사용 하 여 여러 첨부 파일을 포함할 수 있습니다 **AddAttachments** 메서드.</span><span class="sxs-lookup"><span data-stu-id="34f51-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="34f51-155">다음 예제는 hello 첨부 tooa 메시지를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="34f51-156">방법: 메일 설정 tooenable 바닥글, 추적 및 분석을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34f51-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="34f51-157">SendGrid 메일 설정 및 추적 설정을 hello 사용을 통해 추가 전자 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="34f51-158">이러한 설정은 tooan 전자 메일 메시지 tooenable 특정 기능 클릭 추적, Google 분석, 추적, 구독 등을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="34f51-159">앱의 전체 목록을 참조 hello [설정을 설명서][settings-documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="34f51-160">앱을 너무 적용 될 수 있습니다.**SendGrid** hello의 일부로 구현 된 메서드를 사용 하 여 메시지를 전자 메일로 보내기 **SendGridMessage** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="34f51-161">hello 다음 예제 hello 바닥글을 보여 주고 추적 필터를 클릭:</span><span class="sxs-lookup"><span data-stu-id="34f51-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="34f51-162">hello 다음 예제 hello 바닥글을 보여 주고 추적 필터를 클릭:</span><span class="sxs-lookup"><span data-stu-id="34f51-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="34f51-163">바닥글 설정</span><span class="sxs-lookup"><span data-stu-id="34f51-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="34f51-164">클릭 추적</span><span class="sxs-lookup"><span data-stu-id="34f51-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="34f51-165">방법: 추가 SendGrid 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="34f51-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="34f51-166">SendGrid는 몇 가지 Api 및 Azure 응용 프로그램 내에서 tooleverage 추가 기능을 사용할 수 있는 webhook을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="34f51-167">자세한 내용은 참조 hello [SendGrid API 참조][SendGrid API documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="34f51-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34f51-168">Next steps</span></span>
<span data-ttu-id="34f51-169">Hello SendGrid 전자 메일 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f51-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="34f51-170">SendGrid C\# 라이브러리 리포지토리: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="34f51-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="34f51-171">SendGrid API 설명서: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="34f51-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
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

[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/solutions
[트랜잭션 전자 메일 배달]: https://sendgrid.com/use-cases/transactional-email

