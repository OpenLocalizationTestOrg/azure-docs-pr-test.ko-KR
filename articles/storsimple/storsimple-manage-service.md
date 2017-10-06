---
title: "StorSimple Manager 서비스 aaaDeploy hello | Microsoft Docs"
description: "어떻게 toocreate 및 delete hello hello Azure 클래식 포털에서에서 StorSimple Manager 서비스에 설명 하 고 toomanage 서비스 등록 키를 hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 hello StorSimple Manager 서비스를 배포 합니다.

## <a name="overview"></a>개요
hello StorSimple Manager 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다. Hello 서비스를 만든 후 toomanage hello 장치 hello Microsoft Azure 클래식 포털에서 실행 되는 브라우저에서 사용할 수 있습니다. 이렇게 하면 하므로 관리 부담이 최소화 하나의 중앙 위치에서 모든 hello 장치에 연결 된 toohello StorSimple 관리자 서비스 toomonitor 있습니다.

StorSimple Manager 방문 페이지 hello 모든 hello StorSimple Manager 서비스를 사용할 수 있는 toomanage StorSimple 저장소 장치를 나열 합니다. 각 StorSimple Manager 서비스에 대해 다음 정보는 hello hello StorSimple 관리자 페이지에 표시 됩니다.

* **이름** – tooyour StorSimple Manager 서비스를 만들 때 할당 된 hello 이름입니다. **hello 서비스를 만든 후에 hello 서비스 이름을 변경할 수 없습니다. 장치, 볼륨, 볼륨 컨테이너 및 백업 정책을 hello Azure 클래식 포털에서에서 이름을 바꿀 수 없는 같은 다른 엔터티에도 마찬가지 이기도 합니다.**
* **상태** – 될 수 있는 hello 서비스의 상태를 hello **활성**, **만들기**, 또는 **온라인**합니다.
* **위치** – hello 지리적 위치는 hello StorSimple 장치 배포 됩니다.
* **구독** – hello 서비스와 연결 된 구독을 청구 합니다.

hello hello StorSimple 관리자 페이지를 통해 수행할 수 있는 일반적인 작업입니다.

* 서비스 만들기
* 서비스 삭제
* Hello 서비스 등록 키 가져오기
* Hello 서비스 등록 키 다시 생성

이 자습서에서는 설명 방법을 각 tooperform 작업 합니다.

## <a name="create-a-service"></a>서비스 만들기
사용 하 여 hello **빠른 생성** toocreate StorSimple Manager 서비스 toodeploy StorSimple 장치를 원하는 경우 옵션입니다. 서비스 toocreate toohave가 필요합니다.

* 엔터프라이즈 계약을 사용하여 구독
* 활성 Microsoft Azure 저장소 계정
* hello 청구 액세스 관리에 사용 되는 정보

선택할 수 있습니다도 toogenerate 기본 저장소 계정 hello 서비스를 만들 때.

하나의 서비스로 여러 장치를 관리할 수 있습니다. 하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다. 대규모 엔터프라이즈는 여러 서비스 인스턴스 toowork 서로 다른 구독, 조직 또는 배포 위치를 가질 수 있습니다. StorSimple Manager 서비스 toomanage StorSimple 8000 시리즈 장치 및 StorSimple 가상 배열의 인스턴스를 개별 필요한 note 하십시오.

> [!IMPORTANT] 
> 사용 하지 않는 서비스 (이 리소스에 대해 작업이 장치 없음)이 생성 하는 경우 이전 tooAugust 2016의 경우 Azure 포털 또는 Azure 클래식 포털을 통해 관리할 수 없습니다. Hello Azure 포털에서에서 새 서비스를 만드는 것이 좋습니다.

다음 단계 toocreate 서비스는 hello를 수행 합니다.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>서비스 삭제
서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다. Hello 서비스를 사용 하는 경우 연결 된 hello 장치를 비활성화 합니다. 작업을 비활성화 하는 hello 서버 hello 장치와 hello 서비스 hello 연결 하지만 hello 클라우드에서 hello 장치 데이터를 보존 됩니다.

> [!IMPORTANT] 
> 서비스가 삭제 된 후에 hello 작업을 되돌릴 수 없습니다. Hello 서비스를 사용 하는 모든 장치 toobe 할 초기값으로 재설정 다른 서비스와 함께 사용할 수 있습니다. 이 시나리오에서는 hello 구성 뿐만 아니라 hello 장치에서 hello 로컬 데이터가 손실 됩니다.

다음 단계 toodelete 서비스는 hello를 수행 합니다.

### <a name="toodelete-a-service"></a>toodelete 서비스
1. Hello에 **StorSimple Manager 서비스** toodelete 한다고 hello 선택 서비스 페이지입니다.
2. 클릭 **삭제** hello hello 페이지 맨 아래에 있습니다.
3. 클릭 **예** hello 알림이에 있습니다. 삭제 하는 hello 서비스 toobe 몇 분 정도 걸릴 수 있습니다.

## <a name="get-hello-service-registration-key"></a>Hello 서비스 등록 키 가져오기
서비스를 성공적으로 만든 후 hello 서비스와 StorSimple 장치의 tooregister 필요 합니다. tooregister 첫 번째 StorSimple 장치의 서비스 등록 키 hello 필요 합니다. tooregister 기존 StorSimple 서비스와 장치를 추가할 필요가 hello 등록 키와 hello 서비스 데이터 암호화 키 (생성 된 hello 첫 번째 장치에 등록 하는 동안) 해야 합니다. Hello 서비스 데이터 암호화 키에 대 한 자세한 내용은 참조 [StorSimple 보안](storsimple-security.md)합니다. 에 액세스 하 여 hello 등록 키를 받을 수 **등록 키** hello에 **서비스** 페이지.

Hello 단계 tooget hello 서비스 등록 키를 다음을 수행 합니다.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Hello 서비스 등록 키를 안전한 위치에 유지 합니다. 이 키를으로 hello 서비스 데이터 암호화 키를이 서비스를 사용 하 여 추가 장치 tooregister 필요 합니다. Hello 서비스 등록 키를 얻은 후 StorSimple 인터페이스에 대 한 tooconfigure에 hello Windows PowerShell을 통해 장치가 필요 합니다.

방법에 대 한 자세한 내용은 toouse이 등록 키가 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.

## <a name="regenerate-hello-service-registration-key"></a>Hello 서비스 등록 키 다시 생성
필요한 tooperform 키 회전 또는 서비스 관리자 목록이 hello에 변경 되었는지 여부 tooregenerate 서비스 등록 키가 필요 합니다. Hello 키를 다시 생성 하면 hello 새 키는 후속 장치를 등록 하는 중에 사용 됩니다. 이미 등록 된 hello 장치가이 프로세스에 의해 영향을 받지 않습니다.

Hello 단계 tooregenerate 서비스 등록 키가 다음을 수행 합니다.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 서비스 등록 키
1. Hello에 **StorSimple Manager 서비스** 페이지 **등록 키**합니다.
2. Hello에 **서비스 등록 키** 대화 상자를 클릭 **다시 생성**합니다.
3. 확인 메시지가 표시됩니다. 클릭 **확인** toocontinue와 hello 재생성 합니다.
4. 새 서비스 등록 키가 나타납니다.
5. 이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.
6. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose이 대화 상자.

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [StorSimple 배포 프로세스](storsimple-deployment-walkthrough-u2.md)합니다.
* [StorSimple 저장소 계정 관리](storsimple-manage-storage-accounts.md)에 대해 자세히 알아봅니다.
* 너무 방법에 대 한 자세한[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.
