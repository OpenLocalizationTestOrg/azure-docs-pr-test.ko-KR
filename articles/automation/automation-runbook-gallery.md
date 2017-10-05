---
title: "Azure Automation용 Runbook 및 모듈 갤러리 | Microsoft Docs"
description: "Microsoft 및 커뮤니티의 Runbook과 모듈을 Azure 자동화 환경에 설치하여 사용할 수 있습니다.  이 글에서는 이러한 리소스에 액세스하는 방법과 자신의 Runbook을 갤러리에 올리는 방법을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 04cfafc9e7a037d915f63723fd0b67a07954460b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a><span data-ttu-id="549d7-104">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="549d7-104">Runbook and module galleries for Azure Automation</span></span>
<span data-ttu-id="549d7-105">Azure 자동화에서 사용자 고유의 Runbook 및 모듈을 만드는 대신 Microsoft 및 커뮤니티에서 이미 구성한 다양한 시나리오에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-105">Rather than creating your own runbooks and modules in Azure Automation, you can access a variety of scenarios that have already been built by Microsoft and the community.</span></span>  <span data-ttu-id="549d7-106">이러한 시나리오는 수정 없이 그대로 사용하거나, 이를 기초로 특정 요구 사항에 맞게 편집하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-106">You can either use these scenarios without modification or you can use them as a starting point and edit them for your specific requirements.</span></span>

<span data-ttu-id="549d7-107">Runbook은 [Runbook 갤러리](#runbooks-in-runbook-gallery)에서, 모듈은 [PowerShell 갤러리](#modules-in-powerShell-gallery)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-107">You can get runbooks from the [Runbook Gallery](#runbooks-in-runbook-gallery) and modules from the [PowerShell Gallery](#modules-in-powerShell-gallery).</span></span>  <span data-ttu-id="549d7-108">또한 자신이 개발한 시나리오를 공유하여 커뮤니티에 기여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-108">You can also contribute to the community by sharing scenarios that you develop.</span></span>

## <a name="runbooks-in-runbook-gallery"></a><span data-ttu-id="549d7-109">Runbook 갤러리의 Runbook</span><span class="sxs-lookup"><span data-stu-id="549d7-109">Runbooks in Runbook Gallery</span></span>
<span data-ttu-id="549d7-110">[Runbook 갤러리](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation)는 Azure 자동화로 가져올 수 있는 Microsoft 및 커뮤니티에서 제작한 다양한 Runbook을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-110">The [Runbook Gallery](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) provides a variety of runbooks from Microsoft and the community that you can import into Azure Automation.</span></span> <span data-ttu-id="549d7-111">[TechNet 스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/site/upload)에서 호스팅되는 갤러리로부터 Runbook을 다운로드하거나, Azure 클래식 포털 또는 Azure 포털의 갤러리에서 Runbook을 직접 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-111">You can either download a runbook from the gallery which is hosted in the [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), or you can directly import runbooks from the gallery from either the Azure classic portal or Azure portal.</span></span>

<span data-ttu-id="549d7-112">Azure 클래식 포털 또는 Azure 포털을 사용하는 Runbook 갤러리에서만 직접 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-112">You can only import directly from the Runbook Gallery using the Azure classic portal or Azure portal.</span></span> <span data-ttu-id="549d7-113">Windows PowerShell을 사용하여 이 함수를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-113">You cannot perform this function using Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="549d7-114">프러덕션 환경에서 설치 및 실행할 때는 Runbook 갤러리에서 가져올 Runbook 내용의 유효성을 검사해야 하며 세심한 주의가 필요합니다.| </span><span class="sxs-lookup"><span data-stu-id="549d7-114">You should validate the contents of any runbooks that you get from the Runbook Gallery and use extreme caution in installing and running them in a production environment.|</span></span>
> 
> 

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-classic-portal"></a><span data-ttu-id="549d7-115">Azure 클래식 포털을 사용하여 Runbook 갤러리에서 Runbook을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="549d7-115">To import a runbook from the Runbook Gallery with the Azure classic portal</span></span>
1. <span data-ttu-id="549d7-116">Azure Portal에서 **새로 만들기**, **앱 서비스**, **자동화**, **Runbook**, **Gallery에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-116">In the Azure Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **From Gallery**.</span></span>
2. <span data-ttu-id="549d7-117">관련 Runbook을 볼 범주를 선택하고 Runbook을 선택하여 세부 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-117">Select a category to view related runbooks, and select a runbook to view its details.</span></span> <span data-ttu-id="549d7-118">원하는 Runbook을 선택했으면 오른쪽 화살표 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-118">When you select the runbook you want, click the right arrow button.</span></span>
   
    ![Runbook 갤러리](media/automation-runbook-gallery/runbook-gallery.png)
3. <span data-ttu-id="549d7-120">Runbook의 내용을 검토하고 설명의 모든 요구 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-120">Review the contents of the runbook and note any requirements in the description.</span></span> <span data-ttu-id="549d7-121">마치면 오른쪽 화살표 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-121">Click the right arrow button when you’re done.</span></span>
4. <span data-ttu-id="549d7-122">Runbook의 세부 정보를 입력하고 확인 표시 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-122">Enter the runbook details and then click the checkmark button.</span></span> <span data-ttu-id="549d7-123">Runbook 이름은 이미 입력되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-123">The runbook name will already be filled in.</span></span>
5. <span data-ttu-id="549d7-124">이 Runbook이 자동화 계정의 **Runbook** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-124">The runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal"></a><span data-ttu-id="549d7-125">Azure 포털을 사용하여 Runbook 갤러리에서 Runbook을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="549d7-125">To import a runbook from the Runbook Gallery with the Azure portal</span></span>
1. <span data-ttu-id="549d7-126">Azure 포털에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-126">In the Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="549d7-127">**Runbook** 타일을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-127">Click on the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="549d7-128">**갤러리 찾아보기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-128">Click **Browse gallery** button.</span></span>
   
    ![갤러리 찾아보기 단추](media/automation-runbook-gallery/browse-gallery-button.png)
4. <span data-ttu-id="549d7-130">원하는 갤러리 항목을 찾아 선택하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-130">Locate the gallery item you want and select it to view its details.</span></span>
   
    ![갤러리 찾아보기](media/automation-runbook-gallery/browse-gallery.png)
5. <span data-ttu-id="549d7-132">**TechNet 스크립트 센터** 의 항목을 확인하려면 [소스 프로젝트 보기](http://gallery.technet.microsoft.com/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-132">Click on **View source project** to view the item in the [TechNet Script Center](http://gallery.technet.microsoft.com/).</span></span>
6. <span data-ttu-id="549d7-133">항목을 가져오려면 해당 항목을 클릭하여 세부 정보를 확인한 다음 **가져오기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-133">To import an item, click on it to view its details and then click the **Import** button.</span></span>
   
    ![가져오기 단추](media/automation-runbook-gallery/gallery-item-detail.png)
7. <span data-ttu-id="549d7-135">선택적으로 Runbook의 이름을 변경한 다음 **확인** 을 클릭하여 해당 Runbook을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-135">Optionally, change the name of the runbook and then click **OK** to import the runbook.</span></span>
8. <span data-ttu-id="549d7-136">이 Runbook이 자동화 계정의 **Runbook** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-136">The runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>

### <a name="adding-a-runbook-to-the-runbook-gallery"></a><span data-ttu-id="549d7-137">Runbook 갤러리에 Runbook 추가</span><span class="sxs-lookup"><span data-stu-id="549d7-137">Adding a runbook to the runbook gallery</span></span>
<span data-ttu-id="549d7-138">Microsoft에서는 다른 고객에게 유용하다고 생각하는 Runbook을 Runbook 갤러리에 추가하도록 장려하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-138">Microsoft encourages you to add runbooks to the Runbook Gallery that you think would be useful to other customers.</span></span>  <span data-ttu-id="549d7-139">다음 세부 정보를 고려하여 [스크립트 센터에 업로드](http://gallery.technet.microsoft.com/site/upload) 를 선택하면 Runbook을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-139">You can add a runbook by [uploading it to the Script Center](http://gallery.technet.microsoft.com/site/upload) taking into account the following details.</span></span>

* <span data-ttu-id="549d7-140">*범주*에 **Windows Azure**를 지정하고 *하위 범주*에 **자동화**를 지정해야 Runbook이 마법사에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-140">You must specify *Windows Azure* for the **Category** and *Automation* for the **Subcategory** for the runbook to be displayed in the wizard.</span></span>  
* <span data-ttu-id="549d7-141">단일.ps1 또는 .graphrunbook 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-141">The upload must be a single .ps1 or .graphrunbook file.</span></span>  <span data-ttu-id="549d7-142">Runbook에 필요한 모듈, 자식 Runbook 또는 자산이 있는 경우 Runbook의 제출 설명과 내용 섹션에 해당 항목을 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-142">If the runbook requires any modules, child runbooks, or assets, then you should list those in the description of the submission and in the comments section of the runbook.</span></span>  <span data-ttu-id="549d7-143">여러 Runbook이 필요한 시나리오인 경우 각 Runbook을 개별적으로 업로드하고 설명마다 관련 Runbook의 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-143">If you have a scenario requiring multiple runbooks, then upload each separately and list the names of the related runbooks in each of their descriptions.</span></span> <span data-ttu-id="549d7-144">동일한 범주에 표시되도록 동일한 태그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-144">Make sure that you use the same tags so that they will show up in the same category.</span></span> <span data-ttu-id="549d7-145">시나리오가 작동하기 위해 다른 Runbook이 필요하다는 설명을 사용자가 읽고 알 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-145">A user will have to read the description to know that other runbooks are required the scenario to work.</span></span>
* <span data-ttu-id="549d7-146">**그래픽 Runbook** (그래픽 워크플로가 아닌)을 게시하는 경우 "GraphicalPS" 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-146">Add the tag "GraphicalPS" if you are publishing a **Graphical runbook** (not a Graphical Workflow).</span></span> 
* <span data-ttu-id="549d7-147">**코드 섹션 삽입** 아이콘을 사용하여 PowerShell 또는 PowerShell 워크플로 코드 조각을 설명에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-147">Insert either a PowerShell or PowerShell Workflow code snippet into the description using **Insert code section** icon.</span></span>
* <span data-ttu-id="549d7-148">업로드 요약이 Runbook 갤러리 결과에 표시되므로 사용자가 해당 Runbook의 기능을 파악하는 데 도움이 되는 상세한 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-148">The Summary for the upload will be displayed in the Runbook Gallery results so you should provide detailed information that will help a user identify the functionality of the runbook.</span></span>
* <span data-ttu-id="549d7-149">업로드에 1~3개의 다음 태그를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-149">You should assign one to three of the following Tags to the upload.</span></span>  <span data-ttu-id="549d7-150">Runbook이 마법사에서 태그와 일치하는 범주에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-150">The runbook will be listed in the wizard under the categories that match its tags.</span></span>  <span data-ttu-id="549d7-151">이 목록에 없는 태그는 마법사에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-151">Any tags not on this list will be ignored by the wizard.</span></span> <span data-ttu-id="549d7-152">일치하는 태그를 지정하지 않는 경우 Runbook이 기타 범주에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-152">If you don’t specify any matching tags, the runbook will be listed under the Other category.</span></span>
  
  * <span data-ttu-id="549d7-153">백업</span><span class="sxs-lookup"><span data-stu-id="549d7-153">Backup</span></span>
  * <span data-ttu-id="549d7-154">용량 관리</span><span class="sxs-lookup"><span data-stu-id="549d7-154">Capacity Management</span></span>
  * <span data-ttu-id="549d7-155">변경 제어</span><span class="sxs-lookup"><span data-stu-id="549d7-155">Change Control</span></span>
  * <span data-ttu-id="549d7-156">규정 준수</span><span class="sxs-lookup"><span data-stu-id="549d7-156">Compliance</span></span>
  * <span data-ttu-id="549d7-157">개발/테스트 환경</span><span class="sxs-lookup"><span data-stu-id="549d7-157">Dev / Test Environments</span></span>
  * <span data-ttu-id="549d7-158">재해 복구</span><span class="sxs-lookup"><span data-stu-id="549d7-158">Disaster Recovery</span></span>
  * <span data-ttu-id="549d7-159">모니터링</span><span class="sxs-lookup"><span data-stu-id="549d7-159">Monitoring</span></span>
  * <span data-ttu-id="549d7-160">패치</span><span class="sxs-lookup"><span data-stu-id="549d7-160">Patching</span></span>
  * <span data-ttu-id="549d7-161">프로비전</span><span class="sxs-lookup"><span data-stu-id="549d7-161">Provisioning</span></span>
  * <span data-ttu-id="549d7-162">재구성</span><span class="sxs-lookup"><span data-stu-id="549d7-162">Remediation</span></span>
  * <span data-ttu-id="549d7-163">VM 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="549d7-163">VM Lifecycle Management</span></span>
* <span data-ttu-id="549d7-164">자동화는 갤러리를 한 시간마다 업데이트하므로 제출한 내용이 즉시 확인되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-164">Automation updates the Gallery once an hour, so you won’t see your contributions immediately.</span></span>

## <a name="modules-in-powershell-gallery"></a><span data-ttu-id="549d7-165">PowerShell 갤러리의 모듈</span><span class="sxs-lookup"><span data-stu-id="549d7-165">Modules in PowerShell Gallery</span></span>
<span data-ttu-id="549d7-166">PowerShell 모듈에는 Runbook에 사용할 수 있는 cmdlet이 있으며, Azure 자동화에서 설치할 수 있는 기존 모듈을 [PowerShell 갤러리](http://www.powershellgallery.com)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-166">PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in the [PowerShell Gallery](http://www.powershellgallery.com).</span></span>  <span data-ttu-id="549d7-167">Azure 포털에서 이 갤러리를 실행하여 Azure 자동화에 직접 설치하거나, 수동으로 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-167">You can launch this gallery from the Azure portal and install them directly into Azure Automation or you can download them and install them manually.</span></span>  <span data-ttu-id="549d7-168">Azure 클래식 포털에서 모듈을 직접 설치할 수는 없지만 다운로드하여 다른 모듈처럼 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-168">You cannot install the modules directly from the Azure classic portal, but you can download them install them as you would any other module.</span></span>

### <a name="to-import-a-module-from-the-automation-module-gallery-with-the-azure-portal"></a><span data-ttu-id="549d7-169">Azure 포털을 사용하여 자동화 모듈 갤러리에서 모듈을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="549d7-169">To import a module from the Automation Module Gallery with the Azure portal</span></span>
1. <span data-ttu-id="549d7-170">Azure 포털에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-170">In the Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="549d7-171">**자산** 타일을 클릭하여 자산 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-171">Click on the **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="549d7-172">**모듈** 타일을 클릭하여 모듈 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-172">Click on the **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="549d7-173">**갤러리 찾아보기** 단추를 클릭하면 갤러리 찾아보기 블레이드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-173">Click on the **Browse gallery** button and the Browse gallery blade is launched.</span></span>
   
    ![모듈 갤러리](media/automation-runbook-gallery/modules-blade.png) <br>
5. <span data-ttu-id="549d7-175">갤러리 찾아보기 블레이드에서 시작한 후 다음 필드로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-175">After you have launched the Browse gallery blade, you can search by the following fields:</span></span>
   
   * <span data-ttu-id="549d7-176">모듈 이름</span><span class="sxs-lookup"><span data-stu-id="549d7-176">Module Name</span></span>
   * <span data-ttu-id="549d7-177">태그</span><span class="sxs-lookup"><span data-stu-id="549d7-177">Tags</span></span>
   * <span data-ttu-id="549d7-178">작성자</span><span class="sxs-lookup"><span data-stu-id="549d7-178">Author</span></span>
   * <span data-ttu-id="549d7-179">Cmdlet/DSC 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="549d7-179">Cmdlet/DSC resource name</span></span>
6. <span data-ttu-id="549d7-180">관심이 있는 모듈을 찾아 선택하여 세부 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-180">Locate a module that you're interested in and select it to view its details.</span></span>  
   <span data-ttu-id="549d7-181">특정 모듈을 상세히 검색하면 PowerShell 갤러리로 다시 연결되는 링크, 필요한 모든 종속성, 모듈이 포함하는 모든 cmdlet 및/또는 DSC 리소스를 포함하여 모듈에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-181">When you drill into a specific module, you can view more information about the module, including a link back to the PowerShell Gallery, any required dependencies, and all of the cmdlets and/or DSC resources that the module contains.</span></span>
   
    ![PowerShell 모듈 세부 정보](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. <span data-ttu-id="549d7-183">Azure 자동화에 직접 모듈을 설치하려면 **가져오기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-183">To install the module directly into Azure Automation, click the **Import** button.</span></span>
   
    ![모듈 가져오기 단추](media/automation-runbook-gallery/module-import-button.png)
8. <span data-ttu-id="549d7-185">가져오기 단추를 클릭하면 가져오려고 하는 모듈 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-185">When you click the Import button, you will see the module name that you are about to import.</span></span> <span data-ttu-id="549d7-186">모든 종속성이 설치되면 **확인** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-186">If all the dependencies are installed, the **OK** button will be active.</span></span> <span data-ttu-id="549d7-187">종속성이 없는 경우 종속성을 가져와야만 이 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-187">If you are missing dependencies, you need to import those before you can import this module.</span></span>
9. <span data-ttu-id="549d7-188">모듈을 가져오도록 **확인** 을 클릭하면 모듈 블레이드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-188">Click **OK** to import the module, and the module blade will launch.</span></span> <span data-ttu-id="549d7-189">Azure 자동화가 계정에 모듈을 가져오면 모듈 및 cmdlet에 대한 메타데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-189">When Azure Automation imports a module to your account, it extracts metadata about the module and the cmdlets.</span></span>
   
    ![모듈 가져오기 블레이드](media/automation-runbook-gallery/module-import-blade.png)
   
    <span data-ttu-id="549d7-191">각 활동을 추출해야 하므로 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-191">This may take a couple of minutes since each activity needs to be extracted.</span></span>
10. <span data-ttu-id="549d7-192">모듈을 가져오는 도중과 완료 시점에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-192">You will receive a notification that the module is being deployed and a notification when it has completed.</span></span>
11. <span data-ttu-id="549d7-193">모듈을 가져온 후 사용 가능한 작업이 표시되고 Runbook 및 필요한 상태 구성에서 해당 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-193">After the module is imported, you will see the available activities, and you can use its resources in your runbooks and Desired State Configuration.</span></span>

## <a name="requesting-a-runbook-or-module"></a><span data-ttu-id="549d7-194">Runbook 또는 모듈 요청 중</span><span class="sxs-lookup"><span data-stu-id="549d7-194">Requesting a runbook or module</span></span>
<span data-ttu-id="549d7-195">[사용자 음성](https://feedback.azure.com/forums/246290-azure-automation/)에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549d7-195">You can send requests to [User Voice](https://feedback.azure.com/forums/246290-azure-automation/).</span></span>  <span data-ttu-id="549d7-196">Runbook을 작성하는 데 도움이 필요하거나 PowerShell에 대한 질문이 있으면 [포럼](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)에 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="549d7-196">If you need help writing a runbook or have a question about PowerShell, post a question to our [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).</span></span>

## <a name="next-steps"></a><span data-ttu-id="549d7-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="549d7-197">Next Steps</span></span>
* <span data-ttu-id="549d7-198">Runbook 작성을 시작하려면 [Azure 자동화에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="549d7-198">To get started with runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="549d7-199">Runbook용 PowerShell 및 PowerShell 워크플로 간의 차이점을 이해하려면 [PowerShell 워크플로 학습](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="549d7-199">To understand the differences between PowerShell and PowerShell Workflow with runbooks, see [Learning PowerShell workflow](automation-powershell-workflow.md)</span></span>

