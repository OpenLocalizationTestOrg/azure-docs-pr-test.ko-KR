---
title: "타일 갤러리의 관련 리소스 및 연결된 리소스"
description: "Azure Preview 포털의 타일 갤러리에 표시되는 관련 리소스 및 연결된 리소스 대해 알아봅니다."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="c3268-103">타일 갤러리의 관련 리소스 및 연결된 리소스</span><span class="sxs-lookup"><span data-stu-id="c3268-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="c3268-104">타일 갤러리를 사용하면 특정 리소스에 대한 타일을 찾아 현재 블레이드에 끌어 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="c3268-105">타일 갤러리를 사용하여 리소스에 걸쳐 있는 관리 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="c3268-106">지정된 리소스의 경우 관련 리소스에 해당 리소스 그룹의 모든 리소스 및 해당 리소스로/부터 연결되는 모든 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="c3268-107">Resource Manager의 연결된 리소스</span><span class="sxs-lookup"><span data-stu-id="c3268-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="c3268-108">연결은 Resource Manager의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="c3268-109">동일한 리소스 그룹에 없다고 하더라도 리소스 간의 관계를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="c3268-110">연결은 리소스의 런타임, 청구, 역할 기반 액세스에 전혀 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="c3268-111">이는 단지 타일 갤러리 같은 도구가 풍부한 관리 경험을 제공할 수 있도록 관계를 나타내는 데 사용할 수 있는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="c3268-112">도구는 링크 API를 사용하여 링크를 검사하고 사용자 지정 관계 관리 환경도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="c3268-113">내 리소스를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="c3268-113">How do I link my resources?</span></span>
<span data-ttu-id="c3268-114">포털을 통하거나 Azure PowerShell 또는 Azure CLI를 통해 템플릿을 배포하여 리소스를 만들 때 일부 종속된 리소스에 대해 링크가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="c3268-115">[연결된 리소스 REST API](/rest/api/resources/resourcelinks)를 사용하여 프로그래밍 방식으로 리소스를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3268-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3268-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3268-116">Next steps</span></span>
* <span data-ttu-id="c3268-117">Resource Manager 템플릿 작성에 대한 소개를 보려면 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3268-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c3268-118">포털을 통해 리소스 그룹 작업에 대해 자세하게 파악하려면 [Azure Portal을 사용하여 Azure 리소스 관리](../azure-resource-manager/resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3268-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

