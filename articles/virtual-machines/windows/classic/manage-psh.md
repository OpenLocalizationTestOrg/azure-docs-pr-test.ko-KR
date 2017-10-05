---
title: "Azure PowerShell을 사용하여 가상 컴퓨터 관리 | Microsoft Docs"
description: "가상 컴퓨터 관리에서의 작업 자동화에 사용할 수 있는 명령에 대해 알아봅니다."
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
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="5a008-103">Azure PowerShell을 사용하여 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="5a008-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="5a008-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5a008-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5a008-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5a008-107">Resource Manager 모델을 사용하여 일반적인 PowerShell 명령은 [여기](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a008-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5a008-108">Azure PowerShell cmdlet을 사용하여 매일 VM을 관리하기 위해 수행하는 많은 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5a008-109">이 문서에서는 더 간단한 작업에 대한 예제 명령과 보다 복잡한 작업에 대한 명령을 보여 주는 문서에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="5a008-110">Azure PowerShell을 아직 설치 및 구성하지 않은 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)문서에서 지침을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="5a008-111">예제 명령을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="5a008-111">How to use the example commands</span></span>
<span data-ttu-id="5a008-112">명령의 일부 텍스트는 환경에 적합한 텍스트로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="5a008-113">< 및 > 기호는 바꿔야 하는 텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="5a008-114">텍스트를 바꾸는 경우 기호는 제거하고 따옴표는 그대로 남겨 두세요.</span><span class="sxs-lookup"><span data-stu-id="5a008-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="5a008-115">VM 확인</span><span class="sxs-lookup"><span data-stu-id="5a008-115">Get a VM</span></span>
<span data-ttu-id="5a008-116">자주 사용하게 될 기본 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="5a008-117">이 작업을 사용하여 VM에 대한 정보를 가져오거나 VM에서 작업을 수행하거나 변수에 저장할 출력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="5a008-118">VM에 대한 정보를 가져오려면 이 명령을 실행하고 < 및 > 문자를 포함하여 따옴표 안의 모든 항목을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="5a008-119">출력을 $vm 변수에 저장하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="5a008-120">Windows 기반 VM에 로그온</span><span class="sxs-lookup"><span data-stu-id="5a008-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="5a008-121">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="5a008-122">**Get-AzureVM** 명령 표시에서 가상 컴퓨터 및 클라우드 서비스 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="5a008-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<다운로드한 RDP 파일을 저장할 드라이브 및 폴더 위치, 예: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="5a008-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="5a008-124">VM 중지</span><span class="sxs-lookup"><span data-stu-id="5a008-124">Stop a VM</span></span>
<span data-ttu-id="5a008-125">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="5a008-126">해당 클라우드 서비스의 마지막 VM인 경우 이 매개 변수를 사용하여 클라우드 서비스의 VIP(가상 IP)를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="5a008-127">StayProvisioned 매개 변수를 사용하는 경우 VM에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="5a008-128">VM 시작</span><span class="sxs-lookup"><span data-stu-id="5a008-128">Start a VM</span></span>
<span data-ttu-id="5a008-129">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="5a008-130">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="5a008-130">Attach a data disk</span></span>
<span data-ttu-id="5a008-131">이 작업에는 몇 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-131">This task requires a few steps.</span></span> <span data-ttu-id="5a008-132">먼저, ****Add-AzureDataDisk**** cmdlet를 사용하여 $vm 개체에 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="5a008-133">그런 다음 **Update-AzureVM** cmdlet을 사용하여 VM의 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="5a008-134">또한 새 디스크를 연결할지 데이터를 포함하는 디스크를 연결할지를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="5a008-135">새 디스크의 경우 이 명령은 .vhd 파일을 만들고 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="5a008-136">새 디스크를 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="5a008-137">기존 데이터 디스크를 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="5a008-138">Blob 저장소의 기존 .vhd 파일에서 데이터 디스크를 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="5a008-139">Windows 기반 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="5a008-139">Create a Windows-based VM</span></span>
<span data-ttu-id="5a008-140">Azure에서 새 Windows 기반 가상 컴퓨터를 만들려면 [Azure PowerShell을 사용하여 Windows 기반 가상 컴퓨터를 만들고 미리 구성](create-powershell.md)의 지침을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5a008-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="5a008-141">이 항목에서는 미리 구성할 수 있는 Windows VM을 만드는 Azure PowerShell 명령 집합 만들기를 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5a008-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="5a008-142">Active Directory 도메인 구성원 자격을 통해 만들기</span><span class="sxs-lookup"><span data-stu-id="5a008-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="5a008-143">추가 디스크를 통해 만들기</span><span class="sxs-lookup"><span data-stu-id="5a008-143">With additional disks.</span></span>
* <span data-ttu-id="5a008-144">기존 부하 분산 집합의 구성원으로 만들기</span><span class="sxs-lookup"><span data-stu-id="5a008-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="5a008-145">고정 IP 주소로 만들기</span><span class="sxs-lookup"><span data-stu-id="5a008-145">With a static IP address.</span></span>

