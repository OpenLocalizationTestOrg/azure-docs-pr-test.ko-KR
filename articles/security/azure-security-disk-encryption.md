---
title: "Windows 및 Linux IaaS Vm에 대 한 디스크 암호화 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="ae4a4-103">Windows 및 Linux IaaS VM용 Azure 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="ae4a4-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="ae4a4-104">Microsoft Azure는 강력 하 게 커밋된 tooensuring 데이터 개인 정보를 데이터 sovereignty 및 toocontrol Azure 호스트를 사용 하면 다양 한 고급 기술 tooencrypt 통해 데이터를 제어 하 고 암호화 키를 관리할 데이터의 액세스 제어 및 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="ae4a4-105">이 Azure 고객 hello 유연성 toochoose hello 솔루션을 제공 비즈니스 요구에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="ae4a4-106">이 문서에 소개 tooa 새로운 기술 솔루션 "Windows 및 Linux IaaS VM에 대 한 Azure 디스크 암호화" toohelp 보호 하 고 데이터 toomeet 조직 보안 및 규정 준수 행 결과 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="ae4a4-107">hello 용지 hello를 비롯 한 toouse hello Azure 디스크 암호화 기능 시나리오 및 hello 사용자 환경을 원하는 하는 방법에 자세한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-108">특정 권장 사항으로 인해 데이터, 네트워크 또는 계산 리소스 사용량이 증가할 수 있으며 이로 인해 라이선스 또는 구독 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="ae4a4-109">개요</span><span class="sxs-lookup"><span data-stu-id="ae4a4-109">Overview</span></span>
<span data-ttu-id="ae4a4-110">Azure Disk Encryption은 Windows 및 Linux IaaS 가상 컴퓨터 디스크를 암호화할 수 있도록 하는 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="ae4a4-111">Azure 디스크 암호화 활용 hello 업계 표준 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 창과 hello의 기능 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello OS 및 hello 데이터 디스크에 대 한 Linux tooprovide 볼륨 암호화의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="ae4a4-112">와 통합 된 hello 솔루션 [Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/services/key-vault/) toohelp 제어 및 주요 자격 증명 모음 구독에서 hello 디스크 암호화 키 및 암호를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="ae4a4-113">hello 솔루션 하면 hello 가상 컴퓨터 디스크에 있는 모든 데이터가 Azure 저장소에 저장 된 상태의 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="ae4a4-114">Windows 및 Linux IaaS VM용 Azure Disk Encryption은 이제 Standard VM 및 Premium Storage를 사용하는 VM을 위한 모든 Azure 공용 지역 및 AzureGov 지역에서 **일반 공급**으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="ae4a4-115">암호화 시나리오</span><span class="sxs-lookup"><span data-stu-id="ae4a4-115">Encryption scenarios</span></span>
<span data-ttu-id="ae4a4-116">hello Azure 디스크 암호화 솔루션에서는 hello 다음 고객 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="ae4a4-117">미리 암호화된 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="ae4a4-118">지원 되는 hello Azure 갤러리 이미지에서 만든 새 IaaS Vm에 대 한 암호화를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="ae4a4-119">Azure에서 실행 중인 기존 IaaS VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="ae4a4-120">Windows IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="ae4a4-121">Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="ae4a4-122">관리 디스크 VM의 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="ae4a4-123">기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae4a4-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="ae4a4-124">키 암호화 키를 사용하여 암호화된 VM의 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="ae4a4-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="ae4a4-125">hello 솔루션 hello Microsoft Azure에서 설정 된 경우 IaaS Vm에 대 한 다음 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="ae4a4-126">Azure Key Vault와 통합</span><span class="sxs-lookup"><span data-stu-id="ae4a4-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="ae4a4-127">표준 계층 VM: [A, D, DS, G, GS, F 등 시리즈 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="ae4a4-128">Windows 및 Linux IaaS Vm 및 hello에서 관리 되는 디스크 Vm에서 사용 암호화 Azure 갤러리 이미지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="ae4a4-129">Windows IaaS VM 및 관리 디스크 VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="ae4a4-130">Linux IaaS VM 및 관리 디스크 VM에 대한 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="ae4a4-131">Windows 클라이언트 OS를 실행하는 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="ae4a4-132">탑재 경로가 있는 볼륨에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="ae4a4-133">mdadm을 사용하여 디스크 스트라이프(RAID)로 구성된 Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="ae4a4-134">데이터 디스크에 대해 LVM을 사용하여 Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="ae4a4-135">Storage 공간으로 구성된 Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="ae4a4-136">기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae4a4-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="ae4a4-137">모든 Azure 공용 지역 및 AzureGov 지역 지원됨</span><span class="sxs-lookup"><span data-stu-id="ae4a4-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="ae4a4-138">hello 솔루션 시나리오, 기능 및 기술에 따라 hello를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="ae4a4-139">기본 계층 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="ae4a4-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="ae4a4-140">Linux IaaS VM에 대한 OS 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="ae4a4-141">운영 체제 드라이브 hello Linux Iaas Vm에 대 한 암호화 된 경우 데이터 드라이브에 대 한 암호화를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="ae4a4-142">Hello 클래식 VM 만들기 방법을 사용 하 여 만들어진 IaaS Vm</span><span class="sxs-lookup"><span data-stu-id="ae4a4-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="ae4a4-143">Windows 및 Linux IaaS VM 고객 사용자 지정 이미지에 암호화를 사용하는 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="ae4a4-144">Linux LVM OS 디스크에 암호화를 사용하는 기능은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="ae4a4-145">이 지원은 곧 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-145">This support will come soon.</span></span>
* <span data-ttu-id="ae4a4-146">온-프레미스 키 관리 서비스와의 통합</span><span class="sxs-lookup"><span data-stu-id="ae4a4-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="ae4a4-147">Azure 파일(공유 파일 시스템), NFS(네트워크 파일 시스템), 동적 볼륨, 소프트웨어 기반 RAID 시스템으로 구성된 Windows VM</span><span class="sxs-lookup"><span data-stu-id="ae4a4-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="ae4a4-148">키 암호화 키를 사용하지 않고 암호화된 VM의 백업 및 복원입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="ae4a4-149">기존의 암호화된 Premium Storage VM의 암호화 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-150">암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="ae4a4-151">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="ae4a4-152">KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="ae4a4-153">곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-153">This support is coming soon.</span></span>
> <span data-ttu-id="ae4a4-154">기존의 암호화된 Premium Storage VM의 암호화 설정 업데이트는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="ae4a4-155">곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="ae4a4-156">암호화 기능</span><span class="sxs-lookup"><span data-stu-id="ae4a4-156">Encryption features</span></span>
<span data-ttu-id="ae4a4-157">를 사용 하도록 설정 및 Azure IaaS Vm에 대 한 Azure 디스크 암호화 배포 hello 다음과 같은 기능이 활성화 되어 제공 하는 hello 구성에 따라:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="ae4a4-158">저장소에 저장 된 상태의 hello OS 볼륨 tooprotect hello 부팅 볼륨의 암호화</span><span class="sxs-lookup"><span data-stu-id="ae4a4-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="ae4a4-159">저장소에 있는 미사용 데이터 볼륨 tooprotect hello 데이터 볼륨 암호화</span><span class="sxs-lookup"><span data-stu-id="ae4a4-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="ae4a4-160">Windows IaaS Vm에 대 한 드라이브 hello OS 및 데이터에 대 한 암호화를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="ae4a4-161">(경우에 운영 체제 드라이브 IS NOT 암호화) Linux IaaS Vm에 대 한 드라이브 hello 데이터에 암호화를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="ae4a4-162">Hello 암호화 키 및 키 자격 증명 모음 구독에 암호 보호</span><span class="sxs-lookup"><span data-stu-id="ae4a4-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="ae4a4-163">암호화 된 IaaS VM의 hello hello 암호화 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="ae4a4-164">Hello IaaS 가상 컴퓨터에서 디스크 암호화 구성 설정 제거</span><span class="sxs-lookup"><span data-stu-id="ae4a4-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="ae4a4-165">Hello Azure 백업 서비스를 사용 하 여 암호화 된 Vm의 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="ae4a4-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-166">암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="ae4a4-167">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="ae4a4-168">KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="ae4a4-169">Windows 및 Linux 솔루션용 IaaS VM에 대한 Azure Disk Encryption에는 다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="ae4a4-170">Windows 용 hello 디스크 암호화 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="ae4a4-171">Linux 용 hello 디스크 암호화 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="ae4a4-172">hello 디스크 암호화 PowerShell cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="ae4a4-173">디스크 암호화 Azure CLI (명령줄 인터페이스) cmdlet hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="ae4a4-174">hello 디스크 암호화 Azure 리소스 관리자 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="ae4a4-175">hello Azure 디스크 암호화 솔루션은 Windows 또는 Linux 운영 체제를 실행 중인 IaaS Vm에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="ae4a4-176">Hello 지원 운영 체제에 대 한 자세한 내용은 참조 hello "전제 조건" 섹션.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-177">Azure Disk Encryption으로 VM 디스크를 암호화하는 작업에 대한 추가 요금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="ae4a4-178">가치 제안</span><span class="sxs-lookup"><span data-stu-id="ae4a4-178">Value proposition</span></span>
<span data-ttu-id="ae4a4-179">Hello Azure 디스크 암호화 관리 솔루션에 적용할 때는 hello 다음 비즈니스 요구를 충족 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="ae4a4-180">업계 표준 암호화 기술을 tooaddress 조직 보안 및 규정 준수 요구 사항을 사용할 수 있으므로 IaaS Vm은 미사용 보안이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="ae4a4-181">IaaS VM은 고객이 제어하는 키 및 정책에 따라 부팅되며 Key Vault에서 이러한 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="ae4a4-182">암호화 워크플로</span><span class="sxs-lookup"><span data-stu-id="ae4a4-182">Encryption workflow</span></span>
<span data-ttu-id="ae4a4-183">Windows 및 Linux Vm에 대 한 디스크 암호화 tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-184">암호화 시나리오 hello 앞에 암호화 시나리오 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="ae4a4-185">Hello Azure 디스크 암호화 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 통해 tooenabling 디스크 암호화에서 선택한 hello 암호화 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="ae4a4-186">Hello 고객 암호화 VHD 시나리오에 대 한 암호화 hello VHD tooyour 저장소 계정 및 hello 암호화 키 재료 tooyour 키 자격 증명 모음을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="ae4a4-187">그런 다음 새 IaaS VM에 hello 암호화 구성 tooenable 암호화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="ae4a4-188">Hello 시장에서에서 생성 된 새 Vm 및 Azure에서 이미 실행 중인 기존 Vm에 대 한 hello IaaS VM에 hello 암호화 구성 tooenable 암호화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="ae4a4-189">권한 부여 액세스 toohello Azure 플랫폼 tooread hello 암호화 키 (Windows 시스템에 대 한 BitLocker 암호화 키) 및 Linux에 대 한 암호의에서 자료 hello IaaS VM에 키 자격 증명 모음 tooenable 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="ae4a4-190">Hello Azure Active Directory (Azure AD) 응용 프로그램 identity toowrite hello 암호화 키 재료 tooyour 키 자격 증명 모음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="ae4a4-191">이렇게 하면 특정 2 단계에서 언급 한 hello 시나리오에 대 한 hello IaaS VM에 대 한 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="ae4a4-192">Azure는 암호화와 hello 주요 자격 증명 모음 구성을 hello VM 서비스 모델을 업데이트 하 고 암호화 된 VM을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="ae4a4-194">암호 해독 워크플로</span><span class="sxs-lookup"><span data-stu-id="ae4a4-194">Decryption workflow</span></span>
<span data-ttu-id="ae4a4-195">IaaS vm의 경우 높은 수준의 단계를 수행 하는 전체 hello toodisable 디스크 암호화:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="ae4a4-196">Hello Azure 디스크 암호화 리소스 관리자 템플릿 또는 PowerShell cmdlet을 통해 Azure에서 실행 중인 IaaS VM에 toodisable 암호화 (해독)를 선택 하 고 hello 암호 해독 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="ae4a4-197">이 단계는 hello OS 또는 hello 데이터 볼륨에 또는 둘 다 Windows IaaS VM을 실행 하는 hello의 암호화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="ae4a4-198">그러나 hello 이전 섹션에서 설명 했 듯이 Linux에 대 한 OS 디스크 암호화를 해제 하면 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="ae4a4-199">hello 암호 해독 단계 hello OS 디스크 암호화 되지 않은 상태로 Linux Vm에서 데이터 드라이브에만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="ae4a4-200">Azure 업데이트 hello VM 서비스 모델 및 hello IaaS VM을 암호 해독 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="ae4a4-201">hello VM의 hello 콘텐츠는 더 이상 휴지 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-202">hello 암호화 사용 안 함 작업이 경우 키 자격 증명 모음 및 hello 암호화 키 자료 (Windows 시스템에 대 한 BitLocker 암호화 키) 또는 Linux에 대 한 암호를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="ae4a4-203">Linux OS 디스크 암호화는 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="ae4a4-204">hello 암호 해독 단계 Linux Vm에서 데이터 드라이브에만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="ae4a4-205">Linux 용 데이터 디스크 암호화를 해제 하면 hello 운영 체제 드라이브를 암호화 하는 경우 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae4a4-206">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ae4a4-206">Prerequisites</span></span>
<span data-ttu-id="ae4a4-207">Hello "개요" 섹션에서에서 설명한 hello 지원 시나리오에 대 한 Azure IaaS Vm에 Azure 디스크 암호화를 사용 하기 전에 hello 다음 필수 구성 요소를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="ae4a4-208">유효한 활성 Azure 구독 toocreate 리소스 hello 지원 영역에 Azure에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="ae4a4-209">Azure 디스크 암호화는 hello 다음 Windows Server 버전에서 지원: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="ae4a4-210">Azure 디스크 암호화는 hello 다음 Windows 클라이언트 버전에서 지원: Windows 8 클라이언트 및 Windows 10 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-211">Windows Server 2008 R2의 경우 Azure에서 암호화를 사용하도록 설정하기 전에 .NET Framework 4.5를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="ae4a4-212">Windows Server 2008 R2 x64 기반 시스템에 대 한 Microsoft.NET Framework 4.5.2 hello 선택적 업데이트를 설치 하 여 Windows 업데이트에서 설치할 수 있습니다 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="ae4a4-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="ae4a4-213">Azure 디스크 암호화가 지원 hello Azure 갤러리의 다음 기반으로 Linux 서버 배포 및 버전:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="ae4a4-214">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="ae4a4-214">Linux Distribution</span></span> | <span data-ttu-id="ae4a4-215">버전</span><span class="sxs-lookup"><span data-stu-id="ae4a4-215">Version</span></span> | <span data-ttu-id="ae4a4-216">암호화에 지원되는 볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="ae4a4-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="ae4a4-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae4a4-217">Ubuntu</span></span> | <span data-ttu-id="ae4a4-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="ae4a4-219">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-219">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae4a4-220">Ubuntu</span></span> | <span data-ttu-id="ae4a4-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="ae4a4-222">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-222">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae4a4-223">Ubuntu</span></span> | <span data-ttu-id="ae4a4-224">12.10</span><span class="sxs-lookup"><span data-stu-id="ae4a4-224">12.10</span></span> | <span data-ttu-id="ae4a4-225">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-225">Data disk</span></span> |
| <span data-ttu-id="ae4a4-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae4a4-226">Ubuntu</span></span> | <span data-ttu-id="ae4a4-227">12.04</span><span class="sxs-lookup"><span data-stu-id="ae4a4-227">12.04</span></span> | <span data-ttu-id="ae4a4-228">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-228">Data disk</span></span> |
| <span data-ttu-id="ae4a4-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-229">RHEL</span></span> | <span data-ttu-id="ae4a4-230">7.3</span><span class="sxs-lookup"><span data-stu-id="ae4a4-230">7.3</span></span> | <span data-ttu-id="ae4a4-231">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-231">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-232">RHEL</span></span> | <span data-ttu-id="ae4a4-233">7.2</span><span class="sxs-lookup"><span data-stu-id="ae4a4-233">7.2</span></span> | <span data-ttu-id="ae4a4-234">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-234">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-235">RHEL</span></span> | <span data-ttu-id="ae4a4-236">6.8</span><span class="sxs-lookup"><span data-stu-id="ae4a4-236">6.8</span></span> | <span data-ttu-id="ae4a4-237">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-237">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-238">RHEL</span></span> | <span data-ttu-id="ae4a4-239">6.7</span><span class="sxs-lookup"><span data-stu-id="ae4a4-239">6.7</span></span> | <span data-ttu-id="ae4a4-240">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-240">Data disk</span></span> |
| <span data-ttu-id="ae4a4-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-241">CentOS</span></span> | <span data-ttu-id="ae4a4-242">7.3</span><span class="sxs-lookup"><span data-stu-id="ae4a4-242">7.3</span></span> | <span data-ttu-id="ae4a4-243">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-243">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-244">CentOS</span></span> | <span data-ttu-id="ae4a4-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="ae4a4-245">7.2n</span></span> | <span data-ttu-id="ae4a4-246">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-246">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-247">CentOS</span></span> | <span data-ttu-id="ae4a4-248">6.8</span><span class="sxs-lookup"><span data-stu-id="ae4a4-248">6.8</span></span> | <span data-ttu-id="ae4a4-249">OS 및 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="ae4a4-249">OS and Data disk</span></span> |
| <span data-ttu-id="ae4a4-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-250">CentOS</span></span> | <span data-ttu-id="ae4a4-251">7.1</span><span class="sxs-lookup"><span data-stu-id="ae4a4-251">7.1</span></span> | <span data-ttu-id="ae4a4-252">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-252">Data disk</span></span> |
| <span data-ttu-id="ae4a4-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-253">CentOS</span></span> | <span data-ttu-id="ae4a4-254">7.0</span><span class="sxs-lookup"><span data-stu-id="ae4a4-254">7.0</span></span> | <span data-ttu-id="ae4a4-255">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-255">Data disk</span></span> |
| <span data-ttu-id="ae4a4-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-256">CentOS</span></span> | <span data-ttu-id="ae4a4-257">6.7</span><span class="sxs-lookup"><span data-stu-id="ae4a4-257">6.7</span></span> | <span data-ttu-id="ae4a4-258">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-258">Data disk</span></span> |
| <span data-ttu-id="ae4a4-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-259">CentOS</span></span> | <span data-ttu-id="ae4a4-260">6.6</span><span class="sxs-lookup"><span data-stu-id="ae4a4-260">6.6</span></span> | <span data-ttu-id="ae4a4-261">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-261">Data disk</span></span> |
| <span data-ttu-id="ae4a4-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae4a4-262">CentOS</span></span> | <span data-ttu-id="ae4a4-263">6.5</span><span class="sxs-lookup"><span data-stu-id="ae4a4-263">6.5</span></span> | <span data-ttu-id="ae4a4-264">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-264">Data disk</span></span> |
| <span data-ttu-id="ae4a4-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ae4a4-265">openSUSE</span></span> | <span data-ttu-id="ae4a4-266">13.2</span><span class="sxs-lookup"><span data-stu-id="ae4a4-266">13.2</span></span> | <span data-ttu-id="ae4a4-267">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-267">Data disk</span></span> |
| <span data-ttu-id="ae4a4-268">SLES</span><span class="sxs-lookup"><span data-stu-id="ae4a4-268">SLES</span></span> | <span data-ttu-id="ae4a4-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="ae4a4-269">12 SP1</span></span> | <span data-ttu-id="ae4a4-270">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-270">Data disk</span></span> |
| <span data-ttu-id="ae4a4-271">SLES</span><span class="sxs-lookup"><span data-stu-id="ae4a4-271">SLES</span></span> | <span data-ttu-id="ae4a4-272">12-SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="ae4a4-273">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-273">Data disk</span></span> |
| <span data-ttu-id="ae4a4-274">SLES</span><span class="sxs-lookup"><span data-stu-id="ae4a4-274">SLES</span></span> | <span data-ttu-id="ae4a4-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="ae4a4-275">HPC 12</span></span> | <span data-ttu-id="ae4a4-276">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-276">Data disk</span></span> |
| <span data-ttu-id="ae4a4-277">SLES</span><span class="sxs-lookup"><span data-stu-id="ae4a4-277">SLES</span></span> | <span data-ttu-id="ae4a4-278">11-SP4(Premium)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="ae4a4-279">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-279">Data disk</span></span> |
| <span data-ttu-id="ae4a4-280">SLES</span><span class="sxs-lookup"><span data-stu-id="ae4a4-280">SLES</span></span> | <span data-ttu-id="ae4a4-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="ae4a4-281">11 SP4</span></span> | <span data-ttu-id="ae4a4-282">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="ae4a4-282">Data disk</span></span> |

* <span data-ttu-id="ae4a4-283">Azure 디스크 암호화를 사용 하려면 키 자격 증명 모음 및 Vm에에서 상주 하는 hello 동일한 Azure 지역 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-284">개별 영역에서 hello 리소스 구성 hello Azure 디스크 암호화 기능을 사용 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="ae4a4-285">tooset 위로 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성 섹션을 참조 하십시오 **설정 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성** hello에 *필수 구성 요소* 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="ae4a4-286">tooset 및 Azure 디스크 암호화에 대 한 Azure Active directory에서 Azure AD 응용 프로그램을 구성 하십시오 섹션을 참조 **hello Azure AD 응용 프로그램을 Azure Active Directory에서** hello에 *필수 구성 요소* 이 문서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="ae4a4-287">tooset hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책 구성 및 하십시오 섹션을 참조 **hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책을 설정** hello에 *필수 구성 요소* 의 섹션 이 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="ae4a4-288">미리 암호화 된 Windows VHD tooprepare 섹션을 참조 하세요. **미리 암호화 된 Windows VHD를 준비** hello에 *부록*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="ae4a4-289">미리 암호화 된 Linux VHD tooprepare 섹션을 참조 하세요. **미리 암호화 된 Linux VHD 준비** hello에 *부록*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="ae4a4-290">hello Azure 플랫폼 있어야 액세스 toohello 암호화 키 또는 키 자격 증명 모음 toomake의 암호에 사용할 수 있는 toohello 가상 컴퓨터를 부팅 하 고 hello 가상 컴퓨터 운영 체제 볼륨 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="ae4a4-291">toogrant 권한 tooAzure 플랫폼 집합 hello **EnabledForDiskEncryption** hello 키 자격 증명 모음에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="ae4a4-292">자세한 내용은 참조 **설정 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성** hello 부록에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="ae4a4-293">Key Vault 비밀 및 KEK URL 버전을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="ae4a4-294">Azure에서 이 버전 관리 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="ae4a4-295">유효한 암호 및 KEK Url에 대 한 예제 따르는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="ae4a4-296">올바른 비밀 URL 예제: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="ae4a4-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="ae4a4-297">올바른 KEK URL 예제: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="ae4a4-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="ae4a4-298">Azure Disk Encryption은 Key Vault 비밀 및 KEK URL의 일부로 포트 번호 지정을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="ae4a4-299">지원 되지 않는 및 지원 되는 키 자격 증명 모음 Url의 예를 보려면 hello 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="ae4a4-300">허용되지 않는 Key Vault URL *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="ae4a4-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="ae4a4-301">허용되는 Key Vault URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="ae4a4-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="ae4a4-302">tooenable hello Azure 디스크 암호화 기능을 hello IaaS Vm 네트워크 끝점 구성 요구 사항을 준수 하는 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="ae4a4-303">tooget 토큰 tooconnect tooyour 키 자격 증명 모음을 hello IaaS VM 수 tooconnect tooan Azure Active Directory 끝점 있어야 \[login.microsoftonline.com\]합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="ae4a4-304">toowrite hello 암호화 키 tooyour 키 자격 증명 모음 hello IaaS VM 수 tooconnect toohello 주요 자격 증명 모음 끝점 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="ae4a4-305">hello IaaS VM에는 호스트 hello Azure 확장 리포지토리 및 호스트 hello VHD 파일을 Azure 저장소 계정이 있는지 수 tooconnect tooan Azure 저장소 끝점 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ae4a4-306">보안 정책에 Azure Vm toohello 인터넷에서에서 액세스를 제한 하는 경우 hello 앞에 URI를 확인할 수 있으며 특정 규칙 tooallow 아웃 바운드 연결 toohello Ip를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="ae4a4-307">tooconfigure 및 (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) 방화벽 뒤에 있는 Azure 키 자격 증명 모음 액세스</span><span class="sxs-lookup"><span data-stu-id="ae4a4-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="ae4a4-308">Hello 최신 버전의 Azure PowerShell SDK 버전 tooconfigure Azure 디스크 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="ae4a4-309">최신 버전의 hello 다운로드 [Azure PowerShell 릴리스](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="ae4a4-310">Azure Disk Encryption은 [Azure PowerShell SDK 버전 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="ae4a4-311">오류가 발생 하는 경우 Azure PowerShell 1.1.0, toousing 관련 참조 [Azure 디스크 암호화 관련 오류 tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="ae4a4-312">toorun Azure CLI 명령을 Azure 구독에 연결 하 고, 먼저 Azure CLI를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="ae4a4-313">Azure CLI tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure CLI를 구성 하 고](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="ae4a4-314">Mac, Linux 및 Windows Azure 리소스 관리자와 Azure CLI toouse 참조 [리소스 관리자 모드에서 Azure CLI 명령을](../virtual-machines/azure-cli-arm-commands.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="ae4a4-315">관리 되는 디스크를 암호화 하는 경우, 때는 필수 필수 tootake hello 관리 되는 디스크의 스냅숏을 또는 Azure 디스크 암호화 이전 tooenabling 암호화 외부 hello 디스크의 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="ae4a4-316">위치에 백업 하지 않으면 암호화 하는 동안 예기치 않은 모든 오류 해석할 수 있습니다 hello 디스크 및 VM 복구 옵션 없이 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="ae4a4-317">집합 AzureRmVMDiskEncryptionExtension 않습니다 하지 현재 관리 되는 디스크를 백업 하 고 hello-skipVmBackup 매개 변수를 지정 하지 않은 경우 관리 되는 디스크에 대해 사용 하는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="ae4a4-318">이 매개 변수 표시 되지 않으면 toouse 안전 하지 않은 백업을 Azure 디스크 암호화 외부에서 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="ae4a4-319">Hello-skipVmBackup 매개 변수를 지정 하는 경우 hello cmdlet hello 관리 되는 디스크에 대 한 이전 tooencryption의 백업을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="ae4a4-320">이러한 이유로 hello 경우 복구는 나중에 VM이 Azure 디스크 암호화 tooenabling을 이전 하는 위치에는 관리 되는 디스크의 백업이 필요 있는지 필수 필수 toomake를 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="ae4a4-321">스냅숏 또는 백업 이미 이루어졌을 외부 Azure 디스크 암호화 하지 않는 한 hello-skipVmBackup 매개 변수 사용 하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="ae4a4-322">Azure 디스크 암호화 솔루션 hello Windows IaaS Vm에 대 한 hello BitLocker 외부 키 보호기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="ae4a4-323">도메인 가입 VM의 경우 TPM 보호기를 적용하는 그룹 정책을 푸시하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="ae4a4-324">Hello 그룹 정책에 대 한 "호환 되는 TPM 없이 BitLocker 허용"에 대 한 정보를 참조 하십시오. [BitLocker 그룹 정책 참조](https://technet.microsoft.com/library/ee706521)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="ae4a4-325">사용자 지정 그룹 정책 사용 하 여 도메인에 가입 된 가상 컴퓨터에서 Bitlocker 정책 설정에 따라 hello를 포함 해야 합니다: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure 디스크 암호화는 Bitlocker에 대 한 사용자 지정 그룹 정책 설정을 호환 되지 않을 때 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="ae4a4-326">Hello 되어 있지 않은 컴퓨터에서 올바른 정책 설정, hello 새 정책을 적용 hello 새 정책 tooupdate (gpupdate.exe /force)를 강제 적용 한 다음 다시 시작이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="ae4a4-327">toocreate Azure AD 응용 프로그램 키 자격 증명 모음 만들기 또는 기존 키 자격 증명 모음 설정 및 암호화를 사용 하도록 설정, hello 참조 [필수 PowerShell 스크립트를 Azure 디스크 암호화](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="ae4a4-328">hello Azure CLI를 사용 하 여 tooconfigure 디스크 암호화 필수 구성 요소 참조 [이 Bash 스크립트](https://github.com/ejarvi/ade-cli-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="ae4a4-329">toouse hello Azure 백업 서비스 tooback 및 암호화가 설정 하 여 Azure 디스크 암호화 된 경우 암호화 복원 Vm hello Azure 디스크 암호화 키 구성을 사용 하 여 Vm을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="ae4a4-330">백업 서비스 hello KEK 구성만을 사용 하 여 암호화 된 Vm을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="ae4a4-331">참조 [를 tooback 및 복원 방법을 Azure 백업을 암호화 하 여 가상 컴퓨터를 암호화](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="ae4a4-332">Linux 운영 체제 볼륨을 암호화 하는 경우는 VM이 다시 시작 하는 현재 필요 hello 프로세스의 hello 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="ae4a4-333">Hello 포털, powershell 또는 CLI를 통해이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="ae4a4-334">암호화 tootrack hello 진행률 Get AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus에서 반환 하는 hello 상태 메시지를 주기적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="ae4a4-335">암호화 완료 되 면이이 명령에서 반환 된 hello hello 상태 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="ae4a4-336">예를 들어 "ProgressMessage: 운영 체제 디스크가 성공적으로 암호화, hello VM 다시 부팅 하십시오" VM을 다시 시작 사용 하 고이 지점 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="ae4a4-337">Linux 용 azure 디스크 암호화 데이터 디스크 toohave Linux 이전 tooencryption에 탑재 된 파일 시스템에 필요</span><span class="sxs-lookup"><span data-stu-id="ae4a4-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="ae4a4-338">재귀적으로 탑재 된 데이터 디스크 Linux hello Azure 디스크 암호화에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="ae4a4-339">예를 들어 hello 대상 시스템에 /foo/bar에 디스크를 탑재 하 고 /foo/bar/baz, /foo/bar/baz의 hello 암호화에 다른 성공, 하지만/foo/막대의 암호화 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="ae4a4-340">Azure 디스크 암호화는 hello 앞에서 언급 한 필수 구성 요소를 충족 하는 지원 되는 Azure 갤러리 이미지에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="ae4a4-341">사용자 지정 이미지 고객 toocustom 파티션 구성표 및 이러한 이미지에 있을 수 있는 프로세스 동작 인해 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="ae4a4-342">또한 초기에 필수 조건을 충족했지만 작성 후 수정된 갤러리 이미지 기반 VM도 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="ae4a4-343">에 대 한 새로 갤러리 이미지에서 toostart은 이유로 hello 제안 Linux VM을 암호화 하기 위한 절차는, hello VM을 암호화 하 고 사용자 지정 소프트웨어나 데이터 toohello 필요에 따라 VM 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="ae4a4-344">암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="ae4a4-345">KEK 없이 암호화된 VM에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="ae4a4-346">KEK는 VM을 사용하도록 설정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="ae4a4-347">Azure Active Directory에서 Azure AD 응용 프로그램을 hello를 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="ae4a4-348">Azure에서 실행 중인 VM에서 사용 하도록 설정 하는 암호화 toobe 필요할 때 Azure 디스크 암호화 생성 하 고 hello 암호화 키 tooyour 주요 자격 증명 모음을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="ae4a4-349">Key Vault에서 암호화 키를 관리하려면 Azure AD 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="ae4a4-350">이런 목적으로 Azure AD 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="ae4a4-351">Hello 블로그 게시물의 hello "hello 응용 프로그램에 대 한 Id 가져오기" 섹션에서 응용 프로그램 등록에 대 한 자세한 단계를 찾을 수 있습니다 [Azure 키 자격 증명 모음-단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="ae4a4-352">이 게시물에는 Key Vault 설정 및 구성에 대한 유용한 예제도 다수 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="ae4a4-353">인증을 위해 클라이언트 비밀 기반 인증 또는 클라이언트 인증서 기반 Azure AD 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="ae4a4-354">Azure AD에 대한 클라이언트 비밀 기반 인증</span><span class="sxs-lookup"><span data-stu-id="ae4a4-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="ae4a4-355">hello 다음 섹션에서는 Azure AD에 대 한 클라이언트 암호 기반 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="ae4a4-356">Azure PowerShell을 사용하여 Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ae4a4-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="ae4a4-357">다음 PowerShell cmdlet toocreate Azure AD 응용 프로그램 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="ae4a4-358">$azureAdApplication.ApplicationId hello Azure AD ClientID 이며 $aadClientSecret hello 클라이언트 암호 이후 tooenable Azure 디스크 암호화를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="ae4a4-359">Azure AD hello 클라이언트 암호를 적절 하 게 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="ae4a4-360">Hello Azure 클래식 포털에서에서 Azure AD hello 클라이언트 ID와 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="ae4a4-361">Hello를 사용 하 여 Azure AD 클라이언트 ID와 암호를 설정할 수도 있습니다 [Azure 클래식 포털]( https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="ae4a4-362">tooperform이 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-363">Hello 클릭 **Active Directory** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-363">Click hello **Active Directory** tab.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="ae4a4-365">클릭 **응용 프로그램 추가**, 다음 형식 hello 이름 및 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="ae4a4-367">Hello 화살표 단추를 클릭 하 고 hello 응용 프로그램 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="ae4a4-369">하단 왼쪽된 모서리 toofinish hello에에서 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="ae4a4-370">hello 응용 프로그램 구성 페이지가 나타나고 hello Azure AD 클라이언트 ID는 hello hello 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="ae4a4-372">Hello를 클릭 하 여 Azure AD hello 클라이언트 암호를 저장 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="ae4a4-373">Note hello 키 텍스트 상자에 Azure AD hello 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="ae4a4-374">비밀을 적절하게 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-374">Safeguard it appropriately.</span></span>

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="ae4a4-376">앞에 흐름 hello hello Azure 클래식 포털에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="ae4a4-377">기존 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-377">Use an existing application</span></span>
<span data-ttu-id="ae4a4-378">tooexecute 명령 뒤 hello를 hello를 사용 하 여 [Azure AD PowerShell 모듈이](https://technet.microsoft.com/library/jj151815.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-379">hello 다음 명령은 실행 해야 새 PowerShell 창에서.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="ae4a4-380">Azure PowerShell 또는 hello Azure 리소스 관리자 창 tooexecute hello 명령을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="ae4a4-381">Hello MSOnline 모듈 또는 Azure AD PowerShell에서 이러한 cmdlet은이 접근 방법이 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="ae4a4-382">Azure AD에 대한 인증서 기반 인증</span><span class="sxs-lookup"><span data-stu-id="ae4a4-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="ae4a4-383">Azure AD 인증서 기반 인증은 현재 Linux VM에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="ae4a4-384">다음 섹션에서는 표시 방법을 hello tooconfigure Azure AD에 대 한 인증서 기반 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="ae4a4-385">Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ae4a4-385">Create an Azure AD application</span></span>
<span data-ttu-id="ae4a4-386">Azure AD 응용 프로그램 toocreate hello 다음 PowerShell cmdlet를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-387">Hello 다음 대체 `yourpassword` 보안 암호 및 보호 방법 hello 암호를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="ae4a4-388">이 단계를 완료 한 후 PFX 파일 tooyour 키 자격 증명 모음을 업로드 하 고 해당 인증서 tooa VM 액세스 필요한 정책의 toodeploy hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="ae4a4-389">기존 Azure AD 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="ae4a4-390">기존 응용 프로그램에 대 한 인증서 기반 인증을 구성 하는 경우 여기에 표시 된 hello PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="ae4a4-391">수 있는지 tooexecute 새 PowerShell 창에서.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="ae4a4-392">이 단계를 완료 한 후 PFX 파일 tooyour 키 자격 증명 모음을 업로드 하 고 필요한 toodeploy hello 인증서 tooa VM hello 액세스 정책을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="ae4a4-393">PFX 파일 tooyour 키 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="ae4a4-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="ae4a4-394">이 프로세스에 대 한 자세한 내용은 참조 하십시오. [공식 Azure 키 자격 증명 모음 팀 블로그 hello](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="ae4a4-395">그러나 PowerShell cmdlet을 다음 hello hello 작업에 대 한 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="ae4a4-396">있는지 tooexecute 될 Azure PowerShell 콘솔에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-397">Hello 다음 대체 `yourpassword` 보안 암호 및 보호 방법 hello 암호를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="ae4a4-398">기존 VM 하 여 주요 자격 증명 모음 tooan에 인증서 배포</span><span class="sxs-lookup"><span data-stu-id="ae4a4-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="ae4a4-399">Hello PFX 업로드를 완료 한 후에 hello 주요 자격 증명 모음 tooan hello 다음 함께 존재 하는 VM에에서 인증서 배포:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
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

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="ae4a4-400">Hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책을 설정합니다</span><span class="sxs-lookup"><span data-stu-id="ae4a4-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="ae4a4-401">Azure AD 응용 프로그램 권한 tooaccess hello 키 또는 hello 자격 증명 모음의 암호 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="ae4a4-402">사용 하 여 hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant 권한 toohello 응용 프로그램 (있음 hello 응용 프로그램이 등록 될 때 생성 된) hello 클라이언트 ID를 사용 하 여 hello로 _– ServicePrincipalName_ 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="ae4a4-403">toolearn hello 블로그 게시물을 더 참조 [Azure 키 자격 증명 모음-단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="ae4a4-404">다음은 어떻게 tooperform이 작업을 통해의 예제 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="ae4a4-405">Azure 디스크 암호화는 클라이언트 응용 프로그램을 Azure AD tooyour 액세스 정책에 따라 tooconfigure hello 필요: _WrapKey_ 및 _설정_ 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="ae4a4-406">용어</span><span class="sxs-lookup"><span data-stu-id="ae4a4-406">Terminology</span></span>
<span data-ttu-id="ae4a4-407">이 기술을 사용 하 여 hello 용어 표 다음에서 사용 하는 일반적인 용어 hello toounderstand:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="ae4a4-408">용어</span><span class="sxs-lookup"><span data-stu-id="ae4a4-408">Terminology</span></span> | <span data-ttu-id="ae4a4-409">정의</span><span class="sxs-lookup"><span data-stu-id="ae4a4-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae4a4-410">Azure AD</span></span> | <span data-ttu-id="ae4a4-411">Azure AD는 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="ae4a4-412">Azure AD 계정은 Key Vault에서 비밀을 인증, 저장 및 검색하기 위한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="ae4a4-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ae4a4-413">Azure Key Vault</span></span> | <span data-ttu-id="ae4a4-414">Key Vault는 암호화 키 및 중요한 비밀을 안전하게 보호하는 FIPS(Federal Information Processing Standard) 유효성을 검사한 하드웨어 보안 모듈 기반의 암호화 키 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="ae4a4-415">자세한 내용은 [Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="ae4a4-416">ARM</span><span class="sxs-lookup"><span data-stu-id="ae4a4-416">ARM</span></span> | <span data-ttu-id="ae4a4-417">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="ae4a4-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="ae4a4-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="ae4a4-418">BitLocker</span></span> |<span data-ttu-id="ae4a4-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) 업계에서 통용 되 Windows 볼륨 암호화 하는 기술로 Windows IaaS Vm에 tooenable 디스크 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="ae4a4-420">BEK</span><span class="sxs-lookup"><span data-stu-id="ae4a4-420">BEK</span></span> | <span data-ttu-id="ae4a4-421">BitLocker 암호화 키는 사용 되는 tooencrypt hello 운영 체제 부팅 볼륨 및 데이터 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="ae4a4-422">hello BitLocker 키를 암호로 키 자격 증명 모음에 통해 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="ae4a4-423">CLI</span><span class="sxs-lookup"><span data-stu-id="ae4a4-423">CLI</span></span> | <span data-ttu-id="ae4a4-424">[Azure 명령줄 인터페이스](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="ae4a4-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="ae4a4-425">DM-Crypt</span></span> |<span data-ttu-id="ae4a4-426">[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 가 Linux IaaS Vm에 tooenable 디스크 암호화를 사용 하는 hello Linux ± â, 투명 한 디스크 암호화 하위 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="ae4a4-427">KEK</span><span class="sxs-lookup"><span data-stu-id="ae4a4-427">KEK</span></span> | <span data-ttu-id="ae4a4-428">키 암호화 키가 hello 비대칭 키 (RSA 2048) tooprotect 사용 또는 hello 비밀을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="ae4a4-429">HSM(하드웨어 보안 모듈) 보호 키 또는 소프트웨어 보호 키를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="ae4a4-430">자세한 내용은 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="ae4a4-431">PS cmdlet</span><span class="sxs-lookup"><span data-stu-id="ae4a4-431">PS cmdlets</span></span> | <span data-ttu-id="ae4a4-432">[Azure PowerShell cmdlet](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="ae4a4-433">Azure Disk Encryption을 위한 Key Vault 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="ae4a4-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="ae4a4-434">Azure 디스크 암호화 보호 방법 hello 디스크 암호화 키와 키 저장소의 암호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="ae4a4-435">Azure 디스크 암호화에 대 한 주요 자격 증명 모음을 tooset, 전체 hello hello 다음 섹션의 각 단계 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="ae4a4-436">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="ae4a4-436">Create a key vault</span></span>
<span data-ttu-id="ae4a4-437">주요 자격 증명 모음 toocreate hello 다음 옵션 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="ae4a4-438">"101-Key-Vault-Create" Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="ae4a4-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="ae4a4-439">Azure PowerShell Key Vault cmdlet</span><span class="sxs-lookup"><span data-stu-id="ae4a4-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="ae4a4-440">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="ae4a4-440">Azure Resource Manager</span></span>
* <span data-ttu-id="ae4a4-441">어떻게 너무[주요 자격 증명 모음 보안](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-442">이미 설정한 경우 키 자격 증명 모음을 구독에 대 한, toohello 다음 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="ae4a4-444">주요 암호화 키 설정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="ae4a4-445">Hello BitLocker 암호화 키에 대 한 보안에 대 한 추가 수준의 대 한 toouse는 KEK를 원하는 경우 KEK tooyour 주요 자격 증명 모음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="ae4a4-446">사용 하 여 hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello 키 자격 증명 모음에 키 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="ae4a4-447">또한 온-프레미스 키 관리 HSM에서 KEK를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="ae4a4-448">자세한 내용은 [Key Vault 설명서](https://azure.microsoft.com/documentation/services/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="ae4a4-449">리소스 관리자 tooAzure 이동 하 여 또는 키 자격 증명 모음 인터페이스를 사용 하 여 hello KEK를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="ae4a4-451">Key Vault 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-451">Set key vault permissions</span></span>
<span data-ttu-id="ae4a4-452">hello Azure 플랫폼 있어야 액세스 toohello 암호화 키 또는 키 자격 증명 모음 toomake의 비밀을 사용할 수 있는 toohello VM 부팅 하 고 hello 볼륨의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="ae4a4-453">toogrant 권한 toohello Azure 플랫폼 집합 hello **EnabledForDiskEncryption** hello 주요 자격 증명 모음 PowerShell cmdlet을 사용 하 여 자격 증명 모음에 hello 키의 속성:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="ae4a4-454">Hello를 설정할 수도 있습니다 **EnabledForDiskEncryption** hello를 방문 하 여 속성 [Azure 리소스 탐색기](https://resources.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="ae4a4-455">Hello를 설정 해야 듯이, **EnabledForDiskEncryption** 주요 자격 증명 모음에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="ae4a4-456">그렇지 않으면 hello 배포가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="ae4a4-457">다음 그림과 같이 hello 주요 자격 증명 모음 인터페이스에서 Azure AD 응용 프로그램에 대 한 액세스 정책을 구성도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="ae4a4-460">Hello에 **고급 액세스 정책은** 탭, 주요 자격 증명 모음 Azure 디스크 암호화를 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="ae4a4-462">디스크 암호화 배포 시나리오 및 사용자 환경</span><span class="sxs-lookup"><span data-stu-id="ae4a4-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="ae4a4-463">많은 디스크 암호화 시나리오를 활성화 하 고 hello 단계 toohello 시나리오에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="ae4a4-464">hello 다음 섹션에서는 시나리오에 설명 hello 보다 자세히 설명에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="ae4a4-465">Hello Marketplace에서에서 생성 된 새 IaaS Vm에 대 한 암호화를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="ae4a4-466">Hello를 사용 하 여 hello azure에서 Marketplace에서에서 새 IaaS Windows VM에 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="ae4a4-467">Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="ae4a4-468">Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** 새 IaaS VM에 tooenable 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-469">이 템플릿은 Windows Server 2012 hello 갤러리 이미지를 사용 하는 새로운 암호화 된 Windows VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="ae4a4-470">이 [Resource Manager 템플릿](https://aka.ms/fde-rhel)을 사용하여 200GB RAID-0 배열이 있는 새 IaaS RedHat Linux 7.2 VM에서 디스크 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="ae4a4-471">Hello 서식 파일을 배포한 후 hello를 사용 하 여 hello VM 암호화 상태를 확인할 `Get-AzureRmVmDiskEncryptionStatus` 에 설명 된 대로 cmdlet [실행 중인 Linux VM의 OS 암호화 드라이브](#encrypting-os-drive-on-a-running-linux-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="ae4a4-472">Hello 컴퓨터의 상태를 반환 하는 경우 _VMRestartPending_, hello VM을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="ae4a4-473">hello 다음 표에 나타난 hello 리소스 관리자 템플릿 매개 변수 Azure AD 클라이언트 ID를 사용 하 여 hello 마켓플레이스 시나리오에서 새 Vm에 대 한.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="ae4a4-474">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae4a4-474">Parameter</span></span> | <span data-ttu-id="ae4a4-475">설명</span><span class="sxs-lookup"><span data-stu-id="ae4a4-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-476">adminUserName</span></span> | <span data-ttu-id="ae4a4-477">Hello 가상 컴퓨터에 대 한 관리 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="ae4a4-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="ae4a4-478">adminPassword</span></span> | <span data-ttu-id="ae4a4-479">Hello 가상 컴퓨터에 대 한 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="ae4a4-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-480">newStorageAccountName</span></span> | <span data-ttu-id="ae4a4-481">Hello 저장소 계정 toostore OS 및 데이터 Vhd의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="ae4a4-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="ae4a4-482">vmSize</span></span> | <span data-ttu-id="ae4a4-483">Hello VM의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-483">Size of hello VM.</span></span> <span data-ttu-id="ae4a4-484">현재 표준 A, D 및 G 시리즈만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="ae4a4-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-485">virtualNetworkName</span></span> | <span data-ttu-id="ae4a4-486">Hello 해당 hello VM NIC VNet의 이름에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="ae4a4-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-487">subnetName</span></span> | <span data-ttu-id="ae4a4-488">Hello hello VM NIC 해당 VNet에에서 hello 서브넷의 이름에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="ae4a4-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="ae4a4-489">AADClientID</span></span> | <span data-ttu-id="ae4a4-490">사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="ae4a4-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="ae4a4-491">AADClientSecret</span></span> | <span data-ttu-id="ae4a4-492">사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="ae4a4-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-493">keyVaultURL</span></span> | <span data-ttu-id="ae4a4-494">URL hello 키 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="ae4a4-495">Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="ae4a4-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="ae4a4-497">Hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL (선택 사항) BitLocker 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="ae4a4-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ae4a4-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="ae4a4-499">리소스 그룹 hello 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="ae4a4-500">vmName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-500">vmName</span></span> | <span data-ttu-id="ae4a4-501">Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="ae4a4-502">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="ae4a4-503">주요 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (암호 secret)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="ae4a4-504">고객 암호화 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="ae4a4-505">이 시나리오에서는 hello 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용 하 여 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="ae4a4-506">hello 다음 섹션에서는 큰 세부 hello 리소스 관리자 템플릿 및 CLI 명령에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="ae4a4-507">이 섹션에서는 Azure에서 사용할 수 있는 미리 암호화 된 이미지를 준비 하기 위한 중 하나에서 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="ae4a4-508">Hello 이미지를 만든 후 hello 단계 hello 다음 섹션 toocreate 암호화 된 Azure VM에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="ae4a4-509">사전에 암호화된 Windows VHD 준비</span><span class="sxs-lookup"><span data-stu-id="ae4a4-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="ae4a4-510">사전에 암호화된 Linux VHD 준비</span><span class="sxs-lookup"><span data-stu-id="ae4a4-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="ae4a4-511">Hello 리소스 관리자 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae4a4-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="ae4a4-512">Hello를 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="ae4a4-513">Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="ae4a4-514">Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 새 IaaS VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="ae4a4-515">hello 다음 표에 나타난 hello 리소스 관리자 템플릿 매개 변수 암호화 된 VHD에 대 한.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="ae4a4-516">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae4a4-516">Parameter</span></span> | <span data-ttu-id="ae4a4-517">설명</span><span class="sxs-lookup"><span data-stu-id="ae4a4-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-518">newStorageAccountName</span></span> | <span data-ttu-id="ae4a4-519">운영 체제 VHD 암호화 하는 hello 저장소 계정 toostore hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="ae4a4-520">이 저장소 계정은 이미 만들어야 hello에 동일한 리소스 그룹 및 VM hello와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="ae4a4-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="ae4a4-521">osVhdUri</span></span> | <span data-ttu-id="ae4a4-522">Hello 저장소 계정에서 hello OS VHD의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="ae4a4-523">osType</span><span class="sxs-lookup"><span data-stu-id="ae4a4-523">osType</span></span> | <span data-ttu-id="ae4a4-524">OS 제품 유형(Windows/Linux)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="ae4a4-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-525">virtualNetworkName</span></span> | <span data-ttu-id="ae4a4-526">Hello 해당 hello VM NIC VNet의 이름에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="ae4a4-527">hello 이름 해야 이미 만들어져 hello에 동일한 리소스 그룹 및 VM hello와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="ae4a4-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-528">subnetName</span></span> | <span data-ttu-id="ae4a4-529">Hello hello VM NIC 해당 VNet에 hello 서브넷의 이름에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="ae4a4-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="ae4a4-530">vmSize</span></span> | <span data-ttu-id="ae4a4-531">Hello VM의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-531">Size of hello VM.</span></span> <span data-ttu-id="ae4a4-532">현재 표준 A, D 및 G 시리즈만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="ae4a4-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="ae4a4-533">keyVaultResourceID</span></span> | <span data-ttu-id="ae4a4-534">Azure 리소스 관리자의 hello 주요 자격 증명 모음 리소스를 식별 하는 리소스 Id 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="ae4a4-535">Hello PowerShell cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="ae4a4-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="ae4a4-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="ae4a4-537">Hello 키 자격 증명 모음에 설정 된 hello 디스크 암호화 키의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="ae4a4-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="ae4a4-538">keyVaultKekUrl</span></span> | <span data-ttu-id="ae4a4-539">생성 된 hello 디스크 암호화 키를 암호화 하기 위한 hello 키 암호화 키의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="ae4a4-540">vmName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-540">vmName</span></span> | <span data-ttu-id="ae4a4-541">Hello IaaS VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="ae4a4-542">PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="ae4a4-543">Hello PowerShell cmdlet을 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="ae4a4-544">CLI 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-544">Using CLI commands</span></span>
<span data-ttu-id="ae4a4-545">CLI 명령을 사용 하 여이 시나리오에 대 한 디스크 암호화 tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-546">Key Vault에 대한 액세스 정책 설정:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="ae4a4-547">집합 hello **EnabledForDiskEncryption** 플래그:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="ae4a4-548">사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="ae4a4-549">기존 또는 실행 중인 VM, 형식에서 tooenable 암호화:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="ae4a4-550">암호화 상태 가져오기:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="ae4a4-551">암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="ae4a4-552">Azure에서 기존 또는 실행 중인 IaaS Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="ae4a4-553">이 시나리오에서는 hello 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용 하 여 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="ae4a4-554">hello 다음 섹션에 설명 자세히 어떻게 리소스 관리자 템플릿 및 CLI 명령을 사용 하 여 hello tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="ae4a4-555">Hello 리소스 관리자 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae4a4-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="ae4a4-556">디스크 암호화 기존 컨트롤이 나 hello를 사용 하 여 Azure에서 IaaS Windows Vm 실행에 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="ae4a4-557">Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="ae4a4-558">Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 기존 컨트롤이 나 IaaS VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="ae4a4-559">hello 다음 표에 나타난 기존 컨트롤이 나 실행 중인 Azure AD 클라이언트 ID를 사용 하는 Vm에 대 한 hello 리소스 관리자 템플릿 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="ae4a4-560">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae4a4-560">Parameter</span></span> | <span data-ttu-id="ae4a4-561">설명</span><span class="sxs-lookup"><span data-stu-id="ae4a4-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="ae4a4-562">AADClientID</span></span> | <span data-ttu-id="ae4a4-563">사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="ae4a4-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="ae4a4-564">AADClientSecret</span></span> | <span data-ttu-id="ae4a4-565">사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="ae4a4-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-566">keyVaultName</span></span> | <span data-ttu-id="ae4a4-567">Hello 키의 이름 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="ae4a4-568">Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="ae4a4-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="ae4a4-570">BitLocker 키를 생성 한 hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="ae4a4-571">이 매개 변수는 선택 하는 경우 선택적 **nokek** hello UseExistingKek 드롭 다운 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="ae4a4-572">선택 하는 경우 **kek** hello UseExistingKek 드롭 다운 목록에서 hello를 입력 해야 _keyEncryptionKeyURL_ 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="ae4a4-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="ae4a4-573">volumeType</span></span> | <span data-ttu-id="ae4a4-574">Hello 암호화 작업이 수행 되는 볼륨의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="ae4a4-575">유효한 값은 _OS_, _Data_ 및 _All_입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="ae4a4-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="ae4a4-576">sequenceVersion</span></span> | <span data-ttu-id="ae4a4-577">Hello BitLocker 작업의 시퀀스 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="ae4a4-578">Hello에서 디스크 암호화 연산이 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="ae4a4-579">vmName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-579">vmName</span></span> | <span data-ttu-id="ae4a4-580">Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="ae4a4-581">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="ae4a4-582">Hello 키 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (BitLocker 암호화 암호)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="ae4a4-583">PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="ae4a4-584">PowerShell cmdlet을 사용 하 여 Azure 디스크 암호화를 사용 하 여 암호화를 사용 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [1 부-Azure PowerShell을 사용한 Azure 디스크 암호화 탐색](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [탐색 Azure 디스크 암호화 Azure powershell-2 부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="ae4a4-585">CLI 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-585">Using CLI commands</span></span>
<span data-ttu-id="ae4a4-586">기존 컨트롤이 나 CLI 명령을 사용 하 여 Azure에서 IaaS Windows VM 실행에 tooenable 암호화 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-587">tooset hello 키 자격 증명 모음에 대 한 액세스 정책:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="ae4a4-588">집합 hello **EnabledForDiskEncryption** 플래그:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="ae4a4-589">사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="ae4a4-590">기존 또는 실행 중인 VM에서 tooenable 암호화:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="ae4a4-591">tooget 암호화 상태:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="ae4a4-592">암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="ae4a4-593">Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="ae4a4-594">Hello를 사용 하 여 Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="ae4a4-595">클릭 **tooAzure 배포** hello Azure 빠른 시작 서식 파일에 hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="ae4a4-596">Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 기존 컨트롤이 나 IaaS VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="ae4a4-597">다음 표에서 hello 기존 컨트롤이 나 실행 중인 Azure AD 클라이언트 ID를 사용 하는 Vm에 대 한 리소스 관리자 템플릿 매개 변수를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="ae4a4-598">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae4a4-598">Parameter</span></span> | <span data-ttu-id="ae4a4-599">설명</span><span class="sxs-lookup"><span data-stu-id="ae4a4-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="ae4a4-600">AADClientID</span></span> | <span data-ttu-id="ae4a4-601">사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="ae4a4-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="ae4a4-602">AADClientSecret</span></span> | <span data-ttu-id="ae4a4-603">사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="ae4a4-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-604">keyVaultName</span></span> | <span data-ttu-id="ae4a4-605">Hello 키의 이름 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="ae4a4-606">Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="ae4a4-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="ae4a4-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="ae4a4-608">BitLocker 키를 생성 한 hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="ae4a4-609">이 매개 변수는 선택 하는 경우 선택적 **nokek** hello UseExistingKek 드롭 다운 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="ae4a4-610">선택 하는 경우 **kek** hello UseExistingKek 드롭 다운 목록에서 hello를 입력 해야 _keyEncryptionKeyURL_ 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="ae4a4-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="ae4a4-611">volumeType</span></span> | <span data-ttu-id="ae4a4-612">Hello 암호화 작업이 수행 되는 볼륨의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="ae4a4-613">지원되는 유효한 값은 _OS_ 또는 _All_(RHEL 7.2, CentOS 7.2, Ubuntu 16.04의 경우)이고 다른 모든 배포판의 경우 _Data_입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="ae4a4-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="ae4a4-614">sequenceVersion</span></span> | <span data-ttu-id="ae4a4-615">Hello BitLocker 작업의 시퀀스 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="ae4a4-616">Hello에서 디스크 암호화 연산이 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="ae4a4-617">vmName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-617">vmName</span></span> | <span data-ttu-id="ae4a4-618">Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="ae4a4-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="ae4a4-619">passPhrase</span></span> | <span data-ttu-id="ae4a4-620">Hello 데이터 암호화 키로 강력한 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="ae4a4-621">_KeyEncryptionKeyURL_은 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="ae4a4-622">주요 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (암호 secret)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="ae4a4-623">CLI 명령</span><span class="sxs-lookup"><span data-stu-id="ae4a4-623">CLI commands</span></span>
<span data-ttu-id="ae4a4-624">설치 하 고 hello를 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [CLI 명령을](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="ae4a4-625">기존 컨트롤이 나 CLI 명령을 사용 하 여 Azure에서 IaaS Linux Vm을 실행 중인 tooenable 암호화 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-626">Hello 키 자격 증명 모음에 액세스 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="ae4a4-627">집합 hello **EnabledForDiskEncryption** 플래그:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="ae4a4-628">사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="ae4a4-629">기존 또는 실행 중인 VM에서 tooenable 암호화:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="ae4a4-630">암호화 상태 가져오기:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="ae4a4-631">암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="ae4a4-632">암호화 된 IaaS VM의 hello 암호화 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="ae4a4-633">Azure 리소스 관리자를 사용 하 여 hello 암호화 상태를 가져올 수 있습니다 [PowerShell cmdlet](/powershell/azure/overview), 또는 CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="ae4a4-634">다음 섹션 hello 어떻게 toouse hello Azure 클래식 포털 및 CLI 명령 tooget hello 암호화 상태를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="ae4a4-635">Azure 리소스 관리자를 사용 하 여 암호화 된 Windows VM의 hello 암호화 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="ae4a4-636">Hello 다음을 수행 하 여 hello IaaS VM의 hello 암호화 상태를 Azure 리소스 관리자에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="ae4a4-637">Toohello 로그인 [Azure 클래식 포털](https://portal.azure.com/), 클릭 하 고 **가상 컴퓨터** hello 왼쪽된 창 toosee hello 구독의 가상 컴퓨터의 요약 보기에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="ae4a4-638">Hello에 hello 구독 이름을 선택 하 여 hello 가상 컴퓨터 보기를 필터링 할 수 **구독** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="ae4a4-639">Hello의 hello 위쪽 **가상 컴퓨터** 페이지 **열**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="ae4a4-640">Hello에 **선택 열** 블레이드를 **디스크 암호화**, 클릭 하 고 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="ae4a4-641">Hello 디스크 암호화 열 보여 주는 hello 암호화 상태 표시 되어야 _Enabled_ 또는 _해제_ hello 다음 그림에에서 나와 있는 것 처럼 각 VM에 대해:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="ae4a4-643">Hello 디스크 암호화 PowerShell cmdlet을 사용 하 여 암호화 된 IaaS VM (Windows/Linux)의 hello 암호화 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="ae4a4-644">Hello 디스크 암호화 PowerShell cmdlet에서 hello IaaS VM의 hello 암호화 상태를 가져올 수 있습니다 `Get-AzureRmVMDiskEncryptionStatus`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="ae4a4-645">VM에 대 한 tooget hello 암호화 설정을 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="ae4a4-646">hello 출력을 검사할 수 _Get AzureRmVMDiskEncryptionStatus_ 암호화에 대 한 Url을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="ae4a4-647">OSVolumeEncrypted hello 및 DataVolumesEncrypted 설정 값을 보여 주 Azure 디스크 암호화를 사용 하 여 두 볼륨 암호화 된 too_Encrypted_ 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="ae4a4-648">PowerShell cmdlet을 사용 하 여 Azure 디스크 암호화를 사용 하 여 암호화를 사용 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [1 부-Azure PowerShell을 사용한 Azure 디스크 암호화 탐색](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [탐색 Azure 디스크 암호화 Azure powershell-2 부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-649">Linux Vm에서 hello에 대 한 3 toofour 분 걸리는 `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello 암호화 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="ae4a4-650">Hello 디스크 암호화 CLI 명령에서 hello IaaS VM의 hello 암호화 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="ae4a4-651">Hello 디스크 암호화 CLI 명령을 사용 하 여 hello IaaS VM의 hello 암호화 상태를 가져올 수 있습니다 `azure vm show-disk-encryption-status`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="ae4a4-652">VM에 대 한 tooget hello 암호화 설정을 Azure CLI 세션을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="ae4a4-653">실행 중인 Windows IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="ae4a4-654">Hello Azure 디스크 암호화 리소스 관리자 템플릿 또는 PowerShell cmdlet을 통해 실행 중인 Windows 또는 Linux IaaS VM에 대 한 암호화를 사용 하지 않도록 설정할 수 있으며 hello 암호 해독 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="ae4a4-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="ae4a4-655">Windows VM</span></span>
<span data-ttu-id="ae4a4-656">hello 사용 안 함 암호화 단계는 hello OS, hello 데이터 볼륨에 또는 둘 다 Windows IaaS VM을 실행 하는 hello의 암호화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="ae4a4-657">Hello OS 볼륨을 사용 하지 않도록 설정 하 고 hello 데이터 볼륨이 암호화 된 상태로 둡니다 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="ae4a4-658">Hello 암호화 사용 안 함 작업을 수행 하는 경우 hello Azure 클래식 배포 모델 hello VM 서비스 모델을 업데이트 하 고 IaaS VM Windows hello를 암호 해독 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="ae4a4-659">hello VM의 hello 콘텐츠는 더 이상 휴지 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="ae4a4-660">hello 암호 해독 경우 키 자격 증명 모음 및 hello 암호화 키 자료 (Windows 및 Linux에 대 한 암호에 대 한 BitLocker 암호화 키)를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="ae4a4-661">Linux VM</span><span class="sxs-lookup"><span data-stu-id="ae4a4-661">Linux VM</span></span>
<span data-ttu-id="ae4a4-662">hello 사용 안 함 암호화 단계는 Linux IaaS VM을 실행 하는 hello에 hello 데이터 볼륨의 암호화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="ae4a4-663">이 단계는 hello OS 디스크 암호화 되지 않은 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-664">Hello OS 디스크에 대 한 암호화를 사용 하지 않으면 Linux Vm에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="ae4a4-665">기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="ae4a4-666">Hello를 사용 하 여 실행 중인 Windows IaaS Vm에 디스크 암호화를 비활성화할 수 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="ae4a4-667">Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호 해독 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="ae4a4-668">Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** 새 IaaS VM에 tooenable 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="ae4a4-669">Linux Vm에 대 한 hello를 사용 하 여 암호화를 비활성화할 수 [실행 중인 Linux VM에 대 한 암호화를 사용 하지 않도록 설정](https://aka.ms/decrypt-linuxvm) 템플릿.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="ae4a4-670">hello 다음 표에서 실행 중인 IaaS VM에 대 한 암호화를 사용 하지 않도록 설정 하는 것에 대 한 리소스 관리자 템플릿 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="ae4a4-671">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae4a4-671">Parameter</span></span> | <span data-ttu-id="ae4a4-672">설명</span><span class="sxs-lookup"><span data-stu-id="ae4a4-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae4a4-673">vmName</span><span class="sxs-lookup"><span data-stu-id="ae4a4-673">vmName</span></span> | <span data-ttu-id="ae4a4-674">Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="ae4a4-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="ae4a4-675">volumeType</span></span> | <span data-ttu-id="ae4a4-676">암호 해독 작업을 수행할 볼륨의 유형.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="ae4a4-677">유효한 값은 _OS_, _Data_ 및 _All_입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="ae4a4-678">Hello에 대 한 암호화를 사용 하지 않도록 설정 하지 않고 Windows IaaS VM OS/부팅 볼륨 실행에 대 한 암호화를 비활성화할 수 없습니다 _데이터_ 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="ae4a4-679">또한 Linux Vm에서 hello OS 디스크에 암호화 사용 안 함은 허용 되지 않음을 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="ae4a4-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="ae4a4-680">sequenceVersion</span></span> | <span data-ttu-id="ae4a4-681">Hello BitLocker 작업의 시퀀스 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="ae4a4-682">Hello에 디스크 암호 해독 작업은 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="ae4a4-683">기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="ae4a4-684">hello PowerShell cmdlet을 사용 하 여 기존 또는 실행 중인 IaaS VM에 toodisable 암호화 참조 [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="ae4a4-685">이 cmdlet에는 Windows 및 Linux VM을 둘 다 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="ae4a4-686">toodisable 암호화 hello 가상 컴퓨터 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="ae4a4-687">경우 hello _이름_ 매개 변수를 지정 하지 않으면 hello 기본 이름에 확장명 _Windows Vm에 대 한 AzureDiskEncryption_ 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="ae4a4-688">Linux Vm에서 hello AzureDiskEncryptionForLinux 확장 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4a4-689">이 cmdlet hello 가상 컴퓨터를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="ae4a4-690">Azure 관리 디스크를 사용하여 미리 암호화된 IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="ae4a4-691">Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate hello ARM 템플릿을 사용 하 여 미리 암호화 된 VHD에서 암호화 된 VM에 있는 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="ae4a4-692">[미리 암호화된 VHD/저장소 BLOB를 통해 암호화된 관리 디스크 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="ae4a4-693">Azure 관리 디스크를 사용하여 새로운 Linux IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="ae4a4-694">Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate 새 Linux IaaS VM에 있는 hello ARM 템플릿을 사용 하 여 암호화를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae4a4-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="ae4a4-695">[전체 디스크 암호화를 사용하여 RHEL 7.2 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="ae4a4-696">Azure 관리 디스크를 사용하여 새로운 Windows IaaS VM에 대한 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="ae4a4-697">Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate 새 Linux IaaS VM에 있는 hello ARM 템플릿을 사용 하 여 암호화를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae4a4-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="ae4a4-698">[갤러리 이미지로 암호화된 Windows IaaS 관리 디스크 VM 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="ae4a4-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="ae4a4-699">외부 VM 인스턴스 및 이전 tooenabling Azure 디스크 암호화 백업 관리 되는 디스크 기반 이거나 필수 toosnapshot는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="ae4a4-700">Hello 관리 되는 디스크의 스냅숏을 hello 포털에서 가져올 수 있습니다 또는 Azure 백업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="ae4a4-701">백업을은 암호화 하는 동안 복구 옵션 hello 경우 예기치 않은 실패의 가능한 지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="ae4a4-702">백업이 만들어지지 면 hello 집합 AzureRmVMDiskEncryptionExtension cmdlet hello-skipVmBackup 매개 변수를 지정 하 여 관리 되는 사용 되는 tooencrypt 디스크를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="ae4a4-703">이 명령은 백업을 만들고 이 매개 변수가 지정될 때까지 관리 디스크 기반 VM에 대해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="ae4a4-704">기존의 암호화된 프리미엄 이외 VM의 암호화 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae4a4-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="ae4a4-705">Hello 기존 Azure 디스크 암호화를 지원 인터페이스 사용 [PS cmdlet, CLI 또는 ARM 템플릿] VM tooupdate hello 암호화 설정을 실행 하기 위한 AAD 클라이언트 ID/비밀 키 암호화 키 [KEK]에 대 한 암호 또는 Windows VM에 대 한 BitLocker 암호화 키와 같은 Linux VM 등 hello 업데이트 암호화 설정은 프리미엄 저장소에서 지원 되는 Vm에 대해서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="ae4a4-706">Premium Storage에서 지원하는 VM에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="ae4a4-707">부록</span><span class="sxs-lookup"><span data-stu-id="ae4a4-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="ae4a4-708">Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="ae4a4-708">Connect tooyour subscription</span></span>
<span data-ttu-id="ae4a4-709">계속 진행 하기 전에 검토 hello *필수 구성 요소* 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="ae4a4-710">모든 필수 조건이 충족 되었는지 확인 한 후 hello 다음을 수행 하 여 tooyour 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="ae4a4-711">Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="ae4a4-712">구독이 여러 개 있고 toospecify 하나의 toouse 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="ae4a4-713">toouse, 원하는 toospecify hello 구독 유형:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="ae4a4-714">구성 된 hello 구독 올바른지 tooverify, 유형:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="ae4a4-715">tooconfirm hello Azure 디스크 암호화 cmdlet이 설치 유형:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="ae4a4-716">다음 출력 hello hello Azure 디스크 암호화 PowerShell 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="ae4a4-717">사전에 암호화된 Windows VHD 준비</span><span class="sxs-lookup"><span data-stu-id="ae4a4-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="ae4a4-718">hello 다음 섹션에서는 필요한 tooprepare Azure IaaS에서 암호화 된 VHD로 배포를 위한 Windows VHD 사전에 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="ae4a4-719">새 Windows VM (VHD) Azure 또는 Azure Site Recovery에서 부팅 및 정보 tooprepare hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="ae4a4-720">그룹 정책 tooallow 비 TPM 보호 운영 체제에 대 한 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae4a4-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="ae4a4-721">Hello BitLocker 그룹 정책 설정을 구성 **BitLocker 드라이브 암호화**, 아래에서 찾을 수 있는 **로컬 컴퓨터 정책** > **컴퓨터 구성**  >  **관리 템플릿** > **Windows 구성 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="ae4a4-722">이 설정을 너무 변경할**운영 체제 드라이브** > **시작 시 추가 인증을 요구** > **호환되는TPM없이BitLocker허용**hello 다음 그림에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="ae4a4-724">BitLocker 기능 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="ae4a4-724">Install BitLocker feature components</span></span>
<span data-ttu-id="ae4a4-725">Windows Server 2012 이상 버전에서는 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="ae4a4-726">Windows Server 2008 r 2에 대 한 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="ae4a4-727">Hello OS 볼륨을 사용 하 여 BitLocker를 위한 준비`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="ae4a4-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="ae4a4-728">toocompress OS 파티션 hello 및 BitLocker에 대 한 hello 컴퓨터를 준비, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="ae4a4-729">BitLocker를 사용 하 여 hello OS 볼륨 보호</span><span class="sxs-lookup"><span data-stu-id="ae4a4-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="ae4a4-730">사용 하 여 hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) 는 외부 키 보호기를 사용 하 여 hello 부팅 볼륨에 명령 tooenable 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="ae4a4-731">또한 hello 외부 키 (.bek 파일) hello 외장형 드라이브 또는 볼륨에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="ae4a4-732">암호화는 hello 다음 다시 부팅 후 hello 시스템/부팅 볼륨에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="ae4a4-733">BitLocker를 사용 하 여 hello 외부 키를 가져오기 위한 별도 데이터/리소스 VHD와 VM hello를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="ae4a4-734">실행 중인 Linux VM에서 OS 드라이브 암호화</span><span class="sxs-lookup"><span data-stu-id="ae4a4-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="ae4a4-735">실행 중인 Linux VM에는 운영 체제 드라이브의 암호화 hello 분포 뒤에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="ae4a4-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="ae4a4-736">RHEL 7.2</span></span>
* <span data-ttu-id="ae4a4-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="ae4a4-737">CentOS 7.2</span></span>
* <span data-ttu-id="ae4a4-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="ae4a4-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="ae4a4-739">OS 디스크 암호화를 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="ae4a4-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="ae4a4-740">Azure 리소스 관리자의 hello 마켓플레이스 이미지 로부터 hello VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="ae4a4-741">4GB 이상의 RAM이 있는 Azure VM(권장 크기는 7GB)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="ae4a4-742">(RHEL 및 CentOS) SELinux를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="ae4a4-743">toodisable SELinux, 참조 "4.4.2 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="ae4a4-744">사용할 수 없도록 SELinux"hello [SELinux 사용자 및 관리자의 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) hello VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="ae4a4-745">SELinux 해제 한 후 한 번 이상 hello VM 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="ae4a4-746">단계</span><span class="sxs-lookup"><span data-stu-id="ae4a4-746">Steps</span></span>
1. <span data-ttu-id="ae4a4-747">이전에 지정한 hello 분포 중 하나를 사용 하 여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="ae4a4-748">CentOS 7.2의 경우 특수 이미지를 통해 OS 디스크 암호화가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="ae4a4-749">toouse 이미지이 hello VM을 만들 때 SKU hello 대로 "7.2n"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="ae4a4-750">Tooyour 요구에 따라 hello VM을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="ae4a4-751">것 tooencrypt 모든 hello (OS + 데이터) 드라이브를 지정 및 /etc/fstab에서 탑재 가능한 hello 데이터 드라이브 toobe를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="ae4a4-752">UUID를 사용 하 여 데이터 드라이브/등/fstab hello 블록 장치 이름 (예를 들어 /dev/sdb1)를 지정 하는 대신에 toospecify =....</span><span class="sxs-lookup"><span data-stu-id="ae4a4-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="ae4a4-753">암호화 하는 동안 VM hello 드라이브의 hello 순서가 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="ae4a4-754">Toomount 못합니다 VM 블록 장치의 특정 순서를 사용 하는 경우 암호화 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="ae4a4-755">세션 로그 아웃 한 hello SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="ae4a4-756">tooencrypt hello OS를 지정으로 volumeType **모든** 또는 **OS** 때 있습니다 [암호화 사용](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="ae4a4-757">`systemd` 서비스로 실행되지 않는 모든 사용자 공간 프로세스는 `SIGKILL`로 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="ae4a4-758">Hello VM 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-758">Reboot hello VM.</span></span> <span data-ttu-id="ae4a4-759">실행 중인 VM에서 OS 디스크 암호화를 사용할 경우 VM의 가동 중지 시간을 계획하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="ae4a4-760">주기적으로 hello에 hello 지침을 사용 하 여 암호화 hello 진행률을 모니터링할 [절로](#monitoring-os-encryption-progress)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="ae4a4-761">Get AzureRmVmDiskEncryptionStatus "VMRestartPending" 표시 되 면 tooit에 로그인 하거나 hello 포털, PowerShell 또는 CLI를 사용 하 여 VM 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="ae4a4-762">컴퓨터를 다시 부팅 하기 전에 저장 하는 것이 좋습니다 [진단 부팅](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) hello VM의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="ae4a4-763">OS 암호화 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="ae4a4-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="ae4a4-764">OS 암호화 진행 상태를 모니터링하는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="ae4a4-765">사용 하 여 hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet hello ProgressMessage 필드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="ae4a4-766">약 40 hello VM이 "운영 체제는 시작 하는 암호화 디스크"에 도달 하면 후 걸리는 too50 분 프리미엄 저장소에서 VM을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="ae4a4-767">WALinuxAgent에서 [문제 #388](https://github.com/Azure/WALinuxAgent/issues/388)으로 인해 일부 배포판에서 `OsVolumeEncrypted` 및 `DataVolumesEncrypted`가 `Unknown`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="ae4a4-768">WALinuxAgent 2.1.5 버전 이상에서는 이 문제가 자동으로 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="ae4a4-769">표시 되 면 `Unknown` hello 출력에 hello Azure 리소스 탐색기를 사용 하 여 디스크 암호화 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="ae4a4-770">너무 이동[Azure 리소스 탐색기](https://resources.azure.com/), 한 다음 왼쪽에 hello 선택 패널에서이 계층 구조를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

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

 <span data-ttu-id="ae4a4-771">Hello InstanceView, toosee 드라이브의 암호화 상태를 hello 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![VM 인스턴스 보기](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="ae4a4-773">[부트 진단](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="ae4a4-774">Hello 이름 확장 프로그램에서에서 메시지를 접두사로와 야 `[AzureDiskEncryption]`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="ae4a4-775">Toohello SSH 통해 VM에에서 로그인 하 고 hello 확장 로그에서 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="ae4a4-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="ae4a4-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="ae4a4-777">서명 하지 않은 toohello VM의에서 OS 암호화가 진행 중인 동안 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="ae4a4-778">Hello 다른 두 가지 방법은 실패 한 경우에 hello 로그를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="ae4a4-779">사전에 암호화된 Linux VHD 준비</span><span class="sxs-lookup"><span data-stu-id="ae4a4-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="ae4a4-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="ae4a4-780">Ubuntu 16</span></span>
<span data-ttu-id="ae4a4-781">Hello 다음을 수행 하 여 hello 배포 설치 중에 암호화를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="ae4a4-782">선택 **암호화 된 볼륨 구성** hello 디스크를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="ae4a4-784">암호화되지 않아야 하는 별도의 부트 드라이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="ae4a4-785">루트 드라이브를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="ae4a4-787">암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-787">Provide a passphrase.</span></span> <span data-ttu-id="ae4a4-788">Toohello 주요 자격 증명 모음을 업로드 하는 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="ae4a4-790">분할을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="ae4a4-792">Hello VM 부팅 하 고 암호를 요구 하는 경우 3 단계에서 제공 하는 hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="ae4a4-794">VM hello를 사용 하 여 Azure에 업로드 하기 위한 준비 [이러한 지침](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="ae4a4-795">Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="ae4a4-796">Hello 다음을 수행 하 여 Azure를 사용한 암호화 toowork를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="ae4a4-797">다음 스크립트는 hello hello 콘텐츠와 함께 /usr/local/sbin/azure_crypt_key.sh, 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="ae4a4-798">Azure에서 사용 하는 hello 암호 파일 이름 이므로 주의 toohello KeyFileName, 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="ae4a4-799">Hello crypt 구성에서 변경 */등/crypttab*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="ae4a4-800">다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="ae4a4-801">편집 하는 경우 *azure_crypt_key.sh* Windows에서 복사한 실행 tooLinux `dos2unix /usr/local/sbin/azure_crypt_key.sh`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="ae4a4-802">Toohello 스크립트 실행 권한을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="ae4a4-803">줄을 추가하여 */etc/initramfs-tools/modules*를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="ae4a4-804">실행 `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="ae4a4-805">이제 VM hello를 프로 비전 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-805">Now you can deprovision hello VM.</span></span>

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="ae4a4-807">Toohello 다음 단계를 계속 하 고 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="ae4a4-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="ae4a4-808">openSUSE 13.2</span></span>
<span data-ttu-id="ae4a4-809">tooconfigure hello 배포 설치 중에 암호화 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="ae4a4-810">Hello 디스크를 분할 하는 경우 선택 **볼륨 그룹 암호화**, 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="ae4a4-811">이 hello 암호 tooyour 주요 자격 증명 모음을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="ae4a4-813">암호를 사용 하 여 VM hello를 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-813">Boot hello VM using your password.</span></span>

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="ae4a4-815">준비 tooAzure hello 지침에 따라 업로드 하기 위한 VM hello [SLES 또는 openSUSE 가상 컴퓨터를 Azure에 대 한 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="ae4a4-816">Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="ae4a4-817">Azure 통해 암호화 toowork tooconfigure 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="ae4a4-818">Hello /etc/dracut.conf 편집한 hello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="ae4a4-819">Hello hello 끝날 때이 줄 주석 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="ae4a4-820">Hello 다음 hello 파일 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 맨 앞에 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="ae4a4-821">다음 항목을 그 아래 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="ae4a4-822">to:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="ae4a4-823">/Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 편집한 너무 추가할 "# 열기 LUKS 장치":</span><span class="sxs-lookup"><span data-stu-id="ae4a4-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="ae4a4-824">실행 `/usr/sbin/dracut -f -v` tooupdate hello initrd 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="ae4a4-825">프로 비전 해제할 수 이제 VM hello 및 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="ae4a4-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="ae4a4-826">CentOS 7</span></span>
<span data-ttu-id="ae4a4-827">tooconfigure hello 배포 설치 중에 암호화 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="ae4a4-828">디스크를 분할할 때 **내 데이터 암호화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="ae4a4-830">루트 파티션에 대해 **암호화**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="ae4a4-832">암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-832">Provide a passphrase.</span></span> <span data-ttu-id="ae4a4-833">이 hello 암호 tooyour 주요 자격 증명 모음을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="ae4a4-835">Hello VM 부팅 하 고 암호를 요구 하는 경우 3 단계에서 제공 하는 hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="ae4a4-837">hello "CentOS 7.0 이상" 지침을 사용 하 여 Azure에 업로드 하기 위한 준비 hello VM [CentOS 기반 가상 컴퓨터를 Azure에 대 한 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="ae4a4-838">Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="ae4a4-839">프로 비전 해제할 수 이제 VM hello 및 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="ae4a4-840">Azure 통해 암호화 toowork tooconfigure 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="ae4a4-841">Hello /etc/dracut.conf 편집한 hello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="ae4a4-842">Hello hello 끝날 때이 줄 주석 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일:</span><span class="sxs-lookup"><span data-stu-id="ae4a4-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="ae4a4-843">Hello 다음 hello 파일 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 맨 앞에 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="ae4a4-844">다음 항목을 그 아래 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="ae4a4-845">to</span><span class="sxs-lookup"><span data-stu-id="ae4a4-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="ae4a4-846">/Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh를 편집 하 고 hello "# 열기 LUKS 장치" 뒤에이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="ae4a4-847">Hello 실행 "/ usr/sbin/dracut-f-v" tooupdate hello initrd 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="ae4a4-849">암호화 된 VHD tooan Azure 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="ae4a4-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="ae4a4-850">BitLocker 암호화 또는 DM Crypt 암호화 사용 하도록 설정한 후 hello 로컬 VHD 요구 업로드 toobe tooyour 저장소 계정을 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="ae4a4-851">Hello 미리 암호화 된 VM tooyour 주요 자격 증명 모음에 대 한 hello 디스크 암호화 암호를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="ae4a4-852">이전에 가져온 hello 디스크 암호화 암호 키 저장소의 암호로 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="ae4a4-853">hello 주요 자격 증명 모음 toohave 디스크 암호화 및 Azure AD 클라이언트에서 사용 하도록 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="ae4a4-854">KEK로 암호화되지 않은 디스크 암호화 암호</span><span class="sxs-lookup"><span data-stu-id="ae4a4-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="ae4a4-855">키 저장소를 사용 하 여의 hello 보안을 tooset [집합 AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="ae4a4-856">Windows 가상 컴퓨터를 설정한 경우 hello bek base64 문자열로 인코딩된 파일과 tooyour 주요 자격 증명 모음 hello를 사용 하 여 업로드 된 다음 `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="ae4a4-857">Linux 용 hello 암호 base64 문자열로 인코딩한 다음 toohello 주요 자격 증명 모음을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="ae4a4-858">또한 있는지 확인 하십시오 hello 키 자격 증명 모음에 hello 암호를 만들 때 해당 hello 태그 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="ae4a4-859">사용 하 여 hello `$secretUrl` hello에 대 한 다음 단계에서 [KEK를 사용 하지 않고 hello OS 디스크를 연결](#without-using-a-kek)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="ae4a4-860">KEK로 암호화된 디스크 암호화 암호</span><span class="sxs-lookup"><span data-stu-id="ae4a4-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="ae4a4-861">Hello 비밀 toohello 자격 증명 모음 키를 업로드 하기 전에 키 암호화 키를 사용 하 여 선택적으로 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="ae4a4-862">사용 하 여 hello 래핑 [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst hello 키 암호화 키를 사용 하 여 hello 보안을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="ae4a4-863">hello이 wrap 작업의 출력은 hello를 사용 하 여 비밀으로 업로드할 수 있습니다 하는 base64 인코딩된 URL 문자열을 [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
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

<span data-ttu-id="ae4a4-864">사용 하 여 `$KeyEncryptionKey` 및 `$secretUrl` hello에 대 한 다음 단계에서 [KEK를 사용 하 여 hello OS 디스크를 연결](#using-a-kek)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="ae4a4-865">OS 디스크를 연결할 때 비밀 URL 지정</span><span class="sxs-lookup"><span data-stu-id="ae4a4-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="ae4a4-866">KEK 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae4a4-866">Without using a KEK</span></span>
<span data-ttu-id="ae4a4-867">Toopass hello OS 디스크를 연결 하는 동안 필요한 `$secretUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="ae4a4-868">hello URL hello "디스크 암호화 암호는 KEK를 사용 하 여 암호화 되지 않습니다." 섹션에 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="ae4a4-869">KEK 사용</span><span class="sxs-lookup"><span data-stu-id="ae4a4-869">Using a KEK</span></span>
<span data-ttu-id="ae4a4-870">Hello OS 디스크를 연결할 경우 전달 `$KeyEncryptionKey` 및 `$secretUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="ae4a4-871">hello URL hello "디스크 암호화 암호는 KEK를 사용 하 여 암호화 되지 않습니다." 섹션에 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="ae4a4-872">이 가이드 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae4a4-872">Download this guide</span></span>
<span data-ttu-id="ae4a4-873">Hello에서이 가이드를 다운로드할 수 있습니다 [TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4a4-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="ae4a4-874">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="ae4a4-874">For more information</span></span>
[<span data-ttu-id="ae4a4-875">Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 1부</span><span class="sxs-lookup"><span data-stu-id="ae4a4-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="ae4a4-876">Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부</span><span class="sxs-lookup"><span data-stu-id="ae4a4-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
