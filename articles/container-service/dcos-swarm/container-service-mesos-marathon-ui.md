---
title: "Marathon UI를 사용하여 Azure DC/OS 클러스터 관리 | Microsoft Docs"
description: "Marathon 웹 UI를 사용하여 컨테이너를 Azure 컨테이너 서비스 클러스터 서비스에 배포합니다."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: b00088bb005519dc5d533433308c0e3e33c7f433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="213c5-104">Marathon 웹 UI를 통해 Azure Container Service DC/OS 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="213c5-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="213c5-105">DC/OS는 기본 하드웨어를 추상화하는 동안 클러스터형 워크로드를 배포 및 확장하기 위한 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="213c5-106">DC/OS의 상단에 계산 워크로드의 예약 및 실행을 관리하는 프레임워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="213c5-107">프레임워크를 널리 사용되고 있는 많은 워크로드에 사용할 수 있지만 이 문서에서는 Marathon으로 컨테이너를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="213c5-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="213c5-108">Prerequisites</span></span>
<span data-ttu-id="213c5-109">이러한 예제를 통해 작업하기 전에 Azure 컨테이너 서비스에 구성된 DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="213c5-110">또한 이 클러스터에 원격으로 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="213c5-111">이러한 항목에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="213c5-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="213c5-112">Azure 컨테이너 서비스 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="213c5-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="213c5-113">Azure 컨테이너 서비스 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="213c5-113">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="213c5-114">이 문서에서는 로컬 포트 80을 통해 DC/OS 클러스터에 터널링한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="213c5-115">DC/OS UI 탐색</span><span class="sxs-lookup"><span data-stu-id="213c5-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="213c5-116">SSH(Secure Shell) 터널이 [설정된](../container-service-connect.md) 상태에서 http://localhost/로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="213c5-117">DC/OS 웹 UI가 로드되면서 클러스터에 대한 정보(예: 사용된 리소스, 활성 에이전트)가 표시되고 실행 중인 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="213c5-119">Marathon UI 탐색</span><span class="sxs-lookup"><span data-stu-id="213c5-119">Explore the Marathon UI</span></span>
<span data-ttu-id="213c5-120">Marathon UI를 보려면 http://localhost/marathon으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="213c5-121">이 화면에서는 Azure 컨테이너 서비스 DC/OS 클러스터에 새 컨테이너 또는 다른 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="213c5-122">컨테이너 및 응용 프로그램을 실행하는 방법에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-122">You can also see information about running containers and applications.</span></span>  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="213c5-124">Docker로 포맷된 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="213c5-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="213c5-125">Marathon을 사용하여 새 컨테이너를 배포하려면, **응용 프로그램 만들기**를 클릭하고 양식 탭에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="213c5-126">필드</span><span class="sxs-lookup"><span data-stu-id="213c5-126">Field</span></span> | <span data-ttu-id="213c5-127">값</span><span class="sxs-lookup"><span data-stu-id="213c5-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="213c5-128">ID</span><span class="sxs-lookup"><span data-stu-id="213c5-128">ID</span></span> |<span data-ttu-id="213c5-129">nginx</span><span class="sxs-lookup"><span data-stu-id="213c5-129">nginx</span></span> |
| <span data-ttu-id="213c5-130">메모리</span><span class="sxs-lookup"><span data-stu-id="213c5-130">Memory</span></span> | <span data-ttu-id="213c5-131">32</span><span class="sxs-lookup"><span data-stu-id="213c5-131">32</span></span> |
| <span data-ttu-id="213c5-132">이미지</span><span class="sxs-lookup"><span data-stu-id="213c5-132">Image</span></span> |<span data-ttu-id="213c5-133">nginx</span><span class="sxs-lookup"><span data-stu-id="213c5-133">nginx</span></span> |
| <span data-ttu-id="213c5-134">네트워크</span><span class="sxs-lookup"><span data-stu-id="213c5-134">Network</span></span> |<span data-ttu-id="213c5-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="213c5-135">Bridged</span></span> |
| <span data-ttu-id="213c5-136">호스트 포트</span><span class="sxs-lookup"><span data-stu-id="213c5-136">Host Port</span></span> |<span data-ttu-id="213c5-137">80</span><span class="sxs-lookup"><span data-stu-id="213c5-137">80</span></span> |
| <span data-ttu-id="213c5-138">프로토콜</span><span class="sxs-lookup"><span data-stu-id="213c5-138">Protocol</span></span> |<span data-ttu-id="213c5-139">TCP</span><span class="sxs-lookup"><span data-stu-id="213c5-139">TCP</span></span> |

![새 응용 프로그램 UI--일반](./media/container-service-mesos-marathon-ui/dcos4.png)

![새 응용 프로그램 UI--Docker 컨테이너](./media/container-service-mesos-marathon-ui/dcos5.png)

![새 응용 프로그램 UI--포트 및 서비스 검색](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="213c5-143">에이전트의 포트에 컨테이너 포트를 정적으로 매핑하려는 경우 JSON 모드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="213c5-144">이렇게 하려면 토글을 사용하여 새 응용 프로그램 마법사를 **JSON 모드** 로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="213c5-145">그런 다음 응용 프로그램 정의의 `portMappings` 섹션에 다음 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="213c5-146">이 예제는 컨테이너의 포트 80을 DC/OS 에이전트의 포트80으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="213c5-147">이렇게 변경한 후에 이 마법사를 JSON 모드에서 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![새 응용 프로그램 UI--포트 80 예제](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="213c5-149">상태 검사를 설정하려면 **상태 검사** 탭에서 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![새 응용 프로그램 UI--상태 검사](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="213c5-151">DC/OS 클러스터는 사설 및 공용 에이전트와 함께 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="213c5-152">클러스터를 인터넷에서 응용 프로그램에 액세스할 수 있으려면 공용 에이전트에 응용 프로그램을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="213c5-153">이를 위해, 새 응용 프로그램 마법사의 **선택 사항** 탭을 선택하고 **수락된 리소스 역할**에 **slave_public**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="213c5-154">그런 다음 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-154">Then click **Create Application**.</span></span>

![새 응용 프로그램 UI--공용 에이전트 설정](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="213c5-156">다시 Marathon 주 페이지에서 컨테이너에 대한 배포 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="213c5-157">처음에는 **배포 중** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="213c5-158">성공적으로 배포된 후에는 상태가 **실행 중**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-158">After a successful deployment, the status changes to **Running**.</span></span>

![Marathon 기본 페이지 UI--컨테이너 배포 상태](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="213c5-160">DC/OS 웹 UI(http://localhost/)로 다시 전환하면 이 경우 Docker로 포맷된 컨테이너인 태스크가 DC/OS 클러스터에서 실행 중임이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![DC/OS 웹 UI--클러스터에서 실행 중인 작업](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="213c5-162">또한 태스크가 실행되는 클러스터 노드를 보려면 **노드** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![DC/OS 웹 UI--작업 클러스터 노드](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="213c5-164">컨테이너에 연결</span><span class="sxs-lookup"><span data-stu-id="213c5-164">Reach the container</span></span>

<span data-ttu-id="213c5-165">이 예제에서 응용 프로그램은 공용 에이전트 노드에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="213c5-166">클러스터의 에이전트 FQDN으로 이동하여 인터넷에서 응용 프로그램에 연결합니다. `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com` 여기서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="213c5-167">**DNSPREFIX** 는 클러스터를 배포할 때 제공한 DNS 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="213c5-168">**REGION** 은 리소스 그룹이 있는 하위 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="213c5-168">**REGION** is the region in which your resource group is located.</span></span>

    ![인터넷의 Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="213c5-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="213c5-170">Next steps</span></span>
* [<span data-ttu-id="213c5-171">DC/OS 및 Marathon API 작업</span><span class="sxs-lookup"><span data-stu-id="213c5-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="213c5-172">Mesos와 함께 Azure Container Service에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="213c5-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
