---
title: "Azure Container Instances 자습서 - Azure Container Registry 준비 | Microsoft Docs"
description: "Azure Container Instances 자습서 - Azure Container Registry 준비"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cc96ba9f5abd45a7503ba3327b30e1f809391384
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="f63cf-104">Azure Container Registry 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="f63cf-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="f63cf-105">세 부분으로 이루어진 자습서의 두 번째 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="f63cf-106">[이전 단계](./container-instances-tutorial-prepare-app.md)에서 [Node.js](http://nodejs.org)로 작성된 간단한 웹 응용 프로그램에 컨테이너 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-106">In the [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="f63cf-107">이 자습서에서는 이 이미지를 Azure Container Registry에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-107">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="f63cf-108">컨테이너 이미지를 만들지 않은 경우 [자습서 1 - 컨테이너 이미지 만들기](./container-instances-tutorial-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-108">If you have not created the container image, return to [Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="f63cf-109">Azure Container Registry는 Docker 컨테이너 이미지를 위한 Azure 기반의 개인 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-109">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="f63cf-110">이 자습서에서는 Azure Container Registry 인스턴스를 배포하고 컨테이너 이미지를 이 인스턴스에 밀어넣는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="f63cf-111">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f63cf-112">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="f63cf-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="f63cf-113">Azure Container Registry에 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="f63cf-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="f63cf-114">Azure Container Registry에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="f63cf-114">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="f63cf-115">후속 자습서에서는 Azure Container Instances에 개인 레지스트리의 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-115">In subsequent tutorials, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f63cf-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f63cf-116">Before you begin</span></span>

<span data-ttu-id="f63cf-117">이 자습서에는 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f63cf-118">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="f63cf-119">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f63cf-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="f63cf-120">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="f63cf-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="f63cf-121">Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="f63cf-122">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="f63cf-123">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f63cf-124">이 예제에서는 *eastus* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-124">In this example, a resource group named *myResourceGroup* is created in the *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f63cf-125">[az acr create](/cli/azure/acr#create) 명령으로 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="f63cf-126">컨테이너 레지스트리의 이름은 **고유해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="f63cf-126">The name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="f63cf-127">다음 예제에서는 *mycontainerregistry082*라는 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-127">In the following example, we use the name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="f63cf-128">이 자습서의 나머지 부분에서는 선택한 컨테이너 레지스트리 이름의 자리 표시자로 `<acrname>`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-128">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="f63cf-129">컨테이너 레지스트리 로그인</span><span class="sxs-lookup"><span data-stu-id="f63cf-129">Container registry login</span></span>

<span data-ttu-id="f63cf-130">ACR 인스턴스에 이미지를 밀어넣기 전에 먼저 ACR 인스턴스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-130">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="f63cf-131">[az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) 명령을 사용하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-131">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="f63cf-132">컨테이너 레지스트리가 생성될 때 지정된 고유한 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-132">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="f63cf-133">이 명령은 완료되면 ‘로그인했습니다.’ 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-133">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="f63cf-134">컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="f63cf-134">Tag container image</span></span>

<span data-ttu-id="f63cf-135">개인 레지스트리의 컨테이너 이미지를 배포하려면 이미지는 레지스트리 `loginServer` 이름으로 태그를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-135">To deploy a container image from a private registry, the image needs to be tagged with the `loginServer` name of the registry.</span></span>

<span data-ttu-id="f63cf-136">현재 이미지 목록을 보려면 `docker images` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-136">To see a list of current images, use the `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="f63cf-137">출력:</span><span class="sxs-lookup"><span data-stu-id="f63cf-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="f63cf-138">loginServer 이름을 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="f63cf-139">*aci-tutorial-app* 이미지에 컨테이너 레지스트리의 loginServer로 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-139">Tag the *aci-tutorial-app* image with the loginServer of the container registry.</span></span> <span data-ttu-id="f63cf-140">또한 이미지 이름 끝에 `:v1`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-140">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="f63cf-141">이 태그는 이미지 버전 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-141">This tag indicates the image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="f63cf-142">태그가 지정되면 `docker images`를 실행하여 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-142">Once tagged, run `docker images` to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="f63cf-143">출력:</span><span class="sxs-lookup"><span data-stu-id="f63cf-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="f63cf-144">Azure Container Registry에 이미지 푸시하기</span><span class="sxs-lookup"><span data-stu-id="f63cf-144">Push image to Azure Container Registry</span></span>

<span data-ttu-id="f63cf-145">*aci-tutorial-app* 이미지를 레지스트리에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-145">Push the *aci-tutorial-app* image to the registry.</span></span>

<span data-ttu-id="f63cf-146">다음 예제를 사용하여 컨테이너 레지스트리 loginServer 이름을 사용자 환경의 loginServer로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-146">Using the following example, replace the container registry loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="f63cf-147">Azure Container Registry에서 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="f63cf-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="f63cf-148">Azure Container Registry에 밀어넣은 이미지 목록을 반환하려면 [az acr repository list](/cli/azure/acr/repository#list) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-148">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="f63cf-149">이 명령을 컨테이너 레지스트리 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-149">Update the command with the container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="f63cf-150">출력:</span><span class="sxs-lookup"><span data-stu-id="f63cf-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="f63cf-151">그런 다음 특정 이미지에 대한 태그를 보려면 [az acr repository show-tags](/cli/azure/acr/repository#show-tags) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-151">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="f63cf-152">출력:</span><span class="sxs-lookup"><span data-stu-id="f63cf-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="f63cf-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f63cf-153">Next steps</span></span>

<span data-ttu-id="f63cf-154">이 자습서에서는 Azure Container Registry를 Azure Container Instances와 함께 사용하도록 준비하고 컨테이너 이미지를 푸시했습니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and the container image was pushed.</span></span> <span data-ttu-id="f63cf-155">다음 단계가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-155">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f63cf-156">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="f63cf-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="f63cf-157">Azure Container Registry에 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="f63cf-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="f63cf-158">Azure Container Registry에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="f63cf-158">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="f63cf-159">Azure Container Instances를 사용하여 컨테이너를 Azure에 배포하는 방법에 대해 자세히 알아보려면 다음 자습서를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="f63cf-159">Advance to the next tutorial to learn about deploying the container to Azure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f63cf-160">Azure Container Instances에 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="f63cf-160">Deploy containers to Azure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
