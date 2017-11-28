---
title: "Azure의 셀프 서비스 등록이란? | Microsoft Docs"
description: "Azure의 셀프 서비스 등록, 등록 프로세스 관리 방법 및 DNS 도메인 이름 인수 방법에 대한 개요입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: de8b55516ae7e19f2b42466fa4dc387b82495a5b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-self-service-signup-for-azure"></a><span data-ttu-id="4d070-104">Azure의 셀프 서비스 등록이란?</span><span class="sxs-lookup"><span data-stu-id="4d070-104">What is Self-Service Signup for Azure?</span></span>
<span data-ttu-id="4d070-105">이 항목에서는 셀프 서비스 등록 프로세스 및 DNS 도메인 이름을 인수하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-105">This topic explains the self-service signup process and how to take over a DNS domain name.</span></span>  

## <a name="why-use-self-service-signup"></a><span data-ttu-id="4d070-106">셀프 서비스 등록을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="4d070-106">Why use self-service signup?</span></span>
* <span data-ttu-id="4d070-107">고객이 원하는 서비스를 더욱 빠르게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-107">Get customers to services they want faster.</span></span>
* <span data-ttu-id="4d070-108">서비스에 대한 메일 기반 제공 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-108">Create email-based offers for a service.</span></span>
* <span data-ttu-id="4d070-109">사용자가 기억하기 쉬운 업무용 메일 별칭을 사용하여 신속하게 ID를 만들 수 있도록 하는 메일 기반 등록 플로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-109">Create email-based signup flows which quickly allow users to create identities using their easy-to-remember work email aliases.</span></span>
* <span data-ttu-id="4d070-110">관리되지 않는 Azure 디렉터리를 나중에 관리되는 디렉터리에 만들 수 있으며 다른 서비스에 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="4d070-111">용어 및 정의</span><span class="sxs-lookup"><span data-stu-id="4d070-111">Terms and Definitions</span></span>
* <span data-ttu-id="4d070-112">**셀프 서비스 등록**: 사용자가 클라우드 서비스에 등록하고 해당 메일 도메인을 기반으로 Azure AD(Active Directory)에 ID가 자동으로 생성되게 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-112">**Self-service sign up**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span></span>
* <span data-ttu-id="4d070-113">**관리되지 않는 Azure 디렉터리**: ID가 생성되는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-113">**Unmanaged Azure directory**: This is the directory where that identity is created.</span></span> <span data-ttu-id="4d070-114">관리되지 않는 디렉터리는 전역 관리자가 없는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="4d070-115">**메일로 확인된 사용자**: Azure AD의 사용자 계정의 한 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="4d070-116">셀프 서비스 제공 사항에 등록한 후 자동으로 생성된 ID를 갖는 사용자를 메일로 확인된 사용자라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="4d070-117">메일로 확인된 사용자는 creationmethod=EmailVerified로 태그가 지정된 디렉터리의 일반 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="user-experience"></a><span data-ttu-id="4d070-118">사용자 환경</span><span class="sxs-lookup"><span data-stu-id="4d070-118">User experience</span></span>
<span data-ttu-id="4d070-119">예를 들어 있는 메일이 Dan@BellowsCollege.com 인 사용자가 메일을 통해 중요한 파일을 받는다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span></span> <span data-ttu-id="4d070-120">파일은 Azure Rights Management(Azure RMS)로 보호되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-120">The files have been protected by Azure Rights Management (Azure RMS).</span></span> <span data-ttu-id="4d070-121">하지만 Dan의 조직인 Bellows College는 Azure RMS에 등록하지 않았으며 Active Directory RMS도 배포하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span></span> <span data-ttu-id="4d070-122">이 경우 Dan은 보호된 파일을 읽기 위해 개인용 RMS에 대한 무료 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-122">In this case, Dan can sign up for a free subscription to RMS for individuals in order to read the protected files.</span></span>

<span data-ttu-id="4d070-123">Dan이 이 셀프 서비스 제공 사항에 등록하는 BellowsCollege.com 메일 주소를 가진 첫 번째 사용자인 경우에는 Azure AD에서 BellowsCollege.com에 대해 관리되지 않는 디렉터리가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-123">If Dan is the first user with an email address from BellowsCollege.com to sign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span></span> <span data-ttu-id="4d070-124">BellowsCollege.com 도메인의 다른 사용자가 이 제공 사항 또는 비슷한 셀프 서비스 제공 사항에 등록하는 경우 이 사용자도 Azure에서 동일한 관리되지 않는 디렉터리에 생성된 메일로 확인된 사용자 계정을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-124">If other users from the BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in the same unmanaged directory in Azure.</span></span>

## <a name="admin-experience"></a><span data-ttu-id="4d070-125">관리자 환경</span><span class="sxs-lookup"><span data-stu-id="4d070-125">Admin experience</span></span>
<span data-ttu-id="4d070-126">관리되지 않는 Azure 디렉터리의 DNS 도메인 이름을 소유한 관리자는 소유권을 증명한 후 디렉터리를 인수하거나 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-126">An admin who owns the DNS domain name of an unmanaged Azure directory can take over or merge the directory after proving ownership.</span></span> <span data-ttu-id="4d070-127">다음 섹션에서 관리자 환경을 보다 자세히 설명하지만 요약 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-127">The next sections explain the admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="4d070-128">관리되지 않는 Azure 디렉터리를 인수하면 관리되지 않는 디렉터리의 전역 관리자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-128">When you take over an unmanaged Azure directory, you simply become the global administrator of the unmanaged directory.</span></span> <span data-ttu-id="4d070-129">이를 내부 인수라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-129">This is sometimes called an internal takeover.</span></span>
* <span data-ttu-id="4d070-130">관리되지 않는 Azure 디렉터리를 병합하고 관리되지 않는 디렉터리의 DNS 도메인 이름을 관리되는 Azure 디렉터리에 추가하여 사용자에서 리소스로 매핑되면 사용자가 중단 없이 서비스에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-130">When you merge an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory and a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="4d070-131">이를 외부 인수라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-131">This is sometimes called an external takeover.</span></span>

## <a name="what-gets-created-in-azure-active-directory"></a><span data-ttu-id="4d070-132">Azure Active Directory에 생성되는 것은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4d070-132">What gets created in Azure Active Directory?</span></span>
#### <a name="directory"></a><span data-ttu-id="4d070-133">디렉터리</span><span class="sxs-lookup"><span data-stu-id="4d070-133">directory</span></span>
* <span data-ttu-id="4d070-134">도메인에 대한 Azure Active Directory 디렉터리가 도메인당 디렉터리 하나씩 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-134">An Azure Active Directory directory for the domain is created, one directory per domain.</span></span>
* <span data-ttu-id="4d070-135">Azure AD 디렉터리에는 전역 관리자가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-135">The Azure AD directory has no global admin.</span></span>

#### <a name="users"></a><span data-ttu-id="4d070-136">사용자</span><span class="sxs-lookup"><span data-stu-id="4d070-136">Users</span></span>
* <span data-ttu-id="4d070-137">등록하는 사용자마다 Azure AD 디렉터리에 사용자 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-137">For each user who signs up, a user object is created in the Azure AD directory.</span></span>
* <span data-ttu-id="4d070-138">각 사용자 개체는 외부로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-138">Each user object is marked as external.</span></span>
* <span data-ttu-id="4d070-139">각 사용자는 등록한 서비스에 대한 액세스 권한을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-139">Each user is given access to the service that they signed up for.</span></span>

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a><span data-ttu-id="4d070-140">소유한 도메인에 대한 셀프 서비스 Azure AD 디렉터리를 어떻게 요구하나요?</span><span class="sxs-lookup"><span data-stu-id="4d070-140">How do I claim a self-service Azure AD directory for a domain I own?</span></span>
<span data-ttu-id="4d070-141">도메인 유효성 검사를 수행하여 셀프 서비스 Azure AD 디렉터리를 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-141">You can claim a self-service Azure AD directory by performing domain validation.</span></span> <span data-ttu-id="4d070-142">도메인 유효성 검사는 DNS 레코드를 만들어 도메인 소유권을 증명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-142">Domain validation proves you own the domain by creating DNS records.</span></span>

<span data-ttu-id="4d070-143">Azure AD 디렉터리의 DNS 인수를 수행하는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-143">There are two ways to do a DNS takeover of an Azure AD directory:</span></span>

* <span data-ttu-id="4d070-144">내부 인수(관리자가 관리되지 않는 Azure 디렉터리를 검색하여 관리되는 디렉터리로 바꾸려고 함)</span><span class="sxs-lookup"><span data-stu-id="4d070-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants to turn into a managed directory)</span></span>
* <span data-ttu-id="4d070-145">외부 인수(관리자가 새 도메인을 관리되는 Azure 디렉터리에 추가하려고 함)</span><span class="sxs-lookup"><span data-stu-id="4d070-145">external takeover (Admin tries to add a new domain to their managed Azure directory)</span></span>

<span data-ttu-id="4d070-146">사용자의 셀프 서비스 등록 후 관리되지 않는 디렉터리를 인수하는 중이므로 도메인 소유권을 확인하고 싶거나 관리되는 기존 디렉터리에 새 도메인을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain to an existing managed directory.</span></span> <span data-ttu-id="4d070-147">예를 들어 contoso.com이라는 이름의 도메인을 가지고 있으며 contoso.co.uk 또는 contoso.uk라는 이름의 새 도메인을 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-147">For example, you have a domain named contoso.com and you want to add a new domain named contoso.co.uk or contoso.uk.</span></span>

## <a name="what-is-domain-takeover"></a><span data-ttu-id="4d070-148">도메인 인수란?</span><span class="sxs-lookup"><span data-stu-id="4d070-148">What is domain takeover?</span></span>
<span data-ttu-id="4d070-149">이 섹션에서는 도메인 소유권을 확인하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-149">This section covers how to validate that you own a domain</span></span>

### <a name="what-is-domain-validation-and-why-is-it-used"></a><span data-ttu-id="4d070-150">도메인 유효성 검사란 무엇이며 사용해야 하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="4d070-150">What is domain validation and why is it used?</span></span>
<span data-ttu-id="4d070-151">Azure AD를 사용하여 디렉터리에서 작업을 수행하려면 DNS 도메인의 소유권이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-151">In order to perform operations on a directory, Azure AD requires that you validate ownership of the DNS domain.</span></span>  <span data-ttu-id="4d070-152">도메인의 유효성 검사를 사용하면 디렉터리를 요구하거나 셀프 서비스 디렉터리를 관리되는 디렉터리로 승격시키거나 관리되는 기존 디렉터리에 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-152">Validation of the domain allows you to claim the directory and either promote the self-service directory to a managed directory, or merge the self-service directory into an existing managed directory.</span></span>

## <a name="examples-of-domain-validation"></a><span data-ttu-id="4d070-153">도메인 유효성 검사 예</span><span class="sxs-lookup"><span data-stu-id="4d070-153">Examples of domain validation</span></span>
<span data-ttu-id="4d070-154">디렉터리의 DNS 인수를 수행하는 데는 다음 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-154">There are two ways to do a DNS takeover of a directory:</span></span>

* <span data-ttu-id="4d070-155">내부 인수(예: 관리자가 셀프 서비스와 관리되지 않는 디렉터리를 검색하여 관리되는 디렉터리로 바꾸려고 함)</span><span class="sxs-lookup"><span data-stu-id="4d070-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants to turn into managed directory)</span></span>
* <span data-ttu-id="4d070-156">외부 인수(예: 관리자가 새 도메인을 관리되는 디렉터리에 추가하려고 함)</span><span class="sxs-lookup"><span data-stu-id="4d070-156">external takeover (For example, a admin tries to add a new domain to a managed directory)</span></span>

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-to-be-a-managed-directory"></a><span data-ttu-id="4d070-157">내부 인수 - 셀프 서비스, 관리되지 않는 디렉터리를 관리되는 디렉터리로 승격</span><span class="sxs-lookup"><span data-stu-id="4d070-157">Internal Takeover - promote a self-service, unmanaged directory to be a managed directory</span></span>
<span data-ttu-id="4d070-158">내부 인수를 수행하면 관리되지 않는 디렉터리가 관리되는 디렉터리로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-158">When you do internal takeover, the directory gets converted from an unmanaged directory to a managed directory.</span></span> <span data-ttu-id="4d070-159">DNS 도메인 이름 유효성 검사를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-159">You need to complete DNS domain name validation, where you create an MX record or a TXT record in the DNS zone.</span></span> <span data-ttu-id="4d070-160">DNS 영역에 MX 레코드 또는 TXT 레코드를 만드는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-160">That action:</span></span>

* <span data-ttu-id="4d070-161">도메인 소유 확인</span><span class="sxs-lookup"><span data-stu-id="4d070-161">Validates that you own the domain</span></span>
* <span data-ttu-id="4d070-162">관리되는 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="4d070-162">Makes the directory managed</span></span>
* <span data-ttu-id="4d070-163">디렉터리의 전역 관리자가 됨</span><span class="sxs-lookup"><span data-stu-id="4d070-163">Makes you the global admin of the directory</span></span>

<span data-ttu-id="4d070-164">Bellows College의 IT 관리자가 셀프 서비스 제공 사항에 등록한 교내 사용자를 찾았다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-164">Let's say an IT administrator from Bellows College discovers that users from the school have signed up for self-service offerings.</span></span> <span data-ttu-id="4d070-165">IT 관리자는 BellowsCollege.com이란 DNS 이름의 등록된 소유자로서 Azure에서 DNS 이름의 소유권을 확인한 다음 관리되지 않는 디렉터리를 인수할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-165">As the registered owner of the DNS name BellowsCollege.com, the IT administrator can validate ownership of the DNS name in Azure and then take over the unmanaged directory.</span></span> <span data-ttu-id="4d070-166">그러면 이 디렉터리는 관리되는 디렉터리가 되며 IT 관리자에게 BellowsCollege.com 디렉터리에 대한 전역 관리자 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-166">The directory then becomes a managed directory, and the IT administrator is assigned the global administrator role for the BellowsCollege.com directory.</span></span>

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a><span data-ttu-id="4d070-167">외부 인수 - 셀프 서비스 디렉터리를 관리되는 기존 디렉터리에 병합</span><span class="sxs-lookup"><span data-stu-id="4d070-167">External Takeover - merge a self-service directory into an existing managed directory</span></span>
<span data-ttu-id="4d070-168">외부 인수의 경우 이미 관리되는 디렉터리가 있으며 두 개의 별도의 디렉터리를 소유하는 대신 관리되지 않는 디렉터리의 모든 사용자 및 그룹을 관리되는 디렉터리에 결합시키려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory to join that managed directory, rather than own two separate directories.</span></span>

<span data-ttu-id="4d070-169">관리되는 디렉터리의 관리자는 도메인을 추가하며 이 도메인은 연결된 관리되지 않는 디렉터리를 가지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-169">As an admin of a managed directory, you add a domain, and that domain happens to have an unmanaged directory associated with it.</span></span>

<span data-ttu-id="4d070-170">예를 들어 IT 관리자이며 조직에 등록된 도메인 이름인 Contoso.com의 관리되는 디렉터리를 가지고 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered to your organization.</span></span> <span data-ttu-id="4d070-171">조직의 사용자가 조직이 소유하는 또 다른 도메인 이름인 전자 메일 도메인 이름 user@contoso.co.uk를 사용하여 제품에 대한 셀프 서비스 등록을 수행한 것을 발견합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span></span> <span data-ttu-id="4d070-172">이 사용자는 현재 contoso.co.uk의 관리되지 않는 디렉터리에 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span></span>

<span data-ttu-id="4d070-173">두 개의 디렉터리를 별도로 관리하고 싶지 않으므로 contoso.co.uk의 관리되지 않는 디렉터리를 contoso.com의 IT 관리되는 기존 디렉터리에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-173">You don't want to manage two separate directories, so you merge the unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span></span>

<span data-ttu-id="4d070-174">외부 인수는 내부 인수와 동일한 DNS 유효성 검사 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-174">External takeover follows the same DNS validation process as internal takeover.</span></span>  <span data-ttu-id="4d070-175">차이: 사용자와 서비스는 IT 관리되는 디렉터리에 다시 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-175">Difference being: users and services are remapped to the IT managed directory.</span></span>

#### <a name="whats-the-impact-of-performing-an-external-takeover"></a><span data-ttu-id="4d070-176">외부 인수 수행 효과는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4d070-176">What's the impact of performing an external takeover?</span></span>
<span data-ttu-id="4d070-177">외부 인수를 통해 사용자에서 리소스로 매핑되어 사용자가 중단 없이 서비스에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-177">With an external takeover, a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="4d070-178">개인용 RMS를 포함한 많은 응용 프로그램이 사용자에서 리소스로의 매핑을 잘 처리하므로 사용자가 변경하지 않고 이러한 서비스에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-178">Many applications, including RMS for individuals, handle the mapping of users-to-resources well, and users can continue to access those services without change.</span></span> <span data-ttu-id="4d070-179">응용 프로그램이 사용자에서 리소스로의 매핑을 효과적으로 처리하지 않을 경우 외부 인수는 사용자에게 만족스러운 환경을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-179">If an application does not handle the mapping of users-to-resources effectively, external takeover may be explicitly blocked to prevent users from a poor experience.</span></span>

#### <a name="directory-takeover-support-by-service"></a><span data-ttu-id="4d070-180">디렉터리 인수 지원 서비스</span><span class="sxs-lookup"><span data-stu-id="4d070-180">directory takeover support by service</span></span>
<span data-ttu-id="4d070-181">현재 인수를 지원하는 서비스:</span><span class="sxs-lookup"><span data-stu-id="4d070-181">Currently the following services support takeover:</span></span>

* <span data-ttu-id="4d070-182">RMS</span><span class="sxs-lookup"><span data-stu-id="4d070-182">RMS</span></span>

<span data-ttu-id="4d070-183">인수를 곧 지원할 예정인 서비스:</span><span class="sxs-lookup"><span data-stu-id="4d070-183">The following services will soon be supporting takeover:</span></span>

* <span data-ttu-id="4d070-184">PowerBI</span><span class="sxs-lookup"><span data-stu-id="4d070-184">PowerBI</span></span>

<span data-ttu-id="4d070-185">다음 서비스는 외부 인수 후 사용자 데이터를 마이그레이션하기 위한 관리자 추가 작업이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-185">The following do not and require additional admin action to migrate user data after an external takeover.</span></span>

* <span data-ttu-id="4d070-186">SharePoint/OneDrive</span><span class="sxs-lookup"><span data-stu-id="4d070-186">SharePoint/OneDrive</span></span>

## <a name="how-to-perform-a-dns-domain-name-takeover"></a><span data-ttu-id="4d070-187">DNS 도메인 이름 인수를 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d070-187">How to perform a DNS domain name takeover</span></span>
<span data-ttu-id="4d070-188">도메인 유효성 검사를 수행하는 방법으로 다음과 같은 몇 가지 옵션이 있습니다(원하는 경우 인수 수행).</span><span class="sxs-lookup"><span data-stu-id="4d070-188">You have a few options for how to perform a domain validation (and do a takeover if you wish):</span></span>

1. <span data-ttu-id="4d070-189">Azure 관리 포털</span><span class="sxs-lookup"><span data-stu-id="4d070-189">Azure Management Portal</span></span>

   <span data-ttu-id="4d070-190">도메인을 추가하면 인수가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-190">A takeover is triggered by doing a domain addition.</span></span>  <span data-ttu-id="4d070-191">해당 도메인에 대한 디렉터리가 이미 존재하면 외부 인수를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-191">If a directory already exists for the domain, you'll have the option to perform an external takeover.</span></span>

   <span data-ttu-id="4d070-192">자격 증명을 사용하여 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-192">Sign in to the Azure portal using your credentials.</span></span>  <span data-ttu-id="4d070-193">기존 디렉터리로 이동한 다음 **도메인 추가**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-193">Navigate to your existing directory and then to **Add domain**.</span></span>
2. <span data-ttu-id="4d070-194">Office 365</span><span class="sxs-lookup"><span data-stu-id="4d070-194">Office 365</span></span>

   <span data-ttu-id="4d070-195">Office 365의 [도메인 관리](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) 페이지에 있는 옵션을 사용하여 도메인 및 DNS 레코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-195">You can use the options on the [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 to work with your domains and DNS records.</span></span> <span data-ttu-id="4d070-196">[Office 365에서 도메인 확인](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d070-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span></span>
3. <span data-ttu-id="4d070-197">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d070-197">Windows PowerShell</span></span>

   <span data-ttu-id="4d070-198">Windows PowerShell을 사용하여 유효성 검사를 수행하려면 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-198">The following steps are required to perform a validation using Windows PowerShell.</span></span>

   | <span data-ttu-id="4d070-199">단계</span><span class="sxs-lookup"><span data-stu-id="4d070-199">Step</span></span> | <span data-ttu-id="4d070-200">사용할 cmdlet</span><span class="sxs-lookup"><span data-stu-id="4d070-200">Cmdlet to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="4d070-201">자격 증명 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4d070-201">Create a credential object</span></span> |<span data-ttu-id="4d070-202">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="4d070-202">Get-Credential</span></span> |
   | <span data-ttu-id="4d070-203">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="4d070-203">Connect to Azure AD</span></span> |<span data-ttu-id="4d070-204">Connect-MsolService</span><span class="sxs-lookup"><span data-stu-id="4d070-204">Connect-MsolService</span></span> |
   | <span data-ttu-id="4d070-205">도메인 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="4d070-205">get a list of domains</span></span> |<span data-ttu-id="4d070-206">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="4d070-206">Get-MsolDomain</span></span> |
   | <span data-ttu-id="4d070-207">챌린지 만들기</span><span class="sxs-lookup"><span data-stu-id="4d070-207">Create a challenge</span></span> |<span data-ttu-id="4d070-208">Get-MsolDomainVerificationDns</span><span class="sxs-lookup"><span data-stu-id="4d070-208">Get-MsolDomainVerificationDns</span></span> |
   | <span data-ttu-id="4d070-209">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="4d070-209">Create DNS record</span></span> |<span data-ttu-id="4d070-210">DNS 서버에서 수행</span><span class="sxs-lookup"><span data-stu-id="4d070-210">Do this on your DNS server</span></span> |
   | <span data-ttu-id="4d070-211">챌린지 확인</span><span class="sxs-lookup"><span data-stu-id="4d070-211">Verify the challenge</span></span> |<span data-ttu-id="4d070-212">Confirm-MsolEmailVerifiedDomain</span><span class="sxs-lookup"><span data-stu-id="4d070-212">Confirm-MsolEmailVerifiedDomain</span></span> |

<span data-ttu-id="4d070-213">예:</span><span class="sxs-lookup"><span data-stu-id="4d070-213">For example:</span></span>

1. <span data-ttu-id="4d070-214">셀프 서비스 제공 사항에 응답하는 데 사용된 자격 증명을 사용하여 Azure AD에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-214">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span></span>

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. <span data-ttu-id="4d070-215">도메인 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-215">Get a list of domains:</span></span>

    <span data-ttu-id="4d070-216">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="4d070-216">Get-MsolDomain</span></span>
3. <span data-ttu-id="4d070-217">그런 다음 Get-MsolDomainVerificationDns cmdlet을 실행하여 챌린지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-217">Then run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span></span>

    <span data-ttu-id="4d070-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="4d070-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span></span>

    <span data-ttu-id="4d070-219">예:</span><span class="sxs-lookup"><span data-stu-id="4d070-219">For example:</span></span>

    <span data-ttu-id="4d070-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="4d070-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span></span>
4. <span data-ttu-id="4d070-221">이 명령에서 반환되는 값(챌린지)을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-221">Copy the value (the challenge) that is returned from this command.</span></span>

    <span data-ttu-id="4d070-222">예:</span><span class="sxs-lookup"><span data-stu-id="4d070-222">For example:</span></span>

    <span data-ttu-id="4d070-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span><span class="sxs-lookup"><span data-stu-id="4d070-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span></span>
5. <span data-ttu-id="4d070-224">공용 DNS 네임스페이스에서 이전 단계에서 복사한 값이 포함된 DNS txt 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-224">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span></span>

    <span data-ttu-id="4d070-225">이 레코드의 이름은 부모 도메인의 이름이므로 Windows Server의 DNS 역할을 사용하여 이 리소스 레코드를 만드는 경우 레코드 이름은 비워두고 값을 텍스트 상자에 붙여넣기만 하세요.</span><span class="sxs-lookup"><span data-stu-id="4d070-225">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box</span></span>
6. <span data-ttu-id="4d070-226">Confirm-MsolDomain cmdlet을 실행하여 챌린지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-226">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span></span>

    <span data-ttu-id="4d070-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span><span class="sxs-lookup"><span data-stu-id="4d070-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span></span>

    <span data-ttu-id="4d070-228">예:</span><span class="sxs-lookup"><span data-stu-id="4d070-228">for example:</span></span>

    <span data-ttu-id="4d070-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span><span class="sxs-lookup"><span data-stu-id="4d070-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span></span>

<span data-ttu-id="4d070-230">챌린지가 성공하면 오류 없이 프롬프트로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-230">A successful challenge returns you to the prompt without an error.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="4d070-231">셀프 서비스 설정을 제어하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d070-231">How do I control self-service settings?</span></span>
<span data-ttu-id="4d070-232">관리자는 현재 두 개의 셀프 서비스 컨트롤을 보유하며</span><span class="sxs-lookup"><span data-stu-id="4d070-232">Admins have two self-service controls today.</span></span> <span data-ttu-id="4d070-233">다음을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-233">They can control:</span></span>

* <span data-ttu-id="4d070-234">사용자가 메일을 통해 디렉터리를 결합할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="4d070-234">Whether or not users can join the directory via email.</span></span>
* <span data-ttu-id="4d070-235">응용 프로그램 및 서비스를 사용자 자신이 사용하도록 허가할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="4d070-235">Whether or not users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="4d070-236">이러한 기능은 어떻게 제어할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="4d070-236">How can I control these capabilities?</span></span>
<span data-ttu-id="4d070-237">관리자는 Azure AD cmdlet인 Set-MsolCompanySettings 매개 변수를 사용하여 이러한 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="4d070-238">**AllowEmailVerifiedUsers** 는 관리되지 않는 디렉터리를 만들거나 결합시킬 수 있는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="4d070-239">이 매개 변수를 $false로 설정하면 메일로 확인된 사용자가 디렉터리를 결합시킬 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-239">If you set that parameter to $false, no email-verified users can join the directory.</span></span>
* <span data-ttu-id="4d070-240">**AllowAdHocSubscriptions** 는 사용자의 셀프 서비스 등록 수행을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-240">**AllowAdHocSubscriptions** controls the ability for users to perform self-service sign up.</span></span> <span data-ttu-id="4d070-241">이 매개 변수를 $false로 설정하면 사용자가 셀프 서비스 등록을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-241">If you set that parameter to $false, no users can perform self-service signup.</span></span>

### <a name="how-do-the-controls-work-together"></a><span data-ttu-id="4d070-242">컨트롤이 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="4d070-242">How do the controls work together?</span></span>
<span data-ttu-id="4d070-243">이 두 매개 변수를 함께 사용하여 정의하면 셀프 서비스 등록을 더욱 세밀하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-243">These two parameters can be used in conjunction to define more precise control over self-service sign up.</span></span> <span data-ttu-id="4d070-244">예를 들어 Azure AD에 이미 계정이 있는 사용자만 다음 명령을 사용하여 셀프 서비스 등록을 수행할 수 있습니다. 즉, 메일로 확인된 계정을 만들어야 하는 사용자는 셀프 서비스 등록을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-244">For example, the following command will allow users to perform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created cannot perform self-service sign up):</span></span>

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

<span data-ttu-id="4d070-245">다음 순서도는 디렉터리와 셀프 서비스 등록에 대한 이러한 매개 변수 및 그 결과 조건의 다양한 모든 조합을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d070-245">The following flowchart explains all the different combinations for these parameters and the resulting conditions for the directory and self-service sign up.</span></span>

![][1]

<span data-ttu-id="4d070-246">매개 변수 사용 방법에 대한 자세한 내용 및 예는 [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d070-246">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d070-247">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4d070-247">See Also</span></span>
* [<span data-ttu-id="4d070-248">Azure PowerShell을 설치 및 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d070-248">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="4d070-249">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d070-249">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="4d070-250">Azure Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="4d070-250">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="4d070-251">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="4d070-251">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
