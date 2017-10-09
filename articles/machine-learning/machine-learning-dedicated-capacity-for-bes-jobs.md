---
title: "시스템 학습 일괄 처리 실행 서비스 작업에 대 한 용량 aaaDedicated | Microsoft Docs"
description: "Machine Learning 작업에 대한 Azure 배치 서비스 개요입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Machine Learning 작업에 대한 Azure 배치 서비스

Hello Azure 컴퓨터 학습 배치 실행 서비스에 대 한 고객이 관리 하는 소수 자릿수를 제공 하는 컴퓨터 학습 배치 풀을 처리 합니다. 클래식 일괄 기계 학습에 대 한 처리는 선입 선출 별로 제한 hello 번호를 제출할 수 있습니다 및 작업의 동시 작업의 대기 중인는 다중 테 넌 트 환경에서 수행 합니다. 이 불확실성은 작업이 실행되는 시기를 예측할 수 없다는 것입니다.

일괄 처리 풀 처리 toocreate 풀을에 일괄 처리 작업을 제출할 수 있습니다. Hello 풀의 hello 크기를 제한 및 toowhich 풀 hello 작업이 제출 됩니다. BES 작업 자체 처리 공간을 제공 하 예측 가능한 처리 성능 및 제출 하면 toohello 처리 부하에 해당 하는 hello 기능 toocreate 리소스 풀에서 실행 됩니다.

## <a name="how-toouse-batch-pool-processing"></a>어떻게 toouse 배치 풀을 처리

구성의 일괄 처리 풀 처리 hello Azure 포털을 통해 현재 사용할 수 없는 합니다. toouse 배치 풀을 처리 해야 합니다.

-   일괄 처리 풀 계정 CSS toocreate를 호출 하 고 풀 서비스 URL 및 인증 키 가져오기
-   새 Resource Manager 기반 웹 서비스 및 청구 계획 만들기

toocreate 계정에 Microsoft 고객 서비스 및 지원 (CSS)를 호출 하 고 id입니다. 구독 제공 CSS 있습니다 toodetermine hello 적절 한 용량 시나리오에 사용 합니다. CSS는 hello 최대 수를 만들 수 있으며 각 풀에 배치할 수 있는 가상 컴퓨터 (Vm)의 최대 수를 hello 풀의 계정을 구성 합니다. 계정이 구성되면 풀 서비스 URL과 인증 키가 제공됩니다.

사용자 계정을 만든 후 hello 풀 서비스 URL 및 권한 부여 키 tooperform 풀의 관리 작업을 일괄 처리 풀 사용 합니다.

![배치 풀 서비스 아키텍처](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

해당 CSS 제공 tooyou hello 풀 서비스 URL에서 hello 풀 만들기 작업을 호출 하 여 풀을 만들어야 합니다. 풀을 만들 때 Vm 및 hello swagger.json 새 리소스 관리자의의 hello URL의 hello 수 기반 기계 학습 웹 서비스를 지정 합니다. 이 웹 서비스 tooestablish hello 청구 연결을 제공 됩니다. 일괄 처리 풀 서비스 hello 청구 계획 hello swagger.json을 tooassociate hello 풀을 사용합니다. 웹 서비스를 모두 새 리소스 관리자 기반 모든 BES를 실행할 수 있습니다 및 hello 풀에서 선택한 기본 합니다.

모든 새 리소스 관리자 기반 웹 서비스를 사용할 수 있지만 유의 hello 작업에 대 한 hello 청구 해당 서비스와 연결 된 hello 청구 계획에 따라 청구 됩니다. 실행 중인 일괄 처리 풀 작업에 맞게 toocreate 웹 서비스와 새 청구 계획을 할 수 있습니다.

웹 서비스 만들기에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

Hello BES를 제출 하는 풀을 만들었으면 hello 웹 서비스에 대 한 일괄 처리 요청 URL hello 사용 하 여 작업 합니다. Toosubmit를 선택할 수 있습니다이 tooa 풀이나 tooclassic 일괄 처리 합니다. 작업 tooBatch 풀 처리 toosubmit hello toohello 작업 제출 요청 본문 매개 변수를 다음 추가할 수 있습니다.

"AzureBatchPoolId":"&lt;pool ID&gt;"

Hello 매개 변수를 추가 하지 않으면 hello 작업이 hello 클래식 일괄 처리 프로세스 환경에서 실행 됩니다. Hello 풀 사용 가능한 리소스가 있으면 hello 작업이 실행을 즉시 시작 됩니다. Hello 풀에 리소스를 해제 하는 경우 리소스 있을 때까지 작업 대기 됩니다.

정기적으로 풀의 hello 용량에 도달 하면 고 증가 된 용량 필요를 찾을 경우 CSS를 호출 하 고 할당량 대표 tooincrease 사용할 수 있습니다.

요청 예제:

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>배치 풀 처리 사용 시 고려 사항

일괄 처리 풀 처리 항상 청구 서비스 이며 청구 계획을 기반으로 하는 리소스 관리자와 tooassociate 필요로 하 합니다. 계산 시간 hello 풀이 실행 되 고; hello 수에 대 한만 청구 됩니다. 시간 풀에 해당 하는 동안 실행 되는 작업의 hello 개수에 관계 없이 풀을 만들 경우 요금이 청구 됩니다 hello 풀의 각 가상 컴퓨터의 hello 계산 시간에 대 한 hello 풀 삭제 될 때까지 hello 풀에서 실행 중인 일괄 처리 작업이 없을 경우에 합니다. Hello 가상 컴퓨터에 대 한 청구 프로 비전 완료 되기 시작 하 고 삭제 된 경우를 중지 합니다. Hello에 hello 계획 중 하나를 사용할 수 [컴퓨터 학습 가격 페이지](https://azure.microsoft.com/pricing/details/machine-learning/)합니다.

청구 예제:

2개의 가상 컴퓨터로 배치 풀을 만들고 24시간 후에 삭제하는 경우 해당 기간 동안 실행된 작업 수에 관계 없이 48 계산 시간에 대한 청구 계획이 계상됩니다.

4개의 가상 컴퓨터로 배치 풀을 만들고 12시간 후에 삭제하는 경우에도 48 계산 시간에 대한 청구 계획이 계상됩니다.

작업을 완료할 때 작업 상태 toodetermine hello를 폴링하는 것이 좋습니다. 모든 작업 실행을 완료 하는 경우 가상 컴퓨터의 hello 풀 크기 조정 작업 tooset hello 수 hello 풀 toozero를 호출 합니다. Toocreate 새 풀을 다른 청구 계획에 대 한 예를 들어 toobill를 해야 하는 리소스 풀에 짧은 경우 풀을 삭제 하려면 hello 대신 모든 작업 실행을 완료 합니다.


| **배치 풀 처리를 사용하는 경우**    | **클래식 일괄 처리를 사용하는 경우**  |
|---|---|
|작업의 많은 toorun 필요<br>또는<br/>작업을 즉시 실행 될 tooknow 필요<br/>또는<br/>처리량을 보장해야 합니다. 예를 들어 필요한 toorun 지정된 된 시간 내에 있는 작업 수와 때 tooscale 계산 리소스 toomeet 아웃 필요 합니다.    | 몇 가지 작업만 실행하고 있습니다.<br/>and<br/> 즉시 hello 작업 toorun 필요 하지 않습니다. |
