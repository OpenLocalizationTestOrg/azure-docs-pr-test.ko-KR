---
title: "Azure에서 aaaIntroduction tooLinux | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 사용하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a><span data-ttu-id="1a646-103">Azure에서 tooLinux 소개</span><span class="sxs-lookup"><span data-stu-id="1a646-103">Introduction tooLinux on Azure</span></span>
<span data-ttu-id="1a646-104">이 항목에서는 일부의 Linux 가상 컴퓨터를 사용 하 여 Azure 클라우드 hello에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-104">This topic provides an overview of some aspects of using Linux virtual machines in hello Azure cloud.</span></span> <span data-ttu-id="1a646-105">Hello 갤러리에서 이미지를 사용 하는 간단한 프로세스는 Linux 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-105">Deploying a Linux virtual machine is a straightforward process using an image from hello gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="1a646-106">인증: 사용자 이름, 암호 및 SSH 키</span><span class="sxs-lookup"><span data-stu-id="1a646-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="1a646-107">어느 사용자 이름을 tooprovide 묻는 hello Azure 포털을 사용 하 여 Linux 가상 컴퓨터를 만들 때 암호 또는 SSH 공개 키 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-107">When creating a Linux virtual machine using hello Azure portal, you are asked tooprovide a either username and password or an SSH public key.</span></span> <span data-ttu-id="1a646-108">hello 선택 Azure에서 Linux 가상 컴퓨터를 배포 하기 위한 사용자 이름이 제약 조건에 따라 주체 toohello: 시스템 계정의 이름이 (UID < 100) hello에 이미 있는 가상 컴퓨터가 허용 되지 않으면 '루트' 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-108">hello choice of a username for deploying a Linux virtual machine on Azure is subject toohello following constraint: names of system accounts (UID <100) already present in hello virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="1a646-109">[Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a646-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="1a646-110">참조 [어떻게 tooUse와 Azure에서 Linux에 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1a646-110">See [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="1a646-111">`sudo`</span><span class="sxs-lookup"><span data-stu-id="1a646-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="1a646-112">Azure에서 가상 컴퓨터 인스턴스에 배포 하는 동안 지정 된 hello 사용자 계정은 권한 있는 계정이입니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-112">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="1a646-113">Hello Azure Linux 에이전트 toobe 수 tooelevate 권한 tooroot (superuser 계정이) hello를 사용 하 여이 계정이 구성 되어 `sudo` 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-113">This account is configured by hello Azure Linux Agent toobe able tooelevate privileges tooroot (superuser account) using hello `sudo` utility.</span></span> <span data-ttu-id="1a646-114">이 사용자 계정을 사용 하 여 로그인 한 hello 명령 구문을 사용 하는 루트로 수 toorun 명령 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-114">Once logged in using this user account, you will be able toorun commands as root using hello command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="1a646-115">선택적으로 **sudo -s**를 사용하여 루트 셸을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="1a646-116">[Azure의 Linux 가상 컴퓨터에서 루트 권한 사용](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a646-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="1a646-117">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="1a646-117">Firewall Configuration</span></span>
<span data-ttu-id="1a646-118">Azure 연결 tooports hello Azure 포털에에서 지정 된 제한 하는 인바운드 패킷 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-118">Azure provides an inbound packet filter that restricts connectivity tooports specified in hello Azure portal.</span></span> <span data-ttu-id="1a646-119">기본적으로 hello 허용 되는 포트만 SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-119">By default, hello only allowed port is SSH.</span></span> <span data-ttu-id="1a646-120">Hello Azure 포털에서에서 끝점을 구성 하 여 Linux 가상 컴퓨터에 액세스 tooadditional 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-120">You may open up access tooadditional ports on your Linux virtual machine by configuring endpoints in hello Azure portal:</span></span>

* <span data-ttu-id="1a646-121">참고: [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1a646-121">See: [How tooSet Up Endpoints tooa Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="1a646-122">hello Azure 갤러리의에서 hello Linux 이미지 hello를 사용 하지 않으면 *iptables* 기본적으로 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-122">hello Linux images in hello Azure Gallery do not enable hello *iptables* firewall by default.</span></span> <span data-ttu-id="1a646-123">원하는 경우 hello 방화벽을 구성할 수 있습니다 tooprovide 추가 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-123">If desired, hello firewall may be configured tooprovide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="1a646-124">호스트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="1a646-124">Hostname Changes</span></span>
<span data-ttu-id="1a646-125">Linux 이미지의 인스턴스를 처음 배포할 때는 필요한 tooprovide hello 가상 컴퓨터에 대 한 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-125">When you initially deploy an instance of a Linux image, you are required tooprovide a host name for hello virtual machine.</span></span> <span data-ttu-id="1a646-126">Hello 가상 컴퓨터가 실행 되 면 여러 연결 된 가상 컴퓨터 tooeach 다른 호스트 이름을 사용 하는 IP 주소 조회를 수행할 수 있도록이 호스트 이름에 게시 된 toohello 플랫폼 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-126">Once hello virtual machine is running, this hostname is published toohello platform DNS servers so that multiple virtual machines connected tooeach other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="1a646-127">가상 컴퓨터를 배포한 후 호스트 이름 변경 내용을 원하는 경우 경우 hello 명령을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1a646-127">If hostname changes are desired after a virtual machine has been deployed, please use hello command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="1a646-128">기능을 포함 하는 hello Azure Linux 에이전트 tooautomatically이 이름을 변경 내용을 검색 적절 하 게 구성 hello 가상 컴퓨터 toopersist이이 변경 하 고이 변경 toohello 플랫폼 DNS 서버를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-128">hello Azure Linux Agent includes functionality tooautomatically detect this name change and appropriately configure hello virtual machine toopersist this change and publish this change toohello platform DNS servers.</span></span>

* [<span data-ttu-id="1a646-129">Azure Linux 에이전트 사용자 가이드</span><span class="sxs-lookup"><span data-stu-id="1a646-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="1a646-130">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="1a646-130">Cloud-Init</span></span>
<span data-ttu-id="1a646-131">**Ubuntu** 및 **CoreOS** 이미지는 cloud-init pn Azure를 활용하여 가상 컴퓨터를 부트스트랩하기 위한 추가 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="1a646-132">어떻게 tooInject 데이터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1a646-132">How tooInject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="1a646-133">Microsoft Azure의 사용자 지정 데이터 및 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="1a646-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="1a646-134">Init 클라우드를 사용하여 Azure 스왑 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="1a646-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="1a646-135">어떻게 tooUse CoreOS Azure에서</span><span class="sxs-lookup"><span data-stu-id="1a646-135">How tooUse CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="1a646-136">가상 컴퓨터 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="1a646-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="1a646-137">Azure는 이후에 사용된 toodeploy 추가 가상 컴퓨터 인스턴스 수 있는 이미지에 기존 가상 컴퓨터의 hello 기능 toocapture hello 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-137">Azure provides hello ability toocapture hello state of an existing virtual machine into an image that can subsequently be used toodeploy additional virtual machine instances.</span></span> <span data-ttu-id="1a646-138">hello Azure Linux 에이전트에 사용 되는 toorollback 일부 hello hello를 프로 비전 프로세스 중 수행 된 사용자 지정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-138">hello Azure Linux Agent may be used toorollback some of hello customization that was performed during hello provisioning process.</span></span> <span data-ttu-id="1a646-139">이미지 형식으로 toocapture 가상 컴퓨터 아래 hello 단계를 수행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-139">You may follow hello steps below toocapture a virtual machine as an image:</span></span>

1. <span data-ttu-id="1a646-140">실행 **waagent-deprovision** tooundo 사용자 지정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-140">Run **waagent -deprovision** tooundo provisioning customization.</span></span> <span data-ttu-id="1a646-141">또는 **waagent-deprovision + 사용자** toooptionally hello 사용자 계정을 프로 비전 및 모든 관련 데이터 중에 지정한를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-141">Or **waagent -deprovision+user** toooptionally delete hello user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="1a646-142">/ 전원 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-142">Shut down/power off hello virtual machine.</span></span>
3. <span data-ttu-id="1a646-143">클릭 **캡처** hello Azure 포털 또는 사용 하 여 hello PowerShell 또는 CLI 도구 toocapture hello 가상 컴퓨터를 이미지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-143">Click **Capture** in hello Azure portal or use hello PowerShell or CLI tools toocapture hello virtual machine as an image.</span></span>
   
   * <span data-ttu-id="1a646-144">참고: [어떻게 tooCapture 템플릿으로 Linux 가상 컴퓨터 tooUse](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1a646-144">See: [How tooCapture a Linux Virtual Machine tooUse as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="1a646-145">디스크 연결</span><span class="sxs-lookup"><span data-stu-id="1a646-145">Attaching Disks</span></span>
<span data-ttu-id="1a646-146">각 가상 컴퓨터에는 임시 로컬 *리소스 디스크* 가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="1a646-147">다시 부팅 해도 리소스 디스크의 데이터를 영구 수 있습니다, 때문에 종종 응용 프로그램 및 일시적이 지에 대 한 hello 가상 컴퓨터에서 실행 중인 프로세스에서 사용 됩니다 하 고 **임시** 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in hello virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="1a646-148">사용 되는 toostore hello 운영 체제에 대 한 페이지 또는 스왑 파일과 hello 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-148">It is also used toostore hello page or swap files for hello operating system.</span></span>

<span data-ttu-id="1a646-149">Linux hello 리소스 디스크 hello Azure Linux 에이전트에서 관리 하는 않으며 자동으로 너무 탑재**/mnt/리소스** (또는 **/mnt** Ubuntu 이미지에).</span><span class="sxs-lookup"><span data-stu-id="1a646-149">On Linux, hello resource disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="1a646-150">해당 하는 hello 리소스 디스크는 한 **임시** , 디스크 및 수 삭제 되 고 hello VM 다시 부팅 될 때 다시 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-150">Note that hello resource disk is a **temporary** disk, and might be deleted and reformatted when hello VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="1a646-151">Linux에서 hello 데이터 디스크와 hello 커널에서 이름이 수 있습니다 `/dev/sdc`, 사용자가을 toopartition 해야 하 고 서식을 지정 하 고 해당 리소스를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-151">On Linux hello data disk might be named by hello kernel as `/dev/sdc`, and users will need toopartition, format and mount that resource.</span></span> <span data-ttu-id="1a646-152">이 내용은 hello 자습서의 단계별 설명: [어떻게 tooAttach 데이터 디스크 tooa 가상 컴퓨터](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a646-152">This is covered step-by-step in hello tutorial: [How tooAttach a Data Disk tooa Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="1a646-153">**참고 항목:** [Linux에서 소프트웨어 RAID 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Azure에서 Linux VM에 대해 LVM 구성](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1a646-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

