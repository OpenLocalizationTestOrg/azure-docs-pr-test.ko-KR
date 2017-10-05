---
title: "Azure Blob Storage 간 데이터 이동 | Microsoft Docs"
description: "Azure Blob 저장소의 데이터 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="71734-103">Azure Blob Storage 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="71734-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="71734-104">가장 적합한 방법은 시나리오에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="71734-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="71734-105">[Azure 기계 학습의 고급 분석 시나리오](machine-learning-data-science-plan-sample-scenarios.md) 문서는 고급 분석 프로세스에서 사용되는 다양한 데이터 과학 워크플로에 필요한 리소스를 결정하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="71734-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="71734-106">Azure Blob Storage에 대한 전체 소개 내용은 [Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71734-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="71734-107">또는 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71734-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="71734-108">Azure blob 저장소의 데이터를 다운로드하는 파이프라인 만들기 및 예약</span><span class="sxs-lookup"><span data-stu-id="71734-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="71734-109">게시된 Azure 기계 학습 웹 서비스에 전달</span><span class="sxs-lookup"><span data-stu-id="71734-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="71734-110">예측 분석 결과 수신</span><span class="sxs-lookup"><span data-stu-id="71734-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="71734-111">결과를 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="71734-111">upload the results to storage.</span></span> 

<span data-ttu-id="71734-112">자세한 내용은 [Azure 데이터 팩터리 및 Azure 기계 학습을 사용하여 예측 파이프라인 만들기](../data-factory/data-factory-azure-ml-batch-execution-activity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71734-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71734-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="71734-113">Prerequisites</span></span>
<span data-ttu-id="71734-114">이 문서에서는 사용자에게 Azure 구독, 저장소 계정 및 계정에 해당하는 저장소 키가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="71734-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="71734-115">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71734-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="71734-116">Azure 구독을 설정하려면 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71734-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="71734-117">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71734-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

