---
title: "aaaHow toouse hello SendGrid 전자 메일 서비스 (Node.js) | Microsoft Docs"
description: "자세한 내용은 Azure에서 SendGrid 전자 메일 서비스 hello로 전자 메일을 보내려면 어떻게 합니다. 코드 샘플 hello Node.js API를 사용 하 여 작성 합니다."
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
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="d2e00-104">어떻게 tooSend Node.js에서 사용 하 여 SendGrid 전자 메일</span><span class="sxs-lookup"><span data-stu-id="d2e00-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="d2e00-105">이 가이드에서는 tooperform 일반적인 프로그래밍 작업 SendGrid Azure에서 서비스 메일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="d2e00-106">hello 샘플 hello Node.js API를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="d2e00-107">hello 가이드에서 다루는 시나리오 포함 **전자 메일 구성**, **메일을 보내는**, **첨부 파일 추가**, **필터를 사용 하 여**, 및 **속성 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="d2e00-108">SendGrid 및 전자 메일에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="d2e00-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="d2e00-109">Hello SendGrid 전자 메일 서비스는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d2e00-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="d2e00-110">SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="d2e00-111">일반적인 SendGrid 사용 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="d2e00-112">자동으로 확인 메일 toocustomers 보내기</span><span class="sxs-lookup"><span data-stu-id="d2e00-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="d2e00-113">월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리</span><span class="sxs-lookup"><span data-stu-id="d2e00-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="d2e00-114">차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="d2e00-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="d2e00-115">Toohelp 추세를 파악 하는 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="d2e00-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="d2e00-116">고객 문의 전달</span><span class="sxs-lookup"><span data-stu-id="d2e00-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="d2e00-117">응용 프로그램의 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="d2e00-117">Email notifications from your application</span></span>

<span data-ttu-id="d2e00-118">자세한 내용은 [https://sendgrid.com](https://sendgrid.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2e00-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="d2e00-119">SendGrid 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d2e00-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="d2e00-120">참조 hello SendGrid Node.js 모듈</span><span class="sxs-lookup"><span data-stu-id="d2e00-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="d2e00-121">Node.js 용 hello SendGrid 모듈 hello 다음 명령을 사용 하 여 hello 노드 패키지 관리자 (npm)를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="d2e00-122">설치 후 코드 다음 hello를 사용 하 여 응용 프로그램에서 hello 모듈을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="d2e00-123">hello SendGrid 모듈이 내보내는 hello **SendGrid** 및 **전자 메일** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="d2e00-124">**SendGrid**는 Web API를 통해 전자 메일을 보내는 역할을 맡고, **Email**은 전자 메일 메시지를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="d2e00-125">방법: 전자 메일 만들기</span><span class="sxs-lookup"><span data-stu-id="d2e00-125">How to: Create an Email</span></span>
<span data-ttu-id="d2e00-126">Hello SendGrid 모듈을 사용 하 여 전자 메일 메시지를 만들면 먼저 hello 전자 메일 함수를 사용 하 고 다음 hello SendGrid 함수를 사용 하 여 보내는 전자 메일 메시지를 만드는 과정이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="d2e00-127">hello 다음은 hello 전자 메일 함수를 사용 하 여 새 메시지를 만드는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="d2e00-128">클라이언트 hello html 속성을 설정 하 여 지원에 대 한 HTML 메시지를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="d2e00-129">예:</span><span class="sxs-lookup"><span data-stu-id="d2e00-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="d2e00-130">Hello 텍스트 및 html 속성이 모두 설정 HTML 메시지를 지원할 수 없는 클라이언트에 대 한 정상적인 대체 텍스트 콘텐츠를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="d2e00-131">Hello 전자 메일 함수에서 지 원하는 모든 속성에 대 한 자세한 내용은 참조 하십시오. [sendgrid nodejs][sendgrid-nodejs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="d2e00-132">방법: 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="d2e00-132">How to: Send an Email</span></span>
<span data-ttu-id="d2e00-133">전자 메일 함수 hello를 사용 하 여 전자 메일 메시지를 만든 후 hello SendGrid에서 제공 하는 웹 API를 사용 하 여 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="d2e00-134">Web API</span><span class="sxs-lookup"><span data-stu-id="d2e00-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="d2e00-135">위의 예제는 hello 표시 메일 개체와 콜백 함수에 전달 하는 동안에 직접 직접 전자 메일 속성을 지정 하 여 hello 보내기 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="d2e00-136">예:</span><span class="sxs-lookup"><span data-stu-id="d2e00-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="d2e00-137">방법: 첨부 파일 추가</span><span class="sxs-lookup"><span data-stu-id="d2e00-137">How to: Add an Attachment</span></span>
<span data-ttu-id="d2e00-138">첨부 파일 hello에 hello 파일 이름 및 경로 지정 하 여 tooa 메시지 추가할 수 있습니다 **파일** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="d2e00-139">다음 예제는 hello 첨부 파일을 전송 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="d2e00-140">Hello를 사용 하는 경우 **파일** 속성 hello 파일을 통해 액세스할 수 있어야 [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="d2e00-141">Blob 컨테이너와 같이 Azure 저장소에 tooattach hello 파일이 호스트 되는 경우 먼저 복사 해야 hello 파일 toolocal 저장소 또는 Azure 드라이브 tooan hello를 사용 하 여 첨부 파일로 보내기 전에 **파일** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="d2e00-142">방법: 추적 및 tooEnable 바닥글에는 필터를 사용 하</span><span class="sxs-lookup"><span data-stu-id="d2e00-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="d2e00-143">SendGrid는 hello 필터 사용을 통해 추가 전자 메일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="d2e00-144">이 클릭 추적, Google 분석, 추적, 구독을 설정 하는 등 특정 기능을 사용 하도록 설정 하려면 tooan 전자 메일 메시지를 추가할 수 있는 설정 등입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="d2e00-145">전체 필터 목록은 [필터 설정][Filter Settings](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2e00-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="d2e00-146">필터는 hello를 사용 하 여 적용 된 tooa 메시지 수 **필터** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="d2e00-147">각 필터는 필터별 설정을 포함하는 해시에 의해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="d2e00-148">hello 다음 예제 hello 바닥글을 보여 주고 추적 필터를 클릭:</span><span class="sxs-lookup"><span data-stu-id="d2e00-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="d2e00-149">바닥글</span><span class="sxs-lookup"><span data-stu-id="d2e00-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="d2e00-150">클릭 추적</span><span class="sxs-lookup"><span data-stu-id="d2e00-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="d2e00-151">방법: 전자 메일 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2e00-151">How to: Update Email Properties</span></span>
<span data-ttu-id="d2e00-152">사용 하 여 일부 전자 메일 속성을 덮어쓸 수  **설정*속성** *를 사용 하 여 추가 또는  **추가*속성** *입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="d2e00-153">예를 들어 다음을 사용하여 받는 사람을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="d2e00-154">또는 다음을 사용하여 필터를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="d2e00-155">자세한 내용은 참조 [sendgrid nodejs][sendgrid-nodejs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="d2e00-156">방법: 추가 SendGrid 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="d2e00-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="d2e00-157">SendGrid 웹 기반 Api 제공 tooleverage 추가 SendGrid 기능을 Azure 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="d2e00-158">전체 세부 정보에 대 한 참조 hello [SendGrid API 설명서][SendGrid API documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2e00-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2e00-159">Next Steps</span></span>
<span data-ttu-id="d2e00-160">Hello SendGrid 전자 메일 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e00-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="d2e00-161">SendGrid Node.js 모듈 리포지토리: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="d2e00-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="d2e00-162">SendGrid API 설명서: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="d2e00-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="d2e00-163">Azure 고객을 위한 SendGrid 특가 제공: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="d2e00-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions
[트랜잭션 전자 메일 배달]: https://sendgrid.com/transactional-email
