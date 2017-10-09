---
title: "aaaDeploy hello azure에서 StorSimple 장치 관리자 서비스 | Microsoft Docs"
description: "어떻게 toocreate 및 delete hello hello Azure 포털에서에서 StorSimple 장치 관리자 서비스에 설명 하 고 toomanage 서비스 등록 키를 hello 하는 방법을 설명 합니다."
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
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>StorSimple 8000 시리즈 장치에 대 한 hello StorSimple 장치 관리자 서비스를 배포 합니다.

## <a name="overview"></a>개요

hello StorSimple 장치 관리자 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다. Hello 서비스를 만든 후 있습니다 사용할 수 모든 hello 장치에 연결 된 toohello StorSimple 장치 관리자 서비스 toomanage 하나의 중앙 위치에서 하므로 관리 부담이 최소화 합니다.

이 자습서에서는 hello 만들기, 삭제, hello 서비스의 마이그레이션 및 hello 서비스 등록 키의 hello 관리에 필요한 hello 단계를 설명 합니다. 이 문서에 포함 된 hello 정보에는 적용 가능한 유일한 tooStorSimple 8000 시리즈 장치입니다. StorSimple 가상 배열에 대 한 자세한 내용은 이동 너무[StorSimple 가상 배열에 대 한 StorSimple 장치 관리자 서비스를 배포](storsimple-virtual-array-manage-service.md)합니다.

## <a name="create-a-service"></a>서비스 만들기
StorSimple 장치 관리자 서비스 toocreate toohave가 필요합니다.

* 엔터프라이즈 계약을 사용하여 구독
* 활성 Microsoft Azure 저장소 계정
* hello 청구 액세스 관리에 사용 되는 정보

기업 계약 hello 구독만 허용 됩니다. Microsoft 스폰서쉽 구독 hello Azure 클래식 포털에에서 허용 된 hello Azure 포털에서에서 지원 되지 않습니다. Hello는 지원 되지 않는 구독을 사용 하는 경우 메시지의 뒤에 표시 됩니다.

![유효하지 않은 구독](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

선택할 수 있습니다도 toogenerate 기본 저장소 계정 hello 서비스를 만들 때.

하나의 서비스로 여러 장치를 관리할 수 있습니다. 하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다. 대규모 엔터프라이즈는 여러 서비스 인스턴스 toowork 서로 다른 구독, 조직 또는 배포 위치를 가질 수 있습니다. 

> [!NOTE]
> StorSimple 장치 관리자 서비스 toomanage StorSimple 8000 시리즈 장치 및 StorSimple 가상 배열의 별도 인스턴스 필요합니다.

다음 단계 toocreate 서비스는 hello를 수행 합니다.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


각 StorSimple 장치 관리자 서비스에 대 한 특성을 다음 hello가 있습니다.

* **이름** – tooyour StorSimple 장치 관리자 서비스를 만들 때 할당 된 hello 이름입니다. **hello 서비스를 만든 후에 hello 서비스 이름을 변경할 수 없습니다. 장치, 볼륨, 볼륨 컨테이너 및 백업 정책을 hello Azure 포털에서에서 이름을 바꿀 수 없는 같은 다른 엔터티에도 마찬가지 이기도 합니다.**
* **상태** – 될 수 있는 hello 서비스의 상태를 hello **활성**, **만들기**, 또는 **온라인**합니다.
* **위치** – hello 지리적 위치는 hello StorSimple 장치 배포 됩니다.
* **구독** – hello 서비스와 연결 된 구독을 청구 합니다.

## <a name="move-a-service-tooazure-portal"></a>서비스 tooAzure 포털 이동
StorSimple 8000 시리즈 hello Azure 포털에서에서 이제 관리할 수 있습니다. 기존 서비스 toomanage hello StorSimple 장치를 설정한 경우에 Azure 포털에 서비스 toohello 이동 하는 것이 좋습니다. 2017 년 9 월 30 후 hello StorSimple Manager 서비스에 대 한 Azure 클래식 포털 hello를 사용할 수 없습니다.

hello 옵션 toomigrate toohello Azure 포털 작업 단계에서 제공 됩니다. 옵션 toomigrate tooAzure 포털을 볼 수 없지만 toomove을 hello에 설명 된 대로 마이그레이션의 hello 영향을 검토 해야 하는 경우 [변환에 대 한 고려 사항](#considerations-for-transition)를 할 수 있습니다 [요청을 제출](https://aka.ms/ss8000-cx-signup)합니다.

### <a name="considerations-for-transition"></a>전환에 대한 고려 사항

Hello 서비스를 이동 하기 전에 마이그레이션 toohello 새 Azure 포털의 hello 영향을 검토 합니다.

#### <a name="before-you-transition"></a>전환하기 전에

* 장치가 업데이트 3.0 이상을 실행하고 있습니다. 장치에서 이전 버전을 실행 중인 경우 hello 최신 업데이트를 설치 합니다. 자세한 내용은 이동 너무[업데이트 4 설치](storsimple-8000-install-update-4.md)합니다. StorSimple Cloud Appliance(8010/8020)를 사용하는 경우 업데이트 4.0을 사용하여 새로운 클라우드 어플라이언스를 만듭니다. 

* 새 Azure 포털로 전환된 toohello 했으면에 StorSimple 장치를 Azure 클래식 포털 toomanage hello 사용할 수 없습니다.

* hello 변환은 무중단 이며 hello 장치에 대 한 가동 중지 시간이 없습니다.

* Hello에서 모든 hello StorSimple 장치 관리자를 지정 된 구독 전환 됩니다.

#### <a name="during-hello-transition"></a>Hello 전환 중

* Hello 포털에서 장치를 관리할 수 없습니다.
* 계층화 및 예약 된 백업 등의 작업 toooccur를 계속합니다.
* 삭제 하지 마십시오 hello 전환이 진행 중인 동안 오래 된 StorSimple 장치 관리자 hello 합니다.

#### <a name="after-hello-transition"></a>Hello 전환 후

* 더 이상 hello 클래식 포털에서 장치를 관리할 수 없습니다.

* hello 기존 Azure 서비스 관리 (ASM) PowerShell cmdlet이 지원 되지 않습니다. Hello 스크립트 toomanage hello Azure 리소스 관리자를 통해 장치를 업데이트 합니다.

* 서비스 및 장치 구성이 유지됩니다. 모든 볼륨 및 백업 전환된 toohello Azure 포털 됩니다.

### <a name="begin-transition"></a>전환 시작

Azure 포털에 서비스 toohello hello 단계 tootransition 다음을 수행 합니다.

1. Tooyour hello 클래식 포털에서 기존 StorSimple Manager 서비스를 이동 합니다.

2. Hello StorSimple 장치 관리자 서비스를 지금 hello Azure 포털에서에서 사용할 수 있는지 여부를 알려 주는 알림이 표시 됩니다. 에 Azure 포털에서 hello 서비스 hello 참조 tooas StorSimple 장치 관리자 서비스입니다.

    ![마이그레이션 알림](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. 확인 hello 마이그레이션의 영향을 검토 해야 합니다.
    2. Hello 클래식 포털에서 이동할 수는 StorSimple 장치 관리자의 hello 목록을 검토 합니다.

3. **마이그레이션**을 클릭합니다. hello 전환을 시작 되 고 몇 분 toocomplete 사용.

Hello 전환을 완료 되 면 hello hello Azure 포털에서에서 StorSimple 장치 관리자 서비스를 통해 장치를 관리할 수 있습니다.

Hello Azure 포털에에서만 Update 3.0을 실행 하는 StorSimple 장치를 hello 및 이상이 지원 됩니다. 이전 버전을 실행 하는 hello 장치 제한 된 지원을 제공 합니다. hello 테이블 summrizes hello 클래식 toohello Azure 포털에서에서 마이그레이션한 후 versios 이전 tooUpdate 3.0을 실행 하는 hello 장치에 지원 되는 작업을 수행 합니다.

| 작업                                                                                                                       | 지원됨      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| 장치 등록                                                                                                               | 예            |
| 일반, 네트워크 및 보안과 같은 장치 설정 구성                                                                | 예            |
| 업데이트 검사, 다운로드 및 설치                                                                                             | 예            |
| 장치 비활성화                                                                                                               | 예            |
| 장치 삭제                                                                                                                   | 예            |
| 볼륨 컨테이너 만들기, 수정 및 삭제                                                                                   | 아니요             |
| 볼륨 만들기, 수정 및 삭제                                                                                             | 아니요             |
| 백업 정책 만들기, 수정 및 삭제                                                                                      | 아니요             |
| 수동 백업 수행                                                                                                            | 아니요             |
| 예약된 백업 수행                                                                                                         | 해당 없음 |
| backupset에서 복원                                                                                                        | 아니요             |
| 3.0 이상 업데이트를 실행 하는 복제 tooa 장치 <br> hello 소스 장치 버전 이전 tooUpdate 3.0이 실행 중입니다.                                | 예            |
| 버전 이전 tooUpdate 3.0을 실행 하는 복제 tooa 장치                                                                          | 아니요             |
| 원본 장치로 장애 조치 <br> (3.0 이상 업데이트를 실행 하는 버전 3.0 이전 tooUpdate tooa 장치를 실행 하는 장치)에서                                                               | 예            |
| 대상 장치로 장애 조치 <br> (tooa 장치 소프트웨어 버전 이전 tooUpdate 3.0 실행)                                                                                   | 아니요             |
| 경고 지우기                                                                                                                  | 예            |
| 클래식 포털에서 생성된 백업 정책, 백업 카탈로그, 볼륨, 볼륨 컨테이너, 모니터링 차트, 작업 및 경고 보기 | 예            |
| 장치 컨트롤러 설정 및 해제                                                                                              | 예            |


## <a name="delete-a-service"></a>서비스 삭제

서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다. Hello 서비스를 사용 하는 경우 연결 된 hello 장치를 비활성화 합니다. 작업을 비활성화 하는 hello 서버 hello 장치와 hello 서비스 hello 연결 하지만 hello 클라우드에서 hello 장치 데이터를 보존 됩니다.

> [!IMPORTANT]
> 서비스가 삭제 된 후에 hello 작업을 되돌릴 수 없습니다. Hello 서비스를 사용 하는 모든 장치 toobe 재설정 toofactory 기본값 있어야 다른 서비스와 함께 사용할 수 있습니다. 이 시나리오에서는 hello 구성 뿐만 아니라 hello 장치에서 hello 로컬 데이터가 손실 됩니다.

다음 단계 toodelete 서비스는 hello를 수행 합니다.

### <a name="toodelete-a-service"></a>toodelete 서비스

1. 검색 하려는 toodelete hello 서비스에 대 한 합니다. 클릭 **리소스** 아이콘 및 입력 한 다음 적절 한 용어 toosearch hello 합니다. Hello 검색 결과에서 toodelete hello 서비스를 클릭 합니다.

    ![검색 서비스 toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. StorSimple 장치 관리자 서비스 블레이드 toohello 이동합니다. **삭제**를 클릭합니다.

    ![서비스 삭제](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. 클릭 **예** hello 알림이에 있습니다. 삭제 하는 hello 서비스 toobe 몇 분 정도 걸릴 수 있습니다.

    ![삭제 확인](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Hello 서비스 등록 키 가져오기

서비스를 성공적으로 만든 후 hello 서비스와 StorSimple 장치의 tooregister 필요 합니다. tooregister 첫 번째 StorSimple 장치의 서비스 등록 키 hello 필요 합니다. tooregister 기존 StorSimple 서비스와 장치를 추가할 필요가 hello 등록 키와 hello 서비스 데이터 암호화 키 (생성 된 hello 첫 번째 장치에 등록 하는 동안) 해야 합니다. Hello 서비스 데이터 암호화 키에 대 한 자세한 내용은 참조 [StorSimple 보안](storsimple-8000-security.md)합니다. 에 액세스 하 여 hello 등록 키를 받을 수 **키** StorSimple 장치 관리자 블레이드의 합니다.

Hello 단계 tooget hello 서비스 등록 키를 다음을 수행 합니다.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Hello 서비스 등록 키를 안전한 위치에 유지 합니다. 이 키를으로 hello 서비스 데이터 암호화 키를이 서비스를 사용 하 여 추가 장치 tooregister 필요 합니다. Hello 서비스 등록 키를 얻은 후 StorSimple 인터페이스에 대 한 hello Windows PowerShell을 통해 장치를 구성 해야 합니다.

방법에 대 한 자세한 내용은 toouse이 등록 키가 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.

## <a name="regenerate-hello-service-registration-key"></a>Hello 서비스 등록 키 다시 생성
필요한 tooperform 키 회전 또는 서비스 관리자 목록이 hello에 변경 되었는지 여부는 tooregenerate 서비스 등록 키가 필요 합니다. Hello 키를 다시 생성 하면 hello 새 키는 후속 장치를 등록 하는 중에 사용 됩니다. 이미 등록 된 hello 장치가이 프로세스에 의해 영향을 받지 않습니다.

Hello 단계 tooregenerate 서비스 등록 키가 다음을 수행 합니다.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 서비스 등록 키
1. Hello에 **StorSimple 장치 관리자** 블레이드에서 너무 이동**관리 &gt;**  **키**합니다.
    
    ![키 블레이드](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Hello에 **키** 블레이드에서 클릭 **다시 생성**합니다.

    ![다시 생성 클릭](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Hello에 **Regenerate 서비스 등록 키** 블레이드를 검토 hello 작업 때 필요한 hello 키 다시 생성 됩니다. 이 서비스에 등록 된 하는 모든 hello 후속 장치 hello 새 등록 키를 사용 합니다. 클릭 **다시 생성** tooconfirm 합니다. Hello 재생성 완료 되 면 알림이 표시 됩니다.

    ![다시 생성 확인](./media/storsimple-8000-manage-service/regenregkey4.png)

4. 새 서비스 등록 키가 나타납니다.

5. 이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.



## <a name="change-hello-service-data-encryption-key"></a>Hello 서비스 데이터 암호화 키 변경
서비스 데이터 암호화 키는 StorSimple 관리자 서비스 toohello StorSimple 장치에서 전송 된 저장소 계정 자격 증명과 같은 사용 되는 tooencrypt 고객 기밀 데이터입니다. 필요 합니다 toochange 이러한 키는 정기적으로 IT 조직 hello 저장 장치에 대 한 키 순환 정책을 경우. hello 키 변경 프로세스 수 약간 다를 수 있는지에 따라 장치를 하나 또는 여러 장치 hello StorSimple Manager 서비스에서 관리 합니다. 자세한 내용은 이동 너무[StorSimple 보안 및 데이터 보호](storsimple-8000-security.md)합니다.

Hello 서비스 데이터 암호화 키 변경 3 단계로 구성 됩니다.

1. Azure 리소스 관리자에 대 한 Windows PowerShell 스크립트를 사용 하는 장치 toochange hello 서비스 데이터 암호화 키 권한을 부여 합니다.
2. StorSimple 용 Windows PowerShell을 사용 하 여, hello 서비스 데이터 암호화 키 변경을 시작 합니다.
3. 하나 이상의 StorSimple 장치가 있는 경우 hello 서비스 데이터 암호화 키 hello에 다른 장치를 업데이트 합니다.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>1 단계: Windows PowerShell을 사용 하 여 스크립트 tooAuthorize 장치 toochange hello 서비스 데이터 암호화 키
일반적으로 장치 관리자에 게 서비스 관리자에 게 해당 장치 toochange 서비스 데이터 암호화 키 권한 부여를 요청 합니다. 서비스 관리자에 게 hello 장치 toochange hello 키를 승인 합니다.

이 단계는 hello Azure 리소스 관리자 기반 스크립트를 사용 하 여 수행 합니다. 서비스 관리자에 게 적합 toobe 권한이 있는 장치를 선택할 수 있습니다. hello 장치가 다음 권한이 있는 toostart hello 서비스 데이터 암호화 키 변경 프로세스입니다. 

너무 hello 스크립트를 사용 하는 방법에 대 한 자세한 내용을 보려면 이동[ServiceEncryptionRollover.ps1 권한 부여](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Toochange 서비스 데이터 암호화 키를 권한이 있는 장치 수 있습니까?
장치에 권한이 부여 된 tooinitiate 서비스 데이터 암호화 키 변경 되기 전 조건 다음 hello를 충족 해야 합니다.

* hello 장치 온라인 toobe 서비스 데이터 암호화 키 변경 권한 부여에 적합 해야 합니다.
* 같은 장치 다시 30 분 후 hello 키 변경 시작 되지 않았습니다 hello 권한을 부여할 수 있습니다.
* Hello 이전에 인증 된 장치에 의해 hello 키 변경 시작 되지 않았습니다는 다른 장치를 인증할 수 있습니다. Hello 새 장치에 권한이 부여 되 후 hello 이전 장치 hello 변경을 시작할 수 없습니다.
* Hello 서비스 데이터 암호화 키의 hello 롤오버가 진행 중인 동안에 장치를 인증할 수 없습니다.
* Hello 서비스에 등록 된 hello 장치 롤오버 않은 hello 암호화 되지 않은 다른 경우에 장치를 인증할 수 있습니다. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>2 단계: StorSimple tooinitiate hello 서비스 데이터 암호화 키 변경에 대 한 Windows PowerShell 사용
이 단계는 StorSimple 인터페이스 hello에 권한이 StorSimple 장치에 대 한 hello Windows PowerShell에서에서 수행 됩니다.

> [!NOTE]
> Hello 키 롤오버가 완료 될 때까지 어떤 작업도 hello StorSimple 관리자 서비스의 Azure 포털에서에서 수행할 수 있습니다.
> 
> 

Hello 장치 직렬 콘솔 tooconnect toohello Windows PowerShell 인터페이스를 사용 하는 경우 hello 다음 단계를 수행 합니다.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello 서비스 데이터 암호화 키 변경
1. 에 대 한 모든 권한을 toolog 옵션 1 선택 합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Hello cmdlet 성공적으로 완료 되 면 새 서비스 데이터 암호화 키를 받아볼 수 있습니다. 이 키를 복사하고 저장해 두었다가 이 프로세스의 3단계에서 사용합니다. 이 키는 tooupdate hello StorSimple Manager 서비스에 등록 된 장치에 남은 모든 hello를 사용 합니다.
   
   > [!NOTE]
   > 이 프로세스는 StorSimple 장치에 권한을 부여한 후 4시간 이내에 시작되어야 합니다.
   > 
   > 
   
   이 새 키는 toohello 푸시 toobe tooall hello 장치를 서비스 hello 서비스에 등록 된 전송 됩니다. Hello 서비스 대시보드에 경고가 표시 됩니다. hello 서비스는 hello 등록 된 장치에서 모든 hello 작업이 비활성화 됩니다 한 장치 관리자에 게는 다음 tooupdate hello 서비스 데이터 암호화 키 hello에 다른 장치 합니다. 그러나 hello (toohello 클라우드 데이터를 보내는 호스트) i/o가 중단 되지 않습니다.
   
   설정한 경우 단일 장치 등록 서비스 tooyour hello 롤오버 프로세스가 완료 되었으므로 이제 고 hello 다음 단계를 건너뛸 수 있습니다. 를 여러 장치 등록된 tooyour 서비스가 있는 경우에 3 toostep을 진행 합니다.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>3 단계: hello 다른 StorSimple 장치에서 서비스 데이터 암호화 키 업데이트
장치 등록된 tooyour StorSimple Manager 서비스를 여러 개 있는 경우 다음이 단계를 StorSimple 장치의 hello Windows PowerShell 인터페이스에서 수행 되어야 합니다. 2 단계에서에서 적어 둔 hello 키에 사용 되는 tooupdate hello StorSimple Manager 서비스에 등록 된 StorSimple 장치에 남은 모든 hello 이어야 합니다.

Hello 단계 tooupdate hello 서비스 데이터 암호화 장치에서 다음을 수행 합니다.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello 서비스 데이터 암호화 키
1. StorSimple tooconnect toohello 콘솔에 대 한 Windows PowerShell을 사용 합니다. 에 대 한 모든 권한을 toolog 옵션 1 선택 합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Hello 서비스 데이터 암호화 키에서 가져온 제공 [2 단계: StorSimple tooinitiate hello 서비스 데이터 암호화 키 변경에 대 한 Windows PowerShell을 사용 하 여](#to-initiate-the-service-data-encryption-key-change)합니다.


## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [StorSimple 배포 프로세스](storsimple-8000-deployment-walkthrough-u2.md)합니다.
* [StorSimple 저장소 계정 관리](storsimple-8000-manage-storage-accounts.md)에 대해 자세히 알아봅니다.
* 너무 방법에 대 한 자세한[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.
