---
title: "Azure에서 Kubernetes 컨테이너 부하 분산 | Microsoft Docs"
description: "외부에서 연결하고 Azure Container Service의 Kubernetes 클러스터에서 여러 컨테이너 간에 부하를 분산합니다."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, 마이크로 서비스, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="ef1dd-104">Azure Container Service의 Kubernetes 클러스터에서 컨테이너 부하 분산</span><span class="sxs-lookup"><span data-stu-id="ef1dd-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="ef1dd-105">이 문서에서는 Azure Container Service의 Kubernetes 클러스터에서 부하를 분산하는 과정을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="ef1dd-106">부하 분산 서비스는 서비스에 대해 외부에서 액세스할 수 있는 IP 주소를 제공하고 에이전트 VM에서 실행되는 Pod 간에 네트워크 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="ef1dd-107">[Azure Load Balancer](../../load-balancer/load-balancer-overview.md)를 사용하여 외부 네트워크(TCP) 트래픽을 관리하도록 Kubernetes 서비스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="ef1dd-108">추가 구성을 통해 HTTP 또는 HTTPS 트래픽의 부하 분산 및 라우팅이나 좀 더 고급 시나리오도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef1dd-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef1dd-109">Prerequisites</span></span>
* <span data-ttu-id="ef1dd-110">Azure Container Service에서 [Kubernetes 클러스터 배포](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="ef1dd-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="ef1dd-111">클러스터에 [클라이언트 연결](../container-service-connect.md)</span><span class="sxs-lookup"><span data-stu-id="ef1dd-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="ef1dd-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ef1dd-112">Azure load balancer</span></span>

<span data-ttu-id="ef1dd-113">기본적으로 Azure Container Service에 배포된 Kubernetes 클러스터에는 에이전트 VM에 대한 인터넷 연결 Azure Load Balancer가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="ef1dd-114">(마스터 VM에 대해서는 별도 부하 분산 장치 리소스가 구성됩니다.) Azure Load Balancer는 계층 4 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="ef1dd-115">현재 부하 분산 장치는 Kubernetes의 TCP 트래픽만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="ef1dd-116">Kubernetes 서비스를 만드는 경우 서비스에 대한 액세스를 허용하도록 Azure Load Balancer를 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="ef1dd-117">부하 분산 장치를 구성하려면 서비스 `type`을 `LoadBalancer`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="ef1dd-118">부하 분산 장치는 들어오는 서비스 트래픽의 공용 IP 주소 및 포트 번호를 에이전트 VM에 있는 Pod의 개인 IP 주소 및 포트 번호로 매핑(응답 트래픽의 경우 반대 방향으로 매핑)하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="ef1dd-119">다음은 Kubernetes 서비스 `type`을 `LoadBalancer`로 설정하는 방법을 보여 주는 두 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="ef1dd-120">(예제를 시도한 후 더 이상 필요하지 않은 배포는 삭제합니다.)</span><span class="sxs-lookup"><span data-stu-id="ef1dd-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="ef1dd-121">예제: `kubectl expose` 명령 사용</span><span class="sxs-lookup"><span data-stu-id="ef1dd-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="ef1dd-122">[Kubernetes 연습](container-service-kubernetes-walkthrough.md)에는 `kubectl expose` 명령 및 해당 `--type=LoadBalancer` 플래그를 사용하여 서비스를 노출하는 방법의 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="ef1dd-123">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-123">Here are the steps :</span></span>

1. <span data-ttu-id="ef1dd-124">새 컨테이너 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-124">Start a new container deployment.</span></span> <span data-ttu-id="ef1dd-125">예를 들어 다음 명령은 `mynginx`라는 새 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="ef1dd-126">배포에는 Nginx 웹 서버에 대한 Docker 이미지를 기준으로 하는 세 개의 컨테이너로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="ef1dd-127">컨테이너가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-127">Verify that the containers are running.</span></span> <span data-ttu-id="ef1dd-128">예를 들어 `kubectl get pods`를 사용하여 컨테이너를 쿼리하면 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Nginx 컨테이너 가져오기](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="ef1dd-130">배포에 대한 외부 트래픽을 허용하도록 부하 분산 장치를 구성하려면 `--type=LoadBalancer`를 사용하여 `kubectl expose`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="ef1dd-131">다음 명령은 포트 80에서 Nginx 서버를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="ef1dd-132">`kubectl get svc`를 입력하여 클러스터의 서비스 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="ef1dd-133">부하 분산 장치가 규칙을 구성하는 동안 서비스의 `EXTERNAL-IP`가 `<pending>`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="ef1dd-134">몇 분 후에 외부 IP 주소가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-134">After a few minutes, the external IP address is configured:</span></span> 

    ![Azure Load Balancer 구성](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="ef1dd-136">서비스에 외부 IP 주소로 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="ef1dd-137">예를 들어 표시되는 IP 주소로 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="ef1dd-138">브라우저는 컨테이너 중 하나에서 실행되는 Nginx 웹 서버를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="ef1dd-139">또는 `curl`이나 `wget` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="ef1dd-140">예:</span><span class="sxs-lookup"><span data-stu-id="ef1dd-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="ef1dd-141">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-141">You should see output similar to:</span></span>

    ![curl을 사용하여 Nginx에 액세스](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="ef1dd-143">Azure Load Balancer의 구성을 보려면 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="ef1dd-144">컨테이너 서비스 클러스터의 리소스 그룹을 찾은 후 에이전트 VM에 대한 부하 분산 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="ef1dd-145">해당 이름은 컨테이너 서비스와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="ef1dd-146">(해당 이름에 **master-lb**가 포함된 마스터 노드에 대한 부하 분산 장치는 선택하지 마세요.)</span><span class="sxs-lookup"><span data-stu-id="ef1dd-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![리소스 그룹의 부하 분산 장치](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="ef1dd-148">부하 분산 장치 구성의 세부 정보를 보려면 **부하 분산 장치 규칙** 및 구성된 규칙의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![부하 분산 장치 규칙](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="ef1dd-150">예제: 서비스 구성 파일에 `type: LoadBalancer` 지정</span><span class="sxs-lookup"><span data-stu-id="ef1dd-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="ef1dd-151">YAML 또는 JSON [서비스 구성 파일](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file)에서 Kubernetes 컨테이너 앱을 배포하는 경우 서비스 사양에 다음 줄을 추가하여 외부 부하 분산 장치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="ef1dd-152">다음 단계에서는 Kubernetes [방명록 예제](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="ef1dd-153">이 예제는 Redis 및 PHP Docker 이미지를 기준으로 하는 다중 계층 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="ef1dd-154">서비스 구성 파일에서 프런트 엔드 PHP 서버가 Azure Load Balancer를 사용하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="ef1dd-155">[GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one)에서 `guestbook-all-in-one.yaml` 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="ef1dd-156">`frontend` 서비스에 대한 `spec`을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="ef1dd-157">`type: LoadBalancer` 줄의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![서비스 구성의 부하 분산 장치](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="ef1dd-159">파일을 저장하고 다음 명령을 실행하여 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="ef1dd-160">`kubectl get svc`를 입력하여 클러스터의 서비스 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="ef1dd-161">부하 분산 장치가 규칙을 구성하는 동안 `frontend` 서비스의 `EXTERNAL-IP`가 `<pending>`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="ef1dd-162">몇 분 후에 외부 IP 주소가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-162">After a few minutes, the external IP address is configured:</span></span> 

    ![Azure Load Balancer 구성](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="ef1dd-164">서비스에 외부 IP 주소로 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="ef1dd-165">예를 들어 서비스의 외부 IP 주소로 웹 브라우저를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![외부에서 방명록 액세스](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="ef1dd-167">방명록 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="ef1dd-168">Azure Load Balancer의 구성을 보려면 [Azure Portal](https://portal.azure.com)에서 클러스터에 대한 부하 분산 장치 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ef1dd-169">이전 예제의 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="ef1dd-170">고려 사항</span><span class="sxs-lookup"><span data-stu-id="ef1dd-170">Considerations</span></span>

* <span data-ttu-id="ef1dd-171">부하 분산 장치 규칙은 비동기적으로 생성되고 프로비전된 분산 장치에 대한 정보는 서비스의 `status.loadBalancer` 필드에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="ef1dd-172">모든 서비스는 부하 분산 장치의 자체 가상 IP 주소에 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="ef1dd-173">DNS 이름으로 부하 분산 장치에 연결하려는 경우 도메인 서비스 공급자와 함께 규칙의 IP 주소에 대한 DNS 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="ef1dd-174">HTTP 또는 HTTPS 트래픽</span><span class="sxs-lookup"><span data-stu-id="ef1dd-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="ef1dd-175">컨테이너 웹앱으로 HTTP 또는 HTTPS 트래픽 부하를 분산하고 TLS(전송 계층 보안)에 대한 인증서를 관리하려면 Kubernetes [수신](https://kubernetes.io/docs/user-guide/ingress/) 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="ef1dd-176">수신은 인바운드 연결이 클러스터 서비스에 연결하도록 하는 규칙 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="ef1dd-177">수신 리소스가 작동하려면 Kubernetes 클러스터에서 [수신 컨트롤러](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers)가 실행되고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="ef1dd-178">Azure Container Service는 Kubernetes 수신 컨트롤러를 자동으로 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="ef1dd-179">여러 컨트롤러 구현을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-179">Several controller implementations are available.</span></span> <span data-ttu-id="ef1dd-180">현재 수신 규칙을 구성하고 HTTP 및 HTTPS 트래픽 부하를 분산하기 위해 [Nginx 수신 컨트롤러](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx)가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="ef1dd-181">자세한 내용은 [Nginx 수신 컨트롤러 설명서](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef1dd-182">Azure Container Service에서 Nginx 수신 컨트롤러를 사용하려면 `type: LoadBalancer`를 사용하여 컨트롤러 배포를 서비스로 노출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="ef1dd-183">이렇게 하면 Azure Load Balancer가 해당 컨트롤러로 트래픽을 라우팅하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="ef1dd-184">자세한 내용은 이전 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef1dd-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ef1dd-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef1dd-185">Next steps</span></span>

* <span data-ttu-id="ef1dd-186">[Kubernetes LoadBalancer 설명서](https://kubernetes.io/docs/user-guide/load-balancer/) 참조</span><span class="sxs-lookup"><span data-stu-id="ef1dd-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="ef1dd-187">[Kubernetes 송/수신 컨트롤러](https://kubernetes.io/docs/user-guide/ingress/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ef1dd-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="ef1dd-188">[Kubernetes 예제](https://github.com/kubernetes/kubernetes/tree/master/examples) 참조</span><span class="sxs-lookup"><span data-stu-id="ef1dd-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

