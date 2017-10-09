---
title: "Microsoft Azure StorSimple 8000 시리즈 장치에 대 한 StorSimple 저장소 계정 자격 증명 aaaManage | Microsoft Docs"
description: "저장소 계정에 대 한 hello StorSimple 장치 관리자 구성 페이지 tooadd, 편집, 삭제 또는 회전 hello 보안 키를 사용 하는 방법을 설명 합니다."
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
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Hello StorSimple 장치 관리자 서비스 toomanage 저장소 계정 자격 증명 사용

## <a name="overview"></a>개요

hello **구성** hello StorSimple 장치 관리자 서비스 블레이드에서 섹션에서는 hello StorSimple 장치 관리자 서비스에서에서 만들 수 있는 모든 hello 글로벌 서비스 매개 변수를 제공 합니다. 이러한 매개 변수에 적용 된 tooall hello 장치 toohello 서비스를 연결 하 고 포함 될 수 있습니다.

* 저장소 계정 자격 증명
* 대역폭 템플릿 
* 액세스 제어 레코드 

이 자습서에서는 tooadd를 편집 하거나 저장소 계정 자격 증명을 삭제 또는 저장소 계정에 대 한 hello 보안 키를 바꾸는 방법을 설명 합니다.

 ![저장소 계정 자격 증명 목록](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

저장소 계정은 hello StorSimple 장치 사용 하 여 tooaccess 저장소 계정과 클라우드 서비스 공급자는 hello 자격 증명을 포함 합니다. Microsoft Azure 저장소 계정에 대 한 hello 계정 이름 및 hello 기본 액세스 키 등의 자격 증명 이들은입니다. 

Hello에 **저장소 계정 자격 증명** 블레이드, 모든 저장소 계정을 구독 청구 hello에 대해 생성 된 hello 다음 정보를 포함 하는 테이블 형식으로 표시 됩니다.

* **이름** – 만들어질 때 할당 된 고유한 이름 toohello 계정 hello 합니다.
* **SSL 사용 가능** – 여부 hello SSL을 사용 및 장치-클라우드 간 통신이 보안 채널 hello 됩니다.
* **사용 하는** – hello hello 저장소 계정을 사용 하 여 볼륨의 수입니다.

hello 가장 일반적인 작업 관련된 toostorage 계정을 수행할 수 있는 됩니다.

* 저장소 계정 추가 
* 저장소 계정 편집 
* 저장소 계정 삭제 
* 저장소 계정의 키 회전 

## <a name="types-of-storage-accounts"></a>저장소 계정 유형

StorSimple 장치에서 사용할 수 있는 저장소 계정에는 다음과 같은 세 종류가 있습니다.

* **자동 생성 된 저장소 계정은** – hello 서비스를 처음 만들 때 이러한 유형의 저장소 계정 자동으로 생성 hello 이름에서 알 수 있듯이 합니다. 이 저장소 계정을 만든 방법에 대해 자세히 toolearn 참조 [1 단계: 새 서비스 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) 에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다. 
* **Hello 서비스 구독의 저장소 계정에에서** – hello와 관련 된 hello Azure 저장소 계정 hello 서비스와 동일한 구독 합니다. 이러한 저장소 계정이 생성 되는 방법에 대해 자세히 toolearn 참조 [Azure 저장소 계정에 대 한](../storage/common/storage-create-storage-account.md)합니다. 
* **Hello 서비스 구독 외부 저장소 계정** – 서비스와 연결 되지 않은 hello Azure 저장소 계정 및 가능성이 하기 전에 기존된 hello 서비스를 만들었습니다.

## <a name="add-a-storage-account"></a>저장소 계정 추가

고유한 제공 하 여 저장소 계정을 추가할 수 있습니다 친숙 한 이름 및 액세스 자격 증명을 toohello 저장소 계정 (hello 지정 된 클라우드 서비스 공급자)에 연결 합니다. Hello secure sockets layer (SSL) 모드 toocreate 장치와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널 설정의 hello 옵션이 있습니다.

특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다. 그러나 주의 저장소 계정이 만들어지면 hello 클라우드 서비스 공급자 변경할 수 없습니다.

Hello 저장소 계정, 저장 하는 동안 hello 서비스는 클라우드 서비스 공급자와 toocommunicate을 시도 합니다. 이 이번에 hello 자격 증명 및 사용자가 제공한 hello 액세스 자료가 인증 됩니다. 저장소 계정에는 hello 인증에 성공 하는 경우에 생성 됩니다. Hello 인증에 실패 하면 적절 한 오류 메시지가 표시 됩니다.

다음 프로시저 tooadd Azure 저장소 계정 자격 증명 hello를 사용 합니다.

* 저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독
* tooadd hello 장치 관리자 서비스 구독 외부의 Azure 저장소 계정 자격 증명

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd hello StorSimple 장치 관리자 서비스 구독 외부 Azure 저장소 계정 자격 증명

1. Tooyour StorSimple 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션. Hello StorSimple 장치 관리자 서비스와 관련 된 모든 기존 저장소 계정 자격 증명을 나열 합니다.
3. **추가**를 클릭합니다.
4. Hello에 **저장소 계정 자격 증명 추가** 블레이드에서 다음 hello지 않습니다:
   
    1. **구독**에 **기타**를 선택합니다.
   
    2. Azure 저장소 계정 자격 증명의 hello 이름을 제공 합니다.
   
    3. Hello에 **저장소 계정 액세스 키** 텍스트 상자 공급 hello Azure 저장소 계정 자격 증명에 대 한 기본 액세스 키입니다. 이 키 tooget toohello Azure 저장소 서비스를 이동 저장소 계정 자격 증명을 선택 하 고 클릭 **계정 키를 관리**합니다. 이제 hello 기본 액세스 키를 복사할 수 있습니다.
   
    4. SSL을 tooenable 클릭 hello **사용** 단추 toocreate StorSimple 장치 관리자 서비스와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다. Hello 클릭 **사용 하지 않도록 설정** 사설 클라우드 내에서 작동 하는 경우에 단추입니다.
   
    5. **추가**를 클릭합니다. 저장소 계정 자격 증명 hello 정상적으로 만들어지면 알림이 표시 됩니다.

5. hello 새로 만든 저장소 계정 자격 증명 hello 장치 관리자를 구성 하는 StorSimple 서비스 블레이드 아래에 표시 되는 **저장소 계정 자격 증명**합니다.
   


## <a name="edit-a-storage-account"></a>저장소 계정 편집

볼륨 컨테이너에서 사용되는 저장소 계정을 편집할 수 있습니다. 현재 사용 중인 저장소 계정을 편집할 경우 hello 필드 에서만 사용할 수 있는 toomodify는 hello hello 저장소 계정 액세스 키입니다. Hello 새로운 저장소 액세스 키를 제공 하 고 업데이트 hello 설정을 저장할 수 있습니다.

#### <a name="tooedit-a-storage-account"></a>tooedit 저장소 계정

1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.

    ![저장소 계정 자격 증명](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. Hello에 **저장소 계정 자격 증명** 블레이드에서 저장소 계정 자격 증명을 선택 hello 목록에서 하 고 hello tooedit 시겠습니까 하나 클릭 합니다. 

3. Hello를 수정할 수 있습니다 **SSL 사용** 선택 합니다. 클릭할 수도 있습니다 **더...**  선택한 후 **동기화 액세스 키 toorotate** 저장소 계정 액세스 키입니다. 너무 이동[키 저장소 계정의 순환](#key-rotation-of-storage-accounts) tooperform 키 순환 하는 방법에 대 한 자세한 내용은 합니다. Hello 설정을 수정한 후 클릭 **저장**합니다. 

    ![편집된 저장소 계정 자격 증명 저장](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. 

    ![수정 확인](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

hello 설정은 업데이트 하 고 저장소 계정에 대 한 저장 해야 합니다. 

## <a name="delete-a-storage-account"></a>저장소 계정 삭제

> [!IMPORTANT]
> 볼륨 컨테이너에서 사용하지 않는 경우에만 저장소 계정을 삭제할 수 있습니다. 저장소 계정이 볼륨 컨테이너에서 사용 중인 먼저 hello 볼륨 컨테이너를 삭제 한 다음 hello 연결 된 저장소 계정을 삭제 합니다.

#### <a name="toodelete-a-storage-account"></a>toodelete 저장소 계정

1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.

2. 저장소 계정의 hello 테이블 형식 목록에서 원하는 toodelete hello 계정 마우스로 가리킵니다. Tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.

    ![저장소 계정 자격 증명 삭제](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. 확인 메시지가 나타나면 클릭 **예** toocontinue hello 삭제 합니다. hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 변경 됩니다.

    ![삭제 확인](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>저장소 계정의 키 회전

보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다. 각 Microsoft Azure 구독에 하나 이상의 연결된 저장소 계정을 만들 수 있습니다. hello 액세스 toothese 계정은 hello 구독 및 각 저장소 계정에 대 한 선택 키에 의해 제어 됩니다. 

저장소 계정을 만들 때 Microsoft Azure hello 저장소 계정에 액세스할 때 인증에 사용 되는 두 개의 512 비트 저장소 액세스 키를 생성 합니다. 두 개의 저장소 액세스 키를 갖는 것 중단 tooyour 저장소 서비스와 액세스 toothat 서비스 없는 tooregenerate hello 키가 있습니다. hello 현재 사용 중인 키는 hello *기본* 키와 hello 백업 키가 참조 tooas hello *보조* 키입니다. Microsoft Azure StorSimple 장치가 클라우드 저장소 서비스 공급자에 액세스할 때 이러한 두 키 중 하나를 제공해야 합니다.

## <a name="what-is-key-rotation"></a>키 회전 정의

일반적으로 응용 프로그램 중 하나만 사용 hello 키 tooaccess 데이터입니다. 특정 시간이 지나면, toousing hello에 대 한 두 번째 키 전환 하는 응용 프로그램을 사용할 수 있습니다. 응용 프로그램 toohello 보조 키를 전환한 후 hello 첫 번째 키를 사용 중지 하 고 새 키를 생성 합니다. 이러한 방식으로 hello 두 키를 사용 하 여 가동 중지 시간 없이 응용 프로그램 액세스 toohello 데이터 수 있습니다.

hello 저장소 계정 키는 항상 암호화 된 형태로 hello 서비스에 저장 됩니다. 그러나 이러한 hello StorSimple 장치 관리자 서비스를 통해 재설정할 수 있습니다. hello 서비스는 hello 기본 키를 얻을 수 있습니다 및 보조 키 hello 기본 저장소 계정을 hello 저장소 서비스에서 만들어지는 계정과 포함 하 여 동일한 구독을 생성 하는 hello에 있는 저장소 계정의 모든 hello에 대 한 StorSimple 장치 관리자 hello 때 서비스 서비스를 처음 만들 합니다. hello StorSimple 장치 관리자 서비스는 항상 이러한 키 hello Azure 클래식 포털에서에서 가져오고 그런 다음 암호화 된 방식에서 모두를 저장 합니다.

## <a name="rotation-workflow"></a>회전 워크플로

Microsoft Azure 관리자가 다시 생성 하거나 (Microsoft Azure 저장소 서비스 hello)를 통해 hello 저장소 계정에 직접 액세스 하 여 hello 기본 또는 보조 키를 변경할 수 있습니다. hello StorSimple 장치 관리자 서비스는이 변경 내용을 자동으로 표시 되지 않습니다.

hello 변경의 tooinform hello StorSimple 장치 관리자 서비스를 해야 tooaccess hello StorSimple 장치 관리자 서비스 hello 저장소 계정에 액세스 한 후 (변경 된 어떤 것에 따라) hello 기본 또는 보조 키를 동기화 합니다. hello 서비스 다음 hello 최신 키를 가져옵니다, 그리고 hello 키 암호화 및 hello 키 toohello 장치 암호화를 보냅니다.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>저장소 계정에 대 한 키 toosynchronize hello hello 서비스와 같은 구독 
1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.
2. 저장소 계정의 테이블 형식 목록 hello에서 원하는 toomodify hello 하나를 클릭 합니다. 

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. 클릭 **중... 더 많은** 선택한 후 **동기화 액세스 키 toorotate**합니다.   

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. StorSimple 장치 관리자 서비스 hello hello Microsoft Azure 저장소 서비스에서에서 이전에 변경 된 tooupdate hello 키를 해야 합니다. Hello 기본 액세스 키 (다시 생성)가 변경 되었을 경우 선택 **기본** 키입니다. Hello 보조 키가 변경 된 경우 선택 **보조** 키입니다. **키 동기화**를 클릭합니다.
      
      ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Hello 키가 성공적으로 sycnhronized 후 알림이 표시 됩니다.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize는 hello 서비스 구독 외부 저장소 계정에 대 한 키
1. Hello에 **서비스** 페이지에서 hello **구성** 탭 합니다.
2. **저장소 계정 추가/편집**을 클릭합니다.
3. Hello 대화 상자에서 수행 hello를 수행 합니다.
   
   1. 원하는 tooupdate hello 액세스 키를 가진 hello 저장소 계정을 선택 합니다.
   2. StorSimple 장치 관리자 서비스 hello tooupdate hello 저장소 액세스 키를 해야 합니다. 이 경우 hello 저장소 액세스 키를 볼 수 있습니다. Hello에 hello 새 키를 입력 **저장소 계정 액세스 키** 상자입니다. 
   3. 변경 내용을 저장합니다. 이제 저장소 계정 액세스 키가 업데이트됩니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

