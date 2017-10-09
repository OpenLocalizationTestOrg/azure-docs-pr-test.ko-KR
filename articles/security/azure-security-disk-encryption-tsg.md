---
title: "디스크 암호화 문제 해결 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a><span data-ttu-id="3b42f-103">Azure Disk Encryption 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3b42f-103">Azure Disk Encryption Troubleshooting Guide</span></span>

<span data-ttu-id="3b42f-104">이 가이드는 정보 정보 기술 (IT) 전문가 위한 보안 분석가 및 관련 문제를 클라우드 관리자 인 Azure 디스크 암호화를 사용 하는 조직과 지침 tootroubleshoot 디스크 암호화가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure disk encryption and need guidance tootroubleshoot disk-encryption related issues.</span></span>

## <a name="troubleshooting-linux-os-disk-encryption"></a><span data-ttu-id="3b42f-105">Linux OS 디스크 암호화 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3b42f-105">Troubleshooting Linux OS disk encryption</span></span>

<span data-ttu-id="3b42f-106">Linux 운영 체제 디스크 암호화 hello 운영 체제 드라이브 이전 toorunning 탑재 해제 해야 hello 전체 디스크 암호화 프로세스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-106">Linux OS disk encryption must unmount hello OS drive prior toorunning it through hello full disk encryption process.</span></span>   <span data-ttu-id="3b42f-107">불가능 한 경우, 오류 메시지의 "실패 후 toounmount..."</span><span class="sxs-lookup"><span data-stu-id="3b42f-107">If it cannot, an error message of "failed toounmount after…"</span></span> <span data-ttu-id="3b42f-108">오류 메시지는 가능성이 toooccur입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-108">error message is likely toooccur.</span></span>

<span data-ttu-id="3b42f-109">이는 지원되는 재고 갤러리 이미지에서 수정되거나 변경된 대상 VM 환경에서 OS 디스크 암호화를 시도할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-109">This is most likely when OS disk encryption is attempted on a target VM environment that has been modified or changed from its supported stock gallery image.</span></span>  <span data-ttu-id="3b42f-110">Hello 확장의 기능 toounmount hello 운영 체제 드라이브와 충돌할 수 있는 지원 되는 hello 이미지에서 편차의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-110">Examples of deviations from hello supported image, which can interfere with hello extension’s ability toounmount hello OS drive include:</span></span>
- <span data-ttu-id="3b42f-111">지원되는 파일 시스템 및/또는 파티션 구성표와 더 이상 일치하지 않는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="3b42f-111">Customized images that no longer match a supported file system and/or partitioning scheme.</span></span>
- <span data-ttu-id="3b42f-112">예: 바이러스 백신 응용 프로그램, Docker, SAP, MongoDB, 또는 Apache Cassandra hello OS 이전 tooencryption에서 실행을 사용 하 여 사용자 지정 된 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-112">Customized images with applications such as antivirus, Docker, SAP, MongoDB, or Apache Cassandra running in hello OS prior tooencryption.</span></span>  <span data-ttu-id="3b42f-113">이러한 응용 프로그램은 어려운 tooterminate 하 고 열려 있는 파일 핸들 toohello 운영 체제 드라이브, 유지 hello 드라이브를 탑재 되지 않은 오류를 발생 시키는 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-113">These applications are difficult tooterminate, and when they retain open file handles toohello OS drive, hello drive cannot be unmounted, causing failure.</span></span>
- <span data-ttu-id="3b42f-114">실행 되는 사용자 지정 스크립트 근접 toohello 암호화 단계 충돌할 수 있으며이 오류가 발생 하는 시간을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-114">Custom scripts that run in close time proximity toohello encryption step can interfere and cause this failure.</span></span> <span data-ttu-id="3b42f-115">이 사용자 지정 스크립트 확장 또는 기타 작업이 실행 될 때 동시에 toodisk 암호화 또는 리소스 관리자 템플릿 동시에 여러 확장 tooexecute를 정의 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-115">This can happen when a Resource Manager template defines multiple extensions tooexecute simultaneously, or when a custom script extension or other action is run simultaneously toodisk encryption.</span></span>   <span data-ttu-id="3b42f-116">직렬화 하는 작업 및 이러한 단계를 분리 hello 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-116">Serializing and isolating such steps may resolve hello issue.</span></span>
- <span data-ttu-id="3b42f-117">SELinux 사용할 수 없는 이전 tooenabling 암호화 되지 않았으면 hello 단계 실패를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-117">When SELinux has not been disabled prior tooenabling encryption, hello unmount step fails.</span></span>  <span data-ttu-id="3b42f-118">암호화가 완료되면 SELinux를 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-118">SELinux can be re-enabled after encryption has completed.</span></span>
- <span data-ttu-id="3b42f-119">Hello OS 디스크 LVM 체계 사용 하는 경우 (제한 된 LVM 데이터 디스크 지원을 사용할 수 있는 경우에 LVM OS 디스크는 아님)</span><span class="sxs-lookup"><span data-stu-id="3b42f-119">When hello OS disk is using an LVM scheme (although limited LVM data disk support is available, LVM OS disk is not)</span></span>
- <span data-ttu-id="3b42f-120">최소 메모리 요구 사항이 충족되지 않는 경우 - OS 디스크 암호화에 권장되는 메모리 크기는 7GB입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-120">When minimum memory requirements are not met (7GB is suggested for OS disk encryption)</span></span>
- <span data-ttu-id="3b42f-121">데이터 드라이브가 /mnt/ 디렉터리 또는 다른 디렉터리(예: /mnt/data1, /mnt/data2, /data3 + /data3/data4 등) 아래에 재귀적으로 탑재된 경우</span><span class="sxs-lookup"><span data-stu-id="3b42f-121">When data drives have been recursively mounted under /mnt/ directory, or each other (for example, /mnt/data1, /mnt/data2, /data3 + /data3/data4, etc.)</span></span>
- <span data-ttu-id="3b42f-122">Linux에 대한 다른 Azure Disk Encryption [필수 구성 요소](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)가 충족되지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="3b42f-122">When other Azure Disk Encryption [prerequisites](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) for Linux are not met</span></span>

## <a name="unable-tooencrypt"></a><span data-ttu-id="3b42f-123">Tooencrypt 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-123">Unable tooencrypt</span></span>

<span data-ttu-id="3b42f-124">경우에 따라 hello Linux 디스크 암호화 toobe "OS 디스크 암호화 시작"에서 중단 하 고 SSH를 비활성화 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-124">In some cases, hello Linux disk encryption appears toobe stuck at "OS disk encryption started" and SSH is disabled.</span></span> <span data-ttu-id="3b42f-125">이 프로세스는 주식 갤러리 이미지에 3-16 시간 toocomplete 간의 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-125">This process can take between 3-16 hours toocomplete on a stock gallery image.</span></span>  <span data-ttu-id="3b42f-126">다중 TB 크기 데이터 디스크 추가 되 면 hello 프로세스 일 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-126">If multi-TB size data disks are added, hello process may take days.</span></span> <span data-ttu-id="3b42f-127">hello Linux 운영 체제 디스크 암호화 시퀀스 일시적으로 hello 운영 체제 드라이브를 탑재 해제 하 고 암호화 된 상태에서 다시 탑재 하기 전에 hello 전체 운영 체제 디스크의 블록 단위로 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-127">hello Linux OS disk encryption sequence unmounts hello OS drive temporarily, and performs block by block encryption of hello entire OS disk, before remounting it in its encrypted state.</span></span>   <span data-ttu-id="3b42f-128">Windows Azure 디스크 암호화를와 달리 Linux 디스크 암호화 허용 하지 않습니다 hello VM의 동시 사용 hello 암호화가 진행 중인 동안.</span><span class="sxs-lookup"><span data-stu-id="3b42f-128">Unlike Azure Disk Encryption on Windows, Linux Disk Encryption does not allow concurrent use of hello VM while hello encryption is in progress.</span></span>  <span data-ttu-id="3b42f-129">hello hello 디스크와 표준 또는 프리미엄 (SSD) 저장소 hello 저장소 계정 기반한 여부의 hello 크기를 포함 한 VM의 성능 특성 hello hello 필요한 시간 toocomplete 암호화 하는 데 상당한 영향을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-129">hello performance characteristics of hello VM, including hello size of hello disk and whether hello storage account is backed by standard or premium (SSD) storage, can greatly influence hello time required toocomplete encryption.</span></span>

<span data-ttu-id="3b42f-130">toocheck 상태 hello에서 반환 된 hello ProgressMessage 필드 [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) 명령을 폴링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-130">toocheck status, hello ProgressMessage field returned from hello [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) command can be polled.</span></span>   <span data-ttu-id="3b42f-131">Hello 운영 체제 드라이브를 암호화 하는 hello VM 서비스 상태가 하 고 SSH 비활성화 tooprevent 이기도 모든 중단 toohello 지속적인 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-131">While hello OS drive is being encrypted, hello VM enters a servicing state, and SSH is also disabled tooprevent any disruption toohello ongoing process.</span></span>  <span data-ttu-id="3b42f-132">진행 중, 아래에 몇 시간이 나중 toorestart hello VM는 VMRestartPending 메시지가 암호화 하는 동안 EncryptionInProgress hello 시간의 hello 대부분에 대 한 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-132">EncryptionInProgress will be reported for hello majority of hello time while encryption is in progress, followed several hours later with a VMRestartPending message prompting toorestart hello VM.</span></span>  <span data-ttu-id="3b42f-133">예:</span><span class="sxs-lookup"><span data-stu-id="3b42f-133">For example:</span></span>


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
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

<span data-ttu-id="3b42f-134">한 번 tooreboot hello VM을 묻는 메시지가 표시 하 고 hello VM을 다시 시작 하 고 2-3 분 hello 다시 부팅 하 고 hello 대상에서 수행 하는 마지막 단계는 toobe 제공, 후 hello 상태 메시지가 암호화는 완료 된 마지막으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-134">Once prompted tooreboot hello VM, and after restarting hello VM, and giving 2-3 minutes for hello reboot and for final steps toobe performed on hello target, hello status message will indicate that encryption has finally completed.</span></span>   <span data-ttu-id="3b42f-135">이 메시지를 사용할 수 있는 암호화 된 hello 운영 체제 드라이브가 사용 하기 위해 수행 하 고 사용 가능한 hello VM toobe에 대 한 예상된 toobe 다시 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-135">Once this message is available, hello encrypted OS drive is expected toobe ready for use and for hello VM toobe usable again.</span></span>

<span data-ttu-id="3b42f-136">경우에이 시퀀스를 찾을 수 없습니다 또는 부팅 정보, 진행률 메시지 또는 기타 오류 지표 보고서 (예:이 가이드에 설명 된 hello "toounmount 실패 했습니다." 오류가 표시 되는 경우)이이 프로세스의 hello 가운데에 운영 체제 암호화에 실패 했음을 toorestore hello VM 백 toohello 스냅숏 또는 즉시 이전 tooencryption 수행 된 백업 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-136">In cases where this sequence was not seen, or if boot information, progress message, or other error indicators report that OS encryption has failed in hello middle of this process (for example if you are seeing hello "failed toounmount" error described in this guide), it is recommended toorestore hello VM back toohello snapshot or backup taken immediately prior tooencryption.</span></span>  <span data-ttu-id="3b42f-137">이전 toohello 다음 시도 제안 된 toore-hello VM의 hello 특징을 평가 하 고 모든 필수 조건이 충족 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-137">Prior toohello next attempt, it is suggested toore-evaluate hello characteristics of hello VM and ensure that all prerequisites are satisfied.</span></span>

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a><span data-ttu-id="3b42f-138">방화벽 뒤에 있는 Azure Disk Encryption 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3b42f-138">Troubleshooting Azure Disk Encryption behind a Firewall</span></span>
<span data-ttu-id="3b42f-139">때 연결이 필요한 작업 중단 수 hello 확장 tooperform의 방화벽, 프록시 요구 사항 또는 네트워크 보안 그룹 (NSG) 설정 hello 능력에 의해 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-139">When connectivity is restricted by a firewall, proxy requirement, or network security group (NSG) settings, hello ability of hello extension tooperform needed tasks can be disrupted.</span></span>   <span data-ttu-id="3b42f-140">상태 메시지 "hello VM에서 사용할 수 없는 확장 상태" 등이 될 수 있습니다 및 예상된 시나리오가 toofinish 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-140">This can result in status messages such as "Extension status not available on hello VM" and in expected scenarios failing toofinish.</span></span>  <span data-ttu-id="3b42f-141">이어지는 hello 섹션에 몇 가지 일반적인 방화벽 문제를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-141">hello sections that follow has some common firewall issues that you may investigate.</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="3b42f-142">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3b42f-142">Network security groups</span></span>
<span data-ttu-id="3b42f-143">적용 된 모든 네트워크 보안 그룹 설정은 hello 끝점 toomeet 문서화 hello 네트워크 구성 허용 여전히 해야 [필수 구성 요소](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) 디스크 암호화에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-143">Any network security group settings applied must still allow hello endpoint toomeet hello documented network configuration [prerequisites](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) for disk encryption.</span></span>

### <a name="azure-keyvault-behind-firewall"></a><span data-ttu-id="3b42f-144">방화벽 뒤에 있는 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3b42f-144">Azure Keyvault behind firewall</span></span>
<span data-ttu-id="3b42f-145">hello VM 수 tooaccess 키 자격 증명 모음 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-145">hello VM must be able tooaccess key vault.</span></span> <span data-ttu-id="3b42f-146">Hello로 유지 관리 되는 방화벽 뒤에서 액세스 tookey 오류에서 tooguidance 참조 [키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) 팀입니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-146">Refer tooguidance on access tookey fault from behind a firewall that is maintained by hello [Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) team.</span></span>

### <a name="linux-package-management-behind-firewall"></a><span data-ttu-id="3b42f-147">방화벽 뒤에 있는 Linux 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="3b42f-147">Linux package management behind firewall</span></span>
<span data-ttu-id="3b42f-148">Linux 용 Azure 디스크 암호화는 런타임 시 hello 대상 배포 패키지 관리 시스템 tooinstall 필요한 필수 구성 요소 이전 tooenabling 암호화에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-148">At run time, Azure Disk Encryption for Linux relies on hello target distribution’s package management system tooinstall needed prerequisite components prior tooenabling encryption.</span></span>  <span data-ttu-id="3b42f-149">Hello VM toodownload 수 없도록 방지 하 고 이러한 구성 요소를 설치 하는 방화벽 설정, 다른 연결이 실패 예상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-149">If firewall settings prevent hello VM from being able toodownload and install these components, then subsequent failures are expected.</span></span>    <span data-ttu-id="3b42f-150">hello 단계 tooconfigure 분배 하 여 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-150">hello steps tooconfigure this may vary by distribution.</span></span>  <span data-ttu-id="3b42f-151">Red Hat에서 프록시가 필요한 경우에는 subscription-manager와 yum이 올바르게 설정되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-151">On Red Hat, when a proxy is required, ensuring that subscription-manager and yum are set up properly is vital.</span></span>  <span data-ttu-id="3b42f-152">이 항목은 [여기](https://access.redhat.com/solutions/189533)에 있는 Red Hat 지원 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b42f-152">See [this](https://access.redhat.com/solutions/189533) Red Hat support article on this topic.</span></span>  

## <a name="troubleshooting-windows-server-2016-server-core"></a><span data-ttu-id="3b42f-153">Windows Server 2016 Server Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3b42f-153">Troubleshooting Windows Server 2016 Server Core</span></span>

<span data-ttu-id="3b42f-154">Windows Server 2016 Server Core에서 hello bdehdcfg 구성 요소가 기본적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-154">On Windows Server 2016 Server Core, hello bdehdcfg component is not available by default.</span></span> <span data-ttu-id="3b42f-155">이 구성 요소는 Azure Disk Encryption에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-155">This component is required by Azure Disk Encryption.</span></span>

<span data-ttu-id="3b42f-156">tooworkaround이 문제점, hello Server Core 이미지의 Windows Server 2016 데이터 센터 VM toohello c:\windows\system32 폴더에서 다음 4 파일이 복사 hello:</span><span class="sxs-lookup"><span data-stu-id="3b42f-156">tooworkaround this issue, copy hello following 4 files from a Windows Server 2016 Data Center VM toohello c:\windows\system32 folder of hello Server Core image:</span></span>

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

<span data-ttu-id="3b42f-157">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-157">Then, run hello following command:</span></span>

```
bdehdcfg.exe -target default
```

<span data-ttu-id="3b42f-158">550MB 시스템 파티션을 만들어집니다 고 다시 부팅 한 후 수 있습니다 Diskpart toocheck hello 볼륨을 사용 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-158">This will create a 550MB system partition and then after a reboot, you can use Diskpart toocheck hello volumes, and proceed.</span></span>  

<span data-ttu-id="3b42f-159">예:</span><span class="sxs-lookup"><span data-stu-id="3b42f-159">For example:</span></span>

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a><span data-ttu-id="3b42f-160">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3b42f-160">See also</span></span>
<span data-ttu-id="3b42f-161">이 문서에서 배운 Azure 디스크 암호화에서는 몇 가지 일반적인 문제에 대 한 자세한 방법과 tootroubleshoot 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b42f-161">In this document, you learned more about some common issues in Azure disk encryption, and how tootroubleshoot.</span></span> <span data-ttu-id="3b42f-162">이 서비스 및 기능에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b42f-162">For more information about this service and its capability read:</span></span>

- [<span data-ttu-id="3b42f-163">Azure Security Center에서 디스크 암호화 적용</span><span class="sxs-lookup"><span data-stu-id="3b42f-163">Apply disk encryption in Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [<span data-ttu-id="3b42f-164">Azure 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="3b42f-164">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [<span data-ttu-id="3b42f-165">Azure 미사용 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="3b42f-165">Azure Data Encryption-at-Rest</span></span>](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
