---
title: "Azure Docker VM 확장 사용 | Microsoft Docs"
description: "Docker VM 확장을 사용하여 Azure에서 Resource Manager 템플릿 및 Azure CLI 2.0을 사용하여 Docker 환경을 빠르고 안전하게 배포하는 방법에 대해 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="946ae-103">Docker VM 확장을 사용하여 Azure에서 Docker 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="946ae-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="946ae-104">Docker는 Linux에서 컨테이너와 함께 빠르게 사용할 수 있는 인기 있는 컨테이너 관리 및 이미징 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="946ae-105">Azure에는 필요에 맞게 Docker를 배포할 수 있는 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="946ae-106">이 문서는 Azure CLI 2.0을 사용하여 Docker VM 확장 및 Azure Resource Manager 템플릿을 사용하는 방법에 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="946ae-107">[Azure CLI 1.0](dockerextension-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="946ae-108">Azure Docker VM 확장 개요</span><span class="sxs-lookup"><span data-stu-id="946ae-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="946ae-109">Azure Docker VM 확장은 Linux 가상 컴퓨터(VM)에 Docker 데몬, Docker 클라이언트 및 Docker Compose를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="946ae-110">Azure Docker VM 확장을 사용하면 직접 Docker 호스트를 만들거나 Docker Machine을 사용하는 것보다 더 많은 제어와 가능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="946ae-111">[Docker Compose](https://docs.docker.com/compose/overview/)와 같은 이러한 추가 기능은 Azure Docker VM 확장을 보다 강력한 개발자 또는 프로덕션 환경에 적합하도록 만들어 줍니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="946ae-112">Docker Machine 및 Azure Container Service 사용을 비롯한 다른 배포 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="946ae-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="946ae-113">앱을 신속하게 프로토타이핑하려면 [Docker Machine](docker-machine.md)을 사용하여 단일 Docker 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="946ae-114">추가 예약 및 관리 도구를 제공하는 프로덕션이 준비된 확장성 있는 환경을 구축하려면 [Azure Container Services에 Docker Swarm 클러스터](../../container-service/dcos-swarm/container-service-deployment.md)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="946ae-115">Azure Docker VM 확장을 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="946ae-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="946ae-116">기존의 빠른 시작 템플릿을 사용하여 Docker 호스트를 설치 및 구성하기 위해 Azure Docker VM 확장을 사용하는 Ubuntu VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="946ae-117">템플릿은 [Docker를 사용한 간단한 Ubuntu VM 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="946ae-118">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="946ae-119">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="946ae-120">다음 예제에서는 *westus* 위치에*myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="946ae-121">다음으로 [GitHub의 이 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)의 Azure Docker VM 확장을 포함하는 [az group deployment create](/cli/azure/group/deployment#create)로 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="946ae-122">다음과 같이 *newStorageAccountName*, *adminUsername*, *adminPassword* 및 *dnsNameForPublicIP*에 대한 고유한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="946ae-123">배포를 완료하려면 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="946ae-124">배포가 완료되면 [다음 단계로 이동](#deploy-your-first-nginx-container)하여 VM에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="946ae-125">필요에 따라 프롬프트에 대한 제어를 반환하고 백그라운드에서 배포를 계속하려면 `--no-wait` 플래그를 이전 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="946ae-126">이 프로세스를 통해 배포가 몇 분 동안 계속되는 동안 CLI에서 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="946ae-127">[az vm show](/cli/azure/vm#show)를 사용하여 Docker 호스트 상태에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="946ae-128">다음 예제에서는 *myResourceGroup*이라는 리소스 그룹에서 *myDockerVM*(템플릿의 기본 이름이므로 변경하지 말 것)이라는 VM의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="946ae-129">이 명령이 *Succeeded*를 반환하는 경우 배포가 완료되었으며 다음 단계에서 VM에 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="946ae-130">첫 번째 nginx 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="946ae-130">Deploy your first nginx container</span></span>
<span data-ttu-id="946ae-131">DNS 이름을 비롯한 VM의 세부 정보를 보려면 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="946ae-132">다음과 같이 로컬 컴퓨터에서 새 Docker 호스트에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="946ae-133">Docker 호스트에 로그인되면 nginx 컨테이너를 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="946ae-134">출력 내용은 nginx 이미지가 다운로드되고 컨테이너가 시작되는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="946ae-135">다음과 같이 Docker 호스트에서 실행 중인 컨테이너의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="946ae-136">출력 내용은 nginx 컨테이너를 실행 중이고 TCP 포트 80 및 443이 전달되는 것을 보여주는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="946ae-137">작동되는 컨테이너를 보려면 웹 브라우저를 열고 Docker 호스트의 DNS 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![ngnix 컨테이너 실행](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="946ae-139">Azure Docker VM 확장 템플릿 참조</span><span class="sxs-lookup"><span data-stu-id="946ae-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="946ae-140">이전 예제는 기존의 빠른 시작 템플릿을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="946ae-141">자신만의 Resource Manager 템플릿을 사용하여 Azure Docker VM 확장을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="946ae-142">이렇게 하려면 VM의 `vmName`을 적합하게 정의하는 다음 내용을 Resource Manager 템플릿에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="946ae-143">Resource Manager 템플릿 사용에 대한 자세한 연습은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="946ae-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="946ae-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="946ae-144">Next steps</span></span>
<span data-ttu-id="946ae-145">[Docker Compose](https://docs.docker.com/compose/overview/)를 사용하여 [Docker 디먼 TCP 포트를 구성](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket)하고, [Docker 보안](https://docs.docker.com/engine/security/security/)을 이해하거나 컨테이너를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946ae-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="946ae-146">Azure Docker VM 확장 자체에 대한 자세한 내용은 [GitHub 프로젝트](https://github.com/Azure/azure-docker-extension/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="946ae-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="946ae-147">Azure의 추가적인 Docker 배포 옵션에 대한 자세한 내용을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="946ae-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="946ae-148">Azure 드라이버로 Docker Machine 사용</span><span class="sxs-lookup"><span data-stu-id="946ae-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="946ae-149">[Azure 가상 컴퓨터에서 다중 컨테이너 응용 프로그램 정의 및 실행을 위해 Docker 및 Compose 시작](docker-compose-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="946ae-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="946ae-150">Azure 컨테이너 서비스 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="946ae-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

