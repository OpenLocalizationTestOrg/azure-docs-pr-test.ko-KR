---
title: "컨테이너 인스턴스 자습서-aaaAzure 앱 준비 | Azure 문서"
description: "응용 프로그램 배포 tooAzure 컨테이너 인스턴스 준비"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="8ade6-103">컨테이너에 대 한 배포 tooAzure 컨테이너 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="8ade6-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="8ade6-104">Azure Container Instances를 통해 어떠한 가상 컴퓨터를 프로비전하지 않고 또 더 높은 수준의 서비스를 채택하지 않고도 Azure로 Docker 컨테이너를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="8ade6-105">이 자습서에서는 Node.js에서 간단한 웹 응용 프로그램을 빌드하고 Azure Container Instances를 사용하여 실행할 수 있는 컨테이너로 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="8ade6-106">다음 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8ade6-107">GitHub에서 응용 프로그램 소스 복제</span><span class="sxs-lookup"><span data-stu-id="8ade6-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="8ade6-108">응용 프로그램 소스에서 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="8ade6-108">Creating container images from application source</span></span>
> * <span data-ttu-id="8ade6-109">Hello 이미지 로컬 Docker 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="8ade6-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="8ade6-110">후속 자습서에서는 사용자 이미지 tooan Azure 컨테이너 레지스트리 업로드 한 후에 tooAzure 컨테이너 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ade6-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8ade6-111">Before you begin</span></span>

<span data-ttu-id="8ade6-112">이 자습서에서는 컨테이너, 컨테이너 이미지 및 기본 Docker 명령과 같은 핵심 Docker 개념에 대한 기본적인 지식이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="8ade6-113">필요한 경우 컨테이너 기본 사항에 대한 입문서는 [Get started with Docker(Docker 시작)]( https://docs.docker.com/get-started/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ade6-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="8ade6-114">toocomplete이이 자습서에서는 Docker 개발 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="8ade6-115">Docker는 모든 [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) 또는 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 시스템에서 쉽게 Docker를 구성하는 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="8ade6-116">응용 프로그램 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ade6-116">Get application code</span></span>

<span data-ttu-id="8ade6-117">이 자습서에서는 hello 샘플에서 기본적으로 제공 하는 간단한 웹 응용 프로그램에 포함 되어 [Node.js](http://nodejs.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="8ade6-118">hello 앱 정적 HTML 페이지를 사용 되 고는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-118">hello app serves a static HTML page and looks like this:</span></span>

![브라우저에 표시된 자습서 앱][aci-tutorial-app]

<span data-ttu-id="8ade6-120">Git toodownload hello 샘플을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="8ade6-121">Hello 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="8ade6-121">Build hello container image</span></span>

<span data-ttu-id="8ade6-122">Dockerfile hello 샘플 리포지토리에 제공 된 hello hello 컨테이너 빌드되는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="8ade6-123">시작 되는 [공식 Node.js 이미지] [ dockerhub-nodeimage] 기반 [Alpine Linux](https://alpinelinux.org/), 컨테이너와 적합된 toouse 있는 소규모 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="8ade6-124">그런 다음 hello 컨테이너로 hello 응용 프로그램 파일을 복사, hello Node Package Manager를 사용 하 여 종속성을 설치 및 마지막으로 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="8ade6-125">사용 하 여 hello `docker build` 명령 toocreate hello 컨테이너 이미지를로 태그 지정 *aci 자습서 앱*:</span><span class="sxs-lookup"><span data-stu-id="8ade6-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="8ade6-126">사용 하 여 hello `docker images` toosee hello 빌드된 이미지:</span><span class="sxs-lookup"><span data-stu-id="8ade6-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="8ade6-127">출력:</span><span class="sxs-lookup"><span data-stu-id="8ade6-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="8ade6-128">Hello 컨테이너를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="8ade6-128">Run hello container locally</span></span>

<span data-ttu-id="8ade6-129">Hello 컨테이너 tooAzure 컨테이너 인스턴스 배포를 시도 하기 전에 로컬로 실행 작동 tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="8ade6-130">hello `-d` 스위치를 통해 hello 컨테이너 hello 백그라운드에서 실행 하는 동안 `-p` toomap 프로그램 계산 tooport hello 컨테이너에는 80에는 임의의 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="8ade6-131">컨테이너 hello open hello 브라우저 toohttp://localhost:8080 tooconfirm ï ´ ù.</span><span class="sxs-lookup"><span data-stu-id="8ade6-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Hello 브라우저에서 로컬로 실행 중인 hello 응용 프로그램][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="8ade6-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ade6-133">Next steps</span></span>

<span data-ttu-id="8ade6-134">이 자습서에서는 배포 된 tooAzure 컨테이너 인스턴스 수 있는 컨테이너 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="8ade6-135">단계를 수행 하는 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8ade6-136">GitHub에서 응용 프로그램 소스 hello 복제</span><span class="sxs-lookup"><span data-stu-id="8ade6-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="8ade6-137">응용 프로그램 소스에서 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="8ade6-137">Creating container images from application source</span></span>
> * <span data-ttu-id="8ade6-138">Hello 컨테이너 로컬로 테스트</span><span class="sxs-lookup"><span data-stu-id="8ade6-138">Testing hello container locally</span></span>

<span data-ttu-id="8ade6-139">Azure 컨테이너 레지스트리에 컨테이너 이미지를 저장 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade6-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ade6-140">푸시 이미지 tooAzure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="8ade6-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png