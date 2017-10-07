---
title: "aaaManage Azure DC/OS 마라톤 UI를 사용한 클러스터 | Microsoft Docs"
description: "Hello 마라톤 웹 UI를 사용 하 여 컨테이너 tooan Azure 컨테이너 서비스 클러스터 서비스를 배포 합니다."
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
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="1e6d0-104">Hello 마라톤 웹 UI 사용 하는 Azure 컨테이너 서비스 DC/OS 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="1e6d0-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="1e6d0-105">DC/OS를 배포 및 hello 기본 하드웨어를 추상화 하는 동안 클러스터 된 작업 확장에 대 한 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="1e6d0-106">DC/OS의 상단에 계산 워크로드의 예약 및 실행을 관리하는 프레임워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="1e6d0-107">프레임 워크는 다양 한 인기 있는 작업에 사용할 수 있는,이 문서에서는 tooget 시작 마라톤을 사용 하 여 컨테이너를 배포 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="1e6d0-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1e6d0-108">Prerequisites</span></span>
<span data-ttu-id="1e6d0-109">이러한 예제를 통해 작업하기 전에 Azure 컨테이너 서비스에 구성된 DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="1e6d0-110">Toohave 원격 연결 toothis 클러스터도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="1e6d0-111">이러한 항목에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="1e6d0-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="1e6d0-112">Azure 컨테이너 서비스 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="1e6d0-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="1e6d0-113">Tooan Azure 컨테이너 서비스 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="1e6d0-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="1e6d0-114">이 문서에서는 toohello DC/OS 클러스터 로컬 포트 80 통해 터널링 할 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="1e6d0-115">DC/OS UI hello 탐색</span><span class="sxs-lookup"><span data-stu-id="1e6d0-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="1e6d0-116">SSH (보안 셸) 터널와 [설정](../container-service-connect.md), toohttp://localhost/ 찾아보기 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="1e6d0-117">이 hello DC/OS 웹 UI를 로드 하 고 사용 되는 리소스, 활성 에이전트를 실행 중인 서비스와 같은 hello 클러스터에 대 한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="1e6d0-119">Hello 마라톤 UI 탐색</span><span class="sxs-lookup"><span data-stu-id="1e6d0-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="1e6d0-120">toosee hello 마라톤 UI toohttp://localhost/marathon를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="1e6d0-121">이 화면에서 hello Azure 컨테이너 서비스 DC/OS 클러스터에서 새 컨테이너 또는 다른 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="1e6d0-122">컨테이너 및 응용 프로그램을 실행하는 방법에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-122">You can also see information about running containers and applications.</span></span>  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="1e6d0-124">Docker로 포맷된 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="1e6d0-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="1e6d0-125">toodeploy 마라톤을 사용 하 여 새 컨테이너를 클릭 하 여 **응용 프로그램 만들기**, hello hello 양식 탭에 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="1e6d0-126">필드</span><span class="sxs-lookup"><span data-stu-id="1e6d0-126">Field</span></span> | <span data-ttu-id="1e6d0-127">값</span><span class="sxs-lookup"><span data-stu-id="1e6d0-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1e6d0-128">ID</span><span class="sxs-lookup"><span data-stu-id="1e6d0-128">ID</span></span> |<span data-ttu-id="1e6d0-129">nginx</span><span class="sxs-lookup"><span data-stu-id="1e6d0-129">nginx</span></span> |
| <span data-ttu-id="1e6d0-130">메모리</span><span class="sxs-lookup"><span data-stu-id="1e6d0-130">Memory</span></span> | <span data-ttu-id="1e6d0-131">32</span><span class="sxs-lookup"><span data-stu-id="1e6d0-131">32</span></span> |
| <span data-ttu-id="1e6d0-132">이미지</span><span class="sxs-lookup"><span data-stu-id="1e6d0-132">Image</span></span> |<span data-ttu-id="1e6d0-133">nginx</span><span class="sxs-lookup"><span data-stu-id="1e6d0-133">nginx</span></span> |
| <span data-ttu-id="1e6d0-134">네트워크</span><span class="sxs-lookup"><span data-stu-id="1e6d0-134">Network</span></span> |<span data-ttu-id="1e6d0-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="1e6d0-135">Bridged</span></span> |
| <span data-ttu-id="1e6d0-136">호스트 포트</span><span class="sxs-lookup"><span data-stu-id="1e6d0-136">Host Port</span></span> |<span data-ttu-id="1e6d0-137">80</span><span class="sxs-lookup"><span data-stu-id="1e6d0-137">80</span></span> |
| <span data-ttu-id="1e6d0-138">프로토콜</span><span class="sxs-lookup"><span data-stu-id="1e6d0-138">Protocol</span></span> |<span data-ttu-id="1e6d0-139">TCP</span><span class="sxs-lookup"><span data-stu-id="1e6d0-139">TCP</span></span> |

![새 응용 프로그램 UI--일반](./media/container-service-mesos-marathon-ui/dcos4.png)

![새 응용 프로그램 UI--Docker 컨테이너](./media/container-service-mesos-marathon-ui/dcos5.png)

![새 응용 프로그램 UI--포트 및 서비스 검색](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="1e6d0-143">Toostatically hello 컨테이너 포트 tooa 포트 매핑 hello 에이전트에서 원하는 경우 toouse JSON 모드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="1e6d0-144">toodo 따라서 전환 hello 새 응용 프로그램 마법사 너무**JSON 모드** hello 설정/해제를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="1e6d0-145">Hello hello에서 설정은 다음에 enter `portMappings` hello 응용 프로그램 정의의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="1e6d0-146">이 예에서는 hello DC/OS 에이전트의 hello 컨테이너 tooport 80의 포트 80을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="1e6d0-147">이렇게 변경한 후에 이 마법사를 JSON 모드에서 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![새 응용 프로그램 UI--포트 80 예제](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="1e6d0-149">Tooenable 상태 검사를 하려는 경우 hello에 경로 설정 **상태 검사** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![새 응용 프로그램 UI--상태 검사](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="1e6d0-151">hello DC/OS 클러스터는 개인 및 공용 에이전트 집합을 함께 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="1e6d0-152">Hello 클러스터 toobe 수 tooaccess 응용 프로그램에서 인터넷 hello toodeploy hello 응용 프로그램 tooa 공용 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="1e6d0-153">toodo hello를 따라서 선택 **옵션** hello 새 응용 프로그램 마법사의 탭 하 고 입력 **slave_public** hello에 대 한 **리소스 역할 수락**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="1e6d0-154">그런 다음 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-154">Then click **Create Application**.</span></span>

![새 응용 프로그램 UI--공용 에이전트 설정](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="1e6d0-156">Hello 마라톤 기본 페이지에서 다시 hello 컨테이너에 대 한 hello 배포 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="1e6d0-157">처음에는 **배포 중** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="1e6d0-158">배포 된 후 상태를 변경할 수을 너무 hello**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Marathon 기본 페이지 UI--컨테이너 배포 상태](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="1e6d0-160">뒤로 toohello DC/OS 웹 UI http://localhost/ 전환 하면 hello DC/OS 클러스터에서 작업 (이 경우 Docker로 포맷 된 컨테이너)에 실행 되 고 있는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![DC/OS 웹 UI-hello 클러스터에서 실행 중인 작업](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="1e6d0-162">실행 되 고 작업을 hello toosee hello 클러스터 노드를 hello 클릭 **노드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![DC/OS 웹 UI--작업 클러스터 노드](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="1e6d0-164">Hello 컨테이너에 도달</span><span class="sxs-lookup"><span data-stu-id="1e6d0-164">Reach hello container</span></span>

<span data-ttu-id="1e6d0-165">이 예제에서는 공용 에이전트 노드에서 hello 응용 프로그램 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="1e6d0-166">Hello에서 hello 응용 프로그램에 도달 하면 toohello hello 클러스터의 에이전트를 검색 하 여 인터넷: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, 여기서:</span><span class="sxs-lookup"><span data-stu-id="1e6d0-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="1e6d0-167">**DNSPREFIX** hello 클러스터를 배포할 때 제공 하는 hello DNS 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="1e6d0-168">**지역** 리소스 그룹의 위치를 가리키는 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1e6d0-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![인터넷의 Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="1e6d0-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e6d0-170">Next steps</span></span>
* [<span data-ttu-id="1e6d0-171">DC/OS를 사용 하 고 hello 마라톤 API</span><span class="sxs-lookup"><span data-stu-id="1e6d0-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="1e6d0-172">Azure 컨테이너 서비스 Mesos hello에 대 한 고찰</span><span class="sxs-lookup"><span data-stu-id="1e6d0-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
