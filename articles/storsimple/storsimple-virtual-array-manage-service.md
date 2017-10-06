---
title: "StorSimple 장치 관리자 서비스 aaaDeploy | Microsoft Docs"
description: "어떻게 toocreate 및 delete hello hello Azure 포털에서에서 StorSimple 장치 관리자 서비스에 설명 하 고 toomanage 서비스 등록 키를 hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>StorSimple 가상 배열에 대 한 hello StorSimple 장치 관리자 서비스를 배포 합니다.
## <a name="overview"></a>개요

hello StorSimple 장치 관리자 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다. Hello 서비스를 만든 후 toomanage hello 장치 hello Microsoft Azure 포털에서 실행 되는 브라우저에서 사용할 수 있습니다. 이렇게 하면 모든 hello 장치에 연결 된 toohello StorSimple 장치 관리자 하므로 관리 부담이 최소화 하나의 중앙 위치에서 서비스 toomonitor 있습니다.

hello 일반적인 작업 관련된 tooa StorSimple 장치 관리자 서비스는.

* 서비스 만들기
* 서비스 삭제
* Hello 서비스 등록 키 가져오기
* Hello 서비스 등록 키 다시 생성

이 자습서에서는 각 tooperform의 선행 작업 hello 하는 방법을 설명 합니다. 이 문서에 포함 된 hello 정보에만 적용 가능한 tooStorSimple 가상 배열입니다. StorSimple 8000 시리즈에 대 한 자세한 내용은 이동 너무[StorSimple Manager 서비스를 배포](storsimple-manage-service.md)합니다.

## <a name="create-a-service"></a>서비스 만들기

서비스 toocreate toohave가 필요합니다.

* 엔터프라이즈 계약을 사용하여 구독
* 활성 Microsoft Azure 저장소 계정
* hello 청구 액세스 관리에 사용 되는 정보

선택할 수 있습니다도 toogenerate 저장소 계정을 hello 서비스를 만들 때.

하나의 서비스로 여러 장치를 관리할 수 있습니다. 하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다. 대규모 엔터프라이즈는 여러 서비스 인스턴스 toowork 서로 다른 구독, 조직 또는 배포 위치를 가질 수 있습니다.

> [!NOTE]
> StorSimple 장치 관리자 서비스 toomanage StorSimple 8000 시리즈 장치 및 StorSimple 가상 배열의 별도 인스턴스 필요합니다.


다음 단계 toocreate 서비스는 hello를 수행 합니다.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>서비스 삭제

서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다. Hello 서비스를 사용 하는 경우 연결 된 hello 장치를 비활성화 합니다. 작업을 비활성화 하는 hello 서버 hello 장치와 hello 서비스 hello 연결 하지만 hello 클라우드에서 hello 장치 데이터를 보존 됩니다.

> [!IMPORTANT]
> 서비스가 삭제 된 후에 hello 작업을 되돌릴 수 없습니다. Hello 서비스를 사용 하는 모든 장치 toobe 할 초기값으로 재설정 다른 서비스와 함께 사용할 수 있습니다. 이 시나리오에서는 hello 구성 뿐만 아니라 hello 장치에서 hello 로컬 데이터가 손실 됩니다.
 

다음 단계 toodelete 서비스는 hello를 수행 합니다.

#### <a name="toodelete-a-service"></a>toodelete 서비스

1. 너무 이동**모든 리소스**합니다. StorSimple Device Manager 서비스를 검색합니다. 원하는 toodelete hello 서비스를 선택 합니다.
   
    ![서비스 toodelete 선택](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. 이동 tooyour 서비스 대시보드 tooensure는 연결 된 toohello 서비스는 장치가 없습니다. 이 서비스에 등록 된 장치가 경우 배너 메시지 toohello 효과를 나타납니다. **삭제**를 클릭합니다.
   
    ![서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. 확인 메시지가 나타나면 클릭 **예** hello 알림이에 있습니다. 
   
    ![서비스 삭제 확인](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. 삭제 하는 hello 서비스 toobe 몇 분 정도 걸릴 수 있습니다. Hello 후 서비스가 성공적으로 삭제 된 메시지가 표시 됩니다.
   
    ![성공적인 서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

서비스의 hello 목록이 새로 고쳐집니다.

 ![업데이트된 서비스 목록](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Hello 서비스 등록 키 가져오기
서비스를 성공적으로 만든 후 hello 서비스와 StorSimple 장치의 tooregister 필요 합니다. tooregister 첫 번째 StorSimple 장치의 서비스 등록 키 hello 필요 합니다. tooregister 기존 StorSimple 서비스와 장치를 추가할 필요가 hello 등록 키와 hello 서비스 데이터 암호화 키 (생성 된 hello 첫 번째 장치에 등록 하는 동안) 해야 합니다. Hello 서비스 데이터 암호화 키에 대 한 자세한 내용은 참조 [StorSimple 보안](storsimple-security.md)합니다. Hello에 액세스 하 여 hello 등록 키를 받을 수 **키** 블레이드 서비스에 대 한 합니다.

Hello 단계 tooget hello 서비스 등록 키를 다음을 수행 합니다.

#### <a name="tooget-hello-service-registration-key"></a>tooget hello 서비스 등록 키
1. Hello에 **StorSimple 장치 관리자** 블레이드에서 너무 이동**관리 &gt;**  **키**합니다.
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Hello에 **키** 블레이드에서 서비스 등록 키가 나타납니다. Hello 복사 아이콘을 사용 하 여 hello 등록 키를 복사 합니다. 

Hello 서비스 등록 키를 안전한 위치에 유지 합니다. 이 키를으로 hello 서비스 데이터 암호화 키를이 서비스를 사용 하 여 추가 장치 tooregister 필요 합니다. Hello 서비스 등록 키를 얻은 후 StorSimple 인터페이스에 대 한 tooconfigure에 hello Windows PowerShell을 통해 장치가 필요 합니다.

## <a name="regenerate-hello-service-registration-key"></a>Hello 서비스 등록 키 다시 생성
필요한 tooperform 키 회전 또는 서비스 관리자 목록이 hello에 변경 되었는지 여부 tooregenerate 서비스 등록 키가 필요 합니다. Hello 키를 다시 생성 하면 hello 새 키는 후속 장치를 등록 하는 중에 사용 됩니다. 이미 등록 된 hello 장치가이 프로세스에 의해 영향을 받지 않습니다.

Hello 단계 tooregenerate 서비스 등록 키가 다음을 수행 합니다.

#### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 서비스 등록 키
1. Hello에 **StorSimple 장치 관리자** 블레이드에서 너무 이동**관리 &gt;**  **키**합니다.
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Hello에 **키** 블레이드에서 클릭 **다시 생성**합니다.
   
   ![다시 생성 클릭](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. Hello에 **Regenerate 서비스 등록 키** 블레이드를 검토 hello 작업 때 필요한 hello 키 다시 생성 됩니다. 이 서비스에 등록 된 하는 모든 hello 후속 장치 hello 새 등록 키를 사용 합니다. 클릭 **다시 생성** tooconfirm 합니다. Hello 등록 완료 되 면 알림이 표시 됩니다.
   
   ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. 새 서비스 등록 키가 나타납니다.
   
    ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[시작](storsimple-virtual-array-deploy1-portal-prep.md) StorSimple 가상 배열입니다.
* 너무 방법에 대해 알아봅니다[StorSimple 장치를 관리할](storsimple-ova-web-ui-admin.md)합니다.

