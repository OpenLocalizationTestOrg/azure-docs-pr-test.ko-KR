---
title: "Linux VM에 Azure에서 처음 부팅 aaaCustomize | Microsoft Docs"
description: "어떻게 toouse 클라우드 init 및 주요 자격 증명 모음 toocustomze Linux Vm의 경우 hello 처음 부팅 될 Azure에 알아봅니다."
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="0f81d-103">어떻게 toocustomize 첫 번째 부팅의 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="0f81d-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="0f81d-104">이전 자습서에서는 방법에 대해 배웠습니다 tooSSH tooa 가상 컴퓨터 (VM) NGINX를 수동으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="0f81d-105">Vm을 신속 하 고 일관 된 방식으로 자동화 toocreate 방법이 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="0f81d-106">일반적인 접근 방식을 toocustomize 첫 번째 부팅 시 VM은 toouse [클라우드 init](https://cloudinit.readthedocs.io)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="0f81d-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f81d-108">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="0f81d-109">cloud-init 파일을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="0f81d-110">VM이 생성 하는 hello 후 실행 중인 Node.js 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="0f81d-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="0f81d-111">주요 자격 증명 모음 toosecurely 인증서 저장소를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0f81d-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="0f81d-112">cloud-init를 사용하여 NGINX 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="0f81d-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0f81d-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="0f81d-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0f81d-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0f81d-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="0f81d-116">Cloud-init 개요</span><span class="sxs-lookup"><span data-stu-id="0f81d-116">Cloud-init overview</span></span>
<span data-ttu-id="0f81d-117">[클라우드 init](https://cloudinit.readthedocs.io) 는 널리 사용 되는 접근 방식을 toocustomize Linux VM 처음으로 hello에 대 한 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="0f81d-118">클라우드 init tooinstall 패키지를 사용할 수 있으며 파일, 또는 tooconfigure 사용자 및 보안에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="0f81d-119">추가 단계 없이 없는 클라우드 init hello 초기 부팅 프로세스 중 실행 될 때 또는 에이전트 tooapply 구성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="0f81d-120">Cloud-init는 배포에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="0f81d-121">예를 들어 사용 하지 않는 **apt get 설치** 또는 **yum 설치** tooinstall 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="0f81d-122">대신 패키지 tooinstall의 목록을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="0f81d-123">클라우드 init 자동으로 선택 하는 hello 배포판에 대 한 hello 네이티브 패키지 관리 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="0f81d-124">TooAzure를 제공 하는 hello 이미지에서 작업 및 우리의 파트너 tooget 클라우드 초기화 포함을 사용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="0f81d-125">다음 표에서 hello Azure 플랫폼 이미지에 현재 클라우드 init 가용성 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="0f81d-126">Alias</span><span class="sxs-lookup"><span data-stu-id="0f81d-126">Alias</span></span> | <span data-ttu-id="0f81d-127">게시자</span><span class="sxs-lookup"><span data-stu-id="0f81d-127">Publisher</span></span> | <span data-ttu-id="0f81d-128">제안</span><span class="sxs-lookup"><span data-stu-id="0f81d-128">Offer</span></span> | <span data-ttu-id="0f81d-129">SKU</span><span class="sxs-lookup"><span data-stu-id="0f81d-129">SKU</span></span> | <span data-ttu-id="0f81d-130">버전</span><span class="sxs-lookup"><span data-stu-id="0f81d-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0f81d-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0f81d-131">UbuntuLTS</span></span> |<span data-ttu-id="0f81d-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="0f81d-132">Canonical</span></span> |<span data-ttu-id="0f81d-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0f81d-133">UbuntuServer</span></span> |<span data-ttu-id="0f81d-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="0f81d-134">16.04-LTS</span></span> |<span data-ttu-id="0f81d-135">최신</span><span class="sxs-lookup"><span data-stu-id="0f81d-135">latest</span></span> |
| <span data-ttu-id="0f81d-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0f81d-136">UbuntuLTS</span></span> |<span data-ttu-id="0f81d-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="0f81d-137">Canonical</span></span> |<span data-ttu-id="0f81d-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0f81d-138">UbuntuServer</span></span> |<span data-ttu-id="0f81d-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="0f81d-139">14.04.5-LTS</span></span> |<span data-ttu-id="0f81d-140">최신</span><span class="sxs-lookup"><span data-stu-id="0f81d-140">latest</span></span> |
| <span data-ttu-id="0f81d-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0f81d-141">CoreOS</span></span> |<span data-ttu-id="0f81d-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0f81d-142">CoreOS</span></span> |<span data-ttu-id="0f81d-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0f81d-143">CoreOS</span></span> |<span data-ttu-id="0f81d-144">Stable</span><span class="sxs-lookup"><span data-stu-id="0f81d-144">Stable</span></span> |<span data-ttu-id="0f81d-145">최신</span><span class="sxs-lookup"><span data-stu-id="0f81d-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="0f81d-146">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-146">Create cloud-init config file</span></span>
<span data-ttu-id="0f81d-147">toosee 클라우드 초기화 작업에서 NGINX를 설치 하 고 간단한 ' Hello World' Node.js 응용 프로그램을 실행 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="0f81d-148">같은 클라우드 init 구성이 hello hello 필요한 패키지를 설치, Node.js 응용 프로그램을 만들고 초기화 하 고 hello 앱이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="0f81d-149">현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="0f81d-150">예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="0f81d-151">원하는 모든 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-151">You can use any editor you wish.</span></span> <span data-ttu-id="0f81d-152">입력 `sensible-editor cloud-init.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="0f81d-153">해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="0f81d-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="0f81d-154">cloud-init 구성 옵션에 대한 자세한 내용은 [cloud-init 구성 예제](https://cloudinit.readthedocs.io/en/latest/topics/examples.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f81d-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="0f81d-155">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-155">Create virtual machine</span></span>
<span data-ttu-id="0f81d-156">VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0f81d-157">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAutomate* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="0f81d-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="0f81d-158">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0f81d-159">사용 하 여 hello `--custom-data` 클라우드 init 구성 파일에서 매개 변수 toopass 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="0f81d-160">Hello 전체 경로 toohello 제공 *클라우드 init.txt* config 현재 작업 디렉터리 외부의 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="0f81d-161">hello 다음 예제에서는 V *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="0f81d-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="0f81d-162">Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="0f81d-163">Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="0f81d-164">다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="0f81d-165">Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="0f81d-166">이 주소는 웹 브라우저를 통해 사용 되는 tooaccess hello Node.js 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="0f81d-167">tooallow 웹 트래픽 tooreach VM을 열고에 포트 80에서 인터넷 hello [az vm-포트를 열](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="0f81d-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="0f81d-168">Web App 테스트</span><span class="sxs-lookup"><span data-stu-id="0f81d-168">Test web app</span></span>
<span data-ttu-id="0f81d-169">웹 브라우저를 열고 입력 수 이제 *http://<publicIpAddress>*  hello 주소 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="0f81d-170">제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="0f81d-171">Node.js 앱 hello 다음 예제와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-171">Your Node.js app is displayed as in hello following example:</span></span>

![실행 중인 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="0f81d-173">Key Vault의 인증서 삽입</span><span class="sxs-lookup"><span data-stu-id="0f81d-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="0f81d-174">이 선택적 섹션이 안전 하 게 Azure 키 자격 증명 모음에 인증서를 저장 하는 방법을 hello VM 배포 하는 동안 이러한 구성 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="0f81d-175">Hello 인증서를 포함 하는 사용자 지정 이미지를 사용 하는 대신 구운 기능,이 과정을 사용 하면 가장 최신 인증서 hello은 첫 번째 부팅 시 tooa VM을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="0f81d-176">Hello 과정에서 hello 인증서 되지 hello Azure 플랫폼 벗어나거나 스크립트, 명령줄 기록 또는 서식 파일에 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="0f81d-177">Azure Key Vault는 암호화 키 및 비밀(인증서 또는 암호)을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="0f81d-178">주요 자격 증명 모음은 hello 키 관리 프로세스를 간소화 하는 데 도움이 됩니다 하 고 액세스 하 고 데이터를 암호화 하는 키의 toomaintain 제어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="0f81d-179">이 시나리오에서는 몇 가지 주요 자격 증명 모음 개념 toocreate 및 인증서 사용 소개, 방법에 대 한 철저 한 개요를 통해는 toouse 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="0f81d-180">hello 단계를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="0f81d-181">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="0f81d-182">생성 또는 인증서 toohello 주요 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="0f81d-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="0f81d-183">Hello 인증서 tooinject tooa VM에서에서에서 암호 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="0f81d-184">VM을 만들고 hello 인증서 삽입</span><span class="sxs-lookup"><span data-stu-id="0f81d-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="0f81d-185">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="0f81d-186">먼저 [az keyvault create](/cli/azure/keyvault#create)를 사용하여 Key Vault를 만들고 VM 배포 시에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="0f81d-187">각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="0f81d-188">대체 *mykeyvault* 다음 예에서는 고유 키 자격 증명 모음 이름으로 hello에:</span><span class="sxs-lookup"><span data-stu-id="0f81d-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="0f81d-189">인증서 생성 및 Key Vault에 저장</span><span class="sxs-lookup"><span data-stu-id="0f81d-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="0f81d-190">프로덕션 사용을 위해 [az keyvault certificate import](/cli/azure/keyvault/certificate#import)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="0f81d-191">이 자습서에 대 한 hello 다음 예제와 자체 서명 된 인증서를 생성 하는 방법을 [az keyvault 인증서 만들기](/cli/azure/keyvault/certificate#create) hello 기본 인증서 정책을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="0f81d-192">VM에 사용할 인증서 준비</span><span class="sxs-lookup"><span data-stu-id="0f81d-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="0f81d-193">hello VM 중 toouse hello 인증서 프로세스 만들기, 사용 하 여 인증서의 hello ID를 가져오려면 [az keyvault 비밀 목록-버전](/cli/azure/keyvault/secret#list-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="0f81d-194">hello VM hello 인증서가 필요는 특정 형식 tooinject 부팅에 있으므로 변환로 hello 인증서 [az vm 형식 비밀](/cli/azure/vm#format-secret)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="0f81d-195">다음 예제는 hello hello 출력 hello 사용 하 여 쉽게 이러한 명령 toovariables의 다음 단계에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="0f81d-196">클라우드 init config toosecure NGINX 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="0f81d-197">인증서는 VM을 만들 시점과 키가 보호 하는 hello에 저장 */var/lib/waagent/* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="0f81d-198">tooautomate 추가 hello 인증서 toohello VM 하 고 구성한 NGINX hello 이전 예제의 업데이트 된 클라우드 init config는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="0f81d-199">라는 파일을 만들어 *클라우드-init-secured.txt* 붙여넣기 hello 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="0f81d-200">다시 클라우드 셸 hello를 사용 하는 경우 파일을 만듭니다 hello 클라우드 init 구성 없어 및 로컬 컴퓨터에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="0f81d-201">사용 하 여 `sensible-editor cloud-init-secured.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="0f81d-202">해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="0f81d-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="0f81d-203">보안 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-203">Create secure VM</span></span>
<span data-ttu-id="0f81d-204">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0f81d-205">hello 인증서 데이터를 키 자격 증명 모음에서 hello로 주입 `--secrets` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="0f81d-206">Hello 이전 예제와 같이 전달 hello로 hello 클라우드 init config `--custom-data` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0f81d-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="0f81d-207">Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="0f81d-208">Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="0f81d-209">다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="0f81d-210">Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="0f81d-211">이 주소는 웹 브라우저를 통해 사용 되는 tooaccess hello Node.js 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="0f81d-212">tooallow 보안 웹 트래픽을 tooreach VM, 열린 포트 443에서 인터넷 hello와 [az vm-포트를 열](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="0f81d-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="0f81d-213">보안 Web App 테스트</span><span class="sxs-lookup"><span data-stu-id="0f81d-213">Test secure web app</span></span>
<span data-ttu-id="0f81d-214">웹 브라우저를 열고 입력 수 이제 *https://<publicIpAddress>*  hello 주소 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="0f81d-215">제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="0f81d-216">자체 서명 된 인증서를 사용 하는 경우 hello 보안 경고를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![웹 브라우저 보안 경고 허용](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="0f81d-218">보안 된 NGINX 사이트와 Node.js 앱 hello 다음 예제와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![실행 중인 보안 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="0f81d-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f81d-220">Next steps</span></span>
<span data-ttu-id="0f81d-221">이 자습서에서는 cloud-init를 사용하여 처음 부팅할 때 VM을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="0f81d-222">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f81d-223">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="0f81d-224">cloud-init 파일을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="0f81d-225">VM이 생성 하는 hello 후 실행 중인 Node.js 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="0f81d-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="0f81d-226">주요 자격 증명 모음 toosecurely 인증서 저장소를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0f81d-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="0f81d-227">cloud-init를 사용하여 NGINX 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="0f81d-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="0f81d-228">다음 자습서 toolearn toohello 어떻게 발전 toocreate 사용자 지정 VM 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="0f81d-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f81d-229">사용자 지정 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f81d-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
