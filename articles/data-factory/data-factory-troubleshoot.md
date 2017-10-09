---
title: "aaaTroubleshoot Azure Data Factory 문제"
description: "Azure 데이터 팩터리를 사용 하 여 tootroubleshoot 발급 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="1ae12-103">데이터 팩터리 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1ae12-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="1ae12-104">이 문서에서는 Azure Data Factory 사용 시 발생하는 문제에 대한 문제 해결 팁을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="1ae12-105">이 문서에 나열 되지 hello 문제가 모두 hello 서비스를 사용할 때 않지만 일부 문제 및 일반적인 문제 해결 팁을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="1ae12-106">문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="1ae12-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="1ae12-107">오류: hello 등록은 등록된 toouse 네임 스페이스가 'microsoft.datafactory 가' 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="1ae12-108">이 오류가 나타나면 hello Azure Data Factory 리소스 공급자 컴퓨터에 등록 된 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="1ae12-109">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-109">Do hello following:</span></span>

1. <span data-ttu-id="1ae12-110">Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="1ae12-111">다음 명령을 hello를 사용 하 여 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="1ae12-112">Hello 명령 tooregister hello Azure 데이터 팩터리 공급자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="1ae12-113">문제: 데이터 팩터리 cmdlet을 실행할 때 권한 없음 오류 발생</span><span class="sxs-lookup"><span data-stu-id="1ae12-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="1ae12-114">Hello Azure PowerShell로 하지 못할 hello 오른쪽 Azure 계정 또는 구독을 사용 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="1ae12-115">다음 cmdlet tooselect hello 오른쪽 hello Azure PowerShell로 Azure 계정과 구독 toouse hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="1ae12-116">로그인 AzureRmAccount-사용 하 여 hello 올바른 사용자 ID 및 암호</span><span class="sxs-lookup"><span data-stu-id="1ae12-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="1ae12-117">Get AzureRmSubscription-모든 hello hello 계정에 대 한 구독 보기.</span><span class="sxs-lookup"><span data-stu-id="1ae12-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="1ae12-118">선택 AzureRmSubscription &lt;구독 이름&gt; -hello 오른쪽 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="1ae12-119">사용 하 여 hello 동일한 hello Azure 포털에서 toocreate 데이터 팩터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="1ae12-120">문제: Azure 포털에서 toolaunch 데이터 관리 게이트웨이 Express 설치 실패</span><span class="sxs-lookup"><span data-stu-id="1ae12-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="1ae12-121">데이터 관리 게이트웨이 hello에 대 한 hello Express 설치에는 Internet Explorer 나 Microsoft ClickOnce 호환 웹 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="1ae12-122">Hello Express 설치 프로그램에 실패 하면 toostart hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="1ae12-123">Internet Explorer 또는 Microsoft ClickOnce 호환 웹 브라우저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="1ae12-124">Chrome을 사용 하는 경우 이동 toohello [크롬 웹 저장소](https://chrome.google.com/webstore/), "ClickOnce" 키워드를 사용 하 여 검색, hello ClickOnce 확장 중 하나를 선택 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="1ae12-125">Firefox (설치 추가 기능에서)에 대 한 마십시오 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="1ae12-126">Hello 도구 모음 (세 개의 가로선 hello 오른쪽 위 모서리에)에 열기 메뉴 단추를 클릭, 추가 기능을 클릭, "ClickOnce" 키워드를 사용 하 여 검색, hello ClickOnce 확장 중 하나를 선택 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="1ae12-127">사용 하 여 hello **수동 설치** hello에 표시 된 링크 hello 포털에서 동일한 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="1ae12-128">이 접근 방식을 toodownload 설치 파일을 사용 하 고이 정보를 수동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="1ae12-129">Hello 설치에 성공한 후 hello 데이터 관리 게이트웨이 구성 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="1ae12-130">복사 hello **키** hello 포털 화면 및 hello 게이트웨이 hello 서비스를 등록 하는 configuration manager toomanually hello에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="1ae12-131">문제: 실패 tooconnect tooon 온-프레미스 SQL Server</span><span class="sxs-lookup"><span data-stu-id="1ae12-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="1ae12-132">시작 **데이터 관리 게이트웨이 구성 관리자** 게이트웨이 컴퓨터 hello 되 고 hello를 사용 하 여 **문제 해결** tootest hello 연결 tooSQL 서버 hello 게이트웨이 컴퓨터에서를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="1ae12-133">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="1ae12-134">문제: 입력 조각이 무기한 대기 상태임</span><span class="sxs-lookup"><span data-stu-id="1ae12-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="1ae12-135">hello 분할 영역에 있을 수 **대기** toovarious 이유로 인해 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="1ae12-136">Hello 일반적인 이유 중 하나는 해당 hello **외부** 속성이 너무 설정 되지 않은**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="1ae12-137">Azure Data Factory의 생성 된 외부 hello 범위가 있는 데이터 집합으로 표시 해야 **외부** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="1ae12-138">이 속성 hello 데이터가 외부 및 hello 데이터 팩터리 내 모든 파이프라인에서 백업 되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="1ae12-139">hello 데이터 조각으로 표시 된 **준비** hello 각 스토어에서 hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="1ae12-140">다음의 hello hello 사용에 대 한 예제는 hello 참조 **외부** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="1ae12-141">선택적으로 지정할 수 **externalData*** 외부 tootrue를 설정 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1ae12-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="1ae12-142">이 속성에 대한 자세한 내용은 [데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="1ae12-143">tooresolve 오류 hello, hello 추가 **외부** 속성과 선택적 hello **externalData** hello 입력된 테이블의 toohello JSON 정의 섹션 및 hello 테이블을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="1ae12-144">문제: 하이브리드 복사 작업 실패</span><span class="sxs-lookup"><span data-stu-id="1ae12-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="1ae12-145">참조 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) tootroubleshoot 문제/온-프레미스 데이터에서 복사를 사용 하 여 저장 하는 단계는 데이터 관리 게이트웨이 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="1ae12-146">문제: 주문형 HDInsight 프로비전 실패</span><span class="sxs-lookup"><span data-stu-id="1ae12-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="1ae12-147">HDInsightOnDemand 형식의 연결 된 서비스를 사용 하 여 toospecify tooan Azure Blob 저장소를 가리키는 linkedServiceName가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="1ae12-148">데이터 팩터리 서비스에서는 주문형 HDInsight 클러스터에 대 한이 저장소 toostore 로그 및 지원 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="1ae12-149">다음 오류가 hello로 주문형 HDInsight 클러스터의 경우에 따라 프로 비전에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="1ae12-150">이 오류는 일반적으로 hello linkedServiceName에 지정 된 hello 저장소 계정의 hello 위치 hello에 있지 않음을 나타냅니다 동일한 데이터 센터 위치 hello HDInsight 프로 비전 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="1ae12-151">미국 서 부에 데이터 팩터리 hello Azure 저장소에 있는 경우 미국 동부, 예: hello West US에 주문형으로 프로 비전 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="1ae12-152">또한 주문형 HDInsight에서 추가 저장소 계정을 지정할 수 있는 두 번째 JSON 속성 additionalLinkedServiceNames가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="1ae12-153">이러한 추가 연결 된 저장소 계정을 hello로 hello 실패 하거나 hello HDInsight 클러스터와 동일한 위치에에서 있어야 합니다. 동일한 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ae12-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="1ae12-154">문제: 사용자 지정 .NET 작업 실패</span><span class="sxs-lookup"><span data-stu-id="1ae12-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="1ae12-155">자세한 단계는 [사용자 지정 작업을 사용하여 파이프라인 디버그](data-factory-use-custom-activities.md#troubleshoot-failures) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="1ae12-156">Azure 포털 tootroubleshoot 사용</span><span class="sxs-lookup"><span data-stu-id="1ae12-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="1ae12-157">포털 블레이드 사용</span><span class="sxs-lookup"><span data-stu-id="1ae12-157">Using portal blades</span></span>
<span data-ttu-id="1ae12-158">단계는 [파이프라인 모니터링](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="1ae12-159">모니터링 및 관리 앱 사용</span><span class="sxs-lookup"><span data-stu-id="1ae12-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="1ae12-160">자세한 내용은 [모니터링 및 관리 앱을 사용하여 데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="1ae12-161">Azure PowerShell tootroubleshoot를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1ae12-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="1ae12-162">Azure PowerShell tootroubleshoot 오류를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1ae12-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="1ae12-163">자세한 내용은 [Azure PowerShell을 사용하여 Data Factory 파이프라인 모니터링](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ae12-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
