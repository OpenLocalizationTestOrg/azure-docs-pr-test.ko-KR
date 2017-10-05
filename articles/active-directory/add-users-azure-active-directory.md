---
title: "Azure Active Directory에 새 사용자 추가 | Microsoft Docs"
description: "Azure Active Directory에서 새 사용자를 추가하는 방법을 설명합니다."
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
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="f1925-103">빠른 시작: Azure Active Directory에 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="f1925-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="f1925-104">이 문서에서는 Azure Porta을 사용하거나 온-프레미스 Windows Server AD 사용자 계정 데이터를 동기화하여 한 번에 하나씩 Azure AD(Azure Active Directory)에서 조직에 새 사용자를 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="f1925-105">클라우드 기반 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="f1925-105">Add cloud-based users</span></span>
1. <span data-ttu-id="f1925-106">디렉터리에 대한 전역 관리자인 계정으로 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="f1925-107">**Azure Active Directory**를 선택한 후 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="f1925-108">**사용자 및 그룹** 블레이드에서 **모든 사용자**를 선택한 다음 **새 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="f1925-109">![추가 명령 선택](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="f1925-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="f1925-110">**이름** 및 **사용자 이름**과 같은 사용자에 대한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="f1925-111">사용자 이름의 도메인 이름 부분은 초기 기본 도메인 이름 "[domain name].onmicrosoft.com" 또는 "contoso.com"과 같은 확인된 페더레이션되지 않은 [사용자 지정 도메인 이름](add-custom-domain.md)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="f1925-112">이 프로세스가 완료된 후 사용자에게 제공할 수 있도록 복사하거나 그렇지 않은 경우 생성된 사용자 암호를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="f1925-113">필요에 따라 **프로필** 블레이드, **그룹** 블레이드 또는 사용자에 대한 **디렉터리 역할** 블레이드의 정보를 열고 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="f1925-114">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1925-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="f1925-115">**사용자** 블레이드에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="f1925-116">사용자가 로그인할 수 있도록 새 사용자에게 생성된 암호를 안전하게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="f1925-117">또한 온-프레미스 Windows Server AD에서 사용자 계정 데이터를 동기화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="f1925-118">Microsoft의 ID 솔루션은 온-프레미스 및 클라우드 기반 기능을 확장하며 이는 위치에 관계 없이 모든 리소스에 인증 및 권한 부여에 대한 단일 사용자 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="f1925-119">하이브리드 ID라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="f1925-120">하이브리드 ID 시나리오에서는 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)를 사용하여 온-프레미스 디렉터리를 Azure Active Directory에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="f1925-121">이렇게 하면 Azure AD와 통합된 Office 365, Azure 및 SaaS 응용 프로그램 사용자를 위한 공통 ID를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="f1925-122">Azure AD에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="f1925-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="f1925-123">디렉터리에 대한 전역 관리자인 계정으로 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="f1925-124">**사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="f1925-125">**사용자 및 그룹** 블레이드의 목록에서 삭제할 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="f1925-126">선택한 사용자에 대한 블레이드에서 **개요**를 선택한 다음 명령 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="f1925-127">![추가 명령 선택](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="f1925-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="f1925-128">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f1925-128">Learn more</span></span> 
* [<span data-ttu-id="f1925-129">외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="f1925-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="f1925-130">Azure AD의 역할에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f1925-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="f1925-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1925-131">Next steps</span></span>
<span data-ttu-id="f1925-132">이 빠른 시작에서는 Azure AD Premium에 새 사용자를 추가하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="f1925-133">다음 링크를 사용하여 Azure Portal에서 Azure AD에 새로운 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1925-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1925-134">Azure AD에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="f1925-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 