---
title: "aaaAzure 컨테이너 인스턴스 자습서-Azure 컨테이너 레지스트리 준비 | Microsoft Docs"
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
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="07426-104">Azure Container Registry 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="07426-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="07426-105">세 부분으로 이루어진 자습서의 두 번째 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="07426-106">Hello에 [이전 단계](./container-instances-tutorial-prepare-app.md), 컨테이너 이미지를 작성 하는 간단한 웹 응용 프로그램에 대해 만들어진 [Node.js](http://nodejs.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="07426-107">이 자습서에서는이 이미지는 Azure 컨테이너 레지스트리 tooan이 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07426-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="07426-108">Hello 컨테이너 이미지를 만들지 않은 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-instances-tutorial-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="07426-109">Azure 컨테이너 레지스트리 hello Docker 컨테이너 이미지에 대 한 Azure 기반, 사설 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="07426-110">이 자습서는 Azure 컨테이너 레지스트리 인스턴스 배포 하 고 컨테이너 이미지 tooit 푸시하여 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="07426-111">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07426-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07426-112">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="07426-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="07426-113">Azure Container Registry에 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="07426-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="07426-114">이미지 tooAzure 컨테이너 레지스트리를 업로드 하는 중</span><span class="sxs-lookup"><span data-stu-id="07426-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="07426-115">이후 자습서에서 사용자 개인 레지스트리 tooAzure 컨테이너 인스턴스 hello 컨테이너를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="07426-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="07426-116">Before you begin</span></span>

<span data-ttu-id="07426-117">이 자습서에서는 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="07426-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="07426-118">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="07426-119">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="07426-120">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="07426-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="07426-121">Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="07426-122">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="07426-123">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="07426-124">이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에서 만든 *eastus* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="07426-125">Azure 컨테이너 레지스트리 hello로 만들기 [az acr 만들기](/cli/azure/acr#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="07426-126">컨테이너 레지스트리의 hello 이름 **고유 해야**합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="07426-127">다음 예제는 hello를 사용 하 여 hello 이름 *mycontainerregistry082*합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="07426-128">이 자습서의 나머지에서는 hello 전체에서 사용 하 여 `<acrname>` 선택한 hello 컨테이너 레지스트리 이름에 대 한 자리 표시자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="07426-129">컨테이너 레지스트리 로그인</span><span class="sxs-lookup"><span data-stu-id="07426-129">Container registry login</span></span>

<span data-ttu-id="07426-130">이미지 tooit 푸시하기 전에 tooyour ACR 인스턴스 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="07426-131">사용 하 여 hello [az acr 로그인](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello 작업 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="07426-132">Tooprovide hello 고유한 이름을 만들 때 toohello 컨테이너 레지스트리를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="07426-133">hello 명령은 완료 되 면 로그인 성공 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="07426-134">컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="07426-134">Tag container image</span></span>

<span data-ttu-id="07426-135">컨테이너 이미지 전용 레지스트리에서 toodeploy hello 이미지 필요 hello로 태그가 지정 된 toobe `loginServer` hello 레지스트리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="07426-136">현재 이미지를 사용 하 여 hello 목록이 toosee `docker images` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="07426-137">출력:</span><span class="sxs-lookup"><span data-stu-id="07426-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="07426-138">tooget hello loginServer 이름 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="07426-139">태그 hello *aci 자습서 앱* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="07426-140">또한 추가 `:v1` hello 이미지 이름의 toohello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="07426-141">이 태그는 hello 이미지 버전 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="07426-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="07426-142">태그가 지정 되 면 실행 `docker images` tooverify hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="07426-143">출력:</span><span class="sxs-lookup"><span data-stu-id="07426-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="07426-144">푸시 이미지 tooAzure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="07426-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="07426-145">Hello 푸시 *aci 자습서 앱* 이미지 toohello 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="07426-146">다음 예제는 hello를 사용 하 여 hello 컨테이너 레지스트리 loginServer 이름을 사용자 환경에서 hello loginServer로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07426-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="07426-147">Azure Container Registry에서 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="07426-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="07426-148">tooreturn tooyour Azure 컨테이너 레지스트리에 사용자 hello 밀어 넣은 이미지 목록 [az acr 리포지토리 목록](/cli/azure/acr/repository#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="07426-149">Hello 명령 hello 컨테이너 레지스트리 이름으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="07426-150">출력:</span><span class="sxs-lookup"><span data-stu-id="07426-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="07426-151">다음 toosee hello 태그 특정 이미지를 사용 하 여 hello [az acr 리포지토리 표시 태그](/cli/azure/acr/repository#show-tags) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07426-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="07426-152">출력:</span><span class="sxs-lookup"><span data-stu-id="07426-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="07426-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07426-153">Next steps</span></span>

<span data-ttu-id="07426-154">이 자습서에서는 Azure 컨테이너 레지스트리 Azure 컨테이너 인스턴스를 사용 하도록 준비 된 하 고 hello 컨테이너 이미지에 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07426-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="07426-155">단계를 수행 하는 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07426-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07426-156">Azure Container Registry 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="07426-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="07426-157">Azure Container Registry에 컨테이너 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="07426-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="07426-158">이미지 tooAzure 컨테이너 레지스트리를 업로드 하는 중</span><span class="sxs-lookup"><span data-stu-id="07426-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="07426-159">Azure 컨테이너 인스턴스를 사용 하 여 hello 컨테이너 tooAzure 배포에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07426-160">컨테이너 tooAzure 컨테이너 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="07426-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
