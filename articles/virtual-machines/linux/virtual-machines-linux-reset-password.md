---
title: "Azure VM에서 로컬 Linux 암호를 다시 설정하는 방법 | Microsoft Docs"
description: "Azure VM에서 로컬 Linux 암호를 다시 설정하는 단계 소개"
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
ms.openlocfilehash: 084cdb26c7dfd8f46fb6ec7f8c48f7b4a327e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="4c99d-103">Azure VM에서 로컬 Linux 암호를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="4c99d-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="4c99d-104">이 문서에서는 로컬 Linux VM(가상 컴퓨터) 암호를 다시 설정하는 여러 가지 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="4c99d-105">사용자 계정이 만료되거나 새 계정을 만들려는 경우 다음 메서드를 사용하여 새 로컬 관리자 계정을 만들거나 VM에 대한 액세스를 다시 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="4c99d-106">증상</span><span class="sxs-lookup"><span data-stu-id="4c99d-106">Symptoms</span></span>

<span data-ttu-id="4c99d-107">VM에 로그인할 수 없다면 사용한 암호가 잘못되었음을 나타내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="4c99d-108">또한 VMAgent를 사용하여 Azure Portal에서 암호를 다시 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="4c99d-109">수동 암호 다시 설정 프로시저</span><span class="sxs-lookup"><span data-stu-id="4c99d-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="4c99d-110">VM을 삭제하고 연결된 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="4c99d-111">같은 위치에서 다른 임시 VM에 데이터 디스크로 OS 드라이브를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="4c99d-112">임시 VM에서 상위 사용자가 되는 다음과 같은 SSH 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="4c99d-113">**fdisk -l**을 실행하거나 시스템 로그를 확인하여 새로 연결된 디스크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="4c99d-114">탑재할 드라이브 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-114">Locate the drive name to mount.</span></span> <span data-ttu-id="4c99d-115">그런 다음 임시 VM에서 관련 로그 파일에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="4c99d-116">다음은 grep 명령의 예제 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="4c99d-117">**tempmount**라는 탑재 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="4c99d-118">탑재 지점에 OS 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="4c99d-119">일반적으로 sdc1 또는 sdc2를 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="4c99d-120">손상된 컴퓨터 디스크의 /etc 디렉터리에 있는 호스팅 파티션에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="4c99d-121">변경하기 전에 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="4c99d-122">필요한 사용자 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="4c99d-123">손상된 컴퓨터의 디스크의 올바른 위치에 수정된 파일을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c99d-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="4c99d-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="4c99d-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)