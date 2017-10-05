---
title: "DirSync 및 Azure AD Sync에서 업그레이드 | Microsoft Docs"
description: "DirSync 및 Azure AD Sync에서 Azure AD Connect로 업그레이드하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3674670e10500d2992539ab60fbdb31b666fcf9a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a><span data-ttu-id="cde5e-103">Windows Azure Active Directory Sync 및 Azure Active Directory Sync 업그레이드</span><span class="sxs-lookup"><span data-stu-id="cde5e-103">Upgrade Windows Azure Active Directory Sync and Azure Active Directory Sync</span></span>
<span data-ttu-id="cde5e-104">Azure AD Connect는 온-프레미스 디렉터리를 Azure AD와 Office 365에 연결하는 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-104">Azure AD Connect is the best way to connect your on-premises directory with Azure AD and Office 365.</span></span> <span data-ttu-id="cde5e-105">이제 이러한 도구가 사용되지 않으며 2017년 4월 13일에 지원이 종료될 예정이므로 Microsoft Azure Active Directory 동기화(DirSync) 또는 Azure AD Sync에서 Azure AD Connect로 지금 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-105">This is a great time to upgrade to Azure AD Connect from Windows Azure Active Directory Sync (DirSync) or Azure AD Sync as these tools are now deprecated and will reach end of support on April 13, 2017.</span></span>

<span data-ttu-id="cde5e-106">사용 중단되는 이 두 가지 ID 동기화 도구는 단일 포리스트 고객(DirSync)과 다중 포리스트 및 기타 고급 고객(Azure AD Sync)을 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-106">The two identity synchronization tools that are deprecated were offered for single forest customers (DirSync) and for multi-forest and other advanced customers (Azure AD Sync).</span></span> <span data-ttu-id="cde5e-107">이러한 이전 도구는 모든 시나리오에 사용할 수 있는 단일 솔루션(Azure AD Connect)으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-107">These older tools have been replaced with a single solution that is available for all scenarios: Azure AD Connect.</span></span> <span data-ttu-id="cde5e-108">이 도구는 새로운 기능, 향상된 기능 및 새로운 시나리오에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-108">It offers new functionality, feature enhancements, and support for new scenarios.</span></span> <span data-ttu-id="cde5e-109">온-프레미스 ID 데이터를 Azure AD 및 Office 365로 계속 동기화하려면 Azure AD Connect로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-109">To be able to continue to synchronize your on-premises identity data to Azure AD and Office 365, we strongly recommend that you upgrade to Azure AD Connect.</span></span>

<span data-ttu-id="cde5e-110">DirSync의 마지막 버전은 2014년 7월에 릴리스되었으며 Azure AD Sync의 마지막 버전은 2015년 5월에 릴리스되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-110">The last release of DirSync was released in July 2014 and the last release of Azure AD Sync was released in May 2015.</span></span>

## <a name="what-is-azure-ad-connect"></a><span data-ttu-id="cde5e-111">Azure AD Connect의 정의</span><span class="sxs-lookup"><span data-stu-id="cde5e-111">What is Azure AD Connect</span></span>
<span data-ttu-id="cde5e-112">Azure AD Connect는 DirSync 및 Azure AD Sync의 후속 도구로서,</span><span class="sxs-lookup"><span data-stu-id="cde5e-112">Azure AD Connect is the successor to DirSync and Azure AD Sync.</span></span> <span data-ttu-id="cde5e-113">이 두 도구가 지원하는 모든 시나리오를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-113">It combines all scenarios these two supported.</span></span> <span data-ttu-id="cde5e-114">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-114">You can read more about it in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="deprecation-schedule"></a><span data-ttu-id="cde5e-115">사용 중단 일정</span><span class="sxs-lookup"><span data-stu-id="cde5e-115">Deprecation schedule</span></span>
| <span data-ttu-id="cde5e-116">Date</span><span class="sxs-lookup"><span data-stu-id="cde5e-116">Date</span></span> | <span data-ttu-id="cde5e-117">주석</span><span class="sxs-lookup"><span data-stu-id="cde5e-117">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="cde5e-118">2016년 4월 13일</span><span class="sxs-lookup"><span data-stu-id="cde5e-118">April 13, 2016</span></span> |<span data-ttu-id="cde5e-119">Microsoft Azure Active Directory 동기화("DirSync") 및 Azure Active Directory 동기화("Azure AD Sync")가 사용 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-119">Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”) are announced as deprecated.</span></span> |
| <span data-ttu-id="cde5e-120">2017년 4월 13일</span><span class="sxs-lookup"><span data-stu-id="cde5e-120">April 13, 2017</span></span> |<span data-ttu-id="cde5e-121">지원이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-121">Support ends.</span></span> <span data-ttu-id="cde5e-122">이제 고객은 Azure AD Connect로 업그레이드해야만 지원 사례를 개설할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-122">Customers will no longer be able to open a support case without upgrading to Azure AD Connect first.</span></span> |
|<span data-ttu-id="cde5e-123">2017년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="cde5e-123">December 31, 2017</span></span>|<span data-ttu-id="cde5e-124">Azure AD는 더 이상 Windows Azure Active Directory Sync(“DirSync”) 및 Microsoft Azure Active Directory Sync(“Azure AD Sync”)의 통신을 수락하지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-124">Azure AD will no longer accept communications from Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”).</span></span>

## <a name="how-to-transition-to-azure-ad-connect"></a><span data-ttu-id="cde5e-125">Azure AD Connect로 전환하는 방법</span><span class="sxs-lookup"><span data-stu-id="cde5e-125">How to transition to Azure AD Connect</span></span>
<span data-ttu-id="cde5e-126">DirSync를 실행 중인 경우 전체 업그레이드와 병렬 배포의 두 가지 방법으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-126">If you are running DirSync, there are two ways you can upgrade: In-place upgrade and parallel deployment.</span></span> <span data-ttu-id="cde5e-127">전체 업그레이드는 대부분의 고객에게 권장되며, 최신 운영 체제가 설치되어 있고 개체 수가 50,000개 미만인 경우에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-127">An in-place upgrade is recommended for most customers and if you have a recent operating system and less than 50,000 objects.</span></span> <span data-ttu-id="cde5e-128">그렇지 않은 경우에는 DirSync 구성이 Azure AD Connect를 실행하는 새 서버로 전환되는 병렬 배포를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-128">In other cases, it is recommended to do a parallel deployment where your DirSync configuration is moved to a new server running Azure AD Connect.</span></span>

<span data-ttu-id="cde5e-129">Azure AD Sync를 사용하는 경우에는 전체 업그레이드가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-129">If you use Azure AD Sync, then an in-place upgrade is recommended.</span></span> <span data-ttu-id="cde5e-130">필요한 경우 새 Azure AD Connect 서버를 병렬로 설치하고 Azure AD Sync 서버에서 Azure AD Connect로 스윙 마이그레이션을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-130">If you want to, it is possible to install a new Azure AD Connect server in parallel and do a swing migration from your Azure AD Sync server to Azure AD Connect.</span></span>

| <span data-ttu-id="cde5e-131">해결 방법</span><span class="sxs-lookup"><span data-stu-id="cde5e-131">Solution</span></span> | <span data-ttu-id="cde5e-132">시나리오</span><span class="sxs-lookup"><span data-stu-id="cde5e-132">Scenario</span></span> |
| --- | --- |
| [<span data-ttu-id="cde5e-133">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="cde5e-133">Upgrade from DirSync</span></span>](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li><span data-ttu-id="cde5e-134">기존 DirSync 서버를 이미 실행 중인 경우</span><span class="sxs-lookup"><span data-stu-id="cde5e-134">If you have an existing DirSync server already running.</span></span></li> |
| [<span data-ttu-id="cde5e-135">Azure AD Sync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="cde5e-135">Upgrade from Azure AD Sync</span></span>](active-directory-aadconnect-upgrade-previous-version.md) |<li><span data-ttu-id="cde5e-136">Azure AD Sync에서 전환하는 경우</span><span class="sxs-lookup"><span data-stu-id="cde5e-136">If you are moving from Azure AD Sync.</span></span></li> |

<span data-ttu-id="cde5e-137">DirSync에서 Azure AD Connect로 전체 업그레이드를 수행하는 방법은 이 Channel 9 동영상을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cde5e-137">If you want to see how to do an in-place upgrade from DirSync to Azure AD Connect, then see this Channel 9 video:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a><span data-ttu-id="cde5e-138">FAQ</span><span class="sxs-lookup"><span data-stu-id="cde5e-138">FAQ</span></span>
<span data-ttu-id="cde5e-139">**Q: Azure 팀에서 메일 알림을 받았거나 Office 365 메시지 센터에서 메시지를 받았지만 Connect를 사용하고 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="cde5e-139">**Q: I have received an email notification from the Azure Team and/or a message from the Office 365 message center, but I am using Connect.**</span></span>  
<span data-ttu-id="cde5e-140">빌드 번호 1.0.\*.0(사전 1.1 릴리스 사용)의 Azure AD Connect를 사용하는 고객에게도 알림을 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-140">The notification was also sent to customers using Azure AD Connect with a build number 1.0.\*.0 (using a pre-1.1 release).</span></span> <span data-ttu-id="cde5e-141">고객은 Azure AD Connect 릴리스를 최신 상태로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-141">Microsoft recommends customers to stay current with Azure AD Connect releases.</span></span> <span data-ttu-id="cde5e-142">1.1 버전에 도입된 [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 기능은 Azure AD Connect가 항상 최신 버전으로 설치되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-142">The [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature introduced in 1.1 makes it easy to always have a recent version of Azure AD Connect installed.</span></span>

<span data-ttu-id="cde5e-143">**Q: DirSync/Azure AD Sync의 작동이 2017년 4월 13일에 중지됩니까?**</span><span class="sxs-lookup"><span data-stu-id="cde5e-143">**Q: Will DirSync/Azure AD Sync stop working on April 13, 2017?**</span></span>  
<span data-ttu-id="cde5e-144">DirSync/Azure AD Sync는 2017년 4월 13일까지 계속 작동할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-144">DirSync/Azure AD Sync will continue to work on April 13th 2017.</span></span>  <span data-ttu-id="cde5e-145">그러나 Azure AD는 2017년 12월 31일이 되면 더 이상 DirSync/Azure AD Sync의 통신을 수락하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-145">However, Azure AD will no longer accept communications from DirSync/Azure AD Sync on December 31st 2017.</span></span>

<span data-ttu-id="cde5e-146">**Q: 어떤 DirSync 버전에서 업그레이드할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="cde5e-146">**Q: Which DirSync versions can I upgrade from?**</span></span>  
<span data-ttu-id="cde5e-147">현재 사용 중인 모든 DirSync 릴리스의 업그레이드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-147">It is supported to upgrade from any DirSync release currently being used.</span></span>

<span data-ttu-id="cde5e-148">**Q: FIM/MIM용 Azure AD 커넥터는 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="cde5e-148">**Q: What about the Azure AD Connector for FIM/MIM?**</span></span>  
<span data-ttu-id="cde5e-149">FIM/MIM용 Azure AD 커넥터는 사용 중단되는 것으로 발표되지 **않았습니다**.</span><span class="sxs-lookup"><span data-stu-id="cde5e-149">The Azure AD Connector for FIM/MIM has **not** been announced as deprecated.</span></span> <span data-ttu-id="cde5e-150">현재 **기능 동결**상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-150">It is at **feature freeze**; no new functionality is added and it receives no bug fixes.</span></span> <span data-ttu-id="cde5e-151">즉, 새 기능이 추가되지 않으며 버그 수정이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-151">Microsoft recommends customers using it to plan to move from it to Azure AD Connect.</span></span> <span data-ttu-id="cde5e-152">고객은 Azure AD Connect로 전환할 계획을 수립하고, 이 커넥터를 사용하여 새 배포를 시작하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-152">It is strongly recommended to not start any new deployments using it.</span></span> <span data-ttu-id="cde5e-153">이 커넥터는 향후에 사용 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="cde5e-153">This Connector will be announced deprecated in the future.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cde5e-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cde5e-154">Additional Resources</span></span>
* [<span data-ttu-id="cde5e-155">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="cde5e-155">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
