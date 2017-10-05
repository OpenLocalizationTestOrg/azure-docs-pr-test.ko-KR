---
title: "Azure에서 Linux VM 장치 이름이 변경됨 | Microsoft Docs"
description: "장치 이름이 변경된 이름을 설명하고 이 문제에 대한 솔루션을 제공합니다."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="19a47-103">문제 해결: Linux VM 장치 이름이 변경됨</span><span class="sxs-lookup"><span data-stu-id="19a47-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="19a47-104">문서는 Linux VM(가상 컴퓨터)을 다시 시작하거나 디스크를 다시 연결한 후 장치 이름이 변경되는 이유를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="19a47-105">또한 이 문제에 대한 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="19a47-106">증상</span><span class="sxs-lookup"><span data-stu-id="19a47-106">Symptom</span></span>

<span data-ttu-id="19a47-107">Microsoft Azure에서 Linux VM을 실행하는 경우 다음과 같은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="19a47-108">VM에서 다시 시작한 후 부팅에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="19a47-109">데이터 디스크가 분리되고 다시 연결되는 경우 디스크에 대한 장치 이름이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="19a47-110">장치 이름을 사용하여 디스크를 참조하는 응용 프로그램 또는 스크립트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="19a47-111">디스크의 장치 이름이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="19a47-112">원인</span><span class="sxs-lookup"><span data-stu-id="19a47-112">Cause</span></span>

<span data-ttu-id="19a47-113">Linux의 장치 경로는 다시 시작에 대해 일관되도록 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="19a47-114">장치 이름은 주(문자) 및 보조 번호로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="19a47-115">Linux 저장소 장치 드라이버에서 새 장치를 검색하는 경우 주 및 보조 장치 번호를 사용할 수 있는 범위에서 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="19a47-116">장치가 제거되는 경우 장치 번호는 나중에 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="19a47-117">SCSI 하위 시스템에서 예약된 Linux에서 검색하는 장치가 비동기적으로 발생하므로 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="19a47-118">최종 장치 경로 이름 지정은 다시 시작에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="19a47-119">해결 방법</span><span class="sxs-lookup"><span data-stu-id="19a47-119">Solution</span></span>

<span data-ttu-id="19a47-120">이 문제를 해결하려면 영구 이름 지정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="19a47-121">영구적으로 이름을 지정하는 네 가지 메서드로, 파일 시스템 레이블별, uuid별, ID별 및 경로별이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="19a47-122">Azure Linux VM에 대해 파일 시스템 레이블 및 UUID 메서드를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="19a47-123">또한 대부분의 배포판은 **nofail** 또는 **nobootwait** fstab 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="19a47-124">이러한 옵션을 사용하면 디스크가 시작 시 탑재되지 않더라도 시스템을 부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="19a47-125">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19a47-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="19a47-126">데이터 디스크를 추가할 때 UUID를 사용하도록 Linux VM을 구성하는 방법에 대한 자세한 내용은 [Linux VM에 연결하여 새 디스크 탑재](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19a47-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="19a47-127">Azure Linux 에이전트가 VM에 설치될 때 Udev 규칙을 사용하여 **/dev/disk/azure** 아래에 기호 링크의 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="19a47-128">이러한 Udev 규칙은 응용 프로그램 및 스크립트에서 디스크가 VM, 해당 유형 및 LUN에 연결되었는지 식별하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="19a47-129">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="19a47-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="19a47-130">디스크 LUN 식별</span><span class="sxs-lookup"><span data-stu-id="19a47-130">Identify disk LUNs</span></span>

<span data-ttu-id="19a47-131">응용 프로그램은 LUN을 사용하여 모든 연결된 디스크 및 기호 링크 생성을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="19a47-132">이제 Azure Linux 에이전트는 다음과 같이 LUN에서 장치로 기호 링크를 설정하는 udev 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="19a47-133">Linux 게스트에서 다음과 같이 lsscsi 또는 유사한 도구를 사용하여 LUN 정보를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="19a47-134">이 게스트 LUN 정보를 파티션 데이터를 저장하는 VHD의 Azure 저장소의 위치를 식별하는 데 Azure 구독 메타데이터와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="19a47-135">예를 들어 az cli를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-135">For example, use the az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="19a47-136">blkid를 사용하여 파일 시스템 UUID 검색</span><span class="sxs-lookup"><span data-stu-id="19a47-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="19a47-137">스크립트 또는 응용 프로그램은 blkid의 출력 또는 유사한 원본의 정보를 읽고 사용하기 위해 **/dev**에서 기호 링크를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="19a47-138">출력은 연결되어 있는 VM 및 장치 파일에 연결된 모든 디스크의 UUID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="19a47-139">waagent udev 규칙은 **/dev/disk/azure** 아래에 기호 링크의 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="19a47-140">응용 프로그램은 이 정보를 사용하여 부팅 디스크 장치 및 리소스(임시) 디스크를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="19a47-141">Azure에서 응용 프로그램은 **/dev/disk/azure/root-part1** 또는 **/dev/disk/azure-resource-part1**을 참조하여 이러한 파티션을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="19a47-142">blkid 목록에서 추가 파티션이 있는 경우 데이터 디스크에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="19a47-143">응용 프로그램에서 이러한 파티션에 대한 UUID를 유지 관리하고 아래와 같은 경로를 사용하여 런타임 시 장치 이름을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="19a47-144">최신 Azure 저장소 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="19a47-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="19a47-145">최신 Azure 저장소 규칙을 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19a47-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="19a47-146">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19a47-146">For more information, see the following articles:</span></span>

- [<span data-ttu-id="19a47-147">Ubuntu: UUID 사용</span><span class="sxs-lookup"><span data-stu-id="19a47-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="19a47-148">Red Hat: 영구 이름 지정</span><span class="sxs-lookup"><span data-stu-id="19a47-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="19a47-149">Linux: UUID에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="19a47-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="19a47-150">Udev: 최신 Linux 시스템에서 장치 관리 소개</span><span class="sxs-lookup"><span data-stu-id="19a47-150">Udev: Introduction to Device Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

