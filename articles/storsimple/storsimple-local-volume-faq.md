---
title: "aaaStorSimple 로컬 고정 볼륨 FAQ | Microsoft Docs"
description: "StorSimple에 대 한 질문 로컬 고정 볼륨 답변 toofrequently 묻는 제공 합니다."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 7a2f4b1a-4ac9-4ce1-9359-bd40a9cbbb5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/11/2017
ms.author: manuaery
ms.openlocfilehash: 6a0c742acea836c2b960cb604e4010bcb08c3169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>StorSimple 로컬로 고정된 볼륨: 질문과 대답(FAQ)
## <a name="overview"></a>개요
hello 다음은 질문 및 답변 로컬로 고정 된 StorSimple 볼륨을 만들 때 발생할 수 있습니다는 계층화 된 볼륨 tooa 로컬로 고정 된 볼륨으로 변환 (및 그 반대로)를 백업 하 고 로컬로 고정 된 볼륨을 복원 합니다.

질문 및 답변 hello 범주를 다음으로 정렬 된

* 로컬로 고정된 볼륨 만들기
* 로컬 고정된 백업
* 계층화 된 볼륨 tooa 로컬로 고정 된 볼륨으로 변환
* 로컬로 고정된 볼륨 복원
* 로컬로 고정된 볼륨 장애 조치

## <a name="questions-about-creating-a-locally-pinned-volume"></a>로컬로 고정된 볼륨 만들기에 대한 질문
**Q.** Hello hello 8000 시리즈 장치에 만들 수 있습니다 하는 로컬 고정된 볼륨의 최대 크기는 무엇입니까?

**A** StorSimple 8000 시리즈 업데이트 3.0을 실행 하는 장치에 too8.5 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 구성할 수 있습니다. Hello 큰 8600 장치의 too22.5 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다.    
장치에서 StorSimple 8000 시리즈 업데이트 실행 2.x too8 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 구성할 수 있습니다. Hello 큰 8600 장치의 too20 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다.   

**Q.** 최근에 2.0 내 8100 장치 tooUpdate를 업그레이드 하 고 hello 최대 사용 가능한 크기는 6 t B 및 8TB 하지를 할 때 로컬 고정된 볼륨 toocreate 합니다. 8TB 볼륨을 만들 수 없는 이유는?

**A** 장치 업데이트 2.0에서 실행 중인 too8 TB 로컬로 고정 된 볼륨을 프로 비전 할 수 또는 계층화 된 볼륨에 too200 TB hello 8100 장치입니다. 이미 장치에 볼륨을 계층에, 그에 따라이 최대 한도 보다 낮은으로 로컬로 고정 된 볼륨을 만드는 데 사용할 수 있는 hello 공간이 됩니다. 예를 들어, 계층화 된 볼륨의 최대 100TB 8100 장치에 이미 배포 되어 (용량 계층형 hello의 절반 이상), hello hello 8100 장치에서 만들 수 있는 로컬 볼륨의 최대 크기 (약 절반 줄어듭니다 too4 TB 됩니다 hello 최대 로컬 고정 볼륨 용량).

Hello 장치의 로컬 공간이 사용 되는 toohost hello 작업 계층화 된 볼륨의 집합 이므로 hello 장치에 볼륨을 계층화 된 경우 로컬 고정된 볼륨 만들기 위한 사용 가능한 공간 hello 줄어듭니다. 반대로, 그에 따라 로컬 고정된 볼륨 만들기 hello 사용 가능한 공간을 계층화 된 볼륨을 줄입니다. 로컬로 고정 된 볼륨을 만들 때 다음 표는 hello hello hello 8100 및 8600 장치의 사용 가능한 계층화 된 용량을 요약 합니다.

####<a name="update-30"></a>업데이트 3.0 
| 로컬로 고정된 볼륨이 프로비전된 용량 | 사용 가능한 용량 toobe 8100-계층화 된 볼륨에 대 한 프로 비전 | 사용 가능한 용량 toobe 8600-계층화 된 볼륨에 대 한 프로 비전 |
| --- | --- | --- |
| 0 |200TB |500TB |
| 1TB |176.5TB |477.8TB |
| 4TB |105.9TB |411.1TB |
| 8.5TB |0TB |311.1TB |
| 10TB |해당 없음 |277.8TB |
| 15TB |해당 없음 |166.7TB |
| 22.5TB |해당 없음 |0TB |

####<a name="update-2x"></a>업데이트 2.x  
 | 로컬로 고정된 볼륨이 프로비전된 용량 | 사용 가능한 용량 toobe 8100-계층화 된 볼륨에 대 한 프로 비전 | 사용 가능한 용량 toobe 8600-계층화 된 볼륨에 대 한 프로 비전 |  
 | --- | --- | --- |  
 | 0 |200TB |500TB |  
 | 1TB |25TB |475TB |  
 | 4TB |100TB |400TB |  
 | 8TB |0TB |300TB |  
 | 10TB |해당 없음 |250TB |  
 | 15TB |해당 없음 |125TB |  
 | 20TB |해당 없음 |0TB |   

**Q.** 로컬로 고정된 볼륨 만들기가 장기 실행 작업인 이유는? 

**A.** 로컬로 고정된 볼륨은 씩 프로비전됩니다. toocreate 공간 hello hello 장치의 로컬 계층, 기존 계층화 된 볼륨에서 일부 데이터 hello를 프로 비전 프로세스 중 toohello 클라우드 푸시할 수 있습니다. 고 hello 시간 이동 toocreate 로컬 볼륨에는 몇 시간 수 있으므로 hello hello 볼륨 프로 비전 hello 장치와 hello 사용 가능한 대역폭 toohello 클라우드를 기존 데이터 크기에 따라 다릅니다.

**Q.** 얼마나 오래 걸립니까 toocreate 로컬 고정된 볼륨?

**A.** 로컬로 고정 된 볼륨은 씩 프로 비전, 때문에 계층화 된 볼륨에서 일부 기존 데이터 hello를 프로 비전 프로세스 중 toohello 클라우드를 푸시 될 수 있습니다. 따라서 hello에 걸린 시간 toocreate 로컬 고정된 볼륨 hello 볼륨의 hello 크기를 비롯 한 여러 요인에 따라 달라 집니다 장치의 데이터에 hello 및 사용 가능한 대역폭 hello 합니다. 에 볼륨이 없으면 새로 설치 된 장치에서는 hello 시간 toocreate 로컬로 고정 된 볼륨 데이터 테라바이트 당 약 10 분입니다. 그러나 로컬 볼륨 만들기에 사용 중인 장치에서 위에서 설명한 hello 요인에 따라 몇 시간이 걸릴 수 있습니다.

**Q.** 로컬 고정된 볼륨 toocreate를 하겠습니다. 유용한 toobe 인식 필요 한가요 있나요?

**A.** 로컬로 고정 된 볼륨은 대기 시간이 중요 한 toocloud 되며 항상 데이터의 로컬 보증을 요구 하는 작업에 적합 합니다. 작업에 대 한 로컬 볼륨의 사용을 고려 하십시오 hello 다음 고려해 야 합니다.

* 로컬로 고정 된 볼륨은 씩 프로 비전 및 hello 사용 가능한 공간을 계층화 된 볼륨을 한 영향 로컬 볼륨 만들기. 따라서 더 작은 크기의 볼륨을 시작하고 저장소 요구 사항이 증가하면 확장하는 것이 좋습니다.
* 로컬 볼륨의 프로 비전은 toohello 클라우드 계층화 된 볼륨에서에서 기존 데이터를 푸시할 수 반하는 장기 실행 작업입니다. 결과적으로, 이러한 볼륨의 성능이 저하될 수 있습니다.
* 로컬 볼륨의 프로비전은 시간이 오래 걸리는 작업입니다. 여러 요소에 따라 관련 된 실제 시간 hello: hello hello 볼륨을 프로 비전 되 고, 장치 및 사용 가능한 대역폭에 대 한 데이터의 크기입니다. 기존 볼륨 toohello 클라우드, 백업 되지 않은 경우 볼륨 만들기는 속도가 느립니다. 로컬 볼륨을 프로비전하기 전에 기존 볼륨의 클라우드 스냅숏을 만드는 것이 좋습니다.
* 기존의 계층화 된 볼륨이 고정 toolocally 볼륨 변환한이 변환은 프로 비전 (더하기 toobringing hello 클라우드에서 계층형된 데이터 [해당 되는 경우] 아래로)에서 로컬 고정된 볼륨으로 인해 발생 하는 hello에 대 한 hello 장치에 공간을 포함 합니다. 다시, 위에서 설명한 요인에 따라 결정되는 장기 실행 작업입니다. Hello 프로세스 속도 느려집니다도 기존 볼륨을 백업 되지 않은 경우 처럼 기존 볼륨 이전 tooconversion를 백업 하는 것이 좋습니다. 또한 이 과정에서 장치의 성능이 감소할 수 있습니다.

방법에 대 한 자세한 내용은 너무[로컬 고정된 볼륨 만들기](storsimple-manage-volumes-u2.md#add-a-volume)

**Q.** Hello에 여러 개의 로컬 고정된 볼륨을 만들 수 동시?

**A.** 예, 하지만 로컬로 고정된 볼륨 만들기 및 확장 작업은 순차적으로 처리됩니다.

로컬로 고정 된 볼륨은 씩 프로 비전 하 고이에서는 (있음 기존 데이터를 계층화 된 볼륨 toobe hello를 프로 비전 프로세스 중 toohello 클라우드 푸시 될 수 있습니다) hello 장치의 로컬 공간을 만들어야 합니다. 따라서 프로비전 작업이 진행 중이면 해당 작업이 완료될 때까지 다른 로컬 볼륨 만들기 작업은 큐에 대기됩니다.

마찬가지로, 기존 로컬 볼륨 확장 되 나 계층화 된 볼륨을 변환 되는 경우 tooa 로컬 고정 볼륨 다음 hello 새 로컬 고정된 볼륨 만들기는 큐에 대기 hello 이전 작업이 완료 될 때까지 합니다. 로컬로 고정 된 볼륨의 hello 크기를 확장 합니다. 해당 볼륨에 대 한 기존 로컬 공간 hello의 hello 확장을 작업이 포함 됩니다. 계층화 된 toolocally 고정 된 볼륨에서 변환에는 로컬 고정된 볼륨으로 인해 발생 하는 hello에 대 한 로컬 공간이 hello 만들기도를 포함 됩니다. 이러한 작업 모두에서 로컬 공간의 만들기 또는 확장은 장기 실행 작업입니다.

Hello에 이러한 작업을 볼 수 **작업** hello Azure StorSimple Manager 서비스의 페이지입니다. hello 적극적으로 처리 되 고 있는 작업은 계속 해 서 공간에 프로 비전의 tooreflect hello 진행 상태를 업데이트 합니다. hello 남아 있는 로컬 고정된 볼륨 작업 실행 중으로 표시 된 하지만 진행률은 중단 되 고 지연 된 hello 순서 대로 선택 됩니다.

**Q.** 로컬로 고정된 볼륨을 삭제했습니다. 공간 회수 hello 반영 hello 사용 가능한 공간에 toocreate 때 새 볼륨을 볼 수 없는? 

**A.** 로컬로 고정 된 볼륨을 삭제 하면 hello 공간 새 볼륨에 사용할 수 있는 즉시 업데이트 되지 않을 수 있습니다. hello StorSimple Manager 서비스는 사용 가능한 로컬 공간 hello 약 1 시간 마다 업데이트 됩니다. Toocreate hello 새 볼륨을 시도 하기 전에 1 시간 동안 대기 하는 것이 좋습니다.

**Q.** Hello 클라우드 어플라이언스에 로컬 고정된 볼륨이 지원 되나요?

**A.** Hello 클라우드 어플라이언스에 (8010 및 8020 장치 이전의 참조 tooas hello StorSimple 가상 장치)는 로컬 고정된 볼륨이 지원 되지 않습니다.

**Q.** Azure PowerShell cmdlet toocreate hello를 사용 하 여을 로컬로 고정 된 볼륨을 관리할 수 있습니까? 

**A.** 아니요, Azure PowerShell cmdlet을 통해 로컬로 고정된 볼륨을 만들 수 없습니다(Azure PowerShell을 통해 만든 볼륨은 계층화됨). 또한 추가할 수는 사용 하지 않는 hello Azure PowerShell cmdlet toomodify 로컬로 고정 된 볼륨의 속성 수정 hello 볼륨 유형 tootiered의 원하지 않는 효과 hello 하 것 처럼 있습니다.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>로컬로 고정된 볼륨 백업에 대한 질문
**Q.** 로컬로 고정된 볼륨의 로컬 스냅숏이 지원되나요?

**A.** 예, 로컬로 고정된 볼륨의 로컬 스냅숏을 사용할 수 있습니다. 그러나 재해에 대비해 hello 로컬 고정된 볼륨에 데이터를 보호 하는 클라우드 스냅숏 tooensure와를 백업 하면 정기적으로 하는 것이 좋습니다.

**Q.** 로컬로 고정된 볼륨에서 로컬 스냅숏을 관리하기 위한 지침이 있나요?

**A.** 높은 수준의 데이터와 함께 로컬 스냅숏을 자주 변동 hello 로컬로 고정 된 볼륨 때문 로컬 공간을 많이 hello 장치 toobe 및 밀어 넣는 toohello 클라우드 계층화 된 볼륨에서 데이터가 생성 될 수 있습니다. 따라서 hello 로컬 스냅숏 수를 최소화 하는 것이 좋습니다.

**Q.** 로컬로 고정 볼륨의 내 로컬 스냅숏이 무효화될 수 있다는 경고가 나타났습니다. 언제 발생할 수 있나요?

**A.** 높은 수준의 데이터와 함께 로컬 스냅숏을 자주 고정 된 볼륨 빠르게 사용 하는 hello 장치 toobe에서 로컬 공간을 발생할 수 있습니다 로컬로 hello 변동 합니다. Hello 장치의 로컬 계층 hello는 많이 사용 하는 경우, 꽉 차지 하는 hello 장치 확장된 클라우드 중단 될 수 있습니다. 및 들어오는 쓰기 toohello 볼륨 (있어 공간이 없으면 tooupdate hello 스냅숏을 toorefer hello 스냅숏이 무효화 될 수 있습니다. toohello 이전 블록 덮어썼습니다 데이터). 이러한 상황 hello 쓰기 toohello 볼륨 toobe served hello 로컬 스냅숏 잘못 되었을 수 있지만 계속 됩니다. 클라우드 스냅숏이 기존 없습니다 영향 tooyour 있습니다.

hello 경고 경고는 toonotify 해당 예외의 발생 하는 hello 로컬 스냅숏을 자주 또는 더 이상 삭제 하는 중 오래 된 로컬 스냅숏이 덜 tootake 예약 동일 하거나 로컬 스냅숏을 검토 하 여 적절 한 시기에 해결 확인 필수.

Hello 로컬 스냅숏이 무효화 hello 특정 백업 정책의 로컬 스냅숏 hello hello 목록이 hello 로컬 스냅숏 무효화의 타임 스탬프와 함께 무효화 된 알려 주는 정보 알림을 받게 됩니다. 이러한 스냅숏은 자동 삭제 되며 수 tooview 더 이상 됩니다 hello에서 해당 **백업 카탈로그** hello Azure 클래식 포털에서에서 페이지입니다.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>계층화 된 볼륨 tooa 로컬로 고정 된 볼륨을 변환 하는 방법에 대 한 질문
**Q.** 계층화 된 볼륨 tooa 로컬로 고정 된 볼륨을 변환 하는 동안 hello 장치에서 만료 경고를 관찰 중 I. 이것이 발생하는 이유는? 

**A.** hello 변환 프로세스에는 두 단계로 이루어집니다. 

1. 프로 비전 hello에 대 한 hello 장치에 공간을 볼륨 로컬로 고정 곧-에--변환 합니다.
2. 보장 hello 클라우드 tooensure 로컬에서 모든 계층 구성된 데이터를 다운로드 합니다.

다음이 단계 중에 모두 긴 hello 볼륨 변환 중인 hello 장치 및 사용 가능한 대역폭에 대 한 데이터의 hello 크기에 의존 하는 작업을 실행 합니다. 기존의 계층화 된 볼륨에서 일부 데이터는 hello 프로 비전 프로세스의 일부로 toohello 클라우드 spill 수,으로 장치는이 시간 동안 성능이 저하를 경험할 수 있습니다. 또한 hello 변환 프로세스 속도가 느릴 수 하는 경우:

* 기존 볼륨 toohello 클라우드;를 백업 되지 않았습니다. 되므로 볼륨 이전 tooinitiating 변환을 백업 하는 것이 좋습니다.
* 대역폭 제한 정책은 적용 된 hello 사용 가능한 대역폭 toohello 클라우드; 제한 될 수 있습니다는 따라서 전용된 40mbps 또는 더 많은 연결 toohello 클라우드를 설정한 것이 좋습니다.
* hello 변환 프로세스; 위에서 설명한 toohello 여러 요소로 인해 몇 시간이 걸릴 수 있습니다. 따라서 좋습니다 최대치 외 시간 동안 이나 주말 tooavoid에이 작업을 수행 하는 hello 최종 소비자에 미치는 영향입니다.

방법에 대 한 자세한 내용은 너무[계층화 된 볼륨 tooa 로컬로 고정 된 볼륨으로 변환](storsimple-manage-volumes-u2.md#change-the-volume-type)

**Q.** Hello 볼륨 변환 작업을 취소할 수 있습니까?

**A.** 아니요, 취소 hello 변환 작업이 시작 되 면 hello 수 없습니다. Hello 이전 질문에 설명한 대로에 주의 해야 hello 잠재적 성능 문제 hello 과정에서 발생할 수 있습니다 및 변환을 계획할 때 위에 나열 된 hello 모범 사례를 따라야 합니다.

**Q.** Toomy 볼륨 hello 변환 작업에 실패 하면 어떻게 됩니까?

**A.** 볼륨으로의 변환 toocloud 연결 문제로 인해 실패할 수 있습니다. 결국 hello 장치 일련의 실패 한 시도 toobring hello 클라우드에서 데이터를 계층화 된 후 hello 변환 프로세스를 중지할 수 있습니다. 이러한 시나리오에서는 hello 볼륨 종류가 toobe hello 원본 볼륨 유형 이전 tooconversion, 계속 및:

* 중요 한 알림이 발생된 toonotify 됩니다 hello 볼륨 변환 오류. 자세한 내용은 [관련된 toolocally 고정 된 볼륨 경고](storsimple-manage-alerts.md#locally-pinned-volume-alerts)
* 로컬로 고정 된 계층화 된 tooa 볼륨을 변환 하는 경우 데이터 hello 클라우드에서 계속 있을 수도 있습니다 hello 볼륨 계층화 된 볼륨의 tooexhibit 속성 계속 됩니다. Hello 연결 문제를 해결 한 다음 hello 변환 작업을 다시 시도 하는 것이 좋습니다.
* 마찬가지로, 로컬로 고정 된 tooa에서 변환 hello 볼륨 로컬로 고정 된 볼륨으로 표시할 수는 있지만 볼륨 실패 하는 계층을 지정할 때 작동지 것입니다 계층화 된 볼륨으로 (이므로 toohello 클라우드 데이터를 유출 있을 수 없습니다). 그러나 hello 장치의 hello 로컬 계층에 toooccupy 공간을 계속 됩니다. 이 공간은 다른 로컬로 고정된 볼륨에 사용할 수 없습니다. 이 작업 tooensure hello 볼륨 변환 작업이 완료 되 고 hello hello 장치의 로컬 공간을 확보할 수 있는 다시 시도 하는 것이 좋습니다.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>로컬로 고정된 볼륨 복원에 대한 질문
**Q.** 로컬로 고정된 볼륨이 즉시 복원되나요?

**A.** 네, 로컬로 고정된 볼륨이 즉시 복원됩니다. Hello 볼륨에 대 한 메타 데이터 정보 hello hello 복원 작업의 일부로 hello 클라우드에서 끌어온,으로 hello 볼륨이 온라인 상태가 되 고 hello 호스트에서 액세스할 수 있습니다. 그러나 데이터 hello 클라우드에서 모든 hello 데이터 다운로드를 발생할 수 있습니다 때까지 표시 되지 않을 hello 볼륨에 대 한 로컬 보장 hello 복원 hello 기간에 대 한 이러한 볼륨에서 성능이 줄어듭니다.

**Q.** 얼마나 오래 걸립니까 toorestore 로컬 고정된 볼륨?

**A.** 로컬 고정된 볼륨이 즉시 복원 되며 hello 볼륨 데이터 계속 toobe hello 백그라운드로 다운로드 되는 동안 hello 클라우드에서 hello 볼륨 메타 데이터 정보가 검색 되는 즉시 온라인 상태로 전환 됩니다. 이 두 번째 부분에서는 hello 볼륨 데이터-에 대 한 로컬 보장 hello를 다시 가져오는-hello 복원 작업은 장기 실행 작업 및 모든 hello 데이터 toobe 로컬로 다시 생성 하는 데 몇 시간이 걸릴 수 있습니다. hello에 걸린 시간 toocomplete hello hello 복원할 hello 볼륨 크기와 같은 여러 요소에 따라 동일 하 고 사용 가능한 대역폭 hello 합니다. 복원 중인 hello 원래 볼륨 삭제 되었지만 추가 시간이 toocreate hello hello 복원 작업의 일부로 hello 장치의 로컬 공간을 수행 됩니다.

**Q.** 고정 된 볼륨 tooan 오래 된 스냅숏 (hello 볼륨 계층을 지정할 때 수행) 기존 로컬로 toorestore가 필요 합니다. Hello 볼륨은이 예제의 계층으로 복원할 수 있습니까?

**A.** 아니요, hello 볼륨을 로컬 고정된 볼륨으로 복원 됩니다. 되지만 hello 스냅숏 날짜 toohello 시간 때 hello 볼륨 된 계층, 기존 볼륨을 복원 하는 동안 StorSimple 항상 사용 볼륨의 hello 종류 hello 디스크에 현재 존재 합니다.

**Q.** 내 로컬 고정된 볼륨을 최근에 확장 I 하지만 hello 볼륨 크기가 더 작은 된 toorestore hello 데이터 tooa 시간 필요 합니다. 복원 hello 현재 볼륨 조정 하 고 필요 hello 볼륨의 tooextend hello 크기 hello 복원이 완료 되 면?

**A.** 예, hello 복원 hello 볼륨 크기를 조정 하 고 hello 복원이 완료 된 후 hello 볼륨의 tooextend hello 크기가 필요 합니다.

**Q.** 복원 중 hello 유형의 볼륨을 변경할 수 있나요?

**1.**아니요, 복원 중 hello 볼륨 종류를 변경할 수 없습니다.

* 삭제 된 볼륨 hello 스냅숏에 저장 된 hello 종류로 복원 됩니다.
* Hello 스냅숏에 저장 된 hello 형식에 관계 없이 자신의 현재 형식에 따라 기존 볼륨이 복원 됩니다 (이전 두 toohello 질문 참조).

**Q.** 내 로컬 고정된 볼륨 toorestore 필요 하지만 스냅숏 시간에에서 잘못 된 지점 선택한 합니다. Hello 현재 복원 작업을 취소할 수 있습니까?

**A.** 예, 진행 중인 복원 작업을 취소할 수 있습니다. hello 볼륨의 hello 상태가 롤백되어 toohello 상태 hello 복원의 시작 부분 hello에 있습니다. 그러나 모든 된 쓰기 toohello 볼륨 hello 복원 진행 중인 동안 손실 됩니다.

**Q.** 내 로컬로 고정된 볼륨 중 하나에서 복원 작업을 시작했지만 이제 만들기를 다시 수집하지 않는 내 백로그 카탈로그에 스냅숏을 표시합니다. 이 용도는 무엇인가요?

**A.** 이전 toohello 복원 작업이 만들어지고 hello 복원을 취소 되거나 실패 한 경우에 롤백을 위해 사용 하는 hello 임시 스냅숏입니다. 이 스냅숏을 삭제 하지 마십시오 hello 복원이 완료 되 면 자동으로 삭제 됩니다. 복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 계층화 된 볼륨에만 있는 hello 복원 작업의 경우,이 문제가 발생 하지 않습니다.

**Q.** 로컬로 고정된 볼륨을 복제할 수 있나요?

**A.** 예, 할 수 있습니다. 그러나 기본적으로 hello 로컬로 고정 된 볼륨을 계층화 된 볼륨으로 복제할 수 됩니다. 방법에 대 한 자세한 내용은 너무[로컬로 고정 된 볼륨을 복제](storsimple-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>로컬로 고정된 볼륨 장애 조치에 대한 질문
**Q.** 내 장치 tooanother 물리적 장치를 통해 toofail이 필요합니다. 내 로컬로 고정된 볼륨이 로컬로 고정되거나 계층화되어 실패하나요?

**A.** Hello hello 대상 장치의 소프트웨어 버전에 따라 로컬 고정된 볼륨이 조치할로:

* Hello 대상 장치에서 StorSimple 8000을 실행 하는 경우 로컬로 고정 시리즈 업데이트 2
* Hello 대상 장치에서 StorSimple을 실행 하는 경우 계층 8000 시리즈 업데이트 1.x
* Hello 대상 장치가 hello 클라우드 어플라이언스에 이면 계층 (소프트웨어 버전 업데이트 2 또는 1.x 업데이트)

자세한 내용은 [버전에 걸쳐 로컬로 고정된 볼륨의 장애 조치 및 DR](storsimple-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**Q.** 로컬로 고정된 볼륨이 DR(재해 복구) 중에 즉시 복원되나요?

**A.** 네, 장애 조치 중에 로컬로 고정된 볼륨이 즉시 복원됩니다. Hello 볼륨에 대 한 메타 데이터 정보 hello hello 장애 조치 작업의 일부로 hello 클라우드에서 끌어온,으로 hello 볼륨 hello 대상 장치에서 온라인 상태로 전환 및 hello 호스트에서 액세스할 수 있습니다. 한편, hello 볼륨 데이터 toodownload hello 백그라운드에서 계속 있으며 hello hello 장애 조치 동안 이러한 볼륨에서 성능이 저하를 발생할 수 있습니다.

**Q.** Hello 장애 조치 작업을 완료 했지만 표시, 추적 하려면 어떻게 해야 로컬 고정 볼륨이 복원 중인 hello 진행률 hello 대상 장치에 있습니까?

**A.** 장애 조치를 수행 하는 동안 hello 장애 조치 집합의 모든 hello 볼륨이 즉시 복원 하 고 hello 대상 장치에서 온라인 상태로 전환 되 면 hello 장애 조치 작업 완료 상태로 표시 됩니다. 로컬로 고정 된 볼륨을 수 있는 장애 조치 한; 여기에 그러나 hello 데이터의 로컬 보증 hello 볼륨에 대 한 모든 hello 데이터 다운로드 될 때만 제공 됩니다. Hello 장애 조치의 일부로 만들어진 hello 해당 하는 복원 작업 모니터링를 하나씩 못한 각 로컬 고정된 볼륨에 대 한이 진행률을 추적할 수 있습니다. 이러한 개별 복원 작업은 로컬로 고정된 볼륨에 대해서만 만들어집니다.

**Q.** 장애 조치 중 hello 유형의 볼륨을 변경할 수 있나요?

**A.** 아니요, 장애 조치 중 hello 볼륨 종류를 변경할 수 없습니다. 물리적 tooanother를 통해 실패 하는 경우 StorSimple 8000 시리즈 업데이트 2 일 hello 볼륨 실행 중인 장치를 조치할 hello 스냅숏에 저장 된 hello 볼륨 형식을 기반으로 합니다. Tooany 장애 조치할 때 다른 장치 버전 toohello 위에 있는 질문 hello 볼륨 종류가 장애 조치 후를 참조 하십시오.

**Q.** 있습니까 장애 조치할 수 볼륨 컨테이너와 로컬 고정된 볼륨이 toohello 클라우드 어플라이언스에?

**A.** 예, 할 수 있습니다. 로컬로 고정 hello 볼륨 계층화 된 볼륨으로 장애 조치 됩니다. 자세한 내용은 [버전에 걸쳐 로컬로 고정된 볼륨의 장애 조치 및 DR](storsimple-device-failover-disaster-recovery.md#considerations-for-device-failover)

