---
title: "Azure의 Linux 소개 | Microsoft Docs"
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
ms.openlocfilehash: 7bd0c5549a2e1f592681760d5ef464b9570ca4ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-linux-on-azure"></a><span data-ttu-id="bc6e8-103">Azure의 Linux 소개</span><span class="sxs-lookup"><span data-stu-id="bc6e8-103">Introduction to Linux on Azure</span></span>
<span data-ttu-id="bc6e8-104">이 항목에서는 Azure 클라우드에서 Linux 가상 컴퓨터를 사용하는 몇 가지 측면을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-104">This topic provides an overview of some aspects of using Linux virtual machines in the Azure cloud.</span></span> <span data-ttu-id="bc6e8-105">갤러리의 기존 이미지를 사용하여 Linux 가상 컴퓨터 배포는 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-105">Deploying a Linux virtual machine is a straightforward process using an image from the gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="bc6e8-106">인증: 사용자 이름, 암호 및 SSH 키</span><span class="sxs-lookup"><span data-stu-id="bc6e8-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="bc6e8-107">Azure Portal을 사용하여 Linux 가상 컴퓨터를 만들 때, 사용자 이름, 암호 또는 SSH 공개 키 중 하나가 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-107">When creating a Linux virtual machine using the Azure portal, you are asked to provide a either username and password or an SSH public key.</span></span> <span data-ttu-id="bc6e8-108">Azure에 Linux 가상 컴퓨터를 배포할 때 선택하는 사용자 이름에는 다음과 같은 제약이 있습니다. 가상 컴퓨터에 이미 존재하던 시스템 계정의 이름(UID <100)(예: 'root')은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-108">The choice of a username for deploying a Linux virtual machine on Azure is subject to the following constraint: names of system accounts (UID <100) already present in the virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="bc6e8-109">[Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="bc6e8-110">[Azure에서 Linux와 함께 SSH를 사용하는 방법](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-110">See [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="bc6e8-111">`sudo`</span><span class="sxs-lookup"><span data-stu-id="bc6e8-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="bc6e8-112">Azure에서 가상 컴퓨터 인스턴스를 배포하는 동안 지정한 사용자 계정이 권한 있는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-112">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="bc6e8-113">Azure Linux 에이전트에서 `sudo` 유틸리티를 사용하여 루트(superuser 계정)로 권한을 상승하도록 이 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-113">This account is configured by the Azure Linux Agent to be able to elevate privileges to root (superuser account) using the `sudo` utility.</span></span> <span data-ttu-id="bc6e8-114">이 사용자 계정을 사용하여 로그인한 후 다음 명령 구문을 사용하여 루트로 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-114">Once logged in using this user account, you will be able to run commands as root using the command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="bc6e8-115">선택적으로 **sudo -s**를 사용하여 루트 셸을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="bc6e8-116">[Azure의 Linux 가상 컴퓨터에서 루트 권한 사용](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="bc6e8-117">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="bc6e8-117">Firewall Configuration</span></span>
<span data-ttu-id="bc6e8-118">Azure는 Azure Portal에서 지정된 포트에 연결을 제한하는 인바운드 패킷 필터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-118">Azure provides an inbound packet filter that restricts connectivity to ports specified in the Azure portal.</span></span> <span data-ttu-id="bc6e8-119">기본적으로 허용되는 유일한 포트는 SSH입니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-119">By default, the only allowed port is SSH.</span></span> <span data-ttu-id="bc6e8-120">Azure Portal에서 끝점을 구성하여 Linux 가상 컴퓨터의 추가 포트 액세스를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-120">You may open up access to additional ports on your Linux virtual machine by configuring endpoints in the Azure portal:</span></span>

* <span data-ttu-id="bc6e8-121">[가상 컴퓨터에 끝점을 설정하는 방법](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-121">See: [How to Set Up Endpoints to a Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="bc6e8-122">Azure 갤러리의 Linux 이미지는 기본적으로 *iptables* 방화벽을 사용하도록 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-122">The Linux images in the Azure Gallery do not enable the *iptables* firewall by default.</span></span> <span data-ttu-id="bc6e8-123">원하는 경우 추가 필터링을 제공하도록 이 방화벽을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-123">If desired, the firewall may be configured to provide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="bc6e8-124">호스트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="bc6e8-124">Hostname Changes</span></span>
<span data-ttu-id="bc6e8-125">Linux 이미지의 인스턴스를 처음 배포할 때 가상 컴퓨터의 호스트 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-125">When you initially deploy an instance of a Linux image, you are required to provide a host name for the virtual machine.</span></span> <span data-ttu-id="bc6e8-126">가상 컴퓨터를 실행하면 이 호스트 이름이 플랫폼 DNS 서버에 게시되므로 서로 연결된 여러 가상 컴퓨터에서 호스트 이름을 사용하여 IP 주소를 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-126">Once the virtual machine is running, this hostname is published to the platform DNS servers so that multiple virtual machines connected to each other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="bc6e8-127">가상 컴퓨터를 배포한 후 호스트 이름을 변경해야 하는 경우 다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-127">If hostname changes are desired after a virtual machine has been deployed, please use the command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="bc6e8-128">Azure Linux 에이전트에는 이 이름 변경을 자동으로 검색하여 이 변경 내용을 기억하도록 가상 컴퓨터를 적절히 구성하고 플랫폼 DNS 서버에 이 변경 내용을 게시하는 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-128">The Azure Linux Agent includes functionality to automatically detect this name change and appropriately configure the virtual machine to persist this change and publish this change to the platform DNS servers.</span></span>

* [<span data-ttu-id="bc6e8-129">Azure Linux 에이전트 사용자 가이드</span><span class="sxs-lookup"><span data-stu-id="bc6e8-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="bc6e8-130">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="bc6e8-130">Cloud-Init</span></span>
<span data-ttu-id="bc6e8-131">**Ubuntu** 및 **CoreOS** 이미지는 cloud-init pn Azure를 활용하여 가상 컴퓨터를 부트스트랩하기 위한 추가 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="bc6e8-132">사용자 지정 데이터를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc6e8-132">How to Inject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="bc6e8-133">Microsoft Azure의 사용자 지정 데이터 및 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="bc6e8-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="bc6e8-134">Init 클라우드를 사용하여 Azure 스왑 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="bc6e8-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="bc6e8-135">Azure에서 CoreOS를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc6e8-135">How to Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="bc6e8-136">가상 컴퓨터 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="bc6e8-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="bc6e8-137">Azure는 기존 가상 컴퓨터의 상태를 이미지로 캡처하는 기능을 제공합니다. 이 이미지는 이후에 추가 가상 컴퓨터 인스턴스를 배포하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-137">Azure provides the ability to capture the state of an existing virtual machine into an image that can subsequently be used to deploy additional virtual machine instances.</span></span> <span data-ttu-id="bc6e8-138">Azure Linux 에이전트는 프로비전 프로세스 중 수행된 일부 사용자 지정을 롤백하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-138">The Azure Linux Agent may be used to rollback some of the customization that was performed during the provisioning process.</span></span> <span data-ttu-id="bc6e8-139">아래 단계를 따르면 가상 컴퓨터를 이미지로 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-139">You may follow the steps below to capture a virtual machine as an image:</span></span>

1. <span data-ttu-id="bc6e8-140">**waagent -deprovision**을 실행하여 사용자 지정 프로비전을 실행 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-140">Run **waagent -deprovision** to undo provisioning customization.</span></span> <span data-ttu-id="bc6e8-141">또는 선택적으로 프로비전 중 지정한 사용자 계정 및 연결된 모든 데이터를 삭제하려면 **waagent -deprovision+user**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-141">Or **waagent -deprovision+user** to optionally delete the user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="bc6e8-142">가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-142">Shut down/power off the virtual machine.</span></span>
3. <span data-ttu-id="bc6e8-143">Azure Portal에서 **캡쳐**를 클릭하거나 PowerShell 또는 CLI 도구를 사용하여 가상 컴퓨터를 이미지로 캡쳐할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-143">Click **Capture** in the Azure portal or use the PowerShell or CLI tools to capture the virtual machine as an image.</span></span>
   
   * <span data-ttu-id="bc6e8-144">참고: [Linux 가상 컴퓨터를 캡처하여 템플릿으로 사용하는 방법](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc6e8-144">See: [How to Capture a Linux Virtual Machine to Use as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="bc6e8-145">디스크 연결</span><span class="sxs-lookup"><span data-stu-id="bc6e8-145">Attaching Disks</span></span>
<span data-ttu-id="bc6e8-146">각 가상 컴퓨터에는 임시 로컬 *리소스 디스크* 가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="bc6e8-147">리소스 디스크의 데이터는 다시 부팅 후 지속되지 않을 수도 있으므로 가상 컴퓨터에서 실행되는 응용 프로그램 및 프로세스에서 **임시** 데이터 저장소에 사용되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in the virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="bc6e8-148">또한 운영 체제의 페이지 또는 스왑 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-148">It is also used to store the page or swap files for the operating system.</span></span>

<span data-ttu-id="bc6e8-149">Linux에서 리소스 디스크는 일반적으로 Azure Linux 에이전트에 의해 관리되며 **/mnt/resource**(또는 Ubuntu 이미지의 **/mnt**)에 자동으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-149">On Linux, the resource disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="bc6e8-150">리소스 디스크는 **임시** 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-150">Note that the resource disk is a **temporary** disk, and might be deleted and reformatted when the VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="bc6e8-151">Linux에서 데이터 디스크 이름은 커널에서 `/dev/sdc`로 지정될 수 있으며 사용자는 해당 리소스를 파티셔닝, 형식 지정 및 마운트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-151">On Linux the data disk might be named by the kernel as `/dev/sdc`, and users will need to partition, format and mount that resource.</span></span> <span data-ttu-id="bc6e8-152">[데이터 디스크를 가상 컴퓨터에 연결하는 방법](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에 대한 자습서의 단계를 다루었습니다.</span><span class="sxs-lookup"><span data-stu-id="bc6e8-152">This is covered step-by-step in the tutorial: [How to Attach a Data Disk to a Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="bc6e8-153">**참고 항목:** [Linux에서 소프트웨어 RAID 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Azure에서 Linux VM에 대해 LVM 구성](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc6e8-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

