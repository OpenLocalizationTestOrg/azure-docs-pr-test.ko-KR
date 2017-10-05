---
title: "Azure Container Service 및 Azure Container Registry에서 Draft 사용 | Microsoft Docs"
description: "ACS Kubernetes 클러스터와 Azure Container Registry를 만들어 Azure에서 Draft로 첫 번째 응용 프로그램을 만듭니다."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, Draft, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="8abca-104">Azure Container Service 및 Azure Container Registry에서 Draft를 사용하여 응용 프로그램 빌드 및 Kubernetes에 배포</span><span class="sxs-lookup"><span data-stu-id="8abca-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="8abca-105">[Draft](https://aka.ms/draft)는 Docker와 Kubernetes에 대해 잘 알지 못하거나 패키지를 설치하지 않고도 손쉽게 컨테이너 기반 응용 프로그램을 개발하여 Kubernetes 클러스터에 배포할 수 있는 새로운 오픈 소스 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="8abca-106">Draft와 같은 도구를 사용하면 사용자와 팀이 Kubernetes로 응용 프로그램을 빌드하는 데 집중할 수 있는 한편 인프라에는 많은 주의를 기울이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="8abca-107">로컬을 포함하여 모든 Docker 이미지 레지스트리와 Kubernetes 클러스터에서 Draft를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="8abca-108">이 자습서에서는 Kubernetes, ACR 및 Azure DNS와 함께 ACS를 사용하여 Draft를 통해 라이브 CI/CD 개발자 파이프라인을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="8abca-109">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="8abca-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="8abca-110">[새 Azure Container Registry를 쉽게 만들](../../container-registry/container-registry-get-started-azure-cli.md) 수 있으며, 그 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="8abca-111">ACS에서 ACR 레지스트리와 Kubernetes 클러스터를 관리하기 위한 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="8abca-112">[az acr create](/cli/azure/acr#create)를 사용하여 ACR 이미지 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="8abca-113">Kubernetes로 Azure Container Service 만들기</span><span class="sxs-lookup"><span data-stu-id="8abca-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="8abca-114">이제 [az acs create](/cli/azure/acs#create)를 통해 Kubernetes를 `--orchestrator-type` 값으로 사용하여 ACS 클러스터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="8abca-115">Kubernetes는 기본 조정자 유형이 아니므로 `--orchestrator-type kubernetes` 스위치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="8abca-116">성공했을 때의 출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="8abca-117">이제 클러스터가 있으므로 [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) 명령을 사용하여 자격 증명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="8abca-118">그리고 클러스터에 대한 로컬 구성 파일이 있습니다. 이는 Helm과 Draft가 작업을 완료하는 데 필요한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="8abca-119">Draft 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="8abca-119">Install and configure draft</span></span>
<span data-ttu-id="8abca-120">Draft에 대한 설치 지침은 [Draft 리포지토리](https://github.com/Azure/draft/blob/master/docs/install.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="8abca-121">이 지침은 상대적으로 간단하지만, Helm 차트를 만들고 Kubernetes 클러스터에 배포하는 [Helm](https://aka.ms/helm)을 사용하기 때문에 일부 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="8abca-122">[Helm을 다운로드하고 설치합니다](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="8abca-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="8abca-123">Helm을 사용하여 `stable/traefik`를 검색하여 설치하고, 수신 컨트롤러에서 빌드에 대한 인바운드 요청을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="8abca-124">이제 `ingress` 컨트롤러에 대한 조사식을 설정하여 해당 컨트롤러를 배포할 때 외부 IP 값을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="8abca-125">이 IP 주소는 다음 섹션에서 [배포 도메인에 매핑되는](#wire-up-deployment-domain) 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="8abca-126">이 경우 배포 도메인의 외부 IP는 `13.64.108.240`입니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="8abca-127">이제 도메인을 해당 IP에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="8abca-128">배포 도메인 연결</span><span class="sxs-lookup"><span data-stu-id="8abca-128">Wire up deployment domain</span></span>

<span data-ttu-id="8abca-129">Draft는 자체에서 만든 각 Helm 차트, 즉 작업 중인 각 응용 프로그램에 대한 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="8abca-130">각각은 Draft에서 사용자가 제어하는 루트 _배포 도메인_의 최상위에 있는 _하위 도메인_으로 사용하도록 생성된 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="8abca-131">(이 예제에서는 `squillace.io`를 배포 도메인으로 사용합니다.) 이 하위 도메인 동작을 사용하도록 설정하려면 `'*'`에 대한 A 레코드를 배포 도메인의 DNS 항목에 만들어 생성된 각 하위 도메인이 Kubernetes 클러스터의 수신 컨트롤러로 라우팅되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="8abca-132">사용자의 도메인 공급자에는 DNS 서버를 할당하는 자체의 고유한 방법이 있습니다. [도메인 이름 서버를 Azure DNS로 위임](../../dns/dns-delegate-domain-azure-dns.md)하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="8abca-133">사용자 영역에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="8abca-134">도메인에 대한 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="8abca-135">[az network dns zone create](/cli/azure/network/dns/zone#create) 명령을 사용하여 DNS 컨트롤을 도메인에 대한 Azure DNS에 위임할 이름 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="8abca-136">제공된 DNS 서버를 배포 도메인의 도메인 공급자에 추가합니다. 이렇게 하면 Azure DNS를 사용하여 원하는 대로 도메인을 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="8abca-137">이전 섹션의 2단계에 있는 `ingress` IP에 매핑되는 배포 도메인에 대한 A 레코드 집합 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="8abca-138">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-138">The output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="8abca-139">Draft를 구성하여 레지스트리를 사용하고 만든 각 Helm 차트에 대한 하위 도메인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="8abca-140">Draft을 구성하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="8abca-141">Azure Container Registry 이름(이 예제에서는 `draft`)</span><span class="sxs-lookup"><span data-stu-id="8abca-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="8abca-142">레지스트리 키 또는 암호(`az acr credential show -n <registry name> --output tsv --query "passwords[0].value"` 명령 사용)</span><span class="sxs-lookup"><span data-stu-id="8abca-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="8abca-143">Kubernetes 수신 외부 IP 주소(여기서는 `squillace.io`)에 매핑하도록 구성된 루트 배포 도메인</span><span class="sxs-lookup"><span data-stu-id="8abca-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="8abca-144">`draft init`를 호출하면 구성 프로세스에서 위의 값을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="8abca-145">프로세스를 처음 실행하면 다음과 같은 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-145">The process looks something like the following the first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="8abca-146">이제 응용 프로그램을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="8abca-147">응용 프로그램 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="8abca-147">Build and deploy an application</span></span>

<span data-ttu-id="8abca-148">Draft 리포지토리에는 [간단한 6개 예제 응용 프로그램](https://github.com/Azure/draft/tree/master/examples)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="8abca-149">해당 리포지토리를 복제하고 [Python 예제](https://github.com/Azure/draft/tree/master/examples/python)를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="8abca-150">examples/Python 디렉터리로 변경하고 `draft create`를 입력하여 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="8abca-151">다음 예제와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="8abca-152">출력에는 Dockerfile과 Helm 차트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="8abca-153">빌드하고 배포하려면 `draft up`만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="8abca-154">출력은 광범위하지만 다음 예제와 같이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-154">The output is extensive, but begins like the following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="8abca-155">성공적인 경우 다음 예제와 같이 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="8abca-156">이제 차트 이름에 관계없이 `curl http://gangly-bronco.squillace.io` 명령을 실행하면 `Hello World!` 회신을 받을 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="8abca-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8abca-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8abca-157">Next steps</span></span>

<span data-ttu-id="8abca-158">이제 ACS Kubernetes 클러스터가 있으므로 [Azure Container Registry](../../container-registry/container-registry-intro.md)에서 조사하여 이 시나리오의 다양한 배포를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="8abca-159">예를 들어 특정 ACS 배포에 대해 더 깊은 하위 도메인의 작업을 제어하는 draft._basedomain.toplevel_ 도메인 DNS 레코드 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abca-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






