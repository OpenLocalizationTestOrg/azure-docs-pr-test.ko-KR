---
title: "Azure Active Directory 장치 기반 조건부 액세스 정책 구성 | Microsoft Docs"
description: "Azure Active Directory 장치 기반 조건부 액세스 정책을 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="909ac-103">Azure Active Directory 장치 기반 조건부 액세스 정책 구성</span><span class="sxs-lookup"><span data-stu-id="909ac-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="909ac-104">[Azure AD(Azure Active Directory) 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 사용하여 권한 있는 사용자가 리소스를 액세스하는 방법을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="909ac-105">예를 들어 특정 리소스에 대한 액세스를 신뢰할 수 있는 장치로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="909ac-106">신뢰할 수 있는 장치를 요구하는 조건부 액세스 정책을 장치 기반 조건부 액세스 정책이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="909ac-107">이 항목에서는 Azure AD 연결 응용 프로그램에 대한 장치 기반 조건부 액세스 정책을 구성하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="909ac-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="909ac-108">Before you begin</span></span>

<span data-ttu-id="909ac-109">장치 기반 조건부 액세스는 **Azure AD 조건부 액세스**와 **Azure AD 장치 관리**를 함께 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="909ac-110">이러한 내용에 익숙하지 않은 경우 먼저 다음 항목을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="909ac-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="909ac-111">**[Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)** - 이 항목에서는 조건부 액세스 및 관련 용어에 대한 개념적 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="909ac-112">**[Azure Active Directory의 장치 관리 소개](device-management-introduction.md)**  - 이 항목에서는 Azure AD에 장치를 연결할 때 사용할 수 있는 다양한 옵션에 대해 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="909ac-113">신뢰할 수 있는 장치</span><span class="sxs-lookup"><span data-stu-id="909ac-113">Trusted devices</span></span>

<span data-ttu-id="909ac-114">모바일 우선, 클라우드 우선 세계에서 Azure Active Directory는 어디에서나 장치, 앱 및 서비스에 대한 Single Sign-On을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="909ac-115">작업 환경의 특정 리소스의 경우, 적절한 사용자에게 액세스 권한을 부여하는 것만으로 충분하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="909ac-116">적절한 사용자 외에도, 리소스에 액세스할 때 신뢰할 수 있는 장치를 사용하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="909ac-117">사용자 환경에서 다음 구성 요소 중에서 장치를 신뢰할 수 있는 장치로 만들어주는 요인을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="909ac-118">장치의 [장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms)</span><span class="sxs-lookup"><span data-stu-id="909ac-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="909ac-119">장치는 규정을 준수하는지 여부</span><span class="sxs-lookup"><span data-stu-id="909ac-119">Whether a device is compliant</span></span>
- <span data-ttu-id="909ac-120">장치가 도메인에 가입되어 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="909ac-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="909ac-121">[장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms)은 다음 장치에서 실행되는 운영 체제를 특징으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="909ac-122">장치 기반 조건부 액세스 정책에서 특정 리소스에 대 한 액세스를 특정 장치 플랫폼으로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="909ac-123">장치 기반 조건부 액세스 정책에서 신뢰할 수 있는 장치를 규격으로 표시하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="909ac-125">장치는 다음을 통해 디렉터리에 규격으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="909ac-126">Intune</span><span class="sxs-lookup"><span data-stu-id="909ac-126">Intune</span></span> 
- <span data-ttu-id="909ac-127">Azure AD와 통합되는 타사 모바일 장치 관리 시스템</span><span class="sxs-lookup"><span data-stu-id="909ac-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="909ac-128">Azure AD에 연결된 장치만 규격으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="909ac-129">장치를 Azure Active Directory에 연결하려는 경우 다음 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="909ac-130">Azure AD 등록</span><span class="sxs-lookup"><span data-stu-id="909ac-130">Azure AD registered</span></span>
- <span data-ttu-id="909ac-131">Azure AD 가입</span><span class="sxs-lookup"><span data-stu-id="909ac-131">Azure AD joined</span></span>
- <span data-ttu-id="909ac-132">하이브리드 Azure AD 가입</span><span class="sxs-lookup"><span data-stu-id="909ac-132">Hybrid Azure AD joined</span></span>

    ![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="909ac-134">온-프레미스 AD(Active Directory) 공간을 설정한 경우 Azure AD에 연결되어 있지 않지만 AD에 가입된 장치는 신뢰할 수 있는 장치로 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="909ac-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="909ac-136">Next steps</span></span>

<span data-ttu-id="909ac-137">환경에서 장치 기반 조건부 액세스 정책을 구성하기 전에 [Azure Active Directory의 조건부 액세스 모범 사례](active-directory-conditional-access-best-practices.md)를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="909ac-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

