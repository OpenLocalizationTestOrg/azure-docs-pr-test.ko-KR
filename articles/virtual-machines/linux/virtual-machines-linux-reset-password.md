---
title: "Azure Vm에서 aaaHow tooreset 로컬 Linux 암호 | Microsoft Docs"
description: "Hello 단계 tooreset hello 로컬 Linux 암호 Azure VM에서 소개"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="43041-103">어떻게 tooreset Azure Vm에서 로컬 Linux 암호</span><span class="sxs-lookup"><span data-stu-id="43041-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="43041-104">이 문서에서는 여러 가지 방법을 tooreset 로컬 Linux 가상 컴퓨터 (VM) 암호를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="43041-105">Hello 사용자 계정이 만료 하거나 새 계정을 toocreate 원하는 hello 다음 메서드 toocreate 새 로컬 관리자 계정을 사용 하 여 수 있으며 액세스 toohello VM을 다시 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43041-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="43041-106">증상</span><span class="sxs-lookup"><span data-stu-id="43041-106">Symptoms</span></span>

<span data-ttu-id="43041-107">Toohello VM에 로그인 할 수 없습니다 및 사용한 hello 암호가 올바르지 않습니다. 나타내는 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="43041-108">또한 사용할 수 없습니다 VMAgent tooreset 암호 hello Azure 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43041-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="43041-109">수동 암호 다시 설정 프로시저</span><span class="sxs-lookup"><span data-stu-id="43041-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="43041-110">Hello VM을 삭제 하 고 hello 연결 된 디스크 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="43041-111">데이터 디스크 tooanother와 운영 체제 드라이브 hello 연결 임시 VM hello에 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="43041-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="43041-112">다음 임시 VM toobecome hello에서 SSH 명령을 hello 슈퍼 사용자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="43041-113">실행 **fdisk l** 또는 시스템 로그 toofind hello에 새로 연결 된 디스크.</span><span class="sxs-lookup"><span data-stu-id="43041-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="43041-114">Hello 드라이브 이름 toomount를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="43041-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="43041-115">그런 다음 hello에 임시 VM을 찾는 위치 hello 관련 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="43041-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="43041-116">hello 다음은 hello grep 명령의 예제 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="43041-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="43041-117">**tempmount**라는 탑재 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43041-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="43041-118">Hello 탑재 지점에 hello OS 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="43041-119">일반적으로 toomount sdc1 또는 sdc2 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="43041-120">이 hello 끊어진된 컴퓨터 디스크에서 /etc 디렉터리에 파티션을 호스팅하는 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="43041-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="43041-121">변경하기 전에 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="43041-122">필요한 hello 사용자의 암호를 다시 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="43041-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="43041-123">이동 hello hello 컴퓨터의 디스크 손상 파일 toohello 올바른 위치를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43041-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="43041-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="43041-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
