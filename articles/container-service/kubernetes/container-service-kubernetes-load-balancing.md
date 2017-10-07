---
title: "aaaLoad 균형 Azure에서 컨테이너 Kubernetes | Microsoft Docs"
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
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="b3309-104">Azure Container Service의 Kubernetes 클러스터에서 컨테이너 부하 분산</span><span class="sxs-lookup"><span data-stu-id="b3309-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="b3309-105">이 문서에서는 Azure Container Service의 Kubernetes 클러스터에서 부하를 분산하는 과정을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="b3309-106">부하 분산 hello 서비스에 대 한 외부에서 액세스할 수 있는 IP 주소를 제공 하 고 Vm 에이전트를 실행 하는 hello 포드 간에 네트워크 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="b3309-107">Kubernetes 서비스 toouse를 설정할 수 있습니다 [Azure 부하 분산 장치](../../load-balancer/load-balancer-overview.md) toomanage 외부 (TCP) 네트워크 트래픽이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="b3309-108">추가 구성을 통해 HTTP 또는 HTTPS 트래픽의 부하 분산 및 라우팅이나 좀 더 고급 시나리오도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3309-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b3309-109">Prerequisites</span></span>
* <span data-ttu-id="b3309-110">Azure Container Service에서 [Kubernetes 클러스터 배포](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="b3309-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="b3309-111">[클라이언트 연결](../container-service-connect.md) tooyour 클러스터</span><span class="sxs-lookup"><span data-stu-id="b3309-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="b3309-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="b3309-112">Azure load balancer</span></span>

<span data-ttu-id="b3309-113">기본적으로 컨테이너 서비스를 Azure에 배포 하는 Kubernetes 클러스터 hello 에이전트 Vm에 대 한 인터넷 연결 Azure 부하 분산 장치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="b3309-114">(별도 부하 분산 장치 리소스가 hello 마스터 Vm에 대해 구성 됩니다.) Azure Load Balancer는 계층 4 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="b3309-115">현재 hello 부하 분산 장치는만 Kubernetes에 TCP 트래픽의 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="b3309-116">Kubernetes 서비스를 만드는 경우 hello Azure 부하 분산 장치 tooallow 액세스 toohello 서비스를 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="b3309-117">tooconfigure hello 부하 분산 장치를 hello 서비스 설정 `type` 너무`LoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="b3309-118">hello 부하 분산 장치가 만듭니다 규칙 toomap 공용 IP 주소 및 포트 번호 들어오는 서비스 트래픽 toohello 개인 IP 주소와 hello 포드의 포트 번호의 Vm 에이전트 (및 그 반대로 응답 트래픽에 대 한).</span><span class="sxs-lookup"><span data-stu-id="b3309-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="b3309-119">다음은 tooset Kubernetes 서비스 hello 하는 방법을 보여 주는 두 가지 예제 `type` 너무`LoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="b3309-120">(이후 동안 hello 예제 배포를 삭제 hello 더 이상 필요 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b3309-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="b3309-121">예: 사용 하 여 hello `kubectl expose` 명령</span><span class="sxs-lookup"><span data-stu-id="b3309-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="b3309-122">hello [Kubernetes 연습](container-service-kubernetes-walkthrough.md) 방법의 예가 포함 되어 tooexpose hello로 서비스 `kubectl expose` 명령 및 해당 `--type=LoadBalancer` 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="b3309-123">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-123">Here are hello steps :</span></span>

1. <span data-ttu-id="b3309-124">새 컨테이너 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-124">Start a new container deployment.</span></span> <span data-ttu-id="b3309-125">예를 들어 다음 새 배포 라는 명령 시작을 hello `mynginx`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="b3309-126">hello 배포는 세 개의 컨테이너가 hello Nginx 웹 서버에 대 한 hello Docker 이미지에 따라 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="b3309-127">Hello 컨테이너 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-127">Verify that hello containers are running.</span></span> <span data-ttu-id="b3309-128">예를 들어, 사용 하 여 hello 컨테이너에 대 한 쿼리 하는 경우 `kubectl get pods`, 유사한 toohello 다음 출력을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3309-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Nginx 컨테이너 가져오기](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="b3309-130">tooconfigure hello 부하 분산 장치 tooaccept 외부 트래픽이 toohello 배포, 실행 `kubectl expose` 와 `--type=LoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="b3309-131">hello 다음 명령을 노출 포트 80에서 Nginx 서버 hello:</span><span class="sxs-lookup"><span data-stu-id="b3309-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="b3309-132">형식 `kubectl get svc` hello 클러스터에서 hello 서비스의 toosee hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="b3309-133">Hello 부하 분산 장치는 hello 규칙을 구성을 하는 동안 hello `EXTERNAL-IP` hello 서비스로 나타나는 `<pending>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="b3309-134">몇 분 후 hello 외부 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure Load Balancer 구성](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="b3309-136">Hello 외부 IP 주소에서 hello 서비스에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="b3309-137">예를 들어, 표시 된 웹 브라우저 toohello IP 주소를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="b3309-138">hello 브라우저 hello 컨테이너 중 하나에서 실행 하는 hello Nginx 웹 서버를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="b3309-139">또는 실행된 hello `curl` 또는 `wget` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="b3309-140">예:</span><span class="sxs-lookup"><span data-stu-id="b3309-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="b3309-141">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-141">You should see output similar to:</span></span>

    ![curl을 사용하여 Nginx에 액세스](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="b3309-143">hello Azure 부하 분산 장치, 이동 toohello toosee hello 구성 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="b3309-144">컨테이너 서비스 클러스터에 대 한 hello 리소스 그룹을 찾아서 hello 에이전트 Vm에 대 한 hello 부하 분산 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="b3309-145">해당 이름을 hello 컨테이너 서비스와 동일 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="b3309-146">(마스터 노드 hello에 대 한 hello 부하 분산 장치를 선택 하지 마십시오, 이름이 포함 하나 hello **마스터 lb**.)</span><span class="sxs-lookup"><span data-stu-id="b3309-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![리소스 그룹의 부하 분산 장치](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="b3309-148">hello 부하 분산 장치 구성의 toosee hello 세부 정보 클릭 **부하 분산 규칙** 및 구성 된 hello 규칙의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![부하 분산 장치 규칙](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="b3309-150">예: 지정 `type: LoadBalancer` hello 서비스 구성 파일에서</span><span class="sxs-lookup"><span data-stu-id="b3309-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="b3309-151">YAML 또는 JSON에서 Kubernetes 컨테이너 앱을 배포 하는 경우 [서비스 구성 파일](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), 줄 toohello 서비스 사양을 따르는 hello를 추가 하 여에서 외부 부하 분산 장치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="b3309-152">hello 다음 단계 사용 하 여 hello Kubernetes [방명록 예제](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="b3309-153">이 예제는 Redis 및 PHP Docker 이미지를 기준으로 하는 다중 계층 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="b3309-154">해당 hello 프런트 엔드 PHP 서버 hello Azure 부하 분산 장치를 사용 하 여 hello 서비스 구성 파일에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="b3309-155">Hello 파일을 다운로드 `guestbook-all-in-one.yaml` 에서 [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="b3309-156">Hello에 대 한 찾아보기 `spec` hello에 대 한 `frontend` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="b3309-157">Hello 줄의 주석 처리 제거 `type: LoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![서비스 구성의 부하 분산 장치](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="b3309-159">Hello 파일을 저장 하 고 hello 다음 명령을 실행 하 여 hello 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="b3309-160">형식 `kubectl get svc` hello 클러스터에서 hello 서비스의 toosee hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="b3309-161">부하 분산 장치 hello hello 규칙을 구성 하는 동안 hello `EXTERNAL-IP` 의 hello `frontend` 로 표시 된 서비스 `<pending>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="b3309-162">몇 분 후 hello 외부 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure Load Balancer 구성](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="b3309-164">Hello 외부 IP 주소에서 hello 서비스에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="b3309-165">예를 들어 hello 서비스의 웹 브라우저 toohello 외부 IP 주소를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![외부에서 방명록 액세스](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="b3309-167">방명록 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="b3309-168">hello에 hello 클러스터에 대 한 hello 부하 분산 장치 리소스에 대 한 찾아보기 hello Azure 부하 분산 장치 toosee hello 구성 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b3309-169">Hello hello 이전 예제에서 단계를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3309-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="b3309-170">고려 사항</span><span class="sxs-lookup"><span data-stu-id="b3309-170">Considerations</span></span>

* <span data-ttu-id="b3309-171">Hello 부하 분산 장치 규칙 만들기는 비동기적으로 발생 하며 hello 서비스에서 사용자를 프로 비전 하는 hello 분산 장치에 대 한 정보를 게시 `status.loadBalancer` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="b3309-172">모든 서비스는 hello 부하 분산 장치에 고유 가상 IP 주소를 자동으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="b3309-173">경우 tooreach hello에 대 한 부하 분산 장치 DNS 이름으로 원하는 작업을 사용자 도메인 서비스 공급자 toocreate hello 규칙의 IP 주소에 대 한 DNS 이름.</span><span class="sxs-lookup"><span data-stu-id="b3309-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="b3309-174">HTTP 또는 HTTPS 트래픽</span><span class="sxs-lookup"><span data-stu-id="b3309-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="b3309-175">hello Kubernetes를 사용할 수 있습니다, 웹 앱 및 전송 계층 보안 (TLS)에 대 한 인증서 관리 tooload 잔액 HTTP 또는 HTTPS 트래픽 toocontainer [수신](https://kubernetes.io/docs/user-guide/ingress/) 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="b3309-176">수신은 tooreach hello 클러스터 서비스 인바운드 연결을 허용 하는 규칙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="b3309-177">Hello Kubernetes 클러스터는 Ingress 리소스 toowork에 대 한 있어야는 [수신 컨트롤러](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="b3309-178">Azure Container Service는 Kubernetes 수신 컨트롤러를 자동으로 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="b3309-179">여러 컨트롤러 구현을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-179">Several controller implementations are available.</span></span> <span data-ttu-id="b3309-180">현재 hello [Nginx 수신 컨트롤러](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) tooconfigure 수신 규칙 및 부하 분산 HTTP 및 HTTPS 트래픽 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="b3309-181">자세한 내용은 참조 hello [Nginx 수신 컨트롤러 설명서](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3309-182">사용 하 여 서비스로 hello 컨트롤러 배포를 노출 해야 Azure 컨테이너 서비스의 hello Nginx 수신 컨트롤러를 사용할 경우 `type: LoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="b3309-183">Hello Azure 부하 분산 장치 tooroute 트래픽 toohello 컨트롤러를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3309-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="b3309-184">자세한 내용은 hello 이전 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b3309-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b3309-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3309-185">Next steps</span></span>

* <span data-ttu-id="b3309-186">Hello 참조 [Kubernetes LoadBalancer 설명서](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="b3309-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="b3309-187">[Kubernetes 송/수신 컨트롤러](https://kubernetes.io/docs/user-guide/ingress/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b3309-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="b3309-188">[Kubernetes 예제](https://github.com/kubernetes/kubernetes/tree/master/examples) 참조</span><span class="sxs-lookup"><span data-stu-id="b3309-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

