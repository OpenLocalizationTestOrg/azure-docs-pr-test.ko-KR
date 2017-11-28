---
title: "Azure에서 Jenkins를 사용하여 개발 파이프라인 만들기 | Microsoft Docs"
description: "각 코드 커밋의 GitHub에서 가져오고 앱을 실행하기 위해 새 Docker 컨테이너를 빌드하는 Azure에서 Jenkins 가상 컴퓨터를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="18df9-103">Jenkins, GitHub 및 Docker를 사용하여 Azure에서 Linux VM의 개발 인프라를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="18df9-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="18df9-104">응용 프로그램 개발의 빌드 및 테스트 단계를 자동화하려면 CI/CD(연속 통합 및 배포) 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="18df9-105">이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18df9-106">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="18df9-107">Jenkins 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="18df9-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="18df9-108">GitHub 및 Jenkins 간 웹후크 통합 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="18df9-109">GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거</span><span class="sxs-lookup"><span data-stu-id="18df9-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="18df9-110">앱에 대한 Docker 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="18df9-111">새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="18df9-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="18df9-112">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="18df9-113">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="18df9-114">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df9-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="18df9-115">Jenkins 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-115">Create Jenkins instance</span></span>
<span data-ttu-id="18df9-116">[처음 부팅 시 Linux 가상 컴퓨터를 사용자 지정하는 방법](tutorial-automate-vm-deployment.md)에 대한 이전 자습서에서 cloud-init를 사용하여 VM 사용자 지정을 자동화하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="18df9-117">이 자습서는 cloud-init 파일을 사용하여 VM에 Jenkins 및 Docker를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="18df9-118">현재 셸에서 *cloud-init.txt*라는 파일을 만들고 다음 구성을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="18df9-119">예를 들어 로컬 컴퓨터에 없는 Cloud Shell에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="18df9-120">`sensible-editor cloud-init-jenkins.txt`를 입력하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="18df9-121">전체 cloud-init 파일, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="18df9-122">VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="18df9-123">다음 예제에서는 *eastus* 위치에 *myResourceGroupJenkins*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="18df9-124">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="18df9-125">`--custom-data` 매개 변수를 사용하여 cloud-init 구성 파일을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="18df9-126">현재 작업 디렉터리 외부에 파일을 저장한 경우 *cloud-init-jenkins.txt*에 전체 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="18df9-127">VM을 만들고 구성하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="18df9-128">웹 트래픽이 VM에 연결되도록 허용하려면 [az vm open-port](/cli/azure/vm#open-port)를 사용하여 샘플 앱을 실행하는 데 사용되는 Jenkins 트래픽에 대한 포트 *8080* 및 Node.js 앱에 대한 포트 *1337*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="18df9-129">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="18df9-129">Configure Jenkins</span></span>
<span data-ttu-id="18df9-130">Jenkins 인스턴스에 액세스하려면 VM의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="18df9-131">보안을 위해 VM에서 텍스트 파일로 저장된 초기 관리자 암호를 입력하여 Jenkins 설치를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="18df9-132">이전 단계에서 가져온 공용 IP 주소를 사용하여 VM에 SSH를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="18df9-133">Jenkins 설치를 위해 `initialAdminPassword`를 보고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="18df9-134">파일을 아직 사용할 수 없는 경우 cloud-init이 Jenkins 및 Docker 설치를 완료할 때까지 몇 분 더 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="18df9-135">이제 웹 브라우저를 열고 `http://<publicIps>:8080`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="18df9-136">다음과 같이 초기 Jenkins 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="18df9-137">이전 단계에서 VM에서 가져온 *initialAdminPassword*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="18df9-138">**설치할 플러그 인 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="18df9-139">맨 위에 있는 텍스트 상자에서 *GitHub*를 검색하고 *GitHub 플러그 인*을 선택한 다음, **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="18df9-140">Jenkins 사용자 계정을 만들려면 원하는 대로 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="18df9-141">보안 관점에서 기본 관리자 계정으로 계속 진행하지 않고 이 첫 번째 Jenkins 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="18df9-142">완료되면 **Jenkins를 사용하여 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="18df9-143">GitHub 웹후크 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-143">Create GitHub webhook</span></span>
<span data-ttu-id="18df9-144">GitHub를 통해 통합을 구성하려면 Azure 샘플 리포지토리에서 [Node.js 헬로 월드 샘플 앱](https://github.com/Azure-Samples/nodejs-docs-hello-world)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="18df9-145">사용자 고유의 GitHub 계정에 리포지토리를 분기하려면 오른쪽 위 모서리에 있는 **분기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="18df9-146">만든 분기 내부에 웹후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="18df9-147">**설정**을 클릭한 다음 왼쪽에 있는 **통합 및 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="18df9-148">**서비스 추가**를 클릭한 다음, 필터 상자에 *Jenkins*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="18df9-149">*Jenkins(GitHub 플러그 인)*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="18df9-150">**Jenkins 후크 URL**의 경우 `http://<publicIps>:8080/github-webhook/`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="18df9-151">후행 슬래시(/)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="18df9-152">**서비스 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-152">Click **Add service**</span></span>

![분기된 리포지토리에 GitHub 웹후크 추가](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="18df9-154">Jenkins 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-154">Create Jenkins job</span></span>
<span data-ttu-id="18df9-155">코드 커밋과 같은 GitHub의 이벤트에 대해 Jenkins가 응답하도록 하려면 Jenkins 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="18df9-156">Jenkins 웹 사이트에서 홈 페이지에서 **새 작업 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="18df9-157">*HelloWorld*를 작업 이름으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="18df9-158">**프리스타일 프로젝트**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="18df9-159">**일반** 섹션에서 **GitHub** 프로젝트를 선택하고 *https://github.com/iainfoulds/nodejs-docs-hello-world*와 같은 분기된 리포지토리 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="18df9-160">**원본 코드 관리** 섹션에서 **Git**을 선택하고 *https://github.com/iainfoulds/nodejs-docs-hello-world.git*과 같은 분기된 리포지토리 *.git* URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="18df9-161">**트리거 빌드**에서 **GITscm 폴링에 대한 GitHub 후크 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="18df9-162">**빌드** 섹션 아래에서 **빌드 단계 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="18df9-163">**셸 실행**을 선택한 다음, `echo "Testing"`을 명령 창에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="18df9-164">작업 창 맨 아래에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="18df9-165">GitHub 통합 테스트</span><span class="sxs-lookup"><span data-stu-id="18df9-165">Test GitHub integration</span></span>
<span data-ttu-id="18df9-166">Jenkins와 GitHub의 통합을 테스트하려면 사용자 분기의 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="18df9-167">GitHub 웹 UI로 돌아가서 분기된 리포지토리를 선택한 다음, **index.js** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="18df9-168">연필 아이콘을 클릭하여 이 파일을 편집하면 6번 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="18df9-169">변경 사항을 커밋하려면 맨 아래쪽에 **변경 내용 커밋** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="18df9-170">Jenkins에서 작업 페이지의 왼쪽 아래 모서리에 있는 **기록 빌드** 섹션에서 새 빌드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="18df9-171">빌드 번호 링크를 클릭하고 왼쪽 크기에 있는 **콘솔 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="18df9-172">코드가 GitHub에서 로드되면 Jenkins가 수행하는 단계와 콘솔에 메시지 `Testing`을 출력하는 빌드 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="18df9-173">GitHub에서 커밋이 수행될 때마다 웹후크는 Jenkins에 도달하며, 이 방법으로 새 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="18df9-174">Docker 빌드 이미지 정의</span><span class="sxs-lookup"><span data-stu-id="18df9-174">Define Docker build image</span></span>
<span data-ttu-id="18df9-175">GitHub 커밋에 기반하여 실행되는 Node.js 앱을 확인하려면 Docker 이미지를 빌드하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="18df9-176">이미지는 앱을 실행하는 컨테이너를 구성하는 방법을 정의하는 Dockerfile에서 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="18df9-177">SSH 연결부터 VM까지 이전 단계에서 만든 작업 이후에 명명된 Jenkins 작업 영역 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="18df9-178">이 예제에서 *HelloWorld*라고 명명되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="18df9-179">이 작업 영역 디렉터리에 `sudo sensible-editor Dockerfile`이라는 파일을 만들고 다음 콘텐츠를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="18df9-180">전체 Dockerfile, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="18df9-181">이 Dockerfile은 Alpine Linux를 사용하는 기본 Node.js 이미지를 사용하며, 헬로 월드 앱이 실행되는 포트 1337을 노출한 다음, 앱 파일을 복사하고 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="18df9-182">Jenkins 빌드 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-182">Create Jenkins build rules</span></span>
<span data-ttu-id="18df9-183">이전 단계에서 콘솔에 메시지를 출력하는 기본 Jenkins 빌드 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="18df9-184">Dockerfile을 사용하고 앱을 실행하는 빌드 단계를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="18df9-185">Jenkins 인스턴스로 돌아가서 이전 단계에서 만든 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="18df9-186">왼쪽에 있는 **구성**을 클릭하고 **빌드** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="18df9-187">기존 `echo "Test"` 빌드 단계를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="18df9-188">기존 빌드 단계 상자의 오른쪽 위 모서리에 있는 빨간색 십자가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="18df9-189">**빌드 단계 추가**를 클릭한 다음, **셸 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="18df9-190">**명령** 상자에서 다음 Docker 명령을 입력한 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="18df9-191">Docker 빌드 단계는 이미지를 만들고, 이미지에 대한 기록을 유지할 수 있도록 하는 Jenkins 빌드 번호로 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="18df9-192">앱을 실행하는 기존 컨테이너가 모두 중지되었다가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="18df9-193">새 컨테이너는 이미지를 사용하여 시작되었다가 GitHub의 최신 커밋에 따라 Node.js 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="18df9-194">파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="18df9-194">Test your pipeline</span></span>
<span data-ttu-id="18df9-195">전체 파이프라인의 실제 동작을 확인하려면 분기된 GitHub 리포지토리에서 다시 *index.js* 파일을 편집하고 **변경 내용 커밋**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="18df9-196">GitHub에 대한 웹후크에 기반하는 Jenkins에서 새 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="18df9-197">Docker 이미지를 만들고 새 컨테이너에서 앱을 시작하는 데는 몇 초가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="18df9-198">필요한 경우 다시 VM의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="18df9-199">웹 브라우저를 열고 `http://<publicIps>:1337`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="18df9-200">Node.js 앱이 표시되고 다음과 같이 GitHub 분기에서 최신 커밋 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="18df9-202">이제 GitHub의 *index.js* 파일을 다시 편집하고 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="18df9-203">Jenkins에서 작업이 완료되는 동안 몇 초 대기한 다음, 웹 브라우저를 새로 고쳐서 다음과 같이 새 컨테이너에서 실행되는 앱의 업데이트된 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![다른 GitHub 커밋 후 Node.js 앱 실행](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="18df9-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18df9-205">Next steps</span></span>
<span data-ttu-id="18df9-206">이 자습서에서는 각 코드 커밋에서 Jenkins 빌드 작업을 실행한 다음 앱을 테스트하는 Docker 컨테이너를 배포하도록 GitHub를 구성하였습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="18df9-207">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18df9-208">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="18df9-209">Jenkins 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="18df9-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="18df9-210">GitHub 및 Jenkins 간 웹후크 통합 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="18df9-211">GitHub 커밋에서 Jenkins 빌드 작업 만들기 및 트리거</span><span class="sxs-lookup"><span data-stu-id="18df9-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="18df9-212">앱에 대한 Docker 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="18df9-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="18df9-213">새 Docker 이미지를 빌드한 GitHub 커밋 및 앱을 실행하는 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="18df9-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="18df9-214">Visual Studio Team Services와 Jenkins를 통합하는 방법에 대한 자세한 내용을 보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18df9-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="18df9-215">Jenkins 및 Team Services를 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="18df9-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)