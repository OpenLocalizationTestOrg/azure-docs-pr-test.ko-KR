---
title: "aaaManage StorSimple 볼륨 (업데이트 3) | Microsoft Docs"
description: "고 tooadd, 수정, 모니터링 및 StorSimple 볼륨을 삭제 하는 방법에 대해 설명 tootake 필요한 경우 오프 라인입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Hello StorSimple 장치 관리자 서비스 toomanage 볼륨 (업데이트 3 이상)를 사용 하 여

## <a name="overview"></a>개요

이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 3 이상 업데이트를 실행 하는 hello StorSimple 8000 시리즈 장치에 볼륨을 관리 하는 방법을 설명 합니다.

hello StorSimple 장치 관리자 서비스는 hello 단일 웹 인터페이스에서 StorSimple 솔루션을 관리할 수 있는 Azure 포털의에서 확장입니다. 모든 장치에서 hello Azure 포털 toomanage 볼륨을 사용 합니다. StorSimple 서비스를 만들고 관리하고, 장치를 관리하고, 정책을 백업하고, 카탈로그를 백업하고, 경고를 볼 수도 있습니다.

## <a name="volume-types"></a>볼륨 유형

StorSimple 볼륨은 다음과 같을 수 있습니다.

* **로컬로 고정 볼륨**: 이러한 볼륨의 데이터에 항상 hello 로컬 StorSimple 장치에 남아 있습니다.
* **볼륨을 계층화 된**: 이러한 볼륨의 데이터 toohello 클라우드 spill 수 있습니다.

보관 볼륨은 계층화된 볼륨의 유형입니다. hello 더 큰 중복 제거 청크 크기 보관 볼륨에 사용 되는 hello 장치 tootransfer toohello 클라우드 데이터의 더 큰 세그먼트 수 있습니다.

필요한 경우 로컬 tootiered 또는 계층화 된 toolocal hello 볼륨 유형을 변경할 수 있습니다. 자세한 내용은 이동 너무[hello 볼륨 유형 변경](#change-the-volume-type)합니다.

### <a name="locally-pinned-volumes"></a>로컬로 고정된 볼륨

로컬로 고정 된 볼륨 데이터 toohello 클라우드 계층 하지 않는 완전 하 게 볼륨을 기본 데이터의 경우 클라우드 연결의 독립적인 보장 되므로 로컬 합니다. 로컬로 고정된 볼륨의 데이터는 중복 제거되고 압축되지 않지만 로컬로 고정된 볼륨의 스냅숏은 중복 제거됩니다. 

로컬로 고정된 볼륨은 완전히 프로비전되므로 만들 때 장치에 충분한 공간이 있어야 합니다. 로컬 고정된 볼륨이 tooa 8TB hello StorSimple 8100 장치 및 hello 8600 장치의 20TB의 최대 크기를 제공할 수 있습니다. StorSimple는 스냅숏, 메타 데이터 및 데이터 처리에 대 한 hello 장치에 hello 나머지 로컬 공간을 예약합니다. Hello 크기의는 로컬 고정된 볼륨 toohello 최대 사용 가능한 공간을 늘릴 수 있습니다 하지만 한 번 만든 볼륨의 hello 크기를 줄일 수는 없습니다.

로컬로 고정 된 볼륨을 만들 경우 계층화 된 볼륨 만들기에 대 한 사용 가능한 공간 hello 줄어듭니다. 역방향 hello도 마찬가지입니다: 고정 된 볼륨을 로컬 만들기에 사용할 수 있는 hello 공간 위에 명시 된 hello 최대 제한 보다 작아야 기존 계층화 된 볼륨이 있는 경우. 로컬 볼륨에 대 한 자세한 내용은 참조 toohello [로컬 고정된 볼륨에 자주 묻는 질문](storsimple-8000-local-volume-faq.md)합니다.

### <a name="tiered-volumes"></a>계층화된 볼륨

계층화 된 볼륨은 씬 프로 비전 된 볼륨에는 hello 자주 액세스 데이터가 로컬 hello 장치에 유지 되 고 자주 사용 되는 데이터를 적게는 자동으로 toohello 클라우드 계층입니다. 씬 프로비저닝는 사용 가능한 저장소 tooexceed 물리적 리소스를 표시 되는 가상화 기술입니다. 충분 한 저장소를 미리 예약 하는 대신 StorSimple 데 충분 한 공간이 toomeet 현재 요구 씬 프로 비전 tooallocate을 사용 합니다. 클라우드 저장소의 탄력적인 특징 hello StorSimple 거 나 낮출 수 클라우드 저장소 toomeet 변화 하는 요구 하기 때문에이 방법을 지원 합니다.

사용 중인 경우 선택 hello 않는 아카이브 데이터를 계층화 된 볼륨 hello **이 볼륨을 사용 하 여 자주 액세스 하지 않는 아카이브 데이터에 대 한** 볼륨에 대 한 확인란 toochange hello 중복 제거 청크 크기 too512 (kb)입니다. 이 옵션을 선택 하지 않으면 해당 계층화 된 볼륨 hello 64KB의 청크 크기를 사용 합니다. 더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.


### <a name="provisioned-capacity"></a>프로비전된 용량

Toohello 다음 각 볼륨 및 장치 유형에 대 한 프로 비전 된 최대 용량에 대 한 표를 참조 하십시오. (로컬로 고정된 볼륨은 가상 장치에서 사용할 수 없습니다.)

|  | 최대 계층화된 볼륨 크기 | 최대 로컬로 고정된 볼륨 크기 |
| --- | --- | --- |
| **물리적 장치** | | |
| 8100 |64TB |8TB |
| 8600 |64TB |20TB |
| **가상 장치** | | |
| 8010 |30TB |해당 없음 |
| 8020 |64TB |해당 없음 |

## <a name="hello-volumes-blade"></a>hello 볼륨 블레이드

hello **볼륨** 블레이드에서는 초기자 (서버)에 대 한 hello Microsoft Azure StorSimple 장치에서 프로 비전 되는 toomanage hello 저장소 볼륨 수 있습니다. Hello StorSimple 장치 tooyour 연결 된 서비스에 볼륨 목록이 hello를 표시합니다.

 ![볼륨 페이지](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

볼륨은 다음과 같은 특성으로 구성됩니다.

* **볼륨 이름** –를 설명 하는 이름을 고유 해야 하며 hello 볼륨을 식별 하는 데 도움이 됩니다. 이 이름은 특정 볼륨에 필터링하는 경우 모니터링 보고서에서도 사용됩니다. Hello 볼륨을 만든 후에 바꿀 수 없습니다.
* **상태** – 온라인 또는 오프라인 상태가 될 수 있습니다. 볼륨이 오프 라인 상태 이면 허용 되는 액세스 toouse hello 볼륨 표시 tooinitiators (서버) 않습니다.
* **용량** – hello 총 hello 초기자 (서버)가 저장 될 수 있는 데이터의 양을 지정 합니다. 로컬로 고정 된 볼륨이 완전히 프로 비전 및 hello StorSimple 장치에 상주 합니다. 계층화 된 볼륨은 씬 프로비저닝 및 hello 데이터는 중복 제거 합니다. 씬 프로 비전 된 볼륨으로 장치에 미리 할당 하지 않습니다 실제 저장소 용량 내부적으로 또는 tooconfigured 볼륨 용량에 따라 hello 클라우드입니다. hello 볼륨 용량 할당 되 고 필요에 따라 사용 됩니다.
* **형식** – hello 볼륨 인지를 나타내는 **계층화 됨** (기본 hello) 또는 **로컬로 고정**합니다.

이 자습서 tooperform hello 작업 다음에 hello 지침을 따르세요.

* 볼륨 추가 
* 볼륨 수정 
* Hello 볼륨 유형 변경
* 볼륨 삭제 
* 볼륨을 오프라인으로 전환 
* 볼륨 모니터링 

## <a name="add-a-volume"></a>볼륨 추가

StorSimple 8000 시리즈 장치를 배포하는 동안 [볼륨을 만들었습니다](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume). 볼륨 추가는 과정이 비슷합니다.

#### <a name="tooadd-a-volume"></a>tooadd 볼륨

1. Hello에서 hello 장치 hello 테이블 형식 목록에서 **장치** 블레이드에서 장치를 선택 합니다. **+ 볼륨 추가**를 클릭합니다.

    ![새 볼륨 추가](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. Hello에 **볼륨 추가** 블레이드:
   
    1. hello **선택 장치** 필드는 현재 장치의 자동으로 채워집니다.

    2. Hello 드롭 다운 목록에서 볼륨 tooadd 해야 하는 hello 볼륨 컨테이너를 선택 합니다.

    3.  볼륨의 **이름** 을 입력합니다. Hello 볼륨을 만든 후 hello 볼륨을 바꿀 수 없습니다.

    4. Hello 드롭 다운 목록에서 선택 hello **형식** 볼륨에 대 한 합니다. 로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 볼륨을 선택합니다. 다른 모든 데이터에 대해서는 **계층화됨** 볼륨을 선택합니다. 아카이브 데이터에 이 볼륨을 사용하려면 **자주 액세스하지 않는 아카이브 데이터에 대해 이 볼륨 사용**을 선택합니다.
      
       계층화된 볼륨은 씬 프로비전되며 빠르게 만들 수 있습니다. 선택 하면 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 볼륨에 대 한 아카이브 데이터 변경 내용 hello 중복 제거 청크 크기에 대 한 대상으로 하는 계층화 된 볼륨에 대 한 too512 (kb)입니다. 이 필드를 선택 하지 않으면 해당 계층화 된 볼륨 hello 청크 크기는 64KB를 사용 합니다. 더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.
       
       로컬 고정된 볼륨 씩 프로 비전 하 고 hello hello 볼륨에 기본 데이터를 로컬 toohello 장치 상태를 유지 하 고 toohello 클라우드를 분산 하지 않습니다.  Hello 장치가 hello 로컬 계층에서 사용 가능한 공간을 확인 하는 로컬 고정된 볼륨을 만드는 경우의 hello tooprovision hello 볼륨 크기를 요청 했습니다. 로컬 고정된 볼륨 만들기의 hello 작동 hello 장치 toohello 클라우드에서 기존 데이터를 모두 포함 될 수 있습니다 및 toocreate hello 볼륨 hello 시간이 길어질 수 있습니다. hello 총 시간 hello 프로 비전 된 볼륨, 사용 가능한 네트워크 대역폭 및 장치의 hello 데이터의 hello 크기에 따라 달라 집니다.

    5. Hello 지정 **프로 비전 된 용량** 볼륨에 대 한 합니다. 선택 하는 hello 볼륨 종류에 따라 사용할 수 있는 hello 용량의 메모를 확인 합니다. hello 지정 hello 사용 가능한 공간 볼륨 크기를 초과할 수 없습니다.
      
       Too8.5 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 큰 8600 장치의 too22.5 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 장치의 로컬 공간이 필요한 toohost hello 작업 계층화 된 볼륨의 집합 이므로 로컬 고정된 볼륨 만들기 hello 공간을 계층화 된 볼륨을 프로 비전에 사용할 수 있는 영향을 줍니다. 따라서 로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다. 마찬가지로, 계층화 된 볼륨을 만들면 로컬 고정된 볼륨 만들기에 대 한 hello 사용 가능한 공간이 줄어듭니다.
      
       8100 장치에서 로컬로 고정 된 양의 8.5 TB (최대 허용 크기)를 프로 비전 hello 장치에서 사용 가능한 모든 hello 로컬 공간이 소진 되었을 있습니다. Hello의 hello 장치 toohost hello 작업 집합에 로컬 공간이 없을 때부터 해당 지점에서 모든 계층화 된 볼륨을 만들 수 없습니다 볼륨 계층입니다. 기존의 계층화 된 볼륨에 사용할 수 있는 hello 공간을 영향이 있습니다. 예를 들어 대략 106TB의 계층화된 볼륨이 있는 8100 장치에서는 로컬 고정 볼륨에 대해 4TB의 공간만 사용할 수 있습니다.

    6. Hello에 **호스트 연결** 필드 hello 화살표를 클릭 합니다. 

        ![연결된 호스트](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. Hello에 **호스트 연결** 블레이드에서 기존 ACR을 선택 하거나 새 ACR을 추가 합니다. 새 ACR을 선택 하는 경우 제공 합니다는 **이름** ACR를 hello 제공 **iSCSI Qualified Name** (IQN) Windows 호스트의 합니다. IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다. **만들기**를 클릭합니다. 볼륨을 지정 하는 hello로 만들면 설정 합니다.

        ![만들기 클릭](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

새 볼륨 toouse 준비 되었습니다.

> [!NOTE]
> 그런 다음 hello 볼륨 만들기 작업 실행 순서 대로 즉시 로컬 고정된 볼륨 만들기 한 다음 다른 로컬로 만드는 경우 고정 볼륨. hello 다음 볼륨 만들기 작업을 시작 하기 전에 hello 첫 번째 볼륨 만들기 작업이 완료 되어야 합니다.

## <a name="modify-a-volume"></a>볼륨 수정

Tooexpand 또는 hello 볼륨에 액세스 하는 호스트 hello 변경 해야 하는 경우 볼륨을 수정 합니다.

> [!IMPORTANT]
> * Hello 장치에서 hello 볼륨 크기를 수정 하면 hello 볼륨 크기 toobe hello 호스트 에서도 변경 해야 합니다.
> * 여기에 설명 된 hello 호스트 측 단계는 Windows Server 2012 (2012R2) 합니다. Linux 또는 다른 호스트 운영 체제에 대한 절차는 이와 다릅니다. 다른 운영 체제를 실행 하는 호스트의 hello 볼륨을 수정할 때 tooyour 호스트 운영 체제 지침을 참조 하십시오.

#### <a name="toomodify-a-volume"></a>toomodify 볼륨

1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다. 테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다. **설정 > 볼륨**을 클릭합니다.

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. 선택 **오프 라인 상태로 만드는** tootake hello 볼륨을 오프 라인을 수정 합니다.

    ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Hello에 **오프 라인 상태로 만드는** 블레이드에서 hello 볼륨을 오프 라인의 hello 영향을 검토 하 고 hello 해당 확인란을 선택 합니다. 먼저 hello hello 호스트에서 해당 볼륨은 오프 라인 상태를 확인 합니다. 볼륨을 오프 라인 tootake 호스트 서버에 연결 하는 방법을 tooStorSimple 대 한 자세한 내용은 toooperating 시스템에 대 한 구체적인 지침을 참조 하십시오. **오프라인으로 전환**을 클릭합니다.

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Hello 볼륨이 오프 라인 (같이 hello 볼륨 상태별) 일 후 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. **볼륨 수정**을 선택합니다.

    ![볼륨 수정 선택](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. Hello에 **볼륨 수정** 블레이드에서 hello 변경 내용에 따라 만들 수 있습니다.
   
   1. 볼륨 hello **이름** 편집할 수 없습니다.
   2. Hello 변환 **형식** 로컬로 고정 된 tootiered 또는 고정 된 계층화 된 toolocally (참조 [hello 볼륨 유형 변경](#change-the-volume-type) 에 대 한 자세한 내용은).
   3. Hello 증가 **프로 비전 된 용량**합니다. hello **프로 비전 된 용량** 늘릴 수만 있습니다. 만든 후에는 볼륨을 축소할 수 없습니다.
   4. 아래 **호스트 연결**, hello ACR을 수정할 수 있습니다. ACR toomodify hello 볼륨은 오프 라인 이어야 합니다.

       ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. 클릭 **저장** toosave 변경 내용을 합니다. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. hello Azure 포털에서 업데이트 볼륨 메시지를 표시 합니다. Hello 볼륨 성공적으로 업데이트 되었을 때 성공 메시지가 표시 됩니다.

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. 볼륨을 확장 하는 경우 hello Windows 호스트 컴퓨터에서 다음 단계를 완료 합니다.
   
   1. 너무 이동**컴퓨터 관리** ->**디스크 관리**합니다.
   2. **디스크 관리**를 마우스 오른쪽 단추로 클릭하고 **디스크 다시 검사**를 선택합니다.
   3. 디스크의 hello 목록에서 업데이트 된 hello 볼륨, 마우스 오른쪽 단추를 선택한 후 선택 **볼륨 확장**합니다. hello 볼륨 확장 마법사를 시작합니다. **다음**을 누릅니다.
   4. Hello 기본값을 적용 하는 hello 마법사를 완료 합니다. Hello 마법사가 완료 되 면 hello 볼륨 hello 증가 크기를 나타내야 합니다.
      
      > [!NOTE]
      > 로컬로 고정 된 볼륨을 확장 한 다음를 확장 하는 경우 다른 로컬로 고정 된 볼륨 hello 볼륨 확장 작업이 순차적으로 실행 하는 그 후에 즉시입니다. hello 다음 볼륨 확장 작업이 시작 하기 전에 hello 첫 번째 볼륨 확장 작업이 완료 되어야 합니다.
      

## <a name="change-hello-volume-type"></a>Hello 볼륨 유형 변경

로컬로 고정 된 tootiered 또는 고정 된 계층화 된 toolocally에서 hello 볼륨 유형을 변경할 수 있습니다. 그러나 이 변환은 자주 발생해서는 안됩니다.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Toolocal 계층화 된 볼륨에 대 한 변환 고려 사항

고정 된 계층화 된 toolocally에서 볼륨을 변환 하기 위한 몇 가지 원인은 다음과 같습니다.

* 데이터 가용성 및 성능에 대한 로컬 보장
* 클라우드 대기 시간 및 클라우드 연결 문제를 제거합니다.

작은 이들은 일반적으로 기존 볼륨 tooaccess 자주 되도록 합니다. 로컬로 고정된 볼륨은 생성될 때 완벽하게 프로비전됩니다. 

계층화 된 볼륨 tooa 로컬로 고정 된 볼륨을 변환 하는 경우 StorSimple hello 변환을 시작 하기 전에 장치에 공간이 충분 한지 확인 합니다. 공간이 부족 한 경우 오류가 표시 됩니다 및 hello 작업이 취소 됩니다. 

> [!NOTE]
> 계층화 된 toolocally 고정으로 변환을 시작 하기 전에 고려해 야 hello 다른 워크 로드의 공간 요구 사항을 확인 합니다. 

로컬로 고정 된 계층화 된 tooa 볼륨으로 변환 하면 장치 성능이 저하 될 수 있습니다. 또한 요인에 따라 hello toocomplete hello 변환 hello 시간을 늘어날 수 있습니다.

* 대역폭이 충분하지 않습니다.
* 현재 백업이 없습니다.

이러한 요인이 있을 수 있는 toominimize hello 효과:

* 대역폭 제한 정책을 검토하고 전용 40Mbps 대역폭을 사용할 수 있는지 확인합니다.
* 사용량이 적은 시간에 대 한 hello 변환을 예약 합니다.
* Hello 변환을 시작 하기 전에 클라우드 스냅숏을 만드십시오.

(다른 작업을 지 원하는) 여러 볼륨을 변환 하는 경우 다음 하면 우선 순위를 매기 hello 볼륨으로의 변환 더 높은 우선 순위 볼륨 먼저 변환 되도록 합니다. 예를 들어 파일 공유 워크로드가 있는 볼륨을 변환하기 전에 VM(가상 컴퓨터)을 호스트하는 볼륨 또는 SQL 워크로드가 있는 볼륨을 변환해야 합니다.

### <a name="local-tootiered-volume-conversion-considerations"></a>로컬 tootiered 볼륨 변환 고려 사항

로컬 고정된 볼륨 tooa toochange 계층화 된 볼륨 추가 공간 tooprovision 해야 할 경우 다른 볼륨을 할 수 있습니다. 로컬로 고정 hello 볼륨 tootiered를 변환할 때는 hello hello 장치에서 사용 가능한 용량 출시 hello 용량의 hello 크기에 따라 증가 합니다. 연결에 문제가 있어 hello 변환할 볼륨의 hello 지역 형식 toohello에서 계층 유형, hello 로컬 볼륨 발생할 것 계층화 된 볼륨의 속성 hello 변환이 완료 될 때까지 합니다. 즉, 일부 데이터가 유출 toohello 클라우드를 있을 수 있습니다. 이 이러한 데이터 toooccupy hello 작업을 다시 시작 하 고 완료 될 때까지 해제 될 수 없습니다 hello 장치의 로컬 공간을 계속 합니다.

> [!NOTE]
> 볼륨 변환은 다소 시간이 걸릴 수 있으며 시작된 후에 변환을 취소할 수 없습니다. hello 볼륨을 hello 변환 하는 동안 온라인 상태로 유지 하 고 백업을 가져올 수 있지만 확장 하거나 hello 변환이 수행 되는 동안 hello 볼륨을 복원할 수 없습니다.


#### <a name="toochange-hello-volume-type"></a>toochange hello 볼륨 유형

1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다. 테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다. **설정 > 볼륨**을 클릭합니다.

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. **수정**을 선택합니다.

    ![상황에 맞는 메뉴에서 수정 선택](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Hello에 **볼륨 수정** 블레이드에서 hello에서 hello 새 유형을 선택 하 여 hello 볼륨 형식을 변경 **형식** 드롭 다운 목록입니다.
   
   * 형식을 변경 하는 hello 너무 경우**로컬로 고정**, 충분 한 용량이 있는 경우 StorSimple toosee를 확인 합니다.
   * 형식을 변경 하는 hello 너무 경우**계층화 됨** 고이 볼륨을 사용 하 여 보관 데이터 선택 hello 됩니다 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.
   * 계층화 된 대로 로컬 고정된 볼륨을 구성 하는 경우 또는 _반대로_, hello 다음과 같은 메시지가 나타납니다.
   
    ![볼륨 유형 변경 메시지](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. 클릭 **저장** toosave hello 변경 합니다. 확인 메시지가 나타나면 클릭 **예** toostart hello 변환 프로세스입니다. 

    ![저장 및 확인](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Azure 포털 hello hello 볼륨을 업데이트 하는 hello 작업 만들기에 대 한 알림을 표시 합니다. Hello 볼륨 변환 작업이의 hello 알림 toomonitor hello 상태를 클릭 합니다.

    ![볼륨 전환을 위한 작업](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>볼륨을 오프라인으로 전환

Toomodify 제작 하거나 hello 볼륨을 삭제 하는 경우 볼륨을 오프 tootake를 할 수 있습니다. 볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다. Hello 호스트와 hello 장치에서 hello 볼륨을 오프 수행 해야 합니다.

#### <a name="tootake-a-volume-offline"></a>tootake 오프 라인 볼륨

1. Hello 볼륨이 오프 라인으로 전환 하기 전에 있지 않은지 확인 합니다.
2. 첫 번째 hello 호스트에서 hello 볼륨을 오프 라인입니다. 따라서 hello 볼륨에서 데이터가 손상 될 위험이 제거 됩니다. 특정 단계에 대 한 호스트 운영 체제에 대 한 toohello 지침을 참조 하십시오.
3. Hello 호스트 오프 라인 상태 이면 후 hello 다음 단계를 수행 하 여 hello 볼륨 hello 장치에 오프 라인에서 수행 합니다.
   
    1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다. 테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다. **설정 > 볼륨**을 클릭합니다.

        ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. 선택 **오프 라인 상태로 만드는** tootake hello 볼륨을 오프 라인을 수정 합니다.

        ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Hello에 **오프 라인 상태로 만드는** 블레이드에서 hello 볼륨을 오프 라인의 hello 영향을 검토 하 고 hello 해당 확인란을 선택 합니다. **오프라인으로 전환**을 클릭합니다. 

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Hello 볼륨이 오프 라인 상태일 때 알림이 표시 됩니다. 또한 hello 볼륨 상태 tooOffline를 업데이트합니다.
      
4. 볼륨은 오프 라인 hello 볼륨 및 마우스 오른쪽 단추를 선택 하는 경우 후 **온라인 상태로 만들기** 옵션을 hello 상황에 맞는 메뉴에서 사용할 수 있습니다.

> [!NOTE]
> hello **오프 라인으로 전환** 명령은 요청 toohello 장치 tootake hello 볼륨을 오프 라인으로 보냅니다. 호스트는 hello 볼륨을 사용 하는 경우이 인해 연결이 끊어지지만된 하지만 hello 볼륨을 오프 라인 실패 하지 않습니다.

## <a name="delete-a-volume"></a>볼륨 삭제

> [!IMPORTANT]
> 오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.

다음 단계 toodelete 볼륨 hello를 완료 합니다.

#### <a name="toodelete-a-volume"></a>toodelete 볼륨

1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다. 테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다. **설정 > 볼륨**을 클릭합니다.

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Hello 상태를 확인 하려는 toodelete hello 볼륨의 합니다. Toodelete hello 볼륨을 오프 라인 없으면 오프 라인 상태로 먼저 합니다. Hello 단계에 따라 [볼륨을 오프 라인](#take-a-volume-offline)합니다.
4. Hello 볼륨이 오프 라인 상태 이면 후 hello 볼륨을 선택 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다.

    ![상황에 맞는 메뉴에서 삭제 선택](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. Hello에 **삭제** 블레이드, 검토 및 선택 hello 볼륨을 삭제의 hello 영향에 대 한 확인란을 선택 합니다. 볼륨을 삭제 하면 hello 볼륨에 있는 모든 hello 데이터가 손실 됩니다. 

    ![변경 내용 저장 및 확인](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Hello 볼륨을 삭제 한 후 볼륨의 테이블 형식 목록을 hello tooindicate hello 삭제를 업데이트 합니다.

    ![업데이트된 볼륨 목록](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > 로컬로 고정 된 볼륨을 삭제 하면 hello 공간 새 볼륨에 사용할 수 있는 즉시 업데이트 되지 않을 수 있습니다. StorSimple 장치 관리자 서비스 hello 사용 가능한 로컬 공간 hello를 주기적으로 업데이트합니다. Toocreate hello 새 볼륨을 시도 하기 전에 몇 분 정도 대기 하는 것이 좋습니다.
   >
   > 또한 로컬로 고정 된 볼륨을 삭제 한 다음 다른 로컬로 삭제 하는 경우 고정 된 볼륨 hello 볼륨 삭제 작업 순차적으로 실행 하는 그 후에 즉시입니다. 볼륨 삭제 작업을 첫 번째 hello hello 다음 볼륨 삭제 작업을 시작 하기 전에 완료 해야 합니다.

## <a name="monitor-a-volume"></a>볼륨 모니터링

볼륨 모니터링 toocollect 볼륨에 대 한 통계를 O 관련 있습니다. 기본적으로 hello에 대해 모니터링이 활성화를 만들면 처음 32 개 볼륨입니다. 추가 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다. 

> [!NOTE]
> 복제된 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.


다음 단계 tooenable hello 하거나 볼륨에 대 한 모니터링을 사용 하지 않도록 설정 합니다.

#### <a name="tooenable-or-disable-volume-monitoring"></a>볼륨 모니터링을 비활성화 또는 tooenable

1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다. 테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다. **설정 > 볼륨**을 클릭합니다.
2. Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. **수정**을 선택합니다.
3. Hello에 **볼륨 수정** 블레이드에서 대 한 **모니터링** 선택 **사용** 또는 **사용 하지 않도록 설정** tooenable 하거나 모니터링을 사용 하지 않도록 합니다.

    ![모니터링 사용 안 함](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. **저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다. Azure 포털 hello hello 볼륨 및 성공 메시지 hello 볼륨 업데이트 된 후 업데이트에 대 한 알림을 표시 합니다.

## <a name="next-steps"></a>다음 단계

* 너무 방법에 대해 알아봅니다[StorSimple 볼륨을 복제](storsimple-8000-clone-volume-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

