---
title: "가상 컴퓨터 확장으로 응용 프로그램 배포 aaaAutomating | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Linux VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포

모든 Azure 인프라 요구 사항 파악 고 배포 템플릿을로 변환 되었습니다, 해결 toobe hello 실제 응용 프로그램 배포에 필요 합니다. 여기에 응용 프로그램 배포를 Azure 리소스 tooinstalling hello 실제 응용 프로그램 이진 파일을 참조 합니다. Hello Music Store 샘플을.Net Core, NGINX, 및 감독자 toobe 각 가상 컴퓨터에 설치 및 구성 필요 합니다. 이진 파일 toobe hello 가상 컴퓨터에 설치 해야 하는 Music Store hello 및 hello Music Store 데이터베이스 미리 만들어 합니다.

이 문서는 가상 컴퓨터 확장 응용 프로그램 배포 및 구성 tooAzure 가상 컴퓨터를 자동화할 수 방법을 자세히 설명 합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다. hello 완전 한 템플릿 여기 – 있습니다 [ubuntu 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.

## <a name="configuration-script"></a>구성 스크립트
가상 컴퓨터 확장은 tooprovide 구성 자동화 가상 컴퓨터에 대해 실행 되는 특별 한 프로그램입니다. 바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다. 사용자 지정 스크립트 확장에는 모든 가상 컴퓨터에 대 한 스크립트를 사용 하는 toorun 될 수 있습니다. Hello Music Store 샘플 toohello 사용자 지정 스크립트 확장 tooconfigure hello Ubuntu 가상 컴퓨터를 사용 되며 hello 음악 스토어 응용 프로그램을 설치 합니다. 

가상 컴퓨터 확장 된 Azure 리소스 관리자 템플릿을에서 선언 되는 방법을 자세히 보여 주는 하기 전에를 실행 하는 hello 스크립트를 검사 합니다. 이 스크립트는 hello Ubuntu 가상 컴퓨터 toohost hello 음악 스토어 응용 프로그램을 구성합니다. Hello 스크립트에 필요한 모든 소프트웨어 설치를 실행 하는 경우 소스 제어를 hello 음악 스토어 응용 프로그램을 설치 하 고 hello 데이터베이스를 준비 합니다. 

.NET 호스팅에 대 한 더 toolearn 핵심 응용 프로그램 참조 linux [게시 tooa Linux 프로덕션 환경](https://docs.asp.net/en/latest/publishing/linuxproduction.html)합니다.

> 이 샘플은 데모용입니다.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>VM 스크립트 확장
VM 확장 수에 대해 실행할 수는 가상 컴퓨터 빌드 시 hello Azure 리소스 관리자 템플릿을에 hello 확장을 리소스를 포함 하 여 합니다. hello Visual Studio 추가 리소스 마법사를 사용 하거나 hello 서식 파일에 유효한 JSON을 삽입 하 여 hello 확장을 추가할 수 있습니다. 가상 컴퓨터 리소스; hello 안에 중첩 hello 스크립트 확장을 리소스 이 hello 다음 예제에서에서 볼 수 있습니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)합니다. 

아래 스크립트 hello JSON hello에서는 GitHub에 저장 됩니다. 이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다. 또한 Azure 리소스 관리자 템플릿을 사용 hello 스크립트 실행 문자열 tooconstructed는 스크립트 실행에 대 한 템플릿 매개 변수 값을 매개 변수로 사용할 수 있습니다. Hello 서식 파일을 배포 하는 경우 데이터는 제공 하는 경우에 되며 이러한 값 hello 스크립트를 실행할 때 사용할 수 있습니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Hello 사용자 지정 스크립트 확장을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [사용자 지정 스크립트 확장을 리소스 관리자 템플릿으로](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="next-step"></a>다음 단계
<hr>

[추가 Azure Resource Manager 템플릿 살펴보기](https://github.com/Azure/azure-quickstart-templates)

