---
title: "Azure에서 aaaManaging 역할 클라우드 Visual Studio와 함께 서비스 | Microsoft Docs"
description: "Tooadd 및 제거 하는 Azure에서 역할에에서 Visual Studio를 사용 하 여 서비스 클라우드 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="e3bc9-103">Visual Studio에서 Azure Cloud Services의 역할 관리</span><span class="sxs-lookup"><span data-stu-id="e3bc9-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="e3bc9-104">Azure 클라우드 서비스를 만든 후에 새 역할 tooit 추가 하거나 기존 역할에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="e3bc9-105">또한 기존 프로젝트 가져오고 tooa 역할 변환 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="e3bc9-106">예를 들어, ASP.NET 웹 응용 프로그램을 가져오고 웹 역할로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="e3bc9-107">추가 역할 tooan Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e3bc9-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="e3bc9-108">단계를 수행 하는 hello Visual Studio에서 웹 또는 작업자 역할 tooan Azure 클라우드 서비스 프로젝트를 추가 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e3bc9-109">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e3bc9-110">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="e3bc9-111">마우스 오른쪽 단추로 클릭 hello **역할** 노드 toodisplay hello 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="e3bc9-112">Hello 상황에 맞는 메뉴에서 선택 **추가**, 다음 hello 현재 솔루션에서 기존 웹 역할 또는 작업자 역할을 선택 하거나 웹 또는 작업자 역할 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="e3bc9-113">또한 ASP.NET 웹 응용 프로그램 프로젝트와 같은 적절한 프로젝트를 선택하고 역할 프로젝트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![메뉴 옵션 tooadd 역할 tooan Azure 클라우드 서비스 프로젝트](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="e3bc9-115">Azure 클라우드 서비스에서 역할 제거</span><span class="sxs-lookup"><span data-stu-id="e3bc9-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="e3bc9-116">hello 다음 단계 과정을 안내 하면 Visual Studio에서 Azure 클라우드 서비스 프로젝트에서 웹 또는 작업자 역할을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e3bc9-117">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e3bc9-118">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="e3bc9-119">Hello 확장 **역할** 노드.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="e3bc9-120">마우스 오른쪽 단추로 클릭 hello 사용할 노드 tooremove, 마우스, hello 상황에 맞는 메뉴에서 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![메뉴 옵션 tooadd 역할 tooan Azure 클라우드 서비스](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="e3bc9-122">역할 tooan Azure 클라우드 서비스 프로젝트를 다시 추가 중</span><span class="sxs-lookup"><span data-stu-id="e3bc9-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="e3bc9-123">클라우드 서비스 프로젝트에서 역할 제거 하지만 나중에 다시 tooadd hello 역할 프로젝트 toohello hello 역할 선언과 기본 특성을, 끝점 및 진단 정보 등 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="e3bc9-124">추가 리소스 및 참조가 없는 toohello 추가 `ServiceDefinition.csdef` 파일 또는 toohello `ServiceConfiguration.cscfg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="e3bc9-125">Toomanually tooadd이 정보를 표시할 경우 해야 이러한 파일에 다시 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="e3bc9-126">예를 들어 웹 서비스 역할을 제거할 수 있습니다 및 나중 tooadd이이 역할에서 다시 솔루션으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="e3bc9-127">이 작업을 수행하는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-127">If you do this, an error occurs.</span></span> <span data-ttu-id="e3bc9-128">tooprevent이이 오류를 tooadd hello 있는 `<LocalResources>` XML hello로 다시 hello 뒤에 나오는 요소 `ServiceDefinition.csdef` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="e3bc9-129">Hello hello에 대 한 hello name 특성의 일부로 hello 프로젝트에 다시 추가한 웹 서비스 역할의 사용 하 여 hello 이름을  **<LocalStorage>**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="e3bc9-130">이 예제에서는 hello hello 웹 서비스 역할의 이름은 **WCFServiceWebRole1**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3bc9-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e3bc9-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3bc9-131">Next steps</span></span>
- [<span data-ttu-id="e3bc9-132">Visual Studio에서 Azure 클라우드 서비스에 대 한 hello 역할 구성</span><span class="sxs-lookup"><span data-stu-id="e3bc9-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
