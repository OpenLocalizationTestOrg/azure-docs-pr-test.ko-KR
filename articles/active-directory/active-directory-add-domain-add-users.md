---
title: "aaaAssign 사용자 tooa Azure Active Directory에서 사용자 지정 도메인 | Microsoft Docs"
description: "어떻게 toopopulate 사용자 계정으로 Azure Active Directory에서 사용자 지정 도메인입니다."
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="9bbae-103">사용자가 사용자 지정 도메인을 tooa 할당</span><span class="sxs-lookup"><span data-stu-id="9bbae-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="9bbae-104">사용자 지정 도메인 tooAzure Active Directory 사용자를 추가한 후에 인증을 시작할 수 있도록이 도메인에 대 한 hello 사용자 계정을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bbae-105">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="9bbae-106">어떻게 toomanage 도메인 이름 hello Azure AD 관리 센터에서 참조 [Azure Active Directory에서 사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="9bbae-107">온-프레미스 디렉터리에서 동기화된 사용자</span><span class="sxs-lookup"><span data-stu-id="9bbae-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="9bbae-108">이미 설정한 경우 한 연결을 온-프레미스 간의 Active Directory와 Azure Active Directory를 동기화 hello 계정을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="9bbae-109">Toosynchronize 온-프레미스 Active Directory와 Azure Active Directory 확인 하려면 어떻게 해야 대 한 자세한 내용은 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="9bbae-110">사용자 추가 하 고 hello 클라우드에서 관리</span><span class="sxs-lookup"><span data-stu-id="9bbae-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="9bbae-111">기존 사용자 계정에 대 한 toochange hello 도메인:</span><span class="sxs-lookup"><span data-stu-id="9bbae-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="9bbae-112">열기 hello 전역 관리자 또는 사용자 관리자 인 계정을 사용 하 여 Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="9bbae-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9bbae-113">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-113">Open your directory.</span></span>
3. <span data-ttu-id="9bbae-114">선택 hello **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="9bbae-115">Hello 사용자 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="9bbae-116">Hello 사용자에 대 한 hello 도메인을 변경 하 고 다음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="9bbae-117">또한 이렇게 사용 하 여 [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) 또는 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="9bbae-118">새 사용자를 만들 때 사용자 지정 도메인 선택</span><span class="sxs-lookup"><span data-stu-id="9bbae-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="9bbae-119">열기 hello 전역 관리자 또는 사용자 관리자 인 계정을 사용 하 여 Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="9bbae-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9bbae-120">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-120">Open your directory.</span></span>
3. <span data-ttu-id="9bbae-121">선택 hello **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="9bbae-122">Hello 명령 모음에서 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="9bbae-123">Hello 사용자 이름을 추가 하면 사용자 지정 도메인 hello hello 도메인 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="9bbae-124">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbae-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bbae-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9bbae-125">Next steps</span></span>
* [<span data-ttu-id="9bbae-126">사용자에 대 한 사용자 지정 도메인 이름을 toosimplify hello 로그인 환경을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9bbae-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="9bbae-127">사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="9bbae-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="9bbae-128">Azure AD에서 도메인 관리 개념 알아보기</span><span class="sxs-lookup"><span data-stu-id="9bbae-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

