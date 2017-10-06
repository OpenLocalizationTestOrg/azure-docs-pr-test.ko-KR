---
title: "aaa \"Azure 배치 풀을 만드는 이벤트 | \"Microsoft Docs"
description: "Batch 풀 만들기 이벤트에 대한 참조입니다."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>풀 만들기 이벤트

 이 이벤트는 풀이 생성되면 내보내집니다. hello 로그의 hello 콘텐츠는 hello 풀에 대 한 일반 정보를 제공 합니다. 참고 hello 풀의 hello 대상 크기 계산 노드를 0 보다 큰 경우이 이벤트 직후 풀 크기 조정 시작 이벤트 수행 됩니다.

 hello 다음 예제에서는 풀의 hello 본문 hello CloudServiceConfiguration 속성을 사용 하 여 만든 풀에 대 한 이벤트를 만들려면

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|요소|형식|참고 사항|
|-------------|----------|-----------|
|id|문자열|hello 풀의 hello id입니다.|
|displayName|문자열|hello는 hello 풀의 이름을 표시 합니다.|
|vmSize|문자열|hello 풀의 hello 가상 컴퓨터의 hello 크기입니다. 풀의 모든 가상 컴퓨터는 hello 크기가 동일 합니다. <br/><br/> Cloud Services 풀(cloudServiceConfiguration을 사용하여 만든 풀)에 사용 가능한 가상 컴퓨터 크기에 대한 자세한 내용은 [Cloud Services에 적합한 크기](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/)를 참조하세요. Batch는 `ExtraSmall`을 제외한 모든 Cloud Services VM 크기를 지원합니다.<br/><br/> 사용 가능한 VM에 대 한 정보에 대 한 가상 컴퓨터 마켓플레이스 (virtualMachineConfiguration를 사용 하 여 만든 풀) hello에서 이미지를 사용 하 여 풀에 대 한 크기 참조 [가상 컴퓨터의 크기](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) 또는 [에 대 한 크기 가상 컴퓨터](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Batch는 `STANDARD_A0`및 프리미엄 저장소(`STANDARD_GS`, `STANDARD_DS` 및 `STANDARD_DSV2` 시리즈) 크기를 제외한 모든 Azure VM 크기를 지원합니다.|
|[cloudServiceConfiguration](#bk_csconf)|복합 형식|hello 풀에 대 한 hello 클라우드 서비스 구성입니다.|
|[virtualMachineConfiguration](#bk_vmconf)|복합 형식|hello hello 풀에 대 한 가상 컴퓨터 구성입니다.|
|[networkConfiguration](#bk_netconf)|복합 형식|hello hello 풀에 대 한 네트워크 구성입니다.|
|resizeTimeout|Time|hello hello 풀에서 마지막 크기 조정 작업에 대해 지정 된 계산 노드 toohello 풀의 할당에 대 한 hello 제한 시간입니다.  (hello 초기 hello 풀 크기가 조정으로 개수 만들어질 때 크기를 조정 합니다.)|
|targetDedicated|Int32|hello hello 풀에 대해 요청 된 계산 노드 수입니다.|
|enableAutoScale|Bool|Hello 풀 크기 시간에 따라 자동으로 조정 되는지 여부를 지정 합니다.|
|enableInterNodeCommunication|Bool|Hello 풀이 노드 간 직접 통신에 대 한 설정 되는지 여부를 지정 합니다.|
|isAutoPool|Bool|지정 hello 풀 작업의 자동 풀 메커니즘을 통해 생성 된 여부.|
|maxTasksPerNode|Int32|hello hello 풀의 단일 계산 노드에서 동시에 실행할 수 있는 작업의 최대 수입니다.|
|vmFillType|문자열|일괄 처리 서비스 hello hello 풀의 계산 노드 간에 작업을 배포 하는 방법을 정의 합니다. 유효한 값은 Spread 또는 Pack입니다.|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|osFamily|문자열|hello 풀의 hello 가상 컴퓨터에 설치 된 Azure 게스트 OS 제품군 toobe을 hello 합니다.<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> **2** – OS 제품군 2, 해당 tooWindows 서버 2008 R2 s p 1입니다.<br /><br /> **3** – 해당 tooWindows Server 2012 운영 체제 제품군 3입니다.<br /><br /> **4** – OS 제품군 4, 해당 tooWindows Server 2012 r 2입니다.<br /><br /> 자세한 내용은 [Azure 게스트 OS 릴리스](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases)를 참조하세요.|
|targetOSVersion|문자열|hello Azure 게스트 OS 버전 toobe hello 풀의 hello 가상 컴퓨터에 설치 합니다.<br /><br /> hello 기본값은  **\***  hello hello에 대 한 최신 운영 체제 버전을 지정 하는 제품군을 지정 합니다.<br /><br /> 기타 허용된 값은 [Azure 게스트 OS 릴리스](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases)를 참조하세요.|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|복합 형식|Hello 플랫폼 또는 마켓플레이스 이미지 toouse에 대 한 정보를 지정합니다.|
|nodeAgentSKUId|문자열|hello 계산 노드를 프로 비전 hello 배치 노드 에이전트 SKU 번호입니다.|
|[windowsConfiguration](#bk_winconf)|복합 형식|Hello 가상 컴퓨터에서 Windows 운영 체제 설정을 지정합니다. 이 속성 아니어야 hello imageReference Linux 운영 체제 이미지를 참조 하는 경우를 지정 합니다.|

###  <a name="bk_imgref"></a> imageReference

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|publisher|문자열|hello 이미지의 hello 게시자입니다.|
|offer|문자열|hello 이미지의 hello 제품입니다.|
|sku|문자열|hello hello 이미지의 SKU입니다.|
|버전|문자열|hello 이미지의 hello 버전입니다.|

###  <a name="bk_winconf"></a> windowsConfiguration

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|enableAutomaticUpdates|Boolean|자동 업데이트에 대 한 hello 가상 컴퓨터를 사용 하는지 여부를 나타냅니다. 이 속성이 지정 되지 않은 경우 hello 기본값은 true입니다.|

###  <a name="bk_netconf"></a> networkConfiguration

|요소 이름|형식|참고 사항|
|------------------|--------------|----------|
|subnetId|문자열|hello 풀 계산 노드가 생성 되어 hello 서브넷의 hello 리소스 식별자를 지정 합니다.|
