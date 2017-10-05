---
title: "Azure의 리소스 액세스 이해 | Microsoft Docs"
description: "이 항목에서는 구독 관리자를 사용하여 전체 Azure Portal에서 리소스 액세스를 제어하는 방법에 대한 개념을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: f1fda3c4192d0dae4fa60788f4d88fb72ddba4ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-resource-access-in-azure"></a><span data-ttu-id="31098-103">Azure의 리소스 액세스 이해</span><span class="sxs-lookup"><span data-stu-id="31098-103">Understanding resource access in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31098-104">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-104">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="31098-105">Azure Portal은 Azure 리소스를 보다 정확하게 관리할 수 있도록 [역할 기반 액세스 제어](role-based-access-control-configure.md)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-105">The Azure portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span></span>
> 
> 

<span data-ttu-id="31098-106">2013년 10월에 Azure 클래식 포털 및 서비스 관리 API는 Azure 리소스에 대한 액세스를 관리하기 위한 사용자 환경을 개선하기 위한 토대를 마련하기 위해 Azure Active Directory와 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-106">In October 2013, the Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order to lay the groundwork for improving the user experience for managing access to Azure resources.</span></span> <span data-ttu-id="31098-107">Azure Active Directory는 이미 사용자 관리, 온-프레미스 디렉터리 동기화, 다단계 인증 및 응용 프로그램 액세스 제어와 같은 훌륭한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span></span> <span data-ttu-id="31098-108">물론 이러한 기능들로 Azure 리소스를 전반적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span></span>

<span data-ttu-id="31098-109">Azure의 액세스 제어는 결제 관점에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-109">Access control in Azure starts from a billing perspective.</span></span> <span data-ttu-id="31098-110">[Azure 계정 센터](https://account.windowsazure.com/subscriptions)를 방문하여 액세스하는 Azure 계정의 소유자는 계정 관리자(AA)입니다.</span><span class="sxs-lookup"><span data-stu-id="31098-110">The owner of an Azure account, accessed by visiting the  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is the Account Administrator (AA).</span></span> <span data-ttu-id="31098-111">구독은 결제를 위한 컨테이너이지만 보안 경계로서의 역할도 합니다. 각 구독에는 [Azure 클래식 포털](https://manage.windowsazure.com/)을 사용하여 해당 구독에서 Azure 리소스를 추가, 제거 및 수정할 수 있는 서비스 관리자(SA)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="31098-112">새 구독의 기본 SA는 AA이지만 AA가 Azure 계정 센터에서 SA를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-112">The default SA of a new subscription is the AA, but the AA can change the SA in the Azure Accounts Center.</span></span>

<br><br>![Azure 계정][1]

<span data-ttu-id="31098-114">또한 구독은 디렉터리와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-114">Subscriptions also have an association with a directory.</span></span> <span data-ttu-id="31098-115">디렉터리는 사용자 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-115">The directory defines a set of users.</span></span> <span data-ttu-id="31098-116">사용자 집합은 디렉터리를 만든 회사 또는 학교 사용자가 될 수 있습니다. 또는 외부 사용자(즉, Microsoft 계정)이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-116">These can be users from the work or school that created the directory or they can be external users (that is, Microsoft Accounts).</span></span> <span data-ttu-id="31098-117">구독은 서비스 관리자(SA) 또는 CA(공동 관리자)로 할당된 해당 디렉터리 사용자의 하위 집합에서 액세스할 수 있습니다. 유일한 예외는 레거시의 이유로 Microsoft 계정(이전의 Windows Live ID)이 디렉터리에 없는 SA 또는 CA로 할당될 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="31098-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); the only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in the directory.</span></span>

<br><br>![Azure의 액세스 제어][2]

<span data-ttu-id="31098-119">Azure 클래식 포털 내의 기능은 Microsoft 계정을 통해 로그인하는 SA를 사용하여 구독이 연결되어 있는 디렉터리를 변경합니다. 이 때, **설정**의 **구독** 페이지에서 **디렉터리 편집** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-119">Functionality within the Azure classic portal enables SAs that are signed in using a Microsoft Account to change the directory that a subscription is associated with by using the **Edit Directory** command on the **Subscriptions** page in **Settings**.</span></span> <span data-ttu-id="31098-120">이 작업은 해당 구독의 액세스 제어에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31098-120">Note that this operation has implications on the access control of that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="31098-121">회사 또는 학교 계정은 소속된 디렉터리에만 로그인할 수 있기 때문에 Azure 클래식 포털의 **디렉터리 편집** 명령은 회사 또는 학교 계정을 사용하여 로그인하는 사용자에게 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-121">The **Edit Directory** command in the Azure classic portal is not available to users who are signed in using a work or school account because those accounts can sign in only to the directory to which they belong.</span></span>
> 
> 

<br><br>![간단한 사용자 로그인 흐름][3]

<span data-ttu-id="31098-123">단순한 경우 조직(예: Contoso)은 요금 청구를 적용하고 동일한 집합의 구독에 대해 액세스 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="31098-123">In the simple case, an organization (such as Contoso) will enforce billing and access control across the same set of subscriptions.</span></span> <span data-ttu-id="31098-124">즉, 디렉터리는 단일 Azure 계정에 의해 소유된 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="31098-124">That is, the directory is associated to subscriptions that are owned by a single Azure Account.</span></span> <span data-ttu-id="31098-125">Azure 클래식 포털에 로그인하면 사용자는 리소스의 두 가지 컬렉션(이전 그림에서 주황색으로 표시)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-125">Upon successful login to the Azure classic portal, users see two collections of resources (depicted in orange in the previous illustration):</span></span>

* <span data-ttu-id="31098-126">사용자 계정이 있는 디렉터리 (원본 또는 외래 사용자로 추가).</span><span class="sxs-lookup"><span data-stu-id="31098-126">Directories where their user account exists (sourced or added as a foreign principal).</span></span> <span data-ttu-id="31098-127">로그인에 사용되는 디렉터리는 이 계산과 관련이 없으므로 디렉터리는 로그인 위치에 관계없이 항상 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31098-127">Note that the directory used for login isn’t relevant to this computation, so your directories will always be shown regardless of where you logged in.</span></span>
* <span data-ttu-id="31098-128">(SA 또는 CA인 경우) 사용자가 액세스 할 수 있는 로그인 AND로 사용되는 디렉터리와 연결된 구독의 일부인 리소스.</span><span class="sxs-lookup"><span data-stu-id="31098-128">Resources that are part of subscriptions that are associated with the directory used for login AND which the user can access (where they are an SA or CA).</span></span>

<br><br>![여러 구독 및 디렉터리가 있는 사용자][4]

<span data-ttu-id="31098-130">여러 디렉터리에 구독이 있는 사용자는 구독 필터를 사용하여 Azure 클래식 포털의 현재 컨텍스트를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-130">Users with subscriptions across multiple directories have the ability to switch the current context of the Azure classic portal by using the subscription filter.</span></span> <span data-ttu-id="31098-131">내부적으로 이렇게 하면 다른 디렉터리에 별도로 로그인하게 되지만, single sign-on (SSO)을 사용하여 원활하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-131">Under the covers, this results in a separate login to a different directory, but this is accomplished seamlessly using single sign-on (SSO).</span></span>

<span data-ttu-id="31098-132">구독 간에 리소스를 이동하는 등의 작업은 구독의 단일 디렉터리 보기의 결과로 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span></span> <span data-ttu-id="31098-133">리소스 전송을 수행하려면 **설정**에서 구독 페이지의 **디렉터리 편집** 명령을 처음 사용하여 동일한 디렉터리에 구독을 연결해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31098-133">To perform the resource transfer, it may be necessary to first use the **Edit Directory** command on the Subscriptions page in **Settings** to associate the subscriptions to the same directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31098-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31098-134">Next Steps</span></span>
* <span data-ttu-id="31098-135">Azure 구독에 대한 관리자를 변경하는 방법에 대해 자세히 알아보려면 [Azure 관리자 역할을 추가 또는 변경하는 방법](../billing/billing-add-change-azure-subscription-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="31098-135">To learn more about how to change administrators for an Azure subscription, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span></span>
* <span data-ttu-id="31098-136">Azure 구독에 Azure Active Directory가 연결되는 방법에 대한 자세한 내용은 [Azure 구독을 Azure Active Directory에 연결하는 방법](active-directory-how-subscriptions-associated-directory.md)</span><span class="sxs-lookup"><span data-stu-id="31098-136">For more information on how Azure Active Directory relates to your Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span></span>
* <span data-ttu-id="31098-137">Azure AD에서 역할을 할당하는 방법에 대한 자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="31098-137">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
