---
title: "Azure Disk Encryption 문제 해결| Microsoft Docs"
description: "이 문서에서는 Windows 및 Linux IaaS VM용 Microsoft Azure Disk Encryption에 대한 문제 해결 팁을 제공합니다."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 5f482a92b8fcd71a1b767fcc5741bc57605997ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a><span data-ttu-id="4862d-103">Azure Disk Encryption 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4862d-103">Azure Disk Encryption Troubleshooting Guide</span></span>

<span data-ttu-id="4862d-104">이 가이드는 조직에서 Azure Disk Encryption을 사용하고 디스크 암호화 관련 문제를 해결하기 위한 지침이 필요한 IT(정보 기술) 전문가, 정보 보안 분석가 및 클라우드 관리자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure disk encryption and need guidance to troubleshoot disk-encryption related issues.</span></span>

## <a name="troubleshooting-linux-os-disk-encryption"></a><span data-ttu-id="4862d-105">Linux OS 디스크 암호화 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4862d-105">Troubleshooting Linux OS disk encryption</span></span>

<span data-ttu-id="4862d-106">Linux OS 디스크 암호화에서는 전체 디스크 암호화 프로세스를 실행하기 전에 OS 드라이브를 분리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-106">Linux OS disk encryption must unmount the OS drive prior to running it through the full disk encryption process.</span></span>   <span data-ttu-id="4862d-107">불가능한 경우 "... 후 분리하지 못했습니다."라는</span><span class="sxs-lookup"><span data-stu-id="4862d-107">If it cannot, an error message of "failed to unmount after…"</span></span> <span data-ttu-id="4862d-108">오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-108">error message is likely to occur.</span></span>

<span data-ttu-id="4862d-109">이는 지원되는 재고 갤러리 이미지에서 수정되거나 변경된 대상 VM 환경에서 OS 디스크 암호화를 시도할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-109">This is most likely when OS disk encryption is attempted on a target VM environment that has been modified or changed from its supported stock gallery image.</span></span>  <span data-ttu-id="4862d-110">OS 확장을 분리하는 확장의 기능을 방해할 수 있는 지원되는 이미지로부터의 편차 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-110">Examples of deviations from the supported image, which can interfere with the extension’s ability to unmount the OS drive include:</span></span>
- <span data-ttu-id="4862d-111">지원되는 파일 시스템 및/또는 파티션 구성표와 더 이상 일치하지 않는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="4862d-111">Customized images that no longer match a supported file system and/or partitioning scheme.</span></span>
- <span data-ttu-id="4862d-112">암호화하기 전에 바이러스 백신, Docker, SAP, MongoDB 또는 Apache Cassandra와 같은 응용 프로그램이 OS에서 실행되는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="4862d-112">Customized images with applications such as antivirus, Docker, SAP, MongoDB, or Apache Cassandra running in the OS prior to encryption.</span></span>  <span data-ttu-id="4862d-113">이러한 응용 프로그램은 종료하기 어려우며 OS 드라이브에 대해 파일 핸들이 열려 있는 경우 드라이브를 분리할 수 없게 되어 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-113">These applications are difficult to terminate, and when they retain open file handles to the OS drive, the drive cannot be unmounted, causing failure.</span></span>
- <span data-ttu-id="4862d-114">암호화 단계에 거의 근접한 시간에 실행되는 사용자 지정 스크립트는 문제를 일으켜 이 오류를 유발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-114">Custom scripts that run in close time proximity to the encryption step can interfere and cause this failure.</span></span> <span data-ttu-id="4862d-115">이러한 경우는 Resource Manager 템플릿에서 동시에 실행하도록 여러 확장을 정의하거나 사용자 지정 스크립트 확장 또는 다른 작업을 디스크 암호화와 동시에 실행할 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-115">This can happen when a Resource Manager template defines multiple extensions to execute simultaneously, or when a custom script extension or other action is run simultaneously to disk encryption.</span></span>   <span data-ttu-id="4862d-116">이러한 단계를 직렬화하고 격리하면 문제가 해결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-116">Serializing and isolating such steps may resolve the issue.</span></span>
- <span data-ttu-id="4862d-117">암호화를 활성화하기 전에 SELinux가 비활성화되지 않은 경우 - 분리 단계가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-117">When SELinux has not been disabled prior to enabling encryption, the unmount step fails.</span></span>  <span data-ttu-id="4862d-118">암호화가 완료되면 SELinux를 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-118">SELinux can be re-enabled after encryption has completed.</span></span>
- <span data-ttu-id="4862d-119">OS 디스크에서 LVM 구성표를 사용하는 경우 - 제한된 LVM 데이터 디스크 지원은 사용할 수 있지만, LVM OS 디스크는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-119">When the OS disk is using an LVM scheme (although limited LVM data disk support is available, LVM OS disk is not)</span></span>
- <span data-ttu-id="4862d-120">최소 메모리 요구 사항이 충족되지 않는 경우 - OS 디스크 암호화에 권장되는 메모리 크기는 7GB입니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-120">When minimum memory requirements are not met (7GB is suggested for OS disk encryption)</span></span>
- <span data-ttu-id="4862d-121">데이터 드라이브가 /mnt/ 디렉터리 또는 다른 디렉터리(예: /mnt/data1, /mnt/data2, /data3 + /data3/data4 등) 아래에 재귀적으로 탑재된 경우</span><span class="sxs-lookup"><span data-stu-id="4862d-121">When data drives have been recursively mounted under /mnt/ directory, or each other (for example, /mnt/data1, /mnt/data2, /data3 + /data3/data4, etc.)</span></span>
- <span data-ttu-id="4862d-122">Linux에 대한 다른 Azure Disk Encryption [필수 구성 요소](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)가 충족되지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="4862d-122">When other Azure Disk Encryption [prerequisites](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) for Linux are not met</span></span>

## <a name="unable-to-encrypt"></a><span data-ttu-id="4862d-123">암호화할 수 없음</span><span class="sxs-lookup"><span data-stu-id="4862d-123">Unable to encrypt</span></span>

<span data-ttu-id="4862d-124">경우에 따라 Linux 디스크 암호화가 "OS 디스크 암호화 시작됨" 상태에서 중단된 것으로 나타나고, SSH가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-124">In some cases, the Linux disk encryption appears to be stuck at "OS disk encryption started" and SSH is disabled.</span></span> <span data-ttu-id="4862d-125">이 프로세스를 재고 갤러리 이미지에 대해 완료하는 데 3-16시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-125">This process can take between 3-16 hours to complete on a stock gallery image.</span></span>  <span data-ttu-id="4862d-126">다중 TB 크기 데이터 디스크가 추가될 경우 이 프로세스는 며칠이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-126">If multi-TB size data disks are added, the process may take days.</span></span> <span data-ttu-id="4862d-127">Linux OS 디스크 암호화 시퀀스에서는 OS 드라이브를 임시로 분리하고, 암호화된 상태로 다시 탑재하기 전에 전체 OS 디스크의 블록 암호화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-127">The Linux OS disk encryption sequence unmounts the OS drive temporarily, and performs block by block encryption of the entire OS disk, before remounting it in its encrypted state.</span></span>   <span data-ttu-id="4862d-128">Windows의 Azure Disk Encryption과 달리 Linux 디스크 암호화는 암호화를 진행하는 동안 VM을 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-128">Unlike Azure Disk Encryption on Windows, Linux Disk Encryption does not allow concurrent use of the VM while the encryption is in progress.</span></span>  <span data-ttu-id="4862d-129">디스크 크기 및 저장소 계정이 표준 또는 프리미엄(SSD) 저장소에서 지원되는지 여부를 포함한 VM의 성능 특성은 암호화를 완료하는 데 필요한 시간에 크게 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-129">The performance characteristics of the VM, including the size of the disk and whether the storage account is backed by standard or premium (SSD) storage, can greatly influence the time required to complete encryption.</span></span>

<span data-ttu-id="4862d-130">상태를 확인하기 위해 [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) 명령에서 반환된 ProgressMessage 필드를 폴링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-130">To check status, the ProgressMessage field returned from the [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) command can be polled.</span></span>   <span data-ttu-id="4862d-131">OS 드라이브가 암호화되는 동안 VM은 서비스 상태가 되고 SSH도 진행 중인 프로세스의 중단을 방지하기 위해 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-131">While the OS drive is being encrypted, the VM enters a servicing state, and SSH is also disabled to prevent any disruption to the ongoing process.</span></span>  <span data-ttu-id="4862d-132">암호화가 진행되는 대부분의 시간 동안 EncryptionInProgress가 보고되고, 몇 시간 후에 VM을 다시 시작하라는 VMRestartPending 메시지가 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-132">EncryptionInProgress will be reported for the majority of the time while encryption is in progress, followed several hours later with a VMRestartPending message prompting to restart the VM.</span></span>  <span data-ttu-id="4862d-133">예:</span><span class="sxs-lookup"><span data-stu-id="4862d-133">For example:</span></span>


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot the VM
```

<span data-ttu-id="4862d-134">VM을 다시 부팅하라는 메시지가 표시되고 VM을 다시 시작한 후 2-3분을 기다려 다시 부팅하고 대상에서 최종 단계를 수행하면 암호화가 최종적으로 완료되었다는 상태 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-134">Once prompted to reboot the VM, and after restarting the VM, and giving 2-3 minutes for the reboot and for final steps to be performed on the target, the status message will indicate that encryption has finally completed.</span></span>   <span data-ttu-id="4862d-135">이 메시지가 제공되면 암호화된 OS 드라이브가 사용할 준비가 되었으며 VM을 다시 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-135">Once this message is available, the encrypted OS drive is expected to be ready for use and for the VM to be usable again.</span></span>

<span data-ttu-id="4862d-136">이 시퀀스가 나타나지 않거나 부팅 정보, 진행 상태 메시지 또는 다른 오류 표시기에서 이 프로세스의 중간에 OS 암호화가 실패했다고 보고하는 경우(예: 이 가이드에 설명한 "분리하지 못했습니다" 오류가 표시되는 경우) 암호화 직전에 VM을 스냅숏 또는 백업으로 다시 복원하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-136">In cases where this sequence was not seen, or if boot information, progress message, or other error indicators report that OS encryption has failed in the middle of this process (for example if you are seeing the "failed to unmount" error described in this guide), it is recommended to restore the VM back to the snapshot or backup taken immediately prior to encryption.</span></span>  <span data-ttu-id="4862d-137">다음 시도를 수행하기 전에 VM의 특성을 다시 평가하고 모든 필수 조건이 충족되는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-137">Prior to the next attempt, it is suggested to re-evaluate the characteristics of the VM and ensure that all prerequisites are satisfied.</span></span>

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a><span data-ttu-id="4862d-138">방화벽 뒤에 있는 Azure Disk Encryption 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4862d-138">Troubleshooting Azure Disk Encryption behind a Firewall</span></span>
<span data-ttu-id="4862d-139">방화벽, 프록시 요구 사항 또는 NSG(네트워크 보안 그룹) 설정으로 연결이 제한되면 필요한 작업을 수행할 수 있는 확장의 기능이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-139">When connectivity is restricted by a firewall, proxy requirement, or network security group (NSG) settings, the ability of the extension to perform needed tasks can be disrupted.</span></span>   <span data-ttu-id="4862d-140">이로 인해 "VM에서 사용할 수 없는 확장 상태"와 같은 상태 메시지가 표시되고, 예상된 시나리오가 완료되지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-140">This can result in status messages such as "Extension status not available on the VM" and in expected scenarios failing to finish.</span></span>  <span data-ttu-id="4862d-141">다음 섹션에서는 조사할 수 있는 몇 가지 일반적인 방화벽 문제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-141">The sections that follow has some common firewall issues that you may investigate.</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="4862d-142">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4862d-142">Network security groups</span></span>
<span data-ttu-id="4862d-143">적용되는 모든 네트워크 보안 그룹 설정은 끝점에서도 디스크 암호화에 대해 문서화된 네트워크 구성 [필수 조건](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites)을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-143">Any network security group settings applied must still allow the endpoint to meet the documented network configuration [prerequisites](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) for disk encryption.</span></span>

### <a name="azure-keyvault-behind-firewall"></a><span data-ttu-id="4862d-144">방화벽 뒤에 있는 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4862d-144">Azure Keyvault behind firewall</span></span>
<span data-ttu-id="4862d-145">VM에서 키 자격 증명 모음에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-145">The VM must be able to access key vault.</span></span> <span data-ttu-id="4862d-146">[Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) 팀이 유지 관리하는 방화벽 뒤에서 키 자격 증명 모음에 액세스하는 방법에 대한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4862d-146">Refer to guidance on access to key fault from behind a firewall that is maintained by the [Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) team.</span></span>

### <a name="linux-package-management-behind-firewall"></a><span data-ttu-id="4862d-147">방화벽 뒤에 있는 Linux 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="4862d-147">Linux package management behind firewall</span></span>
<span data-ttu-id="4862d-148">런타임 시 Linux용 Azure Disk Encryption은 대상 배포판의 패키지 관리 시스템을 사용하여 암호화를 사용하기 전에 필요한 필수 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-148">At run time, Azure Disk Encryption for Linux relies on the target distribution’s package management system to install needed prerequisite components prior to enabling encryption.</span></span>  <span data-ttu-id="4862d-149">방화벽 설정으로 인해 VM에서 이러한 구성 요소를 다운로드하여 설치할 수 없으면 뒤이어서 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-149">If firewall settings prevent the VM from being able to download and install these components, then subsequent failures are expected.</span></span>    <span data-ttu-id="4862d-150">이를 구성하는 단계는 배포판마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-150">The steps to configure this may vary by distribution.</span></span>  <span data-ttu-id="4862d-151">Red Hat에서 프록시가 필요한 경우에는 subscription-manager와 yum이 올바르게 설정되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-151">On Red Hat, when a proxy is required, ensuring that subscription-manager and yum are set up properly is vital.</span></span>  <span data-ttu-id="4862d-152">이 항목은 [여기](https://access.redhat.com/solutions/189533)에 있는 Red Hat 지원 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4862d-152">See [this](https://access.redhat.com/solutions/189533) Red Hat support article on this topic.</span></span>  

## <a name="troubleshooting-windows-server-2016-server-core"></a><span data-ttu-id="4862d-153">Windows Server 2016 Server Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4862d-153">Troubleshooting Windows Server 2016 Server Core</span></span>

<span data-ttu-id="4862d-154">Windows Server 2016 Server Core에서 bdehdcfg 구성 요소는 기본적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-154">On Windows Server 2016 Server Core, the bdehdcfg component is not available by default.</span></span> <span data-ttu-id="4862d-155">이 구성 요소는 Azure Disk Encryption에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-155">This component is required by Azure Disk Encryption.</span></span>

<span data-ttu-id="4862d-156">이 문제를 해결하려면 Windows Server 2016 Data Center VM의 다음 4개 파일을 Server Core 이미지의 c:\windows\system32 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-156">To workaround this issue, copy the following 4 files from a Windows Server 2016 Data Center VM to the c:\windows\system32 folder of the Server Core image:</span></span>

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

<span data-ttu-id="4862d-157">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-157">Then, run the following command:</span></span>

```
bdehdcfg.exe -target default
```

<span data-ttu-id="4862d-158">이렇게 하면 550MB 시스템 파티션이 만들어지고, 다시 부팅한 후에는 Diskpart를 사용하여 볼륨을 확인하고 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-158">This will create a 550MB system partition and then after a reboot, you can use Diskpart to check the volumes, and proceed.</span></span>  

<span data-ttu-id="4862d-159">예:</span><span class="sxs-lookup"><span data-stu-id="4862d-159">For example:</span></span>

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a><span data-ttu-id="4862d-160">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4862d-160">See also</span></span>
<span data-ttu-id="4862d-161">이 문서에서는 일반적인 Azure Disk Encryption 문제와 해결 방법에 대해 자세히 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4862d-161">In this document, you learned more about some common issues in Azure disk encryption, and how to troubleshoot.</span></span> <span data-ttu-id="4862d-162">이 서비스 및 기능에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4862d-162">For more information about this service and its capability read:</span></span>

- [<span data-ttu-id="4862d-163">Azure Security Center에서 디스크 암호화 적용</span><span class="sxs-lookup"><span data-stu-id="4862d-163">Apply disk encryption in Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [<span data-ttu-id="4862d-164">Azure 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="4862d-164">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [<span data-ttu-id="4862d-165">Azure 미사용 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="4862d-165">Azure Data Encryption-at-Rest</span></span>](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
