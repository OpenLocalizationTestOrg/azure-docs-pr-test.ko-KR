---
title: "aaaDeactivate StorSimple 8000 시리즈 장치를 삭제 하 고 | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>StorSimple 장치 비활성화 및 삭제

## <a name="overview"></a>개요

이 문서에서는 설명 방법을 toodeactivate StorSimple 장치에 연결 된 tooa StorSimple 장치 관리자 서비스를 삭제 합니다. 이 문서에 대 한 hello 지침 hello StorSimple 클라우드 어플라이언스에 포함 하 여 tooStorSimple 8000 시리즈 장치 에서만 적용 됩니다. StorSimple 가상 배열을 사용 하는 경우 이동 하 여 너무[비활성화 및 삭제는 StorSimple 가상 배열](storsimple-virtual-array-deactivate-and-delete-device.md)합니다.

비활성화 서버 hello 장치와 StorSimple 장치 관리자 서비스를 해당 하는 hello hello 연결 합니다. (예를 들어 교체 하거나 장치를 업그레이드 하는 경우 또는 StorSimple 더 이상 사용 하는 경우) 서비스에서 StorSimple 장치 tootake을 지정할 수 없습니다. 이 경우 있어야만 toodeactivate hello 장치를 삭제할 수 있습니다.

장치를 비활성화 하면 hello 장치에서 로컬로 저장 된 모든 데이터에는 더 이상 액세스할 수입니다. Hello 클라우드에 저장 된 hello 장치와 연결 된 hello 데이터만 복구할 수 있습니다.

> [!WARNING]
> 비활성화는 영구 작업이며 실행 취소할 수 없습니다. 비활성화 된 장치 toofactory 기본값 다시 설정 하지 않은 hello StorSimple 장치 관리자 서비스에 등록할 수 없습니다.
>
> hello 공장 기본 장치에서 로컬로 저장 된 모든 hello 데이터 프로세스 삭제를 설정 합니다. 따라서 장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다. 이 클라우드 스냅숏을 사용 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.

이 자습서를 읽은 후에 다음을 수행할 수 있습니다.

* 장치 비활성화 하 고 hello 데이터를 삭제 합니다.
* 장치 비활성화를 hello 데이터를 보관 합니다.

> [!NOTE]
> StorSimple의 물리적 장치 또는 클라우드 어플라이언스를 비활성화하려면 먼저 해당 장치에 의존하는 클라이언트와 호스트를 중지하거나 삭제해야 합니다.


## <a name="deactivate-and-delete-data"></a>데이터 비활성화 및 삭제

Hello 장치를 완전히 삭제 하 고 hello 장치에 tooretain hello 데이터 하지 않을 경우 다음 단계를 수행 하는 hello를 완료 합니다.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello 장치 및 delete hello 데이터

1. 장치를 비활성화 하기 전에 모든 hello 볼륨 컨테이너 (및 hello 볼륨) hello 장치와 연결 된 삭제 해야 합니다. 연결 된 hello 백업을 삭제 한 후에 볼륨 컨테이너를 삭제할 수 있습니다.

    > [!NOTE]
    > StorSimple 물리적 장치 또는 클라우드 어플라이언스에 비활성화 하기 전에 삭제 hello 볼륨 컨테이너에서 hello 데이터 hello 장치에서 실제로 삭제 됨을 확인 합니다. Hello 클라우드 소비 차트를 모니터링할 수 있습니다 및 hello 클라우드 사용량 삭제 한 hello 백업으로 인해 삭제를 보면 toodeactivate hello 장치를 진행할 수 있습니다. 전에 hello 장치를 비활성화 하면이 놓기를 수행 hello 데이터 hello 저장소 계정에 잘못 할당 된 및 요금이 발생 합니다.

2. 다음과 같이 hello 장치를 비활성화 합니다.
   
   1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다. Hello에 **장치** 블레이드, toodeactivate 마우스 오른쪽 단추를 클릭 한 다음 원하는 선택 hello 장치 **비활성화**합니다.

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Hello에 **비활성화** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **비활성화**합니다. hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. 비활성화 한 후 hello 장치를 완전히 삭제할 수 있습니다. 장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다. 그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다. 다음 단계 toodelete hello 장치 hello를 사용 합니다.
   
   1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다. Hello에 **장치** 블레이드, toodelete 마우스 오른쪽 단추를 클릭 한 다음 원하는 비활성화 선택 hello 장치 **삭제**합니다.

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Hello에 **삭제** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **삭제**합니다. hello 삭제는 몇 분 toocomplete 합니다.

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Hello 삭제 성공적으로 완료 되 면 알림이 표시 됩니다. hello 장치 목록도 tooreflect hello 삭제를 업데이트합니다.

## <a name="deactivate-and-retain-data"></a>데이터 비활성화 및 보존

관심 있는 hello 장치를 삭제 해도 tooretain hello 데이터를 원하는 경우 다음 단계를 수행 하는 hello를 완료 합니다.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>장치 toodeactivate hello 데이터를 유지 합니다.
1. Hello 장치를 비활성화 합니다. 모든 볼륨 컨테이너를 hello 및 hello 장치의 hello 스냅숏은 그대로 유지 됩니다.
   
   1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다. Hello에 **장치** 블레이드, toodeactivate 마우스 오른쪽 단추를 클릭 한 다음 원하는 선택 hello 장치 **비활성화**합니다.

         ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Hello에 **비활성화** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **비활성화**합니다. hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.

         ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. 이제 hello 볼륨 컨테이너와 연결 된 hello 스냅숏을 조치할 수 있습니다. 너무 절차를 보려면[StorSimple 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.
3. 비활성화 및 장애 조치 후 hello 장치를 완전히 삭제할 수 있습니다. 장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다. 그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다. 다음 단계 완료 hello toodelete hello 장치:
   
   1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다. Hello에 **장치** 블레이드, toodelete 마우스 오른쪽 단추를 클릭 한 다음 원하는 비활성화 선택 hello 장치 **삭제**합니다.

       ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Hello에 **삭제** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **삭제**합니다. hello 삭제는 몇 분 toocomplete 합니다.

       ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Hello 삭제 성공적으로 완료 되 면 알림이 표시 됩니다. hello 장치 목록도 tooreflect hello 삭제를 업데이트합니다.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>클라우드 어플라이언스 비활성화 및 삭제

StorSimple 클라우드 장비에 대 한 hello 포털에서 비활성화 할당을 취소 하 고 hello 가상 컴퓨터 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제 합니다. 일 수 없습니다 hello 클라우드 어플라이언스에 비활성화 된 후 tooits 이전 상태로 복원 합니다.

![StorSimple Cloud Appliance 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

작업을 수행 하는 hello에 비활성화 결과:

* StorSimple 클라우드 어플라이언스에 hello hello 서비스에서 제거 됩니다.
* StorSimple 클라우드 어플라이언스에 hello에 대 한 hello 가상 컴퓨터가 삭제 됩니다.
* hello OS 디스크 및 StorSimple 클라우드 어플라이언스에 hello에 대 한 만든 데이터 디스크 제거 됩니다.
* hello 호스팅된 서비스 및 가상 네트워크를 프로 비전 중에 만들어진 유지 됩니다. 이러한 엔터티를 사용하지 않는 경우 수동으로 삭제해야 합니다.
* StorSimple 클라우드 어플라이언스에 hello에서 만든 클라우드 스냅숏은 유지 됩니다.

Hello 클라우드 어플라이언스에 비활성화 된 후에 hello 장치 목록에서 삭제할 수 있습니다. 장치, 마우스 클릭 한 다음 선택 hello 비활성화 **삭제**합니다. StorSimple는 hello 장치를 삭제 하 고 장치 업데이트 목록이 hello 되 면이 알려 줍니다.

## <a name="next-steps"></a>다음 단계

* toorestore 비활성화 된 장치 toofactory 기본값 hello, 너무 이동[hello 장치 toofactory 기본 설정으로 초기화](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.
* 기술 지원을 받으려면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.
* toouse hello StorSimple 장치 관리자 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

