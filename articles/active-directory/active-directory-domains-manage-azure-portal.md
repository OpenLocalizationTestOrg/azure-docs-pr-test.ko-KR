---
title: "Azure Active Directory에서 사용자 지정 도메인 이름 관리 | Microsoft Docs"
description: "Azure Active Directory에서 도메인 이름 관리에 대한 관리 개념 및 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 402c1be07b8ee885ee5341128fb3f419611b924d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="7ebcd-103">Azure Active Directory에서 사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="7ebcd-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="7ebcd-104">도메인 이름은 많은 디렉터리 리소스에 대한 식별자의 중요한 부분입니다. 사용자의 경우 사용자 이름 또는 메일 주소 부분이고 그룹의 경우 주소 부분이며 응용 프로그램의 경우 앱 ID URI 부분일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="7ebcd-105">Azure AD(Azure Active Directory)의 리소스는 리소스를 포함하는 디렉터리가 소유하는 이미 확인된 도메인 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource.</span></span> <span data-ttu-id="7ebcd-106">전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="7ebcd-107">Azure AD 디렉터리에 대한 주 도메인 이름 설정</span><span class="sxs-lookup"><span data-stu-id="7ebcd-107">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="7ebcd-108">디렉터리를 만든 경우 'contoso.onmicrosoft.com'과 같은 초기 도메인 이름은 주 도메인 이름이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span></span> <span data-ttu-id="7ebcd-109">주 도메인은 새 사용자를 만들 때 새 사용자에 대한 기본 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-109">The primary domain is the default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="7ebcd-110">주 도메인 이름을 설정하면 관리자에 대한 프로세스를 간소화하여 포털에 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-110">Setting a primary domain name streamlines the process for an administrator to create new users in the portal.</span></span> <span data-ttu-id="7ebcd-111">주 도메인 이름을 변경하려면:</span><span class="sxs-lookup"><span data-stu-id="7ebcd-111">To change the primary domain name:</span></span>

1. <span data-ttu-id="7ebcd-112">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-112">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7ebcd-113">**더 많은 서비스**를 선택하고 텍스트 상자에서 **Azure Active Directory**를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-113">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="7ebcd-115">***디렉터리-이름*** 블레이드에서 **도메인 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-115">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="7ebcd-116">***디렉터리 이름* - 도메인 이름** 블레이드에서 주 도메인 이름을 만들려는 도메인 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-116">On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.</span></span>
5. <span data-ttu-id="7ebcd-117">***도메인 이름*** 블레이드(즉, 제목에 새 도메인 이름이 있는 것을 여는 블레이드)에서 **Make primary** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-117">On the ***domain name*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command.</span></span> <span data-ttu-id="7ebcd-118">메시지가 표시되면 선택을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-118">Confirm your choice when prompted.</span></span>
   
   ![주 도메인 이름 만들기](./media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="7ebcd-120">페더레이션되지 않은 모든 확인된 사용자 지정 도메인이 되도록 디렉터리에 대한 주 도메인 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-120">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="7ebcd-121">디렉터리에 대한 주 도메인을 변경해도 기존 사용자에 대한 사용자 이름은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-121">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="7ebcd-122">Azure AD에 사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="7ebcd-122">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="7ebcd-123">각 Azure AD 디렉터리에 최대 900개의 사용자 지정 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-123">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="7ebcd-124">[추가 사용자 지정 도메인 이름을 추가](add-custom-domain.md) 하는 프로세스는 첫 번째 사용자 지정 도메인 이름에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-124">The process to [add an additional custom domain name](add-custom-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="7ebcd-125">사용자 지정 도메인의 하위 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="7ebcd-125">Add subdomains of a custom domain</span></span>
<span data-ttu-id="7ebcd-126">디렉터리에 'europe.contoso.com'과 같은 세 번째 수준 도메인 이름을 추가하려면 먼저 contoso.com과 같은 두 번째 수준 도메인을 추가 및 확인해야 합니다. Azure AD에서 자동으로 하위 도메인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-126">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com. The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="7ebcd-127">방금 추가한 하위 도메인이 확인되었는지 보려면 도메인을 나열하는 브라우저의 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-127">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="7ebcd-128">사용자 지정 도메인 이름의 DNS 등록 기관을 변경하는 경우 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="7ebcd-128">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="7ebcd-129">사용자 지정 도메인 이름을 위해 DNS 등록 기관을 변경할 경우 추가 구성 작업 및 중단 없이 Azure AD 자체로 사용자 지정 도메인 이름을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-129">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="7ebcd-130">Office 365, Intune 또는 Azure AD의 사용자 지정 도메인 이름을 사용하는 다른 서비스에서 사용자 지정 도메인 이름을 사용하는 경우 해당 서비스에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-130">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="7ebcd-131">사용자 지정 도메인 이름 삭제</span><span class="sxs-lookup"><span data-stu-id="7ebcd-131">Delete a custom domain name</span></span>
<span data-ttu-id="7ebcd-132">조직이 더 이상 해당 도메인 이름을 사용하지 않는 경우 또는 다른 Azure AD와 해당 도메인 이름을 사용해야 하는 경우, Azure AD에서 사용자 지정 도메인 이름을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-132">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="7ebcd-133">사용자 지정 도메인 이름을 삭제하려면 먼저 디렉터리에 도메인 이름을 사용하는 리소스가 없는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-133">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="7ebcd-134">다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-134">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="7ebcd-135">임의 사용자가 도메인 이름을 포함하는 사용자 이름, 메일 주소 또는 프록시 주소 사용</span><span class="sxs-lookup"><span data-stu-id="7ebcd-135">Any user has a user name, email address, or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="7ebcd-136">임의 그룹이 도메인 이름을 포함하는 메일 주소 또는 프록시 주소 사용</span><span class="sxs-lookup"><span data-stu-id="7ebcd-136">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="7ebcd-137">Azure AD의 임의 응용 프로그램이 도메인 이름을 포함하는 앱 ID URI 사용</span><span class="sxs-lookup"><span data-stu-id="7ebcd-137">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="7ebcd-138">사용자 지정 도메인 이름을 삭제하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 변경 또는 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-138">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="7ebcd-139">PowerShell 또는 Graph API를 사용하여 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="7ebcd-139">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="7ebcd-140">Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ebcd-140">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="7ebcd-141">PowerShell을 사용하여 Azure AD에서 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="7ebcd-141">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="7ebcd-142">Graph API를 사용하여 Azure AD에서 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="7ebcd-142">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="7ebcd-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ebcd-143">Next steps</span></span>
* [<span data-ttu-id="7ebcd-144">사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="7ebcd-144">Add custom domain names</span></span>](add-custom-domain.md)

