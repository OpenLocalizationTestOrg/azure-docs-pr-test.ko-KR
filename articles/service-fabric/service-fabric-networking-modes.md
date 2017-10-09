---
title: "Azure 서비스 패브릭 컨테이너 서비스에 대 한 모드 네트워킹 aaaConfigure | Microsoft Docs"
description: "Toosetup hello 다른 네트워킹 모드는 Azure 서비스 패브릭에서 지 원하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a>Service Fabric 컨테이너 네트워킹 모드

hello 기본 네트워킹 모드에서에서 제공 hello 서비스 패브릭 클러스터에 대 한 컨테이너 서비스는 hello `nat` 네트워킹 모드입니다. Hello로 `nat` 배포 오류에 대 한 결과 동일한 포트 네트워킹 모드를 둘 이상의 컨테이너 서비스 수신 대기 toohello 필요 합니다. 동일한 포트를 서비스 패브릭 지원 hello에서 수신 하는 몇 가지 서비스를 실행 하기 위한 hello `open` 네트워킹 모드 (5.7 이상 버전). Hello로 `open` 네트워킹 모드, 각 컨테이너 서비스 내부적으로 여러 서비스 toolisten toohello 동일한 포트를 허용 하는 동적으로 할당 된 IP 주소를 가져옵니다.   

따라서 hello 서비스 매니페스트에서 정의 된 정적 끝점과 함께 단일 서비스 형식과 함께 새로운 서비스를 만들어 hello를 사용 하 여 배포 오류 없이 삭제 `open` 네트워킹 모드입니다. 마찬가지로, 하나 צ ְ ײ 동일 hello `docker-compose.yml` 여러 서비스를 만들기 위한 정적 포트 매핑 사용 하 여 파일입니다.

IP toodiscover 서비스를 동적으로 할당 하는 hello를 사용 하 여 권장 하지 않습니다 hello IP 주소 변경 내용을 이후 hello 서비스 다시 시작 하거나 tooanother 노드로 이동 하는 경우. 만 hello를 사용 하 여 **서비스 패브릭 명명 서비스** 또는 hello **DNS 서비스** 서비스 검색에 대 한 합니다. 


> [!WARNING]
> 총 4096개의 IP가 Azure의 vNET에서 허용됩니다. 따라서 hello 노드 수 및 hello 컨테이너 서비스 인스턴스 수의 합을 hello (으로 `open` 네트워킹) vNET 내에서 4, 096를 초과할 수 없습니다. 이러한 고밀도 시나리오에 대 한 hello `nat` 네트워킹 모드를 사용 하는 것이 좋습니다.
>

## <a name="setting-up-open-networking-mode"></a>오픈 네트워킹 모드 설정

1. DNS 서비스를 사용 하 여 hello Azure 리소스 관리자 템플릿을 설정 하 고 아래에서 IP 공급자 hello `fabricSettings`합니다. 

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

2. 여러 IP 주소 toobe hello 클러스터의 각 노드에 구성 하는 hello 네트워크 프로필 섹션 tooallow를 설정 합니다. hello 다음 예제에서는 설정 노드 당 5 개의 IP 주소 (따라서 할 있습니다 각 노드에서 toohello 포트를 수신 대기 하는 5 개의 서비스 인스턴스)는 Windows 서비스 패브릭 클러스터에 대 한 합니다.

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

    Linux 클러스터에 대 한 추가 공용 IP 구성은 tooallow 아웃 바운드 연결이 추가 됩니다. hello 다음 코드 조각 설정 Linux 클러스터에 대 한 노드당 5 개의 IP 주소:

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

3. 클러스터만 NSG를 설정 하는 Windows에 대 한 다음 값에는 hello로 UDP/53 hello vNET에 대 한 포트를 열면 규칙:

   | 우선 순위 |    이름    |    원본      |  대상   |   부여    | 동작 |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS(UDP/53) | 허용  |


4. 각 서비스에 대 한 응용 프로그램 매니페스트에서 hello hello 네트워킹 모드를 지정 `<NetworkConfig NetworkType="open">`합니다.  hello 모드 `open` hello 서비스는 전용된 IP 주소 가져오기에 발생 합니다. 기본 toohello는 모드를 지정 하지 않으면 기본적으로 `nat` 모드입니다. 다음 예제에서는 매니페스트를 hello에 따라서 `NodeContainerServicePackage1` 및 `NodeContainerServicePackage2` 각 수신 toohello 수 동일한 포트 (두 서비스에서 수신 하는 `Endpoint1`).

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
Windows 클러스터용 응용 프로그램 내의 서비스에서 다른 네트워킹 모드를 혼합하고 일치시킬 수 있습니다. 따라서 `open` 모드에 일부 서비스가 있고 `nat` 네트워킹 모드에 일부 서비스가 있을 수 있습니다. 서비스를 사용 하도록 구성 된 경우 `nat`, hello 포트를 수신 대기 toomust는 고유 해야 합니다. 다른 서비스에 네트워킹 모드를 혼합하는 작업은 Linux 클러스터에서 지원되지 않습니다. 


## <a name="next-steps"></a>다음 단계
이 문서에서는 Service Fabric에서 제공하는 네트워킹 모드에 대해 알아보았습니다.  

* [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md)
* [Service Fabric 서비스 매니페스트 리소스](service-fabric-application-model.md)
* [Windows 컨테이너 tooService 패브릭 Windows Server 2016 배포](service-fabric-get-started-containers.md)
* [Docker 컨테이너 tooService 패브릭 linux 배포](service-fabric-get-started-containers-linux.md)
