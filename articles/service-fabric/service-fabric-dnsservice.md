---
title: "서비스 패브릭 DNS 서비스 aaaAzure | Microsoft Docs"
description: "microservices 검색 하기 위한 서비스 패브릭 dns 서비스를 사용 하 여 hello 클러스터 안에서 합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Azure Service Fabric의 DNS 서비스
hello DNS 서비스 클러스터 toodiscover에 사용할 수 있는 선택적인 시스템 서비스는 hello DNS 프로토콜을 사용 하 여 다른 서비스입니다.

많은 서비스, 특히 컨테이너 화 된 서비스 수 tooresolve 되 고 기존 URL 이름을 가질 수 있습니다 이러한 hello 표준 DNS 프로토콜 (hello 서비스 이름 지정 프로토콜 아님)를 사용 하는 것은 "리프트 및 이동" 시나리오에서는 특히 유용 합니다. DNS 서비스 hello toomap DNS 이름을 tooa 서비스 명명 있으며 따라서 끝점 IP 주소를 확인 합니다. 

hello DNS 서비스는 hello 명명 서비스 tooreturn hello 서비스 끝점에 의해 해결 되는 DNS 이름 tooservice 이름을 매핑합니다. hello 서비스에 대 한 DNS 이름은 hello hello 생성 시 제공 됩니다. 

![서비스 끝점][0]

## <a name="enabling-hello-dns-service"></a>Hello DNS 서비스를 사용 하도록 설정
먼저 클러스터의 tooenable hello DNS 서비스를 해야합니다. 원하는 toodeploy hello 클러스터에 대 한 hello 서식 파일을 가져옵니다. 중 하나 사용 하 여 hello 수 [템플릿 샘플](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) 하거나 리소스 관리자 템플릿을 만듭니다. 단계를 수행 하는 hello로 hello DNS 서비스를 활성화할 수 있습니다.

1. 해당 hello 확인 `apiversion` 너무 설정`2017-07-01-preview` hello에 대 한 `Microsoft.ServiceFabric/clusters` 리소스를 하 고 그렇지 않은 경우 업데이트 hello 다음 코드 조각에에서 나와 있는 것 처럼:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Hello 다음을 추가 하 여 hello DNS 서비스를 사용 하는 이제 `addonFeatures` hello 후 섹션 `fabricSettings` hello 다음 코드 조각에에서 나와 있는 것 처럼 섹션: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. 앞에 변경 내용을 hello로 클러스터 서식 파일을 업데이트 하면 업데이트를 적용할를 hello 업그레이드 완료 됩니다. Hello DNS 시스템 서비스가 완료 되 면 호출 하 여 클러스터에서 실행 되기 시작 `fabric:/System/DnsService` hello 서비스 패브릭 탐색기에서 시스템 서비스 섹션에서. 

또는 클러스터 생성 hello 시 hello hello 포털을 통해 DNS 서비스를 사용할 수 있습니다. 에 대 한 hello 상자를 선택 하 여 hello DNS 서비스를 사용할 수 있습니다 `Include DNS service` hello에 `Cluster configuration` hello 스크린 샷 뒤에 표시 된 대로 메뉴:

![Hello 포털을 통해 DNS 서비스를 사용 하도록 설정][2]


## <a name="setting-hello-dns-name-for-your-service"></a>서비스의 DNS 이름을 hello 설정
클러스터의 hello DNS 서비스를 실행 하 고 설정할 수 있습니다 프로그램 서비스에 대 한 DNS 이름을 기본 서비스에 대 한 선언적으로 hello에 `ApplicationManifest.xml` 하거나 Powershell 명령입니다.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Hello ApplicationManifest.xml에서에서 기본 서비스에 대 한 DNS 이름을 hello 설정
Visual Studio에서 프로젝트 또는 선호 하는 편집기를 열고 hello 엽니다 `ApplicationManifest.xml` 파일입니다. Toohello 기본 서비스 섹션을 이동 하 고 각 서비스 추가 hello에 대 한 `ServiceDnsName` 특성입니다. 다음 예제는 hello 방법을 tooset hello hello 서비스의 DNS 이름을 너무 보여 줍니다.`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Hello 응용 프로그램을 배포한 후 hello 서비스 패브릭 탐색기에서에서 서비스 인스턴스 hello hello 다음 그림에에서 나와 있는 것 처럼이 인스턴스에 대 한 hello DNS 이름을 보여 줍니다. 

![서비스 끝점][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Powershell을 사용 하 여 서비스에 대 한 DNS 이름을 hello 설정
Hello를 사용 하 여 만들 때 서비스에 대 한 hello DNS 이름을 설정할 수 있습니다 `New-ServiceFabricService` Powershell 합니다. hello 다음 예제에서는 새 상태 비저장 서비스 hello DNS 이름`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>서비스에 DNS 사용
하나 이상의 서비스를 배포 하는 경우 DNS 이름을 사용 하 여 다른 서비스 toocommunicate와의 hello 끝점을 찾을 수 있습니다. hello DNS 서비스는 hello DNS 프로토콜은 상태 저장 서비스와 통신할 수 없는 적용 가능한 toostateless 서비스 있습니다. 상태 저장 서비스에 대 한 http 호출 toocall 특정 서비스 파티션에 대 한 역방향 프록시를 기본 제공 하는 hello를 사용할 수 있습니다.

hello 다음 코드 호출 방법을 보여 줍니다 toocall 다른 서비스에는 일반 http 단순히 hello URL의 일부분으로 hello 포트 및 모든 선택적 경로 제공 되는 위치입니다.

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>다음 단계
사용 하는 hello 클러스터 내에서 서비스 통신에 대 한 자세한 [연결 하 고 서비스와 통신](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
