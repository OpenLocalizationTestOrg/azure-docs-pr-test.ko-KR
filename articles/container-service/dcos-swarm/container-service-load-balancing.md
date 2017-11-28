---
title: "Azure DC/OS 클러스터의 컨테이너 부하 분산 | Microsoft Docs"
description: "Azure Container Service DC/OS 클러스터에 있는 여러 컨테이너에 대해 부하를 분산합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, 마이크로 서비스, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="4a60f-104">Azure Container Service DC/OS 클러스터에서 컨테이너 부하 분산</span><span class="sxs-lookup"><span data-stu-id="4a60f-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="4a60f-105">이 문서에서는 Marathon-LB를 사용하여 DC/OS로 관리되는 Azure Container Service에 내부 부하 분산 장치를 만드는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="4a60f-106">이 구성은 응용 프로그램을 수평으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="4a60f-107">또한 부하 분산 장치를 공용 클러스터에 배치하고 응용 프로그램 컨테이너를 개인 클러스터에 배치하여 공용 및 개인 에이전트 클러스터를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="4a60f-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a60f-109">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="4a60f-110">부하 분산 장치를 사용하여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4a60f-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="4a60f-111">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="4a60f-112">이 자습서의 단계를 완료하려면 ACS DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="4a60f-113">필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="4a60f-114">이 자습서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4a60f-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="4a60f-116">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a60f-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="4a60f-117">부하 분산 개요</span><span class="sxs-lookup"><span data-stu-id="4a60f-117">Load balancing overview</span></span>

<span data-ttu-id="4a60f-118">Azure Container Service DC/OS 클러스터에는 두 개의 부하 분산 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="4a60f-119">**Azure Load Balancer**는 공용 진입점(최종 사용자가 액세스하는)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="4a60f-120">Azure LB는 Azure Container Service에서 자동으로 제공하며 기본적으로 포트 80, 443 및 8080을 노출하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="4a60f-121">**Marathon Load Balancer(marathon-lb)**는 요청을 서비스하는 컨테이너 인스턴스로 인바운드 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="4a60f-122">웹 서비스를 제공하는 컨테이너를 확장하면 marathon-lb는 동적으로 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="4a60f-123">이 부하 분산 장치는 Container Service에 기본적으로 제공되지 않지만 쉽게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="4a60f-124">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="4a60f-125">Marathon Load Balancer는 배포한 컨테이너를 기준으로 동적으로 자체 재구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="4a60f-126">컨테이너 또는 에이전트 손실에 대한 복원력이 있으며 손실이 발생하는 경우 Apache Mesos가 다른 곳에서 컨테이너를 다시 시작하고 marathon-lb가 상황에 맞게 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="4a60f-127">공용 에이전트의 클러스터에 Marathon Load Balancer를 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="4a60f-128">부하 분산된 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4a60f-128">Deploy load balanced application</span></span>

<span data-ttu-id="4a60f-129">이제 marathon-lb 패키지가 있으므로 부하를 분산하려는 응용 프로그램 컨테이너를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="4a60f-130">먼저 공개적으로 노출된 에이전트의 FQDN을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="4a60f-131">다음으로 *hello-web.json*이라는 파일을 만들고 다음 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="4a60f-132">`HAPROXY_0_VHOST` 레이블을 DC/OS 에이전트의 FQDN으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="4a60f-133">DC/OS CLI를 사용하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="4a60f-134">기본적으로 Marathon은 개인 클러스터에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="4a60f-135">다시 말해서 위의 배포는 부하 분산 장치를 통해서만 액세스할 수 있으며, 이는 일반적으로 고객이 원하는 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="4a60f-136">응용 프로그램이 배포되면 에이전트 클러스터의 FQDN으로 이동하여 부하 분산된 응용 프로그램을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![부하 분산된 응용 프로그램의 이미지](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="4a60f-138">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="4a60f-139">Azure Load Balancer는 기본적으로 포트 80, 8080 및 443을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="4a60f-140">이러한 세 가지 포트 중 하나를 사용하는 경우(위의 예에서 실행하는 것처럼) 수행할 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="4a60f-141">에이전트 부하 분산 장치의 FQDN에 도달할 수 있으며 새로 고칠 때마다 라운드 로빈 방식으로 세 개의 웹 서버 중 하나에 도달할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="4a60f-142">다른 포트를 사용하는 경우 부하 분산 장치에서 사용한 포트에 대해 라운드 로빈 규칙 및 프로브를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="4a60f-143">이는 [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md)에서 `azure network lb rule create` 및 `azure network lb probe create` 명령으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a60f-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a60f-144">Next steps</span></span>

<span data-ttu-id="4a60f-145">이 자습서에서는 다음 작업을 포함하여 Marathon 및 Azure 부하 분산 장치를 사용하여 ACS에서 부하를 분산하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4a60f-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a60f-146">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="4a60f-147">부하 분산 장치를 사용하여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4a60f-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="4a60f-148">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="4a60f-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="4a60f-149">다음 자습서로 넘어가서 Azure에서 Azure 저장소를 DC/OS와 통합하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4a60f-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a60f-150">DC/OS 클러스터에 Azure File Share 탑재</span><span class="sxs-lookup"><span data-stu-id="4a60f-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)