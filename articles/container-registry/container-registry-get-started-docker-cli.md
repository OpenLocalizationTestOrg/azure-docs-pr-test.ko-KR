---
title: "aaaPush Docker 이미지 tooprivate Azure 레지스트리 | Microsoft Docs"
description: "밀어넣기 및 끌어오기 Docker hello Docker CLI를 사용 하 여 Azure에서 이미지 tooa 개인 컨테이너 레지스트리"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="3d287-103">첫 번째 이미지 tooa 개인 Docker 컨테이너 레지스트리 hello Docker CLI를 사용 하 여 푸시</span><span class="sxs-lookup"><span data-stu-id="3d287-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="3d287-104">Azure 컨테이너 레지스트리에 저장 하 고 개인 관리 [Docker](http://hub.docker.com) 컨테이너 이미지, toohello 비슷한 방식으로 [Docker 허브](https://hub.docker.com/) 공용 Docker 이미지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="3d287-105">Hello를 사용 하 여 [Docker 명령줄 인터페이스](https://docs.docker.com/engine/reference/commandline/cli/) Docker CLI ()에 대 한 [로그인](https://docs.docker.com/engine/reference/commandline/login/), [푸시](https://docs.docker.com/engine/reference/commandline/push/), [끌어오기](https://docs.docker.com/engine/reference/commandline/pull/), 및 기타 작업을 컨테이너 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="3d287-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="3d287-106">자세한 배경 및 개념에 대 한 참조 [hello 개요](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="3d287-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="3d287-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3d287-107">Prerequisites</span></span>
* <span data-ttu-id="3d287-108">**Azure Container Registry** - Azure 구독 내에서 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="3d287-109">예를 들어 hello를 사용 하 여 [Azure 포털](container-registry-get-started-portal.md) 또는 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="3d287-110">**Docker CLI** -는 Docker 호스트 및 액세스 hello Docker CLI 명령으로 로컬 컴퓨터를 tooset 설치 [Docker 엔진](https://docs.docker.com/engine/installation/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="3d287-111">Tooa 레지스트리 로그인</span><span class="sxs-lookup"><span data-stu-id="3d287-111">Log in tooa registry</span></span>
<span data-ttu-id="3d287-112">실행 `docker login` 와 tooyour 컨테이너 레지스트리에 toolog 프로그램 [레지스트리 자격 증명](container-registry-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="3d287-113">hello 다음 예제에서는 전달 hello ID와 Azure Active Directory의 암호 [서비스 사용자](../active-directory/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="3d287-114">예를 들어 수 할당 했는지 자동화 시나리오에 대 한 서비스 주체 tooyour 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="3d287-115">있는지 toospecify hello 레지스트리 정규화 된 이름 (모두 소문자)을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="3d287-116">이 예제에서는 `myregistry.azurecr.io`입니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="3d287-117">단계 toopull 및 푸시 이미지</span><span class="sxs-lookup"><span data-stu-id="3d287-117">Steps toopull and push an image</span></span>
<span data-ttu-id="3d287-118">hello는 다운로드 hello 공개 Docker 허브 레지스트리 hello에서에서 Nginx 이미지 태그 프로그램 개인 Azure 컨테이너 레지스트리에 대 한 tooyour 레지스트리 푸시 다음 다시 가져오는 예제를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="3d287-119">**1. Hello Docker 공식 이미지 Nginx에 대 한 끌어오기**</span><span class="sxs-lookup"><span data-stu-id="3d287-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="3d287-120">첫 번째 끌어오기 hello 공용 Nginx 이미지 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="3d287-121">**2. Hello Nginx 컨테이너 시작**</span><span class="sxs-lookup"><span data-stu-id="3d287-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="3d287-122">hello 다음 명령은 hello 로컬 Nginx 컨테이너 대화형으로에서 시작 포트 8080에서 Nginx toosee 출력 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="3d287-123">한 번 중지 하는 컨테이너를 실행 하는 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="3d287-124">너무 찾아보기[http://localhost:8080](http://localhost:8080) tooview hello 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="3d287-125">하나를 따르는 화면 비슷한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-125">You see a screen similar toohello following one.</span></span>

![로컬 컴퓨터의 Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="3d287-127">toostop 실행 중인 컨테이너 hello, ctrl 키를 [] + [c + +].</span><span class="sxs-lookup"><span data-stu-id="3d287-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="3d287-128">**3. 레지스트리에서 hello 이미지의 별칭을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="3d287-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="3d287-129">hello 다음 명령은 hello 이미지의 별칭을 정규화 된 경로 tooyour 레지스트리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="3d287-130">이 예에서는 지정 hello `samples` hello 레지스트리 hello 루트 네임 스페이스 tooavoid 좀 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="3d287-131">**4. 푸시 hello 이미지 tooyour 레지스트리**</span><span class="sxs-lookup"><span data-stu-id="3d287-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="3d287-132">**5. 레지스트리에서 끌어오기 hello 이미지**</span><span class="sxs-lookup"><span data-stu-id="3d287-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="3d287-133">**6. 레지스트리에서 hello Nginx 컨테이너 시작**</span><span class="sxs-lookup"><span data-stu-id="3d287-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="3d287-134">너무 찾아보기[http://localhost:8080](http://localhost:8080) tooview hello 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="3d287-135">toostop 실행 중인 컨테이너 hello, ctrl 키를 [] + [c + +].</span><span class="sxs-lookup"><span data-stu-id="3d287-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="3d287-136">**7. (선택 사항) Hello 이미지 제거**</span><span class="sxs-lookup"><span data-stu-id="3d287-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="3d287-137">동시 제한</span><span class="sxs-lookup"><span data-stu-id="3d287-137">Concurrent Limits</span></span>
<span data-ttu-id="3d287-138">일부 시나리오에서 호출을 동시에 실행하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="3d287-139">다음 표에 hello 레지스트리 Azure 컨테이너에 대 한 "밀어넣기" 및 "끌어오기" 작업을 사용 하 여 동시 호출의 hello 한계를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="3d287-140">작업</span><span class="sxs-lookup"><span data-stu-id="3d287-140">Operation</span></span>  | <span data-ttu-id="3d287-141">제한</span><span class="sxs-lookup"><span data-stu-id="3d287-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="3d287-142">풀링</span><span class="sxs-lookup"><span data-stu-id="3d287-142">PULL</span></span>       | <span data-ttu-id="3d287-143">동시 too10 위로 끌어와서 레지스트리 당</span><span class="sxs-lookup"><span data-stu-id="3d287-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="3d287-144">푸시</span><span class="sxs-lookup"><span data-stu-id="3d287-144">PUSH</span></span>       | <span data-ttu-id="3d287-145">동시 too5를 레지스트리 당 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d287-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d287-146">Next steps</span></span>
<span data-ttu-id="3d287-147">Hello 기본 사항을 배웠으므로 레지스트리를 사용 하 여 준비 toostart 됩니다!</span><span class="sxs-lookup"><span data-stu-id="3d287-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="3d287-148">예를 들어 컨테이너 이미지 tooan 배포를 시작할 [Azure 컨테이너 서비스](https://azure.microsoft.com/documentation/services/container-service/) 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3d287-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
