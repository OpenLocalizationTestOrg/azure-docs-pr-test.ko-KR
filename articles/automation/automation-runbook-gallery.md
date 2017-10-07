---
title: "Azure 자동화에 대 한 aaaRunbook 및 모듈 갤러리 | Microsoft Docs"
description: "Runbook 및 모듈에서 Microsoft 및 hello 커뮤니티 tooinstall 있습니다 사용할 수 있는 및 Azure 자동화 환경에서 사용 합니다.  이 문서에 액세스 하는 방법을 이러한 리소스와 toocontribute runbook toohello 갤러리 설명 합니다."
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
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a><span data-ttu-id="47d1d-104">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="47d1d-104">Runbook and module galleries for Azure Automation</span></span>
<span data-ttu-id="47d1d-105">Azure 자동화에서 사용자 고유의 runbook 및 모듈을 작성 하지 않고 다양 한 Microsoft 및 hello 커뮤니티에 의해 이미 빌드된 시나리오를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-105">Rather than creating your own runbooks and modules in Azure Automation, you can access a variety of scenarios that have already been built by Microsoft and hello community.</span></span>  <span data-ttu-id="47d1d-106">이러한 시나리오는 수정 없이 그대로 사용하거나, 이를 기초로 특정 요구 사항에 맞게 편집하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-106">You can either use these scenarios without modification or you can use them as a starting point and edit them for your specific requirements.</span></span>

<span data-ttu-id="47d1d-107">Hello에서 runbook을 가져올 수 있습니다 [Runbook 갤러리](#runbooks-in-runbook-gallery) hello에서 모듈을 검색 하 고 [PowerShell 갤러리](#modules-in-powerShell-gallery)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-107">You can get runbooks from hello [Runbook Gallery](#runbooks-in-runbook-gallery) and modules from hello [PowerShell Gallery](#modules-in-powerShell-gallery).</span></span>  <span data-ttu-id="47d1d-108">개발 하는 시나리오를 공유 하 여 toohello 커뮤니티를 느려지게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-108">You can also contribute toohello community by sharing scenarios that you develop.</span></span>

## <a name="runbooks-in-runbook-gallery"></a><span data-ttu-id="47d1d-109">Runbook 갤러리의 Runbook</span><span class="sxs-lookup"><span data-stu-id="47d1d-109">Runbooks in Runbook Gallery</span></span>
<span data-ttu-id="47d1d-110">hello [Runbook 갤러리](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) runbook의 다양 한 Azure 자동화로 가져올 수 있는 Microsoft 및 hello 커뮤니티에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-110">hello [Runbook Gallery](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) provides a variety of runbooks from Microsoft and hello community that you can import into Azure Automation.</span></span> <span data-ttu-id="47d1d-111">Hello에서 호스팅되는 hello 갤러리에서 runbook을 다운로드 하거나 [TechNet 스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/site/upload), hello Azure 클래식 포털 또는 Azure 포털에서 hello 갤러리에서 runbook을 직접 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-111">You can either download a runbook from hello gallery which is hosted in hello [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), or you can directly import runbooks from hello gallery from either hello Azure classic portal or Azure portal.</span></span>

<span data-ttu-id="47d1d-112">가져올 수 있습니다 hello Runbook 갤러리에서 직접 hello Azure 클래식 포털 또는 Azure 포털을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-112">You can only import directly from hello Runbook Gallery using hello Azure classic portal or Azure portal.</span></span> <span data-ttu-id="47d1d-113">Windows PowerShell을 사용하여 이 함수를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-113">You cannot perform this function using Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="47d1d-114">Hello Runbook 갤러리에서에서 가져올 때 각별히 주의 해야 설치 하 고 프로덕션 환경에서 실행을 사용 하는 모든 runbook의 hello 내용의 유효성을 검사 해야 합니다. |</span><span class="sxs-lookup"><span data-stu-id="47d1d-114">You should validate hello contents of any runbooks that you get from hello Runbook Gallery and use extreme caution in installing and running them in a production environment.|</span></span>
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a><span data-ttu-id="47d1d-115">Azure 클래식 포털 hello로 hello Runbook 갤러리에서에서 runbook tooimport</span><span class="sxs-lookup"><span data-stu-id="47d1d-115">tooimport a runbook from hello Runbook Gallery with hello Azure classic portal</span></span>
1. <span data-ttu-id="47d1d-116">Hello Azure 포털에서에서 클릭 하 고, **새로**, **응용 프로그램 서비스**, **자동화**, **Runbook**, **갤러리에서**.</span><span class="sxs-lookup"><span data-stu-id="47d1d-116">In hello Azure Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **From Gallery**.</span></span>
2. <span data-ttu-id="47d1d-117">범주 tooview 선택 관련 runbook 및 runbook tooview 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-117">Select a category tooview related runbooks, and select a runbook tooview its details.</span></span> <span data-ttu-id="47d1d-118">원하는 hello runbook을 선택 하면 hello 오른쪽 화살표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-118">When you select hello runbook you want, click hello right arrow button.</span></span>
   
    ![Runbook 갤러리](media/automation-runbook-gallery/runbook-gallery.png)
3. <span data-ttu-id="47d1d-120">Hello runbook의 내용을 hello를 검토 하 고 hello 설명에서 모든 요구 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-120">Review hello contents of hello runbook and note any requirements in hello description.</span></span> <span data-ttu-id="47d1d-121">완료 되 면 hello 오른쪽 화살표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-121">Click hello right arrow button when you’re done.</span></span>
4. <span data-ttu-id="47d1d-122">Hello runbook 세부 정보를 입력 하 고 hello 확인 표시 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-122">Enter hello runbook details and then click hello checkmark button.</span></span> <span data-ttu-id="47d1d-123">hello runbook 이름 이미 입력 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-123">hello runbook name will already be filled in.</span></span>
5. <span data-ttu-id="47d1d-124">hello runbook hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-124">hello runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a><span data-ttu-id="47d1d-125">Azure 포털 hello로 hello Runbook 갤러리에서에서 runbook tooimport</span><span class="sxs-lookup"><span data-stu-id="47d1d-125">tooimport a runbook from hello Runbook Gallery with hello Azure portal</span></span>
1. <span data-ttu-id="47d1d-126">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-126">In hello Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="47d1d-127">Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-127">Click on hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="47d1d-128">**갤러리 찾아보기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-128">Click **Browse gallery** button.</span></span>
   
    ![갤러리 찾아보기 단추](media/automation-runbook-gallery/browse-gallery-button.png)
4. <span data-ttu-id="47d1d-130">한 tooview 선택 hello 갤러리 항목을 찾아 해당 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-130">Locate hello gallery item you want and select it tooview its details.</span></span>
   
    ![갤러리 찾아보기](media/automation-runbook-gallery/browse-gallery.png)
5. <span data-ttu-id="47d1d-132">클릭 **보기 소스 프로젝트** hello에서 tooview hello 항목 [TechNet 스크립트 센터](http://gallery.technet.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-132">Click on **View source project** tooview hello item in hello [TechNet Script Center](http://gallery.technet.microsoft.com/).</span></span>
6. <span data-ttu-id="47d1d-133">tooimport 항목을 클릭 하 여 조치 tooview 세부 정보 클릭 hello 및 **가져오기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-133">tooimport an item, click on it tooview its details and then click hello **Import** button.</span></span>
   
    ![가져오기 단추](media/automation-runbook-gallery/gallery-item-detail.png)
7. <span data-ttu-id="47d1d-135">필요에 따라 hello runbook의 hello 이름을 변경 하 고 클릭 **확인** tooimport hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-135">Optionally, change hello name of hello runbook and then click **OK** tooimport hello runbook.</span></span>
8. <span data-ttu-id="47d1d-136">hello runbook hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-136">hello runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>

### <a name="adding-a-runbook-toohello-runbook-gallery"></a><span data-ttu-id="47d1d-137">Runbook toohello runbook 갤러리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-137">Adding a runbook toohello runbook gallery</span></span>
<span data-ttu-id="47d1d-138">Microsoft는 tooadd runbook toohello 유용한 tooother 고객 것으로 판단 되는 Runbook 갤러리를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-138">Microsoft encourages you tooadd runbooks toohello Runbook Gallery that you think would be useful tooother customers.</span></span>  <span data-ttu-id="47d1d-139">runbook을 추가할 수 [toohello 스크립트 센터 업로드](http://gallery.technet.microsoft.com/site/upload) 계정 hello 다음 세부 정보를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-139">You can add a runbook by [uploading it toohello Script Center](http://gallery.technet.microsoft.com/site/upload) taking into account hello following details.</span></span>

* <span data-ttu-id="47d1d-140">지정 해야 *Windows Azure* hello에 대 한 **범주** 및 *자동화* hello에 대 한 **Subcategory** hello runbook toobe 표시에 대 한 hello 마법사의 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-140">You must specify *Windows Azure* for hello **Category** and *Automation* for hello **Subcategory** for hello runbook toobe displayed in hello wizard.</span></span>  
* <span data-ttu-id="47d1d-141">hello 업로드는 단일.ps1 또는.graphrunbook 파일 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-141">hello upload must be a single .ps1 or .graphrunbook file.</span></span>  <span data-ttu-id="47d1d-142">Hello runbook에는 모든 모듈, 자식 runbook 또는 자산이 필요한 경우 다음 나열 해야 hello runbook의 주석 섹션 hello 및 hello 제출의 hello 설명에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-142">If hello runbook requires any modules, child runbooks, or assets, then you should list those in hello description of hello submission and in hello comments section of hello runbook.</span></span>  <span data-ttu-id="47d1d-143">여러 runbook을 요구 하는 시나리오를 설정한 경우에 각각 개별적으로 업로드 하 고 목록 hello 형태의 hello 관련 해당 설명의 각 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-143">If you have a scenario requiring multiple runbooks, then upload each separately and list hello names of hello related runbooks in each of their descriptions.</span></span> <span data-ttu-id="47d1d-144">Hello에 표시 됩니다 되도록 동일한 태그를 삽입 하는 hello를 사용 하면 동일한 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-144">Make sure that you use hello same tags so that they will show up in hello same category.</span></span> <span data-ttu-id="47d1d-145">다른 runbook은 필요한 hello 시나리오 toowork는 tooread hello 설명 tooknow를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-145">A user will have tooread hello description tooknow that other runbooks are required hello scenario toowork.</span></span>
* <span data-ttu-id="47d1d-146">게시 하는 경우 "GraphicalPS" hello 태그를 추가 **그래픽 runbook** (하지 그래픽 워크플로).</span><span class="sxs-lookup"><span data-stu-id="47d1d-146">Add hello tag "GraphicalPS" if you are publishing a **Graphical runbook** (not a Graphical Workflow).</span></span> 
* <span data-ttu-id="47d1d-147">Hello 설명을 사용 하 여 PowerShell 워크플로 또는 PowerShell 코드 조각을 삽입 **코드 섹션을 삽입** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-147">Insert either a PowerShell or PowerShell Workflow code snippet into hello description using **Insert code section** icon.</span></span>
* <span data-ttu-id="47d1d-148">hello hello 업로드에 대 한 요약에에서 표시 됩니다 hello Runbook 갤러리 결과 사용자 hello runbook의 hello 기능을 식별 하는 데 도움이 되는 자세한 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-148">hello Summary for hello upload will be displayed in hello Runbook Gallery results so you should provide detailed information that will help a user identify hello functionality of hello runbook.</span></span>
* <span data-ttu-id="47d1d-149">Hello 태그 toohello 업로드 다음의 하나 toothree를 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-149">You should assign one toothree of hello following Tags toohello upload.</span></span>  <span data-ttu-id="47d1d-150">hello runbook hello 마법사 해당 태그와 일치 하는 hello 범주 아래에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-150">hello runbook will be listed in hello wizard under hello categories that match its tags.</span></span>  <span data-ttu-id="47d1d-151">이 목록에 없는 모든 태그 hello 마법사에 의해 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-151">Any tags not on this list will be ignored by hello wizard.</span></span> <span data-ttu-id="47d1d-152">일치 하는 태그를 지정 하지 않는 경우 hello runbook 됩니다 다른 범주 hello 아래에 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-152">If you don’t specify any matching tags, hello runbook will be listed under hello Other category.</span></span>
  
  * <span data-ttu-id="47d1d-153">백업</span><span class="sxs-lookup"><span data-stu-id="47d1d-153">Backup</span></span>
  * <span data-ttu-id="47d1d-154">용량 관리</span><span class="sxs-lookup"><span data-stu-id="47d1d-154">Capacity Management</span></span>
  * <span data-ttu-id="47d1d-155">변경 제어</span><span class="sxs-lookup"><span data-stu-id="47d1d-155">Change Control</span></span>
  * <span data-ttu-id="47d1d-156">규정 준수</span><span class="sxs-lookup"><span data-stu-id="47d1d-156">Compliance</span></span>
  * <span data-ttu-id="47d1d-157">개발/테스트 환경</span><span class="sxs-lookup"><span data-stu-id="47d1d-157">Dev / Test Environments</span></span>
  * <span data-ttu-id="47d1d-158">재해 복구</span><span class="sxs-lookup"><span data-stu-id="47d1d-158">Disaster Recovery</span></span>
  * <span data-ttu-id="47d1d-159">모니터링</span><span class="sxs-lookup"><span data-stu-id="47d1d-159">Monitoring</span></span>
  * <span data-ttu-id="47d1d-160">패치</span><span class="sxs-lookup"><span data-stu-id="47d1d-160">Patching</span></span>
  * <span data-ttu-id="47d1d-161">프로비전</span><span class="sxs-lookup"><span data-stu-id="47d1d-161">Provisioning</span></span>
  * <span data-ttu-id="47d1d-162">재구성</span><span class="sxs-lookup"><span data-stu-id="47d1d-162">Remediation</span></span>
  * <span data-ttu-id="47d1d-163">VM 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="47d1d-163">VM Lifecycle Management</span></span>
* <span data-ttu-id="47d1d-164">자동화 하므로 업로드 한 항목이 즉시 표시 되지 않습니다는 시간에 한 번씩 hello 갤러리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-164">Automation updates hello Gallery once an hour, so you won’t see your contributions immediately.</span></span>

## <a name="modules-in-powershell-gallery"></a><span data-ttu-id="47d1d-165">PowerShell 갤러리의 모듈</span><span class="sxs-lookup"><span data-stu-id="47d1d-165">Modules in PowerShell Gallery</span></span>
<span data-ttu-id="47d1d-166">PowerShell 모듈, runbook에서 사용할 수 있는 cmdlet을 포함 하 고 Azure 자동화에서 설치할 수 있는 기존 모듈 hello에서 사용할 수 있으며 [PowerShell 갤러리](http://www.powershellgallery.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-166">PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in hello [PowerShell Gallery](http://www.powershellgallery.com).</span></span>  <span data-ttu-id="47d1d-167">Hello Azure 포털에서에서이 갤러리를 시작 하 고 Azure 자동화로 직접 설치 하거나을 다운로드 하 고 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-167">You can launch this gallery from hello Azure portal and install them directly into Azure Automation or you can download them and install them manually.</span></span>  <span data-ttu-id="47d1d-168">Hello Azure 클래식 포털에서 직접 hello 모듈을 설치할 수 없지만 다운로드할 수 있는 다른 모듈와 마찬가지로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-168">You cannot install hello modules directly from hello Azure classic portal, but you can download them install them as you would any other module.</span></span>

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a><span data-ttu-id="47d1d-169">Azure 포털 hello로 hello 자동화 모듈 갤러리에서에서 모듈 tooimport</span><span class="sxs-lookup"><span data-stu-id="47d1d-169">tooimport a module from hello Automation Module Gallery with hello Azure portal</span></span>
1. <span data-ttu-id="47d1d-170">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-170">In hello Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="47d1d-171">Hello 클릭 **자산** 자산의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-171">Click on hello **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="47d1d-172">Hello 클릭 **모듈** 타일 tooopen hello 모듈 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-172">Click on hello **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="47d1d-173">Hello 클릭 **찾아보기 갤러리** 단추와 hello 찾아보기 갤러리 블레이드 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-173">Click on hello **Browse gallery** button and hello Browse gallery blade is launched.</span></span>
   
    ![모듈 갤러리](media/automation-runbook-gallery/modules-blade.png) <br>
5. <span data-ttu-id="47d1d-175">Hello 찾아보기 갤러리 블레이드를 시작한 후에 hello 필드를 수행 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-175">After you have launched hello Browse gallery blade, you can search by hello following fields:</span></span>
   
   * <span data-ttu-id="47d1d-176">모듈 이름</span><span class="sxs-lookup"><span data-stu-id="47d1d-176">Module Name</span></span>
   * <span data-ttu-id="47d1d-177">태그</span><span class="sxs-lookup"><span data-stu-id="47d1d-177">Tags</span></span>
   * <span data-ttu-id="47d1d-178">작성자</span><span class="sxs-lookup"><span data-stu-id="47d1d-178">Author</span></span>
   * <span data-ttu-id="47d1d-179">Cmdlet/DSC 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="47d1d-179">Cmdlet/DSC resource name</span></span>
6. <span data-ttu-id="47d1d-180">관심이 tooview 선택 하는 모듈을 찾습니다 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-180">Locate a module that you're interested in and select it tooview its details.</span></span>  
   <span data-ttu-id="47d1d-181">링크 백 toohello를 포함 하 여 hello 모듈에 대 한 자세한 정보를 볼 수를 특정 모듈에 드릴 종속성, 필요한 PowerShell 갤러리 및 hello cmdlet 및/또는 DSC 리소스 모듈 hello를 모두 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-181">When you drill into a specific module, you can view more information about hello module, including a link back toohello PowerShell Gallery, any required dependencies, and all of hello cmdlets and/or DSC resources that hello module contains.</span></span>
   
    ![PowerShell 모듈 세부 정보](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. <span data-ttu-id="47d1d-183">Azure 자동화로 직접 tooinstall hello 모듈 클릭 hello **가져오기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-183">tooinstall hello module directly into Azure Automation, click hello **Import** button.</span></span>
   
    ![모듈 가져오기 단추](media/automation-runbook-gallery/module-import-button.png)
8. <span data-ttu-id="47d1d-185">Hello 가져오기 단추를 클릭 하면 tooimport 넣으려는 hello 모듈 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-185">When you click hello Import button, you will see hello module name that you are about tooimport.</span></span> <span data-ttu-id="47d1d-186">모든 hello 종속성 설치 된 경우 hello **확인** 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-186">If all hello dependencies are installed, hello **OK** button will be active.</span></span> <span data-ttu-id="47d1d-187">종속성 목록에 없으면 있어야만 tooimport 하는 것이 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-187">If you are missing dependencies, you need tooimport those before you can import this module.</span></span>
9. <span data-ttu-id="47d1d-188">클릭 **확인** tooimport hello 모듈 및 모듈 블레이드 hello 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-188">Click **OK** tooimport hello module, and hello module blade will launch.</span></span> <span data-ttu-id="47d1d-189">Azure 자동화 모듈 tooyour 계정을 가져오면 hello 모듈 및 hello cmdlet에 대 한 메타 데이터를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-189">When Azure Automation imports a module tooyour account, it extracts metadata about hello module and hello cmdlets.</span></span>
   
    ![모듈 가져오기 블레이드](media/automation-runbook-gallery/module-import-blade.png)
   
    <span data-ttu-id="47d1d-191">각 활동 추출 toobe 있기 때문에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-191">This may take a couple of minutes since each activity needs toobe extracted.</span></span>
10. <span data-ttu-id="47d1d-192">알림을 받게 배포 되 고 해당 hello 모듈 및 완료 되지 않았을 때의 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-192">You will receive a notification that hello module is being deployed and a notification when it has completed.</span></span>
11. <span data-ttu-id="47d1d-193">Hello 모듈을 가져온 후 hello 사용 가능한 활동 표시 되 고 runbook 및 원하는 상태 구성의 해당 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-193">After hello module is imported, you will see hello available activities, and you can use its resources in your runbooks and Desired State Configuration.</span></span>

## <a name="requesting-a-runbook-or-module"></a><span data-ttu-id="47d1d-194">Runbook 또는 모듈 요청 중</span><span class="sxs-lookup"><span data-stu-id="47d1d-194">Requesting a runbook or module</span></span>
<span data-ttu-id="47d1d-195">요청을 너무 보낼 수[사용자 음성](https://feedback.azure.com/forums/246290-azure-automation/)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-195">You can send requests too[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).</span></span>  <span data-ttu-id="47d1d-196">Runbook을 작성 하는 데 도움이 필요 하거나 PowerShell에 대 한 질문을 하는 경우 게시 질문 tooour [포럼](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d1d-196">If you need help writing a runbook or have a question about PowerShell, post a question tooour [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d1d-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47d1d-197">Next Steps</span></span>
* <span data-ttu-id="47d1d-198">runbook을 시작 하는 tooget 참조 [만들기 또는 Azure 자동화에서 runbook 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="47d1d-198">tooget started with runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="47d1d-199">toounderstand hello 차이점 PowerShell 및 PowerShell 워크플로 runbook으로 참조 [학습 PowerShell 워크플로](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="47d1d-199">toounderstand hello differences between PowerShell and PowerShell Workflow with runbooks, see [Learning PowerShell workflow](automation-powershell-workflow.md)</span></span>

