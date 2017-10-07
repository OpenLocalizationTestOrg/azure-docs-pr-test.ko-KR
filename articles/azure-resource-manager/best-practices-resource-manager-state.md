---
title: "Azure 템플릿 간에 복잡 한 값 aaaPass | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 및 연결 된 템플릿을 사용 하 여 복잡 한 개체 tooshare 상태 데이터를 사용 하는 방법을 권장 하는 보여 줍니다."
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="8d7ef-103">공유 상태 tooand Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="8d7ef-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="8d7ef-104">이 항목에서는 템플릿 내에서 상태를 관리 및 공유하는 방법에 대한 모범 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="8d7ef-105">hello 매개 변수 및 변수를이 항목의 뒤에 예 tooconveniently의 배포 요구 사항을 구성의 hello 유형의 개체를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="8d7ef-106">이러한 예를 통해 사용자 환경에 맞는 속성 값으로 고유한 개체를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="8d7ef-107">이 항목은 더 큰 백서의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="8d7ef-108">전체 용지 tooread hello 다운로드 [세계 클래스 리소스 관리자 템플릿 고려 사항 및 입증 된 사례](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="8d7ef-109">표준 구성 설정 제공</span><span class="sxs-lookup"><span data-stu-id="8d7ef-109">Provide standard configuration settings</span></span>
<span data-ttu-id="8d7ef-110">총 유연 하 고 무수 한 변형 하는 서식 파일, 제공 하는 것이 아니라 일반적인 패턴은 tooprovide 알려진된 구성 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="8d7ef-111">실제로 샌드박스, 작음, 중간 및 대량과 같은 표준 티셔츠 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="8d7ef-112">티셔츠 크기의 다른 예에는 커뮤니티 버전이나 엔터프라이즈 버전 같은 제품이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="8d7ef-113">그 외 경우에는 Map Reduce 또는 No SQL 같은 특정 워크로드에 대한 기술 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="8d7ef-114">복잡 한 개체 "속성 모음" 라고도 하는 데이터 컬렉션을 포함 하는 변수 만들고 해당 데이터 toodrive hello 리소스 선언이 서식 파일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="8d7ef-115">이러한 접근 방식은 고객을 위해 미리 구성된 다양한 크기의 좋은, 알려진 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="8d7ef-116">알려진된 구성을 없이 hello 서식 파일의 사용자 확인 플랫폼 리소스 제약 조건에서 자체적으로 요소에는 클러스터 크기 조정 하 고 해야 수학 tooidentify hello 결과의 저장소 계정 및 기타 리소스 분할을 수행 (toocluster 크기 인해 및 리소스 제약 조건)입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="8d7ef-117">또한 hello 고객에 대 한 향상 된 환경 toomaking 몇 가지 알려진된 구성을 쉽게 toosupport 됩니다 하 고 더 높은 수준의 밀도 제공 하는 데 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="8d7ef-118">hello 방법을 예제와 다음 복잡 한 데이터의 컬렉션을 나타내는 개체를 포함 하는 toodefine 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="8d7ef-119">가상 컴퓨터 크기, 네트워크 설정, 운영 체제 설정 및 가용성 설정에 사용 되는 값을 정의 하는 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="8d7ef-120">해당 hello 확인 **tshirtSize** 변수 연결 매개 변수를 통해 제공 하는 hello 티셔츠 크기 (**작은**, **보통**, **Large**) toohello 텍스트 **tshirtSize**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="8d7ef-121">티셔츠 크기에 대 한이 변수 tooretrieve hello 관련 된 복잡 한 개체 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="8d7ef-122">그런 다음 hello 서식 파일의 뒷부분에 나오는 이러한 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="8d7ef-123">hello 기능 tooreference 라는-변수 및 해당 속성 hello 템플릿 구문을 간소화 하 고 쉽게 toounderstand 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="8d7ef-124">다음 예제는 hello tooset 값 앞에 표시 된 hello 개체를 사용 하 여 리소스 toodeploy를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="8d7ef-125">에 대 한 hello 값을 검색 하 여 hello VM 크기는 설정 하는 예를 들어 `variables('tshirtSize').vmSize` 에서 hello 디스크 크기를 검색에 대 한 hello 값 동안 `variables('tshirtSize').diskSize`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="8d7ef-126">또한 연결 된 서식 파일에 대 한 hello 값으로 설정 되어에 대 한 URI를 hello `variables('tshirtSize').vmTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="8d7ef-127">상태 tooa 서식 파일을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-127">Pass state tooa template</span></span>
<span data-ttu-id="8d7ef-128">배포 중에 직접 제공한 매개 변수를 통해 템플릿으로 상태를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="8d7ef-129">다음 템플릿에서 테이블 일반적으로 사용 되는 목록을 매개 변수 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="8d7ef-130">이름</span><span class="sxs-lookup"><span data-stu-id="8d7ef-130">Name</span></span> | <span data-ttu-id="8d7ef-131">값</span><span class="sxs-lookup"><span data-stu-id="8d7ef-131">Value</span></span> | <span data-ttu-id="8d7ef-132">설명</span><span class="sxs-lookup"><span data-stu-id="8d7ef-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d7ef-133">location</span><span class="sxs-lookup"><span data-stu-id="8d7ef-133">location</span></span> |<span data-ttu-id="8d7ef-134">제한된 Azure 영역 목록의 문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="8d7ef-135">hello 위치 hello 리소스가 배포 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="8d7ef-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="8d7ef-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="8d7ef-137">문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-137">String</span></span> |<span data-ttu-id="8d7ef-138">Hello hello VM 디스크를 배치 하는 저장소 계정에 대 한 고유 DNS 이름</span><span class="sxs-lookup"><span data-stu-id="8d7ef-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="8d7ef-139">domainName</span><span class="sxs-lookup"><span data-stu-id="8d7ef-139">domainName</span></span> |<span data-ttu-id="8d7ef-140">문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-140">String</span></span> |<span data-ttu-id="8d7ef-141">Hello 형식에서 hello 공개적으로 액세스 가능한 jumpbox VM의 도메인 이름: **{domainName}. { location}.cloudapp.com** 예: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="8d7ef-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="8d7ef-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="8d7ef-142">adminUsername</span></span> |<span data-ttu-id="8d7ef-143">문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-143">String</span></span> |<span data-ttu-id="8d7ef-144">Hello Vm에 대 한 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="8d7ef-144">Username for hello VMs</span></span> |
| <span data-ttu-id="8d7ef-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="8d7ef-145">adminPassword</span></span> |<span data-ttu-id="8d7ef-146">문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-146">String</span></span> |<span data-ttu-id="8d7ef-147">Hello Vm에 대 한 암호</span><span class="sxs-lookup"><span data-stu-id="8d7ef-147">Password for hello VMs</span></span> |
| <span data-ttu-id="8d7ef-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="8d7ef-148">tshirtSize</span></span> |<span data-ttu-id="8d7ef-149">제공된 티셔츠 크기의 제한된 목록에서 가져온 문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="8d7ef-150">배율 단위 크기 tooprovision 명명 된 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="8d7ef-151">예: "Small", "Medium", "Large"</span><span class="sxs-lookup"><span data-stu-id="8d7ef-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="8d7ef-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="8d7ef-152">virtualNetworkName</span></span> |<span data-ttu-id="8d7ef-153">문자열</span><span class="sxs-lookup"><span data-stu-id="8d7ef-153">String</span></span> |<span data-ttu-id="8d7ef-154">소비자 hello hello 가상 네트워크의 이름 toouse를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="8d7ef-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="8d7ef-155">enableJumpbox</span></span> |<span data-ttu-id="8d7ef-156">제한된 목록에서 가져온 문자열(enabled/disabled)</span><span class="sxs-lookup"><span data-stu-id="8d7ef-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="8d7ef-157">매개 변수를 식별 하는 여부 tooenable hello 환경에 대 한 jumpbox 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="8d7ef-158">값: "enabled", "disabled"</span><span class="sxs-lookup"><span data-stu-id="8d7ef-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="8d7ef-159">hello **tshirtSize** hello 이전 섹션에서 사용 되는 매개 변수를 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="8d7ef-160">상태 toolinked 템플릿 전달</span><span class="sxs-lookup"><span data-stu-id="8d7ef-160">Pass state toolinked templates</span></span>
<span data-ttu-id="8d7ef-161">Toolinked 서식 파일에 연결할 때 종종 정적을 함께 사용 했으며 변수를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="8d7ef-162">정적 변수</span><span class="sxs-lookup"><span data-stu-id="8d7ef-162">Static variables</span></span>
<span data-ttu-id="8d7ef-163">정적 변수 예: Url 템플릿 전체에서 사용 되는 사용 되는 tooprovide 기준 값 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="8d7ef-164">다음 템플릿 발췌 hello에 `templateBaseUrl` GitHub에서 hello 서식 파일에 대 한 hello 루트 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="8d7ef-165">새 변수를 작성 하는 hello 다음 줄 `sharedTemplateUrl` hello 기준 URL hello 공유 리소스에 대 한 템플릿의 hello 알려진된 이름으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="8d7ef-166">해당 줄 아래 복잡 한 개체 변수는 사용 되는 toostore 티셔츠 크기, 여기서 hello 기준 URL은 연결 된 toohello 구성 템플릿 위치를 알고 있으며 hello에 저장 된 `vmTemplate` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="8d7ef-167">이 방법의 hello 이점은 hello 템플릿 위치 변경 되 면 하기만 하면 연결 된 hello 템플릿 전체에서 전달 하는 한 곳에서 toochange hello 정적 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="8d7ef-168">생성된 변수</span><span class="sxs-lookup"><span data-stu-id="8d7ef-168">Generated variables</span></span>
<span data-ttu-id="8d7ef-169">또한 toostatic 변수에서 여러 변수는 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="8d7ef-170">이 섹션의 hello 일반적인 형식이 생성 된 변수를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="8d7ef-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="8d7ef-171">tshirtSize</span></span>
<span data-ttu-id="8d7ef-172">위의 hello 예제에서이 생성 된 변수 잘 알고 있다면 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="8d7ef-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="8d7ef-173">networkSettings</span></span>
<span data-ttu-id="8d7ef-174">용량, 기능, 또는 범위가 지정 된 종단 간 솔루션 템플릿을 hello 연결 된 템플릿 일반적으로 네트워크에 있는 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="8d7ef-175">간단 하 게 하는 한 가지 방법은 toouse 복합 개체 toostore 네트워크 설정 이며 toolinked 서식 파일을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="8d7ef-176">아래에서 네트워크 설정을 전달하는 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="8d7ef-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="8d7ef-177">availabilitySettings</span></span>
<span data-ttu-id="8d7ef-178">연결된 템플릿에서 만든 리소스는 종종 가용성 집합에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="8d7ef-179">다음 예제는 hello, hello 가용성 집합 이름을 지정 하 고도 장애 도메인을 hello와 업데이트 도메인 개수 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="8d7ef-180">여러 가용성 집합 (예를 들어 마스터 노드가 마다 하나씩) 및 다른 데이터 노드를 해야 하는 경우 이름을 접두사로 사용 가용성 집합이 여러 개 지정 하거나 특정 티셔츠 크기에 대 한 변수를 만들기 위한 앞에 표시 된 hello 모델을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="8d7ef-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="8d7ef-181">storageSettings</span></span>
<span data-ttu-id="8d7ef-182">저장소 세부 정보는 연결된 템플릿과 종종 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="8d7ef-183">다음 hello 예제에는 *storageSettings* 개체 hello에 대 한 세부 정보를 저장소 계정 및 컨테이너 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="8d7ef-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="8d7ef-184">osSettings</span></span>
<span data-ttu-id="8d7ef-185">연결 된 템플릿으로 알려진된 여러 가지 구성 유형을 통해 toopass 운영 체제 설정을 toovarious 노드 종류를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="8d7ef-186">복잡 한 개체는 쉽게 toostore 및 공유 운영 체제 정보 및을 사용 하면 보다 쉽게 toosupport 배포에 대 한 여러 운영 체제 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="8d7ef-187">hello 다음 보여 주는 예제에 대 한 개체 *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="8d7ef-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="8d7ef-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="8d7ef-188">machineSettings</span></span>
<span data-ttu-id="8d7ef-189">생성된 변수인 *machineSettings*는 VM을 만들기 위한 혼합된 핵심 변수를 포함하는 복잡한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="8d7ef-190">hello 변수는 관리자 사용자 이름 및 암호, hello VM 이름에 대 한 접두사 및 운영 체제 이미지 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="8d7ef-191">*osImageReference* 검색 hello hello 값 *osSettings* hello 기본 서식 파일에 정의 된 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="8d7ef-192">즉, VM에 대 한 hello 운영 체제를 쉽게 변경할 수 있습니다-완전히 또는 템플릿 소비자의 hello 기본 설정에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="8d7ef-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="8d7ef-193">vmScripts</span></span>
<span data-ttu-id="8d7ef-194">hello *vmScripts* 개체 스크립트 toodownload hello에 대 한 세부 정보를 포함 하 고 외부 및 내부 참조를 포함 하 여 VM 인스턴스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="8d7ef-195">외부 참조 hello 인프라를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="8d7ef-196">내부 참조 hello 설치 된 소프트웨어를 설치 및 구성에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="8d7ef-197">Hello를 사용 하 여 *scriptsToDownload* 속성 toolist hello toodownload toohello VM을 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="8d7ef-198">이 개체는 또한 여러 유형의 동작에 대 한 참조가 toocommand 줄 인수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="8d7ef-199">이 해당 각 개별 노드, 설치 된 모든 노드에 배포 된 후에 실행 되 고 서식 파일을 지정 하는 특정 tooa 수 있는 추가 스크립트에 대 한 hello 기본 설치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="8d7ef-200">이 예제에서 사용 되는 템플릿 toodeploy MongoDB 중재자 toodeliver 높은 가용성을 필요로 하는.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="8d7ef-201">hello *arbiterNodeInstallCommand* 너무 추가한*vmScripts* tooinstall hello 중재자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="8d7ef-202">hello 변수 섹션 hello 적절 한 값을 사용 하 여 hello tooexecute hello 스크립트를 특정 텍스트를 정의 하는 hello 변수를 찾을 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="8d7ef-203">템플릿에서 상태 반환</span><span class="sxs-lookup"><span data-stu-id="8d7ef-203">Return state from a template</span></span>
<span data-ttu-id="8d7ef-204">뿐만 아니라 수 데이터를 템플릿으로,, 공유 데이터 백 toohello 호출 서식 파일을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="8d7ef-205">Hello에 **출력** 섹션, 연결 된 템플릿의 hello 원본 템플릿을 사용할 수 있는 키/값 쌍을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="8d7ef-206">hello 다음 예제에서는 어떻게 toopass hello 연결 된 서식 파일에서 생성 된 개인 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8d7ef-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="8d7ef-207">Hello 주 템플릿 내에서 구문 다음 hello로 해당 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="8d7ef-208">이 식은 hello 출력 섹션 또는 hello 기본 서식 파일의 hello 리소스 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="8d7ef-209">Hello 런타임 상태를 사용 하기 때문에 hello 식 hello 변수 섹션에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="8d7ef-210">tooreturn hello 기본 서식 파일에서 사용 하 여가이 값:</span><span class="sxs-lookup"><span data-stu-id="8d7ef-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="8d7ef-211">가상 컴퓨터에 대 한 연결 된 템플릿 tooreturn 데이터 디스크의 섹션을 출력 하는 hello를 사용 하는 예제를 참조 [가상 컴퓨터에 대 한 여러 데이터 디스크를 만드는](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="8d7ef-212">가상 컴퓨터에 대한 인증 설정 정의</span><span class="sxs-lookup"><span data-stu-id="8d7ef-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="8d7ef-213">Hello를 사용할 수는 가상 컴퓨터에 대 한 구성 설정 toospecify hello 인증 설정에 대해 이전에 표시 된 같은 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="8d7ef-214">인증 유형 hello에에서 전달 하기 위한 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="8d7ef-215">Hello 서로 다른 인증 유형과 hello hello 매개 변수 값에 따라이 배포에 대 한 어떤 유형이 사용 되는 변수 toostore에 대 한 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="8d7ef-216">Hello 설정 hello 가상 컴퓨터를 정의할 때 **osProfile** 만든 toohello 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7ef-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="8d7ef-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d7ef-217">Next steps</span></span>
* <span data-ttu-id="8d7ef-218">toolearn hello 템플릿의 hello 섹션에 대 한 참조 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="8d7ef-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="8d7ef-219">toosee hello 함수는 서식 파일에서 사용할 수 있는 참조 [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="8d7ef-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
