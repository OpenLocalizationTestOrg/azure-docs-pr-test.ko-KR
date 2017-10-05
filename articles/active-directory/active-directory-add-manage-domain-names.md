---
title: "Azure Active Directory에서 사용자 지정 도메인 이름 관리 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 지정 도메인에 대한 관리 개념 및 관리 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="16435-103">Azure Active Directory에서 사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="16435-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="16435-104">도메인 이름은 다음의 일부로 많은 디렉터리 리소스에 대한 중요한 식별자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="16435-105">사용자 이름 또는 사용자에 대한 전자 메일 주소</span><span class="sxs-lookup"><span data-stu-id="16435-105">A user name or email address for a user</span></span>
* <span data-ttu-id="16435-106">그룹에 대한 주소</span><span class="sxs-lookup"><span data-stu-id="16435-106">The address for a group</span></span>
* <span data-ttu-id="16435-107">응용 프로그램에 대한 앱 ID URI</span><span class="sxs-lookup"><span data-stu-id="16435-107">The app ID URI for an application</span></span>

<span data-ttu-id="16435-108">Azure AD(Azure Active Directory)의 리소스는 리소스를 포함하는 디렉터리가 소유하는 이미 확인된 도메인 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="16435-109">전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16435-110">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="16435-111">Azure AD 관리 센터에서 도메인 이름을 관리하는 방법은 [Azure Active Directory에서 사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16435-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="16435-112">Azure AD 디렉터리에 대한 주 도메인 이름 설정</span><span class="sxs-lookup"><span data-stu-id="16435-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="16435-113">디렉터리를 만든 경우 'contoso.onmicrosoft.com'과 같은 초기 도메인 이름은 디렉터리에 대한 주 도메인 이름이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="16435-114">[Azure 클래식 포털](https://manage.windowsazure.com/)또는 Office 365 관리자 포털 등 다른 포털에 새 사용자를 만들 때 주 도메인은 새 사용자에 대한 기본 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="16435-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="16435-115">관리자에 대한 프로세스를 간소화하여 포털에 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16435-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="16435-116">디렉터리에 대한 주 도메인 이름을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="16435-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="16435-117">Azure AD 디렉터리의 전역 관리자인 사용자 계정으로 [Azure 클래식 포털](https://manage.windowsazure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="16435-118">왼쪽 탐색 모음에서 **Active Directory** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="16435-119">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16435-119">Open your directory.</span></span>
4. <span data-ttu-id="16435-120">**도메인** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="16435-121">명령 모음에서 **기본 변경** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="16435-122">디렉터리에 대한 새 주 도메인으로 지정할 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="16435-123">페더레이션되지 않은 모든 확인된 사용자 지정 도메인이 되도록 디렉터리에 대한 주 도메인 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="16435-124">디렉터리에 대한 주 도메인을 변경해도 기존 사용자에 대한 사용자 이름은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="16435-125">Azure AD에 사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="16435-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="16435-126">각 Azure AD 디렉터리에 최대 900개의 사용자 지정 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="16435-127">[추가 사용자 지정 도메인 이름을 추가](active-directory-add-domain.md) 하는 프로세스는 첫 번째 사용자 지정 도메인 이름에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="16435-128">사용자 지정 도메인의 하위 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="16435-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="16435-129">디렉터리에 'europe.contoso.com'과 같은 세 번째 수준 도메인 이름을 추가하려면 먼저 contoso.com과 같은 두 번째 수준 도메인을 추가 및 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="16435-130">Azure AD에서 자동으로 하위 도메인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="16435-131">방금 추가한 하위 도메인이 확인되었는지 보려면 디렉터리의 도메인을 나열하는 브라우저의 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="16435-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="16435-132">사용자 지정 도메인 이름의 DNS 등록 기관을 변경하는 경우 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="16435-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="16435-133">사용자 지정 도메인 이름을 위해 DNS 등록 기관을 변경할 경우 추가 구성 작업 및 중단 없이 Azure AD 자체로 사용자 지정 도메인 이름을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="16435-134">Office 365, Intune 또는 Azure AD의 사용자 지정 도메인 이름을 사용하는 다른 서비스에서 사용자 지정 도메인 이름을 사용하는 경우 해당 서비스에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16435-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="16435-135">사용자 지정 도메인 이름 삭제</span><span class="sxs-lookup"><span data-stu-id="16435-135">Delete a custom domain name</span></span>
<span data-ttu-id="16435-136">조직이 더 이상 해당 도메인 이름을 사용하지 않는 경우 또는 다른 Azure AD와 해당 도메인 이름을 사용해야 하는 경우, Azure AD에서 사용자 지정 도메인 이름을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="16435-137">사용자 지정 도메인 이름을 삭제하려면 먼저 디렉터리에 도메인 이름을 사용하는 리소스가 없는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="16435-138">다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="16435-139">임의 사용자가 도메인 이름을 포함하는 사용자 이름, 메일 주소 또는 프록시 주소 사용</span><span class="sxs-lookup"><span data-stu-id="16435-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="16435-140">임의 그룹이 도메인 이름을 포함하는 메일 주소 또는 프록시 주소 사용</span><span class="sxs-lookup"><span data-stu-id="16435-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="16435-141">Azure AD의 임의 응용 프로그램이 도메인 이름을 포함하는 앱 ID URI 사용</span><span class="sxs-lookup"><span data-stu-id="16435-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="16435-142">사용자 지정 도메인 이름을 삭제하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 변경 또는 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16435-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="16435-143">PowerShell 또는 Graph API를 사용하여 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="16435-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="16435-144">Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16435-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="16435-145">PowerShell을 사용하여 Azure AD에서 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="16435-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="16435-146">Graph API를 사용하여 Azure AD에서 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="16435-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="16435-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16435-147">Next steps</span></span>
* [<span data-ttu-id="16435-148">Azure AD에서 도메인 이름에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="16435-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="16435-149">사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="16435-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

