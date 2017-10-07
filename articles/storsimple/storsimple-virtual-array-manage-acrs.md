---
title: "StorSimple 가상 배열에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toomanage 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 가상 배열에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>StorSimple 가상 배열에 대 한 StorSimple 장치 관리자를 사용 하 여 toomanage 액세스 제어 레코드

## <a name="overview"></a>개요

액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 가상 배열 (라고도 hello StorSimple 온-프레미스 가상 장치)에 연결할 수 있는 호스트를 허용 합니다. Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함). 호스트 오류 tooconnect tooa 볼륨 값을 hello 장치 hello 해당 볼륨 hello IQN 이름에 대 한 연결 된 ACR 확인 하 고 일치 하는 경우 hello 연결이 설정 됩니다. hello **액세스 제어 레코드** hello 내 블레이드 **구성** 장치 관리자 서비스의 섹션 hello 해당 hello 호스트의 iqn이 포함 된 모든 hello 액세스 제어 레코드를 표시 합니다.

![액세스 제어 레코드 관리](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.

* Hello IQN 가져오기
* 액세스 제어 레코드 추가
* 액세스 제어 레코드 편집
* 액세스 제어 레코드 삭제

> [!IMPORTANT]
> 
> * ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.
> * 볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.


## <a name="get-hello-iqn"></a>Hello IQN 가져오기

Hello 단계 tooget hello Windows Server 2012를 실행 중인 Windows 호스트의 IQN을 다음을 수행 합니다.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>ACR 추가

사용 하면 **액세스 제어 레코드** hello 내 블레이드 **구성** StorSimple 장치 관리자 서비스 tooadd Acr의 섹션입니다. 일반적으로 볼륨 하나와 ACR 하나를 연결합니다.

볼륨에 ACR을 연결 하는 방법에 대 한 내용은 이동 너무[볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)합니다.

> [!IMPORTANT]
> ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.


Hello 단계 tooadd ACR 다음을 수행 합니다.

#### <a name="tooadd-an-acr"></a>ACR tooadd

1. Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.
2. Hello에 **액세스 제어 레코드** 블레이드에서 클릭 **추가**합니다.
3. Hello에 **ACR 추가** 블레이드에서 다음 hello지 않습니다.
   
    1. ACR의 **이름** 을 지정합니다.
    
    2. 아래 **iSCSI 초기자 이름**, Windows 호스트의 IQN 이름을 hello를 제공 합니다. Windows Server 호스트의 IQN tooget hello 다음 hello지 않습니다.
   
    3. Windows 호스트에 hello Microsoft iSCSI 초기자를 시작 합니다. Hello iSCSI 초기자 속성 창의 hello에서 **구성** 탭 선택 하 고 hello에서 hello 문자열을 복사 **초기자 이름** 필드입니다.
    Hello에이 문자열을 붙여 넣습니다. **IQN** 필드 hello에 **ACR 추가** 블레이드입니다.
   
    6. 클릭 **추가** tooadd hello ACR 합니다.  
   
        ![액세스 제어 레코드 추가](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. 테이블 형식 목록 hello 업데이트 tooreflect이이 추가 됩니다.

## <a name="edit-an-acr"></a>ACR 편집

Hello를 사용 하 여 **액세스 제어 레코드** hello 내 블레이드 **구성** hello Azure 포털 tooedit Acr에서에서 장치 관리자 서비스의 섹션입니다.

> [!NOTE]
> 현재 사용 중인 ACR을 수정하지 않아야 합니다. 현재 사용 중인 볼륨와 연결 된 ACR tooedit, 먼저 수행 해야 hello 볼륨 오프 라인입니다.


Hello 단계 tooedit ACR 다음을 수행 합니다.

#### <a name="tooedit-an-acr"></a>ACR tooedit

1. Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션 **액세스 제어 레코드**합니다.
2. Hello에 **액세스 제어 레코드** hello hello 액세스 제어 레코드의 테이블 형식 목록에서 블레이드 hello toomodify 한다고 ACR를 두 번 클릭 합니다.
3. Hello에 **액세스 제어 레코드 편집** 블레이드에서 다음 hello지 않습니다.
   
    1. ACR hello에 대 한 hello IQN을 제공 합니다.
   
    2. 클릭 **저장** hello hello 블레이드 toosave hello 위쪽에 ACR을 수정 합니다. Hello 다음 확인 메시지가 표시 됩니다.
   
        ![액세스 제어 레코드 편집](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>액세스 제어 레코드 삭제

Hello를 사용 하 여 **구성** hello Azure 포털 toodelete Acr의에서 페이지입니다.

> [!NOTE]
> 
> * 현재 사용 중인 ACR을 삭제하지 않아야 합니다. 현재 사용 중인 볼륨와 연결 된 ACR toodelete, 먼저 수행 해야 hello 볼륨 오프 라인입니다.
> * 볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.


Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.

#### <a name="toodelete-an-access-control-record"></a>toodelete 액세스 제어 레코드

1. Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션 **액세스 제어 레코드**합니다.

2. Hello에 **액세스 제어 레코드** hello hello 액세스 제어 레코드의 테이블 형식 목록에서 블레이드 hello toodelete 한다고 ACR를 두 번 클릭 합니다.

3. Hello 편집 액세스 제어 레코드 블레이드에서 클릭 **삭제**합니다.
   
    ![ACR 삭제](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. 확인 메시지가 나타나면 클릭 **삭제** toocontinue hello 삭제 합니다. hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제입니다.
   
   ![경고 메시지](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>다음 단계

* [볼륨 추가 및 ACR 구성](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)에 대해 자세히 알아봅니다.

