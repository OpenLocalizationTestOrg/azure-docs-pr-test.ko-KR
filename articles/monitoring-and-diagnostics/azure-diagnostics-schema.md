---
title: "aaaAzure 진단 확장 구성 스키마 버전 및 기록 | Microsoft Docs"
description: "Azure 가상 컴퓨터, VM 크기 집합이, 서비스 패브릭 및 클라우드 서비스에서 perf 카운터를 관련 toocollecting입니다."
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
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="f13c1-103">Azure 진단 확장 구성 스키마 버전 및 기록</span><span class="sxs-lookup"><span data-stu-id="f13c1-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="f13c1-104">이 페이지 인덱스 Azure 진단 확장 스키마 버전 hello Microsoft Azure SDK의 일부로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-104">This page indexes Azure Diagnostics extension schema versions shipped as part of hello Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="f13c1-105">hello Azure 진단 확장은 toocollect 성능 카운터 및 기타 통계에서 사용 하는 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-105">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="f13c1-106">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="f13c1-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="f13c1-107">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="f13c1-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="f13c1-108">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="f13c1-108">Service Fabric</span></span> 
> - <span data-ttu-id="f13c1-109">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="f13c1-109">Cloud Services</span></span> 
> - <span data-ttu-id="f13c1-110">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="f13c1-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="f13c1-111">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="f13c1-112">Azure 진단 확장 hello Azure 모니터, Application Insights 및 분석 로그와 같은 다른 Microsoft 진단 제품과 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-112">hello Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="f13c1-113">자세한 내용은 [Microsoft 모니터링 도구 개요](monitoring-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13c1-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="f13c1-114">Azure SDK 및 진단 버전 전달 차트</span><span class="sxs-lookup"><span data-stu-id="f13c1-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="f13c1-115">Azure SDK 버전</span><span class="sxs-lookup"><span data-stu-id="f13c1-115">Azure SDK version</span></span> | <span data-ttu-id="f13c1-116">진단 확장 버전</span><span class="sxs-lookup"><span data-stu-id="f13c1-116">Diagnostics extension version</span></span> | <span data-ttu-id="f13c1-117">모델</span><span class="sxs-lookup"><span data-stu-id="f13c1-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="f13c1-118">1.x</span><span class="sxs-lookup"><span data-stu-id="f13c1-118">1.x</span></span>               |<span data-ttu-id="f13c1-119">1.0</span><span class="sxs-lookup"><span data-stu-id="f13c1-119">1.0</span></span>                            |<span data-ttu-id="f13c1-120">플러그 인</span><span class="sxs-lookup"><span data-stu-id="f13c1-120">plug-in</span></span>|  
|<span data-ttu-id="f13c1-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="f13c1-121">2.0 - 2.4</span></span>         |<span data-ttu-id="f13c1-122">1.0</span><span class="sxs-lookup"><span data-stu-id="f13c1-122">1.0</span></span>                            |<span data-ttu-id="f13c1-123">플러그 인</span><span class="sxs-lookup"><span data-stu-id="f13c1-123">plug-in</span></span>|  
|<span data-ttu-id="f13c1-124">2.5</span><span class="sxs-lookup"><span data-stu-id="f13c1-124">2.5</span></span>               |<span data-ttu-id="f13c1-125">1.2</span><span class="sxs-lookup"><span data-stu-id="f13c1-125">1.2</span></span>                            |<span data-ttu-id="f13c1-126">확장</span><span class="sxs-lookup"><span data-stu-id="f13c1-126">extension</span></span>|  
|<span data-ttu-id="f13c1-127">2.6</span><span class="sxs-lookup"><span data-stu-id="f13c1-127">2.6</span></span>               |<span data-ttu-id="f13c1-128">1.3</span><span class="sxs-lookup"><span data-stu-id="f13c1-128">1.3</span></span>                            |<span data-ttu-id="f13c1-129">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-129">"</span></span>|  
|<span data-ttu-id="f13c1-130">2.7</span><span class="sxs-lookup"><span data-stu-id="f13c1-130">2.7</span></span>               |<span data-ttu-id="f13c1-131">1.4</span><span class="sxs-lookup"><span data-stu-id="f13c1-131">1.4</span></span>                            |<span data-ttu-id="f13c1-132">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-132">"</span></span>|  
|<span data-ttu-id="f13c1-133">2.8</span><span class="sxs-lookup"><span data-stu-id="f13c1-133">2.8</span></span>               |<span data-ttu-id="f13c1-134">1.5</span><span class="sxs-lookup"><span data-stu-id="f13c1-134">1.5</span></span>                            |<span data-ttu-id="f13c1-135">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-135">"</span></span>|  
|<span data-ttu-id="f13c1-136">2.9</span><span class="sxs-lookup"><span data-stu-id="f13c1-136">2.9</span></span>               |<span data-ttu-id="f13c1-137">1.6</span><span class="sxs-lookup"><span data-stu-id="f13c1-137">1.6</span></span>                            |<span data-ttu-id="f13c1-138">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-138">"</span></span>|
|<span data-ttu-id="f13c1-139">2.96</span><span class="sxs-lookup"><span data-stu-id="f13c1-139">2.96</span></span>              |<span data-ttu-id="f13c1-140">1.7</span><span class="sxs-lookup"><span data-stu-id="f13c1-140">1.7</span></span>                            |<span data-ttu-id="f13c1-141">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-141">"</span></span>|
|<span data-ttu-id="f13c1-142">2.96</span><span class="sxs-lookup"><span data-stu-id="f13c1-142">2.96</span></span>              |<span data-ttu-id="f13c1-143">1.8</span><span class="sxs-lookup"><span data-stu-id="f13c1-143">1.8</span></span>                            |<span data-ttu-id="f13c1-144">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-144">"</span></span>|
|<span data-ttu-id="f13c1-145">2.96</span><span class="sxs-lookup"><span data-stu-id="f13c1-145">2.96</span></span>              |<span data-ttu-id="f13c1-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="f13c1-146">1.8.1</span></span>                          |<span data-ttu-id="f13c1-147">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-147">"</span></span>|
|<span data-ttu-id="f13c1-148">2.96</span><span class="sxs-lookup"><span data-stu-id="f13c1-148">2.96</span></span>              |<span data-ttu-id="f13c1-149">1.9</span><span class="sxs-lookup"><span data-stu-id="f13c1-149">1.9</span></span>                            |<span data-ttu-id="f13c1-150">"</span><span class="sxs-lookup"><span data-stu-id="f13c1-150">"</span></span>|



 <span data-ttu-id="f13c1-151">Azure 진단 버전 1.0 hello Azure SDK를 설치할 때 함께 제공 되는 Azure 진단의 hello 버전을 가져온을 의미 하는 플러그 인 모델--에 처음 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed hello Azure SDK, you got hello version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="f13c1-152">Azure 진단 (진단 버전 1.2) SDK 2.5 부터는 tooan 확장 모델을 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went tooan extension model.</span></span> <span data-ttu-id="f13c1-153">hello 도구 tooutilize 새로운 기능 최신 Azure Sdk에서 사용할 수만 있었습니다. 하지만 Azure 진단을 사용 하 여 모든 서비스는 Azure에서 직접 hello 최신 배송 버전을 선택 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-153">hello tools tooutilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up hello latest shipping version directly from Azure.</span></span> <span data-ttu-id="f13c1-154">예를 들어 여전히 SDK 2.5를 사용 하 여 모든 사용자는 로드할 수 hello 최신 버전 hello 최신 기능을 사용 중인 경우와 상관 없이 hello 이전 표에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-154">For example, anyone still using SDK 2.5 would be loading hello latest version shown in hello previous table, regardless if they are using hello newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="f13c1-155">스키마 색인</span><span class="sxs-lookup"><span data-stu-id="f13c1-155">Schemas index</span></span>  
<span data-ttu-id="f13c1-156">서로 다른 버전의 Azure 진단은 다른 구성 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="f13c1-157">진단 1.0 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="f13c1-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="f13c1-158">진단 1.2 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="f13c1-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="f13c1-159">진단 1.3 이상 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="f13c1-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="f13c1-160">버전 기록</span><span class="sxs-lookup"><span data-stu-id="f13c1-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="f13c1-161">진단 확장 1.9</span><span class="sxs-lookup"><span data-stu-id="f13c1-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="f13c1-162">Docker 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="f13c1-163">진단 확장 1.8.1</span><span class="sxs-lookup"><span data-stu-id="f13c1-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="f13c1-164">Hello 개인 구성에서 저장소 계정 키 대신 SAS 토큰을 지정할 수 있습니다. SAS 토큰을 지정 하는 경우 hello 저장소 계정 키가 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-164">Can specify a SAS token instead of a storage account key in hello private config. If a SAS token is provided, hello storage account key is ignored.</span></span>


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


### <a name="diagnostics-extension-18"></a><span data-ttu-id="f13c1-165">진단 확장 1.8</span><span class="sxs-lookup"><span data-stu-id="f13c1-165">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="f13c1-166">추가 된 저장 유형 tooPublicConfig 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-166">Added Storage Type tooPublicConfig.</span></span> <span data-ttu-id="f13c1-167">StorageType은 *Table*, *Blob*, *TableAndBlob*이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-167">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="f13c1-168">*테이블* hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-168">*Table* is hello default.</span></span>


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


### <a name="diagnostics-extension-17"></a><span data-ttu-id="f13c1-169">진단 확장 1.7</span><span class="sxs-lookup"><span data-stu-id="f13c1-169">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="f13c1-170">추가 된 hello 기능 tooroute tooEventHub 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-170">Added hello ability tooroute tooEventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="f13c1-171">진단 확장 1.5</span><span class="sxs-lookup"><span data-stu-id="f13c1-171">Diagnostics extension 1.5</span></span>
<span data-ttu-id="f13c1-172">Hello 요소와 hello 기능 toosend 진단 데이터를 너무 싱크 추가[Application Insights](../application-insights/app-insights-cloudservices.md) hello 시스템 및 인프라 수준 뿐만 아니라 응용 프로그램에서 쉽게 toodiagnose 문제 만들기.</span><span class="sxs-lookup"><span data-stu-id="f13c1-172">Added hello sinks element and hello ability toosend diagnostics data too[Application Insights](../application-insights/app-insights-cloudservices.md) making it easier toodiagnose issues across your application as well as hello system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="f13c1-173">Azure SDK 2.6 및 진단 확장 1.3</span><span class="sxs-lookup"><span data-stu-id="f13c1-173">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="f13c1-174">Visual Studio에서 클라우드 서비스 프로젝트에 대 한 변경 내용을 따라 hello 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-174">For Cloud Service projects in Visual Studio, hello following changes were made.</span></span> <span data-ttu-id="f13c1-175">(이러한 변경 내용을 적용할 수도 toolater 버전의 Azure SDK.)</span><span class="sxs-lookup"><span data-stu-id="f13c1-175">(These changes also apply toolater versions of Azure SDK.)</span></span>

* <span data-ttu-id="f13c1-176">hello 로컬 에뮬레이터는 이제 진단을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-176">hello local emulator now supports diagnostics.</span></span> <span data-ttu-id="f13c1-177">즉, 진단 데이터를 수집 하 고 응용 프로그램은 hello 오른쪽 추적 생성 개발 하 고 Visual Studio에서 테스트 하는 동안 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-177">This means you can collect diagnostics data and ensure your application is creating hello right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="f13c1-178">연결 문자열 hello `UseDevelopmentStorage=true` hello Azure 저장소 에뮬레이터를 사용 하 여 Visual Studio에서 클라우드 서비스 프로젝트를 실행 하는 동안 진단 데이터 수집을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-178">hello connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using hello Azure storage emulator.</span></span> <span data-ttu-id="f13c1-179">Hello (개발 저장소) 저장소 계정에서 모든 진단 데이터 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-179">All diagnostics data is collected in hello (Development Storage) storage account.</span></span>
* <span data-ttu-id="f13c1-180">hello 진단 저장소 계정 연결 문자열 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) hello 서비스 구성 (.cscfg) 파일에 다시 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-180">hello diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in hello service configuration (.cscfg) file.</span></span> <span data-ttu-id="f13c1-181">Azure SDK 2.5에서 hello 진단 저장소 계정은 hello diagnostics.wadcfgx 파일에 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-181">In Azure SDK 2.5 hello diagnostics storage account was specified in hello diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="f13c1-182">Azure SDK 2.4 및 이전 버전 hello 연결 문자열의 작동 방법 및 Azure SDK 2.6 이상 작동 방식에 몇 가지 주목할 만한 차이점 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-182">There are some notable differences between how hello connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="f13c1-183">Azure SDK 2.4 및 이전 버전에서는 hello 연결 문자열이 사용 되었습니다 런타임 hello 진단 플러그 인 tooget hello 저장소 계정 정보로 진단 로그를 전송에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-183">In Azure SDK 2.4 and earlier, hello connection string was used as a runtime by hello diagnostics plugin tooget hello storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="f13c1-184">Azure SDK 2.6 이상 버전에서 게시 하는 동안 hello 적절 한 저장소 계정 정보로 Visual Studio tooconfigure hello 진단 확장에서 hello 진단 연결 문자열이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-184">In Azure SDK 2.6 and later, hello diagnostics connection string is used by Visual Studio tooconfigure hello diagnostics extension with hello appropriate storage account information during publishing.</span></span> <span data-ttu-id="f13c1-185">hello 연결 문자열에는 Visual Studio에서 게시할 때 사용할 다른 서비스 구성에 대 한 다른 저장소 계정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-185">hello connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="f13c1-186">그러나 hello 진단 플러그 인 (Azure SDK 2.5) 한 후 사용할 수 없게 되었기 때문에 hello.cscfg 파일이 자체적으로 hello 진단 확장을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-186">However, because hello diagnostics plugin is no longer available (after Azure SDK 2.5), hello .cscfg file by itself can't enable hello Diagnostics Extension.</span></span> <span data-ttu-id="f13c1-187">Visual Studio 또는 PowerShell과 같은 도구를 통해 개별적으로 tooenable hello 확장 프로그램이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-187">You have tooenable hello extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="f13c1-188">PowerShell을 사용 하 여 hello 진단 확장 구성의 toosimplify hello 프로세스를 Visual Studio의 패키지 출력 hello hello 공용 구성 XML에 대 한 각 역할에 대 한 hello 진단 확장도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-188">toosimplify hello process of configuring hello diagnostics extension with PowerShell, hello package output from Visual Studio also contains hello public configuration XML for hello diagnostics extension for each role.</span></span> <span data-ttu-id="f13c1-189">Visual Studio hello 진단 연결 문자열 toopopulate hello 저장소 계정 정보 hello 공용 구성에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-189">Visual Studio uses hello diagnostics connection string toopopulate hello storage account information present in hello public configuration.</span></span> <span data-ttu-id="f13c1-190">hello 공용 구성 파일은 hello 확장 폴더에 만들어지며 PaaSDiagnostics hello 패턴을 따릅니다. <RoleName>. PubConfig.xml 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-190">hello public config files are created in hello Extensions folder and follow hello pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="f13c1-191">모든 PowerShell 기반 배포는 각 구성 tooa 역할 패턴 toomap이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-191">Any PowerShell based deployments can use this pattern toomap each configuration tooa Role.</span></span>
* <span data-ttu-id="f13c1-192">hello hello.cscfg 파일에서 연결 문자열 에서도 사용 hello Azure 포털 tooaccess hello 진단 데이터 hello에 나타날 수 있도록 **모니터링** 탭 hello 연결 문자열은 필요한 tooconfigure hello 서비스 tooshow 자세한 정보 hello 포털에서 데이터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-192">hello connection string in hello .cscfg file is also used by hello Azure portal tooaccess hello diagnostics data so it can appear in hello **Monitoring** tab. hello connection string is needed tooconfigure hello service tooshow verbose monitoring data in hello portal.</span></span>

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a><span data-ttu-id="f13c1-193">마이그레이션 프로젝트 tooAzure SDK 2.6 이상</span><span class="sxs-lookup"><span data-stu-id="f13c1-193">Migrating projects tooAzure SDK 2.6 and later</span></span>
<span data-ttu-id="f13c1-194">Azure SDK 2.5 tooAzure SDK 2.6에서에서 마이그레이션 또는 그 이후 버전 hello.wadcfgx 파일에 지정 된 진단 저장소 계정을 사용 했던 경우 다음이 계속 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-194">When migrating from Azure SDK 2.5 tooAzure SDK 2.6 or later, if you had a diagnostics storage account specified in hello .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="f13c1-195">다른 저장소 구성에 대 한 다른 저장소를 사용 하 여 hello 유연성 tootake 활용 계정, toomanually hello 연결 문자열 tooyour 프로젝트에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-195">tootake advantage of hello flexibility of using different storage accounts for different storage configurations, you'll have toomanually add hello connection string tooyour project.</span></span> <span data-ttu-id="f13c1-196">Azure SDK 2.4 또는 이전 tooAzure SDK 2.6에서 프로젝트를 마이그레이션하는, 진단 연결 문자열이 유지 됩니다를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-196">If you're migrating a project from Azure SDK 2.4 or earlier tooAzure SDK 2.6, then hello diagnostics connection strings are preserved.</span></span> <span data-ttu-id="f13c1-197">그러나 hello 변경 내용 처리 방법에 연결 문자열은 Azure SDK 2.6에서 지정 된 대로 hello 이전 단원의 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f13c1-197">However, please note hello changes in how connection strings are treated in Azure SDK 2.6 as specified in hello previous section.</span></span>

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a><span data-ttu-id="f13c1-198">Visual Studio hello 진단 저장소 계정을 결정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f13c1-198">How Visual Studio determines hello diagnostics storage account</span></span>
* <span data-ttu-id="f13c1-199">Hello.cscfg 파일에 진단 연결 문자열이 지정 된, Visual Studio 사용 tooconfigure hello 진단 확장을 게시 하면 및 패키징 시 hello 공용 구성 xml 파일을 생성할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-199">If a diagnostics connection string is specified in hello .cscfg file, Visual Studio uses it tooconfigure hello diagnostics extension when publishing, and when generating hello public configuration xml files during packaging.</span></span>
* <span data-ttu-id="f13c1-200">진단 연결 문자열이 없는 hello.cscfg 파일에 지정 된, 다음 Visual Studio를 대신 hello.wadcfgx 파일 tooconfigure hello 진단 확장을 게시 하 고 hello 공개를 생성 하는 경우에 지정 된 toousing hello 저장소 계정 구성 xml 파일 패키징할 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-200">If no diagnostics connection string is specified in hello .cscfg file, then Visual Studio falls back toousing hello storage account specified in hello .wadcfgx file tooconfigure hello diagnostics extension when publishing, and generating hello public configuration xml files when packaging.</span></span>
* <span data-ttu-id="f13c1-201">hello.cscfg 파일에 진단 연결 문자열 hello hello.wadcfgx 파일의 저장소 계정 hello 보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-201">hello diagnostics connection string in hello .cscfg file takes precedence over hello storage account in hello .wadcfgx file.</span></span> <span data-ttu-id="f13c1-202">진단 연결 문자열은 hello.cscfg 파일에 지정 된 다음 Visual Studio를 사용 하 고 무시.wadcfgx의 저장소 계정을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-202">If a diagnostics connection string is specified in hello .cscfg file, then Visual Studio uses that and ignores hello storage account in .wadcfgx.</span></span>

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="f13c1-203">"... 개발 저장소 연결 문자열 업데이트" hello 않는 내용</span><span class="sxs-lookup"><span data-stu-id="f13c1-203">What does hello "Update development storage connection strings…"</span></span> <span data-ttu-id="f13c1-204">확인란의 기능은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f13c1-204">checkbox do?</span></span>
<span data-ttu-id="f13c1-205">에 대 한 확인란 hello **tooMicrosoft Azure에 게시할 때 진단 및 캐싱을 위한 개발 저장소 연결 문자열을 Microsoft Azure 저장소 계정 자격 증명으로 업데이트** 하면 편리 tooupdate 어떤 게시 하는 동안 지정 된 hello Azure 저장소 계정으로 개발 저장소 계정 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-205">hello checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing tooMicrosoft Azure** gives you a convenient way tooupdate any development storage account connection strings with hello Azure storage account specified during publishing.</span></span>

<span data-ttu-id="f13c1-206">예를 들어이 확인란을 선택 하 고 hello 진단 연결 문자열 지정 `UseDevelopmentStorage=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-206">For example, suppose you select this checkbox and hello diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="f13c1-207">Hello 프로젝트 tooAzure를 게시 하면 Visual Studio hello 게시 마법사에서 지정한 hello 스토리지 계정으로 hello 진단 연결 문자열을 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-207">When you publish hello project tooAzure, Visual Studio will automatically update hello diagnostics connection string with hello storage account you specified in hello Publish wizard.</span></span> <span data-ttu-id="f13c1-208">그러나 실제 저장소 계정을 hello 진단 연결 문자열로 지정 된 경우 다음 해당 계정은 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-208">However, if a real storage account was specified as hello diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="f13c1-209">Azure SDK 2.4 이하 및 Azure SDK 2.5 이상 간의 진단 기능 차이점</span><span class="sxs-lookup"><span data-stu-id="f13c1-209">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="f13c1-210">Azure SDK 2.4 tooAzure SDK 2.5 이상에서 프로젝트를 업그레이드 하는 경우에 유의 hello 진단 기능의 차이 다음에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-210">If you're upgrading your project from Azure SDK 2.4 tooAzure SDK 2.5 or later, you should bear in mind hello following diagnostics functionality differences.</span></span>

* <span data-ttu-id="f13c1-211">**구성 API가 더 이상 사용되지 않음** – 진단의 프로그래밍 방식 구성은 Azure SDK 2.4 이하 버전에서는 사용할 수 있지만 Azure SDK 2.5 이상 버전에서는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-211">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="f13c1-212">코드에서 진단 구성에 현재 정의 된 hello 마이그레이션된 프로젝트에서 진단 tookeep 작업에 대 한 처음부터 이러한 설정을 tooreconfigure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-212">If your diagnostics configuration is currently defined in code, you'll need tooreconfigure those settings from scratch in hello migrated project in order for diagnostics tookeep working.</span></span> <span data-ttu-id="f13c1-213">Azure SDK 2.4 용 hello 진단 구성 파일 diagnostics.wadcfg이 고 Azure SDK 2.5 이상 diagnostics.wadcfgx 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-213">hello diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="f13c1-214">**클라우드 서비스 응용 프로그램에 대 한 진단 hello 인스턴스 수준이 아닌 hello 역할 수준에서 구성할 수만 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="f13c1-214">**Diagnostics for cloud service applications can only be configured at hello role level, not at hello instance level.**</span></span>
* <span data-ttu-id="f13c1-215">**Hello 진단 구성이 업데이트 될 때마다 응용 프로그램을 배포한** -서버 탐색기에서 진단 구성을 변경한 다음 응용 프로그램을 다시 배포 하는 경우이 패리티 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-215">**Every time you deploy your app, hello diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="f13c1-216">**크래시 덤프 코드에 없는 hello 진단 구성 파일에서 구성 된 Azure SDK 2.5 이상 버전에서는** -코드에 구성 된 크래시 덤프를 설정한 경우 toomanually 전송 hello 구성 코드 toohello 구성 파일에서 hello 크래시 덤프 때문에 hello 마이그레이션 tooAzure SDK 2.6 하는 동안 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f13c1-216">**In Azure SDK 2.5 and later, crash dumps are configured in hello diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have toomanually transfer hello configuration from code toohello configuration file, because hello crash dumps aren't transferred during hello migration tooAzure SDK 2.6.</span></span>

