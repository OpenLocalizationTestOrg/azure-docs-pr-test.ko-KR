---
title: "Azure Service Fabric 컨테이너 서비스에 대한 네트워킹 모드 구성 | Microsoft Docs"
description: "Azure Service Fabric에서 지원하는 다른 네트워킹 모드를 설정하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f792f9604a5d6e62551ed92c1049d6e2b4216417
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="76e70-103">Service Fabric 컨테이너 네트워킹 모드</span><span class="sxs-lookup"><span data-stu-id="76e70-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="76e70-104">컨테이너 서비스에 대해 Service Fabric 클러스터에서 제공되는 기본 네트워킹 모드는 `nat` 네트워킹 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-104">The default networking mode offered in the Service Fabric cluster for container services is the `nat` networking mode.</span></span> <span data-ttu-id="76e70-105">`nat` 네트워킹 모드에서 동일한 포트에 수신 대기하는 둘 이상의 컨테이너 서비스가 있는 경우 배포 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-105">With the `nat` networking mode, having more than one containers service listening to the same port results in deployment errors.</span></span> <span data-ttu-id="76e70-106">동일한 포트에서 여러 서비스가 수신 대기하도록 하기 위해 Service Fabric은 `open` 네트워킹 모드(버전 5.7 이상)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-106">For running several services that listen on the same port, Service Fabric supports the `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="76e70-107">`open` 네트워킹 모드에서 각 컨테이너 서비스는 내부적으로 여러 서비스를 동일한 포트에서 수신 대기할 수 있는 동적으로 할당된 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-107">With the `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services to listen to the same port.</span></span>   

<span data-ttu-id="76e70-108">따라서 서비스 매니페스트에 정의된 고정 끝점을 갖는 단일 서비스 형식으로 `open` 네트워킹 모드를 사용하여 배포 오류 없이 새로운 서비스를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-108">Thus, with a single service type with a static endpoint defined in the service manifest, new services may be created and deleted without deployment errors using the `open` networking mode.</span></span> <span data-ttu-id="76e70-109">마찬가지로 여러 서비스를 만들기 위해 고정 포트 매핑을 포함한 동일한 `docker-compose.yml` 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-109">Similarly, one can use the same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="76e70-110">서비스를 다시 시작하거나 다른 노드로 이동하는 경우 IP 주소를 변경하기 때문에 서비스를 검색하는 데 동적으로 할당된 IP를 사용하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-110">Using the dynamically assigned IP to discover services is not advisable since the IP address changes when the service restarts or moves to another node.</span></span> <span data-ttu-id="76e70-111">서비스 검색을 위해 **Service Fabric 명명 서비스** 또는 **DNS 서비스**만을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-111">Only use the **Service Fabric Naming Service**  or the **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="76e70-112">총 4096개의 IP가 Azure의 vNET에서 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="76e70-113">따라서 노드 수 및 컨테이너 서비스 인스턴스 수의 합계(`open` 네트워킹을 포함)는 vNET 내에서 4096개를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-113">Thus, the sum of the number of nodes and the number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="76e70-114">이러한 고밀도 시나리오에는 `nat` 네트워킹 모드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-114">For such high-density scenarios, the `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="76e70-115">오픈 네트워킹 모드 설정</span><span class="sxs-lookup"><span data-stu-id="76e70-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="76e70-116">`fabricSettings`에서 DNS 서비스와 IP 공급자를 사용하여 Azure Resource Manager 템플릿을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-116">Set up the Azure Resource Manager template by enabling DNS Service and the IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="76e70-117">클러스터의 각 노드에서 구성되어야 하는 여러 IP 주소를 허용하도록 네트워크 프로필 섹션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-117">Set up the network profile section to allow multiple IP addresses to be configured on each node of the cluster.</span></span> <span data-ttu-id="76e70-118">다음 예제에서는 Windows Service Fabric 클러스터에 노드당 5개의 IP 주소를 설정합니다(따라서 각 노드에서 포트에 수신 대기하는 5개의 서비스 인스턴스가 있을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="76e70-118">The following example sets up five IP addresses per node (thus you can have five service instances listening to the port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="76e70-119">Linux 클러스터의 경우 아웃바운드 연결을 허용하는 추가 공용 IP 구성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-119">For Linux clusters, an additional public IP configuration is added to allow outbound connectivity.</span></span> <span data-ttu-id="76e70-120">다음 코드 조각은 Linux 클러스터에 노드당 5개의 IP 주소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-120">The following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="76e70-121">Windows 클러스터의 경우에만 다음 값을 갖는 vNET에 UDP/53 포트를 여는 NSG 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for the vNET with the following values:</span></span>

   | <span data-ttu-id="76e70-122">우선 순위</span><span class="sxs-lookup"><span data-stu-id="76e70-122">Priority</span></span> |    <span data-ttu-id="76e70-123">이름</span><span class="sxs-lookup"><span data-stu-id="76e70-123">Name</span></span>    |    <span data-ttu-id="76e70-124">원본</span><span class="sxs-lookup"><span data-stu-id="76e70-124">Source</span></span>      |  <span data-ttu-id="76e70-125">대상</span><span class="sxs-lookup"><span data-stu-id="76e70-125">Destination</span></span>   |   <span data-ttu-id="76e70-126">부여</span><span class="sxs-lookup"><span data-stu-id="76e70-126">Service</span></span>    | <span data-ttu-id="76e70-127">동작</span><span class="sxs-lookup"><span data-stu-id="76e70-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="76e70-128">2000</span><span class="sxs-lookup"><span data-stu-id="76e70-128">2000</span></span> | <span data-ttu-id="76e70-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="76e70-129">Custom_Dns</span></span> | <span data-ttu-id="76e70-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="76e70-130">VirtualNetwork</span></span> | <span data-ttu-id="76e70-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="76e70-131">VirtualNetwork</span></span> | <span data-ttu-id="76e70-132">DNS(UDP/53)</span><span class="sxs-lookup"><span data-stu-id="76e70-132">DNS (UDP/53)</span></span> | <span data-ttu-id="76e70-133">허용</span><span class="sxs-lookup"><span data-stu-id="76e70-133">Allow</span></span>  |


4. <span data-ttu-id="76e70-134">각 `<NetworkConfig NetworkType="open">` 서비스에 대해 응용 프로그램 매니페스트에서 네트워킹 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-134">Specify the networking mode in the app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="76e70-135">`open` 모드에서는 서비스가 전용 IP 주소를 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-135">The mode `open` results in the service getting a dedicated IP address.</span></span> <span data-ttu-id="76e70-136">모드를 지정하지 않으면 기본 `nat` 모드를 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-136">If a mode isn't specified, it defaults to the basic `nat` mode.</span></span> <span data-ttu-id="76e70-137">따라서 다음 매니페스트 예제에서 `NodeContainerServicePackage1` 및 `NodeContainerServicePackage2`는 동일한 포트를 각각 수신할 수 있습니다(두 서비스는 모두 `Endpoint1`에서 수신 중).</span><span class="sxs-lookup"><span data-stu-id="76e70-137">Thus, in the following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen to the same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="76e70-138">Windows 클러스터용 응용 프로그램 내의 서비스에서 다른 네트워킹 모드를 혼합하고 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="76e70-139">따라서 `open` 모드에 일부 서비스가 있고 `nat` 네트워킹 모드에 일부 서비스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="76e70-140">`nat`로 서비스를 구성한 경우 수신하는 포트는 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-140">When a service is configured with `nat`, the port it is listening to must be unique.</span></span> <span data-ttu-id="76e70-141">다른 서비스에 네트워킹 모드를 혼합하는 작업은 Linux 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="76e70-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76e70-142">Next steps</span></span>
<span data-ttu-id="76e70-143">이 문서에서는 Service Fabric에서 제공하는 네트워킹 모드에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="76e70-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="76e70-144">서비스 패브릭 응용 프로그램 모델</span><span class="sxs-lookup"><span data-stu-id="76e70-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="76e70-145">Service Fabric 서비스 매니페스트 리소스</span><span class="sxs-lookup"><span data-stu-id="76e70-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="76e70-146">Windows Server 2016에서 Windows 컨테이너를 Service Fabric에 배포</span><span class="sxs-lookup"><span data-stu-id="76e70-146">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="76e70-147">Linux에서 Docker 컨테이너를 Service Fabric에 배포</span><span class="sxs-lookup"><span data-stu-id="76e70-147">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
