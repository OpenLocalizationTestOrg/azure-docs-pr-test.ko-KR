---
title: "Azure DC/OS 클러스터와 ACR aaaUsing | Microsoft Docs"
description: "Azure Container Service에서 DC/OS 클러스터에 Azure Container Registry 사용"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="28d81-104">ACR DC/OS 클러스터 toodeploy와 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="28d81-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="28d81-105">탐색이 문서에서는 어떻게 DC/OS 클러스터와 Azure 컨테이너 레지스트리 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="28d81-106">ACR을 사용 하 여 컨테이너 이미지를 관리 및 tooprivately 저장소 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="28d81-107">이 자습서에서는 hello 다음 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28d81-108">Azure Container Registry 배포(필요한 경우)</span><span class="sxs-lookup"><span data-stu-id="28d81-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="28d81-109">DC/OS 클러스터에서 ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="28d81-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="28d81-110">이미지 toohello Azure 컨테이너 레지스트리 업로드</span><span class="sxs-lookup"><span data-stu-id="28d81-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="28d81-111">Azure 컨테이너 레지스트리 hello에서 컨테이너 이미지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="28d81-112">ACS DC/OS 클러스터 toocomplete hello이이 자습서의 단계를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="28d81-113">필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="28d81-114">이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상.</span><span class="sxs-lookup"><span data-stu-id="28d81-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="28d81-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="28d81-116">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="28d81-117">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="28d81-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="28d81-118">필요한 경우 Azure 컨테이너 레지스트리 hello로 만들 [az acr 만들기](/cli/azure/acr#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="28d81-119">hello 다음 예제에서는 사용 하 여 레지스트리를는 이름을 임의로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="28d81-120">hello 레지스트리 hello를 사용 하 여 관리자 계정으로도 구성 된 `--admin-enabled` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="28d81-121">Hello 레지스트리를 만든 후 Azure CLI hello 비슷한 toohello 다음 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="28d81-122">Hello를 메모해 `name` 및 `loginServer`, 이후 단계에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="28d81-123">Hello 컨테이너 레지스트리 자격 증명 hello를 사용 하 여 가져오기 [az acr 자격 증명 표시](/cli/azure/acr/credential) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="28d81-124">대체 hello `--name` hello 마지막 단계에서 기록한 하나 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="28d81-125">이후 단계에서 필요하므로 하나의 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="28d81-126">Azure 컨테이너 레지스트리에 대 한 자세한 내용은 참조 하십시오. [소개 tooprivate Docker 컨테이너 레지스트리에](../../container-registry/container-registry-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="28d81-127">ACR 인증 관리</span><span class="sxs-lookup"><span data-stu-id="28d81-127">Manage ACR authentication</span></span>

<span data-ttu-id="28d81-128">개인 레지스트리에서 toopush 및 끌어오기 이미지는 toofirst hello 편리한 방법 hello 레지스트리를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="28d81-129">toodo hello를 사용 합니다, `docker login` tooaccess hello 개인 등록 해야 하는 모든 클라이언트에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="28d81-130">DC/OS 클러스터 노드가 여러 개인 경우 toobe ACR hello를 사용 하 여 인증을 해야는 모두 포함 될 수 있으므로 유용한 tooautomate이이 프로세스에서에서 각 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="28d81-131">공유 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="28d81-131">Create shared storage</span></span>

<span data-ttu-id="28d81-132">이 프로세스는 hello 클러스터의 각 노드에서 탑재 된 경우 Azure 파일 공유를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="28d81-133">아직 공유 저장소를 설정하지 않은 경우 [DC/OS 클러스터 내부에서 파일 공유 설정](container-service-dcos-fileshare.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28d81-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="28d81-134">ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="28d81-134">Configure ACR authentication</span></span>

<span data-ttu-id="28d81-135">먼저, hello를 hello DC/OS 마스터 및 변수에 저장의 FQDN을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="28d81-136">DC/OS 기반 클러스터의 hello 마스터 (또는 hello 첫 번째 마스터)에 대 한 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="28d81-137">기본값이 아닌 값 hello 클러스터를 만들 때 사용 된 경우 hello 사용자 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="28d81-138">다음 명령 toologin toohello Azure 컨테이너 레지스트리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="28d81-139">Hello 대체 `--username` hello 컨테이너 레지스트리 및 hello hello 이름의 `--password` hello 제공 된 암호 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="28d81-140">마지막 인수 hello *mycontainerregistry.azurecr.io* hello 컨테이너 레지스트리 hello loginServer 이름의 hello 예제에서입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="28d81-141">이 명령은 hello 인증 값 hello에서 로컬로 저장 `~/.docker` 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="28d81-142">Hello 컨테이너 레지스트리 인증 값이 포함 된 압축된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="28d81-143">이 파일 toohello 클러스터 공유 저장소에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="28d81-144">이 단계를 수행 하면 hello 파일 hello DC/OS 클러스터의 모든 노드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="28d81-145">이미지 tooACR 업로드</span><span class="sxs-lookup"><span data-stu-id="28d81-145">Upload image tooACR</span></span>

<span data-ttu-id="28d81-146">이제 개발 컴퓨터 또는 설치 하는 Docker가 있는 다른 시스템에서 이미지 만들기와 toohello Azure 컨테이너 레지스트리 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="28d81-147">Hello Ubuntu 이미지에서 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="28d81-148">이제 새 이미지로 hello 컨테이너를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="28d81-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="28d81-149">hello 이미지 이름 필요한 tooinclude hello `loginServer` hello 컨테이너 registrywith의 형식 이름 `loginServer/imageName`합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="28d81-150">Azure 컨테이너 레지스트리 hello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="28d81-151">Hello 이름을 hello loginServer 이름으로 바꿉니다, 그리고 hello-hello 컨테이너 레지스트리 및 hello-hello 제공 된 암호 중 하나에 포함 된 암호의 hello 이름으로 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="28d81-152">Hello 이미지 toohello ACR 레지스트리를 마지막으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="28d81-153">이 예제에서는 dcos-demo라는 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="28d81-154">ACR에서 이미지 실행</span><span class="sxs-lookup"><span data-stu-id="28d81-154">Run an image from ACR</span></span>

<span data-ttu-id="28d81-155">toouse hello ACR 레지스트리에서 이미지 파일 이름을 만들 *acrDemo.json* 복사 hello에 텍스트를 다음 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="28d81-156">예를 들어 hello 이미지 이름을 hello 컨테이너 레지스트리 loginServer 이름 및 이미지 이름으로 대체 `loginServer/imageName`합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="28d81-157">Hello를 메모해 `uris` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="28d81-158">Hello hello 컨테이너 레지스트리 인증 파일 위치 hello DC/OS 클러스터의 각 노드에서 탑재 된 hello Azure 파일 공유에이 경우에이 속성을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="28d81-159">DC/OC CLI hello로 hello 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="28d81-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28d81-160">Next steps</span></span>

<span data-ttu-id="28d81-161">이 자습서에서 DC/OS toouse hello 다음을 포함 하 여 Azure 컨테이너 레지스트리 작업을 구성할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28d81-162">Azure Container Registry 배포(필요한 경우)</span><span class="sxs-lookup"><span data-stu-id="28d81-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="28d81-163">DC/OS 클러스터에서 ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="28d81-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="28d81-164">이미지 toohello Azure 컨테이너 레지스트리 업로드</span><span class="sxs-lookup"><span data-stu-id="28d81-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="28d81-165">Azure 컨테이너 레지스트리 hello에서 컨테이너 이미지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d81-165">Run a container image from hello Azure Container Registry</span></span>
