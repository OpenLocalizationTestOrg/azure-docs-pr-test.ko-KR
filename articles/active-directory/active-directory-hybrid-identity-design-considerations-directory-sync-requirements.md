---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - 디렉터리 동기화 요구 사항 확인 | Microsoft Docs"
description: "기업에 대한 온-프레미스와 클라우드 사이의 모든 사용자를 동기화하는 데 필요한 요구 사항을 식별합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="53e6f-103">디렉터리 동기화 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="53e6f-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="53e6f-104">동기화는 해당 온-프레미스 ID에 기반하여 클라우드에서 사용자에게 ID를 제공하는 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="53e6f-105">인증에 대해 동기화된 계정 또는 페더레이션된 인증을 사용하는지와 무관하게 사용자는 클라우드에서 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="53e6f-106">이 ID는 정기적으로 유지 관리하고 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="53e6f-107">업데이트는 제목 변경에서 암호 변경까지 다양한 형태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="53e6f-108">조직 온-프레미스 ID 솔루션 및 사용자 요구 사항을 평가하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="53e6f-109">이 평가판은 사용자 ID가 클라우드에서 생성되고 유지 관리되는 방법에 대한 기술 요구 사항을 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="53e6f-110">대부분의 조직의 경우 Active Directory는 온-프레미스이며 사용자가 동기화하는 온-프레미스 디렉터리이지만 경우에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="53e6f-111">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="53e6f-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="53e6f-112">AD 포리스트가 하나 또는 다수가 있거나 없습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="53e6f-113">Azure AD 디렉터리를 몇 개나 동기화합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="53e6f-114">필터링을 사용하십니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="53e6f-115">여러 Azure AD Connect 서버를 계획했습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="53e6f-116">현재 동기화 도구 온-프레미스가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="53e6f-117">그렇다면 사용자에게 ID의 가상 디렉터리/통합이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="53e6f-118">동기화하려는 다른 디렉터리 온-프레미스(예: LDAP 디렉터리, HR 데이터베이스 등)가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="53e6f-119">GALSync를 수행할 것입니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="53e6f-120">조직에서 UPN의 현재 상태는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="53e6f-121">사용자가 인증하는 다른 디렉터리가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="53e6f-122">회사는 Microsoft Exchange를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="53e6f-123">하이브리드 Exchange를 배포할 계획입니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="53e6f-124">이제 동기화 요구 사항을 이해했으므로 이러한 요구 사항을 만족하기에 알맞은 도구를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="53e6f-125">Microsoft는 디렉터리 통합 및 동기화를 수행하기 위한 여러 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="53e6f-126">자세한 내용은 [하이브리드 ID 디렉터리 통합 도구 비교표](active-directory-hybrid-identity-design-considerations-tools-comparison.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e6f-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="53e6f-127">이제 동기화 요구 사항을 확인하고 회사에 대해 이를 수행하는 도구를 가지고 있으므로 이러한 디렉터리 서비스를 사용하는 응용 프로그램을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="53e6f-128">이 평가판은 클라우드에 이러한 응용 프로그램을 통합하는 기술 요구 사항을 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="53e6f-129">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="53e6f-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="53e6f-130">이러한 응용 프로그램이 클라우드로 이동되고 디렉터리를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="53e6f-131">클라우드로 동기화되어야 하는 특수한 특성 사항이 있으므로 이러한 응용 프로그램이 특성을 성공적으로 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="53e6f-132">이러한 응용 프로그램은 클라우드 인증을 활용하기 위해 다시 작성해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="53e6f-133">사용자가 클라우드 ID를 사용하여 액세스하는 동안 이러한 응용 프로그램은 계속 온-프레미스에서 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="53e6f-134">또한 보안 요구 사항 및 제약 조건 디렉터리 동기화를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="53e6f-135">이 평가판은 클라우드에서 사용자의 ID를 만들고 유지하기 위해 필요한 요구 사항 목록을 가져오는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="53e6f-136">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="53e6f-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="53e6f-137">동기화 서버는 어디에 배치됩니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="53e6f-138">가입된 도메인입니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-138">Will it be domain joined?</span></span>
* <span data-ttu-id="53e6f-139">DMZ와 같은 방화벽 뒤에 제한된 네트워크에 서버가 위치합니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="53e6f-140">동기화를 지원하기 위해 필요한 방화벽 포트를 열 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="53e6f-141">동기화 서버에 대한 재해 복구 계획이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="53e6f-142">동기화하려는 모든 포리스트에 대한 올바른 사용 권한이 있는 계정이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="53e6f-143">회사가 이 질문에 대한 대답을 모르는 경우 [Azure Active Directory 동기화 서비스 설치](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) 문서에서 "암호 동기화에 대한 사용 권한" 섹션을 검토하고 이러한 사용 권한이 있는 계정이 이미 있는지 혹은 하나를 만들어야 할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="53e6f-144">다중 포리스트 동기화가 있는 경우 동기화 서버가 각 포리스트에 도달할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="53e6f-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="53e6f-145">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="53e6f-146">[사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 은 사용할 수 있는 옵션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="53e6f-147">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e6f-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="53e6f-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53e6f-148">Next steps</span></span>
[<span data-ttu-id="53e6f-149">Multi-Factor Authentication 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="53e6f-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="53e6f-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="53e6f-150">See also</span></span>
[<span data-ttu-id="53e6f-151">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="53e6f-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

