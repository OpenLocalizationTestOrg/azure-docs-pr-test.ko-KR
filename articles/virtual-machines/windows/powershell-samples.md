---
title: "Azure Virtual Machine PowerShell 샘플 | Microsoft Docs"
description: "Azure Virtual Machine PowerShell 샘플"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ff8b741b04ff37fa1a5fbaddabdd588ab43f19c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a><span data-ttu-id="33fc4-103">Azure Virtual Machine PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="33fc4-103">Azure Virtual Machine PowerShell samples</span></span>

<span data-ttu-id="33fc4-104">다음 표에는 Windows 가상 컴퓨터를 만들고 관리하는 PowerShell 스크립트 샘플에 대한 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-104">The following table includes links to PowerShell scripts samples that create and manage Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="33fc4-105">**가상 컴퓨터 만들기**</span><span class="sxs-lookup"><span data-stu-id="33fc4-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="33fc4-106">완벽히 구성된 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-106">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-107">리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-107">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="33fc4-108">고가용성 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-108">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-109">고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-109">Creates several virtual machines in a highly available and load balanced configuration.</span></span>|
| [<span data-ttu-id="33fc4-110">VM 만들기 및 구성 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="33fc4-110">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-111">가상 컴퓨터를 만들고 Azure 사용자 지정 스크립트 확장을 사용하여 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-111">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="33fc4-112">VM 만들기 및 DSC 구성 실행</span><span class="sxs-lookup"><span data-stu-id="33fc4-112">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-113">가상 컴퓨터를 만들고 Azure DSC(필요한 상태 구성) 확장을 사용하여 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-113">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
| [<span data-ttu-id="33fc4-114">VHD 업로드 및 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-114">Upload a VHD and create VMs</span></span>](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | <span data-ttu-id="33fc4-115">로컬 VHD 파일을 Azure에 업로드하고 VHD에서 이미지 만든 후 해당 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-115">Uplaods a local VHD file to Azure, creates and image from the VHD and then creates a VM from that image.</span></span> |
| [<span data-ttu-id="33fc4-116">관리되는 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-116">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-117">기존 관리되는 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-117">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="33fc4-118">스냅숏에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-118">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-119">먼저 스냅숏에서 관리되는 디스크를 만들고 새 관리되는 디스크를 OS 디스크로 연결하여 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-119">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching the new managed disk as OS disk.</span></span> |
|<span data-ttu-id="33fc4-120">**저장소 관리**</span><span class="sxs-lookup"><span data-stu-id="33fc4-120">**Manage storage**</span></span>||
| [<span data-ttu-id="33fc4-121">동일하거나 다른 구독의 VHD에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-121">Create managed disk from a VHD in same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-122">동일하거나 다른 구독에서 특수화된 VHD의 관리 디스크를 OS 디스크로 만들거나 데이터 VHD의 관리 디스크를 데이터 디스크로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-122">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk in same or different subscription.</span></span>  |
| [<span data-ttu-id="33fc4-123">스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-123">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-124">스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-124">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="33fc4-125">동일하거나 다른 구독으로 관리 디스크 복사</span><span class="sxs-lookup"><span data-stu-id="33fc4-125">Copy managed disk to same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-126">부모 관리 디스크와 같은 지역에 있지만 동일하거나 다른 구독으로 관리 디스크를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-126">Copies managed disk to same or different subscription but in the same region as the parent managed disk.</span></span> 
| [<span data-ttu-id="33fc4-127">저장소 계정에 VHD로 스냅샷 내보내기</span><span class="sxs-lookup"><span data-stu-id="33fc4-127">Export a snapshot as VHD to a storage account</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-128">다른 지역의 저장소 계정에 관리 스냅숏을 VHD로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-128">Exports a managed snapshot as VHD to a storage account in different region.</span></span> |
| [<span data-ttu-id="33fc4-129">VHD에서 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="33fc4-129">Create a snapshot from a VHD</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-130">VHD에서 스냅숏을 만들어 짧은 시간 동안 스냅숏에서 동일한 여러 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-130">Creates snapshot from a VHD to create multiple identical managed disks from snapshot in short amount of time.</span></span>  |
| [<span data-ttu-id="33fc4-131">동일하거나 다른 구독으로 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="33fc4-131">Copy snapshot to same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-132">부모 스냅숏과 같은 지역에 있지만 동일하거나 다른 구독으로 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-132">Copies snapshot to same or different subscription but in the same region as the parent snapshot.</span></span> |
|<span data-ttu-id="33fc4-133">**가상 컴퓨터 보호**</span><span class="sxs-lookup"><span data-stu-id="33fc4-133">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="33fc4-134">VM 및 데이터 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="33fc4-134">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | <span data-ttu-id="33fc4-135">Azure Key Vault, 암호화 키 및 서비스 주체를 만든 다음 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-135">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="33fc4-136">**가상 컴퓨터 모니터링**</span><span class="sxs-lookup"><span data-stu-id="33fc4-136">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="33fc4-137">Operations Management Suite를 사용하여 VM 모니터링</span><span class="sxs-lookup"><span data-stu-id="33fc4-137">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="33fc4-138">가상 컴퓨터를 만들고 Operations Management Suite 에이전트를 설치하고 OMS 작업 영역에서 VM을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="33fc4-138">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |

