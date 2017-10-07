---
title: "Linux 용 Docker VM 확장 aaaUsing | Microsoft Docs"
description: "Docker 및 hello Azure 가상 컴퓨터 확장 및 클래식 배포 모델에서 toocreate Azure 가상 컴퓨터의 docker 호스트를 사용 하 여 Azure CLI hello 하는 방법을 설명 합니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Azure 클래식 포털 hello로 hello Docker VM 확장을 사용 하 여
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

[Docker](https://www.docker.com/) hello 중 하나를 사용 하는 가장 인기 있는 가상화 방법입니다. [Linux 컨테이너](http://en.wikipedia.org/wiki/LXC) 데이터 격리 하 고 공유 리소스에서 계산 하는 방법으로 가상 컴퓨터 대신 합니다. 관리 하는 hello Docker VM 확장을 사용할 수 있습니다 [Azure Linux 에이전트] toocreate 개수에 관계 없이 Azure에서 응용 프로그램에 대 한 컨테이너를 호스트 하는 Docker VM입니다.

> [!NOTE]
> 이 항목에서 Docker VM a toocreate Azure 클래식 포털 hello 하는 방법을 설명 합니다. hello 명령줄에서 Docker VM toocreate 참조 toosee [toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]합니다. 높은 수준의 컨테이너와 그 장점을 설명 toosee 참조 hello [Docker 높은 수준 화이트 보드](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)합니다.
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Hello 이미지 갤러리에서에서 새 VM 만들기
hello 첫 번째 단계는 Azure VM hello 예제 서버 이미지 및 Ubuntu 14.04 데스크톱으로 hello 이미지 갤러리에서에서 Ubuntu 14.04 LTS 이미지를 사용 하 여 클라이언트로 Docker VM 확장을 지 원하는 Linux 이미지에서 필요 합니다. Hello 포털에서 클릭 **+ 새로 만들기** 의 hello 하단 왼쪽 모서리 toocreate 새 VM 인스턴스 고 hello 또는 hello 선택할 수 있는 항목이에서 Ubuntu 14.04 LTS 이미지를 선택 아래와 같이 이미지 갤러리를 완료 합니다.

> [!NOTE]
> 현재 2014 년 7 월 보다 더 최신 Ubuntu 14.04 LTS 이미지만 hello Docker VM 확장을 지원 합니다.
> 
> 

![새 Ubuntu 이미지 만들기](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Docker 인증서 만들기
VM을 만든 hello, 후 클라이언트 컴퓨터에 Docker가 설치 되어 있는지 확인 합니다. 자세한 내용은 [Docker 설치 지침](https://docs.docker.com/installation/#installation)을 참조하세요.

Hello 너무에 따라 Docker 통신에 대 한 인증서 및 키 파일을 만들[https로 Docker 실행] hello 안에 위치 시켜야합니다  **`~/.docker`**  클라이언트 컴퓨터에 디렉터리입니다.

> [!NOTE]
> hello 포털에 hello Docker VM 확장에는 현재 base64 인코딩 되는 자격 증명이 필요 합니다.
> 
> 

Hello 명령줄에서 사용 하 여  **`base64`**  또는 다른 즐겨찾기 tool toocreate base64 인코딩된 항목 인코딩. 인증서 및 키 파일의 간단한 집합으로이 작업을 수행 하면 비슷한 toothis 변경할 수 있습니다.

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Hello Docker VM 확장 추가
tooadd hello Docker VM 확장을 만들었으므로 hello VM 인스턴스를 찾아서 너무 아래로 스크롤하여**확장** 아래와 같이 toobring VM 확장을 클릭 합니다.

> [!NOTE]
> 이 기능은 hello 미리 보기 포털에서 지원 됩니다: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>확장 추가
Hello 클릭 **+ 추가** toodisplay hello 가능한 VM 확장 toothis VM을 추가할 수 있습니다.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Hello Docker VM 확장을 선택 합니다.
Hello hello Docker 설명 및 중요 링크 되면서 Docker VM 확장을 선택 하 고 클릭 한 다음 **만들기** hello 아래쪽 toobegin hello 설치 절차에서 합니다.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>인증서 및 키 파일 추가
Hello 양식 필드의 hello 다음 그래픽에에서 표시 된 대로 hello base64 인코딩된 버전의 CA 인증서, 해당 서버 인증서 및 서버 키를 입력 합니다.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> 참고는 (예: hello 이미지 이전) hello 2376은 기본적으로 채워집니다. 여기에서 모든 끝점을 입력할 수 있습니다 하지만 hello 다음 단계를 끝점에 일치 하는 hello tooopen 됩니다. Hello 기본값을 변경 하는 경우 있는지 tooopen hello 끝점 hello 다음 단계에서 일치를 확인 합니다.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Hello Docker 통신 끝점 추가
만든 hello 리소스 그룹을 볼 때 hello VM과와 연결 된 네트워크 보안 그룹을 선택 하 고 클릭 **인바운드 보안 규칙** tooview hello 규칙 다음과 같이 합니다.

![](media/portal-use-docker/AddingEndpoint.png)

클릭 **+ 추가** tooadd 규칙 다른 hello 기본적인 경우에서 hello 끝점에 대 한 이름을 입력 합니다 (이 예제에서는 **Docker**), 및 2376 대상 ' 포트 범위 '. Hello 프로토콜 보여 주는 값을 설정 **TCP**를 클릭 하 고 **확인** toocreate hello 규칙입니다.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Docker 클라이언트 및 Azure Docker 호스트 테스트
찾아 hello 형식 클라이언트 컴퓨터의 명령줄에서 VM의 도메인의 hello 이름을 복사 `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (여기서 *dockerextension* hello로 대체 됩니다 하위 도메인 VM에 대 한)입니다.

hello 결과 유사한 toothis 같아야 합니다.

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Hello 단계를 완료 한 후 해야 구성 하는 Azure VM에서 실행 되는 모든 기능을 갖춘 Docker 호스트 toobe 다른 클라이언트에서 tooremotely 연결 합니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
준비 toogo toohello는 [Docker 사용자 가이드] Docker VM을 사용 합니다. 명령줄 인터페이스를 통해 Azure Vm에서 Docker 호스트를 만드는 tooautomate 참조 [toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux 에이전트]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[https로 Docker 실행]:http://docs.docker.com/articles/https/
[Docker 사용자 가이드]:https://docs.docker.com/userguide/
