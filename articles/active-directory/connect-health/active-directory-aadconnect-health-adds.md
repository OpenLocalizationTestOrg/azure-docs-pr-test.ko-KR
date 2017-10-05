---
title: "AD DS와 함께 Azure AD Connect Health 사용 | Microsoft Docs"
description: "AD DS를 모니터링하는 방법을 설명하는 Azure AD Connect Health 페이지입니다."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9e5b45d71b978c383932409f0037a4f6f32d0cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a><span data-ttu-id="948eb-103">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="948eb-103">Using Azure AD Connect Health with AD DS</span></span>
<span data-ttu-id="948eb-104">다음 문서는 Azure AD Connect Health와 함께 Active Directory 도메인 서비스를 모니터링하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-104">The following documentation is specific to monitoring Active Directory Domain Services with Azure AD Connect Health.</span></span> <span data-ttu-id="948eb-105">지원되는 AD DS 버전은 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016입니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-105">The supported versions of AD DS are: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>

<span data-ttu-id="948eb-106">Azure AD Connect Health를 사용한 AD FS 모니터링에 대한 자세한 내용은 [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="948eb-106">For more information on monitoring AD FS with Azure AD Connect Health, see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="948eb-107">또한 Azure AD Connect Health와 함께 Azure AD Connect (동기화)를 모니터링하는 방법에 대한 정보는 [동기화를 위해 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="948eb-107">Additionally, for information on monitoring Azure AD Connect (Sync) with Azure AD Connect Health see [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md).</span></span>

![AD DS용 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a><span data-ttu-id="948eb-109">AD DS용 Azure AD Connect Health에 대한 경고</span><span class="sxs-lookup"><span data-stu-id="948eb-109">Alerts for Azure AD Connect Health for AD DS</span></span>
<span data-ttu-id="948eb-110">AD DS용 Azure AD Connect Health 내의 경고 섹션은 도메인 컨트롤러와 관련된 활성 경고 및 해결된 경고의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-110">The Alerts section within Azure AD Connect Health for AD DS, provides you a list of active and resolved alerts, related to your domain controllers.</span></span> <span data-ttu-id="948eb-111">활성 경고 또는 해결된 경고를 선택하면 해결 단계 및 지원 설명서로의 링크와 함께 추가 정보가 포함된 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-111">Selecting an active or resolved alert opens a new blade with additional information, along with resolution steps, and links to supporting documentation.</span></span> <span data-ttu-id="948eb-112">각 경고 유형에는 하나 이상의 인스턴스가 있고 이 인스턴스는 해당 특정 경고의 영향을 받는 도메인 컨트롤러 각각에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-112">Each alert type can have one or more instances, which correspond to each of the domain controllers affected by that particular alert.</span></span> <span data-ttu-id="948eb-113">경고 블레이드 하단 근처에서 영향을 받는 도메인 컨트롤러를 두 번 클릭하면 해당 경고 인스턴스에 대한 자세한 내용을 포함하는 추가적인 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-113">Near the bottom of the alert blade, you can double-click an affected domain controller to open an additional blade with more details about that alert instance.</span></span>

<span data-ttu-id="948eb-114">이 블레이드 내에서 경고에 대한 전자 메일 알림을 사용하도록 설정하고 보기의 시간 범위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-114">Within this blade, you can enable email notifications for alerts and change the time range in view.</span></span> <span data-ttu-id="948eb-115">시간 범위를 확장하면 이전에 해결된 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-115">Expanding the time range allows you to see prior resolved alerts.</span></span>

![Azure AD Connect 동기화 오류](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a><span data-ttu-id="948eb-117">도메인 컨트롤러 대시보드</span><span class="sxs-lookup"><span data-stu-id="948eb-117">Domain Controllers Dashboard</span></span>
<span data-ttu-id="948eb-118">이 대시보드에서는 모니터링 도메인 컨트롤러 각각의 주요 작업 메트릭 및 상태와 함께 사용자 환경의 토폴로지 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-118">This dashboard provides a topological view of your environment, along with key operational metrics and health status of each of your monitored domain controllers.</span></span> <span data-ttu-id="948eb-119">표시된 메트릭은 추가 조사가 필요할 수 있는 모든 도메인 컨트롤러를 신속하게 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-119">The presented metrics help to quickly identify, any domain controllers that might require further investigation.</span></span> <span data-ttu-id="948eb-120">기본적으로 열의 하위 집합만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-120">By default, only a subset of the columns is displayed.</span></span> <span data-ttu-id="948eb-121">하지만, 열 명령을 두 번 클릭하면 사용 가능한 열 집합 전체를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-121">However, you can find the entire set of available columns, by double-clicking the columns command.</span></span> <span data-ttu-id="948eb-122">가장 원하는 열을 선택하면 이 대시보드가 AD DS 환경의 상태를 한 곳에서 쉽게 볼 수 있는 곳으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-122">Selecting the columns that you most care about, turns this dashboard into a single and easy place to view the health of your AD DS environment.</span></span>

![도메인 컨트롤러](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

<span data-ttu-id="948eb-124">해당하는 도메인 또는 사이트에서 도메인 컨트롤러를 그룹화할 수 있으며 환경 토폴로지를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-124">Domain controllers can be grouped by their respective domain or site, which is helpful for understanding the environment topology.</span></span> <span data-ttu-id="948eb-125">마지막으로 블레이드 헤더를 두 번 클릭하면 사용 가능한 화면을 활용하도록 대시보드가 최대화됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-125">Lastly, if you double-click the blade header, the dashboard maximizes to utilize the available screen real-estate.</span></span> <span data-ttu-id="948eb-126">여러 열을 표시하는 경우 크게 볼수록 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-126">This larger view is helpful when multiple columns are displayed.</span></span>

## <a name="replication-status-dashboard"></a><span data-ttu-id="948eb-127">복제 상태 대시보드</span><span class="sxs-lookup"><span data-stu-id="948eb-127">Replication Status Dashboard</span></span>
<span data-ttu-id="948eb-128">이 대시보드에서는 모니터링되는 도메인 컨트롤러의 복제 상태 및 복제 토폴로지 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-128">This dashboard provides a view of the replication status and replication topology of your monitored domain controllers.</span></span> <span data-ttu-id="948eb-129">발견된 모든 오류에 대한 유용한 설명서와 함께 가장 최근 복제를 시도한 상태가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-129">The status of the most recent replication attempt is listed, along with helpful documentation for any error that is found.</span></span> <span data-ttu-id="948eb-130">오류가 있는 도메인 컨트롤러를 두 번 클릭하면 오류에 대한 자세한 정보, 권장되는 해결 단계, 문제 해결 설명서에 대한 링크와 같은 정보를 포함하는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-130">You can double-click a domain controller with an error, to open a new blade with information such as: details about the error, recommended resolution steps, and links to troubleshooting documentation.</span></span>

![복제 상태](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a><span data-ttu-id="948eb-132">모니터링</span><span class="sxs-lookup"><span data-stu-id="948eb-132">Monitoring</span></span>
<span data-ttu-id="948eb-133">이 기능은 다양한 성능 카운터의 추세를 그래프로 제공하며 이 정보는 계속해서 모니터링되는 각각의 도메인 컨트롤러에서 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-133">This feature provides graphical trends of different performance counters, which are continuously collected from each of the monitored domain controllers.</span></span> <span data-ttu-id="948eb-134">도메인 컨트롤러의 성능은 포리스트에 있는 다른 모든 모니터된 도메인 컨트롤러 간에 쉽게 비교될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-134">Performance of a domain controller can easily be compared across all other monitored domain controllers in your forest.</span></span> <span data-ttu-id="948eb-135">또한 다양한 성능 카운터를 나란히 볼 수 있으며 환경에서 문제를 해결할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-135">Additionally, you can see various performance counters side by side, which is helpful when troubleshooting issues in your environment.</span></span>

![모니터링](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

<span data-ttu-id="948eb-137">기본적으로 미리 선택한 네 개의 성능 카운터가 있습니다. 그러나 필터 명령을 클릭하고 원하는 성능 카운터를 선택하거나 선택을 취소하여 다른 성능 카운터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-137">By default, we have preselected four performance counters; however, you can include others by clicking the filter command and selecting or deselecting any desired performance counters.</span></span> <span data-ttu-id="948eb-138">또한, 성능 카운터 그래프를 두 번 클릭하면 새 블레이드가 열리며, 여기에는 모니터링되는 각각의 도메인 컨트롤러에 대한 데이터 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="948eb-138">Additionally, you can double-click a performance counter graph to open a new blade, which includes data points for each of the monitored domain controllers.</span></span>

## <a name="related-links"></a><span data-ttu-id="948eb-139">관련 링크</span><span class="sxs-lookup"><span data-stu-id="948eb-139">Related links</span></span>
* [<span data-ttu-id="948eb-140">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="948eb-140">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="948eb-141">Azure AD Connect Health Agent 설치</span><span class="sxs-lookup"><span data-stu-id="948eb-141">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="948eb-142">Azure AD Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="948eb-142">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="948eb-143">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="948eb-143">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="948eb-144">동기화에 대한 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="948eb-144">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="948eb-145">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="948eb-145">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="948eb-146">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="948eb-146">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)

