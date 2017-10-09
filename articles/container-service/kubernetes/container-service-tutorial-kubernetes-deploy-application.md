---
title: "aaaAzure 컨테이너 서비스 자습서-응용 프로그램 배포 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 배포"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="b3738-104">Kubernetes에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b3738-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="b3738-105">7개 중 4단계인 이 자습서에서는 응용 프로그램 예제를 Kubernetes 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="b3738-106">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3738-107">Kubernetes 매니페스트 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3738-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="b3738-108">Kubernetes에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b3738-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="b3738-109">Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="b3738-109">Test hello application</span></span>

<span data-ttu-id="b3738-110">이후 자습서에서이 응용 프로그램은 확장 업데이트 하 고 Operations Management Suite toomonitor hello Kubernetes 클러스터 구성.</span><span class="sxs-lookup"><span data-stu-id="b3738-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="b3738-111">이 자습서에 Kubernetes 개념에 대 한 기본 지식이 있다고 가정, 참조 hello에 대 한 자세한 내용은 Kubernetes [Kubernetes 설명서](https://kubernetes.io/docs/home/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b3738-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b3738-112">Before you begin</span></span>

<span data-ttu-id="b3738-113">이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램 하 고이 이미지는 업로드 컨테이너 레지스트리 tooAzure Kubernetes 클러스터를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="b3738-114">다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="b3738-115">최소한 이 자습서에는 Kubernetes 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="b3738-116">매니페스트 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="b3738-116">Get manifest file</span></span>

<span data-ttu-id="b3738-117">이 자습서에서는 Kubernetes 매니페스트를 사용하여 [Kubernetes 개체](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="b3738-118">Kubernetes 매니페스트는 Kubernetes 개체 배포 및 구성 지침이 포함된 YAML 또는 JSON 형식이 지정된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="b3738-119">이 자습서에 대 한 hello 응용 프로그램 매니페스트 파일은 이전 자습서에서 복제 된 hello Azure 투표 응용 프로그램 리포지토리를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="b3738-120">이미 수행 하는 경우 다음 명령을 hello로 hello 리포지토리를 복제:</span><span class="sxs-lookup"><span data-stu-id="b3738-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="b3738-121">hello 매니페스트 파일은 복제 hello 리포지토리의 디렉터리를 다음 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="b3738-122">매니페스트 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="b3738-122">Update manifest file</span></span>

<span data-ttu-id="b3738-123">Azure 컨테이너 레지스트리 toostore hello 컨테이너 이미지를 사용 하는 경우 hello 매니페스트 요구 toobe hello ACR loginServer 이름으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="b3738-124">Hello로 hello ACR 로그인 서버 이름을 가져오는 [az acr 목록](/cli/azure/acr#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="b3738-125">hello 샘플 매니페스트 미리 만들었습니다 리포지토리 이름이 *microsoft*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="b3738-126">임의의 텍스트 편집기로 hello 파일을 열고 및 hello 바꾸기 *microsoft* hello ACR 인스턴스 로그인 서버 이름 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="b3738-127">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b3738-127">Deploy application</span></span>

<span data-ttu-id="b3738-128">사용 하 여 hello [kubectl 만들](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun hello 응용 프로그램 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="b3738-129">이 명령 구문 분석 하 여 hello 매니페스트 파일을 정의 된 hello Kubernetes 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="b3738-130">출력:</span><span class="sxs-lookup"><span data-stu-id="b3738-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="b3738-131">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="b3738-131">Test application</span></span>

<span data-ttu-id="b3738-132">A [Kubernetes 서비스](https://kubernetes.io/docs/concepts/services-networking/service/) hello 응용 프로그램 toohello를 노출 하는 만들어집니다 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="b3738-133">이 프로세스는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="b3738-134">toomonitor 진행 상황을 사용 하 여 hello [kubectl 서비스를 가져올](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) hello로 명령을 `--watch` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="b3738-135">처음에 hello **외부 IP** hello에 대 한 *azure 투표 프런트* 으로 서비스 나타납니다 *보류 중인*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="b3738-136">hello 외부 IP 주소가 변경 되 면 *보류 중인* tooan *IP 주소*를 사용 하 여 `CTRL-C` toostop hello kubectl 조사식 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="b3738-137">toosee hello 응용 프로그램, 찾아보기 toohello 외부 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-137">toosee hello application, browse toohello external IP address.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="b3738-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3738-139">Next steps</span></span>

<span data-ttu-id="b3738-140">이 자습서에서는 Azure 투표 응용 프로그램 hello tooan 배포 된 Azure 컨테이너 서비스 Kubernetes 클러스터 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="b3738-141">완료된 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="b3738-142">Kubernetes 매니페스트 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3738-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="b3738-143">Kubernetes에 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="b3738-144">테스트 된 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b3738-144">Tested hello application</span></span>

<span data-ttu-id="b3738-145">Kubernetes 응용 프로그램과 hello Kubernetes 인프라 내부 크기 조정 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3738-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3738-146">Kubernetes 응용 프로그램 및 인프라 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b3738-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)