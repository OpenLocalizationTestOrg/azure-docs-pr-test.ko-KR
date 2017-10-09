---
title: "aaaConnect tooyour StorSimple 장치에 원격으로 | Microsoft Docs"
description: "에 대해 설명 어떻게 tooconfigure 원격 관리를 위한 장치 방법과 tooconnect tooWindows HTTP 또는 HTTPS를 통해 StorSimple 용 PowerShell 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Tooyour StorSimple 8000 시리즈 장치에 원격으로 연결

## <a name="overview"></a>개요

Windows PowerShell을 통해 tooyour 장치를 원격으로 연결할 수 있습니다. 이러한 방식으로 연결하면 메뉴가 표시되지 않습니다. (표시 메뉴 hello 장치 tooconnect에 hello 직렬 콘솔을 사용 하는 경우에.) Windows PowerShell 원격 기능에서는 특정 runspace tooa 연결할 수 있습니다. Hello 표시 언어를 지정할 수 있습니다.

Windows PowerShell remoting toomanage 장치를 사용 하는 방법에 대 한 자세한 내용은 이동 너무[tooadminister StorSimple에 대 한 Windows PowerShell을 사용 하 여 StorSimple 장치](storsimple-8000-windows-powershell-administration.md)합니다.

이 자습서에 설명 방법을 tooconfigure 다음 방법과 원격 관리에 대 한 장치 tooconnect tooWindows StorSimple 용 PowerShell 합니다. HTTP를 사용할 수 있습니다 또는 Windows PowerShell을 통해 HTTPS tooremotely 연결 합니다. 그러나 결정할 때 tooconnect tooWindows StorSimple에 대 한 PowerShell hello 다음 정보를 고려 하는 방법:

* Toohello 직접 연결 하는 장치 직렬 콘솔은 안전 하지만 네트워크 스위치를 통해 연결 toohello 직렬 콘솔을 없습니다. 네트워크 스위치를 통해 toohello 장치 직렬 콘솔을 연결할 때에 hello 보안 위험에 주의 해야 합니다.
* HTTP 세션을 통해 연결 hello 네트워크를 통해 hello 직렬 콘솔을 통한 연결 보다 더 강화 된 보안을 제공할 수 있습니다. 가장 안전한 방법은 hello 하지 않더라도 신뢰할 수 있는 네트워크는 것이 좋습니다.
* 가장 안전한 hello 및 hello 권장 옵션은 자체 서명 된 인증서와 HTTPS 세션을 통해 연결 합니다.

Windows PowerShell 인터페이스 toohello 원격으로 연결할 수 있습니다. 그러나, hello Windows PowerShell 인터페이스를 통해 원격 액세스 tooyour StorSimple 장치는 기본적으로 사용 되지 않습니다. 먼저, hello 장치에서 원격 관리를 사용 하도록 설정 하 고에 hello tooaccess 사용된 되는 클라이언트 장치 해야 합니다.

이 문서에 설명 된 hello 단계는 Windows Server 2012 r 2를 실행 하는 호스트 시스템에서 수행 된 합니다.

## <a name="connect-through-http"></a>HTTP를 통해 연결

TooWindows PowerShell StorSimple에 대 한 HTTP 세션을 통해 연결 하는 hello StorSimple 장치의 직렬 콘솔을 통한 연결 보다 더 강화 된 보안을 제공 합니다. 가장 안전한 방법은 hello 하지 않더라도 신뢰할 수 있는 네트워크는 것이 좋습니다.

Hello Azure 포털 또는 hello 직렬 콘솔 tooconfigure 원격 관리 중 하나를 사용할 수 있습니다. 다음 절차를 수행 하는 hello에서 선택 합니다.

* [Hello Azure 포털 tooenable 원격 관리를 사용 하 여 HTTP를 통해](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTP를 통해](#use-the-serial-console-to-enable-remote-management-over-http)

원격 관리를 활성화 한 후 다음 원격 연결에 대 한 프로시저 tooprepare hello 클라이언트 hello를 사용 합니다.

* [원격 연결에 대 한 hello 클라이언트 준비](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a>Hello Azure 포털 tooenable 원격 관리를 사용 하 여 HTTP를 통해

HTTP를 통해 hello Azure 포털 tooenable 원격 관리의 단계를 실행 하는 hello를 수행 합니다.

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a>tooenable hello Azure 포털을 통해 원격 관리

1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. 선택 **장치** 다음 선택 하 고 원격 관리를 위한 tooconfigure 원하는 hello 장치를 클릭 합니다. 너무 이동**장치 설정 > 보안**합니다.
2. Hello에 **보안 설정** 블레이드에서 클릭 **원격 관리**합니다.
3. Hello에 **원격 관리** 설정 블레이드에서 **원격 관리를 사용 하도록 설정** 너무**예**합니다.
4. 이제 HTTP를 사용 하 여 tooconnect를 선택할 수 있습니다. (hello 기본값은 tooconnect HTTPS를 통한.) HTTP가 선택되었는지 확인합니다.
   
   > [!NOTE]
   > HTTP를 통한 연결은 신뢰할 수 있는 네트워크에서만 허용됩니다.
   
5. **저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 선택합니다.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTP를 통해
Hello hello 장치 직렬 콘솔 tooenable 원격 관리에 대 한 단계를 수행 합니다.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable hello 장치 직렬 콘솔을 통해 원격 관리
1. Hello 직렬 콘솔 메뉴에서 옵션 1을 선택 합니다. 너무 hello 장치 hello 직렬 콘솔을 사용 하는 방법에 대 한 자세한 내용을 보려면 이동[장치 직렬 콘솔을 통해 tooWindows PowerShell StorSimple에 대 한 연결](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)합니다.
2. Hello 프롬프트에서 다음을 입력 합니다.`Enable-HcsRemoteManagement –AllowHttp`
3. HTTP tooconnect toohello 장치를 사용 하 여 hello 보안 취약점에 대 한 알림이 표시 됩니다. 메시지가 표시되면 **Y**를 입력하여 확인합니다.
4. 다음을 입력하여 HTTP를 사용할 수 있는지 확인합니다. `Get-HcsSystem`
5. 해당 hello 확인 **RemoteManagementMode** 필드 **HttpsAndHttpEnabled**.hello 그림 다음 PuTTY에서 이러한 설정을 보여 줍니다.
   
     ![직렬 HTTPS 및 HTTP 사용](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>원격 연결에 대 한 hello 클라이언트 준비
Hello hello 클라이언트 tooenable 원격 관리에 대 한 단계를 수행 합니다.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>원격 연결에 대 한 tooprepare hello 클라이언트
1. 관리자 권한으로 Windows PowerShell 세션을 시작합니다.
2. Hello 다음 hello StorSimple 장치 toohello 클라이언트의 신뢰할 수 있는 호스트 목록의 명령 tooadd hello IP 주소를 입력 합니다.
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     대체 <*device_ip*> 장치; hello IP 주소로 예: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. 다음 명령은 toosave hello 장치 자격 증명을 변수에 hello를 입력 합니다. 
   
    ```
    $cred = Get-Credential
    ```
    
4. Hello 대화 상자가 나타나면:
   
   1. 이 형식으로 hello 사용자 이름을 입력: *device_ip\SSAdmin*합니다.
   2. Hello hello 설치 마법사를 사용 hello 장치를 구성할 때 설정한 장치 관리자 암호를 입력 합니다. hello 기본 암호는 *Password1*합니다.
5. 이 명령을 입력 하 여 hello 장치에서 Windows PowerShell 세션을 시작 합니다.
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > hello를 추가 하는 hello StorSimple 가상 장치에 사용 하기 위해 Windows PowerShell 세션 toocreate `–Port` 매개 변수 hello StorSimple 가상 어플라이언스 Remoting에서 구성한 공용 포트를 지정 합니다.
   
   
이 시점에서 활성 원격 Windows PowerShell 세션 toohello 장치가 있어야 합니다.
   
![HTTP를 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>HTTPS를 통해 연결

TooWindows PowerShell StorSimple에 대 한 HTTPS 세션을 통해 연결 하는 가장 안전한 hello 및 권장 되는 방법의 tooyour Microsoft Azure StorSimple 장치를 원격으로 연결 합니다. 다음 절차를 수행 하는 hello StorSimple에 대 한 HTTPS tooconnect tooWindows PowerShell을 사용할 수 있도록 직렬 콘솔과 클라이언트 컴퓨터를 tooset hello 하는 방법을 설명 합니다.

Hello Azure 포털 또는 hello 직렬 콘솔 tooconfigure 원격 관리 중 하나를 사용할 수 있습니다. 다음 절차를 수행 하는 hello에서 선택 합니다.

* [Hello Azure 포털 tooenable 원격 관리를 사용 하 여 HTTPS를 통해](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTPS를 통해](#use-the-serial-console-to-enable-remote-management-over-https)

원격 관리를 활성화 한 후 다음 원격 관리에 대 한 프로시저 tooprepare hello 호스트 hello를 사용 하 고 hello 원격 호스트에서 toohello 장치를 연결 합니다.

* [원격 관리를 위해 hello 호스트 준비](#prepare-the-host-for-remote-management)
* [Hello 원격 호스트에서 toohello 장치 연결](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a>Hello Azure 포털 tooenable 원격 관리를 사용 하 여 HTTPS를 통해

HTTPS를 통해 hello Azure 포털 tooenable 원격 관리의 단계를 실행 하는 hello를 수행 합니다.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a>hello Azure 포털에서에서 HTTPS 통한 tooenable 원격 관리

1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. 선택 **장치** 다음 선택 하 고 원격 관리를 위한 tooconfigure 원하는 hello 장치를 클릭 합니다. 너무 이동**장치 설정 > 보안**합니다.
2. Hello에 **보안 설정** 블레이드에서 클릭 **원격 관리**합니다.
3. 설정 **원격 관리를 사용 하도록 설정** 너무**예**합니다.
4. 이제 HTTPS를 사용 하 여 tooconnect를 선택할 수 있습니다. (hello 기본값은 tooconnect HTTPS를 통한.) HTTPS가 선택되었는지 확인합니다.
5. ...를 클릭한 후 **원격 관리 인증서 다운로드**를 클릭합니다. 위치 toosave이이 파일을 지정 합니다. Tooconnect toohello 장치 사용 하 여 hello 클라이언트 또는 호스트 컴퓨터에이 인증서 tooinstall가 필요 합니다.
6. **저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTPS를 통해

Hello hello 장치 직렬 콘솔 tooenable 원격 관리에 대 한 단계를 수행 합니다.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable hello 장치 직렬 콘솔을 통해 원격 관리
1. Hello 직렬 콘솔 메뉴에서 옵션 1을 선택 합니다. 너무 hello 장치 hello 직렬 콘솔을 사용 하는 방법에 대 한 자세한 내용을 보려면 이동[장치 직렬 콘솔을 통해 tooWindows PowerShell StorSimple에 대 한 연결](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)합니다.
2. Hello 프롬프트에서 다음을 입력 합니다.
   
     `Enable-HcsRemoteManagement`
   
    이제 장치에서 HTTPS를 사용할 수 있습니다.
3. 다음을 입력하여 HTTPS를 사용할 수 있는지 확인합니다. 
   
     `Get-HcsSystem`
   
    해당 hello 있는지 확인 **RemoteManagementMode** 필드 **HttpsEnabled**.hello 그림 다음 PuTTY에서 이러한 설정을 보여 줍니다.
   
     ![직렬 HTTPS 사용](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. hello 출력에서 `Get-HcsSystem`, hello hello 장치 일련 번호를 복사 하 고 나중에 사용할 저장 합니다.
   
   > [!NOTE]
   > hello 일련 번호 hello 인증서에 CN 이름을 toohello 매핑합니다.
   
5. 다음을 입력하여 원격 관리 인증서를 가져옵니다. 
   
     `Get-HcsRemoteManagementCert`
   
    인증서 비슷한 toohello 다음 표시 됩니다.
   
    ![원격 관리 인증서 가져오기](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. hello 인증서의 hello 정보 복사 **---BEGIN 인증서---** 너무**---END 인증서---** .cer 파일로 저장 하 고 메모장과 같은 텍스트 편집기에 있습니다. (복사할 파일 tooyour 원격 호스트가 hello 호스트를 준비할 때.)
   
   > [!NOTE]
   > toogenerate 새 인증서를 사용 하 여 hello `Set-HcsRemoteManagementCert` cmdlet.
   
### <a name="prepare-hello-host-for-remote-management"></a>원격 관리를 위해 hello 호스트 준비

다음 절차를 수행 하는 hello를 수행 하는 HTTPS 세션을 사용 하는 원격 연결에 대 한 tooprepare hello 호스트 컴퓨터.

* [클라이언트 hello 또는 원격 호스트의 루트 저장소 hello hello.cer 파일 가져오기](#to-import-the-certificate-on-the-remote-host)합니다.
* [원격 호스트 hello 장치 일련 번호 toohello 호스트 파일을 추가](#to-add-device-serial-numbers-to-the-remote-host)합니다.

각각 hello 절차 앞의 설명은 다음과 같습니다.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>hello 원격 호스트에서 tooimport hello 인증서
1. Hello.cer 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **인증서 설치**합니다. Hello 인증서 가져오기 마법사를 시작합니다.
   
    ![인증서 가져오기 마법사 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. **저장소 위치**에 대해 **로컬 컴퓨터**를 선택하고 **다음**을 클릭합니다.
3. 선택 **모든 인증서 저장소를 다음 hello에 저장**, 클릭 하 고 **찾아보기**합니다. 원격 호스트의 루트 저장소 toohello 탐색 한 다음 클릭 **다음**합니다.
   
    ![인증서 가져오기 마법사 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. **마침**을 클릭합니다. Hello 가져오기가 완료 되었는지 여부를 알려 주는 메시지가 표시 됩니다.
   
    ![인증서 가져오기 마법사 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>tooadd 장치 일련 번호 toohello 원격 호스트
1. 관리자 권한으로 메모장을 시작 하 고 \Windows\System32\Drivers\etc에 위치한 hello 호스트 파일을 엽니다.
2. 다음 세 가지 항목 tooyour 호스트 파일 hello 추가: **DATA 0 IP 주소**, **컨트롤러 0 고정 IP 주소**, 및 **컨트롤러 1 고정 IP 주소**합니다.
3. 이전에 저장 하는 hello 장치 일련 번호를 입력 합니다. 다음 이미지는 hello와 같이이 toohello IP 주소를 매핑하십시오. 컨트롤러 0과 컨트롤러 1에 대 한 추가 **Controller0** 및 **Controller1** hello 일련 번호 (CN 이름)의 hello 끝에 있습니다.
   
    ![CN 이름 toohosts 파일 추가](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Hello 호스트 파일을 저장 합니다.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Hello 원격 호스트에서 toohello 장치 연결

Windows PowerShell 및 SSL을 사용 하 여 원격 호스트 또는 클라이언트 장치에서 SSAdmin 세션 tooenter 합니다. hello SSAdmin 세션 매핑합니다 hello에 1 toooption [직렬 콘솔](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) 장치의 메뉴.

Hello 절차 toomake hello 원격 Windows PowerShell 연결 하려는 hello 컴퓨터에서 다음을 수행 합니다.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>Windows PowerShell 및 SSL을 사용 하 여 hello 장치에서 SSAdmin 세션 tooenter
1. 관리자 권한으로 Windows PowerShell 세션을 시작합니다.
2. 입력 하 여 hello 장치 IP 주소 toohello 클라이언트의 신뢰할 수 있는 호스트를 추가 합니다.
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    여기서 <*device_ip*> 장치의 hello IP 주소입니다; 예: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. toocreate 새 자격 증명을 입력 합니다.
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    여기서 <*대상 장치의 IP*>는 해당 장치용; DATA 0의 hello IP 주소 예를 들어 **10.126.173.90** hello hello 호스트 파일의 이미지를 앞에 표시 된 대로 합니다. 또한 장치에 대 한 hello 관리자 암호를 제공 합니다.
4. 다음을 입력하여 세션을 만듭니다.
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Hello cmdlet의 hello-ComputerName 매개 변수에 대해 제공 hello <*대상 장치의 일련 번호*> 합니다. 이 일련 번호 매핑된 toohello 원격 호스트; hello hosts 파일에서 DATA 0 IP 주소 예를 들어 **SHX0991003G44MT** hello 다음 이미지와 같이 합니다.
5. 형식:
   
     `Enter-PSSession $session`
6. Toowait 몇 분 필요 하며 SSL을 통한 HTTPS 통해 연결 된 tooyour 장치 수 합니다. 연결 된 tooyour 장치 지 나타내는 메시지가 표시 됩니다.
   
    ![HTTPS 및 SSL을 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>다음 단계

* 에 대 한 자세한 내용은 [StorSimple 장치의 Windows PowerShell tooadminister를 사용 하 여](storsimple-8000-windows-powershell-administration.md)합니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

