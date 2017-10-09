---
title: "aaaDeactivate 및 Microsoft Azure StorSimple 가상 배열 delete | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>StorSimple 가상 배열 비활성화 및 삭제

## <a name="overview"></a>개요

StorSimple 가상 배열을 비활성화 하면 hello 장치와 StorSimple 장치 관리자 서비스를 해당 하는 hello hello 연결도를 끊어집니다. 이 자습서에서는 다음을 수행하는 방법을 설명합니다.

* 장치 비활성화 
* 비활성화된 장치 삭제

이 문서의 정보 hello tooStorSimple 가상 배열만 적용 됩니다. 8000 시리즈에 대 한 내용은 toohow을 너무 이동[비활성화 또는 장치를 삭제](storsimple-deactivate-and-delete-device.md)합니다.

## <a name="when-toodeactivate"></a>때 toodeactivate?

비활성화는 영구 작업이며 실행 취소할 수 없습니다. StorSimple 장치 관리자 서비스 hello로 비활성화 된 장치 다시 등록할 수 없습니다. Toodeactivate 필요 하 고 hello 다음 시나리오에에서는 StorSimple 가상 배열 삭제할 수 있습니다.

* **계획 된 장애 조치** : 장치가 온라인 상태이 고 장치를 통해 toofail를 계획 합니다. Tooupgrade tooa 큰 장치를 계획 하는 경우 장치를 통해 toofail을 할 수 있습니다. Hello 데이터 소유권은 전송 hello 장애 조치가 완료 후 자동 hello 원본 장치가 삭제 됩니다.
* **계획 되지 않은 장애 조치** : 장치가 오프 라인 상태 이며 hello 장치를 통해 toofail 필요 합니다. 이 시나리오는 hello 데이터 센터에서 중단 되 고 다운 기본 장치는 재해 발생 시 발생할 수 있습니다. Hello 장치 tooa 보조 장치를 통해 toofail를 계획합니다. Hello 데이터 소유권은 전송 hello 장애 조치가 완료 후 자동 hello 원본 장치가 삭제 됩니다.
* **서비스 해제** : toodecommission hello 장치를 선택 합니다. 이 옵션을 toofirst hello 장치를 비활성화 한 다음 삭제 해야 합니다. 장치를 비활성화하면 로컬로 저장된 데이터에 더 이상 액세스할 수 없게 됩니다. 액세스 및 복구 hello 데이터만 hello 클라우드에 저장을 수 있습니다. 비활성화 후 tookeep hello 장치 데이터를 계획 하는 경우 장치를 비활성화 하기 전에 모든 데이터의 클라우드 스냅숏을 수행 해야 합니다. 이 클라우드 스냅숏을 사용 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.

## <a name="deactivate-a-device"></a>장치 비활성화

toodeactivate 장치 hello 다음 단계를 수행 합니다.

#### <a name="toodeactivate-hello-device"></a>toodeactivate hello 장치

1. 서비스에 이동 너무**관리 > 장치**합니다. Hello에 **장치** 블레이드, 클릭 및 선택 hello 장치 toodeactivate 한다고 합니다.
   
    ![장치 toodeactivate 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. 사용자 **장치 대시보드** 블레이드에서 클릭 **중... 더 많은** hello 목록에서 선택 **비활성화**합니다.
   
    ![비활성화 클릭](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. Hello에 **비활성화** 블레이드, 형식 hello 장치 이름 및 클릭 **비활성화**합니다. 
   
    ![비활성화 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.
   
    ![진행 중인 비활성화](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. 비활성화 한 후 장치의 hello 목록을 새로 고칩니다.
   
    ![비활성화 완료](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    이제 이 장치를 삭제할 수 있습니다.

## <a name="delete-hello-device"></a>Hello 장치 삭제

장치에 첫 번째 비활성화 toodelete toobe 것입니다. 장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다. 그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다. 그러나 hello 장치와 연결 된 hello 데이터 hello 클라우드 유지 됩니다. 그러면 이 데이터를 사용하는 데 요금이 발생합니다.

toodelete hello 장치 hello 다음 단계를 수행 합니다.

#### <a name="toodelete-hello-device"></a>toodelete hello 장치

1. StorSimple 장치 관리자 프로그램 너무 이동**관리 > 장치**합니다. Hello에 **장치** 블레이드에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.
2. Hello에 **장치 대시보드** 블레이드에서 클릭 **중... 더 많은** 클릭 하 고 **삭제**합니다.
   
   ![장치 toodelete 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. Hello에 **삭제** 블레이드, 형식 hello 이름을 클릭 하 여 장치 tooconfirm hello 삭제 **삭제**합니다. 삭제 hello 장치 hello 장치와 연결 된 hello 클라우드 데이터를 삭제 하지 않습니다. 
   
   ![삭제 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. hello 삭제 시작 되 고 몇 분 toocomplete를 걸립니다.
   
   ![진행 중인 삭제](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Hello 장치를 삭제 한 후 장치의 hello 업데이트 목록을 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

* 방법에 대 한 조치 toofail 너무 이동[StorSimple 가상 배열의 장애 조치 및 재해 복구](storsimple-virtual-array-failover-dr.md)합니다.

* toouse hello StorSimple 장치 관리자 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 hello StorSimple 장치 관리자 서비스 tooadminister StorSimple 가상 배열](storsimple-virtual-array-manager-service-administration.md)합니다. 

