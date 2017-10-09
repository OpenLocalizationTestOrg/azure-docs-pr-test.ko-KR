---
title: "Azure DC/OS 클러스터의 aaaLoad 균형 컨테이너 | Microsoft Docs"
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="86c68-104">Azure Container Service DC/OS 클러스터에서 컨테이너 부하 분산</span><span class="sxs-lookup"><span data-stu-id="86c68-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="86c68-105">이 문서에서는 toocreate DC/OS에는 내부 부하 분산 장치 풀 마라톤 LB를 사용 하 여 Azure 컨테이너 서비스를 관리 하는 방법을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="86c68-106">이 구성을 통해 tooscale 하면 응용 프로그램 가로로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="86c68-107">또한 있습니다 tootake 활용을 hello 공용 및 개인 에이전트 클러스터 hello 공용 클러스터와 사용자 응용 프로그램 컨테이너에서 hello 개인 클러스터에 부하 분산을 배치 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="86c68-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86c68-109">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="86c68-110">Hello 부하 분산 장치를 사용 하 여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="86c68-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="86c68-111">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="86c68-112">ACS DC/OS 클러스터 toocomplete hello이이 자습서의 단계를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="86c68-113">필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="86c68-114">이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상.</span><span class="sxs-lookup"><span data-stu-id="86c68-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="86c68-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="86c68-116">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="86c68-117">부하 분산 개요</span><span class="sxs-lookup"><span data-stu-id="86c68-117">Load balancing overview</span></span>

<span data-ttu-id="86c68-118">Azure Container Service DC/OS 클러스터에는 두 개의 부하 분산 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="86c68-119">**Azure 부하 분산 장치** 공용 진입점 (최종 사용자가 해당 항목에 액세스 하는 hello)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="86c68-120">Azure LB Azure 컨테이너 서비스에 의해 자동으로 제공 되며, 기본적으로 구성 된 tooexpose 포트 80, 443 및 8080 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="86c68-121">**hello 마라톤 부하 분산 장치 (마라톤 파운드)** 경로 인바운드 요청 toocontainer 이러한 요청을 서비스 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="86c68-122">웹 서비스를 제공 하는 hello 컨테이너의 크기를 조정 했습니다 hello 마라톤 lb 동적으로 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="86c68-123">이 부하 분산 장치의 기본 컨테이너 서비스에 의해 제공 되지 않습니다 이지만 쉽게 tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="86c68-124">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="86c68-125">부하 분산 장치 풀 마라톤 배포한 hello 컨테이너를 기준으로 자체에 동적으로 재구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="86c68-126">이 발생 Apache Mesos hello 컨테이너를 다른 곳에서 다시 시작 하 고 마라톤 lb 조정 탄력적 toohello 손실 컨테이너 또는 에이전트-이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="86c68-127">Hello 명령 tooinstall hello 마라톤 부하 분산 장치 hello 공용 에이전트의 클러스터에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="86c68-128">부하 분산된 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="86c68-128">Deploy load balanced application</span></span>

<span data-ttu-id="86c68-129">Hello 마라톤 lb 패키지를 만들었으므로 이제 해당 했는데도 tooload 분산 하는 응용 프로그램 컨테이너를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="86c68-130">먼저, hello를 공개적으로 노출 하는 hello 에이전트의 FQDN을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="86c68-131">다음으로 파일을 만듭니다 *hello web.json* 내용에 따라 hello에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="86c68-132">hello `HAPROXY_0_VHOST` 레이블 toobe hello hello DC/OS 에이전트의 FQDN으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="86c68-133">Hello DC/OS CLI toorun hello 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="86c68-134">기본적으로 풀 마라톤 hello toohello 개인 클러스터 hello 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="86c68-135">이 즉 배포 위에 hello는 부하 분산 장치를 통해 액세스할 수 있는는 일반적으로 필요한 hello 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="86c68-136">Hello 응용 프로그램을 배포한 후에 toohello FQDN hello 에이전트 클러스터 tooview 부하 분산 된 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![부하 분산된 응용 프로그램의 이미지](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="86c68-138">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="86c68-139">Azure Load Balancer는 기본적으로 포트 80, 8080 및 443을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="86c68-140">사용 중인 경우이 세 가지 중 하나 (같이 hello 위 예제) 포트를 다음 toodo 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="86c68-141">수 toohit 있어야 에이전트 부하 분산 장치의 FQDN 및 새로 고칠 때마다 합니다 적중할 라운드 로빈 방식으로 세 개의 웹 서버 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="86c68-142">다른 포트를 사용 하는 경우 사용한 hello 포트에 대 한 라운드 로빈 tooadd 규칙 및 hello 부하 분산 장치 프로브 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="86c68-143">Hello에서 이렇게 하려면 [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), hello 명령을 사용 하 여 `azure network lb rule create` 및 `azure network lb probe create`합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c68-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86c68-144">Next steps</span></span>

<span data-ttu-id="86c68-145">이 자습서에서는 hello 마라톤와 Azure 부하 분산 장치 포함 하 여 작업을 다음 hello ACS에서 부하 분산에 대 한 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86c68-146">Marathon Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="86c68-147">Hello 부하 분산 장치를 사용 하 여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="86c68-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="86c68-148">Azure Load Balancer 구성</span><span class="sxs-lookup"><span data-stu-id="86c68-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="86c68-149">Azure에서 DC/OS와 Azure 저장소 통합 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86c68-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86c68-150">DC/OS 클러스터에 Azure File Share 탑재</span><span class="sxs-lookup"><span data-stu-id="86c68-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)