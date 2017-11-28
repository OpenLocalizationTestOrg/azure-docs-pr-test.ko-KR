---
title: "Azure 리소스 관리자 템플릿 aaaExport | Microsoft Docs"
description: "Azure 리소스 관리 tooexport 기존 리소스 그룹에서 서식 파일을 사용 합니다."
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
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="8a97c-103">기존 리소스에서 Azure Resource Manager 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="8a97c-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="8a97c-104">이 문서에서는 설명 어떻게 tooexport 구독에 기존 리소스에서 리소스 관리자 템플릿 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="8a97c-105">해당 생성 된 템플릿 toogain 템플릿 구문에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="8a97c-106">서식 파일은 두 가지 방법으로 tooexport:</span><span class="sxs-lookup"><span data-stu-id="8a97c-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="8a97c-107">Hello를 내보낼 수 **배포에 사용 되는 실제 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="8a97c-108">hello 내보낸된 템플릿에 hello 원본 서식 파일에 표시 된 그대로 hello 매개 변수 및 변수를 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="8a97c-109">이 방법은 hello 포털을 통해 리소스를 배포할 때 유용 하 고 toosee hello 템플릿 toocreate 이러한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="8a97c-110">이 템플릿은 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-110">This template is readily usable.</span></span> 
* <span data-ttu-id="8a97c-111">내보낼 수는 **hello hello 리소스 그룹의 현재 상태를 나타내는 템플릿을 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="8a97c-112">hello에서 내보낸된 템플릿 배포에 사용 된 파일 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="8a97c-113">대신, 템플릿에 hello 리소스 그룹의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="8a97c-114">hello에서 내보낸된 템플릿에 하드 코드 된 값이 많은 및 일반적으로 정의할 때와 하지 못할 수의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="8a97c-115">이 방법은 배포 후 hello 리소스 그룹을 수정한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="8a97c-116">일반적으로 이 템플릿을 사용하기 전에 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="8a97c-117">이 항목에서는 hello 포털을 통해 두 가지 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="8a97c-118">리소스 배포</span><span class="sxs-lookup"><span data-stu-id="8a97c-118">Deploy resources</span></span>
<span data-ttu-id="8a97c-119">서식 파일로 내보내는 데 사용할 수 있는 리소스 tooAzure를 배포 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="8a97c-120">Tooexport tooa 템플릿을 하려는 구독에 리소스 그룹이 이미 있는 경우에이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="8a97c-121">이 문서의 나머지 부분에서는 hello hello web app 및이 섹션에 표시 된 SQL 데이터베이스 솔루션을 배포한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="8a97c-122">다른 솔루션을 사용 하 여 환경을 약간 다를 수 있습니다 있지만 tooexport 서식 파일은 hello 단계 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="8a97c-123">Hello에 [Azure 포털](https://portal.azure.com)선택, **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![새로 만들기 선택](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="8a97c-125">검색할 **웹 응용 프로그램 + SQL** hello 사용 가능한 옵션에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![웹앱 및 SQL 검색](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="8a97c-127">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-127">Select **Create**.</span></span>

      ![만들기 선택](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="8a97c-129">Hello web app 및 SQL 데이터베이스에 대 한 hello 필요한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="8a97c-130">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-130">Select **Create**.</span></span>

      ![웹 및 SQL 값 제공](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="8a97c-132">hello 배포 1 분을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-132">hello deployment may take a minute.</span></span> <span data-ttu-id="8a97c-133">Hello 배포 완료 되 면 hello 솔루션 구독에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="8a97c-134">배포 기록의 템플릿 보기</span><span class="sxs-lookup"><span data-stu-id="8a97c-134">View template from deployment history</span></span>
1. <span data-ttu-id="8a97c-135">새 리소스 그룹에 대 한 toohello 리소스 그룹 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="8a97c-136">해당 hello 블레이드 hello hello 마지막 배포 결과 보여 줍니다. 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="8a97c-137">이 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-137">Select this link.</span></span>
   
      ![리소스 그룹 블레이드](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="8a97c-139">Hello 그룹에 대 한 배포의 기록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="8a97c-140">여기에서 hello 블레이드 아마도 하나의 배포를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="8a97c-141">이 배포를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-141">Select this deployment.</span></span>
   
     ![마지막 배포](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="8a97c-143">hello 블레이드 hello 배포의 요약 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="8a97c-144">hello 요약 hello 배포의 hello 상태 작업 및 매개 변수에 대해 제공 하는 hello 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="8a97c-145">hello 배포에 사용한 toosee hello 템플릿을 **템플릿 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![배포 요약 보기](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="8a97c-147">리소스 관리자를 다음 7 개의 파일이 hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="8a97c-148">**템플릿** -솔루션에 대 한 hello 인프라를 정의 하는 hello 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="8a97c-149">리소스 관리자 템플릿 toodeploy 사용 hello 포털을 통해 hello 저장소 계정을 만들 때 해당 하 고 나중에 참조할 수에 대 한 해당 서식 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="8a97c-150">**매개 변수** -배포 중 toopass을 사용할 값의 수 있는 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="8a97c-151">Hello 첫 번째 배포 중에 제공 하는 hello 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="8a97c-152">Hello 서식 파일을 다시 배포할 때 다음이 값 중 하나를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="8a97c-153">**CLI** -Azure command 명령줄 인터페이스 (CLI) 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="8a97c-154">**CLI 2.0** -Azure command 명령줄 인터페이스 (CLI) 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="8a97c-155">**PowerShell** -는 Azure PowerShell 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="8a97c-156">**.NET** -A.NET 클래스 toodeploy hello 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="8a97c-157">**Ruby** -A Ruby 클래스 toodeploy hello 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="8a97c-158">hello 파일 hello 블레이드에서 링크를 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="8a97c-159">기본적으로 hello 블레이드 hello 템플릿을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-159">By default, hello blade displays hello template.</span></span>
      
       ![템플릿 보기](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="8a97c-161">이 템플릿은 hello 실제 템플릿을 toocreate 사용 하는 경우 웹 앱 및 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="8a97c-162">배포 하는 동안 tooprovide 서로 다른 값을 사용 하는 매개 변수를 포함 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="8a97c-163">참조는 템플릿의 hello 구조에 대해 자세히 toolearn [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="8a97c-164">리소스 그룹에서 hello 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="8a97c-164">Export hello template from resource group</span></span>
<span data-ttu-id="8a97c-165">리소스 변경 수동으로 했거나 여러 배포에서 리소스를 추가 하는 경우 hello 배포 기록에서 서식 파일을 검색 반영 하지 않습니다 hello hello 리소스 그룹의 현재 상태.</span><span class="sxs-lookup"><span data-stu-id="8a97c-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="8a97c-166">이 섹션에서는 tooexport 반영 하는 템플릿을 hello 리소스 그룹의 현재 상태를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="8a97c-167">200개 이상의 리소스가 있는 리소스 그룹에 대한 템플릿을 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="8a97c-168">리소스 그룹 선택에 대 한 tooview hello 템플릿을 **자동화 스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![리소스 그룹 내보내기](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="8a97c-170">Hello 리소스 그룹의 hello 리소스를 평가 하 고 해당 리소스에 대 한 서식 파일을 생성 하는 리소스 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="8a97c-171">일부 리소스 형식은 hello 내보내기 템플릿 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="8a97c-172">Hello 내보내기에 문제가 있다는 것을 나타내는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="8a97c-173">어떻게 toohandle 된 문제에 대해 알아봅니다 hello [내보내기 관련 문제를 해결할](#fix-export-issues) 섹션.</span><span class="sxs-lookup"><span data-stu-id="8a97c-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="8a97c-174">다시 tooredeploy hello 솔루션을 사용할 수 있는 hello 6 개의 파일을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8a97c-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="8a97c-175">그러나이 시간 hello 서식 파일은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="8a97c-176">생성 된 템플릿 hello 포함 매개 변수가 이전 섹션에서 hello 서식 파일 보다 적습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="8a97c-177">또한 많은 hello 값 (예: 위치 및 SKU 값) 매개 변수 값을 허용 하는 대신이 서식 파일에 하드 코드 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="8a97c-178">이 서식 파일을 다시 사용 하기 전에 tooedit hello 템플릿 toomake를 효과적으로 사용할 매개 변수를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="8a97c-179">두 가지 toowork이이 템플릿 사용 하 여 계속 하기 위한 옵션이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="8a97c-180">Hello 템플릿을 다운로드 고 로컬로 JSON 편집기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="8a97c-181">또는 hello 템플릿 tooyour 라이브러리를 저장 하 고 hello 포털을 통해에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="8a97c-182">에 익숙한 경우와 같은 JSON 편집기를 사용 하 여 [VS Code](https://code.visualstudio.com/) 또는 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), hello 서식 파일을 로컬로 다운로드 하 고 해당 편집기를 사용 하 여 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="8a97c-183">toowork 로컬로 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-183">toowork locally, select **Download**.</span></span>
   
      ![템플릿 다운로드](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="8a97c-185">JSON 편집기를 설정 하지, hello 포털을 통해 hello 템플릿을 편집 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="8a97c-186">이 항목의 나머지 부분에서는 hello hello 템플릿 tooyour 라이브러리 hello 포털에 저장 한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="8a97c-187">그러나 수행한 동일한 hello 구문 JSON 편집기로 또는 hello 포털을 통해 로컬로 작동 하는지 toohello 서식 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="8a97c-188">hello 포털을 통해 toowork 선택 **toolibrary 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![toolibrary 추가](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="8a97c-190">템플릿 toohello 라이브러리에 추가할 때는 이름 및 설명을 hello 서식 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="8a97c-191">그런 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-191">Then, select **Save**.</span></span>
   
     ![템플릿 값 설정](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="8a97c-193">tooview 라이브러리에 저장 된 템플릿을 선택 **더 많은 서비스**, 형식 **템플릿** toofilter 결과 **템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![템플릿 찾기](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="8a97c-195">저장 하는 hello 이름의 hello 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-195">Select hello template with hello name you saved.</span></span>
   
      ![템플릿 선택](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="8a97c-197">Hello 템플릿을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8a97c-197">Customize hello template</span></span>
<span data-ttu-id="8a97c-198">내보낸 hello 템플릿 작동 동일한 웹 응용 프로그램 및 모든 배포에 대 한 SQL 데이터베이스 toocreate hello를 원하는 경우 세밀 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="8a97c-199">하지만 Resource Manager는 훨씬 더 유연하게 템플릿을 배포할 수 있도록 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="8a97c-200">이 문서에서는 tooadd 매개 변수 hello에 대 한 데이터베이스 관리자 이름 및 암호를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="8a97c-201">Hello 서식 파일의 다른 값에 대 한이 동일한 접근 방식을 tooadd를 보다 융통성 있게를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="8a97c-202">선택 toocustomize hello 템플릿을 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![템플릿 표시](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="8a97c-204">Hello 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-204">Select hello template.</span></span>
   
     ![템플릿 편집](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="8a97c-206">toobe 수 toopass hello 값 toospecify 배포 하는 동안 선택 추가 다음 두 개의 매개 변수 toohello hello **매개 변수** hello 서식 파일의 섹션:</span><span class="sxs-lookup"><span data-stu-id="8a97c-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="8a97c-207">toouse hello 새 매개 변수를 대체 hello에 SQL server 정의 hello **리소스** 섹션.</span><span class="sxs-lookup"><span data-stu-id="8a97c-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="8a97c-208">**administratorLogin** 및 **administratorLoginPassword**는 이제 매개 변수 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

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

6. <span data-ttu-id="8a97c-209">선택 **확인** 완료 한 경우 hello 서식 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="8a97c-210">선택 **저장** toosave hello 변경 toohello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="8a97c-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![템플릿 저장](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="8a97c-212">선택 tooredeploy 업데이트 hello 템플릿을 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![템플릿 배포](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="8a97c-214">매개 변수 값을 제공 하 고 한 리소스 그룹 toodeploy hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="8a97c-215">내보내기 문제 수정</span><span class="sxs-lookup"><span data-stu-id="8a97c-215">Fix export issues</span></span>
<span data-ttu-id="8a97c-216">일부 리소스 형식은 hello 내보내기 템플릿 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="8a97c-217">이 문제를 수동으로 tooresolve 서식 파일에 다시 hello 누락 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="8a97c-218">hello 오류 메시지에 내보낼 수 없는 hello 리소스 종류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="8a97c-219">[템플릿 참조](/azure/templates/)에서 리소스 종류를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="8a97c-220">예를 들어 가상 네트워크 게이트웨이 추가, 참조 toomanually [Microsoft.Network/virtualNetworkGateways 템플릿 참조](/azure/templates/microsoft.network/virtualnetworkgateways)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="8a97c-221">배포 기록이 아닌 리소스 그룹에서 내보낸 경우 내보내기 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="8a97c-222">마지막 배포 hello hello 리소스 그룹의 현재 상태를 정확 하 게 나타내는 경우 hello 리소스 그룹 대신 hello 배포 기록에서 hello 서식 파일을 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="8a97c-223">만 단일 서식 파일에 정의 되어 있지 않은 변경 내용 toohello 리소스 그룹을 변경한 경우 리소스 그룹에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8a97c-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a97c-224">Next steps</span></span>
<span data-ttu-id="8a97c-225">배웠습니다 어떻게 tooexport hello 포털에서 만든 리소스에서 템플릿 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="8a97c-226">[PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) 또는 [REST API](resource-group-template-deploy-rest.md)를 통해 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="8a97c-227">tooexport PowerShell 통해서만 템플릿을 참조 하는 방법을 toosee [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8a97c-228">tooexport Azure CLI를 통해 템플릿을 참조 하는 방법을 toosee [사용 하 여 hello Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI](xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a97c-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

