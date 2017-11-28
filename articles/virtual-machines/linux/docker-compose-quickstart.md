---
title: "Azure에서 Linux VM에 대한 Docker Compose 사용 | Microsoft Docs"
description: "Azure CLI와 함께 Linux 가상 컴퓨터에서 Docker 및 Compose를 사용하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="6c6a3-103">Azure에서 다중 컨테이너 응용 프로그램 정의 및 실행을 위해 Docker 및 Compose 시작</span><span class="sxs-lookup"><span data-stu-id="6c6a3-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="6c6a3-104">[Compose](http://github.com/docker/compose)를 사용하면 간단한 텍스트 파일을 사용하여 여러 Docker 컨테이너로 구성된 응용 프로그램을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="6c6a3-105">그런 다음 정의된 환경을 배포하도록 모든 작업을 수행하는 단일 명령으로 응용 프로그램을 스핀업합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="6c6a3-106">그 예로, 이 문서에서는 Ubuntu VM의 백 엔드 MariaDB SQL Database로 WordPress 블로그를 신속하게 설정하는 방법을 보여주지만</span><span class="sxs-lookup"><span data-stu-id="6c6a3-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="6c6a3-107">Compose를 사용하여 좀더 복잡한 응용 프로그램을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="6c6a3-108">Docker 호스트로 Linux VM 설정</span><span class="sxs-lookup"><span data-stu-id="6c6a3-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="6c6a3-109">다양한 Azure 절차와 Azure Markeplace에서 사용 가능한 이미지 또는 Resource Manager 템플릿을 사용하여 Linux VM을 만들고 Docker 호스트로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="6c6a3-110">예를 들어 [빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)을 사용하여 Azure Docker VM 확장으로 Ubuntu VM을 빠르게 만들려면 [Docker VM 확장을 사용하여 환경 배포](dockerextension.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="6c6a3-111">Docker VM 확장을 사용하면 VM이 자동으로 Docker 호스트로 설정되고 Compose는 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="6c6a3-112">Azure CLI 2.0을 사용하여 Docker 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="6c6a3-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="6c6a3-113">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6c6a3-114">먼저 [az group create](/cli/azure/group#create)를 사용하여 Docker 환경에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6c6a3-115">다음 예제에서는 *westus* 위치에*myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="6c6a3-116">다음으로 [GitHub의 이 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)의 Azure Docker VM 확장을 포함하는 [az group deployment create](/cli/azure/group/deployment#create)로 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="6c6a3-117">*newStorageAccountName*, *adminUsername*, *adminPassword* 및 *dnsNameForPublicIP*에 대한 고유한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="6c6a3-118">배포를 완료하려면 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="6c6a3-119">배포가 완료되면 [다음 단계로 이동](#verify-that-compose-is-installed)하여 VM에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="6c6a3-120">필요에 따라 프롬프트에 대한 제어를 반환하고 백그라운드에서 배포를 계속하려면 `--no-wait` 플래그를 이전 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="6c6a3-121">이 프로세스를 통해 배포가 몇 분 동안 계속되는 동안 CLI에서 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="6c6a3-122">[az vm show](/cli/azure/vm#show)를 사용하여 Docker 호스트 상태에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="6c6a3-123">다음 예제에서는 *myResourceGroup*이라는 리소스 그룹에서 *myDockerVM*(템플릿의 기본 이름이므로 변경하지 말 것)이라는 VM의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="6c6a3-124">이 명령이 *Succeeded*를 반환하는 경우 배포가 완료되었으며 다음 단계에서 VM에 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="6c6a3-125">Compose 설치 여부 확인</span><span class="sxs-lookup"><span data-stu-id="6c6a3-125">Verify that Compose is installed</span></span>
<span data-ttu-id="6c6a3-126">배포가 완료되면 배포 중 입력한 DNS 이름을 사용하여 새 Docker 호스트에 SSH를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="6c6a3-127">`az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`을 사용하여 DNS 이름을 비롯한 VM의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="6c6a3-128">Compose가 VM에 설치되어 있는지 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="6c6a3-129">*docker-compose 1.6.2, build 4d72027*과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="6c6a3-130">다른 방법을 사용하여 Docker 호스트를 만들었고 Compose를 직접 설치할 필요가 있다면 [Compose 설명서](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="6c6a3-131">docker-compose.yml 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6c6a3-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="6c6a3-132">그 다음, `docker-compose.yml` 파일을 만드는데, 이 파일은 VM에서 실행할 Docker 컨테이너를 정의하기 위한 텍스트 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="6c6a3-133">파일은 각 컨테이너에서 실행되는 이미지(또는 Dockerfile에서 빌드일 수 있음), 필요한 환경 변수 및 종속성, 포트, 컨테이너 간 링크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="6c6a3-134">yml 파일 구문에 대한 세부 정보는 [Compose 파일 참조](https://docs.docker.com/compose/compose-file/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="6c6a3-135">다음과 같이 *docker-compose.yml* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="6c6a3-136">원하는 텍스트 편집기를 사용하여 파일에 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="6c6a3-137">다음 예제에서는 *vi* 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="6c6a3-138">다음 예제를 텍스트 파일로 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-138">Paste the following example into your text file.</span></span> <span data-ttu-id="6c6a3-139">이 구성은 [DockerHub 레지스트리](https://registry.hub.docker.com/_/wordpress/) 의 이미지를 사용하여 WordPress(오픈 소스 블로깅 및 콘텐츠 관리 시스템) 및 연결된 백 엔드 MariaDB SQL 데이터베이스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="6c6a3-140">다음과 같이 고유한 *MYSQL_ROOT_PASSWORD*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="6c6a3-141">Compose를 사용하여 컨테이너 시작</span><span class="sxs-lookup"><span data-stu-id="6c6a3-141">Start the containers with Compose</span></span>
<span data-ttu-id="6c6a3-142">*docker-compose.yml* 파일과 동일한 디렉터리에서 다음 명령을 실행합니다(환경에 따라 `sudo`를 사용하여 `docker-compose`를 실행해야 할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="6c6a3-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="6c6a3-143">이 명령은 *docker-compose.yml*에 지정된 Docker 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="6c6a3-144">이 단계를 완료하려면 1~2분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="6c6a3-145">다음 예제와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="6c6a3-146">백그라운드에서 계속 실행되도록 **-d** 옵션을 시작에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="6c6a3-147">컨테이너가 동작하는지 확인하려면 `docker-compose ps`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="6c6a3-148">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="6c6a3-149">이제는 포트 80에서 VM에서 직접 WordPress에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="6c6a3-150">웹 브라우저를 열고 VM의 DNS 이름을 입력합니다(예: `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="6c6a3-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="6c6a3-151">이제 WordPress 시작 화면이 표시되면 이 화면에서 설치를 완료하고 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![WordPress 시작 화면][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="6c6a3-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c6a3-153">Next steps</span></span>
* <span data-ttu-id="6c6a3-154">Docker VM에서 Docker 및 Compose를 구성하는 더 많은 옵션을 보려면 [Docker VM 확장 사용자 가이드](https://github.com/Azure/azure-docker-extension/blob/master/README.md) 로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="6c6a3-155">예를 들어, 하나의 옵션은 Compose yml 파일(JSON으로 변환)을 직접 Docker VM 확장에 구성에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="6c6a3-156">다중 컨테이너 앱 빌드 및 배포의 추가 예제는 [Compose 명령줄 참조](http://docs.docker.com/compose/reference/) 및 [사용자 가이드](http://docs.docker.com/compose/)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="6c6a3-157">Azure 리소스 관리자 템플릿, 사용자 자신의 템플릿 또는 [커뮤니티](https://azure.microsoft.com/documentation/templates/)에서 배포된 템플릿을 사용하여, Azure VM을 Docker로 배포하고 Compose로 응용 프로그램을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="6c6a3-158">예를 들어 [Docker를 사용한 WordPress 블로그 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) 템플릿은 Docker 및 Compose를 사용하여 Ubuntu VM에 MySQL 백 엔드와 함께 WordPress를 신속하게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="6c6a3-159">Docker Swarm 클러스터와 Docker Compose 통합을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="6c6a3-160">시나리오의 경우 [Swarm으로 Compose 사용](https://docs.docker.com/compose/swarm/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6a3-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
