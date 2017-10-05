---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하는 개발자 정보 | Microsoft Docs"
description: "사용자 지정 정책으로 Azure AD B2C를 구성 및 유지 관리하는 개발자를 위한 정보"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="c2ba8-103">Azure Active Directory B2C 사용자 지정 정책 공개 미리 보기에 대한 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c2ba8-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="c2ba8-104">사용자 지정 정책 기능 집합은 현재 모든 Azure Active Directory B2C(Azure AD B2C) 고객에 대해 공개 미리 보기에서 평가용으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="c2ba8-105">이 기능 집합은 가장 복잡한 ID 솔루션을 구축하는 고급 ID 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="c2ba8-106">현재, 이 기능 집합을 사용하려면 개발자가 XML 파일 편집을 통해 ID 경험 프레임워크를 직접 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="c2ba8-107">이 구성 방법은 강력하고 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="c2ba8-108">ID 경험 프레임워크를 사용하는 고급 ID 개발자는 연습을 완료하고 참조 문서를 확인하여 시간을 투자할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="c2ba8-109">이 공개 미리 보기에 포함된 기능</span><span class="sxs-lookup"><span data-stu-id="c2ba8-109">Features included in this public preview</span></span>
<span data-ttu-id="c2ba8-110">공개 검토에 포함된 새 기능을 통해 개발자는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="c2ba8-111">사용자 지정 정책을 사용하여 사용자 지정 인증 사용자 경험을 작성 및 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="c2ba8-112">클레임 공급자 간의 교환으로 사용자 경험을 단계별로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="c2ba8-113">사용자 경험에서 조건부 분기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="c2ba8-114">사용자 지정 인증 사용자 경험에서 REST API 사용 서비스를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="c2ba8-115">OpenIDConnect 표준과 호환되는 ID 공급자와의 페더레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="c2ba8-116">SAML 2.0 프로토콜을 준수하는 ID 공급자와의 페더레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="c2ba8-117">공개 미리 보기 약관</span><span class="sxs-lookup"><span data-stu-id="c2ba8-117">Terms of the public preview</span></span>

* <span data-ttu-id="c2ba8-118">새 기능의 사용은 평가 목적으로만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="c2ba8-119">새 기능은 프로덕션 환경에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="c2ba8-120">Service Level Agreement(서비스 수준 약정)는 새 기능에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="c2ba8-121">정식 지원 채널을 통해 지원 요청을 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="c2ba8-122">일반 공급에 대해 정해진 날짜는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="c2ba8-123">Microsoft의 재량에 따라 어떠한 이유로든, Azure AD B2C 제품 정관의 범위를 벗어나는 시나리오 및 사용자 경험을 고객 ID 및 액세스 관리(CIAM) 플랫폼으로 서비스하도록 플래그를 지정하고 거부 또는 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="c2ba8-124">사용자 지정 정책 기능 집합 개발자의 책임</span><span class="sxs-lookup"><span data-stu-id="c2ba8-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="c2ba8-125">수동 정책 구성은 Azure AD B2C의 기본 플랫폼에 대해 낮은 수준의 액세스 권한을 부여하며 완전히 사용자 지정할 수 있는 보안 프레임워크를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="c2ba8-126">다각적인 사용자 지정 ID 공급자, 트러스트 관계, 외부 서비스와의 통합 및 단계별 워크플로 관계로 인해, 이를 사용하는 고급 개발자의 요구가 더욱 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="c2ba8-127">공개 미리 보기를 최대한 활용하기 위해 사용자 지정 정책 기능 집합을 사용하는 개발자는 다음 지침을 준수하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="c2ba8-128">ID 경험 엔진의 구성 언어 및 키/암호 관리에 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="c2ba8-129">시나리오 및 사용자 지정 통합을 직접 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="c2ba8-130">체계적인 시나리오 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="c2ba8-131">최소 1개의 개발/테스트 환경과 1개의 프로덕션 환경을 구축하여 소프트웨어 개발 및 스테이징 모범 사례를 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="c2ba8-132">사용자와 통합된 ID 공급자 및 서비스에 대한 새로운 개발 정보를 바로 입수합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="c2ba8-133">예를 들어 기밀 변경 내용과 예정되었거나 갑작스럽게 진행되는 서비스 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="c2ba8-134">활성 모니터링을 설정하고 프로덕션 환경의 응답성을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="c2ba8-135">연락처 전자 메일 주소를 최신 상태로 유지하고 Microsoft 라이브 사이트 팀 전자 메일에 즉시 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="c2ba8-136">Microsoft 라이브 사이트 팀에서 권고할 때 시기 적절하게 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="c2ba8-137">이러한 기능은 결국 Azure AD 기본 제공 정책에 포함되어 모든 개발자가 보다 쉽게 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ba8-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2ba8-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2ba8-138">Next steps</span></span>
<span data-ttu-id="c2ba8-139">[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="c2ba8-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
