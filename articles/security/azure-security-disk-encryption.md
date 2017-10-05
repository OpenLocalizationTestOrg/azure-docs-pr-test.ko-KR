---
title: "Windows 및 Linux IaaS VM용 Azure Disk Encryption | Microsoft Docs"
description: "이 문서에서는 Windows 및 Linux IaaS VM용 Microsoft Azure Disk Encryption에 대한 개요를 제공합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="c3a3d-103">Windows 및 Linux IaaS VM용 Azure 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="c3a3d-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="c3a3d-104">Microsoft Azure는 데이터 프라이버시, 데이터 독립성을 보장하기 위해 노력하고 있으며 암호화 키를 암호화, 제어 및 관리하고 데이터 액세스를 제어 및 감사하는 광범위한 고급 기술을 통해 Azure 호스팅 데이터를 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="c3a3d-105">또한 Azure 고객에게 비즈니스 요구에 가장 잘 맞는 솔루션을 선택할 수 있는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="c3a3d-106">이 문서에는 "Windows 및 Linux IaaS VM용 Azure 디스크 암호화"라는 새로운 기술 솔루션을 소개하여 조직의 보안 및 규정 준수 약정에 따라 데이터를 보호하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="c3a3d-107">이 문서에서는 지원되는 시나리오와 사용자 환경을 비롯하여 Azure 디스크 암호화 기능을 사용하는 방법에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-108">특정 권장 사항으로 인해 데이터, 네트워크 또는 계산 리소스 사용량이 증가할 수 있으며 이로 인해 라이선스 또는 구독 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="c3a3d-109">개요</span><span class="sxs-lookup"><span data-stu-id="c3a3d-109">Overview</span></span>
<span data-ttu-id="c3a3d-110">Azure Disk Encryption은 Windows 및 Linux IaaS 가상 컴퓨터 디스크를 암호화할 수 있도록 하는 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="c3a3d-111">Azure Disk Encryption은 업계 표준인 Windows의 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 기능과 Linux의 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 기능을 활용하여 OS 및 데이터 디스크를 위한 볼륨 암호화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="c3a3d-112">또한 고객이 Key Vault 구독에서 디스크 암호화 키 및 암호를 관리 및 제어할 수 있도록 [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/)에 통합되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="c3a3d-113">이 솔루션은 가상 컴퓨터 디스크에 있는 모든 데이터가 미사용 시 Azure Storage에 암호화되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="c3a3d-114">Windows 및 Linux IaaS VM용 Azure Disk Encryption은 이제 Standard VM 및 Premium Storage를 사용하는 VM을 위한 모든 Azure 공용 지역 및 AzureGov 지역에서 **일반 공급**으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="c3a3d-115">암호화 시나리오</span><span class="sxs-lookup"><span data-stu-id="c3a3d-115">Encryption scenarios</span></span>
<span data-ttu-id="c3a3d-116">Azure 디스크 암호화 솔루션은 다음의 고객 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="c3a3d-117">미리 암호화된 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="c3a3d-118">지원되는 Azure 갤러리 이미지에서 만든 새 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="c3a3d-119">Azure에서 실행 중인 기존 IaaS VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="c3a3d-120">Windows IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="c3a3d-121">Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="c3a3d-122">관리 디스크 VM의 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="c3a3d-123">기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3a3d-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c3a3d-124">키 암호화 키를 사용하여 암호화된 VM의 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="c3a3d-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="c3a3d-125">이 솔루션은 Microsoft Azure에서 사용되도록 설정될 경우 IaaS VM에 대해 다음 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="c3a3d-126">Azure Key Vault와 통합</span><span class="sxs-lookup"><span data-stu-id="c3a3d-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="c3a3d-127">표준 계층 VM: [A, D, DS, G, GS, F 등 시리즈 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="c3a3d-128">지원되는 Azure 갤러리 이미지의 Windows 및 Linux IaaS VM과 관리 디스크 VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="c3a3d-129">Windows IaaS VM 및 관리 디스크 VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c3a3d-130">Linux IaaS VM 및 관리 디스크 VM에 대한 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c3a3d-131">Windows 클라이언트 OS를 실행하는 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="c3a3d-132">탑재 경로가 있는 볼륨에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="c3a3d-133">mdadm을 사용하여 디스크 스트라이프(RAID)로 구성된 Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="c3a3d-134">데이터 디스크에 대해 LVM을 사용하여 Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="c3a3d-135">Storage 공간으로 구성된 Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="c3a3d-136">기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3a3d-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c3a3d-137">모든 Azure 공용 지역 및 AzureGov 지역 지원됨</span><span class="sxs-lookup"><span data-stu-id="c3a3d-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="c3a3d-138">이 솔루션은 다음 시나리오, 기능 및 기술을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="c3a3d-139">기본 계층 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="c3a3d-140">Linux IaaS VM에 대한 OS 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="c3a3d-141">OS 드라이브가 Linux Iaas VM에 대해 암호화되는 경우 데이터 드라이브에 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="c3a3d-142">클래식 VM 만들기 방법을 사용하여 만든 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="c3a3d-143">Windows 및 Linux IaaS VM 고객 사용자 지정 이미지에 암호화를 사용하는 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="c3a3d-144">Linux LVM OS 디스크에 암호화를 사용하는 기능은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="c3a3d-145">이 지원은 곧 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-145">This support will come soon.</span></span>
* <span data-ttu-id="c3a3d-146">온-프레미스 키 관리 서비스와의 통합</span><span class="sxs-lookup"><span data-stu-id="c3a3d-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="c3a3d-147">Azure 파일(공유 파일 시스템), NFS(네트워크 파일 시스템), 동적 볼륨, 소프트웨어 기반 RAID 시스템으로 구성된 Windows VM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="c3a3d-148">키 암호화 키를 사용하지 않고 암호화된 VM의 백업 및 복원입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="c3a3d-149">기존의 암호화된 Premium Storage VM의 암호화 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-150">암호화된 VM의 백업 및 복원은 KEK 구성으로 암호화된 VM에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c3a3d-151">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c3a3d-152">KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="c3a3d-153">곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-153">This support is coming soon.</span></span>
> <span data-ttu-id="c3a3d-154">기존의 암호화된 Premium Storage VM의 암호화 설정 업데이트는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="c3a3d-155">곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="c3a3d-156">암호화 기능</span><span class="sxs-lookup"><span data-stu-id="c3a3d-156">Encryption features</span></span>
<span data-ttu-id="c3a3d-157">Azure IaaS VM에 대한 Azure Disk Encryption을 사용하도록 설정하고 배포할 때 제공된 구성에 따라 다음 기능이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="c3a3d-158">사용자 저장소에서 미사용 부팅 볼륨을 보호하기 위해 OS 볼륨 암호화</span><span class="sxs-lookup"><span data-stu-id="c3a3d-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="c3a3d-159">사용자 저장소에서 미사용 데이터 볼륨을 보호하기 위해 데이터 볼륨 암호화</span><span class="sxs-lookup"><span data-stu-id="c3a3d-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="c3a3d-160">Windows IaaS VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="c3a3d-161">Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함(OS 드라이브가 암호화되지 않는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="c3a3d-162">사용자의 Key Vault 구독에서 암호화 키 및 비밀 보호</span><span class="sxs-lookup"><span data-stu-id="c3a3d-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="c3a3d-163">암호화된 IaaS VM의 암호화 상태 보고</span><span class="sxs-lookup"><span data-stu-id="c3a3d-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="c3a3d-164">IaaS 가상 컴퓨터에서 디스크 암호화 구성 설정 제거</span><span class="sxs-lookup"><span data-stu-id="c3a3d-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="c3a3d-165">Azure Backup 서비스로 암호화된 VM 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="c3a3d-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-166">암호화된 VM의 백업 및 복원은 KEK 구성으로 암호화된 VM에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c3a3d-167">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c3a3d-168">KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="c3a3d-169">Windows 및 Linux 솔루션용 IaaS VM에 대한 Azure Disk Encryption에는 다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="c3a3d-170">Windows용 디스크 암호화 확장</span><span class="sxs-lookup"><span data-stu-id="c3a3d-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="c3a3d-171">Linux용 디스크 암호화 확장</span><span class="sxs-lookup"><span data-stu-id="c3a3d-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="c3a3d-172">디스크 암호화 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="c3a3d-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="c3a3d-173">디스크 암호화 Azure CLI(명령줄 인터페이스) cmdlet</span><span class="sxs-lookup"><span data-stu-id="c3a3d-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="c3a3d-174">디스크 암호화 Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c3a3d-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="c3a3d-175">Azure Disk Encryption은 Windows 또는 Linux OS를 실행하는 IaaS VM에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="c3a3d-176">지원되는 운영 체제에 대한 자세한 내용은 "필수 조건" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-177">Azure Disk Encryption으로 VM 디스크를 암호화하는 작업에 대한 추가 요금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="c3a3d-178">가치 제안</span><span class="sxs-lookup"><span data-stu-id="c3a3d-178">Value proposition</span></span>
<span data-ttu-id="c3a3d-179">Azure Disk Encryption 관리 솔루션을 적용할 때 다음 비즈니스 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="c3a3d-180">업계 표준 암호화 기술을 사용하여 조직의 보안 및 규정 준수 요구 사항을 충족할 수 있으므로 미사용 상태에서 IaaS VM이 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="c3a3d-181">IaaS VM은 고객이 제어하는 키 및 정책에 따라 부팅되며 Key Vault에서 이러한 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="c3a3d-182">암호화 워크플로</span><span class="sxs-lookup"><span data-stu-id="c3a3d-182">Encryption workflow</span></span>
<span data-ttu-id="c3a3d-183">Windows 및 Linux VM용 디스크 암호화를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="c3a3d-184">위의 암호화 시나리오 중에서 암호화 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="c3a3d-185">고객은 Azure Disk Encryption Resource Manager 템플릿, PowerShell cmdlet 또는 CLI 명령을 통해 디스크 암호화를 사용하도록 선택하고 암호화 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="c3a3d-186">고객 암호화 VHD 시나리오의 경우, 암호화된 VHD를 저장소 계정에, 암호화 키 자료를 Key Vault에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="c3a3d-187">그런 다음 암호화 구성을 제공하여 새로운 IaaS VM에서 암호화를 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="c3a3d-188">Marketplace에서 만든 새 VM과 Azure에서 이미 실행 중인 기존의 VM에 대해 암호화 구성을 제공하여 IaaS VM에서 암호화를 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="c3a3d-189">Azure 플랫폼에 대한 액세스를 부여하여 Key Vault에서 암호화 키 자료(Windows 시스템의 경우 BitLocker 암호화 키, Linux의 경우 Passphrase)를 읽고 IaaS VM에서 암호화를 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="c3a3d-190">암호화 키 자료를 Key Vault에 기록하기 위한 Azure Active Directory(Azure AD) 응용 프로그램 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="c3a3d-191">이렇게 하면 2단계에서 설명된 시나리오인 경우 IaaS VM에서 암호화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="c3a3d-192">Azure에서는 암호화 및 Key Vault 구성으로 VM 서비스 모델을 업데이트하고 암호화된 VM을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="c3a3d-194">암호 해독 워크플로</span><span class="sxs-lookup"><span data-stu-id="c3a3d-194">Decryption workflow</span></span>
<span data-ttu-id="c3a3d-195">IaaS VM용 디스크 암호화를 사용하지 않도록 설정하려면 다음 대략적인 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="c3a3d-196">Azure Disk Encryption Resource Manager 템플릿 또는 PowerShell cmdlet을 통해 Azure에서 실행 중인 IaaS VM에 암호화(암호 해독)를 사용하지 않도록 선택하고 암호 해독 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="c3a3d-197">이 단계는 실행 중인 Windows IaaS VM에서 OS 또는 데이터 볼륨이나 둘 모두의 암호화를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="c3a3d-198">그러나 이전 섹션에 나와 있는 것처럼 Linux에 대해 OS 디스크를 사용하지 않도록 설정하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c3a3d-199">암호 해독 단계는 OS 디스크가 암호화되지 않는 한 Linux VM의 데이터 드라이브에만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="c3a3d-200">Azure에서는 VM 서비스 모델을 업데이트하고 IaaS VM은 암호가 해독되었다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c3a3d-201">VM의 콘텐츠는 더 이상 미사용 상태에서 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-202">암호화 사용 안 함 작업은 Key Vault 및 암호화 키 자료(Windows 시스템의 경우 BitLocker 암호화 키, Linux의 경우 Passphrase)를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="c3a3d-203">Linux OS 디스크 암호화는 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c3a3d-204">암호 해독 단계는 Linux VM에서 데이터 드라이브에만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="c3a3d-205">OS 드라이브가 암호화되는 경우 Linux에 데이터 디스크 암호화를 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3a3d-206">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3a3d-206">Prerequisites</span></span>
<span data-ttu-id="c3a3d-207">"개요" 섹션에 설명된 지원되는 시나리오에 대해 Azure IaaS VM에서 Azure Disk Encryption를 사용하도록 설정하기 전에 다음 필수 조건을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="c3a3d-208">사용자는 유효한 활성 Azure 구독을 포함하여 지원되는 지역에서 Azure에 리소스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="c3a3d-209">Azure Disk Encryption은 다음 Windows Server 버전: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="c3a3d-210">Azure Disk Encryption은 다음 Windows 클라이언트 버전: Windows 8 클라이언트 및 Windows 10 클라이언트에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-211">Windows Server 2008 R2의 경우 Azure에서 암호화를 사용하도록 설정하기 전에 .NET Framework 4.5를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="c3a3d-212">선택적 업데이트인 Windows Server 2008 R2 x64 기반 시스템용 Microsoft .NET Framework 4.5.2([KB2901983](https://support.microsoft.com/kb/2901983))를 설치하여 Windows 업데이트에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="c3a3d-213">Azure Disk Encryption은 다음과 같은 Azure 갤러리 기반 Linux 서버 배포판 및 버전에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="c3a3d-214">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="c3a3d-214">Linux Distribution</span></span> | <span data-ttu-id="c3a3d-215">버전</span><span class="sxs-lookup"><span data-stu-id="c3a3d-215">Version</span></span> | <span data-ttu-id="c3a3d-216">암호화에 지원되는 볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="c3a3d-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="c3a3d-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3a3d-217">Ubuntu</span></span> | <span data-ttu-id="c3a3d-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="c3a3d-219">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-219">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3a3d-220">Ubuntu</span></span> | <span data-ttu-id="c3a3d-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="c3a3d-222">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-222">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3a3d-223">Ubuntu</span></span> | <span data-ttu-id="c3a3d-224">12.10</span><span class="sxs-lookup"><span data-stu-id="c3a3d-224">12.10</span></span> | <span data-ttu-id="c3a3d-225">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-225">Data disk</span></span> |
| <span data-ttu-id="c3a3d-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3a3d-226">Ubuntu</span></span> | <span data-ttu-id="c3a3d-227">12.04</span><span class="sxs-lookup"><span data-stu-id="c3a3d-227">12.04</span></span> | <span data-ttu-id="c3a3d-228">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-228">Data disk</span></span> |
| <span data-ttu-id="c3a3d-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-229">RHEL</span></span> | <span data-ttu-id="c3a3d-230">7.3</span><span class="sxs-lookup"><span data-stu-id="c3a3d-230">7.3</span></span> | <span data-ttu-id="c3a3d-231">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-231">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-232">RHEL</span></span> | <span data-ttu-id="c3a3d-233">7.2</span><span class="sxs-lookup"><span data-stu-id="c3a3d-233">7.2</span></span> | <span data-ttu-id="c3a3d-234">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-234">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-235">RHEL</span></span> | <span data-ttu-id="c3a3d-236">6.8</span><span class="sxs-lookup"><span data-stu-id="c3a3d-236">6.8</span></span> | <span data-ttu-id="c3a3d-237">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-237">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-238">RHEL</span></span> | <span data-ttu-id="c3a3d-239">6.7</span><span class="sxs-lookup"><span data-stu-id="c3a3d-239">6.7</span></span> | <span data-ttu-id="c3a3d-240">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-240">Data disk</span></span> |
| <span data-ttu-id="c3a3d-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-241">CentOS</span></span> | <span data-ttu-id="c3a3d-242">7.3</span><span class="sxs-lookup"><span data-stu-id="c3a3d-242">7.3</span></span> | <span data-ttu-id="c3a3d-243">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-243">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-244">CentOS</span></span> | <span data-ttu-id="c3a3d-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="c3a3d-245">7.2n</span></span> | <span data-ttu-id="c3a3d-246">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-246">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-247">CentOS</span></span> | <span data-ttu-id="c3a3d-248">6.8</span><span class="sxs-lookup"><span data-stu-id="c3a3d-248">6.8</span></span> | <span data-ttu-id="c3a3d-249">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="c3a3d-249">OS and Data disk</span></span> |
| <span data-ttu-id="c3a3d-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-250">CentOS</span></span> | <span data-ttu-id="c3a3d-251">7.1</span><span class="sxs-lookup"><span data-stu-id="c3a3d-251">7.1</span></span> | <span data-ttu-id="c3a3d-252">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-252">Data disk</span></span> |
| <span data-ttu-id="c3a3d-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-253">CentOS</span></span> | <span data-ttu-id="c3a3d-254">7.0</span><span class="sxs-lookup"><span data-stu-id="c3a3d-254">7.0</span></span> | <span data-ttu-id="c3a3d-255">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-255">Data disk</span></span> |
| <span data-ttu-id="c3a3d-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-256">CentOS</span></span> | <span data-ttu-id="c3a3d-257">6.7</span><span class="sxs-lookup"><span data-stu-id="c3a3d-257">6.7</span></span> | <span data-ttu-id="c3a3d-258">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-258">Data disk</span></span> |
| <span data-ttu-id="c3a3d-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-259">CentOS</span></span> | <span data-ttu-id="c3a3d-260">6.6</span><span class="sxs-lookup"><span data-stu-id="c3a3d-260">6.6</span></span> | <span data-ttu-id="c3a3d-261">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-261">Data disk</span></span> |
| <span data-ttu-id="c3a3d-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="c3a3d-262">CentOS</span></span> | <span data-ttu-id="c3a3d-263">6.5</span><span class="sxs-lookup"><span data-stu-id="c3a3d-263">6.5</span></span> | <span data-ttu-id="c3a3d-264">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-264">Data disk</span></span> |
| <span data-ttu-id="c3a3d-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c3a3d-265">openSUSE</span></span> | <span data-ttu-id="c3a3d-266">13.2</span><span class="sxs-lookup"><span data-stu-id="c3a3d-266">13.2</span></span> | <span data-ttu-id="c3a3d-267">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-267">Data disk</span></span> |
| <span data-ttu-id="c3a3d-268">SLES</span><span class="sxs-lookup"><span data-stu-id="c3a3d-268">SLES</span></span> | <span data-ttu-id="c3a3d-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="c3a3d-269">12 SP1</span></span> | <span data-ttu-id="c3a3d-270">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-270">Data disk</span></span> |
| <span data-ttu-id="c3a3d-271">SLES</span><span class="sxs-lookup"><span data-stu-id="c3a3d-271">SLES</span></span> | <span data-ttu-id="c3a3d-272">12-SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="c3a3d-273">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-273">Data disk</span></span> |
| <span data-ttu-id="c3a3d-274">SLES</span><span class="sxs-lookup"><span data-stu-id="c3a3d-274">SLES</span></span> | <span data-ttu-id="c3a3d-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="c3a3d-275">HPC 12</span></span> | <span data-ttu-id="c3a3d-276">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-276">Data disk</span></span> |
| <span data-ttu-id="c3a3d-277">SLES</span><span class="sxs-lookup"><span data-stu-id="c3a3d-277">SLES</span></span> | <span data-ttu-id="c3a3d-278">11-SP4(Premium)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="c3a3d-279">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-279">Data disk</span></span> |
| <span data-ttu-id="c3a3d-280">SLES</span><span class="sxs-lookup"><span data-stu-id="c3a3d-280">SLES</span></span> | <span data-ttu-id="c3a3d-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="c3a3d-281">11 SP4</span></span> | <span data-ttu-id="c3a3d-282">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="c3a3d-282">Data disk</span></span> |

* <span data-ttu-id="c3a3d-283">Azure Disk Encryption은 Key Vault 및 VM이 동일한 Azure 하위 지역 및 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-284">별도 하위 지역에서 리소스를 구성하면 Azure Disk Encryption 기능 사용 시 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="c3a3d-285">Azure Disk Encryption을 위한 Key Vault를 설정하고 구성하려면 이 문서의 *필수 조건* 섹션에서 **Azure Disk Encryption을 위한 Key Vault 설정 및 구성** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c3a3d-286">Azure Active Directory에 Azure Disk Encryption을 위한 Azure AD 응용 프로그램을 설정하고 구성하려면 이 문서의 *필수 조건* 섹션에서 **Azure Active Directory에서 Azure AD 응용 프로그램 설치**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c3a3d-287">Azure AD 응용 프로그램에 대한 Key Vault 액세스 정책을 설정하고 구성하려면 이 문서의 *필수 조건* 섹션에서 **Azure AD 응용 프로그램에 대한 Key Vault 액세스 정책 설정**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c3a3d-288">미리 암호화된 Windows VHD를 준비하려면 *부록*에서 **미리 암호화된 Windows VHD 준비**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="c3a3d-289">미리 암호화된 Windows VHD를 준비하려면 *부록*에서 **미리 암호화된 Windows VHD 준비** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="c3a3d-290">Azure 플랫폼은 가상 컴퓨터 OS 볼륨을 부팅하고 해독할 때 가상 컴퓨터에서 사용할 수 있도록 Key Vault에서 암호화 키 또는 암호에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="c3a3d-291">Azure 플랫폼에 권한을 부여하려면 Key Vault에서 **EnabledForDiskEncryption** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="c3a3d-292">자세한 내용은 부록에서**Azure Disk Encryption을 위한 Key Vault 설정 및 구성**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="c3a3d-293">Key Vault 비밀 및 KEK URL 버전을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="c3a3d-294">Azure에서 이 버전 관리 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="c3a3d-295">유효한 비밀과 KEK URL은 다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="c3a3d-296">올바른 비밀 URL 예제: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c3a3d-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c3a3d-297">올바른 KEK URL 예제: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c3a3d-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c3a3d-298">Azure Disk Encryption은 Key Vault 비밀 및 KEK URL의 일부로 포트 번호 지정을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="c3a3d-299">지원 또는 지원되지 않는 Key Vault URL에 대한 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="c3a3d-300">허용되지 않는 Key Vault URL *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c3a3d-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c3a3d-301">허용되는 Key Vault URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c3a3d-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c3a3d-302">Azure Disk Encryption 기능을 사용하도록 설정하려면 IaaS VM이 다음 네트워크 끝점 구성 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="c3a3d-303">Key Vault에 연결할 토큰을 얻으려면 IaaS VM에서 Azure Active Directory 끝점인 \[login.microsoftonline.com\]에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="c3a3d-304">암호화 키를 고객 Key Vault에 쓰려면 IaaS VM에서 Key Vault 끝점에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="c3a3d-305">IaaS VM은 Azure 확장 리포지토리를 호스팅하는 Azure Storage 끝점 및 VHD 파일을 호스팅하는 Azure Storage 계정에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c3a3d-306">보안 정책이 Azure VM에서 인터넷으로 액세스를 제한하는 경우 이전 URI를 확인하고 IP에 대한 아웃바운드 연결을 허용하도록 특정 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="c3a3d-307">방화벽 뒤에 있는 Azure Key Vault 구성 및 액세스(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="c3a3d-308">Azure PowerShell SDK의 최신 버전을 사용하여 Azure 디스크 암호화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="c3a3d-309">최신 버전의 [Azure PowerShell 릴리스](https://github.com/Azure/azure-powershell/releases) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c3a3d-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="c3a3d-310">Azure Disk Encryption은 [Azure PowerShell SDK 버전 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="c3a3d-311">Azure PowerShell 1.1.0을 사용하는 경우 관련된 오류가 나타나면 [Azure PowerShell 1.1.0과 관련된 Azure Disk Encryption 오류](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="c3a3d-312">Azure CLI 명령을 실행하고 Azure 구독에 연결하려면 먼저 Azure CLI를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="c3a3d-313">Azure CLI를 설치하고 Azure 구독에 연결하려면 [Azure CLI 설치 및 구성 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="c3a3d-314">Azure Resource Manager와 함께 Mac, Linux 및 Windows용 Azure CLI를 사용하려면 [Resource Manager 모드에서 Azure CLI 명령](../virtual-machines/azure-cli-arm-commands.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="c3a3d-315">관리 디스크를 암호화할 때는 암호화를 사용하기 전에 Azure Disk Encryption 외부에 관리 디스크의 스냅숏을 만들고 디스크를 백업하는 것이 필수 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="c3a3d-316">백업을 준비하지 않으면 암호화 중에 예기치 않은 오류가 발생하는 경우 복구 옵션 없이 디스크와 VM이 액세스할 수 없게 렌더링될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="c3a3d-317">Set-AzureRmVMDiskEncryptionExtension은 현재 관리 디스크를 백업하지 않으며 -skipVmBackup 매개 변수가 지정되지 않은 경우 관리 디스크에 대해 사용될 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="c3a3d-318">이 매개 변수는 Azure Disk Encryption 외부에 아직 백업하지 않은 경우 사용하기에 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="c3a3d-319">-skipVmBackup 매개 변수를 지정하면 cmdlet은 암호화되기 전에 관리 디스크를 백업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="c3a3d-320">이러한 이유로 복구가 나중에 필요한 경우 Azure Disk Encryption을 사용하기 전에 관리 디스크 VM의 백업이 준비되어 있는지 확인하는 것이 필수 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="c3a3d-321">스냅숏 또는 백업이 Azure Disk Encryption 외부에 아직 만들어지지 않은 경우에는 -skipVmBackup 매개 변수를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="c3a3d-322">Azure Disk Encryption 솔루션은 Windows IaaS VM에 대해 BitLocker 외부 키 보호기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="c3a3d-323">도메인 가입 VM의 경우 TPM 보호기를 적용하는 그룹 정책을 푸시하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="c3a3d-324">"호환되는 TPM이 없이 BitLocker 허용"에 대한 그룹 정책 정보는 [BitLocker 그룹 정책 참조](https://technet.microsoft.com/library/ee706521)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="c3a3d-325">사용자 지정 그룹 정책을 사용하는 도메인 가입 가상 컴퓨터의 Bitlocker 정책은 다음 설정을 포함해야 합니다. `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Bitlocker의 사용자 지정 그룹 정책 설정이 호환되지 않으면 Azure Disk Encryption이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="c3a3d-326">올바른 정책 설정이 없는 컴퓨터에서 새 정책을 적용하고 강제로 새 정책을 업데이트(gpupdate.exe /force)한 다음 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="c3a3d-327">Azure AD 응용 프로그램을 만들고 Key Vault를 만들거나 기존 Key Vault를 설정하고 암호화를 사용하려면 [Azure Disk Encryption 필수 요소 PowerShell 스크립트](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="c3a3d-328">Azure CLI를 사용하여 디스크 암호화 필수 구성 요소를 구성하려면 [이 Bash 스크립트](https://github.com/ejarvi/ade-cli-getting-started)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="c3a3d-329">Azure Backup 서비스를 사용하여 암호화된 VM을 백업 및 복원하려는데, Azure Disk Encryption으로 암호화가 사용하도록 설정되어 있다면, Azure Disk Encryption 키 구성을 사용하여 VM을 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="c3a3d-330">Backup 서비스는 KEK 구성만을 사용하여 암호화된 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="c3a3d-331">[Azure Backup 암호화로 암호화된 가상 컴퓨터를 백업 및 복원하는 방법](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="c3a3d-332">Linux OS 볼륨을 암호화할 때 프로세스가 끝나면 현재 VM을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="c3a3d-333">이 작업은 포털, PowerShell 또는 CLI를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="c3a3d-334">암호화 진행률을 추적하려면 Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus에 의해 반환되는 상태 메시지를 주기적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="c3a3d-335">암호화가 완료되면 이 명령에 의해 반환되는 상태 메시지가 이를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="c3a3d-336">예를 들어 "ProgressMessage: OS 디스크가 성공적으로 암호화되었으므로 VM을 재부팅하십시오."입니다. 이 시점에서 VM을 다시 시작하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="c3a3d-337">Linux용 Azure Disk Encryption을 사용하려면 암호화하기 전에 데이터 디스크에 Linux의 탑재된 파일 시스템이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="c3a3d-338">재귀적으로 탑재된 데이터 디스크는 Linux용 Azure Disk Encryption에서 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="c3a3d-339">예를 들어 대상 시스템이 /foo/bar에 디스크를 탑재한 다음 /foo/bar/baz에 다른 디스크를 탑재한 경우 /foo/bar/baz의 암호화는 성공하지만 /foo/bar의 암호화는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="c3a3d-340">Azure Disk Encryption은 위에서 언급한 필수 조건을 충족하는 Azure 갤러리 지원 이미지에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="c3a3d-341">고객 사용자 지정 이미지는 이러한 이미지에 있을 수 있는 사용자 지정 파티션 구성표 및 프로세스 동작으로 인해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="c3a3d-342">또한 초기에 필수 조건을 충족했지만 작성 후 수정된 갤러리 이미지 기반 VM도 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="c3a3d-343">이러한 이유로 Linux VM을 암호화하기 위한 권장 절차는 클린 갤러리 이미지에서 시작하여 VM을 암호화한 다음 필요에 따라 사용자 지정 소프트웨어 또는 데이터를 VM에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="c3a3d-344">암호화된 VM의 백업 및 복원은 KEK 구성으로 암호화된 VM에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c3a3d-345">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c3a3d-346">KEK는 VM을 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="c3a3d-347">Azure Active Directory에서 Azure AD 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="c3a3d-348">Azure에서 실행 중인 VM에서 암호화를 사용하도록 설정해야 하는 경우 Azure Disk Encryption이 암호화 키를 생성하고 Key Vault에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="c3a3d-349">Key Vault에서 암호화 키를 관리하려면 Azure AD 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="c3a3d-350">이런 목적으로 Azure AD 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="c3a3d-351">응용 프로그램을 등록하는 자세한 단계는 블로그 게시물 [Azure Key Vault - 단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)의 "응용 프로그램 ID 가져오기" 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c3a3d-352">이 게시물에는 Key Vault 설정 및 구성에 대한 유용한 예제도 다수 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="c3a3d-353">인증을 위해 클라이언트 비밀 기반 인증 또는 클라이언트 인증서 기반 Azure AD 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="c3a3d-354">Azure AD에 대한 클라이언트 비밀 기반 인증</span><span class="sxs-lookup"><span data-stu-id="c3a3d-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="c3a3d-355">이어지는 섹션을 통해 Azure AD에 대한 클라이언트 비밀 기반 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="c3a3d-356">Azure PowerShell을 사용하여 Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="c3a3d-357">Azure AD 응용 프로그램을 만들려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="c3a3d-358">$azureAdApplication.ApplicationId는 Azure AD ClientID이며 $aadClientSecret은 나중에 Azure Disk Encryption을 설정하는 데 사용할 클라이언트 비밀입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="c3a3d-359">Azure AD 클라이언트 비밀을 적절하게 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="c3a3d-360">Azure 클래식 포털에서 Azure AD 클라이언트 ID 및 비밀 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="c3a3d-361">[Azure 클래식 포털]( https://manage.windowsazure.com)을 사용하여 Azure AD 클라이언트 ID 및 비밀을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="c3a3d-362">이 작업을 수행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="c3a3d-363">**Active Directory** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-363">Click the **Active Directory** tab.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="c3a3d-365">**응용 프로그램 추가**를 클릭하고 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="c3a3d-367">화살표 단추를 클릭하고 응용 프로그램 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="c3a3d-369">왼쪽 하단에 있는 확인 표시를 클릭하여 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="c3a3d-370">응용 프로그램 구성 페이지가 나타나고 Azure AD 클라이언트 ID는 페이지의 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="c3a3d-372">**저장** 단추를 클릭하여 Azure AD 클라이언트 비밀을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="c3a3d-373">키 텍스트 상자에서 Azure AD 클라이언트 비밀을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="c3a3d-374">비밀을 적절하게 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-374">Safeguard it appropriately.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="c3a3d-376">Azure 클래식 포털에서는 위의 흐름이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="c3a3d-377">기존 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-377">Use an existing application</span></span>
<span data-ttu-id="c3a3d-378">다음 명령을 실행하려면 [Azure AD PowerShell 모듈](https://technet.microsoft.com/library/jj151815.aspx)을 가져와 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-379">새 PowerShell 창에서 다음 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="c3a3d-380">이러한 명령을 실행하는 데 Azure PowerShell 또는 Azure Resource Manager 창을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="c3a3d-381">이러한 cmdlet이 MSOnline 모듈 또는 Azure AD PowerShell에 있으므로 이 방법을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="c3a3d-382">Azure AD에 대한 인증서 기반 인증</span><span class="sxs-lookup"><span data-stu-id="c3a3d-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="c3a3d-383">Azure AD 인증서 기반 인증은 현재 Linux VM에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="c3a3d-384">이어지는 섹션에서는 Azure AD에 대한 인증서 기반 인증을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="c3a3d-385">Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-385">Create an Azure AD application</span></span>
<span data-ttu-id="c3a3d-386">Azure AD 응용 프로그램을 만들려면 다음 PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-387">다음 `yourpassword` 문자열을 보안 암호로 바꾸고 암호를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="c3a3d-388">이 단계를 마친 후 PFX 파일을 Key Vault에 업로드하고 인증서를 VM에 배포하는 데 필요한 액세스 정책을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="c3a3d-389">기존 Azure AD 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="c3a3d-390">기존 응용 프로그램을 위한 인증서 기반 인증을 구성하는 경우 아래 표시된 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="c3a3d-391">새 PowerShell 창에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="c3a3d-392">이 단계를 마친 후 PFX 파일을 Key Vault에 업로드하고 인증서를 VM에 배포하는 데 필요한 액세스 정책을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="c3a3d-393">PFX 파일을 Key Vault에 업로드</span><span class="sxs-lookup"><span data-stu-id="c3a3d-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="c3a3d-394">이 프로세스에 대한 자세한 설명은 [공식 Azure Key Vault 팀 블로그](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="c3a3d-395">그러나 다음 PowerShell cmdlet만으로도 이 작업을 충분히 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="c3a3d-396">Azure PowerShell 콘솔에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-397">다음 `yourpassword` 문자열을 보안 암호로 바꾸고 암호를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="c3a3d-398">Key Vault의 인증서를 기존 VM에 배포</span><span class="sxs-lookup"><span data-stu-id="c3a3d-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="c3a3d-399">PFX 업로드를 완료한 후 다음과 같이 Key Vault의 인증서를 기존 VM에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="c3a3d-400">Azure AD 응용 프로그램에 대한 Key Vault 액세스 정책 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="c3a3d-401">Azure AD 응용 프로그램에 자격 증명 모음의 키 또는 암호에 액세스할 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="c3a3d-402">_–ServicePrincipalName_ 매개 변수 값으로 클라이언트 ID(응용 프로그램이 등록될 때 생성됨)를 사용하여 [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet으로 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="c3a3d-403">자세한 내용은 블로그 게시물 [Azure Key Vault - 단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c3a3d-404">다음은 PowerShell을 통해 이 작업을 수행하는 방법에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="c3a3d-405">Azure Disk Encryption에서는 Azure AD 클라이언트 응용 프로그램에 _WrapKey_ 및 _Set_ 권한과 같은 액세스 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="c3a3d-406">용어</span><span class="sxs-lookup"><span data-stu-id="c3a3d-406">Terminology</span></span>
<span data-ttu-id="c3a3d-407">이 기술에 사용되는 일반적인 용어를 이해하려면 다음 용어 표를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="c3a3d-408">용어</span><span class="sxs-lookup"><span data-stu-id="c3a3d-408">Terminology</span></span> | <span data-ttu-id="c3a3d-409">정의</span><span class="sxs-lookup"><span data-stu-id="c3a3d-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3a3d-410">Azure AD</span></span> | <span data-ttu-id="c3a3d-411">Azure AD는 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="c3a3d-412">Azure AD 계정은 Key Vault에서 비밀을 인증, 저장 및 검색하기 위한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="c3a3d-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c3a3d-413">Azure Key Vault</span></span> | <span data-ttu-id="c3a3d-414">Key Vault는 암호화 키 및 중요한 비밀을 안전하게 보호하는 FIPS(Federal Information Processing Standard) 유효성을 검사한 하드웨어 보안 모듈 기반의 암호화 키 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="c3a3d-415">자세한 내용은 [Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c3a3d-416">ARM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-416">ARM</span></span> | <span data-ttu-id="c3a3d-417">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="c3a3d-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="c3a3d-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="c3a3d-418">BitLocker</span></span> |<span data-ttu-id="c3a3d-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx)는 Windows IaaS VM에서 디스크 암호화를 설정하는 데 사용되는 업계에서 공인된 Windows 볼륨 암호화 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="c3a3d-420">BEK</span><span class="sxs-lookup"><span data-stu-id="c3a3d-420">BEK</span></span> | <span data-ttu-id="c3a3d-421">BitLocker 암호화 키는 OS 부팅 볼륨 및 데이터 볼륨을 암호화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="c3a3d-422">BitLocker 키는 Key Vault에서 비밀 보안 수단입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="c3a3d-423">CLI</span><span class="sxs-lookup"><span data-stu-id="c3a3d-423">CLI</span></span> | <span data-ttu-id="c3a3d-424">[Azure 명령줄 인터페이스](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="c3a3d-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="c3a3d-425">DM-Crypt</span></span> |<span data-ttu-id="c3a3d-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt)는 Linux IaaS VM에서 디스크 암호화를 설정하는 데 사용되는 Linux 기반의 투명한 디스크 암호화 하위 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="c3a3d-427">KEK</span><span class="sxs-lookup"><span data-stu-id="c3a3d-427">KEK</span></span> | <span data-ttu-id="c3a3d-428">주요 암호화 키는 비밀을 보호하거나 래핑하는 데 사용할 수 있는 비대칭 키(RSA 2048)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="c3a3d-429">HSM(하드웨어 보안 모듈) 보호 키 또는 소프트웨어 보호 키를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="c3a3d-430">자세한 내용은 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c3a3d-431">PS cmdlet</span><span class="sxs-lookup"><span data-stu-id="c3a3d-431">PS cmdlets</span></span> | <span data-ttu-id="c3a3d-432">[Azure PowerShell cmdlet](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="c3a3d-433">Azure Disk Encryption을 위한 Key Vault 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="c3a3d-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="c3a3d-434">Azure Disk Encryption을 통해 Key Vault에서 디스크 암호화 키 및 비밀을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="c3a3d-435">Azure Disk Encryption에 대한 Key Vault를 설명하려면 다음 각 섹션의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="c3a3d-436">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-436">Create a key vault</span></span>
<span data-ttu-id="c3a3d-437">Key Vault를 만들려면 다음 옵션 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="c3a3d-438">"101-Key-Vault-Create" Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c3a3d-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="c3a3d-439">Azure PowerShell Key Vault cmdlet</span><span class="sxs-lookup"><span data-stu-id="c3a3d-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="c3a3d-440">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="c3a3d-440">Azure Resource Manager</span></span>
* <span data-ttu-id="c3a3d-441">[Key Vault를 보호](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)하는 방법</span><span class="sxs-lookup"><span data-stu-id="c3a3d-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-442">구독에 대한 Key Vault 설정이 이미 있는 경우 다음 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="c3a3d-444">주요 암호화 키 설정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="c3a3d-445">BitLocker 암호화 키에 대한 추가 보안 계층으로 KEK를 사용하려는 경우 KEK를 Key Vault에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="c3a3d-446">[`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet을 사용하여 Key Vault에 주요 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="c3a3d-447">또한 온-프레미스 키 관리 HSM에서 KEK를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="c3a3d-448">자세한 내용은 [Key Vault 설명서](https://azure.microsoft.com/documentation/services/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="c3a3d-449">Azure Resource Manager로 이동하거나 Key Vault 인터페이스를 사용하여 KEK를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="c3a3d-451">Key Vault 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-451">Set key vault permissions</span></span>
<span data-ttu-id="c3a3d-452">Azure 플랫폼은 VM을 부팅하고 볼륨을 해독할 수 있도록 Key Vault의 암호화 키 또는 비밀에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="c3a3d-453">Azure 플랫폼에 권한을 부여하려면 Key Vault PowerShell cmdlet을 사용하여 **EnabledForDiskEncryption** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="c3a3d-454">또한 [Azure Resource Explorer](https://resources.azure.com)에 방문하여 **EnabledForDiskEncryption** 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="c3a3d-455">앞서 설명한 것처럼 Key Vault에 **EnabledForDiskEncryption** 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="c3a3d-456">그렇지 않으면 배포에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="c3a3d-457">여기 표시된 것처럼, Key Vault 인터페이스에서 Azure AD 응용 프로그램에 대한 액세스 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="c3a3d-460">**고급 액세스 정책** 탭에서 Azure Disk Encryption에 대해 Key Vault가 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="c3a3d-462">디스크 암호화 배포 시나리오 및 사용자 환경</span><span class="sxs-lookup"><span data-stu-id="c3a3d-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="c3a3d-463">수많은 디스크 암호화 시나리오를 사용할 수 있으며 단계는 시나리오에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="c3a3d-464">다음 섹션에서는 이러한 시나리오를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="c3a3d-465">Marketplace에서 만든 새 IaaS VM에서 암호화를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="c3a3d-466">[Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)을 사용하여 Azure에서 Marketplace의 새 IaaS Windows VM에 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="c3a3d-467">Azure 빠른 시작 템플릿에서 **Azure에 배포**를 클릭하고 **매개 변수** 블레이드에 암호화 구성을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c3a3d-468">구독, 리소스 그룹, 리소스 그룹 위치, 약관 및 규약을 선택하고 **만들기**를 클릭하여 새 IaaS VM에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-469">이 템플릿은 Windows Server 2012 갤러리 이미지를 사용하는 새 암호화된 Windows VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="c3a3d-470">이 [Resource Manager 템플릿](https://aka.ms/fde-rhel)을 사용하여 200GB RAID-0 배열이 있는 새 IaaS RedHat Linux 7.2 VM에서 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="c3a3d-471">템플릿을 배포한 후 [실행 중인 Linux VM에서 OS 드라이브 암호화](#encrypting-os-drive-on-a-running-linux-vm) 섹션에 설명된 대로 `Get-AzureRmVmDiskEncryptionStatus` cmdlet을 사용하여 VM 암호화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="c3a3d-472">컴퓨터에서 _VMRestartPending_ 상태를 반환하면 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="c3a3d-473">다음 표에 Azure AD 클라이언트 ID를 사용하는 Marketplace 시나리오에서 새 VM에 대한 Resource Manager 템플릿 매개 변수 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="c3a3d-474">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c3a3d-474">Parameter</span></span> | <span data-ttu-id="c3a3d-475">설명</span><span class="sxs-lookup"><span data-stu-id="c3a3d-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-476">adminUserName</span></span> | <span data-ttu-id="c3a3d-477">가상 컴퓨터의 관리 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="c3a3d-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="c3a3d-478">adminPassword</span></span> | <span data-ttu-id="c3a3d-479">가상 컴퓨터의 관리 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="c3a3d-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="c3a3d-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-480">newStorageAccountName</span></span> | <span data-ttu-id="c3a3d-481">OS 및 데이터 VHD를 저장할 저장소 계정의 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="c3a3d-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="c3a3d-482">vmSize</span></span> | <span data-ttu-id="c3a3d-483">VM의 크기.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-483">Size of the VM.</span></span> <span data-ttu-id="c3a3d-484">현재 표준 A, D 및 G 시리즈만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c3a3d-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-485">virtualNetworkName</span></span> | <span data-ttu-id="c3a3d-486">VM NIC가 속해야 하는 VNet의 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c3a3d-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-487">subnetName</span></span> | <span data-ttu-id="c3a3d-488">VM NIC가 속해야 하는 VNet의 서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c3a3d-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-489">AADClientID</span></span> | <span data-ttu-id="c3a3d-490">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c3a3d-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c3a3d-491">AADClientSecret</span></span> | <span data-ttu-id="c3a3d-492">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c3a3d-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-493">keyVaultURL</span></span> | <span data-ttu-id="c3a3d-494">BitLocker 키가 업로드될 Key Vault의 URL.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c3a3d-495">cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`를 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="c3a3d-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c3a3d-497">생성된 BitLocker 키를 암호화하는 데 사용되는 주요 암호화 키의 URL(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="c3a3d-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c3a3d-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="c3a3d-499">Key Vault의 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="c3a3d-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="c3a3d-500">vmName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-500">vmName</span></span> | <span data-ttu-id="c3a3d-501">암호화 작업을 수행할 VM의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c3a3d-502">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c3a3d-503">Key Vault에서 데이터 암호화 키(암호 비밀)에 대한 보안을 강화하기 위해 고유한 KEK를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="c3a3d-504">고객 암호화 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="c3a3d-505">이 시나리오에서는 Resource Manager 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용하여 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c3a3d-506">다음 섹션에서는 Resource Manager 템플릿과 CLI 명령에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="c3a3d-507">Azure에서 사용할 수 있는 미리 암호화된 이미지를 준비하는 방법은 다음 섹션의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="c3a3d-508">이미지를 만든 후 다음 섹션의 단계를 사용하여 암호화된 Azure VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="c3a3d-509">사전에 암호화된 Windows VHD 준비</span><span class="sxs-lookup"><span data-stu-id="c3a3d-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="c3a3d-510">사전에 암호화된 Linux VHD 준비</span><span class="sxs-lookup"><span data-stu-id="c3a3d-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="c3a3d-511">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-511">Using the Resource Manager template</span></span>
<span data-ttu-id="c3a3d-512">[Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)을 사용하여 암호화된 VHD에서 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="c3a3d-513">Azure 빠른 시작 템플릿에서 **Azure에 배포**를 클릭하고 **매개 변수** 블레이드에 암호화 구성을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c3a3d-514">구독, 리소스 그룹, 리소스 그룹 위치, 약관 및 규약을 선택하고 **만들기**를 클릭하여 새 IaaS VM에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="c3a3d-515">다음 표에 암호화된 VHD에 대한 Resource Manager 템플릿 매개 변수 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="c3a3d-516">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c3a3d-516">Parameter</span></span> | <span data-ttu-id="c3a3d-517">설명</span><span class="sxs-lookup"><span data-stu-id="c3a3d-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-518">newStorageAccountName</span></span> | <span data-ttu-id="c3a3d-519">암호화된 OS VHD를 저장할 저장소 계정의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="c3a3d-520">이 저장소 계정은 VM과 동일한 리소스 그룹 및 동일한 위치에 이미 만들어져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="c3a3d-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="c3a3d-521">osVhdUri</span></span> | <span data-ttu-id="c3a3d-522">저장소 계정에서 OS VHD의 URI</span><span class="sxs-lookup"><span data-stu-id="c3a3d-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="c3a3d-523">osType</span><span class="sxs-lookup"><span data-stu-id="c3a3d-523">osType</span></span> | <span data-ttu-id="c3a3d-524">OS 제품 유형(Windows/Linux)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="c3a3d-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-525">virtualNetworkName</span></span> | <span data-ttu-id="c3a3d-526">VM NIC가 속해야 하는 VNet의 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="c3a3d-527">이 이름은 VM과 동일한 리소스 그룹 및 동일한 위치에 이미 만들어져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="c3a3d-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-528">subnetName</span></span> | <span data-ttu-id="c3a3d-529">VM NIC가 속해야 하는 VNet의 서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c3a3d-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="c3a3d-530">vmSize</span></span> | <span data-ttu-id="c3a3d-531">VM의 크기.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-531">Size of the VM.</span></span> <span data-ttu-id="c3a3d-532">현재 표준 A, D 및 G 시리즈만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c3a3d-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-533">keyVaultResourceID</span></span> | <span data-ttu-id="c3a3d-534">Azure Resource Manager에서 Key Vault 리소스를 식별하는 ResourceID.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="c3a3d-535">PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`를 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="c3a3d-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="c3a3d-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="c3a3d-537">Key Vault에 설정된 디스크 암호화 키의 URL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="c3a3d-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="c3a3d-538">keyVaultKekUrl</span></span> | <span data-ttu-id="c3a3d-539">생성된 디스크 암호화 키를 암호화하기 위한 주요 암호화 키의 URL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="c3a3d-540">vmName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-540">vmName</span></span> | <span data-ttu-id="c3a3d-541">IaaS VM의 이름</span><span class="sxs-lookup"><span data-stu-id="c3a3d-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c3a3d-542">PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c3a3d-543">PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk)를 사용하여 암호화된 VHD에서 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="c3a3d-544">CLI 명령 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-544">Using CLI commands</span></span>
<span data-ttu-id="c3a3d-545">CLI 명령을 사용하여 이 시나리오에 대한 디스크 암호화를 사용하도록 설정하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c3a3d-546">Key Vault에 대한 액세스 정책 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="c3a3d-547">**EnabledForDiskEncryption** 플래그 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c3a3d-548">Azure AD 응용 프로그램에 Key Vault에 비밀을 쓸 수 있는 권한 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c3a3d-549">기존 또는 실행 중인 VM에서 암호화를 사용하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c3a3d-550">암호화 상태 가져오기:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c3a3d-551">암호화된 VHD에서 새 VM에 암호화를 사용하도록 설정하려면 `azure vm create` 명령에 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="c3a3d-552">Azure에서 기존 또는 실행 중인 IaaS Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="c3a3d-553">이 시나리오에서는 Resource Manager 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용하여 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c3a3d-554">다음 섹션에서는 Resource Manager 템플릿과 CLI 명령을 사용하여 활성화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="c3a3d-555">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-555">Using the Resource Manager template</span></span>
<span data-ttu-id="c3a3d-556">[Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)을 사용하여 Azure에서 기존 또는 실행 중인 IaaS Windows VM에 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c3a3d-557">Azure 빠른 시작 템플릿에서 **Azure에 배포**를 클릭하고 **매개 변수** 블레이드에 암호화 구성을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c3a3d-558">구독, 리소스 그룹, 리소스 그룹 위치, 약관 및 규약을 선택하고 **만들기**를 클릭하여 기존 또는 실행 중인 IaaS VM에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="c3a3d-559">다음 표에 Azure AD 클라이언트 ID를 사용하는 기존 또는 실행 중인 VM에 대한 Resource Manager 템플릿 매개 변수 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c3a3d-560">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c3a3d-560">Parameter</span></span> | <span data-ttu-id="c3a3d-561">설명</span><span class="sxs-lookup"><span data-stu-id="c3a3d-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-562">AADClientID</span></span> | <span data-ttu-id="c3a3d-563">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c3a3d-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c3a3d-564">AADClientSecret</span></span> | <span data-ttu-id="c3a3d-565">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 비밀</span><span class="sxs-lookup"><span data-stu-id="c3a3d-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c3a3d-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-566">keyVaultName</span></span> | <span data-ttu-id="c3a3d-567">BitLocker 키가 업로드될 Key Vault의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c3a3d-568">cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`을 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c3a3d-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c3a3d-570">생성된 BitLocker 키를 암호화하는 데 사용되는 주요 암호화 키의 URL.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="c3a3d-571">UseExistingKek 드롭다운 목록에서 **nokek**를 선택하면 이 매개 변수가 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="c3a3d-572">UseExistingKek 드롭다운 목록에서 **kek**를 선택하면 _keyEncryptionKeyURL_ 값을 반드시 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c3a3d-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="c3a3d-573">volumeType</span></span> | <span data-ttu-id="c3a3d-574">암호화 작업을 수행할 볼륨의 유형.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="c3a3d-575">유효한 값은 _OS_, _Data_ 및 _All_입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="c3a3d-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c3a3d-576">sequenceVersion</span></span> | <span data-ttu-id="c3a3d-577">BitLocker 작업의 시퀀스 버전.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c3a3d-578">동일한 VM에서 디스크 암호화 작업이 수행될 때마다 이 버전 번호가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="c3a3d-579">vmName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-579">vmName</span></span> | <span data-ttu-id="c3a3d-580">암호화 작업을 수행할 VM의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c3a3d-581">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c3a3d-582">Key Vault에서 데이터 암호화 키(BitLocker 암호화 비밀)에 대한 보안을 강화하기 위해 고유한 KEK를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c3a3d-583">PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c3a3d-584">PowerShell cmdlet을 사용하여 Azure Disk Encryption으로 암호화를 사용하는 방법은 블로그 게시물 [Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 1부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="c3a3d-585">CLI 명령 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-585">Using CLI commands</span></span>
<span data-ttu-id="c3a3d-586">CLI 명령을 사용하여 Azure에서 기존 또는 실행 중인 IaaS Windows VM에서 암호화를 사용하도록 설정하려면 다음을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c3a3d-587">Key Vault에서 액세스 정책을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="c3a3d-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="c3a3d-588">**EnabledForDiskEncryption** 플래그 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c3a3d-589">Azure AD 응용 프로그램에 Key Vault에 비밀을 쓸 수 있는 권한 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="c3a3d-590">기존 또는 실행 중인 VM에서 암호화를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="c3a3d-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="c3a3d-591">암호화 상태를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="c3a3d-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="c3a3d-592">암호화된 VHD에서 새 VM에 암호화를 사용하도록 설정하려면 `azure vm create` 명령에 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="c3a3d-593">Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="c3a3d-594">[Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)을 사용하여 Azure에서 기존 또는 실행 중인 IaaS Linux VM에 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="c3a3d-595">Azure 빠른 시작 템플릿에서 **Azure에 배포**를 클릭하고 **매개 변수** 블레이드에 암호화 구성을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c3a3d-596">구독, 리소스 그룹, 리소스 그룹 위치, 약관 및 규약을 선택하고 **만들기**를 클릭하여 기존 또는 실행 중인 IaaS VM에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="c3a3d-597">다음 표에 Azure AD 클라이언트 ID를 사용하는 기존 또는 실행 중인 VM에 대한 Resource Manager 템플릿 매개 변수 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c3a3d-598">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c3a3d-598">Parameter</span></span> | <span data-ttu-id="c3a3d-599">설명</span><span class="sxs-lookup"><span data-stu-id="c3a3d-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-600">AADClientID</span></span> | <span data-ttu-id="c3a3d-601">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c3a3d-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c3a3d-602">AADClientSecret</span></span> | <span data-ttu-id="c3a3d-603">Key Vault에 비밀을 쓸 수 있는 권한이 있는 Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="c3a3d-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c3a3d-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-604">keyVaultName</span></span> | <span data-ttu-id="c3a3d-605">BitLocker 키가 업로드될 Key Vault의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c3a3d-606">cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`을 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c3a3d-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c3a3d-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c3a3d-608">생성된 BitLocker 키를 암호화하는 데 사용되는 주요 암호화 키의 URL.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="c3a3d-609">UseExistingKek 드롭다운 목록에서 **nokek**를 선택하면 이 매개 변수가 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="c3a3d-610">UseExistingKek 드롭다운 목록에서 **kek**를 선택하면 _keyEncryptionKeyURL_ 값을 반드시 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c3a3d-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="c3a3d-611">volumeType</span></span> | <span data-ttu-id="c3a3d-612">암호화 작업을 수행할 볼륨의 유형.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="c3a3d-613">지원되는 유효한 값은 _OS_ 또는 _All_(RHEL 7.2, CentOS 7.2, Ubuntu 16.04의 경우)이고 다른 모든 배포판의 경우 _Data_입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="c3a3d-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c3a3d-614">sequenceVersion</span></span> | <span data-ttu-id="c3a3d-615">BitLocker 작업의 시퀀스 버전.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c3a3d-616">동일한 VM에서 디스크 암호화 작업이 수행될 때마다 이 버전 번호가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="c3a3d-617">vmName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-617">vmName</span></span> | <span data-ttu-id="c3a3d-618">암호화 작업을 수행할 VM의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="c3a3d-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="c3a3d-619">passPhrase</span></span> | <span data-ttu-id="c3a3d-620">데이터 암호화 키로 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="c3a3d-621">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c3a3d-622">Key Vault에서 데이터 암호화 키(암호 비밀)에 대한 보안을 강화하기 위해 고유한 KEK를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="c3a3d-623">CLI 명령</span><span class="sxs-lookup"><span data-stu-id="c3a3d-623">CLI commands</span></span>
<span data-ttu-id="c3a3d-624">[CLI 명령](../cli-install-nodejs.md)을 설치 및 사용하여 암호화된 VHD에서 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c3a3d-625">CLI 명령을 사용하여 Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 암호화를 사용하도록 설정하려면 다음을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c3a3d-626">Key Vault에서 액세스 정책 설정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="c3a3d-627">**EnabledForDiskEncryption** 플래그 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="c3a3d-628">Azure AD 응용 프로그램에 Key Vault에 비밀을 쓸 수 있는 권한 설정:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c3a3d-629">기존 또는 실행 중인 VM에서 암호화를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="c3a3d-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c3a3d-630">암호화 상태 가져오기:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c3a3d-631">암호화된 VHD에서 새 VM에 암호화를 사용하도록 설정하려면 `azure vm create` 명령에 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="c3a3d-632">암호화된 IaaS VM의 암호화 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="c3a3d-633">Azure Resource Manager, [PowerShell cmdlet](/powershell/azure/overview) 또는 CLI 명령을 사용하여 암호화 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="c3a3d-634">다음 섹션에서는 Azure 클래식 포털 및 CLI 명령을 사용하여 암호화 상태를 가져오는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="c3a3d-635">Azure Resource Manager를 사용하여 암호화된 Windows VM의 암호화 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="c3a3d-636">다음을 수행하여 Azure Resource Manager에서 IaaS VM의 암호화 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="c3a3d-637">[Azure 클래식 포털](https://portal.azure.com/)에 로그인하고 왼쪽 메뉴에서 **가상 컴퓨터**를 클릭하여 구독에서 가상 컴퓨터의 요약 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="c3a3d-638">**구독** 드롭다운 목록에서 구독 이름을 선택하여 가상 컴퓨터 보기를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="c3a3d-639">**가상 컴퓨터** 페이지 위쪽에서 **열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="c3a3d-640">**열 선택** 블레이드에서 **디스크 암호화**를 선택한 후 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="c3a3d-641">다음 그림에 표시된 것처럼 각 VM에 대한 _사용_ 또는 _사용 안 함_ 암호화 상태를 보여주는 디스크 암호화 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="c3a3d-643">디스크 암호화 PowerShell cmdlet을 사용하여 암호화된(Windows/Linux) IaaS VM의 암호화 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="c3a3d-644">디스크 암호화 PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`에서 IaaS VM의 암호화 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="c3a3d-645">VM에 대한 암호화 설정을 가져오려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="c3a3d-646">암호화 키 URL에 대해 _Get-AzureRmVMDiskEncryptionStatus_의 출력을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="c3a3d-647">OSVolumeEncrypted 및 DataVolumesEncrypted 설정 값이 _Encrypted_로 설정되어 두 볼륨이 Azure Disk Encryption을 사용하여 암호화됨을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="c3a3d-648">PowerShell cmdlet을 사용하여 Azure Disk Encryption으로 암호화를 사용하는 방법은 블로그 게시물 [Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 1부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-649">Linux VM에서는 `Get-AzureRmVMDiskEncryptionStatus` cmdlet으로 암호화 상태를 보고하는 데 3-4분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="c3a3d-650">디스크 암호화 CLI 명령에서 IaaS VM의 암호화 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3a3d-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="c3a3d-651">디스크 암호화 CLI 명령 `azure vm show-disk-encryption-status`에서 IaaS VM의 암호화 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="c3a3d-652">VM에 대한 암호화 설정을 가져오려면 Azure CLI 세션을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="c3a3d-653">실행 중인 Windows IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="c3a3d-654">Azure Disk Encryption Resource Manager 템플릿 또는 PowerShell cmdlet을 통해 실행 중인 Windows 또는 Linux IaaS VM에서 암호화를 사용하지 않고 암호 해독 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="c3a3d-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-655">Windows VM</span></span>
<span data-ttu-id="c3a3d-656">암호화 사용 안 함 단계는 실행 중인 Windows IaaS VM에서 OS, 데이터 볼륨이나 둘 모두의 암호화를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="c3a3d-657">OS 볼륨을 사용하지 않고 암호화된 데이터 볼륨은 그대로 둘 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="c3a3d-658">암호화 사용 안 함 단계를 수행하면 Azure 클래식 배포 모델은 VM 서비스 모델을 업데이트하고 Windows IaaS VM은 암호가 해독되었다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c3a3d-659">VM의 콘텐츠는 더 이상 미사용 상태에서 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="c3a3d-660">암호 해독은 Key Vault 및 암호화 키 자료(Windows의 경우 BitLocker 암호화 키, Linux의 경우 Passphrase)를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="c3a3d-661">Linux VM</span><span class="sxs-lookup"><span data-stu-id="c3a3d-661">Linux VM</span></span>
<span data-ttu-id="c3a3d-662">암호화 사용 안 함 단계는 실행 중인 Linux IaaS VM에서 데이터 볼륨의 암호화를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="c3a3d-663">이 단계는 OS 디스크가 암호화되지 않은 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-664">OS 디스크에서 암호화를 사용하지 않도록 설정하는 것은 Linux VM에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c3a3d-665">기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c3a3d-666">[Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)을 사용하여 실행 중인 Windows IaaS VM에서 디스크 암호화를 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c3a3d-667">Azure 빠른 시작 템플릿에서 **Azure에 배포**를 클릭하고 **매개 변수** 블레이드에 암호 해독 구성을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c3a3d-668">구독, 리소스 그룹, 리소스 그룹 위치, 약관 및 규약을 선택하고 **만들기**를 클릭하여 새 IaaS VM에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="c3a3d-669">Linux VM의 경우 [실행 중인 Linux VM에서 암호화 사용 안 함](https://aka.ms/decrypt-linuxvm) 템플릿을 사용하여 암호화를 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="c3a3d-670">다음 표는 실행 중인 IaaS VM에서 암호화를 사용하지 않는 Resource Manager 템플릿 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="c3a3d-671">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c3a3d-671">Parameter</span></span> | <span data-ttu-id="c3a3d-672">설명</span><span class="sxs-lookup"><span data-stu-id="c3a3d-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3a3d-673">vmName</span><span class="sxs-lookup"><span data-stu-id="c3a3d-673">vmName</span></span> | <span data-ttu-id="c3a3d-674">암호화 작업을 수행할 VM의 이름.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="c3a3d-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="c3a3d-675">volumeType</span></span> | <span data-ttu-id="c3a3d-676">암호 해독 작업을 수행할 볼륨의 유형.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="c3a3d-677">유효한 값은 _OS_, _Data_ 및 _All_입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="c3a3d-678">_Data_ 볼륨에서 암호화를 사용하고도 실행 중인 Windows IaaS VM OS/부팅 볼륨에서 암호화를 사용하지 않을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="c3a3d-679">OS 디스크에서 암호화를 사용하지 않도록 설정하는 것은 Linux VM에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="c3a3d-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c3a3d-680">sequenceVersion</span></span> | <span data-ttu-id="c3a3d-681">BitLocker 작업의 시퀀스 버전.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c3a3d-682">동일한 VM에서 디스크 암호 해독 작업이 수행될 때마다 이 버전 번호가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c3a3d-683">기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c3a3d-684">PowerShell cmdlet을 사용하여 기존 또는 실행 중인 IaaS VM에서 암호화를 사용하지 않도록 설정하려면 [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="c3a3d-685">이 cmdlet에는 Windows 및 Linux VM을 둘 다 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="c3a3d-686">암호화를 사용하지 않도록 설정하려면 가상 컴퓨터에서 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="c3a3d-687">_이름_ 매개 변수를 지정하지 않으면 _Windows VM용 AzureDiskEncryption_ 기본 이름을 포함한 확장이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="c3a3d-688">Linux VM에서는 AzureDiskEncryptionForLinux 확장이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a3d-689">이 cmdlet은 가상 컴퓨터를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c3a3d-690">Azure 관리 디스크를 사용하여 미리 암호화된 IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c3a3d-691">Azure 관리 디스크 ARM 템플릿을 사용하여 미리 암호화된 VHD를 통해 암호화된 VM 만들기(다음에 있는 ARM 템플릿 사용)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="c3a3d-692">[미리 암호화된 VHD/저장소 BLOB를 통해 암호화된 관리 디스크 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c3a3d-693">Azure 관리 디스크를 사용하여 새로운 Linux IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c3a3d-694">Azure 관리 디스크 ARM 템플릿을 사용하여 암호화된 Linux IaaS VM 새로 만들기(다음에 있는 ARM 템플릿 사용)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="c3a3d-695">[전체 디스크 암호화를 사용하여 RHEL 7.2 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c3a3d-696">Azure 관리 디스크를 사용하여 새로운 Windows IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="c3a3d-697">Azure 관리 디스크 ARM 템플릿을 사용하여 암호화된 Linux IaaS VM 새로 만들기(다음에 있는 ARM 템플릿 사용)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="c3a3d-698">[갤러리 이미지로 암호화된 Windows IaaS 관리 디스크 VM 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="c3a3d-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="c3a3d-699">Azure Disk Encryption을 사용하기 전에 외부에 관리 디스크 기반 VM 인스턴스에 대해 스냅숏을 만들고 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="c3a3d-700">포털에서 관리 디스크의 스냅숏을 만들거나 Azure Backup을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="c3a3d-701">백업은 암호화 중에 예기치 않은 오류가 발생할 경우 복구 옵션으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="c3a3d-702">백업을 만들면 Set-AzureRmVMDiskEncryptionExtension cmdlet에 -skipVmBackup 매개 변수를 지정하여 관리 디스크를 암호화하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="c3a3d-703">이 명령은 백업을 만들고 이 매개 변수가 지정될 때까지 관리 디스크 기반 VM에 대해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="c3a3d-704">기존의 암호화된 프리미엄 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3a3d-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="c3a3d-705">VM 실행에 사용되는 기존의 Azure Disk Encryption 지원 인터페이스[PS cmdlet, CLI 또는 ARM 템플릿]를 사용하여 Windows VM의 AAD 클라이언트 ID/비밀, 키 암호화 키[KEK], BitLocker 암호화 키 또는 Linux VM의 암호 같은 암호화 설정을 업데이트하세요. 암호화 설정 업데이트는 비Premium Storage에서 지원하는 VM에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="c3a3d-706">Premium Storage에서 지원하는 VM에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="c3a3d-707">부록</span><span class="sxs-lookup"><span data-stu-id="c3a3d-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="c3a3d-708">구독에 연결</span><span class="sxs-lookup"><span data-stu-id="c3a3d-708">Connect to your subscription</span></span>
<span data-ttu-id="c3a3d-709">진행하기 전에 이 문서의 *필수 조건* 섹션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="c3a3d-710">모든 필수 조건이 충족되면 다음을 수행하여 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="c3a3d-711">Azure PowerShell 세션을 시작하고 다음 명령을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="c3a3d-712">여러 구독이 있고 사용할 구독을 지정하려면 다음을 입력하여 계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="c3a3d-713">사용할 구독을 지정하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="c3a3d-714">구성된 구독이 올바른지 확인하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="c3a3d-715">Azure Disk Encryption cmdlet이 설치되어 있는지 확인하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="c3a3d-716">다음 출력은 Azure Disk Encryption PowerShell 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="c3a3d-717">사전에 암호화된 Windows VHD 준비</span><span class="sxs-lookup"><span data-stu-id="c3a3d-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="c3a3d-718">Azure IaaS에서 암호화된 VHD로 배포용으로 사전에 암호화된 Windows VHD를 준비하려면 이어지는 섹션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="c3a3d-719">이 정보를 사용하여 Azure Site Recovery 또는 Azure에서 최신 Windows VM(VHD)을 준비 및 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="c3a3d-720">OS 보호를 위해 비-TPM을 허용하도록 그룹 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3a3d-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="c3a3d-721">**BitLocker 드라이브 암호화**라는 BitLocker 그룹 정책 설정을 구성하는데, **로컬 컴퓨터 정책** > **컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="c3a3d-722">다음 그림처럼 이 설정을 **운영 체제 드라이브** > **시작 시 추가 인증 요구** > **호환되는 TPM 없이 BitLocker 허용**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="c3a3d-724">BitLocker 기능 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="c3a3d-724">Install BitLocker feature components</span></span>
<span data-ttu-id="c3a3d-725">Windows Server 2012 이상에서는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="c3a3d-726">Windows Server 2008 R2에서는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="c3a3d-727">`bdehdcfg`를 사용하여 BitLocker에 대한 OS 볼륨 준비</span><span class="sxs-lookup"><span data-stu-id="c3a3d-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="c3a3d-728">OS 파티션을 압축하고 BitLocker에 대한 컴퓨터를 준비하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="c3a3d-729">BitLocker를 사용하여 OS 볼륨 보호</span><span class="sxs-lookup"><span data-stu-id="c3a3d-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="c3a3d-730">[`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) 명령으로 외부 키 보호기를 사용하여 부팅 볼륨에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="c3a3d-731">도한 외부 드라이브 또는 볼륨에 외부 키(.bek 파일)를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="c3a3d-732">암호화는 다음 재부팅 후 시스템/부팅 볼륨에 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="c3a3d-733">BitLocker를 사용하여 외부 키를 가져오기 위해서는 별도의 데이터/리소스 VHD로 VM을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="c3a3d-734">실행 중인 Linux VM에서 OS 드라이브 암호화</span><span class="sxs-lookup"><span data-stu-id="c3a3d-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="c3a3d-735">실행 중인 Linux VM에서 OS 드라이브 암호화는 다음과 같은 배포판에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="c3a3d-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="c3a3d-736">RHEL 7.2</span></span>
* <span data-ttu-id="c3a3d-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="c3a3d-737">CentOS 7.2</span></span>
* <span data-ttu-id="c3a3d-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c3a3d-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="c3a3d-739">OS 디스크 암호화를 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3a3d-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="c3a3d-740">Azure Resource Manager의 Marketplace 이미지에서 VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="c3a3d-741">4GB 이상의 RAM이 있는 Azure VM(권장 크기는 7GB)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="c3a3d-742">(RHEL 및 CentOS) SELinux를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="c3a3d-743">SELinux를 사용하지 않도록 설정하려면 VM에 대한</span><span class="sxs-lookup"><span data-stu-id="c3a3d-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="c3a3d-744">[SELinux 사용자 및 관리자 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux)에서 "4.4.2. SELinux 사용 안 함"을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="c3a3d-745">SELinux를 사용하지 않도록 설정한 후 VM을 한 번 이상 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="c3a3d-746">단계</span><span class="sxs-lookup"><span data-stu-id="c3a3d-746">Steps</span></span>
1. <span data-ttu-id="c3a3d-747">이전에 지정한 배포판 중 하나를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="c3a3d-748">CentOS 7.2의 경우 특수 이미지를 통해 OS 디스크 암호화가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="c3a3d-749">이 이미지를 사용하려면 VM을 만들 때 SKU로 "7.2n"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="c3a3d-750">필요에 따라 VM을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="c3a3d-751">모든(OS + 데이터) 드라이브를 암호화하려는 경우 데이터 드라이브를 지정하고 /etc/fstab에서 탑재할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="c3a3d-752">블록 장치 이름(예: /dev/sdb1)을 지정하는 대신, UUID=...를 사용하여 /etc/fstab에서 데이터 드라이브를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="c3a3d-753">암호화하는 동안 드라이브의 순서는 VM에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="c3a3d-754">VM이 블록 장치의 특정 순서에 의존하는 경우 암호화 후 탑재하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="c3a3d-755">SSH 세션에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="c3a3d-756">OS를 암호화하려면 [암호화 사용 시](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure) volumeType을 **All** 또는 **OS**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="c3a3d-757">`systemd` 서비스로 실행되지 않는 모든 사용자 공간 프로세스는 `SIGKILL`로 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="c3a3d-758">VM을 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-758">Reboot the VM.</span></span> <span data-ttu-id="c3a3d-759">실행 중인 VM에서 OS 디스크 암호화를 사용할 경우 VM의 가동 중지 시간을 계획하세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="c3a3d-760">[다음 섹션](#monitoring-os-encryption-progress)의 지침에 따라 암호화 진행 상태를 주기적으로 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="c3a3d-761">Get-AzureRmVmDiskEncryptionStatus에 "VMRestartPending"이 표시되면 VM에 로그인하거나 포털, PowerShell 또는 CLI를 사용하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="c3a3d-762">VM을 다시 부팅하기 전에 VM의 [부트 진단](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)을 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="c3a3d-763">OS 암호화 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="c3a3d-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="c3a3d-764">OS 암호화 진행 상태를 모니터링하는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="c3a3d-765">`Get-AzureRmVmDiskEncryptionStatus` cmdlet을 사용하고 ProgressMessage 필드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="c3a3d-766">Premium 저장소 지원 VM의 경우 VM이 "OS 디스크 암호화 시작됨"에 도달한 후 약 40-50분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="c3a3d-767">WALinuxAgent에서 [문제 #388](https://github.com/Azure/WALinuxAgent/issues/388)으로 인해 일부 배포판에서 `OsVolumeEncrypted` 및 `DataVolumesEncrypted`가 `Unknown`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="c3a3d-768">WALinuxAgent 2.1.5 버전 이상에서는 이 문제가 자동으로 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="c3a3d-769">출력에 `Unknown`이 표시되는 경우 Azure Resource Explorer를 사용하여 디스크 암호화 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="c3a3d-770">[Azure Resource Explorer](https://resources.azure.com/)로 이동한 후 왼쪽의 선택 패널에서 이 계층 구조를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="c3a3d-771">InstanceView에서 아래로 스크롤하여 드라이브의 암호화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![VM 인스턴스 보기](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="c3a3d-773">[부트 진단](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="c3a3d-774">ADE 확장의 메시지에는 `[AzureDiskEncryption]`이라는 접두사가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="c3a3d-775">SSH를 통해 VM에 로그온하고 다음에서 확장 로그를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="c3a3d-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="c3a3d-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="c3a3d-777">OS 암호화가 진행 중인 동안에는 VM에 로그온하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="c3a3d-778">다른 두 가지 방법이 실패한 경우에만 로그가 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="c3a3d-779">사전에 암호화된 Linux VHD 준비</span><span class="sxs-lookup"><span data-stu-id="c3a3d-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="c3a3d-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="c3a3d-780">Ubuntu 16</span></span>
<span data-ttu-id="c3a3d-781">다음을 수행하여 배포 설치 중에 암호화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="c3a3d-782">디스크를 분할할 때 **암호화된 볼륨 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="c3a3d-784">암호화되지 않아야 하는 별도의 부트 드라이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="c3a3d-785">루트 드라이브를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="c3a3d-787">암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-787">Provide a passphrase.</span></span> <span data-ttu-id="c3a3d-788">Key Vault에 업로드하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="c3a3d-790">분할을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="c3a3d-792">VM을 부팅하고 암호를 묻는 메시지가 표시되면 3단계에서 제공한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="c3a3d-794">[이 지침](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)을 사용하여 Azure에 업로드하기 위한 VM을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="c3a3d-795">마지막 단계(VM 프로비전 해제)를 아직 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="c3a3d-796">다음을 수행하여 Azure로 작업할 암호화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="c3a3d-797">다음 스크립트 내용으로 /usr/local/sbin/azure_crypt_key.sh라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="c3a3d-798">Azure에서 사용된 암호 파일 이름이므로 KeyFileName에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="c3a3d-799">*/etc/crypttab*에서 암호화 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="c3a3d-800">다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="c3a3d-801">Windows에서 *azure_crypt_key.sh*를 편집하고 Linux에 복사한 경우 `dos2unix /usr/local/sbin/azure_crypt_key.sh`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="c3a3d-802">스크립트에 실행 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="c3a3d-803">줄을 추가하여 */etc/initramfs-tools/modules*를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="c3a3d-804">initramfs를 업데이트하는 `update-initramfs -u -k all`을 실행하여 `keyscript`를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="c3a3d-805">이제 VM을 프로비전 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-805">Now you can deprovision the VM.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="c3a3d-807">다음 단계를 계속하여 Azure에 [VHD를 업로드](#upload-encrypted-vhd-to-an-azure-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="c3a3d-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="c3a3d-808">openSUSE 13.2</span></span>
<span data-ttu-id="c3a3d-809">배포 설치 중에 암호화를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="c3a3d-810">디스크를 파티션하는 경우 **볼륨 그룹 암호화**를 선택하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="c3a3d-811">Key Vault에 업로드할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-811">This is the password that you will upload to your key vault.</span></span>

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="c3a3d-813">암호를 사용하여 VM을 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-813">Boot the VM using your password.</span></span>

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="c3a3d-815">[Azure용 SLES 또는 openSUSE 가상 컴퓨터 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)의 지침에 따라 Azure에 업로드할 VM을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="c3a3d-816">마지막 단계(VM 프로비전 해제)를 아직 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="c3a3d-817">Azure로 작업할 암호화를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="c3a3d-818">/etc/dracut.conf를 편집하고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="c3a3d-819">/usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일의 끝에서 다음 줄을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="c3a3d-820">/usr/lib/dracut/modules.d/90crypt/parse-crypt.sh 파일의 시작 부분에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="c3a3d-821">다음 항목을 그 아래 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="c3a3d-822">to:</span><span class="sxs-lookup"><span data-stu-id="c3a3d-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c3a3d-823">/usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh를 편집하고 "# Open LUKS device"에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="c3a3d-824">`/usr/sbin/dracut -f -v`를 실행하여 initrd를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="c3a3d-825">이제 VM을 프로비전 해제하고 [VHD를 Azure에 업로드](#upload-encrypted-vhd-to-an-azure-storage-account)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="c3a3d-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c3a3d-826">CentOS 7</span></span>
<span data-ttu-id="c3a3d-827">배포 설치 중에 암호화를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="c3a3d-828">디스크를 분할할 때 **내 데이터 암호화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="c3a3d-830">루트 파티션에 대해 **암호화**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="c3a3d-832">암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-832">Provide a passphrase.</span></span> <span data-ttu-id="c3a3d-833">Key Vault에 업로드할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="c3a3d-835">VM을 부팅하고 암호를 묻는 메시지가 표시되면 3단계에서 제공한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="c3a3d-837">[Azure용 CentOS 기반 가상 컴퓨터 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)의 "CentOS 7.0+" 지침에 따라 Azure에 업로드할 VM을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="c3a3d-838">마지막 단계(VM 프로비전 해제)를 아직 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="c3a3d-839">이제 VM을 프로비전 해제하고 [VHD를 Azure에 업로드](#upload-encrypted-vhd-to-an-azure-storage-account)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="c3a3d-840">Azure로 작업할 암호화를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="c3a3d-841">/etc/dracut.conf를 편집하고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="c3a3d-842">/usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일의 끝에서 다음 줄을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="c3a3d-843">/usr/lib/dracut/modules.d/90crypt/parse-crypt.sh 파일의 시작 부분에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="c3a3d-844">다음 항목을 그 아래 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="c3a3d-845">to</span><span class="sxs-lookup"><span data-stu-id="c3a3d-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c3a3d-846">/usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh를 편집하고 "# Open LUKS device" 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="c3a3d-847">"/usr/sbin/dracut -f -v"를 실행하여 initrd를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="c3a3d-849">Azure Storage 계정에 암호화된 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="c3a3d-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="c3a3d-850">BitLocker 암호화 또는 DM-Crypt 암호화를 사용하도록 설정한 후에는 로컬 암호화된 VHD를 저장소 계정에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="c3a3d-851">사전에 암호화된 VM에 대한 디스크 암호화 비밀을 Key Vault에 업로드</span><span class="sxs-lookup"><span data-stu-id="c3a3d-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="c3a3d-852">이전에 가져온 디스크 암호화 비밀을 Key Vault에 비밀 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="c3a3d-853">Key Vault에는 디스크 암호화 및 Azure AD 클라이언트를 위해 설정된 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="c3a3d-854">KEK로 암호화되지 않은 디스크 암호화 암호</span><span class="sxs-lookup"><span data-stu-id="c3a3d-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="c3a3d-855">Key Vault에서 비밀을 설정하려면 [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="c3a3d-856">Windows 가상 컴퓨터의 경우 bek 파일이 base64 문자열로 인코딩된 후 `Set-AzureKeyVaultSecret` cmdlet을 사용하여 Key Vault로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="c3a3d-857">Linux의 경우 암호는 base64 문자열로 인코딩된 후 Key Vault로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="c3a3d-858">또한 Key Vault에서 비밀을 만들 때 다음 태그가 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="c3a3d-859">[KEK를 사용하지 않고 OS 디스크를 연결](#without-using-a-kek)하기 위해 다음 단계에서 `$secretUrl`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="c3a3d-860">KEK로 암호화된 디스크 암호화 암호</span><span class="sxs-lookup"><span data-stu-id="c3a3d-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="c3a3d-861">비밀을 Key Vault에 업로드하기 전에 주요 암호화 키를 사용하여 선택적으로 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="c3a3d-862">먼저 래핑 [API](https://msdn.microsoft.com/library/azure/dn878066.aspx)를 사용하여 주요 암호화 키로 비밀을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="c3a3d-863">이 래핑 작업의 출력은 base64 URL 인코딩 문자열로, [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet을 사용하여 비밀로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="c3a3d-864">`$KeyEncryptionKey` 및 `$secretUrl`은 [KEK를 사용하여 OS 디스크를 연결](#using-a-kek)하기 위해 다음 단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="c3a3d-865">OS 디스크를 연결할 때 비밀 URL 지정</span><span class="sxs-lookup"><span data-stu-id="c3a3d-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="c3a3d-866">KEK 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c3a3d-866">Without using a KEK</span></span>
<span data-ttu-id="c3a3d-867">OS 디스크를 연결하는 동안 `$secretUrl`을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="c3a3d-868">URL은 "KEK로 암호화되지 않은 디스크 암호화 비밀" 섹션에서 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="c3a3d-869">KEK 사용</span><span class="sxs-lookup"><span data-stu-id="c3a3d-869">Using a KEK</span></span>
<span data-ttu-id="c3a3d-870">OS 디스크를 연결할 때 `$KeyEncryptionKey` 및 `$secretUrl`을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="c3a3d-871">URL은 "KEK로 암호화되지 않은 디스크 암호화 비밀" 섹션에서 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="c3a3d-872">이 가이드 다운로드</span><span class="sxs-lookup"><span data-stu-id="c3a3d-872">Download this guide</span></span>
<span data-ttu-id="c3a3d-873">[TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)에서 이 가이드를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a3d-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="c3a3d-874">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="c3a3d-874">For more information</span></span>
[<span data-ttu-id="c3a3d-875">Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 1부</span><span class="sxs-lookup"><span data-stu-id="c3a3d-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="c3a3d-876">Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부</span><span class="sxs-lookup"><span data-stu-id="c3a3d-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
