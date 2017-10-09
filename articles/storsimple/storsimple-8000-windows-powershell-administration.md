---
title: "StorSimple 장치 관리를 위한 aaaPowerShell | Microsoft Docs"
description: "자세한 내용은 방법 toomanage StorSimple에 대 한 Windows PowerShell toouse StorSimple 장치입니다."
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
ms.date: 04/03/2017
ms.author: alkohli@microsoft.com
ms.openlocfilehash: e9e4bd025933cdef68b861d93749a107d1689536
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>장치를 StorSimple tooadminister에 대 한 Windows PowerShell 사용

## <a name="overview"></a>개요

StorSimple 용 Windows PowerShell 명령줄 인터페이스를 제공 합니다. 사용할 수 있는 toomanage Microsoft Azure StorSimple 장치입니다. Hello 이름에서 알 수 있듯이 제한 된 runspace에 기본 제공 되는 Windows PowerShell 기반 명령줄 인터페이스입니다. Hello hello 명령줄에서 hello 사용자의 관점에서 제한 된 runspace는 Windows PowerShell의 제한 된 버전으로 표시 됩니다. 이 인터페이스는 Windows PowerShell의 hello 기본 기능 중 일부를 유지 하면서 Microsoft Azure StorSimple 장치 관리에 맞춰진 추가 전용된 cmdlet에 있습니다.

이 문서 toothis 인터페이스를 연결 하는 방법을 포함 하 여 StorSimple 기능에 대 한 hello Windows PowerShell에 설명 하 고 링크 단계별 toostep 프로시저나이 인터페이스를 사용 하 여 수행할 수 있는 워크플로 포함 합니다. hello 워크플로에 tooregister 장치를 장치에 필요한 유지 관리 모드에서 장치 toobe hello, hello 장치 상태를 변경 하는 업데이트 설치에서 hello 네트워크 인터페이스 구성 방법과 발생할 수 있는 문제를 해결 포함 됩니다.

이 문서를 읽은 후 다음을 수행할 수 있습니다.

* StorSimple 용 Windows PowerShell을 사용 하 여 tooyour StorSimple 장치를 연결 합니다.
* StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치 관리
* StorSimple용 Windows PowerShell에서 도움말 보기

> [!NOTE]
> * Windows PowerShell for StorSimple cmdlet 허용 toomanage StorSimple 장치 직렬 콘솔에서 또는 원격으로 Windows PowerShell 원격을 통해. 너무 hello이이 인터페이스에서 사용할 수 있는 개별 cmdlet에 대 한 자세한 내용을 보려면 이동[StorSimple 용 Windows PowerShell 용 cmdlet 참조](https://technet.microsoft.com/library/dn688168.aspx)합니다.
> * hello Azure PowerShell StorSimple cmdlet은 StorSimple 서비스 수준 tooautomate hello 명령줄에서 마이그레이션 작업을 수행할 수 있는 cmdlet의 다른 컬렉션입니다. StorSimple 용 hello Azure PowerShell cmdlet에 대 한 자세한 내용을 보려면 이동 toohello [Azure StorSimple cmdlet 참조](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple)합니다.


Hello 메서드를 다음 중 하나를 사용 하 여 StorSimple 용 Windows PowerShell hello를 액세스할 수 있습니다.

* [TooStorSimple 장치 직렬 콘솔에 연결](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Windows PowerShell을 사용 하 여 tooStorSimple 원격으로 연결](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Hello 장치 직렬 콘솔을 통해 tooWindows PowerShell StorSimple에 대 한 연결

있습니다 수 [PuTTY 다운로드](http://www.putty.org/) 또는 유사한 터미널 에뮬레이션 소프트웨어 tooconnect tooWindows StorSimple 용 PowerShell 합니다. PuTTY tooconfigure 필요한 특히 tooaccess hello Microsoft Azure StorSimple 장치입니다. hello 다음 항목 포함 하는 방법에 대 한 자세한 단계 tooconfigure PuTTy toohello 장치를 연결 합니다. Hello 직렬 콘솔에서 다양 한 메뉴 옵션에 대해서도 설명 합니다.

### <a name="putty-settings"></a>PuTTY 설정

PuTTY 설정 tooconnect toohello Windows PowerShell 인터페이스 hello 직렬 콘솔에서 다음 hello를 사용 하 고 있는지 확인 합니다.

#### <a name="tooconfigure-putty"></a>PuTTY tooconfigure

1. Hello PuTTY에서에서 **재구성** 대화 상자의 hello **범주** 창 선택 **키보드**합니다.
2. 해당 hello 다음 옵션을 선택 했는지 확인 (이러한 hello 기본 설정이 새 세션을 시작 하는 경우).
   
   | 키보드 항목 | 여기서 |
   | --- | --- |
   | 백스페이스 키 |Ctrl-? (127) |
   | Home 및 End 키 |Standard |
   | 기능 키 및 키패드 |Esc[n~ |
   | 커서 키의 초기 상태 |정상 |
   | 숫자 키패드의 초기 상태 |정상 |
   | 추가 키보드 기능 사용 |Ctrl-Alt는 AltGr과 다름 |
   
    ![지원되는 Putty 설정](./media/storsimple-windows-powershell-administration/IC740877.png)
3. **Apply**를 클릭합니다.
4. Hello에 **범주** 창 선택 **번역**합니다.
5. Hello에 **원격 문자 집합** 목록 상자 **u t F-8**합니다.
6. **선 그리기 문자 처리** 아래에서 **유니코드 선 그리기 코드 포인트 사용**을 선택합니다. hello 다음 스크린샷은 hello 올바른 PuTTY 선택 항목이 있습니다.
   
    ![UTF Putty 설정](./media/storsimple-windows-powershell-administration/IC740878.png)
7. **Apply**를 클릭합니다.

이제 hello 다음 단계를 수행 하 여 PuTTY tooconnect toohello 장치 직렬 콘솔을 사용할 수 있습니다.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Hello 직렬 콘솔에 대 한

StorSimple 장치의 Windows PowerShell 인터페이스 hello hello 직렬 콘솔을 통해 액세스 하면 배너 메시지와 메뉴 옵션이 차례로 표시 됩니다.

hello 배너 메시지 hello 모델, 이름, 설치 된 소프트웨어 버전 및 액세스 하는 hello 컨트롤러의 상태와 같은 기본적인 StorSimple 장치 정보가 포함 됩니다. 다음 이미지는 hello는 배너 메시지의 예를 보여 줍니다.

![직렬 배너 메시지](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> 들은 hello 컨트롤러 hello 배너 메시지 tooidentify를 사용할 수 있습니다 toois 연결 _활성_ 또는 _수동_합니다.

다음 그림과 hello hello hello 직렬 콘솔 메뉴에서 사용할 수 있는 다양 한 runspace 옵션입니다.

![장치 2 등록](./media/storsimple-windows-powershell-administration/IC740906.png)

Hello 설정을 다음에서 선택할 수 있습니다.

1. **모든 권한으로 로그인** 수 있습니다 (적절 한 자격 증명 hello)와 tooconnect toohello **SSAdminConsole** hello 로컬 컨트롤러에 runspace 합니다. (로컬 컨트롤러 hello hello hello StorSimple 장치의 직렬 콘솔을 통해 현재 액세스 중인 컨트롤러가입니다.) 이 옵션을 사용할 수도 있습니다 tooallow Microsoft 지원 tooaccess 무제한 runspace (지원 세션) tootroubleshoot 가능한 장치 문제입니다. 옵션 1 toolog를 사용 하 여에 허용할 수 있습니다 hello Microsoft 지원 엔지니어 tooaccess 무제한 runspace 특정 cmdlet을 실행 하 여 합니다. 자세한 내용은 참조 너무[지원 세션 시작](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple)합니다.
   
2. **모든 권한으로 컨트롤러 toopeer 로그인** 이 옵션은 옵션 1와 동일한 hello 제외 된다는 (hello 적절 한 자격 증명)을 연결할 수 있습니다 toohello **SSAdminConsole** hello 피어 컨트롤러에 runspace 합니다. Hello StorSimple 장치의 두 컨트롤러가 활성-수동 구성에서 고가용성 장치 이므로 피어 참조 toohello hello 직렬 콘솔을 통해 액세스 하는 hello 장치에 다른 컨트롤러) 합니다.
   비슷한 toooption 1,이 옵션에는 피어 컨트롤러에서 사용 되는 tooallow Microsoft 지원 tooaccess 무제한 runspace 될 수도 있습니다.

3. **제한 된 액세스를 사용 하 여 연결** 이 옵션은 제한 된 모드에서 사용 되는 tooaccess Windows PowerShell 인터페이스입니다. 액세스 자격 증명을 묻는 메시지가 표시되지 않습니다. 이 옵션 tooa 더 제한 된 runspace 비교 toooptions 1과 2를 연결합니다.  옵션 1 통해 사용할 수 있는 hello 작업 중 일부는 **없습니다* 이 runspace에서는 수행할 수는:
   
   * Toohello 출하 시 설정 다시 설정
   * Hello 암호 변경
   * 지원 액세스 사용 또는 사용 안 함
   * 업데이트 적용
   * 핫픽스 설치

    > [!NOTE]
    > Hello 장치 관리자 암호를 잊어버려 옵션 1 이나 2를 통해 연결할 수 없으면 하는 경우 기본 설정 hello 옵션입니다.

4. **언어 변경** 이 옵션 hello Windows PowerShell 인터페이스에서 toochange hello 표시 언어를 허용 합니다. 지원 되는 hello 언어는 영어, 일본어, 러시아어, 프랑스어, 한국어, 스페인어, 이탈리아어, 독일어, 중국어, 포르투갈어 (브라질) 됩니다.

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell을 사용 하 여 tooStorSimple 원격으로 연결

Windows PowerShell remoting tooconnect tooyour StorSimple 장치를 사용할 수 있습니다. 이러한 방식으로 연결하면 메뉴가 표시되지 않습니다. (메뉴가 표시 hello 장치 tooconnect에 hello 직렬 콘솔을 사용 하는 경우에 합니다. 원격으로 연결 하면 hello 직렬 콘솔에 "옵션 1 – 모든 권한"의 직접 toohello 동일 합니다.) Windows PowerShell 원격 기능에서는 특정 runspace tooa 연결할 수 있습니다. Hello 표시 언어를 지정할 수 있습니다.

hello 표시 언어는 hello를 사용 하 여 설정한 hello 언어와 독립적 **언어 변경** hello 직렬 콘솔 메뉴에서 옵션입니다. 원격 PowerShell에서 연결 하는 지정 하지 않으면 hello 장치의 hello 로캘을 자동으로 선택 됩니다.

> [!NOTE]
> Microsoft Azure 가상 호스트 및 StorSimple 클라우드 어플라이언스에 작업 하는 경우에 Windows PowerShell remoting과 hello 가상 호스트 tooconnect toohello 클라우드 어플라이언스에 사용할 수 있습니다. 설정한 경우 공유 위치를 hello hello Windows PowerShell 세션에서 toosave 정보에는 호스트에 알고 있어야 해당 hello _Everyone_ 보안 주체가 인증 된 사용자만 포함 됩니다. 따라서 하 여 hello 공유 tooallow 액세스를 설정한 경우 _Everyone_ 자격 증명을 지정 하지 않고 연결 하 고 인증 되지 않은 익명 사용자 hello 사용 되 고 오류가 표시 됩니다. toofix hello 게스트 계정을 사용 하도록 설정 하 고 다음 hello 게스트 계정 전체 액세스 toohello 공유 또는 사용자를 제공 해야 하는 호스트를 공유 하는 hello에서이 문제는 hello Windows PowerShell cmdlet과 함께 유효한 자격 증명을 지정 해야 합니다.


Windows PowerShell 원격을 통해 tooconnect HTTP 또는 HTTPS를 사용할 수 있습니다. 자습서를 따라 hello에 hello 지침을 따르세요.

* [HTTP를 사용하여 원격으로 연결](storsimple-remote-connect.md#connect-through-http)
* [HTTPS를 사용하여 원격으로 연결](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>연결 보안 고려 사항

결정할 때 tooconnect tooWindows StorSimple에 대 한 PowerShell hello 다음을 고려 하는 방법.

* Toohello 직접 연결 하는 장치 직렬 콘솔은 안전 하지만 네트워크 스위치를 통해 연결 toohello 직렬 콘솔을 없습니다. Toodevice 직렬 네트워크 스위치를 통해 연결할 때에 hello 보안 위험에 주의 해야 합니다.
* HTTP 세션을 통해 연결 네트워크를 통해 hello 직렬 콘솔을 통한 연결 보다 더 강화 된 보안을 제공할 수 있습니다. 가장 안전한 방법은 hello 하지 않더라도 신뢰할 수 있는 네트워크는 것이 좋습니다.
* 가장 안전한 hello 및 hello 권장 옵션은 HTTPS 세션을 통해 연결 합니다.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치 관리

hello 다음 표에 모든 hello 일반 관리 작업 및 수행할 수 있는 복잡 한 워크플로에 대 한 요약 StorSimple 장치의 Windows PowerShell 인터페이스 hello 안에 있습니다. 각 워크플로에 대 한 자세한 내용은 hello hello 테이블에 적절 한 항목을 클릭 합니다.

#### <a name="windows-powershell-for-storsimple-workflows"></a>StorSimple용 Windows PowerShell 워크플로

| 이 toodo 원하는 경우... | 이 절차를 사용합니다. |
| --- | --- |
| 장치 등록 |[StorSimple 용 Windows PowerShell을 사용 하 여 hello 장치를 등록 및 구성](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| 웹 프록시 구성</br>웹 프록시 설정 보기 |[StorSimple 장치에 대한 웹 프록시 구성](storsimple-8000-configure-web-proxy.md) |
| 장치에서 DATA 0 네트워크 인터페이스 설정 수정 |[StorSimple 장치에 대한 DATA 0 네트워크 인터페이스 수정](storsimple-8000-modify-data-0.md) |
| 컨트롤러 중지  </br> 컨트롤러 다시 시작 또는 종료 </br> 장치 종료</br>Hello 장치 toofactory 기본 설정으로 초기화 |[장치 컨트롤러 관리](storsimple-8000-manage-device-controller.md) |
| 유지 관리 모드 업데이트 및 핫픽스 설치 |[장치 업데이트](storsimple-update-device.md) |
| 유지 관리 모드 시작  </br>유지 관리 모드 종료 |[StorSimple 장치 모드](storsimple-8000-device-modes.md) |
| 지원 패키지 만들기</br>지원 패키지 암호 해독 및 편집 |[지원 패키지 만들기 및 관리](storsimple-8000-create-manage-support-package.md) |
| 지원 세션 시작</br> |[StorSimple용 Windows PowerShell에서 지원 세션 시작](storsimple-8000-create-manage-support-package.md#create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell에서 도움말 보기

StorSimple용 Windows PowerShell에서 cmdlet 도움말을 사용할 수 있습니다. 이 도움말의 온라인, 최신 버전도 있습니다를 사용할 수 있는 tooupdate hello 도움말 시스템에 있습니다.

이 인터페이스에서 도움말을 보는 Windows PowerShell에서 유사한 toothat 이며 대부분의 hello 도움말 관련 cmdlet이 작동 합니다. 에 대 한 Windows PowerShell 도움말 온라인 hello TechNet 라이브러리에서에서 찾을 수 있습니다: [Windows PowerShell과 함께 스크립팅](http://go.microsoft.com/fwlink/?LinkID=108518)합니다.

hello 다음은 tooupdate 도움말 hello 하는 방법을 포함 하 여이 Windows PowerShell 인터페이스에 대 한 도움말의 hello 형식의 간략 한 설명입니다.

### <a name="tooget-help-for-a-cmdlet"></a>cmdlet에 대 한 tooget 도움말

* 모든 cmdlet 또는 함수에서 다음 명령을 사용 하 여 hello에 대 한 도움말을 tooget:`Get-Help <cmdlet-name>`
* tooget를 cmdlet에 대 한 온라인 도움말 hello 이전 cmdlet를 사용 하 여 hello로 `-Online` 매개 변수:`Get-Help <cmdlet-name> -Online`
* 전체 도움말에 대 한 hello를 사용할 수 있습니다 `–Full` 매개 변수를 hello를 사용 하 여 예제를 보려면 `–Examples` 매개 변수입니다.

### <a name="tooupdate-help"></a>tooupdate 도움말

쉽게 hello hello Windows PowerShell 인터페이스에 대 한 도움말을 업데이트할 수 있습니다. Hello 단계 tooupdate hello 도움말 시스템에 다음을 수행 합니다.

#### <a name="tooupdate-cmdlet-help"></a>tooupdate cmdlet 도움말
1. Hello로 Windows PowerShell을 시작 **관리자 권한으로 실행** 옵션입니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.`Update-Help`
3. hello 업데이트 도움말 파일이 설치 됩니다.
4. Hello 도움말 파일을 설치한 후 입력: `Get-Help Get-Command`합니다. 도움말을 사용할 수 있는 cmdlet 목록이 표시됩니다.

> [!NOTE]
> tooget runspace에서 모든 hello 사용 가능한 cmdlet의 목록 toohello 해당 메뉴 옵션에 로그인 하 고 hello 실행 `Get-Command` cmdlet.


## <a name="next-steps"></a>다음 단계

워크플로 위에 hello 중 하나를 수행할 때 StorSimple 장치에 문제가 발생 하면 너무 참조[StorSimple 배포 문제 해결 도구](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments)합니다.

