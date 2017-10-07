---
title: "서비스 패브릭 aaaAzure 역방향 프록시 | Microsoft Docs"
description: "서비스 패브릭 역방향 프록시를 사용 하 여 내부 및 외부 hello 클러스터에서 toomicroservices 통신에 대 한 합니다."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Azure Service Fabric의 역방향 프록시
Azure Service Fabric에 기본 제공 되는 역방향 프록시를 hello microservices HTTP 끝점을 노출 하는 hello 서비스 패브릭 클러스터에서 해결 합니다.

## <a name="microservices-communication-model"></a>마이크로 서비스 통신 모델
일반적으로 서비스 패브릭에서 Microservices hello 클러스터의 가상 컴퓨터의 하위 집합에서 실행 하 고 다양 한 이유로 하나의 가상 컴퓨터 tooanother에서 이동할 수 있습니다. 따라서 microservices에 대 한 hello 끝점 동적으로 변경할 수 있습니다. hello 대부분의 일반적인 패턴 toocommunicate toohello 마이크로 서비스는 hello 다음 루프를 해결 합니다.

1. Hello 명명 서비스를 통해 처음 hello 서비스 위치를 확인 합니다.
2. Toohello 서비스를 연결 합니다.
3. Hello 연결 실패 원인을 확인 하 고 필요한 경우 hello 서비스 위치를 다시 확인 합니다.

이 프로세스는 일반적으로 hello 서비스 확인 및 다시 시도 정책을 구현 하는 다시 시도 루프에서 클라이언트 통신 라이브러리 래핑 포함 됩니다.
자세한 내용은 [서비스와 연결 및 통신](service-fabric-connect-and-communicate-with-services.md)을 참조하세요.

### <a name="communicating-by-using-hello-reverse-proxy"></a>Hello 역방향 프록시를 사용 하 여 통신 합니다.
서비스 패브릭에서 역방향 프록시 hello hello 클러스터의 모든 hello 노드에서 실행 됩니다. 클라이언트를 대신 하 여 hello 전체 서비스 확인 프로세스를 수행 하 고 hello 클라이언트 요청을 전달 합니다. 따라서 hello 클러스터에서 실행 하는 클라이언트에서 로컬로 실행 hello 동일한 노드는 hello 역방향 프록시를 사용 하 여 클라이언트 쪽 HTTP 통신 라이브러리 tootalk toohello 대상 서비스를 사용할 수 있습니다.

![내부 통신][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Hello 클러스터 외부에서 microservices 도달
microservices hello 기본 외부 통신 모델은 외부 클라이언트에서 직접 각 서비스에 액세스할 수 없는 옵트인 모델입니다. [Azure 부하 분산 장치](../load-balancer/load-balancer-overview.md)microservices와 외부 클라이언트 간의 네트워크 경계는 네트워크 주소 변환 하 고 수행한 전달 외부 toointernal ip: port 끝점 요청 합니다. toomake 마이크로 서비스의 끝점 tooexternal 직접 액세스할 수 있는 클라이언트를 먼저 구성 해야 tooforward 트래픽 tooeach 포트 서비스 hello를 사용 하 여 부하 분산 장치 hello 클러스터에 있습니다. 또한 대부분 microservices, 상태 저장 microservices 특히 hello 클러스터의 모든 노드에서 실시간 하지 않습니다. hello microservices 장애 조치 노드 간에 이동할 수 있습니다. 이러한 경우 부하 분산 장치 결정할 수 없습니다 효율적으로 hello 위치 hello 복제본 toowhich hello 대상 노드의 트래픽을 전달 합니다.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Hello 외부 hello 클러스터에서 역방향 프록시를 통해 microservices 도달
부하 분산 장치에서 개별 서비스의 hello 포트를 구성 하는 대신 부하 분산 장치에만 hello 포트 hello 역방향 프록시를 구성할 수 있습니다. 이 구성을 통해 hello 클러스터 외부의 클라이언트가 추가 구성 없이 hello 역방향 프록시를 사용 하 여 hello 클러스터 내 서비스를 연결할 수 있습니다.

![외부 통신][0]

> [!WARNING]
> 부하 분산 장치에서 hello 역방향 프록시 포트를 구성 하는 경우 HTTP 끝점을 노출 하는 hello 클러스터의 모든 microservices hello 클러스터 외부에서 주소 지정 가능한 됩니다.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Hello 역방향 프록시를 사용 하 여 서비스를 해결 하기 위한 URI 형식
hello 역방향 프록시 사용 하 여 특정 uniform 리소스 URI (identifier) 형식 tooidentify hello 서비스 파티션 toowhich hello 들어오는 요청을 전달 해야 합니다.

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http (s):** hello 역방향 프록시 구성된 tooaccept HTTP 또는 HTTPS 트래픽이 될 수 있습니다. HTTPS 전달 하기 위해 참조 너무[hello 역방향 프록시를 사용 하 여 보안 서비스 tooa 연결](service-fabric-reverseproxy-configure-secure-communication.md) HTTPS에 대해 역방향 프록시 설치 toolisten를 설정한 후 합니다.
* **클러스터 정규화 된 도메인 이름 (FQDN) | 내부 IP:** 외부 클라이언트에 대해 구성할 수 있습니다 hello 역방향 프록시 mycluster.eastus.cloudapp.azure.com 같은 hello 클러스터 도메인을 통해 연결할 수 있도록 합니다. 기본적으로 모든 노드에 대해 hello 역방향 프록시 실행 합니다. 내부 트래픽에 대 한 역방향 프록시 hello 10.0.0.1와 같은 모든 내부 노드 IP 또는 localhost에 도달할 수 있습니다.
* **포트:** hello 역방향 프록시에 대 한 지정 된 19081, 같은 hello 포트입니다.
* **ServiceInstanceName:** hello hello 없이 tooreach를 시도 하는 배포 된 hello 서비스 인스턴스의 정규화 된 이름 "fabric: /" 구성표입니다. 예를 들어 tooreach hello *패브릭: / myapp/myservice/* 서비스를 사용 하 여 *myapp/myservice*합니다.

    hello 서비스 인스턴스 이름은 대/소문자 구분입니다. 404 (찾을 수 없음) hello 요청 toofail 되 면 서로 다른 대/소문자를 사용 하 여 hello URL에서 hello 서비스 인스턴스 이름을.
* **경로 접미사:** 같은 hello 실제 URL 경로입니다 *myapi/값/추가/3*, tooconnect를 원하는 hello 서비스에 대 한 합니다.
* **PartitionKey:** 분할 된 서비스 tooreach hello 파티션의 hello 계산 된 파티션 키입니다. 이것은 *하지* hello 파티션 ID GUID입니다. 이 매개 변수 hello singleton 파티션 구성표를 사용 하는 서비스에 대 한 필요 하지 않습니다.
* **PartitionKind:** hello 서비스 파티션 구성표입니다. 이는 'Int64Range' 또는 'Named'일 수 있습니다. 이 매개 변수 hello singleton 파티션 구성표를 사용 하는 서비스에 대 한 필요 하지 않습니다.
* **ListenerName** hello 폼의 hello 서비스에서 hello 끝점은 {"끝점": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}. 이 식별 hello 끝점 hello 서비스에서 여러 끝점을 노출할 때 해당 hello 클라이언트 요청을 전달 해야 합니다. Hello 서비스에 수신기가 하나만 있으면 생략할 수 있습니다.
* **TargetReplicaSelector** 방법을 hello 대상 복제본 또는 인스턴스 선택 해야 합니다.이 지정 합니다.
  * Hello TargetReplicaSelector hello 다음 중 하나일 수 hello 대상 서비스 이면 상태 저장: 'PrimaryReplica', 'RandomSecondaryReplica' 또는 'RandomReplica'. 이 매개 변수를 지정 하지 않으면 'PrimaryReplica' hello 기본값은입니다.
  * Hello 대상 서비스는 상태 비저장 역방향 프록시에서는 hello 서비스 파티션 tooforward hello 요청을의 임의 인스턴스를 선택 합니다.
* **시간 초과:** hello 클라이언트 요청을 대신해 hello 역방향 프록시 toohello 서비스에 의해 만들어진 hello HTTP 요청에 대 한 hello 시간 제한을 지정 합니다. hello 기본값은 60 초입니다. 선택적 매개 변수입니다.

### <a name="example-usage"></a>사용 예
예를 들어 보겠습니다 hello *패브릭: / MyApp/MyService* hello url에 HTTP 수신기를 서비스:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

다음은 hello 서비스에 대 한 hello 리소스:

* `/index.html`
* `/api/users/<userId>`

Hello 서비스가 hello singleton 파티션 구성표를 사용 하는 경우 hello *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수가 필요 하지 않습니다. 및 hello 게이트웨이 사용 하 여 hello 서비스에 연결할 수 있습니다.

* 외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* 내부에서: `http://localhost:19081/MyApp/MyService`

Hello 서비스가 hello 균일 Int64 파티션 구성표를 사용 하는 경우 hello *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수가 사용 되는 tooreach hello 서비스의 파티션을 이어야 합니다.

* 외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* 내부에서: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

tooreach hello 리소스 hello 서비스를 노출 하는 단순히 hello URL에 hello 서비스 이름 뒤에 오는 hello 리소스 경로 배치 합니다.

* 외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* 내부에서: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

hello 게이트웨이 이러한 요청 toohello 서비스의이 URL을 전달 합니다.

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>포트 공유 서비스에 대한 특수 처리
Azure 응용 프로그램 게이트웨이 시도 tooresolve 서비스 다시 주소와 서비스에 연결할 수 없는 경우 hello 요청을 다시 시도 합니다. 응용 프로그램 게이트웨이의 큰 장점은 클라이언트 코드는 자체 서비스 해상도 tooimplement 필요 하며 루프를 해결 하지 때문입니다.

일반적으로 서비스에 연결할 수 없는 경우 hello 서비스 인스턴스나 복제본에 이동의 기본 수명 주기의 일부로 tooa 다른 노드. 이 경우 응용 프로그램 게이트웨이 네트워크 연결 오류 끝점 임을 나타내는 hello에 긴 열지 않고는 원래 주소 확인을 받을 수 없습니다.

그러나 복제 또는 서비스 인스턴스는 호스트 프로세스를 공유할 수 있으며 다음을 비롯하여 http.sys 기반 웹 서버에 의해 호스팅될 경우 포트를 공유할 수도 있습니다.

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET 코어 WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [카타나](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

이 경우 해당 hello 웹 서버 hello 호스트 프로세스 및 toorequests, 하지만 hello 해결 서비스 인스턴스 또는 복제본을 더 이상 사용할 수 hello 호스트에 응답에서 사용할 수 있는 가능성이 높습니다. 이 경우 hello 게이트웨이 hello 웹 서버에서 HTTP 404 응답을 받게 됩니다. 따라서 HTTP 404에는 다음과 같은 두 가지 의미가 있습니다.

- 사례 #1: hello 서비스 주소가 올바르지만 요청 사용자 hello hello 리소스가 존재 하지 않아야 합니다.
- 사례 2: hello 서비스 주소가 올바르지 않은 및 사용자 요청 hello hello 리소스는 서로 다른 노드에 있을 수 있습니다.

hello 첫 번째 경우에는 사용자 오류 하다 고 간주 되는 일반 HTTP 404입니다. 그러나 hello 두 번째 경우에 hello 사용자가 존재 하는 리소스를 요청 했습니다. 응용 프로그램 게이트웨이 없습니다 toolocate hello 서비스 자체 때문에 이동 했습니다. 응용 프로그램 게이트웨이 요구 tooresolve hello 주소 다시 및 hello 요청을 다시 시도 합니다.

응용 프로그램 게이트웨이 이러한 두 사례 사이의 방식으로 toodistinguish 따라서 해야합니다. 이러한 방식으로 구분 hello 서버에서 힌트 필수임 toomake 합니다.

* 기본적으로 응용 프로그램 게이트웨이 대/소문자 #2 맡고 tooresolve 및 문제 hello 요청을 다시 시도 됩니다.
* tooindicate 사례 #1 tooApplication 게이트웨이, hello 서비스 HTTP 응답 헤더 뒤에 오는 hello를 반환 합니다.

  `X-ServiceFabric : ResourceNotFound`

이 HTTP 응답 헤더는 hello에 요청 된 리소스가 존재 하지 않습니다, 일반적인 HTTP 404 상황을 나타내고 응용 프로그램 게이트웨이 tooresolve hello 서비스 주소를 다시 시도 하지 않습니다.

## <a name="setup-and-configuration"></a>설정 및 구성

### <a name="enable-reverse-proxy-via-azure-portal"></a>Azure Portal을 통해 역방향 프록시 사용

Azure 포털은 새 서비스 패브릭 클러스터를 만드는 동안 옵션 tooenable 역방향 프록시를 제공 합니다.
아래 **만들 서비스 패브릭 클러스터**, 2 단계: 클러스터 구성에서 노드 유형 구성 너무 hello 확인란을 선택 "역방향 프록시 사용"입니다.
보안 역방향 프록시를 구성 하는 데 SSL 인증서에에서 지정할 수 3 단계: 클러스터 보안 설정 구성, 확인란 선택 hello 너무 "역방향 프록시에 대 한 SSL 인증서가 포함" 보안과 hello 인증서 세부 정보를 입력 합니다.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿을 통해 역방향 프록시 사용

Hello를 사용할 수 있습니다 [Azure 리소스 관리자 템플릿](service-fabric-cluster-creation-via-arm.md) tooenable hello 역방향 프록시 서비스 패브릭에서 hello 클러스터에 대 한 합니다.

너무 참조[HTTPS 역방향 프록시 구성에서 보안 클러스터](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) Azure 리소스 관리자에 대 한 서식 파일 예제 tooconfigure 보안 역방향 프록시 인증서 및 처리 인증서 롤오버로 합니다.

첫째, 얻게 hello 템플릿 hello 클러스터에 대 한 toodeploy 되도록 합니다. Hello 예제 서식 파일을 사용 하거나 사용자 지정 리소스 관리자 템플릿을 만들 수 있습니다. 그런 다음 단계를 수행 하는 hello를 사용 하 여 hello 역방향 프록시를 설정할 수 있습니다.

1. Hello에 hello 역방향 프록시에 대 한 포트 정의 [매개 변수 섹션](../azure-resource-manager/resource-group-authoring-templates.md) hello 템플릿의 합니다.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. 각 hello에 hello nodetype 개체에 hello 포트를 지정 **클러스터** [리소스 유형 섹션](../azure-resource-manager/resource-group-authoring-templates.md)합니다.

    hello 포트 reverseProxyEndpointPort hello 매개 변수 이름으로 식별 됩니다.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. 1 단계에서 지정한 hello 포트에 대 한 hello Azure 부하 분산 장치 규칙을 설정 해 서 Azure 클러스터 hello 외부에서 tooaddress hello의 역방향 프록시입니다.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. hello 역방향 프록시에 대 한 hello 포트에서 SSL 인증서 tooconfigure 추가 hello 인증서 toohello ***reverseProxyCertificate*** hello에 대 한 속성 **클러스터** [리소스 유형 섹션](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Hello 클러스터 인증서와에서 다른 역방향 프록시 인증서를 지원 합니다.
 Hello 역방향 프록시 인증서 hello 클러스터를 보호 하는 hello 인증서와에서 다른 경우 다음 hello 이전에 지정한 인증서 hello 가상 컴퓨터에 설치 해야 하 고 서비스 패브릭 수 있도록 toohello 액세스 제어 목록 (ACL)에 추가 액세스. Hello에 이렇게 **virtualMachineScaleSets** [리소스 유형 섹션](../resource-group-authoring-templates.md)합니다. 설치의 경우 해당 인증서 toohello osProfile를 추가 합니다. hello 서식 파일의 확장명 섹션 hello hello ACL에에서 hello 인증서를 업데이트할 수 있습니다.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Hello 클러스터 인증서 tooenable hello 역방향 프록시를 기존 클러스터의 다른 인증서를 사용할 때 hello 역방향 프록시 인증서를 설치 하 고 hello 역방향 프록시를 사용 하기 전에 hello 클러스터에서 hello ACL을 업데이트 합니다. 전체 hello [Azure 리소스 관리자 템플릿](service-fabric-cluster-creation-via-arm.md) 배포 언급 된 hello 설정을 사용 하 여 이전에 배포 tooenable hello 역방향 프록시를 시작 하기 전에에 1-4 단계.

## <a name="next-steps"></a>다음 단계
* [GitHub의 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)에서 서비스 간 HTTP 통신의 예제를 참조하세요.
* [Hello 역방향 프록시를 사용 하 여 HTTP 서비스 toosecure 전달](service-fabric-reverseproxy-configure-secure-communication.md)
* [Reliable Services 원격을 사용하여 원격 프로시저 호출](service-fabric-reliable-services-communication-remoting.md)
* [Reliable Services에서 OWIN을 사용하는 Web API](service-fabric-reliable-services-communication-webapi.md)
* [Reliable Services를 사용한 WCF 통신](service-fabric-reliable-services-communication-wcf.md)
* 추가적인 역방향 프록시 구성 옵션은 [Service Fabric 클러스터 설정 사용자 지정](service-fabric-cluster-fabric-settings.md)의 응용 프로그램 게이트웨이/HTTP 섹션을 참조하세요.

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
