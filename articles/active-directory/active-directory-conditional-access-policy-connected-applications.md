---
title: "Azure Active Directory 장치 기반 조건부 액세스 정책이 aaaConfigure | Microsoft Docs"
description: "어떻게 tooconfigure Azure Active Directory 장치 기반 조건부 액세스 정책에 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="f994d-103">Azure Active Directory 장치 기반 조건부 액세스 정책 구성</span><span class="sxs-lookup"><span data-stu-id="f994d-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="f994d-104">[Azure AD(Azure Active Directory) 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 사용하여 권한 있는 사용자가 리소스를 액세스하는 방법을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="f994d-105">예를 들어 hello toocertain 리소스 tootrusted 장치에 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="f994d-106">신뢰할 수 있는 장치를 요구하는 조건부 액세스 정책을 장치 기반 조건부 액세스 정책이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="f994d-107">이 항목에서는 Azure AD에 연결 된 응용 프로그램에 대 한 정책 tooconfigure 장치 기반 조건부 액세스 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="f994d-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f994d-108">Before you begin</span></span>

<span data-ttu-id="f994d-109">장치 기반 조건부 액세스는 **Azure AD 조건부 액세스**와 **Azure AD 장치 관리**를 함께 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="f994d-110">가 아닌 이러한 영역 중 하나에 대해 잘 알고 아직 hello 이벤트에 대 한 다음 항목을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="f994d-111">**[Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)**  -이 항목에서는 액세스 하 고 관련된 용어를 hello 조건부의 개념적인 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="f994d-112">**[Azure Active Directory에서 소개 toodevice 관리](device-management-introduction.md)**  -이 항목에서는 간략히 hello의 다양 한 옵션이 있는 Azure AD 사용 하 여 tooconnect 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="f994d-113">신뢰할 수 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f994d-113">Trusted devices</span></span>

<span data-ttu-id="f994d-114">먼저 모바일, 클라우드 우선 세계에서 Azure Active Directory single sign on toodevices, 앱 및 서비스를 어디에서 든 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="f994d-115">특정 toohello 적절 한 사용자 액세스를 부여, 사용자 환경에서 리소스 충분 한 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="f994d-116">또한 toohello 적절 한 사용자를도 필요할 수 신뢰할 수 있는 장치 toobe tooaccess 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="f994d-117">사용자 환경에서 정의할 수 있습니다에 기반 하는 신뢰할 수 있는 장치는 다음 구성 요소 hello:</span><span class="sxs-lookup"><span data-stu-id="f994d-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="f994d-118">hello [장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms) 장치에서</span><span class="sxs-lookup"><span data-stu-id="f994d-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="f994d-119">장치는 규정을 준수하는지 여부</span><span class="sxs-lookup"><span data-stu-id="f994d-119">Whether a device is compliant</span></span>
- <span data-ttu-id="f994d-120">장치가 도메인에 가입되어 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="f994d-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="f994d-121">hello [장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms) 장치에서 실행 되는 hello 운영 체제의 특징은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="f994d-122">장치 기반 조건부 액세스 정책에서 액세스 toocertain 리소스 toospecific 장치 플랫폼을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="f994d-123">장치 기반 조건부 액세스 정책에서 신뢰할 수 있는 장치 toobe 준수 상태로 표시 됨을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="f994d-125">장치는 hello 디렉터리 내에서 호환으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="f994d-126">Intune</span><span class="sxs-lookup"><span data-stu-id="f994d-126">Intune</span></span> 
- <span data-ttu-id="f994d-127">Azure AD와 통합되는 타사 모바일 장치 관리 시스템</span><span class="sxs-lookup"><span data-stu-id="f994d-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="f994d-128">만 있는 장치를 연결 된 tooAzure AD 규격으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="f994d-129">장치 tooAzure Active Directory tooconnect hello 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="f994d-130">Azure AD 등록</span><span class="sxs-lookup"><span data-stu-id="f994d-130">Azure AD registered</span></span>
- <span data-ttu-id="f994d-131">Azure AD 가입</span><span class="sxs-lookup"><span data-stu-id="f994d-131">Azure AD joined</span></span>
- <span data-ttu-id="f994d-132">하이브리드 Azure AD 가입</span><span class="sxs-lookup"><span data-stu-id="f994d-132">Hybrid Azure AD joined</span></span>

    ![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="f994d-134">온-프레미스 AD (Active Directory) 공간을 설정한 경우에 연결 된 tooAzure AD 하지만 신뢰할 수 있는 조인된 tooyour AD toobe 되지 않는 장치를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="f994d-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f994d-136">Next steps</span></span>

<span data-ttu-id="f994d-137">장치 기반 조건부 액세스 정책이 사용자 환경에서를 구성 하기 전에 hello 살펴보면 취해야 [Azure Active Directory의 조건부 액세스에 대 한 유용한](active-directory-conditional-access-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f994d-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

