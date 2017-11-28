---
title: "Azure Container Service 자습서 - 응용 프로그램 업데이트 | Microsoft Docs"
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
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="0fa17-104">Kubernetes에서 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="0fa17-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="0fa17-105">Kubernetes에서 응용 프로그램을 배포한 후 새 컨테이너 이미지 또는 이미지 버전을 지정하여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="0fa17-106">응용 프로그램을 업데이트할 때 배포의 일부분만 동시에 업데이트되도록 업데이트 출시가 스테이징됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-106">When you update an application, the update rollout is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="0fa17-107">이 스테이징된 업데이트를 사용하면 업데이트 동안 응용 프로그램을 실행 중 상태로 유지할 수 있으며 배포 오류가 발생할 경우 롤백 메커니즘이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-107">This staged update enables the application to keep running during the update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="0fa17-108">이 자습서(전체 7부 중 6부)에서는 샘플 Azure 투표 앱을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="0fa17-109">완료하는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fa17-110">프런트 엔드 응용 프로그램 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="0fa17-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="0fa17-111">업데이트된 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0fa17-111">Creating an updated container image</span></span>
> * <span data-ttu-id="0fa17-112">Azure Container Registry에 컨테이너 이미지 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="0fa17-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="0fa17-113">업데이트된 컨테이너 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="0fa17-113">Deploying the updated container image</span></span>

<span data-ttu-id="0fa17-114">후속 자습서에서는 Kubernetes 클러스터를 모니터링하도록 Operations Management Suite를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0fa17-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0fa17-115">Before you begin</span></span>

<span data-ttu-id="0fa17-116">이전 자습서에서는 응용 프로그램을 컨테이너 이미지에 패키지하고, Azure Container Registry에 이러한 이미지를 업로드하고, Kubernetes 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="0fa17-117">그런 다음 Kubernetes 클러스터에서 응용 프로그램을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="0fa17-118">이러한 단계를 완료하지 않은 경우 수행하려면 [자습서 1 - 컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-118">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="0fa17-119">응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="0fa17-119">Update application</span></span>

<span data-ttu-id="0fa17-120">이 자습서의 단계를 완료하려면 Azure 투표 응용 프로그램의 복사본을 복제한 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-120">To complete the steps in this tutorial, you must have cloned a copy of the Azure Vote application.</span></span> <span data-ttu-id="0fa17-121">필요한 경우 다음 명령을 사용하여 이 복제된 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-121">If necessary, create this cloned copy with the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="0fa17-122">아무 코드 또는 텍스트 편집기나 사용하여 `config_file.cfg` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-122">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="0fa17-123">복제된 리포지토리의 다음 디렉터리에서 이 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-123">You can find this file under the following directory of the cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="0fa17-124">`VOTE1VALUE` 및 `VOTE2VALUE`의 값을 변경한 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-124">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="0fa17-125">[docker-compose](https://docs.docker.com/compose/)를 사용하여 프런트 엔드 이미지를 다시 만들고 업데이트된 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-125">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="0fa17-126">로컬에서 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="0fa17-126">Test application locally</span></span>

<span data-ttu-id="0fa17-127">`http://localhost:8080`으로 이동하여 업데이트된 응용 프로그램을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-127">Browse to `http://localhost:8080` to see the updated application.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="0fa17-129">이미지 태그 지정 및 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="0fa17-129">Tag and push images</span></span>

<span data-ttu-id="0fa17-130">*azure-vote-front* 이미지에 컨테이너 레지스트리의 loginServer로 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-130">Tag the *azure-vote-front* image with the loginServer of the container registry.</span></span>

<span data-ttu-id="0fa17-131">Azure Container Registry를 사용 중인 경우 [az acr list](/cli/azure/acr#list) 명령을 사용하여 로그인 서버 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-131">If you're using Azure Container Registry, get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="0fa17-132">[docker tag](https://docs.docker.com/engine/reference/commandline/tag/)를 사용하여 이미지에 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="0fa17-133">`<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="0fa17-134">[docker push](https://docs.docker.com/engine/reference/commandline/push/)를 사용하여 레지스트리에 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="0fa17-135">`<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="0fa17-136">업데이트된 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="0fa17-136">Deploy update application</span></span>

<span data-ttu-id="0fa17-137">최대 작동 시간을 보장하려면 응용 프로그램 Pod의 여러 인스턴스가 실행되고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-137">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="0fa17-138">[kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령을 사용하여 이 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-138">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="0fa17-139">출력:</span><span class="sxs-lookup"><span data-stu-id="0fa17-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="0fa17-140">azure-vote-front 이미지를 실행 중인 여러 Pod가 없는 경우 *azure-vote-front* 배포를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-140">If you don't have multiple pods running the azure-vote-front image, scale the *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="0fa17-141">응용 프로그램을 업데이트하려면 [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-141">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="0fa17-142">`<acrLoginServer>`를 컨테이너 레지스트리의 로그인 서버 또는 호스트 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-142">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="0fa17-143">배포를 모니터링하려면 [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-143">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="0fa17-144">업데이트된 응용 프로그램이 배포되면 Pod가 종료되고 새 컨테이너 이미지로 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-144">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="0fa17-145">출력:</span><span class="sxs-lookup"><span data-stu-id="0fa17-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="0fa17-146">업데이트된 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="0fa17-146">Test updated application</span></span>

<span data-ttu-id="0fa17-147">*azure-vote-front* 서비스의 외부 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-147">Get the external IP address of the *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="0fa17-148">IP 주소로 이동하여 업데이트된 응용 프로그램을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-148">Browse to the IP address to see the updated application.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="0fa17-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fa17-150">Next steps</span></span>

<span data-ttu-id="0fa17-151">이 자습서에서는 응용 프로그램을 업데이트하고 이 업데이트를 Kubernetes 클러스터에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-151">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="0fa17-152">다음 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-152">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fa17-153">프런트 엔드 응용 프로그램 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="0fa17-153">Updated the front-end application code</span></span>
> * <span data-ttu-id="0fa17-154">업데이트된 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0fa17-154">Created an updated container image</span></span>
> * <span data-ttu-id="0fa17-155">Azure Container Registry에 컨테이너 이미지 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="0fa17-155">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="0fa17-156">업데이트된 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="0fa17-156">Deployed the updated application</span></span>

<span data-ttu-id="0fa17-157">다음 자습서로 이동하여 Operations Management Suite로 Kubernetes를 모니터링하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0fa17-157">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0fa17-158">OMS로 Kubernetes 모니터링</span><span class="sxs-lookup"><span data-stu-id="0fa17-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)