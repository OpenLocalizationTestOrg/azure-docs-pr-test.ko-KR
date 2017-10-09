---
title: " Azure Site Recovery에서 구성 서버 관리 | Microsoft Doc"
description: "이 문서에서는 설명 방법을 tooset 하 고 구성 서버를 관리 합니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>구성 서버 관리

구성 서버 hello Site Recovery 서비스와 온-프레미스 인프라 간의 코디네이터로 작동합니다. 이 문서에서는 설정, 구성 하는 방법 관리 hello 구성 서버를 설명 합니다.

## <a name="prerequisites"></a>필수 조건
hello 다음 hello 최소 하드웨어, 소프트웨어 및 구성 서버를 네트워크 구성이 필요 tooset은입니다.

> [!NOTE]
> [용량 계획](site-recovery-capacity-planner.md) 를 배포 하는 구성 사용 하 여 구성 서버 hello 해당 도구 모음 하는 중요 한 단계 tooensure는 로드 요구 합니다. [구성 서버에 대한 크기 조정 요구 사항](#sizing-requirements-for-a-configuration-server)에 대해 자세히 읽어보세요.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Hello 구성 서버 소프트웨어를 다운로드합니다.
1. Azure 포털 및 찾아보기 tooyour 복구 서비스 자격 증명 모음 toohello에 로그온 합니다.
2. 너무 찾아보기**사이트 복구 인프라** > **구성 서버** (아래에 대 한 VMware & 물리적 컴퓨터의 경우).

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Hello 클릭 **+ 서버** 단추입니다.
4. Hello에 **서버 추가** 페이지 hello 다운로드 단추 toodownload hello 등록 키를 클릭 합니다. Hello 구성 서버 설치 tooregister 하는 동안이 키가 필요 하면 Azure Site Recovery 서비스와 합니다.
5. Hello 클릭 **다운로드 hello Microsoft Azure Site Recovery 통합 설치** 링크 toodownload hello 최신 버전의 구성 서버 hello 합니다.

  ![다운로드 페이지](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  최신 버전의 hello 구성 서버에서 직접 다운로드할 수 있습니다 [Microsoft 다운로드 센터 다운로드 페이지](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>GUI에서 구성 서버 설치 및 등록
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>명령줄에서 구성 서버 설치 및 등록

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>샘플 사용
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>구성 서버 설치 관리자 명령줄 인수
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>MySql 자격 증명 파일 만들기
MySQLCredsFilePath 매개 변수는 입력으로 파일을 사용합니다. 다음 서식을 지정 하 고 입력된 MySQLCredsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 hello 파일을 만듭니다.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>프록시 설정 구성 파일 만들기
ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다. 다음 서식을 지정 하 고 입력된 ProxySettingsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 hello 파일을 만듭니다.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>구성 서버의 프록시 설정 수정
1. 로그인 tooyour 구성 서버입니다.
2. 바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 실행 하면 됩니다.
3. Hello 클릭 **자격 증명 모음 등록** 탭 합니다.
4. Hello 포털에서 새 자격 증명 모음 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Hello 새 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.
6. 관리자 PowerShell 명령 창을 엽니다.
7. Hello 다음 명령을 실행 합니다.
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  있는 경우 확장 프로세스 서버 toothis 구성 서버를 연결, 너무 해야[hello 프록시 설정을 모든 hello 확장 프로세스 서버에서 수정](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) 배포에서 합니다.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Hello 사용 하 여 구성 서버를 다시 등록 동일한 복구 서비스 자격 증명 모음
  1. 로그인 tooyour 구성 서버입니다.
  2. 바탕 화면에 바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 시작 합니다.
  3. Hello 클릭 **자격 증명 모음 등록** 탭 합니다.
  4. Hello 포털에서 새 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Hello 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.  
  6. 관리자 PowerShell 명령 창을 엽니다.
  7. Hello 다음 명령을 실행 합니다.

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  있는 경우 확장 프로세스 서버 toothis 구성 서버를 연결, 너무 필요한[모든 hello 확장 프로세스 서버를 다시 등록](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) 배포에서 합니다.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>다른 Recovery Services 자격 증명 모음에 구성 서버 등록
1. 로그인 tooyour 구성 서버입니다.
2. hello 명령을 실행 하는 관리자 명령 프롬프트에서

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. 바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 실행 하면 됩니다.
4. Hello 클릭 **자격 증명 모음 등록** 탭 합니다.
5. Hello 포털에서 새 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Hello 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.  
7. 관리자 PowerShell 명령 창을 엽니다.
8. Hello 다음 명령을 실행 합니다.
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>구성 서버 서비스 해제
구성 서버를 서비스 해제를 시작 하기 전에 hello 다음을 확인 합니다.
1. 이 구성 서버 아래의 모든 가상 컴퓨터에 대한 보호를 사용하지 않도록 설정합니다.
2. 모든 복제 정책을 hello 구성 서버에서에서 연결이 해제 됩니다.
3. Vcenter 서버/vSphere 있는 모든 호스트에 연결 된 toohello 구성 서버를 삭제 합니다.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Azure 포털에서 구성 서버 hello를 삭제 합니다.
1. Azure 포털에서 찾아보기 너무**사이트 복구 인프라** > **구성 서버** hello 자격 증명 모음의 메뉴에서 합니다.
2. Hello toodecommission 구성 서버를 클릭 합니다.
3. Hello 구성 서버 세부 정보 페이지에서 hello 삭제 단추를 클릭 합니다.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. 클릭 **예** hello 서버의 tooconfirm hello 삭제 합니다.

  >[!WARNING]
  모든 가상 컴퓨터, 복제 정책 또는 vCenter 서버/vSphere 호스트가 구성 서버와 연결 된 경우 hello 서버를 삭제할 수 없습니다. Toodelete hello 자격 증명 모음을 시도 하기 전에 이러한 엔터티를 삭제 합니다.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Hello 구성 서버 소프트웨어와 그 종속성 제거
  > [!TIP]
  Tooreuse hello Azure Site Recovery와 구성 서버를 다시 계획 하는 경우를 건너뛸 수 있습니다 toostep 4 직접

1. 관리자 권한으로 toohello 구성 서버에 로그온 합니다.
2. 제어판 > 프로그램 > 프로그램 제거 열기
3. 시퀀스를 수행 하는 hello의 hello 프로그램을 제거 합니다.
  * Microsoft Azure Recovery Services 에이전트
  * Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버
  * Microsoft Azure Site Recovery 공급자
  * Microsoft Azure Site Recovery 구성 서버/프로세스 서버
  * Microsoft Azure Site Recovery 구성 서버 종속성
  * MySQL Server 5.5
4. 다음에서 명령을 hello 및 관리자 명령 프롬프트를 실행 합니다.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>구성 서버 SSL(Secure Socket Layer) 인증서 갱신
hello 구성 서버에는 기본 제공된 웹 서버, 프로세스 서버 hello 모바일 서비스의 활동을 hello를 오케스트레이션 하는 및 마스터 대상 서버가 toohello 구성 서버를 연결 합니다. hello 구성 서버의 웹 서버 SSL 인증서 tooauthenticate 여기에 클라이언트를 사용합니다. 이 인증서 만료 3 년 개이고 메서드 뒤 hello를 사용 하 여 언제 든 갱신할 수 있습니다.

> [!WARNING]
인증서 만료는 버전 9.4.XXXX.X 이상에서만 수행할 수 있습니다. 모든 hello Azure Site Recovery 구성 요소 (구성 서버, 프로세스 서버, 마스터 대상 서버, 모바일 서비스)를 업그레이드 전에 hello 인증서 갱신 워크플로 시작 합니다.

1. Azure 포털 hello, 자격 증명 모음 tooyour 찾아보기 > 사이트 복구 인프라 > 구성 서버입니다.
2. 클릭 toorenew 필요한 hello 구성 서버 hello에 대 한 SSL 인증서입니다.
3. Hello 구성 서버 상태에서 hello SSL 인증서에 대 한 hello 만료 날짜를 확인할 수 있습니다.
4. Hello를 클릭 하 여 hello 인증서 갱신 **인증서 갱신** hello 다음 이미지와 같이 작업:

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>보안 소켓 계층 인증서 만료 경고

> [!NOTE]
hello 2016 년 5 월 이전에 발생 하는 모든 설치에 대 한 SSL 인증서의 유효 기간 설정 된 tooone 연도입니다. hello Azure 포털에에서 표시 하는 인증서 만료 알림 보기를 시작 했습니다.

1. Hello 구성 서버 SSL 인증서를 송신 경우 hello에 tooexpire 향후 2 개월 이내, hello Azure 포털 및 전자 메일 (구독 toobe tooAzure Site Recovery 알림 필요)를 통해 사용자에 게 알리는 hello 서비스가 시작 됩니다. 먼저 hello 자격 증명 모음의 리소스 페이지에 알림 배너를 표시 합니다.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Hello 배너 tooget hello 인증서 만료 시 추가 정보를 클릭 합니다.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  **지금 갱신** 단추 대신 **지금 업그레이드** 단추가 표시됩니다. 이 일부 구성 요소는 사용자 환경에서 아직 않은 업그레이드 된 too9.4.xxxx.x 또는 더 높은 버전을 의미 합니다.

## <a name="sizing-requirements-for-a-configuration-server"></a>구성 서버에 대한 크기 조정 요구 사항

| **CPU** | **메모리** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- | --- |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) |16GB |300GB |500GB 이하 |100대 미만의 컴퓨터를 복제합니다. |
| 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) |18GB |600GB |500GB too1 TB |100-150대 컴퓨터를 복제합니다. |
| 16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz) |32GB |1TB |1TB too2 TB |150-200대 컴퓨터를 복제합니다. |

  >[!TIP]
  일별 데이터 변동을 프로그램 2TB를 초과 하거나 tooreplicate 200 개 이상의 가상 컴퓨터를 계획, toodeploy 추가 프로세스 서버 tooload hello 복제 트래픽은 분산 좋습니다. 어떻게 toodeploy 확장 프로세스 서버에 대해 자세히 알아보기


## <a name="common-issues"></a>일반적인 문제
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
