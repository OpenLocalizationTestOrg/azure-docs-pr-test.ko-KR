---
title: "디렉터리 동기화 및 Azure AD Sync에서 aaaUpgrade | Microsoft Docs"
description: "설명 방법을 디렉터리 동기화 및 Azure AD Sync tooAzure AD에서에서 tooupgrade 연결 합니다."
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
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a><span data-ttu-id="b2e40-103">Windows Azure Active Directory Sync 및 Azure Active Directory Sync 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b2e40-103">Upgrade Windows Azure Active Directory Sync and Azure Active Directory Sync</span></span>
<span data-ttu-id="b2e40-104">Azure AD Connect 가장 좋은 방법은 tooconnect Azure AD와 온-프레미스 디렉터리 hello는 및 Office 365 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-104">Azure AD Connect is hello best way tooconnect your on-premises directory with Azure AD and Office 365.</span></span> <span data-ttu-id="b2e40-105">이것이 좋은 시간 tooupgrade tooAzure Windows Azure Active Directory 동기화 (DirSync) 또는 Azure AD Sync에서 AD 연결 이러한 도구는 이제 사용 되지 않으며 2017 년 4 월 13에 대 한 지원의 끝에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-105">This is a great time tooupgrade tooAzure AD Connect from Windows Azure Active Directory Sync (DirSync) or Azure AD Sync as these tools are now deprecated and will reach end of support on April 13, 2017.</span></span>

<span data-ttu-id="b2e40-106">hello 두 id 동기화 도구의 사용 되지 않는 단일 포리스트 고객 (DirSync) 및 다중 포리스트 및 기타 고급 고객 (Azure AD Sync) 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-106">hello two identity synchronization tools that are deprecated were offered for single forest customers (DirSync) and for multi-forest and other advanced customers (Azure AD Sync).</span></span> <span data-ttu-id="b2e40-107">이러한 이전 도구는 모든 시나리오에 사용할 수 있는 단일 솔루션(Azure AD Connect)으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-107">These older tools have been replaced with a single solution that is available for all scenarios: Azure AD Connect.</span></span> <span data-ttu-id="b2e40-108">이 도구는 새로운 기능, 향상된 기능 및 새로운 시나리오에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-108">It offers new functionality, feature enhancements, and support for new scenarios.</span></span> <span data-ttu-id="b2e40-109">toobe 수 toocontinue toosynchronize 프로그램 identity 데이터 tooAzure 온-프레미스 AD 및 Office 365 좋습니다 tooAzure AD를 업그레이드 하는 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-109">toobe able toocontinue toosynchronize your on-premises identity data tooAzure AD and Office 365, we strongly recommend that you upgrade tooAzure AD Connect.</span></span>

<span data-ttu-id="b2e40-110">디렉터리 동기화의 마지막 릴리스입니다 hello은 2014 년 7 월에에서 발표 되었지만 및 Azure AD Sync의 hello 마지막 릴리스는 2015 년 5 월에에서 발표 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-110">hello last release of DirSync was released in July 2014 and hello last release of Azure AD Sync was released in May 2015.</span></span>

## <a name="what-is-azure-ad-connect"></a><span data-ttu-id="b2e40-111">Azure AD Connect의 정의</span><span class="sxs-lookup"><span data-stu-id="b2e40-111">What is Azure AD Connect</span></span>
<span data-ttu-id="b2e40-112">Azure AD Connect hello 후속 tooDirSync 및 Azure AD Sync가 있습니다. 이 두 도구가 지원하는 모든 시나리오를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-112">Azure AD Connect is hello successor tooDirSync and Azure AD Sync. It combines all scenarios these two supported.</span></span> <span data-ttu-id="b2e40-113">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-113">You can read more about it in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="deprecation-schedule"></a><span data-ttu-id="b2e40-114">사용 중단 일정</span><span class="sxs-lookup"><span data-stu-id="b2e40-114">Deprecation schedule</span></span>
| <span data-ttu-id="b2e40-115">Date</span><span class="sxs-lookup"><span data-stu-id="b2e40-115">Date</span></span> | <span data-ttu-id="b2e40-116">주석</span><span class="sxs-lookup"><span data-stu-id="b2e40-116">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="b2e40-117">2016년 4월 13일</span><span class="sxs-lookup"><span data-stu-id="b2e40-117">April 13, 2016</span></span> |<span data-ttu-id="b2e40-118">Microsoft Azure Active Directory 동기화("DirSync") 및 Azure Active Directory 동기화("Azure AD Sync")가 사용 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-118">Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”) are announced as deprecated.</span></span> |
| <span data-ttu-id="b2e40-119">2017년 4월 13일</span><span class="sxs-lookup"><span data-stu-id="b2e40-119">April 13, 2017</span></span> |<span data-ttu-id="b2e40-120">지원이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-120">Support ends.</span></span> <span data-ttu-id="b2e40-121">고객 수 tooopen tooAzure AD를 업그레이드 하지 않고 지원 케이스 더 이상 됩니다 먼저 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-121">Customers will no longer be able tooopen a support case without upgrading tooAzure AD Connect first.</span></span> |
|<span data-ttu-id="b2e40-122">2017년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="b2e40-122">December 31, 2017</span></span>|<span data-ttu-id="b2e40-123">Azure AD는 더 이상 Windows Azure Active Directory Sync(“DirSync”) 및 Microsoft Azure Active Directory Sync(“Azure AD Sync”)의 통신을 수락하지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-123">Azure AD will no longer accept communications from Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”).</span></span>

## <a name="how-tootransition-tooazure-ad-connect"></a><span data-ttu-id="b2e40-124">어떻게 tootransition tooAzure AD 연결</span><span class="sxs-lookup"><span data-stu-id="b2e40-124">How tootransition tooAzure AD Connect</span></span>
<span data-ttu-id="b2e40-125">DirSync를 실행 중인 경우 전체 업그레이드와 병렬 배포의 두 가지 방법으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-125">If you are running DirSync, there are two ways you can upgrade: In-place upgrade and parallel deployment.</span></span> <span data-ttu-id="b2e40-126">전체 업그레이드는 대부분의 고객에게 권장되며, 최신 운영 체제가 설치되어 있고 개체 수가 50,000개 미만인 경우에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-126">An in-place upgrade is recommended for most customers and if you have a recent operating system and less than 50,000 objects.</span></span> <span data-ttu-id="b2e40-127">경우에 따라 toodo 여기서 디렉터리 동기화 구성에는 병렬 배포에 Azure AD Connect를 실행 하는 새 tooa 서버 이동이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-127">In other cases, it is recommended toodo a parallel deployment where your DirSync configuration is moved tooa new server running Azure AD Connect.</span></span>

<span data-ttu-id="b2e40-128">Azure AD Sync를 사용하는 경우에는 전체 업그레이드가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-128">If you use Azure AD Sync, then an in-place upgrade is recommended.</span></span> <span data-ttu-id="b2e40-129">가능한 tooinstall 병렬로 새 Azure AD Connect 서버 및 Azure AD Sync 서버 tooAzure AD에서에서 회전 마이그레이션을 수행 하려는 경우, 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-129">If you want to, it is possible tooinstall a new Azure AD Connect server in parallel and do a swing migration from your Azure AD Sync server tooAzure AD Connect.</span></span>

| <span data-ttu-id="b2e40-130">해결 방법</span><span class="sxs-lookup"><span data-stu-id="b2e40-130">Solution</span></span> | <span data-ttu-id="b2e40-131">시나리오</span><span class="sxs-lookup"><span data-stu-id="b2e40-131">Scenario</span></span> |
| --- | --- |
| [<span data-ttu-id="b2e40-132">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b2e40-132">Upgrade from DirSync</span></span>](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li><span data-ttu-id="b2e40-133">기존 DirSync 서버를 이미 실행 중인 경우</span><span class="sxs-lookup"><span data-stu-id="b2e40-133">If you have an existing DirSync server already running.</span></span></li> |
| [<span data-ttu-id="b2e40-134">Azure AD Sync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b2e40-134">Upgrade from Azure AD Sync</span></span>](active-directory-aadconnect-upgrade-previous-version.md) |<li><span data-ttu-id="b2e40-135">Azure AD Sync에서 전환하는 경우</span><span class="sxs-lookup"><span data-stu-id="b2e40-135">If you are moving from Azure AD Sync.</span></span></li> |

<span data-ttu-id="b2e40-136">어떻게 toosee 사용 하려는 경우 전체 toodo AD Connect 디렉터리 동기화 tooAzure에서 업그레이드 한 다음이 채널 9 비디오를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b2e40-136">If you want toosee how toodo an in-place upgrade from DirSync tooAzure AD Connect, then see this Channel 9 video:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a><span data-ttu-id="b2e40-137">FAQ</span><span class="sxs-lookup"><span data-stu-id="b2e40-137">FAQ</span></span>
<span data-ttu-id="b2e40-138">**Q: 전자 메일 알림을 hello Azure 팀 및/또는 hello Office 365 메시지 센터에서 메시지를 받았는데 Connect를 사용 하 고 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b2e40-138">**Q: I have received an email notification from hello Azure Team and/or a message from hello Office 365 message center, but I am using Connect.**</span></span>  
<span data-ttu-id="b2e40-139">hello 알림은 toocustomers Azure AD Connect를 사용 하 여 빌드 번호 1.0도 전송 되었습니다. \*.0 (1.1 이전 릴리스를 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="b2e40-139">hello notification was also sent toocustomers using Azure AD Connect with a build number 1.0.\*.0 (using a pre-1.1 release).</span></span> <span data-ttu-id="b2e40-140">Azure AD Connect와 현재 toostay를 해제 하는 고객을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-140">Microsoft recommends customers toostay current with Azure AD Connect releases.</span></span> <span data-ttu-id="b2e40-141">hello [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 1.1에서 도입 된 기능을 쉽게 tooalways 통해 최신 버전의 Azure AD Connect 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-141">hello [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature introduced in 1.1 makes it easy tooalways have a recent version of Azure AD Connect installed.</span></span>

<span data-ttu-id="b2e40-142">**Q: DirSync/Azure AD Sync의 작동이 2017년 4월 13일에 중지됩니까?**</span><span class="sxs-lookup"><span data-stu-id="b2e40-142">**Q: Will DirSync/Azure AD Sync stop working on April 13, 2017?**</span></span>  
<span data-ttu-id="b2e40-143">DirSync/Azure AD Sync 13 2017 년 4 월에 toowork를 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-143">DirSync/Azure AD Sync will continue toowork on April 13th 2017.</span></span>  <span data-ttu-id="b2e40-144">그러나 Azure AD는 2017년 12월 31일이 되면 더 이상 DirSync/Azure AD Sync의 통신을 수락하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-144">However, Azure AD will no longer accept communications from DirSync/Azure AD Sync on December 31st 2017.</span></span>

<span data-ttu-id="b2e40-145">**Q: 어떤 DirSync 버전에서 업그레이드할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="b2e40-145">**Q: Which DirSync versions can I upgrade from?**</span></span>  
<span data-ttu-id="b2e40-146">현재 사용 중인 디렉터리 동기화 릴리스에서 지원 되는 tooupgrade 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-146">It is supported tooupgrade from any DirSync release currently being used.</span></span>

<span data-ttu-id="b2e40-147">**Q: FIM/MIM에 대 한 Azure AD 커넥터를 hello?**</span><span class="sxs-lookup"><span data-stu-id="b2e40-147">**Q: What about hello Azure AD Connector for FIM/MIM?**</span></span>  
<span data-ttu-id="b2e40-148">hello FIM/MIM에 대 한 Azure AD 커넥터에 **하지** 되었습니다 발표 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-148">hello Azure AD Connector for FIM/MIM has **not** been announced as deprecated.</span></span> <span data-ttu-id="b2e40-149">현재 **기능 동결**상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-149">It is at **feature freeze**; no new functionality is added and it receives no bug fixes.</span></span> <span data-ttu-id="b2e40-150">Microsoft 권장 tooplan toomove 여기에서 사용 하는 고객 tooAzure AD 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-150">Microsoft recommends customers using it tooplan toomove from it tooAzure AD Connect.</span></span> <span data-ttu-id="b2e40-151">강력히 권장 toonot 시작 모든 새 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-151">It is strongly recommended toonot start any new deployments using it.</span></span> <span data-ttu-id="b2e40-152">이 커넥터는 hello 향후에 더 이상 사용 되지 발표 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e40-152">This Connector will be announced deprecated in hello future.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2e40-153">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b2e40-153">Additional Resources</span></span>
* [<span data-ttu-id="b2e40-154">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="b2e40-154">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
