---
title: "Azure 템플릿 간의 복잡한 값 전달 | Microsoft Docs"
description: "복잡한 개체를 사용하여 Azure Resource Manager 템플릿 및 연결된 템플릿과 상태 데이터를 공유하는 권장 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="439a3-103">Azure Resource Manager 템플릿과 상태 공유</span><span class="sxs-lookup"><span data-stu-id="439a3-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="439a3-104">이 항목에서는 템플릿 내에서 상태를 관리 및 공유하는 방법에 대한 모범 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="439a3-105">이 항목에 표시된 매개 변수 및 변수는 배포 요구 사항을 편리하게 구성하기 위해 정의할 수 있는 개체 유형의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="439a3-106">이러한 예를 통해 사용자 환경에 맞는 속성 값으로 고유한 개체를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="439a3-107">이 항목은 더 큰 백서의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="439a3-108">전체 문서를 읽으려면 [세계적인 Resource Manager 템플릿 고려 사항 및 입증 사례](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="439a3-109">표준 구성 설정 제공</span><span class="sxs-lookup"><span data-stu-id="439a3-109">Provide standard configuration settings</span></span>
<span data-ttu-id="439a3-110">일반적인 패턴은 절대적인 유연성과 수많은 변형을 제공하는 템플릿이 아니라 알려진 구성 중에서 선택하도록 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="439a3-111">실제로 샌드박스, 작음, 중간 및 대량과 같은 표준 티셔츠 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="439a3-112">티셔츠 크기의 다른 예에는 커뮤니티 버전이나 엔터프라이즈 버전 같은 제품이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="439a3-113">그 외 경우에는 Map Reduce 또는 No SQL 같은 특정 워크로드에 대한 기술 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="439a3-114">복잡한 개체의 경우 "속성 모음"이라고도 하는 데이터 컬렉션을 포함하는 변수를 만들고 해당 데이터를 사용하여 템플릿에서 리소스 선언을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="439a3-115">이러한 접근 방식은 고객을 위해 미리 구성된 다양한 크기의 좋은, 알려진 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="439a3-116">알려진 구성이 없는 경우, 템플릿 사용자는 자체적으로 클러스터 크기, 플랫폼 리소스 제약 조건의 요소를 결정하고 그에 따라 파생되는 저장소 계정 및 기타 리소스(클러스터 크기 및 리소스 제약 조언에 따른)에 대한 분할을 식별하기 위해 계산해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="439a3-117">고객을 위한 환경을 개선하는 것 외에도, 몇몇 알려진 구성은 지원하기가 쉽고 높은 수준의 밀도를 제공하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="439a3-118">다음 예제에서는 데이터 컬렉션을 나타내기 위한 복잡한 개체를 포함하는 변수의 정의 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="439a3-119">이 컬렉션은 가상 컴퓨터 크기, 네트워크 설정, 운영 체제 설정 및 가용성 설정에 사용되는 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="439a3-120">**tshirtSize** 변수는 매개 변수(**Small**, **Medium**, **Large**)를 통해 제공한 티셔츠 크기를 **tshirtSize** 텍스트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="439a3-121">이 변수를 사용하여 해당 티셔츠 크기에 대한 연결된 복잡한 개체 변수를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="439a3-122">그런 다음 템플릿의 뒷부분에서 이러한 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="439a3-123">명명된 변수 및 해당 속성을 참조하는 기능이 구현되면 템플릿 구문이 단순화되며 컨텍스트를 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="439a3-124">다음 예제에서는 위에 표시된 개체를 통해 값을 설정하여 배포할 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="439a3-125">예를 들어 디스크 크기 값은 `variables('tshirtSize').diskSize`에서 검색되지만 VM 크기는 `variables('tshirtSize').vmSize` 값을 검색하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="439a3-126">또한 연결된 템플릿에 대한 URI는 `variables('tshirtSize').vmTemplate`값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="439a3-127">템플릿에 상태 전달</span><span class="sxs-lookup"><span data-stu-id="439a3-127">Pass state to a template</span></span>
<span data-ttu-id="439a3-128">배포 중에 직접 제공한 매개 변수를 통해 템플릿으로 상태를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="439a3-129">다음 테이블에는 템플릿 내에서 일반적으로 사용되는 매개 변수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="439a3-130">이름</span><span class="sxs-lookup"><span data-stu-id="439a3-130">Name</span></span> | <span data-ttu-id="439a3-131">값</span><span class="sxs-lookup"><span data-stu-id="439a3-131">Value</span></span> | <span data-ttu-id="439a3-132">설명</span><span class="sxs-lookup"><span data-stu-id="439a3-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="439a3-133">location</span><span class="sxs-lookup"><span data-stu-id="439a3-133">location</span></span> |<span data-ttu-id="439a3-134">제한된 Azure 영역 목록의 문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="439a3-135">리소스가 배포되어 있는 위치</span><span class="sxs-lookup"><span data-stu-id="439a3-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="439a3-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="439a3-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="439a3-137">문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-137">String</span></span> |<span data-ttu-id="439a3-138">VM의 디스크가 배치될 저장소 계정의 고유 DNS 이름</span><span class="sxs-lookup"><span data-stu-id="439a3-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="439a3-139">domainName</span><span class="sxs-lookup"><span data-stu-id="439a3-139">domainName</span></span> |<span data-ttu-id="439a3-140">문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-140">String</span></span> |<span data-ttu-id="439a3-141">공개적으로 액세스할 수 있는 jumpbox VM의 도메인 이름 형식: **{domainName}.{location}.cloudapp.com** 예: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="439a3-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="439a3-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="439a3-142">adminUsername</span></span> |<span data-ttu-id="439a3-143">문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-143">String</span></span> |<span data-ttu-id="439a3-144">VM의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="439a3-144">Username for the VMs</span></span> |
| <span data-ttu-id="439a3-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="439a3-145">adminPassword</span></span> |<span data-ttu-id="439a3-146">문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-146">String</span></span> |<span data-ttu-id="439a3-147">VM에 대한 암호</span><span class="sxs-lookup"><span data-stu-id="439a3-147">Password for the VMs</span></span> |
| <span data-ttu-id="439a3-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="439a3-148">tshirtSize</span></span> |<span data-ttu-id="439a3-149">제공된 티셔츠 크기의 제한된 목록에서 가져온 문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="439a3-150">프로비전할 명명된 배율 단위 크기.</span><span class="sxs-lookup"><span data-stu-id="439a3-150">The named scale unit size to provision.</span></span> <span data-ttu-id="439a3-151">예: "Small", "Medium", "Large"</span><span class="sxs-lookup"><span data-stu-id="439a3-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="439a3-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="439a3-152">virtualNetworkName</span></span> |<span data-ttu-id="439a3-153">문자열</span><span class="sxs-lookup"><span data-stu-id="439a3-153">String</span></span> |<span data-ttu-id="439a3-154">소비자가 사용하려는 가상 네트워크의 이름.</span><span class="sxs-lookup"><span data-stu-id="439a3-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="439a3-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="439a3-155">enableJumpbox</span></span> |<span data-ttu-id="439a3-156">제한된 목록에서 가져온 문자열(enabled/disabled)</span><span class="sxs-lookup"><span data-stu-id="439a3-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="439a3-157">환경에 대해 jumpbox를 사용하도록 설정할지 여부를 식별하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="439a3-158">값: "enabled", "disabled"</span><span class="sxs-lookup"><span data-stu-id="439a3-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="439a3-159">이전 섹션에서 사용된 **tshirtSize** 매개 변수는 다음으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="439a3-160">연결된 템플릿에 상태 전달</span><span class="sxs-lookup"><span data-stu-id="439a3-160">Pass state to linked templates</span></span>
<span data-ttu-id="439a3-161">연결된 템플릿에 연결할 경우 정적 변수와 생성된 변수를 혼합해서 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="439a3-162">정적 변수</span><span class="sxs-lookup"><span data-stu-id="439a3-162">Static variables</span></span>
<span data-ttu-id="439a3-163">정적 변수는 템플릿 전체에서 사용되는 URL과 같은 기본값을 제공하는 데 종종 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="439a3-164">아래에 발췌한 다음 템플릿에서 `templateBaseUrl`은 GitHub에서 템플릿의 루트 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="439a3-165">다음 줄은 기본 URL을 공유 리소스 템플릿의 알려진 이름에 연결하는 새 변수 `sharedTemplateUrl`을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="439a3-166">해당 줄 아래에서 복잡한 개체 변수는 티셔츠 크기를 저장하는 데 사용됩니다. 여기서 기본 URL은 알려진 구성 템플릿 위치에 연결되어 `vmTemplate` 속성에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="439a3-167">이 접근 방식의 이점은 템플릿 위치가 변경된 경우 한 곳에서만 정적 변수를 변경하면 된다는 점입니다. 그러면 연결된 템플릿 전체로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="439a3-168">생성된 변수</span><span class="sxs-lookup"><span data-stu-id="439a3-168">Generated variables</span></span>
<span data-ttu-id="439a3-169">정적 변수 외에도 다양한 변수가 동적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="439a3-170">이 섹션에서는 생성된 변수의 몇 가지 일반적인 유형에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="439a3-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="439a3-171">tshirtSize</span></span>
<span data-ttu-id="439a3-172">위 예제에서 생성된 이 변수는 이미 잘 알고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="439a3-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="439a3-173">networkSettings</span></span>
<span data-ttu-id="439a3-174">용량, 기능 또는 전체 범위의 솔루션 템플릿에서 연결된 템플릿은 일반적으로 네트워크에 존재하는 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="439a3-175">한 가지 간단한 방법은 복잡한 개체를 사용하여 네트워크 설정을 저장하고 연결된 템플릿에 전달하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="439a3-176">아래에서 네트워크 설정을 전달하는 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="439a3-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="439a3-177">availabilitySettings</span></span>
<span data-ttu-id="439a3-178">연결된 템플릿에서 만든 리소스는 종종 가용성 집합에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="439a3-179">다음 예에서는 가용성 집합 이름이 지정되고, 사용할 장애 도메인 및 업데이트 도메인 수도 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="439a3-180">여러 가용성 집합(예를 들어 마스터 노드용 하나와 데이터 노드용 하나)이 필요한 경우 이름을 접두사로 사용하거나, 여러 가용성 집합을 지정하거나, 앞서 제시된 특정 티셔츠 크기에 해당하는 변수 생성 방법 예를 따라 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="439a3-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="439a3-181">storageSettings</span></span>
<span data-ttu-id="439a3-182">저장소 세부 정보는 연결된 템플릿과 종종 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="439a3-183">아래 예제에서 *storageSettings* 개체는 저장소 계정 및 컨테이너 이름에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="439a3-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="439a3-184">osSettings</span></span>
<span data-ttu-id="439a3-185">연결된 템플릿을 사용할 경우 알려진 여러 구성 유형의 다양한 노드 형식에 운영 체제 설정을 전달해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="439a3-186">복잡한 개체는 운영 체제 정보를 쉽게 저장 및 공유하고 운영 체제에서 제공되는 다양한 배포 옵션을 보다 쉽게 지원할 수 있도록 하는 간편한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="439a3-187">다음 예제에는 *osSettings*용 개체가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="439a3-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="439a3-188">machineSettings</span></span>
<span data-ttu-id="439a3-189">생성된 변수인 *machineSettings*는 VM을 만들기 위한 혼합된 핵심 변수를 포함하는 복잡한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="439a3-190">변수에는 관리자 사용자 이름 및 암호, VM 이름의 접두사 및 운영 체제 이미지 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="439a3-191">*osImageReference*는 주 템플릿에 정의된 *osSettings* 변수에서 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="439a3-192">즉, VM에 대한 운영 체제를 완전히 또는 템플릿 소비자의 기본 설정에 따라 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="439a3-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="439a3-193">vmScripts</span></span>
<span data-ttu-id="439a3-194">*vmScripts* 개체에는 외부 및 내부 참조를 포함하여 VM 인스턴스에서 다운로드 및 실행할 스크립트에 대한 세부 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="439a3-195">외부 참조는 인프라를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="439a3-196">내부 참조에는 설치된 소프트웨어와 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="439a3-197">*scriptsToDownload* 속성을 사용하여 VM으로 다운로드할 스크립트 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="439a3-198">이 개체에는 다양한 유형의 동작에 대한 명령줄 인수의 참조도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="439a3-199">이러한 동작에는 각 개별 노드에 대한 기본 설치, 모든 노드를 배포한 후에 실행되는 설치 및 지정된 템플릿에서만 사용할 수 있는 추가 스크립트의 실행이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="439a3-200">이 예제는 MongoDB를 배포하는 데 사용되는 템플릿에서 가져온 것입니다. 여기서 중재자는 고가용성을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="439a3-201">중재자를 설치하기 위해 *vmScripts*에 *arbiterNodeInstallCommand*가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="439a3-202">변수 섹션은 적절한 값으로 스크립트를 실행하기 위해 특정 텍스트를 정의하는 변수를 찾는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="439a3-203">템플릿에서 상태 반환</span><span class="sxs-lookup"><span data-stu-id="439a3-203">Return state from a template</span></span>
<span data-ttu-id="439a3-204">템플릿으로 데이터를 전달할 뿐만 아니라 호출 템플릿과 다시 데이터를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="439a3-205">연결된 템플릿의 **출력** 섹션에서는 원본 템플릿에서 사용될 수 있는 키/값 쌍을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="439a3-206">다음 예제에서는 연결된 템플릿에서 생성된 개인 IP 주소를 전달하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="439a3-207">주 템플릿 내에서 다음 구문을 사용하여 해당 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="439a3-208">주 템플릿의 출력 섹션 또는 리소스 섹션에서 이 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="439a3-209">변수 섹션은 런타임 상태에 의존하므로 이 식을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="439a3-210">주 템플릿에서 이 값을 반환하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="439a3-211">연결된 템플릿의 출력 섹션을 사용하여 가상 컴퓨터에 대한 데이터 디스크를 반환하는 예제는 [가상 컴퓨터에 대한 여러 데이터 디스크 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="439a3-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="439a3-212">가상 컴퓨터에 대한 인증 설정 정의</span><span class="sxs-lookup"><span data-stu-id="439a3-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="439a3-213">위에 표시된 동일한 패턴을 구성 설정에 사용하여 가상 컴퓨터의 인증 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="439a3-214">인증 형식을 전달하기 위한 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="439a3-215">다른 인증 형식에 대한 변수 및 매개 변수 값에 따라 이 배포에 사용되는 형식을 저장할 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="439a3-216">가상 컴퓨터를 정의할 때 **osProfile** 을 사용자가 만든 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="439a3-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="439a3-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="439a3-217">Next steps</span></span>
* <span data-ttu-id="439a3-218">템플릿의 섹션에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="439a3-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="439a3-219">템플릿 내에서 사용할 수 있는 모든 함수는 [Azure Resource Manager 템플릿 함수](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="439a3-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
