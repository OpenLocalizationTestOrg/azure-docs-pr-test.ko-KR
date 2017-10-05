---
title: "Azure Active Directory의 디렉터리에서 사용자 삭제 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 및 모든 해당 정보를 삭제하는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bd1c9ccc-2d80-42bf-82cc-db37bb1a1d67
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: 19a4d2c37c785b3b56a2e0e1b6797ec56dad9835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-user-from-a-directory-in-azure-active-directory"></a><span data-ttu-id="54ae0-103">Azure Active Directory의 디렉터리에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="54ae0-103">Delete a user from a directory in Azure Active Directory</span></span>
<span data-ttu-id="54ae0-104">이 문서는 Azure AD(Azure Active Directory)의 디렉터리에서 사용자를 삭제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-104">This article explains how to delete a user from a directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="54ae0-105">조직에 새 사용자 추가에 대한 자세한 내용은 [Azure Active Directory에 새 사용자 추가](active-directory-users-create-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54ae0-105">For information about adding new users to your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="to-delete-a-user"></a><span data-ttu-id="54ae0-106">사용자를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="54ae0-106">To delete a user</span></span>
1. <span data-ttu-id="54ae0-107">디렉터리에 대한 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-107">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="54ae0-108">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-users-delete-user-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="54ae0-110">**사용자 및 그룹** 블레이드에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-110">On the **Users and groups** blade, select **Users**.</span></span>

   ![사용자 블레이드 열기](./media/active-directory-users-delete-user-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="54ae0-112">**사용자 및 그룹 - 사용자** 블레이드의 목록에서 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-112">On the **Users and groups - Users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="54ae0-113">선택한 사용자에 대한 블레이드에서 **개요**를 선택한 다음 명령 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54ae0-113">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![삭제 명령 선택](./media/active-directory-users-delete-user-azure-portal/create-users-delete-command.png)

## <a name="next-steps"></a><span data-ttu-id="54ae0-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54ae0-115">Next steps</span></span>
* [<span data-ttu-id="54ae0-116">Azure Active Directory에 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="54ae0-116">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="54ae0-117">Azure Active Directory에서 사용자 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="54ae0-117">Reset the password for a user in Azure Active Directory</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="54ae0-118">Azure Active Directory에서 관리자 역할에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="54ae0-118">Assign a user to administrator roles in Azure Active Directory</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="54ae0-119">Azure Active Directory에서 사용자에 대한 프로필 정보 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="54ae0-119">Add or change profile information for a user in Azure Active Directory</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="54ae0-120">Azure Active Directory의 디렉터리에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="54ae0-120">Delete a user from a directory in Azure Active Directory</span></span>](active-directory-users-profile-azure-portal.md)
