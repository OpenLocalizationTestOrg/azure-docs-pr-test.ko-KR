---
title: "Visual Studio에서 Azure Cloud Services의 역할 관리 | Microsoft Docs"
description: "Visual Studio에서 Azure Cloud Services의 역할을 추가 및 제거하는 방법을 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="36660-103">Visual Studio에서 Azure Cloud Services의 역할 관리</span><span class="sxs-lookup"><span data-stu-id="36660-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="36660-104">Azure 클라우드 서비스를 만든 후 새 역할을 추가하거나 기존 역할에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="36660-105">또한 기존 프로젝트를 가져오고 역할로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="36660-106">예를 들어, ASP.NET 웹 응용 프로그램을 가져오고 웹 역할로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="36660-107">Azure 클라우드 서비스에 역할 추가</span><span class="sxs-lookup"><span data-stu-id="36660-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="36660-108">다음 단계에서는 Visual Studio에서 Azure 클라우드 서비스 프로젝트에 웹 또는 작업자 역할을 추가하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="36660-109">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36660-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="36660-110">**솔루션 탐색기**에서 프로젝트 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="36660-111">**역할** 노드를 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="36660-112">상황에 맞는 메뉴에서 **추가**를 선택한 다음 현재 솔루션에서 기존 웹 역할 또는 작업자 역할을 선택하거나 웹 또는 작업자 역할 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="36660-113">또한 ASP.NET 웹 응용 프로그램 프로젝트와 같은 적절한 프로젝트를 선택하고 역할 프로젝트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Azure 클라우드 서비스 프로젝트에 역할을 추가하는 메뉴 옵션](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="36660-115">Azure 클라우드 서비스에서 역할 제거</span><span class="sxs-lookup"><span data-stu-id="36660-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="36660-116">다음 단계에서는 Visual Studio에서 Azure 클라우드 서비스 프로젝트에 웹 또는 작업자 역할을 제거하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="36660-117">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36660-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="36660-118">**솔루션 탐색기**에서 프로젝트 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="36660-119">**역할** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="36660-120">제거할 노드를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![Azure 클라우드 서비스에 역할을 추가하는 메뉴 옵션](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="36660-122">Azure 클라우드 서비스 프로젝트에 역할 다시 추가</span><span class="sxs-lookup"><span data-stu-id="36660-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="36660-123">클라우드 서비스 프로젝트에서 역할을 제거하지만 나중에 프로젝트에 역할을 추가하려면 기본 끝점 및 진단 정보 등의 역할 선언과 기본 특성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="36660-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="36660-124">`ServiceDefinition.csdef` 파일 또는 `ServiceConfiguration.cscfg` 파일에 추가되는 리소스 또는 참조는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="36660-125">이 정보를 추가하려면 이러한 파일에 수동으로 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="36660-126">예를 들어, 웹 서비스 역할을 제거하고 이 솔루션에 다시 이 역할을 추가하도록 나중에 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36660-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="36660-127">이 작업을 수행하는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-127">If you do this, an error occurs.</span></span> <span data-ttu-id="36660-128">이 오류를 방지하려면 다음 XML에 표시된 `<LocalResources>` 요소를 `ServiceDefinition.csdef` 파일에 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="36660-129">프로젝트에 다시 추가한 웹 서비스 역할의 이름을 **<LocalStorage>** 요소에 대한 이름 특성의 일부로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36660-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="36660-130">이 예제에서 웹 서비스 역할의 이름은 **WCFServiceWebRole1**입니다.</span><span class="sxs-lookup"><span data-stu-id="36660-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="36660-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36660-131">Next steps</span></span>
- [<span data-ttu-id="36660-132">Visual Studio에서 Azure 클라우드 서비스에 대한 역할 구성</span><span class="sxs-lookup"><span data-stu-id="36660-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
