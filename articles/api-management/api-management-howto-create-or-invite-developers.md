---
title: "aaaHow Azure API 관리에서 사용자 계정 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 초대에서에서 사용자의 Azure API 관리"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="0cddc-103">Azure API 관리에서 toomanage 사용자 계정을 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0cddc-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="0cddc-104">API 관리에서 개발자는 hello API 관리를 사용 하 여을 노출 하는 Api의 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="0cddc-105">이 가이드에서는 toohow toocreate 및 초대 개발자 toouse hello Api 및 API 관리 인스턴스를 사용할 수 있는 toothem 하는 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="0cddc-106">프로그래밍 방식으로 사용자 계정 관리에 대 한 내용은 hello 참조 [사용자 엔터티](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello에 대 한 설명서 [API 관리 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="0cddc-107"><a name="create-developer"> </a>새 개발자 만들기</span><span class="sxs-lookup"><span data-stu-id="0cddc-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="0cddc-108">새 개발자 toocreate 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="0cddc-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="0cddc-109">API 관리 게시자 포털 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="0cddc-110">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="0cddc-112">클릭 **사용자** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![개발자 만들기][api-management-create-developer]

<span data-ttu-id="0cddc-114">Hello 입력 **전자 메일**, **암호**, 및 **이름** hello 새 개발자 및 클릭에 대 한 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![개발자 만들기][api-management-add-new-user]

<span data-ttu-id="0cddc-116">새로 만든된 개발자 계정을 기본적으로 **활성**, hello와 관련 된 및 **개발자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![새 개발자][api-management-new-developer]

<span data-ttu-id="0cddc-118">에 있는 개발자 계정을 **활성** 상태가 tooaccess 사용된 될 수 있음 구독 갖고 있는 hello Api의 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="0cddc-119">추가 그룹으로 tooassociate hello 새로 만든 개발자 참조 [tooassociate 개발자와 그룹화 하는 방법을][How tooassociate groups with developers]합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="0cddc-120"><a name="invite-developer"> </a>개발자 초대</span><span class="sxs-lookup"><span data-stu-id="0cddc-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="0cddc-121">개발자 tooinvite 클릭 **사용자** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **사용자 초대**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![개발자 초대][api-management-invite-developer]

<span data-ttu-id="0cddc-123">Hello 개발자의 hello 이름 및 전자 메일 주소를 입력 하 고 클릭 **초대**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![개발자 초대][api-management-invite-developer-window]

<span data-ttu-id="0cddc-125">확인 메시지가 표시 되지만 hello 초대를 수락 하도록 초대 새로 hello 개발자 될 때까지 hello 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![초대 확인][api-management-invite-developer-confirmation]

<span data-ttu-id="0cddc-127">개발자, 초대 toohello 개발자 전자 메일이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="0cddc-128">이 메일은 템플릿을 사용하여 생성되며 사용자 지정 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="0cddc-129">자세한 내용은 [메일 템플릿 구성][Configure email templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cddc-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="0cddc-130">Hello 초대를 수락 되 면 hello 계정 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="0cddc-131"><a name="block-developer"> </a> 개발자 계정 비활성화 또는 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="0cddc-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="0cddc-132">기본적으로, 새로 만들거나 초대한 개발자 계정은 **활성**상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="0cddc-133">개발자 계정으로 toodeactivate 클릭 **블록**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="0cddc-134">차단 된 개발자 계정으로 tooreactivate 클릭 **Activate**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="0cddc-135">차단 된 개발자 계정 없습니다 hello 개발자 포털에 액세스 하거나 Api를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="0cddc-136">사용자 계정 toodelete 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-136">toodelete a user account, click **Delete**.</span></span>

![개발자 차단][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="0cddc-138">사용자 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="0cddc-138">Reset a user password</span></span>
<span data-ttu-id="0cddc-139">사용자 계정에 대 한 tooreset hello 암호 hello hello 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![암호 재설정][api-management-view-developer]

<span data-ttu-id="0cddc-141">클릭 **암호 재설정** toosend 링크 toohello 사용자 tooreset 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![암호 재설정][api-management-reset-password]

<span data-ttu-id="0cddc-143">사용자 계정으로 tooprogrammatically 작업 참조 hello [사용자 엔터티](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello에 대 한 설명서 [API 관리 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="0cddc-144">사용자 계정 암호 tooa 특정 값 tooreset hello를 사용할 수 있습니다 [사용자 업데이트](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) 작업 hello 원하는 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="0cddc-145">확인 보류 중</span><span class="sxs-lookup"><span data-stu-id="0cddc-145">Pending verification</span></span>
![확인 보류 중][api-management-pending-verification]

## <span data-ttu-id="0cddc-147"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cddc-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="0cddc-148">개발자 계정이 만들어지면를 역할에 연결할 수 있으며 tooproducts 및 Api 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="0cddc-149">자세한 내용은 참조 [어떻게 toocreate 및 사용 하 여 그룹][How toocreate and use groups]합니다.</span><span class="sxs-lookup"><span data-stu-id="0cddc-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
