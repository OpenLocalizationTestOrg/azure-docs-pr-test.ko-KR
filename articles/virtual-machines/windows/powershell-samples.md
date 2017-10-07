---
title: "가상 컴퓨터 PowerShell 샘플 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a><span data-ttu-id="b3da7-103">Azure Virtual Machine PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="b3da7-103">Azure Virtual Machine PowerShell samples</span></span>

<span data-ttu-id="b3da7-104">hello 다음 표는 Windows 가상 컴퓨터 만들기 및 관리 하는 링크 tooPowerShell 스크립트 예제.</span><span class="sxs-lookup"><span data-stu-id="b3da7-104">hello following table includes links tooPowerShell scripts samples that create and manage Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="b3da7-105">**가상 컴퓨터 만들기**</span><span class="sxs-lookup"><span data-stu-id="b3da7-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="b3da7-106">완벽히 구성된 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-106">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-107">리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-107">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="b3da7-108">고가용성 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-108">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-109">고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-109">Creates several virtual machines in a highly available and load balanced configuration.</span></span>|
| [<span data-ttu-id="b3da7-110">VM 만들기 및 구성 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="b3da7-110">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-111">Hello Azure 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-111">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="b3da7-112">VM 만들기 및 DSC 구성 실행</span><span class="sxs-lookup"><span data-stu-id="b3da7-112">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-113">Hello Azure DSC 필요한 상태 구성 () 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-113">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="b3da7-114">VHD 업로드 및 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-114">Upload a VHD and create VMs</span></span>](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | <span data-ttu-id="b3da7-115">로컬 VHD Uplaods tooAzure 파일, 및 hello VHD에서에서 이미지 만들고 그런 다음 해당 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-115">Uplaods a local VHD file tooAzure, creates and image from hello VHD and then creates a VM from that image.</span></span> |
| [<span data-ttu-id="b3da7-116">관리되는 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-116">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-117">기존 관리되는 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-117">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="b3da7-118">스냅숏에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-118">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-119">먼저 관리 되는 디스크 스냅숏에서 만들고 운영 체제 디스크로 hello 새 관리 되는 디스크를 연결 하는 다음 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-119">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching hello new managed disk as OS disk.</span></span> |
|<span data-ttu-id="b3da7-120">**저장소 관리**</span><span class="sxs-lookup"><span data-stu-id="b3da7-120">**Manage storage**</span></span>||
| [<span data-ttu-id="b3da7-121">동일하거나 다른 구독의 VHD에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-121">Create managed disk from a VHD in same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-122">동일하거나 다른 구독에서 특수화된 VHD의 관리 디스크를 OS 디스크로 만들거나 데이터 VHD의 관리 디스크를 데이터 디스크로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-122">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk in same or different subscription.</span></span>  |
| [<span data-ttu-id="b3da7-123">스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-123">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-124">스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-124">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="b3da7-125">관리 되는 디스크 toosame 또는 다른 구독 복사</span><span class="sxs-lookup"><span data-stu-id="b3da7-125">Copy managed disk toosame or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-126">관리 되는 복사본이 디스크 toosame 또는 다른 구독 하지만 동일한 hello 지역 hello 부모 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-126">Copies managed disk toosame or different subscription but in hello same region as hello parent managed disk.</span></span> 
| [<span data-ttu-id="b3da7-127">스냅숏을 VHD tooa 저장소 계정으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="b3da7-127">Export a snapshot as VHD tooa storage account</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-128">다른 지역에 VHD tooa 저장소 계정으로 관리 되는 스냅숏을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-128">Exports a managed snapshot as VHD tooa storage account in different region.</span></span> |
| [<span data-ttu-id="b3da7-129">VHD에서 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="b3da7-129">Create a snapshot from a VHD</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-130">스냅숏 VHD toocreate에서 스냅숏에서 여러 개의 동일한 관리 되는 디스크에에서 만듭니다 짧은 시간.</span><span class="sxs-lookup"><span data-stu-id="b3da7-130">Creates snapshot from a VHD toocreate multiple identical managed disks from snapshot in short amount of time.</span></span>  |
| [<span data-ttu-id="b3da7-131">스냅숏 toosame 또는 다른 구독 복사</span><span class="sxs-lookup"><span data-stu-id="b3da7-131">Copy snapshot toosame or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-132">스냅숏 toosame 복사본 또는 hello 동일 하지만 다른 구독 hello 부모 스냅숏으로 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-132">Copies snapshot toosame or different subscription but in hello same region as hello parent snapshot.</span></span> |
|<span data-ttu-id="b3da7-133">**가상 컴퓨터 보호**</span><span class="sxs-lookup"><span data-stu-id="b3da7-133">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="b3da7-134">VM 및 데이터 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="b3da7-134">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | <span data-ttu-id="b3da7-135">Azure Key Vault, 암호화 키 및 서비스 주체를 만든 다음 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-135">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="b3da7-136">**가상 컴퓨터 모니터링**</span><span class="sxs-lookup"><span data-stu-id="b3da7-136">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="b3da7-137">Operations Management Suite를 사용하여 VM 모니터링</span><span class="sxs-lookup"><span data-stu-id="b3da7-137">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="b3da7-138">가상 컴퓨터의 이름을 만들고 hello Operations Management Suite 에이전트를 설치 hello OMS 작업 영역에서 VM을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da7-138">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |

