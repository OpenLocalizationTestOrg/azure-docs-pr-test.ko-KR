---
title: "데이터 관리 게이트웨이 aaaMove 데이터-| Microsoft Docs"
description: "Hello와 온-프레미스 데이터 게이트웨이 toomove 데이터 설정 클라우드입니다. 데이터 toomove Azure Data Factory에서에서 데이터 관리 게이트웨이 사용 합니다."
keywords: "데이터 게이트웨이, 데이터 통합, 데이터 이동, 게이트웨이 자격 증명"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="a0186-105">온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="a0186-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="a0186-106">이 문서에서는 Data Factory를 사용하여 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터 통합의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="a0186-107">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 및 기타 데이터 팩터리 핵심 개념 문서: [데이터 집합](data-factory-create-datasets.md) 및 [파이프라인](data-factory-create-pipelines.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="a0186-108">데이터 관리 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="a0186-108">Data Management Gateway</span></span>
<span data-ttu-id="a0186-109">온-프레미스 데이터 저장소에서 데이터를 이동 하 여 온-프레미스 컴퓨터 tooenable에 데이터 관리 게이트웨이 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="a0186-110">hello 게이트웨이 hello hello 데이터 저장소로 또는 다른 컴퓨터에이 hello 게이트웨이 toohello 데이터 저장소에 연결할 수 있는 상태로 동일를 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0186-111">데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0186-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="a0186-112">hello 다음 연습에서는 표시 하는 toocreate 온-프레미스에서 데이터를 이동 하는 파이프라인으로 데이터 팩터리 **SQL Server** 데이터베이스 tooan Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="a0186-113">Hello 연습의 일부로 설치 하 고 컴퓨터에 hello 데이터 관리 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="a0186-114">연습: 온-프레미스 데이터 toocloud 복사</span><span class="sxs-lookup"><span data-stu-id="a0186-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="a0186-115">이 연습에서는 다음 단계 hello 수행 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="a0186-116">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-116">Create a data factory.</span></span>
2. <span data-ttu-id="a0186-117">데이터 관리 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="a0186-118">원본 및 싱크 데이터 저장소에 대한 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="a0186-119">Toorepresent 입력 데이터 집합을 만들고 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="a0186-120">복사 활동 toomove hello 데이터 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="a0186-121">Hello 자습서에 대 한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a0186-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="a0186-122">이 연습을 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="a0186-123">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="a0186-123">**Azure subscription**.</span></span>  <span data-ttu-id="a0186-124">구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a0186-125">Hello 참조 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/) 을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="a0186-126">**Azure Storage 계정**.</span><span class="sxs-lookup"><span data-stu-id="a0186-126">**Azure Storage Account**.</span></span> <span data-ttu-id="a0186-127">Hello blob 저장소로 사용 하는 **대상/싱크** 이 자습서에서는 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="a0186-128">Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계 toocreate 하나에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="a0186-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a0186-129">**SQL Server**.</span></span> <span data-ttu-id="a0186-130">이 자습서에서는 온-프레미스 SQL Server 데이터베이스를 **원본** 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="a0186-131">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-131">Create data factory</span></span>
<span data-ttu-id="a0186-132">이 단계를 사용 하 여 Azure 데이터 팩터리 인스턴스 이름은 Azure 포털 toocreate hello **ADFTutorialOnPremDF**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="a0186-133">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0186-134">**+ 새로 만들기**, **인텔리전스 + 분석** 및 **데이터 팩터리s**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![새로 만들기->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="a0186-136">Hello에 **새 데이터 팩터리** 페이지에서 입력 **ADFTutorialOnPremDF** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![TooStartboard 추가](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="a0186-138">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="a0186-139">Hello 오류가 나타나면: **"ADFTutorialOnPremDF" 데이터 팩터리 이름을 사용할 수 없으면**을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFTutorialOnPremDF)을 변경 하 고 다시 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="a0186-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="a0186-140">이 자습서의 나머지 단계를 수행하는 동안 ADFTutorialOnPremDF 대신에 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="a0186-141">hello 데이터 팩터리의 hello 이름으로 등록 될 수는 **DNS** hello 미래에 이름을 지정 하 고 따라서 공개적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="a0186-142">선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="a0186-143">기존 **리소스 그룹** 을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="a0186-144">Hello 자습서에 대 한 명명 된 리소스 그룹 만들기: **ADFTutorialResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="a0186-145">클릭 **만들기** hello에 **새 데이터 팩터리** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a0186-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a0186-146">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="a0186-147">Hello 참조 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 페이지:</span><span class="sxs-lookup"><span data-stu-id="a0186-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![데이터 팩터리 홈페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="a0186-149">게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-149">Create gateway</span></span>
1. <span data-ttu-id="a0186-150">Hello에 **Data Factory** 페이지 **작성자 및 배포** 타일 toolaunch hello **편집기** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![작성 및 배포 타일](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="a0186-152">데이터 팩터리 편집기 hello 클릭 **중... 더 많은** 도구 모음 hello 되 고 클릭 **새 데이터 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="a0186-153">단추로 또는 **데이터 게이트웨이** hello 트리 보기와 클릭 **새 데이터 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![도구 모음의 새 데이터 게이트웨이](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="a0186-155">Hello에 **만들기** 페이지에서 입력 **adftutorialgateway** hello에 대 한 **이름**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![게이트웨이 만들기 페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="a0186-157">이 연습에서는 하나의 노드만 (온-프레미스 Windows 컴퓨터)으로 hello 논리 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="a0186-158">Hello 게이트웨이를 여러 온-프레미스 컴퓨터를 연결 하 여 데이터 관리 게이트웨이 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="a0186-159">노드에서 동시에 실행할 수 있는 데이터 이동 작업의 수를 늘려 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="a0186-160">이 기능은 단일 노드가 있는 논리 게이트웨이에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="a0186-161">자세한 내용은 [Azure Data Factory에서 데이터 관리 게이트웨이 확장](data-factory-data-management-gateway-high-availability-scalability.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0186-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="a0186-162">Hello에 **구성** 페이지 **이 컴퓨터에 직접 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="a0186-163">이 작업 hello 게이트웨이에 대 한 hello 설치 패키지를 다운로드, 설치, 구성 하 고 hello 컴퓨터에서 hello 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="a0186-164">Internet Explorer 또는 Microsoft ClickOnce 호환 웹 브라우저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="a0186-165">Chrome을 사용 하는 경우 이동 toohello [크롬 웹 저장소](https://chrome.google.com/webstore/), "ClickOnce" 키워드를 사용 하 여 검색, hello ClickOnce 확장 중 하나를 선택 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="a0186-166">Firefox (설치 추가 기능에서)에 대 한 마십시오 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="a0186-167">클릭 **열기 메뉴** hello 도구 모음에서 단추 (**세 개의 가로선** hello 오른쪽 위 모서리에)를 클릭 하 여 **추가 기능**, "ClickOnce" 키워드를 사용 하 여 검색, hello 중 하나를 선택 ClickOnce 확장 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![게이트웨이 - 구성 페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="a0186-169">이 방법은 가장 쉬운 방법은 (원클릭) toodownload hello, 설치, 구성 및 한 번에 hello 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="a0186-170">Hello 나타나면 **Microsoft 데이터 관리 게이트웨이 구성 관리자** 응용 프로그램이 컴퓨터에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="a0186-171">찾을 수 있습니다 hello 실행 **ConfigManager.exe** hello 폴더에서: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="a0186-172">있습니다 수도 다운로드 하 고이 페이지에 hello 링크를 사용 하 여 게이트웨이 수동으로 설치 하 고 hello에 표시 된 hello 키를 사용 하 여 등록 **새 키** 입력란.</span><span class="sxs-lookup"><span data-stu-id="a0186-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="a0186-173">참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 모든 hello hello 게이트웨이에 대 한 세부 정보에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0186-174">로컬 컴퓨터 tooinstall hello의 관리자 여야 하 고 hello 데이터 관리 게이트웨이 성공적으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="a0186-175">추가 사용자 toohello를 추가할 수 있습니다 **데이터 관리 게이트웨이 사용자** 로컬 Windows 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="a0186-176">이 그룹의 hello 구성원 hello 데이터 관리 게이트웨이 구성 관리자 도구 tooconfigure hello 게이트웨이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="a0186-177">몇 분 정도 표시 될 때까지 기다리거나 hello 알림 메시지의 뒤에 표시 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![성공적인 게이트웨이 설치](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="a0186-179">컴퓨터에서 **데이터 관리 게이트웨이 구성 관리자** 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="a0186-180">Hello에 **검색** 창, 형식 **데이터 관리 게이트웨이** tooaccess이 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="a0186-181">찾을 수 있습니다 hello 실행 **ConfigManager.exe** hello 폴더에서: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="a0186-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![게이트웨이 구성 관리자](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="a0186-183">`adftutorialgateway is connected toohello cloud service` 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="a0186-184">상태 표시줄 아래쪽 디스플레이 hello hello **toohello 클라우드 서비스 연결** 와 함께 한 **녹색 확인 표시가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="a0186-185">Hello에 **홈** 탭 에서도 할 수 있습니다 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="a0186-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="a0186-186">**등록** hello hello 등록 단추를 사용 하 여 Azure 포털에서에서 게이트웨이 키가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="a0186-187">**중지** hello 데이터 관리 게이트웨이 호스트 서비스 게이트웨이 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="a0186-188">**업데이트를 예약할** toobe hello 하루 중 특정 시간에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="a0186-189">Hello 게이트웨이 보기 **마지막으로 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="a0186-190">업데이트 toohello 게이트웨이 설치할 수 있는 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="a0186-191">Toohello 전환 **설정** hello에 지정 된 탭 hello 인증서 **인증서** 섹션은 hello 포털에서 사용자가 지정한 hello 온-프레미스 데이터 저장소에 대 한 자격 증명 사용 되는 tooencrypt/암호 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="a0186-192">(선택 사항) 클릭 **변경** toouse 고유의 인증서 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="a0186-193">기본적으로 hello 게이트웨이 hello 데이터 팩터리 서비스에서 자동 생성 된 hello 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![게이트웨이 인증서 구성](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="a0186-195">수행할 수 있습니다 hello에 다음 작업 hello **설정을** 탭:</span><span class="sxs-lookup"><span data-stu-id="a0186-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="a0186-196">보거나 hello 게이트웨이에서 사용 되는 hello 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="a0186-197">Hello 게이트웨이에서 사용 되는 hello HTTPS 끝점을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="a0186-198">HTTP 프록시 toobe hello 게이트웨이에서 사용 되는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="a0186-199">(선택 사항) Toohello 전환 **진단** 탭에서 확인 hello **자세한 정보 로깅 사용** 옵션이 원하는 tooenable 자세한 로깅을 사용할 수 있는 tootroubleshoot 문제 hello 게이트웨이가 설치 된 경우.</span><span class="sxs-lookup"><span data-stu-id="a0186-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="a0186-200">hello 로깅 정보에서 확인할 수 있습니다 **이벤트 뷰어** 아래 **Applications and Services Logs** -> **데이터 관리 게이트웨이** 노드.</span><span class="sxs-lookup"><span data-stu-id="a0186-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![진단 탭](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="a0186-202">Hello 다음 hello에 대 한 작업을 수행할 수 있습니다 **진단** 탭:</span><span class="sxs-lookup"><span data-stu-id="a0186-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="a0186-203">사용 하 여 **연결 테스트** hello 게이트웨이 사용 하 여 섹션 tooan 온-프레미스 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="a0186-204">클릭 **로그 보기** toosee hello 데이터 관리 게이트웨이 이벤트 뷰어 창에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="a0186-205">클릭 **로그 보내기** tooupload 지난 7 일 tooMicrosoft toofacilitate 문제 해결 과정의 문제에 대 한 로그가 포함 된 zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="a0186-206">Hello에 **진단** 탭 hello **연결 테스트** 섹션에서 **SqlServer** hello 유형의 hello 데이터에 대해 저장, 이름이 hello 데이터베이스 서버의 hello 이름을 입력 데이터베이스 hello 인증 유형을 지정, 사용자 이름 및 암호를 입력 하 고 클릭 **테스트** tootest hello 게이트웨이 toohello 데이터베이스를 연결할 수 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="a0186-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="a0186-207">스위치 toohello 웹 브라우저 및 hello **Azure 포털**, 클릭 **확인** hello에 **구성** 페이지 hello에서 **새 데이터 게이트웨이** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="a0186-208">표시 되어야 **adftutorialgateway** 아래 **데이터 게이트웨이** hello 왼쪽 hello 트리 뷰에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="a0186-209">를 클릭 하면 hello JSON 관련 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="a0186-210">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-210">Create linked services</span></span>
<span data-ttu-id="a0186-211">이 단계에서는 두 개의 연결된 서비스인 **AzureStorageLinkedService** 및 **SqlServerLinkedService**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="a0186-212">hello **SqlServerLinkedService** 온-프레미스 SQL Server 데이터베이스 및 hello 연결 **AzureStorageLinkedService** 연결 된 서비스는 Azure blob 저장소 toohello 데이터 팩터리를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="a0186-213">Hello 온-프레미스 SQL Server 데이터베이스 toohello Azure blob 저장소에서 데이터를 복사 하는이 연습의 뒷부분에서 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="a0186-214">연결 된 서비스 tooan 온-프레미스 SQL Server 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="a0186-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="a0186-215">Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** hello 도구 모음을 선택 **SQL Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![새로운 SQL Server 연결 서비스](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="a0186-217">Hello에 **JSON 편집기** hello 오른쪽에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="a0186-218">Hello에 대 한 **gatewayName**, 지정 **adftutorialgateway**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="a0186-219">Hello에 **connectionString**, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="a0186-220">에 대 한 **servername**, hello hello SQL Server 데이터베이스를 호스팅하는 hello 서버 이름을 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0186-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="a0186-221">에 대 한 **databasename**, hello 데이터베이스의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="a0186-222">클릭 **Encrypt** hello 도구 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="a0186-223">Hello 자격 증명 관리자 응용 프로그램이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-223">You see hello Credentials Manager application.</span></span>

         ![자격 증명 관리자 응용 프로그램](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="a0186-225">Hello에 **자격 증명 설정** 대화 상자, 인증 유형, 사용자 이름 및 암호를 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="a0186-226">Hello 연결 완료 되 면 hello 암호화 된 자격 증명 hello JSON에에서 저장 됩니다 및 hello 대화 상자가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="a0186-227">자동으로 닫히지 않은 경우 hello 대화 상자를 시작 및 돌아갈 toohello 탭 hello Azure 포털으로 된 hello 빈 브라우저 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="a0186-228">Hello 게이트웨이 컴퓨터에서 이러한 자격 증명은 **암호화 된** Data Factory hello 인증서를 사용 하 여 서비스를 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="a0186-229">대신 데이터 관리 게이트웨이 hello와 연결 된 toouse hello 인증서 참조 [자격 증명을 안전 하 게 설정](#set-credentials-and-security)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="a0186-230">클릭 **배포** hello 명령 toodeploy hello SQL Server에 연결 된 서비스 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="a0186-231">Hello 연결 된 서비스 hello 트리 뷰에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-231">You should see hello linked service in hello tree view.</span></span>

      ![Hello 트리 보기에서 SQL Server 연결 된 서비스](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="a0186-233">Azure 저장소 계정에 대한 연결된 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="a0186-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="a0186-234">Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** 명령 모음 hello 되 고 클릭 **Azure 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="a0186-235">Hello hello에 대 한 Azure 저장소 계정 이름을 입력 **계정 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="a0186-236">Hello에 대 한 Azure 저장소 계정에 대 한 hello 키 입력 **계정 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="a0186-237">클릭 **배포** toodeploy hello **AzureStorageLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="a0186-238">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-238">Create datasets</span></span>
<span data-ttu-id="a0186-239">이 단계에서는 사용자 입력 및 출력 만드는 hello 복사 작업에 대 한 입력 및 출력 데이터를 나타내는 데이터 집합 (온-프레미스 SQL Server 데이터베이스 = > Azure blob 저장소).</span><span class="sxs-lookup"><span data-stu-id="a0186-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="a0186-240">데이터 집합을 만들기 전에 수행 hello (자세한 단계는 hello 목록 뒤) 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="a0186-241">라는 테이블을 만들어 **emp** 에 연결 된 서비스 toohello 데이터 팩터리로 추가 하는 SQL Server 데이터베이스 hello 및 몇 가지 샘플 항목 hello 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="a0186-242">라는 blob 컨테이너 만들기 **adftutorial** hello Azure에서에서 blob 저장소 계정을 연결 된 서비스 toohello 데이터 팩터리로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="a0186-243">Hello 자습서에 대 한 온-프레미스 SQL Server 준비</span><span class="sxs-lookup"><span data-stu-id="a0186-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="a0186-244">Hello 온-프레미스 SQL Server를 지정 하는 hello 데이터베이스에 연결 된 서비스 (**SqlServerLinkedService**)를 다음 SQL 스크립트 toocreate hello hello를 사용 하 여 **emp** hello 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="a0186-245">몇 가지 샘플 hello 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="a0186-246">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-246">Create input dataset</span></span>

1. <span data-ttu-id="a0186-247">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은**, 클릭 **새 데이터 집합** 명령 모음 hello 되 고 클릭 **SQL Server 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="a0186-248">Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-248">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="a0186-249">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="a0186-249">Note hello following points:</span></span>

   * <span data-ttu-id="a0186-250">**형식** 너무 설정**SqlServerTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="a0186-251">**tableName** 너무 설정**emp**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="a0186-252">**linkedServiceName** 너무 설정**SqlServerLinkedService** (이 연습의 앞부분에서이 연결 된 서비스를 생성 했습니다.).</span><span class="sxs-lookup"><span data-stu-id="a0186-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="a0186-253">다른 Azure 데이터 팩터리 파이프라인에서 생성 되지 않습니다는 입력된 데이터 집합을로 설정 해야 **외부** 너무**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="a0186-254">Hello 입력된 데이터는 생성 된 외부 toohello Azure 데이터 팩터리 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="a0186-255">Hello를 사용 하 여 모든 외부 데이터 정책을 지정할 수도 있습니다 **externalData** hello 요소 **정책** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0186-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="a0186-256">JSON 속성에 대한 자세한 내용은 [SQL Server 간 데이터 이동 데이터 이동](data-factory-sqlserver-connector.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0186-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="a0186-257">클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="a0186-258">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-258">Create output dataset</span></span>

1. <span data-ttu-id="a0186-259">Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 집합** 명령 모음 hello 되 고 클릭 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="a0186-260">Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-260">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="a0186-261">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="a0186-261">Note hello following points:</span></span>

   * <span data-ttu-id="a0186-262">**형식** 너무 설정**AzureBlob**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="a0186-263">**linkedServiceName** 너무 설정**AzureStorageLinkedService** (2 단계에서에서이 연결 된 서비스 만든 했습니다).</span><span class="sxs-lookup"><span data-stu-id="a0186-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="a0186-264">**folderPath** 너무 설정**adftutorial/outfromonpremdf** outfromonpremdf hello adftutorial 컨테이너에서 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="a0186-265">Hello 만들기 **adftutorial** 아직 없는 경우에 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="a0186-266">hello **가용성** 너무 설정**매시간** (**주파수** 도**시간** 및 **간격** 너무 설정 **1**).</span><span class="sxs-lookup"><span data-stu-id="a0186-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="a0186-267">hello 데이터 팩터리 서비스에서는 발생 하는 출력 데이터 조각 1 시간 마다 hello에 **emp** hello Azure SQL 데이터베이스의에서 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="a0186-268">지정 하지 않는 경우는 **fileName** 에 대 한는 **출력 테이블**, hello에 생성 된 hello 파일 **folderPath** 형식에 따라 hello에 이름이 지정: 데이터.<Guid>합니다. txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="a0186-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="a0186-269">tooset **folderPath** 및 **fileName** hello에 따라 동적으로 **SliceStart** 시간 hello partitionedBy 속성을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0186-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="a0186-270">다음 예제는 hello에서 folderPath hello SliceStart (처리 되 고 hello 조각의 시작 시간)에서 연도, 월 및 일을 사용 하 고 파일 이름을 hello SliceStart에서에서 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="a0186-271">예를 들어, 2014에 대 한 조각이 생성 되는 경우-10-20T08:00:00, hello folderName toowikidatagateway/wikisampledataout/2014/10/20 설정 및 hello fileName too08.csv 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="a0186-272">JSON 속성에 대한 자세한 내용은 [Azure Blob Storage 간의 데이터 이동](data-factory-azure-blob-connector.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0186-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="a0186-273">클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="a0186-274">Hello 트리 보기에서 두 hello 데이터 집합에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="a0186-275">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="a0186-275">Create pipeline</span></span>
<span data-ttu-id="a0186-276">이 단계에서는 **EmpOnPremSQLTable**을 입력으로, **OutputBlobTable**을 출력으로 사용하는 **복사 작업**을 포함하는 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="a0186-277">[데이터 팩터리 편집기]에서 **... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="a0186-278">Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="a0186-279">Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="a0186-280">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="a0186-280">Note hello following points:</span></span>

   * <span data-ttu-id="a0186-281">Hello 활동 섹션에는 활동만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="a0186-282">**입력** hello 활동 너무 설정 되어**EmpOnPremSQLTable** 및 **출력** hello 활동 너무 설정 되어**OutputBlobTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="a0186-283">Hello에 **typeProperties** 섹션 **SqlSource** hello로 지정 된 **소스 형식** 및 * * BlobSink * * hello로 지정 된 **싱크 유형**.</span><span class="sxs-lookup"><span data-stu-id="a0186-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="a0186-284">SQL 쿼리 `select * from emp` hello에 대 한 지정 된 **sqlReaderQuery** 속성 **SqlSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="a0186-285">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="a0186-286">예: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="a0186-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="a0186-287">hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="a0186-288">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="a0186-289">toorun hello 파이프라인 무제한으로 지정 **9/9/9999** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="a0186-290">Hello hello에 따라 어떤 hello 데이터 조각이 처리 되는 시간 기간을 정의 하는 **가용성** 각 Azure 데이터 팩터리 데이터 집합에 대해 정의 된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="a0186-291">Hello 예제에서는 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="a0186-292">클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 (테이블 데이터 집합이 사각형).</span><span class="sxs-lookup"><span data-stu-id="a0186-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="a0186-293">Hello 파이프라인 hello 트리 보기 아래에 표시 확인 **파이프라인** 노드.</span><span class="sxs-lookup"><span data-stu-id="a0186-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="a0186-294">이제 클릭 **X** 두 번 tooclose hello 페이지 tooget 뒤로 toohello **Data Factory** hello에 대 한 페이지 **ADFTutorialOnPremDF**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="a0186-295">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0186-295">**Congratulations!**</span></span> <span data-ttu-id="a0186-296">Azure 데이터 팩터리에, 연결 된 서비스, 데이터 집합 및 파이프라인 및 예약 된 hello 파이프라인 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="a0186-297">다이어그램 보기에서 보기 hello 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="a0186-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="a0186-298">Hello에 **Azure 포털**, 클릭 **다이어그램** hello에 대 한 hello 홈 페이지에서 타일 **ADFTutorialOnPremDF** 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="a0186-299">:</span><span class="sxs-lookup"><span data-stu-id="a0186-299">:</span></span>

    ![다이어그램 링크](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="a0186-301">다음 이미지 hello 다이어그램 비슷한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-301">You should see hello diagram similar toohello following image:</span></span>

    ![다이어그램 뷰](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="a0186-303">확대, 축소, 확대/축소 too100%, toofit 확대/축소, 자동으로 위치 파이프라인 및 데이터 집합 및 계보 정보를 표시 합니다 (선택 된 항목의 업스트림 및 다운스트림 항목을 강조 표시).</span><span class="sxs-lookup"><span data-stu-id="a0186-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="a0186-304">에 대 한 개체 (입/출력 데이터 집합 또는 파이프라인) toosee 속성을 두 번 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="a0186-305">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="a0186-305">Monitor pipeline</span></span>
<span data-ttu-id="a0186-306">이 단계에서 진행 되는 상황에서 Azure 데이터 팩터리에 Azure 포털 toomonitor hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="a0186-307">PowerShell cmdlet toomonitor 집합과 파이프라인을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="a0186-308">모니터링에 대한 자세한 내용은 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0186-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="a0186-309">Hello 다이어그램에서 두 번 클릭 **EmpOnPremSQLTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable 조각](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="a0186-311">에 있는 모든 hello 데이터 조각이를 사라졌는지 **준비** hello 지난 hello 파이프라인 기간 (시작 시간 tooend 시간) 중 이므로 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="a0186-312">Hello 데이터 hello SQL Server 데이터베이스에 삽입 한 모든 hello 시간 거기 때문 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="a0186-313">조각이 없습니다 hello에 표시 되는지 확인 **문제 조각** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0186-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="a0186-314">tooview 모든 hello 분할 영역 클릭 **더 참조** hello 조각 hello 목록 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="a0186-315">Hello에 이제 **데이터 집합** 페이지 **OutputBlobTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable 조각](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="a0186-317">Hello 목록에서 데이터 조각을 아무 것 이나 클릭 하 고 hello 표시 되어야 **데이터 조각을** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a0186-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="a0186-318">Hello 조각에 대 한 활동을 실행 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="a0186-319">일반적으로 하나의 작업 실행만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-319">You see only one activity run usually.</span></span>  

    ![데이터 조각 블레이드](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="a0186-321">Hello 조각 hello에 없는 경우 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않은 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="a0186-322">Hello 클릭 **작업 실행** hello 아래쪽 toosee에 hello 목록에서 **활동 실행 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![작업 실행 세부 정보 페이지](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="a0186-324">사용 되는 tootransfer hello 데이터 처리량, 기간 및 hello 게이트웨이 같은 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="a0186-325">클릭 **X** tooclose 할 때까지 페이지 hello 모든</span><span class="sxs-lookup"><span data-stu-id="a0186-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="a0186-326">hello에 대 한 toohello 홈 페이지를 다시 가져오기 **ADFTutorialOnPremDF**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="a0186-327">(선택 사항) **파이프라인**, **ADFTutorialOnPremDF**를 차례로 클릭한 다음 입력 데이터 집합(**Consumed**) 또는 출력 데이터 집합(**Produced**)을 드릴스루합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="a0186-328">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) tooverify blob/파일 각 시간에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Azure Storage 탐색기](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="a0186-330">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0186-330">Next steps</span></span>
* <span data-ttu-id="a0186-331">참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 모든 hello 데이터 관리 게이트웨이 hello에 대 한 세부 정보에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="a0186-332">참조 [Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn toouse 복사 작업 toomove 데이터를 원본 데이터에서에서 tooa 싱크 데이터 저장소를 저장 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0186-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
