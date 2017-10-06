---
title: "StorSimple 장치에 대 한 웹 프록시를 aaaSet | Microsoft Docs"
description: "자세한 방법을 tooconfigure StorSimple에 대 한 Windows PowerShell toouse 웹 StorSimple 장치에 대 한 프록시 설정 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>StorSimple 장치에 대한 웹 프록시 구성
## <a name="overview"></a>개요
이 자습서에서는 설명 방법을 뷰와 tooconfigure StorSimple 용 Windows PowerShell toouse 웹 StorSimple 장치에 대 한 프록시 설정 합니다. hello 웹 프록시 설정은 hello 클라우드와 통신할 때 hello StorSimple 장치에서 사용 됩니다. 웹 프록시 서버는 사용 되는 tooadd 다른 보안 계층 콘텐츠 필터링, tooease 대역폭 요구 사항이 캐시 또는 분석에도 도움이 됩니다.

웹 프록시는 StorSimple 장치에 대한 선택적 구성입니다. StorSimple용 Windows PowerShell을 통해서만 웹 프록시를 구성할 수 있습니다. hello 구성 과정은 다음과 같습니다.

1. 먼저 StorSimple cmdlet에 대 한 hello 설치 마법사 또는 Windows PowerShell을 통해 웹 프록시 설정을 구성 합니다.
2. 그런 다음 StorSimple cmdlet에 대 한 Windows PowerShell을 통해 되는 구성 하는 hello 웹 프록시 설정을 활성화.

Hello 웹 프록시 구성을 완료 되 면 StorSimple에 대 한 웹 프록시 설정을 구성 하는 hello hello Microsoft Azure StorSimple Manager 서비스와 Windows PowerShell hello 모두에서 볼 수 있습니다. 

이 자습서를 읽은 후에 다음을 수행할 수 있습니다.

* 설치 마법사 및 cmdlet을 사용하여 웹 프록시 구성
* Cmdlet을 사용하여 웹 프록시 활성화
* Hello Azure 클래식 포털에서에서 웹 프록시 설정 보기
* 웹 프록시 구성하는 동안 오류 해결

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell을 통해 웹 프록시 구성
Hello tooconfigure 웹 프록시 설정을 다음 중 하나를 사용 합니다.

* 설치 마법사 tooguide hello 구성 단계를 안내 합니다.
* StorSimple용 Windows PowerShell에서 Cmdlet

이러한 각 방법의 hello 다음 섹션에서에서 설명 합니다.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Hello 설치 마법사를 통해 웹 프록시 구성
웹 프록시 구성에 대 한 hello 설치 마법사 tooguide hello 통해 단계를 사용할 수 있습니다. Hello 단계 tooconfigure 웹 프록시 장치에서 다음을 수행 합니다.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>hello 설치 마법사를 통해 tooconfigure 웹 프록시
1. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인** hello 설명과 **장치 관리자 암호**합니다. 형식 hello 다음 설치 마법사 세션 toostart를 명령 수 있습니다.
   
    `Invoke-HcsSetupWizard`
2. 장치 등록에 대 한 hello 설치 마법사를 사용 하는 처음으로 hello 이것이 할 경우 tooconfigure 모든 hello 필요한 네트워크 설정을 hello 웹 프록시 구성에 도달할 때까지 합니다. 이미 장치에 등록 하는 경우에 hello 웹 프록시 구성에 도달할 때까지 모든 hello 구성 된 네트워크 설정을 허용할 수 있습니다. Hello 설치 마법사에서 입력 정보 요청된 tooconfigure 웹 프록시 설정 때 입력 **예**합니다.
3. Hello에 대 한 **웹 프록시 URL**, hello IP 주소를 지정 또는 웹 프록시 서버와 hello TCP 포트 번호의 싶다는 의사를 장치 toouse hello 클라우드와 통신할 때 정규화 된 도메인 이름 (FQDN)을 환영 합니다. 형식에 따라 hello를 사용 합니다.
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    기본적으로 TCP 포트 번호 8080가 지정됩니다.
4. Hello 인증 유형을 선택 **NTLM**, **기본**, 또는 **None**합니다. Basic은 hello hello 프록시 서버 구성에 대 한 보안 수준이 가장 낮은 인증입니다. NT LAN Manager (NTLM)은 3 방향 메시징 시스템 (4 추가 무결성이 필요한 경우)을 사용 하는 매우 안전 하 고 복잡 한 인증 프로토콜 tooauthenticate 사용자입니다. hello 기본 인증이 NTLM입니다. 자세한 내용은 [기본](http://hc.apache.org/httpclient-3.x/authentication.html) 및 [NTLM 인증](http://hc.apache.org/httpclient-3.x/authentication.html)을 참조하세요. 
   
   > [!IMPORTANT]
   > **StorSimple Manager 서비스 hello, 기본 hello 장치 모니터링 차트가 작동 하지 않습니다 또는 hello 장치에 대 한 hello 프록시 서버 구성에서 NTLM 인증을 사용 합니다. 모니터링 차트 toowork hello에 대 한 해야 tooensure 인증 tooNONE을 설정 합니다.**
   > 
   > 
5. 인증을 사용하면 **웹 프록시 사용자 이름** 및 **웹 프록시 암호**를 제공합니다. 또한 tooconfirm hello 암호가 필요 합니다.
   
    ![StorSimple 장치1에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751830.png)

처음으로 hello에 대 한 장치를 등록 하는, hello 등록 계속 진행 합니다. 장치가 이미 등록 된 경우 hello 마법사 종료 됩니다. hello 구성 설정이 저장 됩니다.

웹 프록시를 사용할 수 있습니다. Hello를 건너뛸 수 [웹 프록시를 사용 하려는](#enable-web-proxy) 단계를 너무 직접 이동[hello Azure 클래식 포털에서에서 웹 프록시 설정 보기](#view-web-proxy-settings-in-the-azure-classic-portal)합니다.

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>StorSimple cmdlet용 Windows PowerShell을 통해 웹 프록시 구성
다른 방법 tooconfigure 웹 프록시 설정을 통해 Windows PowerShell for StorSimple cmdlet hello입니다. Hello 단계 tooconfigure 웹 프록시를 다음을 수행 합니다.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>cmdlet 통해 tooconfigure 웹 프록시
1. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. 메시지가 표시 되 면 제공 hello **장치 관리자 암호**합니다. hello 기본 암호는 `Password1`합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    입력 하 고 아래와 같이 메시지가 표시 되 면 hello 암호를 확인 합니다.
   
    ![StorSimple 장치3에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751831.png)

hello 웹 프록시는 이제 구성 및 toobe 사용 하도록 설정 해야 합니다.

## <a name="enable-web-proxy"></a>웹 프록시 활성화
웹 프록시는 기본적으로 사용하지 않도록 설정되어 있습니다. StorSimple 장치에서 hello 웹 프록시 설정을 구성한 후 Windows PowerShell toouse hello StorSimple tooenable hello 웹 프록시 설정이 필요 합니다.

> [!NOTE]
> **이 단계 hello 설치 마법사 tooconfigure 웹 프록시를 사용 하는 경우 필요한 되지 않습니다. 웹 프록시는 설치 마법사 세션 후 기본적으로 자동으로 사용하도록 설정됩니다.**
> 
> 

장치에서 StorSimple tooenable 웹 프록시에 대 한 Windows PowerShell에서 단계를 수행 하는 hello를 수행 합니다.

#### <a name="tooenable-web-proxy"></a>tooenable 웹 프록시
1. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. 메시지가 표시 되 면 제공 hello **장치 관리자 암호**합니다. hello 기본 암호는 `Password1`합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Enable-HcsWebProxy`
   
    StorSimple 장치에서 이제 hello 웹 프록시 구성을 설정한 합니다.
   
    ![StorSimple 장치4에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 웹 프록시 설정 보기
hello 웹 프록시 설정이 hello Windows PowerShell 인터페이스를 통해 구성 및 hello 클래식 포털 내에서 변경할 수 없습니다. 그러나 hello 클래식 포털에서 이러한 구성된 설정은 볼 수, 있습니다. Hello 단계 tooview 웹 프록시를 다음을 수행 합니다.

#### <a name="tooview-web-proxy-settings"></a>tooview 웹 프록시 설정
1. 너무 이동**StorSimple Manager 서비스 > 장치**합니다. 선택 하 고 장치를 클릭 하 고 이동 하 여 너무**구성**합니다.
2. Hello에서 아래로 스크롤하여 **구성** 너무 페이지**웹 프록시 설정** 섹션. 아래와 같이 hello 구성 된 웹 프록시 설정이 StorSimple 장치에서 볼 수 있습니다.
   
    ![관리 포털에서 웹 프록시 보기](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>웹 프록시 구성하는 동안 오류
Hello 웹 프록시 설정이 제대로 구성 되어 있는, 오류 메시지 StorSimple 용 Windows PowerShell에 표시 된 toohello 사용자 됩니다. 다음 표에서 hello 이러한 오류 메시지, 가능한 원인 및 권장 되는 작업 중 일부를 설명 합니다.

| 일련 번호 | HRESULT 오류 코드 | 가능한 근본 원인 | 권장 작업 |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Hello 수동 컨트롤러에서 명령을 실행 하 고 hello 활성 컨트롤러와 수 toocommunicate 않습니다. |Hello 활성 컨트롤러에서 hello 명령을 실행 합니다. hello 수동 컨트롤러에서 toorun hello 명령을 tooactive 수동 컨트롤러에서 toofix hello 연결을 해야 합니다. 이 연결이 끊어진 경우 tooengage Microsoft 지원 해야 합니다. |
| 2. |0x800710dd-작업 식별자 hello 잘못 되었습니다. |프록시 설정은 StorSimple 가상 장치에서 지원되지 않습니다. |프록시 설정은 StorSimple 가상 장치에서 지원되지 않습니다. 물리적 StorSimple 장치에만 구성할 수 있습니다. |
| 3. |0x80070057 - 잘못된 매개 변수 |Hello 프록시 설정에 대해 제공 된 hello 매개 변수 중 하나가 올바르지 않습니다. |hello URI 형식이 잘못 된 제공 되지 않습니다. 형식에 따라 hello를 사용 합니다.`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - RPC 서버를 사용할 수 없음 |hello 근본 원인을 hello 다음 중 하나입니다.</br></br>클러스터가 켜지지 않았습니다.</br></br>데이터 경로 서비스가 실행되고 있지 않습니다.</br></br>수동 컨트롤러에서 hello 명령을 실행 이므로 hello 활성 컨트롤러와 수 toocommunicate 합니다. |하십시오 hello 클러스터는 Microsoft 지원 tooensure 참여 작동 중 이며 데이터 경로 서비스가 실행 되 고 있습니다.</br></br>Hello 활성 컨트롤러에서 hello 명령을 실행 합니다. Tooensure 할 hello 수동 컨트롤러에서 toorun hello 명령을 원하는 경우 hello 수동 컨트롤러가 hello 활성 컨트롤러와 통신할 수 있습니다. 이 연결이 끊어진 경우 tooengage Microsoft 지원 해야 합니다. |
| 5. |0x800706be - RPC 호출 실패 |클러스터의 작동이 중단되었습니다. |클러스터 hello tooensure 중일 Microsoft 지원에 문의 합니다. |
| 6. |0x8007138f - 클러스터 리소스를 찾을 수 없음 |플랫폼 서비스 클러스터 리소스를 찾을 수 없습니다. 이 hello 설치가 적절 하지 않은 경우 발생할 수 있습니다. |장치에서 공장 재설정 tooperform을 할 수 있습니다. Toocreate 플랫폼 리소스를 할 수 있습니다. 다음 단계는 Microsoft 지원에 문의하세요. |
| 7. |0x8007138c - 클러스터 리소스는 온라인 상태가 아님 |플랫폼 또는 데이터 경로 클러스터 리소스는 온라인 상태가 아닙니다. |하십시오 연락처 Microsoft 지원 toohelp hello 데이터 경로 및 플랫폼 서비스 리소스가 온라인 상태 인지 확인 합니다. |

> [!NOTE]
> * 오류 메시지 목록은 위에 hello 완전 하지 않습니다. 
> * 오류 관련된 tooweb 프록시 설정은 hello StorSimple Manager 서비스에서 Azure 클래식 포털에에서 나타나지 않습니다. Hello 구성이 완료 되 면 웹 프록시에 문제가 경우 hello 장치 상태 너무 변경**오프 라인** hello 클래식 포털의. |
> 
> 

## <a name="next-steps"></a>다음 단계
* 장치 배포 또는 웹 프록시 설정을 구성 하는 동안에 문제가 발생 하는 경우 참조 너무[StorSimple 장치 배포 문제를 해결](storsimple-troubleshoot-deployment.md)합니다.
* StorSimple Manager 서비스 toouse hello 너무 이동 toolearn[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

