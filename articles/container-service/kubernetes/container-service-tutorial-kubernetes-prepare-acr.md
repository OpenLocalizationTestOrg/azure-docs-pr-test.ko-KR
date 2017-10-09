---
title: "aaaAzure 컨테이너 서비스 자습서-ACR 준비 | Microsoft Docs"
description: "Azure Container Service 자습서 - ACR 준비"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="4b1ac-104">Azure Container Registry 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="4b1ac-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="4b1ac-105">ACR(Azure Container Registry)은 Docker 컨테이너 이미지를 위한 Azure 기반의 개인 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="4b1ac-106">이 자습서를 통해 Azure 컨테이너 레지스트리 인스턴스 배포 하 고 컨테이너 이미지 tooit 푸시하여 7, 워크의 파트 2입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="4b1ac-107">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b1ac-108">ACR(Azure Container Registry) 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="4b1ac-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="4b1ac-109">ACR에 대한 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="4b1ac-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="4b1ac-110">Hello 이미지 tooACR를 업로드 하는 중</span><span class="sxs-lookup"><span data-stu-id="4b1ac-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="4b1ac-111">이후 자습서에서는 컨테이너 이미지를 안전하게 실행하기 위해 이 ACR 인스턴스를 Azure Container Service Kubernetes 클러스터와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4b1ac-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4b1ac-112">Before you begin</span></span>

<span data-ttu-id="4b1ac-113">Hello에 [이전 자습서](./container-service-tutorial-kubernetes-prepare-app.md), 간단한 Azure 투표 응용 프로그램에 대 한 컨테이너 이미지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="4b1ac-114">이 자습서에서는이 이미지는 Azure 컨테이너 레지스트리 tooan이 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="4b1ac-115">Hello Azure 투표 앱 이미지를 만들지 않은 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="4b1ac-116">또는 hello 단계 여기에서 자세히 설명 된 컨테이너 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="4b1ac-117">이 자습서에서는 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4b1ac-118">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4b1ac-119">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="4b1ac-120">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="4b1ac-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="4b1ac-121">Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="4b1ac-122">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4b1ac-123">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4b1ac-124">이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에서 만든 *westeurope* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="4b1ac-125">Azure 컨테이너 레지스트리 hello로 만들기 [az acr 만들기](/cli/azure/acr#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="4b1ac-126">컨테이너 레지스트리의 hello 이름 **고유 해야**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="4b1ac-127">이 자습서의 나머지에서는 hello 통해 "acrname" 자리 표시자로를 위해 사용 hello 컨테이너 레지스트리 선택한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="4b1ac-128">컨테이너 레지스트리 로그인</span><span class="sxs-lookup"><span data-stu-id="4b1ac-128">Container registry login</span></span>

<span data-ttu-id="4b1ac-129">이미지 tooit 푸시하기 전에 tooyour ACR 인스턴스 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="4b1ac-130">사용 하 여 hello [az acr 로그인](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello 작업 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="4b1ac-131">Tooprovide hello 고유한 이름을 만들 때 toohello 컨테이너 레지스트리를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="4b1ac-132">hello 명령은 완료 되 면 로그인 성공 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="4b1ac-133">컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="4b1ac-133">Tag container images</span></span>

<span data-ttu-id="4b1ac-134">각 컨테이너 이미지 필요 toobe hello 레지스트리 hello loginServer 이름의 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="4b1ac-135">이 태그는 컨테이너 이미지 tooan 이미지 레지스트리 푸시할 때 다음 라우팅에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="4b1ac-136">현재 이미지를 사용 하 여 hello 목록이 toosee [docker 이미지](https://docs.docker.com/engine/reference/commandline/images/) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="4b1ac-137">출력:</span><span class="sxs-lookup"><span data-stu-id="4b1ac-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="4b1ac-138">tooget hello loginServer 이름 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="4b1ac-139">이제 태그 hello *azure 투표 프런트* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="4b1ac-140">또한 추가 `:redis-v1` hello 이미지 이름의 toohello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="4b1ac-141">이 태그는 hello 이미지 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="4b1ac-142">태그가 지정 되 면 [docker 이미지] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="4b1ac-143">출력:</span><span class="sxs-lookup"><span data-stu-id="4b1ac-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="4b1ac-144">이미지 tooregistry 푸시</span><span class="sxs-lookup"><span data-stu-id="4b1ac-144">Push images tooregistry</span></span>

<span data-ttu-id="4b1ac-145">Hello 푸시 *azure 투표 프런트* 이미지 toohello 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="4b1ac-146">다음 예제는 hello를 사용 하 여 hello ACR loginServer 이름을 사용자 환경에서 hello loginServer로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="4b1ac-147">이 작업은 몇 분 toocomplete입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="4b1ac-148">레지스트리에서 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="4b1ac-148">List images in registry</span></span>

<span data-ttu-id="4b1ac-149">tooreturn tooyour Azure 컨테이너 레지스트리에 사용자 hello 밀어 넣은 이미지 목록 [az acr 리포지토리 목록](/cli/azure/acr/repository#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="4b1ac-150">Hello 명령 hello ACR 인스턴스 이름으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="4b1ac-151">출력:</span><span class="sxs-lookup"><span data-stu-id="4b1ac-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="4b1ac-152">다음 toosee hello 태그 특정 이미지를 사용 하 여 hello [az acr 리포지토리 표시 태그](/cli/azure/acr/repository#show-tags) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="4b1ac-153">출력:</span><span class="sxs-lookup"><span data-stu-id="4b1ac-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="4b1ac-154">자습서 완료 시 hello 컨테이너 이미지 전용 Azure 컨테이너 레지스트리 인스턴스에 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="4b1ac-155">이 이미지는 이후 자습서에서 ACR tooa Kubernetes 클러스터에서 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b1ac-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b1ac-156">Next steps</span></span>

<span data-ttu-id="4b1ac-157">이 자습서에서는 ACS Kubernetes 클러스터에서 사용하기 위해 Azure Container Registry를 준비했습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="4b1ac-158">단계를 수행 하는 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b1ac-159">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="4b1ac-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="4b1ac-160">ACR에 대한 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="4b1ac-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="4b1ac-161">업로드 된 hello 이미지 tooACR</span><span class="sxs-lookup"><span data-stu-id="4b1ac-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="4b1ac-162">Azure에서 Kubernetes 클러스터를 배포 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1ac-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b1ac-163">Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="4b1ac-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)