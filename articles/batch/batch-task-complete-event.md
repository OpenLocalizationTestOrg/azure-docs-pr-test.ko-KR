---
title: "aaa \"Azure 일괄 처리 작업 완료 이벤트 | \"Microsoft Docs"
description: "Batch 태스크 완료 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a>태스크 완료 이벤트

 이 이벤트는 hello 종료 코드에 관계 없이 작업이 완료 되 면 내보내집니다. 이 이벤트를 다시 시도 여부 및 hello 작업 실행 되는 작업의 사용된 toodetermine hello 기간 수 수 있습니다.


 hello 다음 예제에서는 작업 완료 이벤트의 hello 본문

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|jobId|문자열|hello 작업을 포함 하는 hello 작업의 hello id입니다.|
|id|문자열|hello 작업의 hello id입니다.|
|taskType|문자열|hello 작업의 hello 형식입니다. 이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다. 작업 준비 태스크, 작업 릴리스 태스크 또는 시작 태스크의 경우 이 이벤트가 내보내지지 않습니다.|
|systemTaskVersion|Int32|작업에 내부 다시 시도 카운터가 hello입니다. 내부적으로 hello 일괄 처리 서비스는 일시적인 문제에 대 한 작업 tooaccount 다시 시도할 수 있습니다. 이러한 문제는 잘못 된 상태에 계산 노드 모두에서 내부 일정 오류나 시도 toorecover를 포함할 수 있습니다.|
|[nodeInfo](#nodeInfo)|복합 형식|Hello 계산 노드는 hello 작업 실행에 대 한 정보를 포함 합니다.|
|[multiInstanceSettings](#multiInstanceSettings)|복합 형식|해당 hello 작업은 여러 계산 노드를 요구 하는 다중 인스턴스 작업을 지정 합니다.  자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.|
|[constraints](#constraints)|복합 형식|hello 실행 적용 되는 제약 toothis 작업 합니다.|
|[executionInfo](#executionInfo)|복합 형식|Hello hello 작업 실행에 대 한 정보가 포함 됩니다.|

###  <a name="nodeInfo"></a> nodeInfo

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|poolId|문자열|태스크가 실행 하는 hello에 hello 풀의 hello id입니다.|
|nodeId|문자열|태스크가 실행 하는 hello에 hello 노드의 hello id입니다.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|numberOfInstances|Int32|hello hello 작업에 필요한 하는 계산 노드 수입니다.|

###  <a name="constraints"></a> constraints

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|hello 최대 횟수 hello 작업을 다시 시도할 수 있습니다. 종료 코드가 0이 아니면 hello 일괄 처리 서비스는 작업을 다시 시도 합니다.<br /><br /> 이 값 hello 재시도 횟수를 구체적으로 제어 하는 참고 합니다. hello 일괄 처리 서비스 hello 작업을 한 번 시도 합니다 및 toothis 한도를 다음 다시 시도할 수 있습니다. 예를 들어 hello 최대 다시 시도 횟수는 3, 일괄 처리 (한 번의 초기 시도 및 3 회) 시간 too4 구성 작업을 시도 합니다.<br /><br /> Hello 최대 다시 시도 횟수가 0 인 경우 hello 일괄 처리 서비스 작업을 재시도 하지 않습니다.<br /><br /> Hello 최대 다시 시도 횟수가-1 이면 hello 일괄 처리 서비스가 작업 제한 없이 다시 시도 합니다.<br /><br /> hello 기본값은 0 (다시 시도 안 함)입니다.|

###  <a name="executionInfo"></a> executionInfo

|요소 이름|형식|참고 사항|
|------------------|----------|-----------|
|startTime|DateTime|hello 작업 실행이 시작 시 hello 시간입니다. Toohello 해당 '실행 중' **실행** 상태 이면 나타내도록 hello 작업에서 리소스 파일 또는 응용 프로그램 패키지를 지정 하는 경우 다음 hello 시작 시간 hello 시간 다운로드 하거나 배포를 시작 하는 hello 작업입니다.  Hello 작업 다시 시작 되거나 다시 시도 된 경우이 hello 실행이 시작 되는 hello 작업에 대 한 가장 최근 시간입니다.|
|endTime|DateTime|hello 시기는 hello 작업이 완료 되었습니다.|
|exitCode|Int32|hello hello 작업의 종료 코드입니다.|
|retryCount|Int32|hello hello 작업 hello 일괄 처리 서비스에서 다시 시도한 횟수입니다. 지정 된 MaxTaskRetryCount toohello를 0이 아닌 종료 코드로 종료 하는 경우에 hello 태스크를 다시 시도 합니다.|
|requeueCount|Int32|hello hello 작업이 다시 대기 hello 일괄 처리 서비스에서 사용자 요청의 hello 결과로 횟수입니다.<br /><br /> 때 실행을 위해 다시 대기열에 hello 사용자 제거 (하 여 hello 풀 축소) 풀 또는 hello 작업이 해제 되는 경우, hello 사용자에서 노드 hello 노드에서 실행 중인 작업을 지정할 수 있습니다. 이 개수 이러한 이유로 몇 번 hello 작업을 다시 대기를 추적 합니다.|
