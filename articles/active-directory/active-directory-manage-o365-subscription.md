---
title: "Azure에서 Office 365 구독의 디렉터리 관리 | Microsoft Docs"
description: "Azure Active Directory 및 Azure 클래식 포털을 사용하여 Office 365 구독 디렉터리 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: b520a5e96417fb766a757fabc384a1fc4eb0f14e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-the-directory-for-your-office-365-subscription-in-azure"></a><span data-ttu-id="c9427-103">Azure에서 Office 365 구독의 디렉터리 관리</span><span class="sxs-lookup"><span data-stu-id="c9427-103">Manage the directory for your Office 365 subscription in Azure</span></span>
<span data-ttu-id="c9427-104">이 문서에서는 Azure 클래식 포털을 사용하여 Office 365 구독에 대해 만들어진 디렉터리를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-104">This article describes how to manage a directory that was created for an Office 365 subscription, using the Azure classic portal.</span></span> <span data-ttu-id="c9427-105">Azure 클래식 포털에 로그인하려면 Azure 구독의 서비스 관리자 또는 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-105">You must be either the Service Administrator or a co-administrator of an Azure subscription to sign in to the Azure classic portal.</span></span> <span data-ttu-id="c9427-106">Azure 구독이 없는 경우 지금 [무료 30일 평가판](https://azure.microsoft.com/trial/get-started-active-directory/) 에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-106">If you don’t yet have an Azure subscription, you can sign up for a [free 30-day trial](https://azure.microsoft.com/trial/get-started-active-directory/) today and deploy your first cloud solution in under 5 minutes, using this link.</span></span> <span data-ttu-id="c9427-107">Office 365에 로그인하는 데 사용하는 회사 또는 학교 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-107">Be sure to use the work or school account that you use to sign in to Office 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9427-108">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="c9427-109">Azure 구독을 완료한 후 Azure 클래식 포털에 로그인하고 Azure 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-109">After you complete the Azure subscription, you can sign in to the Azure classic portal and access Azure services.</span></span> <span data-ttu-id="c9427-110">Active Directory 확장을 클릭하여 Office 365 사용자를 인증하는 동일한 디렉터리를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-110">Click the Active Directory extension to manage the same directory that authenticates your Office 365 users.</span></span>

<span data-ttu-id="c9427-111">Azure 구독이 이미 있는 경우 추가 디렉터리를 관리하는 프로세스도 간단히 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-111">If you do already have an Azure subscription, the process to manage an additional directory is also straightforward.</span></span> <span data-ttu-id="c9427-112">예를 들어 Michael Smith는 Contoso.com에 대한 Office 365 구독을 보유하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-112">For example, Michael Smith might have an Office 365 subscription for Contoso.com.</span></span> <span data-ttu-id="c9427-113">그에게는 본인의 Microsoft 계정인 msmith@hotmail.com을 사용하여 등록한 Azure 구독도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-113">He also has an Azure subscription that he signed up for by using his Microsoft account, msmith@hotmail.com.</span></span> <span data-ttu-id="c9427-114">이 경우 두 개의 디렉터리를 관리하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-114">In this case, he manages two directories.</span></span>

| <span data-ttu-id="c9427-115">구독</span><span class="sxs-lookup"><span data-stu-id="c9427-115">Subscription</span></span> | <span data-ttu-id="c9427-116">Office 365</span><span class="sxs-lookup"><span data-stu-id="c9427-116">Office 365</span></span> | <span data-ttu-id="c9427-117">Azure</span><span class="sxs-lookup"><span data-stu-id="c9427-117">Azure</span></span> |
| --- | --- | --- |
|   <span data-ttu-id="c9427-118">표시 이름</span><span class="sxs-lookup"><span data-stu-id="c9427-118">Display name</span></span> |<span data-ttu-id="c9427-119">Contoso</span><span class="sxs-lookup"><span data-stu-id="c9427-119">Contoso</span></span> |<span data-ttu-id="c9427-120">기본 Azure AD(Azure Active Directory) 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c9427-120">Default Azure Active Directory (Azure AD) directory</span></span> |
|   <span data-ttu-id="c9427-121">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="c9427-121">Domain name</span></span> |<span data-ttu-id="c9427-122">contoso.com</span><span class="sxs-lookup"><span data-stu-id="c9427-122">contoso.com</span></span> |<span data-ttu-id="c9427-123">msmithhotmail.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c9427-123">msmithhotmail.onmicrosoft.com</span></span> |

<span data-ttu-id="c9427-124">그는 다단계 인증 등의 Azure AD 기능을 설정할 수 있도록 Microsoft 계정을 사용하여 Azure에 로그인한 동안 Contoso 디렉터리의 사용자 ID를 관리하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-124">He wants to manage the user identities in the Contoso directory while he is signed in to Azure using his Microsoft account, so that he can enable Azure AD features such as multifactor authentication.</span></span> <span data-ttu-id="c9427-125">다음 다이어그램은 프로세스를 설명하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-125">The following diagram may help to illustrate the process.</span></span>

![독립적인 두 디렉터리를 관리하는 다이어그램](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

<span data-ttu-id="c9427-127">이 경우 두 디렉터리는 서로 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-127">In this case, the two directories are independent of each other.</span></span>

## <a name="to-manage-two-independent-directories"></a><span data-ttu-id="c9427-128">독립적인 두 디렉터리를 관리하려면</span><span class="sxs-lookup"><span data-stu-id="c9427-128">To manage two independent directories</span></span>
<span data-ttu-id="c9427-129">Michael Smith는 Azure에 msmith@hotmail.com으로 로그인한 동안 두 디렉터리를 관리하기 위해 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-129">In order for Michael Smith to manage both directories while he is signed in to Azure as msmith@hotmail.com, he must complete the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="c9427-130">이러한 단계는 사용자가 Microsoft 계정으로 로그인한 경우에만 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-130">These steps can be completed only when a user is signed in with a Microsoft account.</span></span> <span data-ttu-id="c9427-131">사용자가 회사 또는 학교 계정을 사용하여 로그인하는 경우 **기존 디렉터리 사용** 을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-131">If the user is signed in with a work or school account, the option to **Use existing directory** isn't available.</span></span> <span data-ttu-id="c9427-132">회사 또는 학교 계정은 홈 디렉터리(즉, 회사 또는 학교 계정이 저장되고 회사 또는 학교에서 소유한 디렉터리)에 의해서만 인증될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-132">A work or school account can be authenticated only by its home directory (that is, the directory where the work or school account is stored, and that the business or school owns).</span></span>
>
>

1. <span data-ttu-id="c9427-133">[Azure 클래식 포털](https://manage.windowsazure.com)에 msmith@hotmail.com으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-133">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as msmith@hotmail.com.</span></span>
2. <span data-ttu-id="c9427-134">**새로 만들기** > **App services** > **Active Directory** > **디렉터리** > **사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-134">Click **New** > **App services** > **Active Directory** > **Directory** > **Custom Create**.</span></span>
3. <span data-ttu-id="c9427-135">기존 디렉터리 사용을 클릭하고 **지금 로그아웃** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-135">Click Use existing directory and select the **I am ready to be signed out now** checkbox.</span></span>
4. <span data-ttu-id="c9427-136">Contoso.onmicrosoft.com의 전역 관리자로 Azure 클래식 포털에 로그인합니다(예: msmith@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="c9427-136">Sign in to the Azure classic portal as global admin of Contoso.onmicrosoft.com (for example, msmith@contoso.com).</span></span>
5. <span data-ttu-id="c9427-137">**Azure로 Contoso 디렉터리를 사용할까요?**라는 메시지가 나타나면 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-137">When prompted to **Use the Contoso directory with Azure?**, click **Continue**.</span></span>
6. <span data-ttu-id="c9427-138">**지금 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-138">Click **Sign out now**.</span></span>
7. <span data-ttu-id="c9427-139">msmith@hotmail.com에서와 같이 Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-139">Sign in to the Azure classic portal as msmith@hotmail.com.</span></span> <span data-ttu-id="c9427-140">Contoso 디렉터리와 기본 디렉터리가 Active Directory 확장에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-140">The Contoso directory and the Default directory appear in the Active Directory extension.</span></span>

<span data-ttu-id="c9427-141">다음 단계가 완료되면 msmith@hotmail.com은 Contoso 디렉터리의 전역 관리자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-141">After completing these steps, msmith@hotmail.com is a global administrator in the Contoso directory.</span></span>

## <a name="to-administer-resources-as-the-global-admin"></a><span data-ttu-id="c9427-142">전역 관리자로 리소스를 관리하려면</span><span class="sxs-lookup"><span data-stu-id="c9427-142">To administer resources as the global admin</span></span>
<span data-ttu-id="c9427-143">이제 Jane Doe가 msmith@hotmail.com의 Azure 구독과 연결된 웹 사이트 및 데이터베이스 리소스를 관리해야 한다고 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-143">Now let’s suppose that Jane Doe needs administer websites and database resources that are associated with the Azure subscription for msmith@hotmail.com.</span></span> <span data-ttu-id="c9427-144">이렇게 하려면 Michael Smith는 다음 추가 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-144">Before she can do that, Michael Smith needs to complete these additional steps:</span></span>

1. <span data-ttu-id="c9427-145">Azure 구독의 서비스 관리자 계정(이 예의 경우 msmith@hotmail.com)을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-145">Sign in to the [Azure classic portal](https://manage.windowsazure.com) using the Service Administrator account for the Azure subscription (in this example, msmith@hotmail.com).</span></span>
2. <span data-ttu-id="c9427-146">Contoso 디렉터리로 구독을 전송합니다. 이를 위해 **설정** > **구독**을 클릭하고 구독 > **디렉터리 편집** > **Contoso(Contoso.com)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-146">Transfer the subscription to the Contoso directory: click **Settings** > **Subscriptions** > select the subscription > **Edit Directory** > select **Contoso (Contoso.com)**.</span></span> <span data-ttu-id="c9427-147">전송 과정이 진행되면서 구독의 공동 관리자인 모든 회사 또는 학교 계정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-147">As part of the transfer, any work or school accounts that are co-administrators of the subscription are removed.</span></span>
3. <span data-ttu-id="c9427-148">Jane Doe를 구독의 공동 관리자로 추가합니다. 이를 위해 **설정** > **관리자**를 클릭하고 구독 > **추가**를 선택한 다음 **JohnDoe@Contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9427-148">Add Jane Doe as co-administrator of the subscription: click **Settings** > **Administrators** > select the subscription > **Add** > type **JohnDoe@Contoso.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9427-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9427-149">Next steps</span></span>
<span data-ttu-id="c9427-150">구독과 디렉터리 간의 관계에 대한 자세한 내용은 [구독과 디렉터리의 연관 관계](active-directory-how-subscriptions-associated-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9427-150">For more information about the relationship between subscriptions and directories, see [How a subscription is associated with a directory](active-directory-how-subscriptions-associated-directory.md).</span></span>
