---
title: "액세스 검토를 수행하는 방법 | Microsoft Docs"
description: "Azure Privileged Identity Management 응용 프로그램을 사용하여 검토를 수행하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b67f6-103">Azure AD Privileged Identity Management의 액세스 검토를 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="b67f6-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b67f6-104">Azure AD(Active Directory) Privileged Identity Management를 사용하면 기업이 Azure AD 및 기타 Microsoft Online Services(Office 365 또는 Microsoft Intune 등)에서 권한 있는 리소스에 대한 액세스를 관리하는 방법을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="b67f6-105">관리 역할에 할당된 경우 조직의 권한 있는 역할 관리자가 작업에 해당 역할이 여전히 필요한지 정기적으로 확인하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="b67f6-106">링크가 포함된 메일을 받거나 [Azure 포털](https://portal.azure.com)로 바로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b67f6-107">할당된 역할을 자체 검토하려면 이 문서의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="b67f6-108">액세스 검토에 관심이 있는 권한 있는 역할 관리자인 경우 [액세스 검토를 시작하는 방법](active-directory-privileged-identity-management-how-to-start-security-review.md)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67f6-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="b67f6-109">Privileged Identity Management 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b67f6-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="b67f6-110">[Azure 포털](https://portal.azure.com/) 에서 Azure AD PIM(Privileged Identity Management) 응용 프로그램을 사용하여 검토를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="b67f6-111">Azure AD Privileged Identity Management 응용 프로그램이 포털에 없는 경우 다음 단계에 따라 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="b67f6-112">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b67f6-113">Azure 포털의 오른쪽 위에서 사용자 이름을 선택하고 작동할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="b67f6-114">**더 많은 서비스**를 선택하고 [필터] 텍스트 상자를 사용하여 **Azure AD Privileged Identity Management**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="b67f6-115">**대시보드에 고정** 옵션을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="b67f6-116">Privileged Identity Management 응용 프로그램이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="b67f6-117">액세스 승인 또는 거부</span><span class="sxs-lookup"><span data-stu-id="b67f6-117">Approve or deny access</span></span>
<span data-ttu-id="b67f6-118">액세스를 승인하거나 거부할 때, 단지 검토자에게 이 역할을 사용할지를 알리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="b67f6-119">역할을 유지하려면 **승인**을, 또는 더 이상 액세스를 필요로 하지 않는 경우 **거부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="b67f6-120">검토자가 결과를 적용할 때까지는 사용자의 상태가 바로 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="b67f6-121">액세스 검토를 찾아 완료하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="b67f6-122">PIM 응용 프로그램에서 **권한 있는 액세스 검토**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="b67f6-123">보류 중인 액세스 검토가 있다면 Azure AD 액세스 검토 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="b67f6-124">완료할 검토를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="b67f6-125">검토를 만들지 않은 한, 검토에서 유일한 사용자로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="b67f6-126">사용자 이름 옆에 있는 확인 표시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="b67f6-127">**승인** 또는 **거부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="b67f6-128">**이유 설명** 텍스트 상자에 결정 이유를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="b67f6-129">**Review Azure AD roles** (Azure AD 역할 검토)를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b67f6-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b67f6-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b67f6-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
