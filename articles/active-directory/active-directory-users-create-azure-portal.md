---
title: "Azure Active Directory에 새 사용자 추가 | Microsoft Docs"
description: "Azure Active Directory에서 새 사용자를 추가하거나 사용자 정보를 변경하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="8b7f9-103">Azure Active Directory에 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8b7f9-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b7f9-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8b7f9-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="8b7f9-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="8b7f9-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="8b7f9-106">이 문서에서는 Azure AD(Azure Active Directory)에서 새 사용자를 조직에 추가하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="8b7f9-107">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8b7f9-108">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 및 그룹 열기](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="8b7f9-110">**사용자 및 그룹** 블레이드에서 **모든 사용자**를 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![추가 명령 선택](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="8b7f9-112">**이름** 및 **사용자 이름**과 같은 사용자에 대한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="8b7f9-113">사용자 이름의 도메인 이름 부분은 초기 기본 도메인 이름 "foo.onmicrosoft.com" 도메인 이름 또는 "contoso.com"과 같은 확인된 페더레이션되지 않은 도메인 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="8b7f9-114">이 프로세스가 완료된 후 사용자에게 제공할 수 있도록 복사하거나 그렇지 않은 경우 생성된 사용자 암호를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="8b7f9-115">필요에 따라 **프로필** 블레이드, **그룹** 블레이드 또는 사용자에 대한 **디렉터리 역할** 블레이드의 정보를 열고 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="8b7f9-116">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="8b7f9-117">**사용자** 블레이드에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="8b7f9-118">사용자가 로그인할 수 있도록 새 사용자에게 생성된 암호를 안전하게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f9-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="8b7f9-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b7f9-119">Next steps</span></span>
* [<span data-ttu-id="8b7f9-120">외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8b7f9-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="8b7f9-121">새 Azure 포털에서 사용자의 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="8b7f9-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="8b7f9-122">사용자의 작업 정보 변경</span><span class="sxs-lookup"><span data-stu-id="8b7f9-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="8b7f9-123">사용자 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="8b7f9-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="8b7f9-124">Azure AD에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="8b7f9-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="8b7f9-125">Azure AD의 역할에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8b7f9-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
