---
title: "StorSimple 8000 시리즈 장치에 대 한 CHAP aaaConfigure | Microsoft Docs"
description: "StorSimple 장치에 tooconfigure Challenge Handshake 인증 프로토콜 CHAP () hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>StorSimple 장치에 대한 CHAP 구성

이 자습서에서는 tooconfigure StorSimple 장치에 대 한 CHAP 하는 방법을 설명 합니다. 이 문서에 자세히 설명 하는 hello 프로시저는 tooStorSimple 8000 시리즈 장치에 적용 됩니다.

CHAP는 Challenge Handshake Authentication Protocol의 약어입니다. 원격 클라이언트의 서버 toovalidate hello id에서 사용 하는 인증 체계 이며 hello 확인 공유 암호를 기반으로 합니다. CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다. 단방향 CHAP는 hello 대상은 초기자를 인증 하는 경우입니다. 상호 / 역방향 CHAP의 hello 대상 hello 초기자를 인증 한 hello 초기자 인증 hello 대상입니다. 대상 인증 없이 초기자 인증을 구현할 수 있습니다. 그러나 초기자 인증도 구현하는 경우 대상 인증을 구현할 수 있습니다.

모범 사례로, CHAP tooenhance iSCSI 보안을 사용 하는 것이 좋습니다.

> [!NOTE]
> IPSEC는 StorSimple 장치에서 현재 지원되지 않습니다.

다음 방법으로 hello에 hello StorSimple 장치에서 CHAP 설정은 hello를 구성할 수 있습니다.

* 단방향 또는 일방 인증
* 양방향 또는 상호 또는 역방향 인증

각각의이 경우 hello 장치와 hello 서버 iSCSI 초기자 소프트웨어에 대 한 hello 포털 구성 toobe 제공 되어야 합니다. hello이 구성에 대 한 자세한 단계는 hello 자습서에서 설명 합니다.

## <a name="unidirectional-or-one-way-authentication"></a>단방향 또는 일방 인증

단방향 인증 hello 대상 hello 초기자를 인증 합니다. 이 인증 하려면 hello StorSimple 장치와 hello iSCSI 초기자 소프트웨어 hello 호스트에서 hello CHAP 초기자 설정을 구성 해야 합니다. StorSimple 장치에 대 한 자세한 절차 hello 및 Windows 호스트는 다음과 같습니다.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure 단방향 인증을 위해 장치

1. Azure 포털 hello tooyour StorSimple 장치 관리자 서비스를 이동 합니다. 클릭 **장치** 선택 하 고 클릭 tooconfigure CHAP는 장치에 대 한 합니다. 너무 이동**장치 설정 > 보안**합니다. Hello에 **보안 설정** 블레이드에서 클릭 **CHAP**합니다.
   
    ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. Hello에 **CHAP** 블레이드 및 hello **CHAP 초기자** 섹션:
   
   1. CHAP 초기자에 대한 사용자 이름을 입력합니다.
   2. CHAP 초기자에 대한 암호를 입력합니다.
      
    > [!IMPORTANT]
    > hello CHAP 사용자 이름에 보다 적은 233 자 이어야 합니다. hello CHAP 암호는 12 ~ 16 자 사이 여야 합니다. 더 긴 사용자 이름이 나 암호가 hello Windows 호스트에서 인증 오류가 발생합니다.
   
   3. Hello 암호를 확인 합니다.

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. **Save**를 클릭합니다. 확인 메시지가 표시됩니다. 클릭 **확인** toosave hello 변경 합니다.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>Windows hello에서 tooconfigure 단방향 인증 서버를 호스트 합니다.
1. Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.
2. Hello에 **iSCSI 초기자 속성** 창의 hello 다음 단계를 수행 합니다.
   
   1. Hello 클릭 **검색** 탭 합니다.
      
       ![iSCSI 초기자 속성](./media/storsimple-configure-chap/IC740944.png)
   2. **포털 검색**을 클릭합니다.
3. Hello에 **대상 포털 검색** 대화 상자:
   
   1. 장치의 hello IP 주소를 지정 합니다.
   2. **고급**을 클릭합니다.
      
       ![대상 포털 검색](./media/storsimple-configure-chap/IC740945.png)
4. Hello에 **고급 설정** 대화 상자:
   
   1. 선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.
   2. Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.
   3. Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.
   4. **확인**을 클릭합니다.
      
       ![고급 설정 일반](./media/storsimple-configure-chap/IC740946.png)
5. Hello에 **대상** hello 탭 **iSCSI 초기자 속성** 창으로 hello 장치 상태를 표시 해야 **연결 됨**합니다. StorSimple 1200 장치를 사용하는 경우 각 볼륨은 iSCSI 대상으로 탑재됩니다. 따라서 3-4 단계 toobe 각 볼륨에 대해 반복 해야 합니다.
   
    ![별도 대상으로 탑재된 볼륨](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Hello iSCSI 이름을 변경 하면 새 iSCSI 세션에 대 한 hello 새 이름이 사용 됩니다. 새 설정은 로그오프하고 다시 로그온할 때까지 기존 세션에 대해 다시 사용되지 않습니다.

너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.

## <a name="bidirectional-or-mutual-authentication"></a>양방향 또는 상호 인증

양방향 인증에서는 hello 대상 hello 초기자를 인증 한 hello 초기자 인증 hello 대상입니다. 이 절차를 수행 하려면 hello 사용자 tooconfigure hello CHAP 초기자 설정을, hello 장치와 iSCSI 초기자 소프트웨어 hello 호스트에서 CHAP 설정을 반대로 합니다. hello 다음 절차에서는 설명 hello 단계 tooconfigure 상호 인증 hello Windows 호스트와 hello 장치에 있습니다.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure 상호 인증을 위해 장치

1. Azure 포털 hello tooyour StorSimple 장치 관리자 서비스를 이동 합니다. 클릭 **장치** 선택 하 고 클릭 tooconfigure CHAP는 장치에 대 한 합니다. 너무 이동**장치 설정 > 보안**합니다. Hello에 **보안 설정** 블레이드에서 클릭 **CHAP**합니다.
   
    ![CHAP 대상](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. Hello 및이 페이지에서 아래로 스크롤하여 **CHAP 대상** 섹션:
   
   1. 장치에 대한 **역방향 CHAP 사용자 이름** 을 입력합니다.
   2. 장치에 대한 **역방향 CHAP 암호** 를 입력합니다.
   3. Hello 암호를 확인 합니다.
3. Hello에 **CHAP 초기자** 섹션:
   
   1. 장치에 대한 **사용자 이름** 을 입력합니다.
   2. 장치에 대한 **암호** 를 입력합니다.
   3. Hello 암호를 확인 합니다.

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. **Save**를 클릭합니다. 확인 메시지가 표시됩니다. 클릭 **확인** toosave hello 변경 합니다.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>Windows hello에서 tooconfigure 양방향 인증 서버를 호스트 합니다.

1. Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.
2. Hello에 **iSCSI 초기자 속성** 창의 hello 클릭 **구성** 탭 합니다.
3. **CHAP**를 클릭합니다.
4. Hello에 **iSCSI 초기자 상호 CHAP 암호** 대화 상자:
   
   1. 형식 hello **역방향 CHAP 암호** hello Azure 포털에에서 구성 합니다.
   2. **확인**을 클릭합니다.
      
       ![iSCSI 초기자 상호 CHAP 암호](./media/storsimple-configure-chap/IC740949.png)
5. Hello 클릭 **대상** 탭 합니다.
6. Hello 클릭 **연결** 단추입니다. 
7. Hello에 **tooTarget 연결** 대화 상자를 클릭 **고급**합니다.
8. Hello에 **고급 속성** 대화 상자:
   
   1. 선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.
   2. Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.
   3. Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.
   4. 선택 hello **상호 인증 수행** 확인란 합니다.
      
       ![고급 설정 상호 인증](./media/storsimple-configure-chap/IC740950.png)
   5. 클릭 **확인** toocomplete hello CHAP 구성

너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.

## <a name="additional-considerations"></a>추가 고려 사항

hello **빠른 연결** 기능은 CHAP를 사용할 수 있는 연결을 지원 하지 않습니다. CHAP를 사용 하는 hello를 사용 하는지 확인 **연결** hello에서 사용할 수 있는 단추 **대상** 탭 tooconnect tooa 대상입니다.

![Tootarget 연결](./media/storsimple-configure-chap/IC740947.png)

Hello에 **tooTarget 연결** 대화 상자는 선택에 나타난 hello **즐겨 찾는 대상의 연결 toohello 목록이 추가** 확인란 합니다. 이 옵션을이 선택 하 hello 컴퓨터를 다시 시작 될 때마다 하려고 toorestore hello 연결 toohello iSCSI 즐겨찾기 대상 되도록 합니다.

## <a name="errors-during-configuration"></a>구성 중 오류

CHAP 구성이 올바르지 않을 경우 가능성이 toosee 됩니다는 **인증 실패** 오류 메시지입니다.

## <a name="verification-of-chap-configuration"></a>CHAP 구성 확인

CHAP hello 다음 단계를 완료 하 여 사용 되 고 있는지 확인할 수 있습니다.

#### <a name="tooverify-your-chap-configuration"></a>tooverify CHAP 구성
1. **즐겨찾는 대상**을 클릭합니다.
2. 인증 사용 하도록 설정한 hello 대상을 선택 합니다.
3. **세부 정보**를 클릭합니다.
   
    ![iSCSI 초기자 속성 즐겨찾는 대상](./media/storsimple-configure-chap/IC740951.png)
4. Hello에 **즐겨 찾는 대상 세부 정보** 대화 상자, hello에 메모 hello 항목 **인증** 필드입니다. 경우 hello 구성에 성공 했는지를 필드 **CHAP**합니다.
   
    ![즐겨찾는 대상 세부 정보](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>다음 단계

* [StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

