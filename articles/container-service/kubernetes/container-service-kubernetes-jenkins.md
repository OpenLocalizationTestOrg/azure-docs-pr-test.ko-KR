---
title: "Azure 컨테이너 서비스의 Kubernetes와 CI/CD aaaJenkins | Microsoft Docs"
description: "CI/CD tooautomate Jenkins toodeploy 및 업그레이드는 컨테이너 화 된 응용 프로그램에 액세스 Kubernetes Azure 컨테이너 서비스에서 처리 하는 방법"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, 컨테이너, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Azure Container Service 및 Kubernetes로 Jenkins 통합 
이 자습서에서는 진행 hello 프로세스 tooset 다중 컨테이너 응용 프로그램의 연속 통합을 통해 Azure hello Jenkins 플랫폼을 사용 하는 컨테이너 서비스 Kubernetes로 합니다. hello 워크플로 hello 컨테이너 이미지 Docker 허브를 업데이트 하 고 배포 구축 하는 데 사용 하 여 hello Kubernetes 포드를 업그레이드 합니다. 

## <a name="high-level-process"></a>상위 수준 프로세스
이 문서에 자세히 설명 하는 hello 기본 단계입니다. 
- Container Service에서 Kubernetes 클러스터 설치
- Jenkins를 설정 하 고 액세스 tooContainer 서비스 구성
- Jenkins 워크플로 만들기
- Hello CI/CD 프로세스 종료 tooend 테스트

## <a name="install-a-kubernetes-cluster"></a>Kubernetes 클러스터 설치
    
단계를 수행 하는 hello를 사용 하 여 Azure 컨테이너 서비스의 hello Kubernetes 클러스터를 배포 합니다. 전체 설명서는 [여기](container-service-kubernetes-walkthrough.md)에 있습니다.

### <a name="step-1-create-a-resource-group"></a>1단계: 리소스 그룹 만들기
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>2 단계: hello 클러스터 배포
> [!NOTE]
> hello 다음 단계 있어야 로컬 SSH 공개 키 hello ~/.ssh 폴더에 저장 합니다.
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Jenkins를 설정 하 고 액세스 tooContainer 서비스 구성

### <a name="step-1-install-jenkins"></a>1단계: Jenkins 설치
1. Ubuntu 16.04 LTS로 Azure VM을 만듭니다  Hello의 뒷부분에 나오는 단계 이후 됩니다 필요 사용 하 여 tooconnect toothis VM를 이용한 적 hello '인증 유형' too'SSH 공개 키 설정 로컬 컴퓨터의 '와 붙여넣기 hello SSH 공개 키를 ~/.ssh 폴더에 로컬로 저장 됩니다.  또한 주의 hello '사용자 이름' 있으므로이 사용자 이름은 필요한 tooview hello Jenkins 대시보드 및 toohello Jenkins VM 이후 단계에서 연결 하기 위해 지정 해야 합니다.
2. 다음 [지침](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)을 통해 Jenkins를 설치합니다. 자세한 자습서는 [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04)에 있습니다.
3. tooview 로컬 컴퓨터의 Jenkins 대시보드 hello, 액세스 tooport 8080 허용 하는 인바운드 규칙을 추가 하 여 hello Azure 네트워크 보안 그룹 tooallow 포트 8080을 업데이트 합니다.  또는 `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip` 명령을 실행하여 포트 전달을 설정할 수 있습니다.
4. Tooyour Jenkins 서버 hello 브라우저를 사용 하 여 toohello 공용 IP를 이동 하 여 연결 (http:// < your_jenkins_public_ip >: 8080) 및 hello 초기 관리자 암호와 함께 처음으로 hello에 대 한 hello Jenkins 대시보드를 잠금 해제 합니다.  hello 관리자 암호는 hello Jenkins VM에 /var/lib/jenkins/secrets/initialAdminPassword에 저장 됩니다.  이 암호는 tooSSH에는 쉽게 tooget hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`합니다.  그런 다음, `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`를 실행합니다.
5. Docker를 통해 이러한 hello Jenkins 컴퓨터에 설치 [지침](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts)합니다. Docker 명령 toobe Jenkins 작업에서 실행할 수 있습니다.
6. Docker 권한 tooallow Jenkins tooaccess hello Docker 끝점을 구성 합니다.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Jenkins에 `kubectl` CLI를 설치합니다. 자세한 내용은 [kubectl 설치 및 설정](https://kubernetes.io/docs/tasks/kubectl/install/)에 나와 있습니다.  Jenkins 작업 'kubectl' toomanage 사용 및 toohello Kubernetes 클러스터를 배포 합니다.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>2 단계: 액세스 toohello Kubernetes 클러스터 설정

> [!NOTE]
> 단계를 수행 하는 여러 방법을 tooaccomplishing hello 있습니다. 더 쉽게 hello 방법을 사용 합니다.
>

1. 복사 hello `kubectl` config 파일 toohello Jenkins 컴퓨터 Jenkins 작업 액세스 toohello Kubernetes 클러스터 갖도록 합니다. 이러한 지침에는 Jenkins VM hello 보다 다른 컴퓨터에서 bash를 사용 하는 및 SSH 공개 키를 로컬 컴퓨터의 hello ~/.ssh 폴더에 저장 됩니다 가정 합니다.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. 해당 hello Kubernetes Jenkins에서 유효성 검사 클러스터는 액세스할 수 있습니다.  toodo hello Jenkins VM에이, SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`합니다.  다음으로 Jenkins tooyour 클러스터에 연결할 수 있는지를 확인: `kubectl cluster-info`합니다.
    

## <a name="create-a-jenkins-workflow"></a>Jenkins 워크플로 만들기

### <a name="prerequisites"></a>필수 조건

- 코드 리포지토리용 GitHub 계정.
- Docker 허브 계정 toostore 및 update 이미지입니다.
- 다시 작성하여 업데이트할 수 있는 컨테이너화된 응용 프로그램. Golang으로 작성된 다음 샘플 컨테이너를 사용할 수 있습니다. https://github.com/chzbrgr71/go-web 

> [!NOTE]
> hello 다음 단계 수행 해야 자신의 GitHub 계정. 리포지토리에 위에 무료 tooclone hello 생각 될 있지만 사용자 고유의 계정 tooconfigure hello webhook을 사용 해야 및 Jenkins에 액세스 합니다.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>1단계: 응용 프로그램의 초기 v1 배포
1. 다음 명령을 hello로 hello 개발자 컴퓨터에서 hello 응용 프로그램을 빌드하십시오. `myrepo`를 사용자 고유의 값으로 바꿉니다.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. 이미지 tooDocker 허브를 푸시하십시오.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Toohello Kubernetes 클러스터를 배포 합니다.
    
    > [!NOTE] 
    > Hello 편집 `go-web.yaml` tooupdate의 파일 컨테이너 이미지 및 리 포 합니다.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>2단계: Jenkins 시스템 구성
1. **Jenkins 관리** > **시스템 구성**을 클릭합니다.
2. **GitHub**에서 **GitHub 서버 추가**를 선택합니다.
3. **API URL**은 기본값으로 둡니다.
4. **자격 증명** 아래에서 **비밀 텍스트**를 사용하여 Jenkins 자격 증명을 추가합니다. GitHub 사용자 계정 설정에 구성된 GitHub 개인 액세스 토큰을 사용하는 것이 좋습니다. 자세한 내용은 [여기](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)에 있습니다.
5. 클릭 **연결 테스트** tooensure이 올바르게 구성 되어 있습니다.
6. **전역 속성** 아래에서 환경 변수 `DOCKER_HUB`를 추가하고 Docker Hub 암호를 제공합니다. (이 데모에서는 유용하지만 프로덕션 시나리오에는 보다 안전한 방법을 사용해야 합니다.)
7. 저장합니다.

![Jenkins GitHub 액세스](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>3 단계: hello Jenkins 워크플로 만들기
1. Jenkins 항목을 만듭니다.
2. 이름(예: "go-web")을 제공하고 **Freestyle Project**를 선택합니다. 
3. 확인 **GitHub 프로젝트** hello URL tooyour GitHub 리포지토리를 제공 합니다.
4. **소스 코드 관리**, hello GitHub 리포지토리 URL과 자격 증명을 제공 합니다. 
5. 추가 **빌드 단계** 형식의 **셸 실행** 사용 하 여 hello 텍스트에 따라:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. 다른 항목 추가 **빌드 단계** 형식의 **셸 실행** 사용 하 여 hello 텍스트에 따라:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins 빌드 단계](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Hello Jenkins 항목을 저장 하 고 있는 테스트 **이제 빌드**합니다.

### <a name="step-4-connect-github-webhook"></a>4단계: GitHub 웹후크 연결
1. 만든 hello Jenkins 항목에서 클릭 **구성**합니다.
2. **트리거 빌드** 아래에서 **GITScm 폴링에 대한 GitHub 후크 트리거** 및 **저장**을 선택합니다. 그러면 hello GitHub webhook 자동으로 구성 됩니다.
3. go-web에 대한 GitHub 리포지토리에서 **설정 > 웹후크**를 클릭합니다.
4. 해당 hello Jenkins webhook URL 성공적으로 추가 확인 합니다. "github webhook" hello URL을 종료 해야 합니다.

![Jenkins 웹후크 구성](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Hello CI/CD 프로세스 종료 tooend 테스트

1. Hello GitHub 리포지토리에 푸시/동기화 hello 리포지토리에 대 한 코드를 업데이트 합니다.
2. Hello Jenkins 콘솔에서 확인 hello **빌드 기록** 해당 hello 유효성을 검사 하 고 작업을 실행 합니다. 콘솔 출력 toosee 자세히 보기
3. Hello의 세부 정보 보기 Kubernetes에서 배포를 업그레이드 합니다.

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>다음 단계

- Azure Container Registry를 배포하고 안전한 리포지토리에 이미지를 저장합니다. [Azure Container Registry 문서](https://docs.microsoft.com/azure/container-registry)를 참조하세요.
- Jenkins에서 단계별 배포 및 자동화된 테스트를 포함하는 좀더 복잡한 워크플로를 빌드합니다.
- Kubernetes 및 Jenkins CI/CD에 대 한 자세한 내용은 참조 hello [Jenkins 블로그](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/)합니다.
