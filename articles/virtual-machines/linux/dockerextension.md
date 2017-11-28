---
title: "aaaUse hello Azure Docker VM 확장 | Microsoft Docs"
description: "Toouse Docker VM 확장 tooquickly hello와 안전 하 게 리소스 관리자 템플릿을 사용 하 여 Azure에서 Docker 환경을 배포 방법과 hello Azure CLI 2.0에 알아봅니다"
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
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="aef58-103">Hello Docker VM 확장을 사용 하 여 Azure에서 Docker 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="aef58-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="aef58-104">Docker는 인기 있는 컨테이너 관리와 이미징 플랫폼 linux 컨테이너와 tooquickly 작업을 허용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="aef58-105">Azure에서 다양 한 방법으로 Docker tooyour 요구에 따라 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="aef58-106">이 문서에서는 Azure CLI 2.0 hello hello Docker VM 확장 및 Azure 리소스 관리자 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="aef58-107">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](dockerextension-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="aef58-108">Azure Docker VM 확장 개요</span><span class="sxs-lookup"><span data-stu-id="aef58-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="aef58-109">hello Azure Docker VM 확장을 설치 하 고 Linux 가상 컴퓨터 (VM)에서 hello Docker 디먼을, Docker 클라이언트 및 Docker Compose를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="aef58-110">Hello Azure Docker VM 확장을 사용 하 여 더 많은 제어 및 기능 보다 간단히 Docker 컴퓨터를 사용 하 여 hello Docker 호스트를 직접 만드는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="aef58-111">등의 이러한 추가 기능은 [Docker Compose](https://docs.docker.com/compose/overview/), 더욱 강력한 개발자 또는 프로덕션 환경에 적합 한 hello Azure Docker VM 확장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="aef58-112">Docker 컴퓨터 및 Azure 컨테이너 서비스를 사용 하는 등 hello 다양 한 배포 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="aef58-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="aef58-113">tooquickly 프로토타입 응용 프로그램을 사용 하 여 단일 Docker 호스트를 만들 수 있습니다 [Docker 컴퓨터](docker-machine.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="aef58-114">배포할 수 있습니다 toobuild 즉시 사용, 확장 가능한 환경 추가 일정 예약 및 관리 도구를 제공 하는 한 [Azure 컨테이너 서비스에서 클러스터 docker는 Docker Swarm](../../container-service/dcos-swarm/container-service-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="aef58-115">Azure Docker VM 확장 hello로 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="aef58-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="aef58-116">보겠습니다 기존 퀵 스타트 템플릿 toocreate hello Azure Docker VM 확장 tooinstall를 사용 하는 Ubuntu VM을 사용 하 고 hello Docker 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="aef58-117">여기에 hello 서식 파일을 볼 수 있습니다: [Docker가 있는 Ubuntu VM의 간단한 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="aef58-118">최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="aef58-119">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="aef58-120">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westus* 위치:</span><span class="sxs-lookup"><span data-stu-id="aef58-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="aef58-121">다음에 사용 하 여 VM을 배포 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) hello Azure Docker VM 확장을 포함 하는 [GitHub에서이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="aef58-122">다음과 같이 *newStorageAccountName*, *adminUsername*, *adminPassword* 및 *dnsNameForPublicIP*에 대한 고유한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="aef58-123">배포 toofinish hello에 대 한 몇 가지 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="aef58-124">응용 프로그램이 완료 되 면 hello 배포 [toonext 단계 이동](#deploy-your-first-nginx-container) tooSSH tooyour VM입니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="aef58-125">필요에 따라 hello 추가 tooinstead 반환 컨트롤 toohello 확인 및 let hello 배포 hello 백그라운드에서 계속 `--no-wait` toohello 명령 앞에 플래그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="aef58-126">이 프로세스 tooperform 수 있습니다. 몇 분 동안 계속 hello 배포 하는 동안 CLI hello에서 다른 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="aef58-127">와 hello Docker 호스트 상태에 대 한 세부 정보를 볼 수 있습니다 [az vm 표시](/cli/azure/vm#show)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="aef58-128">hello 다음 예제에서는 hello의 상태를 검사 hello 라는 VM *myDockerVM* (hello hello 서식 파일에서 기본 이름-이 이름은 변경 하지 않는) 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="aef58-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="aef58-129">이 명령은 반환 하는 경우 *Succeeded*, hello 배포가 완료 되 고 단계 다음에 나오는 hello에 SSH toohello VM을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="aef58-130">첫 번째 nginx 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="aef58-130">Deploy your first nginx container</span></span>
<span data-ttu-id="aef58-131">VM 포함 하 여 hello DNS 이름의 tooview 세부 정보를 사용 하 여 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="aef58-132">SSH tooyour 새 Docker 호스트 로컬 컴퓨터에서 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="aef58-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="aef58-133">로그인 한 toohello Docker 호스트 nginx 컨테이너를 실행 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="aef58-134">hello 출력은 hello nginx 이미지 다운로드는 다음 예제와 비슷한 toohello 및 시작 하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="aef58-135">다음과 같이 Docker 호스트에서 실행 되는 hello 컨테이너의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="aef58-136">hello 출력은 다음 예제와 비슷한 toohello, 실행 중 이며 TCP 포트 80 및 443 및 전달 되 고 해당 hello nginx 컨테이너를 보여 주는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="aef58-137">toosee 컨테이너 작업에서 열 웹 브라우저를 및 Docker 호스트의 hello DNS 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![ngnix 컨테이너 실행](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="aef58-139">Azure Docker VM 확장 템플릿 참조</span><span class="sxs-lookup"><span data-stu-id="aef58-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="aef58-140">hello 이전 예제에서는 기존 퀵 스타트 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="aef58-141">사용자 리소스 관리자 템플릿을 hello Azure Docker VM 확장을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="aef58-142">toodo hello tooyour 리소스 관리자 템플릿을 다음, hello 정의 추가, `vmName` vm 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="aef58-143">Resource Manager 템플릿 사용에 대한 자세한 연습은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aef58-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef58-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aef58-144">Next steps</span></span>
<span data-ttu-id="aef58-145">너무 수도[hello Docker 디먼이 TCP 포트 구성](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), 이해 [Docker 보안](https://docs.docker.com/engine/security/security/), 컨테이너를 사용 하 여 배포 또는 [Docker Compose](https://docs.docker.com/compose/overview/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="aef58-146">자체 Azure Docker VM 확장 hello에 대 한 자세한 내용은 참조 hello [GitHub 프로젝트](https://github.com/Azure/azure-docker-extension/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="aef58-147">Azure의 hello 추가 Docker 배포 옵션에 대 한 자세한 정보를 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="aef58-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="aef58-148">Azure 드라이버 hello로 사용 하 여 Docker 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="aef58-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="aef58-149">[Docker로 시작 하 고 toodefine를 작성 하 고, Azure 가상 컴퓨터에서 여러 컨테이너 응용 프로그램 실행](docker-compose-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef58-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="aef58-150">Azure 컨테이너 서비스 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="aef58-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

