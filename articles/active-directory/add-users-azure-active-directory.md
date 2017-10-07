---
title: "aaaAdd 새 사용자 tooAzure Active Directory | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd Azure Active Directory에 새 사용자입니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="e3ee7-103">빠른 시작: 새로운 사용자가 tooAzure Active Directory를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="e3ee7-104">이 문서는 어떻게 hello Azure Active Directory (Azure AD)에서 조직 내에서 새 사용자 tooadd hello Azure 포털을 사용 하 여 한 번에 또는 온-프레미스 Windows Server AD 사용자를 동기화 하 여 계정 데이터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="e3ee7-105">클라우드 기반 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e3ee7-105">Add cloud-based users</span></span>
1. <span data-ttu-id="e3ee7-106">Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e3ee7-107">**Azure Active Directory**를 선택한 후 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="e3ee7-108">Hello에 **사용자 및 그룹** 블레이드를 **모든 사용자에 게**를 선택한 후 **새 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="e3ee7-109">![Hello 추가 명령을 선택 하면](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="e3ee7-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="e3ee7-110">와 같은 hello 사용자에 대 한 세부 정보를 입력 **이름** 및 **사용자 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="e3ee7-111">hello hello 사용자 이름의 도메인 이름 부분 이어야 합니다. hello 초기 기본 도메인 이름 "[도메인 이름].onmicrosoft.com" 또는 검증 된 페더레이션 되지 않은 [사용자 지정 도메인 이름을](add-custom-domain.md) "contoso.com" 등</span><span class="sxs-lookup"><span data-stu-id="e3ee7-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="e3ee7-112">복사 또는 다른 방법 참고 hello을 제공할 수 있습니다 toohello 사용자가이 프로세스가 완료 된 후 사용자 암호를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="e3ee7-113">필요에 따라 수를 열고 hello에 hello 정보를 채울 **프로필** 블레이드, hello **그룹** 블레이드에서 또는 hello **디렉터리 역할** 블레이드 hello 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="e3ee7-114">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="e3ee7-115">Hello에 **사용자** 블레이드를 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="e3ee7-116">Hello 사용자 로그인 할 수 있도록 생성 된 hello 암호 toohello 새 사용자를 안전 하 게 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="e3ee7-117">또한 온-프레미스 Windows Server AD에서 사용자 계정 데이터를 동기화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="e3ee7-118">Microsoft의 id 솔루션에는 온-프레미스 및 클라우드 기반 기능을 위치에 관계 없이 tooall 리소스, 인증 및 권한 부여에 대 한 단일 사용자 id를 만드는 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="e3ee7-119">하이브리드 ID라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="e3ee7-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) toointegrate 사용 하는 하이브리드 id 시나리오에 대 한 Azure Active Directory와 온-프레미스 디렉터리를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="e3ee7-121">이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 사용자에 대 한 일반 id를 Azure AD와 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="e3ee7-122">Azure AD에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="e3ee7-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="e3ee7-123">Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e3ee7-124">**사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="e3ee7-125">Hello에 **사용자 및 그룹** 블레이드, hello 목록에서 선택 hello 사용자 toodelete 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="e3ee7-126">Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **개요**를 선택한 다음 hello 명령 모음에서 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="e3ee7-127">![Hello 추가 명령을 선택 하면](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="e3ee7-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="e3ee7-128">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e3ee7-128">Learn more</span></span> 
* [<span data-ttu-id="e3ee7-129">외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e3ee7-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="e3ee7-130">Azure AD에서 사용자 tooa 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="e3ee7-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3ee7-131">Next steps</span></span>
<span data-ttu-id="e3ee7-132">이 빠른 시작에서 배운 어떻게 tooadd 새 사용자 tooAzure AD Premium입니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="e3ee7-133">Hello hello Azure 포털에서에서 링크 toocreate 새 사용자를 Azure AD에서 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3ee7-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3ee7-134">사용자가 tooAzure AD 추가</span><span class="sxs-lookup"><span data-stu-id="e3ee7-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
