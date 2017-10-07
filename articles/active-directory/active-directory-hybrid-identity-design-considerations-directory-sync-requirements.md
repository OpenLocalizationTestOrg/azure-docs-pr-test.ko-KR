---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-디렉터리 동기화 요구 사항을 결정 | Microsoft Docs"
description: "사이의 모든 hello 사용자를 동기화 하는 데 필요한 요구 사항을 식별 내부와 클라우드 hello 엔터프라이즈에 대 한 on = 합니다."
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
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="ea2c5-103">디렉터리 동기화 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="ea2c5-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="ea2c5-104">모두 동기화는 온-프레미스 id에 따라 hello 클라우드에서 id 사용자에 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-104">Synchronization is all about providing users an identity in hello cloud based on their on-premises identity.</span></span> <span data-ttu-id="ea2c5-105">인증 또는 페더레이션된 인증에 대 한 동기화 된 계정을 사용 합니다, 여부 hello 사용자 toohave hello 클라우드에서 id를 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-105">Whether or not they will use synchronized account for authentication or federated authentication, hello users will still need toohave an identity in hello cloud.</span></span>  <span data-ttu-id="ea2c5-106">이 id는 toobe 유지 관리 하 고 정기적으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-106">This identity will need toobe maintained and updated periodically.</span></span>  <span data-ttu-id="ea2c5-107">hello 업데이트 제목 변경 toopassword 변경 된 내용에서 다양 한 형태를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-107">hello updates can take many forms, from title changes toopassword changes.</span></span>  

<span data-ttu-id="ea2c5-108">Hello 조직에서는 온-프레미스 id 솔루션 및 사용자 요구 사항 평가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-108">Start by evaluating hello organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="ea2c5-109">이 평가 중요 한 toodefine hello 기술 요구 사항에 사용자 id는 생성 및 hello 클라우드에서 유지 관리 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-109">This evaluation is important toodefine hello technical requirements for how user identities will be created and maintained in hello cloud.</span></span>  <span data-ttu-id="ea2c5-110">하지만 대부분의 조직에 대 한 Active Directory는 온-프레미스 및에서 사용자에 게 hello 온-프레미스 디렉터리에서 동기화 되도록, 일부 경우에이 되지 것입니다 hello 대/소문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-110">For a majority of organizations, Active Directory is on-premises and will be hello on-premises directory that users will by synchronized from, however in some cases this will not be hello case.</span></span>  

<span data-ttu-id="ea2c5-111">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-111">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="ea2c5-112">AD 포리스트가 하나 또는 다수가 있거나 없습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="ea2c5-113">Azure AD 디렉터리를 몇 개나 동기화합니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="ea2c5-114">필터링을 사용하십니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="ea2c5-115">여러 Azure AD Connect 서버를 계획했습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="ea2c5-116">현재 동기화 도구 온-프레미스가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="ea2c5-117">그렇다면 사용자에게 ID의 가상 디렉터리/통합이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="ea2c5-118">모든 다른 디렉터리 온-프레미스 toosynchronize (예: LDAP 디렉터리, HR 데이터베이스 등)을 지정 하 고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-118">Do you have any other directory on-premises that you want toosynchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="ea2c5-119">모든 GALSync를 수행 하는 toobe 예정 입니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-119">Are you going toobe doing any GALSync?</span></span>
  * <span data-ttu-id="ea2c5-120">조직의 Upn의 hello 현재 상태는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-120">What is hello current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="ea2c5-121">사용자가 인증하는 다른 디렉터리가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="ea2c5-122">회사는 Microsoft Exchange를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="ea2c5-123">하이브리드 Exchange를 배포할 계획입니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="ea2c5-124">동기화 요구 사항에 대 한 아이디어를가지고 이러한 요구 사항을 도구는 hello 올바른 하나의 toomeet toodetermine 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-124">Now that you have an idea about your synchronization requirements, you need toodetermine which tool is hello correct one toomeet these requirements.</span></span>  <span data-ttu-id="ea2c5-125">Microsoft는 여러 가지 도구 tooaccomplish 디렉터리 통합 및 동기화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-125">Microsoft provides several tools tooaccomplish directory integration and synchronization.</span></span>  <span data-ttu-id="ea2c5-126">Hello 참조 [하이브리드 Id 디렉터리 통합 도구 비교 표](active-directory-hybrid-identity-design-considerations-tools-comparison.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-126">See hello [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="ea2c5-127">동기화 요구 사항 및 귀사에 대 한이 수행 합니다 hello 도구를가지고는 이러한 디렉터리 서비스를 사용 하는 tooevaluate hello 응용 프로그램이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-127">Now that you have your synchronization requirements and hello tool that will accomplish this for your company, you need tooevaluate hello applications that use these directory services.</span></span> <span data-ttu-id="ea2c5-128">이 평가 toodefine hello 기술 요구 사항 toointegrate 이러한 응용 프로그램 toohello 클라우드 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-128">This evaluation is important toodefine hello technical requirements toointegrate these applications toohello cloud.</span></span> <span data-ttu-id="ea2c5-129">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-129">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="ea2c5-130">이 응용 프로그램 이동된 toohello 되어야 클라우드와 hello 디렉터리 사용?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-130">Will these applications be moved toohello cloud and use hello directory?</span></span>
* <span data-ttu-id="ea2c5-131">이러한 응용 프로그램이 성공적으로 사용할 수 있도록 동기화 toobe toohello 클라우드를 필요로 하는 특별 한 특성이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-131">Are there special attributes that need toobe synchronized toohello cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="ea2c5-132">이러한 응용 프로그램 toobe tootake 활용 클라우드 인증을 다시 작성 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-132">Will these applications need toobe re-written tootake advantage of cloud auth?</span></span>
* <span data-ttu-id="ea2c5-133">이러한 응용 프로그램 계속 toolive 온-프레미스 사용자가 액세스 하는 동안 hello 클라우드 id를 사용 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-133">Will these applications continue toolive on-premises while users access them using hello cloud identity?</span></span>

<span data-ttu-id="ea2c5-134">Toodetermine hello 보안 요구 사항 및 제약 조건 디렉터리 동기화를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-134">You also need toodetermine hello security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="ea2c5-135">이 평가 중요 한 tooget 순서 toocreate에 필요 하 고 hello 클라우드에서 사용자의 id를 유지 하는 hello 요구 사항 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-135">This evaluation is important tooget a list of hello requirements that will be needed in order toocreate and maintain user’s identities in hello cloud.</span></span> <span data-ttu-id="ea2c5-136">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-136">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="ea2c5-137">Hello 동기화 서버 배치 될 위치?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-137">Where will hello synchronization server be located?</span></span>
* <span data-ttu-id="ea2c5-138">가입된 도메인입니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-138">Will it be domain joined?</span></span>
* <span data-ttu-id="ea2c5-139">Hello 서버 DMZ와 같은 방화벽 뒤에 제한 된 네트워크에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-139">Will hello server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="ea2c5-140">가 수 tooopen hello 필수 방화벽 포트 toosupport 동기화 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-140">Will you be able tooopen hello required firewall ports toosupport synchronization?</span></span>
* <span data-ttu-id="ea2c5-141">동기화 서버 hello에 대 한 재해 복구 계획 했습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-141">Do you have a disaster recovery plan for hello synchronization server?</span></span>
* <span data-ttu-id="ea2c5-142">Hello와 toosynch 원하는 포리스트 전반에 대 한 올바른 권한이 있는 계정의 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-142">Do you have an account with hello correct permissions for all forests you want toosynch with?</span></span>
  * <span data-ttu-id="ea2c5-143">회사가이 질문에 대 한 hello 대답을 알고 하지 않는 경우 hello 섹션 "암호 동기화에 대 한 사용 권한" hello 문서를 검토 [Azure Active Directory 동기화 서비스 설치 hello](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) 이미 있는지 확인 하 고는 이러한 사용 권한이 있는 계정 또는 하나 toocreate 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-143">If your company doesn’t know hello answer for this question, review hello section “Permissions for password synchronization” in hello article [Install hello Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need toocreate one.</span></span>
* <span data-ttu-id="ea2c5-144">다중 포리스트 동기화 있을 경우 hello 동기화 서버 수 tooget tooeach 포리스트?</span><span class="sxs-lookup"><span data-stu-id="ea2c5-144">If you have mutli-forest sync is hello sync server able tooget tooeach forest?</span></span>

> [!NOTE]
> <span data-ttu-id="ea2c5-145">각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-145">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="ea2c5-146">[사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 에서는 사용할 수 있는 hello 옵션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over hello options available.</span></span> <span data-ttu-id="ea2c5-147">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea2c5-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ea2c5-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea2c5-148">Next steps</span></span>
[<span data-ttu-id="ea2c5-149">Multi-Factor Authentication 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="ea2c5-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="ea2c5-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ea2c5-150">See also</span></span>
[<span data-ttu-id="ea2c5-151">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="ea2c5-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

