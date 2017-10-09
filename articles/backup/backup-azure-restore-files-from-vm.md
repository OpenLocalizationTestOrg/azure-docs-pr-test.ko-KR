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
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a><span data-ttu-id="178eb-104">Azure Virtual Machine 백업에서 파일 복구</span><span class="sxs-lookup"><span data-stu-id="178eb-104">Recover files from Azure virtual machine backup</span></span>

<span data-ttu-id="178eb-105">Azure 백업 기능은 hello 기능 toorestore [Azure Vm 및 디스크](./backup-azure-arm-restore-vms.md) Azure VM 백업에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-105">Azure backup provides hello capability toorestore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="178eb-106">이제 이 문서에서는 Azure VM 백업에서 파일 및 폴더와 같은 항목을 어떻게 복구할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="178eb-107">이 기능은 hello 리소스 관리자 모델 및 보호 된 tooa 복구 서비스 자격 증명 모음을 사용 하 여 배포 하는 Azure Vm에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-107">This feature is available for Azure VMs deployed using hello Resource Manager model and protected tooa Recovery services vault.</span></span>
> <span data-ttu-id="178eb-108">암호화된 VM 백업으로부터 파일 복구는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-hello-volume-and-copy-files"></a><span data-ttu-id="178eb-109">Hello 볼륨 및 복사 파일 탑재</span><span class="sxs-lookup"><span data-stu-id="178eb-109">Mount hello volume and copy files</span></span>

1. <span data-ttu-id="178eb-110">Hello에 로그인 [Azure 포털](http://portal.Azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-110">Sign into hello [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="178eb-111">Hello 관련 복구 서비스 자격 증명 모음 및 백업 hello 필요한 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-111">Find hello relevant Recovery services vault and hello required backup item.</span></span>

2. <span data-ttu-id="178eb-112">Hello 백업 항목 블레이드에서 클릭 **파일 복구**</span><span class="sxs-lookup"><span data-stu-id="178eb-112">On hello Backup Item blade, click **File Recovery**</span></span>

    ![Recovery Services 자격 증명 모음 백업 항목 열기](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="178eb-114">hello **파일 복구** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-114">hello **File Recovery** blade opens.</span></span>

    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="178eb-116">Hello에서 **복구 지점을 선택** 원하는 hello 파일이 포함 된 select hello 복구 지점, 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="178eb-116">From hello **Select recovery point** drop-down menu, select hello recovery point that contains hello files you want.</span></span> <span data-ttu-id="178eb-117">기본적으로 이미 hello 최신 복구 지점을 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-117">By default, hello latest recovery point is already selected.</span></span>

4. <span data-ttu-id="178eb-118">클릭 **실행 파일을 다운로드** (용 Windows Azure VM의 경우) 또는 **스크립트 다운로드** (Azure Linux VM)에 대 한 toodownload hello 소프트웨어 hello 복구 지점에서 toocopy 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) toodownload hello software that you'll use toocopy files from hello recovery point.</span></span>

  <span data-ttu-id="178eb-119">hello 실행/스크립팅 간의 연결을 만듭니다 hello 로컬 컴퓨터와 hello 지정 된 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-119">hello executable/script creates a connection between hello local computer and hello specified recovery point.</span></span>

5. <span data-ttu-id="178eb-120">암호 toorun hello 다운로드 한 스크립트/실행 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-120">You need a password toorun hello downloaded script/executable.</span></span> <span data-ttu-id="178eb-121">생성 된 hello 암호 옆에 있는 hello 복사 단추를 사용 하 여 hello 포털에서 hello 암호를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-121">You can copy hello password from hello portal using hello copy button beside hello generated password</span></span>

    ![생성된 암호](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. <span data-ttu-id="178eb-123">Hello toorecover hello 파일을 컴퓨터에서 실행 hello 실행/스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-123">On hello computer where you want toorecover hello files, run hello executable/script.</span></span> <span data-ttu-id="178eb-124">관리자 자격 증명으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-124">You must run it with Administrator credentials.</span></span> <span data-ttu-id="178eb-125">제한 된 액세스 된 컴퓨터에 hello 스크립트를 실행 하는 경우에 액세스할 수 있는지 확인:</span><span class="sxs-lookup"><span data-stu-id="178eb-125">If you run hello script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="178eb-126">download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="178eb-126">download.microsoft.com</span></span>
    - <span data-ttu-id="178eb-127">Azure VM 백업에 사용된 Azure 끝점</span><span class="sxs-lookup"><span data-stu-id="178eb-127">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="178eb-128">아웃바운드 포트 3260</span><span class="sxs-lookup"><span data-stu-id="178eb-128">outbound port 3260</span></span>

   <span data-ttu-id="178eb-129">Linux 용 hello 스크립트에 필요한 ' 오픈 iscsi' 및 'lshw' 구성 요소 tooconnect toohello 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-129">For Linux, hello script requires 'open-iscsi' and 'lshw' components tooconnect toohello recovery point.</span></span> <span data-ttu-id="178eb-130">된 hello 컴퓨터 실행 되는 위치에 존재 하지 않는 경우 권한 tooinstall hello 관련 구성 요소를 요청 하 고 승인 시이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-130">If those do not exist on hello machine where it is run, it asks for permission tooinstall hello relevant components and installs them upon consent.</span></span>
   
   <span data-ttu-id="178eb-131">메시지가 표시 되 면 hello 포털에서 복사 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-131">Enter hello password copied from hello portal when prompted.</span></span> <span data-ttu-id="178eb-132">Hello 유효한 암호를 입력 한 후 hello 스크립트 toohello 복구 지점을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-132">Once hello valid password is entered hello scripts connects toohello recovery point.</span></span>
      
    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="178eb-134">Hello 백업 VM으로 동일한 (또는 호환) hello 운영 체제는 모든 컴퓨터에 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-134">You can run hello script on any machine that has hello same (or compatible) operating system as hello backed-up VM.</span></span> <span data-ttu-id="178eb-135">Hello 참조 [호환 OS 테이블](backup-azure-restore-files-from-vm.md#compatible-os) 호환 되는 운영 체제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-135">See hello [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="178eb-136">이면 hello 보호 Azure 가상 컴퓨터 사용 (Windows Azure Vm)에 대 한 Windows 저장소 공간 또는 LVM/RAID Arrays(for Linux VMs) 하면에서 hello 실행 파일/스크립트를 실행할 수 없습니다 hello 동일한 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="178eb-136">If hello protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run hello executable/script on hello same virtual machine.</span></span> <span data-ttu-id="178eb-137">대신, 호환되는 운영 체제로 다른 컴퓨터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-137">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="178eb-138">호환되는 OS</span><span class="sxs-lookup"><span data-stu-id="178eb-138">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="178eb-139">Windows의 경우</span><span class="sxs-lookup"><span data-stu-id="178eb-139">For Windows</span></span>

<span data-ttu-id="178eb-140">테이블 표시 hello 호환성 서버와 컴퓨터 운영 체제 간의 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-140">hello following table shows hello compatibility between server and computer operating systems.</span></span> <span data-ttu-id="178eb-141">파일을 복구할 경우 호환되지 않는 운영 체제 간에는 파일을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-141">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="178eb-142">서버 OS</span><span class="sxs-lookup"><span data-stu-id="178eb-142">Server OS</span></span> | <span data-ttu-id="178eb-143">호환되는 클라이언트 OS</span><span class="sxs-lookup"><span data-stu-id="178eb-143">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="178eb-144">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="178eb-144">Windows Server 2012 R2</span></span> | <span data-ttu-id="178eb-145">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="178eb-145">Windows 8.1</span></span> |
| <span data-ttu-id="178eb-146">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="178eb-146">Windows Server 2012</span></span>    | <span data-ttu-id="178eb-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="178eb-147">Windows 8</span></span>  |
| <span data-ttu-id="178eb-148">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="178eb-148">Windows Server 2008 R2</span></span> | <span data-ttu-id="178eb-149">윈도우 7</span><span class="sxs-lookup"><span data-stu-id="178eb-149">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="178eb-150">Linux의 경우</span><span class="sxs-lookup"><span data-stu-id="178eb-150">For Linux</span></span>

<span data-ttu-id="178eb-151">Linux에서 hello 기본 요구 사항은 hello 파일 시스템을 지원 해야 하는 hello 스크립트가 실행 되는 hello 컴퓨터의 해당 hello 운영 체제의 hello hello에 있는 파일 백업 Linux VM입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-151">In Linux, hello fundamental requirement is that hello OS of hello machine where hello script is run should support hello filesystem of hello files present in hello backed-up Linux VM.</span></span> <span data-ttu-id="178eb-152">컴퓨터 toorun hello 스크립트를 선택 하는 동안 hello 테이블 아래에 설명 된 대로 hello 호환 되는 OS 및 hello 버전을에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="178eb-152">While selecting a machine toorun hello script, please ensure it has hello compatible OS and hello versions as mentioned in hello table below.</span></span>

|<span data-ttu-id="178eb-153">Linux OS</span><span class="sxs-lookup"><span data-stu-id="178eb-153">Linux OS</span></span> | <span data-ttu-id="178eb-154">버전</span><span class="sxs-lookup"><span data-stu-id="178eb-154">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="178eb-155">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="178eb-155">Ubuntu</span></span> | <span data-ttu-id="178eb-156">12.04 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-156">12.04 and above</span></span> |
| <span data-ttu-id="178eb-157">CentOS</span><span class="sxs-lookup"><span data-stu-id="178eb-157">CentOS</span></span> | <span data-ttu-id="178eb-158">6.5 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-158">6.5 and above</span></span>  |
| <span data-ttu-id="178eb-159">RHEL</span><span class="sxs-lookup"><span data-stu-id="178eb-159">RHEL</span></span> | <span data-ttu-id="178eb-160">6.7 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-160">6.7 and above</span></span> |
| <span data-ttu-id="178eb-161">Debian</span><span class="sxs-lookup"><span data-stu-id="178eb-161">Debian</span></span> | <span data-ttu-id="178eb-162">7 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-162">7 and above</span></span> |
| <span data-ttu-id="178eb-163">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="178eb-163">Oracle Linux</span></span> | <span data-ttu-id="178eb-164">6.4 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-164">6.4 and above</span></span> |

<span data-ttu-id="178eb-165">hello 스크립트도 필요 python 및 구성 요소 tooexecute를 이용한 적 하 고 toohello 복구 지점에 안전 하 게 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-165">hello script also requires python and bash components tooexecute and connect securely toohello recovery point.</span></span>

|<span data-ttu-id="178eb-166">구성 요소</span><span class="sxs-lookup"><span data-stu-id="178eb-166">Component</span></span> | <span data-ttu-id="178eb-167">버전</span><span class="sxs-lookup"><span data-stu-id="178eb-167">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="178eb-168">bash</span><span class="sxs-lookup"><span data-stu-id="178eb-168">bash</span></span> | <span data-ttu-id="178eb-169">4 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-169">4 and above</span></span> |
| <span data-ttu-id="178eb-170">python</span><span class="sxs-lookup"><span data-stu-id="178eb-170">python</span></span> | <span data-ttu-id="178eb-171">2.6.6 이상</span><span class="sxs-lookup"><span data-stu-id="178eb-171">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="178eb-172">볼륨 식별</span><span class="sxs-lookup"><span data-stu-id="178eb-172">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="178eb-173">Windows의 경우</span><span class="sxs-lookup"><span data-stu-id="178eb-173">For Windows</span></span>

<span data-ttu-id="178eb-174">Hello 사용 하 여 실행을 실행 하면 hello 운영 체제 hello 새 볼륨을 탑재 하 고 드라이브 문자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-174">When you run hello exectuable, hello operating system mounts hello new volumes and assigns drive letters.</span></span> <span data-ttu-id="178eb-175">Windows 탐색기 또는 파일 탐색기 toobrowse 해당 드라이브를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-175">You can use Windows Explorer or File Explorer toobrowse those drives.</span></span> <span data-ttu-id="178eb-176">그러나 hello toohello 볼륨에 할당 된 드라이브 문자 아닐 수도 있습니다 hello 동일한 문자 hello 원래 가상 컴퓨터 hello 볼륨 이름으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-176">hello drive letters assigned toohello volumes may not be hello same letters as hello original virtual machine, however, hello volume name is preserved.</span></span> <span data-ttu-id="178eb-177">예를 들어 hello 볼륨 hello 원래 가상 컴퓨터에이 경우 "데이터 디스크 (e:\)", 볼륨으로 연결할 수 있습니다 "데이터 디스크 ('사용 가능한 드라이브 문자는 ':\) hello 로컬 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-177">For example, if hello volume on hello original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on hello local computer.</span></span> <span data-ttu-id="178eb-178">파일/폴더를 찾을 때까지 hello 스크립트 출력에 언급 된 모든 볼륨을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-178">Browse through all volumes mentioned in hello script output until you find your files/folder.</span></span>  
       
   ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="178eb-180">Linux의 경우</span><span class="sxs-lookup"><span data-stu-id="178eb-180">For Linux</span></span>

<span data-ttu-id="178eb-181">Linux에서 hello 복구 지점의 hello 볼륨에 탑재 된 toohello 폴더 hello 스크립트가 실행 되는.</span><span class="sxs-lookup"><span data-stu-id="178eb-181">In Linux, hello volumes of hello recovery point are mounted toohello folder where hello script is run.</span></span> <span data-ttu-id="178eb-182">hello 연결 된 디스크, 볼륨 및 hello 해당 탑재 경로 적절 하 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-182">hello attached disks, volumes and hello corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="178eb-183">이러한 탑재 경로 표시 toousers 루트 수준 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-183">These mount paths are visible toousers having root level access.</span></span> <span data-ttu-id="178eb-184">Hello 스크립트 출력에서 언급 한 hello 볼륨을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-184">Browse through hello volumes mentioned in hello script output.</span></span>

  ![Linux 파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a><span data-ttu-id="178eb-186">Hello 연결을 닫는 중</span><span class="sxs-lookup"><span data-stu-id="178eb-186">Closing hello connection</span></span>

<span data-ttu-id="178eb-187">Hello 파일을 확인 하 고 tooa 로컬 저장소 위치를 복사, 제거 또는 분리 hello 추가 드라이브.</span><span class="sxs-lookup"><span data-stu-id="178eb-187">After identifying hello files and copying them tooa local storage location, remove (or unmount) hello additional drives.</span></span> <span data-ttu-id="178eb-188">hello에 toounmount hello 드라이브 **파일 복구** 블레이드 hello Azure 포털에서에서 클릭 **디스크 분리**합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-188">toounmount hello drives, on hello **File Recovery** blade in hello Azure portal, click **Unmount Disks**.</span></span>

![디스크 분리](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="178eb-190">Hello 디스크 탑재 되지 않은, 되 면 성공 했는지 알려주는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-190">Once hello disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="178eb-191">Hello 디스크를 제거할 수 있도록 hello 연결 toorefresh 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-191">It may take a few minutes for hello connection toorefresh so that you can remove hello disks.</span></span>

<span data-ttu-id="178eb-192">Linux에서 끊어지면 hello 연결점 toohello 복구 후 hello OS 제거 되지 않습니다 탑재 경로 해당 하는 hello 자동으로.</span><span class="sxs-lookup"><span data-stu-id="178eb-192">In Linux, after hello connection toohello recovery point is severed, hello OS doesn't remove hello corresponding mount paths automatically.</span></span> <span data-ttu-id="178eb-193">이러한 메서드는 "분리" 볼륨으로 존재 하 고 때 하면 액세스/쓰기 hello 파일 오류를 throw 되지만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-193">These exist as "orphan" volumes and they are visible but throw an error when you access/write hello files.</span></span> <span data-ttu-id="178eb-194">수동으로 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-194">They can be manually removed.</span></span> <span data-ttu-id="178eb-195">모든 이전 복구 지점에서 기존 이러한 볼륨을 식별 하 고 승인 시 정리 하는 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-195">hello script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="178eb-196">특수 구성</span><span class="sxs-lookup"><span data-stu-id="178eb-196">Special configurations</span></span>

### <a name="dynamic-disks"></a><span data-ttu-id="178eb-197">동적 디스크</span><span class="sxs-lookup"><span data-stu-id="178eb-197">Dynamic Disks</span></span>

<span data-ttu-id="178eb-198">다음에서 hello 실행 스크립트를 실행할 수 없습니다 hello 백업 된 Azure VM에 볼륨이 여러 디스크 (스팬 및 스트라이프 볼륨) 및/또는 동적 디스크에 내결함성 (미러된 및 raid-5 볼륨) 볼륨에 걸쳐 있는 경우 동일한 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-198">If hello Azure VM that was backed up has volumes that span multiple disks (spanned and striped volumes) and/or fault-tolerant volumes (mirrored and RAID-5 volumes) on dynamic disks, then you can't run hello executable script on hello same VM.</span></span> <span data-ttu-id="178eb-199">대신, 호환 되는 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 실행 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-199">Instead, run hello executable script on any other machine with a compatible operating system.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="178eb-200">Windows 저장소 공간</span><span class="sxs-lookup"><span data-stu-id="178eb-200">Windows Storage Spaces</span></span>

<span data-ttu-id="178eb-201">Windows 저장소 공간에 toovirtualize 저장소를 사용 하면 Windows 저장소에 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-201">Windows Storage Spaces is a technology in Windows storage that enables you toovirtualize storage.</span></span> <span data-ttu-id="178eb-202">Windows 저장소 공간 사용 업계 표준 디스크를 저장소 풀으로 그룹화 하 고 해당 저장소 풀의 사용 가능한 공간 hello에서에서 저장소 공간 이라는 가상 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-202">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from hello available space in those storage pools.</span></span>

<span data-ttu-id="178eb-203">Hello 백업 된 Azure VM hello 실행 스크립트를 실행할 수 없습니다 Windows 저장소 공간을 사용 하는 경우 동일한 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-203">If hello Azure VM that was backed up uses Windows Storage Spaces, then you can't run hello executable script on hello same VM.</span></span> <span data-ttu-id="178eb-204">대신, 호환 되는 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 실행 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-204">Instead, run hello executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="178eb-205">LVM/RAID 배열</span><span class="sxs-lookup"><span data-stu-id="178eb-205">LVM/RAID Arrays</span></span>

<span data-ttu-id="178eb-206">Linux, 논리 볼륨 관리자 (LVM) 및/또는 소프트웨어에 RAID 배열은 여러 디스크에 걸쳐 사용 되는 toomanage 논리 볼륨을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-206">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used toomanage logical volumes over multiple disks.</span></span> <span data-ttu-id="178eb-207">Hello에서 hello 스크립트를 실행할 수 없습니다 Linux VM을 백업 하는 hello LVM 및/또는 RAID 배열을 사용 하는 경우 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-207">If hello backed up Linux VM uses LVM and/or RAID Arrays, you can't run hello script on hello same VM.</span></span> <span data-ttu-id="178eb-208">대신 호환 가능한 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 스크립트를 실행 하 고 VM을 백업 하는 hello의 파일 시스템을 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-208">Instead run hello script on any other machine with compatible OS and which supports filesystem of hello backed up VM.</span></span>

<span data-ttu-id="178eb-209">hello 스크립트 출력 LVM hello 및/또는 RAID 배열 디스크와 hello 볼륨 아래와 같이 hello 파티션 형식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-209">hello script output displays hello LVM and/or RAID Arrays disks and hello volumes with hello partition type as shown below</span></span>

   ![Linux LVM 출력 블레이드](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="178eb-211">다음 hello toobe 실행 hello 사용자 toobring 하 여 이러한 파티션을 온라인 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-211">hello following commands need toobe run by hello user toobring these partitions online.</span></span> 

<span data-ttu-id="178eb-212">**LVM 파티션의 경우**</span><span class="sxs-lookup"><span data-stu-id="178eb-212">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in hello script output> 
```
<span data-ttu-id="178eb-213">이 실제 볼륨에 hello 볼륨 그룹 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-213">This lists hello volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
<span data-ttu-id="178eb-214">볼륨 그룹에 모든 논리 볼륨, 이름 및 해당 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-214">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="178eb-215">hello 논리 볼륨 toohello 경로 선택한 toomount 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-215">toomount hello logical volumes toohello path of your choice.</span></span>


<span data-ttu-id="178eb-216">**RAID 배열의 경우**</span><span class="sxs-lookup"><span data-stu-id="178eb-216">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="178eb-217">모든 raid 디스크에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-217">This displays details about all raid disks.</span></span> <span data-ttu-id="178eb-218">hello 관련 RAID 디스크도 표시 됩니다.`/dev/mdm/<RAID array name in hello backed up VM>`</span><span class="sxs-lookup"><span data-stu-id="178eb-218">hello relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in hello backed up VM>`</span></span>

<span data-ttu-id="178eb-219">Hello RAID 디스크에 실제 볼륨 경우 hello mount 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-219">Use hello mount command if hello RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="178eb-220">따라야 합니다 LVM 파티션에 대 한 hello RAID 디스크 이름 되 고 hello 볼륨 이름으로 위에서 설명한 것과 동일한 절차 hello이 RAID 디스크의 다른 LVM 여기에 구성 된 경우</span><span class="sxs-lookup"><span data-stu-id="178eb-220">If this RAID disk has another LVM configured in it then follow hello same procedure as outlined above for LVM partitions with hello volume name being hello RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="178eb-221">문제 해결</span><span class="sxs-lookup"><span data-stu-id="178eb-221">Troubleshooting</span></span>

<span data-ttu-id="178eb-222">Hello 가상 컴퓨터에서 파일을 복구 하는 동안 문제가 되 면 hello 다음 추가 정보에 대 한 표를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-222">If you have problems while recovering files from hello virtual machines, check hello following table for additional information.</span></span>

| <span data-ttu-id="178eb-223">오류 메시지/시나리오</span><span class="sxs-lookup"><span data-stu-id="178eb-223">Error Message / Scenario</span></span> | <span data-ttu-id="178eb-224">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="178eb-224">Probable Cause</span></span> | <span data-ttu-id="178eb-225">권장 작업</span><span class="sxs-lookup"><span data-stu-id="178eb-225">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="178eb-226">Exe 출력: *toohello 대상 연결 예외*</span><span class="sxs-lookup"><span data-stu-id="178eb-226">Exe output: *Exception connecting toohello target*</span></span> |<span data-ttu-id="178eb-227">스크립트는 수 tooaccess hello 복구 지점</span><span class="sxs-lookup"><span data-stu-id="178eb-227">Script is not able tooaccess hello recovery point</span></span> | <span data-ttu-id="178eb-228">Hello 컴퓨터 위에서 언급 한 hello 액세스 요구 사항을 충족 하는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="178eb-228">Check whether hello machine fulfills hello access requirements mentioned above</span></span>|  
|   <span data-ttu-id="178eb-229">Exe 출력: *hello 대상에 이미 로그인 ISCSI 세션을 통해.*</span><span class="sxs-lookup"><span data-stu-id="178eb-229">Exe output: *hello target has already been logged in via an ISCSI session.*</span></span> |   <span data-ttu-id="178eb-230">동일한 컴퓨터와 hello 드라이브가 첨부 된 hello에서 이미 실행 된 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="178eb-230">hello script was already executed on hello same machine and hello drives have been attached</span></span> |   <span data-ttu-id="178eb-231">hello 복구 지점 볼륨 hello가 이미 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-231">hello volumes of hello recovery point have already been attached.</span></span> <span data-ttu-id="178eb-232">같은 드라이브 문자를 hello로 탑재 되지 않을 수 있습니다 원본 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-232">They may NOT be mounted with hello same drive letters of hello original VM.</span></span> <span data-ttu-id="178eb-233">Hello 사용 가능한 모든 볼륨에 파일에 대 한 hello 파일 탐색기에서 탐색</span><span class="sxs-lookup"><span data-stu-id="178eb-233">Browse through all hello available volumes in hello file explorer for your file</span></span> |
| <span data-ttu-id="178eb-234">Exe 출력: *포털/초과 hello 12 시간 제한을 통해 hello 디스크 분리 되어 있으므로이 스크립트 올바르지 않습니다. Hello 포털에서 새 스크립트를 다운로드 하십시오.*</span><span class="sxs-lookup"><span data-stu-id="178eb-234">Exe output: *This script is invalid because hello disks have been dismounted via portal/exceeded hello 12-hr limit. Please download a new script from hello portal.*</span></span> |    <span data-ttu-id="178eb-235">hello 디스크 hello 포털 또는 hello 12 시간 제한 초과에서 분리 되어</span><span class="sxs-lookup"><span data-stu-id="178eb-235">hello disks have been dismounted from hello portal or hello 12-hr limit exceeded</span></span> |  <span data-ttu-id="178eb-236">이 특정 exe는 현재 유효하지 않고 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-236">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="178eb-237">Tooaccess hello 해당 복구 지점 시간의 파일을 원하는 경우 새 exe에 대 한 hello 포털을 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-237">If you want tooaccess hello files of that recovery point-in-time, visit hello portal for a new exe</span></span>|
| <span data-ttu-id="178eb-238">Hello 컴퓨터 hello exe 실행 되는 위치에: hello 새 볼륨 hello 분리 단추를 클릭 한 후 분리 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="178eb-238">On hello machine where hello exe is run: hello new volumes are not dismounted after hello dismount button is clicked</span></span> |    <span data-ttu-id="178eb-239">hello 컴퓨터 hello ISCSI 초기자는 하지 응답/연결 toohello 목표를 새로 고치고 hello 캐시를 유지 관리</span><span class="sxs-lookup"><span data-stu-id="178eb-239">hello ISCSI initiator on hello machine is not responding/refreshing its connection toohello target and maintaining hello cache</span></span> |    <span data-ttu-id="178eb-240">Hello 분리 단추를 누른 후 몇 분까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-240">Wait for some mins after hello dismount button is pressed.</span></span> <span data-ttu-id="178eb-241">새 볼륨 hello 여전히 분리 되지 경우 모든 hello 볼륨을 찾으십시오.</span><span class="sxs-lookup"><span data-stu-id="178eb-241">If hello new volumes are still not dismounted, please browse through all hello volumes.</span></span> <span data-ttu-id="178eb-242">사용할 수 없으면 디스크 hello이 강제로 오류 메시지와 함께 hello는 시작자 toorefresh hello 연결과 hello 볼륨이 분리 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-242">This forces hello initiator toorefresh hello connection and hello volume is dismounted with an error message that hello disk is not available</span></span>|
| <span data-ttu-id="178eb-243">Exe 출력: 스크립트가 성공적으로 실행 되지만 "새 볼륨이 연결 되어" hello 스크립트 출력에 표시 되지 않으면</span><span class="sxs-lookup"><span data-stu-id="178eb-243">Exe output: Script is run successfully but “New volumes attached” is not displayed on hello script output</span></span> |   <span data-ttu-id="178eb-244">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-244">This is a transient error</span></span>   | <span data-ttu-id="178eb-245">hello 볼륨 이미 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-245">hello volumes would have been already attached.</span></span> <span data-ttu-id="178eb-246">탐색기 toobrowse를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-246">Open Explorer toobrowse.</span></span> <span data-ttu-id="178eb-247">동일 컴퓨터 hello 스크립트 때마다 실행을 사용 하는 경우에 hello 후속 exe 실행에 표시 되어야 hello 목록과 hello 컴퓨터를 다시 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-247">If you are using hello same machine for running scripts every time, consider restarting hello machine and hello list should be displayed in hello subsequent exe runs.</span></span> |
| <span data-ttu-id="178eb-248">Linux 특정: 수 없습니다. tooview hello 필요한 볼륨</span><span class="sxs-lookup"><span data-stu-id="178eb-248">Linux specific: Not able tooview hello desired volumes</span></span> | <span data-ttu-id="178eb-249">hello 스크립트가 실행 되는 hello 컴퓨터의 운영 체제 hello의 VM을 백업 하는 hello hello 기본 파일 시스템을 인식 하지 못할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-249">hello OS of hello machine where hello script is run may not recognize hello underlying filesystem of hello backed up VM</span></span> | <span data-ttu-id="178eb-250">Hello 복구 지점 수 있는지 여부를 확인은 크래시 일관성이 또는 파일에 일관적인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-250">Check whether hello recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="178eb-251">해당 OS hello를 인식 하는 다른 컴퓨터에서 일관 되 고 실행 hello 스크립트 파일 VM의 파일 시스템 백업</span><span class="sxs-lookup"><span data-stu-id="178eb-251">If file consistent, run hello script on another machine whose OS recognizes hello backed up VM's filesystem</span></span> |
| <span data-ttu-id="178eb-252">Windows 특정: 수 없습니다. tooview hello 필요한 볼륨</span><span class="sxs-lookup"><span data-stu-id="178eb-252">Windows specific: Not able tooview hello desired volumes</span></span> | <span data-ttu-id="178eb-253">hello 디스크가 연결 되어 있지만 hello 볼륨 구성 되지 않은</span><span class="sxs-lookup"><span data-stu-id="178eb-253">hello disks may have been attached but hello volumes were not configured</span></span> | <span data-ttu-id="178eb-254">Hello 디스크 관리 화면에서 hello 추가 디스크 관련된 toohello 복구 지점을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-254">From hello disk management screen, identify hello additional disks related toohello recovery point.</span></span> <span data-ttu-id="178eb-255">이러한 디스크 없는 오프 라인 상태 시도 온라인 hello 디스크를 마우스 오른쪽 단추로 클릭 하 고 '온라인 ' 상태를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="178eb-255">If any of these disks are in offline state try making them online by right-clicking on hello disk and click 'Online'</span></span>|
