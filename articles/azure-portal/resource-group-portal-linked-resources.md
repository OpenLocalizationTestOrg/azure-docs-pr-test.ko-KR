---
title: "aaaRelated 및 hello에 연결 된 리소스 타일 갤러리"
description: "Hello Azure preview 포털의 hello 타일 갤러리에 표시 되는 관련 및 연결 된 리소스에 알아봅니다."
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
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="f6f52-103">Hello 타일 갤러리에 관련 및 연결 된 리소스</span><span class="sxs-lookup"><span data-stu-id="f6f52-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="f6f52-104">hello 타일 갤러리 toofind 타일 특정 리소스에 대 한 있으며 현재 사용자 블레이드로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="f6f52-105">Hello 타일 갤러리를 사용 하 여 리소스를 포괄 하는 관리 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="f6f52-106">지정 된 모든 리소스에 대 한 hello 관련 리소스는 리소스 그룹, 및 tooor hello 리소스에서 연결 된 모든 리소스의 모든 hello 리소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="f6f52-107">Resource Manager의 연결된 리소스</span><span class="sxs-lookup"><span data-stu-id="f6f52-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="f6f52-108">연결의 hello 리소스 관리자의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="f6f52-109">하면 리소스 간의 관계 toodeclare은 별도로 hello에 동일한 경우에 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="f6f52-110">리소스, 대금 청구에 영향을 주지 및 역할 기반 액세스에 영향을 주지 hello 런타임 연결에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="f6f52-111">이 장치가 단순히 hello 타일 갤러리 다양 한 관리를 제공할 수와 같은 도구를 경험할 수 있도록 toorepresent 관계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="f6f52-112">도구는 hello 링크 API를 사용 하 여 hello 링크를 검사 하 고 사용자 지정 관계 관리도 환경을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="f6f52-113">내 리소스를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6f52-113">How do I link my resources?</span></span>
<span data-ttu-id="f6f52-114">Hello 포털을 통해 또는 Azure PowerShell 또는 Azure CLI를 통해 서식 파일을 배포 하 여 리소스를 만들 때 몇 가지 종속 된 리소스에 대 한 링크가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="f6f52-115">Hello를 사용 하 여 리소스를 연결 또한 프로그래밍 방식으로 [연결 된 리소스 REST API](/rest/api/resources/resourcelinks)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f52-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6f52-116">Next steps</span></span>
* <span data-ttu-id="f6f52-117">소개 toowriting 리소스 관리자 템플릿을 해야 할 경우 참조 [템플릿을 작성](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f6f52-118">toounderstand hello 포털을 통해 리소스 그룹 작업에 대 한 참조 [사용 하 여 Azure 리소스를 Azure 포털 toomanage hello](../azure-resource-manager/resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f52-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

