---
title: "Docker 컴퓨터를 사용 하 여 Azure에서 호스트를 Docker aaaCreate | Microsoft Docs"
description: "Azure에서 Docker 컴퓨터 toocreate docker 호스트의 사용 방법을 설명 합니다."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Docker Machine으로 Azure에서 Docker 호스트 만들기
실행 [Docker](https://www.docker.com/) 컨테이너 호스트 VM 실행 중인 hello docker 디먼이 필요 합니다.
이 항목에서는 설명 방법을 toouse hello [docker 컴퓨터](https://docs.docker.com/machine/) toocreate 새 Linux Vm을 사용 하 여 구성 hello Docker 디먼을 Azure에서 실행 되는 명령입니다. 

**참고:** 

* *이 문서는 docker-machine 버전 0.9.0-rc2 이상에 따라 달라집니다.*
* *Windows 컨테이너는 docker-hello 가까운 미래에에서 컴퓨터를 통해 지원 됩니다.*

## <a name="create-vms-with-docker-machine"></a>Docker Machine으로 VM 만들기
Docker 호스트 Vm 만들기 Azure의 hello로 `docker-machine create` hello를 사용 하 여 명령을 `azure` 드라이버입니다. 

Azure 드라이버 hello 구독 ID가 필요 합니다. Hello를 사용할 수 있습니다 [Azure CLI](cli-install-nodejs.md) 또는 hello [Azure 포털](https://portal.azure.com) tooretrieve Azure 구독. 

**Hello Azure 포털을 사용 하 여**

* 선택 **구독** hello 왼쪽된 탐색 페이지 및 복사 hello 구독 id에서입니다.

**Hello Azure CLI를 사용 하 여**

* 형식 ```azure account list``` 및 복사 hello 구독 id입니다.

형식 `docker-machine create --driver azure` toosee hello 옵션과 해당 기본값입니다.
Hello 볼 수 있습니다 [Docker Azure 드라이버 설명서](https://docs.docker.com/machine/drivers/azure/) 대 한 자세한 정보. 

hello 다음 예제에서는 hello [기본값](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), 하지만 이러한 값을 설정할 필요에 따라 않습니다. 

* hello 공용 IP와 연결 된 hello 이름 및 생성 한 인증서에 대 한 azure dns입니다. 가상 컴퓨터의 hello DNS 이름입니다. hello VM 안전 하 게 중지, hello 동적 IP를 해제 하 여 새 ip hello vm 다시 시작 되 면 hello 기능 tooreconnect를 제공 합니다. hello 이름 접두사는 해당 지역의 UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com 고유 해야 합니다.
* 아웃 바운드 인터넷 액세스에 대 한 hello VM에서 포트 80을 열려면
* hello VM tooutilize 더 빠른 프리미엄 저장소의 크기
* hello vm 디스크에 사용 되는 프리미엄 저장소

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Docker-machine으로 docker 호스트를 선택합니다.
호스트에 대 한 항목 docker 컴퓨터에 있으면 docker 명령을 실행할 때 hello 기본 호스트를 설정할 수 있습니다.

## <a name="using-powershell"></a>PowerShell 사용
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Bash 사용
```bash
eval $(docker-machine env MyDockerHost)
```

Hello 지정 된 호스트에 대해 docker 명령을 실행할 수 있습니다.

```
docker ps
docker info
```

## <a name="run-a-container"></a>컨테이너 실행
구성 된 호스트와 호스트를 올바르게 구성 되어 있는지 여부를 간단한 웹 서버 tootest 지금 실행할 수 있습니다.
여기 hello 호스트 VM을 다시 시작 되 면 hello 컨테이너가 표준 nginx 이미지를 사용 하 여 우리, 포트 80에서 수신 대기 해야 지정 및 다시 시작도 (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

hello 출력 hello 다음과 같아야 합니다.

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>테스트 hello 컨테이너
`docker ps`를 사용하여 실행 중인 컨테이너 검사

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

및 컨테이너를 형식 실행 toosee hello `docker-machine ip <VM name>` toofind hello IP 주소 tooenter hello 브라우저에서:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![ngnix 컨테이너 실행](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>요약
docker-machine을 사용하면 개별 docker 호스트 유효성 검사를 위해 Azure에서 docker 호스트를 쉽게 프로비전할 수 있습니다.
프로덕션 hello 참조 컨테이너에서의 호스팅을 [Azure 컨테이너 서비스](http://aka.ms/AzureContainerService)

Visual Studio와 함께.NET Core 응용 프로그램 toodevelop 참조 [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)

