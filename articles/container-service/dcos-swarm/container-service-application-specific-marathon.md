---
title: "응용 프로그램 또는 사용자 특정 Marathon 서비스 | Microsoft 문서"
description: "응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, Marathon, 마이크로 서비스, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="94a38-104">응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="94a38-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="94a38-105">Azure 컨테이너 서비스는 Apache Mesos 및 Marathon을 미리 구성하는 마스터 서버 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="94a38-106">클러스터에서 응용 프로그램을 오케스트레이션하는 데 사용할 수 있지만 이러한 목적으로는 마스터 서버를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="94a38-107">예를 들어 Marathon 구성을 조정하려면 마스터 서버 자체에 로그인하고 변경해야 합니다. 이 방법에서는 표준과 약간 다르고 독립적으로 처리 및 관리해야 하는 고유 마스터 서버를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="94a38-108">또한 한 팀에 필요한 구성은 다른 팀에게는 최적의 구성이 아닐 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="94a38-109">이 문서에서는 응용 프로그램 또는 사용자 특정 Marathon 서비스를 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="94a38-110">이 서비스는 단일 사용자 또는 팀에 속하므로 원하는 방식으로 자유롭게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="94a38-111">또한 Azure 컨테이너 서비스를 사용하여 서비스를 계속해서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="94a38-112">서비스가 실패하면 Azure 컨테이너 서비스는 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="94a38-113">중단 시간은 대부분 느끼지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94a38-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="94a38-114">Prerequisites</span></span>
<span data-ttu-id="94a38-115">DC/OS Orchestrator 유형을 사용하여 [Azure Container Service의 인스턴스를 배포](container-service-deployment.md)하고 [클라이언트가 클러스터에 연결될 수 있는지 확인합니다](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="94a38-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="94a38-116">또한 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="94a38-117">응용 프로그램 또는 사용자 특정 Marathon 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="94a38-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="94a38-118">만들려는 응용 프로그램 서비스의 이름을 정의하는 JSON 구성 파일을 만드는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="94a38-119">여기서는 프레임워크 이름으로 `marathon-alice` 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="94a38-120">`marathon-alice.json`과 같이 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="94a38-121">다음으로, DC/OS CLI를 사용하여 구성 파일에서 설정한 옵션으로 Marathon 인스턴스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="94a38-122">이제 `marathon-alice` 서비스가 DC/OS UI의 서비스 탭에서 실행되는 것을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="94a38-123">이 UI는 직접 액세스하려는 경우 `http://<hostname>/service/marathon-alice/` 가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="94a38-124">서비스에 액세스하는 DC/OS CLI 설정</span><span class="sxs-lookup"><span data-stu-id="94a38-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="94a38-125">다음과 같이 `marathon-alice` 인스턴스를 가리키도록 `marathon.url` 속성을 설정하여 이 새 서비스에 액세스하도록 DC/OS CLI를 선택적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="94a38-126">`dcos config show` 명령을 사용하여 CLI가 작동 중인 Marathon의 인스턴스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="94a38-127">`dcos config unset marathon.url`명령으로 마스터 Marathon 서비스를 사용하도록 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a38-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

