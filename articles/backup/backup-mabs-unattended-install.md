---
title: "Azure 백업 서버 v 2의 aaaSilent 설치 | Microsoft Docs"
description: "Azure 백업 서버 v 2를 설치 하는 PowerShell 스크립트 toosilently 사용 합니다. 이런 종류의 설치를 무인 설치라고도 합니다."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Azure Backup Server v2의 무인 설치 실행

자세한 내용은 방법 toorun Azure 백업 서버 v 2의 무인된 설치 합니다. 

Azure Backup Server v1을 설치할 경우에는 이러한 단계가 적용되지 않습니다.

## <a name="install-backup-server-v2"></a>Backup Server v2 설치

1. Azure 백업 서버 v 2를 호스팅하는 hello 서버에서 텍스트 파일을 만듭니다. (만들 수 있습니다 hello 파일 메모장 또는 다른 텍스트 편집기.) MABSSetup.ini로 hello 파일을 저장 합니다. 

2. Hello를 hello MABSSetup.ini 파일에서 코드 다음에 붙여 넣습니다. Hello 대괄호 hello 텍스트 바꾸기 (\< \>)를 사용자 환경 값으로. hello 텍스트 다음은 예입니다.

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Hello 파일을 저장 합니다. 그런 다음 hello 설치 서버에서 관리자 권한 명령 프롬프트를에서이 명령을 입력 합니다.

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Hello 설치에 대 한 이러한 플래그를 사용할 수 있습니다.</br>
**/f**: .ini 파일 경로</br>
**/l**: 로그 경로</br>
**/i**: 설치 경로</br>
**/x**: 제거 경로</br>

## <a name="next-steps"></a>다음 단계
백업 서버를 설치한 후에 대해 알아봅니다 어떻게 tooprepare 서버의 작업 보호를 시작 또는 합니다.

- [Backup Server 워크로드 준비](backup-azure-microsoft-azure-backup.md)
- [백업 서버 tooback VMware 서버를 사용 하 여](backup-azure-backup-server-vmware.md)
- [SQL Server를 tooback 백업 서버를 사용 하 여](backup-azure-sql-mabs.md)
- [최신 백업 저장소 tooBackup 서버 추가](backup-mabs-add-storage.md)
