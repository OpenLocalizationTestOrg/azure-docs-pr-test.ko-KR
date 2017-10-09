---
title: "aaaAzure 컨테이너 서비스 자습서-업데이트 응용 프로그램 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 업데이트"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="d7ca4-104">Kubernetes에서 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="d7ca4-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="d7ca4-105">Kubernetes에서 응용 프로그램을 배포한 후 새 컨테이너 이미지 또는 이미지 버전을 지정하여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="d7ca4-106">응용 프로그램을 업데이트 하면 hello 배포의 일부분만 동시에 업데이트 되도록 hello 업데이트 배포를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="d7ca4-107">준비 된이 업데이트 hello 응용 프로그램 tookeep hello 업데이트 하는 동안 실행을 사용 하도록 설정 하 고 배포 오류가 발생 하는 경우는 롤백 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="d7ca4-108">이 자습서에서는 6, 7 개의 hello 샘플 Azure 투표 응용 프로그램의 일부 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="d7ca4-109">완료하는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7ca4-110">Hello 프런트 엔드 응용 프로그램 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="d7ca4-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="d7ca4-111">업데이트된 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d7ca4-111">Creating an updated container image</span></span>
> * <span data-ttu-id="d7ca4-112">푸시 hello 컨테이너 이미지 tooAzure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="d7ca4-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="d7ca4-113">Hello 업데이트 된 컨테이너 이미지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-113">Deploying hello updated container image</span></span>

<span data-ttu-id="d7ca4-114">후속 자습서에서는 Operations Management Suite은 구성 된 toomonitor hello Kubernetes 클러스터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d7ca4-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d7ca4-115">Before you begin</span></span>

<span data-ttu-id="d7ca4-116">이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램, 컨테이너 레지스트리 tooAzure 및 만들어진 Kubernetes 클러스터 hello 이미지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="d7ca4-117">그런 다음 hello 응용 프로그램 hello Kubernetes 클러스터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="d7ca4-118">이 단계를 완료 하지 않은 toofollow와 함께 사용할 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="d7ca4-119">응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="d7ca4-119">Update application</span></span>

<span data-ttu-id="d7ca4-120">이 자습서를 toocomplete hello 단계 해야 복제 hello Azure 투표 응용 프로그램의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="d7ca4-121">필요한 경우 다음 명령을 hello로이 복제 된 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="d7ca4-122">열기 hello `config_file.cfg` 코드 또는 텍스트 편집기로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="d7ca4-123">Hello 복제 hello 리포지토리의 디렉터리를 다음으로이 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="d7ca4-124">Hello 값을 변경 `VOTE1VALUE` 및 `VOTE2VALUE`, hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="d7ca4-125">사용 하 여 [docker 작성](https://docs.docker.com/compose/) toore-hello 프런트 엔드 이미지 및 업데이트 실행된 hello 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="d7ca4-126">로컬에서 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d7ca4-126">Test application locally</span></span>

<span data-ttu-id="d7ca4-127">너무 찾아보기`http://localhost:8080` toosee hello 응용 프로그램을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="d7ca4-129">이미지 태그 지정 및 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="d7ca4-129">Tag and push images</span></span>

<span data-ttu-id="d7ca4-130">태그 hello *azure 투표 프런트* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="d7ca4-131">Azure 컨테이너 레지스트리를 사용 하 여 hello로 hello 로그인 서버 이름을 가져오는 [az acr 목록](/cli/azure/acr#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="d7ca4-132">사용 하 여 [docker 태그](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="d7ca4-133">`<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="d7ca4-134">사용 하 여 [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello 이미지 tooyour 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="d7ca4-135">`<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="d7ca4-136">업데이트된 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d7ca4-136">Deploy update application</span></span>

<span data-ttu-id="d7ca4-137">tooensure 최대 가동 시간 hello 응용 프로그램 pod의 여러 인스턴스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="d7ca4-138">Hello로이 구성을 확인 [kubectl 가져오기 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="d7ca4-139">출력:</span><span class="sxs-lookup"><span data-stu-id="d7ca4-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="d7ca4-140">Hello azure 투표 프런트 이미지를 실행 하는 여러 포드를 설정 하지 않은 경우 확장 hello *azure 투표 프런트* 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="d7ca4-141">tooupdate hello 응용 프로그램을 사용 하 여 hello [kubectl 집합](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="d7ca4-142">업데이트 `<acrLoginServer>` 컨테이너 레지스트리 hello 로그인 서버 또는 호스트 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="d7ca4-143">toomonitor hello 배포를 사용 하 여 hello [kubectl 가져오기 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="d7ca4-144">Hello 업데이트 응용 프로그램을 배포할 때 사용자 포드 종료 되 고 hello 새 컨테이너 이미지를 사용 하 여 다시 만든 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="d7ca4-145">출력:</span><span class="sxs-lookup"><span data-stu-id="d7ca4-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="d7ca4-146">업데이트된 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d7ca4-146">Test updated application</span></span>

<span data-ttu-id="d7ca4-147">Hello hello의 외부 IP 주소 가져오기 *azure 투표 프런트* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="d7ca4-148">찾아보기 toohello IP 주소 toosee hello 응용 프로그램을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-148">Browse toohello IP address toosee hello updated application.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="d7ca4-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7ca4-150">Next steps</span></span>

<span data-ttu-id="d7ca4-151">이 자습서에서는 응용 프로그램을 업데이트 하 고이 업데이트 tooa Kubernetes 클러스터에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="d7ca4-152">작업을 수행 하는 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7ca4-153">업데이트 된 hello 프런트 엔드 응용 프로그램 코드</span><span class="sxs-lookup"><span data-stu-id="d7ca4-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="d7ca4-154">업데이트된 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d7ca4-154">Created an updated container image</span></span>
> * <span data-ttu-id="d7ca4-155">Hello 컨테이너 이미지 tooAzure 컨테이너 레지스트리 푸시</span><span class="sxs-lookup"><span data-stu-id="d7ca4-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="d7ca4-156">업데이트는 배포 된 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d7ca4-156">Deployed hello updated application</span></span>

<span data-ttu-id="d7ca4-157">이동 하는 방법에 대 한 다음 자습서 toolearn toohello toomonitor Operations Management Suite로 Kubernetes 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ca4-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7ca4-158">OMS로 Kubernetes 모니터링</span><span class="sxs-lookup"><span data-stu-id="d7ca4-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)