---
title: "게스트 OS 제품군 1 사용 중지 알림 | Microsoft Docs"
description: "Azure 게스트 OS 제품군 1 사용 중지가 발생한 시기 및 적용되는 지를 확인하는 방법에 대한 정보를 제공합니다."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="d8ca6-103">게스트 OS 제품군 1 사용 중지 확인</span><span class="sxs-lookup"><span data-stu-id="d8ca6-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="d8ca6-104">OS 제품군 1의 사용 중지가 2013 년 6월 1일에 처음 발표되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="d8ca6-105">**2014 년 9월 2일** Windows Server 2008 운영 체제에 기반을 둔 Azure 게스트 운영 체제(게스트 OS) 제품군 1.x가 공식적으로 사용 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="d8ca6-106">게스트 OS 제품군 1이 사용 중지된 것을 알리는 오류 메시지와 함께 새 서비스를 배포하거나 제품군 1을 사용하여 기존 서비스를 업그레이드 하려는 모든 시도가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="d8ca6-107">**2014년 11월 3일** 게스트 OS 제품군 1에 대한 연장 지원이 종료되어 완전히 사용 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="d8ca6-108">제품군 1의 모든 서비스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="d8ca6-109">언제든지 이러한 서비스를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-109">We may stop those services at any time.</span></span> <span data-ttu-id="d8ca6-110">수동으로 직접 업그레이드하지 않으면 서비스가 계속된다는 보장이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="d8ca6-111">추가 질문이 있으면 [Cloud Services 포럼](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc)을 방문하거나 [Azure 지원에 문의하세요](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="d8ca6-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="d8ca6-112">영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="d8ca6-112">Are you affected?</span></span>
<span data-ttu-id="d8ca6-113">다음 중 하나에 적용되는 경우 클라우드 서비스에 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="d8ca6-114">클라우드 서비스에 대한 ServiceConfiguration.cscfg 파일에 명시적으로 지정된 "osFamily ="1"의 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="d8ca6-115">클라우드 서비스에 대한 ServiceConfiguration.cscfg 파일에 명시적으로 지정된 osFamily의 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="d8ca6-116">현재, 이 경우 시스템은 "1"의 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="d8ca6-117">Azure Portal은 게스트 운영 체제 제품군 값을 "Windows Server 2008"로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="d8ca6-118">어떤 클라우드 서비스가 어떤 OS 제품군을 실행 중인지 알기 위해, Azure PowerShell에서 다음 스크립트를 실행할 수 있지만 먼저 [Azure PowerShell을 설정해야](/powershell/azureps-cmdlets-docs) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="d8ca6-119">스크립트에 대한 자세한 내용은 [Azure 게스트 OS 제품군 1 만료: 2014년 6월](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="d8ca6-120">스크립트 출력의 osFamily 열이 비어 있거나 "1"을 포함하는 경우 클라우드 서비스는 OS 제품군 1 사용 중지의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="d8ca6-121">영향을 받는 경우 권장 사항</span><span class="sxs-lookup"><span data-stu-id="d8ca6-121">Recommendations if you are affected</span></span>
<span data-ttu-id="d8ca6-122">지원되는 게스트 OS 제품군 중 하나에 클라우드 서비스 역할을 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="d8ca6-123">**게스트 OS 제품군 4.x** -Windows Server 2012 R2 *(권장)*</span><span class="sxs-lookup"><span data-stu-id="d8ca6-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="d8ca6-124">응용 프로그램이.NET framework 4.0, 4.5 또는 4.5.1과 함께 SDK 2.1 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="d8ca6-125">ServiceConfiguration.cscfg 파일에서 osFamily 특성을 "4"으로 설정하고 클라우드 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="d8ca6-126">**게스트 OS 제품군 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d8ca6-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="d8ca6-127">응용 프로그램이.NET framework 4.0 또는 4.5와 함께 SDK 1.8 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="d8ca6-128">ServiceConfiguration.cscfg 파일에서 osFamily 특성을 "3"으로 설정하고 클라우드 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="d8ca6-129">**게스트 OS 제품군 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d8ca6-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="d8ca6-130">응용 프로그램이.NET framework 3.5 또는 4.0과 함께 SDK 1.3 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="d8ca6-131">ServiceConfiguration.cscfg 파일에서 osFamily 특성을 "2"로 설정하고 클라우드 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="d8ca6-132">게스트 OS 제품군 1에 대한 연장된 지원이 2014년 11월 3일에 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="d8ca6-133">게스트 OS 제품군 1에서 클라우드 서비스는 더 이상 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="d8ca6-134">서비스 중단을 방지하려면 가능한 빨리 제품군 1을 마이그레이션 해제하세요.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d8ca6-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8ca6-135">Next steps</span></span>
<span data-ttu-id="d8ca6-136">최신 [게스트 OS 릴리스](cloud-services-guestos-update-matrix.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="d8ca6-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
