---
title: "Azure Container Service 자습서 - 응용 프로그램 배포 | Microsoft Docs"
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
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="d4c68-104">Kubernetes에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d4c68-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="d4c68-105">7개 중 4단계인 이 자습서에서는 응용 프로그램 예제를 Kubernetes 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="d4c68-106">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4c68-107">Kubernetes 매니페스트 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="d4c68-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="d4c68-108">Kubernetes에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d4c68-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="d4c68-109">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d4c68-109">Test the application</span></span>

<span data-ttu-id="d4c68-110">후속 자습서에서는 이 응용 프로그램을 스케일 아웃하고 업데이트하며, Kubernetes 클러스터를 모니터링하도록 Operations Management Suite를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="d4c68-111">이 자습서에서는 Kubernetes 개념에 대한 기본적인 이해가 있다고 가정하며 Kubernetes에 대한 자세한 정보는 [Kubernetes 설명서](https://kubernetes.io/docs/home/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4c68-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d4c68-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d4c68-112">Before you begin</span></span>

<span data-ttu-id="d4c68-113">이전 자습서에서는 응용 프로그램을 컨테이너 이미지에 패키지하고, Azure Container Registry에 이러한 이미지를 업로드하고, Kubernetes 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="d4c68-114">이러한 단계를 수행하지 않은 경우 수행하려면 [자습서 1 - 컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="d4c68-115">최소한 이 자습서에는 Kubernetes 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="d4c68-116">매니페스트 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="d4c68-116">Get manifest file</span></span>

<span data-ttu-id="d4c68-117">이 자습서에서는 Kubernetes 매니페스트를 사용하여 [Kubernetes 개체](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="d4c68-118">Kubernetes 매니페스트는 Kubernetes 개체 배포 및 구성 지침이 포함된 YAML 또는 JSON 형식이 지정된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="d4c68-119">이 자습서의 응용 프로그램 매니페스트 파일은 이전 자습서에서 복제된 Azure Vote 응용 프로그램 리포지토리에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="d4c68-120">아직 이 리포지토리를 복제하지 않은 경우 다음 명령을 사용하여 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="d4c68-121">매니페스트 파일은 복제된 리포지토리의 다음 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="d4c68-122">매니페스트 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="d4c68-122">Update manifest file</span></span>

<span data-ttu-id="d4c68-123">Azure Container Registry를 사용하여 컨테이너 이미지를 저장하는 경우 매니페스트를 ACR loginServer 이름으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="d4c68-124">[az acr list](/cli/azure/acr#list) 명령을 사용하여 ACR 로그인 서버 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="d4c68-125">샘플 매니페스트를 *microsoft*라는 리포지토리 이름으로 미리 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="d4c68-126">텍스트 편집기로 파일을 열고 *microsoft* 값을 ACR 인스턴스의 로그인 서버 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="d4c68-127">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d4c68-127">Deploy application</span></span>

<span data-ttu-id="d4c68-128">[kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) 명령을 사용하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="d4c68-129">이 명령은 매니페스트 파일을 구문 분석하고 정의된 Kubernetes 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="d4c68-130">출력:</span><span class="sxs-lookup"><span data-stu-id="d4c68-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="d4c68-131">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d4c68-131">Test application</span></span>

<span data-ttu-id="d4c68-132">인터넷에 응용 프로그램을 노출하는 [Kubernetes 서비스](https://kubernetes.io/docs/concepts/services-networking/service/)가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="d4c68-133">이 프로세스는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="d4c68-134">진행 상태를 모니터링하려면 `--watch` 인수와 함께 [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="d4c68-135">처음에는 *azure-vote-front* 서비스에 대한 **EXTERNAL-IP**가 *보류 중*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="d4c68-136">EXTERNAL-IP 주소가 *보류 중*에서 *IP 주소*로 변경되면 `CTRL-C`를 사용하여 kubectl 조사식 프로세스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="d4c68-137">응용 프로그램을 보려면 외부 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-137">To see the application, browse to the external IP address.</span></span>

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="d4c68-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4c68-139">Next steps</span></span>

<span data-ttu-id="d4c68-140">이 자습서에서는 Azure 투표 응용 프로그램을 Azure Container Service Kubernetes 클러스터에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="d4c68-141">완료된 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="d4c68-142">Kubernetes 매니페스트 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="d4c68-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="d4c68-143">Kubernetes에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d4c68-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="d4c68-144">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="d4c68-144">Tested the application</span></span>

<span data-ttu-id="d4c68-145">다음 자습서로 이동하여 Kubernetes 응용 프로그램과 기본 Kubernetes 인프라를 모두 크기 조정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4c68-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4c68-146">Kubernetes 응용 프로그램 및 인프라 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d4c68-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)