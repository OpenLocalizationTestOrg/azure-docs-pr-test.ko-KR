---
title: "Azure Container Instances 문제 해결"
description: "Azure Container Instances 관련 문제 해결 방법 알아보기"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="7f62c-103">Azure Container Instances로의 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7f62c-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="7f62c-104">이 문서에는 컨테이너를 Azure Container Instances로 배포하는 경우 문제를 해결하는 방법을 보여줄 뿐만 아니라,</span><span class="sxs-lookup"><span data-stu-id="7f62c-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="7f62c-105">발생할 수 있는 일반적인 문제 중 일부를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="7f62c-106">진단 이벤트 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f62c-106">Getting diagnostic events</span></span>

<span data-ttu-id="7f62c-107">컨테이너 내에서 응용 프로그램 코드에서 로그를 보려면 [az 컨테이너 로그](/cli/azure/container#logs) 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="7f62c-108">하지만 컨테이너가 성공적으로 배포되지 않을 경우 Azure Container Instances 리소스 공급자가 제공하는 진단 정보를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="7f62c-109">컨테이너에 대한 이벤트를 보려면 다음 명령을 실행하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f62c-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="7f62c-110">출력에 배포 이벤트와 함께 컨테이너의 핵심 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-110">The output includes the core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="7f62c-111">일반 배포 문제</span><span class="sxs-lookup"><span data-stu-id="7f62c-111">Common deployment issues</span></span>

<span data-ttu-id="7f62c-112">배포에서 대부분 오류를 차지하는 몇 가지 일반적인 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="7f62c-113">이미지를 풀링할 수 없음</span><span class="sxs-lookup"><span data-stu-id="7f62c-113">Unable to pull image</span></span>

<span data-ttu-id="7f62c-114">Azure Container Instances가 초기에 이미지를 풀링할 수 없는 경우 결과적으로 실패하기 전까지 당분간 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="7f62c-115">이미지를 풀링할 수 없는 경우에는 다음과 같은 이미지가 표시됩니다</span><span class="sxs-lookup"><span data-stu-id="7f62c-115">If the image cannot be pulled, events like the following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="7f62c-116">해결하려면 해당 컨테이너를 삭제하고 이미지 이름을 정확하게 입력했는 세심하게 주의하면서 배포를 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="7f62c-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="7f62c-117">컨테이너가 지속적으로 종료 후 다시 시작함</span><span class="sxs-lookup"><span data-stu-id="7f62c-117">Container continually exits and restarts</span></span>

<span data-ttu-id="7f62c-118">현재 Azure Container Instances는 장기 실행 서비스만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="7f62c-119">컨테이너가 실행 후 완료되어 종료될 경우 자동으로 다시 시작하고 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="7f62c-120">이 경우 다음과 같은 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="7f62c-121">이때 컨테이너가 성공적으로 시작되어 빨리 다시 시작했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7f62c-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="7f62c-122">Container Instances API에 특정 컨테이너가 다시 시작한 횟수를 보여 주는 `retryCount` 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="7f62c-123">Linux 배포판에 대한 대부분 컨테이너 이미지는 기본 명령으로 Bash와 같은 셸을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="7f62c-124">자체 셸은 장기 실행 서비스이므로, 이러한 컨테이너는 즉시 종료된 후 다시 시작 루프를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="7f62c-125">컨테이너는 시작하는 데 오래 걸림</span><span class="sxs-lookup"><span data-stu-id="7f62c-125">Container takes a long time to start</span></span>

<span data-ttu-id="7f62c-126">컨테이너가 시작하는 데 오래 걸리지만, 결과적으로 성공할 경우 먼저 컨테이너 이미지의 크기를 살펴 보세요.</span><span class="sxs-lookup"><span data-stu-id="7f62c-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="7f62c-127">Azure Container Instances가 요청 시 컨테이너 이미지를 풀링하므로, 경험하는 시작 시간은 크기와 직접 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="7f62c-128">Docker CLI를 사용하여 컨테이너 이미지의 크기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="7f62c-129">출력:</span><span class="sxs-lookup"><span data-stu-id="7f62c-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="7f62c-130">이미지 크기를 작게 유지하는 핵심 요소는 최종 이미지에 런타임 시 필요하지 않은 것은 아무 것도 포함하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="7f62c-131">이 작업을 수행하는 한 가지 방법은 [다단계 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)를 활용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="7f62c-132">다단계 빌드를 통해 간편하게 최종 이미지에 빌드 시간에 필요한 추가 콘텐츠가 아닌 응용 프로그램에 필요한 아티팩트만 포함하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="7f62c-133">컨테이너 시작 시간에서 이미지 풀의 영향을 줄이는 다른 방법은 Azure Container Instances를 사용하는 같은 영역에서 Azure Container Registry를 사용하여 컨테이너 이미지를 호스팅하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="7f62c-134">이를 통해 컨테이너 이미지가 이동해야 하는 네트워크 경를 단축하여 다운로드 시간을 크게 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f62c-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>