---
title: "SendGrid 메일 서비스를 사용하는 방법(Node.js) | Microsoft Docs"
description: "Azure에서 SendGrid 메일 서비스를 사용하여 메일을 보내는 방법을 알아봅니다. 코드 샘플은 Node.js API를 사용하여 작성되었습니다."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="d1529-104">Node.js에서 SendGrid를 사용하여 메일을 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="d1529-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="d1529-105">이 가이드에서는 Azure에서 SendGrid 전자 메일 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="d1529-106">샘플은 Node.js API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="d1529-107">**전자 메일 생성**, **전자 메일 보내기**, **첨부 파일 추가**, **필터 사용**, **속성 업데이트** 등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="d1529-108">SendGrid 및 전자 메일 보내기에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1529-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="d1529-109">SendGrid 전자 메일 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="d1529-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="d1529-110">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 발송], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="d1529-111">일반적인 SendGrid 사용 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="d1529-112">고객에게 확인 메일 자동으로 보내기</span><span class="sxs-lookup"><span data-stu-id="d1529-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="d1529-113">월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리</span><span class="sxs-lookup"><span data-stu-id="d1529-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="d1529-114">차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="d1529-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="d1529-115">경향을 식별하는 데 도움이 되도록 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="d1529-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="d1529-116">고객 문의 전달</span><span class="sxs-lookup"><span data-stu-id="d1529-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="d1529-117">응용 프로그램의 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="d1529-117">Email notifications from your application</span></span>

<span data-ttu-id="d1529-118">자세한 내용은 [https://sendgrid.com](https://sendgrid.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1529-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="d1529-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d1529-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="d1529-120">SendGrid Node.js 모듈 참조</span><span class="sxs-lookup"><span data-stu-id="d1529-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="d1529-121">Node.js용 SendGrid 모듈은 다음 명령을 사용하여 NPM(Node Package Manager)을 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="d1529-122">설치 후에는 다음 코드를 사용하여 응용 프로그램에서 이 모듈을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="d1529-123">SendGrid 모듈은 **SendGrid** 및 **Email** 함수를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="d1529-124">**SendGrid**는 Web API를 통해 전자 메일을 보내는 역할을 맡고, **Email**은 전자 메일 메시지를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="d1529-125">방법: 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="d1529-125">How to: Create an Email</span></span>
<span data-ttu-id="d1529-126">SendGrid 모듈을 사용하여 전자 메일 메시지를 만들려면 먼저 Email 함수로 전자 메일 메시지를 만든 후, SendGrid 함수를 사용하여 이 메시지를 보내면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="d1529-127">다음 예제는 Email 함수를 사용하여 새 메시지를 만드는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="d1529-128">또한 html 속성을 설정하여 HTML 메시지를 지원하는 클라이언트를 위해 HTML 메시지를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="d1529-129">예:</span><span class="sxs-lookup"><span data-stu-id="d1529-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="d1529-130">텍스트 속성과 html 속성을 모두 설정하면 HTML 메시지를 지원할 수 없는 클라이언트에서 텍스트 콘텐츠로 안정적으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="d1529-131">전자 메일 함수에서 지 원하는 모든 속성에 대 한 자세한 내용은 참조 하십시오. [sendgrid nodejs][sendgrid-nodejs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="d1529-132">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="d1529-132">How to: Send an Email</span></span>
<span data-ttu-id="d1529-133">Email 함수를 사용하여 전자 메일 메시지를 만든 후에는 SendGrid에서 제공하는 Web API를 사용하여 해당 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="d1529-134">Web API</span><span class="sxs-lookup"><span data-stu-id="d1529-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="d1529-135">위 예제에서는 email 개체 및 콜백 함수를 전달하고 있지만, email 속성을 직접 지정하여 send 함수를 바로 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="d1529-136">예:</span><span class="sxs-lookup"><span data-stu-id="d1529-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="d1529-137">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="d1529-137">How to: Add an Attachment</span></span>
<span data-ttu-id="d1529-138">**files** 속성에서 파일 이름 및 경로를 지정하여 메시지에 첨부 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="d1529-139">다음 예제에서는 첨부 파일을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="d1529-140">**files** 속성을 사용할 경우, 해당 파일은 [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile)을 통해 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="d1529-141">첨부하려는 파일이 Blob 컨테이너 등의 Azure Storage에서 호스트되는 경우, 먼저 파일을 로컬 저장소 또는 Azure 드라이브에 복사해야 **files** 속성을 사용하여 해당 파일을 첨부 파일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="d1529-142">방법: 필터를 사용하여 바닥글 및 추적을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d1529-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="d1529-143">SendGrid는 필터 사용을 통해 추가 전자 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="d1529-144">클릭 추적, Google 분석, 구독 추적 등을 사용하도록 설정하는 것과 같이 특정 기능을 사용하도록 설정하기 위해 전자 메일 메시지에 추가할 수 있는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="d1529-145">전체 필터 목록은 [필터 설정][Filter Settings](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1529-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="d1529-146">필터는 **filters** 속성을 사용하여 메시지에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="d1529-147">각 필터는 필터별 설정을 포함하는 해시에 의해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="d1529-148">다음 예에서는 바닥글 및 클릭 추적 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="d1529-149">바닥글</span><span class="sxs-lookup"><span data-stu-id="d1529-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="d1529-150">클릭 추적</span><span class="sxs-lookup"><span data-stu-id="d1529-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="d1529-151">방법: 전자 메일 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="d1529-151">How to: Update Email Properties</span></span>
<span data-ttu-id="d1529-152">사용 하 여 일부 전자 메일 속성을 덮어쓸 수  **설정*속성** *를 사용 하 여 추가 또는  **추가*속성** *입니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="d1529-153">예를 들어 다음을 사용하여 받는 사람을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="d1529-154">또는 다음을 사용하여 필터를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="d1529-155">자세한 내용은 참조 [sendgrid nodejs][sendgrid-nodejs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="d1529-156">방법: 추가 SendGrid 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="d1529-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="d1529-157">SendGrid는 Azure 응용 프로그램에서 추가 SendGrid 기능을 활용하는 데 사용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1529-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="d1529-158">자세한 내용은 [SendGrid API 설명서][SendGrid API documentation](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1529-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1529-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1529-159">Next Steps</span></span>
<span data-ttu-id="d1529-160">SendGrid 전자 메일 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="d1529-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="d1529-161">SendGrid Node.js 모듈 리포지토리: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="d1529-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="d1529-162">SendGrid API 설명서: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="d1529-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="d1529-163">Azure 고객을 위한 SendGrid 특가 제공: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="d1529-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
<span data-ttu-id="d1529-164">[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="d1529-164">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="d1529-165">[트랜잭션 전자 메일 발송]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="d1529-165">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
