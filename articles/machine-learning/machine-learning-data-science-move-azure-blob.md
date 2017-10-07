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
# <a name="move-data-tooand-from-azure-blob-storage"></a>Azure Blob 저장소에서 데이터 tooand 이동
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

가장 적합한 방법은 시나리오에 따라 달라집니다. hello [Azure 기계 학습에서 고급 분석에 대 한 시나리오](machine-learning-data-science-plan-sample-scenarios.md) 문서를 사용 하면 다양 한 고급 분석 프로세스 hello에 사용 되는 데이터 과학 워크플로에 필요한 hello 리소스를 결정 합니다.

> [!NOTE]
> 전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.
> 
> 

또는 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 를 사용하여 다음을 수행할 수 있습니다. 

* Azure blob 저장소의 데이터를 다운로드하는 파이프라인 만들기 및 예약 
* 전달 tooa Azure 기계 학습 웹 서비스 게시 
* hello 예측 분석 결과 수신 하 고 
* hello 결과 toostorage를 업로드 합니다. 

자세한 내용은 [Azure 데이터 팩터리 및 Azure 기계 학습을 사용하여 예측 파이프라인 만들기](../data-factory/data-factory-azure-ml-batch-execution-activity.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다. 데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.

* 한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* 저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.

