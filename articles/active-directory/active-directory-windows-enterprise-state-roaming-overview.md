---
title: "엔터프라이즈 상태 로밍 개요 | Microsoft Docs"
description: "Windows 장치의 엔터프라이즈 상태 로밍 설정에 대한 정보를 제공합니다. 엔터프라이즈 상태 로밍은 사용자의 모든 Windows 장치에 통합된 환경을 제공하고 새 장치 구성에 드는 시간을 줄여 줍니다."
services: active-directory
keywords: "엔터프라이즈 상태 로밍이란, 엔터프라이즈 동기화, windows 클라우드"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: b3c01f8d332d26e92dc3052681a4b2c95142d440
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-state-roaming-overview"></a><span data-ttu-id="50e74-105">엔터프라이즈 상태 로밍 개요</span><span class="sxs-lookup"><span data-stu-id="50e74-105">Enterprise State Roaming overview</span></span>
<span data-ttu-id="50e74-106">Windows 10에서는 [Azure Active Directory(Azure AD)](active-directory-whatis.md) 사용자가 사용자 설정 및 응용 프로그램 설정 데이터를 클라우드와 안전하게 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-106">With Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) users gain the ability to securely synchronize their user settings and application settings data to the cloud.</span></span> <span data-ttu-id="50e74-107">엔터프라이즈 상태 로밍은 사용자의 모든 Windows 장치에 통합된 환경을 제공하고 새 장치 구성에 드는 시간을 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-107">Enterprise State Roaming provides users with a unified experience across their Windows devices and reduces the time needed for configuring a new device.</span></span> <span data-ttu-id="50e74-108">엔터프라이즈 상태 로밍은 Windows 8에서 처음 도입된 표준 [소비자 설정 동기화](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) 와 비슷한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-108">Enterprise State Roaming operates similar to the standard [consumer settings sync](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) that was first introduced in Windows 8.</span></span> <span data-ttu-id="50e74-109">뿐만 아니라 엔터프라이즈 상태 로밍은 다음 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-109">Additionally, Enterprise State Roaming offers:</span></span>

* <span data-ttu-id="50e74-110">**기업 데이터와 소비자 데이터 분리** - 조직에서 데이터를 제어할 수 있으며, 소비자 클라우드 계정에 회사 데이터가 섞이거나 엔터프라이즈 클라우드 계정에 기업 데이터가 섞이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-110">**Separation of corporate and consumer data** – Organizations are in control of their data, and there is no mixing of corporate data in a consumer cloud account or consumer data in an enterprise cloud account.</span></span>
* <span data-ttu-id="50e74-111">**보안 강화** – 데이터가 사용자의 Windows 10 장치에서 나가기 전에 Azure RMS(Azure Rights Management)를 사용하여 자동으로 암호화되고, 암호화된 상태로 클라우드에 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-111">**Enhanced security** – Data is automatically encrypted before leaving the user’s Windows 10 device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in the cloud.</span></span> <span data-ttu-id="50e74-112">설정 이름 및 Windows 앱 이름 같은 네임 스페이스를 제외한 모든 콘텐츠가 암호화된 상태로 클라우드에 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-112">All content stays encrypted at rest in the cloud, except for the namespaces, like settings names and Windows app names.</span></span>  
* <span data-ttu-id="50e74-113">**더 나은 관리 및 모니터링** – Azure AD 포털 통합을 통해 조직에서 누가, 어떤 장치에서 설정을 동기화할 수 있는지를 제어하고 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-113">**Better management and monitoring** – Provides control and visibility over who syncs settings in your organization and on which devices through the Azure AD portal integration.</span></span> 

<span data-ttu-id="50e74-114">엔터프라이즈 상태 로밍은 여러 Azure 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-114">Enterprise State Roaming is available in multiple Azure regions.</span></span> <span data-ttu-id="50e74-115">사용할 수 있는 지역 목록 업데이트는 Azure Active Directory의 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services) 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-115">You can find the updated list of available regions on the [Azure Services by Regions](https://azure.microsoft.com/regions/#services) page under Azure Active Directory.</span></span>

| <span data-ttu-id="50e74-116">문서</span><span class="sxs-lookup"><span data-stu-id="50e74-116">Article</span></span> | <span data-ttu-id="50e74-117">설명</span><span class="sxs-lookup"><span data-stu-id="50e74-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="50e74-118">Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화</span><span class="sxs-lookup"><span data-stu-id="50e74-118">Enable Enterprise State Roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md) |<span data-ttu-id="50e74-119">엔터프라이즈 상태 로밍은 프리미엄 Azure Active Directory(Azure AD)를 구독하는 모든 조직에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-119">Enterprise State Roaming is available to any organization with a Premium Azure Active Directory (Azure AD) subscription.</span></span> <span data-ttu-id="50e74-120">Azure AD 구독 방법에 대한 자세한 내용은 [Azure AD 제품](https://azure.microsoft.com/services/active-directory) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50e74-120">For more details on how to get an Azure AD subscription, see the [Azure AD product](https://azure.microsoft.com/services/active-directory) page.</span></span> |
| [<span data-ttu-id="50e74-121">설정 및 데이터 로밍 FAQ</span><span class="sxs-lookup"><span data-stu-id="50e74-121">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md) |<span data-ttu-id="50e74-122">이 토픽에서는 설정 및 앱 데이터 동기화에 대한 IT 관리자의 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-122">This topic answers some questions IT administrators might have about settings and app data sync.</span></span> |
| [<span data-ttu-id="50e74-123">설정 동기화에 대한 그룹 정책 및 MDM 설정</span><span class="sxs-lookup"><span data-stu-id="50e74-123">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |<span data-ttu-id="50e74-124">Windows 10은 설정 동기화를 제한하는 그룹 정책 및 MDM(모바일 장치 관리) 정책 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-124">Windows 10 provides Group Policy and mobile device management (MDM) policy settings to limit settings sync.</span></span> |
| [<span data-ttu-id="50e74-125">Windows 10 로밍 설정 참조</span><span class="sxs-lookup"><span data-stu-id="50e74-125">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |<span data-ttu-id="50e74-126">다음은 Windows 10에서 로밍 및/또는 백업되는 모든 설정의 전체 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-126">The following is a complete list of all the settings that will be roamed and/or backed-up in Windows 10.</span></span> |
| [<span data-ttu-id="50e74-127">문제 해결</span><span class="sxs-lookup"><span data-stu-id="50e74-127">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |<span data-ttu-id="50e74-128">이 토픽은 문제 해결을 위한 몇 가지 기본 단계를 살펴 보며 알려진 문제 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e74-128">This topic goes through some basic steps for troubleshooting, and contains a list of known issues.</span></span> |

