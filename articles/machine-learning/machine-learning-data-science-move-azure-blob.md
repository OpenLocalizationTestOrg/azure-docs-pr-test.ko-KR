---
title: "Azure Blob 저장소에서 데이터 tooand aaaMove | Microsoft Docs"
description: "Azure Blob 저장소에서 데이터 tooand 이동"
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
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="3e26f-103">Azure Blob 저장소에서 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="3e26f-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="3e26f-104">가장 적합한 방법은 시나리오에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="3e26f-105">hello [Azure 기계 학습에서 고급 분석에 대 한 시나리오](machine-learning-data-science-plan-sample-scenarios.md) 문서를 사용 하면 다양 한 고급 분석 프로세스 hello에 사용 되는 데이터 과학 워크플로에 필요한 hello 리소스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="3e26f-106">전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="3e26f-107">또는 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="3e26f-108">Azure blob 저장소의 데이터를 다운로드하는 파이프라인 만들기 및 예약</span><span class="sxs-lookup"><span data-stu-id="3e26f-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="3e26f-109">전달 tooa Azure 기계 학습 웹 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="3e26f-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="3e26f-110">hello 예측 분석 결과 수신 하 고</span><span class="sxs-lookup"><span data-stu-id="3e26f-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="3e26f-111">hello 결과 toostorage를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="3e26f-112">자세한 내용은 [Azure 데이터 팩터리 및 Azure 기계 학습을 사용하여 예측 파이프라인 만들기](../data-factory/data-factory-azure-ml-batch-execution-activity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26f-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e26f-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e26f-113">Prerequisites</span></span>
<span data-ttu-id="3e26f-114">이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="3e26f-115">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="3e26f-116">한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e26f-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3e26f-117">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e26f-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

