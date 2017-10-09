---
title: "파일 서버와 StorSimple 가상 배열을 aaaSet | Microsoft Docs"
description: "StorSimple 가상 배열 배포에서이 세 번째 자습서 파일 서버로 가상 장치를 tooset에 지시합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>StorSimple 가상 배열 배포 - Azure Portal을 통해 파일 서버로 설정
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>소개
이 문서에서는 어떻게 tooperform 초기 설정을 완료 hello 장치 설치 StorSimple 파일 서버를 등록 하 고 만들고 연결 tooSMB 공유를 설명 합니다. 이 hello 마지막의 문서를 hello 일련의 필요한 배포 자습서 toocompletely 파일 서버 또는 iSCSI 서버로 가상 배열을 배포 합니다.

hello 설치 및 구성 프로세스는 약 10 분 toocomplete를 걸릴 수 있습니다. 이 문서의 정보 hello hello StorSimple 가상 배열 toohello 배포만을 적용 됩니다. StorSimple 8000 시리즈 장치와의 hello 배포용으로 이동: [업데이트 2를 실행 하 여 StorSimple 8000 시리즈 장치 배포](storsimple-deployment-walkthrough-u2.md)합니다.

## <a name="setup-prerequisites"></a>설정 필수 조건
StorSimple 가상 배열을 구성하고 설정하기 전에 다음 사항을 확인합니다.

* 가상 배열 및 연결 된 tooit에 설명된 된 hello로 프로 비전 [Hyper-v에서 사용 되는 StorSimple 가상 배열 프로 비전](storsimple-virtual-array-deploy2-provision-hyperv.md) 또는 [VMware에서 StorSimple 가상 배열 프로 비전](storsimple-virtual-array-deploy2-provision-vmware.md)합니다.
* Toomanage StorSimple 가상 배열 하 여 만든 hello StorSimple 장치 관리자 서비스에서 hello 서비스 등록 키를 있습니다. 자세한 내용은 참조 [2 단계: Get hello 서비스 등록 키](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) StorSimple 가상 배열에 대 한 합니다.
* Hello 두 번째 또는 그 가상 배열 기존 StorSimple 장치 관리자 서비스를 사용 하 여 등록 된 경우에 hello 서비스 데이터 암호화 키가 있어야 합니다. 첫 번째 장치 hello가이 서비스와 성공적으로 등록 될 때이 키가 생성 되었습니다. 이 키를 잃어버린 경우 참조 [Get hello 서비스 데이터 암호화 키](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) StorSimple 가상 배열에 대 한 합니다.

## <a name="step-by-step-setup"></a>단계별 설정
단계별 지침은 tooset 이후의 hello를 사용 하 고 StorSimple 가상 배열을 구성 합니다.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>1 단계: hello 로컬 웹 UI 설치를 완료 하 고 장치 등록
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete 설치 hello 및 hello 장치 등록
1. 브라우저 창을 열고 toohello 로컬 웹 UI를 연결 합니다. 형식:
   
   `https://<ip-address of network interface>`
   
   Hello 이전 단계에서 설명 하는 hello 연결 URL을 사용 합니다. Hello 웹 사이트의 보안 인증서에 문제가 있음을 나타내는 오류가 표시 됩니다. 클릭 **toothis 웹 페이지를 계속**합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Toohello 로그인 웹 UI로 가상 배열 **StorSimpleAdmin**합니다. 3 단계에서에서 사용자가 변경한 hello 장치 관리자 암호를 입력: 시작 hello 가상 배열에서 [Hyper-v에서 사용 되는 StorSimple 가상 배열 프로 비전](storsimple-virtual-array-deploy2-provision-hyperv.md) 또는 [VMware에서 StorSimple 가상 배열 프로 비전](storsimple-virtual-array-deploy2-provision-vmware.md)합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Toohello 취해집니다 **홈** 페이지. 이 페이지에서는 hello tooconfigure와 레지스터 hello hello StorSimple 장치 관리자 서비스와 가상 배열 다양 한 설정이 필요 합니다. hello **네트워크 설정**, **웹 프록시 설정**, 및 **시간 설정** 는 선택 사항입니다. 필요한 설정은 hello **장치 설정** 및 **클라우드 설정**합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. Hello에 **네트워크 설정** 페이지 **네트워크 인터페이스**, 데이터 0을 자동으로 구성 됩니다. 각 네트워크 인터페이스 기본 tooget IP 주소로 자동으로 설정 됩니다 (DHCP). 따라서 IP 주소, 서브넷 및 게이트웨이가 자동으로 할당됩니다(IPv4 및 IPv6 모두에 대해).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Hello hello 장치의 프로 비전 중 둘 이상의 네트워크 인터페이스를 추가한 경우에 여기 구성할 수 있습니다. 네트워크 인터페이스를 IPv4로만 구성하거나 IPv4와 IPv6 둘 다로 구성할 수 있습니다. IPv6 전용 구성은 지원되지 않습니다.
5. 장치는 클라우드 저장소 서비스 공급자 또는 tooresolve toocommunicate 장치를 시도할 때 파일 서버를 구성 하는 경우 이름으로 사용 되므로 DNS 서버가 필요 합니다. Hello에 **네트워크 설정** hello 페이지 **DNS 서버**:
   
   1. 기본 및 보조 DNS 서버는 자동으로 구성됩니다. Tooconfigure 고정 IP 주소를 선택한 경우에 DNS 서버를 지정할 수 있습니다. 고가용성을 위해 기본 및 보조 DNS 서버를 구성하는 것이 좋습니다.
   2. 클릭 **적용** tooapply hello 네트워크 설정의 유효성을 검사 합니다.
6. Hello에 **장치 설정** 페이지:
   
   1. 고유한 할당 **이름** tooyour 장치입니다. 이름에는 1-15자를 사용할 수 있으며 문자, 숫자 및 하이픈을 포함할 수 있습니다.
   2. Hello 클릭 **파일 서버** 아이콘 ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) hello에 대 한 **형식** 만들고 있는 장치입니다. 파일 서버 공유 toocreate 폴더 수 있습니다.
   3. 장치는 파일 서버에 그대로 toojoin hello 장치 tooa 도메인이 필요 합니다. **도메인 이름**을 입력합니다.
   4. **Apply**를 클릭합니다.
7. 대화 상자가 표시됩니다. 지정 된 형식의 hello 도메인 자격 증명을 입력 합니다. Hello 확인 아이콘을 클릭 합니다. hello 도메인 자격 증명 확인 됩니다. Hello 자격 증명이 올바르지 않을 경우 오류 메시지가 표시 됩니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. **Apply**를 클릭합니다. 적용 되 고 hello 장치 설정의 유효성을 검사 합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Active Directory에 대 한 자체 OU (조직 단위)가 가상 배열 및 그룹 정책 개체 (GPO) 적용된 tooit 되거나 상속 되는 확인 합니다. 그룹 정책 hello StorSimple 가상 배열에서 바이러스 백신 소프트웨어 등의 응용 프로그램을 설치할 수 있습니다. 추가 소프트웨어를 설치할은 지원 되지 않으며 toodata 손상 될 수 있습니다. 
   > 
   > 
9. 선택적으로 웹 프록시 서버를 구성합니다. 웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   Hello에 **웹 프록시** 페이지:
   
   1. 공급 hello **웹 프록시 URL** 형식에서: *http://&lt;호스트 IP 주소 또는 FDQN&gt;: 포트 번호*합니다. HTTPS URL은 지원되지 않습니다.
   2. **인증**은 **기본** 또는 **없음**으로 지정합니다.
   3. 인증을 사용 하는 또한 경우 tooprovide는 **Username** 및 **암호**합니다.
   4. **Apply**를 클릭합니다. 유효성 검사 되 고 구성 하는 hello 웹 프록시 설정을 적용 합니다.
10. 표준 시간대 등 장치에 대 한 hello 시간 설정을 구성 하 고 기본 및 보조 NTP 서버 hello (선택 사항). 클라우드 서비스 공급자와 인증할 수 있도록 장치 시간을 동기화해야 하기 때문에 NTP 서버가 필요합니다.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    Hello에 **시간 설정** 페이지:
    
    1. Hello 드롭다운 목록에서 선택 hello **시간대** hello 지리적 위치 장치 배포 되 고 있는 hello에 기반 합니다. 장치에 대 한 hello 기본 표준 시간대 PST입니다. 장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.
    2. 지정 된 **주 NTP 서버** 장치에 대 한 하거나 time.windows.com의 hello 기본값을 적용 합니다. 네트워크 사용자 데이터 센터 toohello 인터넷에서에서 NTP 트래픽이 toopass 허용 되는지 확인 합니다.
    3. 선택적으로 장치에 대한 **보조 NTP 서버**를 지정합니다.
    4. **Apply**를 클릭합니다. 유효성 검사 되 고 구성 하는 hello 시간 설정을 적용 합니다.
11. 장치에 대 한 hello 클라우드 설정을 구성 합니다. 이 단계에서는 hello 로컬 장치 구성을 완료 한 후 StorSimple 장치 관리자 서비스와 hello 장치를 등록 합니다.
    
    1. Hello 입력 **서비스 등록 키** 가져온 [2 단계: Get hello 서비스 등록 키](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) StorSimple 가상 배열에 대 한 합니다.
    2. 이 서비스를 등록 하면 첫 번째 장치 이면 나타납니다 hello로 **서비스 데이터 암호화 키**합니다. 이 키를 복사하고 안전한 위치에 저장합니다. 이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple 장치 관리자 서비스 hello 필요 합니다. 
       
       이 서비스에 등록 하는 첫 번째 장치의 hello 없는 경우에 tooprovide hello 서비스 데이터 암호화 키를 해야 합니다. 자세한 내용은 참조 tooget hello [서비스 데이터 암호화 키](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 에 로컬 웹 UI입니다.
    3. **Register**를 클릭합니다. Hello 장치 다시 시작 됩니다. Hello 장치를 등록 하기 전에 2-3 분 동안 toowait을 할 수 있습니다. Hello 장치를 다시 시작한 후 이동 됩니다 toohello 로그인 페이지에 있습니다.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Azure 포털 toohello를 반환 합니다. 너무 이동**모든 리소스**, StorSimple 장치 관리자 서비스를 검색 합니다.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. 필터링 하는 hello 나열, StorSimple 장치 관리자 서비스를 선택 하 고 다음 너무 탐색**관리 > 장치**합니다. Hello에 **장치** 블레이드에서 hello 장치 toohello 서비스 연결 되어 있으며 hello 상태 확인 **를 tooset 준비**합니다.
    
    ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>2 단계: 파일 서버로 hello 장치 구성
Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/) toocomplete hello 필수 장치 설정 합니다.

#### <a name="tooconfigure-hello-device-as-file-server"></a>파일 서버와 tooconfigure hello 장치
1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 이동 하 여 너무 **관리 > 장치**합니다. Hello에 **장치** 블레이드, 방금 만든 선택 hello 장치입니다. 이 장치도 표시 됩니다 **를 tooset 준비**합니다.
   
   ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. 클릭 하 여 hello 장치의 hello 장치 준비 toosetup 인지 나타내는 배너 메시지가 표시 됩니다.
   
    ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. 클릭 **구성** hello 명령 모음에서 합니다. Hello를 열어서이 **구성** 블레이드입니다. Hello에 **구성** 블레이드에서 다음 hello지 않습니다.
   
    1. hello 파일 서버 이름은 자동으로 채워집니다.
    
    2. Hello 클라우드 저장소 암호화 너무 설정 되어 있는지 확인**Enabled**합니다. 모든 hello 전송 된 데이터를 toohello 클라우드 암호화. 
    
    3. 256 비트 AES 키 암호화에 대 한 hello 사용자 정의 키로 사용 됩니다. 32 자 키를 지정 하 고 다음 키 tooconfirm hello를 다시 입력 것입니다. 키 관리 응용 프로그램의 hello 키 레코드를 나중에 참조할 수입니다.
    
    4. 클릭 **필요한 설정 구성** toospecify 저장소 계정 자격 증명을 toobe 장치와 함께 사용 합니다. 구성된 저장소 계정 자격 증명이 없는 경우 **새로 추가**를 클릭합니다. **저장소 계정을 사용 하 든 hello 블록 blob을 지원 하는지 확인 합니다. 페이지 Blob은 지원되지 않습니다.** [블록 Blob 및 페이지 Blob에 대한](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 자세한 내용입니다.
   
    ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. Hello에 **저장소 계정 자격 증명 추가** 블레이드에서 다음 hello지 않습니다: 

    1. 저장소 계정이 hello hello에 경우 현재 구독을 선택 hello 서비스와 같은 구독 합니다. 다른 하나는 hello 저장소 지정 hello 서비스 구독 외부 계정이 됩니다. 
    
    2. Hello 드롭다운 목록에서 기존 저장소 계정을 선택 합니다. 
    
    3. hello 위치는 자동으로 채움 hello 지정에 따라 저장소 계정입니다. 
    
    4. SSL tooensure hello 장치와 hello 클라우드 간의 네트워크 보안 통신 채널을 사용 하도록 설정 합니다.
    
    5. 클릭 **추가** tooadd이이 저장소 계정 자격 증명입니다. 
   
        ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Hello 저장소 계정 자격 증명을 성공적으로 만들어지면 hello **구성** 블레이드 업데이트할지 toodisplay hello 저장소 계정 자격 증명을 지정 합니다. **Configure**를 클릭합니다.
   
   ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   만들어진 파일 서버가 표시됩니다. Hello 파일 서버를 성공적으로 만들어지면 알려 줍니다.
   
   ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   hello 장치 상태를 바뀌고 너무**온라인**합니다.
   
   ![파일 서버 구성](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   공유 tooadd를 진행할 수 있습니다.

## <a name="step-3-add-a-share"></a>3단계: 공유 추가
Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/) toocreate를 공유 합니다.

#### <a name="toocreate-a-share"></a>toocreate 공유
1. Hello 앞 단계에서에서 구성한 hello 파일 서버 장치를 선택 하 고 클릭 **중...**  (또는 마우스 오른쪽 단추로 클릭). Hello 상황에 맞는 메뉴에서 선택 **추가 공유**합니다. 클릭 수 있습니다 **공유 추가 +** hello 장치 명령 모음에서 합니다.
   
   ![공유 추가](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. 공유 설정에 따라 hello를 지정 합니다.

    1. 공유에 대한 고유 이름입니다. hello 이름에는 3 too127 문자를 포함 하는 문자열 이어야 합니다.
    
    2. 선택적 **설명** hello 공유에 대 한 합니다. hello 설명 hello 공유 소유자를 식별 하는 데 도움이 됩니다.
    
    3. A **형식** hello 공유에 대 한 합니다. hello 유형은 가능 **계층화 됨** 또는 **로컬로 고정**, 계층 구성 되 고 기본 hello 합니다. 로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 공유를 선택합니다. 다른 모든 데이터에 대해서는 **계층화됨** 공유를 선택합니다.
    로컬로 고정 된 공유 씩 프로 비전 하 고 hello hello 공유에 기본 데이터를 로컬 toohello 장치 상태를 유지 하 고 toohello 클라우드를 분산 하지 않습니다. 계층화 된 공유 hello에 다른 손 씬 프로 비전 합니다. 계층화 된 공유를 만들 때 hello 공간이 10% 남았을 hello 로컬 계층에서 프로 비전 하 고 hello 공간을 90 %hello 클라우드 프로 비전 됩니다. 예를 들어, 1 t B 볼륨을 프로 비전, 100GB hello 로컬 공간에 있게 및 900GB hello 클라우드에서 사용할 수 있도록 하는 경우 데이터 계층이 때 hello 합니다. 차례로 hello 장치에서 모든 hello 로컬 공간이 부족 하면 계층화 된 공유 프로비저닝할 수 없습니다 것을 의미 합니다.
   
    4. Hello에 **기본 대 한 모든 권한을 설정할** 필드, hello 권한 toohello 사용자 또는이 공유에 액세스 하는 hello 그룹을 할당 합니다. Hello 사용자 또는 사용자 그룹에 hello의 hello 이름을 지정  *john@contoso.com*  형식입니다. 사용 하는 사용자 그룹 (단일 사용자)가 아니라 tooallow admin 권한이 tooaccess 이러한 공유 하는 것이 좋습니다. Hello 권한을 여기에 할당 한 후 파일 탐색기 toomodify를 이러한 사용 권한은 다음 사용할 수 있습니다.
   
    5. 클릭 **추가** toocreate hello 공유 합니다. 
    
        ![공유 추가](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        진행 중인 hello 공유 만들기 알림이 표시 됩니다.
   
        ![공유 추가](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Hello로 hello 공유를 만든 후 지정 된 설정을 hello **공유** 블레이드 tooreflect hello 새 공유를 업데이트 합니다. 기본적으로 모니터링 및 백업 hello 공유에 대 한 활성화 됩니다.
   
    ![공유 추가](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>4 단계: 연결 toohello 공유
이제 tooconnect tooone 또는 hello 이전 단계에서 만든 공유를 더 필요 합니다. Windows Server 연결 호스트 tooyour StorSimple 가상 배열에서 이러한 단계를 수행 합니다.

#### <a name="tooconnect-toohello-share"></a>tooconnect toohello 공유
1. 키를 눌러 ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) R. + Hello 실행 창에서 지정 hello *&#92; &#92;&lt; 파일 서버 이름&gt;*  hello 경로로 대체 *파일 서버 이름* hello 장치와 해당 하면 할당 된 tooyour 파일 서버 이름을 지정 합니다. **확인**을 클릭합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. 그러면 파일 탐색기가 열립니다. 이제 폴더에 만든 수 toosee hello 공유 됩니다. 선택한 공유 (폴더) tooview hello 콘텐츠를 두 번 클릭 합니다.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. 이제 파일 toothese 공유를 추가 하 고로 백업할 수 있습니다.

## <a name="next-steps"></a>다음 단계
어떻게 toouse hello 로컬 웹 UI 너무 자세한[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.

