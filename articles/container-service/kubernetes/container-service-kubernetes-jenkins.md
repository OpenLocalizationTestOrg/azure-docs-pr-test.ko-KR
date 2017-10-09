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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="c7ea3-104">Azure Container Service 및 Kubernetes로 Jenkins 통합</span><span class="sxs-lookup"><span data-stu-id="c7ea3-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="c7ea3-105">이 자습서에서는 진행 hello 프로세스 tooset 다중 컨테이너 응용 프로그램의 연속 통합을 통해 Azure hello Jenkins 플랫폼을 사용 하는 컨테이너 서비스 Kubernetes로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="c7ea3-106">hello 워크플로 hello 컨테이너 이미지 Docker 허브를 업데이트 하 고 배포 구축 하는 데 사용 하 여 hello Kubernetes 포드를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="c7ea3-107">상위 수준 프로세스</span><span class="sxs-lookup"><span data-stu-id="c7ea3-107">High level process</span></span>
<span data-ttu-id="c7ea3-108">이 문서에 자세히 설명 하는 hello 기본 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="c7ea3-109">Container Service에서 Kubernetes 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="c7ea3-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="c7ea3-110">Jenkins를 설정 하 고 액세스 tooContainer 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c7ea3-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="c7ea3-111">Jenkins 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="c7ea3-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="c7ea3-112">Hello CI/CD 프로세스 종료 tooend 테스트</span><span class="sxs-lookup"><span data-stu-id="c7ea3-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="c7ea3-113">Kubernetes 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="c7ea3-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="c7ea3-114">단계를 수행 하는 hello를 사용 하 여 Azure 컨테이너 서비스의 hello Kubernetes 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="c7ea3-115">전체 설명서는 [여기](container-service-kubernetes-walkthrough.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="c7ea3-116">1단계: 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c7ea3-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="c7ea3-117">2 단계: hello 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="c7ea3-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="c7ea3-118">hello 다음 단계 있어야 로컬 SSH 공개 키 hello ~/.ssh 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="c7ea3-119">Jenkins를 설정 하 고 액세스 tooContainer 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c7ea3-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="c7ea3-120">1단계: Jenkins 설치</span><span class="sxs-lookup"><span data-stu-id="c7ea3-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="c7ea3-121">Ubuntu 16.04 LTS로 Azure VM을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="c7ea3-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="c7ea3-122">Hello의 뒷부분에 나오는 단계 이후 됩니다 필요 사용 하 여 tooconnect toothis VM를 이용한 적 hello '인증 유형' too'SSH 공개 키 설정 로컬 컴퓨터의 '와 붙여넣기 hello SSH 공개 키를 ~/.ssh 폴더에 로컬로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="c7ea3-123">또한 주의 hello '사용자 이름' 있으므로이 사용자 이름은 필요한 tooview hello Jenkins 대시보드 및 toohello Jenkins VM 이후 단계에서 연결 하기 위해 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="c7ea3-124">다음 [지침](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)을 통해 Jenkins를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="c7ea3-125">자세한 자습서는 [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="c7ea3-126">tooview 로컬 컴퓨터의 Jenkins 대시보드 hello, 액세스 tooport 8080 허용 하는 인바운드 규칙을 추가 하 여 hello Azure 네트워크 보안 그룹 tooallow 포트 8080을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="c7ea3-127">또는 `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip` 명령을 실행하여 포트 전달을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="c7ea3-128">Tooyour Jenkins 서버 hello 브라우저를 사용 하 여 toohello 공용 IP를 이동 하 여 연결 (http:// < your_jenkins_public_ip >: 8080) 및 hello 초기 관리자 암호와 함께 처음으로 hello에 대 한 hello Jenkins 대시보드를 잠금 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="c7ea3-129">hello 관리자 암호는 hello Jenkins VM에 /var/lib/jenkins/secrets/initialAdminPassword에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="c7ea3-130">이 암호는 tooSSH에는 쉽게 tooget hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="c7ea3-131">그런 다음, `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="c7ea3-132">Docker를 통해 이러한 hello Jenkins 컴퓨터에 설치 [지침](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="c7ea3-133">Docker 명령 toobe Jenkins 작업에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="c7ea3-134">Docker 권한 tooallow Jenkins tooaccess hello Docker 끝점을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="c7ea3-135">Jenkins에 `kubectl` CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="c7ea3-136">자세한 내용은 [kubectl 설치 및 설정](https://kubernetes.io/docs/tasks/kubectl/install/)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="c7ea3-137">Jenkins 작업 'kubectl' toomanage 사용 및 toohello Kubernetes 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="c7ea3-138">2 단계: 액세스 toohello Kubernetes 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="c7ea3-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="c7ea3-139">단계를 수행 하는 여러 방법을 tooaccomplishing hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="c7ea3-140">더 쉽게 hello 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="c7ea3-141">복사 hello `kubectl` config 파일 toohello Jenkins 컴퓨터 Jenkins 작업 액세스 toohello Kubernetes 클러스터 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="c7ea3-142">이러한 지침에는 Jenkins VM hello 보다 다른 컴퓨터에서 bash를 사용 하는 및 SSH 공개 키를 로컬 컴퓨터의 hello ~/.ssh 폴더에 저장 됩니다 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="c7ea3-143">해당 hello Kubernetes Jenkins에서 유효성 검사 클러스터는 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="c7ea3-144">toodo hello Jenkins VM에이, SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="c7ea3-145">다음으로 Jenkins tooyour 클러스터에 연결할 수 있는지를 확인: `kubectl cluster-info`합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="c7ea3-146">Jenkins 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="c7ea3-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c7ea3-147">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7ea3-147">Prerequisites</span></span>

- <span data-ttu-id="c7ea3-148">코드 리포지토리용 GitHub 계정.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="c7ea3-149">Docker 허브 계정 toostore 및 update 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="c7ea3-150">다시 작성하여 업데이트할 수 있는 컨테이너화된 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="c7ea3-151">Golang으로 작성된 다음 샘플 컨테이너를 사용할 수 있습니다. https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="c7ea3-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="c7ea3-152">hello 다음 단계 수행 해야 자신의 GitHub 계정.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="c7ea3-153">리포지토리에 위에 무료 tooclone hello 생각 될 있지만 사용자 고유의 계정 tooconfigure hello webhook을 사용 해야 및 Jenkins에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="c7ea3-154">1단계: 응용 프로그램의 초기 v1 배포</span><span class="sxs-lookup"><span data-stu-id="c7ea3-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="c7ea3-155">다음 명령을 hello로 hello 개발자 컴퓨터에서 hello 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="c7ea3-156">`myrepo`를 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="c7ea3-157">이미지 tooDocker 허브를 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="c7ea3-158">Toohello Kubernetes 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="c7ea3-159">Hello 편집 `go-web.yaml` tooupdate의 파일 컨테이너 이미지 및 리 포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="c7ea3-160">2단계: Jenkins 시스템 구성</span><span class="sxs-lookup"><span data-stu-id="c7ea3-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="c7ea3-161">**Jenkins 관리** > **시스템 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="c7ea3-162">**GitHub**에서 **GitHub 서버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="c7ea3-163">**API URL**은 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="c7ea3-164">**자격 증명** 아래에서 **비밀 텍스트**를 사용하여 Jenkins 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="c7ea3-165">GitHub 사용자 계정 설정에 구성된 GitHub 개인 액세스 토큰을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="c7ea3-166">자세한 내용은 [여기](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="c7ea3-167">클릭 **연결 테스트** tooensure이 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="c7ea3-168">**전역 속성** 아래에서 환경 변수 `DOCKER_HUB`를 추가하고 Docker Hub 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="c7ea3-169">(이 데모에서는 유용하지만 프로덕션 시나리오에는 보다 안전한 방법을 사용해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="c7ea3-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="c7ea3-170">저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-170">Save.</span></span>

![Jenkins GitHub 액세스](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="c7ea3-172">3 단계: hello Jenkins 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="c7ea3-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="c7ea3-173">Jenkins 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="c7ea3-174">이름(예: "go-web")을 제공하고 **Freestyle Project**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="c7ea3-175">확인 **GitHub 프로젝트** hello URL tooyour GitHub 리포지토리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="c7ea3-176">**소스 코드 관리**, hello GitHub 리포지토리 URL과 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="c7ea3-177">추가 **빌드 단계** 형식의 **셸 실행** 사용 하 여 hello 텍스트에 따라:</span><span class="sxs-lookup"><span data-stu-id="c7ea3-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="c7ea3-178">다른 항목 추가 **빌드 단계** 형식의 **셸 실행** 사용 하 여 hello 텍스트에 따라:</span><span class="sxs-lookup"><span data-stu-id="c7ea3-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins 빌드 단계](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="c7ea3-180">Hello Jenkins 항목을 저장 하 고 있는 테스트 **이제 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="c7ea3-181">4단계: GitHub 웹후크 연결</span><span class="sxs-lookup"><span data-stu-id="c7ea3-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="c7ea3-182">만든 hello Jenkins 항목에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="c7ea3-183">**트리거 빌드** 아래에서 **GITScm 폴링에 대한 GitHub 후크 트리거** 및 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="c7ea3-184">그러면 hello GitHub webhook 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="c7ea3-185">go-web에 대한 GitHub 리포지토리에서 **설정 > 웹후크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="c7ea3-186">해당 hello Jenkins webhook URL 성공적으로 추가 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="c7ea3-187">"github webhook" hello URL을 종료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-187">hello URL should end in "github-webhook".</span></span>

![Jenkins 웹후크 구성](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="c7ea3-189">Hello CI/CD 프로세스 종료 tooend 테스트</span><span class="sxs-lookup"><span data-stu-id="c7ea3-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="c7ea3-190">Hello GitHub 리포지토리에 푸시/동기화 hello 리포지토리에 대 한 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="c7ea3-191">Hello Jenkins 콘솔에서 확인 hello **빌드 기록** 해당 hello 유효성을 검사 하 고 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="c7ea3-192">콘솔 출력 toosee 자세히 보기</span><span class="sxs-lookup"><span data-stu-id="c7ea3-192">View console output toosee details.</span></span>
3. <span data-ttu-id="c7ea3-193">Hello의 세부 정보 보기 Kubernetes에서 배포를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="c7ea3-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7ea3-194">Next steps</span></span>

- <span data-ttu-id="c7ea3-195">Azure Container Registry를 배포하고 안전한 리포지토리에 이미지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="c7ea3-196">[Azure Container Registry 문서](https://docs.microsoft.com/azure/container-registry)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="c7ea3-197">Jenkins에서 단계별 배포 및 자동화된 테스트를 포함하는 좀더 복잡한 워크플로를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="c7ea3-198">Kubernetes 및 Jenkins CI/CD에 대 한 자세한 내용은 참조 hello [Jenkins 블로그](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ea3-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
