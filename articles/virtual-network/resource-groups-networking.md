---
title: "리소스 공급자 개요 aaaNetwork | Microsoft Docs"
description: "Hello에 대 한 자세한 내용은 새로운 네트워크 리소스 공급자 Azure 리소스 관리자"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a>네트워크 리소스 공급자
기능 toobuild hello 및 agile, 유연한, 안전 하 고 반복 가능한 방식으로 대규모 네트워크 인식 응용 프로그램 관리를 하는 오늘날의 비즈니스 성취도에 기본 필요 합니다. Azure 리소스 관리자 리소스 그룹에 있는 리소스의 단일 컬렉션으로 이러한 응용 프로그램을 toocreate 있습니다 있습니다. 이러한 리소스는 Resource Manager의 다양한 리소스 공급자를 통해 관리됩니다.

Azure 리소스 관리자는 다른 리소스 공급자 tooprovide tooyour 리소스 액세스를 사용합니다. 네트워크, 저장소 및 계산의 세 가지 주요 리소스 공급자가 있습니다. 이 문서에서는 hello 특성과 hello 네트워크 리소스 공급자의 이점 포함 하 여:

* **메타 데이터** – 정보 tooresources 태그를 사용 하 여 추가할 수 있습니다. 이러한 태그 리소스 그룹 및 구독에서 사용 되는 tootrack 리소스 사용률을 수 있습니다.
* **네트워크 제어 향상** - 네트워크 리소스가 느슨하게 결합되고 네트워크 리소스를 세부적으로 제어할 수 있습니다. 즉, hello 네트워킹 리소스 관리에서 더 많은 유연성이 있습니다.
* **더 빠른 구성** - 네트워크 리소스가 느슨하게 결합되므로 네트워크 리소스를 병렬로 만들어서 조정할 수 있습니다. 따라서 구성 시간이 크게 단축됩니다.
* **역할 기반 액세스 제어** -RBAC 보안 관리에 대 한 사용자 정의 역할의 추가 tooallowing hello 생성에서 특정 보안 범위를 갖는 기본 역할을 제공 합니다.
* **보다 쉽게 관리 및 배포** -쉽게 toodeploy 되 고 응용 프로그램 관리 페이지의 리소스 그룹 리소스의 단일 컬렉션으로 전체 응용 프로그램 스택 만들 수 있습니다. 및 더 빠른 toodeploy 이후 단순히 템플릿 JSON 페이로드를 제공 하 여 배포할 수 있습니다.
* **신속한 사용자 지정** -배포의 선언적 스타일 템플릿 tooenable 반복 가능 하 고 신속 하 게 사용자 지정을 사용할 수 있습니다.
* **반복 가능한 사용자 지정** -배포의 선언적 스타일 템플릿 tooenable 반복 가능 하 고 신속 하 게 사용자 지정을 사용할 수 있습니다.
* **관리 인터페이스** -hello 인터페이스 toomanage 뒤의 모든 리소스를 사용할 수 있습니다.
  * REST 기반 API
  * PowerShell
  * .NET SDK
  * Node.JS SDK
  * Java SDK
  * Azure CLI
  * Preview 포털
  * Resource Manager 템플릿 언어

## <a name="network-resources"></a>네트워크 리소스
이제 네트워크 리소스를 단일 컴퓨팅 리소스(가상 컴퓨터)를 통해 모두 함께 관리하지 않고 독립적으로 관리할 수 있습니다. 이렇게 하면 리소스 그룹에서 복잡한 대규모 인프라를 더 유연하고 신속하게 구성할 수 있습니다.

다중 계층 응용 프로그램을 포함하는 샘플 배포의 개념 보기는 아래와 같습니다. NIC, 공용 IP 주소 및 VM과 같은 표시되는 각 리소스를 독립적으로 관리할 수 있습니다.

![네트워크 리소스 모델](./media/resource-groups-networking/Figure2.png)

모든 리소스에는 공통 속성 집합 및 개별 속성 집합이 포함되어 있습니다. hello 일반적인 속성은:

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **name** |고유한 리소스 이름입니다. 각 리소스 종류에 고유한 명명 제한이 있습니다. |PIP01, VM01, NIC01 |
| **위치** |hello에 리소스가 있는 azure 지역 |westus, eastus |
| **id** |고유한 URI 기반 ID입니다. |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Hello hello 섹션 아래에 리소스의 개별 속성을 확인할 수 있습니다.

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a>관리 인터페이스
다양한 인터페이스를 사용하여 Azure 네트워킹 리소스를 관리할 수 있습니다. 이 문서에서는 이러한 인터페이스 중 REST API 및 템플릿 두 가지를 중점적으로 살펴보겠습니다.

### <a name="rest-api"></a>REST API
앞서 설명한 것처럼 REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure 포털, 템플릿을 비롯하여 다양한 인터페이스를 통해 네트워크 리소스를 관리할 수 있습니다.

hello Rest API toohello HTTP 1.1 프로토콜 사양을 준수합니다. hello hello API의 일반적인 URI 구조는 아래와 같습니다.

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

고 hello 매개 변수는 중괄호에서 뒤 요소 hello:

* **subscription-id** - Azure 구독 ID입니다.
* **리소스 공급자-네임 스페이스** -사용 중인 hello 공급자에 대 한 네임 스페이스입니다. hello 네트워크 리소스 공급자에 대 한 hello 값은 *Microsoft.Network*합니다.
* **지역 이름** -hello Azure 지역 이름

hello 다음과 같은 HTTP 메서드는 지원 호출 toohello REST API를 만들 때.

* **배치** -사용 되는 지정 된 형식의 리소스 toocreate 리소스 속성을 수정 하거나 리소스 간의 연결을 변경 합니다.
* **가져오기** -프로 비전 된 리소스에 대 한 tooretrieve 정보를 사용 합니다.
* **삭제** -toodelete 기존 리소스를 사용 합니다.

Hello 요청과 응답 모두 tooa JSON 페이로드 형식을 준수합니다. 자세한 내용은 [Azure 리소스 관리 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)를 참조하세요.

### <a name="resource-manager-template-language"></a>Resource Manager 템플릿 언어
명령적으로 (통해 Api 또는 SDK) 더하기 toomanaging 리소스에서 선언적 프로그래밍 스타일 toobuild를 사용 하 고 hello 리소스 관리자 템플릿 언어를 사용 하 여 네트워크 리소스를 관리 합니다.

템플릿의 샘플 표현은 아래와 같습니다.

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

hello 서식 파일은 주로 hello 리소스 및 매개 변수를 통해 삽입 hello 인스턴스 값의 JSON 설명 합니다. 다음 예제에서는 hello 2 서브넷과 가상 네트워크를 사용 하는 toocreate 될 수 있습니다.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

서식 파일을 사용 하는 경우 hello 매개 변수 값을 수동으로 제공 하는 중 hello 옵션이 또는 매개 변수 파일을 사용할 수 있습니다. 아래 예제에서는 hello 위의 hello 템플릿으로 사용 되는 매개 변수 값 toobe 가능한 집합을 보여 줍니다.

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


서식 파일을 사용 하 여 hello 주요 이점은 다음과 같습니다.

* 선언적 스타일로 리소스 그룹에서 복잡한 인프라를 빌드할 수 있습니다. 종속성 관리 하는 등 hello 리소스를 만드는 오케스트레이션 hello, 리소스 관리자에서 처리 됩니다.
* hello 인프라 만들 수 있습니다 반복 가능한 방식으로 다양 한 지역에 걸쳐 및 영역 내에서 단순히 매개 변수를 변경 하 여 합니다.
* hello 선언적 스타일 hello 서식 파일을 작성 하 고 hello 인프라 롤아웃하기 tooshorter 지연 시간을 보여 줍니다.

샘플 템플릿은 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)을 참조하세요.

리소스 관리자 템플릿 언어 hello에 대 한 자세한 내용은 참조 하십시오. [Azure 리소스 관리자 템플릿 언어](../azure-resource-manager/resource-group-authoring-templates.md)합니다.

위의 hello 샘플 템플릿 hello 가상 네트워크 및 서브넷 리소스를 사용합니다. 사용 가능한 다른 네트워크 리소스는 아래 목록을 참조하세요.

### <a name="using-a-template"></a>템플릿 사용
서식 파일에서 서비스 tooAzure AzureCLI, PowerShell을 사용 하 여 하거나 클릭 toodeploy GitHub에서 수행 하 여 배포할 수 있습니다. GitHub에서 템플릿으로 toodeploy 서비스 단계를 수행 하는 hello를 실행 합니다.

1. GitHub에서 hello template3 파일을 엽니다. 예를 들어, [두 서브넷을 사용하는 가상 네트워크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)를 엽니다.
2. 클릭 **tooAzure 배포**, 한 다음 로그인 toohello에 자격 증명으로 Azure 포털입니다.
3. Hello 서식 파일을 확인 한 다음 클릭 **저장**합니다.
4. 클릭 **매개 변수 편집** 같은 위치를 선택 하 고 *West US*, hello vnet 및 서브넷에 대 한 합니다.
5. 필요한 경우 변경할 hello **ADDRESSPREFIX** 및 **SUBNETPREFIX** 매개 변수 및 클릭 **확인**합니다.
6. 클릭 **리소스 그룹을 선택** tooadd hello vnet 및 서브넷을 원하는 hello 리소스 그룹을 클릭 하 고 있습니다. **또는 새로 만들기**를 클릭하여 새 리소스 그룹을 만들 수도 있습니다.
7. **만들기**를 클릭합니다. 타일 표시 hello 확인 **프로 비전 템플릿 배포**합니다. Hello 배포 작업이 완료 되 면 아래 화면 비슷한 tooone를 표시 됩니다.

![샘플 템플릿 배포](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>다음 단계
[Azure 리소스 관리자 템플릿 언어](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure 네트워킹- 일반적으로 사용되는 템플릿](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)

[Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)

