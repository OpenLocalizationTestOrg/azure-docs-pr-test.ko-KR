---
title: "Azure CLI 1.0 hello로 Linux 가상 컴퓨터에서 램프 aaaDeploy | Microsoft Docs"
description: "Azure에서 Linux VM의 tooinstall hello LAMP 스택 하는 방법을 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>LAMP 스택 hello Azure CLI 1.0로 배포
이 문서 toodeploy는 Apache 웹 서버, MySQL 및 Azure에서 PHP (hello LAMP 스택) 방법을 안내 합니다. Azure 계정이 필요 합니다 ([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 hello [Azure CLI](../../cli-install-nodejs.md) 즉 [tooyour Azure 계정을 연결](../../xplat-cli-connect.md)합니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0]-우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* 기존 VM에 LAMP 배포

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>새 VM에 LAMP 배포 연습
만들어서 시작할 수는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md) 를 포함할 새 VM hello:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate VM 자체 hello, 찾을 수는 이미 작성 된 Azure 리소스 관리자 템플릿을 사용 하 여 [GitHub에서 여기](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)합니다.

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

입력을 몇 가지 더 하라는 메시지가 담긴 응답을 보게 될 것입니다.

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

이미 설치된 LAMP를 사용해 이제 Linux VM을 만들었습니다. 원하는 경우 너무 아래로 이동 하 여 hello 설치를 확인할 수 있습니다[확인 램프 성공적으로 설치](#verify-lamp-successfully-installed)합니다.

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>기존 VM에 LAMP 배포 연습
Head 수 Linux VM을 만드는 데 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. Hello Linux VM에 tooSSH을 다음으로, 해야 합니다. Head 수 SSH 키 만들기에서 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux/Mac에서 SSH 키](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
SSH 키가 있는 경우 계속해서 `ssh exampleUsername@exampleDNS`을 사용하여 Linux VM에 SSH합니다.

Linux VM에서 작업 하는 했으므로 Debian 기반 배포판의 hello LAMP 스택 설치 진행할 수 있습니다. 다른 Linux 배포판에 대 한 hello 정확한 명령 다를 수 있습니다.

#### <a name="installing-on-debianubuntu"></a>Debian/Ubuntu에 설치
설치 된 패키지를 다음 hello 필요한: `apache2`, `mysql-server`, `php5`, 및 `php5-mysql`합니다. 이러한 패키지를 직접 가져오거나 Tasksel을 사용하여 설치할 수 있습니다. 아래에는 두 옵션 모두에 대한 지침이 나와 있습니다.
설치 하기 전에 필요한 toodownload 및 패키지 목록을 업데이트 합니다.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>개별 패키지
apt-get을 사용합니다.

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Tasksel 사용
또는 관련된 여러 패키지를 하나의 조정된 “작업”으로 시스템에 설치하는 Debian/Ubuntu 도구인 Tasksel을 다운로드할 수 있습니다.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

hello 이전 옵션 중 하나를 실행 한 후이 패키지 및 기타 다양 한 종속성 증명된 tooinstall 수입니다. 'Y' 및 'Enter' toocontinue 누르고 MySQL에 대 한 모든 다른 프롬프트 tooset 관리자 암호를 수행 합니다. 이 MySQL와 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다. 

![][1]

다음 명령은 toosee hello 패키지로 사용할 수 있는 기타 PHP 확장을 실행 합니다.

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Info.php 문서 만들기
이제 있을 수 toocheck Apache, MySQL 및 PHP의 버전 있는 hello 명령줄을 통해 입력 하 여 `apache2 -v`, `mysql -v`, 또는 `php -v`합니다.

Tootest 같은 앞서는, 경우에 브라우저에서 빠른 PHP 정보 페이지 tooview를 만들 수 있습니다. 이 명령을 사용하여 Nano 텍스트 편집기로 파일을 만듭니다.

    user@ubuntu$ sudo nano /var/www/html/info.php

Hello GNU Nano 텍스트 편집기에서 줄을 다음 hello를 추가 합니다.

    <?php
    phpinfo();
    ?>

그런 다음 저장 하 고 hello 텍스트 편집기를 종료 합니다.

모든 새 설치 항목이 적용되도록 이 명령을 사용하여 Apache를 다시 시작합니다.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>LAMP 설치가 성공적인지 확인
이제 브라우저를 열고 toohttp://youruniqueDNS/info.php 라인으로 전환 하 여 만든 hello PHP 정보 페이지를 확인할 수 있습니다. 이와 유사한 toothis 이미지 표시 됩니다.

![][2]

Tooyou http://youruniqueDNS/ 이동 하 여 hello Apache2 Ubuntu 기본 페이지를 확인 하 여 Apache 설치를 확인할 수 있습니다. 다음 이미지와 유사하게 표시됩니다.

![][3]

축하합니다. 이제 방금 Azure Vm에 LAMP 스택 설정을 마쳤습니다!

## <a name="next-steps"></a>다음 단계
체크 아웃 하 hello hello 램프 스택에 Ubuntu 설명서:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png