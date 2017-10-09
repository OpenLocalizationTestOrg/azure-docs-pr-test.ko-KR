---
title: Windows VHD tooupload tooAzure aaaPrepare | Microsoft Docs
description: "어떻게 tooprepare Windows VHD 또는 VHDX tooAzure 업로드 하기 전에"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Windows VHD 또는 VHDX tooupload tooAzure 준비
온-프레미스 tooMicrosoft Azure에서에서 Windows 가상 컴퓨터 (VM)를 업로드 하기 전에 hello 가상 하드 디스크 (VHD 또는 VHDX)를 준비 해야 합니다. Azure는 hello VHD 파일 형식으로 고정된 크기 디스크를 포함 하는 1 세대 Vm 에서만 지원 합니다. hello 최대 허용 크기 hello에 대 한 VHD는 1, 023 GB입니다. 한 세대 VHDX hello에서 1 VM 시스템 tooVHD 파일 및 toofixed 크기의 디스크를 동적 확장에서 변환할 수 있습니다. 하지만 VM의 세대는 변경할 수 없습니다. 자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 합니까?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.

Azure VM에 대 한 hello 지원 정책에 대 한 자세한 내용은 참조 [Microsoft Azure Vm에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)합니다.

> [!Note]
> 이 문서의 지침 hello toohello 64 비트 버전의 Windows Server 2008 R2 및 이후 Windows server 운영 체제 적용 됩니다. Azure에서 실행 중인 32비트 버전 운영 체제에 대한 정보는 [Azure 가상 컴퓨터에서 32비트 운영 체제 지원](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines)을 참조하세요.

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>가상 디스크 tooVHD hello와 고정된 크기 디스크 변환 
Tooconvert 필요한 경우 가상 디스크 toohello 형식 Azure를 사용 하 여가이 섹션의 hello 방법 중 하나에 대 한 필요 합니다. Hello 가상 디스크의 변환 프로세스를 실행 하 고 Windows VHD hello 로컬 서버에서 제대로 작동 하는 hello 있는지 확인 하기 전에 VM hello를 백업 합니다. Tooconvert 시도 하거나 tooAzure 업로드 하기 전에 hello VM 자체 내에서 모든 오류를 해결 합니다.

Hello 디스크를 변환한 후 변환 하는 hello 디스크를 사용 하는 VM을 만듭니다. 시작 하 고 업로드에 대 한 hello VM 준비 toohello VM toofinish에 로그인 합니다.

### <a name="convert-disk-using-hyper-v-manager"></a>Hyper-V 관리자를 사용하여 디스크 변환
1. Hyper-v 관리자를 열고 hello 왼쪽에 로컬 컴퓨터를 선택 합니다. Hello hello 컴퓨터 목록 위의 메뉴에서 **동작** > **디스크 편집**합니다.
2. Hello에 **가상 하드 디스크 찾기** 화면을 찾아서 가상 디스크를 선택 합니다.
3. Hello에 **작업 선택** 화면에서 선택한 후 **변환** 및 **다음**합니다.
4. Tooconvert VHDX에서 필요한 경우에 선택 **VHD** 클릭 하 고 **다음**
5. 동적 확장 디스크에서 tooconvert 필요한 경우에 선택 **고정 크기** 클릭 하 고 **다음**
6. 찾아 경로 toosave hello 새 VHD 파일을 선택 합니다.
7. **마침**을 클릭합니다.

>[!NOTE]
>이 문서의 hello 명령은 관리자 권한 PowerShell 세션에서 실행 되어야 합니다.

### <a name="convert-disk-by-using-powershell"></a>PowerShell을 사용한 디스크 변환
Hello를 사용 하 여 가상 디스크를 변환할 수 [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) Windows PowerShell에서 명령을 합니다. PowerShell을 시작할 때 **관리자 권한으로 실행**을 선택합니다. 

hello 다음 예제 명령은 VHDX tooVHD에서 인스턴스 간에 변환 동적 확장 디스크 toofixed-크기:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
이 명령에 대 한 hello 값을 대체 "-경로" hello 경로 toohello 가상 하드 디스크를 원하는 tooconvert 및 hello 값에 대 한 "-DestinationPath" hello 새 경로 및 이름 hello로 디스크를 변환 합니다.

### <a name="convert-from-vmware-vmdk-disk-format"></a>VMware VMDK 디스크 형식에서 변환
Windows VM 이미지를 hello에 있는 경우 [VMDK 파일 형식](https://en.wikipedia.org/wiki/VMDK), hello를 사용 하 여 tooa VHD 변환 [Microsoft VM 변환기](https://www.microsoft.com/download/details.aspx?id=42497)합니다. 자세한 내용은 hello 블로그 게시물을 참조 하십시오. [어떻게 tooConvert VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx)합니다.

## <a name="set-windows-configurations-for-azure"></a>Azure에 대한 Windows 구성 설정

VM hello hello 다음에서 모든 명령을 실행 하는 tooupload tooAzure 단계에서 한 [관리자 권한 명령 프롬프트 창을](https://technet.microsoft.com/library/cc947813.aspx):

1. Hello 라우팅 테이블에 모든 정적 영구 경로 제거 합니다.
   
   * 실행 tooview hello 경로 테이블 `route print` hello 명령 프롬프트입니다.
   * Hello 확인 **지 속성 경로** 섹션. 사용 하 여 일관 된 경로 이면 [경로 삭제](https://technet.microsoft.com/library/cc739598.apx) tooremove 것입니다.
2. Hello WinHTTP 프록시를 제거 합니다.
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. 너무 hello 디스크 SAN 정책을 설정[Onlineall](https://technet.microsoft.com/library/gg252636.aspx)합니다. 
   
    ```PowerShell
    diskpart 
    ```
    Hello open 명령 프롬프트 창에서 다음 명령을 hello를 입력 합니다.

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Windows에 대 한 utc (협정 세계시) 시간을 설정 하 고 hello (w32time) Windows 시간 서비스의 시작 유형을 너무 hello**자동으로**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Hello 전원 프로필 toohello 설정 **고성능**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Windows 서비스의 hello 확인
각 Windows 서비스를 수행 하는 hello toohello 설정 되어 있는지 확인 **Windows 기본값**합니다. 이들은 hello toomake 해당 hello VM에 연결 되어 있는지를 설정 해야 하는 서비스의 최소 번호입니다. tooreset hello 시작 설정, hello 다음 명령을 실행 합니다.
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>원격 데스크톱 레지스트리 설정 업데이트
원격 데스크톱 연결에 대 한 설정에 따라 해당 hello 올바르게 구성 되어 있는지 확인 합니다.

>[!Note] 
>Hello를 실행할 때 오류 메시지가 나타날 수 있습니다 **Set-itemproperty-경로 ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal 서비스-이름 &lt;개체 이름&gt; &lt;값&gt;** 다음이 단계에 있습니다. hello 오류 메시지는 무시 해도 됩니다. 해당 hello 도메인은 그룹 정책 개체를 통해 해당 구성을 보내지 의미 합니다.
>
>

1. RDP(원격 데스크톱 프로토콜)이 활성화되어 있습니다.
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. hello RDP 포트가 제대로 설정 (기본 포트 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    VM을 배포할 때 포트 3389에 대해 hello 기본 규칙 생성 됩니다. Toochange hello 포트 번호를 수행 하는 hello VM이 Azure에 배포 된 후 합니다.

3. hello 수신기가 모든 네트워크 인터페이스에서 수신 대기 합니다.
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Hello RDP 연결에 대 한 hello 네트워크 수준 인증 모드를 구성 합니다.
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Hello 유지 값을 설정 합니다.
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. 다시 연결합니다.
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Hello 동시 연결 수를 제한 합니다.
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. 자체 서명 된 인증서 toohello RDP 수신기 연결 되어 있는 경우 제거 합니다.
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    이 hello VM을 배포할 때 hello 시작 부분에 연결할 수 있는지 toomake입니다. 또한에서 검토할 수 있습니다이 이후 단계 후 필요한 경우 Azure에서 VM을 배포 하는 hello 합니다.

9. Hello VM 도메인의 일부가 인 경우 모든 hello 설정을 toomake hello 이전 설정은 되돌려지지 않습니다 있는지 다음을 확인 합니다. 확인 해야 하는 hello 정책을 hello 다음과 같습니다.
    
    - RDP 활성화됨:

         Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:
         
         **원격 데스크톱을 사용 하 여 사용자가 tooconnect를 원격으로 허용**

    - NLA 그룹 정책:

        Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security: 
        
        **네트워크 수준 인증을 사용한 원격 연결에 대해 사용자 인증 필요**
    
    - 연결 유지 설정:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **연결 유지 연결 간격 구성**

    - 다시 연결 설정:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **자동 다시 연결**

    - 연결 설정의 hello 수 제한:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **연결 수 제한**

## <a name="configure-windows-firewall-rules"></a>Windows 방화벽 규칙 구성
1. 세 hello 프로필 (도메인, Standard 및 공용)에서 Windows 방화벽을 설정 합니다.

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Hello 다음 (도메인, 개인 및 공용) hello 3 개의 방화벽 프로필을 통해 PowerShell tooallow WinRM에서에서 명령을 실행 하 고 hello PowerShell 원격 서비스를 사용 하도록 설정 합니다.
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. 다음 방화벽 규칙 tooallow hello RDP 트래픽 hello를 사용 하도록 설정 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Hello VM 응답할 수 있도록 hello 가상 네트워크 내 tooa ping 명령을 hello 파일 및 프린터 공유 규칙을 설정 합니다.

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Hello VM 도메인의 일부가 인 경우 hello 설정을 toomake hello 이전 설정은 되돌려지지 않습니다 있는지 다음을 확인 합니다. 확인 해야 하는 hello AD 정책을 hello 다음과 같습니다.

    - Hello Windows 방화벽 프로필을 사용 하도록 설정

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **모든 네트워크 연결 보호**

       Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **모든 네트워크 연결 보호**

    - RDP를 사용하도록 설정 

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**

    - ICMP-V4를 사용하도록 설정

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **ICMP 예외 허용**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **ICMP 예외 허용**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>VM이 정상 상태이고 안전하며 RDP로 액세스할 수 있는지 확인 
1. toomake 있는지 hello 디스크가 정상 상태이 고 일관 된 hello 다음 VM 다시 시작 시 검사 디스크 작업을 실행:

    ```PowerShell
    Chkdsk /f
    ```
    Hello  명확 하 고 정상 디스크 있는지 확인 합니다.

2. Hello 데이터 BCD (부팅 구성) 설정을 구성 합니다. 

    > [!Note]
    > 이러한 명령을 PowerShell이 **아닌** 관리자 권한 CMD 창에서 실행하고 있는지 확인합니다.
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. 일관성이 해당 hello Windows 관리 Instrumentations 리포지토리를 확인 합니다. tooperform 다음 명령이 실행된이, hello:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Hello 저장소 손상 된 경우 참조 [WMI: 저장소 손상 여부](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)합니다.

4. 다른 모든 응용 프로그램 hello 포트 3389를 사용 하지 않는 있는지 확인 합니다. 이 포트는 hello Azure의 RDP 서비스에 사용 됩니다. 실행할 수 있습니다 **netstat-anob** toosee 사용 되는 포트에 hello VM에서:

    ```PowerShell
    netstat -anob
    ```

5. Hello tooupload 되도록 Windows VHD 도메인 컨트롤러인 경우에 다음이 단계를 수행 합니다.

    A. 에 따라 [이러한 추가 단계](https://support.microsoft.com/kb/2904015) tooprepare hello 디스크.

    B. Toostart hello VM DSRM에서 특정 시점에 있을 경우 hello DSRM 암호를 알고 있는지 확인 합니다. Toorefer toothis tooset hello를 연결 하는 것이 좋습니다 [DSRM 암호](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx)합니다.

6. Tooyou hello 기본 제공 관리자 계정 및 암호 정상 인지 확인 합니다. Hello RDP 연결을 통해 tooWindows에이 계정을 toosign를 사용할 수 있는지 확인 하 고 tooreset hello 현재 로컬 관리자 암호를 사용할 수 있습니다. 이 액세스 권한은 hello "로그온 허용 원격 데스크톱 서비스를 통해" 그룹 정책 개체에 의해 제어 됩니다. Hello 로컬 그룹 정책 편집기에서에서이 개체를 볼 수 있습니다에서:

    Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment

7. 다음 AD hello 정책을 toomake RDP를 통해 또는 hello 네트워크에서 RDP 액세스를 차단 하지 않는지 선택 되어 있는지 확인 합니다.

    - Hello 네트워크에서 컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 Assignment\Deny 액세스 toothis 컴퓨터

    - Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services


8. Windows가 아직 정상 상태가 되었는지 다시 시작 hello VM toomake hello RDP 연결을 사용 하 여 도달할 수 있습니다. 이 시점에서 수 있습니다 toocreate VM에서 사용자 로컬 Hyper-v toomake 있는지 hello VM이 완전히 시작 중임을 다음 RDP 연결할 수 인지 테스트 합니다.

9. TCP 패킷 또는 추가 방화벽을 분석하는 소프트웨어와 같은 추가 전송 드라이버 인터페이스 필터를 모두 제거합니다. 또한에서 검토할 수 있습니다이 이후 단계 후 필요한 경우 Azure에서 VM을 배포 하는 hello 합니다.

10. 제 3 자 소프트웨어 및 관련된 toophysical 구성 요소 또는 다른 가상화 기술 되는 드라이버를 제거 합니다.

### <a name="install-windows-updates"></a>Windows 업데이트 설치
hello 이상적인 구성은 너무**hello hello 최신 버전에 있는 컴퓨터의 hello 패치 수준이**합니다. 없는 경우 업데이트를 수행 하는 hello 설치 되어 있는지 확인 합니다.

|                       |                   |           |                                       최소 파일 버전 x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| 구성 요소               | 이진            | Windows 7 및 Windows Server 2008 R2 | Windows 8 및 Windows Server 2012             | Windows 8.1 및 Windows Server 2012 R2 | Windows 10 & Windows Server 2016 RS1 | Windows 10 RS2             |
| 저장소                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| 네트워크                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| 코어                    | ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| 원격 데스크톱 서비스 | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| 보안                | 기한 tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### 때 toouse sysprep<a id="step23"></a>    

Sysprep는 hello 시스템의 hello 설치를 다시 설정 됩니다 하는 "hello 초기 경험" 모든 개인 데이터를 제거 하 고 여러 구성 요소가 다시 설정 하 여를 제공 하는 windows 설치로 실행 될 수 있는 프로세스입니다. 일반적으로 이렇게 하면 toocreate 하려는 경우 템플릿을 특정 구성에 있는 다른 여러 Vm을 배포할 수 있습니다. 이를 **일반화된 이미지**라고 합니다.

대신 하나 유일한 toocreate 하려는 경우 VM 한 디스크에서 toouse sysprep 필요가 없습니다. 이 경우에만 만들 수 있습니다 VM과 라고 하는 hello는 **특수 이미지**합니다.

Toocreate 특수 한 디스크에서 VM 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은:

- [특수화된 디스크에서 VM 만들기](create-vm-specialized.md)
- [특수화된 VHD 디스크에서 VM 만들기](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Toocreate 일반화 된 이미지를 원하는 경우 toorun sysprep을 해야 합니다. Sysprep에 대 한 자세한 내용은 참조 [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다. 

Windows 기반 컴퓨터에 설치된 모든 역할 또는 응용 프로그램이 이 일반화를 지원하는 것은 아닙니다. 이 절차를 실행, toohello 문서 toomake 있는지 다음을 참조 되기 전에 해당 컴퓨터의 해당 hello 역할 sysprep에서 지원 됩니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.

### <a name="steps-toogeneralize-a-vhd"></a>단계 toogeneralize VHD

>[!NOTE]
> 다음 단계에 지정 된 hello로 sysprep.exe를 실행 한 후 VM hello 끈 수행 하지 다시 설정에서 Azure에서 이미지를 만들 때까지.

1. Toohello Windows VM에에서 로그인 합니다.
2. 관리자 권한으로 **명령 프롬프트**를 실행합니다. 
3. Hello 디렉터리를 변경 하려면: **%windir%\system32\sysprep**, 한 다음 실행 **sysprep.exe**합니다.
3. Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.

    ![시스템 준비 도구](media/prepare-for-upload-vhd-image/syspre.png)
4. **종료 옵션**에서 **종료**를 선택합니다.
5. **확인**을 클릭합니다.
6. Sysprep이 완료 되 면 VM hello를 종료 합니다. 사용 하지 마십시오 **다시 시작** tooshut hello VM 다운 합니다.
7. 이제 hello VHD가 준비 toobe 업로드 합니다. Toocreate 일반화 된 디스크에서 VM 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [일반화 된 VHD를 업로드 하 고 Azure에서 새 Vm toocreate 사용](sa-upload-generalized.md)합니다.


## <a name="complete-recommended-configurations"></a>권장된 구성 완료
다음 설정을 hello VHD 업로드 영향을 주지 않습니다. 단, 반드시 구성하는 것이 좋습니다.

* Hello 설치 [Azure Vm 에이전트](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 그런 다음 VM 확장을 사용하도록 설정할 수 있습니다. hello VM 확장을 수도 toouse RDP를 구성 하 여 vm 암호를 재설정 같은 있으며 등 hello 중요 한 기능을 대부분을 구현 합니다. 자세한 내용은 다음을 참조하세요.

    - [VM 에이전트 및 확장 - 1부](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [VM 에이전트 및 확장 - 2부](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* hello 덤프 로그 Windows 충돌 문제를 해결 하는 데 도움이 될 수 있습니다. Hello 덤프 로그 수집을 사용 합니다.
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    표시 되 면이 문서의 단계를 hello 절차적 동안 모든 오류, hello 레지스트리 키 이미 존재 한다는 것을 의미 합니다. 이러한 상황에서 명령 대신 다음 hello를 사용 합니다.

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Azure의 hello VM을 만든 후에 hello "임시 드라이브" 볼륨 tooimprove 성능에 hello 페이지 파일을 두는 것이 좋습니다. 이 작업은 다음과 같이 준비할 수 있습니다.

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
연결 된 toohello VM이 있는 모든 데이터 디스크 이면 hello 임시 드라이브 볼륨의 드라이브 문자는 일반적으로 "4". 이 지정 hello 사용 가능한 드라이브 수 및 설정한 hello 설정에 따라 달라질 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [리소스 관리자 배포에 대 한 Windows VM 이미지 tooAzure 업로드](upload-generalized-managed.md)

