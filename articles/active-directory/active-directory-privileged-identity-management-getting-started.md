---
title: "Azure AD Privileged Identity Management 시작 | Microsoft Docs"
description: "Azure 포털에서 Azure Active Directory Privileged Identity Management 응용 프로그램을 사용하여 권한 있는 ID를 관리하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="7fd76-103">Azure AD Privileged Identity Management 시작</span><span class="sxs-lookup"><span data-stu-id="7fd76-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7fd76-104">Azure Active Directory(AD) Privileged Identity Management를 사용하여 조직 내에서 액세스를 관리, 제어 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="7fd76-105">여기에는 Azure AD 및 다른 Microsoft 온라인 서비스(예: Office 365 또는 Microsoft Intune)의 리소스에 대한 액세스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="7fd76-106">이 문서에서는 Azure AD PIM 앱을 Azure 포털 대시보드에 추가하는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="7fd76-107">Privileged Identity Management 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="7fd76-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="7fd76-108">Azure AD Privileged Identity Management를 사용하기 전에 응용 프로그램을 Azure 포털 대시보드에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="7fd76-109">해당 디렉터리의 전역 관리자로 [Azure 포털](https://portal.azure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="7fd76-110">조직에 둘 이상의 디렉터리가 있는 경우 Azure 포털의 오른쪽 위에서 사용자 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="7fd76-111">PIM을 사용할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="7fd76-112">**더 많은 서비스**를 선택하고 [필터] 텍스트 상자를 사용하여 **Azure AD Privileged Identity Management**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="7fd76-113">**대시보드에 고정** 옵션을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="7fd76-114">Privileged Identity Management 응용 프로그램이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="7fd76-115">디렉터리에서 Azure AD Privileged Identity Management를 사용하는 첫 번째 사용자인 경우 디렉터리에 **보안 관리자** 및 **권한 있는 역할 관리자** 역할이 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="7fd76-116">권한 있는 역할 관리자만 사용자의 역할 할당을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="7fd76-117">또한 [보안 마법사](active-directory-privileged-identity-management-security-wizard.md)를 실행하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="7fd76-118">초기 검색 및 할당 경험을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="7fd76-119">태스크로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-119">Navigate to your tasks</span></span>
<span data-ttu-id="7fd76-120">Azure AD Privileged Identity Management를 설정하면 응용 프로그램을 열 때마다 탐색 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="7fd76-121">이 블레이드를 사용하여 사용자 ID 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-121">Use this blade to accomplish your identity management tasks.</span></span>

![PIM의 최상위 태스크 - 스크린샷](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="7fd76-123">**내 역할**은 자신에게 할당된 역할 목록으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="7fd76-124">이 섹션은 자격이 있는 모든 역할을 활성화하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="7fd76-125">**요청 승인(미리 보기)**은 디렉터리에 있는 사용자의 보류 중인 활성화 요청 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="7fd76-126">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7fd76-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="7fd76-127">**보류 중인 요청(미리 보기)**은 현재 활성화된 요청을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="7fd76-128">**액세스 검토**를 사용하면 자신 또는 다른 사용자에 대한 액세스를 검토하는지와 관계 없이 완료해야 하는 보류 중인 액세스 검토로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="7fd76-129">'관리' 섹션 아래에 있는 **Azure AD 디렉터리 역할**은 권한 있는 역할 관리자가 역할 할당을 관리하고, 역할 활성화 설정을 변경하고, 액세스 검토를 시작하는 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="7fd76-130">이 대시보드에서의 옵션은 권한 있는 역할 관리자가 아닌 사용자에게 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd76-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7fd76-131">Next steps</span></span>
<span data-ttu-id="7fd76-132">[Azure AD Privileged Identity Management 개요](active-directory-privileged-identity-management-configure.md) 에는 조직의 관리 액세스 권한을 관리할 수 있는 방법에 대한 자세한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fd76-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
