---
title: "Docker Machine으로 Azure에서 Docker 호스트 만들기 | Microsoft Docs"
description: "Docker Machine을 사용하여 Azure에서 Docker 호스트를 만드는 방법에 대해 설명합니다."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="3ffa6-103">Docker Machine으로 Azure에서 Docker 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="3ffa6-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="3ffa6-104">[Docker](https://www.docker.com/) 컨테이너를 실행하려면 호스트 VM이 docker 데몬을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="3ffa6-105">이 항목에서는 Docker 데몬과 함께 구성된, Azure에서 실행되는 새 Linux VM을 만들기 위해 [docker-machine](https://docs.docker.com/machine/) 명령을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="3ffa6-106">**참고:**</span><span class="sxs-lookup"><span data-stu-id="3ffa6-106">**Note:**</span></span> 

* <span data-ttu-id="3ffa6-107">*이 문서는 docker-machine 버전 0.9.0-rc2 이상에 따라 달라집니다.*</span><span class="sxs-lookup"><span data-stu-id="3ffa6-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="3ffa6-108">*가까운 미래에 Windows 컨테이너가 docker-machine을 통해 지원될 예정입니다.*</span><span class="sxs-lookup"><span data-stu-id="3ffa6-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="3ffa6-109">Docker Machine으로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3ffa6-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="3ffa6-110">`azure` 드라이버를 사용한 `docker-machine create` 명령으로 Azure에서 Docker 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="3ffa6-111">Azure 드라이버에는 구독 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="3ffa6-112">[Azure CLI](cli-install-nodejs.md) 또는 [Azure Portal](https://portal.azure.com)을 사용하여 Azure 구독을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="3ffa6-113">**Azure 포털 사용**</span><span class="sxs-lookup"><span data-stu-id="3ffa6-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="3ffa6-114">왼쪽 탐색 페이지에서 **구독**을 선택하고, 구독 ID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="3ffa6-115">**Azure CLI 사용**</span><span class="sxs-lookup"><span data-stu-id="3ffa6-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="3ffa6-116">```azure account list``` 을 입력하고 구독 ID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="3ffa6-117">옵션과 해당 옵션의 기본값을 보려면 `docker-machine create --driver azure` 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="3ffa6-118">또한 자세한 내용은 [Docker Azure 드라이버 설명서](https://docs.docker.com/machine/drivers/azure/) 를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="3ffa6-119">다음 예제는 [기본값](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22)을 사용하지만 선택적으로 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="3ffa6-120">공용 IP 및 생성된 인증서와 연결된 이름의 경우 azure-dns.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="3ffa6-121">가상 컴퓨터의 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="3ffa6-122">그러면 VM이 안전하게 중지하고 동적 IP를 해제하며 VM이 새 IP로 다시 시작된 후 다시 연결하는 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="3ffa6-123">이름 접두사는 해당 영역 UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="3ffa6-124">아웃 바운드 인터넷 액세스를 위한 VM의 개방 포트 80</span><span class="sxs-lookup"><span data-stu-id="3ffa6-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="3ffa6-125">더 빠른 Premium Storage를 활용할 수 있는 VM 크기</span><span class="sxs-lookup"><span data-stu-id="3ffa6-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="3ffa6-126">VM 디스크에 사용하는 Premium Storage</span><span class="sxs-lookup"><span data-stu-id="3ffa6-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="3ffa6-127">Docker-machine으로 docker 호스트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="3ffa6-128">호스트에 대해 docker-machine에 항목이 있다면, docker 명령을 실행할 때 기본 호스트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="3ffa6-129">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="3ffa6-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="3ffa6-130">Bash 사용</span><span class="sxs-lookup"><span data-stu-id="3ffa6-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="3ffa6-131">이제 지정된 호스트에 대해 docker 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="3ffa6-132">컨테이너 실행</span><span class="sxs-lookup"><span data-stu-id="3ffa6-132">Run a container</span></span>
<span data-ttu-id="3ffa6-133">호스트 구성을 마치면, 이제 간단한 웹 서버를 실행하여 호스트가 올바르게 구성되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="3ffa6-134">여기서는 표준 nginx 이미지를 사용하고 포트 80에서 수신 대기하도록 지정하며 호스트 VM이 다시 시작될 경우 컨테이너도 다시 시작합니다(`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="3ffa6-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="3ffa6-135">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="3ffa6-136">컨테이너 테스트</span><span class="sxs-lookup"><span data-stu-id="3ffa6-136">Test the container</span></span>
<span data-ttu-id="3ffa6-137">`docker ps`를 사용하여 실행 중인 컨테이너 검사</span><span class="sxs-lookup"><span data-stu-id="3ffa6-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="3ffa6-138">또한 실행 중인 컨테이너를 확인하려면 `docker-machine ip <VM name>`을 입력하여 브라우저에 입력할 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![ngnix 컨테이너 실행](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="3ffa6-140">요약</span><span class="sxs-lookup"><span data-stu-id="3ffa6-140">Summary</span></span>
<span data-ttu-id="3ffa6-141">docker-machine을 사용하면 개별 docker 호스트 유효성 검사를 위해 Azure에서 docker 호스트를 쉽게 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffa6-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="3ffa6-142">컨테이너의 프로덕션 호스팅은 [Azure 컨테이너 서비스](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="3ffa6-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="3ffa6-143">Visual Studio를 사용한 .NET 핵심 응용 프로그램 개발은 [Visual Studio 용 Docker 도구](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="3ffa6-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

