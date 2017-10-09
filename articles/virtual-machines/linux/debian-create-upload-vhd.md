---
title: "Azure에 VHD는 Debian Linux aaaPrepare | Microsoft Docs"
description: "Azure에서 배포에 대 한 toocreate Debian 7 및 8 VHD 파일 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="4bac5-103">Azure용 Debian VHD 준비</span><span class="sxs-lookup"><span data-stu-id="4bac5-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="4bac5-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4bac5-104">Prerequisites</span></span>
<span data-ttu-id="4bac5-105">이 섹션에서는 이미 hello에서 다운로드 한.iso 파일 Debian Linux 운영 체제를 설치한 가정 [Debian 웹 사이트](https://www.debian.org/distrib/) tooa 가상 하드 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="4bac5-106">여러 도구 존재 toocreate.vhd 파일입니다. Hyper-v는 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="4bac5-107">Hyper-v를 사용 하 여 지침은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](https://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="4bac5-108">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="4bac5-108">Installation notes</span></span>
* <span data-ttu-id="4bac5-109">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bac5-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="4bac5-110">Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="4bac5-111">Hyper-v 관리자 또는 hello를 사용 하 여 hello 디스크 tooVHD 형식으로 변환할 수 있습니다 **convert vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4bac5-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="4bac5-112">Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="4bac5-113">OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이.</span><span class="sxs-lookup"><span data-stu-id="4bac5-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="4bac5-114">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="4bac5-115">스왑 파티션을 hello OS 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="4bac5-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="4bac5-116">hello Azure Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="4bac5-117">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="4bac5-118">모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="4bac5-119">Azure 관리 toocreate Debian Vhd를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4bac5-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="4bac5-120">Azure에 Vhd를 Debian hello 등 생성에 사용할 수 있는 도구가 있습니다 [azure-관리](https://github.com/credativ/azure-manage) 에서 스크립트 [credativ](http://www.credativ.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="4bac5-121">이 이미지를 처음부터 새로 만드는 방식과 권장 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="4bac5-122">예를 들어 toocreate Debian 8 VHD hello 다음 toodownload azure 관리 되는 명령 (및 종속성)를 실행 한 hello azure_build_image 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="4bac5-123">Debian VHD 수동 준비</span><span class="sxs-lookup"><span data-stu-id="4bac5-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="4bac5-124">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="4bac5-125">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="4bac5-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="4bac5-126">에 대 한 hello 줄 주석 **deb cdrom** 에 `/etc/apt/source.list` ISO 파일에 대해 VM hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="4bac5-127">Hello 편집 `/etc/default/grub` 파일을 수정 hello **GRUB_CMDLINE_LINUX** Azure에 대 한 tooinclude 추가 커널 매개 변수를 다음과 같이 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="4bac5-128">Hello grub 다시 작성 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="4bac5-129">Debian 7 또는 8 대 Debian의 Azure 저장소 too/etc/apt/sources.list를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="4bac5-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="4bac5-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="4bac5-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="4bac5-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="4bac5-132">Hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="4bac5-133">Debian 7 hello wheezy backports 리포지토리에서 필요한 toorun hello 3.16 기반 커널입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="4bac5-134">첫 번째 내용을 따라 hello로 /etc/apt/preferences.d/linux.pref 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="4bac5-135">Tooinstall hello 새 커널 "get-sudo apt 설치 amd64-이미지-linux를" 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="4bac5-136">Hello 가상 컴퓨터를 프로 비전 해제 하 고 Azure에서 프로 비전에 대 한 준비을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="4bac5-137">Hyper-V 관리자에서 **작업** -> 종료를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="4bac5-138">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bac5-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bac5-139">Next steps</span></span>
<span data-ttu-id="4bac5-140">사용자는 이제 준비 toouse Azure에서 가상 하드 디스크 Debian toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="4bac5-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="4bac5-141">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bac5-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

