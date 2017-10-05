---
title: "Azure Service Fabric DNS 서비스 | Microsoft Docs"
description: "Service Fabric의 DNS 서비스를 사용하여 클러스터 내부에서 마이크로 서비스를 검색할 수 있습니다."
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="4db55-103">Azure Service Fabric의 DNS 서비스</span><span class="sxs-lookup"><span data-stu-id="4db55-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="4db55-104">DNS 서비스는 DNS 프로토콜을 통해 다른 서비스를 검색하기 위해 클러스터에서 사용할 수 있는 선택적 시스템 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="4db55-105">많은 서비스, 특히 컨테이너화된 서비스는 기존 URL 이름을 사용할 수 있으며, 특히 "리프트 앤 시프트" 시나리오에서는 명명 서비스 프로토콜 대신 표준 DNS 프로토콜을 사용하여 이러한 이름을 확인할 수 있으면 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="4db55-106">DNS 서비스를 통해 DNS 이름을 서비스 이름에 매핑할 수 있으므로 끝점 IP 주소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="4db55-107">DNS 서비스는 DNS 이름을 서비스 이름에 매핑하며, 서비스 이름은 명명 서비스를 통해 확인되어 서비스 끝점이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="4db55-108">서비스의 DNS 이름은 생성 시 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-108">The DNS name for the service is provided at the time of creation.</span></span> 

![서비스 끝점][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="4db55-110">DNS 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="4db55-110">Enabling the DNS service</span></span>
<span data-ttu-id="4db55-111">먼저 클러스터에서 DNS 서비스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="4db55-112">배포하려는 클러스터에 대한 템플릿을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="4db55-113">[샘플 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)을 사용하거나 Resource Manager 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="4db55-114">다음 단계에 따라 DNS 서비스를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="4db55-115">먼저 다음 코드 조각과 같이 `Microsoft.ServiceFabric/clusters` 리소스에 대해 `apiversion`이 `2017-07-01-preview`로 설정되었는지 확인하고 이렇게 설정되어 있지 않으면 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="4db55-116">이제 아래 코드 조각과 같이 다음 `addonFeatures` 섹션을 `fabricSettings` 섹션 뒤에 추가하여 DNS 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="4db55-117">위와 같은 변경 내용으로 클러스터 템플릿을 업데이트한 후 변경 내용을 적용하고 업그레이드가 완료되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="4db55-118">업그레이드가 완료되면 `fabric:/System/DnsService`라는 DNS 시스템 서비스가 클러스터에서 실행되기 시작하여 Service Fabric Explorer의 시스템 서비스 섹션 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="4db55-119">클러스터를 만들 때 포털을 통해 DNS 서비스를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="4db55-120">다음 스크린샷에 나와 있는 것처럼 `Cluster configuration` 메뉴에서 `Include DNS service`의 확인란을 선택하면 DNS 서비스를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![포털을 통해 DNS 서비스를 사용하도록 설정][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="4db55-122">서비스에 대한 DNS 이름 설정</span><span class="sxs-lookup"><span data-stu-id="4db55-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="4db55-123">DNS 서비스가 클러스터에서 실행되는 경우 `ApplicationManifest.xml`에서 기본 서비스에 대해 선언적으로 또는 Powershell 명령을 통해 서비스에 대한 DNS 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="4db55-124">ApplicationManifest.xml에서 기본 서비스에 대한 DNS 이름 설정</span><span class="sxs-lookup"><span data-stu-id="4db55-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="4db55-125">Visual Studio 또는 원하는 편집기에서 프로젝트를 연 다음 `ApplicationManifest.xml` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="4db55-126">기본 서비스 섹션으로 이동한 다음 각 서비스에 대해 `ServiceDnsName` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="4db55-127">다음 예제에서는 서비스의 DNS 이름을 `service1.application1`로 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="4db55-128">응용 프로그램을 배포한 후 Service Fabric Explorer의 서비스 인스턴스에는 다음 그림에 나와 있는 것처럼 이 인스턴스에 대한 DNS 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![서비스 끝점][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="4db55-130">Powershell을 사용하여 서비스에 대한 DNS 이름 설정</span><span class="sxs-lookup"><span data-stu-id="4db55-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="4db55-131">`New-ServiceFabricService` Powershel을 사용하여 만들 때 서비스에 대한 DNS 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="4db55-132">다음 예제에서는 DNS 이름 `service1.application1`을 사용하여 새로운 상태 비저장 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="4db55-133">서비스에 DNS 사용</span><span class="sxs-lookup"><span data-stu-id="4db55-133">Using DNS in your services</span></span>
<span data-ttu-id="4db55-134">둘 이상의 서비스를 배포하는 경우 DNS 이름을 사용하여 통신할 다른 서비스의 끝점을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="4db55-135">DNS 서비스는 상태 비저장 서비스에만 적용됩니다. DNS 프로토콜은 상태 저장 서비스와 통신할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="4db55-136">상태 저장 서비스의 경우 http 호출에 기본 제공 역방향 프록시를 사용하여 특정 서비스 파티션을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="4db55-137">다음 코드는 URL의 일부분으로 포트와 선택적 경로를 제공하는 일반 http 호출인 다른 서비스를 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4db55-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4db55-138">Next steps</span></span>
<span data-ttu-id="4db55-139">[서비스와 연결 및 통신](service-fabric-connect-and-communicate-with-services.md)에서 클러스터 내의 서비스 통신에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4db55-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
