---
title: " Azure Site Recovery에서 확장 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooset 및 Azure 사이트 복구에서 확장 프로세스 서버를 관리 합니다."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>확장 프로세스 서버 관리

확장 프로세스 서버 hello Site Recovery 서비스와 온-프레미스 인프라 간의 데이터 전송을 위해 코디네이터로 작동합니다. 이 문서에서는 확장 프로세스 서버를 설정, 구성 및 관리하는 방법을 설명합니다.

## <a name="prerequisites"></a>필수 조건
hello 하드웨어, 소프트웨어 및 네트워크 구성이 필요 tooset 확장 프로세스 서버를 권장 하는 hello 다음과가 같습니다.

> [!NOTE]
> [용량 계획](site-recovery-capacity-planner.md) 배포 하는 hello 확장 프로세스 서버와 구성 도구 모음의 해당 하는 중요 한 단계 tooensure는 로드 요구 합니다. [확장 프로세스 서버에 대한 특성 크기 조정](#sizing-requirements-for-a-configuration-server)에 대해 자세히 알아봅니다.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Hello 확장 프로세스 서버 소프트웨어를 다운로드합니다.
1. Azure 포털 및 찾아보기 tooyour 복구 서비스 자격 증명 모음 toohello에 로그온 합니다.
2. 너무 찾아보기**사이트 복구 인프라** > **구성 서버** (아래에 대 한 VMware & 물리적 컴퓨터의 경우).
3. 아래로 hello 구성 서버 세부 정보 페이지에 구성 서버 toodrill를 선택 합니다.
4. Hello 클릭 **+ 프로세스 서버** 단추입니다.
5. Hello에 **추가 프로세스 서버** 페이지에서 **프로세스 서버를 확장 배포 온-프레미스** hello에서 옵션 **저장할 toodeploy 프로세스 서버 선택** 드롭 다운 합니다.

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Hello 클릭 **다운로드 hello Microsoft Azure Site Recovery 통합 설치** 링크 toodownload hello hello 확장 프로세스 서버 설치의 최신 버전입니다.

  > [!WARNING]
  hello 확장 프로세스 서버 버전이 같아야 tooor 사용자 환경에서 실행 하는 hello 구성 서버 버전 보다 낮습니다. 간단한 방법을 tooensure 버전 호환성은 toouse 최근에 사용 하 여 tooinstall/업데이트 구성 서버에 동일한 설치 관리자 비트 hello 합니다.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>GUI에서 확장 프로세스 서버 설치 및 등록
원본 컴퓨터를 200 개 초과 배포 아웃 tooscale 했거나 총 매일 변동 비율로 2 테라바이트 이상 경우 추가 프로세스 서버 toohandle hello 트래픽 볼륨을 해야 합니다.

Hello 확인 [크기 프로세스 서버에 대 한 권장 사항](#size-recommendations-for-the-process-server), 한 다음 이러한 지침 tooset hello 프로세스 서버를 따릅니다. 마이그레이션한 원본 컴퓨터 toouse hello 서버를 설정한 후 것입니다.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>명령줄을 사용하여 확장 프로세스 서버 설치 및 등록

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>샘플 사용
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>확장 프로세스 서버 설치 관리자 명령줄 인수
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>프록시 설정 구성 파일 만들기
ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다. 다음 서식을 지정 하 고 입력된 ProxySettingsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 파일을 만듭니다.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>확장 프로세스 서버에 대한 프록시 설정 수정
1. 확장 프로세스 서버에 로그인합니다.
2. 관리자 PowerShell 명령 창을 엽니다.
3. Hello 다음 명령을 실행 합니다.
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. 그런 다음 toohello 디렉터리 찾아보기 **%PROGRAMDATA%\ASR\Agent** 다음 명령이 실행된 하는 hello 및
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>확장 프로세스 서버 다시 등록
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* 그런 다음 관리자 명령 프롬프트를 엽니다.
* Toohello 디렉터리 찾아보기 **%PROGRAMDATA%\ASR\Agent** hello 명령을 실행 하 고

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>확장 프로세스 서버 업그레이드
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>확장 프로세스 서버 서비스 해제
1. 다음 사항을 확인합니다.
  - 구성 서버의 연결 상태 표시 **연결 됨** hello Azure 포털에서
  - 프로세스 서버 hello 구성 서버와 여전히 수 toocommunicate 됩니다.
2. 관리자 권한으로 toohello 프로세스 서버에 로그인
3. 제어판 > 프로그램 > 프로그램 제거 열기
4. Hello 시퀀스 지정 된 다음에 hello 프로그램을 제거 합니다.
  * Microsoft Azure Site Recovery 구성 서버/프로세스 서버
  * Microsoft Azure Site Recovery 구성 서버 종속성
  * Microsoft Azure Recovery Services 에이전트

Hello Azure 포털에서에서 hello 프로세스 서버 삭제 tooreflect 위쪽 too15 분 걸릴 수 있습니다.

  > [!NOTE]
  Hello 프로세스 서버가 구성 서버 hello로 없습니다 toocommunicate 인지 (포털에 대 한 연결 상태가 Disconnected)를 toofollow 필요 hello 단계 toopurge 다음 그 hello 구성 서버에서에서 합니다.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>구성 서버에서 연결이 끊긴 확장 프로세스 서버 등록 취소

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>확장 프로세스 서버에 대한 크기 조정 요구 사항

| **추가 프로세스 서버** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- |
|4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB 메모리 |300GB |250GB 이하 |85대 이하의 컴퓨터를 복제합니다. |
|8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB 메모리 |600GB |250GB too1 TB |85-150대 컴퓨터를 복제합니다. |
|12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB 메모리 |1TB |1TB too2 TB |150-225대 컴퓨터를 복제합니다. |
