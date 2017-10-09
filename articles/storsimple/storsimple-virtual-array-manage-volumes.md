---
title: "StorSimple 가상 배열에 있는 aaaManage 볼륨 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자를 설명 하 고 설명 어떻게 toouse 것 toomanage 볼륨을 StorSimple 가상 배열입니다."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Hello StorSimple 가상 배열에서 StorSimple 장치 관리자를 사용 하 여 서비스 toomanage 볼륨

## <a name="overview"></a>개요

이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 StorSimple 가상 배열에 있는 볼륨을 관리 하는 방법을 설명 합니다.

hello StorSimple 장치 관리자 서비스는 hello 단일 웹 인터페이스에서 StorSimple 솔루션을 관리할 수 있는 Azure 포털의에서 확장입니다. 또한 toomanaging 공유 및 볼륨에 있습니다 StorSimple 장치 관리자 서비스 tooview hello를 사용 하 여 및 장치를 관리, 경고, 보기 및 볼 수 있으며 백업 정책 및 hello 백업 카탈로그.

## <a name="volume-types"></a>볼륨 유형

StorSimple 볼륨은 다음과 같을 수 있습니다.

* **로컬로 고정**: 이러한 볼륨의 데이터가 항상 hello 배열에 유지 되 고 toohello 클라우드를 분산 하지 않습니다.
* **계층**: 이러한 볼륨의 데이터 toohello 클라우드 spill 수 있습니다. 계층화 된 볼륨을 만들 때 hello 공간의 약 10 %hello 로컬 계층에서 프로 비전 하 고 hello 공간을 90 %hello 클라우드 프로 비전 됩니다. 예를 들어 1 t B 볼륨을 프로 비전, 100GB hello 로컬 공간에 있게 및 900GB hello 클라우드에서 사용할 수 있도록 하는 경우 데이터 계층이 때 hello 합니다. 이 차례로 hello 장치에서 모든 hello 로컬 공간이 소진 되 면 제공 해야 할 수 없습니다 계층화 된 볼륨 (필요 하기 때문에 hello 10 %hello 로컬에서 계층을 사용할 수 없습니다)을 의미 합니다.

### <a name="provisioned-capacity"></a>프로비전된 용량
Toohello 다음 각 볼륨 형식에 대 한 프로 비전 된 최대 용량에 대 한 표를 참조 하십시오.

| **제한 식별자**                                       | **제한**     |
|------------------------------------------------------------|---------------|
| 계층화 볼륨의 최소 크기                            | 500GB        |
| 계층화 볼륨의 최대 크기                            | 5TB          |
| 로컬로 고정된 볼륨의 최소 크기                    | 50GB         |
| 로컬로 고정된 볼륨의 최대 크기                    | 500GB        |

## <a name="hello-volumes-blade"></a>hello 볼륨 블레이드
hello **볼륨** StorSimple 서비스 요약 블레이드에서 메뉴 지정된 StorSimple 배열에 저장소 볼륨 목록이 hello를 표시 하 고 toomanage 있습니다 이러한.

![볼륨 블레이드](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

볼륨은 다음과 같은 특성으로 구성됩니다.

* **볼륨 이름** –를 설명 하는 이름을 고유 해야 하며 hello 볼륨을 식별 하는 데 도움이 됩니다.
* **상태** – 온라인 또는 오프라인 상태가 될 수 있습니다. 볼륨이 오프 라인 상태 이면 허용 되는 액세스 toouse hello 볼륨 표시 tooinitiators (서버) 않습니다.
* **형식** – hello 볼륨 인지를 나타내는 **계층화 됨** (기본 hello) 또는 **로컬로 고정**합니다.
* **용량** – hello 비교 toohello hello 초기자 (서버)가 저장 될 수 있는 데이터의 총 금액으로 사용 되는 데이터 양을 지정 합니다.
* **백업** – 경우 hello StorSimple 가상 배열의 모든 볼륨은 자동으로 백업에 사용할 수 있습니다.
* **호스트 연결** – toothis 볼륨 액세스를 허용 되는 hello 초기자 (서버)를 지정 합니다.

![볼륨 세부 정보](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

이 자습서 tooperform hello 작업 다음에 hello 지침을 따르세요.

* 볼륨 추가
* 볼륨 수정
* 볼륨을 오프라인으로 전환
* 볼륨 삭제

## <a name="add-a-volume"></a>볼륨 추가

1. Hello StorSimple 서비스 요약 블레이드를에서 클릭 **+ 볼륨 추가** hello 명령 모음에서 합니다. Hello를 열어서이 **볼륨 추가** 블레이드입니다.
   
    ![볼륨 추가](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. Hello에 **볼륨 추가** 블레이드에서 다음 hello지 않습니다:
   
   * Hello에 **볼륨 이름을** 필드에서 볼륨에 대 한 고유한 이름을 입력 합니다. hello 이름에는 3 too127 문자를 포함 하는 문자열 이어야 합니다.
   * Hello에 **형식** 드롭다운 목록에서 지정 하는지 여부를 toocreate는 **계층화 됨** 또는 **로컬로 고정** 볼륨입니다. 로컬 보증, 낮은 대기 시간 및 높은 성능을 필요로 하는 워크로드의 경우 **로컬로 고정된 볼륨**을 선택합니다. 다른 모든 데이터에 대해서는 **계층화된** 볼륨을 선택합니다.
   * Hello에 **용량** 필드 hello hello 볼륨 크기를 지정 합니다. 계층화된 볼륨은 500GB에서 5TB 사이여야 하고 로컬로 고정된 볼륨은 50GB에서 500GB 사이여야 합니다.
   * * 클릭 **호스트 연결**, 액세스 제어 레코드 (ACR) 해당 toohello iSCSI 초기자는 tooconnect toothis 볼륨을 클릭 한 다음 선택 **선택**합니다.
3. tooadd 새 연결 된 호스트를 클릭 **새로 추가**, hello 호스트와 해당 iSCSI에 대 한 이름을 입력 하 고 클릭 한 다음 정규화 된 이름 (IQN) **추가**합니다.
   
    ![볼륨 추가](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. 볼륨 구성을 완료했다면 **만들기**를 클릭합니다. 지정 된 hello로 볼륨을 만들 수는 설정 하 고는 동일 hello을 성공적으로 만들기 hello에 알림이 표시 됩니다. 기본적으로 hello 볼륨에 대 한 백업 설정 됩니다.
5. 볼륨 hello tooconfirm를 만드는 방법, 이동 toohello **볼륨** 블레이드입니다. Hello 볼륨이 나열 되어 표시 됩니다.
   
    ![볼륨 만들기 성공](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>볼륨 수정

Hello 볼륨에 액세스 하는 toochange hello 호스트가 필요 하면 볼륨을 수정 합니다. hello 볼륨의 다른 특성 수정할 수 없습니다 만들어지면 hello 볼륨.

#### <a name="toomodify-a-volume"></a>toomodify 볼륨

1. Hello에서 **볼륨** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello는 hello toomodify 하면 원하는 볼륨 상주 하는 가상 배열입니다.
2. **선택** 볼륨 hello 및 클릭 **호스트 연결** tooview 현재 연결 된 호스트 hello 및 tooa 다른 서버를 수정 합니다.
   
    ![볼륨 편집](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Hello를 클릭 하 여 변경 내용을 저장 **저장** 명령 모음입니다. 지정된 설정이 적용되고 알림이 표시됩니다.

## <a name="take-a-volume-offline"></a>볼륨을 오프라인으로 전환

계획할 때 toomodify 하거나 삭제 tootake 볼륨을 오프 라인으로 작업을 할 수 있습니다 것입니다. 볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다. Tootake hello 볼륨을 오프 hello 장치 뿐 아니라 hello 호스트 해야 합니다.

#### <a name="tootake-a-volume-offline"></a>tootake 오프 라인 볼륨

1. Hello 볼륨이 오프 라인으로 전환 하기 전에 있지 않은지 확인 합니다.
2. 첫 번째 hello 호스트에서 hello 볼륨을 오프 라인입니다. 따라서 hello 볼륨에서 데이터가 손상 될 위험이 제거 됩니다. 특정 단계에 대 한 호스트 운영 체제에 대 한 toohello 지침을 참조 하십시오.
3. Hello 볼륨 hello 호스트에서 오프 라인 상태 이면 후 hello 다음 단계를 수행 하 여 hello 볼륨 hello 배열 오프 라인에서 수행 합니다.
   
   * Hello에서 **볼륨** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello는 hello 원하는 있습니다 tootake 오프 라인 볼륨 상주 하는 가상 배열입니다.
   * **선택** 볼륨 hello 및 클릭 **중...**  (또는이 행의 오른쪽 클릭) hello 상황에 맞는 메뉴에서 선택 하 고 **오프 라인 상태로 만드는**합니다.
     
        ![오프라인 볼륨](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Hello hello 정보를 검토 **오프 라인 상태로 만드는** 블레이드 hello 작업의 동의 확인 합니다. 클릭 **오프 라인 상태로 만드는** tootake hello 볼륨을 오프 합니다. 진행 중인 hello 작업의 알림이 표시 됩니다.
   * hello 볼륨을 오프 라인 성공적으로 tooconfirm 이동 toohello **볼륨** 블레이드입니다. 오프 라인으로 hello 볼륨의 hello 상태를 표시 되어야 합니다.
     
       ![오프라인 볼륨 확인](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>볼륨 삭제

> [!IMPORTANT]
> 오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.
> 
> 

다음 단계 toodelete 볼륨 hello를 완료 합니다.

#### <a name="toodelete-a-volume"></a>toodelete 볼륨

1. Hello에서 **볼륨** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello는 hello toodelete 하면 원하는 볼륨 상주 하는 가상 배열입니다.
2. **선택** 볼륨 hello 및 클릭 **중...**  (또는이 행의 오른쪽 클릭) hello 상황에 맞는 메뉴에서 선택 하 고 **삭제**합니다.
   
    ![볼륨 삭제](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Hello 상태를 확인 하려는 toodelete hello 볼륨의 합니다. Toodelete hello 볼륨을 오프 라인 없으면 라인 오프 라인 첫 번째, 다음 hello 단계 [볼륨을 오프 라인](#take-a-volume-offline)합니다.
4. Hello에 확인 메시지가 나타나면 **삭제** 블레이드에서 hello 확인을 적용 하 고 클릭 **삭제**합니다. hello 볼륨 이제 삭제 되 고 hello **볼륨** 블레이드 hello 가상 배열 내에서 볼륨의 hello 업데이트 목록이 표시 됩니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[StorSimple 볼륨을 복제](storsimple-virtual-array-clone.md)합니다.

