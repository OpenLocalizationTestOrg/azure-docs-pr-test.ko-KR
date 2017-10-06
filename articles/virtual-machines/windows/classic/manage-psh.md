---
title: "aaaManage Azure PowerShell을 사용 하 여 가상 컴퓨터 | Microsoft Docs"
description: "가상 컴퓨터 관리의 tooautomate 작업을 사용할 수 있는 명령에 알아봅니다."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="3a93b-103">Azure PowerShell을 사용하여 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="3a93b-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3a93b-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3a93b-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3a93b-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3a93b-107">Hello 리소스 관리자 모델을 사용 하 여 일반적인 PowerShell 명령 참조 [여기](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3a93b-108">많은 작업을 수행할 일 toomanage 각 Vm에 Azure PowerShell cmdlet을 사용 하 여 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3a93b-109">이 문서에서는 간단한 작업 및 링크 tooarticles 더 복잡 한 작업에 대 한 hello 명령을 보여 주는 예제 명령을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="3a93b-110">아직 설치 하 고 Azure PowerShell을 구성 하지 않은 hello 문서의 지침을 가져올 수 있습니다 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="3a93b-111">어떻게 toouse hello 명령 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-111">How toouse hello example commands</span></span>
<span data-ttu-id="3a93b-112">사용자 환경에 적합 한 텍스트로 명령을 hello hello 텍스트의 일부 tooreplace가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="3a93b-113">hello < 및 > 기호 tooreplace 필요한 텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="3a93b-114">Hello 텍스트를 대체 hello 기호를 제거 하지만 원위치에서 hello 인용 부호를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="3a93b-115">VM 확인</span><span class="sxs-lookup"><span data-stu-id="3a93b-115">Get a VM</span></span>
<span data-ttu-id="3a93b-116">자주 사용하게 될 기본 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="3a93b-117">VM에 대 한 tooget 정보를 사용 하, vm에서 작업을 수행 하거나 변수에 출력 toostore를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="3a93b-118">VM hello에 대 한 정보 tooget hello < 및 > 문자를 포함 하 여 hello 따옴표로 모두 교체,이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="3a93b-119">$vm 변수에 출력 toostore hello 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="3a93b-120">Windows 기반 VM tooa 로그온</span><span class="sxs-lookup"><span data-stu-id="3a93b-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="3a93b-121">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="3a93b-122">Hello hello 표시에서 hello 가상 컴퓨터 및 클라우드 서비스 이름을 얻을 수 **Get-azurevm** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="3a93b-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< 드라이브 및 폴더 위치 toostore hello 다운로드 한 RDP 파일, 예: c:\temp >" $localFile $localPath = + "\" + $vmname +".rdp"Get-azureremotedesktopfile- ServiceName $svcName-$vmName LocalPath $localFile 이름-시작</span><span class="sxs-lookup"><span data-stu-id="3a93b-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="3a93b-124">VM 중지</span><span class="sxs-lookup"><span data-stu-id="3a93b-124">Stop a VM</span></span>
<span data-ttu-id="3a93b-125">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="3a93b-126">VIP (가상 IP) hello 클라우드 서비스는 경우이 매개 변수 tookeep hello를 사용 하 여 해당 클라우드 서비스에서 마지막 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="3a93b-127">Hello StayProvisioned 매개 변수를 사용 하는 경우 VM hello에 대 한 청구 여전히 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="3a93b-128">VM 시작</span><span class="sxs-lookup"><span data-stu-id="3a93b-128">Start a VM</span></span>
<span data-ttu-id="3a93b-129">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="3a93b-130">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="3a93b-130">Attach a data disk</span></span>
<span data-ttu-id="3a93b-131">이 작업에는 몇 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-131">This task requires a few steps.</span></span> <span data-ttu-id="3a93b-132">먼저, 사용 하 여 hello * * * 추가-AzureDataDisk * * * cmdlet tooadd hello 디스크 toohello $vm 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="3a93b-133">그런 다음 **Update-azurevm** hello VM의 cmdlet tooupdate hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="3a93b-134">또한 해야 toodecide tooattach 새 디스크 또는 하나를 포함 하는지 여부를 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="3a93b-135">새 디스크에 대 한 hello 명령 hello.vhd 파일을 만들어 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="3a93b-136">새 디스크 tooattach이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="3a93b-137">기존의 데이터 디스크를 tooattach이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="3a93b-138">tooattach 데이터 디스크 blob 저장소에 기존.vhd 파일에서이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="3a93b-139">Windows 기반 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3a93b-139">Create a Windows-based VM</span></span>
<span data-ttu-id="3a93b-140">새 Windows 기반 가상 컴퓨터를 azure에서의 지침을 사용 하 여 hello toocreate [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](create-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="3a93b-141">이 항목의 단계 hello 생성 된 Azure PowerShell 명령 집합을 통해을 만듭니다 Windows 기반 VM을 미리 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a93b-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="3a93b-142">Active Directory 도메인 구성원 자격을 통해 만들기</span><span class="sxs-lookup"><span data-stu-id="3a93b-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="3a93b-143">추가 디스크를 통해 만들기</span><span class="sxs-lookup"><span data-stu-id="3a93b-143">With additional disks.</span></span>
* <span data-ttu-id="3a93b-144">기존 부하 분산 집합의 구성원으로 만들기</span><span class="sxs-lookup"><span data-stu-id="3a93b-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="3a93b-145">고정 IP 주소로 만들기</span><span class="sxs-lookup"><span data-stu-id="3a93b-145">With a static IP address.</span></span>

