---
title: "Azure Kubernetes에 투구를 사용 하 여 aaaDeploy 컨테이너 | Microsoft Docs"
description: "Azure 컨테이너 서비스의 Kubernetes 클러스터에서 hello 투구 패키징 도구 toodeploy 컨테이너를 사용 하 여"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="e593f-103">투구 toodeploy 컨테이너 Kubernetes 클러스터에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e593f-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="e593f-104">[투구](https://github.com/kubernetes/helm/) 설치 하 고 hello Kubernetes 응용 프로그램 수명 주기를 관리할 때 도움이 되는 오픈 소스 패키징 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="e593f-105">예: Apt get 및 Yum 비슷한 tooLinux 패키지 관리자 투구 패키지인 미리 구성 된 Kubernetes 리소스의 사용 되는 toomanage Kubernetes 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="e593f-106">이 문서 toowork 투구와 Kubernetes 클러스터에서 Azure 컨테이너 서비스에 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="e593f-107">Helm에는 두 가지 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-107">Helm has two components:</span></span> 
* <span data-ttu-id="e593f-108">hello **투구 CLI** hello 클라우드 또는 로컬 컴퓨터에서 실행 되는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e593f-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="e593f-109">**Tiller** 는 hello Kubernetes 클러스터에서 실행 되 고 Kubernetes 응용 프로그램의 hello 수명 주기 관리 하는 서버</span><span class="sxs-lookup"><span data-stu-id="e593f-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="e593f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e593f-110">Prerequisites</span></span>

* <span data-ttu-id="e593f-111">Azure Container Service에서 [Kubernetes 클러스터 생성](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="e593f-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="e593f-112">로컬 컴퓨터에서 [설치 및 구성`kubectl`](../container-service-connect.md)</span><span class="sxs-lookup"><span data-stu-id="e593f-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="e593f-113">로컬 컴퓨터에 [Helm 설치](https://github.com/kubernetes/helm/blob/master/docs/install.md)</span><span class="sxs-lookup"><span data-stu-id="e593f-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="e593f-114">Helm 기초</span><span class="sxs-lookup"><span data-stu-id="e593f-114">Helm basics</span></span> 

<span data-ttu-id="e593f-115">tooview 정보 hello Kubernetes 클러스터에 대 한 Tiller을 설치 하 고 hello 다음 명령을 입력 하 고 응용 프로그램의 배포:</span><span class="sxs-lookup"><span data-stu-id="e593f-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="e593f-117">투구를 설치한 후 hello 다음 명령을 입력 하 여 Tiller Kubernetes 클러스터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="e593f-118">성공적으로 완료 hello 다음과 같은 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-118">When it completes successfully, you see output like hello following:</span></span>

![Tiller 설치](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="e593f-120">모든 hello 투구 차트 사용할 수 있는 다음 형식 hello hello 리포지토리에 명령 tooview 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="e593f-121">Hello 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-121">You see output like hello following:</span></span>

![Helm 검색](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="e593f-123">tooupdate hello 차트 tooget hello 최신 버전을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="e593f-124">Nginx 수신 컨트롤러 차트 배포</span><span class="sxs-lookup"><span data-stu-id="e593f-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="e593f-125">toodeploy Nginx 수신 컨트롤러 차트는 단일 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![수신 컨트롤러 배포](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="e593f-127">입력 하는 경우 `kubectl get svc` tooview IP 주소 toohello 수신 컨트롤러에 할당 되어 있는지 확인할 hello 클러스터에서 실행 되는 모든 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="e593f-128">(참조 hello 할당 진행 중이면 `<pending>`합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="e593f-129">걸리는 시간은 몇 분 toocomplete 가지.)</span><span class="sxs-lookup"><span data-stu-id="e593f-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="e593f-130">Hello IP 주소를 할당 한 후 이동 toohello 값 hello 외부 IP 주소 toosee hello Nginx 백 엔드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![수신 IP 주소](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="e593f-132">클러스터를 형식에 설치 하는 막대형 차트의 목록 toosee:</span><span class="sxs-lookup"><span data-stu-id="e593f-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="e593f-133">Hello 명령 너무 축약할 수 있습니다`helm ls`합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="e593f-134">MariaDB 차트 및 클라이언트 배포</span><span class="sxs-lookup"><span data-stu-id="e593f-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="e593f-135">이제 MariaDB 차트 및 MariaDB 클라이언트 tooconnect toohello 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="e593f-136">toodeploy hello MariaDB 차트에서 다음 명령을 형식 hello:</span><span class="sxs-lookup"><span data-stu-id="e593f-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="e593f-137">여기서 `--name`은 릴리스에 사용되는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="e593f-138">Hello 배포가 실패 하는 경우 실행 `helm repo update` 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e593f-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="e593f-139">tooview 형식 클러스터에 배포 된 모든 hello 차트:</span><span class="sxs-lookup"><span data-stu-id="e593f-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="e593f-140">tooview 클러스터에서 실행 중인 모든 배포를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="e593f-141">마지막으로, toorun pod tooaccess hello 클라이언트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="e593f-142">tooconnect toohello 클라이언트에서 다음 명령을, 대체 형식 hello `v1-mariadb` 배포의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="e593f-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="e593f-143">이제 표준 SQL 명령 toocreate 데이터베이스, 테이블 등을 사용할 수 있습니다. 예를 들어 `Create DATABASE testdb1;`은 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="e593f-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e593f-144">Next steps</span></span>

* <span data-ttu-id="e593f-145">Kubernetes 차트를 관리 하는 방법에 대 한 자세한 내용은 참조 hello [투구 설명서](https://github.com/kubernetes/helm/blob/master/docs/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e593f-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

