---
title: "CLI hello에서 aaaReset Linux VM 암호 및 SSH 키 | Microsoft Docs"
description: "Toouse hello hello Azure 명령줄 인터페이스 (CLI) tooreset Linux VM 암호 또는 SSH 키에서 VMAccess 확장 hello SSH 구성을 수정 하 고 디스크 일관성을 검사 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Tooreset Linux VM 암호 또는 SSH 키를 hello SSH 구성을 수정 하 고 hello VMAccess 확장을 사용 하 여 디스크 일관성 검사 방법
Hello 작업에서는 VMAccessForLinux 확장을 사용 하 여 hello Azure CLI tooreset hello 암호 또는 SSH 키와 암호를 잊은 경우, 잘못 된 SSH (보안 셸) 키 또는 hello SSH 구성 문제가 때문에 Azure에서 tooa Linux 가상 컴퓨터를 연결할 수 없는 경우, 수정 SSH 구성을 hello 및 디스크 일관성을 검사 합니다. 

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)합니다.

Hello를 사용 하면 Azure CLI hello로 **azure vm 확장 집합** 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트) tooaccess 명령에서 명령을 합니다. 자세한 확장 사용을 보려면 **azure help vm extension set** 를 실행합니다.

Azure CLI hello로 할 수 있는 다음 작업 hello:

* [Hello 암호 재설정](#pwresetcli)
* [Hello SSH 키를 다시 설정](#sshkeyresetcli)
* [Hello 암호 및 hello SSH 키를 다시 설정](#resetbothcli)
* [새 sudo 사용자 계정 만들기](#createnewsudocli)
* [Hello SSH 구성을 다시 설정](#sshconfigresetcli)
* [사용자 삭제](#deletecli)
* [Hello VMAccess 확장의 hello 상태를 표시 합니다.](#statuscli)
* [추가된 디스크의 일관성 검사](#checkdisk)
* [Linux VM에서 추가된 디스크 복구](#repairdisk)

## <a name="prerequisites"></a>필수 조건
Toodo hello 다음이 필요 합니다.

* 너무 해야[hello Azure CLI를 설치](../../../cli-install-nodejs.md) 및 [tooyour 구독을 연결](../../../xplat-cli-connect.md) toouse Azure 계정과 연결 된 리소스입니다.
* Hello 명령 프롬프트에서 hello 다음을 입력 하 여 hello hello 클래식 배포 모델에 대 한 올바른 모드를 설정 합니다.
    ``` 
        azure config mode asm
    ```
* Tooreset 둘 중 하나를 원하는 경우 새 암호 또는 SSH 키 집합이 있어야 합니다. Tooreset hello SSH 구성을 하려는 경우 이러한 필요 하지 않습니다.

## <a name="pwresetcli"></a>Hello 암호 재설정
1. 다음 줄을 사용하여 PrivateConf.json이라는 파일을 로컬 컴퓨터에 만듭니다. **myUserName** 및 **myP@ssW0rd**를 고유한 사용자 이름과 암호로 바꾸고 만료 날짜를 고유하게 설정합니다.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. 에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Hello SSH 키를 다시 설정
1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다. Hello 대체 **: myUserName** 및 **mySSHKey** 고유한 정보가 포함 된 값입니다.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. 에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Hello 암호와 hello SSH 키를 모두 다시 설정
1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다. Hello 대체 **: myUserName**, **mySSHKey** 및  **myP@ssW0rd**  고유한 정보가 포함 된 값입니다.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. 에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>새 sudo 사용자 계정 만들기

사용자 이름을 잊은 경우 hello sudo 권한이로 새 레코드 toocreate VMAccess를 사용할 수 있습니다. 이 경우 기존 사용자 이름 hello 및 암호는 수정 되지 않습니다.

암호 액세스를 사용 하 여 hello 스크립트에 있는 새 sudo 사용자 toocreate [hello 암호 재설정](#pwresetcli) hello 새 사용자 이름을 지정 합니다.

SSH 키 액세스를 사용 하 여 hello 스크립트에 있는 새 sudo 사용자 toocreate [hello SSH 키 재설정](#sshkeyresetcli) hello 새 사용자 이름을 지정 합니다.

사용할 수도 있습니다 [hello 암호 및 hello SSH 키 재설정](#resetbothcli) toocreate 암호 및 SSH 키 액세스 권한을 모두 사용 하 여 새 사용자입니다.

## <a name="sshconfigresetcli"></a>Hello SSH 구성을 다시 설정
Hello SSH 구성이 원치 않는 상태가 되 면 액세스 toohello VM을 손실 될 수 있습니다. Hello VMAccess 확장 tooreset hello 구성 tooits 기본 상태를 사용할 수 있습니다. toodo 따라서 하기만 하면 tooset hello "reset_ssh" 키 너무 "True"입니다. hello 확장 hello SSH 서버를 다시 시작을 열고 hello SSH 포트를 VM에는 hello SSH 구성 toodefault 값 다시 설정 합니다. hello 사용자 계정 (이름, 암호 또는 SSH 키)은 바뀌지 않습니다.

> [!NOTE]
> 다시 설정 됩니다. hello SSH 구성 파일은 /etc/ssh/sshd_config에 있습니다.
> 
> 

1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. 에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>사용자 삭제
사용자 계정을 직접 toohello VM에 로그인 하지 않고도 toodelete 하려는 경우이 스크립트를 사용할 수 있습니다.

1. 이 콘텐츠를 대체에 대 한 사용자 이름 tooremove hello와 PrivateConf.json 라는 파일을 만들어 **removeUserName**합니다. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. 에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Hello VMAccess 확장의 hello 상태를 표시 합니다.
이 명령을 실행 하는 hello VMAccess 확장의 toodisplay hello 상태입니다.

```
        azure vm extension get
```

## <a name='checkdisk'></a>추가된 디스크의 일관성 검사
Linux 가상 컴퓨터의 모든 디스크에서 toorun fsck, toodo hello 다음이 필요 합니다.

1. 이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다. 디스크 검사 toocheck 디스크 연결 tooyour 가상 컴퓨터 여부는 부울 값을 사용 합니다. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. 실행에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령 tooexecute **myVM**합니다.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>디스크 복구
Linux 가상 컴퓨터에 hello VMAccess 확장 tooreset hello 탑재 구성을 사용 하는 toorepair 하거나 디스크를 탑재 하 탑재 구성 오류가 발생 합니다. 이때 hello 이름에 대 한 디스크의 **myDisk**합니다.

1. 이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. 실행에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령 tooexecute **myVM**합니다.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>다음 단계
* Toouse Azure PowerShell cmdlet 또는 Azure 리소스 관리자 템플릿 tooreset hello 암호 또는 SSH 키를 원하는 경우 hello SSH 구성을 수정 하 고 디스크 일관성 검사, hello 참조 [GitHub에서 VMAccess 확장 문서](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)합니다. 
* Hello를 사용할 수도 있습니다 [Azure 포털](https://portal.azure.com) tooreset hello 암호 또는 SSH 키는 Linux VM의 hello 클래식 배포 모델에 배포 합니다. 현재 hello 리소스 관리자 배포 모델에 배포 된 Linux VM에 대 한 hello 포털 do toothis를 사용할 수 없습니다.
* Azure 가상 컴퓨터에 VM 확장을 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

