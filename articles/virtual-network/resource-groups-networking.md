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
# <a name="network-resource-provider"></a><span data-ttu-id="35674-103">네트워크 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="35674-103">Network Resource Provider</span></span>
<span data-ttu-id="35674-104">기능 toobuild hello 및 agile, 유연한, 안전 하 고 반복 가능한 방식으로 대규모 네트워크 인식 응용 프로그램 관리를 하는 오늘날의 비즈니스 성취도에 기본 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="35674-105">Azure 리소스 관리자 리소스 그룹에 있는 리소스의 단일 컬렉션으로 이러한 응용 프로그램을 toocreate 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="35674-106">이러한 리소스는 Resource Manager의 다양한 리소스 공급자를 통해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="35674-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="35674-107">Azure 리소스 관리자는 다른 리소스 공급자 tooprovide tooyour 리소스 액세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="35674-108">네트워크, 저장소 및 계산의 세 가지 주요 리소스 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="35674-109">이 문서에서는 hello 특성과 hello 네트워크 리소스 공급자의 이점 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="35674-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="35674-110">**메타 데이터** – 정보 tooresources 태그를 사용 하 여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="35674-111">이러한 태그 리소스 그룹 및 구독에서 사용 되는 tootrack 리소스 사용률을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="35674-112">**네트워크 제어 향상** - 네트워크 리소스가 느슨하게 결합되고 네트워크 리소스를 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="35674-113">즉, hello 네트워킹 리소스 관리에서 더 많은 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="35674-114">**더 빠른 구성** - 네트워크 리소스가 느슨하게 결합되므로 네트워크 리소스를 병렬로 만들어서 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="35674-115">따라서 구성 시간이 크게 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="35674-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="35674-116">**역할 기반 액세스 제어** -RBAC 보안 관리에 대 한 사용자 정의 역할의 추가 tooallowing hello 생성에서 특정 보안 범위를 갖는 기본 역할을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="35674-117">**보다 쉽게 관리 및 배포** -쉽게 toodeploy 되 고 응용 프로그램 관리 페이지의 리소스 그룹 리소스의 단일 컬렉션으로 전체 응용 프로그램 스택 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="35674-118">및 더 빠른 toodeploy 이후 단순히 템플릿 JSON 페이로드를 제공 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="35674-119">**신속한 사용자 지정** -배포의 선언적 스타일 템플릿 tooenable 반복 가능 하 고 신속 하 게 사용자 지정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="35674-120">**반복 가능한 사용자 지정** -배포의 선언적 스타일 템플릿 tooenable 반복 가능 하 고 신속 하 게 사용자 지정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="35674-121">**관리 인터페이스** -hello 인터페이스 toomanage 뒤의 모든 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="35674-122">REST 기반 API</span><span class="sxs-lookup"><span data-stu-id="35674-122">REST based API</span></span>
  * <span data-ttu-id="35674-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35674-123">PowerShell</span></span>
  * <span data-ttu-id="35674-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="35674-124">.NET SDK</span></span>
  * <span data-ttu-id="35674-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="35674-125">Node.JS SDK</span></span>
  * <span data-ttu-id="35674-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="35674-126">Java SDK</span></span>
  * <span data-ttu-id="35674-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35674-127">Azure CLI</span></span>
  * <span data-ttu-id="35674-128">Preview 포털</span><span class="sxs-lookup"><span data-stu-id="35674-128">Preview Portal</span></span>
  * <span data-ttu-id="35674-129">Resource Manager 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35674-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="35674-130">네트워크 리소스</span><span class="sxs-lookup"><span data-stu-id="35674-130">Network resources</span></span>
<span data-ttu-id="35674-131">이제 네트워크 리소스를 단일 컴퓨팅 리소스(가상 컴퓨터)를 통해 모두 함께 관리하지 않고 독립적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="35674-132">이렇게 하면 리소스 그룹에서 복잡한 대규모 인프라를 더 유연하고 신속하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="35674-133">다중 계층 응용 프로그램을 포함하는 샘플 배포의 개념 보기는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="35674-134">NIC, 공용 IP 주소 및 VM과 같은 표시되는 각 리소스를 독립적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![네트워크 리소스 모델](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="35674-136">모든 리소스에는 공통 속성 집합 및 개별 속성 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="35674-137">hello 일반적인 속성은:</span><span class="sxs-lookup"><span data-stu-id="35674-137">hello common properties are:</span></span>

| <span data-ttu-id="35674-138">속성</span><span class="sxs-lookup"><span data-stu-id="35674-138">Property</span></span> | <span data-ttu-id="35674-139">설명</span><span class="sxs-lookup"><span data-stu-id="35674-139">Description</span></span> | <span data-ttu-id="35674-140">샘플 값</span><span class="sxs-lookup"><span data-stu-id="35674-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35674-141">**name**</span><span class="sxs-lookup"><span data-stu-id="35674-141">**name**</span></span> |<span data-ttu-id="35674-142">고유한 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="35674-142">Unique resource name.</span></span> <span data-ttu-id="35674-143">각 리소스 종류에 고유한 명명 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="35674-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="35674-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="35674-145">**위치**</span><span class="sxs-lookup"><span data-stu-id="35674-145">**location**</span></span> |<span data-ttu-id="35674-146">hello에 리소스가 있는 azure 지역</span><span class="sxs-lookup"><span data-stu-id="35674-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="35674-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="35674-147">westus, eastus</span></span> |
| <span data-ttu-id="35674-148">**id**</span><span class="sxs-lookup"><span data-stu-id="35674-148">**id**</span></span> |<span data-ttu-id="35674-149">고유한 URI 기반 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="35674-149">Unique URI based identification</span></span> |<span data-ttu-id="35674-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="35674-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="35674-151">Hello hello 섹션 아래에 리소스의 개별 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-151">You can check hello individual properties of resources in hello sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="35674-152">관리 인터페이스</span><span class="sxs-lookup"><span data-stu-id="35674-152">Management interfaces</span></span>
<span data-ttu-id="35674-153">다양한 인터페이스를 사용하여 Azure 네트워킹 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="35674-154">이 문서에서는 이러한 인터페이스 중 REST API 및 템플릿 두 가지를 중점적으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="35674-155">REST API</span><span class="sxs-lookup"><span data-stu-id="35674-155">REST API</span></span>
<span data-ttu-id="35674-156">앞서 설명한 것처럼 REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure 포털, 템플릿을 비롯하여 다양한 인터페이스를 통해 네트워크 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="35674-157">hello Rest API toohello HTTP 1.1 프로토콜 사양을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="35674-158">hello hello API의 일반적인 URI 구조는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="35674-159">고 hello 매개 변수는 중괄호에서 뒤 요소 hello:</span><span class="sxs-lookup"><span data-stu-id="35674-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="35674-160">**subscription-id** - Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="35674-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="35674-161">**리소스 공급자-네임 스페이스** -사용 중인 hello 공급자에 대 한 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="35674-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="35674-162">hello 네트워크 리소스 공급자에 대 한 hello 값은 *Microsoft.Network*합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="35674-163">**지역 이름** -hello Azure 지역 이름</span><span class="sxs-lookup"><span data-stu-id="35674-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="35674-164">hello 다음과 같은 HTTP 메서드는 지원 호출 toohello REST API를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="35674-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="35674-165">**배치** -사용 되는 지정 된 형식의 리소스 toocreate 리소스 속성을 수정 하거나 리소스 간의 연결을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="35674-166">**가져오기** -프로 비전 된 리소스에 대 한 tooretrieve 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="35674-167">**삭제** -toodelete 기존 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="35674-168">Hello 요청과 응답 모두 tooa JSON 페이로드 형식을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="35674-169">자세한 내용은 [Azure 리소스 관리 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35674-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="35674-170">Resource Manager 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35674-170">Resource Manager template language</span></span>
<span data-ttu-id="35674-171">명령적으로 (통해 Api 또는 SDK) 더하기 toomanaging 리소스에서 선언적 프로그래밍 스타일 toobuild를 사용 하 고 hello 리소스 관리자 템플릿 언어를 사용 하 여 네트워크 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="35674-172">템플릿의 샘플 표현은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="35674-173">hello 서식 파일은 주로 hello 리소스 및 매개 변수를 통해 삽입 hello 인스턴스 값의 JSON 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="35674-174">다음 예제에서는 hello 2 서브넷과 가상 네트워크를 사용 하는 toocreate 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="35674-175">서식 파일을 사용 하는 경우 hello 매개 변수 값을 수동으로 제공 하는 중 hello 옵션이 또는 매개 변수 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="35674-176">아래 예제에서는 hello 위의 hello 템플릿으로 사용 되는 매개 변수 값 toobe 가능한 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35674-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

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


<span data-ttu-id="35674-177">서식 파일을 사용 하 여 hello 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="35674-178">선언적 스타일로 리소스 그룹에서 복잡한 인프라를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="35674-179">종속성 관리 하는 등 hello 리소스를 만드는 오케스트레이션 hello, 리소스 관리자에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35674-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="35674-180">hello 인프라 만들 수 있습니다 반복 가능한 방식으로 다양 한 지역에 걸쳐 및 영역 내에서 단순히 매개 변수를 변경 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="35674-181">hello 선언적 스타일 hello 서식 파일을 작성 하 고 hello 인프라 롤아웃하기 tooshorter 지연 시간을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35674-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="35674-182">샘플 템플릿은 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35674-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="35674-183">리소스 관리자 템플릿 언어 hello에 대 한 자세한 내용은 참조 하십시오. [Azure 리소스 관리자 템플릿 언어](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="35674-184">위의 hello 샘플 템플릿 hello 가상 네트워크 및 서브넷 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="35674-185">사용 가능한 다른 네트워크 리소스는 아래 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35674-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="35674-186">템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="35674-186">Using a template</span></span>
<span data-ttu-id="35674-187">서식 파일에서 서비스 tooAzure AzureCLI, PowerShell을 사용 하 여 하거나 클릭 toodeploy GitHub에서 수행 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="35674-188">GitHub에서 템플릿으로 toodeploy 서비스 단계를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="35674-189">GitHub에서 hello template3 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35674-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="35674-190">예를 들어, [두 서브넷을 사용하는 가상 네트워크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35674-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="35674-191">클릭 **tooAzure 배포**, 한 다음 로그인 toohello에 자격 증명으로 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="35674-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="35674-192">Hello 서식 파일을 확인 한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="35674-193">클릭 **매개 변수 편집** 같은 위치를 선택 하 고 *West US*, hello vnet 및 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="35674-194">필요한 경우 변경할 hello **ADDRESSPREFIX** 및 **SUBNETPREFIX** 매개 변수 및 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="35674-195">클릭 **리소스 그룹을 선택** tooadd hello vnet 및 서브넷을 원하는 hello 리소스 그룹을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="35674-196">**또는 새로 만들기**를 클릭하여 새 리소스 그룹을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35674-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="35674-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-197">Click **Create**.</span></span> <span data-ttu-id="35674-198">타일 표시 hello 확인 **프로 비전 템플릿 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="35674-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="35674-199">Hello 배포 작업이 완료 되 면 아래 화면 비슷한 tooone를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35674-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![샘플 템플릿 배포](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="35674-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35674-201">Next steps</span></span>
[<span data-ttu-id="35674-202">Azure 리소스 관리자 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35674-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="35674-203">Azure 네트워킹- 일반적으로 사용되는 템플릿</span><span class="sxs-lookup"><span data-stu-id="35674-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="35674-204">Azure Resource Manager 및 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="35674-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="35674-205">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="35674-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

