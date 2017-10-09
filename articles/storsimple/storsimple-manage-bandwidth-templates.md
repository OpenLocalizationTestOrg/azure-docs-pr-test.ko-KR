---
title: "aaaManage StorSimple 대역폭 템플릿을 | Microsoft Docs"
description: "설명 방법을 toomanage StorSimple 대역폭 템플릿을 toocontrol 대역폭 사용을 허용 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a>Hello StorSimple 관리자 서비스 toomanage StorSimple 대역폭 템플릿을 사용 하 여
## <a name="overview"></a>개요
대역폭 템플릿을 여러 시간에 일정이 tootier hello 데이터로 hello StorSimple 장치 toohello 클라우드 간에 tooconfigure 네트워크 대역폭 사용량 사용.

일정을 제한하는 대역폭을 사용하면 다음과 같은 작업을 수행할 수 있습니다.

* Hello 작업 네트워크 사용량에 따라 사용자 지정 된 대역폭 일정을 지정 합니다.
* 관리를 중앙 집중화 하 고 쉽고 원활한 방식으로 여러 장치 간에 hello 일정을 다시 사용 합니다.

> [!NOTE]
> 이 기능은 가상 장치가 아닌 StorSimple 물리적 장치에 대해서만 사용할 수 있습니다.
> 
> 

서비스에 대 한 모든 hello 대역폭 템플릿을 표 형식으로 표시 하며 hello 다음 정보를 포함 합니다.

* **이름** -할당 된 고유한 이름 toohello 대역폭 템플릿을 만들 때.
* **일정** – hello에 지정된 된 대역폭 템플릿에 포함 된 일정의 수입니다.
* **사용 하는** – hello hello 대역폭 템플릿을 사용 하 여 볼륨의 수입니다.

Hello StorSimple Manager 서비스를 사용 하 여 **구성** hello Azure 클래식 포털 toomanage 대역폭 템플릿의 페이지.

또한 toohelp 대역폭 템플릿을 구성 하는 추가 정보를 찾을 수 있습니다에:

* 대역폭 템플릿에 대한 질문과 대답
* 대역폭 템플릿에 대한 모범 사례

## <a name="add-a-bandwidth-template"></a>대역폭 템플릿 추가
Hello 단계 toocreate 새 대역폭 템플릿을 다음을 수행 합니다.

#### <a name="tooadd-a-bandwidth-template"></a>대역폭 템플릿 tooadd
1. Hello StorSimple Manager 서비스에서 **구성** 페이지 **대역폭 템플릿 추가/편집**합니다.
2. Hello에 **대역폭 템플릿 추가/편집** 대화 상자:
   
   1. Hello에서 **템플릿** 드롭 다운 목록 **새로 만들기** tooadd 새 대역폭 템플릿 합니다.
   2. 대역폭 템플릿에 대한 고유 이름을 지정합니다.
3. **대역폭 일정**을 정의합니다. toocreate 일정:
   
   1. Hello 드롭 다운 목록에서에 대해 구성 된 hello 주 hello 일정의 hello 일을 선택 합니다. Hello hello 목록에서 개별 요일 앞에 있는 hello 확인란을 선택 하 여 여러 날짜를 선택할 수 있습니다.
   2. 선택 hello **하루 종일** 옵션을 하루 종일 hello에 대 한 hello 일정이 적용 됩니다. 이 옵션을 선택하면 **시작 시간** 또는 **종료 시간**을 더 이상 지정할 수 없습니다. 오전 12시 too11에서 hello 일정이 실행: 59 PM입니다.
   3. Hello 드롭 다운 목록에서 선택 된 **시작 시간**합니다. 이 hello 일정 시작 됩니다.
   4. Hello 드롭 다운 목록에서 선택 된 **종료 시간**합니다. 이 hello 일정을 중지 합니다.
      
      > [!NOTE]
      > 겹치는 일정은 허용되지 않습니다. Hello 시작 및 종료 시간 발생 일정이 겹치면 오류 메시지 toothat 효과 표시 됩니다.
      > 
      > 
   5. Hello 지정 **대역폭 속도**합니다. 이 hello 메가 비트 초당 대역폭 (Mbps) (업로드 및 다운로드) hello 클라우드 관련 작업에서 StorSimple 장치에서 사용 합니다. 이 필드에 대해 1에서 1,000 사이의 숫자를 제공합니다.
   6. Hello 확인 아이콘을 클릭 ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)합니다. 사용자가 만든 hello 서식 파일에 추가 됩니다 toohello 대역폭 템플릿 목록이 hello 서비스 **구성** 페이지.
      
      ![새 대역폭 템플릿 만들기](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. 클릭 **저장** hello 클릭 하 고 hello 페이지 맨 아래에 **예** 확인 메시지가 나타나면 합니다. 그러면 hello 구성 변경 내용이 저장 됩니다.

## <a name="edit-a-bandwidth-template"></a>대역폭 템플릿 편집
Hello 단계 tooedit 대역폭 템플릿을 다음을 수행 합니다.

### <a name="tooedit-a-bandwidth-template"></a>대역폭 템플릿 tooedit
1. **대역폭 템플릿 추가/편집**을 클릭합니다.
2. Hello에 **대역폭 템플릿 추가/편집** 대화 상자:
   
   1. Hello에서 **템플릿** 드롭 다운 목록에서 기존 대역폭 toomodify 원하는 서식 파일입니다.
   2. 변경을 완료합니다. (수정 가능 hello 기존 설정을.)
   3. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)에서도 확인할 수 있습니다. Hello 서비스 구성 페이지에서 hello 수정 된 템플릿을 hello 대역폭 템플릿 목록에 표시 됩니다.
3. 변경 내용을 클릭 toosave **저장** hello hello 페이지 맨 아래에 있습니다. 페이지의 아래쪽에서 **예** 를 클릭합니다.

> [!NOTE]
> Hello 대역폭 서식 파일에 예약 된 기존 hello 편집한 일정이 겹치면 변경 내용을 수정 하는 toosave를 사용할 수 없으므로 합니다.
> 
> 

## <a name="delete-a-bandwidth-template"></a>대역폭 템플릿 삭제
Hello 단계 toodelete 대역폭 템플릿을 다음을 수행 합니다.

#### <a name="toodelete-a-bandwidth-template"></a>대역폭 템플릿 toodelete
1. 서비스에 대 한 hello 대역폭 템플릿의 테이블 형식 목록 hello에서에서 원하는 toodelete hello 서식 파일을 선택 합니다. 삭제 아이콘 (**x**) toohello hello 선택한 템플릿의 오른쪽 끝에 표시 됩니다. Hello 클릭 **x** 아이콘 toodelete hello 템플릿.
2. 확인하라는 메시지가 표시됩니다. 클릭 **확인** tooproceed 합니다.

Hello 서식 파일은 볼륨에서 사용 중인 경우 있습니다 허용 되지 것입니다 toodelete 것입니다. 사용 중인 해당 hello 템플릿은 나타내는 오류 메시지가 표시 됩니다. 모든 hello 참조 toohello 서식 파일을 제거 해야 하 라는 오류 메시지 대화 상자가 표시 됩니다.

Hello에 액세스 하 여 모든 hello 참조 toohello 파일을 삭제할 수 **볼륨 컨테이너** 페이지 및 다른 서식 파일을 사용 하거나 사용자 지정 또는 무제한 대역폭을 사용 하 여이 템플릿을 사용 하는 hello 볼륨 컨테이너 수정 설정입니다. 모든 hello 참조를 제거한 경우에 hello 서식 파일을 삭제할 수 있습니다.

## <a name="use-a-default-bandwidth-template"></a>기본 대역폭 템플릿 사용
기본 대역폭 템플릿이 제공 하 고 hello 클라우드를 액세스할 때 기본 tooenforce 대역폭 제어 하 여 볼륨 컨테이너에 의해 사용 됩니다. hello 기본 템플릿은 템플릿을 직접 만드는 사용자에 대 한 준비를 참조로도 사용 됩니다. 이 기본 템플릿의 hello 세부 정보는.

* **이름** – 무제한 저녁 시간 및 주말
* **일정** – 월요일 tooFriday 오전 8 시 ~ 오후 5 시 장치 시간 1mbps의 대역폭 속도 적용 하는 단일 일정입니다. hello 대역폭 tooUnlimited hello 주 hello 나머지에 대해 설정 됩니다.

hello 기본 서식 파일을 편집할 수 있습니다. (편집 된 버전 포함)이 서식이 파일의 hello 사용량 추적 됩니다.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기
이 절차 toocreate 지정된 된 시간에 시작 되어 하루 종일 실행 되는 일정에 따라 합니다. Hello 예에서 hello 일정 hello 아침 오전 9 시에 시작 하 고 오전 9 시 hello 다음 날 아침 될 때까지 실행 합니다. 시작 hello 중요 toonote 이며 지정된 된 일정에 대 한 종료 시간 둘 다에 포함 되어야 합니다 hello 동일 24 시간을 예약 하 고 일정 기간에 걸쳐 있을 수 있습니다. 여러 날짜를 포함 하는 대역폭 템플릿은를 tooset 해야 할 경우 (hello 예제 에서처럼) 일정을 여러 개 toouse 해야 합니다.

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate는 하루 종일 대역폭 템플릿
1. Hello 아침 오전 9 시에 시작 되어 자정까지 실행 되는 일정을 만듭니다.
2. 다른 일정을 추가합니다. Hello 아침에 오전 9 시까지 자정에서 두 번째 일정 toorun hello를 구성 합니다.
3. Hello 대역폭 템플릿을 저장 합니다.

hello 복합 일정이 선택한 시간에 시작 및 하루 종일 실행 됩니다.

## <a name="questions-and-answers-about-bandwidth-templates"></a>대역폭 템플릿에 대한 질문과 대답
**Q**. Toobandwidth 컨트롤 hello 일정 사이는 어떻게 될까요? (하나의 일정이 종료되고 다른 일정이 아직 시작되지 않았습니다.)

**A**. 이러한 경우 적용되는 대역폭 제어는 없습니다. 즉, 데이터 toohello 클라우드 계층을 지정할 때 해당 hello 장치 무제한 대역폭을 사용할 수 있습니다.

**Q**. 오프라인 장치에서 대역폭 템플릿을 수정할 수 있습니까?

**A**. Hello 해당 장치가 오프 라인 이면 볼륨 컨테이너에서 대역폭 템플릿 수 toomodify 되지 않습니다.

**Q**. Hello 연결 된 볼륨이 오프 라인일 때는 볼륨 컨테이너와 연결 된 대역폭 템플릿을 편집할 수 있습니까?

**A**. 볼륨이 오프라인 상태인 볼륨 컨테이너와 연결된 대역폭 템플릿을 수정할 수 있습니다. 참고 볼륨이 오프 라인일 때 데이터가 없는 hello 장치 toohello 클라우드에서 계층이지 것입니다.

**Q**. 기본 템플릿을 삭제할 수 있습니까?

**A**. 기본 서식 파일을 삭제할 수 있지만 않습니다 것이 좋습니다 toodo 하므로. 편집 된 버전을 포함 하 여 기본 서식 파일의 hello 사용량 추적 됩니다. hello 추적 데이터를 분석 하 고 hello 시간이 흐름에 사용 되는 tooimprove hello에 대 한 기본 서식 파일에서 합니다.

**Q**. 대역폭 템플릿을 수정 toobe 필요 하다는 어떻게 확인 합니까?

**A**. 속도가 저하 또는 하루에 여러 번 억제 hello 네트워크 표시 toomodify hello 대역폭 템플릿을 사용 해야 하는 기호는 시작할 때 hello 중 하나입니다. 이 경우 hello I/O 성능 및 네트워크 처리량 차트를 보면 hello 저장소 및 사용 현황 네트워크를 모니터링 합니다.

Hello 네트워크 처리량 데이터에서 hello 시간을 확인 하 고 볼륨 컨테이너 네트워크 병목 현상이 발생 하는 hello에 hello. 경우 이런 데이터를 계층화 된 toohello 클라우드 중인 경우 (이 정보를 가져올 모든 볼륨 컨테이너에 대 한 I/O 성능에서 toocloud 장치에 대 한), toomodify hello 대역폭 템플릿이 볼륨 컨테이너와 연결 해야 합니다.

Hello 수정 후 사용 중인 템플릿은가 toomonitor hello 네트워크 다시 상당한 대기 합니다. 계속 발생 하는 경우 해야 합니다 toorevisit 대역폭 템플릿을 합니다.

**Q**. 겹치는 일정이 다 수 볼륨 컨테이너가 장치에 있는 경우 어떤 일이 생기 하지만 서로 다른 제한이 적용 tooeach?

**A**. 3개의 볼륨 컨테이너가 있는 장치가 있다고 가정해 보겠습니다. hello 완전히 이러한 컨테이너와 연결 된 일정이 겹칩니다. 각이 컨테이너에 대 한 hello 대역폭 사용은 5, 10, 15mbps 각각입니다. 이러한 모든 컨테이너에서 hello 동시 hello 최소 3 hello 대역폭 제한 적용할 수에서 i/o가 발생 하는 경우:이 경우 이러한 나가는 I/O 요청이 공유 하므로 5mbps hello 동일한 큐입니다.

## <a name="best-practices-for-bandwidth-templates"></a>대역폭 템플릿에 대한 모범 사례
StorSimple 장치에 대해 이 모범 사례를 따릅니다.

* 사용자 장치 tooenable 처리량의 가변 제한을 hello 네트워크 hello 장치별 hello 일의 서로 다른 시간에 대역폭 템플릿을 구성 합니다. 백업 일정을 함께 사용하면 이 대역폭 템플릿은 사용량이 가장 적을 때 클라우드 작업에 대해 효과적으로 추가 네트워크 대역폭을 활용할 수 있습니다.
* Hello 배포 및 hello 필요한 복구 시간 목표 (RTO) hello 크기를 기준으로 특정 배포에 필요한 hello 실제 대역폭을 계산 합니다.

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.

