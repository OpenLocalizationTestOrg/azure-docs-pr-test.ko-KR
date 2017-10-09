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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>문제 해결: Linux VM 장치 이름이 변경됨

hello 문서는 Linux 가상 컴퓨터 (VM)를 다시 시작 하거나 hello 디스크를 다시 연결 하면 장치 이름이 변경 하는 이유를 설명 합니다. 또한이 문제에 대 한 hello 솔루션을 제공합니다.

## <a name="symptom"></a>증상

Hello Linux Vm의 경우 Microsoft Azure에서 실행 하는 경우 뒤에 문제가 발생할 수 있습니다.

- hello VM 다시 시작 후 tooboot을 실패합니다.

- 데이터 디스크를 분리 및 다시 연결 하는 경우 디스크에 대 한 hello 장치 이름이 변경 됩니다.

- 장치 이름을 사용하여 디스크를 참조하는 응용 프로그램 또는 스크립트가 실패합니다. 해당 hello 찾을 hello 디스크의 장치 이름이 변경 됩니다.

## <a name="cause"></a>원인

Linux에서 장치 경로 않을 toobe 일관 된 컴퓨터를 다시 시작할. 장치 이름은 주(문자) 및 보조 번호로 구성됩니다.  Hello Linux 저장 장치 드라이버에서 새 장치를 검색 하는 경우 주 및 부 장치 번호 tooit hello 사용 가능한 범위를 할당 합니다. 장치를 제거 하는 경우 hello 장치 번호는 해제 된 toobe 나중에 다시 사용 합니다.

hello 문제 때문에 발생 hello hello SCSI 하위 시스템에서 예약 된 Linux에서 검색 하는 장치 발생 하는 비동기적으로 합니다. 컴퓨터를 다시 시작할 hello 최종 장치 경로 명명 달라질 수 있습니다. 

## <a name="solution"></a>해결 방법

tooresolve이이 문제를 영구 이름을 사용 합니다. 네 개의 메서드에 toopersistent는 이름 지정-파일 시스템 레이블, uuid, id 및 경로 의해 합니다. Azure Linux Vm에 대해 hello 파일 시스템 레이블 및 UUID 메서드 권장 합니다. 

대부분의 배포판 제공 하거나 hello **nofail** 또는 **nobootwait** fstab 옵션입니다. 이 옵션을 toomount 시작 시 hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot을 사용 합니다. 이러한 매개 변수에 대 한 자세한 내용은 hello 분포의 설명서를 확인 합니다. Linux VM toouse UUID 데이터 디스크를 추가 하면 참조 하는 tooconfigure 방법에 대 한 자세한 내용은 [toohello Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)합니다. 

Hello Azure Linux 에이전트는 VM에 설치 될 때 사용 하 여 Udev 규칙 tooconstruct에서 바로 가기 링크 집합이 **/dev/disk/azure**합니다. 응용 프로그램에서 사용할 수 있습니다 이러한 Udev 규칙 및 스크립트 tooidentify 디스크 되는 VM을의 형식에 연결 된 toohello LUN hello 합니다.

## <a name="more-information"></a>자세한 정보

### <a name="identify-disk-luns"></a>디스크 LUN 식별

모든 hello 연결 된 디스크 및 기호화 된 링크를 구성할 응용 프로그램에서 Lun toofind를 사용할 수 있습니다. hello Azure Linux 에이전트에는 이제 다음과 같이 LUN toohello 장치에서 바로 가기 링크를 설정 하는 udev 규칙을 포함 되어 있습니다.

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
                                 

Lsscsi 또는 유사한 도구를 다음과 같이 사용 하 여 hello Linux 게스트에서 LUN 정보를 검색할 수도 있습니다.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Azure 구독 메타 데이터 tooidentify hello에에서 위치와 Azure 저장소의 hello hello 파티션 데이터를 저장 하는 VHD의이 게스트 LUN 정보를 사용할 수 있습니다. 예를 들어 hello az cli를 사용 합니다.

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>blkid를 사용하여 파일 시스템 UUID 검색

스크립트 또는 응용 프로그램 blkid의 hello 출력 또는 유사한 리소스의 정보를 읽고 수에 대 한 바로 가기 링크를 생성 **/dev** 사용 합니다. hello 출력의 모든 디스크 Uuid hello 연결 toohello VM과 hello 장치 파일 toowhich 연결 되어 표시 됩니다.

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

기호화 된 링크의 집합을 생성 하는 hello waagent udev 규칙 **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


hello 응용 프로그램에서이 정보를 사용할 수 hello 부팅 디스크 장치 및 hello 리소스 (임시) 디스크를 식별 합니다. Azure에서 응용 프로그램 참조 해야 너무**/dev/disk/azure/root-part1** 또는 **/dev/disk/azure-resource-part1** toodiscover 이러한 파티션을 합니다.

Hello blkid 목록에서 추가 파티션을 없을 경우 데이터 디스크에 상주 합니다. 응용 프로그램 hello UUID 이러한 파티션에 대 한 유지 관리 및 hello toodiscover hello 장치 이름 아래와 같은 경로에서 런타임에 사용할 수 있습니다.

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Hello 최신 Azure 저장소 규칙 가져오기

최신 Azure 저장소 규칙 toohello 명령 다음과 같은 실행 합니다.

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


자세한 내용은 다음 문서는 hello 참조:

- [Ubuntu: UUID 사용](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: 영구 이름 지정](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: UUID에서 수행할 수 있는 작업](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: 소개 tooDevice 최신 Linux 시스템 관리](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

