---
title: "aaaEnterprise 상태 로밍 개요 | Microsoft Docs"
description: "Windows 장치의 엔터프라이즈 상태 로밍 설정에 대한 정보를 제공합니다. 엔터프라이즈 상태 로밍 hello 소요 되는 새 장치를 구성 하는 데 필요한 시간이 단축 및 해당 Windows 장치 간에 통합 된 환경을 사용자를 제공 합니다."
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
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a><span data-ttu-id="4c052-105">엔터프라이즈 상태 로밍 개요</span><span class="sxs-lookup"><span data-stu-id="4c052-105">Enterprise State Roaming overview</span></span>
<span data-ttu-id="4c052-106">Windows 10과 [Azure Active Directory (Azure AD)](active-directory-whatis.md) 사용자 이득 hello 기능 toosecurely 해당 사용자 설정 및 응용 프로그램 설정 데이터 toohello 클라우드를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-106">With Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) users gain hello ability toosecurely synchronize their user settings and application settings data toohello cloud.</span></span> <span data-ttu-id="4c052-107">엔터프라이즈 상태 로밍 hello 소요 되는 새 장치를 구성 하는 데 필요한 시간이 단축 및 해당 Windows 장치 간에 통합 된 환경을 사용자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-107">Enterprise State Roaming provides users with a unified experience across their Windows devices and reduces hello time needed for configuring a new device.</span></span> <span data-ttu-id="4c052-108">비슷한 toohello 표준 작동 엔터프라이즈 상태 로밍 [소비자 설정 동기화](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) Windows 8에 처음 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-108">Enterprise State Roaming operates similar toohello standard [consumer settings sync](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) that was first introduced in Windows 8.</span></span> <span data-ttu-id="4c052-109">뿐만 아니라 엔터프라이즈 상태 로밍은 다음 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-109">Additionally, Enterprise State Roaming offers:</span></span>

* <span data-ttu-id="4c052-110">**기업 데이터와 소비자 데이터 분리** - 조직에서 데이터를 제어할 수 있으며, 소비자 클라우드 계정에 회사 데이터가 섞이거나 엔터프라이즈 클라우드 계정에 기업 데이터가 섞이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-110">**Separation of corporate and consumer data** – Organizations are in control of their data, and there is no mixing of corporate data in a consumer cloud account or consumer data in an enterprise cloud account.</span></span>
* <span data-ttu-id="4c052-111">**향상 된 보안** – 데이터는 Azure 권한 관리 (Azure RMS)를 사용 하 여 hello 사용자의 Windows 10 장치에서 없어지기 전에 자동으로 암호화 하 고 데이터를 안전 하 게 암호화 hello 클라우드에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-111">**Enhanced security** – Data is automatically encrypted before leaving hello user’s Windows 10 device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in hello cloud.</span></span> <span data-ttu-id="4c052-112">모든 콘텐츠를 안전 하 게 암호화 설정 이름 및 Windows 응용 프로그램 이름 같은 hello 네임 스페이스를 제외 하 고 hello 클라우드에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-112">All content stays encrypted at rest in hello cloud, except for hello namespaces, like settings names and Windows app names.</span></span>  
* <span data-ttu-id="4c052-113">**향상 된 관리 및 모니터링** – 조직에서, hello Azure AD 포털 통합을 통해 어떤 장치에서 설정을 동기화 되는 보다 제어 및 표시 유형 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-113">**Better management and monitoring** – Provides control and visibility over who syncs settings in your organization and on which devices through hello Azure AD portal integration.</span></span> 

<span data-ttu-id="4c052-114">엔터프라이즈 상태 로밍은 여러 Azure 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-114">Enterprise State Roaming is available in multiple Azure regions.</span></span> <span data-ttu-id="4c052-115">Hello에 사용할 수 있는 지역 hello 업데이트 목록을 찾을 수 있습니다 [지역으로 Azure 서비스](https://azure.microsoft.com/regions/#services) Azure Active Directory 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-115">You can find hello updated list of available regions on hello [Azure Services by Regions](https://azure.microsoft.com/regions/#services) page under Azure Active Directory.</span></span>

| <span data-ttu-id="4c052-116">문서</span><span class="sxs-lookup"><span data-stu-id="4c052-116">Article</span></span> | <span data-ttu-id="4c052-117">설명</span><span class="sxs-lookup"><span data-stu-id="4c052-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="4c052-118">Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화</span><span class="sxs-lookup"><span data-stu-id="4c052-118">Enable Enterprise State Roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md) |<span data-ttu-id="4c052-119">엔터프라이즈 상태 로밍 하는 것은 Premium Azure Active Directory (Azure AD) 구독에 사용할 수 있는 tooany 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-119">Enterprise State Roaming is available tooany organization with a Premium Azure Active Directory (Azure AD) subscription.</span></span> <span data-ttu-id="4c052-120">방법에 대 한 자세한 내용은 Azure AD 구독 tooget 참조 hello [Azure AD 제품](https://azure.microsoft.com/services/active-directory) 페이지.</span><span class="sxs-lookup"><span data-stu-id="4c052-120">For more details on how tooget an Azure AD subscription, see hello [Azure AD product](https://azure.microsoft.com/services/active-directory) page.</span></span> |
| [<span data-ttu-id="4c052-121">설정 및 데이터 로밍 FAQ</span><span class="sxs-lookup"><span data-stu-id="4c052-121">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md) |<span data-ttu-id="4c052-122">이 토픽에서는 설정 및 앱 데이터 동기화에 대한 IT 관리자의 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-122">This topic answers some questions IT administrators might have about settings and app data sync.</span></span> |
| [<span data-ttu-id="4c052-123">설정 동기화에 대한 그룹 정책 및 MDM 설정</span><span class="sxs-lookup"><span data-stu-id="4c052-123">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |<span data-ttu-id="4c052-124">Windows 10 모바일 장치 관리 (MDM) 정책 toolimit 설정 동기화 설정 및 그룹 정책을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-124">Windows 10 provides Group Policy and mobile device management (MDM) policy settings toolimit settings sync.</span></span> |
| [<span data-ttu-id="4c052-125">Windows 10 로밍 설정 참조</span><span class="sxs-lookup"><span data-stu-id="4c052-125">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |<span data-ttu-id="4c052-126">hello 다음은 됩니다 로밍 및/또는 수 백업 Windows 10에 있는 모든 hello 설정의 전체 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-126">hello following is a complete list of all hello settings that will be roamed and/or backed-up in Windows 10.</span></span> |
| [<span data-ttu-id="4c052-127">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4c052-127">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |<span data-ttu-id="4c052-128">이 토픽은 문제 해결을 위한 몇 가지 기본 단계를 살펴 보며 알려진 문제 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c052-128">This topic goes through some basic steps for troubleshooting, and contains a list of known issues.</span></span> |

