---
title: "Azure에서 Linux 가상 컴퓨터에서 램프 aaaDeploy | Microsoft Docs"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Azure에서 LAMP 스택 배포
이 문서 toodeploy는 Apache 웹 서버, MySQL 및 Azure에서 PHP (hello LAMP 스택) 방법을 안내 합니다. Azure 계정이 필요 ([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="quick-command-summary"></a>빠른 명령 요약

1. 저장 및 편집 hello [azuredeploy.parameters.json 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) 로컬 컴퓨터의 tooyour 기본 설정 합니다.
2. 다음 두 명령을 toocreate hello 리소스 그룹을 실행 하 고 템플릿을 배포 합니다.

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>기존 VM에 LAMP 배포
hello 다음 업데이트 패키지 명령 후 Apache, MySQL 및 PHP를 설치 합니다.

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>새 VM에 LAMP 배포 연습

1. 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) toocontain hello 새 VM:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate VM 자체 hello, 찾을 수는 이미 작성 된 Azure 리소스 관리자 템플릿을 사용 하 여 [GitHub에서 여기](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)합니다.

2. Hello 저장 [azuredeploy.parameters.json 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour 로컬 컴퓨터입니다.
3. Hello 편집 **azuredeploy.parameters.json** 파일 tooyour 기본 입력 설정입니다.
4. 배포 된 hello 서식 파일 [az 그룹 배포 만들기] json 파일을 다운로드 한 hello 참조:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

hello 비슷한 toohello 다음은 예제 출력:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

이미 설치된 LAMP를 사용해 이제 Linux VM을 만들었습니다. 원하는 경우 너무 아래로 이동 하 여 hello 설치를 확인할 수 있습니다[확인 램프 성공적으로 설치](#verify-lamp-successfully-installed)합니다.

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>기존 VM에 LAMP 배포 연습
Head 수 Linux VM을 만드는 데 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli)합니다. Hello Linux VM에 tooSSH을 다음으로, 해야 합니다. Head 수 SSH 키 만들기에서 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux/Mac에서 SSH 키](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
SSH 키가 있는 경우 계속해서 `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`을 사용하여 Linux VM에 SSH합니다.

Linux VM에서 작업 하는 했으므로 Debian 기반 배포판의 hello LAMP 스택 설치 진행할 수 있습니다. 다른 Linux 배포판에 대 한 hello 정확한 명령 다를 수 있습니다.

#### <a name="installing-on-debianubuntu"></a>Debian/Ubuntu에 설치
설치 된 패키지를 다음 hello 필요한: `apache2`, `mysql-server`, `php5`, 및 `php5-mysql`합니다. 이러한 패키지를 직접 가져오거나 Tasksel을 사용하여 설치할 수 있습니다.
설치 하기 전에 필요한 toodownload 및 패키지 목록을 업데이트 합니다.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>개별 패키지
apt-get을 사용합니다.

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Tasksel 사용
또는 관련된 여러 패키지를 하나의 조정된 “작업”으로 시스템에 설치하는 Debian/Ubuntu 도구인 Tasksel을 다운로드할 수 있습니다.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

hello 이전 옵션 중 하나를 실행 한 후이 패키지 및 기타 다양 한 종속성 증명된 tooinstall 수입니다. MySQL에 대 한 관리 암호 tooset 'y' 및 'Enter' toocontinue 누르고 다른 지시에 따라 합니다. 이 프로세스는 MySQL 가진 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다. 

![][1]

다음 명령은 toosee hello 패키지로 사용할 수 있는 기타 PHP 확장을 실행 합니다.

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Info.php 문서 만들기
이제 있을 수 toocheck Apache, MySQL 및 PHP의 버전 있는 hello 명령줄을 통해 입력 하 여 `apache2 -v`, `mysql -v`, 또는 `php -v`합니다.

Tootest 같은 앞서는, 경우에 브라우저에서 빠른 PHP 정보 페이지 tooview를 만들 수 있습니다. 이 명령을 사용하여 Nano 텍스트 편집기로 파일을 만듭니다.

```bash
sudo nano /var/www/html/info.php
```

Hello GNU Nano 텍스트 편집기에서 줄을 다음 hello를 추가 합니다.

```php
<?php
phpinfo();
?>
```

그런 다음 저장 하 고 hello 텍스트 편집기를 종료 합니다.

모든 새 설치 항목이 적용되도록 이 명령을 사용하여 Apache를 다시 시작합니다.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>LAMP 설치가 성공적인지 확인
이제 브라우저를 열고 toohttp://youruniqueDNS/info.php 라인으로 전환 하 여 만든 hello PHP 정보 페이지를 확인할 수 있습니다. 이와 유사한 toothis 이미지 표시 됩니다.

![][2]

Tooyou http://youruniqueDNS/ 이동 하 여 hello Apache2 Ubuntu 기본 페이지를 확인 하 여 Apache 설치를 확인할 수 있습니다. hello 비슷한 toohello 다음은 예제 출력:

![][3]

축하합니다. 이제 방금 Azure Vm에 LAMP 스택 설정을 마쳤습니다!

## <a name="next-steps"></a>다음 단계
체크 아웃 하 hello hello 램프 스택에 Ubuntu 설명서:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
