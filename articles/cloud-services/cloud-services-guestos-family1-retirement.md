---
title: "aaaGuest OS 제품군 1 사용 중지 확인 | Microsoft Docs"
description: "Hello Azure 게스트 OS 제품군 1 사용 중지 발생 한 시기와 방법에 대 한 정보를 제공 하는 경우 toodetermine"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="6c22f-103">게스트 OS 제품군 1 사용 중지 확인</span><span class="sxs-lookup"><span data-stu-id="6c22f-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="6c22f-104">hello OS 제품군 1 사용 중지는 2013 년 6 월 1 일에 처음 발표 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="6c22f-105">**2014 년 9 월 2 일** hello Azure 게스트 운영 체제 (게스트 OS) 제품군 1.x hello Windows Server 2008 운영 체제를 기반 하는 공식적으로 사용 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="6c22f-106">모든 시도 toodeploy 새로운 서비스 또는 제품군 1을 사용 하 여 업그레이드 기존 서비스는 게스트 OS 제품군 1이 더 이상 해당 hello를 알리는 오류 메시지와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="6c22f-107">**2014년 11월 3일** 게스트 OS 제품군 1에 대한 연장 지원이 종료되어 완전히 사용 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="6c22f-108">제품군 1의 모든 서비스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="6c22f-109">언제든지 이러한 서비스를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-109">We may stop those services at any time.</span></span> <span data-ttu-id="6c22f-110">서비스는 수동으로 업그레이드 하지 않으면 해당 사용자가 직접 toorun 계속 보장이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="6c22f-111">추가 질문이 있으면 방문 hello [클라우드 서비스 포럼](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) 또는 [Azure 지원에 문의](https://azure.microsoft.com/support/options/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="6c22f-112">영향을 받나요?</span><span class="sxs-lookup"><span data-stu-id="6c22f-112">Are you affected?</span></span>
<span data-ttu-id="6c22f-113">클라우드 서비스는 hello 다음 중 하나에 적용 되는 경우 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="6c22f-114">값이 있는 "osFamily ="1"클라우드 서비스에 대 한 hello ServiceConfiguration.cscfg 파일에 명시적으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="6c22f-115">클라우드 서비스에 대 한 hello ServiceConfiguration.cscfg 파일에 명시적으로 지정 된 osFamily에 대 한 값을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="6c22f-116">현재, hello 시스템은이 경우 "1"의 hello 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="6c22f-117">hello Azure 포털 게스트 운영 체제 제품군 값이 "Windows Server 2008"로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="6c22f-118">클라우드 서비스가 어떤 OS 제품군을 실행 하는 toofind, 해야 하지만 hello 다음 Azure PowerShell에서 스크립트를 실행할 수 있습니다 [Azure PowerShell을 설정](/powershell/azureps-cmdlets-docs) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="6c22f-119">Hello 스크립트에 대 한 자세한 내용은 참조 하십시오. [Azure 게스트 OS 제품군 1 만료: 2014 년 6 월](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="6c22f-120">Hello 스크립트 출력의 osFamily 열 hello 비어 있거나 "1"을 포함 하는 경우 클라우드 서비스가 OS 제품군 1 사용 중지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="6c22f-121">영향을 받는 경우 권장 사항</span><span class="sxs-lookup"><span data-stu-id="6c22f-121">Recommendations if you are affected</span></span>
<span data-ttu-id="6c22f-122">Hello 지원 게스트 OS 제품군의 클라우드 서비스 역할 tooone 프로그램을 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="6c22f-123">**게스트 OS 제품군 4.x** -Windows Server 2012 R2 *(권장)*</span><span class="sxs-lookup"><span data-stu-id="6c22f-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="6c22f-124">응용 프로그램이.NET framework 4.0, 4.5 또는 4.5.1과 함께 SDK 2.1 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="6c22f-125">Hello osFamily 특성이 너무 "4"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="6c22f-126">**게스트 OS 제품군 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6c22f-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="6c22f-127">응용 프로그램이.NET framework 4.0 또는 4.5와 함께 SDK 1.8 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="6c22f-128">Hello osFamily 특성이 너무 "3"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="6c22f-129">**게스트 OS 제품군 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="6c22f-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="6c22f-130">응용 프로그램이.NET framework 3.5 또는 4.0과 함께 SDK 1.3 이상을 사용 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="6c22f-131">Hello osFamily 특성이 너무 "2"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="6c22f-132">게스트 OS 제품군 1에 대한 연장된 지원이 2014년 11월 3일에 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="6c22f-133">게스트 OS 제품군 1에서 클라우드 서비스는 더 이상 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="6c22f-134">제품군 1 제거 가능한 tooavoid 서비스 중단으로 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c22f-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6c22f-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c22f-135">Next steps</span></span>
<span data-ttu-id="6c22f-136">검토 hello 최신 [게스트 OS 릴리스와](cloud-services-guestos-update-matrix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c22f-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
