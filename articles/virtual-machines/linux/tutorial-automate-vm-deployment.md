---
title: "Azure에서 처음 부팅 시 Linux VM 사용자 지정 | Microsoft Docs"
description: "Cloud-init 및 Key Vault를 사용하여 Azure에서 처음 부팅 시 Linux VM을 사용자 지정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="c8a89-103">처음 부팅 시 Linux 가상 컴퓨터를 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c8a89-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="c8a89-104">이전 자습서에서는 VM(가상 컴퓨터)에 SSH를 적용하고 NGINX를 수동으로 설치하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="c8a89-105">빠르고 일관된 방식으로 VM을 만들려면 일반적으로 자동화 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="c8a89-106">처음 부팅 시 VM을 사용자 지정하는 일반적인 방법은 [cloud-init](https://cloudinit.readthedocs.io)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="c8a89-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8a89-108">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="c8a89-109">cloud-init 파일을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="c8a89-110">VM을 만든 후에 실행 중인 Node.js 앱 보기</span><span class="sxs-lookup"><span data-stu-id="c8a89-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="c8a89-111">Key Vault를 사용하여 안전하게 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="c8a89-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="c8a89-112">cloud-init를 사용하여 NGINX 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="c8a89-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c8a89-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c8a89-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="c8a89-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8a89-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="c8a89-116">Cloud-init 개요</span><span class="sxs-lookup"><span data-stu-id="c8a89-116">Cloud-init overview</span></span>
<span data-ttu-id="c8a89-117">[Cloud-init](https://cloudinit.readthedocs.io)는 처음 부팅 시 Linux VM을 사용자 지정하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="c8a89-118">Cloud-init를 사용하여 패키지를 설치하고 파일을 쓰거나, 사용자 및 보안을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="c8a89-119">초기 부팅 프로세스 중에 cloud-init가 실행되면 구성을 적용하기 위한 추가 단계나 필요한 에이전트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="c8a89-120">Cloud-init는 배포에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="c8a89-121">예를 들어, 패키지를 설치하는 데 **apt-get install** 또는 **yum install**은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="c8a89-122">대신 설치할 패키지 목록을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="c8a89-123">cloud-init에서 선택한 배포판의 기본 패키지 관리 도구를 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="c8a89-124">당사는 파트너와 협력하여 파트너가 Azure에 제공하는 이미지에 cloud-init를 포함하고 이러한 이미지에서 cloud-init가 작동하도록 설정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="c8a89-125">다음 표에서는 Azure 플랫폼 이미지에서 현재 cloud-init 가용성을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="c8a89-126">Alias</span><span class="sxs-lookup"><span data-stu-id="c8a89-126">Alias</span></span> | <span data-ttu-id="c8a89-127">게시자</span><span class="sxs-lookup"><span data-stu-id="c8a89-127">Publisher</span></span> | <span data-ttu-id="c8a89-128">제안</span><span class="sxs-lookup"><span data-stu-id="c8a89-128">Offer</span></span> | <span data-ttu-id="c8a89-129">SKU</span><span class="sxs-lookup"><span data-stu-id="c8a89-129">SKU</span></span> | <span data-ttu-id="c8a89-130">버전</span><span class="sxs-lookup"><span data-stu-id="c8a89-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c8a89-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="c8a89-131">UbuntuLTS</span></span> |<span data-ttu-id="c8a89-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="c8a89-132">Canonical</span></span> |<span data-ttu-id="c8a89-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c8a89-133">UbuntuServer</span></span> |<span data-ttu-id="c8a89-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="c8a89-134">16.04-LTS</span></span> |<span data-ttu-id="c8a89-135">최신</span><span class="sxs-lookup"><span data-stu-id="c8a89-135">latest</span></span> |
| <span data-ttu-id="c8a89-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="c8a89-136">UbuntuLTS</span></span> |<span data-ttu-id="c8a89-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="c8a89-137">Canonical</span></span> |<span data-ttu-id="c8a89-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c8a89-138">UbuntuServer</span></span> |<span data-ttu-id="c8a89-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c8a89-139">14.04.5-LTS</span></span> |<span data-ttu-id="c8a89-140">최신</span><span class="sxs-lookup"><span data-stu-id="c8a89-140">latest</span></span> |
| <span data-ttu-id="c8a89-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a89-141">CoreOS</span></span> |<span data-ttu-id="c8a89-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a89-142">CoreOS</span></span> |<span data-ttu-id="c8a89-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c8a89-143">CoreOS</span></span> |<span data-ttu-id="c8a89-144">Stable</span><span class="sxs-lookup"><span data-stu-id="c8a89-144">Stable</span></span> |<span data-ttu-id="c8a89-145">최신</span><span class="sxs-lookup"><span data-stu-id="c8a89-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="c8a89-146">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-146">Create cloud-init config file</span></span>
<span data-ttu-id="c8a89-147">cloud-init의 실제 동작을 확인하려면 NGINX를 설치하고 간단한 'Hello World' Node.js 앱을 실행하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="c8a89-148">다음 cloud-init 구성은 필요한 패키지를 설치하고 Node.js 앱을 만든 다음 앱을 초기화하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="c8a89-149">현재 셸에서 *cloud-init.txt*라는 파일을 만들고 다음 구성을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="c8a89-150">예를 들어 로컬 컴퓨터에 없는 Cloud Shell에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="c8a89-151">원하는 모든 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-151">You can use any editor you wish.</span></span> <span data-ttu-id="c8a89-152">`sensible-editor cloud-init.txt`를 입력하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="c8a89-153">전체 cloud-init 파일, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="c8a89-154">cloud-init 구성 옵션에 대한 자세한 내용은 [cloud-init 구성 예제](https://cloudinit.readthedocs.io/en/latest/topics/examples.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8a89-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c8a89-155">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-155">Create virtual machine</span></span>
<span data-ttu-id="c8a89-156">VM을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c8a89-157">다음 예제에서는 *eastus* 위치에 *myResourceGroupAutomate*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="c8a89-158">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c8a89-159">`--custom-data` 매개 변수를 사용하여 cloud-init 구성 파일을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="c8a89-160">현재 작업 디렉터리 외부에 파일을 저장한 경우 *cloud-init.txt* 구성의 전체 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="c8a89-161">다음 예제에서는 *myAutomatedVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="c8a89-162">VM을 만들고 패키지를 설치하고 앱을 시작하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="c8a89-163">Azure CLI에서 프롬프트로 반환한 후 실행을 계속하는 백그라운드 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="c8a89-164">앱에 액세스하려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="c8a89-165">VM이 만들어지면 Azure CLI에 표시된 `publicIpAddress`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="c8a89-166">이 주소는 웹 브라우저를 통해 Node.js 앱에 액세스할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="c8a89-167">웹 트래픽이 VM에 도달하도록 허용하려면 [az vm open-port](/cli/azure/vm#open-port)를 사용하여 인터넷에서 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="c8a89-168">Web App 테스트</span><span class="sxs-lookup"><span data-stu-id="c8a89-168">Test web app</span></span>
<span data-ttu-id="c8a89-169">이제 웹 브라우저를 열고 주소 표시줄에 *http://<publicIpAddress>*를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="c8a89-170">VM 만들기 프로세스에서 사용자 고유의 공용 IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="c8a89-171">Node.js 앱은 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-171">Your Node.js app is displayed as in the following example:</span></span>

![실행 중인 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="c8a89-173">Key Vault의 인증서 삽입</span><span class="sxs-lookup"><span data-stu-id="c8a89-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="c8a89-174">이 선택적 섹션에서는 Azure Key Vault에 안전하게 인증서를 저장하고 VM 배포 중에 이 인증서를 삽입할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="c8a89-175">내재된 인증서를 포함하는 사용자 지정 이미지를 사용하는 대신 이 프로세스를 통해 처음 부팅 시 가장 최신 인증서를 VM에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="c8a89-176">프로세스 동안 인증서는 Azure 플랫폼에서 벗어나거나 스크립트, 명령줄 기록 또는 템플릿에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="c8a89-177">Azure Key Vault는 암호화 키 및 비밀(인증서 또는 암호)을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="c8a89-178">Key Vault를 사용하면 키 관리 프로세스를 간소화하고 데이터를 액세스하고 암호화하는 키의 제어를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="c8a89-179">이 시나리오는 Key Vault를 사용하는 방법에 대한 자세한 개요는 아니지만 인증서를 만들고 사용할 수 있는 Key Vault의 몇 가지 개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="c8a89-180">다음 단계에서는 다음과 같은 작업을 수행할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-180">The following steps show how you can:</span></span>

- <span data-ttu-id="c8a89-181">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="c8a89-182">Key Vault에 인증서 생성 또는 업로드</span><span class="sxs-lookup"><span data-stu-id="c8a89-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="c8a89-183">VM에 삽입할 인증서의 비밀 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="c8a89-184">VM 만들기 및 인증서 삽입</span><span class="sxs-lookup"><span data-stu-id="c8a89-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="c8a89-185">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="c8a89-186">먼저 [az keyvault create](/cli/azure/keyvault#create)를 사용하여 Key Vault를 만들고 VM 배포 시에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="c8a89-187">각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="c8a89-188">다음 예제에서 *mykeyvault*를 사용자 고유의 Key Vault 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="c8a89-189">인증서 생성 및 Key Vault에 저장</span><span class="sxs-lookup"><span data-stu-id="c8a89-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="c8a89-190">프로덕션 사용을 위해 [az keyvault certificate import](/cli/azure/keyvault/certificate#import)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="c8a89-191">이 자습서에서는 다음 예제를 통해 [az keyvault certificate create](/cli/azure/keyvault/certificate#create)를 사용하여 기본 인증서 정책을 사용하는 자체 서명된 인증서를 생성할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="c8a89-192">VM에 사용할 인증서 준비</span><span class="sxs-lookup"><span data-stu-id="c8a89-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="c8a89-193">VM 만들기 프로세스 동안 인증서를 사용하려면 [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions)를 사용하여 인증서 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="c8a89-194">VM에는 부팅 시 삽입하는 특정 형식의 인증서가 필요하므로 [az vm format-secret](/cli/azure/vm#format-secret)을 사용하여 인증서를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="c8a89-195">다음 예제에서는 다음 단계의 사용 편의성을 위해 변수에 이러한 명령의 출력을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="c8a89-196">NGINX를 보호할 cloud-init 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="c8a89-197">VM을 만들 때 인증서와 키는 보호되는 */var/lib/waagent/* 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="c8a89-198">VM에 인증서 추가 및 NGINX 구성을 자동화하기 위해 이전 예제에서 업데이트된 cloud-init 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="c8a89-199">*cloud-init-secured.txt*라는 파일을 만들고 다음 구성을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="c8a89-200">다시, Cloud Shell을 사용하는 경우 로컬 컴퓨터가 아닌 해당 위치에서 cloud-init 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="c8a89-201">`sensible-editor cloud-init-secured.txt`를 사용하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="c8a89-202">전체 cloud-init 파일, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="c8a89-203">보안 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-203">Create secure VM</span></span>
<span data-ttu-id="c8a89-204">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c8a89-205">인증서 데이터는 `--secrets` 매개 변수를 사용하여 Key Vault에서 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="c8a89-206">이전 예제와 마찬가지로 `--custom-data` 매개 변수를 사용하여 cloud-init 구성을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="c8a89-207">VM을 만들고 패키지를 설치하고 앱을 시작하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="c8a89-208">Azure CLI에서 프롬프트로 반환한 후 실행을 계속하는 백그라운드 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="c8a89-209">앱에 액세스하려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="c8a89-210">VM이 만들어지면 Azure CLI에 표시된 `publicIpAddress`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="c8a89-211">이 주소는 웹 브라우저를 통해 Node.js 앱에 액세스할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="c8a89-212">보안 웹 트래픽이 VM에 도달하도록 허용하려면 [az vm open-port](/cli/azure/vm#open-port)를 사용하여 인터넷에서 포트 443을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="c8a89-213">보안 Web App 테스트</span><span class="sxs-lookup"><span data-stu-id="c8a89-213">Test secure web app</span></span>
<span data-ttu-id="c8a89-214">이제 웹 브라우저를 열고 주소 표시줄에 *https://<publicIpAddress>*를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="c8a89-215">VM 만들기 프로세스에서 사용자 고유의 공용 IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="c8a89-216">자체 서명된 인증서를 사용하는 경우 보안 경고를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-216">Accept the security warning if you used a self-signed certificate:</span></span>

![웹 브라우저 보안 경고 허용](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="c8a89-218">그러면 보안 NGINX 사이트와 Node.js 앱이 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![실행 중인 보안 NGINX 사이트 보기](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="c8a89-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8a89-220">Next steps</span></span>
<span data-ttu-id="c8a89-221">이 자습서에서는 cloud-init를 사용하여 처음 부팅할 때 VM을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="c8a89-222">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8a89-223">cloud-init 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="c8a89-224">cloud-init 파일을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="c8a89-225">VM을 만든 후에 실행 중인 Node.js 앱 보기</span><span class="sxs-lookup"><span data-stu-id="c8a89-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="c8a89-226">Key Vault를 사용하여 안전하게 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="c8a89-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="c8a89-227">cloud-init를 사용하여 NGINX 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="c8a89-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="c8a89-228">사용자 지정 VM 이미지를 만드는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a89-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8a89-229">사용자 지정 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c8a89-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
