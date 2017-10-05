---
title: "Miscrosoft Azure 진단을 사용하여 Azure Service Fabric 이벤트 집계 | Microsoft Docs"
description: "Azure Service Fabric 클러스터 모니터링 및 진단을 위해 MAD를 사용하여 이벤트를 집계 및 수집하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="163d0-103">Miscrosoft Azure 진단을 사용하여 이벤트 집계 및 수집</span><span class="sxs-lookup"><span data-stu-id="163d0-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="163d0-104">Windows</span><span class="sxs-lookup"><span data-stu-id="163d0-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="163d0-105">Linux</span><span class="sxs-lookup"><span data-stu-id="163d0-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="163d0-106">Azure 서비스 패브릭 클러스터를 실행할 때 모든 노드의 로그를 중앙 위치에 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="163d0-107">중앙 위치에 로그를 두면 클러스터나 해당 클러스터에서 실행 중인 응용 프로그램 및 서비스의 문제를 분석하고 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="163d0-108">로그를 업로드 및 수집하는 방법 중 하나는 MAD(Microsoft Azure 진단) 확장을 사용하는 것입니다. 이 확장을 사용하면 Azure Storage에 로그를 업로드하고 Azure Application Insights 또는 Event Hubs에 로그를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="163d0-109">또한 외부 프로세스를 사용하여 저장소의 이벤트를 읽고 [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) 또는 기타 로그 구문 분석 솔루션 등의 분석 플랫폼 제품에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="163d0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="163d0-110">Prerequisites</span></span>
<span data-ttu-id="163d0-111">이러한 도구는 이 문서의 일부 작업을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="163d0-112">[Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md)(Azure Cloud Services와 관련이 있지만 여러 좋은 정보와 예 제공)</span><span class="sxs-lookup"><span data-stu-id="163d0-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="163d0-113">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="163d0-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="163d0-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="163d0-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="163d0-115">Azure Resource Manager 클라이언트</span><span class="sxs-lookup"><span data-stu-id="163d0-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="163d0-116">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="163d0-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="163d0-117">로그 및 이벤트 원본</span><span class="sxs-lookup"><span data-stu-id="163d0-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="163d0-118">Service Fabric 플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="163d0-118">Service Fabric platform events</span></span>
<span data-ttu-id="163d0-119">[이 문서](service-fabric-diagnostics-event-generation-infra.md)의 설명대로 Service Fabric은 WAD를 사용하여 모니터링 및 진단 데이터를 저장소 테이블이나 다른 곳에 보내도록 다음 채널을 쉽게 구성할 수 있는 몇 가지 기본 제공 로깅 채널을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="163d0-120">작업 이벤트: Service Fabric 플랫폼이 수행하는 상위 수준 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="163d0-121">응용 프로그램 및 서비스 만들기, 노드 상태 변경, 업그레이드 정보 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="163d0-122">이러한 이벤트를 ETW(Windows용 이벤트 추적) 로그로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="163d0-123">Reliable Actors 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="163d0-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="163d0-124">Reliable Services 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="163d0-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="163d0-125">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="163d0-125">Application events</span></span>
 <span data-ttu-id="163d0-126">응용 프로그램 및 서비스 코드에서 발생하며 Visual Studio에서 제공하는 EventSource 도우미 클래스를 사용하여 작성된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="163d0-127">응용 프로그램에서 EventSource 로그를 작성하는 방법에 대한 자세한 내용은 [로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="163d0-128">진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="163d0-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="163d0-129">로그를 수집하는 첫 단계는 서비스 패브릭 클러스터의 각 VM에 진단 확장을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="163d0-130">진단 확장은 각 VM에서 로그를 수집하여 사용자가 지정하는 저장소 계정에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="163d0-131">단계는 Azure Portal 또는 Azure Resource Manager 사용 여부에 따라 약간 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="163d0-132">또한 배포가 클러스터 생성의 일부인지 아니면 이미 있는 클러스터에 대한 것인지에 따라서도 단계가 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="163d0-133">각 시나리오에 대한 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="163d0-134">Azure Portal을 통해 클러스터 만들기의 일환으로 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="163d0-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="163d0-135">클러스터 만들기의 일부로 클러스터의 VM에 진단 확장을 배포하려면 다음 이미지에 표시된 진단 설정 패널을 사용합니다. [진단]이 **켜기**(기본 설정)로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="163d0-136">클러스터를 만든 후에는 포털을 사용하여 이러한 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![클러스터를 만들기 위해 포털에서 Azure 진단 설정](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="163d0-138">포털을 사용하여 클러스터를 만드는 경우 클러스터를 만들기 위해 **확인을 클릭하기 전에** 템플릿을 다운로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="163d0-139">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 Service Fabric 클러스터 설정](service-fabric-cluster-creation-via-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="163d0-140">일부는 포털을 사용하여 변경할 수 없으므로 나중에 변경하려면 템플릿이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="163d0-141">Azure 리소스 관리자를 사용하여 클러스터 만들기의 일환으로 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="163d0-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="163d0-142">리소스 관리자를 사용하여 클러스터를 만들려면 클러스터를 만들기 전에 진단 구성 JSON을 전체 클러스터 Resource Manager 템플릿에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="163d0-143">Resource Manager 템플릿 샘플의 일부로 진단 구성이 추가된 샘플 5VM 클러스터 Resource Manager 템플릿이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="163d0-144">Azure 샘플 갤러리의 [진단 Resource Manager 템플릿 샘플이 포함된 5노드 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)에서 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="163d0-145">Resource Manager 템플릿에서 진단 설정을 표시하려면 azuredeploy.json 파일을 열고 **IaaSDiagnostics**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="163d0-146">이 템플릿을 사용하여 클러스터를 만들려면 이전 링크에 제공된 **Azure에 배포** 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="163d0-147">또는 리소스 관리자 샘플을 다운로드하여 변경한 후 Azure PowerShell 창에서 `New-AzureRmResourceGroupDeployment` 명령을 사용하여 수정된 템플릿으로 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="163d0-148">명령에 전달할 매개 변수는 다음 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="163d0-149">PowerShell을 사용하여 리소스 그룹을 배포하는 방법에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 리소스 그룹 배포](../azure-resource-manager/resource-group-template-deploy.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="163d0-150">기존 클러스터에 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="163d0-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="163d0-151">진단이 배포되지 않은 기존 클러스터가 있거나 기존 구성을 수정하려는 경우 기존 클러스터를 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="163d0-152">기존 클러스터를 만드는 데 사용되는 Resource Manager 템플릿을 수정하거나 앞의 설명대로 포털에서 템플릿을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="163d0-153">다음 작업을 수행하여 template.json 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="163d0-154">리소스 섹션에 추가하여 새 저장소 리소스를 템플릿에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-154">Add a new storage resource to the template by adding to the resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="163d0-155">저장소 계정 정의 바로 뒤 `supportLogStorageAccountName`과 `vmNodeType0Name` 사이의 매개 변수 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="163d0-156">자리 표시자 텍스트 *storage account name goes here*를 저장소 계정의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="163d0-157">그런 다음 확장 배열 내에 다음 코드를 추가하여 template.json의 `VirtualMachineProfile` 섹션을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="163d0-158">삽입되는 위치에 따라 시작 부분 또는 끝 부분에 쉼표를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="163d0-159">template.json 파일을 설명대로 수정한 후에는 Resource Manager 템플릿을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="163d0-160">템플릿을 내보낸 후 deploy.ps1 파일을 실행하면 템플릿이 다시 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="163d0-161">배포 후에는 **ProvisioningState**가 **성공**했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="163d0-162">상태 및 부하 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="163d0-162">Collect health and load events</span></span>

<span data-ttu-id="163d0-163">Service Fabric 5.4 버전부터 상태 및 부하 메트릭 이벤트를 컬렉션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="163d0-164">이러한 이벤트는 시스템이나 코드에서 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 또는 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx) 등의 상태 또는 부하 보고 API를 사용하여 시스템 또는 코드에서 생성한 이벤트를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="163d0-165">이를 통해 시간 경과에 따른 시스템 상태의 집계 및 확인과 상태 또는 부하 이벤트 기반의 경고가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="163d0-166">Visual Studio의 Diagnostic Event Viewer에서 이 이벤트를 보려면 ETW 공급자 목록에 "Microsoft-ServiceFabric:4:0x4000000000000008"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="163d0-167">이벤트를 수집하려면 Resource Manager 템플릿을 수정하여 다음을 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-167">To collect the events, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="163d0-168">역방향 프록시 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="163d0-168">Collect reverse proxy events</span></span>

<span data-ttu-id="163d0-169">Service Fabric 5.7 릴리스부터 [역방향 프록시](service-fabric-reverseproxy.md) 이벤트를 컬렉션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="163d0-170">역방향 프록시는 요청 처리 실패를 나타내는 오류 이벤트가 담긴 채널 하나와, 역방향 프록시에서 처리된 모든 요청에 대한 상세 정보가 담긴 채널 하나 등, 두 채널로 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="163d0-171">오류 이벤트 수집: Visual Studio의 Diagnostic Event Viewer에서 이 이벤트를 보려면 ETW 공급자 목록에 "Microsoft-ServiceFabric:4:0x4000000000000010"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="163d0-172">Azure 클러스터에서 이벤트를 수집하려면 Resource Manager 템플릿을 수정하여 다음을 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="163d0-173">모든 요청 처리 이벤트 수집: Visual Studio의 진단 이벤트 뷰어에서 ETW 공급자 목록의 Microsoft-ServiceFabric 항목을 "Microsoft-ServiceFabric:4:0x4000000000000020"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="163d0-174">Azure Service Fabric 클러스터의 경우 Resource Manager 템플릿을 수정하여 다음을 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="163d0-175">여기서는 역방향 프록시를 통과하는 모든 트래픽을 수집하여 저장소 용량을 신속하게 소비할 수 있으므로 이 채널을 통한 이벤트 수집을 활성화할 때는 주의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="163d0-176">Azure Service Fabric 클러스터의 경우 모든 노드의 이벤트가 SystemEventTable에 수집되어 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="163d0-177">역방향 프록시 이벤트의 문제 해결에 관한 자세한 내용은 [역방향 프록시 진단 가이드](service-fabric-reverse-proxy-diagnostics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="163d0-178">새 EventSource 채널에서 수집</span><span class="sxs-lookup"><span data-stu-id="163d0-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="163d0-179">배포하려는 새 응용 프로그램을 나타내는 새 EventSource 채널에서 로그를 수집하도록 진단을 업데이트하려면 기존 클러스터에 대한 이전 설명과 동일한 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="163d0-180">새 EventSource 채널의 항목을 추가하도록 template.json 파일의 `EtwEventSourceProviderConfiguration` 섹션을 업데이트한 후 `New-AzureRmResourceGroupDeployment` PowerShell 명령을 사용하여 구성 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="163d0-181">이벤트 원본의 이름은 ServiceEventSource.cs 파일을 생성한 Visual Studio에서 코드의 일부로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="163d0-182">예를 들어 이벤트 원본의 이름을 Eventsource라고 지정한 경우 My-Eventsource의 이벤트를 MyDestinationTableName이라는 테이블에 배치하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="163d0-183">성능 카운터 또는 이벤트 로그를 수집하려면 [Azure Resource Manager 템플릿을 사용하여 모니터링 및 진단이 포함된 Windows 가상 컴퓨터 만들기](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 제공된 예제를 사용하여 Resource Manager 템플릿을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="163d0-184">그런 다음 Resource Manager 템플릿을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="163d0-185">성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="163d0-185">Collect Performance Counters</span></span>

<span data-ttu-id="163d0-186">클러스터에서 성능 메트릭을 수집하려면 클러스터에 대한 Resource Manager 템플릿에서 "WadCfg > DiagnosticMonitorConfiguration"에 성능 카운터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="163d0-187">수집을 권장하는 성능 카운터에 대해서는 [Service Fabric 성능 카운터](service-fabric-diagnostics-event-generation-perf.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="163d0-188">예를 들어, 여기서는 15초마다 샘플링되고(이 값은 변경될 수 있고 "PT\<시간>\<단위>" 형식이 적용됨. 예를 들어 PT3M은 3분 간격으로 샘플링됨) 1분마다 적절한 저장소 테이블에 전송되는 하나의 성능 카운터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="163d0-189">아래 섹션에 설명된 대로 Application Insights 싱크를 사용하고 있을 때 이러한 메트릭을 Application Insights에 표시하려면 위에 표시된 대로 "sinks" 섹션에 싱크 이름을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="163d0-190">또한 성능 카운터를 보낼 별도의 테이블을 만들어 보세요. 그러면 성능 카운터는 사용하도록 설정한 다른 로깅 채널에서 들어오는 데이터를 밀어내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="163d0-191">Application Insights에 로그 보내기</span><span class="sxs-lookup"><span data-stu-id="163d0-191">Send logs to Application Insights</span></span>

<span data-ttu-id="163d0-192">WAD 구성의 일부로 모니터링 및 진단 데이터를 AI(Application Insights)에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="163d0-193">이벤트 분석 및 시각화에 AI를 사용하도록 결정할 경우 "WadCfg"의 일부로 AI 싱크를 설정하려면 [Application Insights를 사용하여 이벤트 분석 및 시각화](service-fabric-diagnostics-event-analysis-appinsights.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="163d0-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="163d0-194">Next steps</span></span>

<span data-ttu-id="163d0-195">Azure 진단을 제대로 구성하면 저장소 테이블에서 ETW 및 EventSource 로그의 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="163d0-196">OMS 또는 Kibana를 사용하거나 Resource Manager 템플릿에서 직접 구성되지 않은 기타 데이터 분석 및 시각화 플랫폼을 사용하도록 선택할 경우 선택한 플랫폼이 이러한 저장소 테이블에서 데이터를 읽도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="163d0-197">OMS에 대해 이 작업을 수행하는 방법은 비교적 간단하고 [OMS를 통해 이벤트 및 로그 분석](service-fabric-diagnostics-event-analysis-oms.md)에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="163d0-198">Application Insights는 진단 확장 구성의 일부로 구성될 수 있으므로 이런 의미에서 약간 특별한 경우입니다. 따라서 AI를 사용하도록 선택할 경우 [관련 문서](service-fabric-diagnostics-event-analysis-appinsights.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163d0-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="163d0-199">현재 테이블로 전송되는 이벤트를 필터링하거나 영구 제거할 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="163d0-200">테이블에서 이벤트를 제거하는 프로세스를 구현하지 않으면 테이블이 계속 커집니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="163d0-201">현재 [Watchdog 샘플](https://github.com/Azure-Samples/service-fabric-watchdog-service)에서 실행되는 데이터 그루밍 서비스의 예제가 있고, 30일 또는 90일 넘어서 로그를 저장해야 하는 적절한 이유가 없다면 직접 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="163d0-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="163d0-202">진단 확장을 사용하여 성능 카운터 또는 로그를 수집하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="163d0-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="163d0-203">Application Insights를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="163d0-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="163d0-204">OMS를 사용하여 이벤트 분석 및 시각화</span><span class="sxs-lookup"><span data-stu-id="163d0-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)