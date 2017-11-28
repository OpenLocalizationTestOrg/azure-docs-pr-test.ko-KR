---
title: "Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver aaaTesting | Microsoft Docs"
description: "Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 테스트"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a><span data-ttu-id="d6d86-103">Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 실행</span><span class="sxs-lookup"><span data-stu-id="d6d86-103">Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>
<span data-ttu-id="d6d86-104">이 문서에서는 Microsoft Azure SUSE Linux 가상 컴퓨터 (Vm)에서 SAP NetWeaver를 실행 하는 경우 다양 한 가지 tooconsider를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-104">This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="d6d86-105">2016년 5월 19일을 기준으로 SAP NetWeaver는 Azure의 SUSE Linux VM에서 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-105">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="d6d86-106">Linux 버전, SAP 커널 버전 등과 관련된 모든 세부 정보는 SAP 정보 1928533, "Azure의 SAP 응용 프로그램: 지원 제품 및 Azure VM 유형"에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-106">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>
<span data-ttu-id="d6d86-107">Linux VM의 SAP에 대한 자세한 내용은 [Linux VM(가상 컴퓨터)에서 SAP 사용](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-107">Further documentation about SAP on Linux VMs can be found here : [Using SAP on Linux virtual machines (VMs)](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d6d86-108">다음 정보는 hello 몇 가지 잠재적인 위험을 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-108">hello following information should help you avoid some potential pitfalls.</span></span>

## <a name="suse-images-on-azure-for-running-sap"></a><span data-ttu-id="d6d86-109">SAP 실행을 위한 Azure의 SUSE 이미지</span><span class="sxs-lookup"><span data-stu-id="d6d86-109">SUSE images on Azure for running SAP</span></span>
<span data-ttu-id="d6d86-110">Azure에서 SAP NetWeaver를 실행하기 위해서는 SUSE Linux Enterprise Server SLES 12(SPx)만 사용해야 합니다. 자세한 내용은 SAP 정보 1928533을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-110">For running SAP NetWeaver on Azure, use only SUSE Linux Enterprise Server SLES 12 ( SPx ) - see also SAP note 1928533.</span></span> <span data-ttu-id="d6d86-111">특수 한 SUSE 이미지가 hello Azure 마켓플레이스 ("SLES 11 s p 3 SAP CAL에 대 한"), 이지만이를 사용할 수 없는 일반적인 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-111">A special SUSE image is in hello Azure Marketplace ("SLES 11 SP3 for SAP CAL"), but this is not intended for general usage.</span></span> <span data-ttu-id="d6d86-112">Hello에 대 한 예약 되어 있으므로이 이미지를 사용 하지 마십시오 [SAP 클라우드 어플라이언스에 라이브러리](https://cal.sap.com/) 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-112">Do not use this image because it's reserved for hello [SAP Cloud Appliance Library](https://cal.sap.com/) solution.</span></span>  

<span data-ttu-id="d6d86-113">Azure의 모든 새로운 테스트 및 설치에 대해 Azure Resource Manager를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-113">You should use Azure Resource Manager for all new tests and installations on Azure.</span></span> <span data-ttu-id="d6d86-114">SUSE SLES 이미지 및 버전의 Azure PowerShell 또는 hello Azure CLI (명령줄 인터페이스)를 사용 하 여 hello 다음 명령을 사용 하 여 toolook 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-114">toolook for SUSE SLES images and versions by using Azure PowerShell or hello Azure command-line interface (CLI), use hello following commands.</span></span> <span data-ttu-id="d6d86-115">다음 예를 들어 toodefine hello의에서 OS 이미지는 JSON 템플릿 새 SUSE Linux VM을 배포 하기 위한 hello 출력을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-115">You can then use hello output, for example, toodefine hello OS image in a JSON template for deploying a new SUSE Linux VM.</span></span>
<span data-ttu-id="d6d86-116">PowerShell 명령은 Azure PowerShell 1.0.1 이상 버전에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-116">These PowerShell commands are valid for Azure PowerShell version 1.0.1 and later.</span></span>

<span data-ttu-id="d6d86-117">SAP 설치를 위한 수도 toouse hello 표준 SLES 이미지 있지만 권장 toomake 사용 하 여 사용할 수 있는 SAP 이미지 이제 hello Azure에 이미지 갤러리에 대 한 새 SLES hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-117">While it's still possible toouse hello standard SLES images for SAP installations it's recommended toomake use of hello new SLES for SAP images which are available now on hello Azure image gallery.</span></span> <span data-ttu-id="d6d86-118">이러한 이미지에 대 한 자세한 내용은 hello에 해당 하는에서 확인할 수 있습니다 [Azure 마켓플레이스 페이지]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) 또는 hello [SUSE FAQ 웹 페이지에 대 한 SAP 용 SLES]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ )합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-118">More information about these images can be found on hello corresponding [Azure Marketplace page]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) or hello [SUSE FAQ web page about SLES for SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).</span></span>


* <span data-ttu-id="d6d86-119">SUSE를 포함하는 기존 게시자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-119">Look for existing publishers, including SUSE:</span></span>
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* <span data-ttu-id="d6d86-120">SUSE에서 기존 제품을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-120">Look for existing offerings from SUSE:</span></span>
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* <span data-ttu-id="d6d86-121">SUSE SLES 제품을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-121">Look for SUSE SLES offerings:</span></span>
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* <span data-ttu-id="d6d86-122">특정 버전의 SLES SKU를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-122">Look for a specific version of a SLES SKU:</span></span>
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a><span data-ttu-id="d6d86-123">SUSE VM에 WALinuxAgent 설치</span><span class="sxs-lookup"><span data-stu-id="d6d86-123">Installing WALinuxAgent in a SUSE VM</span></span>
<span data-ttu-id="d6d86-124">hello 에이전트 WALinuxAgent 호출에 hello Azure Marketplace의에서 hello SLES 이미지의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-124">hello agent called WALinuxAgent is part of hello SLES images in hello Azure Marketplace.</span></span> <span data-ttu-id="d6d86-125">수동으로(예: 온-프레미스에서 SLES OS VHD(가상 하드 디스크)를 업로드하는 경우) 설치와 관련된 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-125">For information about installing it manually (for example, when uploading a SLES OS virtual hard disk (VHD) from on-premises), see:</span></span>

* [<span data-ttu-id="d6d86-126">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="d6d86-126">OpenSUSE</span></span>](http://software.opensuse.org/package/WALinuxAgent)
* [<span data-ttu-id="d6d86-127">Azure</span><span class="sxs-lookup"><span data-stu-id="d6d86-127">Azure</span></span>](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d6d86-128">SUSE</span><span class="sxs-lookup"><span data-stu-id="d6d86-128">SUSE</span></span>](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a><span data-ttu-id="d6d86-129">SAP "향상된 모니터링"</span><span class="sxs-lookup"><span data-stu-id="d6d86-129">SAP "enhanced monitoring"</span></span>
<span data-ttu-id="d6d86-130">Azure에서 SAP와 같은 필수 필수 toorun는 SAP "향상 된 모니터링"입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-130">SAP "enhanced monitoring" is a mandatory prerequisite toorun SAP on Azure.</span></span> <span data-ttu-id="d6d86-131">SAP 정보 2191498, “Azure와 Linux의 SAP: 향상된 모니터링”에서 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-131">Please check details in SAP note 2191498 "SAP on Linux with Azure: Enhanced Monitoring".</span></span>

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a><span data-ttu-id="d6d86-132">Azure 데이터 디스크 tooan Azure Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="d6d86-132">Attaching Azure data disks tooan Azure Linux VM</span></span>
<span data-ttu-id="d6d86-133">Hello 장치 id입니다. 사용 하 여 Azure 데이터 디스크 tooan Azure Linux VM을 탑재 하지 해야</span><span class="sxs-lookup"><span data-stu-id="d6d86-133">You should never mount Azure data disks tooan Azure Linux VM by using hello device ID.</span></span> <span data-ttu-id="d6d86-134">Hello 범용 고유 식별자 (UUID) 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-134">Instead, use hello universally unique identifier (UUID).</span></span> <span data-ttu-id="d6d86-135">예를 들어 그래픽 도구 toomount Azure 데이터 디스크를 사용 하는 경우 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-135">Be careful when you use graphical tools toomount Azure data disks, for example.</span></span> <span data-ttu-id="d6d86-136">Hello 항목 /etc/fstab에 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d6d86-136">Double-check hello entries in /etc/fstab.</span></span>

<span data-ttu-id="d6d86-137">hello 수 있는 문제 hello 장치 ID는 변경 될 수 있으므로 및 다음 hello Azure VM의 hello 부팅 프로세스에 중지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-137">hello issue with hello device ID is that it might change, and then hello Azure VM might hang in hello boot process.</span></span> <span data-ttu-id="d6d86-138">toomitigate hello 문제 /etc/fstab에 hello nofail 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-138">toomitigate hello issue, you could add hello nofail parameter in /etc/fstab.</span></span> <span data-ttu-id="d6d86-139">그러나 때문일 nofail 신중 하 게 응용 프로그램으로 hello 탑재 지점 이전에 사용할 수 있습니다 및 외부 Azure 데이터 디스크는 hello 부팅 하는 동안 탑재 되지 않은 경우 hello 루트 파일 시스템에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-139">But, be careful with nofail because applications might use hello mount point as before, and might write into hello root file system in case an external Azure data disk wasn't mounted during hello boot.</span></span>

<span data-ttu-id="d6d86-140">hello 유일한 예외 toomounting UUID 통해이 hello 다음 섹션에에서 설명 된 대로 문제 해결을 위해 OS 디스크는 연결 됨.</span><span class="sxs-lookup"><span data-stu-id="d6d86-140">hello only exception toomounting via UUID is attaching an OS disk for troubleshooting purposes, as described in hello following section.</span></span>

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a><span data-ttu-id="d6d86-141">더 이상 액세스할 수 없는 SUSE VM 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d6d86-141">Troubleshooting a SUSE VM that isn't accessible anymore</span></span>
<span data-ttu-id="d6d86-142">Azure에서 SUSE VM hello 부팅 프로세스에서 (예를 들어 디스크 탑재와 관련 된 오류)와 함께 중단 하는 위치 하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-142">There might be situations where a SUSE VM on Azure hangs in hello boot process (for example, with an error related to mounting disks).</span></span> <span data-ttu-id="d6d86-143">Hello Azure 포털에서에서 Azure 가상 컴퓨터 v 2에 대 한 hello 부트 진단 기능을 사용 하 여이 문제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-143">You can verify this issue by using hello boot diagnostics feature for Azure Virtual Machines v2 in hello Azure portal.</span></span> <span data-ttu-id="d6d86-144">자세한 내용은 [부팅 진단](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-144">For more information, see [Boot diagnostics](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>

<span data-ttu-id="d6d86-145">한 가지 방법은 toosolve hello 문제 hello에서 tooattach hello OS 디스크 손상 VM tooanother Azure에서 VM SUSE입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-145">One way toosolve hello problem is tooattach hello OS disk from hello damaged VM tooanother SUSE VM on Azure.</span></span> <span data-ttu-id="d6d86-146">그런 다음 적절 하 게 변경 /etc/fstab 편집 또는 네트워크 udev 규칙 제거와 같은 hello 다음 섹션에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-146">Then make appropriate changes like editing /etc/fstab or removing network udev rules, as described in hello next section.</span></span>

<span data-ttu-id="d6d86-147">중요 한 사항은 tooconsider 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-147">There is one important thing tooconsider.</span></span> <span data-ttu-id="d6d86-148">OS hello 동일한 Azure 마켓플레이스 이미지 (예를 들어 SLES 11 SP4)로 인해 hello에서 몇 가지 SUSE Vm 배포 디스크 tooalways hello에서 탑재할 수 같은 UUID입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-148">Deploying several SUSE VMs from hello same Azure Marketplace image (for example, SLES 11 SP4) causes hello OS disk tooalways be mounted by hello same UUID.</span></span> <span data-ttu-id="d6d86-149">따라서 hello UUID tooattach 서로 다른 두 개의 동일한 Uuid 동일한 Azure 마켓플레이스 이미지 될 hello를 사용 하 여 배포 된 VM에서 OS 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-149">Therefore, using hello UUID tooattach an OS disk from a different VM that was deployed by using hello same Azure Marketplace image will result in two identical UUIDs.</span></span> <span data-ttu-id="d6d86-150">문제가 발생 하 고 연결 된 hello에서 문제 해결에 VM hello가 부팅 실제로 손상 된 운영 체제 디스크 대신 원래 hello 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-150">This causes problems and could mean that hello VM meant for troubleshooting will in fact boot from hello attached and damaged OS disk instead of hello original one.</span></span>

<span data-ttu-id="d6d86-151">두 가지 방법으로 tooavoid이</span><span class="sxs-lookup"><span data-stu-id="d6d86-151">There are two ways tooavoid this:</span></span>

* <span data-ttu-id="d6d86-152">예를 들어 SLES 11 SPx SLES 12가 아닌 VM 문제를 해결 하는 hello에 대 한 다른 Azure 마켓플레이스 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-152">Use a different Azure Marketplace image for hello troubleshooting VM (for example, SLES 11 SPx instead of SLES 12 ).</span></span>
* <span data-ttu-id="d6d86-153">손상 된 hello OS 디스크 UUID-사용을 사용 하 여 다른 VM 연결 안 함 다른 값인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-153">Don't attach hello damaged OS disk from another VM by using UUID--use something else.</span></span>

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a><span data-ttu-id="d6d86-154">온-프레미스 tooAzure에서 SUSE VM을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-154">Uploading a SUSE VM from on-premises tooAzure</span></span>
<span data-ttu-id="d6d86-155">Hello 단계 tooupload에서 온-프레미스 tooAzure SUSE VM에 대 한 참조 [SLES 또는 openSUSE 가상 컴퓨터를 Azure에 대 한 준비](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-155">For a description of hello steps tooupload a SUSE VM from on-premises tooAzure, see [Prepare a SLES or openSUSE virtual machine for Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d6d86-156">Hello 프로 비전 해제 하지 않고 VM 단계 (예를 들어 기존 SAP 설치를 tookeep으로 hello 호스트 이름) hello 끝 tooupload 원한다 면 hello 다음 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-156">If you want tooupload a VM without hello deprovision step at hello end (for example, tookeep an existing SAP installation, as well as hello host name), check hello following items:</span></span>

* <span data-ttu-id="d6d86-157">해당 하는 hello OS 디스크 UUID 및 하지 hello 장치 ID를 사용 하 여 탑재 되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="d6d86-157">Make sure that hello OS disk is mounted by using UUID and not hello device ID.</span></span> <span data-ttu-id="d6d86-158">TooUUID /etc/fstab에만 있는 변경 하는 hello OS 디스크에 대해 충분입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-158">Changing tooUUID just in /etc/fstab is not enough for hello OS disk.</span></span> <span data-ttu-id="d6d86-159">또한 /boot/grub/menu.lst을 편집 하 여 또는 YaST 통해 tooadapt hello 부트 로더를 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d6d86-159">Also, don't forget tooadapt hello boot loader through YaST or by editing /boot/grub/menu.lst.</span></span>
* <span data-ttu-id="d6d86-160">Hello SUSE OS 디스크에 대 한 hello VHDX 형식을 사용 하 고 tooVHD tooAzure 업로드 하기 위한 변환 하는 경우에 일반적으로 해당 hello 네트워크 장치 eth0 tooeth1에서 변경 됩니다. 집니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-160">If you use hello VHDX format for hello SUSE OS disk and convert it tooVHD for uploading tooAzure, it's very likely that hello network device will change from eth0 tooeth1.</span></span> <span data-ttu-id="d6d86-161">이상 버전에서는 Azure에서 부팅 하는 경우 tooavoid 문제에 설명 된 대로 백 tooeth0 변경 [SLES 11 VMware 복제에서 eth0 수정](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-161">tooavoid issues when you're booting on Azure later, change back tooeth0 as described in [Fixing eth0 in cloned SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).</span></span>

<span data-ttu-id="d6d86-162">Toowhat의 hello 문서에서 설명 하는 또한,이 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-162">In addition toowhat's described in hello article, we recommend that you remove this:</span></span>

   <span data-ttu-id="d6d86-163">/lib/udev/rules.d/75-persistent-net-generator.rules</span><span class="sxs-lookup"><span data-stu-id="d6d86-163">/lib/udev/rules.d/75-persistent-net-generator.rules</span></span>

<span data-ttu-id="d6d86-164">또한 여러 nic를 지원 하지 않습니다.으로 잠재적인 문제를 방지 하는 hello Azure Linux 에이전트 (waagent) toohelp를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-164">You can also install hello Azure Linux Agent (waagent) toohelp you avoid potential issues, as long as there are not multiple NICs.</span></span>

## <a name="deploying-a-suse-vm-on-azure"></a><span data-ttu-id="d6d86-165">Azure에 SUSE VM 배포</span><span class="sxs-lookup"><span data-stu-id="d6d86-165">Deploying a SUSE VM on Azure</span></span>
<span data-ttu-id="d6d86-166">Hello 새 Azure 리소스 관리자 모델 JSON 템플릿 파일을 사용 하 여 새 SUSE Vm을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-166">You should create new SUSE VMs by using JSON template files in hello new Azure Resource Manager model.</span></span> <span data-ttu-id="d6d86-167">Hello JSON 템플릿 파일을 만든 후에 다음 CLI 명령을 대체 tooPowerShell으로 hello를 사용 하 여 hello VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-167">After hello JSON template file is created, you can deploy hello VM by using hello following CLI command as an alternative tooPowerShell:</span></span>

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
<span data-ttu-id="d6d86-168">JSON 템플릿 파일에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../../../resource-group-authoring-templates.md) 및 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-168">For more details about JSON template files, see [Authoring Azure Resource Manager templates](../../../resource-group-authoring-templates.md) and [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span>

<span data-ttu-id="d6d86-169">CLI 및 Azure 리소스 관리자에 대 한 자세한 내용은 참조 하십시오. [사용 하 여 hello Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI](../../../xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-169">For more details about CLI and Azure Resource Manager, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../../../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="sap-license-and-hardware-key"></a><span data-ttu-id="d6d86-170">SAP 라이선스 및 하드웨어 키</span><span class="sxs-lookup"><span data-stu-id="d6d86-170">SAP license and hardware key</span></span>
<span data-ttu-id="d6d86-171">Hello 공식 SAP Azure 인증에 대 한 새로운 메커니즘에 도입 된 toocalculate hello SAP 하드웨어 키 hello SAP 라이선스에 사용 되는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-171">For hello official SAP-Azure certification, a new mechanism was introduced toocalculate hello SAP hardware key that's used for hello SAP license.</span></span> <span data-ttu-id="d6d86-172">hello SAP 커널이 조정 toobe toomake 사용을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-172">hello SAP kernel had toobe adapted toomake use of this.</span></span> <span data-ttu-id="d6d86-173">이전 Linux용 SAP 커널 버전에는 이 코드 변경이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-173">Former SAP kernel versions for Linux did not include this code change.</span></span> <span data-ttu-id="d6d86-174">따라서 특정 한 상황에서에서 (예를 들어 Azure VM 크기를 조정), hello SAP 하드웨어 키 변경 및 hello SAP 라이선스를 더 이상 유효 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-174">Therefore, in certain situations (for example, Azure VM resizing), hello SAP hardware key changed and hello SAP license was no longer be valid.</span></span> <span data-ttu-id="d6d86-175">이 hello 최신 SAP Linux 커널을에서 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-175">This is solved in hello latest SAP Linux kernels.</span></span> <span data-ttu-id="d6d86-176">자세한 내용은 SAP 참고 1928533을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-176">For details please check SAP note 1928533.</span></span>

## <a name="suse-sapconf-package--tuned-adm"></a><span data-ttu-id="d6d86-177">SUSE sapconf 패키지 / tuned-adm</span><span class="sxs-lookup"><span data-stu-id="d6d86-177">SUSE sapconf package / tuned-adm</span></span>
<span data-ttu-id="d6d86-178">SUSE는 일련의 SAP 관련 설정을 관리하는 "sapconf"라는 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-178">SUSE provides a package called "sapconf" that manages a set of SAP-specific settings.</span></span> <span data-ttu-id="d6d86-179">이 패키지의 종류에 대 한 자세한 내용은 않습니다, 방식과 tooinstall를 사용 하 여 참조 하십시오 [SUSE Linux Enterprise Server toorun SAP 시스템 sapconf tooprepare를 사용 하 여](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) 및 [sapconf 란 방식이 나 tooprepare SUSE Linux Enterprise SAP 시스템을 실행 하기 위한 서버? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).</span><span class="sxs-lookup"><span data-stu-id="d6d86-179">For more details about what this package does, and how tooinstall and use it, see [Using sapconf tooprepare a SUSE Linux Enterprise Server toorun SAP systems](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) and [What is sapconf or how tooprepare a SUSE Linux Enterprise Server for running SAP systems?](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).</span></span>

<span data-ttu-id="d6d86-180">Hello 그 동안 있어서 sapconf-.adm 조정으로 대체 하는 새로운 도구</span><span class="sxs-lookup"><span data-stu-id="d6d86-180">In hello meantime there is a new tool which replaces sapconf - tuned-adm.</span></span> <span data-ttu-id="d6d86-181">아래 두 개의 링크가 hello 다음이 도구에 대 한 자세한 내용은 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-181">One can find more details about this tool following hello two links below.</span></span>

<span data-ttu-id="d6d86-182">tuned-adm 프로필 sap-hana에 대한 SLES 설명서는 [여기](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html)</span><span class="sxs-lookup"><span data-stu-id="d6d86-182">SLES documentation about tuned-adm profile sap-hana can be found [here](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html)</span></span> 

<span data-ttu-id="d6d86-183">tuned-adm을 사용하여 SAP 워크로드를 위한 시스템 튜닝은 6.2장의 [여기](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) 에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-183">Tuning Systems for SAP Workloads with tuned-adm - can be found [here](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) in chapter 6.2</span></span>

## <a name="nfs-share-in-distributed-sap-installations"></a><span data-ttu-id="d6d86-184">분산된 SAP 설치에서 NFS 공유</span><span class="sxs-lookup"><span data-stu-id="d6d86-184">NFS share in distributed SAP installations</span></span>
<span data-ttu-id="d6d86-185">분산된 설치-하는 경우 예를 들어 여기서 tooinstall hello 데이터베이스를 별도 Vm의 경우-SAP 응용 프로그램 서버 hello 공유할 수 있습니다 hello /sapmnt 디렉터리를 통해 네트워크 파일 시스템 (NFS).</span><span class="sxs-lookup"><span data-stu-id="d6d86-185">If you have a distributed installation--for example, where you want tooinstall hello database and hello SAP application servers in separate VMs--you can share hello /sapmnt directory via Network File System (NFS).</span></span> <span data-ttu-id="d6d86-186">Hello /sapmnt에 대 한 NFS 공유를 만든 후 hello 설치 단계에 문제가 있으면 "no_root_squash" hello 공유에 대해 설정 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-186">If you have problems with hello installation steps after you create hello NFS share for /sapmnt, check toosee if "no_root_squash" is set for hello share.</span></span>

## <a name="logical-volumes"></a><span data-ttu-id="d6d86-187">논리 볼륨</span><span class="sxs-lookup"><span data-stu-id="d6d86-187">Logical volumes</span></span>
<span data-ttu-id="d6d86-188">지난 hello (예: hello SAP 데이터베이스), 여러 Azure 데이터 디스크에 걸쳐 큰 논리 볼륨입니다. 필요에 따라 하나 것 것이 권장 되었습니다 toouse mdadm lvm Azure에서 아직 유효성 완벽 하 게 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-188">In hello past if one needed a large logical volume across multiple Azure data disks (for example, for hello SAP database), it was recommended toouse mdadm as lvm wasn't fully validated yet on Azure.</span></span> <span data-ttu-id="d6d86-189">mdadm를 사용 하 여 Azure에서 Linux RAID을 tooset 참조 toolearn [소프트웨어 linux RAID 구성](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-189">toolearn how tooset up Linux RAID on Azure by using mdadm, see [Configure software RAID on Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d6d86-190">Hello 2016 년 5 월의 시작 부분을 기준으로 그 동안에 lvm는 Azure에서 완전히 지원 및 대체 toomdadm으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-190">In hello meantime as of beginning of May 2016 also lvm is fully supported on Azure and can be used as an alternative toomdadm.</span></span> <span data-ttu-id="d6d86-191">Azure의 lvm에 대한 자세한 내용은 [Azure에서 Linux VM에 LVM 구성](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d86-191">For additional information regarding lvm on Azure see [Configure LVM on a Linux VM in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-suse-repository"></a><span data-ttu-id="d6d86-192">Azure SUSE 리포지토리</span><span class="sxs-lookup"><span data-stu-id="d6d86-192">Azure SUSE repository</span></span>
<span data-ttu-id="d6d86-193">간단한 명령 tooreset 액세스 toohello 표준 SUSE Azure 저장소에 문제가 있는 경우 사용할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-193">If you have an issue with access toohello standard Azure SUSE repository, you can use a simple command tooreset it.</span></span> <span data-ttu-id="d6d86-194">Azure 지역 및 다음 복사 hello 이미지 tooa 다른 지역의 toodeploy 원하는 개인 OS 이미지를 만드는 경우 이러한 현상이 발생할 수 있습니다이 개인 OS 이미지를 기반으로 하는 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-194">This might happen if you create a private OS image in an Azure region and then copy hello image tooa different region where you want toodeploy new VMs that are based on this private OS image.</span></span> <span data-ttu-id="d6d86-195">다음 명령을 hello VM 내 hello를 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-195">Just run hello following command inside hello VM:</span></span>

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a><span data-ttu-id="d6d86-196">Gnome 데스크톱</span><span class="sxs-lookup"><span data-stu-id="d6d86-196">Gnome desktop</span></span>
<span data-ttu-id="d6d86-197">Toouse hello Gnome 데스크톱 tooinstall-SAP GUI를 포함 하 여 단일 VM 내 전체 SAP 데모 시스템 브라우저 및 SAP 관리 콘솔--사용이 힌트 tooinstall hello Azure SLES 이미지에:</span><span class="sxs-lookup"><span data-stu-id="d6d86-197">If you want toouse hello Gnome desktop tooinstall a complete SAP demo system inside a single VM--including a SAP GUI, browser, and SAP management console--use this hint tooinstall it on hello Azure SLES images:</span></span>

   <span data-ttu-id="d6d86-198">SLES 11의 경우:</span><span class="sxs-lookup"><span data-stu-id="d6d86-198">For SLES 11:</span></span>

   ```
   zypper in -t pattern gnome
   ```

   <span data-ttu-id="d6d86-199">SLES 12의 경우:</span><span class="sxs-lookup"><span data-stu-id="d6d86-199">For SLES 12:</span></span>

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a><span data-ttu-id="d6d86-200">Oracle linux hello 클라우드에서 대 한 SAP 지원</span><span class="sxs-lookup"><span data-stu-id="d6d86-200">SAP support for Oracle on Linux in hello cloud</span></span>
<span data-ttu-id="d6d86-201">가상화된 환경에서 Linux의 Oracle을 지원하는 것에 관한 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-201">There is a support restriction from Oracle on Linux in virtualized environments.</span></span> <span data-ttu-id="d6d86-202">이것이 Azure 관련 항목 이지만 toounderstand 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-202">Although this is not an Azure-specific topic, it's important toounderstand.</span></span> <span data-ttu-id="d6d86-203">SAP은 Azure와 같은 공용 클라우드에 있는 SUSE 또는 Red Hat에서 Oracle을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-203">SAP does not support Oracle on SUSE or Red Hat in a public cloud like Azure.</span></span> <span data-ttu-id="d6d86-204">toodiscuss이이 항목에서는 Oracle에 직접 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d86-204">toodiscuss this topic, contact Oracle directly.</span></span>

