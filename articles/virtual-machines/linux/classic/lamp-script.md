---
title: "aaaUse hello Linux VM의 CustomScript 확장 | Microsoft Docs"
description: "Toouse hello CustomScript 확장 toodeploy 응용 프로그램이 Azure에서 Linux 가상 컴퓨터에 만드는 hello 클래식 배포 모델을 사용 하는 방법에 대해 알아봅니다."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Linux 용 hello Azure CustomScript 확장을 사용 하 여 램프 앱 배포
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Hello 리소스 관리자 모델을 사용 하 여 LAMP 스택 배포에 대 한 내용은 [여기](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Linux 용 Microsoft Azure CustomScript 확장 hello hello (예를 들어 Python 및 Bash)의 VM에서 지 원하는 모든 스크립팅 언어로 작성 된 임의의 코드를 실행 하 여 방식으로 toocustomize 가상 컴퓨터 (Vm)를 제공 합니다. 응용 프로그램 배포 toomultiple 컴퓨터 매우 융통성 있게 tooautomate을 제공합니다.

Hello CustomScript 확장을 배포 하려면 Azure 포털, Windows PowerShell 또는 Azure CLI (명령줄 인터페이스 Azure) hello hello를 사용 하 여 합니다.

이 문서에서는 hello Azure CLI toodeploy 간단한 램프 응용 프로그램 tooan Ubuntu VM hello 클래식 배포 모델을 사용 하 여 만든 합니다.

## <a name="prerequisites"></a>필수 조건
이 예제에서는 먼저 Ubuntu 14.04 이상을 실행하는 두 개의 Azure VM을 만듭니다. hello Vm 라고 *스크립트 vm* 및 *램프 vm*합니다. Hello Vm을 만들 때 고유한 이름을 사용 합니다. 하나는 사용 되는 toorun hello CLI 명령을 고 하나는 사용 되는 toodeploy hello 램프 앱.

또한 해야 Azure 저장소 계정 및 키 tooaccess it (에서 얻을 수 있습니다이 hello Azure 포털).

Azure에서 Linux Vm을 만드는 데 도움이 필요한 경우 너무 참조[만들 가상 컴퓨터 실행 중인 Linux](createportal.md)합니다.

hello 설치 명령은 Ubuntu, 가정 하지만 지원 되는 모든 Linux 배포판에 대 한 hello 설치를 조정할 수 있습니다.

hello 스크립트 vm VM 필요 toohave 작업 연결 tooAzure와 함께 Azure CLI를 설치 합니다. 에 대 한 도움말은이 너무 참조[설치 및 구성 hello Azure 명령줄 인터페이스](../../../cli-install-nodejs.md)합니다.

## <a name="upload-a-script"></a>스크립트 업로드
원격 VM tooinstall hello LAMP 스택 hello CustomScript 확장 toorun 스크립트를 사용 하 여 알아보고 PHP 페이지를 만들 하겠습니다. 어디에서 든 순서 tooaccess hello 스크립트에서 Azure blob으로 업로드 합니다 했습니다.

### <a name="script-overview"></a>스크립트 개요
hello 스크립트 예제는 LAMP 스택 tooUbuntu (MySQL의 자동 설치를 설정 하는 등)를 설치 하 고, 간단한 PHP 파일을 작성, Apache 시작 합니다.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>스크립트 업로드
예를 들어 hello 스크립트를 텍스트 파일로 저장 *install_lamp.sh*를 다음 저장소 tooAzure 업로드 합니다. Azure CLI를 사용하면 이 작업을 쉽게 수행할 수 있습니다. hello 다음 예제에서는 업로드 hello 파일 tooa 저장소 컨테이너 이름이 "스크립트" 합니다. Toocreate 해야 hello 컨테이너 존재 하지 않는 경우 그 첫 번째입니다.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Toodownload Azure 저장소에서 스크립트를 hello 하는 방법을 설명 하는 JSON 파일을 만들 수도 있습니다. 으로 저장할 *public_config.json* ("mystorage" hello 저장소 계정의 이름으로 대체):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Hello 확장 배포
Hello 다음 명령 toodeploy hello Linux CustomScript 확장 toohello 원격에서는 이제 Azure CLI hello 사용 하 여 VM입니다.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

이전 명령은 hello 다운로드 하 고 hello 실행 *install_lamp.sh* hello 라는 VM에서 스크립트 *램프 vm*합니다.

웹 서버를 포함 하는 hello 앱, 이후 기억 hello에 수신 대기 포트는 HTTP tooopen hello 다음 명령 사용 하 여 원격 VM입니다.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>모니터링 및 문제 해결
얼마나 잘 hello 로그 파일 확인 하 여 사용자 지정 스크립트 실행 hello hello 원격 VM을 확인할 수 있습니다. SSH 너무*램프 vm* 및 hello 다음 명령 사용 하 여 비상 hello 로그 파일입니다.

    cd /var/log/azure/customscript
    tail -f handler.log

Hello CustomScript 확장을 실행 한 후에 정보에 대해 만든 toohello PHP 페이지를 찾아볼 수 있습니다. 이 문서의 hello 예제는 hello PHP 페이지 *http://lamp-vm.cloudapp.net/phpinfo.php*합니다.

## <a name="additional-resources"></a>추가 리소스
에서는 동일한 기본 단계 toodeploy hello 더 복잡 한 응용 프로그램입니다. 이 예에서 hello 설치 스크립트는 Azure 저장소에 공개 blob으로 저장 되었습니다. 보다 안전한 옵션을 사용 하 여 보안 blob toostore hello 설치 스크립트 됩니다는 [보안 액세스 서명](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Azure CLI, Linux 및 hello CustomScript 확장을 위한 추가 리소스는 다음에 나열 됩니다.

[CustomScript 확장을 사용하여 Linux VM 사용자 지정 작업 자동화](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Azure Linux 확장(GitHub)](https://github.com/Azure/azure-linux-extensions)