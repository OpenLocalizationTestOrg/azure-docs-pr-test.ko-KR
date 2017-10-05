---
title: "역할을 사용하여 Azure 청구에 대한 액세스 관리 | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="8eeb4-102">역할 기반 액세스 제어를 사용하여 Azure의 요금 청구 정보에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="8eeb4-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="8eeb4-103">구독에는 사용자 역할, 즉 계정 관리자, 서비스 관리자, 공동 관리자, 소유자, 참가자, 읽기 권한자 및 청구 읽기 권한자 중 하나를 할당하여 팀의 구성원에게 Azure 청구 정보에 대한 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="8eeb4-104">이러한 사용자는 [Azure Portal](https://portal.azure.com/)에서 청구 정보에 액세스할 수 있게 되며 [청구 API](billing-usage-rate-card-overview.md)를 사용하여 청구서 및 사용량 정보를 프로그래밍 방식으로 가져올 수 있습니다(옵트인한 경우).</span><span class="sxs-lookup"><span data-stu-id="8eeb4-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="8eeb4-105">역할을 부여할 수 있는 사람, 역할로 수행할 수 있는 작업에 대한 자세한 내용은 [Azure RBAC의 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="8eeb4-106"><a name="opt-in"></a> 추가 사용자가 청구서에 액세스할 수 있도록 허용</span><span class="sxs-lookup"><span data-stu-id="8eeb4-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="8eeb4-107">계정 관리자는 [Azure Portal](https://portal.azure.com/)을 사용하여 옵트인(opt in)하고 API를 통해 다른 사용자에 대한 청구서 액세스를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="8eeb4-108">계정 관리자는 Azure Portal의 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="8eeb4-109">**청구서**를 선택하고 **청구서 액세스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![청구서에 대한 액세스를 위임하는 방법을 보여 주는 스크린샷](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="8eeb4-111">액세스를 **설정**한 후 변경 사항을 저장하면 구독 범위 역할의 사용자가 청구서를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![청구서 액세스에 대한 위임을 설정/해제하는 방법을 보여 주는 스크린샷](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="8eeb4-113">옵트인(opt in)하면 구독의 서비스 관리자, 공동 관리자, 소유자, 참가자, 읽기 권한자 및 청구 읽기 권한자가 Azure Portal에서 PDF 청구서를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="8eeb4-114">그러나 2016년 12월보다 오래된 청구서는 현재 계정 관리자만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="8eeb4-115">또한 계정 관리자는 전자 메일을 통해 청구서가 전송되도록 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="8eeb4-116">자세한 내용은 [전자 메일로 청구서 받기](billing-download-azure-invoice-daily-usage-date.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="8eeb4-117">청구 읽기 권한자 역할에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8eeb4-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="8eeb4-118">청구 읽기 권한자 역할은 Azure Portal에서 구독 청구 정보에 대해 읽기 전용으로 액세스할 수 있으며 VM 및 저장소 계정 등의 서비스에는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="8eeb4-119">구독 청구 정보에만 액세스하면 되며 Azure 서비스 관리 기능은 필요하지 않은 사람에게는 청구 읽기 권한자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="8eeb4-120">이 역할은 Azure 구독에 대해 재무 및 비용 관리만 수행하는 조직의 사용자에게 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="8eeb4-121">Azure Portal의 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="8eeb4-122">**Access Control(IAM)**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![구독 블레이드에서 IAM을 보여 주는 스크린샷](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="8eeb4-124">**역할 선택** 페이지에서 **청구 읽기 권한자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![팝업 보기에서 청구 읽기 권한자를 보여 주는 스크린샷](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="8eeb4-126">초대하려는 사용자의 전자 메일을 입력하고 **확인**을 클릭하여 초대를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![전자 메일을 입력하여 누군가를 초대하는 모습을 보여 주는 스크린샷](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="8eeb4-128">초대 전자 메일의 지침에 따라 청구 읽기 권한자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![청구 읽기 권한자가 Azure Portal에서 볼 수 있는 내용을 보여 주는 스크린샷](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="8eeb4-130">청구 읽기 권한자 기능은 미리 보기의 기능이며 엔터프라이즈(EA) 구독 또는 비 글로벌 클라우드는 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="8eeb4-131">다른 역할에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8eeb4-131">Adding users to other roles</span></span>

<span data-ttu-id="8eeb4-132">소유자 또는 참가자 등의 다른 역할의 사용자는 청구 정보에 액세스할 수만 있고 Azure 서비스에는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="8eeb4-133">이러한 역할을 관리하려면 [구독 또는 서비스를 관리하는 Azure 관리자 역할 추가 또는 변경](billing-add-change-azure-subscription-administrator.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="8eeb4-134">누가 [계정 센터](https://account.windowsazure.com)에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8eeb4-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="8eeb4-135">계정 관리자만 Azure 센터에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="8eeb4-136">계정 관리자는 구독의 법적 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="8eeb4-137">다른 사람에게 [구독 소유권이 양도](billing-subscription-transfer.md)되지 않은 한, 기본적으로 Azure 구독에 등록했거나 구입한 사람이 계정 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="8eeb4-138">계정 관리자는 구독을 만들고, 구독을 취소하고, 구독에 대한 청구 주소를 변경하고, 구독에 대한 액세스 정책을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="8eeb4-139">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="8eeb4-139">Need help?</span></span> <span data-ttu-id="8eeb4-140">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-140">Contact support.</span></span>

<span data-ttu-id="8eeb4-141">계속해서 다른 질문이 있는 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="8eeb4-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
