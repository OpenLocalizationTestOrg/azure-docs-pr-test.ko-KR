---
title: "역할을 활성화하거나 비활성화하는 방법 | Microsoft Docs"
description: "Azure Privileged Identity Management 응용 프로그램을 사용하여 권한 있는 ID에 대한 역할을 활성화하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a143fd78eae52fda0cbadb7e74fd8209f24629a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-activate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9ff37-103">Azure AD Privileged Identity Management 역할을 활성화하거나 비활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff37-103">How to activate or deactivate roles in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9ff37-104">Azure AD(Active Directory) Privileged Identity Management를 사용하면 기업이 Azure AD 및 기타 Microsoft Online Services(Office 365 또는 Microsoft Intune 등)에서 권한 있는 리소스에 대한 액세스를 관리하는 방법을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="9ff37-105">관리 역할에 대해 적격이 되었다면 권한이 필요한 작업을 수행해야 하는 경우 해당 역할을 활성화할 수 있다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform privileged actions.</span></span> <span data-ttu-id="9ff37-106">예를 들어 경우에 따라 Office 365 기능을 관리하는 경우 조직의 권한 있는 역할 관리자는 해당 역할이 다른 서비스에도 또한 영향을 주므로 사용자를 영구적인 전역 관리자로 만들지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="9ff37-107">대신 Exchange Online 관리자와 같은 Azure AD 역할에 대한 자격을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="9ff37-108">이러한 권한이 필요한 경우 해당 역할을 활성화하도록 요청하고 미리 결정된 기간 동안 제어할 수 있는 관리자 권한을 부여받습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-108">You can request to activate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span></span>

<span data-ttu-id="9ff37-109">이 문서는 Azure AD PIM(Privileged Identity Management)에서 해당 역할을 활성화해야 하는 관리자를 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-109">This article is for admins who need to activate their role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="9ff37-110">사용 권한이 필요할 때 역할을 활성화하고 완료 시 역할을 비활성화하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-110">It walks you through the steps to activate a role when you need the permissions, and deactivate the role when you're done.</span></span> <span data-ttu-id="9ff37-111">또한 권한 있는 역할 관리자가 역할(미리 보기)을 활성화하는 데 승인이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-111">In addition, privileged role administrators can require approval to activate a role (Preview).</span></span> <span data-ttu-id="9ff37-112">[PIM 승인 워크플로](./privileged-identity-management/azure-ad-pim-approval-workflow.md)에 대한 자세한 내용은 여기를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff37-112">Learn more about [PIM Approval Workflows](./privileged-identity-management/azure-ad-pim-approval-workflow.md) here.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="9ff37-113">Privileged Identity Management 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="9ff37-113">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="9ff37-114">다른 포털 또는 PowerShell에서 작동하려는 경우에도 [Azure 포털](https://portal.azure.com/) 에서 Azure AD Privileged Identity Management 응용 프로그램을 사용하여 역할 활성화를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-114">Use the Azure AD Privileged Identity Management application in the [Azure portal](https://portal.azure.com/) to request a role activation, even if you're going to operate in another portal or PowerShell.</span></span> <span data-ttu-id="9ff37-115">Azure 포털에 Azure AD Privileged Identity Management 응용 프로그램이 없는 경우 다음 단계에 따라 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-115">If you don't have the Azure AD Privileged Identity Management application on your Azure portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="9ff37-116">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9ff37-117">Azure 포털의 오른쪽 위에서 사용자 이름을 선택하고 작동할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-117">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="9ff37-118">**더 많은 서비스**를 선택하고 [필터] 텍스트 상자를 사용하여 **Azure AD Privileged Identity Management**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-118">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="9ff37-119">**대시보드에 고정** 옵션을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-119">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="9ff37-120">Privileged Identity Management 응용 프로그램이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-120">The Privileged Identity Management application opens.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="9ff37-121">역할 활성화</span><span class="sxs-lookup"><span data-stu-id="9ff37-121">Activate a role</span></span>
<span data-ttu-id="9ff37-122">역할을 사용해야 하는 경우 Azure AD Privileged Identity Management 응용 프로그램의 왼쪽 탐색 열에서 **My Roles**(내 역할) 탐색 옵션을 선택하여 활성화를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-122">When you need to take on a role, you can request activation by selecting the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="9ff37-123">[Azure 포털](https://portal.azure.com/) 에 로그인하고 Azure AD Privileged Identity Management 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-123">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="9ff37-124">**My Roles**(내 역할)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-124">Select **My Roles**.</span></span> <span data-ttu-id="9ff37-125">페이지 맨 위에 있는 그룹화에 할당된 적격 역할 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-125">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="9ff37-126">활성화할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-126">Select a role to activate.</span></span>
4. <span data-ttu-id="9ff37-127">**활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-127">Select **Activate**.</span></span> <span data-ttu-id="9ff37-128">**역할 활성화 요청** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-128">The **Request role activation** blade appears.</span></span>
5. <span data-ttu-id="9ff37-129">일부 역할은 Multi-factor Authentication (MFA)가 있어야 역할을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-129">Some roles require Multi-Factor Authentication (MFA) before you can activate the role.</span></span> <span data-ttu-id="9ff37-130">세션당 한 번만 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-130">You only have to authenticate once per session.</span></span>
   
    ![역할 활성화 전에 MFA 사용하여 확인합니다 - 스크린샷][2]
6. <span data-ttu-id="9ff37-132">텍스트 필드에 활성화 요청 이유를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-132">Enter the reason for the activation request in the text field.</span></span>  <span data-ttu-id="9ff37-133">일부 역할은 문제 티켓 번호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-133">Some roles require you to supply a trouble ticket number.</span></span>
7. <span data-ttu-id="9ff37-134">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-134">Select **OK**.</span></span>  <span data-ttu-id="9ff37-135">역할에서 승인을 요청하지 않는 경우 역할이 활성화된 상태이며 해당 역할이 활성 역할 목록(적격 역할 할당 목록 바로 아래)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-135">If the role does not require approval, it is now activated, and the role appears in the list of active roles (directly below the list of eligible role assignments).</span></span> <span data-ttu-id="9ff37-136">[역할에서 활성화하는 데 승인이 필요](./privileged-identity-management/azure-ad-pim-approval-workflow.md)한 경우 요청이 승인 보류 중임을 알려주는 알림 메시지가 브라우저 오른쪽 상단 모서리에 간단하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-136">If the [role requires approval](./privileged-identity-management/azure-ad-pim-approval-workflow.md) to activate, a toast notification will briefly appear in the upper right-hand corner of your browser informing you the request is pending approval.</span></span>

    ![보류 중인 요청 알림 - 스크린샷][3]

## <a name="deactivate-a-role"></a><span data-ttu-id="9ff37-138">역할 비활성화</span><span class="sxs-lookup"><span data-stu-id="9ff37-138">Deactivate a role</span></span>
<span data-ttu-id="9ff37-139">역할이 활성화된 후 시간 제한(적격 기간)에 도달하면 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-139">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span></span>

<span data-ttu-id="9ff37-140">먼저 관리 작업을 완료한 경우 Azure AD Privileged Identity Management 응용 프로그램에서 수동으로 역할을 비활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-140">If you complete your admin tasks early, you can also deactivate a role manually in the Azure AD Privileged Identity Management application.</span></span>  <span data-ttu-id="9ff37-141">**My Roles**(내 역할)를 선택하고, **Active role assignments**(활성 역할 할당) 그룹화에서 사용이 완료된 역할을 선택하고, **비활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-141">Select **My Roles**, choose the role you're done using from the **Active role assignments** grouping, and select **Deactivate**.</span></span>  

## <a name="cancel-a-pending-request"></a><span data-ttu-id="9ff37-142">보류 중인 요청 취소</span><span class="sxs-lookup"><span data-stu-id="9ff37-142">Cancel a pending request</span></span>
<span data-ttu-id="9ff37-143">승인이 필요한 역할을 활성화할 필요가 없는 경우 언제든 보류 중인 요청을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-143">In the event you do not require activation of a role that requires approval, you may cancel a pending request at any time.</span></span> <span data-ttu-id="9ff37-144">Azure AD Privileged Identity Management 응용 프로그램의 왼쪽 탐색 열에서 **My Roles**(내 역할) 탐색 옵션을 선택하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-144">Simply select the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="9ff37-145">[Azure 포털](https://portal.azure.com/) 에 로그인하고 Azure AD Privileged Identity Management 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-145">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="9ff37-146">**My Roles**(내 역할)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-146">Select **My Roles**.</span></span> <span data-ttu-id="9ff37-147">페이지 맨 위에 있는 그룹화에 할당된 적격 역할 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-147">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="9ff37-148">원하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-148">Select a role.</span></span>
4. <span data-ttu-id="9ff37-149">역할 활성화 세부 정보 블레이드에서 **Activation is pending approval**(활성화가 승인 보류 중임) 배너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-149">Select the **Activation is pending approval** banner on the role activation details blade.</span></span>
5. <span data-ttu-id="9ff37-150">**보류 중인 승인** 블레이드 맨 위에서 **취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff37-150">Select **Cancel** at the top of the **Pending approval** blade.</span></span>

   ![보류 중인 요청 취소 스크린샷][4]

## <a name="next-steps"></a><span data-ttu-id="9ff37-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ff37-152">Next steps</span></span>
<span data-ttu-id="9ff37-153">Azure AD Privileged Identity Management에 대한 자세한 정보는 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff37-153">If you're interested in learning more about Azure AD Privileged Identity Management, the following links have more information.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
