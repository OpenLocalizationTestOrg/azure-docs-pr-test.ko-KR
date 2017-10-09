---
title: "상태 구성에 대 한 Azure 개요 aaaDesired | Microsoft Docs"
description: "PowerShell 필요한 상태 구성에 대 한 hello Microsoft Azure 확장 처리기를 사용 하 여에 대 한 개요를 제공 합니다. 필수 구성 요소, 아키텍처, cmdlet...을 포함"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="c09f9-104">소개 toohello Azure 필요한 상태 구성 확장 처리기</span><span class="sxs-lookup"><span data-stu-id="c09f9-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c09f9-105">hello Azure VM 에이전트와 연결 된 확장은 hello Microsoft Azure 인프라 서비스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="c09f9-106">VM 확장은 hello VM 기능을 확장 하 고 다양 한 VM 관리 작업을 단순화 하는 소프트웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="c09f9-107">Hello VMAccess 확장 관리자의 암호를 사용 하는 tooreset 수 하거나 사용자 지정 스크립트 hello 수 예를 들어 확장명 사용된 tooexecute hello VM에 대 한 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="c09f9-108">이 문서에서는 hello Azure PowerShell SDK의 일부분으로 Azure Vm에 대 한 hello PowerShell 필요한 상태 구성 (DSC) 확장을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="c09f9-109">새 cmdlet tooupload를 사용할 수 있으며 hello PowerShell DSC 확장을 사용 하도록 설정 하는 Azure VM에는 PowerShell DSC 구성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="c09f9-110">PowerShell DSC tooenact hello 하 여 hello PowerShell DSC 확장 호출 hello VM에서 DSC 구성을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="c09f9-111">이 기능은 hello Azure 포털을 통해 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c09f9-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c09f9-112">Prerequisites</span></span>
<span data-ttu-id="c09f9-113">**로컬 컴퓨터** 와 toointeract hello Azure VM 확장, 필요한 toouse 어느 hello Azure 포털 또는 Azure PowerShell SDK를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="c09f9-114">**게스트 에이전트** hello hello DSC 구성에 의해 구성 된 Azure VM 관리 프레임 워크 WMF (Windows) 4.0 또는 5.0 원하는 OS를 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="c09f9-115">hello에 지원 되는 운영 체제 버전의 전체 목록을 hello 있습니다 [DSC 확장 버전 기록](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="c09f9-116">용어 및 개념</span><span class="sxs-lookup"><span data-stu-id="c09f9-116">Terms and concepts</span></span>
<span data-ttu-id="c09f9-117">이 가이드 hello 다음 개념에 익숙하다고를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="c09f9-118">구성 - DSC 구성 문서.</span><span class="sxs-lookup"><span data-stu-id="c09f9-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="c09f9-119">노드 - DSC 구성에 대한 대상.</span><span class="sxs-lookup"><span data-stu-id="c09f9-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="c09f9-120">이 문서에 "노드" tooan Azure VM을 항상 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="c09f9-121">구성 데이터 - 구성에 대한 환경 데이터를 포함하는 .psd1 파일</span><span class="sxs-lookup"><span data-stu-id="c09f9-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="c09f9-122">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="c09f9-122">Architectural overview</span></span>
<span data-ttu-id="c09f9-123">hello Azure VM 에이전트 프레임 워크 toodeliver을 사용 하 여 hello Azure DSC 확장 하 고 시행 하 고, Azure Vm에서 실행 되는 DSC 구성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="c09f9-124">DSC 확장 hello 최소한 구성 문서를 포함 하는.zip 파일을 요구 하 고 매개 변수 집합이 제공 hello Azure PowerShell SDK 또는 hello를 통해 Azure 포털 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="c09f9-125">처음으로 hello에 대 한 hello 확장을 호출할 때 설치 프로세스를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="c09f9-126">이 프로세스 논리 hello를 사용 하 여 hello Windows Management Framework (WMF)의 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="c09f9-127">Windows Server 2016 hello Azure VM OS 이면 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="c09f9-128">Windows Server 2016 설치 된 powershell hello 최신 버전에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="c09f9-129">경우 hello `wmfVersion` 속성을 지정한 경우 해당 버전의 WMF hello hello VM의 OS와 호환 되지 않으면 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="c09f9-130">하지 않으면 `wmfVersion` 속성이 지정 되 면 hello 최신 해당 버전의 hello WMF 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="c09f9-131">Hello WMF 설치 다시 부팅이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="c09f9-132">다시 부팅 후 hello 확장 hello에 지정 된 hello.zip 파일을 다운로드 `modulesUrl` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="c09f9-133">SAS 토큰 hello에 지정할 수 있습니다이 위치가 Azure blob 저장소에 있으면 `sasToken` 속성 tooaccess hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="c09f9-134">Hello.zip을 다운로드 하 여 압축을 푼 후에 정의 된 구성 함수 hello `configurationFunction` toogenerate hello MOF 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="c09f9-135">hello 확장 한 다음 실행 `Start-DscConfiguration -Force` on hello 생성 된 MOF 파일.</span><span class="sxs-lookup"><span data-stu-id="c09f9-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="c09f9-136">hello 확장 출력 캡처하고 toohello Azure 상태 채널 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="c09f9-137">Hello에이 지점에서 DSC LCM 모니터링 및 수정 정상적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="c09f9-138">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="c09f9-138">PowerShell cmdlets</span></span>
<span data-ttu-id="c09f9-139">PowerShell cmdlet Azure 리소스 관리자와 함께 사용할 수 있습니다 또는 클래식 배포 모델 toopackage hello, 게시 및 DSC 확장 배포를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="c09f9-140">hello 나열 된 다음 cmdlet hello 클래식 배포 모듈에 있더라도 "Azure"는 "AzureRm" toouse hello Azure 리소스 관리자 모델으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="c09f9-141">예를 들어 `Publish-AzureVMDscConfiguration` 사용 하 여 hello 클래식 배포 모델 여기서 `Publish-AzureRmVMDscConfiguration` Azure 리소스 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="c09f9-142">`Publish-AzureVMDscConfiguration`구성 파일에서 걸리며 종속 DSC 리소스에 대 한 검색 hello 구성 및 DSC 리소스 필요한 tooenact hello 구성에 포함 된.zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="c09f9-143">Hello를 사용 하 여 로컬로 hello 패키지를 만들 수도 수 `-ConfigurationArchivePath` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="c09f9-144">그렇지 않으면 hello.zip 파일 tooAzure blob 저장소를 게시 하 고 있는 SAS 토큰으로 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="c09f9-145">이 cmdlet에서 만든 hello.zip 파일의 hello.ps1 구성 스크립트를 hello 보관 폴더의 hello 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="c09f9-146">리소스는 hello 모듈 폴더 hello 보관 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="c09f9-147">`Set-AzureVMDscExtension`VM 구성 개체에 hello PowerShell DSC 확장에 필요한 hello 설정을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="c09f9-148">Hello 클래식 배포 모델에서 hello VM 변경 해야 합니다 적용된 tooan Azure VM으로 `Update-AzureVM`합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="c09f9-149">`Get-AzureVMDscExtension`특정 VM의 hello DSC 확장 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="c09f9-150">`Get-AzureVMDscExtensionStatus`hello DSC 확장 처리기를 통해 시행 되 hello DSC 구성의 hello 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="c09f9-151">이 작업을 단일 VM 또는 VM 그룹에 대해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="c09f9-152">`Remove-AzureVMDscExtension`지정된 된 가상 컴퓨터에서 hello 확장 처리기를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="c09f9-153">이 cmdlet이 수행 **하지** hello 구성을 제거, hello WMF, 제거 또는 hello 가상 컴퓨터에 적용 하는 hello 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="c09f9-154">만 hello 확장 처리기를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="c09f9-155">**ASM과 Azure Resource Manager cmdlets의 주요 차이점**</span><span class="sxs-lookup"><span data-stu-id="c09f9-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="c09f9-156">Azure Resource Manager cmdlets는 동기입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="c09f9-157">ASM cmdlet은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="c09f9-158">ResourceGroupName, VMName, ArchiveStorageAccountName, 버전, 위치는 Azure Resource Manager에서 모두 새 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="c09f9-159">ArchiveResourceGroupName은 Azure Resource Manager에 대한 새로운 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="c09f9-160">저장소 계정 하나 hello 보다 tooa 다른 리소스 그룹 hello 가상 컴퓨터를 만들 위치 속해 있는 경우이 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="c09f9-161">ConfigurationArchive는 Azure Resource Manager에서 ArchiveBlobName이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="c09f9-162">ContainerName은 Azure Resource Manager에서 ArchiveContainerName이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="c09f9-163">StorageEndpointSuffix는 Azure Resource Manager에서 ArchiveStorageEndpointSuffix라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="c09f9-164">자동 업데이트 사용 가능 해지면 및 hello 확장 처리기 toohello 최신 버전으로의 리소스 관리자 tooenable tooAzure hello AutoUpdate 스위치 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="c09f9-165">이 매개 변수는 hello 잠재적인 toocause 참고 hello 새 버전의 hello WMF 해제 될 때 VM에 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="c09f9-166">Azure 포털 기능</span><span class="sxs-lookup"><span data-stu-id="c09f9-166">Azure portal functionality</span></span>
<span data-ttu-id="c09f9-167">Tooa VM을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-167">Browse tooa VM.</span></span> <span data-ttu-id="c09f9-168">설정 -> 일반에서 "확장"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="c09f9-169">새 창을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-169">A new pane is created.</span></span> <span data-ttu-id="c09f9-170">"추가"를 클릭하고 PowerShell DSC를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="c09f9-171">hello 포털에 입력을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-171">hello portal needs input.</span></span>
<span data-ttu-id="c09f9-172">**구성 모듈 또는 스크립트**: 이 필드는 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="c09f9-173">구성 스크립트를 포함 하는.ps1 파일 또는 hello 루트에서.ps1 구성 스크립트 및 hello.zip 내의 모듈 폴더의 모든 종속 리소스와.zip 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="c09f9-174">Hello로 만들 수 있습니다 `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet hello Azure PowerShell SDK에에서 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="c09f9-175">hello.zip 파일이 SAS 토큰을 통해 보안이 유지 하 여 사용자 blob 저장소에 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="c09f9-176">**구성 데이터 PSD1 파일**: 이 필드는 선택적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="c09f9-177">구성에 필요한.psd1에서 구성 데이터 파일을 사용 하 여이 필드 tooselect 것는 SAS 토큰에 의해 보호 tooyour 사용자 blob 저장소에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="c09f9-178">**구성의 모듈 정규화된 이름**: .ps1 파일에는 여러 개의 구성 함수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="c09f9-179">Hello 구성.ps1 스크립트 뒤의 hello 이름을 입력 한 '\' hello 함수의 및 이름 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="c09f9-180">예를 들어.ps1 스크립트에서 hello 이름 "configuration.ps1" hello 구성은 "IisInstall"을 입력 합니다.`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="c09f9-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="c09f9-181">**구성 인수**: hello 구성 함수는 인수를 사용 하는 경우 hello 형태로 표시 여기에 입력 한 `argumentName1=value1,argumentName2=value2`합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="c09f9-182">PowerShell cmdlet 또는 Resource Manager 템플릿을 통해 구성 인수를 수락하는 방법과는 다른 서식입니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c09f9-183">시작</span><span class="sxs-lookup"><span data-stu-id="c09f9-183">Getting started</span></span>
<span data-ttu-id="c09f9-184">DSC 구성 문서에는 Azure Vm에서 해당을 시행 하는 hello Azure DSC 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="c09f9-185">구성의 간단한 예제가 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="c09f9-186">"IisInstall.ps1"으로 다음과 같이 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="c09f9-187">hello 단계 위치 hello IisInstall.ps1 스크립트에 나오는 hello에 VM을 지정 하 고 hello 구성, 실행 상태 다시 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="c09f9-188">클래식 모델</span><span class="sxs-lookup"><span data-stu-id="c09f9-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="c09f9-189">Azure Resource Manager 모델</span><span class="sxs-lookup"><span data-stu-id="c09f9-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="c09f9-190">로깅</span><span class="sxs-lookup"><span data-stu-id="c09f9-190">Logging</span></span>
<span data-ttu-id="c09f9-191">로그는 다음에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-191">Logs are placed in:</span></span>

<span data-ttu-id="c09f9-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span><span class="sxs-lookup"><span data-stu-id="c09f9-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c09f9-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c09f9-193">Next steps</span></span>
<span data-ttu-id="c09f9-194">PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="c09f9-195">Hello 검사 [hello DSC 확장에 대 한 Azure Resource Manager 템플릿](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c09f9-196">PowerShell DSC로 관리할 수 있는 toofind 추가 기능 [hello PowerShell 갤러리 찾아보기](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) 자세한 DSC 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="c09f9-197">구성으로 중요 한 매개 변수 전달에 대 한 세부 정보를 참조 하십시오. [hello DSC 확장 처리기와 안전 하 게 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c09f9-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

