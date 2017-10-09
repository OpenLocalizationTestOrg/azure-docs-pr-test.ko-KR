---
title: "Azure에서 aaaLinux VM 장치 이름이 변경 된 | Microsoft Docs"
description: "Hello 장치 이름이 변경 되 고이 문제에 대 한 솔루션을 제공 이유를 설명 합니다."
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
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="69e40-103">문제 해결: Linux VM 장치 이름이 변경됨</span><span class="sxs-lookup"><span data-stu-id="69e40-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="69e40-104">hello 문서는 Linux 가상 컴퓨터 (VM)를 다시 시작 하거나 hello 디스크를 다시 연결 하면 장치 이름이 변경 하는 이유를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="69e40-105">또한이 문제에 대 한 hello 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="69e40-106">증상</span><span class="sxs-lookup"><span data-stu-id="69e40-106">Symptom</span></span>

<span data-ttu-id="69e40-107">Hello Linux Vm의 경우 Microsoft Azure에서 실행 하는 경우 뒤에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="69e40-108">hello VM 다시 시작 후 tooboot을 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="69e40-109">데이터 디스크를 분리 및 다시 연결 하는 경우 디스크에 대 한 hello 장치 이름이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="69e40-110">장치 이름을 사용하여 디스크를 참조하는 응용 프로그램 또는 스크립트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="69e40-111">해당 hello 찾을 hello 디스크의 장치 이름이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="69e40-112">원인</span><span class="sxs-lookup"><span data-stu-id="69e40-112">Cause</span></span>

<span data-ttu-id="69e40-113">Linux에서 장치 경로 않을 toobe 일관 된 컴퓨터를 다시 시작할.</span><span class="sxs-lookup"><span data-stu-id="69e40-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="69e40-114">장치 이름은 주(문자) 및 보조 번호로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="69e40-115">Hello Linux 저장 장치 드라이버에서 새 장치를 검색 하는 경우 주 및 부 장치 번호 tooit hello 사용 가능한 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="69e40-116">장치를 제거 하는 경우 hello 장치 번호는 해제 된 toobe 나중에 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="69e40-117">hello 문제 때문에 발생 hello hello SCSI 하위 시스템에서 예약 된 Linux에서 검색 하는 장치 발생 하는 비동기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="69e40-118">컴퓨터를 다시 시작할 hello 최종 장치 경로 명명 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="69e40-119">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69e40-119">Solution</span></span>

<span data-ttu-id="69e40-120">tooresolve이이 문제를 영구 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="69e40-121">네 개의 메서드에 toopersistent는 이름 지정-파일 시스템 레이블, uuid, id 및 경로 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="69e40-122">Azure Linux Vm에 대해 hello 파일 시스템 레이블 및 UUID 메서드 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="69e40-123">대부분의 배포판 제공 하거나 hello **nofail** 또는 **nobootwait** fstab 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="69e40-124">이 옵션을 toomount 시작 시 hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="69e40-125">이러한 매개 변수에 대 한 자세한 내용은 hello 분포의 설명서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="69e40-126">Linux VM toouse UUID 데이터 디스크를 추가 하면 참조 하는 tooconfigure 방법에 대 한 자세한 내용은 [toohello Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="69e40-127">Hello Azure Linux 에이전트는 VM에 설치 될 때 사용 하 여 Udev 규칙 tooconstruct에서 바로 가기 링크 집합이 **/dev/disk/azure**합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="69e40-128">응용 프로그램에서 사용할 수 있습니다 이러한 Udev 규칙 및 스크립트 tooidentify 디스크 되는 VM을의 형식에 연결 된 toohello LUN hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="69e40-129">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="69e40-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="69e40-130">디스크 LUN 식별</span><span class="sxs-lookup"><span data-stu-id="69e40-130">Identify disk LUNs</span></span>

<span data-ttu-id="69e40-131">모든 hello 연결 된 디스크 및 기호화 된 링크를 구성할 응용 프로그램에서 Lun toofind를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="69e40-132">hello Azure Linux 에이전트에는 이제 다음과 같이 LUN toohello 장치에서 바로 가기 링크를 설정 하는 udev 규칙을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

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
                                 

<span data-ttu-id="69e40-133">Lsscsi 또는 유사한 도구를 다음과 같이 사용 하 여 hello Linux 게스트에서 LUN 정보를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="69e40-134">Azure 구독 메타 데이터 tooidentify hello에에서 위치와 Azure 저장소의 hello hello 파티션 데이터를 저장 하는 VHD의이 게스트 LUN 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="69e40-135">예를 들어 hello az cli를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-135">For example, use hello az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="69e40-136">blkid를 사용하여 파일 시스템 UUID 검색</span><span class="sxs-lookup"><span data-stu-id="69e40-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="69e40-137">스크립트 또는 응용 프로그램 blkid의 hello 출력 또는 유사한 리소스의 정보를 읽고 수에 대 한 바로 가기 링크를 생성 **/dev** 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="69e40-138">hello 출력의 모든 디스크 Uuid hello 연결 toohello VM과 hello 장치 파일 toowhich 연결 되어 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="69e40-139">기호화 된 링크의 집합을 생성 하는 hello waagent udev 규칙 **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="69e40-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="69e40-140">hello 응용 프로그램에서이 정보를 사용할 수 hello 부팅 디스크 장치 및 hello 리소스 (임시) 디스크를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="69e40-141">Azure에서 응용 프로그램 참조 해야 너무**/dev/disk/azure/root-part1** 또는 **/dev/disk/azure-resource-part1** toodiscover 이러한 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="69e40-142">Hello blkid 목록에서 추가 파티션을 없을 경우 데이터 디스크에 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="69e40-143">응용 프로그램 hello UUID 이러한 파티션에 대 한 유지 관리 및 hello toodiscover hello 장치 이름 아래와 같은 경로에서 런타임에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="69e40-144">Hello 최신 Azure 저장소 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="69e40-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="69e40-145">최신 Azure 저장소 규칙 toohello 명령 다음과 같은 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e40-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="69e40-146">자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="69e40-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="69e40-147">Ubuntu: UUID 사용</span><span class="sxs-lookup"><span data-stu-id="69e40-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="69e40-148">Red Hat: 영구 이름 지정</span><span class="sxs-lookup"><span data-stu-id="69e40-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="69e40-149">Linux: UUID에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="69e40-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="69e40-150">Udev: 소개 tooDevice 최신 Linux 시스템 관리</span><span class="sxs-lookup"><span data-stu-id="69e40-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

