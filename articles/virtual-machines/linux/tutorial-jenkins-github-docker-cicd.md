---
title: "Jenkins 사용 하 여 Azure에서 개발 파이프라인 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate는 Jenkins 가상 컴퓨터 각 코드에 GitHub에서 끌어오는 소스 커밋하고 새 Docker 컨테이너 toorun 작성 하는 Azure에서 응용 프로그램에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>어떻게 toocreate Jenkins, GitHub 및 Docker를 사용 하 여 Azure에서 Linux VM의 개발 인프라
tooautomate hello 빌드 및 테스트 단계 응용 프로그램 개발의 연속 통합 및 배포 (CI/CD) 파이프라인 사용할 수 있습니다. 이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.

> [!div class="checklist"]
> * Jenkins VM 만들기
> * Jenkins 설치 및 구성
> * GitHub 및 Jenkins 간 웹후크 통합 만들기
> * GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거
> * 앱에 대한 Docker 이미지 만들기
> * 새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-jenkins-instance"></a>Jenkins 인스턴스 만들기
에 대 한 이전 자습서에서 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md), 방법에 대해 배웠습니다 클라우드 init로 tooautomate VM 사용자 지정 합니다. 이 자습서에서는 VM의 클라우드 init 파일 tooinstall Jenkins 및 Docker를 사용 합니다. 

현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다. 예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다. 입력 `sensible-editor cloud-init-jenkins.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다. 해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupJenkins* hello에 *eastus* 위치:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다. 사용 하 여 hello `--custom-data` 클라우드 init 구성 파일에서 매개 변수 toopass 합니다. Hello 전체 경로 너무 제공*클라우드-init-jenkins.txt* 현재 작업 디렉터리 외부의 hello 파일을 저장 합니다.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Hello VM toobe 생성 및 구성에 대 한 몇 가지 분 걸립니다.

tooallow 웹 트래픽 tooreach VM을 사용 하 여 [az vm-포트를 열](/cli/azure/vm#open-port) tooopen 포트 *8080* Jenkins 트래픽 및 포트에 대 한 *1337* hello Node.js 되 앱을 사용 하는 toorun 샘플 응용 프로그램에 대 한:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Jenkins 구성
tooaccess Jenkins 사용자 인스턴스를 VM의 공용 IP 주소를 hello 가져옵니다.

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

보안상의 이유로 Jenkins를 설치 하 여 VM toostart hello에 텍스트 파일에 저장 된 tooenter hello 초기 관리자 암호가 필요 합니다. Hello 이전 단계 tooSSH tooyour VM에서에서 가져온 hello 공용 IP 주소를 사용 합니다.

```bash
ssh azureuser@<publicIps>
```

보기 hello `initialAdminPassword` 프로그램 Jenkins를 설치 하 고 있기 때문에:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Hello 파일 아직 사용할 수 없는 경우 몇 분 정도 더 클라우드 init toocomplete hello Jenkins 및 Docker 설치 대기 합니다.

이제 웹 브라우저를 열고 너무 이동`http://<publicIps>:8080`합니다. 다음과 같이 hello 초기 Jenkins 설치를 완료 합니다.

- Hello 입력 *initialAdminPassword* hello 이전 단계에서 VM hello에서 가져옵니다.
- 클릭 **tooinstall 플러그 인을 선택 합니다.**
- 검색할 *GitHub* hello 위쪽 hello 텍스트 상자에 선택 hello *GitHub 플러그*, 클릭 **설치**
- 원하는 대로 hello 폼 toocreate Jenkins 사용자 계정을 입력 합니다. 보안 측면에서이 첫 번째 Jenkins 사용자 hello 기본 관리자 계정으로 계속 하는 대신 만들어야 합니다.
- 완료되면 **Jenkins를 사용하여 시작**을 클릭합니다.


## <a name="create-github-webhook"></a>GitHub 웹후크 만들기
GitHub 열기 hello와 tooconfigure hello 통합 [Node.js Hello World 샘플 응용 프로그램](https://github.com/Azure-Samples/nodejs-docs-hello-world) hello Azure 샘플 리포지토리에서 합니다. toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.

만든 hello 포크 내 webhook 만들기:

- 클릭 **설정**을 선택한 후 **통합 및 서비스** hello 왼쪽에 있습니다.
- **서비스 추가**를 클릭한 다음, 필터 상자에 *Jenkins*를 입력합니다.
- *Jenkins(GitHub 플러그 인)*를 선택합니다.
- Hello에 대 한 **Jenkins 연결 URL**, 입력 `http://<publicIps>:8080/github-webhook/`합니다. Hello 후행를 포함 해야 /
- **서비스 추가**를 클릭합니다.

![GitHub webhook tooyour 분기 리포지토리를 추가 합니다.](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Jenkins 작업 만들기
toohave Jenkins 응답 tooan 이벤트 GitHub에서 코드를 커밋 예: Jenkins 작업을 만듭니다. 

Jenkins 웹 사이트의 클릭 **새 작업을 만들** hello 홈 페이지에서:

- *HelloWorld*를 작업 이름으로 입력합니다. **프리스타일 프로젝트**를 선택한 다음 **확인**을 선택합니다.
- Hello에서 **일반** 섹션에서 **GitHub** 프로젝트와 같은 분기 리포지토리 URL을 입력 *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Hello에서 **소스 코드 관리** 섹션에서 **Git**, 분기 리 포 입력 *.git* URL와 같은 *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Hello에서 **빌드 트리거** 섹션에서 **GITscm 폴링에 대 한 GitHub 후크 트리거**합니다.
- Hello에서 **빌드** 섹션에서 선택 **추가 빌드 단계**합니다. 선택 **셸 실행**, 입력 한 다음 `echo "Testing"` toocommand 창에 있습니다.
- 클릭 **저장** hello hello 작업 창 맨 아래에 있습니다.


## <a name="test-github-integration"></a>GitHub 통합 테스트
tootest hello Jenkins와 GitHub 통합에는 포크에 변경을 내용을 커밋합니다. 

GitHub에 웹 UI 분기 리 포 선택한 hello 클릭 **index.js** 파일입니다. 6 행의 내용이 있으므로 hello 연필 아이콘 tooedit이이 파일을 클릭 합니다.

```nodejs
response.end("Hello World!");
```

toocommit 변경 내용을 클릭 hello **변경 내용 커밋** hello 아래쪽 단추입니다.

Jenkins, 새 빌드는 hello에서 시작 **기록 빌드** hello 왼쪽 아래 모서리의 작업 페이지의 섹션입니다. Hello 빌드 번호 링크를 클릭 하는 선택 **콘솔 출력이** hello 왼쪽 크기에 있습니다. GitHub 및 hello 빌드 작업 출력 hello 메시지에서 로드 되는 사용자 코드 처럼 Jenkins를 사용 하는 hello 단계를 확인할 수 `Testing` toohello 콘솔. GitHub에서 커밋 이루어집니다 때마다 hello webhook tooJenkins 아웃에 도달 하 고 이러한 방식으로 새 빌드를 트리거.


## <a name="define-docker-build-image"></a>Docker 빌드 이미지 정의
여 GitHub 커밋에 따라 실행 하는 toosee hello Node.js 응용은 Docker 이미지 toorun hello 앱을 빌드할 수 있습니다. hello 이미지 tooconfigure hello 응용 프로그램을 실행 하는 컨테이너를 hello 하는 방법을 정의 하는 Dockerfile에서 만들어집니다. 

Hello SSH 연결 tooyour VM에서에서 이전 단계에서 만든 hello 작업의 이름을 딴 toohello Jenkins 작업 디렉터리를 변경 합니다. 이 예제에서 *HelloWorld*라고 명명되었습니다.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

이 작업 영역 디렉터리에 있는으로 파일 만들기 `sudo sensible-editor Dockerfile` 붙여넣기 hello 내용에 따라 합니다. 전체 Dockerfile은 해당 hello hello 첫 번째 줄 특히 제대로 복사 되었는지 확인 합니다.

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

이 Dockerfile Alpine Linux를 사용 하 여 hello 기본 Node.js 이미지를 사용 하 여, 앱 Hello World hello 노출 포트 1337 실행 되 다음 hello 응용 프로그램 파일을 복사 하 여 초기화 합니다.


## <a name="create-jenkins-build-rules"></a>Jenkins 빌드 규칙 만들기
이전 단계에서 기본 Jenkins 빌드 규칙 메시지 toohello 콘솔 출력을 생성 합니다. Hello 빌드 단계 toouse 우리의 Dockerfile을 만들고 hello 앱 실행 수 있습니다.

Jenkins 인스턴스를 다시에 이전 단계에서 만든 hello 작업을 선택 합니다. 클릭 **구성** hello 왼쪽 및 toohello 아래로 스크롤하여 **빌드** 섹션:

- 기존 `echo "Test"` 빌드 단계를 제거합니다. Hello 오른쪽 위의 hello 기존 빌드 단계 상자에 크로스 빨간색 hello를 클릭 합니다.
- **빌드 단계 추가**를 클릭한 다음, **셸 실행**을 선택합니다.
- Hello에 **명령** 상자 hello 다음 Docker 명령을 입력 한 다음 선택 **저장**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

hello Docker 빌드 단계 이미지와 이미지의 기록을 유지할 수 있도록 사용 하 여 hello Jenkins 빌드 번호는 태그를 만듭니다. Hello 앱을 실행 하는 모든 기존 컨테이너를 중지 했다가 다음 제거 합니다. 새 컨테이너는 hello 이미지를 사용 하 여 시작 하 고 hello GitHub에서 최신 커밋에 따라 Node.js 응용 프로그램을 실행 합니다.


## <a name="test-your-pipeline"></a>파이프라인 테스트
작업에서 toosee hello 전체 파이프라인 편집 hello *index.js* 분기 GitHub 리포지토리에에서 다시 파일을 클릭 하 여 **변경 내용을 커밋합니다**합니다. Jenkins hello webhook GitHub에 대 한 기준에 새 작업을 시작 합니다. 몇 초 정도 toocreate hello Docker 이미지를 사용 하 고 새 컨테이너에 앱을 시작 합니다.

필요한 경우 다시 hello VM의 공용 IP 주소를 가져옵니다.

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

웹 브라우저를 열고 `http://<publicIps>:1337`을 입력합니다. Node.js 앱 표시 되 고 다음과 같이 hello 최신 커밋 GitHub 포크에 반영 합니다.

![Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

이제 다른 편집 toohello 확인 *index.js* GitHub 및 커밋 hello 변경에는 파일입니다. Jenkins에서 작업 toocomplete hello에 대 한 몇 초 후 다음과 같이 새 컨테이너에서 실행 되는 앱의 웹 브라우저 toosee hello 업데이트 버전을 새로 고침 합니다.

![다른 GitHub 커밋 후 Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 각 코드 커밋에 GitHub toorun Jenkins 빌드 작업을 구성을 다음 Docker 컨테이너 tootest 앱을 배포 합니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Jenkins VM 만들기
> * Jenkins 설치 및 구성
> * GitHub 및 Jenkins 간 웹후크 통합 만들기
> * GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거
> * 앱에 대한 Docker 이미지 만들기
> * 새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인

다음 자습서 toolearn toohello을 이동 하는 방법에 대 한 자세한 toointegrate Jenkins Visual Studio Team Services를 사용 합니다.

> [!div class="nextstepaction"]
> [Jenkins 및 Team Services를 사용하여 앱 배포](tutorial-build-deploy-jenkins.md)