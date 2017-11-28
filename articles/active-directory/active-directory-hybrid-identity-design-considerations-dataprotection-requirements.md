---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-데이터 보호 요구 사항을 확인 | Microsoft Docs"
description: "하이브리드 id 솔루션을 계획을 식별 하는 경우 귀하 비즈니스에 대 한 hello 데이터 보호 요구 사항 및 옵션을 사용할 수 있는 toobest 이러한 요구에 부합 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a><span data-ttu-id="47acb-103">강력한 ID 솔루션을 통해 데이터 보안을 향상하기 위한 계획</span><span class="sxs-lookup"><span data-stu-id="47acb-103">Plan for enhancing data security through strong identity solution</span></span>
<span data-ttu-id="47acb-104">hello 첫 번째 단계 tooprotect hello 데이터가 해당 데이터에 액세스할 수 있는 사용자 식별 되며 toohave 수 있는 id 솔루션 시스템 tooprovide 인증 및 권한 부여 기능 통합이 프로세스의 일부로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-104">hello first step tooprotect hello data is identify who can access that data and as part of this process you need toohave an identity solution that can integrates with your system tooprovide authentication and authorization capabilities.</span></span> <span data-ttu-id="47acb-105">인증 및 권한 부여는 종종 서로 혼동되고 역할은 오해됩니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-105">Authentication and authorization are often confused with each other and their roles misunderstood.</span></span> <span data-ttu-id="47acb-106">실제로 매우 다릅니다, 아래 hello 그림에 나와 있는 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="47acb-106">In reality they are quite different, as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

<span data-ttu-id="47acb-107">**모바일 장치 관리 수명 주기 단계**</span><span class="sxs-lookup"><span data-stu-id="47acb-107">**Mobile device management lifecycle stages**</span></span>

<span data-ttu-id="47acb-108">하이브리드 id 솔루션을 계획할 때 이러한 요구에 부합 조직 및 옵션을 사용할 수 있는 toobest hello 데이터 보호 요구 사항을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-108">When planning your hybrid identity solution you must understand hello data protection requirements for your business and which options are available toobest fulfil these requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="47acb-109">데이터 보안 계획을 완료 한 후 검토 [다단계 인증 요구 사항을 결정](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure는 다단계 인증 요구 사항에 대 한 선택 항목에 영향을 받지 않은 hello 결정 이 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-109">Once you finish planning for data security, review [Determine multi-factor authentication requirements](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure that your selections regarding multi-factor authentication requirements were not affected by hello decisions you made in this section.</span></span>
> 
> 

## <a name="determine-data-protection-requirements"></a><span data-ttu-id="47acb-110">데이터 보호 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="47acb-110">Determine data protection requirements</span></span>
<span data-ttu-id="47acb-111">이동성 hello 시대의 대부분의 기업 들은 공통의 목표를: 해당 사용자가 toobe에서 생산성을 유지 하는 동안 온-프레미스 또는 원격으로 모바일 장치에 순서 tooincrease 생산성 곳에 나 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-111">In hello age of mobility, most companies have a common goal: enable their users toobe productive on their mobile devices while on-premises or remotely from anywhere in order tooincrease productivity.</span></span> <span data-ttu-id="47acb-112">이 수는 공통의 목표를 하는 동안 회사 그러한 요구 사항에 안전 하 게 순서 tookeep 회사의 데이터에 완화 해야 하 고 사용자의 개인 정보를 유지 관리 하는 위협 양 hello에 관한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-112">While this could be a common goal, companies that have such requirement will also be concern regarding hello amount of threats that must be mitigated in order tookeep company’s data secure and maintain user’s privacy.</span></span> <span data-ttu-id="47acb-113">각 회사는 이런 점에서; 서로 다른 요구 사항을 있을 수 있습니다. 다양 한 규정 준수 규칙을 따라 toowhich 업계 hello 회사 달라 집니다가 작동 하는 발생할 toodifferent 디자인 관련 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-113">Each company might have different requirements in this regard; different compliance rules that will vary according toowhich industry hello company is acting will lead toodifferent design decisions.</span></span> 

<span data-ttu-id="47acb-114">그러나 보안 측면이 있습니다 탐색 하 고 hello 업계에 관계 없이 유효성 검사 해야 하는 hello 다음 섹션에 설명 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-114">However, there are some security aspects that should be explored and validated, regardless of hello industry, which are explained in hello next section.</span></span>

## <a name="data-protection-paths"></a><span data-ttu-id="47acb-115">데이터 보호 경로</span><span class="sxs-lookup"><span data-stu-id="47acb-115">Data protection paths</span></span>
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

<span data-ttu-id="47acb-116">**데이터 보호 경로**</span><span class="sxs-lookup"><span data-stu-id="47acb-116">**Data protection paths**</span></span>

<span data-ttu-id="47acb-117">위의 다이어그램 hello, hello id 구성 요소를 데이터에 액세스 하기 전에 확인 하는 첫 번째 toobe hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-117">In hello above diagram, hello identity component will be hello first one toobe verified before data is accessed.</span></span> <span data-ttu-id="47acb-118">그러나이 데이터는 서로 다른 상태에 액세스 하는 hello 시간 동안 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-118">However, this data can be in different states during hello time it was accessed.</span></span> <span data-ttu-id="47acb-119">이 다이어그램의 각 숫자는 데이터가 특정 시점에 위치할 수 있는 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-119">Each number on this diagram represents a path in which data can be located at some point in time.</span></span> <span data-ttu-id="47acb-120">이러한 숫자는 아래에 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-120">These numbers are explained below:</span></span>

1. <span data-ttu-id="47acb-121">Hello 장치 수준의 데이터 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-121">Data protection at hello device level.</span></span>
2. <span data-ttu-id="47acb-122">전송 중에 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="47acb-122">Data protection while in transit.</span></span>
3. <span data-ttu-id="47acb-123">휴지 상태의 온-프레미스에서 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="47acb-123">Data protection while at rest on-premises.</span></span>
4. <span data-ttu-id="47acb-124">hello 클라우드의 데이터 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-124">Data protection while at rest in hello cloud.</span></span>

<span data-ttu-id="47acb-125">Hello 하이브리드 id 솔루션은 온-프레미스를 활용할 수 있는 필요는 없지만 hello 기술적 컨트롤 단계 중 하나에 각 IT tooprotect hello 데이터 자체 수 있게 하는 hello 하이브리드 id 솔루션으로 직접 제공 되지 않습니다. 및 id 관리 리소스 tooidentify hello 사용자 권한 부여 toohello 데이터에 액세스 하기 전에 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-125">Although hello technical controls that will enable IT tooprotect hello data itself on each one of those phases are not directly offered by hello hybrid identity solution, it is necessary that hello hybrid identity solution is capable of leveraging both on-premises and cloud identity management resources tooidentify hello user before grant access toohello data.</span></span> <span data-ttu-id="47acb-126">다음 해당 hello 확인 하이브리드 id 솔루션을 계획 하는 경우 게시 된 질문은 tooyour 조직의 요구 사항에 따라:</span><span class="sxs-lookup"><span data-stu-id="47acb-126">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

## <a name="data-protection-at-rest"></a><span data-ttu-id="47acb-127">휴지 상태의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="47acb-127">Data protection at rest</span></span>
<span data-ttu-id="47acb-128">Hello 데이터 (장치, 클라우드 또는 온-프레미스) 미사용 위치에 관계 없이 반드시 tooperform 평가 toounderstand hello 조직 이런 점에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-128">Regardless of where hello data is at rest (device, cloud or on-premises), it is important tooperform an assessment toounderstand hello organization needs in this regard.</span></span> <span data-ttu-id="47acb-129">이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-129">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="47acb-130">미사용 데이터 tooprotect 회사에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="47acb-130">Does your company need tooprotect data at rest?</span></span>
  * <span data-ttu-id="47acb-131">그렇다면 현재 온-프레미스 인프라와 hello 하이브리드 identity 솔루션 수 toointegrate은?</span><span class="sxs-lookup"><span data-stu-id="47acb-131">If yes, is hello hybrid identity solution able toointegrate with your current on-premises infrastructure?</span></span>
  * <span data-ttu-id="47acb-132">그렇다면 hello 하이브리드 identity 솔루션 수 toointegrate hello 클라우드에 있는 작업으로는?</span><span class="sxs-lookup"><span data-stu-id="47acb-132">If yes, is hello hybrid identity solution able toointegrate with your workloads located in hello cloud?</span></span>
* <span data-ttu-id="47acb-133">Hello 클라우드 id 관리 수 tooprotect hello 사용자의 자격 증명 및 hello 클라우드에 저장 된 데이터를 다른 인가요?</span><span class="sxs-lookup"><span data-stu-id="47acb-133">Is hello cloud identity management able tooprotect hello user’s credentials and other data stored in hello cloud?</span></span>

## <a name="data-protection-in-transit"></a><span data-ttu-id="47acb-134">전송 중인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="47acb-134">Data protection in transit</span></span>
<span data-ttu-id="47acb-135">Hello 장치와 hello 데이터 센터 간 또는 hello 장치와 hello 클라우드 간에 전송 되는 데이터를 보호 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-135">Data in transit between hello device and hello datacenter or between hello device and hello cloud must be protected.</span></span> <span data-ttu-id="47acb-136">그러나 전송 중인 상태는 반드시 클라우드 서비스 외부의 구성 요소와 통신 프로세스를 의미하지 않습니다. 또한 예를 들어 두 가상 네트워크 간에 내부적으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-136">However, being in-transit does not necessarily mean a communications process with a component outside of your cloud service; it moves internally, also, such as between two virtual networks.</span></span> <span data-ttu-id="47acb-137">이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-137">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="47acb-138">Tooprotect 전송 중인 데이터를에서 회사에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="47acb-138">Does your company need tooprotect data in transit?</span></span>
  * <span data-ttu-id="47acb-139">그렇다면 hello 하이브리드 identity 솔루션 수 toointegrate SSL/TLS 보안 컨트롤은?</span><span class="sxs-lookup"><span data-stu-id="47acb-139">If yes, is hello hybrid identity solution able toointegrate with secure controls such as SSL/TLS?</span></span>
* <span data-ttu-id="47acb-140">Hello 클라우드 id 관리는 hello 트래픽 tooand 서명 hello 디렉터리 저장소 (내부 및 데이터 센터 간) 내에서 유지?</span><span class="sxs-lookup"><span data-stu-id="47acb-140">Does hello cloud identity management keep hello traffic tooand within hello directory store (within and between datacenters) signed?</span></span>

## <a name="compliance"></a><span data-ttu-id="47acb-141">규정 준수</span><span class="sxs-lookup"><span data-stu-id="47acb-141">Compliance</span></span>
<span data-ttu-id="47acb-142">규정, 법률 및 규정 준수 요구 사항을 회사 속하는 toohello 업계에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-142">Regulations, laws and regulatory compliance requirements will vary according toohello industry that your company belongs.</span></span> <span data-ttu-id="47acb-143">높은 업계 규정된에 회사 id 관리 문제 관련된 toocompliance 문제를 해결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-143">Companies in high regulated industries must address identity-management concerns related toocompliance issues.</span></span> <span data-ttu-id="47acb-144">Sarbanes-oxley (SOX), Health Insurance Portability hello 및 Accountability Act (HIPAA) 등의 규정 hello Gramm-Leach-Bliley Act (GLBA) 및 id 및 액세스에 대 한 hello Payment Card Industry Data Security Standard (PCI DSS)은 매우 엄격한 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-144">Regulations such as Sarbanes-Oxley (SOX), hello Health Insurance Portability and Accountability Act (HIPAA), hello Gramm-Leach-Bliley Act (GLBA) and hello Payment Card Industry Data Security Standard (PCI DSS) are very strict regarding identity and access.</span></span> <span data-ttu-id="47acb-145">회사에서 채택할 hello 하이브리드 id 솔루션에 하나 이상의 이러한 규정 hello 요구 사항에 맞는 hello 핵심 기능이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-145">hello hybrid identity solution that your company will adopt must have hello core capabilities that will fulfill hello requirements of one or more of these regulations.</span></span> <span data-ttu-id="47acb-146">이 영역에 대 한 질문에 따라 해당 hello 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-146">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="47acb-147">Hello 하이브리드 id 솔루션 hello 비즈니스 규정 요구 사항을 준수 하는?</span><span class="sxs-lookup"><span data-stu-id="47acb-147">Is hello hybrid identity solution compliant with hello regulatory requirements for your business?</span></span>
* <span data-ttu-id="47acb-148">회사 toobe 준수 규정 요구 사항 수 있게 해 주는 기능에는 hello 하이브리드 id 솔루션 내장?</span><span class="sxs-lookup"><span data-stu-id="47acb-148">Does hello hybrid identity solution has built in capabilities that will enable your company toobe compliant regulatory requirements?</span></span> 

> [!NOTE]
> <span data-ttu-id="47acb-149">각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-149">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="47acb-150">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-150">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="47acb-151">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47acb-151">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="47acb-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47acb-152">Next steps</span></span>
 [<span data-ttu-id="47acb-153">콘텐츠 관리 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="47acb-153">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a><span data-ttu-id="47acb-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="47acb-154">See Also</span></span>
[<span data-ttu-id="47acb-155">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="47acb-155">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

