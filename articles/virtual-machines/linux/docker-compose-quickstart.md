---
title: "Azure에서 Linux VM의 Docker Compose aaaUse | Microsoft Docs"
description: "Docker toouse 및 작성 된 Linux 가상 컴퓨터에서 Azure CLI hello 방법"
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
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="03e18-103">Docker 및 작성 toodefine 시작 하 고 Azure에서 다중 컨테이너 응용 프로그램을 실행 가져오기</span><span class="sxs-lookup"><span data-stu-id="03e18-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="03e18-104">와 [Compose](http://github.com/docker/compose), 간단한 텍스트 파일 toodefine 여러 Docker 컨테이너 구성 된 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="03e18-105">그런 다음 모든 작업을 수행 하는 단일 명령으로 응용 프로그램을 회전 toodeploy 정의 된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="03e18-106">예를 들어,이 문서에서는 어떻게 tooquickly를 설정 하는 백엔드와 WordPress 블로그 MariaDB SQL 데이터베이스 Ubuntu VM에서.</span><span class="sxs-lookup"><span data-stu-id="03e18-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="03e18-107">더 복잡 한 응용 프로그램을 작성할 tooset를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="03e18-108">Docker 호스트로 Linux VM 설정</span><span class="sxs-lookup"><span data-stu-id="03e18-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="03e18-109">Hello Azure 마켓플레이스 toocreate Linux VM에서에서 다양 한 Azure 프로시저 및 제공 되는 이미지 또는 리소스 관리자 템플릿을 사용 하는 Docker 호스트를 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="03e18-110">예를 들어 참조 [hello Docker VM 확장 toodeploy 환경을 사용 하 여](dockerextension.md) tooquickly Ubuntu VM hello Azure Docker VM 확장 사용 하 여 작성는 [퀵 스타트 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="03e18-111">Hello Docker VM 확장을 사용 하면 Docker 호스트와 VM은 자동으로 설정 및 Compose가 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="03e18-112">Azure CLI 2.0을 사용하여 Docker 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="03e18-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="03e18-113">최신 설치 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="03e18-114">먼저 [az group create](/cli/azure/group#create)를 사용하여 Docker 환경에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="03e18-115">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westus* 위치:</span><span class="sxs-lookup"><span data-stu-id="03e18-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="03e18-116">다음에 사용 하 여 VM을 배포 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) hello Azure Docker VM 확장을 포함 하는 [GitHub에서이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="03e18-117">*newStorageAccountName*, *adminUsername*, *adminPassword* 및 *dnsNameForPublicIP*에 대한 고유한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="03e18-118">배포 toofinish hello에 대 한 몇 가지 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="03e18-119">응용 프로그램이 완료 되 면 hello 배포 [toonext 단계 이동](#verify-that-compose-is-installed) tooSSH tooyour VM입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="03e18-120">필요에 따라 hello 추가 tooinstead 반환 컨트롤 toohello 확인 및 let hello 배포 hello 백그라운드에서 계속 `--no-wait` toohello 명령 앞에 플래그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="03e18-121">이 프로세스 tooperform 수 있습니다. 몇 분 동안 계속 hello 배포 하는 동안 CLI hello에서 다른 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="03e18-122">와 hello Docker 호스트 상태에 대 한 세부 정보를 볼 수 있습니다 [az vm 표시](/cli/azure/vm#show)합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="03e18-123">hello 다음 예제에서는 hello의 상태를 검사 hello 라는 VM *myDockerVM* (hello hello 서식 파일에서 기본 이름-이 이름은 변경 하지 않는) 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="03e18-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="03e18-124">이 명령은 반환 하는 경우 *Succeeded*, hello 배포가 완료 되 고 단계 다음에 나오는 hello에 SSH toohello VM을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="03e18-125">Compose 설치 여부 확인</span><span class="sxs-lookup"><span data-stu-id="03e18-125">Verify that Compose is installed</span></span>
<span data-ttu-id="03e18-126">응용 프로그램이 완료 되 면 hello 배포 SSH tooyour 새 Docker 호스트 hello DNS 이름을 사용 하 여 제공한 배포 중입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="03e18-127">사용할 수 있습니다 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` hello DNS 이름을 포함 하 여 VM의 tooview 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="03e18-128">toocheck은 구성 하는 hello 다음 명령을 실행 하는 hello VM에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="03e18-129">비슷한 출력이 너무 표시*docker 작성 1.6.2, 4d 72027 빌드*합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="03e18-130">다른 메서드 toocreate Docker 호스트를 사용 하는 경우 필요한 tooinstall 작성 직접 참조 hello [설명서 작성](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="03e18-131">docker-compose.yml 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="03e18-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="03e18-132">다음 작업으로 만듭니다는 `docker-compose.yml` 텍스트 구성 파일, toodefine hello Docker 컨테이너 toorun hello VM에만 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="03e18-133">각 컨테이너에서 hello 이미지 toorun를 지정 하는 hello 파일 (또는 Dockerfile에서 빌드 수) 필요한 환경 변수 및 종속성, 포트 및 컨테이너 간 hello 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="03e18-134">yml 파일 구문에 대한 세부 정보는 [Compose 파일 참조](https://docs.docker.com/compose/compose-file/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03e18-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="03e18-135">Hello 만들기 *docker compose.yml* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="03e18-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="03e18-136">원하는 텍스트 편집기 tooadd 일부 데이터 toohello 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="03e18-137">hello 다음 예제에서는 hello *vi* 편집기:</span><span class="sxs-lookup"><span data-stu-id="03e18-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="03e18-138">Hello를 다음 예제에서는 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="03e18-139">이 구성은 hello에서 이미지를 사용 하 여 [DockerHub 레지스트리](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello 오픈 소스 블로깅 및 콘텐츠 관리 시스템) 및 연결 된 백 엔드 MariaDB SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="03e18-140">다음과 같이 고유한 *MYSQL_ROOT_PASSWORD*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="03e18-141">Compose 사용 하 여 hello 컨테이너 시작</span><span class="sxs-lookup"><span data-stu-id="03e18-141">Start hello containers with Compose</span></span>
<span data-ttu-id="03e18-142">동일 hello로 디렉터리에 *docker compose.yml* hello 다음 명령을 실행 파일 (사용자 환경에 따라 toorun 할 수 있습니다 `docker-compose` 를 사용 하 여 `sudo`):</span><span class="sxs-lookup"><span data-stu-id="03e18-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="03e18-143">이 명령은 hello Docker 컨테이너에 지정 된 시작 *docker compose.yml*합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="03e18-144">이 단계 toocomplete에 대 일 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="03e18-145">다음 예제 출력 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="03e18-146">수 있는지 toouse hello **-d** hello 컨테이너 hello 백그라운드에서 계속 실행 되도록 시작 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="03e18-147">hello 컨테이너는, tooverify 형식 `docker-compose ps`합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="03e18-148">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="03e18-149">TooWordPress hello 포트 80에서 VM에 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="03e18-150">웹 브라우저를 열고 VM의 DNS 이름을 hello 입력 (예: `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="03e18-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="03e18-151">이제 WordPress 시작 화면, hello 설치를 완료할 수 있습니다 및 hello 응용 프로그램을 시작 하는 hello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![WordPress 시작 화면][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="03e18-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03e18-153">Next steps</span></span>
* <span data-ttu-id="03e18-154">Toohello 이동 [Docker VM extension 사용자 가이드](https://github.com/Azure/azure-docker-extension/blob/master/README.md) 더 많은 옵션 tooconfigure Docker 및 Docker VM에서 Compose에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="03e18-155">예를 들어, 한 가지 옵션은 hello Docker VM 확장의 hello 구성에 직접 tooput hello Compose yml 파일 (변환 된 tooJSON).</span><span class="sxs-lookup"><span data-stu-id="03e18-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="03e18-156">체크 아웃 hello [명령줄 참조 작성](http://docs.docker.com/compose/reference/) 및 [사용자 가이드](http://docs.docker.com/compose/) 다중 컨테이너 앱 빌드 및 배포의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="03e18-157">중 하나는 Azure 리소스 관리자 템플릿을 사용 하 여 사용자 고유의 또는 하나 hello에서 제공 됩니다 [커뮤니티](https://azure.microsoft.com/documentation/templates/), toodeploy Docker 및 응용 프로그램으로 Azure VM Compose를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="03e18-158">예를 들어 hello [Docker가 있는 WordPress 블로그 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) 템플릿은 Docker를 사용 하 여 및 Compose tooquickly Ubuntu VM에서 MySQL 백 엔드를 사용 하 여 WordPress를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="03e18-159">Docker Swarm 클러스터와 Docker Compose 통합을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="03e18-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="03e18-160">시나리오의 경우 [Swarm으로 Compose 사용](https://docs.docker.com/compose/swarm/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03e18-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
