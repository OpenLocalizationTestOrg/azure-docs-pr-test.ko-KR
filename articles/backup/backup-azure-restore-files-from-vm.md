---
title: "Azure 백업: Azure VM 백업에서 파일 및 폴더 복구 | Microsoft Docs"
description: "Azure 가상 컴퓨터 복구 지점에서 파일 복구"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "항목 수준 복구, Azure 백업에서 파일 복구, Azure VM에서 파일 복원"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: ae7c345c11a7db25413d60ad822f16f84ca37362
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a><span data-ttu-id="3ba10-104">Azure Virtual Machine 백업에서 파일 복구</span><span class="sxs-lookup"><span data-stu-id="3ba10-104">Recover files from Azure virtual machine backup</span></span>

<span data-ttu-id="3ba10-105">Azure 백업에서는 Azure VM 백업에서 [Azure VM 및 디스크](./backup-azure-arm-restore-vms.md)를 복원하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-105">Azure backup provides the capability to restore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="3ba10-106">이제 이 문서에서는 Azure VM 백업에서 파일 및 폴더와 같은 항목을 어떻게 복구할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="3ba10-107">이 기능은 Resource Manager 모델을 사용하여 배포된 Azure VM에서 사용 가능하며 Recovery Services 자격 증명 모음에 대해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-107">This feature is available for Azure VMs deployed using the Resource Manager model and protected to a Recovery services vault.</span></span>
> <span data-ttu-id="3ba10-108">암호화된 VM 백업으로부터 파일 복구는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-the-volume-and-copy-files"></a><span data-ttu-id="3ba10-109">볼륨 탑재 및 파일 복사</span><span class="sxs-lookup"><span data-stu-id="3ba10-109">Mount the volume and copy files</span></span>

1. <span data-ttu-id="3ba10-110">[Azure 포털](http://portal.Azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-110">Sign into the [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="3ba10-111">관련 Recovery Services 자격 증명 모음 및 필요한 백업 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-111">Find the relevant Recovery services vault and the required backup item.</span></span>

2. <span data-ttu-id="3ba10-112">백업 항목 블레이드에서 **파일 복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-112">On the Backup Item blade, click **File Recovery**</span></span>

    ![Recovery Services 자격 증명 모음 백업 항목 열기](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="3ba10-114">**파일 복구** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-114">The **File Recovery** blade opens.</span></span>

    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="3ba10-116">**복구 지점 선택** 드롭다운 메뉴에서 원하는 파일이 들어 있는 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-116">From the **Select recovery point** drop-down menu, select the recovery point that contains the files you want.</span></span> <span data-ttu-id="3ba10-117">기본적으로 최신 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-117">By default, the latest recovery point is already selected.</span></span>

4. <span data-ttu-id="3ba10-118">**실행 파일 다운로드**(Windows Azure VM의 경우) 또는 **스크립트 다운로드**(Linux Azure VM의 경우)를 클릭하여 복구 지점에서 파일을 복사하는 데 사용할 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) to download the software that you'll use to copy files from the recovery point.</span></span>

  <span data-ttu-id="3ba10-119">실행 파일/스크립트는 로컬 컴퓨터와 지정된 복구 지점 간에 연결을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-119">The executable/script creates a connection between the local computer and the specified recovery point.</span></span>

5. <span data-ttu-id="3ba10-120">다운로드한 스크립트/실행 파일을 실행하려면 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-120">You need a password to run the downloaded script/executable.</span></span> <span data-ttu-id="3ba10-121">생성된 암호 옆에 있는 복사 단추를 사용하여 포털에서 암호를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-121">You can copy the password from the portal using the copy button beside the generated password</span></span>

    ![생성된 암호](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. <span data-ttu-id="3ba10-123">파일을 복구할 컴퓨터에서 실행 파일/스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-123">On the computer where you want to recover the files, run the executable/script.</span></span> <span data-ttu-id="3ba10-124">관리자 자격 증명으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-124">You must run it with Administrator credentials.</span></span> <span data-ttu-id="3ba10-125">제한된 액세스를 포함하는 컴퓨터에서 스크립트를 실행하는 경우 다음에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-125">If you run the script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="3ba10-126">download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3ba10-126">download.microsoft.com</span></span>
    - <span data-ttu-id="3ba10-127">Azure VM 백업에 사용된 Azure 끝점</span><span class="sxs-lookup"><span data-stu-id="3ba10-127">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="3ba10-128">아웃바운드 포트 3260</span><span class="sxs-lookup"><span data-stu-id="3ba10-128">outbound port 3260</span></span>

   <span data-ttu-id="3ba10-129">Linux의 경우 스크립트는 복구 지점에 연결하는 데 'open-iscsi' 및 'lshw' 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-129">For Linux, the script requires 'open-iscsi' and 'lshw' components to connect to the recovery point.</span></span> <span data-ttu-id="3ba10-130">해당 구성 요소가 실행되는 컴퓨터에 존재하지 않는 경우 관련 구성 요소를 설치할 수 있는 권한을 요청하고 승인 시 이를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-130">If those do not exist on the machine where it is run, it asks for permission to install the relevant components and installs them upon consent.</span></span>
   
   <span data-ttu-id="3ba10-131">암호를 입력하라는 메시지가 표시되면 포털에서 복사한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-131">Enter the password copied from the portal when prompted.</span></span> <span data-ttu-id="3ba10-132">올바른 암호를 입력하면 스크립트가 복구 지점에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-132">Once the valid password is entered the scripts connects to the recovery point.</span></span>
      
    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="3ba10-134">백업된 VM과 동일한(또는 호환) 운영 체제가 있는 모든 컴퓨터에서 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-134">You can run the script on any machine that has the same (or compatible) operating system as the backed-up VM.</span></span> <span data-ttu-id="3ba10-135">호환되는 운영 체제는 [호환되는 OS 표](backup-azure-restore-files-from-vm.md#compatible-os)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-135">See the [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="3ba10-136">보호된 Azure 가상 컴퓨터에서 Windows 저장소 공간(Windows Azure VM의 경우) 또는 LVM/RAID 배열(Linux VM의 경우)을 사용하는 경우 동일한 가상 컴퓨터에서 실행 파일/스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-136">If the protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run the executable/script on the same virtual machine.</span></span> <span data-ttu-id="3ba10-137">대신, 호환되는 운영 체제로 다른 컴퓨터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-137">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="3ba10-138">호환되는 OS</span><span class="sxs-lookup"><span data-stu-id="3ba10-138">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="3ba10-139">Windows의 경우</span><span class="sxs-lookup"><span data-stu-id="3ba10-139">For Windows</span></span>

<span data-ttu-id="3ba10-140">다음 표에서는 서버와 컴퓨터 운영 체제 간의 호환성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-140">The following table shows the compatibility between server and computer operating systems.</span></span> <span data-ttu-id="3ba10-141">파일을 복구할 경우 호환되지 않는 운영 체제 간에는 파일을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-141">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="3ba10-142">서버 OS</span><span class="sxs-lookup"><span data-stu-id="3ba10-142">Server OS</span></span> | <span data-ttu-id="3ba10-143">호환되는 클라이언트 OS</span><span class="sxs-lookup"><span data-stu-id="3ba10-143">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="3ba10-144">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3ba10-144">Windows Server 2012 R2</span></span> | <span data-ttu-id="3ba10-145">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3ba10-145">Windows 8.1</span></span> |
| <span data-ttu-id="3ba10-146">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3ba10-146">Windows Server 2012</span></span>    | <span data-ttu-id="3ba10-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="3ba10-147">Windows 8</span></span>  |
| <span data-ttu-id="3ba10-148">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3ba10-148">Windows Server 2008 R2</span></span> | <span data-ttu-id="3ba10-149">윈도우 7</span><span class="sxs-lookup"><span data-stu-id="3ba10-149">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="3ba10-150">Linux의 경우</span><span class="sxs-lookup"><span data-stu-id="3ba10-150">For Linux</span></span>

<span data-ttu-id="3ba10-151">Linux에서 기본적인 요구 사항은 스크립트를 실행하는 컴퓨터의 OS가 백업된 Linux VM에 있는 파일의 파일 시스템을 지원해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-151">In Linux, the fundamental requirement is that the OS of the machine where the script is run should support the filesystem of the files present in the backed-up Linux VM.</span></span> <span data-ttu-id="3ba10-152">스크립트를 실행하는 컴퓨터를 선택하는 동안 아래 표에서 설명했듯이 호환되는 OS 및 버전이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-152">While selecting a machine to run the script, please ensure it has the compatible OS and the versions as mentioned in the table below.</span></span>

|<span data-ttu-id="3ba10-153">Linux OS</span><span class="sxs-lookup"><span data-stu-id="3ba10-153">Linux OS</span></span> | <span data-ttu-id="3ba10-154">버전</span><span class="sxs-lookup"><span data-stu-id="3ba10-154">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="3ba10-155">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3ba10-155">Ubuntu</span></span> | <span data-ttu-id="3ba10-156">12.04 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-156">12.04 and above</span></span> |
| <span data-ttu-id="3ba10-157">CentOS</span><span class="sxs-lookup"><span data-stu-id="3ba10-157">CentOS</span></span> | <span data-ttu-id="3ba10-158">6.5 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-158">6.5 and above</span></span>  |
| <span data-ttu-id="3ba10-159">RHEL</span><span class="sxs-lookup"><span data-stu-id="3ba10-159">RHEL</span></span> | <span data-ttu-id="3ba10-160">6.7 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-160">6.7 and above</span></span> |
| <span data-ttu-id="3ba10-161">Debian</span><span class="sxs-lookup"><span data-stu-id="3ba10-161">Debian</span></span> | <span data-ttu-id="3ba10-162">7 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-162">7 and above</span></span> |
| <span data-ttu-id="3ba10-163">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="3ba10-163">Oracle Linux</span></span> | <span data-ttu-id="3ba10-164">6.4 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-164">6.4 and above</span></span> |

<span data-ttu-id="3ba10-165">스크립트는 복구 지점에 안전하게 연결하고 실행하기 위해 python 및 bash 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-165">The script also requires python and bash components to execute and connect securely to the recovery point.</span></span>

|<span data-ttu-id="3ba10-166">구성 요소</span><span class="sxs-lookup"><span data-stu-id="3ba10-166">Component</span></span> | <span data-ttu-id="3ba10-167">버전</span><span class="sxs-lookup"><span data-stu-id="3ba10-167">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="3ba10-168">bash</span><span class="sxs-lookup"><span data-stu-id="3ba10-168">bash</span></span> | <span data-ttu-id="3ba10-169">4 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-169">4 and above</span></span> |
| <span data-ttu-id="3ba10-170">python</span><span class="sxs-lookup"><span data-stu-id="3ba10-170">python</span></span> | <span data-ttu-id="3ba10-171">2.6.6 이상</span><span class="sxs-lookup"><span data-stu-id="3ba10-171">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="3ba10-172">볼륨 식별</span><span class="sxs-lookup"><span data-stu-id="3ba10-172">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="3ba10-173">Windows의 경우</span><span class="sxs-lookup"><span data-stu-id="3ba10-173">For Windows</span></span>

<span data-ttu-id="3ba10-174">실행 파일을 실행하면 운영 체제는 새 볼륨을 탑재하고 드라이브 문자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-174">When you run the exectuable, the operating system mounts the new volumes and assigns drive letters.</span></span> <span data-ttu-id="3ba10-175">Windows 탐색기 또는 파일 탐색기를 사용하여 해당 드라이브를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-175">You can use Windows Explorer or File Explorer to browse those drives.</span></span> <span data-ttu-id="3ba10-176">볼륨에 할당된 드라이브 문자는 원래 가상 컴퓨터와 다를 수 있지만 볼륨 이름은 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-176">The drive letters assigned to the volumes may not be the same letters as the original virtual machine, however, the volume name is preserved.</span></span> <span data-ttu-id="3ba10-177">예를 들어 원래 가상 컴퓨터에서 볼륨이 "데이터 디스크(E:\)"인 경우 해당 볼륨은 로컬 컴퓨터에서 "데이터 디스크('임의 드라이브 문자 사용 가능':\)로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-177">For example, if the volume on the original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on the local computer.</span></span> <span data-ttu-id="3ba10-178">사용자의 파일/폴더를 찾을 때까지 스크립트 출력에 나와 있는 모든 볼륨을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-178">Browse through all volumes mentioned in the script output until you find your files/folder.</span></span>  
       
   ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="3ba10-180">Linux의 경우</span><span class="sxs-lookup"><span data-stu-id="3ba10-180">For Linux</span></span>

<span data-ttu-id="3ba10-181">Linux에서 복구 지점의 볼륨은 스크립트가 실행되는 폴더에 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-181">In Linux, the volumes of the recovery point are mounted to the folder where the script is run.</span></span> <span data-ttu-id="3ba10-182">연결된 디스크, 볼륨 및 해당 탑재 경로는 적절하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-182">The attached disks, volumes and the corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="3ba10-183">이러한 탑재 경로는 루트 수준 액세스 권한이 있는 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-183">These mount paths are visible to users having root level access.</span></span> <span data-ttu-id="3ba10-184">스크립트 출력에서 언급한 볼륨을 통해 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-184">Browse through the volumes mentioned in the script output.</span></span>

  ![Linux 파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a><span data-ttu-id="3ba10-186">연결 닫기</span><span class="sxs-lookup"><span data-stu-id="3ba10-186">Closing the connection</span></span>

<span data-ttu-id="3ba10-187">파일을 식별하고 로컬 저장소 위치에 복사한 후에는 추가 드라이브를 제거(또는 분리)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-187">After identifying the files and copying them to a local storage location, remove (or unmount) the additional drives.</span></span> <span data-ttu-id="3ba10-188">드라이브를 분리하려면 Azure Portal의 **파일 복구** 블레이드에서 **디스크 분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-188">To unmount the drives, on the **File Recovery** blade in the Azure portal, click **Unmount Disks**.</span></span>

![디스크 분리](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="3ba10-190">디스크가 분리되었으면 분리에 성공했다는 메시지가 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-190">Once the disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="3ba10-191">디스크를 제거할 수 있도록 연결을 새로 고치는 데 몇 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-191">It may take a few minutes for the connection to refresh so that you can remove the disks.</span></span>

<span data-ttu-id="3ba10-192">Linux에서 복구 지점에 대한 연결이 단절된 후 OS는 해당 탑재 경로를 자동으로 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-192">In Linux, after the connection to the recovery point is severed, the OS doesn't remove the corresponding mount paths automatically.</span></span> <span data-ttu-id="3ba10-193">이는 "분리된" 볼륨으로 존재하고 표시되지만 파일에 액세스하거나 파일을 작성할 때 오류를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-193">These exist as "orphan" volumes and they are visible but throw an error when you access/write the files.</span></span> <span data-ttu-id="3ba10-194">수동으로 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-194">They can be manually removed.</span></span> <span data-ttu-id="3ba10-195">스크립트는 실행 시 모든 이전 복구 지점에서 존재하는 이러한 볼륨을 식별하고 승인 시 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-195">The script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="3ba10-196">특수 구성</span><span class="sxs-lookup"><span data-stu-id="3ba10-196">Special configurations</span></span>

### <a name="dynamic-disks"></a><span data-ttu-id="3ba10-197">동적 디스크</span><span class="sxs-lookup"><span data-stu-id="3ba10-197">Dynamic Disks</span></span>

<span data-ttu-id="3ba10-198">백업된 Azure VM에 여러 디스크에 걸쳐 있는 볼륨(스팬 볼륨 및 스트라이프 볼륨) 및/또는 내결함성 볼륨(미러 볼륨 및 RAID-5 볼륨)이 있는 경우 동일한 VM에서 실행 가능한 스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-198">If the Azure VM that was backed up has volumes that span multiple disks (spanned and striped volumes) and/or fault-tolerant volumes (mirrored and RAID-5 volumes) on dynamic disks, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="3ba10-199">대신, 호환되는 운영 체제로 다른 컴퓨터에서 실행 가능한 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-199">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="3ba10-200">Windows 저장소 공간</span><span class="sxs-lookup"><span data-stu-id="3ba10-200">Windows Storage Spaces</span></span>

<span data-ttu-id="3ba10-201">Windows 저장소 공간은 저장소를 가상화할 수 있는 Windows 저장소의 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-201">Windows Storage Spaces is a technology in Windows storage that enables you to virtualize storage.</span></span> <span data-ttu-id="3ba10-202">Windows 저장소 공간으로 업계 표준 디스크를 저장소 풀로 그룹화한 후 해당 저장소 풀에 제공되는 공간에서 저장소 공간이라는 가상 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-202">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from the available space in those storage pools.</span></span>

<span data-ttu-id="3ba10-203">백업된 Azure VM에서 Windows 저장소 공간을 사용하는 경우 동일한 VM에서는 실행 가능한 스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-203">If the Azure VM that was backed up uses Windows Storage Spaces, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="3ba10-204">대신, 호환되는 운영 체제로 다른 컴퓨터에서 실행 가능한 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-204">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="3ba10-205">LVM/RAID 배열</span><span class="sxs-lookup"><span data-stu-id="3ba10-205">LVM/RAID Arrays</span></span>

<span data-ttu-id="3ba10-206">Linux에서 LVM(논리 볼륨 관리자) 및/또는 소프트웨어 RAID 배열은 여러 디스크에 걸쳐 논리 볼륨을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-206">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used to manage logical volumes over multiple disks.</span></span> <span data-ttu-id="3ba10-207">백업된 Linux VM에서 LVM 및/또는 RAID 배열을 사용하는 경우 동일한 VM에서 스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-207">If the backed up Linux VM uses LVM and/or RAID Arrays, you can't run the script on the same VM.</span></span> <span data-ttu-id="3ba10-208">대신 호환되는 OS로 다른 컴퓨터에서 스크립트를 실행하고 백업된 VM의 파일 시스템을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-208">Instead run the script on any other machine with compatible OS and which supports filesystem of the backed up VM.</span></span>

<span data-ttu-id="3ba10-209">스크립트 출력은 아래와 같이 파티션 형식으로 LVM 및/또는 RAID 배열 디스크 및 볼륨을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-209">The script output displays the LVM and/or RAID Arrays disks and the volumes with the partition type as shown below</span></span>

   ![Linux LVM 출력 블레이드](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="3ba10-211">사용자는 해당 파티션을 온라인 상태로 전환하기 위해 다음 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-211">The following commands need to be run by the user to bring these partitions online.</span></span> 

<span data-ttu-id="3ba10-212">**LVM 파티션의 경우**</span><span class="sxs-lookup"><span data-stu-id="3ba10-212">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in the script output> 
```
<span data-ttu-id="3ba10-213">실제 볼륨에 볼륨 그룹 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-213">This lists the volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
<span data-ttu-id="3ba10-214">볼륨 그룹에 모든 논리 볼륨, 이름 및 해당 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-214">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="3ba10-215">선택한 경로에 논리 볼륨을 탑재하려면.</span><span class="sxs-lookup"><span data-stu-id="3ba10-215">To mount the logical volumes to the path of your choice.</span></span>


<span data-ttu-id="3ba10-216">**RAID 배열의 경우**</span><span class="sxs-lookup"><span data-stu-id="3ba10-216">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="3ba10-217">모든 raid 디스크에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-217">This displays details about all raid disks.</span></span> <span data-ttu-id="3ba10-218">관련 RAID 디스크는 `/dev/mdm/<RAID array name in the backed up VM>`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-218">The relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in the backed up VM>`</span></span>

<span data-ttu-id="3ba10-219">RAID 디스크에 실제 볼륨이 있는 경우 탑재 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-219">Use the mount command if the RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="3ba10-220">이 RAID 디스크에 다른 LVM이 구성된 경우 RAID 디스크 이름이 되는 볼륨 이름으로 LVM 파티션에 대해 위에서 설명한 것과 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-220">If this RAID disk has another LVM configured in it then follow the same procedure as outlined above for LVM partitions with the volume name being the RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3ba10-221">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3ba10-221">Troubleshooting</span></span>

<span data-ttu-id="3ba10-222">가상 컴퓨터에서 파일을 복구하는 동안 문제가 생기는 경우 다음 표에서 추가 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-222">If you have problems while recovering files from the virtual machines, check the following table for additional information.</span></span>

| <span data-ttu-id="3ba10-223">오류 메시지/시나리오</span><span class="sxs-lookup"><span data-stu-id="3ba10-223">Error Message / Scenario</span></span> | <span data-ttu-id="3ba10-224">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="3ba10-224">Probable Cause</span></span> | <span data-ttu-id="3ba10-225">권장 작업</span><span class="sxs-lookup"><span data-stu-id="3ba10-225">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="3ba10-226">Exe 출력: *대상에 연결하는 동안 예외가 발생했습니다.*</span><span class="sxs-lookup"><span data-stu-id="3ba10-226">Exe output: *Exception connecting to the target*</span></span> |<span data-ttu-id="3ba10-227">스크립트가 복구 지점에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-227">Script is not able to access the recovery point</span></span> | <span data-ttu-id="3ba10-228">컴퓨터가 위에 설명된 액세스 요구 사항을 충족하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-228">Check whether the machine fulfills the access requirements mentioned above</span></span>|  
|   <span data-ttu-id="3ba10-229">Exe 출력: *ISCSI 세션을 통해 대상이 이미 로그인되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="3ba10-229">Exe output: *The target has already been logged in via an ISCSI session.*</span></span> | <span data-ttu-id="3ba10-230">동일한 컴퓨터에서 스크립트가 이미 실행되었고 드라이브가 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-230">The script was already executed on the same machine and the drives have been attached</span></span> | <span data-ttu-id="3ba10-231">복구 지점의 볼륨이 이미 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-231">The volumes of the recovery point have already been attached.</span></span> <span data-ttu-id="3ba10-232">원래 VM과 동일한 드라이브 문자로 탑재되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-232">They may NOT be mounted with the same drive letters of the original VM.</span></span> <span data-ttu-id="3ba10-233">파일 탐색기에서 사용 가능한 모든 볼륨을 탐색하여 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-233">Browse through all the available volumes in the file explorer for your file</span></span> |
| <span data-ttu-id="3ba10-234">Exe 출력: *디스크가 포털을 통해 분리되었고 12시간 제한을 초과했으므로 이 스크립트는 유효하지 않습니다. 포털에서 새 스크립트를 다운로드하세요.*</span><span class="sxs-lookup"><span data-stu-id="3ba10-234">Exe output: *This script is invalid because the disks have been dismounted via portal/exceeded the 12-hr limit. Please download a new script from the portal.*</span></span> |  <span data-ttu-id="3ba10-235">디스크가 포털에서 분리되었거나 12시간 제한을 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-235">The disks have been dismounted from the portal or the 12-hr limit exceeded</span></span> |    <span data-ttu-id="3ba10-236">이 특정 exe는 현재 유효하지 않고 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-236">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="3ba10-237">복구 지정 시간의 파일에 액세스하려면 포털에서 새 exe를 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-237">If you want to access the files of that recovery point-in-time, visit the portal for a new exe</span></span>|
| <span data-ttu-id="3ba10-238">exe가 실행되는 컴퓨터에서: 분리 단추를 클릭하면 새 볼륨이 분리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-238">On the machine where the exe is run: The new volumes are not dismounted after the dismount button is clicked</span></span> |    <span data-ttu-id="3ba10-239">컴퓨터에서 ISCSI 초기자가 응답하지 않거나 대상에 대한 연결을 새로 고치지 않고 캐시를 유지 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-239">The ISCSI initiator on the machine is not responding/refreshing its connection to the target and maintaining the cache</span></span> |    <span data-ttu-id="3ba10-240">분리 단추를 누른 후 몇 분 정도 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-240">Wait for some mins after the dismount button is pressed.</span></span> <span data-ttu-id="3ba10-241">새 볼륨이 계속 분리되지 않으면 모든 볼륨을 탐색하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba10-241">If the new volumes are still not dismounted, please browse through all the volumes.</span></span> <span data-ttu-id="3ba10-242">이렇게 하면 초기자가 강제로 연결을 새로 고치도록 하여 디스크를 사용할 수 없다는 오류 메시지와 함께 볼륨이 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-242">This forces the initiator to refresh the connection and the volume is dismounted with an error message that the disk is not available</span></span>|
| <span data-ttu-id="3ba10-243">Exe 출력: 스크립트가 성공적으로 실행되지만 스크립트 출력에 "New volumes attached(새 볼륨 연결됨)"이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-243">Exe output: Script is run successfully but “New volumes attached” is not displayed on the script output</span></span> | <span data-ttu-id="3ba10-244">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-244">This is a transient error</span></span>   | <span data-ttu-id="3ba10-245">볼륨은 이미 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-245">The volumes would have been already attached.</span></span> <span data-ttu-id="3ba10-246">Explorer를 열어 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-246">Open Explorer to browse.</span></span> <span data-ttu-id="3ba10-247">스크립트를 실행할 때마다 동일한 컴퓨터를 사용하는 경우 컴퓨터를 다시 시작하면 목록이 후속 exe 실행에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-247">If you are using the same machine for running scripts every time, consider restarting the machine and the list should be displayed in the subsequent exe runs.</span></span> |
| <span data-ttu-id="3ba10-248">Linux 특정: 원하는 볼륨을 볼 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="3ba10-248">Linux specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="3ba10-249">스크립트가 실행되는 컴퓨터의 OS는 백업된 VM의 기본 파일 시스템을 인식하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-249">The OS of the machine where the script is run may not recognize the underlying filesystem of the backed up VM</span></span> | <span data-ttu-id="3ba10-250">복구 지점이 충돌 일관성 또는 파일 일관성인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-250">Check whether the recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="3ba10-251">파일 일관성인 경우 OS가 백업된 VM의 파일 시스템을 인식하는 다른 컴퓨터에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-251">If file consistent, run the script on another machine whose OS recognizes the backed up VM's filesystem</span></span> |
| <span data-ttu-id="3ba10-252">Windows 특정: 원하는 볼륨을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-252">Windows specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="3ba10-253">디스크가 연결되었을 수도 있지만 볼륨이 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-253">The disks may have been attached but the volumes were not configured</span></span> | <span data-ttu-id="3ba10-254">디스크 관리 화면에서 복구 지점과 관련된 추가 디스크를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-254">From the disk management screen, identify the additional disks related to the recovery point.</span></span> <span data-ttu-id="3ba10-255">이러한 디스크가 오프라인 상태이면 디스크를 마우스 오른쪽 단추로 클릭하고 '온라인'을 클릭하여 온라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba10-255">If any of these disks are in offline state try making them online by right-clicking on the disk and click 'Online'</span></span>|
