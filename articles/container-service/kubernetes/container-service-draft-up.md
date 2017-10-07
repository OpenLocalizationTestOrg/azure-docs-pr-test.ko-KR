---
title: "Azure 컨테이너 서비스와 Azure 컨테이너 레지스트리 초안 aaaUse | Microsoft Docs"
description: "ACS Kubernetes 클러스터와 Azure 컨테이너 레지스트리 toocreate 첫 응용 프로그램 만들기 초안을 사용 하 여 Azure에서."
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
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Azure 컨테이너 서비스 및 Azure 컨테이너 레지스트리 toobuild 함께 초안을 사용 하 고 응용 프로그램 tooKubernetes 배포

[초안](https://aka.ms/draft) 는 쉽게 toodevelop 컨테이너 기반 응용 프로그램에서는 새로운 오픈 소스 도구 및 Docker 및 Kubernetes-에 대해 잘 알고 있으면 또는 설치 하지도 않은 tooKubernetes 클러스터를 배포 합니다. 초안와 같은 도구를 사용 하 여 사용 하 고 팀 포커스 Kubernetes와 hello 응용 프로그램을 빌드, 많은 주의 기울여야 tooinfrastructure을 지불 하지 있습니다.

로컬을 포함하여 모든 Docker 이미지 레지스트리와 Kubernetes 클러스터에서 Draft를 사용할 수 있습니다. 이 자습서에서는 어떻게 Kubernetes, ACR를 및 Azure DNS toocreate와 ACS toouse 라이브 CI/CD 개발자 파이프라인 초안을 사용 하 여 보여 줍니다.


## <a name="create-an-azure-container-registry"></a>Azure Container Registry 만들기
에 쉽게 [새 Azure 컨테이너 레지스트리를 만듭니다](../../container-registry/container-registry-get-started-azure-cli.md), 있지만 hello 단계는 다음과 같습니다.

1. ACS에서 Azure 리소스 그룹 toomanage ACR 레지스트리 및 hello Kubernetes 클러스터를 만듭니다.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. [az acr create](/cli/azure/acr#create)를 사용하여 ACR 이미지 레지스트리를 만듭니다.
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Kubernetes로 Azure Container Service 만들기

준비 toouse 이제 [az acs 만들](/cli/azure/acs#create) Kubernetes hello로 사용 하 여 toocreate ACS 클러스터 `--orchestrator-type` 값입니다.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Kubernetes hello 기본 orchestrator 형식이 아니므로 반드시 hello를 사용 하 여 `--orchestrator-type kubernetes` 전환 합니다.

성공 하면 hello 출력 비슷한 toohello 다음을 찾습니다.

```json
waiting for AAD role toopropagate.done
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

Hello를 사용 하 여 hello 자격 증명을 가져올 수는 클러스터를가지고 [az acs kubernetes get-자격 증명](/cli/azure/acs/kubernetes#get-credentials) 명령입니다. 에 어떤 투구 및 초안 tooget 자신의 업무를 할 클러스터에 대 한 로컬 구성 파일을 지금 해야 합니다.

## <a name="install-and-configure-draft"></a>Draft 설치 및 구성
초안에 대 한 설치 지침 hello hello 중인 [초안 리포지토리](https://github.com/Azure/draft/blob/master/docs/install.md)합니다. 상대적으로 간단한 있은 필요 일부 구성에 따라 달라 집니다 [투구](https://aka.ms/helm) toocreate 투구 차트 hello Kubernetes 클러스터에 배포 합니다.

1. [Helm을 다운로드하고 설치합니다](https://aka.ms/helm#install).
2. 에 대 한 투구 toosearch를 사용 하 고 설치 `stable/traefik`, 및 수신 컨트롤러 tooenable 인바운드 빌드에 대 한 요청입니다.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    조사식 hello을 지금 설정 `ingress` 컨트롤러 toocapture hello 외부 IP 값을 배포할 때. 이 IP 주소 하나 hello 됩니다 [tooyour 배포 도메인 매핑하고](#wire-up-deployment-domain) hello 다음 섹션에 있습니다.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    이 경우 hello 배포 도메인에 대 한 외부 IP를 hello `13.64.108.240`합니다. 이제 도메인 toothat IP를 매핑할 수 있습니다.

## <a name="wire-up-deployment-domain"></a>배포 도메인 연결

Draft는 자체에서 만든 각 Helm 차트, 즉 작업 중인 각 응용 프로그램에 대한 릴리스를 만듭니다. 초안으로에서 사용 되는 생성 된 이름을 가져옵니다 각 하나는 _하위 도메인_ hello 루트 위에 _배포 도메인_ 사용자가 제어 하 합니다. (이 예에서는 사용 `squillace.io` hello 배포 도메인으로) tooenable이 하위 도메인 동작을 만들어야 합니다 A 레코드를 `'*'` 배포 도메인에 대 한 사용자 DNS 항목에 각 생성 되도록 하위 도메인은 라우트된 toohello Kubernetes 클러스터의 수신 컨트롤러입니다.

공급자를 도메인에 고유한 방식으로 tooassign DNS 서버가; 너무[도메인 이름 서버 tooAzure DNS 위임](../../dns/dns-delegate-domain-azure-dns.md), hello 다음 단계를 수행 합니다.

1. 사용자 영역에 대한 리소스 그룹을 만듭니다.
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

2. 도메인에 대한 DNS 영역을 만듭니다.
사용 하 여 hello [az 네트워크 dns 영역 만들기](/cli/azure/network/dns/zone#create) tooobtain hello 이름 서버 toodelegate DNS 도메인에 대 한 DNS tooAzure 제어 명령입니다.
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
3. 원하는 만큼 toouse Azure DNS toorepoint 도메인 수 있는 배포 도메인에 toohello 도메인 공급자를 표시 하는 hello DNS 서버를 추가 합니다.
4. 프로그램 배포 도메인 매핑 toohello는 A 레코드 집합 항목을 만들고 `ingress` hello 이전 섹션의 2 단계에서 IP입니다.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
hello 출력은 다음과 같이 합니다.
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

5. 초안 toouse 레지스트리를 구성 하 고 각 투구 차트 생성에 대 한 하위 도메인을 만듭니다. 초안 tooconfigure 해야합니다.
  - Azure Container Registry 이름(이 예제에서는 `draft`)
  - 레지스트리 키 또는 암호(`az acr credential show -n <registry name> --output tsv --query "passwords[0].value"` 명령 사용)
  - hello 루트 배포 도메인 toomap toohello Kubernetes 수신 외부 IP 주소를 구성 했는지 (여기서 `squillace.io`)

  호출 `draft init` 및 hello 구성 프로세스 위의 hello 값을 묻는 메시지를 표시 합니다. hello 프로세스 처럼 문제가 hello 다음 hello 처음으로 실행 하면 됩니다.
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

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

이제 준비 toodeploy 응용 프로그램입니다.


## <a name="build-and-deploy-an-application"></a>응용 프로그램 빌드 및 배포

Hello 초안 리포지토리는 [6 개의 간단한 예제 응용 프로그램](https://github.com/Azure/draft/tree/master/examples)합니다. Hello 리포지토리를 복제 하 고 hello를 사용 하 여 보겠습니다 [Python 예제](https://github.com/Azure/draft/tree/master/examples/python)합니다. Hello 예제/Python 디렉터리 및 형식으로 변경 `draft create` toobuild hello 응용 프로그램입니다. 이 파일은 다음 예제는 hello 같아야 합니다.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

Dockerfile 및 투구 차트 hello 출력에 포함 됩니다. toobuild를 배포 하 고를 입력 하기만 하면 `draft up`합니다. hello 출력 광범위 하지만 다음 예제는 hello와 같은 시작 합니다.
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

시기와 다음 예제는 다음과 유사한 toohello로 성공적으로 끝납니다.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

이제 수 차트의 이름이 무엇이, `curl http://gangly-bronco.squillace.io` tooreceive hello 회신 `Hello World!`합니다.

## <a name="next-steps"></a>다음 단계

사용 하 여 조사할 수 ACS Kubernetes 클러스터를가지고 [Azure 컨테이너 레지스트리](../../container-registry/container-registry-intro.md) toocreate이이 시나리오의 자세한 및 다른 배포 합니다. 예를 들어 특정 ACS 배포에 대해 더 깊은 하위 도메인의 작업을 제어하는 draft._basedomain.toplevel_ 도메인 DNS 레코드 집합을 만들 수 있습니다.






