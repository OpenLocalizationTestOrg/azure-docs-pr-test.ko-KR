---
title: "네트워크 리소스 공급자 개요 | Microsoft Docs"
description: "Azure 리소스 관리자의 새로운 네트워크 리소스 공급자에 대해 알아봅니다."
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
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="35ddb-103">네트워크 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="35ddb-103">Network Resource Provider</span></span>
<span data-ttu-id="35ddb-104">현대 비즈니스의 성공에 있어서 가장 필요한 것은 대규모 네트워크 인식 응용 프로그램을 신속하고 유연하고 안전하고 반복 가능한 방법으로 작성하여 관리할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="35ddb-105">Azure Resource Manager를 사용하면 이러한 응용 프로그램을 리소스 그룹에서 단일 리소스 컬렉션으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="35ddb-106">이러한 리소스는 Resource Manager의 다양한 리소스 공급자를 통해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="35ddb-107">Azure 리소스 관리자는 다양한 리소스 공급자를 사용하여 리소스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="35ddb-108">네트워크, 저장소 및 계산의 세 가지 주요 리소스 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="35ddb-109">이 문서에서는 다음을 비롯한 네트워크 리소스 공급자의 특징 및 이점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="35ddb-110">**메타데이터** - 태그를 사용하여 리소스에 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="35ddb-111">이러한 태그를 사용하여 리소스 그룹 및 구독 간의 리소스 사용률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="35ddb-112">**네트워크 제어 향상** - 네트워크 리소스가 느슨하게 결합되고 네트워크 리소스를 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="35ddb-113">즉, 네트워킹 리소스를 보다 유연하게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="35ddb-114">**더 빠른 구성** - 네트워크 리소스가 느슨하게 결합되므로 네트워크 리소스를 병렬로 만들어서 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="35ddb-115">따라서 구성 시간이 크게 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="35ddb-116">**역할 기반 액세스 제어** - RBAC는 기본 역할에 특정 보안 범위를 제공하고, 안전한 관리를 위해 사용자 지정 역할을 만들 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="35ddb-117">**쉬운 관리 및 배포** - 전체 응용 프로그램 스택을 리소스 그룹에서 단일 리소스 컬렉션으로 만들 수 있으므로 응용 프로그램을 쉽게 배포하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="35ddb-118">단순히 템플릿 JSON 페이로드를 제공하여 배포할 수 있으므로 배포 시간이 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="35ddb-119">**빠른 사용자 지정** - 선언적 스타일 템플릿을 사용하여 배포를 반복 가능하고 빠르게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="35ddb-120">**반복 가능한 사용자 지정** - 선언적 스타일 템플릿을 사용하여 배포를 반복 가능하고 빠르게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="35ddb-121">**관리 인터페이스** - 다음 인터페이스 중 하나를 사용하여 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="35ddb-122">REST 기반 API</span><span class="sxs-lookup"><span data-stu-id="35ddb-122">REST based API</span></span>
  * <span data-ttu-id="35ddb-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35ddb-123">PowerShell</span></span>
  * <span data-ttu-id="35ddb-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="35ddb-124">.NET SDK</span></span>
  * <span data-ttu-id="35ddb-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="35ddb-125">Node.JS SDK</span></span>
  * <span data-ttu-id="35ddb-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="35ddb-126">Java SDK</span></span>
  * <span data-ttu-id="35ddb-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35ddb-127">Azure CLI</span></span>
  * <span data-ttu-id="35ddb-128">Preview 포털</span><span class="sxs-lookup"><span data-stu-id="35ddb-128">Preview Portal</span></span>
  * <span data-ttu-id="35ddb-129">Resource Manager 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35ddb-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="35ddb-130">네트워크 리소스</span><span class="sxs-lookup"><span data-stu-id="35ddb-130">Network resources</span></span>
<span data-ttu-id="35ddb-131">이제 네트워크 리소스를 단일 컴퓨팅 리소스(가상 컴퓨터)를 통해 모두 함께 관리하지 않고 독립적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="35ddb-132">이렇게 하면 리소스 그룹에서 복잡한 대규모 인프라를 더 유연하고 신속하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="35ddb-133">다중 계층 응용 프로그램을 포함하는 샘플 배포의 개념 보기는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="35ddb-134">NIC, 공용 IP 주소 및 VM과 같은 표시되는 각 리소스를 독립적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![네트워크 리소스 모델](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="35ddb-136">모든 리소스에는 공통 속성 집합 및 개별 속성 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="35ddb-137">공용 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-137">The common properties are:</span></span>

| <span data-ttu-id="35ddb-138">속성</span><span class="sxs-lookup"><span data-stu-id="35ddb-138">Property</span></span> | <span data-ttu-id="35ddb-139">설명</span><span class="sxs-lookup"><span data-stu-id="35ddb-139">Description</span></span> | <span data-ttu-id="35ddb-140">샘플 값</span><span class="sxs-lookup"><span data-stu-id="35ddb-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35ddb-141">**name**</span><span class="sxs-lookup"><span data-stu-id="35ddb-141">**name**</span></span> |<span data-ttu-id="35ddb-142">고유한 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-142">Unique resource name.</span></span> <span data-ttu-id="35ddb-143">각 리소스 종류에 고유한 명명 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="35ddb-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="35ddb-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="35ddb-145">**위치**</span><span class="sxs-lookup"><span data-stu-id="35ddb-145">**location**</span></span> |<span data-ttu-id="35ddb-146">리소스가 있는 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="35ddb-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="35ddb-147">westus, eastus</span></span> |
| <span data-ttu-id="35ddb-148">**id**</span><span class="sxs-lookup"><span data-stu-id="35ddb-148">**id**</span></span> |<span data-ttu-id="35ddb-149">고유한 URI 기반 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-149">Unique URI based identification</span></span> |<span data-ttu-id="35ddb-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="35ddb-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="35ddb-151">아래 섹션에서 리소스의 개별 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-151">You can check the individual properties of resources in the sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="35ddb-152">관리 인터페이스</span><span class="sxs-lookup"><span data-stu-id="35ddb-152">Management interfaces</span></span>
<span data-ttu-id="35ddb-153">다양한 인터페이스를 사용하여 Azure 네트워킹 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="35ddb-154">이 문서에서는 이러한 인터페이스 중 REST API 및 템플릿 두 가지를 중점적으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="35ddb-155">REST API</span><span class="sxs-lookup"><span data-stu-id="35ddb-155">REST API</span></span>
<span data-ttu-id="35ddb-156">앞서 설명한 것처럼 REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure 포털, 템플릿을 비롯하여 다양한 인터페이스를 통해 네트워크 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="35ddb-157">Rest API는 HTTP 1.1 프로토콜 사양을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="35ddb-158">API의 일반 URI 구조는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="35ddb-159">중괄호로 묶인 매개 변수는 다음 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="35ddb-160">**subscription-id** - Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="35ddb-161">**resource-provider-namespace** - 사용 중인 공급자의 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="35ddb-162">네트워크 리소스 공급자에 대한 값은 *Microsoft.Network*입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="35ddb-163">**region-name** - Azure 지역 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="35ddb-164">다음은 REST API를 호출할 때 지원되는 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="35ddb-165">**PUT** - 지정된 유형의 리소스를 만들거나, 리소스 속성을 수정하거나, 리소스 간의 연결을 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="35ddb-166">**GET** - 프로비전된 리소스에 대한 정보를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="35ddb-167">**DELETE** - 기존 리소스를 삭제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="35ddb-168">요청과 응답이 모두 JSON 페이로드 형식을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="35ddb-169">자세한 내용은 [Azure 리소스 관리 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35ddb-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="35ddb-170">Resource Manager 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35ddb-170">Resource Manager template language</span></span>
<span data-ttu-id="35ddb-171">API 또는 SDK를 사용하여 명령을 통해 리소스를 관리할 뿐만 아니라, 선언형 프로그래밍 스타일을 사용하여 Resource Manager 템플릿 언어로 네트워크 리소스를 빌드 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="35ddb-172">템플릿의 샘플 표현은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="35ddb-173">템플릿은 주로 매개 변수를 통해 삽입된 인스턴스 값과 리소스에 대한 JSON 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="35ddb-174">아래 예를 사용하여 두 개의 서브넷을 포함하는 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="35ddb-175">템플릿을 사용할 때 매개 변수 값을 수동으로 제공하거나 매개 변수 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="35ddb-176">아래 예에서는 위의 템플릿과 함께 사용할 수 있는 매개 변수 값 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

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


<span data-ttu-id="35ddb-177">템플릿을 사용할 때의 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="35ddb-178">선언적 스타일로 리소스 그룹에서 복잡한 인프라를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="35ddb-179">종속성 관리를 비롯한 리소스 만들기 오케스트레이션은 Resource Manager에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="35ddb-180">간단히 매개 변수를 변경하여 단일 지역에 속하거나 여러 지역에 걸치는 인프라를 반복 가능한 방식으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="35ddb-181">선언적 스타일을 사용하면 템플릿을 작성하고 인프라를 롤아웃하는 사이의 지연 시간이 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="35ddb-182">샘플 템플릿은 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35ddb-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="35ddb-183">Resource Manager 템플릿 언어에 대한 자세한 내용은 [Azure Resource Manager 템플릿 언어](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35ddb-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="35ddb-184">위의 샘플 템플릿에서는 가상 네트워크와 서브넷 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="35ddb-185">사용 가능한 다른 네트워크 리소스는 아래 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35ddb-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="35ddb-186">템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="35ddb-186">Using a template</span></span>
<span data-ttu-id="35ddb-187">PowerShell, AzureCLI를 사용하거나 GitHub에서 배포를 클릭하여 템플릿에서 Azure에 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="35ddb-188">GitHub의 템플릿에서 서비스를 배포하려면 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="35ddb-189">GitHub에서 template3 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="35ddb-190">예를 들어, [두 서브넷을 사용하는 가상 네트워크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="35ddb-191">**Azure에 배포**를 클릭한 다음 자격 증명을 사용하여 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="35ddb-192">템플릿을 확인한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="35ddb-193">**매개 변수 편집** 을 클릭하고 *미국 서부*등과 같은 vnet 및 서브넷 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="35ddb-194">필요한 경우 **ADDRESSPREFIX** 및 **SUBNETPREFIX** 매개 변수를 변경하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="35ddb-195">**리소스 그룹 선택** 을 클릭하고 vnet과 서브넷에 추가하려는 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="35ddb-196">**또는 새로 만들기**를 클릭하여 새 리소스 그룹을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="35ddb-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-197">Click **Create**.</span></span> <span data-ttu-id="35ddb-198">**템플릿 배포 프로비저닝**이라고 표시된 타일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="35ddb-199">배포가 완료되면 아래와 비슷한 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35ddb-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![샘플 템플릿 배포](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="35ddb-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35ddb-201">Next steps</span></span>
[<span data-ttu-id="35ddb-202">Azure 리소스 관리자 템플릿 언어</span><span class="sxs-lookup"><span data-stu-id="35ddb-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="35ddb-203">Azure 네트워킹- 일반적으로 사용되는 템플릿</span><span class="sxs-lookup"><span data-stu-id="35ddb-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="35ddb-204">Azure Resource Manager 및 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="35ddb-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="35ddb-205">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="35ddb-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

