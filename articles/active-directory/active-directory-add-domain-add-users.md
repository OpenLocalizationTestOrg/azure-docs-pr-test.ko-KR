---
title: "Azure Active Directory의 사용자 지정 도메인에 사용자 할당 | Microsoft Docs"
description: "사용자 계정으로 Azure Active Directory의 사용자 지정 도메인을 채우는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="e45fe-103">사용자 지정 도메인에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e45fe-103">Assign users to a custom domain</span></span>
<span data-ttu-id="e45fe-104">Azure Active Directory에 사용자 지정 도메인을 추가한 후에 인증을 시작할 수 있도록 이 도메인에 대한 사용자 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e45fe-105">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="e45fe-106">Azure AD 관리 센터에서 도메인 이름을 관리하는 방법은 [Azure Active Directory에서 사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e45fe-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="e45fe-107">온-프레미스 디렉터리에서 동기화된 사용자</span><span class="sxs-lookup"><span data-stu-id="e45fe-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="e45fe-108">온-프레미스 Active Directory와 Azure Active Directory 간의 연결을 이미 설정한 경우 동기화로 계정을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="e45fe-109">Azure Active Directory를 온-프레미스 Active Directory와 동기화하는 방법에 대한 자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e45fe-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="e45fe-110">클라우드에 추가되고 관리되는 사용자</span><span class="sxs-lookup"><span data-stu-id="e45fe-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="e45fe-111">기존 사용자 계정에 대한 도메인을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="e45fe-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="e45fe-112">전역 관리자 또는 사용자 관리자인 계정을 사용하여 Azure 클래식 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="e45fe-113">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-113">Open your directory.</span></span>
3. <span data-ttu-id="e45fe-114">**사용자** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="e45fe-115">목록에서 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-115">Select the user from the list.</span></span>
5. <span data-ttu-id="e45fe-116">사용자에 대한 도메인을 변경한 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="e45fe-117">이 작업은 [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) 또는 [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)를 사용하여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="e45fe-118">새 사용자를 만들 때 사용자 지정 도메인 선택</span><span class="sxs-lookup"><span data-stu-id="e45fe-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="e45fe-119">전역 관리자 또는 사용자 관리자인 계정을 사용하여 Azure 클래식 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="e45fe-120">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-120">Open your directory.</span></span>
3. <span data-ttu-id="e45fe-121">**사용자** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="e45fe-122">명령 모음에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="e45fe-123">사용자 이름에 추가할 때 도메인 목록에서 사용자 지정 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="e45fe-124">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e45fe-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e45fe-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e45fe-125">Next steps</span></span>
* [<span data-ttu-id="e45fe-126">사용자 지정 도메인 이름을 사용하여 사용자의 로그인 환경 간소화</span><span class="sxs-lookup"><span data-stu-id="e45fe-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="e45fe-127">사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="e45fe-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="e45fe-128">Azure AD에서 도메인 관리 개념 알아보기</span><span class="sxs-lookup"><span data-stu-id="e45fe-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

