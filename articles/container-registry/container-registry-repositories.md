---
title: "Azure 컨테이너 레지스트리 리포지토리 | Microsoft Docs"
description: "Docker 이미지에 Azure 컨테이너 레지스트리 리포지토리를 사용하는 방법"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="54cea-103">Azure 컨테이너 레지스트리 리포지토리</span><span class="sxs-lookup"><span data-stu-id="54cea-103">Azure container registry repositories</span></span>

<span data-ttu-id="54cea-104">Azure 컨테이너 레지스트리를 통해 리포지토리에 컨테이너 이미지를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="54cea-105">리포지토리에 이미지를 저장하면 격리된 환경에 이미지 그룹(또는 이미지 버전)을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="54cea-106">이미지를 레지스트리에 푸시할 때 이러한 리포지토리를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="54cea-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54cea-107">Prerequisites</span></span>
* <span data-ttu-id="54cea-108">**Azure Container Registry** - Azure 구독 내에서 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="54cea-109">예를 들어 [Azure Portal](container-registry-get-started-portal.md) 또는 [Azure CLI 2.0](container-registry-get-started-azure-cli.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="54cea-110">**Docker CLI** - 로컬 컴퓨터를 Docker 호스트로 설정하고 Docker CLI 명령에 액세스하려면 [Docker 엔진](https://docs.docker.com/engine/installation/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="54cea-111">**이미지 끌어오기** - 공개 Docker Hub 레지스트리에서 이미지를 끌어온 후 태그를 지정하고 레지스트리에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="54cea-112">이미지를 밀어넣고 끌어오는 방법은 [Azure 개인 레지스트리에 Docker 이미지 밀어넣기](container-registry-get-started-docker-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54cea-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="54cea-113">포털에서 리포지토리 보기</span><span class="sxs-lookup"><span data-stu-id="54cea-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="54cea-114">이미지를 컨테이너 레지스트리에 밀어넣었으면 Azure Portal에서 이미지를 호스팅하는 리포지토리 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="54cea-115">[Azure 개인 레지스트리에 Docker 이미지 밀어넣기](container-registry-get-started-docker-cli.md) 문서의 단계를 수행하면 컨테이너 레지스트리에 Nginx 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="54cea-116">지침의 일부로 이미지에 대한 네임스페이스를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="54cea-117">아래 예제의 명령은 NGinx 이미지를 "samples" 리포지토리에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="54cea-118">Azure Container Registry는 다단계 리포지토리 네임스페이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="54cea-119">이 기능을 통해 특정 앱과 관련된 이미지 컬렉션 또는 특정 배포 또는 작업 팀에 대한 앱 컬렉션을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="54cea-120">컨테이너 레지스트리의 리포지토리에 대한 자세한 내용은 [Azure의 개인 Docker 컨테이너 레지스트리](container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54cea-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="54cea-121">Azure 컨테이너 레지스트리 리포지토리를 보려면</span><span class="sxs-lookup"><span data-stu-id="54cea-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="54cea-122">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="54cea-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="54cea-123">**Azure 컨테이너 레지스트리** 블레이드에서 검사할 레지스트리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="54cea-124">레지스트리 블레이드에서 **리포지토리**를 클릭하면 모든 리포지토리와 해당 이미지 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54cea-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="54cea-125">(선택 사항) 태그를 볼 특정 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="54cea-125">(Optional) Select a specific image to see tags</span></span>

![포털에서 리포지토리](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="54cea-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54cea-127">Next steps</span></span>
<span data-ttu-id="54cea-128">이제 기본 사항을 배웠으니 레지스트리 사용을 시작할 준비가 되었습니다!</span><span class="sxs-lookup"><span data-stu-id="54cea-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="54cea-129">예를 들어, 컨테이너 이미지를 [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) 클러스터에 배포하기 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="54cea-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
