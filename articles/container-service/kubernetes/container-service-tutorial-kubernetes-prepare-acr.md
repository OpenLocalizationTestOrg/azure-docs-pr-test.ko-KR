---
title: "Azure Container Service 자습서 - ACR 준비 | Microsoft Docs"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="95736-104">Azure Container Registry 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="95736-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="95736-105">ACR(Azure Container Registry)은 Docker 컨테이너 이미지를 위한 Azure 기반의 개인 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="95736-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="95736-106">일곱 가지 중에 두 번째인 이 자습서에서는 Azure Container Registry 인스턴스를 배포하고 컨테이너 이미지를 이 인스턴스에 밀어넣는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="95736-107">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95736-108">ACR(Azure Container Registry) 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="95736-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="95736-109">ACR에 대한 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="95736-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="95736-110">ACR에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="95736-110">Uploading the image to ACR</span></span>

<span data-ttu-id="95736-111">이후 자습서에서는 컨테이너 이미지를 안전하게 실행하기 위해 이 ACR 인스턴스를 Azure Container Service Kubernetes 클러스터와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="95736-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="95736-112">Before you begin</span></span>

<span data-ttu-id="95736-113">[이전 자습서](./container-service-tutorial-kubernetes-prepare-app.md)에서는 간단한 Azure Voting 응용 프로그램에 컨테이너 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="95736-114">이 자습서에서는 이 이미지를 Azure Container Registry에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="95736-115">Azure Voting 앱 이미지를 만들지 않은 경우 [자습서 1 - 컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="95736-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="95736-116">또는 여기에 자세히 설명된 단계는 모든 컨테이너 이미지와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="95736-117">이 자습서에는 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="95736-118">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="95736-119">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95736-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="95736-120">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="95736-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="95736-121">Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="95736-122">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="95736-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="95736-123">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95736-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="95736-124">이 예제에서는 *westeurope* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95736-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="95736-125">[az acr create](/cli/azure/acr#create) 명령으로 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95736-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="95736-126">컨테이너 레지스트리의 이름은 **고유해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="95736-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="95736-127">이 자습서의 나머지 부분에서는 선택한 컨테이너 레지스트리 이름의 자리 표시자로 "acrname"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="95736-128">컨테이너 레지스트리 로그인</span><span class="sxs-lookup"><span data-stu-id="95736-128">Container registry login</span></span>

<span data-ttu-id="95736-129">ACR 인스턴스에 이미지를 밀어넣기 전에 먼저 ACR 인스턴스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="95736-130">[az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) 명령을 사용하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="95736-131">컨테이너 레지스트리가 생성될 때 지정된 고유한 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="95736-132">이 명령은 완료되면 ‘로그인했습니다.’ 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="95736-133">컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="95736-133">Tag container images</span></span>

<span data-ttu-id="95736-134">각 컨테이너 이미지에 레지스트리의 loginServer 이름으로 태그를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="95736-135">이 태그는 컨테이너 이미지를 이미지 레지스트리에 밀어넣을 때 라우팅에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95736-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="95736-136">현재 이미지 목록을 보려면 [docker images](https://docs.docker.com/engine/reference/commandline/images/) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="95736-137">출력:</span><span class="sxs-lookup"><span data-stu-id="95736-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="95736-138">loginServer 이름을 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="95736-139">이제 *azure-vote-front* 이미지에 컨테이너 레지스트리의 loginServer로 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="95736-140">또한 이미지 이름 끝에 `:redis-v1`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="95736-141">이 태그는 이미지 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95736-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="95736-142">태그가 지정되면 [docker images](https://docs.docker.com/engine/reference/commandline/images/)를 실행하여 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="95736-143">출력:</span><span class="sxs-lookup"><span data-stu-id="95736-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="95736-144">레지스트리에 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="95736-144">Push images to registry</span></span>

<span data-ttu-id="95736-145">레지스트리에 *azure-vote-front* 이미지를 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="95736-146">다음 예제를 사용하여 ACR loginServer 이름을 해당 환경의 loginServer로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95736-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="95736-147">이 작업은 완료되는 데 2~3분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="95736-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="95736-148">레지스트리에서 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="95736-148">List images in registry</span></span>

<span data-ttu-id="95736-149">Azure Container Registry에 밀어넣은 이미지 목록을 반환하려면 [az acr repository list](/cli/azure/acr/repository#list) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="95736-150">ACR 인스턴스 이름으로 명령을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="95736-151">출력:</span><span class="sxs-lookup"><span data-stu-id="95736-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="95736-152">그런 다음 특정 이미지에 대한 태그를 보려면 [az acr repository show-tags](/cli/azure/acr/repository#show-tags) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95736-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="95736-153">출력:</span><span class="sxs-lookup"><span data-stu-id="95736-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="95736-154">자습서를 완료하면 개인 Azure Container Registry 인스턴스에 컨테이너 이미지가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="95736-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="95736-155">이후 자습서에서 이 이미지는 ACR에서 Kubernetes 클러스터로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="95736-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95736-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95736-156">Next steps</span></span>

<span data-ttu-id="95736-157">이 자습서에서는 ACS Kubernetes 클러스터에서 사용하기 위해 Azure Container Registry를 준비했습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="95736-158">다음 단계가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95736-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95736-159">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="95736-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="95736-160">ACR에 대한 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="95736-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="95736-161">ACR에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="95736-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="95736-162">다음 자습서로 이동하여 Azure에서 Kubernetes 클러스터 배포에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="95736-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95736-163">Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="95736-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)