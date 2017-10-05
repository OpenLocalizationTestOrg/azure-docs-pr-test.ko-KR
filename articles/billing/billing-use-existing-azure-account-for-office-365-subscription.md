---
title: "Azure 계정으로 Office 365 등록 | Microsoft Docs"
description: "Azure 계정을 사용하여 Office 365 구독을 만드는 방법 알아보기"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: 1c6e277e321980aaf30f821dbb41c7eaf296b4cf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a><span data-ttu-id="7fc72-103">Azure 계정으로 Office 365 구독에 등록</span><span class="sxs-lookup"><span data-stu-id="7fc72-103">Sign up for an Office 365 subscription with your Azure account</span></span>
<span data-ttu-id="7fc72-104">Azure 구독자인 경우 Azure 계정을 사용하여 Office 365 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-104">If you're Azure subscriber, you can use your Azure account to sign up for an Office 365 subscription.</span></span> <span data-ttu-id="7fc72-105">Azure 구독이 있는 조직의 일부인 경우 기존 Azure AD(Azure Active Directory)에서 사용자를 위한 Office 365 구독을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-105">If you're part of an organization that has an Azure subscription, you can create Office 365 subscriptions for users in your existing Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7fc72-106">Azure Active Directory 테넌트에서 전역 관리자 또는 대금 청구 관리자 권한이 있는 계정을 사용하여 Office 365에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-106">Sign up to Office 365 using an account that has Global Admin or Billing Admin permissions in your Azure Active Directory tenant.</span></span> <span data-ttu-id="7fc72-107">자세한 내용은 [Azure AD에서 계정 권한 확인](#RoleInAzureAD) 및 [Azure Active Directory에서 관리자 역할 할당](../active-directory/active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fc72-107">For more information, see [Check my account permissions in Azure AD](#RoleInAzureAD) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="7fc72-108">Office 365 계정과 Azure 구독이 둘 다 이미 있는 경우 [Azure 구독에 Office 365 테넌트 연결](billing-add-office-365-tenant-to-azure-subscription.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-108">If you already have both an Office 365 account and an Azure subscription, you can [Associate an Office 365 tenant to an Azure subscription](billing-add-office-365-tenant-to-azure-subscription.md).</span></span>

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a><span data-ttu-id="7fc72-109">Azure 계정을 사용하여 Office 365 구독 가져오기</span><span class="sxs-lookup"><span data-stu-id="7fc72-109">Get an Office 365 subscription by using your Azure account</span></span>

1. <span data-ttu-id="7fc72-110">[Office 365 제품 페이지](https://products.office.com/business)로 이동한 후 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-110">Go to the [Office 365 product page](https://products.office.com/business), and select a plan.</span></span>
2. <span data-ttu-id="7fc72-111">페이지의 오른쪽 위에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-111">Click **Sign in** on the upper-right corner of the page.</span></span>

    ![Office 365 평가판 페이지 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. <span data-ttu-id="7fc72-113">Azure 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-113">Sign in with your Azure account credentials.</span></span> <span data-ttu-id="7fc72-114">조직에 대한 구독을 만들려고 하는 경우 Azure Active Directory 테넌트 내 전역 관리자 또는 대금 청구 관리자 디렉터리 역할의 구성원인 Azure 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-114">If you're creating a subscription for your organization, use an Azure account that's a member of the Global Admin or Billing Admin directory role in your Azure Active Directory tenant.</span></span>

    ![Office 365 로그인 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. <span data-ttu-id="7fc72-116">**지금 시도**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-116">Click **Try now**.</span></span>

    ![Office 365에 대한 주문을 확인하는 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. <span data-ttu-id="7fc72-118">주문 접수 페이지에서 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-118">On the order receipt page, click **Continue**.</span></span>

    ![Office 365 주문 접수 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

<span data-ttu-id="7fc72-120">이제 모든 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-120">Now you're all set.</span></span> <span data-ttu-id="7fc72-121">조직에 대한 Office 365 구독을 만든 경우 다음 단계에 따라 Azure AD 사용자가 현재 Office 365에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-121">If you created the Office 365 subscription for your organization, use the following steps to check that your Azure AD users are now in Office 365.</span></span>

1. <span data-ttu-id="7fc72-122">Office 365 관리 센터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-122">Open the Office 365 admin center.</span></span>
2. <span data-ttu-id="7fc72-123">**사용자**를 확장한 다음 **활성 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-123">Expand **USERS**, and then click **Active Users**.</span></span>

    ![Office 365 관리 센터 사용자의 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

<span data-ttu-id="7fc72-125">등록 후 Azure 구독이 속해 있는 Azure Active Directory 인스턴스에 Office 365 구독이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-125">After you sign up, the Office 365 subscription is added to the same Azure Active Directory instance that your Azure subscription belongs to.</span></span> <span data-ttu-id="7fc72-126">자세한 내용은 [Azure 및 Office 365 구독에 대한 추가 정보](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) 및 [Azure 구독이 Azure Active Directory와 연결되는 방법](../active-directory/active-directory-how-subscriptions-associated-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fc72-126">For more information, see [More about Azure and Office 365 subscriptions](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) and [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <span data-ttu-id="7fc72-127"><a id="RoleInAzureAD"></a>Azure AD에서 내 계정 사용 권한 확인</span><span class="sxs-lookup"><span data-stu-id="7fc72-127"><a id="RoleInAzureAD"></a>Check my account permissions in Azure AD</span></span>
1. <span data-ttu-id="7fc72-128">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-128">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7fc72-129">**더 많은 서비스**를 클릭하고 **Active Directory**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-129">Click **More services**, and then search for **Active Directory**.</span></span>

    ![Azure Portal의 Active Directory 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. <span data-ttu-id="7fc72-131">**사용자 및 그룹** > **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-131">Click **Users and groups** > **All users**.</span></span>
4. <span data-ttu-id="7fc72-132">사용자 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-132">Select the user name.</span></span> 

    ![Azure Active Directory 사용자를 보여 주는 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. <span data-ttu-id="7fc72-134">**디렉터리 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-134">Click **Directory role**.</span></span>
  
    ![Azure Portal 디렉터리 역할을 보여 주는 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  <span data-ttu-id="7fc72-136">기존 Azure Active Directory에서 사용자를 위한 Office 365 구독을 만들려면 **전역 관리자** 또는 **제한된 관리자** > **대금 청구 관리자** 역할이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7fc72-136">The role **Global administrator** or **Limited administrator** > **Billing administrator** is required to create an Office 365 subscription for users in your existing Azure Active Directory.</span></span>

    ![Azure Portal 디렉터리 역할 대금 청구 관리자를 보여 주는 스크린샷](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="7fc72-138">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="7fc72-138">Need help?</span></span> <span data-ttu-id="7fc72-139">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7fc72-139">Contact support.</span></span>
<span data-ttu-id="7fc72-140">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="7fc72-140">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span> 
