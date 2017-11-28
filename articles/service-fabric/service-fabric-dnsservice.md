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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="4b021-103">Azure Service Fabric의 DNS 서비스</span><span class="sxs-lookup"><span data-stu-id="4b021-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="4b021-104">hello DNS 서비스 클러스터 toodiscover에 사용할 수 있는 선택적인 시스템 서비스는 hello DNS 프로토콜을 사용 하 여 다른 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="4b021-105">많은 서비스, 특히 컨테이너 화 된 서비스 수 tooresolve 되 고 기존 URL 이름을 가질 수 있습니다 이러한 hello 표준 DNS 프로토콜 (hello 서비스 이름 지정 프로토콜 아님)를 사용 하는 것은 "리프트 및 이동" 시나리오에서는 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="4b021-106">DNS 서비스 hello toomap DNS 이름을 tooa 서비스 명명 있으며 따라서 끝점 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="4b021-107">hello DNS 서비스는 hello 명명 서비스 tooreturn hello 서비스 끝점에 의해 해결 되는 DNS 이름 tooservice 이름을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="4b021-108">hello 서비스에 대 한 DNS 이름은 hello hello 생성 시 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![서비스 끝점][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="4b021-110">Hello DNS 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4b021-110">Enabling hello DNS service</span></span>
<span data-ttu-id="4b021-111">먼저 클러스터의 tooenable hello DNS 서비스를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="4b021-112">원하는 toodeploy hello 클러스터에 대 한 hello 서식 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="4b021-113">중 하나 사용 하 여 hello 수 [템플릿 샘플](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) 하거나 리소스 관리자 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="4b021-114">단계를 수행 하는 hello로 hello DNS 서비스를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="4b021-115">해당 hello 확인 `apiversion` 너무 설정`2017-07-01-preview` hello에 대 한 `Microsoft.ServiceFabric/clusters` 리소스를 하 고 그렇지 않은 경우 업데이트 hello 다음 코드 조각에에서 나와 있는 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="4b021-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="4b021-116">Hello 다음을 추가 하 여 hello DNS 서비스를 사용 하는 이제 `addonFeatures` hello 후 섹션 `fabricSettings` hello 다음 코드 조각에에서 나와 있는 것 처럼 섹션:</span><span class="sxs-lookup"><span data-stu-id="4b021-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="4b021-117">앞에 변경 내용을 hello로 클러스터 서식 파일을 업데이트 하면 업데이트를 적용할를 hello 업그레이드 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="4b021-118">Hello DNS 시스템 서비스가 완료 되 면 호출 하 여 클러스터에서 실행 되기 시작 `fabric:/System/DnsService` hello 서비스 패브릭 탐색기에서 시스템 서비스 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="4b021-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="4b021-119">또는 클러스터 생성 hello 시 hello hello 포털을 통해 DNS 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="4b021-120">에 대 한 hello 상자를 선택 하 여 hello DNS 서비스를 사용할 수 있습니다 `Include DNS service` hello에 `Cluster configuration` hello 스크린 샷 뒤에 표시 된 대로 메뉴:</span><span class="sxs-lookup"><span data-stu-id="4b021-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Hello 포털을 통해 DNS 서비스를 사용 하도록 설정][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="4b021-122">서비스의 DNS 이름을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="4b021-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="4b021-123">클러스터의 hello DNS 서비스를 실행 하 고 설정할 수 있습니다 프로그램 서비스에 대 한 DNS 이름을 기본 서비스에 대 한 선언적으로 hello에 `ApplicationManifest.xml` 하거나 Powershell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="4b021-124">Hello ApplicationManifest.xml에서에서 기본 서비스에 대 한 DNS 이름을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="4b021-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="4b021-125">Visual Studio에서 프로젝트 또는 선호 하는 편집기를 열고 hello 엽니다 `ApplicationManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="4b021-126">Toohello 기본 서비스 섹션을 이동 하 고 각 서비스 추가 hello에 대 한 `ServiceDnsName` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="4b021-127">다음 예제는 hello 방법을 tooset hello hello 서비스의 DNS 이름을 너무 보여 줍니다.`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="4b021-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="4b021-128">Hello 응용 프로그램을 배포한 후 hello 서비스 패브릭 탐색기에서에서 서비스 인스턴스 hello hello 다음 그림에에서 나와 있는 것 처럼이 인스턴스에 대 한 hello DNS 이름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![서비스 끝점][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="4b021-130">Powershell을 사용 하 여 서비스에 대 한 DNS 이름을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="4b021-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="4b021-131">Hello를 사용 하 여 만들 때 서비스에 대 한 hello DNS 이름을 설정할 수 있습니다 `New-ServiceFabricService` Powershell 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="4b021-132">hello 다음 예제에서는 새 상태 비저장 서비스 hello DNS 이름`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="4b021-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="4b021-133">서비스에 DNS 사용</span><span class="sxs-lookup"><span data-stu-id="4b021-133">Using DNS in your services</span></span>
<span data-ttu-id="4b021-134">하나 이상의 서비스를 배포 하는 경우 DNS 이름을 사용 하 여 다른 서비스 toocommunicate와의 hello 끝점을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="4b021-135">hello DNS 서비스는 hello DNS 프로토콜은 상태 저장 서비스와 통신할 수 없는 적용 가능한 toostateless 서비스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="4b021-136">상태 저장 서비스에 대 한 http 호출 toocall 특정 서비스 파티션에 대 한 역방향 프록시를 기본 제공 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="4b021-137">hello 다음 코드 호출 방법을 보여 줍니다 toocall 다른 서비스에는 일반 http 단순히 hello URL의 일부분으로 hello 포트 및 모든 선택적 경로 제공 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4b021-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4b021-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b021-138">Next steps</span></span>
<span data-ttu-id="4b021-139">사용 하는 hello 클러스터 내에서 서비스 통신에 대 한 자세한 [연결 하 고 서비스와 통신](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="4b021-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
