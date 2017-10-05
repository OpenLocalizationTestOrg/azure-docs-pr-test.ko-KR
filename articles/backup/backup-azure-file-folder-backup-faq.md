---
title: "Azure Backup 에이전트 FAQ | Microsoft Docs"
description: "Azure Backup 에이전트 작동 방식, 백업 및 보존 제한과 관련된 일반적인 질문에 대한 대답입니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "백업 및 재해 복구; 백업 서비스"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: 227cdc87f3e2c8ed393145f4bbde7f74606bdf3b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="questions-about-the-azure-backup-agent"></a><span data-ttu-id="6a9a9-104">Azure Backup 에이전트에 대한 질문</span><span class="sxs-lookup"><span data-stu-id="6a9a9-104">Questions about the Azure Backup agent</span></span>
<span data-ttu-id="6a9a9-105">이 문서에서는 Azure Backup 에이전트 구성 요소를 빨리 이해하는 데 도움이 되는 일반적인 질문에 대한 대답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-105">This article has answers to common questions to help you quickly understand the Azure Backup agent components.</span></span> <span data-ttu-id="6a9a9-106">대답 중 일부에는 포괄적인 정보를 포함하는 문서에 대한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-106">In some of the answers, there are links to the articles that have comprehensive information.</span></span> <span data-ttu-id="6a9a9-107">또한 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)에 Azure Backup 서비스에 대한 질문도 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-107">You can also post questions about the Azure Backup service in the [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="configure-backup"></a><span data-ttu-id="6a9a9-108">백업 구성</span><span class="sxs-lookup"><span data-stu-id="6a9a9-108">Configure backup</span></span>
### <a name="where-can-i-download-the-latest-azure-backup-agent-br"></a><span data-ttu-id="6a9a9-109">최신 Azure Backup 에이전트를 어디서 다운로드할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-109">Where can I download the latest Azure Backup agent?</span></span> <br/>
<span data-ttu-id="6a9a9-110">Windows Server, System Center DPM 또는 Windows 클라이언트를 백업하기 위한 최신 에이전트를 [여기](http://aka.ms/azurebackup_agent)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-110">You can download the latest agent for backing up Windows Server, System Center DPM, or Windows client, from [here](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="6a9a9-111">가상 컴퓨터를 백업하려는 경우 VM 에이전트(적절한 확장을 자동으로 설치)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-111">If you want to back up a virtual machine, use the VM Agent (which automatically installs the proper extension).</span></span> <span data-ttu-id="6a9a9-112">Azure 갤러리에서 만든 가상 컴퓨터에는 VM 에이전트가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-112">The VM Agent is already present on virtual machines created from the Azure gallery.</span></span>

### <a name="when-configuring-the-azure-backup-agent-i-am-prompted-to-enter-the-vault-credentials-do-vault-credentials-expire"></a><span data-ttu-id="6a9a9-113">Azure Backup 에이전트를 구성할 때 저장소 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-113">When configuring the Azure Backup agent, I am prompted to enter the vault credentials.</span></span> <span data-ttu-id="6a9a9-114">저장소 자격 증명은 만료되나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-114">Do vault credentials expire?</span></span>
<span data-ttu-id="6a9a9-115">예, 저장소 자격 증명은 48시간이 지나면 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-115">Yes, the vault credentials expire after 48 hours.</span></span> <span data-ttu-id="6a9a9-116">파일이 만료되면 Azure 포털에 로그인하고 해당 자격 증명 모음에서 저장소 자격 증명 파일을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-116">If the file expires, log in to the Azure portal and download the vault credentials files from your vault.</span></span>

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a><span data-ttu-id="6a9a9-117">어떤 드라이브 유형의 파일 및 폴더를 백업할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-117">What types of drives can I back up files and folders from?</span></span> <br/>
<span data-ttu-id="6a9a9-118">다음과 같은 드라이브/볼륨은 백업할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-118">You can't back up the following drives/volumes:</span></span>

* <span data-ttu-id="6a9a9-119">이동식 미디어: 모든 백업 항목 원본은 고정된 것으로 보고되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-119">Removable Media: All backup item sources must report as fixed.</span></span>
* <span data-ttu-id="6a9a9-120">읽기 전용 볼륨: VSS(볼륨 섀도 복사본 서비스)가 작동하려면 볼륨에 데이터 쓰기가 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-120">Read-only Volumes: The volume must be writable for the volume shadow copy service (VSS) to function.</span></span>
* <span data-ttu-id="6a9a9-121">오프라인 볼륨: VSS가 작동하려면 볼륨이 온라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-121">Offline Volumes: The volume must be online for VSS to function.</span></span>
* <span data-ttu-id="6a9a9-122">네트워크 공유: 온라인 백업을 사용하여 백업할 서버의 로컬 볼륨이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-122">Network share: The volume must be local to the server to be backed up using online backup.</span></span>
* <span data-ttu-id="6a9a9-123">Bitlocker로 보호된 볼륨: 볼륨의 잠금을 해제해야 백업이 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-123">Bitlocker-protected volumes: The volume must be unlocked before the backup can occur.</span></span>
* <span data-ttu-id="6a9a9-124">파일 시스템 식별: NTFS가 유일하게 지원되는 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-124">File System Identification: NTFS is the only file system supported.</span></span>

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a><span data-ttu-id="6a9a9-125">내 서버에서 어떤 파일 및 폴더 형식을 백업할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-125">What file and folder types can I back up from my server?</span></span><br/>
<span data-ttu-id="6a9a9-126">다음과 같은 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-126">The following types are supported:</span></span>

* <span data-ttu-id="6a9a9-127">암호화</span><span class="sxs-lookup"><span data-stu-id="6a9a9-127">Encrypted</span></span>
* <span data-ttu-id="6a9a9-128">압축</span><span class="sxs-lookup"><span data-stu-id="6a9a9-128">Compressed</span></span>
* <span data-ttu-id="6a9a9-129">스파스</span><span class="sxs-lookup"><span data-stu-id="6a9a9-129">Sparse</span></span>
* <span data-ttu-id="6a9a9-130">압축 + 스파스</span><span class="sxs-lookup"><span data-stu-id="6a9a9-130">Compressed + Sparse</span></span>
* <span data-ttu-id="6a9a9-131">하드 링크: 지원되지 않음, 건너뜀</span><span class="sxs-lookup"><span data-stu-id="6a9a9-131">Hard Links: Not supported, skipped</span></span>
* <span data-ttu-id="6a9a9-132">재분석 지점: 지원되지 않음, 건너뜀</span><span class="sxs-lookup"><span data-stu-id="6a9a9-132">Reparse Point: Not supported, skipped</span></span>
* <span data-ttu-id="6a9a9-133">암호화 + 스파스: 지원되지 않음, 건너뜀</span><span class="sxs-lookup"><span data-stu-id="6a9a9-133">Encrypted + Sparse: Not supported, skipped</span></span>
* <span data-ttu-id="6a9a9-134">압축 스트림: 지원되지 않음, 건너뜀</span><span class="sxs-lookup"><span data-stu-id="6a9a9-134">Compressed Stream: Not supported, skipped</span></span>
* <span data-ttu-id="6a9a9-135">스파스 스트림: 지원되지 않음, 건너뜀</span><span class="sxs-lookup"><span data-stu-id="6a9a9-135">Sparse Stream: Not supported, skipped</span></span>

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-already-backed-by-the-azure-backup-service-using-the-vm-extension-br"></a><span data-ttu-id="6a9a9-136">VM 확장을 사용하여 Azure Backup 서비스에서 이미 지원하는 Azure VM에 Azure Backup 에이전트를 설치할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-136">Can I install the Azure Backup agent on an Azure VM already backed by the Azure Backup service using the VM extension?</span></span> <br/>
<span data-ttu-id="6a9a9-137">그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-137">Absolutely.</span></span> <span data-ttu-id="6a9a9-138">Azure Backup은 VM 확장을 사용하여 Azure VM에 대한 VM 수준 백업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-138">Azure Backup provides VM-level backup for Azure VMs using the VM extension.</span></span> <span data-ttu-id="6a9a9-139">게스트 Windows OS의 파일 및 폴더를 보호하려면 게스트 Windows OS에 Azure Backup 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-139">To protect files and folders on the guest Windows OS, install the Azure Backup agent on the guest Windows OS.</span></span>

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-to-back-up-files-and-folders-present-on-temporary-storage-provided-by-the-azure-vm-br"></a><span data-ttu-id="6a9a9-140">Azure VM에 Azure Backup 에이전트를 설치하여 Azure VM에서 제공하는 임시 저장소에 존재하는 파일 및 폴더를 백업할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-140">Can I install the Azure Backup agent on an Azure VM to back up files and folders present on temporary storage provided by the Azure VM?</span></span> <br/>
<span data-ttu-id="6a9a9-141">예.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-141">Yes.</span></span> <span data-ttu-id="6a9a9-142">게스트 Windows OS에 Azure Backup 에이전트를 설치하고 임시 저장소에 파일 및 폴더를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-142">Install the Azure Backup agent on the guest Windows OS, and back up files and folders to temporary storage.</span></span> <span data-ttu-id="6a9a9-143">임시 저장소 데이터가 초기화된 후에는 백업 작업이 실패합니다. 또한 임시 저장소 데이터가 삭제된 경우 비휘발성 저장소에만 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-143">Backup jobs fail once temporary storage data is wiped out. Also, if the temporary storage data has been deleted, you can only restore to non-volatile storage.</span></span>

### <a name="whats-the-minimum-size-requirement-for-the-cache-folder-br"></a><span data-ttu-id="6a9a9-144">캐시 폴더의 최소 크기 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-144">What's the minimum size requirement for the cache folder?</span></span> <br/>
<span data-ttu-id="6a9a9-145">캐시 폴더의 크기는 백업하는 데이터의 양에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-145">The size of the cache folder determines the amount of data that you are backing up.</span></span> <span data-ttu-id="6a9a9-146">캐시 폴더는 데이터 저장에 필요한 공간의 5%여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-146">Your cache folder should be 5% of the space required for data storage.</span></span>

### <a name="how-do-i-register-my-server-to-another-datacenterbr"></a><span data-ttu-id="6a9a9-147">다른 데이터 센터에 내 서버를 등록하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-147">How do I register my server to another datacenter?</span></span><br/>
<span data-ttu-id="6a9a9-148">백업 데이터는 등록된 자격 증명 모음의 데이터 센터로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-148">Backup data is sent to the datacenter of the vault to which it is registered.</span></span> <span data-ttu-id="6a9a9-149">데이터 센터를 변경하는 가장 쉬운 방법은 에이전트를 제거하고 다시 설치한 후 원하는 데이터 센터에 속한 새 자격 증명 모음에 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-149">The easiest way to change the datacenter is to uninstall the agent and reinstall the agent and register to a new vault that belongs to desired datacenter.</span></span>

### <a name="does-the-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a><span data-ttu-id="6a9a9-150">Azure Backup 에이전트는 Windows 2012 중복제거를 사용하는 서버에서 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-150">Does the Azure Backup agent work on a server that uses Windows Server 2012 deduplication?</span></span> <br/>
<span data-ttu-id="6a9a9-151">예.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-151">Yes.</span></span> <span data-ttu-id="6a9a9-152">에이전트 서비스는 백업 작업을 준비할 때 중복 제거 된 데이터를 일반 데이터로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-152">The agent service converts the deduplicated data to normal data when it prepares the backup operation.</span></span> <span data-ttu-id="6a9a9-153">그 다음 백업에 대한 데이터를 최적화하고 데이터를 암호화한 다음 온라인 백업 서비스에 암호화된 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-153">It then optimizes the data for backup, encrypts the data, and then sends the encrypted data to the online backup service.</span></span>

## <a name="backup"></a><span data-ttu-id="6a9a9-154">백업</span><span class="sxs-lookup"><span data-stu-id="6a9a9-154">Backup</span></span>
### <a name="how-do-i-change-the-cache-location-specified-for-the-azure-backup-agentbr"></a><span data-ttu-id="6a9a9-155">Azure Backup 에이전트에 대해 지정된 캐시 위치를 변경하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-155">How do I change the cache location specified for the Azure Backup agent?</span></span><br/>
<span data-ttu-id="6a9a9-156">다음 목록을 사용하여 캐시 위치를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-156">Use the following list to change the cache location.</span></span>

1. <span data-ttu-id="6a9a9-157">관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 Backup 엔진을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-157">Stop the Backup engine by executing the following command in an elevated command prompt:</span></span>

    ```PS C:\> Net stop obengine``` 
  
2. <span data-ttu-id="6a9a9-158">파일을 이동하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-158">Do not move the files.</span></span> <span data-ttu-id="6a9a9-159">대신 캐시 공간 폴더를 충분한 공간이 있는 다른 드라이브로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-159">Instead, copy the cache space folder to a different drive with sufficient space.</span></span> <span data-ttu-id="6a9a9-160">백업이 새 캐시 공간으로 작업 중임을 확인한 후 원래 캐시 공간을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-160">The original cache space can be removed after confirming the backups are working with the new cache space.</span></span>
3. <span data-ttu-id="6a9a9-161">다음 레지스트리 항목을 새 캐시 공간 폴더의 경로로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-161">Update the following registry entries with the path to the new cache space folder.</span></span><br/>

    | <span data-ttu-id="6a9a9-162">레지스트리 경로</span><span class="sxs-lookup"><span data-stu-id="6a9a9-162">Registry path</span></span> | <span data-ttu-id="6a9a9-163">레지스트리 키</span><span class="sxs-lookup"><span data-stu-id="6a9a9-163">Registry Key</span></span> | <span data-ttu-id="6a9a9-164">값</span><span class="sxs-lookup"><span data-stu-id="6a9a9-164">Value</span></span> |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |<span data-ttu-id="6a9a9-165">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="6a9a9-165">ScratchLocation</span></span> |<span data-ttu-id="6a9a9-166">*새 캐시 폴더 위치*</span><span class="sxs-lookup"><span data-stu-id="6a9a9-166">*New cache folder location*</span></span> |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |<span data-ttu-id="6a9a9-167">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="6a9a9-167">ScratchLocation</span></span> |<span data-ttu-id="6a9a9-168">*새 캐시 폴더 위치*</span><span class="sxs-lookup"><span data-stu-id="6a9a9-168">*New cache folder location*</span></span> |

4. <span data-ttu-id="6a9a9-169">관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 Backup 엔진을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-169">Restart the Backup engine by executing the following command in an elevated command prompt:</span></span>

    ```PS C:\> Net start obengine```

<span data-ttu-id="6a9a9-170">새 캐시 위치로 성공적으로 백업 작성이 완료되면 원래 캐시 폴더를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-170">Once the backup creation is successfully completed in the new cache location, you can remove the original cache folder.</span></span>


### <a name="where-can-i-put-the-cache-folder-for-the-azure-backup-agent-to-work-as-expectedbr"></a><span data-ttu-id="6a9a9-171">Azure Backup 에이전트가 예상대로 작동하도록 캐시 폴더를 어디에 배치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-171">Where can I put the cache folder for the Azure Backup Agent to work as expected?</span></span><br/>
<span data-ttu-id="6a9a9-172">캐시 폴더에 대해 다음 위치는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-172">The following locations for the cache folder are not recommended:</span></span>

* <span data-ttu-id="6a9a9-173">네트워크 공유 또는 이동식 미디어: 캐시 폴더는 온라인 백업을 사용하여 백업해야 하는 서버에 대해 로컬이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-173">Network share or Removable Media: The cache folder must be local to the server that needs backing up using online backup.</span></span> <span data-ttu-id="6a9a9-174">네트워크 위치 또는 USB 드라이브 같은 이동식 미디어는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-174">Network locations or removable media like USB drives are not supported.</span></span>
* <span data-ttu-id="6a9a9-175">오프라인 볼륨: 캐시 폴더는 Azure Backup 에이전트를 사용하는 예상된 백업에 대해 온라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-175">Offline Volumes: The cache folder must be online for expected backup using Azure Backup Agent.</span></span>

### <a name="are-there-any-attributes-of-the-cache-folder-that-are-not-supportedbr"></a><span data-ttu-id="6a9a9-176">지원되지 않는 캐시 폴더의 특성이 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-176">Are there any attributes of the cache-folder that are not supported?</span></span><br/>
<span data-ttu-id="6a9a9-177">다음과 같은 특성 또는 해당 조합은 캐시 폴더에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-177">The following attributes or their combinations are not supported for the cache folder:</span></span>

* <span data-ttu-id="6a9a9-178">암호화</span><span class="sxs-lookup"><span data-stu-id="6a9a9-178">Encrypted</span></span>
* <span data-ttu-id="6a9a9-179">중복 제거</span><span class="sxs-lookup"><span data-stu-id="6a9a9-179">De-duplicated</span></span>
* <span data-ttu-id="6a9a9-180">압축</span><span class="sxs-lookup"><span data-stu-id="6a9a9-180">Compressed</span></span>
* <span data-ttu-id="6a9a9-181">스파스</span><span class="sxs-lookup"><span data-stu-id="6a9a9-181">Sparse</span></span>
* <span data-ttu-id="6a9a9-182">재분석 지점</span><span class="sxs-lookup"><span data-stu-id="6a9a9-182">Reparse-Point</span></span>

<span data-ttu-id="6a9a9-183">캐시 폴더와 메타데이터 VHD에는 모두 Azure Backup 에이전트에 필요한 특성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-183">The cache folder and the metadata VHD do not have the necessary attributes for the Azure Backup agent.</span></span>

### <a name="is-there-a-way-to-adjust-the-amount-of-bandwidth-used-by-the-backup-servicebr"></a><span data-ttu-id="6a9a9-184">백업 서비스에서 사용되는 대역폭의 양을 조정하는 방법이 있나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-184">Is there a way to adjust the amount of bandwidth used by the Backup service?</span></span><br/>
  <span data-ttu-id="6a9a9-185">예, Backup 에이전트에서 **속성 변경** 옵션을 사용하여 대역폭을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-185">Yes, use the **Change Properties** option in the Backup Agent to adjust bandwidth.</span></span> <span data-ttu-id="6a9a9-186">대역폭을 사용하는 경우 시간과 대역폭의 양을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-186">You can adjust the amount of bandwidth and the times when you use that bandwidth.</span></span> <span data-ttu-id="6a9a9-187">단계별 지침은 **[네트워크 제한 사용](backup-configure-vault.md#enable-network-throttling)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-187">For step-by-step instructions, see **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)**.</span></span>

## <a name="manage-backups"></a><span data-ttu-id="6a9a9-188">백업 관리</span><span class="sxs-lookup"><span data-stu-id="6a9a9-188">Manage backups</span></span>
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-to-azurebr"></a><span data-ttu-id="6a9a9-189">Azure에 데이터를 백업하는 Windows 서버 이름을 바꾸면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-189">What happens if I rename a Windows server that is backing up data to Azure?</span></span><br/>
<span data-ttu-id="6a9a9-190">서버 이름을 바꾸면 현재 구성된 모든 백업이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-190">When you rename a server, all currently configured backups are stopped.</span></span>
<span data-ttu-id="6a9a9-191">백업 자격 증명 모음에 서버의 새 이름을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-191">Register the new name of the server with the Backup vault.</span></span> <span data-ttu-id="6a9a9-192">자격 증명 모음에 새 이름을 등록하면 첫 번째 백업 작업은 *전체* 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-192">When you register the new name with the vault, the first backup operation is a *full* backup.</span></span> <span data-ttu-id="6a9a9-193">이전 서버 이름으로 자격 증명 모음에 백업된 데이터를 복원해야 하는 경우에는 **데이터 복구** 마법사의 [**다른 서버**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-193">If you need to recover data backed up to the vault with the old server name, use the [**Another server**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) option in the **Recover Data** wizard.</span></span>

### <a name="what-is-the-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="6a9a9-194">Azure Backup 에이전트를 사용하여 Backup 정책에서 지정할 수 있는 최대 파일 경로 길이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-194">What is the maximum file path length that can be specified in Backup policy using Azure Backup agent?</span></span> <br/>
<span data-ttu-id="6a9a9-195">Azure Backup 에이전트는 NTFS에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-195">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="6a9a9-196">[파일 경로 길이 사양은 Windows API에 의해 제한됩니다](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths).</span><span class="sxs-lookup"><span data-stu-id="6a9a9-196">The [filepath length specification is limited by the Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths).</span></span> <span data-ttu-id="6a9a9-197">보호하려는 파일의 경로가 Windows API에 허용되는 길이보다 긴 경우 상위 폴더 또는 디스크 드라이브를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-197">If the files you want to protect have a file-path length longer than what is allowed by the Windows API, back up the parent folder or the disk drive.</span></span>  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="6a9a9-198">Azure Backup 에이전트를 사용하는 Azure Backup 정책의 파일 경로에 어떤 문자가 허용되나요?</span><span class="sxs-lookup"><span data-stu-id="6a9a9-198">What characters are allowed in file path of Azure Backup policy using Azure Backup agent?</span></span> <br>
 <span data-ttu-id="6a9a9-199">Azure Backup 에이전트는 NTFS에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-199">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="6a9a9-200">파일 사양의 일부분으로 [NTFS 지원 문자](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-200">It enables [NTFS supported characters](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) as part of file specification.</span></span> 
 
### <a name="i-receive-the-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a><span data-ttu-id="6a9a9-201">백업 정책을 구성했는데도 "Azure Backup이 이 서버에 대해 구성되지 않았습니다"라는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-201">I receive the warning, "Azure Backups have not been configured for this server" even though I configured a backup policy</span></span> <br/>
<span data-ttu-id="6a9a9-202">이 경고는 로컬 서버에 저장된 백업 일정 설정과 백업 자격 증명 모음에 저장된 설정이 동일하지 않은 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-202">This warning occurs when the backup schedule settings stored on the local server are not the same as the settings stored in the backup vault.</span></span> <span data-ttu-id="6a9a9-203">서버 혹은 설정이 좋은 상태로 복구된 경우, 백업 일정은 동기화를 잃을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-203">When either the server or the settings have been recovered to a known good state, the backup schedules can lose synchronization.</span></span> <span data-ttu-id="6a9a9-204">이 경고가 발생하면 [백업 정책을 다시 구성](backup-azure-manage-windows-server.md) 한 다음 **지금 백업 실행** 을 수행하여 로컬 서버를 Azure와 다시 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9a9-204">If you receive this warning, [reconfigure the backup policy](backup-azure-manage-windows-server.md) and then **Run Back Up Now** to resynchronize the local server with Azure.</span></span>
