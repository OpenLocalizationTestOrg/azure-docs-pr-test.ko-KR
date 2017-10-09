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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="9df5b-103">어떻게 toocreate Jenkins, GitHub 및 Docker를 사용 하 여 Azure에서 Linux VM의 개발 인프라</span><span class="sxs-lookup"><span data-stu-id="9df5b-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="9df5b-104">tooautomate hello 빌드 및 테스트 단계 응용 프로그램 개발의 연속 통합 및 배포 (CI/CD) 파이프라인 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="9df5b-105">이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9df5b-106">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="9df5b-107">Jenkins 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="9df5b-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="9df5b-108">GitHub 및 Jenkins 간 웹후크 통합 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="9df5b-109">GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거</span><span class="sxs-lookup"><span data-stu-id="9df5b-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="9df5b-110">앱에 대한 Docker 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="9df5b-111">새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="9df5b-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9df5b-112">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="9df5b-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9df5b-113">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9df5b-114">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="9df5b-115">Jenkins 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-115">Create Jenkins instance</span></span>
<span data-ttu-id="9df5b-116">에 대 한 이전 자습서에서 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md), 방법에 대해 배웠습니다 클라우드 init로 tooautomate VM 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="9df5b-117">이 자습서에서는 VM의 클라우드 init 파일 tooinstall Jenkins 및 Docker를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="9df5b-118">현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="9df5b-119">예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9df5b-120">입력 `sensible-editor cloud-init-jenkins.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="9df5b-121">해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="9df5b-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="9df5b-122">VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9df5b-123">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupJenkins* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="9df5b-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="9df5b-124">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9df5b-125">사용 하 여 hello `--custom-data` 클라우드 init 구성 파일에서 매개 변수 toopass 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="9df5b-126">Hello 전체 경로 너무 제공*클라우드-init-jenkins.txt* 현재 작업 디렉터리 외부의 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="9df5b-127">Hello VM toobe 생성 및 구성에 대 한 몇 가지 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="9df5b-128">tooallow 웹 트래픽 tooreach VM을 사용 하 여 [az vm-포트를 열](/cli/azure/vm#open-port) tooopen 포트 *8080* Jenkins 트래픽 및 포트에 대 한 *1337* hello Node.js 되 앱을 사용 하는 toorun 샘플 응용 프로그램에 대 한:</span><span class="sxs-lookup"><span data-stu-id="9df5b-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="9df5b-129">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="9df5b-129">Configure Jenkins</span></span>
<span data-ttu-id="9df5b-130">tooaccess Jenkins 사용자 인스턴스를 VM의 공용 IP 주소를 hello 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="9df5b-131">보안상의 이유로 Jenkins를 설치 하 여 VM toostart hello에 텍스트 파일에 저장 된 tooenter hello 초기 관리자 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="9df5b-132">Hello 이전 단계 tooSSH tooyour VM에서에서 가져온 hello 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="9df5b-133">보기 hello `initialAdminPassword` 프로그램 Jenkins를 설치 하 고 있기 때문에:</span><span class="sxs-lookup"><span data-stu-id="9df5b-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="9df5b-134">Hello 파일 아직 사용할 수 없는 경우 몇 분 정도 더 클라우드 init toocomplete hello Jenkins 및 Docker 설치 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="9df5b-135">이제 웹 브라우저를 열고 너무 이동`http://<publicIps>:8080`합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="9df5b-136">다음과 같이 hello 초기 Jenkins 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="9df5b-137">Hello 입력 *initialAdminPassword* hello 이전 단계에서 VM hello에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="9df5b-138">클릭 **tooinstall 플러그 인을 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9df5b-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="9df5b-139">검색할 *GitHub* hello 위쪽 hello 텍스트 상자에 선택 hello *GitHub 플러그*, 클릭 **설치**</span><span class="sxs-lookup"><span data-stu-id="9df5b-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="9df5b-140">원하는 대로 hello 폼 toocreate Jenkins 사용자 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="9df5b-141">보안 측면에서이 첫 번째 Jenkins 사용자 hello 기본 관리자 계정으로 계속 하는 대신 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="9df5b-142">완료되면 **Jenkins를 사용하여 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="9df5b-143">GitHub 웹후크 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-143">Create GitHub webhook</span></span>
<span data-ttu-id="9df5b-144">GitHub 열기 hello와 tooconfigure hello 통합 [Node.js Hello World 샘플 응용 프로그램](https://github.com/Azure-Samples/nodejs-docs-hello-world) hello Azure 샘플 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="9df5b-145">toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="9df5b-146">만든 hello 포크 내 webhook 만들기:</span><span class="sxs-lookup"><span data-stu-id="9df5b-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="9df5b-147">클릭 **설정**을 선택한 후 **통합 및 서비스** hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="9df5b-148">**서비스 추가**를 클릭한 다음, 필터 상자에 *Jenkins*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="9df5b-149">*Jenkins(GitHub 플러그 인)*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="9df5b-150">Hello에 대 한 **Jenkins 연결 URL**, 입력 `http://<publicIps>:8080/github-webhook/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="9df5b-151">Hello 후행를 포함 해야 /</span><span class="sxs-lookup"><span data-stu-id="9df5b-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="9df5b-152">**서비스 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-152">Click **Add service**</span></span>

![GitHub webhook tooyour 분기 리포지토리를 추가 합니다.](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="9df5b-154">Jenkins 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-154">Create Jenkins job</span></span>
<span data-ttu-id="9df5b-155">toohave Jenkins 응답 tooan 이벤트 GitHub에서 코드를 커밋 예: Jenkins 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="9df5b-156">Jenkins 웹 사이트의 클릭 **새 작업을 만들** hello 홈 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="9df5b-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="9df5b-157">*HelloWorld*를 작업 이름으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="9df5b-158">**프리스타일 프로젝트**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="9df5b-159">Hello에서 **일반** 섹션에서 **GitHub** 프로젝트와 같은 분기 리포지토리 URL을 입력 *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="9df5b-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="9df5b-160">Hello에서 **소스 코드 관리** 섹션에서 **Git**, 분기 리 포 입력 *.git* URL와 같은 *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="9df5b-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="9df5b-161">Hello에서 **빌드 트리거** 섹션에서 **GITscm 폴링에 대 한 GitHub 후크 트리거**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="9df5b-162">Hello에서 **빌드** 섹션에서 선택 **추가 빌드 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="9df5b-163">선택 **셸 실행**, 입력 한 다음 `echo "Testing"` toocommand 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="9df5b-164">클릭 **저장** hello hello 작업 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="9df5b-165">GitHub 통합 테스트</span><span class="sxs-lookup"><span data-stu-id="9df5b-165">Test GitHub integration</span></span>
<span data-ttu-id="9df5b-166">tootest hello Jenkins와 GitHub 통합에는 포크에 변경을 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="9df5b-167">GitHub에 웹 UI 분기 리 포 선택한 hello 클릭 **index.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="9df5b-168">6 행의 내용이 있으므로 hello 연필 아이콘 tooedit이이 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="9df5b-169">toocommit 변경 내용을 클릭 hello **변경 내용 커밋** hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="9df5b-170">Jenkins, 새 빌드는 hello에서 시작 **기록 빌드** hello 왼쪽 아래 모서리의 작업 페이지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="9df5b-171">Hello 빌드 번호 링크를 클릭 하는 선택 **콘솔 출력이** hello 왼쪽 크기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="9df5b-172">GitHub 및 hello 빌드 작업 출력 hello 메시지에서 로드 되는 사용자 코드 처럼 Jenkins를 사용 하는 hello 단계를 확인할 수 `Testing` toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="9df5b-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="9df5b-173">GitHub에서 커밋 이루어집니다 때마다 hello webhook tooJenkins 아웃에 도달 하 고 이러한 방식으로 새 빌드를 트리거.</span><span class="sxs-lookup"><span data-stu-id="9df5b-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="9df5b-174">Docker 빌드 이미지 정의</span><span class="sxs-lookup"><span data-stu-id="9df5b-174">Define Docker build image</span></span>
<span data-ttu-id="9df5b-175">여 GitHub 커밋에 따라 실행 하는 toosee hello Node.js 응용은 Docker 이미지 toorun hello 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="9df5b-176">hello 이미지 tooconfigure hello 응용 프로그램을 실행 하는 컨테이너를 hello 하는 방법을 정의 하는 Dockerfile에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="9df5b-177">Hello SSH 연결 tooyour VM에서에서 이전 단계에서 만든 hello 작업의 이름을 딴 toohello Jenkins 작업 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="9df5b-178">이 예제에서 *HelloWorld*라고 명명되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="9df5b-179">이 작업 영역 디렉터리에 있는으로 파일 만들기 `sudo sensible-editor Dockerfile` 붙여넣기 hello 내용에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="9df5b-180">전체 Dockerfile은 해당 hello hello 첫 번째 줄 특히 제대로 복사 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="9df5b-181">이 Dockerfile Alpine Linux를 사용 하 여 hello 기본 Node.js 이미지를 사용 하 여, 앱 Hello World hello 노출 포트 1337 실행 되 다음 hello 응용 프로그램 파일을 복사 하 여 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="9df5b-182">Jenkins 빌드 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-182">Create Jenkins build rules</span></span>
<span data-ttu-id="9df5b-183">이전 단계에서 기본 Jenkins 빌드 규칙 메시지 toohello 콘솔 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="9df5b-184">Hello 빌드 단계 toouse 우리의 Dockerfile을 만들고 hello 앱 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="9df5b-185">Jenkins 인스턴스를 다시에 이전 단계에서 만든 hello 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="9df5b-186">클릭 **구성** hello 왼쪽 및 toohello 아래로 스크롤하여 **빌드** 섹션:</span><span class="sxs-lookup"><span data-stu-id="9df5b-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="9df5b-187">기존 `echo "Test"` 빌드 단계를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="9df5b-188">Hello 오른쪽 위의 hello 기존 빌드 단계 상자에 크로스 빨간색 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="9df5b-189">**빌드 단계 추가**를 클릭한 다음, **셸 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="9df5b-190">Hello에 **명령** 상자 hello 다음 Docker 명령을 입력 한 다음 선택 **저장**:</span><span class="sxs-lookup"><span data-stu-id="9df5b-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="9df5b-191">hello Docker 빌드 단계 이미지와 이미지의 기록을 유지할 수 있도록 사용 하 여 hello Jenkins 빌드 번호는 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="9df5b-192">Hello 앱을 실행 하는 모든 기존 컨테이너를 중지 했다가 다음 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="9df5b-193">새 컨테이너는 hello 이미지를 사용 하 여 시작 하 고 hello GitHub에서 최신 커밋에 따라 Node.js 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="9df5b-194">파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="9df5b-194">Test your pipeline</span></span>
<span data-ttu-id="9df5b-195">작업에서 toosee hello 전체 파이프라인 편집 hello *index.js* 분기 GitHub 리포지토리에에서 다시 파일을 클릭 하 여 **변경 내용을 커밋합니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="9df5b-196">Jenkins hello webhook GitHub에 대 한 기준에 새 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="9df5b-197">몇 초 정도 toocreate hello Docker 이미지를 사용 하 고 새 컨테이너에 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="9df5b-198">필요한 경우 다시 hello VM의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="9df5b-199">웹 브라우저를 열고 `http://<publicIps>:1337`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="9df5b-200">Node.js 앱 표시 되 고 다음과 같이 hello 최신 커밋 GitHub 포크에 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="9df5b-202">이제 다른 편집 toohello 확인 *index.js* GitHub 및 커밋 hello 변경에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="9df5b-203">Jenkins에서 작업 toocomplete hello에 대 한 몇 초 후 다음과 같이 새 컨테이너에서 실행 되는 앱의 웹 브라우저 toosee hello 업데이트 버전을 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![다른 GitHub 커밋 후 Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="9df5b-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9df5b-205">Next steps</span></span>
<span data-ttu-id="9df5b-206">이 자습서에서는 각 코드 커밋에 GitHub toorun Jenkins 빌드 작업을 구성을 다음 Docker 컨테이너 tootest 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="9df5b-207">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9df5b-208">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="9df5b-209">Jenkins 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="9df5b-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="9df5b-210">GitHub 및 Jenkins 간 웹후크 통합 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="9df5b-211">GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거</span><span class="sxs-lookup"><span data-stu-id="9df5b-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="9df5b-212">앱에 대한 Docker 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9df5b-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="9df5b-213">새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="9df5b-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="9df5b-214">다음 자습서 toolearn toohello을 이동 하는 방법에 대 한 자세한 toointegrate Jenkins Visual Studio Team Services를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df5b-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9df5b-215">Jenkins 및 Team Services를 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="9df5b-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)