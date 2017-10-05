---
title: "Azure Active Directory에 사용자 지정 도메인 이름 추가 | Microsoft Docs"
description: "Azure Active Directory에 회사의 도메인 이름을 추가하는 방법 및 도메인 이름을 확인하는 방법."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: ad72f768add7edc1d34a85c27dc2aa1b4e4b3a50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-custom-domain-name-to-azure-active-directory"></a><span data-ttu-id="c63e3-103">Azure Active Directory에 사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="c63e3-103">Add a custom domain name to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c63e3-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="c63e3-104">Azure portal</span></span>](active-directory-domains-add-azure-portal.md)
> * [<span data-ttu-id="c63e3-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c63e3-105">Azure classic portal</span></span>](active-directory-add-domain.md)
> 

<span data-ttu-id="c63e3-106">Azure AD(Azure Active Directory)를 사용하면 Azure AD에도 회사 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-106">Using Azure Active Directory (Azure AD), you can add your corporate domain name to Azure AD as well.</span></span> <span data-ttu-id="c63e3-107">조직이 비즈니스를 하는 데 사용하는 도메인 이름 및 회사 도메인 이름을 사용하여 로그인하는 사용자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-107">You might have a domain names that you organization uses to do business, and users who sign in using your corporate domain name.</span></span> <span data-ttu-id="c63e3-108">Azure AD에 도메인 이름을 추가하면 사용자에게 ‘alice@contoso.com’ 같은 친숙한 사용자 이름을 디렉터리에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-108">Adding the domain name to Azure AD allows you to assign user names in the directory that are familiar to your users, such as ‘alice@contoso.com.’</span></span> <span data-ttu-id="c63e3-109">프로세스는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-109">The process is simple:</span></span>

1. <span data-ttu-id="c63e3-110">디렉터리에 사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="c63e3-110">Add the custom domain name to your directory</span></span>
2. <span data-ttu-id="c63e3-111">도메인 이름 등록 기관의 도메인 이름에 대한 DNS 항목 추가</span><span class="sxs-lookup"><span data-stu-id="c63e3-111">Add a DNS entry for the domain name at the domain name registrar</span></span>
3. <span data-ttu-id="c63e3-112">Azure AD에서 사용자 지정 도메인 이름 확인</span><span class="sxs-lookup"><span data-stu-id="c63e3-112">Verify the custom domain name in Azure AD</span></span>

## <a name="how-do-i-add-a-domain-name"></a><span data-ttu-id="c63e3-113">도메인 이름을 추가하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c63e3-113">How do I add a domain name?</span></span>
1. <span data-ttu-id="c63e3-114">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-114">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c63e3-115">**더 많은 서비스**를 선택하고 텍스트 상자에서 **Azure Active Directory**를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-115">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="c63e3-117">***디렉터리-이름*** 블레이드에서 **도메인 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-117">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="c63e3-118">***디렉터리-이름* - 도메인 이름** 블레이드에서 **추가** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-118">On the ***directory-name* - Domain names** blade, select the **Add** command.</span></span>
   
   ![추가 명령 선택](./media/active-directory-domains-add-azure-portal/add-command.png)
5. <span data-ttu-id="c63e3-120">**도메인 이름** 블레이드의 상자에서 사용자 지정 도메인 이름(예: 'contoso.com')을 입력한 다음 **도메인 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-120">On the **Domain name** blade, enter the name of your custom domain in the box, such as 'contoso.com', and then select **Add Domain**.</span></span> <span data-ttu-id="c63e3-121">.com, .net 또는 그 외 최상위 확장명을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-121">Be sure to include the .com, .net, or other top-level extension.</span></span>
6. <span data-ttu-id="c63e3-122">***domainname*** 블레이드(즉, 제목에서 새 도메인 이름으로 열린 블레이드)에서 조직이 사용자 지정 도메인 이름을 소유하고 있는지 확인하기 위해 Azure AD에서 사용할 DNS 항목 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-122">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), get the DNS entry information that Azure AD will use to verify that your organization owns the custom domain name.</span></span>
   
   ![DNS 항목 정보 가져오기](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

<span data-ttu-id="c63e3-124">이제 도메인 이름을 추가했으므로 Azure AD에서 조직이 해당 도메인 이름을 소유하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-124">Now that you've added the domain name, Azure AD must verify that your organization owns the domain name.</span></span> <span data-ttu-id="c63e3-125">Azure AD에서 이러한 확인을 수행하기 전에 도메인 이름으로 DNS 영역 파일에 포함된 DNS 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-125">Before Azure AD can perform this verification, you must add a DNS entry in the DNS zone file for the domain name.</span></span> <span data-ttu-id="c63e3-126">이 작업은 도메인 이름을 위한 도메인 이름 등록 기관의 웹 사이트에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-126">This task is performed at the website for domain name registrar for the domain name.</span></span>

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a><span data-ttu-id="c63e3-127">도메인에 대한 도메인 이름 등록 기관에 DNS 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-127">Add the DNS entry at the domain name registrar for the domain</span></span>
<span data-ttu-id="c63e3-128">사용자 지정 도메인 이름을 Azure AD로 사용하는 다음 단계에서는 도메인에 대한 DNS 영역 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-128">The next step to use your custom domain name with Azure AD is to update the DNS zone file for the domain.</span></span> <span data-ttu-id="c63e3-129">이를 통해 Azure AD에서는 조직이 사용자 지정 도메인 이름을 소유하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-129">This enables Azure AD to verify that your organization owns the custom domain name.</span></span>

1. <span data-ttu-id="c63e3-130">도메인에 대한 도메인 이름 등록 기관에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-130">Sign in to the domain name registrar for the domain.</span></span> <span data-ttu-id="c63e3-131">DNS 항목을 업데이트하기 위해 액세스할 수 없는 경우 액세스 권한이 있는 사용자 또는 팀에게 2단계를 완료하고 완료될 때를 알려주도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-131">If you don't have access to update the DNS entry, ask the person or team who has this access to complete step 2 and to let you know when it is completed.</span></span>
2. <span data-ttu-id="c63e3-132">Azure AD에서 제공되는 DNS 항목을 추가하여 도메인에 대한 DNS 영역 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-132">Update the DNS zone file for the domain by adding the DNS entry provided to you by Azure AD.</span></span> <span data-ttu-id="c63e3-133">이러한 DNS 항목을 통해 Azure AD에서 도메인에 대한 소유권을 확인할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-133">This DNS entry enables Azure AD to verify your ownership of the domain.</span></span> <span data-ttu-id="c63e3-134">DNS 항목은 메일 라우팅이나 웹 호스팅 같은 어떠한 동작도 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-134">The DNS entry doesn't change any behaviors such as mail routing or web hosting.</span></span>

<span data-ttu-id="c63e3-135">DNS 항목을 추가하는 방법에 대한 도움말은 [널리 사용되는 DNS 등록 기관에서 DNS 항목을 추가하기 위한 지침](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span><span class="sxs-lookup"><span data-stu-id="c63e3-135">For help with this adding the DNS entry, read [Instructions for adding a DNS entry at popular DNS registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)</span></span>

## <a name="verify-the-domain-name-with-azure-ad"></a><span data-ttu-id="c63e3-136">Azure AD에서 도메인 이름 확인</span><span class="sxs-lookup"><span data-stu-id="c63e3-136">Verify the domain name with Azure AD</span></span>
<span data-ttu-id="c63e3-137">DNS 항목을 추가하고 나면, Azure AD에서 도메인 이름을 확인할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-137">Once you have added the DNS entry, you are ready to verify the domain name with Azure AD.</span></span>

<span data-ttu-id="c63e3-138">DNS 레코드가 전파된 후에 도메인 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-138">A domain name can be verified only after the DNS records have propagated.</span></span> <span data-ttu-id="c63e3-139">이 전파는 보통 몇 초 밖에 걸리지 않지만 한 시간 이상이 걸릴 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-139">This propagation often takes only seconds, but it can sometimes take an hour or more.</span></span> <span data-ttu-id="c63e3-140">확인이 처음에 작동하지 않으면 나중에 재시도하세요.</span><span class="sxs-lookup"><span data-stu-id="c63e3-140">If verification doesn’t work the first time, try again later.</span></span>

1. <span data-ttu-id="c63e3-141">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-141">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c63e3-142">**찾아보기**를 선택하고 텍스트 상자에서 사용자 관리를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-142">Select **Browse**, enter User Management in the text box, and then select **Enter**.</span></span>
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="c63e3-144">**사용자 관리 - 도메인 이름** 블레이드에서 확인하려는 확인되지 않은 도메인 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-144">On the **User management - Domain names** blade, select the unverified domain name that you want to verify.</span></span>
4. <span data-ttu-id="c63e3-145">***domainname*** 블레이드(즉, 제목에서 새 도메인 이름으로 열린 블레이드)에서 **확인**을 선택하여 확인을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-145">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), select **Verify** to complete the verification.</span></span>

<span data-ttu-id="c63e3-146">이제 [사용자 지정 도메인 이름을 포함하는 사용자 이름을 할당](active-directory-users-create-azure-portal.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-146">Now you can [assign user names that include your custom domain name](active-directory-users-create-azure-portal.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c63e3-147">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c63e3-147">Troubleshooting</span></span>
<span data-ttu-id="c63e3-148">사용자 지정 도메인 이름을 확인할 수 없는 경우 다음을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="c63e3-148">If you can't verify a custom domain name, try the following.</span></span> <span data-ttu-id="c63e3-149">가장 일반적인 것부터 시작하여, 가장 드문 것까지 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-149">We'll start with the most common and work down to the least common.</span></span>

1. <span data-ttu-id="c63e3-150">**한 시간을 대기합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63e3-150">**Wait an hour**.</span></span> <span data-ttu-id="c63e3-151">Azure AD가 도메인을 확인할 수 있기 전에 DNS 레코드를 전파해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-151">DNS records need to propagate before Azure AD can verify the domain.</span></span> <span data-ttu-id="c63e3-152">이 작업은 한 시간 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-152">This can take an hour or more.</span></span>
2. <span data-ttu-id="c63e3-153">**DNS 레코드를 입력하고 정확한지 확인합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63e3-153">**Ensure the DNS record was entered, and that it is correct**.</span></span> <span data-ttu-id="c63e3-154">도메인에 대한 도메인 이름 등록 기관의 웹 사이트에서 이 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-154">Complete this step at the website for the domain name registrar for the domain.</span></span> <span data-ttu-id="c63e3-155">DNS 항목을 DNS 영역 파일에 나타나지 않는 경우 또는 Azure AD에서 제공한 DNS 항목과 정확하게 일치하지 않는 경우 Azure AD는 도메인 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-155">Azure AD cannot verify the domain name if the DNS entry is not present in the DNS zone file, or if it is not an exact match with the DNS entry that Azure AD provided you.</span></span> <span data-ttu-id="c63e3-156">도메인 이름 등록 기관에서 도메인에 대한 DNS 레코드를 업데이트하기 위한 액세스 권한이 없는 경우 조직에서 이 액세스 권한이 있는 사람이나 팀과 DNS 항목을 공유하고 DNS 항목을 추가하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-156">If you do not have access to update DNS records for the domain at the domain name registrar, share the DNS entry with the person or team at your organization who has this access, and ask them to add the DNS entry.</span></span>
3. <span data-ttu-id="c63e3-157">**Azure AD에서 도메인 이름을 다른 디렉터리에서 삭제합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63e3-157">**Delete the domain name from another directory in Azure AD**.</span></span> <span data-ttu-id="c63e3-158">단일 디렉터리에서 도메인 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-158">A domain name can be verified in only a single directory.</span></span> <span data-ttu-id="c63e3-159">다른 디렉터리에서 이전에 도메인 이름을 확인한 경우 새 디렉터리에서 확인할 수 있게 되기 전에 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-159">If a domain name was previously verified in another directory, it must be deleted there before it can be verified in your new directory.</span></span> <span data-ttu-id="c63e3-160">도메인 이름을 삭제하는 방법에 대해 자세히 알아보려면 [사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-160">To learn about deleting domain names, read [Manage custom domain names](active-directory-domains-manage-azure-portal.md).</span></span>    

## <a name="add-more-custom-domain-names"></a><span data-ttu-id="c63e3-161">사용자 지정 도메인 이름 더 추가하기</span><span class="sxs-lookup"><span data-stu-id="c63e3-161">Add more custom domain names</span></span>
<span data-ttu-id="c63e3-162">조직에서 사용자 지정 도메인 이름을 여러 개 사용하는 경우(예: ‘contoso.com’ 및 ‘contosobank.com’), 최대 900개의 도메인에 해당 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-162">If your organization uses multiple custom domain names, such as ‘contoso.com’ and ‘contosobank.com’, you can add them up to a maximum of 900 domain names.</span></span> <span data-ttu-id="c63e3-163">이 문서의 동일한 단계를 사용하여 각 도메인 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c63e3-163">Use the same steps in this article to add each of your domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c63e3-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c63e3-164">Next steps</span></span>
[<span data-ttu-id="c63e3-165">사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="c63e3-165">Manage custom domain names</span></span>](active-directory-domains-manage-azure-portal.md)

