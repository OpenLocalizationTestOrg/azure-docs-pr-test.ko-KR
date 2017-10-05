---
title: "Azure에 필요한 상태 구성 개요 | Microsoft Docs"
description: "PowerShell 필요한 상태 구성에 대한 Microsoft Azure 확장 처리기를 사용하는 개요입니다. 필수 구성 요소, 아키텍처, cmdlet...을 포함"
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
ms.openlocfilehash: c05c2d541a5f526f362f9cd72fe6d878374112b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="3789f-104">Azure 필요한 상태 구성 확장 처리기 소개</span><span class="sxs-lookup"><span data-stu-id="3789f-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3789f-105">Azure VM 에이전트 및 연결된 확장은 Microsoft Azure 인프라 서비스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="3789f-106">VM 확장은 VM 기능을 확장하고 다양한 VM 관리 작업을 단순화하는 소프트웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="3789f-107">예를 들어 VMAccess 확장은 관리자의 암호를 다시 설정하는 데 사용될 수 있고 사용자 지정 확장은 VM에서 스크립트를 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="3789f-108">이 문서에서는 Azure PowerShell SDK의 일부로 Azure VM에 대한 PowerShell DSC(필요한 상태 구성) 확장을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="3789f-109">새로운 cmdlet을 사용하여 PowerShell DSC 확장을 사용하는 Azure VM에 PowerShell DSC 구성을 업로드하고 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="3789f-110">PowerShell DSC 확장은 VM에서 받은 DSC 구성을 적용하도록 PowerShell DSC에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="3789f-111">또한 이 기능은 Azure 포털을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3789f-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3789f-112">Prerequisites</span></span>
<span data-ttu-id="3789f-113">**로컬 컴퓨터** Azure VM 확장과 상호 작용하려면 Azure 포털 또는 Azure PowerShell SDK를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="3789f-114">**게스트 에이전트** DSC 구성으로 구성된 Azure VM은 WMF(Windows Management Framework) 4.0 또는 5.0를 지원하는 OS여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="3789f-115">지원되는 OS 버전의 전체 목록은 [DSC 확장 버전 기록](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="3789f-116">용어 및 개념</span><span class="sxs-lookup"><span data-stu-id="3789f-116">Terms and concepts</span></span>
<span data-ttu-id="3789f-117">이 가이드에서는 다음과 같은 개념에 익숙합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="3789f-118">구성 - DSC 구성 문서.</span><span class="sxs-lookup"><span data-stu-id="3789f-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="3789f-119">노드 - DSC 구성에 대한 대상.</span><span class="sxs-lookup"><span data-stu-id="3789f-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="3789f-120">이 문서에서 "노드"는 Azure VM을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="3789f-121">구성 데이터 - 구성에 대한 환경 데이터를 포함하는 .psd1 파일</span><span class="sxs-lookup"><span data-stu-id="3789f-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="3789f-122">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="3789f-122">Architectural overview</span></span>
<span data-ttu-id="3789f-123">Azure DSC 확장은 Azure VM 에이전트 프레임워크를 사용하여 Azure VM에서 실행되는 DSC 구성을 제공하고 적용하며 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="3789f-124">DSC 확장은 Azure PowerShell SDK 또는 Azure 포털을 통해 제공되는 최소한의 구성 문서 및 일련의 매개 변수를 포함하는 .zip 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="3789f-125">확장이 처음으로 호출되면 설치 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="3789f-126">이 프로세스는 다음 논리를 사용하여 WMF(Windows Management Framework)의 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="3789f-127">Azure VM OS가 Windows Server 2016이면 아무 작업도 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="3789f-128">Windows Server 2016에는 이미 최신 버전의 PowerShell이 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="3789f-129">`wmfVersion` 속성을 지정하면 VM의 OS와 호환되지 않는 경우가 아닌 경우 해당 버전의 WMF가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="3789f-130">`wmfVersion` 속성을 지정하면 WMF의 적용 가능한 최신 버전이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="3789f-131">WMF를 설치하려면 다시 부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="3789f-132">다시 부팅한 후에 확장은 `modulesUrl` 속성에 지정된 .zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="3789f-133">이 위치가 Azure Blob 저장소인 경우 SAS 토큰은 `sasToken` 속성에 지정되어 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="3789f-134">.zip을 다운로드하고 압축을 푼 후에 `configurationFunction` 에 정의된 구성 함수를 실행하여 MOF 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="3789f-135">그런 다음 확장은 생성된 MOF 파일에 `Start-DscConfiguration -Force` 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="3789f-136">확장은 출력을 캡처하고 Azure 상태 채널에 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="3789f-137">이 시점부터 DSC LCM은 모니터링 및 수정을 정상적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="3789f-138">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="3789f-138">PowerShell cmdlets</span></span>
<span data-ttu-id="3789f-139">PowerShell cmdlet은 DSC 확장 배포를 패키징하고 게시하며 모니터링하기 위해 Azure Resource Manager 또는 클래식 배포 모델과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="3789f-140">나열된 다음 cmdlet은 클래식 배포 모듈이지만 "Azure"는 Azure Resource Manager 모델을 사용하는 "AzureRm"으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="3789f-141">예를 들어, `Publish-AzureVMDscConfiguration`에서는 클래식 배포 모델을 사용하고 `Publish-AzureRmVMDscConfiguration`에서는 Azure Resource Manager를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="3789f-142">`Publish-AzureVMDscConfiguration` 은 구성 파일을 받고 종속 DSC 리소스를 검색하며 구성 및 구성을 적용하는 데 필요한 DSC 리소스를 포함하는 .zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="3789f-143">또는 `-ConfigurationArchivePath` 매개 변수를 사용하여 패키지를 로컬로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="3789f-144">그렇지 않으면 Azure Blob 저장소에 .zip 파일을 게시하고 SAS 토큰으로 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="3789f-145">이 cmdlet에서 만든 .zip 파일은 보관 폴더의 루트에서 .ps1 구성 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="3789f-146">리소스에는 보관 폴더에 위치한 모듈 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="3789f-147">`Set-AzureVMDscExtension`은 VM 구성 개체에 PowerShell DSC 확장에서 필요한 설정을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="3789f-148">클래식 배포 모델에서 VM 변경 사항은 `Update-AzureVM` 지원 Azure VM에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="3789f-149">`Get-AzureVMDscExtension`은 특정 VM의 DSC 확장 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="3789f-150">`Get-AzureVMDscExtensionStatus` 는 DSC 확장 처리기에 의해 적용되는 DSC 구성의 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="3789f-151">이 작업을 단일 VM 또는 VM 그룹에 대해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="3789f-152">`Remove-AzureVMDscExtension` 은 지정된 가상 컴퓨터에서 확장 처리기를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="3789f-153">이 cmdlet은 구성을 제거하거나 WMF를 제거하거나 가상 컴퓨터에 적용된 설정을 변경하지 **않습니다** .</span><span class="sxs-lookup"><span data-stu-id="3789f-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="3789f-154">확장 처리기를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="3789f-155">**ASM과 Azure Resource Manager cmdlets의 주요 차이점**</span><span class="sxs-lookup"><span data-stu-id="3789f-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="3789f-156">Azure Resource Manager cmdlets는 동기입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="3789f-157">ASM cmdlet은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="3789f-158">ResourceGroupName, VMName, ArchiveStorageAccountName, 버전, 위치는 Azure Resource Manager에서 모두 새 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="3789f-159">ArchiveResourceGroupName은 Azure Resource Manager에 대한 새로운 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="3789f-160">저장소 계정이 가상 컴퓨터를 만들 위치가 아닌 다른 리소스 그룹에 속해 있는 경우 이 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="3789f-161">ConfigurationArchive는 Azure Resource Manager에서 ArchiveBlobName이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="3789f-162">ContainerName은 Azure Resource Manager에서 ArchiveContainerName이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="3789f-163">StorageEndpointSuffix는 Azure Resource Manager에서 ArchiveStorageEndpointSuffix라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="3789f-164">AutoUpdate 스위치가 Azure Resource Manager에 추가되어 확장 처리기를 사용할 수 있는 경우 최신 버전으로 자동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="3789f-165">이 매개 변수를 사용하면 새 버전의 WMF가 릴리스될 때 VM이 다시 시작될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="3789f-166">Azure 포털 기능</span><span class="sxs-lookup"><span data-stu-id="3789f-166">Azure portal functionality</span></span>
<span data-ttu-id="3789f-167">VM으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-167">Browse to a VM.</span></span> <span data-ttu-id="3789f-168">설정 -> 일반에서 "확장"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="3789f-169">새 창을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-169">A new pane is created.</span></span> <span data-ttu-id="3789f-170">"추가"를 클릭하고 PowerShell DSC를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="3789f-171">포털에 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-171">The portal needs input.</span></span>
<span data-ttu-id="3789f-172">**구성 모듈 또는 스크립트**: 이 필드는 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="3789f-173">.zip 파일 내의 모듈 폴더에서 루트 및 모든 종속 리소스 루트에 구성 스크립트를 포함하는 .ps1 파일 또는 .ps1 구성 스크립트를 포함하는 .zip 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="3789f-174">Azure PowerShell SDK에 포함된 `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="3789f-175">.zip 파일은 SAS 토큰에 의해 보호된 사용자 Blob 저장소에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="3789f-176">**구성 데이터 PSD1 파일**: 이 필드는 선택적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="3789f-177">구성에 .psd1의 구성 데이터 파일이 필요한 경우 이 필드를 사용하여 선택하고 사용자 Blob 저장소에 업로드합니다. 이 저장소는 SAS 토큰으로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="3789f-178">**구성의 모듈 정규화된 이름**: .ps1 파일에는 여러 개의 구성 함수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="3789f-179">예를 들어 '\'에 이어서 구성 .ps1 스크립트의 이름 및 구성 함수의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="3789f-180">예를 들어 .ps1 스크립트 이름이 "configuration.ps1"이고 구성이 "IisInstall"이면 `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="3789f-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="3789f-181">**구성 인수**: 구성 함수가 인수를 사용하는 경우 `argumentName1=value1,argumentName2=value2` 형식으로 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="3789f-182">PowerShell cmdlet 또는 Resource Manager 템플릿을 통해 구성 인수를 수락하는 방법과는 다른 서식입니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3789f-183">시작</span><span class="sxs-lookup"><span data-stu-id="3789f-183">Getting started</span></span>
<span data-ttu-id="3789f-184">Azure DSC 확장은 DSC 구성 문서를 수용하고 Azure VM에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="3789f-185">구성의 간단한 예제가 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="3789f-186">"IisInstall.ps1"으로 다음과 같이 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-186">Save it locally as "IisInstall.ps1":</span></span>

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

<span data-ttu-id="3789f-187">다음 단계는 지정된 VM에서 IisInstall.ps1 스크립트를 배치하고 구성을 실행하며 상태를 다시 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="3789f-188">클래식 모델</span><span class="sxs-lookup"><span data-stu-id="3789f-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="3789f-189">Azure Resource Manager 모델</span><span class="sxs-lookup"><span data-stu-id="3789f-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="3789f-190">로깅</span><span class="sxs-lookup"><span data-stu-id="3789f-190">Logging</span></span>
<span data-ttu-id="3789f-191">로그는 다음에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-191">Logs are placed in:</span></span>

<span data-ttu-id="3789f-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span><span class="sxs-lookup"><span data-stu-id="3789f-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3789f-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3789f-193">Next steps</span></span>
<span data-ttu-id="3789f-194">PowerShell DSC에 대한 자세한 내용은 [PowerShell 설명서 센터를 방문하세요](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="3789f-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="3789f-195">[DSC 확장에 대한 Azure Resource Manager 템플릿](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3789f-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3789f-196">PowerShell DSC로 관리할 수 있는 추가 기능을 찾으려면 추가 DSC 리소스는 [PowerShell 갤러리에서 찾아보세요](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) .</span><span class="sxs-lookup"><span data-stu-id="3789f-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="3789f-197">중요한 매개 변수를 구성에 전달하는 세부 정보는 [DSC 확장 처리기로 안전하게 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3789f-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

