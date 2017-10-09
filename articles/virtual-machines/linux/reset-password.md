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
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>어떻게 tooreset Azure Vm에서 로컬 Linux 암호

이 문서에서는 여러 가지 방법을 tooreset 로컬 Linux 가상 컴퓨터 (VM) 암호를 소개 합니다. Hello 사용자 계정이 만료 하거나 새 계정을 toocreate 원하는 hello 다음 메서드 toocreate 새 로컬 관리자 계정을 사용 하 여 수 있으며 액세스 toohello VM을 다시 얻을 수 있습니다.

## <a name="symptoms"></a>증상

Toohello VM에 로그인 할 수 없습니다 및 사용한 hello 암호가 올바르지 않습니다. 나타내는 메시지를 수신 합니다. 또한 사용할 수 없습니다 VMAgent tooreset 암호 hello Azure 포털에 있습니다. 

## <a name="manual-password-reset-procedure"></a>수동 암호 다시 설정 프로시저

1.  Hello VM을 삭제 하 고 hello 연결 된 디스크 유지 합니다.

2.  데이터 디스크 tooanother와 운영 체제 드라이브 hello 연결 임시 VM hello에 동일한 위치입니다.

3.  다음 임시 VM toobecome hello에서 SSH 명령을 hello 슈퍼 사용자를 실행 합니다.


    ~~~~
    sudo su
    ~~~~

4.  실행 **fdisk l** 또는 시스템 로그 toofind hello에 새로 연결 된 디스크. Hello 드라이브 이름 toomount를 찾습니다. 그런 다음 hello에 임시 VM을 찾는 위치 hello 관련 로그 파일입니다.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    hello 다음은 hello grep 명령의 예제 출력입니다.

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  **tempmount**라는 탑재 지점을 만듭니다.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Hello 탑재 지점에 hello OS 디스크를 탑재 합니다. 일반적으로 toomount sdc1 또는 sdc2 필요한 합니다. 이 hello 끊어진된 컴퓨터 디스크에서 /etc 디렉터리에 파티션을 호스팅하는 hello에 따라 달라 집니다.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  변경하기 전에 백업을 수행합니다.

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  필요한 hello 사용자의 암호를 다시 설정 하십시오.

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  이동 hello hello 컴퓨터의 디스크 손상 파일 toohello 올바른 위치를 수정 합니다.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
