---
title: "Azure 데이터 팩터리 문제 해결"
description: "Azure 데이터 팩터리 사용과 관련된 문제를 해결하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="9951e-103">데이터 팩터리 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9951e-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="9951e-104">이 문서에서는 Azure Data Factory 사용 시 발생하는 문제에 대한 문제 해결 팁을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="9951e-105">여기서는 서비스 사용 중 발생할 수 있는 모든 문제를 다루지는 않으며, 몇 가지 문제와 일반적인 문제 해결 팁을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="9951e-106">문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="9951e-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="9951e-107">오류: 구독이 'Microsoft.DataFactory' 네임스페이스를 사용하도록 등록되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="9951e-108">이 오류가 발생하는 경우 Azure Data Factory 리소스 공급자가 컴퓨터에 등록되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="9951e-109">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-109">Do the following:</span></span>

1. <span data-ttu-id="9951e-110">Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="9951e-111">다음 명령을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="9951e-112">다음 명령을 실행하여 Azure Data Factory 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="9951e-113">문제: 데이터 팩터리 cmdlet을 실행할 때 권한 없음 오류 발생</span><span class="sxs-lookup"><span data-stu-id="9951e-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="9951e-114">Azure PowerShell에서 올바른 Azure 계정 또는 구독을 사용하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="9951e-115">다음 cmdlet을 사용하여 Azure PowerShell에서 사용할 올바른 Azure 계정 및 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="9951e-116">Login-AzureRmAccount - 올바른 사용자 ID 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="9951e-117">Get-AzureRmSubscription - 계정의 모든 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="9951e-118">Select-AzureRmSubscription &lt;구독 이름&gt; - 올바른 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="9951e-119">Azure 포털에서 데이터 팩터리를 만드는 데 사용한 것과 동일한 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="9951e-120">문제: Azure 포털에서 데이터 관리 게이트웨이 빠른 설치를 시작하지 못함</span><span class="sxs-lookup"><span data-stu-id="9951e-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="9951e-121">데이터 관리 게이트웨이 빠른 설치를 수행하려면 Internet Explorer 또는 Microsoft ClickOnce 호환 웹 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="9951e-122">빠른 설치를 시작할 수 없는 경우 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="9951e-123">Internet Explorer 또는 Microsoft ClickOnce 호환 웹 브라우저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="9951e-124">Chrome을 사용하는 경우 [Chrome 웹 스토어](https://chrome.google.com/webstore/)로 이동하여 "ClickOnce" 키워드로 검색하고 ClickOnce 확장 중 하나를 선택해 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="9951e-125">Firefox의 경우에도 동일한 작업을 수행합니다(추가 기능 설치).</span><span class="sxs-lookup"><span data-stu-id="9951e-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="9951e-126">도구 모음(상단 오른쪽 모서리의 가로 줄 세 개)의 열기 메뉴 단추를 클릭하고 추가 기능을 클릭하고 "ClickOnce" 키워드로 검색하고 ClickOnce 확장 중 하나를 선택하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="9951e-127">포털의 같은 블레이드에 표시되어 있는 **수동 설치** 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="9951e-128">이 방식을 사용하여 설치 파일을 다운로드해 수동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="9951e-129">설치가 정상적으로 완료되면 데이터 관리 게이트웨이 구성 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="9951e-130">포털 화면에서 **키** 를 복사하고 구성 관리자에서 이 키를 사용하여 게이트웨이를 서비스에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="9951e-131">문제: 온-프레미스 SQL Server에 연결하지 못함</span><span class="sxs-lookup"><span data-stu-id="9951e-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="9951e-132">게이트웨이 컴퓨터에서 **데이터 관리 게이트웨이 구성 관리자**를 시작하고 **문제 해결** 탭을 사용하여 게이트웨이 컴퓨터에서 SQL Server에 대한 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="9951e-133">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="9951e-134">문제: 입력 조각이 무기한 대기 상태임</span><span class="sxs-lookup"><span data-stu-id="9951e-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="9951e-135">이 조각은 다양한 이유로 인해 **대기 중** 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="9951e-136">일반적으로는 **external** 속성이 **true**로 설정되어 있지 않으면 이러한 상태가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="9951e-137">Azure Data Factory 범위 외에서 생성된 데이터 집합은 **external** 속성으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="9951e-138">이 속성은 데이터가 외부에 있으며 데이터 팩터리 내의 파이프라인에서 지원되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="9951e-139">해당 저장소에서 데이터를 사용할 수 있으면 데이터 조각이 **Ready** 로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="9951e-140">**external** 속성의 사용 방법은 다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="9951e-141">external을 true로 설정할 경우 선택적으로 **externalData***를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="9951e-142">이 속성에 대한 자세한 내용은 [데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="9951e-143">오류를 해결하려면 입력 테이블의 JSON 정의에 **external** 속성과 **externalData** 섹션을 추가하고 테이블을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="9951e-144">문제: 하이브리드 복사 작업 실패</span><span class="sxs-lookup"><span data-stu-id="9951e-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="9951e-145">데이터 관리 게이트웨이를 사용하여 온-프레미스 데이터 저장소 간 복사 작업에서 발생하는 문제를 해결하는 단계는 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="9951e-146">문제: 주문형 HDInsight 프로비전 실패</span><span class="sxs-lookup"><span data-stu-id="9951e-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="9951e-147">HDInsightOnDemand 형식의 연결된 서비스를 사용하는 경우 Azure Blob 저장소를 가리키는 linkedServiceName을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="9951e-148">Data Factory 서비스는 이 저장소를 사용하여 주문형 HDInsight 클러스터에 대한 모든 로그 및 지원 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="9951e-149">경우에 따라 다음 오류와 함께 주문형 HDInsight 클러스터 프로비전이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="9951e-150">이 오류는 일반적으로 linkedServiceName에 지정된 저장소 계정의 위치가 HDInsight 프로비전이 발생하는 위치와 동일한 데이터 센터 위치에 있지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="9951e-151">예: 데이터 팩터리는 미국 서부에 있고 Azure Storage는 미국 동부에 있는 경우 미국 서부에서 주문형 프로비전이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="9951e-152">또한 주문형 HDInsight에서 추가 저장소 계정을 지정할 수 있는 두 번째 JSON 속성 additionalLinkedServiceNames가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="9951e-153">이러한 추가 연결된 저장소 계정은 HDInsight 클러스터와 동일한 위치에 있어야 합니다. 그렇지 않으면 동일한 오류가 발생하여 프로비저닝이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9951e-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="9951e-154">문제: 사용자 지정 .NET 작업 실패</span><span class="sxs-lookup"><span data-stu-id="9951e-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="9951e-155">자세한 단계는 [사용자 지정 작업을 사용하여 파이프라인 디버그](data-factory-use-custom-activities.md#troubleshoot-failures) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="9951e-156">Azure 포털을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9951e-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="9951e-157">포털 블레이드 사용</span><span class="sxs-lookup"><span data-stu-id="9951e-157">Using portal blades</span></span>
<span data-ttu-id="9951e-158">단계는 [파이프라인 모니터링](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="9951e-159">모니터링 및 관리 앱 사용</span><span class="sxs-lookup"><span data-stu-id="9951e-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="9951e-160">자세한 내용은 [모니터링 및 관리 앱을 사용하여 데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="9951e-161">Azure PowerShell을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9951e-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="9951e-162">Azure PowerShell을 사용하여 오류 해결</span><span class="sxs-lookup"><span data-stu-id="9951e-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="9951e-163">자세한 내용은 [Azure PowerShell을 사용하여 Data Factory 파이프라인 모니터링](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9951e-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
