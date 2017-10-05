---
title: "Azure Resource Manager 템플릿 내보내기 | Microsoft Docs"
description: "Azure Resource Manager를 사용하여 기존 리소스 그룹에서 템플릿을 내보냅니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 1801ef47e5b182e0bcd5b23970a2999633b4a852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="597e3-103">기존 리소스에서 Azure Resource Manager 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="597e3-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="597e3-104">이 문서에서는 구독에서 기존 리소스의 Resource Manager 템플릿을 내보내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="597e3-105">생성된 해당 템플릿을 사용하여 템플릿 구문을 깊이 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-105">You can use that generated template to gain a better understanding of template syntax.</span></span>

<span data-ttu-id="597e3-106">두 가지 방법으로 템플릿을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-106">There are two ways to export a template:</span></span>

* <span data-ttu-id="597e3-107">**배포에 사용된 실제 템플릿**을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-107">You can export the **actual template used for deployment**.</span></span> <span data-ttu-id="597e3-108">내보낸 템플릿은 원본 템플릿에 나타난 대로 모든 매개 변수 및 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="597e3-109">이 방법은 포털을 통해 리소스를 배포하고 해당 리소스를 만드는 템플릿을 확인하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span></span> <span data-ttu-id="597e3-110">이 템플릿은 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-110">This template is readily usable.</span></span> 
* <span data-ttu-id="597e3-111">**리소스 그룹의 현재 상태를 나타내는 생성된 템플릿을 내보낼** 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-111">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="597e3-112">내보낸 템플릿은 배포에 사용된 템플릿에 기초하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-112">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="597e3-113">대신 리소스 그룹의 스냅숏인 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-113">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="597e3-114">내보낸 템플릿에는 하드 코드된 값이 많으며 일반적으로 정의된 경우와 같이 매개 변수가 많이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="597e3-115">이 방법은 배포 후에 리소스 그룹을 수정한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-115">This approach is useful when you have modified the resource group after deployment.</span></span> <span data-ttu-id="597e3-116">일반적으로 이 템플릿을 사용하기 전에 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="597e3-117">이 항목에서는 포털을 통한 방법을 모두 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-117">This topic shows both approaches through the portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="597e3-118">리소스 배포</span><span class="sxs-lookup"><span data-stu-id="597e3-118">Deploy resources</span></span>
<span data-ttu-id="597e3-119">템플릿으로 내보내는 데 사용할 수 있는 리소스를 Azure에 배포하기 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span></span> <span data-ttu-id="597e3-120">템플릿을 내보내려는 구독에 리소스 그룹이 이미 있는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span></span> <span data-ttu-id="597e3-121">이 문서의 나머지 부분에서는 이 섹션에 표시된 웹앱 및 SQL Database 솔루션을 배포했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-121">The remainder of this article assumes you have deployed the web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="597e3-122">다른 솔루션을 사용하는 경우 환경은 약간 다를 수 있지만 템플릿을 내보내는 단계는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span></span> 

1. <span data-ttu-id="597e3-123">[Azure Portal](https://portal.azure.com)에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-123">In the [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![새로 만들기 선택](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="597e3-125">**웹앱 + SQL**을 검색하고 사용 가능한 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-125">Search for **web app + SQL** and select it from the available options.</span></span>
   
      ![웹앱 및 SQL 검색](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="597e3-127">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-127">Select **Create**.</span></span>

      ![만들기 선택](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="597e3-129">웹앱 및 SQL Database에 필수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-129">Provide the required values for the web app and SQL database.</span></span> <span data-ttu-id="597e3-130">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-130">Select **Create**.</span></span>

      ![웹 및 SQL 값 제공](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="597e3-132">배포는 몇 분 정도가 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-132">The deployment may take a minute.</span></span> <span data-ttu-id="597e3-133">배포가 완료되면 구독에는 솔루션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-133">After the deployment finishes, your subscription contains the solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="597e3-134">배포 기록의 템플릿 보기</span><span class="sxs-lookup"><span data-stu-id="597e3-134">View template from deployment history</span></span>
1. <span data-ttu-id="597e3-135">새 리소스 그룹의 리소스 그룹 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-135">Go to the resource group blade for your new resource group.</span></span> <span data-ttu-id="597e3-136">블레이드가 최종 배포 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-136">Notice that the blade shows the result of the last deployment.</span></span> <span data-ttu-id="597e3-137">이 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-137">Select this link.</span></span>
   
      ![리소스 그룹 블레이드](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="597e3-139">그룹의 배포 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-139">You see a history of deployments for the group.</span></span> <span data-ttu-id="597e3-140">사용자의 경우에 블레이드에 하나의 배포만 나열되어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-140">In your case, the blade probably lists only one deployment.</span></span> <span data-ttu-id="597e3-141">이 배포를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-141">Select this deployment.</span></span>
   
     ![마지막 배포](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="597e3-143">블레이드에 배포 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-143">The blade displays a summary of the deployment.</span></span> <span data-ttu-id="597e3-144">요약에는 배포 상태와 해당 작업, 매개 변수에 입력한 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="597e3-145">배포에 사용된 템플릿을 보려면 **템플릿 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-145">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![배포 요약 보기](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="597e3-147">Resource Manager는 다음 7개의 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-147">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="597e3-148">**템플릿** - 솔루션의 인프라를 정의하는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-148">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="597e3-149">포털을 통해 저장소 계정을 만들 때 Resource Manager는 템플릿을 사용하여 배포하고 나중에 참조할 수 있도록 해당 템플릿을 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="597e3-150">**매개 변수** - 배포하는 동안 값을 전달하는 데 사용할 수 있는 매개 변수 파일.</span><span class="sxs-lookup"><span data-stu-id="597e3-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="597e3-151">첫 번째 배포 중에 제공되는 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-151">It contains the values that you provided during the first deployment.</span></span> <span data-ttu-id="597e3-152">템플릿을 다시 배포할 때 이러한 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-152">You can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="597e3-153">**CLI** - 템플릿 배포에 사용할 수 있는 Azure CLI(명령줄 인터페이스) 스크립트 파일.</span><span class="sxs-lookup"><span data-stu-id="597e3-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   3. <span data-ttu-id="597e3-154">**CLI 2.0** - 템플릿 배포에 사용할 수 있는 Azure CLI(명령줄 인터페이스) 스크립트 파일.</span><span class="sxs-lookup"><span data-stu-id="597e3-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="597e3-155">**PowerShell** - 템플릿 배포에 사용할 수 있는 Azure PowerShell 스크립트 파일.</span><span class="sxs-lookup"><span data-stu-id="597e3-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="597e3-156">**.NET** - 템플릿 배포에 사용할 수 있는 .NET 클래스.</span><span class="sxs-lookup"><span data-stu-id="597e3-156">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="597e3-157">**Ruby** - 템플릿 배포에 사용할 수 있는 Ruby 클래스.</span><span class="sxs-lookup"><span data-stu-id="597e3-157">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="597e3-158">이러한 파일은 전체 블레이드에서 링크를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-158">The files are available through links across the blade.</span></span> <span data-ttu-id="597e3-159">기본적으로 블레이드가 템플릿을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-159">By default, the blade displays the template.</span></span>
      
       ![템플릿 보기](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="597e3-161">이 템플릿은 웹앱 및 SQL Database를 만드는 데 사용되는 실제 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-161">This template is the actual template used to create your web app and SQL database.</span></span> <span data-ttu-id="597e3-162">배포 중에 다른 값을 제공할 수 있는 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-162">Notice it contains parameters that enable you to provide different values during deployment.</span></span> <span data-ttu-id="597e3-163">템플릿 구조에 대해 자세히 알아보려면 [Azure Resource Manager 템플릿 작성하기](resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597e3-163">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="597e3-164">리소스 그룹에서 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="597e3-164">Export the template from resource group</span></span>
<span data-ttu-id="597e3-165">수동으로 리소스를 변경했거나 여러 배포에서 리소스를 추가한 경우 배포 기록에서 템플릿을 검색하면 리소스 그룹의 현재 상태를 반영하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history does not reflect the current state of the resource group.</span></span> <span data-ttu-id="597e3-166">이 섹션에서는 리소스 그룹의 현재 상태를 반영하는 템플릿을 내보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-166">This section shows you how to export a template that reflects the current state of the resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="597e3-167">200개 이상의 리소스가 있는 리소스 그룹에 대한 템플릿을 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="597e3-168">리소스 그룹에 대한 템플릿을 보려면 **자동화 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-168">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![리소스 그룹 내보내기](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="597e3-170">Resource Manager는 리소스 그룹에 있는 리소스를 평가하고 해당 리소스에 대한 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span></span> <span data-ttu-id="597e3-171">모든 리소스 종류가 내보내기 템플릿 함수를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-171">Not all resource types support the export template function.</span></span> <span data-ttu-id="597e3-172">내보내기에 문제가 있다는 것을 나타내는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-172">You may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="597e3-173">[내보내기 문제 수정](#fix-export-issues) 섹션에서 이러한 문제를 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="597e3-174">솔루션을 다시 배포하는 데 사용할 수 있는 6개의 파일을 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-174">You again see the six files that you can use to redeploy the solution.</span></span> <span data-ttu-id="597e3-175">그러나 이번에 이 템플릿은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-175">However, this time the template is a little different.</span></span> <span data-ttu-id="597e3-176">생성된 템플릿에 이전 섹션에서 템플릿보다 더 적은 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-176">Notice that the generated template contains fewer parameters than the template in previous section.</span></span> <span data-ttu-id="597e3-177">또한 대부분의 값(예: 위치 및 SKU 값)은 매개 변수 값을 허용하지 않고 이 템플릿에서 하드 코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="597e3-178">이 템플릿을 다시 사용하기 전에 매개 변수를 효과적으로 사용할 수 있도록 템플릿을 편집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span></span> 
   
3. <span data-ttu-id="597e3-179">이 템플릿을 사용하여 계속해서 작업하기 위한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-179">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="597e3-180">템플릿을 다운로드하고 JSON 편집기를 사용하여 로컬에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-180">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="597e3-181">또는 템플릿을 라이브러리에 저장하고 포털을 통해 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-181">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="597e3-182">[VS Code](https://code.visualstudio.com/) 또는 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)와 같은 JSON 편집기 사용에 익숙한 경우 템플릿을 로컬로 다운로드하고 해당 편집기를 사용하는 것을 선호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="597e3-183">로컬로 작업하려면 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-183">To work locally, select **Download**.</span></span>
   
      ![템플릿 다운로드](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="597e3-185">JSON 편집기를 설정하지 않은 경우 포털을 통해 템플릿을 편집하는 것을 선호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-185">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="597e3-186">이 항목의 나머지 부분에서는 템플릿을 포털의 라이브러리에 저장했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-186">The remainder of this topic assumes you have saved the template to your library in the portal.</span></span> <span data-ttu-id="597e3-187">그러나 JSON 편집기로 로컬에서 작업하든지 포털을 통해 작업하든지 템플릿에 동일한 구문 변경 내용을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span> <span data-ttu-id="597e3-188">포털을 통해 작업하려면 **라이브러리에 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-188">To work through the portal, select **Add to library**.</span></span>
   
      ![라이브러리에 추가](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="597e3-190">템플릿을 라이브러리에 추가할 때 템플릿에 이름 및 설명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-190">When adding a template to the library, give the template a name and description.</span></span> <span data-ttu-id="597e3-191">그런 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-191">Then, select **Save**.</span></span>
   
     ![템플릿 값 설정](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="597e3-193">라이브러리에 저장된 템플릿을 보려면 **더 많은 서비스**를 선택하고 결과를 필터링할 **템플릿**을 입력하고 **템플릿**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![템플릿 찾기](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="597e3-195">저장한 이름으로 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-195">Select the template with the name you saved.</span></span>
   
      ![템플릿 선택](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="597e3-197">템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="597e3-197">Customize the template</span></span>
<span data-ttu-id="597e3-198">모든 배포에 동일한 웹앱 및 SQL Database를 만들려는 경우 내보낸 템플릿이 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span></span> <span data-ttu-id="597e3-199">하지만 Resource Manager는 훨씬 더 유연하게 템플릿을 배포할 수 있도록 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="597e3-200">이 문서에서는 데이터베이스 관리자 이름 및 암호에 매개 변수를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-200">This article shows you how to add parameters for the database administrator name and password.</span></span> <span data-ttu-id="597e3-201">템플릿에서 다른 값에 더 많은 유연성을 추가하려면 이 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-201">You can use this same approach to add more flexibility for other values in the template.</span></span>

1. <span data-ttu-id="597e3-202">템플릿을 사용자 지정하려면 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-202">To customize the template, select **Edit**.</span></span>
   
     ![템플릿 표시](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="597e3-204">템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-204">Select the template.</span></span>
   
     ![템플릿 편집](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="597e3-206">배포 중에 지정하려는 값을 전달할 수 있도록 하려면 템플릿에서 **매개 변수** 섹션에 두 개의 다음 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-206">To be able to pass the values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="597e3-207">새 매개 변수를 사용하려면 **리소스** 섹션에서 SQL Server 정의를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span></span> <span data-ttu-id="597e3-208">**administratorLogin** 및 **administratorLoginPassword**는 이제 매개 변수 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="597e3-209">템플릿 편집을 마친 경우 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-209">Select **OK** when you are done editing the template.</span></span>
7. <span data-ttu-id="597e3-210">**저장**를 선택하여 변경 내용을 템플릿에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-210">Select **Save** to save the changes to the template.</span></span>
   
     ![템플릿 저장](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="597e3-212">업데이트된 템플릿을 다시 배포하려면 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-212">To redeploy the updated template, select **Deploy**.</span></span>
   
     ![템플릿 배포](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="597e3-214">매개 변수 값을 제공하고 리소스를 배포하려는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-214">Provide parameter values, and select a resource group to deploy the resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="597e3-215">내보내기 문제 수정</span><span class="sxs-lookup"><span data-stu-id="597e3-215">Fix export issues</span></span>
<span data-ttu-id="597e3-216">모든 리소스 종류가 내보내기 템플릿 함수를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-216">Not all resource types support the export template function.</span></span> <span data-ttu-id="597e3-217">이 문제를 해결하려면 누락된 리소스를 템플릿에 다시 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-217">To resolve this issue, manually add the missing resources back into your template.</span></span> <span data-ttu-id="597e3-218">오류 메시지에는 내보낼 수 없는 리소스 종류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-218">The error message includes the resource types that cannot be exported.</span></span> <span data-ttu-id="597e3-219">[템플릿 참조](/azure/templates/)에서 리소스 종류를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="597e3-220">예를 들어 가상 네트워크 게이트웨이를 수동으로 추가하려면 [Microsoft.Network/virtualNetworkGateways 템플릿 참조](/azure/templates/microsoft.network/virtualnetworkgateways)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597e3-220">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="597e3-221">배포 기록이 아닌 리소스 그룹에서 내보낸 경우 내보내기 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="597e3-222">마지막 배포가 리소스 그룹의 현재 상태를 정확하게 나타내는 경우 리소스 그룹이 아닌 배포 기록에서 템플릿을 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-222">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="597e3-223">단일 템플릿에서 정의되지 않은 리소스 그룹을 변경한 경우에만 리소스 그룹에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-223">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="597e3-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="597e3-224">Next steps</span></span>
<span data-ttu-id="597e3-225">포털에서 만든 리소스에서 템플릿을 내보내는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-225">You have learned how to export a template from resources that you created in the portal.</span></span>

* <span data-ttu-id="597e3-226">[PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) 또는 [REST API](resource-group-template-deploy-rest.md)를 통해 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="597e3-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="597e3-227">PowerShell을 통해 템플릿을 내보내는 방법을 알아보려면 [Azure Resource Manager에서 Azure PowerShell 사용](powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597e3-227">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="597e3-228">Azure CLI를 통해 템플릿을 내보내는 방법은 [Azure Resource Manager에서 Mac, Linux 및 Windows용 Azure CLI 사용](xplat-cli-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="597e3-228">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

