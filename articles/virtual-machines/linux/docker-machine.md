---
title: "Azure에서 호스트를 aaaUse Docker 컴퓨터 toocreate Linux | Microsoft Docs"
description: "Toouse Docker 컴퓨터 toocreate Docker Azure에서 호스팅하는 방법을 설명 합니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="2b2fd-103">Toouse Docker 컴퓨터 toocreate Azure에서 호스트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2b2fd-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="2b2fd-104">이 세부 정보를 어떻게 문서 toouse [Docker 컴퓨터](https://docs.docker.com/machine/) Azure의 toocreate 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="2b2fd-105">hello `docker-machine` 명령은 Azure에서 Linux 가상 컴퓨터 (VM)를 만든 다음 Docker를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="2b2fd-106">사용 하 여 Azure에서 Docker 호스트를 관리할 수 있습니다 동일한 로컬 도구 및 워크플로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="2b2fd-107">Docker Machine으로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2b2fd-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="2b2fd-108">먼저, 다음과 같이 [az 계정 표시](/cli/azure/account#show)로 Azure 구독 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="2b2fd-109">사용 하 여 Azure에서 Docker 호스트 Vm을 만들 `docker-machine create` 지정 하 여 *azure* hello 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="2b2fd-110">자세한 내용은 참조 hello [Docker Azure 드라이버 설명서](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="2b2fd-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="2b2fd-111">hello 다음 예제에서는 V *myVM*, 라는 사용자 계정을 만듭니다 *azureuser*, 포트 및 *80* VM 호스트 서버 hello에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="2b2fd-112">모든 프롬프트 toolog tooyour Azure 계정에에서 따라 및 Docker 컴퓨터 사용 권한 toocreate를 부여 하 고 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="2b2fd-113">hello 출력은 다음 예제와 비슷한 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-113">hello output looks similar toohello following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="2b2fd-114">Docker 셸 구성</span><span class="sxs-lookup"><span data-stu-id="2b2fd-114">Configure your Docker shell</span></span>
<span data-ttu-id="2b2fd-115">azure에서 tooconnect tooyour Docker 호스트에는 hello 적절 한 연결 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="2b2fd-116">Hello 출력의 hello 끝 부분에서 설명 했 듯이 Docker 호스트에 대 한 hello 연결 정보를 다음과 같이 보기:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="2b2fd-117">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="2b2fd-118">toodefine hello 연결 설정 중 하나가 실행된 hello 수 구성 명령을 제안 (`eval $(docker-machine env myvmdocker)`), 또는 hello 환경 변수를 수동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="2b2fd-119">컨테이너 실행</span><span class="sxs-lookup"><span data-stu-id="2b2fd-119">Run a container</span></span>
<span data-ttu-id="2b2fd-120">toosee 작업에서 컨테이너 기본 NGINX 웹 서버를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="2b2fd-121">`docker run`으로 컨테이너를 만들고 다음과 같이 웹 트래픽에 대해 포트 80을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="2b2fd-122">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="2b2fd-123">`docker ps`를 사용하여 실행 중인 컨테이너를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="2b2fd-124">hello 다음 예제에서는 출력에는 포트 80 노출 실행 하 고 hello NGINX 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="2b2fd-125">테스트 hello 컨테이너</span><span class="sxs-lookup"><span data-stu-id="2b2fd-125">Test hello container</span></span>
<span data-ttu-id="2b2fd-126">다음과 같이 hello Docker 호스트의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="2b2fd-127">toosee hello 컨테이너 작업에서 웹 브라우저를 열고 hello hello 명령 앞의 hello 출력에는 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![ngnix 컨테이너 실행](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="2b2fd-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b2fd-129">Next steps</span></span>
<span data-ttu-id="2b2fd-130">Hello로 호스트를 만들 수도 있습니다 [Docker VM 확장](dockerextension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="2b2fd-131">Docker Compose 사용에 대한 예제는 [Azure에서 Docker 및 Compose 시작](docker-compose-quickstart.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
