---
title: "aaaAutomatically 눈금의에서 계산 노드 Azure 배치 풀 | Microsoft Docs"
description: "Enable에 대해 자동 크기 조정을 클라우드 풀 toodynamically hello hello 풀의 계산 노드 수를 조정 합니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Batch 풀에서 계산 노드의 크기를 조정하는 자동 크기 조정 수식 만들기

Azure Batch는 정의한 매개 변수에 따라 풀을 자동으로 크기 조정합니다. 자동 크기 조정 된 일괄 처리 작업 요구량이 증가으로 노드 tooa 풀을 동적으로 추가 및 감소은 계산 노드를 제거 합니다. Hello 일괄 처리 응용 프로그램에서 사용 되는 계산 노드 수를 자동으로 조정 하 여 시간과 비용을 저장할 수 있습니다. 

사용자가 정의한 *자동 크기 조정 수식*에 연결하면 계산 노드 풀에서 자동으로 크기를 조정할 수 있습니다. hello 일괄 처리 서비스는 hello 자동 크기 조정 수식 toodetermine hello 계산 노드 수를 필요한 tooexecute는 작업을 사용 합니다. 계산 노드는 전용 노드이거나 [우선 순위가 낮은 노드](batch-low-pri-vms.md)일 수 있습니다. 일괄 처리 응답 tooservice 메트릭 데이터는 주기적으로 수집 합니다. 이 메트릭 데이터를 사용 하 여 일괄 처리는 hello 수식에서 구성 가능한 간격을 기반으로 하는 hello 풀의 계산 노드 수를 조정 합니다.

풀을 만들 때 또는 기존 풀에서 자동 크기 조정을 사용하도록 설정할 수 있습니다. 자동 크기 조정에 대해 구성된 풀의 기존 수식을 변경할 수도 있습니다. 일괄 처리에 자동 크기 조정의 toopools 및 toomonitor hello 상태를 할당 하기 전에 수식을 실행 tooevaluate가 있습니다.

이 문서에서는 hello, 변수, 연산자, 작업 및 함수를 포함 하 여 자동 크기 조정 수식을 구성 하는 다양 한 엔터티. 에서는 어떻게 tooobtain 다양 한 일괄 처리 내에서 리소스 및 작업 메트릭을 계산 합니다. 이러한 메트릭을 tooadjust 리소스 사용량 및 작업 상태에 따라 풀의 노드 수를 사용할 수 있습니다. 다음 수식 tooconstruct를 사용 하도록 설정한 자동 풀을 모두 사용 하 여 크기를 조정 배치 REST 및.NET Api hello 하는 방법을 설명 합니다. 마지막으로 몇 가지 예제 수식으로 마무리하겠습니다.

> [!IMPORTANT]
> Hello 일괄 처리 계정을 만들 때 지정할 수 있습니다 [계정 구성](batch-api-basics.md#account), 풀 일괄 처리 서비스 구독 (hello 기본값) 또는 사용자 구독에 할당 된 여부를 결정 하는 합니다. Hello 기본 일괄 처리 서비스 구성을 사용 하 여 일괄 처리 계정이 만든 경우 사용자 계정은 제한 된 tooa 최대 처리를 위해 사용할 수 있는 코어 수입니다. 일괄 처리 서비스 hello toothat 코어 제한부터만 계산 노드를 확장합니다. 이러한 이유로 hello 일괄 처리 서비스 자동 크기 조정 수식에 의해 지정 된 계산 노드의 hello 대상 수에 도달 하지 않을 수 있습니다. 참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 보기 및 계정 할당량 증가에 대 한 내용은 합니다.
>
>Hello 사용자 구독 구성을 사용 하 여 계정의 만든 계정 hello 구독에 대 한 코어 할당량 hello에서에서 공유 합니다. 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 [Virtual Machines 제한](../azure-subscription-service-limits.md#virtual-machines-limits)을 참조하세요.
>
>

## <a name="automatic-scaling-formulas"></a>자동 크기 조정 수식
자동 크기 조정 수식은 하나 이상의 문을 포함하는 사용자가 정의한 문자열 값입니다. hello 자동 크기 조정 수식이 tooa 풀에 할당 된 [autoScaleFormula] [ rest_autoscaleformula] 요소 (일괄 처리 REST) 또는 [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] 속성 (일괄 처리.NET)입니다. hello 일괄 처리 서비스는 hello 다음 처리 간격에 대 한 hello 풀의 수식 toodetermine hello 대상 수가 계산 노드를 사용합니다. hello 수식 문자열 8KB를 초과할 수 없습니다, 그리고 세미콜론으로 구분 되 고 줄 바꿈 및 주석을 포함할 수 있는 too100 문을를 포함할 수 있습니다.

자동 크기 조정 수식은 Batch 자동 크기 조정 "언어"로 고려할 수 있습니다. 수식 문은 서비스 정의 변수 (hello 일괄 처리 서비스에서 정의 된 변수) 및 사용자 정의 변수 (사용자가 정의한 변수)를 모두 포함할 수 있는 자유형 식이 됩니다. 기본 제공 형식, 연산자 및 함수를 사용하여 이러한 값에 다양한 작업을 수행할 수 있습니다. 예를 들어 문을 다음 양식 hello를 걸릴 수 있습니다.

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

수식은 일반적으로 이전 문에서 가져온 값에 대한 작업을 수행하는 여러 문을 포함합니다. 에 대 한 값을 구한 먼저 예를 들어 `variable1`, tooa 함수 toopopulate 전달 `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

대상 수의 계산 노드 자동 크기 조정 수식 tooarrive 프로그램에서 이러한 문을 포함 합니다. 전용 노드와 우선 순위가 낮은 노드에는 각각 자체의 목표 설정이 있으므로 각 노드 형식의 목표를 정의할 수 있습니다. 자동 크기 조정 수식에는 전용 노드의 목표 값, 우선 순위가 낮은 노드의 목표 값 또는 둘 다가 포함될 수 있습니다.

hello 대상 노드 수 이상에서 이하로 되었거나 hello hello 현재 hello 풀에서 해당 형식의 노드 수와 동일 합니다. Batch는 풀의 자동 크기 조정 수식을 특정 간격([자동 크기 조정 간격](#automatic-scaling-interval) 참조)으로 평가합니다. 각 유형의 자동 크기 조정 수식 평가 hello 시 지정 하는 hello 풀 toohello 숫자의 노드에서 hello 대상 수를 조정 하는 일괄 처리 합니다.

### <a name="sample-autoscale-formula"></a>샘플 자동 크기 조정 수식

대부분의 시나리오에 대 한 조정 된 toowork 일 수 있는 자동 크기 조정 수식의 예를 들면 다음과 같습니다. 변수 hello `startingNumberOfVMs` 및 `maxNumberofVMs` hello 예의 수식이 조정된 tooyour 요구 될 수 있습니다. 이 수식은 전용된 노드를 확장 하지만 수정 된 tooapply tooscale 우선 순위가 낮은 노드도 될 수 있습니다. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

이 자동 크기 조정 수식을 사용 하 여 hello 풀은 처음에 단일 VM으로 만들어집니다. hello `$PendingTasks` 메트릭을 실행 중이거나 큐에 대기 중인 작업의 hello 수를 정의 합니다. hello 지난 180 초 동안 hello에서 보류 중인 작업의 hello 평균 수를 찾습니다 수식과 hello 설정 `$TargetDedicatedNodes` 변수 적절 하 게 합니다. hello 수식은 되도록 전용 노드의 hello 대상 수 25 Vm을 초과 하지 않습니다. 새 작업 제출 되 hello 풀 자동으로 증가 합니다. 작업 완료, Vm 하나씩 무료 되 고 hello 자동 크기 조정 수식 hello 풀을 축소 합니다.

## <a name="variables"></a>variables
자동 크기 조정 수식에는 **서비스 정의** 및 **사용자 정의** 변수를 모두 사용할 수 있습니다. 서비스 정의 변수 hello toohello 일괄 처리 서비스에서에서 빌드됩니다. 서비스 정의 변수 일부는 읽기-쓰기이고, 일부는 읽기 전용입니다. 사용자 정의 변수는 사용자가 정의한 변수입니다. Hello 예의 수식을 hello 이전 섹션에 표시 된 것에서 `$TargetDedicatedNodes` 및 `$PendingTasks` 도 서비스 정의 변수가 있습니다. 변수 `startingNumberOfVMs` 및 `maxNumberofVMs`는 사용자 정의 변수입니다.

> [!NOTE]
> 서비스 정의 변수에는 항상 달러($) 기호가 앞에 붙습니다. 사용자 정의 변수에 대 한 hello 달러 기호는 선택 사항입니다.
>
>

다음 표에서 hello 읽기 / 쓰기 권한 모두 및 읽기 전용으로 정의 된 변수 hello 일괄 처리 서비스를 보여 줍니다.

있습니다 가져오고 설정할 수 있습니다 이러한 서비스 정의 변수의 hello 값 toomanage hello 계산 노드 수는 풀에서:

| 읽기-쓰기 서비스 정의 변수 | 설명 |
| --- | --- |
| $TargetDedicatedNodes |hello 대상 수 전용된 hello 풀에 대 한 노드를 계산합니다. 전용된 노드 수가 hello 풀 hello 필요한 노드 수를 항상 얻을 수 있으므로 대상으로 지정 됩니다. 예를 들어 전용 노드의 hello 대상 수 수정 되 면 hello 하기 전에 자동 크기 조정 평가 하 여 풀 hello 최초 목표에 도달 다음 hello 풀 hello 목표에 도달 하지 않을 수 있습니다. <br /><br /> Hello 일괄 처리 서비스 구성을 사용 하 여 생성 된 계정에서 풀 hello 대상 일괄 처리 계정 노드나 코어 할당량을 초과 하는 경우 목표를 얻지 못할 수 있습니다. Hello 사용자 구독 구성으로 생성 하는 계정에 풀 hello 대상 hello 구독에 대 한 hello 공유 코어 할당량을 초과 하는 경우 목표를 얻지 못할 수 있습니다.|
| $TargetLowPriorityNodes |hello 대상 수가 우선 순위가 낮은 hello 풀에 대 한 노드를 계산 합니다. 우선 순위가 낮은 노드 수가 hello 풀 hello 필요한 노드 수를 항상 얻을 수 있으므로 대상으로 지정 됩니다. 예를 들어 우선 순위가 낮은 노드의 hello 대상 수 수정 되 면 hello 하기 전에 자동 크기 조정 평가 하 여 풀 hello 최초 목표에 도달 다음 hello 풀 hello 목표에 도달 하지 않을 수 있습니다. 풀을 수도 얻지 못할 대상 hello 대상 일괄 처리 계정 노드나 코어 할당량을 초과 하는 경우. <br /><br /> 우선 순위가 낮은 계산 노드에 대한 자세한 내용은 [Batch(미리 보기)에서 낮은 우선 순위 VM 사용](batch-low-pri-vms.md)을 참조하세요. |
| $NodeDeallocationOption |계산 노드는 풀에서 제거할 때 발생 하는 hello 동작입니다. 가능한 값은 다음과 같습니다.<ul><li>**다시 대기**-작업을 즉시 종료 하 고 다시 예약할 수 있도록 hello 작업 큐에 다시 넣습니다.<li>**종료**-작업을 즉시 종료 하 고 hello 작업 큐에서 제거 합니다.<li>**taskcompletion**-때까지 대기 toofinish 현재 실행 중인 작업과 다음 hello 풀에서 hello 노드를 제거 합니다.<li>**retaineddata**-에 있는 모든 hello 로컬 태스크 보존 데이터가 hello 노드 toobe 대기 hello 노드 hello 풀에서 제거 하기 전에 정리 합니다.</ul> |

Hello 일괄 처리 서비스에서 메트릭을 기반으로 하는 서비스 정의 변수 toomake 조정의 hello 값을 얻을 수 있습니다.

| 읽기 전용 서비스 정의 변수 | 설명 |
| --- | --- |
| $CPUPercent |hello CPU 사용량 평균 비율입니다. |
| $WallClockSeconds |사용 하는 시간 (초) hello 수입니다. |
| $MemoryBytes |hello 사용 (메가바이트)의 평균 수입니다. |
| $DiskBytes |hello hello 로컬 디스크에 사용 되는 기가바이트의 평균 수입니다. |
| $DiskReadBytes |hello 읽은 바이트 수입니다. |
| $DiskWriteBytes |hello 쓴 바이트 수입니다. |
| $DiskReadOps |디스크 읽기 작업의 hello 수 수행 됩니다. |
| $DiskWriteOps |hello 디스크 쓰기 작업 수행 수입니다. |
| $NetworkInBytes |hello 인바운드 바이트 수입니다. |
| $NetworkOutBytes |hello 아웃 바운드 바이트 수입니다. |
| $SampleNodeCount |hello 계산 노드 수입니다. |
| $ActiveTasks |hello 수 준비 tooexecute 되어 있지만 아직 실행 되지 않는 작업입니다. hello $ActiveTasks 수 hello 활성 상태에 있으며 종속성 조건이 충족 되는 모든 작업이 포함 됩니다. Hello 활성 상태에 있지만 종속성이 충족 되지 않은 모든 작업은 hello $ActiveTasks 개수에서 제외 됩니다.|
| $RunningTasks |태스크 실행 중 상태로 hello 수입니다. |
| $PendingTasks |$ActiveTasks 및 $RunningTasks hello 합입니다. |
| $SucceededTasks |hello 성공적으로 완료 하는 작업 수입니다. |
| $FailedTasks |hello 실패 한 태스크 수입니다. |
| $CurrentDedicatedNodes |hello 현재 개수 전용된 노드를 계산합니다. |
| $CurrentLowPriorityNodes |hello 현재 수가 우선 순위가 낮은 중지 되었던 모든 노드를 포함 하 여 노드를 계산 합니다. |
| $PreemptedNodeCount | 중지 상태에 있는 hello 풀에 있는 노드의 hello 수입니다. |

> [!TIP]
> hello hello 이전 표에 표시 되는 서비스 정의 읽기 전용 변수는 *개체* 다양 한 메서드를 제공 하는 각 연결 된 tooaccess 데이터입니다. 자세한 내용은 이 문서의 뒷부분에 나오는 [샘플 데이터 가져오기](#getsampledata)를 참조하세요.
>
>

## <a name="types"></a>형식
수식에 지원되는 형식은 다음과 같습니다.

* double
* doubleVec
* doubleVecList
* string
* 타임 스탬프-타임 스탬프는 hello 다음 멤버를 포함 하는 복합 구조:

  * year
  * month (1-12)
  * day (1-31)
  * 요일 (소수점 숫자의 hello 형식에서 예를 들어 1은 월요일)
  * hour(24시간 형식, 예: 13은 오후 1시를 의미함)
  * minute (00-59)
  * second (00-59)
* timeinterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>작업
이러한 작업은 hello 이전 섹션에 나열 된 hello 형식에서 허용 됩니다.

| 작업 | 지원되는 연산자 | 결과 형식 |
| --- | --- | --- |
| double *operator* double |+, -, *, / |double |
| double *operator* timeinterval |* |timeinterval |
| doubleVec *operator* double |+, -, *, / |doubleVec |
| doubleVec *operator* doubleVec |+, -, *, / |doubleVec |
| timeinterval *operator* double |*, / |timeinterval |
| timeinterval *operator* timeinterval |+, - |timeinterval |
| timeinterval *operator* timestamp |+ |timestamp |
| timestamp *operator* timeinterval |+ |timestamp |
| timestamp *operator* timestamp |- |timeinterval |
| *operator*double |-, ! |double |
| *operator*timeinterval |- |timeinterval |
| double *operator* double |<, <=, ==, >=, >, != |double |
| string *operator* string |<, <=, ==, >=, >, != |double |
| timestamp *operator* timestamp |<, <=, ==, >=, >, != |double |
| timeinterval *operator* timeinterval |<, <=, ==, >=, >, != |double |
| double *operator* double |&&, &#124;&#124; |double |

3항 연산자(`double ? statement1 : statement2`)가 있는 이중 연산자를 테스트할 경우 0이 아님이 **true**이고 0은 **false**입니다.

## <a name="functions"></a>함수
이러한 미리 정의 된 **함수** toouse는 자동 크기 조정 수식을 정의 사용할 수 있습니다.

| 함수 | 반환 형식 | 설명 |
| --- | --- | --- |
| avg(doubleVecList) |double |반환 hello hello doubleVecList의 모든 값에 대 한 평균 값입니다. |
| len(doubleVecList) |double |반환 hello hello doubleVecList에서 생성 되는 hello 벡터의 길이입니다. |
| lg(double) |double |반환 hello 로그 밑이 2 hello double 합니다. |
| lg(doubleVecList) |doubleVec |밑이 2 hello doubleVecList hello component-wise 로그를 반환합니다. vec(double) hello 매개 변수에 대해 명시적으로 전달 되어야 합니다. 그렇지 않으면 hello double lg (double) 버전으로 간주 됩니다. |
| ln(double) |double |반환 hello hello double의 자연 로그입니다. |
| ln(doubleVecList) |doubleVec |밑이 2 hello doubleVecList hello component-wise 로그를 반환합니다. vec(double) hello 매개 변수에 대해 명시적으로 전달 되어야 합니다. 그렇지 않으면 hello double lg (double) 버전으로 간주 됩니다. |
| log(double) |double |Hello 로그 밑수 10을 반환 hello double입니다. |
| log(doubleVecList) |doubleVec |Hello component-wise 로그 hello doubleVecList의 밑수 10을 반환 합니다. vec(double) hello 단일 double 매개 변수에 대해 명시적으로 전달 되어야 합니다. 그렇지 않으면 hello log (double) 버전으로 간주 됩니다. |
| max(doubleVecList) |double |반환 hello hello doubleVecList의 최대값입니다. |
| min(doubleVecList) |double |반환 hello hello doubleVecList의 최소값입니다. |
| norm(doubleVecList) |double |반환 hello hello doubleVecList에서 생성 되는 hello 벡터의 2-norm 합니다. |
| percentile(doubleVec v, double p) |double |반환 hello hello 벡터 v의 백분위 수 요소입니다. |
| rand() |double |0.0에서 1.0 사이의 임의 값을 반환합니다. |
| range(doubleVecList) |double |Hello doubleveclist에서 hello hello 최소 및 최대 값의 차이 반환 합니다. |
| std(doubleVecList) |double |반환 hello hello doubleVecList의 hello 값 샘플 표준 편차입니다. |
| stop() | |Hello 자동 크기 조정 식의 평가 중지합니다. |
| sum(doubleVecList) |double |반환 hello 전체적인 hello doubleVecList의 모든 hello 구성 요소입니다. |
| time(string dateTime="") |timestamp |매개 변수가 전달 되는 경우 또는 전달 되 면 hello dateTime 문자열의 타임 스탬프를 환영 하는 경우 hello의 타임 스탬프 hello 현재 시간을 반환 합니다. 지원되는 dateTime 형식은 W3C-DTF 및 RFC 1123입니다. |
| val(doubleVec v, double i) |double |시작 인덱스가 0 인 벡터 v의에서 위치 i에 있는 hello 요소의 hello 값을 반환 합니다. |

목록을 수락할 hello 앞의 표에서 설명 하는 hello 함수 중 일부를 인수로 수 있습니다. hello 쉼표로 구분 된 목록은 어떠한 조합의 *double* 및 *doubleVec*합니다. 예:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

hello *doubleVecList* 값은 변환 된 tooa 단일 *doubleVec* 평가 하기 전에. 예를 들어 경우 `v = [1,2,3]`를 호출한 다음 `avg(v)` 해당 toocalling은 `avg(1,2,3)`합니다. 호출 `avg(v, 7)` 해당 toocalling은 `avg(1,2,3,7)`합니다.

## <a name="getsampledata"></a>샘플 데이터 가져오기
자동 크기 조정 수식 hello 일괄 처리 서비스에서 제공 되는 메트릭 데이터 (샘플)에 적용 됩니다. 수식을 확장 하거나 hello 서비스에서 얻은 hello 값에 따라 풀 크기를 축소 합니다. 설명한 hello 서비스 정의 된 변수는 이전에 tooaccess 데이터를 해당 개체와 연결 된 다양 한 메서드를 제공 하는 개체는입니다. 예를 들어 hello 다음 식을 보여 줍니다 요청 tooget hello 지난 5 분 동안 CPU 사용량:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| 메서드 | 설명 |
| --- | --- |
| GetSample() |hello `GetSample()` 메서드 데이터 샘플의 벡터를 반환 합니다.<br/><br/>하나의 샘플은 30초 동안의 메트릭 데이터입니다. 즉 30초마다 샘플을 가져옵니다. 하지만 아래 설명과 같이 샘플 수집 하는 경우와 사용 가능한 tooa 수식을 때 까지는 지연 시간이 있습니다. 따라서 지정된 기간 동안 일부 샘플을 수식에 의한 평가에 사용할 수 없을지도 모릅니다.<ul><li>`doubleVec GetSample(double count)`<br/>수집 된 가장 최근 샘플 hello에서에서 샘플 tooobtain hello 수를 지정 합니다.<br/><br/>`GetSample(1)`hello 마지막 사용 가능한 샘플을 반환합니다. 그러나 메트릭과 같이 `$CPUPercent`,이 쓰일 수 없습니다 불가능 한 tooknow 있기 때문에 *때* hello 샘플이 수집 된 합니다. 최근 샘플일 수도 있지만 시스템 문제로 인해 훨씬 오래된 샘플일 수도 있습니다. 이러한 경우 toouse 아래와 같이 시간 간격에에서 두는 것이 좋습니다.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>샘플 데이터를 수집하기 위한 시간 프레임을 지정합니다. 필요에 따라 지정 hello에서 사용할 수 있어야 하는 샘플의 hello 백분율 시간 프레임을 요청 했습니다.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`지난 10 분 hello에 대 한 모든 샘플 hello CPUPercent 기록에 있는 경우에 20 샘플을 반환 합니다. 그러나 Hello 지난 1 분간 기록 하지 않았으면만 18 샘플 반환 됩니다. 이 경우 다음과 같습니다.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`hello 샘플의 90%에만 사용할 수 있으므로 실패 합니다.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`은 성공합니다.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>시작 시간과 종료 시간을 사용하여 데이터를 수집하기 위한 시간 프레임을 지정합니다.<br/><br/>위에서 설명 했 듯이 샘플 수집 하는 경우와 사용 가능한 tooa 수식을 때 까지는 지연 시간이 있습니다. Hello를 사용 하는 경우 이러한 지연 시간을 고려 `GetSample` 메서드. 아래 `GetSamplePercent` 참조 |
| GetSamplePeriod() |기록 샘플 데이터 집합에서 수행 된 샘플의 hello 기간을 반환 합니다. |
| Count() |반환 hello 총 hello 메트릭 기록에는 샘플 수입니다. |
| HistoryBeginTime() |반환 hello hello hello 메트릭에 대 한 가장 오래 된 사용 가능한 데이터 샘플의 타임 스탬프입니다. |
| GetSamplePercent() |반환 hello는 주어진된 시간 간격에 사용할 수 있는 샘플의 백분율입니다. 예:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>때문에 hello `GetSample` 메서드가 반환 하는 샘플의 hello 백분율 미만이 면 hello 실패 `samplePercent` 지정 hello를 사용할 수 `GetSamplePercent` 메서드 toocheck 첫 번째입니다. 그런 다음 부족 하 여 샘플 hello 자동 크기 조정 평가 중지 하지 않고 표시 되어 있는 경우 다른 동작을 수행할 수 있습니다. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>샘플, 샘플 비율 및 hello *GetSample()* 메서드
자동 크기 조정 수식이의 핵심 작업 hello tooobtain 작업 및 자원 메트릭 데이터 이며 해당 데이터에 따라 풀 크기를 조정 합니다. 따라서 것은 중요 한 toohave 자동 크기 조정 수식 메트릭 데이터 (샘플)와 상호 작용 하는 방법을 파악 합니다.

**샘플**

hello 일괄 처리 서비스는 정기적으로 작업 및 자원 메트릭 샘플을 사용 하 고 자동 크기 조정 수식을 사용할 수 있는 tooyour 끌고 있습니다. 이러한 예제는 hello 일괄 처리 서비스에서 30 초 마다 기록 됩니다. 그러나는 일반적으로 이러한 샘플 기록 된 시간 사이의 너무 사용할 수 있습니다 (고 때에서 읽을 수)는 지연을 자동 크기 조정 수식입니다. 또한 네트워크나 기타 인프라 문제 toovarious 요인 인해 샘플 하지 기록 될 수 있습니다는 특정 기간에 대 한 합니다.

**샘플 비율**

때 `samplePercent` toohello 전달 되 `GetSample()` 메서드 또는 hello `GetSamplePercent()` 메서드는 _%_ tooa 비교 hello 가능한 최대 수 hello 일괄 처리 서비스에서 기록 되는 샘플을 참조 하 고 사용 가능한 tooyour 자동 크기 조정 수식이 있는 샘플 hello 수입니다.

예를 들어 10분 TimeSpan을 살펴보겠습니다. 샘플에는 10 분 시간 범위 내에서 30 초 마다 기록 되므로, 일괄 처리에 의해 기록 되는 샘플의 hello 최대 총 수는 20 샘플 (2 분 당) 것입니다. 그러나 메커니즘 및 Azure 내에서 기타 문제를 보고 하는 hello의 내재 된 대기 시간 toohello 인해 있을 수 있습니다만 15 샘플 읽기에 대 한 사용 가능한 tooyour 자동 크기 조정 수식에는. 따라서 예를 들어 그 10 분 동안 hello 총 기록 하는 샘플 수의 75%에만 수 있습니다 사용할 수 있는 tooyour 수식입니다.

**GetSample() 및 샘플 범위**

자동 크기 조정 수식은 진행 중인 toobe 증가 및 축소 풀 &mdash; 노드 노드 추가 또는 제거 합니다. 노드 비용이 있습니다, 때문 분석 충분 한 데이터를 기반으로 하는 지능형 메서드를 사용 하는 수식을 tooensure를 좋습니다. 따라서 수식에서 추세 형식 분석을 사용하는 것이 좋습니다. 이 형식은 수집된 샘플의 범위에 따라 풀을 확장하고 축소합니다.

toodo를 사용 하 여 `GetSample(interval look-back start, interval look-back end)` tooreturn 벡터의 샘플:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

일괄 처리에 의해 줄 위에 hello 계산할 때 값의 벡터 샘플의 범위를 반환 합니다. 예:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

와 같은 함수를 유도할 수 있습니다 hello 벡터의 샘플을 수집 했습니다 면 `min()`, `max()`, 및 `avg()` tooderive hello에서 의미 있는 값 범위를 수집 합니다.

추가 보안을 위해 특정 기간 동안 사용할 수 있는 특정 샘플 비율 보다 작은 경우 수식 평가 toofail를 강제할 수 있습니다. 수식 평가 toofail 강제 때 지시할 있습니다 일괄 처리 toocease 추가 hello 식의 평가 hello 지정 샘플의 백분율을 사용할 수 없습니다. 이 경우에 변경 되지 않습니다 toohello 풀 크기입니다. hello 평가 toosucceed에 대 한 샘플의 필요한 백분율 toospecify가 세 번째 매개 변수를 너무 hello 대로 지정`GetSample()`합니다. 여기에서는 샘플의 75% 요구 사항이 지정됩니다.

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

샘플 가용성에 지연이 있을 수 있습니다, 때문에 반드시 tooalways 모양을 다시 시작 시간이 1 분 보다 오래 된 시간 범위를 지정 합니다. Hello 시스템을 통해 샘플 toopropagate hello 범위 내에 있으므로 샘플에 대 한 약 1 분 걸리는 `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` 사용할 수 없습니다. hello 백분율 매개 변수를 사용할 수는 다시 `GetSample()` tooforce 특정 샘플 비율 요구 사항입니다.

> [!IMPORTANT]
> **자동 크기 조정 수식의 `GetSample(1)`*만* 신뢰하지 않는** 것이 **좋습니다**. 때문에 이것이 `GetSample(1)` toohello 일괄 처리 서비스를 "me hello를 마지막 예제 제공에 관계 없이 검색 경과한 시간입니다." 라는 내용을 않을 이전 샘플 수도 가구의 단일 샘플만는 최근 작업 또는 리소스 상태 hello 더 큰 그림을 대표 하지 수 있습니다. 사용 않으면 `GetSample(1)`, 더 큰 문의 일부 인지 확인 및 수식에 사용 하는 데이터 요소만 하지 hello 합니다.
>
>

## <a name="metrics"></a>메트릭
수식을 정의할 때 리소스 및 작업 메트릭을 모두 사용할 수 있습니다. 평가 하는 hello 메트릭 데이터를 기반으로 하는 hello 풀의 전용된 노드 hello 대상 수를 조정 합니다. Hello 참조 [변수](#variables) 각 메트릭에 대 한 자세한 내용은 섹션.

<table>
  <tr>
    <th>메트릭</th>
    <th>설명</th>
  </tr>
  <tr>
    <td><b>리소스</b></td>
    <td><p>리소스 메트릭 hello CPU, hello 대역폭, 계산 노드의 hello 메모리 사용량을 기반으로 및 hello 노드 수입니다.</p>
        <p> 이러한 서비스 정의 변수는 노드 수에 기반하여 조정하는 데 유용합니다.</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>이러한 서비스 정의 변수는 노드 리소스 사용량에 기반하여 조정하는 데 유용합니다.</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Task</b></td>
    <td><p>작업은 보류 중, 활성, 같은 작업의 hello 상태에 따라 메트릭과 완료 합니다. hello 다음 서비스 정의 된 변수는 작업 기준에 따라 풀 크기를 조정 하는 데 유용 합니다.</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>자동 크기 조정 수식 작성
구성 요소를 위에서 hello를 사용 하는 문을 형성 하 여 자동 크기 조정 수식을 작성 한 다음 해당 문을 완전 한 수식으로 결합 합니다. 이 섹션에서는 몇 가지 실제 크기 조정을 결정할 수 있는 자동 크기 조정 수식 예제를 만듭니다.

첫째, 이제 새 자동 크기 조정 수식의 hello 요구 사항을 정의 합니다. hello 수식 수행 해야합니다.

1. CPU 사용량이 높은 경우 풀의 전용된 계산 노드 hello 대상 수를 늘립니다.
2. CPU 사용량이 낮을 때 풀의 전용된 계산 노드 hello 대상 수를 줄입니다.
3. 항상 전용된 노드 too400 hello 최대 수를 제한 합니다.

사용자 정의 변수를 채우는 hello 보고서를 정의 하는 동안 CPU 사용량이 노드의 tooincrease hello 수 (`$totalDedicatedNodes`) 경우에만 전용 노드의 hello 현재 대상 수의 110% 있는 값을 가진 hello 최소 평균 CPU 사용량 hello 중 지난 10 분 70% 이상 이었습니다. 그렇지 않으면 hello 현재 전용된 노드 수에 대 한 hello 값을 사용 합니다.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

너무*감소* 중 CPU 사용량이 낮은 전용된 노드 수가 hello, 우리의 수식 집합 hello의 다음 문으로 동일 hello `$totalDedicatedNodes` 변수 too90% 경우 hello 전용 노드의 hello 현재 대상 수의 평균 CPU 사용량 hello에 지난 60 분에서 20% 였습니다. 그렇지 않으면 hello의 현재 값을 사용 하 여 `$totalDedicatedNodes` 위의 hello 문에서 채운 합니다.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

이제 hello 400 전용된 계산 노드 tooa 최대 대상 수 제한:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Hello 완전 한 수식을 다음과 같습니다.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>.NET으로 자동 크기 조정 가능한 풀 만들기

.net을 사용 하도록 설정 하는 자동 크기 조정 기능을 사용 하 여 풀 toocreate 다음이 단계를 따르십시오.

1. 사용 하 여 hello 풀 만들기 [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool)합니다.
2. 집합 hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) 속성 너무`true`합니다.
3. 집합 hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) 자동 크기 조정 수식 사용 하 여 속성입니다.
4. (선택 사항) 집합 hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) 속성 (기본값은 15 분)입니다.
5. 사용 하 여 hello 풀 커밋 [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) 또는 [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync)합니다.

hello 다음 코드 조각에서는 자동 크기 조정 가능한 풀.net에서 합니다. hello 풀의 자동 크기 조정 수식이 hello 대상의 수를 설정 월요일, 전용된 노드 too5 및 hello 주 중 일 마다 1입니다. hello [자동 크기 조정 간격](#automatic-scaling-interval) 는 too30 시간 (분)을 설정 합니다. 이 다른 C# 코드 조각이 문서에서는 hello 및 `myBatchClient` hello는 올바르게 초기화 된 인스턴스가 [BatchClient] [ net_batchclient] 클래스입니다.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> 자동 크기 조정 가능한 풀을 만들 때 hello를 지정 하지 않으면 _targetDedicatedComputeNodes_ 매개 변수 또는 hello _targetLowPriorityComputeNodes_ hello에 매개 변수가 너무 호출 **CreatePool**합니다. 대신, hello 지정 **AutoScaleEnabled** 및 **AutoScaleFormula** hello 풀의 속성입니다. 이러한 속성에 대 한 hello 값 각 유형의 노드에 hello 대상 수를 결정합니다. Toomanually 자동 크기 조정 가능한 풀의 크기를 조정 또한 (예: [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), 첫 번째 **사용 하지 않도록 설정** 에 자동 크기 조정 풀 hello 다음 크기를 조정 합니다.
>
>

또한 tooBatch.NET을 사용할 수 있습니다 다른 hello의 [일괄 처리 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development), [배치 REST](https://docs.microsoft.com/rest/api/batchservice/), [일괄 처리 PowerShell cmdlet](batch-powershell-cmdlets-get-started.md), 및 hello [일괄 처리 CLI](batch-cli-get-started.md)tooconfigure 자동 크기 조정 합니다.


### <a name="automatic-scaling-interval"></a>자동 크기 조정 간격
기본적으로 hello 일괄 처리 서비스가 풀의 크기에 따라 tooits 자동 크기 조정 수식이 15 분 마다 조정 합니다. 이 간격은 다음과 같은 풀 속성 hello를 사용 하 여 구성할 수 있습니다.

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)

hello 최소 간격은 5 분 이며 최대 hello 168 시간입니다. 이 범위를 벗어나는 간격을 지정 하는 경우 hello 일괄 처리 서비스는 잘못 된 요청 (400) 오류를 반환 합니다.

> [!NOTE]
> 자동 크기 조정에 1 분 미만, 현재 상태의 toorespond toochanges은 아니지만 보다는 하기 위해 사용 하면 풀의 tooadjust hello 크기 점진적으로 작업을 실행 합니다.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>기존 풀에서 자동 크기 조정 사용

각 일괄 처리 SDK 방법을 tooenable 자동 크기 조정을 제공합니다. 예:

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync](Batch .NET)
* [풀에서 자동 크기 조정 사용][rest_enableautoscale] (REST API)

기존 풀에서 자동 크기 조정을 사용 하도록 설정 하면 주의 hello 지점 다음에 유의 하십시오.

* 자동 크기 조정을 현재에서 해제 되 면 hello 풀 hello 요청 tooenable 자동 크기 조정 실행 하면, hello 요청을 실행할 유효한 자동 크기 조정 수식을 지정 해야 합니다. 필요에 따라 자동 크기 조정 평가 간격을 지정할 수 있습니다. 간격을 지정 하지 않으면 hello 기본값인 15 분이 사용 됩니다.
* 자동 크기 조정이 hello 풀에서 현재 사용 하는 경우에 자동 크기 조정 수식 평가 간격, 또는 둘 다 지정할 수 있습니다. 이러한 속성 중 하나 이상을 지정해야 합니다.

  * 새 자동 크기 조정 평가 기간을 지정 하면 hello 기존 평가 일정 중지 되 고 새 일정을 시작 하는 것입니다. hello 새 일정의 시작 시간은 hello는 hello 요청 tooenable 자동 크기 조정 발급 된 시간을 시작 합니다.
  * 어느 hello 자동 크기 조정 수식 또는 계산 간격을 생략 하면 hello 일괄 처리 서비스는 hello toouse 해당 설정의 현재 값을 계속 합니다.

> [!NOTE]
> Hello에 대 한 값을 지정한 경우 *targetDedicatedComputeNodes* 또는 *targetLowPriorityComputeNodes* hello의 매개 변수 **CreatePool** hello를 만들 때 메서드 수식을 확장 자동 hello 계산 하는 경우.net, 또는 다른 언어를 다음 그러한 값에 hello 비교 가능한 매개 변수에 대 한 풀은 무시 됩니다.
>
>

이 C# 코드 조각은 hello를 사용 하 여 [일괄 처리.NET] [ net_api] 기존 풀에서 라이브러리 tooenable 자동 크기 조정 기능:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>자동 크기 조정 수식 업데이트

기존 자동 크기 조정 가능한 풀, 호출 hello 작업 tooenable 자동 크기 조정 hello 새 수식 사용 하 여 다시에서 tooupdate hello 수식입니다. 예를 들어, 자동 크기 조정에서 이미 사용 되 면 `myexistingpool` hello 다음.NET 코드를 실행 하면 해당 자동 크기 조정 수식이 아래 템플릿으로 바뀝니다 hello 내용의 `myNewFormula`합니다.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>업데이트 hello 자동 크기 조정 간격

hello 자동 크기 조정 평가 간격은 기존 자동 크기 조정 가능한 풀, 호출 hello 작업 tooenable 자동 크기 조정 hello 새 간격을 사용 하 여 다시의 tooupdate 하 고 있습니다. 예를 들어 tooset hello 자동 크기 조정 평가 간격 too60 (분)는 이미.NET에서 자동 크기 조정 사용 하는 풀에:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>자동 크기 조정 수식 평가

수식을 tooa 풀 적용 하기 전에 평가할 수 있습니다. 이러한 방식으로 hello 수식 toosee hello 수식을 프로덕션 환경에 배포 하기 전에 해당 문을 평가 하는 방법을 테스트할 수 있습니다.

자동 크기 조정 수식이 tooevaluate 먼저 유효한 수식 사용 하 여 hello 풀에서 자동 크기 조정을 설정 해야 합니다. tootest 아직 없는 경우 자동 크기 조정 하는 풀에 대 한 수식을 사용 하도록 설정 사용 하 여 hello 한 줄 수식을 `$TargetDedicatedNodes = 0` 자동 크기 조정 기능을 먼저 활성화 합니다. 그런 다음 다음 tootest 원하는 tooevaluate hello 수식을 hello 중 하나를 따릅니다.

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 또는 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    이러한 일괄 처리.NET 메서드는 기존 풀과 hello 자동 크기 조정 수식 tooevaluate를 포함 하는 문자열의 hello ID가 필요 합니다.

* [자동 크기 조정 수식 평가](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    이 REST API 요청 URI, hello에 hello 풀 ID를 지정 하 고 hello에 대 한 자동 크기 조정 수식을 hello *autoScaleFormula* hello 요청 본문의 요소입니다. hello 연산의 hello 응답 관련된 toohello 수식이 될 수 있는 오류 정보를 포함 합니다.

이 [Batch .NET][net_api] 코드 조각에서는 자동 크기 조정 수식을 평가합니다. Hello 풀에 사용 하도록 설정 하는 자동 크기 조정 설정 여부 것 먼저 합니다.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

이 코드 조각에 표시 하는 hello 수식의 성공적인 평가 비슷한 결과 생성 합니다.

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>자동 크기 조정 실행에 대한 정보 가져오기

tooensure 수식으로 수행 하는 예상 하면 풀에 대해 일괄 처리를 수행 하는 hello 자동 크기 조정 실행의 hello 결과 주기적으로 확인 하는 것이 좋습니다. toodo, get (또는 새로 고침) 참조 toohello, 풀 및 해당 마지막 자동 크기 조정 실행의 hello 속성을 검사 합니다.

일괄 처리.net에서 hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) 속성에는 hello 최신 자동 크기 조정을 수행 hello 풀에서 실행 하는 방법에 대 한 정보를 제공 하는 여러 속성이 있습니다.

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

REST API hello에 hello [풀에 대 한 정보를 가져올](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) hello 최신 자동 크기 조정을 hello에서 실행 되는 정보를 포함 하는 hello 풀에 대 한 정보를 반환 하는 요청 [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) 속성.

hello 다음 C# 코드 조각 정보 사용 하 여 hello 일괄 처리.NET 라이브러리 tooprint hello 마지막 자동 크기 조정 풀에서 실행 하는 방법에 대 한 _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Hello 조각 앞의 예제 출력:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>자동 크기 조정 수식 예제
풀의 계산 리소스의 다양 한 방법 tooadjust hello 크기를 표시 하는 몇 가지 수식을 살펴보겠습니다.

### <a name="example-1-time-based-adjustment"></a>예제1: 시간 기반 조정
Hello 요일 hello 및 하루 중 시간에 따라 tooadjust hello 풀 크기를 한다고 가정 합니다. 이 예제는 hello의 노드 hello 수 tooincrease 또는 감소를 그에 따라 풀을 보여줍니다.

hello 수식은 먼저 hello를 현재 시간 가져옵니다. 요일 (1-5) 이면 및 작업 시간 (오전 8 시 too6 PM), hello 대상 풀 크기는 too20 노드를 설정 합니다. 그렇지 않으면 too10 노드는 설정 합니다.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>예제2: 작업 기반 조정
이 예제에서는 hello 풀 크기는 hello hello 큐에 있는 작업 수에 따라 조정 됩니다. 주석과 줄 바꿈은 모두 수식 문자열에 허용됩니다.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>예제3: 병렬 작업에 대한 회계
이 예제에서는 작업 hello 수에 따라 hello 풀 크기를 조정 합니다. 이 수식에서는 계정 hello에도 사용 [MaxTasksPerComputeNode] [ net_maxtasks] hello 풀에 대해 설정 된 값입니다. 이 방법은 [병렬 작업 실행](batch-parallel-node-tasks.md)이 풀에서 사용된 경우에 특히 유용합니다.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>예제4: 초기 풀 크기 설정
이 예제에서는 C# 코드 조각 설정 하는 자동 크기 조정 수식 사용 하 여 hello 풀 크기 tooa 초기 시간 기간에 대 한 노드 수를 지정 합니다. Hello 실행 수에 따라 hello 풀 크기를 조정 하 고 hello 초기 기간 후 활성 작업 기간이 경과 합니다.

다음 코드 조각 hello에 hello 수식:

* Hello 초기 풀 크기 toofour 노드를 설정합니다.
* Hello 풀 크기를 hello 내에서 처음 10 분 hello 풀의 수명 주기 조정 되지 않습니다.
* 10 분 후 hello의 최대값을 가져옵니다 hello 내에서 작업 실행 수 및 활성 hello 지난 60 분입니다.
  * 두 값이 0 (작업이 없는 되었는지 실행 중이거나 hello에 활성 지난 60 분을 나타냄) 인 경우 hello 풀 크기 too0을 설정 됩니다.
  * 값 중 하나가 0보다 큰 경우 변경되지 않습니다.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>다음 단계
* [동시 노드 작업과 Azure 배치 계산 리소스 사용량을 최대화](batch-parallel-node-tasks.md) 어떻게에 실행할 수 있습니다 여러 작업이 동시에 풀의 계산 노드 hello에 대 한 세부 정보를 포함 합니다. 또한 tooautoscaling,이 기능은 도움이 될 수 있습니다 toolower 작업 기간을 일부 워크 로드에 비용을 절약할 수 있습니다.
* 다른 효율성 부스터 일괄 처리 응용 프로그램 쿼리 hello hello 최적의 방법으로 대부분의 일괄 처리 서비스는 장애 조치 합니다. 참조 [hello Azure 배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md) toolearn toolimit hello 잠재적으로 수천 대의 hello 상태를 쿼리할 때 hello 와이어 교차 하는 데이터 양을 방법 계산 노드 또는 작업입니다.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
