---
title: "웹 UI와 aaaManage Azure Kubernetes 클러스터 | Microsoft Docs"
description: "Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스의 UI"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="3dc67-103">Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스와 UI</span><span class="sxs-lookup"><span data-stu-id="3dc67-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dc67-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3dc67-104">Prerequisites</span></span>
<span data-ttu-id="3dc67-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="3dc67-106">또한 hello Azure CLI 2.0 있다고 가정 하 고 `kubectl` 도구가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="3dc67-107">Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="3dc67-108">Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="3dc67-109">Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="3dc67-110">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="3dc67-111">개요</span><span class="sxs-lookup"><span data-stu-id="3dc67-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="3dc67-112">Toohello 웹 UI를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-112">Connect toohello web UI</span></span>
<span data-ttu-id="3dc67-113">실행 하 여 hello Kubernetes 웹 UI를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="3dc67-114">로컬 컴퓨터 toohello Kubernetes 웹 UI를 연결 합니다. 웹 브라우저 구성 tootalk tooa 보안 프록시를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="3dc67-115">서비스 만들기 및 공개</span><span class="sxs-lookup"><span data-stu-id="3dc67-115">Create and expose a service</span></span>
1. <span data-ttu-id="3dc67-116">Hello Kubernetes 웹 UI에서에서 클릭 **만들기** hello 상단 오른쪽 창에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes 만들기 UI](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="3dc67-118">응용 프로그램을 만들기 시작할 수 있는 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="3dc67-119">Hello 이름을 `hello-nginx`합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="3dc67-120">사용 하 여 hello [ `nginx` 에서 Docker 컨테이너](https://hub.docker.com/_/nginx/) 하 고이 웹 서비스의 세 개의 복제본을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Kubernetes 포드 만들기 대화 상자](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="3dc67-122">**서비스**에서 **외부**를 선택하고 포트 80을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="3dc67-123">이 설정은 트래픽 toohello 세 개의 복제본에 부하를 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Kubernetes 서비스 만들기 대화 상자](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="3dc67-125">클릭 **배포** toodeploy 이러한 컨테이너 및 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Kubernetes 배포](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="3dc67-127">컨테이너 보기</span><span class="sxs-lookup"><span data-stu-id="3dc67-127">View your containers</span></span>
<span data-ttu-id="3dc67-128">클릭 한 후 **배포**, hello UI를 배포할 때 서비스의 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Kubernetes 상태](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="3dc67-130">Hello 원에는 각 Kubernetes 개체의 hello 상태 hello UI의 왼쪽 아래에서 확인할 수 있습니다 **포드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="3dc67-131">부분적으로 원이 이면 다음 hello 개체 여전히 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="3dc67-132">개체가 완전히 배포되면 녹색 확인 표시가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes가 배포됨](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="3dc67-134">모든 것이 실행 되 면 웹 서비스를 실행 하는 hello에 대 한 포드 toosee 회원님의 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Kubernetes 포드](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="3dc67-136">Hello에 **포드** 보기 이러한 컨테이너에서 사용 하는 hello CPU 및 메모리 리소스를 비롯 하 여 hello pod에 hello 컨테이너에 대 한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes 리소스](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="3dc67-138">Hello 리소스 보이지 않으면 해야 toowait 몇 분 정도 데이터 toopropagate 모니터링 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="3dc67-139">클릭 하 여 컨테이너에 대 한 toosee hello 로그 **로그를 볼**합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-139">toosee hello logs for your container, click **View logs**.</span></span>

![kubernetes 로그](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="3dc67-141">서비스 보기</span><span class="sxs-lookup"><span data-stu-id="3dc67-141">Viewing your service</span></span>
<span data-ttu-id="3dc67-142">또한 toorunning 컨테이너에서 hello Kubernetes UI 만들었습니다 외부 `Service` 클러스터는 부하 분산 장치 toobring 트래픽 toohello 컨테이너를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="3dc67-143">Hello 왼쪽된 탐색 창에서 클릭 **서비스** tooview 모든 서비스 (있어야 하나만).</span><span class="sxs-lookup"><span data-stu-id="3dc67-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Kubernetes 서비스](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="3dc67-145">해당 보기의 외부 끝점 (IP 주소) tooyour 서비스 할당 된 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="3dc67-146">해당 IP 주소를 클릭하면 부하 분산 장치 뒤에서 Nginx 컨테이너가 실행되는 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx 보기](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="3dc67-148">서비스 크기 조정</span><span class="sxs-lookup"><span data-stu-id="3dc67-148">Resizing your service</span></span>
<span data-ttu-id="3dc67-149">또한 tooviewing에 사용자 개체에 hello UI, 편집 하 고 hello Kubernetes API 개체를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="3dc67-150">먼저, 클릭 **배포** hello 남아 있는 서비스에 대 한 탐색 창 toosee hello 배포에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="3dc67-151">해당 보기에 있는 경우 hello 복제 세트에 클릭 한 다음 클릭 **편집** hello 위쪽 탐색 모음에서:</span><span class="sxs-lookup"><span data-stu-id="3dc67-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![kubernetes 편집](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="3dc67-153">Hello 편집 `spec.replicas` 필드 toobe `2`를 클릭 하 고 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="3dc67-154">따라서 프로그램 포드 중 하나를 삭제 하 여 복제본 toodrop tootwo hello 수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dc67-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

