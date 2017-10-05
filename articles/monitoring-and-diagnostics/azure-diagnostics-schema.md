---
title: "Azure 진단 확장 구성 스키마 버전 및 기록 | Microsoft Docs"
description: "Azure Virtual Machines, VM Scale Sets, Service Fabric 및 Cloud Services에서 성능 카운터 수집과 관련됩니다."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 119e8a237f24cdc80a1ab8e376f2b308c9eada05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="3f86d-103">Azure 진단 확장 구성 스키마 버전 및 기록</span><span class="sxs-lookup"><span data-stu-id="3f86d-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="3f86d-104">이 페이지는 Microsoft Azure SDK의 일부로 제공되는 Azure 진단 확장 스키마 버전을 인덱스합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-104">This page indexes Azure Diagnostics extension schema versions shipped as part of the Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="3f86d-105">Azure 진단 확장은 성능 카운터 및 기타 통계를 수집하는 데 사용하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-105">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="3f86d-106">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f86d-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="3f86d-107">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="3f86d-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="3f86d-108">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="3f86d-108">Service Fabric</span></span> 
> - <span data-ttu-id="3f86d-109">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="3f86d-109">Cloud Services</span></span> 
> - <span data-ttu-id="3f86d-110">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3f86d-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="3f86d-111">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="3f86d-112">Azure 진단 확장은 Azure Monitor, Application Insights 및 Log Analytics와 같은 다른 Microsoft 진단 제품과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-112">The Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="3f86d-113">자세한 내용은 [Microsoft 모니터링 도구 개요](monitoring-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f86d-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="3f86d-114">Azure SDK 및 진단 버전 전달 차트</span><span class="sxs-lookup"><span data-stu-id="3f86d-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="3f86d-115">Azure SDK 버전</span><span class="sxs-lookup"><span data-stu-id="3f86d-115">Azure SDK version</span></span> | <span data-ttu-id="3f86d-116">진단 확장 버전</span><span class="sxs-lookup"><span data-stu-id="3f86d-116">Diagnostics extension version</span></span> | <span data-ttu-id="3f86d-117">모델</span><span class="sxs-lookup"><span data-stu-id="3f86d-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="3f86d-118">1.x</span><span class="sxs-lookup"><span data-stu-id="3f86d-118">1.x</span></span>               |<span data-ttu-id="3f86d-119">1.0</span><span class="sxs-lookup"><span data-stu-id="3f86d-119">1.0</span></span>                            |<span data-ttu-id="3f86d-120">플러그 인</span><span class="sxs-lookup"><span data-stu-id="3f86d-120">plug-in</span></span>|  
|<span data-ttu-id="3f86d-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="3f86d-121">2.0 - 2.4</span></span>         |<span data-ttu-id="3f86d-122">1.0</span><span class="sxs-lookup"><span data-stu-id="3f86d-122">1.0</span></span>                            |<span data-ttu-id="3f86d-123">플러그 인</span><span class="sxs-lookup"><span data-stu-id="3f86d-123">plug-in</span></span>|  
|<span data-ttu-id="3f86d-124">2.5</span><span class="sxs-lookup"><span data-stu-id="3f86d-124">2.5</span></span>               |<span data-ttu-id="3f86d-125">1.2</span><span class="sxs-lookup"><span data-stu-id="3f86d-125">1.2</span></span>                            |<span data-ttu-id="3f86d-126">확장</span><span class="sxs-lookup"><span data-stu-id="3f86d-126">extension</span></span>|  
|<span data-ttu-id="3f86d-127">2.6</span><span class="sxs-lookup"><span data-stu-id="3f86d-127">2.6</span></span>               |<span data-ttu-id="3f86d-128">1.3</span><span class="sxs-lookup"><span data-stu-id="3f86d-128">1.3</span></span>                            |<span data-ttu-id="3f86d-129">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-129">"</span></span>|  
|<span data-ttu-id="3f86d-130">2.7</span><span class="sxs-lookup"><span data-stu-id="3f86d-130">2.7</span></span>               |<span data-ttu-id="3f86d-131">1.4</span><span class="sxs-lookup"><span data-stu-id="3f86d-131">1.4</span></span>                            |<span data-ttu-id="3f86d-132">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-132">"</span></span>|  
|<span data-ttu-id="3f86d-133">2.8</span><span class="sxs-lookup"><span data-stu-id="3f86d-133">2.8</span></span>               |<span data-ttu-id="3f86d-134">1.5</span><span class="sxs-lookup"><span data-stu-id="3f86d-134">1.5</span></span>                            |<span data-ttu-id="3f86d-135">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-135">"</span></span>|  
|<span data-ttu-id="3f86d-136">2.9</span><span class="sxs-lookup"><span data-stu-id="3f86d-136">2.9</span></span>               |<span data-ttu-id="3f86d-137">1.6</span><span class="sxs-lookup"><span data-stu-id="3f86d-137">1.6</span></span>                            |<span data-ttu-id="3f86d-138">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-138">"</span></span>|
|<span data-ttu-id="3f86d-139">2.96</span><span class="sxs-lookup"><span data-stu-id="3f86d-139">2.96</span></span>              |<span data-ttu-id="3f86d-140">1.7</span><span class="sxs-lookup"><span data-stu-id="3f86d-140">1.7</span></span>                            |<span data-ttu-id="3f86d-141">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-141">"</span></span>|
|<span data-ttu-id="3f86d-142">2.96</span><span class="sxs-lookup"><span data-stu-id="3f86d-142">2.96</span></span>              |<span data-ttu-id="3f86d-143">1.8</span><span class="sxs-lookup"><span data-stu-id="3f86d-143">1.8</span></span>                            |<span data-ttu-id="3f86d-144">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-144">"</span></span>|
|<span data-ttu-id="3f86d-145">2.96</span><span class="sxs-lookup"><span data-stu-id="3f86d-145">2.96</span></span>              |<span data-ttu-id="3f86d-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="3f86d-146">1.8.1</span></span>                          |<span data-ttu-id="3f86d-147">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-147">"</span></span>|
|<span data-ttu-id="3f86d-148">2.96</span><span class="sxs-lookup"><span data-stu-id="3f86d-148">2.96</span></span>              |<span data-ttu-id="3f86d-149">1.9</span><span class="sxs-lookup"><span data-stu-id="3f86d-149">1.9</span></span>                            |<span data-ttu-id="3f86d-150">"</span><span class="sxs-lookup"><span data-stu-id="3f86d-150">"</span></span>|



 <span data-ttu-id="3f86d-151">Azure 진단 버전 1.0은 처음에는 플러그 인 모델로 제공되었습니다. 따라서 Azure SDK를 설치할 때 함께 제공되는 Azure 진단 버전을 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="3f86d-152">SDK 2.5(진단 버전 1.2)부터는 Azure 진단이 확장 모델로 이동되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span></span> <span data-ttu-id="3f86d-153">새 기능을 활용하기 위한 도구는 최신 Azure SDK에서만 사용할 수 있었지만 Azure 진단을 사용하는 모든 서비스는 Azure에서 직접 최신 전달 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-153">The tools to utilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up the latest shipping version directly from Azure.</span></span> <span data-ttu-id="3f86d-154">예를 들어, 여전히 SDK 2.5를 사용하는 모든 사용자는 최신 기능을 사용 중인지 여부와 관계 없이 이전 테이블에 표시된 최신 버전이 로딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-154">For example, anyone still using SDK 2.5 would be loading the latest version shown in the previous table, regardless if they are using the newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="3f86d-155">스키마 색인</span><span class="sxs-lookup"><span data-stu-id="3f86d-155">Schemas index</span></span>  
<span data-ttu-id="3f86d-156">서로 다른 버전의 Azure 진단은 다른 구성 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="3f86d-157">진단 1.0 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="3f86d-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="3f86d-158">진단 1.2 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="3f86d-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="3f86d-159">진단 1.3 이상 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="3f86d-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="3f86d-160">버전 기록</span><span class="sxs-lookup"><span data-stu-id="3f86d-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="3f86d-161">진단 확장 1.9</span><span class="sxs-lookup"><span data-stu-id="3f86d-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="3f86d-162">Docker 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="3f86d-163">진단 확장 1.8.1</span><span class="sxs-lookup"><span data-stu-id="3f86d-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="3f86d-164">개인 구성에서 저장소 계정 키 대신 SAS 토큰을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-164">Can specify a SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="3f86d-165">SAS 토큰이 제공된 경우 저장소 계정 키가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-165">If a SAS token is provided, the storage account key is ignored.</span></span>


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a><span data-ttu-id="3f86d-166">진단 확장 1.8</span><span class="sxs-lookup"><span data-stu-id="3f86d-166">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="3f86d-167">PublicConfig에 저장소 형식이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-167">Added Storage Type to PublicConfig.</span></span> <span data-ttu-id="3f86d-168">StorageType은 *Table*, *Blob*, *TableAndBlob*이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-168">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="3f86d-169">*Table*이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-169">*Table* is the default.</span></span>


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a><span data-ttu-id="3f86d-170">진단 확장 1.7</span><span class="sxs-lookup"><span data-stu-id="3f86d-170">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="3f86d-171">EventHub로 라우팅하는 기능이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-171">Added the ability to route to EventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="3f86d-172">진단 확장 1.5</span><span class="sxs-lookup"><span data-stu-id="3f86d-172">Diagnostics extension 1.5</span></span>
<span data-ttu-id="3f86d-173">[Application Insights](../application-insights/app-insights-cloudservices.md)에 진단 데이터를 전송하는 싱크 요소 및 기능이 추가되어 시스템 및 인프라 수준뿐만 아니라 응용 프로그램 전반에 나타나는 문제를 쉽게 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-173">Added the sinks element and the ability to send diagnostics data to [Application Insights](../application-insights/app-insights-cloudservices.md) making it easier to diagnose issues across your application as well as the system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="3f86d-174">Azure SDK 2.6 및 진단 확장 1.3</span><span class="sxs-lookup"><span data-stu-id="3f86d-174">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="3f86d-175">Visual Studio에서 클라우드 서비스 프로젝트의 경우 다음 사항이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-175">For Cloud Service projects in Visual Studio, the following changes were made.</span></span> <span data-ttu-id="3f86d-176">(이러한 변경 사항은 이후 버전의 Azure SDK에도 적용됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3f86d-176">(These changes also apply to later versions of Azure SDK.)</span></span>

* <span data-ttu-id="3f86d-177">이제 로컬 에뮬레이터에서 진단을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-177">The local emulator now supports diagnostics.</span></span> <span data-ttu-id="3f86d-178">따라서 Visual Studio에서 개발 및 테스트하는 동안 진단 데이터를 수집하고 응용 프로그램에서 올바른 추적을 생성하고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-178">This means you can collect diagnostics data and ensure your application is creating the right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="3f86d-179">연결 문자열 `UseDevelopmentStorage=true` 는 Azure 저장소 에뮬레이터를 사용하여 Visual Studio에서 클라우드 서비스 프로젝트를 실행하는 동안 진단 데이터 수집을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-179">The connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using the Azure storage emulator.</span></span> <span data-ttu-id="3f86d-180">모든 진단 데이터는 (개발 저장소) 저장소 계정에 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-180">All diagnostics data is collected in the (Development Storage) storage account.</span></span>
* <span data-ttu-id="3f86d-181">진단 저장소 계정 연결 문자열(Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString)은 서비스 구성(.cscfg) 파일에 다시 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-181">The diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in the service configuration (.cscfg) file.</span></span> <span data-ttu-id="3f86d-182">Azure SDK 2.5에서는 진단 저장소 계정이 diagnostics.wadcfgx 파일에 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-182">In Azure SDK 2.5 the diagnostics storage account was specified in the diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="3f86d-183">Azure SDK 2.4 이하와 Azure SDK 2.6 이상 버전에서 연결 문자열이 작동하는 방식 간에 몇 가지 주목할 만한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-183">There are some notable differences between how the connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="3f86d-184">Azure SDK 2.4 이하 버전에서는 진단 로그를 전송하기 위한 저장소 계정 정보를 가져오기 위해 진단 플러그인에 의해 런타임으로 연결 문자열이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-184">In Azure SDK 2.4 and earlier, the connection string was used as a runtime by the diagnostics plugin to get the storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="3f86d-185">Azure SDK 2.6 이상 버전에서는 게시하는 동안 적절한 저장소 계정 정보로 진단 확장을 구성하기 위해 Visual Studio에 의해 연결 문자열이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-185">In Azure SDK 2.6 and later, the diagnostics connection string is used by Visual Studio to configure the diagnostics extension with the appropriate storage account information during publishing.</span></span> <span data-ttu-id="3f86d-186">연결 문자열을 통해 사용자는 Visual Studio에서 게시하는 동안 사용할 다양한 서비스 구성에 대해 서로 다른 저장소 계정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-186">The connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="3f86d-187">그러나 진단 플러그인을 더 이상 사용할 수 없으므로(Azure SDK 2.5 이후) .cscfg 파일 자체만으로 진단 확장을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-187">However, because the diagnostics plugin is no longer available (after Azure SDK 2.5), the .cscfg file by itself can't enable the Diagnostics Extension.</span></span> <span data-ttu-id="3f86d-188">Visual Studio 또는 PowerShell과 같은 도구를 통해 별도로 확장을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-188">You have to enable the extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="3f86d-189">PowerShell을 사용한 진단 확장 구성 프로세스를 단순화하기 위해 Visual Studio의 패키지 출력에도 각 역할에 대한 진단 확장의 공용 구성 XML이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-189">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML for the diagnostics extension for each role.</span></span> <span data-ttu-id="3f86d-190">Visual Studio에서는 진단 연결 문자열을 사용하여 공용 구성에 있는 저장소 계정 정보를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-190">Visual Studio uses the diagnostics connection string to populate the storage account information present in the public configuration.</span></span> <span data-ttu-id="3f86d-191">공용 config 파일이 Extensions 폴더에서 생성되고 PaaSDiagnostics<RoleName>.PubConfig.xml 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-191">The public config files are created in the Extensions folder and follow the pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="3f86d-192">모든 PowerShell 기반 배포에서 이 패턴을 사용하여 각 구성을 역할에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-192">Any PowerShell based deployments can use this pattern to map each configuration to a Role.</span></span>
* <span data-ttu-id="3f86d-193">.cscfg 파일의 연결 문자열은 Azure 포털에서 진단 데이터에 액세스하는 데도 사용되므로 **모니터링** 탭에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-193">The connection string in the .cscfg file is also used by the Azure portal to access the diagnostics data so it can appear in the **Monitoring** tab.</span></span> <span data-ttu-id="3f86d-194">이 연결 문자열은 포털에서 자세한 모니터링 데이터를 표시하도록 서비스를 구성하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-194">The connection string is needed to configure the service to show verbose monitoring data in the portal.</span></span>

#### <a name="migrating-projects-to-azure-sdk-26-and-later"></a><span data-ttu-id="3f86d-195">Azure SDK 2.6 이상으로 프로젝트 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3f86d-195">Migrating projects to Azure SDK 2.6 and later</span></span>
<span data-ttu-id="3f86d-196">Azure SDK 2.5에서 Azure SDK 2.6 이상으로 마이그레이션하는 경우 .wadcfgx 파일에 진단 저장소 계정이 지정된 경우 값이 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-196">When migrating from Azure SDK 2.5 to Azure SDK 2.6 or later, if you had a diagnostics storage account specified in the .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="3f86d-197">서로 다른 저장소 구성에 대해 서로 다른 저장소 계정을 유연성 있게 사용하려면 프로젝트에 연결 문자열을 수동으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-197">To take advantage of the flexibility of using different storage accounts for different storage configurations, you'll have to manually add the connection string to your project.</span></span> <span data-ttu-id="3f86d-198">Azure SDK 2.4 또는 이전 버전에서 Azure SDK 2.6으로 프로젝트를 마이그레이션하는 경우 진단 연결 문자열이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-198">If you're migrating a project from Azure SDK 2.4 or earlier to Azure SDK 2.6, then the diagnostics connection strings are preserved.</span></span> <span data-ttu-id="3f86d-199">그러나 이전 섹션에서 지정된 것처럼 Azure SDK 2.6에서 연결 문자열을 처리하는 방식이 변경되었음을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3f86d-199">However, please note the changes in how connection strings are treated in Azure SDK 2.6 as specified in the previous section.</span></span>

#### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a><span data-ttu-id="3f86d-200">Visual Studio에서 진단 저장소 계정을 결정하는 방법</span><span class="sxs-lookup"><span data-stu-id="3f86d-200">How Visual Studio determines the diagnostics storage account</span></span>
* <span data-ttu-id="3f86d-201">진단 연결 문자열이.cscfg 파일에 지정된 경우 Visual Studio에서는 게시할 때와 패키징 중 공용 구성 xml 파일을 생성할 때 이 문자열을 사용하여 진단 확장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-201">If a diagnostics connection string is specified in the .cscfg file, Visual Studio uses it to configure the diagnostics extension when publishing, and when generating the public configuration xml files during packaging.</span></span>
* <span data-ttu-id="3f86d-202">진단 연결 문자열이.cscfg 파일에 지정되지 않은 경우 Visual Studio에서는 게시할 때와 패키징 중 공용 구성 xml 파일을 생성할 때 .wadcfgx 파일에 지정된 저장소 계정을 대신 사용하여 진단 확장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-202">If no diagnostics connection string is specified in the .cscfg file, then Visual Studio falls back to using the storage account specified in the .wadcfgx file to configure the diagnostics extension when publishing, and generating the public configuration xml files when packaging.</span></span>
* <span data-ttu-id="3f86d-203">.cscfg 파일의 진단 연결 문자열은 .wadcfgx 파일의 저장소 계정보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-203">The diagnostics connection string in the .cscfg file takes precedence over the storage account in the .wadcfgx file.</span></span> <span data-ttu-id="3f86d-204">진단 연결 문자열이.cscfg 파일에 지정된 경우, Visual Studio에서는 이 문자열을 사용하고 .wadcfgx의 저장소 계정은 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-204">If a diagnostics connection string is specified in the .cscfg file, then Visual Studio uses that and ignores the storage account in .wadcfgx.</span></span>

#### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="3f86d-205">"개발 저장소 연결 문자열 업데이트..."</span><span class="sxs-lookup"><span data-stu-id="3f86d-205">What does the "Update development storage connection strings…"</span></span> <span data-ttu-id="3f86d-206">확인란의 기능은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3f86d-206">checkbox do?</span></span>
<span data-ttu-id="3f86d-207">**Microsoft Azure에 게시할 때 Microsoft Azure 저장소 계정 자격 증명을 사용하여 진단 및 캐싱을 위한 개발 저장소 연결 문자열 업데이트** 확인란은 게시하는 동안 지정된 Azure 저장소 계정으로 개발 저장소 계정 연결 문자열을 업데이트하는 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-207">The checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing to Microsoft Azure** gives you a convenient way to update any development storage account connection strings with the Azure storage account specified during publishing.</span></span>

<span data-ttu-id="3f86d-208">예를 들어, 사용자가 이 확인란을 선택하고 진단 연결 문자열에서 `UseDevelopmentStorage=true`를 지정한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-208">For example, suppose you select this checkbox and the diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="3f86d-209">Azure에 프로젝트를 게시할 때 Visual Studio는 사용자가 게시 마법사에 지정한 저장소 계정을 사용하여 진단 연결 문자열을 자동으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-209">When you publish the project to Azure, Visual Studio will automatically update the diagnostics connection string with the storage account you specified in the Publish wizard.</span></span> <span data-ttu-id="3f86d-210">그러나 실제 저장소 계정을 진단 연결 문자열로 지정한 경우 해당 계정이 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-210">However, if a real storage account was specified as the diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="3f86d-211">Azure SDK 2.4 이하 및 Azure SDK 2.5 이상 간의 진단 기능 차이점</span><span class="sxs-lookup"><span data-stu-id="3f86d-211">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="3f86d-212">Azure SDK 2.4에서 Azure SDK 2.5 이상으로 업그레이드하는 경우 다음 진단 기능 차이점을 명심해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-212">If you're upgrading your project from Azure SDK 2.4 to Azure SDK 2.5 or later, you should bear in mind the following diagnostics functionality differences.</span></span>

* <span data-ttu-id="3f86d-213">**구성 API가 더 이상 사용되지 않음** – 진단의 프로그래밍 방식 구성은 Azure SDK 2.4 이하 버전에서는 사용할 수 있지만 Azure SDK 2.5 이상 버전에서는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-213">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="3f86d-214">코드에 진단 구성이 현재 정의된 경우 계속해서 진단하려면 마이그레이션된 프로젝트에서 해당 설정을 처음부터 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-214">If your diagnostics configuration is currently defined in code, you'll need to reconfigure those settings from scratch in the migrated project in order for diagnostics to keep working.</span></span> <span data-ttu-id="3f86d-215">Azure SDK 2.4에 대한 진단 구성 파일은 diagnostics.wadcfg이고 Azure SDK 2.5 이상에서는 diagnostics.wadcfgx입니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-215">The diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="3f86d-216">**클라우드 서비스 응용 프로그램에 대한 진단은 인스턴스 수준이 아닌 역할 수준에서만 구성할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="3f86d-216">**Diagnostics for cloud service applications can only be configured at the role level, not at the instance level.**</span></span>
* <span data-ttu-id="3f86d-217">**앱을 배포할 때마다 진단 구성이 업데이트됨** – 이로 인해 서버 탐색기에서 진단 구성을 변경한 후 앱을 다시 배포하는 경우 패리티 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-217">**Every time you deploy your app, the diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="3f86d-218">**Azure SDK 2.5 이상에서 코드가 아닌 진단 구성 파일에 크래시 덤프가 구성됨** – 코드에 크래시 덤프가 구성된 경우, Azure SDK 2.6으로 마이그레이션하는 동안 크래시 덤프가 전송되지 않으므로 해당 구성을 코드에서 구성 파일로 수동으로 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f86d-218">**In Azure SDK 2.5 and later, crash dumps are configured in the diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have to manually transfer the configuration from code to the configuration file, because the crash dumps aren't transferred during the migration to Azure SDK 2.6.</span></span>

