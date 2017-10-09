---
title: "Azure 파일 저장소와 Linux aaaUse | Microsoft Docs"
description: "Linux에서 SMB를 통한 toomount Azure 파일을 공유 하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Linux에서 Azure File Storage 사용
[Azure 파일 저장소](../storage-dotnet-how-to-use-files.md) 는 Microsoft의 쉬운 toouse 클라우드 파일 시스템입니다. Hello를 사용 하 여 Linux 배포에서 azure 파일 공유를 탑재할 수 [cifs 유틸리티 패키지](https://wiki.samba.org/index.php/LinuxCIFS_utils) hello에서 [Samba 프로젝트](https://www.samba.org/)합니다. 이 문서에서는 두 가지 방법으로 toomount Azure 파일 공유: hello로 주문형 `mount` 명령 및에서 항목을 만들어 부팅에 `/etc/fstab`합니다.

> [!NOTE]  
> 순서 toomount hello 외부의 경우 Azure 파일 공유에에서는 다른 Azure 지역의 hello OS 또는 온-프레미스 등,에 호스팅된 Azure 지역 SMB 3.0의 hello 암호화 기능을 지원 해야 합니다. Linux용 SMB 3.0에 대한 암호화 기능이 4.11 커널에 도입되었습니다. 이 기능을 사용하면 온-프레미스 또는 다른 Azure 지역에서 Azure 파일 공유를 탑재할 수 있습니다. 게시의 hello 시이 기능은 backported tooUbuntu 이상 16.04에서 되었습니다.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Linux 및 hello cifs 유틸리티 패키지와 함께 Azure 파일 탑재에 대 한 필수 공유
* **Hello cifs 유틸리티 패키지 설치를 가질 수 있는 Linux 배포판 선택**: hello hello Azure 이미지 갤러리의 Linux 배포판을 따르는 것이 좋습니다.

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**hello cifs 유틸리티 패키지가 설치 되어**: hello 패키지 관리자를 사용 하 여 사용자가 선택한 hello Linux 배포판에 hello cifs 유틸리티를 설치할 수 있습니다. 

    **Ubuntu** 및 **Debian 기반** 배포를 사용 하 여 hello `apt-get` 패키지 관리자.

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    **RHEL** 및 **CentOS**, hello를 사용 하 여 `yum` 패키지 관리자.

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    **openSUSE**, hello를 사용 하 여 `zypper` 패키지 관리자.

    ```
    sudo zypper install samba*
    ```

    Hello 적절 한 패키지 관리자를 사용 하 여 다른 배포 또는 [소스에서 컴파일하여](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)합니다.

* **Hello 탑재 된 공유의 hello 디렉터리/파일 사용 권한을 결정**: hello 아래 예제에서는 사용 하 여, 0777 toogive 읽기, 쓰기 및 실행 tooall 사용자 사용 권한. 다른 [chmod 권한](https://en.wikipedia.org/wiki/Chmod)으로 바꿀 수 있습니다. 

* **저장소 계정 이름**: toomount Azure 파일 공유, hello 저장소 계정의 이름을 hello 필요 합니다.

* **저장소 계정 키**: toomount Azure 파일 공유, 기본 (또는 보조) 저장소 키 hello 필요 합니다. SAS 키는 현재 탑재를 지원하지 않습니다.

* **포트 445가 열려 있는지 확인**: 방화벽에서 TCP를 차단 하면 toosee 포트 445 클라이언트 컴퓨터에서 확인 SMB TCP 포트 445-를 통해 통신 합니다.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Azure 파일 공유와 요청 시 hello 탑재`mount`
1. **[Linux 배포판에 대 한 hello cifs 유틸리티 패키지 설치](#install-cifs-utils)**합니다.

2. **Hello 탑재 지점에 대 한 폴더를 만들고**: hello 파일 시스템에서 아무 곳 이나 수행할 수 있습니다.

    ```
    mkdir mymountpoint
    ```

3. **사용 하 여 hello 탑재 명령 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, 및 `<storage-account-key>` hello 적절 한 정보입니다.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> 완료 되 면 Azure 파일 공유를 hello를 사용 하 여, 사용할 수 있습니다 `sudo umount ./mymountpoint` toounmount hello 공유 합니다.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Azure 파일 공유를 hello에 대 한 영구 탑재 지점 만들기`/etc/fstab`
1. **[Linux 배포판에 대 한 hello cifs 유틸리티 패키지 설치](#install-cifs-utils)**합니다.

2. **Hello 탑재 지점에 대 한 폴더를 만들고**: hello 파일 시스템에서 아무 곳 이나 수행할 수 있습니다 하지만 toonote hello hello 폴더의 절대 경로 필요 합니다. 다음 예제는 hello 루트 아래에 폴더를 만듭니다.

    ```
    sudo mkdir /mymountpoint
    ```

3. **사용 하 여 hello 다음 명령은 다음 줄을 너무 tooappend hello`/etc/fstab`**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, 및 `<storage-account-key>` hello 적절 한 정보입니다.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> 사용할 수 있습니다 `sudo mount -a` 편집한 후 toomount hello Azure 파일 공유 `/etc/fstab` 다시 부팅 하는 대신 합니다.

## <a name="feedback"></a>사용자 의견
Linux 사용자를 toohear 원하는!

Linux 사용자 그룹에 대 한 Azure 파일 저장소 hello 위한 포럼을 제공 하면 tooshare 피드백 평가 하 고 Linux에서 파일 저장소를 채택 합니다. 전자 메일 [Azure 파일 저장소 Linux 사용자](mailto:azurefileslinuxusers@microsoft.com) toojoin hello 사용자의 그룹입니다.

## <a name="next-steps"></a>다음 단계
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.
* [파일 서비스 REST API 참조](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [어떻게 toouse AzCopy Microsoft Azure 저장소](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 Azure 저장소와](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [FAQ](../storage-files-faq.md)
* [문제 해결](storage-troubleshoot-linux-file-connection-problems.md)
