---
title: "aaaConfigure 알림을 하 고 Azure API 관리에서 서식 파일을 전자 메일로 | Microsoft Docs"
description: "자세한 방법을 tooconfigure 알림 및 Azure API 관리에서 서식 파일을 전자 메일입니다."
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
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="53e7c-103">어떻게 tooconfigure 알림 및 Azure API 관리에서 서식 파일을 전자 메일</span><span class="sxs-lookup"><span data-stu-id="53e7c-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="53e7c-104">API 관리 특정 이벤트 및 tooconfigure hello 전자 메일 템플릿으로 사용 되는 toocommunicate hello 관리자와 개발자 API 관리 인스턴스 사용에 대 한 tooconfigure 알림 hello 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="53e7c-105">이 항목에 대 한 tooconfigure 알림을 사용할 수 있는 이벤트를 hello 하는 방법을 보여 줍니다., 이러한 이벤트에 사용 되는 hello 전자 메일 템플릿 구성의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="53e7c-106"><a name="publisher-notifications"> </a>게시자 알림 구성</span><span class="sxs-lookup"><span data-stu-id="53e7c-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="53e7c-107">tooconfigure 알림을 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="53e7c-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="53e7c-108">API 관리 게시자 포털 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-108">This takes you toohello API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="53e7c-110">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="53e7c-111">클릭 **알림** hello에서 **API 관리** 메뉴 hello에 왼쪽 tooview hello 수 있는 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![게시자 알림][api-management-publisher-notifications]

<span data-ttu-id="53e7c-113">hello 이벤트 목록은 다음 구성할 수 있습니다 알림.</span><span class="sxs-lookup"><span data-stu-id="53e7c-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="53e7c-114">**(이렇게 승인을 받도록) 구독 요청** -지정 된 전자 메일 받는 사람 hello 및 사용자가 이렇게 승인을 받도록 API 제품에 대 한 구독 요청에 대 한 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="53e7c-115">**새 구독** -지정 된 전자 메일 받는 사람 hello 및 사용자가 새 API 제품 구독에 대 한 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="53e7c-116">**응용 프로그램 갤러리 요청** -지정 된 전자 메일 받는 사람 hello 및 새 응용 프로그램에 제출 된 toohello 응용 프로그램 갤러리는 하는 경우 사용자가 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="53e7c-117">**숨은 참조** -지정 된 전자 메일 받는 사람 hello 및 사용자 전자 메일 보낸 전자 메일 toodevelopers 모든 항목이 며 탄소 복사본을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="53e7c-118">**새 문제 또는 주석** -지정 된 전자 메일 받는 사람 hello 및 사용자는 전자 메일 알림이 제공 때 새 문제 또는 주석 hello 개발자 포털에서 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="53e7c-119">**계정 닫기 메시지** -지정 된 전자 메일 받는 사람 hello 및 계정을 닫을 때 사용자가 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="53e7c-120">**임박한 구독 할당량 한도** -전자 메일 받는 사람에 게 다음 hello 및 구독 사용 현황 닫기 toousage 할당량을 가져올 때 사용자가 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="53e7c-121">각 이벤트에 대 한 hello 전자 메일 주소 텍스트 상자를 사용 하 여 전자 메일 받는 사람을 지정할 수 있습니다 또는 목록에서 사용자가 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="53e7c-122">알림을 받은 toospecify hello 전자 메일 주소 toobe hello 전자 메일 주소 텍스트 상자에을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="53e7c-123">메일 주소를 여러 개 사용하는 경우 쉼표를 사용하여 구분하세요.</span><span class="sxs-lookup"><span data-stu-id="53e7c-123">If you have multiple email addresses, separate them using commas.</span></span>

![알림 받는 사람][api-management-email-addresses]

<span data-ttu-id="53e7c-125">toospecify hello 사용자 toobe 알림을 클릭 **받는 사람을 추가**알림을 hello 사용자 toobe 옆에 있는 hello 확인란을 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="53e7c-126">관리자만 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="53e7c-127">Hello 알림 받는 사람을 구성한 후 클릭 **저장** tooapply hello 알림 받는 사람을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="53e7c-128">Hello 벗어나 탐색 하면 **게시자 알림** 탭 hello 게시자 포털 알려 변경 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="53e7c-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="53e7c-129"><a name="email-templates"> </a>메일 템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="53e7c-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="53e7c-130">API 관리 전자 메일 템플릿을 제공 hello에 대 한 전자 메일 전송 된 메시지를 관리 하 고 hello 서비스를 사용 하 여 hello 과정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="53e7c-131">다음 전자 메일 템플릿을 hello 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="53e7c-132">응용 프로그램 갤러리 제출 승인</span><span class="sxs-lookup"><span data-stu-id="53e7c-132">Application gallery submission approved</span></span>
* <span data-ttu-id="53e7c-133">개발자 인사 편지</span><span class="sxs-lookup"><span data-stu-id="53e7c-133">Developer farewell letter</span></span>
* <span data-ttu-id="53e7c-134">개발자 할당량 한도 근접 알림</span><span class="sxs-lookup"><span data-stu-id="53e7c-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="53e7c-135">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="53e7c-135">Invite user</span></span>
* <span data-ttu-id="53e7c-136">새 메모 tooan 문제 추가</span><span class="sxs-lookup"><span data-stu-id="53e7c-136">New comment added tooan issue</span></span>
* <span data-ttu-id="53e7c-137">새 문제 수신</span><span class="sxs-lookup"><span data-stu-id="53e7c-137">New issue received</span></span>
* <span data-ttu-id="53e7c-138">새 구독 활성화</span><span class="sxs-lookup"><span data-stu-id="53e7c-138">New subscription activated</span></span>
* <span data-ttu-id="53e7c-139">구독 갱신 확인</span><span class="sxs-lookup"><span data-stu-id="53e7c-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="53e7c-140">구독 요청 거부</span><span class="sxs-lookup"><span data-stu-id="53e7c-140">Subscription request declines</span></span>
* <span data-ttu-id="53e7c-141">구독 요청 수신</span><span class="sxs-lookup"><span data-stu-id="53e7c-141">Subscription request received</span></span>

<span data-ttu-id="53e7c-142">이러한 템플릿은 필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="53e7c-143">tooview API 관리 인스턴스에 대 한 전자 메일 템플릿을 hello 구성를 클릭 하 고 **알림** hello에서 **API 관리** hello 왼쪽, 및 select hello에 메뉴 **전자 메일 템플릿**  탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![메일 템플릿][api-management-email-templates]

<span data-ttu-id="53e7c-145">tooview 특정 템플릿을 수정 하거나, hello에서 선택 **템플릿** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![메일 템플릿 목록][api-management-email-templates-list]

<span data-ttu-id="53e7c-147">각 메일 템플릿의 제목은 일반 텍스트이며 본문 정의는 HTML 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="53e7c-148">각 항목은 필요에 따라 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-148">Each item can be customized as desired.</span></span>

![메일 템플릿 편집기][api-management-email-template]

<span data-ttu-id="53e7c-150">hello **매개 변수** 목록에 매개 변수의 경우에는 hello 제목 또는 본문에 삽입, hello 전자 메일을 보내면 대체 hello 지정 된 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="53e7c-151">tooinsert 매개 변수를 커서 hello hello 매개 변수 toogo를 선택 하 고 hello 매개 변수 이름의 hello 화살표 toohello 왼쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="53e7c-152">클릭 **미리 보기** 또는 **테스트 보내기** toosee hello 전자 메일은 보거나 테스트 전자 메일 보내기 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="53e7c-153">hello 매개 변수는 미리 보기 또는 테스트를 보낼 때 실제 값으로 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="53e7c-154">toosave hello 변경 toohello 전자 메일 템플릿을 클릭 **저장**, toocancel hello 변경 클릭 또는 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="53e7c-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
