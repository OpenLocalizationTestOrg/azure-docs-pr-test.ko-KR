---
title: "aaaWhat azure 셀프서비스 등록 이란? | Microsoft Docs"
description: "Azure에 대 한 개요 셀프 서비스 등록 하 고 toomanage hello 등록 프로세스를 방법 DNS 도메인 이름을 통해 tootake 합니다."
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
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a><span data-ttu-id="12f92-104">Azure의 셀프 서비스 등록이란?</span><span class="sxs-lookup"><span data-stu-id="12f92-104">What is Self-Service Signup for Azure?</span></span>
<span data-ttu-id="12f92-105">이 항목에서는 hello 셀프 서비스 등록 과정을 설명 합니다. 어떻게 하 고 DNS 도메인 이름을 통해 tootake 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-105">This topic explains hello self-service signup process and how tootake over a DNS domain name.</span></span>  

## <a name="why-use-self-service-signup"></a><span data-ttu-id="12f92-106">셀프 서비스 등록을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="12f92-106">Why use self-service signup?</span></span>
* <span data-ttu-id="12f92-107">Get 고객 tooservices 더 빠르게 원합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-107">Get customers tooservices they want faster.</span></span>
* <span data-ttu-id="12f92-108">서비스에 대한 메일 기반 제공 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-108">Create email-based offers for a service.</span></span>
* <span data-ttu-id="12f92-109">신속 하 게 사용자가 기억 하기 쉬운 작업 전자 메일 별칭을 사용 하 여 toocreate id 수 있는 전자 메일 기반 등록 흐름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-109">Create email-based signup flows which quickly allow users toocreate identities using their easy-to-remember work email aliases.</span></span>
* <span data-ttu-id="12f92-110">관리되지 않는 Azure 디렉터리를 나중에 관리되는 디렉터리에 만들 수 있으며 다른 서비스에 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="12f92-111">용어 및 정의</span><span class="sxs-lookup"><span data-stu-id="12f92-111">Terms and Definitions</span></span>
* <span data-ttu-id="12f92-112">**셀프 서비스 등록**:이 사용자가 클라우드 서비스에 등록 하 고 해당 전자 메일 도메인에 따라 Azure Active Directory (Azure AD)에 자동으로 생성 하는 id 수 있는 hello 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-112">**Self-service sign up**: This is hello method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span></span>
* <span data-ttu-id="12f92-113">**관리 되지 않는 Azure directory**: hello 디렉터리를 해당 id를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-113">**Unmanaged Azure directory**: This is hello directory where that identity is created.</span></span> <span data-ttu-id="12f92-114">관리되지 않는 디렉터리는 전역 관리자가 없는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="12f92-115">**메일로 확인된 사용자**: Azure AD의 사용자 계정의 한 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="12f92-116">셀프 서비스 제공 사항에 등록한 후 자동으로 생성된 ID를 갖는 사용자를 메일로 확인된 사용자라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="12f92-117">메일로 확인된 사용자는 creationmethod=EmailVerified로 태그가 지정된 디렉터리의 일반 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="user-experience"></a><span data-ttu-id="12f92-118">사용자 환경</span><span class="sxs-lookup"><span data-stu-id="12f92-118">User experience</span></span>
<span data-ttu-id="12f92-119">예를 들어 있는 메일이 Dan@BellowsCollege.com 인 사용자가 메일을 통해 중요한 파일을 받는다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span></span> <span data-ttu-id="12f92-120">Azure 권한 관리 (Azure RMS)로 보호 된 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-120">hello files have been protected by Azure Rights Management (Azure RMS).</span></span> <span data-ttu-id="12f92-121">하지만 Dan의 조직인 Bellows College는 Azure RMS에 등록하지 않았으며 Active Directory RMS도 배포하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span></span> <span data-ttu-id="12f92-122">이 경우 Dan 등록할 수는 무료 구독 tooRMS 개인 순서 tooread hello 보호 된 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-122">In this case, Dan can sign up for a free subscription tooRMS for individuals in order tooread hello protected files.</span></span>

<span data-ttu-id="12f92-123">Dan hello 첫 번째 사용자 제공이 셀프 서비스에 대해 BellowsCollege.com toosign에서 전자 메일 주소가 있는 경우 다음 관리 되지 않는 디렉터리 만들어질 수 BellowsCollege.com에 대 한 Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-123">If Dan is hello first user with an email address from BellowsCollege.com toosign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span></span> <span data-ttu-id="12f92-124">관리 되지 않는 동일한 hello에서 만들어진 전자 메일 확인 사용자 계정은 해야만 합니다 hello BellowsCollege.com 도메인의 다른 사용자가이 제공 또는 유사한 셀프 서비스 제공에 등록 하는 경우 Azure에서 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-124">If other users from hello BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in hello same unmanaged directory in Azure.</span></span>

## <a name="admin-experience"></a><span data-ttu-id="12f92-125">관리자 환경</span><span class="sxs-lookup"><span data-stu-id="12f92-125">Admin experience</span></span>
<span data-ttu-id="12f92-126">관리 되지 않는 Azure 디렉터리의 hello DNS 도메인 이름을 소유 하 고 관리 인계 하거나 소유권을 증명 후 hello 디렉터리에 병합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-126">An admin who owns hello DNS domain name of an unmanaged Azure directory can take over or merge hello directory after proving ownership.</span></span> <span data-ttu-id="12f92-127">hello 다음 섹션에서는 더 자세하게에서 hello 관리자 환경에 설명 하지만 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-127">hello next sections explain hello admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="12f92-128">관리 되지 않는 Azure 디렉터리를 인수할 때 hello 관리 되지 않는 디렉터리의 전역 관리자에 게 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-128">When you take over an unmanaged Azure directory, you simply become hello global administrator of hello unmanaged directory.</span></span> <span data-ttu-id="12f92-129">이를 내부 인수라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-129">This is sometimes called an internal takeover.</span></span>
* <span data-ttu-id="12f92-130">관리 되지 않는 Azure 디렉터리를 병합 하 고 hello 관리 되지 않는 디렉터리 tooyour 관리 되는 Azure 디렉터리의 hello DNS 도메인 이름을 추가 하면 사용자-리소스의 매핑이 만들어집니다 하므로 tooaccess 서비스 중단 없이 사용자가 계속 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-130">When you merge an unmanaged Azure directory, you add hello DNS domain name of hello unmanaged directory tooyour managed Azure directory and a mapping of users-to-resources is created so users can continue tooaccess services without interruption.</span></span> <span data-ttu-id="12f92-131">이를 외부 인수라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-131">This is sometimes called an external takeover.</span></span>

## <a name="what-gets-created-in-azure-active-directory"></a><span data-ttu-id="12f92-132">Azure Active Directory에 생성되는 것은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="12f92-132">What gets created in Azure Active Directory?</span></span>
#### <a name="directory"></a><span data-ttu-id="12f92-133">디렉터리</span><span class="sxs-lookup"><span data-stu-id="12f92-133">directory</span></span>
* <span data-ttu-id="12f92-134">Hello 도메인에 대 한 Azure Active Directory 디렉터리를 만들어지면 도메인당 한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-134">An Azure Active Directory directory for hello domain is created, one directory per domain.</span></span>
* <span data-ttu-id="12f92-135">hello Azure AD 디렉터리에 없는 전역 관리자</span><span class="sxs-lookup"><span data-stu-id="12f92-135">hello Azure AD directory has no global admin.</span></span>

#### <a name="users"></a><span data-ttu-id="12f92-136">사용자</span><span class="sxs-lookup"><span data-stu-id="12f92-136">Users</span></span>
* <span data-ttu-id="12f92-137">각 사용자가 등록에 대해 사용자 개체에 hello Azure AD 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-137">For each user who signs up, a user object is created in hello Azure AD directory.</span></span>
* <span data-ttu-id="12f92-138">각 사용자 개체는 외부로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-138">Each user object is marked as external.</span></span>
* <span data-ttu-id="12f92-139">각 사용자에 등록 하는 액세스 toohello 서비스를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-139">Each user is given access toohello service that they signed up for.</span></span>

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a><span data-ttu-id="12f92-140">소유한 도메인에 대한 셀프 서비스 Azure AD 디렉터리를 어떻게 요구하나요?</span><span class="sxs-lookup"><span data-stu-id="12f92-140">How do I claim a self-service Azure AD directory for a domain I own?</span></span>
<span data-ttu-id="12f92-141">도메인 유효성 검사를 수행하여 셀프 서비스 Azure AD 디렉터리를 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-141">You can claim a self-service Azure AD directory by performing domain validation.</span></span> <span data-ttu-id="12f92-142">도메인 유효성 검사 DNS 레코드를 만들어 직접 hello 도메인을 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-142">Domain validation proves you own hello domain by creating DNS records.</span></span>

<span data-ttu-id="12f92-143">두 가지 방법으로 toodo Azure AD 디렉터리의 DNS 인수 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-143">There are two ways toodo a DNS takeover of an Azure AD directory:</span></span>

* <span data-ttu-id="12f92-144">내부 인수 (관리자는 관리 되지 않는 Azure 디렉터리를 검색 하는 관리 되는 디렉터리로 tooturn가)</span><span class="sxs-lookup"><span data-stu-id="12f92-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants tooturn into a managed directory)</span></span>
* <span data-ttu-id="12f92-145">외부 인수 (Admin tooadd 새 도메인 tootheir 관리 되는 Azure 디렉터리를 시도 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="12f92-145">external takeover (Admin tries tooadd a new domain tootheir managed Azure directory)</span></span>

<span data-ttu-id="12f92-146">사용자 셀프 서비스 등록을 수행 하거나 새 도메인 tooan 기존의 관리 되는 디렉터리를 추가할 수 있습니다는 관리 되지 않는 디렉터리를 통해 수행한 때문에 도메인을 소유 하는 유효성 검사에 관심을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain tooan existing managed directory.</span></span> <span data-ttu-id="12f92-147">예를 들어 contoso.com 이라는 도메인이 고 tooadd contoso.co.uk 또는 contoso.uk 이라는 이름의 새 도메인을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-147">For example, you have a domain named contoso.com and you want tooadd a new domain named contoso.co.uk or contoso.uk.</span></span>

## <a name="what-is-domain-takeover"></a><span data-ttu-id="12f92-148">도메인 인수란?</span><span class="sxs-lookup"><span data-stu-id="12f92-148">What is domain takeover?</span></span>
<span data-ttu-id="12f92-149">이 섹션에서는 어떻게 toovalidate 도메인을 소유</span><span class="sxs-lookup"><span data-stu-id="12f92-149">This section covers how toovalidate that you own a domain</span></span>

### <a name="what-is-domain-validation-and-why-is-it-used"></a><span data-ttu-id="12f92-150">도메인 유효성 검사란 무엇이며 사용해야 하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="12f92-150">What is domain validation and why is it used?</span></span>
<span data-ttu-id="12f92-151">순서 tooperform 작업 디렉터리에 Azure AD는 hello DNS 도메인의 소유권을 확인 하는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-151">In order tooperform operations on a directory, Azure AD requires that you validate ownership of hello DNS domain.</span></span>  <span data-ttu-id="12f92-152">Hello 도메인의 유효성 검사에 tooclaim hello 디렉터리와 하거나 승격 hello 셀프 서비스 디렉터리 tooa 관리 되는 디렉터리 또는 디렉터리를 관리 하는 hello 셀프 서비스를 기존 디렉터리 병합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-152">Validation of hello domain allows you tooclaim hello directory and either promote hello self-service directory tooa managed directory, or merge hello self-service directory into an existing managed directory.</span></span>

## <a name="examples-of-domain-validation"></a><span data-ttu-id="12f92-153">도메인 유효성 검사 예</span><span class="sxs-lookup"><span data-stu-id="12f92-153">Examples of domain validation</span></span>
<span data-ttu-id="12f92-154">두 가지 방법으로 toodo 디렉터리의 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="12f92-154">There are two ways toodo a DNS takeover of a directory:</span></span>

* <span data-ttu-id="12f92-155">내부 인수 (예를 들어 관리자 셀프 서비스, 관리 되지 않는 디렉터리를 검색 및 관리 되는 디렉터리에 tooturn 원하는)</span><span class="sxs-lookup"><span data-stu-id="12f92-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants tooturn into managed directory)</span></span>
* <span data-ttu-id="12f92-156">외부 인수 (예를 들어 관리자가 시도 tooadd 새 도메인 tooa 관리 되는 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="12f92-156">external takeover (For example, a admin tries tooadd a new domain tooa managed directory)</span></span>

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a><span data-ttu-id="12f92-157">내부 인수-셀프 서비스, 관리 되지 않는 디렉터리 toobe 관리 되는 디렉터리를 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-157">Internal Takeover - promote a self-service, unmanaged directory toobe a managed directory</span></span>
<span data-ttu-id="12f92-158">내부 구성 작업을 수행할 때 hello 디렉터리 관리 되지 않는 디렉터리 tooa 관리 되는 디렉터리에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-158">When you do internal takeover, hello directory gets converted from an unmanaged directory tooa managed directory.</span></span> <span data-ttu-id="12f92-159">Toocomplete DNS 도메인 이름 유효성 검사, TXT 레코드 또는 MX 레코드에에서 만드는 hello DNS 영역이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-159">You need toocomplete DNS domain name validation, where you create an MX record or a TXT record in hello DNS zone.</span></span> <span data-ttu-id="12f92-160">DNS 영역에 MX 레코드 또는 TXT 레코드를 만드는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-160">That action:</span></span>

* <span data-ttu-id="12f92-161">Hello 도메인의 소유를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-161">Validates that you own hello domain</span></span>
* <span data-ttu-id="12f92-162">관리 되는 hello 디렉터리를 사용 하면</span><span class="sxs-lookup"><span data-stu-id="12f92-162">Makes hello directory managed</span></span>
* <span data-ttu-id="12f92-163">Hello 디렉터리의 전역 관리자 hello 만듭니다</span><span class="sxs-lookup"><span data-stu-id="12f92-163">Makes you hello global admin of hello directory</span></span>

<span data-ttu-id="12f92-164">로즈 이동 대학에서 IT 관리자 검색 hello 학교에서 사용자가 셀프 서비스 제공에 대 한 등록 한 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-164">Let's say an IT administrator from Bellows College discovers that users from hello school have signed up for self-service offerings.</span></span> <span data-ttu-id="12f92-165">Hello 등록 hello DNS의 소유자 이름을 BellowsCollege.com, hello IT 관리자는 Azure의 hello DNS 이름의 소유권을 확인 하 고 hello 관리 되지 않는 디렉터리 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-165">As hello registered owner of hello DNS name BellowsCollege.com, hello IT administrator can validate ownership of hello DNS name in Azure and then take over hello unmanaged directory.</span></span> <span data-ttu-id="12f92-166">hello 디렉터리 다음 되는 관리 되는 디렉터리 및 hello IT 관리자는 hello 전역 관리자 역할이 할당 hello BellowsCollege.com 디렉터리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-166">hello directory then becomes a managed directory, and hello IT administrator is assigned hello global administrator role for hello BellowsCollege.com directory.</span></span>

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a><span data-ttu-id="12f92-167">외부 인수 - 셀프 서비스 디렉터리를 관리되는 기존 디렉터리에 병합</span><span class="sxs-lookup"><span data-stu-id="12f92-167">External Takeover - merge a self-service directory into an existing managed directory</span></span>
<span data-ttu-id="12f92-168">외부 프로그램 구성에서 이미 관리 되는 디렉터리 및 모든 사용자 및 그룹 디렉터리를 관리 하는 관리 되지 않는 디렉터리 toojoin에서 원하는 대신 자체 두 디렉터리를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory toojoin that managed directory, rather than own two separate directories.</span></span>

<span data-ttu-id="12f92-169">관리 되는 디렉터리의 관리자의 경우 도메인을 추가 하 고 연결 된 디렉터리를 관리 되지 않는 toohave 발생 하는 해당 도메인.</span><span class="sxs-lookup"><span data-stu-id="12f92-169">As an admin of a managed directory, you add a domain, and that domain happens toohave an unmanaged directory associated with it.</span></span>

<span data-ttu-id="12f92-170">예를 들어는 IT 관리자가 이미 등록 된 tooyour 조직 된 도메인 이름 Contoso.com에 대 한 관리 되는 디렉터리를 사용할 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered tooyour organization.</span></span> <span data-ttu-id="12f92-171">조직의 사용자가 조직이 소유하는 또 다른 도메인 이름인 전자 메일 도메인 이름 user@contoso.co.uk를 사용하여 제품에 대한 셀프 서비스 등록을 수행한 것을 발견합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span></span> <span data-ttu-id="12f92-172">이 사용자는 현재 contoso.co.uk의 관리되지 않는 디렉터리에 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span></span>

<span data-ttu-id="12f92-173">Contoso.com에 대 한 기존 IT 관리 디렉터리에 hello contoso.co.uk에 대 한 관리 되지 않는 디렉터리를 병합 되므로 두 개의 별도 디렉터리 toomanage 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-173">You don't want toomanage two separate directories, so you merge hello unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span></span>

<span data-ttu-id="12f92-174">외부 감염 다음과 같은 DNS 유효성 검사 프로세스 내부 인수 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-174">External takeover follows hello same DNS validation process as internal takeover.</span></span>  <span data-ttu-id="12f92-175">차이점은 기간: 사용자 및 서비스를 다시 매핑된 toohello IT 관리 되는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-175">Difference being: users and services are remapped toohello IT managed directory.</span></span>

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a><span data-ttu-id="12f92-176">외부 인수 수행의 hello 영향 이란?</span><span class="sxs-lookup"><span data-stu-id="12f92-176">What's hello impact of performing an external takeover?</span></span>
<span data-ttu-id="12f92-177">외부 인수, 사용자가 tooaccess 서비스 중단 없이 계속 수 있도록 사용자-리소스의 매핑을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-177">With an external takeover, a mapping of users-to-resources is created so users can continue tooaccess services without interruption.</span></span> <span data-ttu-id="12f92-178">사용자가 계속 tooaccess 변경 없이 이러한 서비스 및 개인별 RMS를 포함 하 여 대부분의 응용 프로그램, 사용자-리소스의 hello 매핑을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-178">Many applications, including RMS for individuals, handle hello mapping of users-to-resources well, and users can continue tooaccess those services without change.</span></span> <span data-ttu-id="12f92-179">응용 프로그램 사용자-리소스의 hello 매핑을 효과적으로 처리 하지 않을 경우 외부 인수 만족 스러운 서비스의 사용자를 명시적으로 차단 된 tooprevent 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-179">If an application does not handle hello mapping of users-to-resources effectively, external takeover may be explicitly blocked tooprevent users from a poor experience.</span></span>

#### <a name="directory-takeover-support-by-service"></a><span data-ttu-id="12f92-180">디렉터리 인수 지원 서비스</span><span class="sxs-lookup"><span data-stu-id="12f92-180">directory takeover support by service</span></span>
<span data-ttu-id="12f92-181">현재 다음 hello 서비스 지원 인수:</span><span class="sxs-lookup"><span data-stu-id="12f92-181">Currently hello following services support takeover:</span></span>

* <span data-ttu-id="12f92-182">RMS</span><span class="sxs-lookup"><span data-stu-id="12f92-182">RMS</span></span>

<span data-ttu-id="12f92-183">다음 서비스는 hello 곧 원하는 인수:</span><span class="sxs-lookup"><span data-stu-id="12f92-183">hello following services will soon be supporting takeover:</span></span>

* <span data-ttu-id="12f92-184">PowerBI</span><span class="sxs-lookup"><span data-stu-id="12f92-184">PowerBI</span></span>

<span data-ttu-id="12f92-185">hello 다음 안을 외부 인수 후 추가 관리 작업 toomigrate 사용자 데이터는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-185">hello following do not and require additional admin action toomigrate user data after an external takeover.</span></span>

* <span data-ttu-id="12f92-186">SharePoint/OneDrive</span><span class="sxs-lookup"><span data-stu-id="12f92-186">SharePoint/OneDrive</span></span>

## <a name="how-tooperform-a-dns-domain-name-takeover"></a><span data-ttu-id="12f92-187">어떻게 tooperform DNS 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="12f92-187">How tooperform a DNS domain name takeover</span></span>
<span data-ttu-id="12f92-188">방법에 대 한 몇 가지 옵션이 tooperform 도메인 유효성 검사 (및는 구성 하려는 경우 수행):</span><span class="sxs-lookup"><span data-stu-id="12f92-188">You have a few options for how tooperform a domain validation (and do a takeover if you wish):</span></span>

1. <span data-ttu-id="12f92-189">Azure 관리 포털</span><span class="sxs-lookup"><span data-stu-id="12f92-189">Azure Management Portal</span></span>

   <span data-ttu-id="12f92-190">도메인을 추가하면 인수가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-190">A takeover is triggered by doing a domain addition.</span></span>  <span data-ttu-id="12f92-191">Hello 도메인에 대 한 디렉터리가 이미 경우 hello 옵션 tooperform 외부 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-191">If a directory already exists for hello domain, you'll have hello option tooperform an external takeover.</span></span>

   <span data-ttu-id="12f92-192">자격 증명을 사용 하 여 Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-192">Sign in toohello Azure portal using your credentials.</span></span>  <span data-ttu-id="12f92-193">Tooyour 기존 디렉터리를 탐색 한 다음 너무**도메인 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-193">Navigate tooyour existing directory and then too**Add domain**.</span></span>
2. <span data-ttu-id="12f92-194">Office 365</span><span class="sxs-lookup"><span data-stu-id="12f92-194">Office 365</span></span>

   <span data-ttu-id="12f92-195">Hello에 hello 옵션을 사용할 수 [도메인 관리](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) 도메인 및 DNS 레코드를 사용한 Office 365 toowork의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-195">You can use hello options on hello [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 toowork with your domains and DNS records.</span></span> <span data-ttu-id="12f92-196">[Office 365에서 도메인 확인](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12f92-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span></span>
3. <span data-ttu-id="12f92-197">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f92-197">Windows PowerShell</span></span>

   <span data-ttu-id="12f92-198">단계를 수행 하는 hello 필요한 tooperform Windows PowerShell을 사용 하는 유효성 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-198">hello following steps are required tooperform a validation using Windows PowerShell.</span></span>

   | <span data-ttu-id="12f92-199">단계</span><span class="sxs-lookup"><span data-stu-id="12f92-199">Step</span></span> | <span data-ttu-id="12f92-200">Cmdlet toouse</span><span class="sxs-lookup"><span data-stu-id="12f92-200">Cmdlet toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="12f92-201">자격 증명 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="12f92-201">Create a credential object</span></span> |<span data-ttu-id="12f92-202">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="12f92-202">Get-Credential</span></span> |
   | <span data-ttu-id="12f92-203">TooAzure AD 연결</span><span class="sxs-lookup"><span data-stu-id="12f92-203">Connect tooAzure AD</span></span> |<span data-ttu-id="12f92-204">Connect-MsolService</span><span class="sxs-lookup"><span data-stu-id="12f92-204">Connect-MsolService</span></span> |
   | <span data-ttu-id="12f92-205">도메인 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="12f92-205">get a list of domains</span></span> |<span data-ttu-id="12f92-206">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="12f92-206">Get-MsolDomain</span></span> |
   | <span data-ttu-id="12f92-207">챌린지 만들기</span><span class="sxs-lookup"><span data-stu-id="12f92-207">Create a challenge</span></span> |<span data-ttu-id="12f92-208">Get-MsolDomainVerificationDns</span><span class="sxs-lookup"><span data-stu-id="12f92-208">Get-MsolDomainVerificationDns</span></span> |
   | <span data-ttu-id="12f92-209">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="12f92-209">Create DNS record</span></span> |<span data-ttu-id="12f92-210">DNS 서버에서 수행</span><span class="sxs-lookup"><span data-stu-id="12f92-210">Do this on your DNS server</span></span> |
   | <span data-ttu-id="12f92-211">Hello 챌린지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-211">Verify hello challenge</span></span> |<span data-ttu-id="12f92-212">Confirm-MsolEmailVerifiedDomain</span><span class="sxs-lookup"><span data-stu-id="12f92-212">Confirm-MsolEmailVerifiedDomain</span></span> |

<span data-ttu-id="12f92-213">예:</span><span class="sxs-lookup"><span data-stu-id="12f92-213">For example:</span></span>

1. <span data-ttu-id="12f92-214">TooAzure AD 연결 사용된 toorespond toohello 셀프 서비스 제공 되었던 hello 자격 증명을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="12f92-214">Connect tooAzure AD using hello credentials that were used toorespond toohello self-service offering:</span></span>

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. <span data-ttu-id="12f92-215">도메인 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-215">Get a list of domains:</span></span>

    <span data-ttu-id="12f92-216">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="12f92-216">Get-MsolDomain</span></span>
3. <span data-ttu-id="12f92-217">그런 다음 Get-msoldomainverificationdns cmdlet toocreate hello challenge를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-217">Then run hello Get-MsolDomainVerificationDns cmdlet toocreate a challenge:</span></span>

    <span data-ttu-id="12f92-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="12f92-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span></span>

    <span data-ttu-id="12f92-219">예:</span><span class="sxs-lookup"><span data-stu-id="12f92-219">For example:</span></span>

    <span data-ttu-id="12f92-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="12f92-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span></span>
4. <span data-ttu-id="12f92-221">이 명령에서 반환 되는 hello 값 (챌린지 hello)를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-221">Copy hello value (hello challenge) that is returned from this command.</span></span>

    <span data-ttu-id="12f92-222">예:</span><span class="sxs-lookup"><span data-stu-id="12f92-222">For example:</span></span>

    <span data-ttu-id="12f92-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span><span class="sxs-lookup"><span data-stu-id="12f92-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span></span>
5. <span data-ttu-id="12f92-224">공용 DNS 네임 스페이스를 hello 이전 단계에서 복사한 hello 값이 포함 된 DNS txt 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-224">In your public DNS namespace, create a DNS txt record that contains hello value that you copied in hello previous step.</span></span>

    <span data-ttu-id="12f92-225">이 레코드에 대 한 hello 이름은 hello hello 부모 도메인의 이름을, 따라서 Windows Server에서 DNS 역할 hello를 사용 하 여이 리소스 레코드를 만드는 경우 hello 레코드 이름을 비워 둡니다 이며 hello 텍스트 상자에 붙여넣을 hello 값</span><span class="sxs-lookup"><span data-stu-id="12f92-225">hello name for this record is hello name of hello parent domain, so if you create this resource record by using hello DNS role from Windows Server, leave hello Record name blank and just paste hello value into hello Text box</span></span>
6. <span data-ttu-id="12f92-226">Hello Confirm-msoldomain cmdlet tooverify hello 챌린지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-226">Run hello Confirm-MsolDomain cmdlet tooverify hello challenge:</span></span>

    <span data-ttu-id="12f92-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span><span class="sxs-lookup"><span data-stu-id="12f92-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span></span>

    <span data-ttu-id="12f92-228">예:</span><span class="sxs-lookup"><span data-stu-id="12f92-228">for example:</span></span>

    <span data-ttu-id="12f92-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span><span class="sxs-lookup"><span data-stu-id="12f92-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span></span>

<span data-ttu-id="12f92-230">챌린지가 성공적 이면 오류 없이 toohello 프롬프트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-230">A successful challenge returns you toohello prompt without an error.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="12f92-231">셀프 서비스 설정을 제어하는 방법</span><span class="sxs-lookup"><span data-stu-id="12f92-231">How do I control self-service settings?</span></span>
<span data-ttu-id="12f92-232">관리자는 현재 두 개의 셀프 서비스 컨트롤을 보유하며</span><span class="sxs-lookup"><span data-stu-id="12f92-232">Admins have two self-service controls today.</span></span> <span data-ttu-id="12f92-233">다음을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-233">They can control:</span></span>

* <span data-ttu-id="12f92-234">여부 사용자 전자 메일을 통해 hello 디렉터리에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-234">Whether or not users can join hello directory via email.</span></span>
* <span data-ttu-id="12f92-235">응용 프로그램 및 서비스를 사용자 자신이 사용하도록 허가할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="12f92-235">Whether or not users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="12f92-236">이러한 기능은 어떻게 제어할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="12f92-236">How can I control these capabilities?</span></span>
<span data-ttu-id="12f92-237">관리자는 Azure AD cmdlet인 Set-MsolCompanySettings 매개 변수를 사용하여 이러한 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="12f92-238">**AllowEmailVerifiedUsers** 는 관리되지 않는 디렉터리를 만들거나 결합시킬 수 있는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="12f92-239">해당 매개 변수를 설정 하는 경우 $false, 더 전자 메일 확인 사용자 hello 디렉터리 조인할 수 너무.</span><span class="sxs-lookup"><span data-stu-id="12f92-239">If you set that parameter too$false, no email-verified users can join hello directory.</span></span>
* <span data-ttu-id="12f92-240">**AllowAdHocSubscriptions** tooperform 셀프 서비스 등록 하는 사용자가 hello 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-240">**AllowAdHocSubscriptions** controls hello ability for users tooperform self-service sign up.</span></span> <span data-ttu-id="12f92-241">너무 해당 매개 변수를 설정 하면 $false 이면 사용자가 수행할 수 셀프 서비스 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-241">If you set that parameter too$false, no users can perform self-service signup.</span></span>

### <a name="how-do-hello-controls-work-together"></a><span data-ttu-id="12f92-242">어떻게 수행 hello 컨트롤 함께 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="12f92-242">How do hello controls work together?</span></span>
<span data-ttu-id="12f92-243">이 두 매개 변수를 사용할 수 함께 toodefine에 보다 자세히 제어할 셀프 서비스 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-243">These two parameters can be used in conjunction toodefine more precise control over self-service sign up.</span></span> <span data-ttu-id="12f92-244">예를 들어 hello 다음 명령을 사용 하면 사용자가 tooperform 셀프 서비스 등록만 해당 사용자 계정이 이미 있는 Azure AD의 경우 (즉, 사용자에 게 생성 하는 전자 메일 확인 된 계정 toobe는 수행할 수 없습니다 셀프서비스 위로):</span><span class="sxs-lookup"><span data-stu-id="12f92-244">For example, hello following command will allow users tooperform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account toobe created cannot perform self-service sign up):</span></span>

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

<span data-ttu-id="12f92-245">hello 다음 순서도 이러한 매개 변수에 대 한 모든 hello 다른 조합 및 설명 hello 디렉터리와 셀프 서비스 등록에 대 한 hello 결과 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-245">hello following flowchart explains all hello different combinations for these parameters and hello resulting conditions for hello directory and self-service sign up.</span></span>

![][1]

<span data-ttu-id="12f92-246">자세한 내용 및 toouse 이러한 매개 변수를 확인 하려면 어떻게의 예제에 대 한 [Set-msolcompanysettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="12f92-246">For more information and examples of how toouse these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span>

## <a name="see-also"></a><span data-ttu-id="12f92-247">참고 항목</span><span class="sxs-lookup"><span data-stu-id="12f92-247">See Also</span></span>
* [<span data-ttu-id="12f92-248">어떻게 tooinstall Azure PowerShell 및 구성</span><span class="sxs-lookup"><span data-stu-id="12f92-248">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="12f92-249">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f92-249">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="12f92-250">Azure Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="12f92-250">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="12f92-251">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="12f92-251">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
