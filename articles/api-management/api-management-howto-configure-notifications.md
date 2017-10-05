---
title: "Azure API Management에서 알림 및 메일 템플릿 구성 | Microsoft Docs"
description: "Azure API 관리에서 알림 및 메일 템플릿을 구성하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="ad799-103">Azure API 관리에서 알림 및 전자 메일 템플릿을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="ad799-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="ad799-104">API 관리는 특정 이벤트에 대한 알림을 구성하는 기능과 API 관리 인스턴스의 관리자 및 개발자와 의사를 전달하는 데 사용되는 메일 템플릿을 구성하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="ad799-105">이 항목에서는 사용 가능한 이벤트에 대한 알림을 구성하는 방법을 보여 주고 이러한 이벤트에 사용된 메일 템플릿 구성에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="ad799-106"><a name="publisher-notifications"> </a>게시자 알림 구성</span><span class="sxs-lookup"><span data-stu-id="ad799-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="ad799-107">알림을 구성하려면 Azure Portal에서 API 관리 서비스에 대해 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ad799-108">API 관리 게시자 포털로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-108">This takes you to the API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="ad799-110">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad799-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="ad799-111">왼쪽의 **API Management** 메뉴에서 **알림**을 클릭하여 사용 가능한 알림을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![게시자 알림][api-management-publisher-notifications]

<span data-ttu-id="ad799-113">알림에 대해 다음 이벤트 목록을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="ad799-114">**구독 요청(승인 필요)** - 지정된 메일 받는 사람 및 사용자가 승인이 필요한 API 제품의 구독 요청에 대한 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="ad799-115">**새 구독** - 지정된 메일 받는 사람 및 사용자가 새 API 제품 구독에 대한 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="ad799-116">**응용 프로그램 갤러리 요청** - 새 응용 프로그램이 응용 프로그램 갤러리에 제출되면 지정된 메일 받는 사람 및 사용자가 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="ad799-117">**BCC** - 지정된 메일 받는 사람 및 사용자가 개발자에게 전송된 모든 메일의 숨은 참조 복사본을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="ad799-118">**새 문제 및 설명** - 개발자 포털에서 새 문제 또는 설명이 제출되면 지정된 메일 받는 사람 및 사용자가 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="ad799-119">**Close account message(계정 종료 메시지)** - 계정이 종료되면 지정된 메일 받는 사람 및 사용자가 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="ad799-120">**구독 할당량 한도 근접** - 구독 사용량이 사용 할당량에 근접하면 다음 메일 받는 사람 및 사용자가 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="ad799-121">각 이벤트에 대해 메일 주소 입력란을 사용하여 메일 받는 사람을 지정하거나 목록에서 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="ad799-122">알릴 메일 주소를 지정하려면 메일 주소 입력란에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="ad799-123">메일 주소를 여러 개 사용하는 경우 쉼표를 사용하여 구분하세요.</span><span class="sxs-lookup"><span data-stu-id="ad799-123">If you have multiple email addresses, separate them using commas.</span></span>

![알림 받는 사람][api-management-email-addresses]

<span data-ttu-id="ad799-125">알릴 사용자를 지정하려면 **받는 사람 추가**를 클릭하고, 알릴 사용자 옆에 있는 확인란을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad799-126">관리자만 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="ad799-127">알림 받는 사람을 구성한 후 **저장** 을 클릭하여 업데이트된 알림 받는 사람을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad799-128">**게시자 알림** 탭 외부로 이동하면 저장되지 않은 변경 내용이 있는 경우 게시자 포털에서 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="ad799-129"><a name="email-templates"> </a>메일 템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="ad799-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="ad799-130">API 관리는 서비스를 관리 및 사용하는 과정에서 전송된 메일 메시지에 대한 메일 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="ad799-131">다음 메일 템플릿이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-131">The following email templates are provided.</span></span>

* <span data-ttu-id="ad799-132">응용 프로그램 갤러리 제출 승인</span><span class="sxs-lookup"><span data-stu-id="ad799-132">Application gallery submission approved</span></span>
* <span data-ttu-id="ad799-133">개발자 인사 편지</span><span class="sxs-lookup"><span data-stu-id="ad799-133">Developer farewell letter</span></span>
* <span data-ttu-id="ad799-134">개발자 할당량 한도 근접 알림</span><span class="sxs-lookup"><span data-stu-id="ad799-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="ad799-135">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="ad799-135">Invite user</span></span>
* <span data-ttu-id="ad799-136">문제에 새 설명 추가</span><span class="sxs-lookup"><span data-stu-id="ad799-136">New comment added to an issue</span></span>
* <span data-ttu-id="ad799-137">새 문제 수신</span><span class="sxs-lookup"><span data-stu-id="ad799-137">New issue received</span></span>
* <span data-ttu-id="ad799-138">새 구독 활성화</span><span class="sxs-lookup"><span data-stu-id="ad799-138">New subscription activated</span></span>
* <span data-ttu-id="ad799-139">구독 갱신 확인</span><span class="sxs-lookup"><span data-stu-id="ad799-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="ad799-140">구독 요청 거부</span><span class="sxs-lookup"><span data-stu-id="ad799-140">Subscription request declines</span></span>
* <span data-ttu-id="ad799-141">구독 요청 수신</span><span class="sxs-lookup"><span data-stu-id="ad799-141">Subscription request received</span></span>

<span data-ttu-id="ad799-142">이러한 템플릿은 필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="ad799-143">API Management 인스턴스의 메일 템플릿을 보고 구성하려면 왼쪽 **API Management** 메뉴에서 **알림**을 클릭하고 **메일 템플릿** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![메일 템플릿][api-management-email-templates]

<span data-ttu-id="ad799-145">특정 템플릿을 보거나 수정하려면 **템플릿** 드롭다운 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![메일 템플릿 목록][api-management-email-templates-list]

<span data-ttu-id="ad799-147">각 메일 템플릿의 제목은 일반 텍스트이며 본문 정의는 HTML 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="ad799-148">각 항목은 필요에 따라 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-148">Each item can be customized as desired.</span></span>

![메일 템플릿 편집기][api-management-email-template]

<span data-ttu-id="ad799-150">**매개 변수** 목록에는 제목 또는 본문에 삽입되는 매개 변수 목록이 포함되며, 이러한 매개 변수는 메일이 전송될 때 지정된 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="ad799-151">매개 변수를 삽입하려면 매개 변수를 넣을 위치에 커서를 놓고 매개 변수 이름 왼쪽 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="ad799-152">**미리 보기** 또는 **테스트 보내기**를 클릭하여 메일의 모양을 보거나 테스트 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad799-153">테스트를 미리 보거나 보낼 때에는 매개 변수가 실제 값으로 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="ad799-154">메일 템플릿의 변경 내용을 저장하려면 **저장**을 클릭하고, 변경 내용을 취소하려면 **취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad799-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
