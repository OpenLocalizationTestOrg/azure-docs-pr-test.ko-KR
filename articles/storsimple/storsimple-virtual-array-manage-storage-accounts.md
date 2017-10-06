---
title: "StorSimple 가상 배열 저장소 계정 자격 증명 aaaManage | Microsoft Docs"
description: "StorSimple 가상 배열 hello와 연결 된 저장소 계정 자격 증명에 대 한 hello StorSimple 장치 관리자 구성 페이지 tooadd, 편집, 삭제 또는 회전 hello 보안 키를 사용 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>StorSimple 가상 배열에 대 한 StorSimple 장치 관리자를 사용 하 여 toomanage 저장소 계정 자격 증명

## <a name="overview"></a>개요
hello **구성** StorSimple 가상 배열의 hello StorSimple 장치 관리자 서비스 블레이드에서의 섹션에서는 hello StorSimple Manager 서비스에서에서 만들 수 있는 hello 글로벌 서비스 매개 변수를 제공 합니다. 이러한 매개 변수에 적용 된 tooall hello 장치 toohello 서비스를 연결 하 고 포함 될 수 있습니다.

* 저장소 계정 자격 증명
* 액세스 제어 레코드
  
  ![장치 관리자 서비스 대시보드](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

이 자습서에서는 StorSimple 가상 배열에 대한 저장소 계정 자격 증명을 추가, 편집 또는 삭제하는 방법에 대해 설명합니다. 이 자습서에서는 hello 정보에는 StorSimple 가상 배열 toohello만 적용 됩니다. 8000 시리즈에 toomanage 저장소 계정 하는 방법에 대 한 정보를 참조 하십시오. [사용 하 여 hello StorSimple 관리자 서비스 toomanage 저장소 계정의](storsimple-manage-storage-accounts.md)합니다.

저장소 계정 자격 증명 장치 hello는 hello 자격 증명은 포함 tooaccess 저장소 계정과 클라우드 서비스 공급자를 사용 합니다. Microsoft Azure 저장소 계정에 대 한 hello 계정 이름 및 hello 기본 액세스 키 등의 자격 증명 이들은입니다.

Hello에 **저장소 계정 자격 증명** 블레이드, 모든 저장소 계정 구독 청구 hello에 대해 생성 된 자격 증명이 hello 다음 정보를 포함 하는 테이블 형식으로 표시 됩니다.

* **이름** – 만들어질 때 할당 된 고유한 이름 toohello 계정 hello 합니다.
* **SSL 사용 가능** – 여부 hello SSL을 사용 및 장치-클라우드 간 통신이 보안 채널 hello 됩니다.
  
  ![구성 섹션](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

hello 가장 일반적인 작업 관련 hello에 수행할 수 있는 toostorage 계정 자격 증명 **저장소 계정 자격 증명** 블레이드 됩니다.

* 저장소 계정 자격 증명 추가
* 저장소 계정 자격 증명 편집
* 저장소 계정 자격 증명 삭제

## <a name="types-of-storage-account-credentials"></a>저장소 계정 자격 증명 유형
StorSimple 장치에서 사용할 수 있는 저장소 계정 자격 증명에는 다음과 같은 세 종류가 있습니다.

* **자동 생성 된 저장소 계정 자격 증명** – hello 서비스를 처음 만들 때 이러한 종류의 저장소 계정 자격 증명은 자동으로 생성 hello 이름에서 알 수 있듯이 합니다. 이 저장소 계정 자격 증명 생성 방법에 대해 자세히 toolearn 참조 [새 서비스 만들기](storsimple-virtual-array-manage-service.md#create-a-service)합니다.
* **hello 서비스 구독에 저장소 계정 자격 증명** –이 hello Azure 저장소 계정 연결 된 자격 증명 hello hello 서비스와 동일한 구독 합니다. 이러한 저장소 계정 자격 증명 만들어지는 방식에 대해 자세히 toolearn 참조 [Azure 저장소 계정에 대 한](../storage/common/storage-create-storage-account.md)합니다.
* **hello 서비스 구독 외부 저장소 계정 자격 증명** – 서비스와 연결 되지 않은 hello Azure 저장소 계정 자격 증명 이며 가능성이 하기 전에 기존된 hello 서비스를 만들었습니다.

## <a name="add-a-storage-account-credential"></a>저장소 계정 자격 증명 추가
고유한 제공 하 여 저장소 계정 자격 증명 tooyour StorSimple 장치 관리자 서비스 구성을 추가할 수 있습니다 친숙 한 이름 및 액세스 자격 증명을 toohello 저장소 계정을 연결 합니다. Hello secure sockets layer (SSL) 모드 toocreate 장치와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널 설정의 hello 옵션이 있습니다.

특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다. Hello 저장소 계정 자격 증명을 저장 하는 동안 hello 서비스는 클라우드 서비스 공급자와 toocommunicate을 시도 합니다. 이 이번에는 hello 자격 증명 및 사용자가 제공한 hello 액세스 자료가 인증 됩니다. 저장소 계정 자격 증명 hello 인증에 성공 하는 경우에 만들어집니다. Hello 인증에 실패 하면 적절 한 오류 메시지가 표시 됩니다.

다음 프로시저 tooadd Azure 저장소 계정 자격 증명 hello를 사용 합니다.

* 저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독
* tooadd hello 장치 관리자 서비스 구독 외부의 Azure 저장소 계정 자격 증명

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독

1. Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션.
3. **추가**를 클릭합니다.
4. Hello에 **저장소 계정 추가** 블레이드에서 다음 hello지 않습니다.
   
    1. **구독**에 **현재**를 선택합니다.
    2. Azure 저장소 계정의 hello 이름을 제공 합니다.
    3. 선택 **사용** toocreate StorSimple 장치 및 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다. 사설 클라우드 내에서 작동하는 경우에만 **사용 안 함**을 선택합니다.
    4. **추가**를 클릭합니다. Hello 저장소 계정이 정상적으로 만들어지면 알림이 표시 됩니다.<br></br>
   
        ![기존 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd hello 장치 관리자 서비스 구독 외부의 Azure 저장소 계정 자격 증명

1. Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션. Hello StorSimple 장치 관리자 서비스와 관련 된 모든 기존 저장소 계정 자격 증명을 나열 합니다.
3. **추가**를 클릭합니다.
4. Hello에 **저장소 계정 추가** 블레이드에서 다음 hello지 않습니다.
   
    1. **구독**에 **기타**를 선택합니다.
   
    2. Azure 저장소 계정 자격 증명의 hello 이름을 제공 합니다.
   
    3. Hello에 **저장소 계정 액세스 키** 텍스트 상자 공급 hello Azure 저장소 계정 자격 증명에 대 한 기본 액세스 키입니다. 이 키 tooget toohello Azure 저장소 서비스를 이동 저장소 계정 자격 증명을 선택 하 고 클릭 **계정 키를 관리**합니다. 이제 hello 기본 액세스 키를 복사할 수 있습니다.
   
    4. SSL을 tooenable 클릭 hello **사용** 단추 toocreate StorSimple 장치 관리자 서비스와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다. Hello 클릭 **사용 하지 않도록 설정** 사설 클라우드 내에서 작동 하는 경우에 단추입니다.
   
    5. **추가**를 클릭합니다. 저장소 계정 자격 증명 hello 정상적으로 만들어지면 알림이 표시 됩니다.

5. hello 새로 만든 저장소 계정 자격 증명 hello 장치 관리자를 구성 하는 StorSimple 서비스 블레이드 아래에 표시 되는 **저장소 계정 자격 증명**합니다.
   
    ![Hello 장치 관리자 서비스 구독 외부 저장소 계정 자격 증명을 추가 합니다.](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>저장소 계정 자격 증명 편집
장치에서 사용하는 저장소 계정 자격 증명을 편집할 수 있습니다. 현재 사용 중인 저장소 계정 자격 증명을 편집할 경우 hello 필드 사용 가능한 toomodify은 hello 액세스 키와 hello 저장소 계정 자격 증명에 대 한 hello SSL 모드를 사용 합니다. Hello 새로운 저장소 액세스 키를 제공 하거나 hello를 수정할 수 있습니다 **SSL 모드 사용** 선택 하 고 업데이트 하는 hello 설정을 저장 합니다.

#### <a name="tooedit-a-storage-account-credential"></a>저장소 계정 자격 증명 tooedit
1. Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션. Hello StorSimple 장치 관리자 서비스와 관련 된 모든 기존 저장소 계정 자격 증명을 나열 합니다.
3. 저장소 계정 자격 증명 hello 테이블 형식 목록에서 선택 하 고 toomodify hello 계정을 두 번 클릭 합니다.
4. Hello 저장소 계정 자격 증명에서 **속성** 블레이드에서 다음 hello지 않습니다.
   
   1. 필요에 따라 수정할 수 있습니다 hello **SSL 사용** 모드 선택 합니다.
   2. Tooregenerate 저장소 계정 자격 증명 액세스 키를 선택할 수 있습니다. 자세한 내용은 참조 [hello 저장소 계정 키 다시 생성](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)합니다. Hello 새 저장소 계정 자격 증명 키를 제공 합니다. Azure 저장소 계정에 대 한 hello 기본 액세스 키입니다.
   3. 클릭 **저장** hello의 hello 위쪽 **속성** 블레이드 toosave hello 설정 합니다. hello 설정은 hello에서 업데이트 됩니다 **저장소 계정 자격 증명** 블레이드입니다.
      
      ![저장소 계정 자격 증명 편집](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>저장소 계정 자격 증명 삭제
> [!IMPORTANT]
> 사용하지 않는 경우에만 저장소 계정 자격 증명을 삭제할 수 있습니다. 저장소 계정 자격 증명을 사용하는 중이면 알림이 표시됩니다.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>저장소 계정 자격 증명 toodelete
1. Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션. Hello StorSimple 장치 관리자 서비스와 관련 된 모든 기존 저장소 계정 자격 증명을 나열 합니다.
3. 저장소 계정 자격 증명 hello 테이블 형식 목록에서 선택 하 고 toodelete hello 계정을 두 번 클릭 합니다.
4. Hello 저장소 계정 자격 증명에서 **속성** 블레이드에서 다음 hello지 않습니다.
   
   1. 클릭 **삭제** toodelete hello 자격 증명입니다.
   2. 확인 메시지가 나타나면 클릭 **예** toocontinue hello 삭제 합니다. 테이블 형식 목록 hello은 업데이트 된 tooreflect hello 변경 합니다.
      
      ![저장소 계정 자격 증명 삭제](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>저장소 계정 자격 증명 키 동기화
보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다. Microsoft Azure 관리자가 다시 생성 하거나 (Microsoft Azure 저장소 서비스 hello)를 통해 저장소 계정 자격 증명 hello에 직접 액세스 하 여 hello 기본 또는 보조 키를 변경할 수 있습니다. hello StorSimple 장치 관리자 서비스는이 변경 내용을 자동으로 표시 되지 않습니다.

tooaccess hello StorSimple 장치 관리자 서비스가 필요한 hello 변경의 tooinform hello StorSimple 장치 관리자 서비스의 경우, 액세스 hello 저장소 계정 자격 증명을 한 후 (변경 된 어떤 것에 따라) hello 기본 또는 보조 키를 동기화 합니다. hello 서비스 다음 hello 최신 키를 가져옵니다, 그리고 hello 키 암호화 및 hello 키 toohello 장치 암호화를 보냅니다.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>저장소 계정 자격 증명에 대 한 키 toosynchronize hello hello 서비스 (Azure에만 해당)와 같은 구독
1. Hello 서비스 방문 블레이드에서 서비스를 선택, hello 서비스 이름 및 다음 hello에 두 번 클릭 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.
2. Hello에 **저장소 계정 자격 증명** 블레이드에서 hello 목록에서 저장소 계정 자격 증명 선택 hello 저장소 계정 자격 증명 toosynchronize 되도록 해당 레지스트리 키입니다.
3. Hello에 **속성** 블레이드 hello에 대 한 저장소 계정 자격 증명을 선택 하면 다음 hello지 않습니다.
   
    1. **추가**를 클릭한 다음 **동기화 선택키**를 클릭합니다.
   
    2. 확인 메시지가 나타나면 클릭 **동기화 키** toocomplete hello 동기화 합니다.
    
4. StorSimple 장치 관리자 서비스 hello hello Microsoft Azure 저장소 서비스에서에서 이전에 변경 된 tooupdate hello 키를 해야 합니다. Hello에 **동기화 저장소 계정 키** 블레이드에서 hello 기본 액세스 키 (다시 생성) 변경 된 경우 기본를 클릭 한 다음 클릭 **동기화 키**합니다. 클릭 하 여 hello 보조 키를 변경한 경우 **보조**, 클릭 하 고 **동기화 키**합니다.
   
    ![동기화 선택키](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.

