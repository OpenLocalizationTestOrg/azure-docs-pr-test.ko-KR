---
title: "풀 마라톤 REST API와 aaaManage Azure DC/OS 클러스터 | Microsoft Docs"
description: "Hello 마라톤 REST API를 사용 하 여 컨테이너 tooan Azure 컨테이너 서비스 DC/OS 클러스터를 배포 합니다."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="10b16-104">Hello 마라톤 REST API를 통해 DC/OS 컨테이너 관리</span><span class="sxs-lookup"><span data-stu-id="10b16-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="10b16-105">DC/OS를 배포 및 hello 기본 하드웨어를 추상화 하는 동안 클러스터 된 작업 확장에 대 한 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="10b16-106">DC/OS의 상단에 계산 워크로드의 예약 및 실행을 관리하는 프레임워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="10b16-107">프레임 워크는 다양 한 인기 있는 작업에 사용할 수 있는,이 문서를 만들고 컨테이너 배포 hello 마라톤 REST API를 사용 하 여 크기 조정 시작 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="10b16-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="10b16-108">Prerequisites</span></span>

<span data-ttu-id="10b16-109">이러한 예제를 통해 작업하기 전에 Azure 컨테이너 서비스에 구성된 DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="10b16-110">Toohave 원격 연결 toothis 클러스터도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="10b16-111">이러한 항목에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="10b16-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="10b16-112">Azure 컨테이너 서비스 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="10b16-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="10b16-113">Tooan Azure 컨테이너 서비스 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="10b16-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="10b16-114">Hello DC/OS Api 액세스</span><span class="sxs-lookup"><span data-stu-id="10b16-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="10b16-115">연결 된 toohello Azure 컨테이너 서비스 클러스터 후 http://localhost:local 포트를 통해 hello DC/OS 및 관련된 REST Api에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="10b16-116">이 문서에 hello 예제 포트 80에서 터널링 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="10b16-117">예를 들어 hello 마라톤 끝점에 연결할 수 Uri에서 부터는 `http://localhost/marathon/v2/`합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="10b16-118">Hello에 대 한 자세한 내용은 다양 한 Api 참조 hello에 대 한 hello Mesosphere 설명서 [마라톤 API](https://mesosphere.github.io/marathon/docs/rest-api.html) 및 [Chronos API](https://mesos.github.io/chronos/docs/api.html), 및 hello에 대 한 Apache 설명서 [Mesos 스케줄러 API ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="10b16-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="10b16-119">DC/OS 및 Marathon에서 정보 수집</span><span class="sxs-lookup"><span data-stu-id="10b16-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="10b16-120">컨테이너 toohello DC/OS 클러스터를 배포 하기 전에 hello 이름 및 hello DC/OS 에이전트의 상태와 같은 hello DC/OS 클러스터에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="10b16-121">toodo hello를 따라서 쿼리 `master/slaves` hello DC/OS REST API의 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="10b16-122">모든 코드가 정상적으로 작동 하는 경우 hello 쿼리 각각에 대 한 DC/OS 에이전트와 여러 가지 속성의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="10b16-123">이제 풀 마라톤 hello를 사용 하 여 `/apps` 현재 응용 프로그램 배포 toohello DC/OS 클러스터에 대 한 끝점 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="10b16-124">새 클러스터인 경우에 앱에 대한 빈 배열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="10b16-125">Docker로 포맷된 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="10b16-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="10b16-126">의도 한 hello 배포 설명 하는 JSON 파일을 사용 하 여 hello 마라톤 REST API를 통해 Docker로 포맷 된 컨테이너를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="10b16-127">hello 다음 샘플 배포 hello 클러스터에서 Nginx 컨테이너 tooa 개인 에이전트 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="10b16-128">toodeploy Docker로 포맷 된 컨테이너에 액세스할 수 있는 위치에 hello JSON 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="10b16-129">그런 다음, toodeploy hello 컨테이너 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="10b16-130">Hello JSON 파일의 hello 이름 지정 (`marathon.json` 이 예에서).</span><span class="sxs-lookup"><span data-stu-id="10b16-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="10b16-131">hello 출력은 toohello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="10b16-132">이제 응용 프로그램에 대 한 풀 마라톤을 쿼리 하는 경우이 새 응용 프로그램 hello 출력에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="10b16-133">Hello 컨테이너에 도달</span><span class="sxs-lookup"><span data-stu-id="10b16-133">Reach hello container</span></span>

<span data-ttu-id="10b16-134">해당 hello hello 클러스터의 hello 개인 에이전트 중 하나에 컨테이너에서 Nginx 실행은 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="10b16-135">toofind hello 호스트와 hello 컨테이너가 실행 되는 포트 작업을 실행 하는 hello에 대 한 풀 마라톤 쿼리:</span><span class="sxs-lookup"><span data-stu-id="10b16-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="10b16-136">hello 값을 찾습니다 `host` hello 출력에 (너무는 IP 주소와 비슷한`10.32.0.x`), 및의 hello 값 `ports`합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="10b16-137">SSH 터미널 연결 (터널링 된 연결이 아닌) toohello 관리 FQDN hello 클러스터의 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="10b16-138">연결 되 면 확인 요청에 따라, hello의 올바른 값으로 대체 hello `host` 및 `ports`:</span><span class="sxs-lookup"><span data-stu-id="10b16-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="10b16-139">hello Nginx 서버 출력은 유사한 toohello 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-139">hello Nginx server output is similar toohello following:</span></span>

![컨테이너의 Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="10b16-141">컨테이너 확장</span><span class="sxs-lookup"><span data-stu-id="10b16-141">Scale your containers</span></span>
<span data-ttu-id="10b16-142">응용 프로그램 배포에서 초과 hello 마라톤 API tooscale 전체 자릿수 또는 소수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="10b16-143">Hello 앞의 예제 응용 프로그램의 한 인스턴스를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="10b16-144">이 응용 프로그램의 toothree 인스턴스를 확장 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="10b16-145">따라서 toodo JSON 파일 JSON 텍스트를 다음 hello를 사용 하 여 만들고 액세스할 수 있는 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="10b16-146">터널링 된 연결에서 명령 tooscale hello 신청서를 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="10b16-147">hello URI는 http://localhost/marathon/v2/apps/ hello 응용 프로그램 tooscale의 hello ID 옵니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="10b16-148">제공 하는 hello Nginx 샘플 여기 사용 하는 경우 URI hello http://localhost/marathon/v2/apps/nginx입니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="10b16-149">마지막으로, 응용 프로그램에 대 한 hello 마라톤 끝점을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="10b16-150">이제 세 가지 Nginx 컨테이너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="10b16-151">동일한 PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="10b16-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="10b16-152">Windows 시스템에서 PowerShell 명령을 사용하여 이러한 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="10b16-153">에이전트 이름 및 에이전트 상태를 같은 hello DC/OS 클러스터에 대 한 정보 toogather hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="10b16-154">의도 한 hello 배포 설명 하는 JSON 파일을 사용 하 여 풀 마라톤을 통해 Docker로 포맷 된 컨테이너를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="10b16-155">hello 다음 샘플 배포의 hello DC/OS 에이전트 tooport 80 hello 컨테이너의 포트 80을 바인딩 hello Nginx 컨테이너 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="10b16-156">toodeploy Docker로 포맷 된 컨테이너에 액세스할 수 있는 위치에 hello JSON 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="10b16-157">그런 다음, toodeploy hello 컨테이너 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="10b16-158">Hello toohello JSON 파일 경로 지정 (`marathon.json` 이 예에서).</span><span class="sxs-lookup"><span data-stu-id="10b16-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="10b16-159">또한 out hello 마라톤 API tooscale 전체 자릿수 또는 소수 응용 프로그램 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="10b16-160">Hello 앞의 예제 응용 프로그램의 한 인스턴스를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="10b16-161">이 응용 프로그램의 toothree 인스턴스를 확장 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="10b16-162">따라서 toodo JSON 파일 JSON 텍스트를 다음 hello를 사용 하 여 만들고 액세스할 수 있는 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="10b16-163">Hello 명령 tooscale hello 신청서를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="10b16-164">hello URI는 http://localhost/marathon/v2/apps/ hello 응용 프로그램 tooscale의 hello ID 옵니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="10b16-165">제공 된 hello Nginx 샘플 여기 사용 하는 경우 URI hello http://localhost/marathon/v2/apps/nginx입니다.</span><span class="sxs-lookup"><span data-stu-id="10b16-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="10b16-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10b16-166">Next steps</span></span>
* [<span data-ttu-id="10b16-167">Hello Mesos HTTP 끝점에 대 한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="10b16-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="10b16-168">Hello 마라톤 REST API에 대 한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="10b16-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

