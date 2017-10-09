---
title: "aaaAzure 컨테이너 서비스 자습서-앱 준비 | Microsoft Docs"
description: "Azure Container Service 자습서 - 앱 준비"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="c6618-104">Azure 컨테이너 서비스와 함께 사용할 컨테이너 이미지 toobe 만들기</span><span class="sxs-lookup"><span data-stu-id="c6618-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="c6618-105">7개 중 1단계인 이 자습서에서는 Kubernetes에서 사용할 수 있도록 다중 컨테이너 응용 프로그램을 준비하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="c6618-106">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="c6618-107">GitHub에서 응용 프로그램 소스 복제</span><span class="sxs-lookup"><span data-stu-id="c6618-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="c6618-108">Hello 응용 프로그램 소스에서 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c6618-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="c6618-109">로컬 Docker 환경에서 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c6618-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="c6618-110">완료 되 면 hello 다음 응용 프로그램은 로컬 개발 환경에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="c6618-112">이후 자습서 hello 컨테이너 이미지는 업로드 된 tooan Azure 컨테이너 레지스트리 하 고 Azure에서 실행 Kubernetes 클러스터를 호스트 하는 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c6618-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c6618-113">Before you begin</span></span>

<span data-ttu-id="c6618-114">이 자습서에서는 컨테이너, 컨테이너 이미지 및 기본 Docker 명령과 같은 핵심 Docker 개념에 대한 기본적인 지식이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="c6618-115">필요한 경우 컨테이너 기본 사항에 대한 입문서는 [Get started with Docker(Docker 시작)]( https://docs.docker.com/get-started/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6618-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="c6618-116">toocomplete이이 자습서에서는 Docker 개발 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="c6618-117">Docker는 모든 [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) 또는 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 시스템에서 쉽게 Docker를 구성하는 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="c6618-118">응용 프로그램 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="c6618-118">Get application code</span></span>

<span data-ttu-id="c6618-119">이 자습서에 사용 된 hello 샘플 응용 프로그램은 기본 투표 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="c6618-120">hello 응용 프로그램 웹 프런트 엔드 구성 요소 및 백 엔드 Redis 인스턴스에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="c6618-121">hello 웹 구성 요소는 사용자 지정 컨테이너 이미지에 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="c6618-122">hello Redis 인스턴스 Docker 허브에서 수정 되지 않은 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="c6618-123">Git toodownload hello 응용 프로그램 tooyour 개발 환경의 복사본을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="c6618-124">내부 hello에 대 한 복제 된 디렉터리는 hello 응용 프로그램 소스 코드, 미리 생성된 된 Docker 파일과 Kubernetes 매니페스트 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="c6618-125">이러한 파일은 hello 자습서 집합에서 사용 되는 toocreate 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="c6618-126">컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c6618-126">Create container images</span></span>

<span data-ttu-id="c6618-127">[Docker Compose](https://docs.docker.com/compose/) 수 tooautomate hello 빌드 컨테이너 이미지와 hello 다중 컨테이너 응용 프로그램 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="c6618-128">Hello docker compose.yml 파일 toocreate hello 컨테이너 이미지를 실행 다운로드 hello 이미지, Redis 하 고 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="c6618-129">완료 되 면 hello를 사용 하 여 [docker 이미지](https://docs.docker.com/engine/reference/commandline/images/) toosee hello 만든 이미지 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="c6618-130">세 개의 이미지가 다운로드되거나 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="c6618-131">hello *azure 투표 프런트* 이미지 hello 응용 프로그램에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="c6618-132">Hello에서 파생 된 *nginx 플라스* 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="c6618-133">Docker 허브에서 hello Redis 이미지 다운로드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="c6618-134">Hello 실행 [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) 명령 toosee hello 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="c6618-135">출력:</span><span class="sxs-lookup"><span data-stu-id="c6618-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="c6618-136">로컬에서 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c6618-136">Test application locally</span></span>

<span data-ttu-id="c6618-137">응용 프로그램을 실행 하는 toohttp://localhost:8080 toosee hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="c6618-139">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="c6618-139">Clean up resources</span></span>

<span data-ttu-id="c6618-140">응용 프로그램의 기능을 확인 했으므로 hello 실행 중인 컨테이너를 중지 하 고 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="c6618-141">Hello 컨테이너 이미지를 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c6618-141">Do not delete hello container images.</span></span> <span data-ttu-id="c6618-142">hello *azure 투표 프런트* 이미지가 업로드 된 tooan Azure 컨테이너 레지스트리 인스턴스 hello 다음 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="c6618-143">실행 중인 컨테이너 toostop hello 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="c6618-144">다음 명령을 hello로 중지 hello 컨테이너를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="c6618-145">작업이 완료 되 면 언제 hello Azure 투표 응용 프로그램을 포함 하는 컨테이너 이미지를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6618-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6618-146">Next steps</span></span>

<span data-ttu-id="c6618-147">이 자습서에서는 응용 프로그램 테스트 및 hello 응용 프로그램에 대 한 컨테이너 이미지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="c6618-148">단계를 수행 하는 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c6618-149">GitHub에서 응용 프로그램 소스 hello 복제</span><span class="sxs-lookup"><span data-stu-id="c6618-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="c6618-150">응용 프로그램 원본에서 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c6618-150">Created a container image from application source</span></span>
> * <span data-ttu-id="c6618-151">로컬 Docker 환경에서 테스트 된 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c6618-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="c6618-152">Azure 컨테이너 레지스트리에 컨테이너 이미지를 저장 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6618-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6618-153">푸시 이미지 tooAzure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="c6618-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
