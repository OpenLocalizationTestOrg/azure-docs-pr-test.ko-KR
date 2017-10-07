---
title: "Azure AD Connect: 어떻게 10GB LocalDB에서 toorecover 제한 문제 | Microsoft Docs"
description: "이 항목에서는 방법을 toorecover Azure AD Connect 동기화 서비스 LocalDB 10GB를 발견 한 경우 설명 문제를 제한 합니다."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: 어떻게 toorecover LocalDB 10GB 제한에서
Azure AD Connect SQL Server 데이터베이스 toostore id 데이터를 필요합니다. Hello 기본 Azure AD Connect와 함께 설치 된 SQL Server 2012 Express LocalDB를 사용 하거나 사용자 고유의 전체 SQL을 사용 하 여 수 있습니다. SQL Server Express는 10GB 크기 제한을 적용합니다. LocalDB를 사용하고 이 제한에 도달하는 경우 Azure AD Connect 동기화 서비스는 더 이상 제대로 시작하거나 동기화할 수 없습니다. 이 문서는 hello 복구 단계를 제공합니다.

## <a name="symptoms"></a>증상
두 가지 일반적인 증상이 있습니다.

* Azure AD Connect 동기화 Service **실행 되 고** 하지만 실패와 toosynchronize *"중지 됨-데이터베이스-디스크-full"을* 오류입니다.

* Azure AD Connect 동기화 Service **가 없습니다 toostart**합니다. 6323 이벤트 및 오류 메시지와 함께 실패 toostart hello 서비스를 만들려고 하면 *"hello 서버 오류가 발생 했습니다 SQL Server 디스크 공간이 부족 하기 때문에."*

## <a name="short-term-recovery-steps"></a>단기 복구 단계
이 섹션에서는 Azure AD Connect 동기화 Service tooresume 작업에 필요한 hello 단계 tooreclaim DB 공간을 제공 합니다. hello 단계는 다음과 같습니다.
1. [Hello 동기화 서비스 상태 확인](#determine-the-synchronization-service-status)
2. [Hello 데이터베이스 축소](#shrink-the-database)
3. [실행 기록 데이터 삭제](#delete-run-history-data)
4. [실행 기록 데이터에 대한 보존 기간 단축](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Hello 동기화 서비스 상태 확인
첫째, 여부 여전히 hello 동기화 서비스가 실행 중인지 여부를 결정 합니다.

1. 관리자 권한으로 Azure AD Connect 서버 tooyour에 로그인 합니다.

2. 너무 이동**서비스 제어 관리자**합니다.

3. Hello 상태를 확인 **Microsoft Azure AD Sync**합니다.


4. 실행 중인 경우 중지 하지 않거나 hello 서비스를 다시 시작 합니다. Skip [축소 hello 데이터베이스](#shrink-the-database) 단계를 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다.

5. 실행 되지 않는 경우 toostart hello 서비스를 시도 하십시오. Hello 서비스가 시작 되 면 건너뛸 [축소 hello 데이터베이스](#shrink-the-database) 단계를 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다. 그렇지 않은 경우 계속 [축소 hello 데이터베이스](#shrink-the-database) 단계입니다.

### <a name="shrink-hello-database"></a>Hello 데이터베이스 축소
Hello 축소 작업 toofree 충분 한 DB 공간 toostart hello 동기화 서비스를 사용 합니다. Hello 데이터베이스에 있는 공백이 제거 하 여 DB 공간을 확보 합니다. 항상 공백을 복구할 수 있다고 보장되지 않으므로 이 단계가 최선적입니다. 이 문서를 참조 하는 축소 작업에 대해 자세히 toolearn [데이터베이스 축소](https://msdn.microsoft.com/library/ms189035.aspx)합니다.

> [!IMPORTANT]
> 동기화 서비스 toorun hello를 얻을 수 있는 경우이 단계를 건너뜁니다. Tooincreased 조각화 인해 toopoor 성능 시킬 수 있으므로 tooshrink hello SQL DB 하지 좋습니다.

hello Azure AD Connect에 대 한 생성 hello 데이터베이스 이름이 **ADSync**합니다. tooperform 축소 작업으로 hello sysadmin 또는 hello 데이터베이스의 DBO에 로그인 해야 합니다. Azure AD Connect 설치 하는 동안 다음 계정 hello sysadmin 권한이 부여 됩니다.
* 로컬 관리자
* 사용 되는 toorun Azure AD Connect 설치 했던 hello 사용자 계정입니다.
* Azure AD 동기화 서비스 연결의 컨텍스트를 운영 하는 hello로 사용 되는 동기화 서비스 계정 번호입니다.
* hello 로컬 설치 중에 만들어진 ADSyncAdmins 그룹입니다.

1. 복사 하 여 hello 데이터베이스를 백업 **ADSync.mdf** 및 **ADSync_log.ldf** 아래에 있는 파일 `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa 안전한 위치입니다.

2. 새 PowerShell 세션을 시작합니다.

3. Toofolder 이동 `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`합니다.

4. 시작 **sqlcmd** hello 명령을 실행 하 여 유틸리티 `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`sysadmin의 hello 자격 증명을 사용 하 여, 또는 데이터베이스 DBO hello 합니다.

5. hello sqlcmd 프롬프트 tooshrink hello 데이터베이스 (1 >)를 입력 `DBCC Shrinkdatabase(ADSync,1);`옵니다 `GO` hello 다음 줄에 있습니다.

6. Hello 작업이 성공한 경우 toostart hello 동기화 서비스를 다시 시도 합니다. Hello 동기화 서비스를 시작할 수 있으면 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다. 그렇지 않은 경우 고객 지원으로 문의하세요.

### <a name="delete-run-history-data"></a>실행 기록 데이터 삭제
기본적으로 Azure AD Connect tooseven 일 분량의 실행된 기록 데이터를 유지합니다. 이 단계에서는 Azure AD Connect 동기화 Service 동기화를 다시 시작할 수 있도록 기록 데이터 tooreclaim DB 공간을 실행 하는 hello를 삭제 합니다.

1.  시작 **동기화 서비스 관리자** tooSTART → 라인으로 전환 하 여 동기화 서비스입니다.

2.  Toohello 이동 **작업** 탭 합니다.

3.  **Actions** 아래에서 **Clear Runs**를 선택합니다.

4.  **Clear all runs** 또는 **Clear runs before… <date>** 옵션 중에서 선택할 수 있습니다. 2일보다 오래된 실행 기록 데이터를 삭제하여 시작하는 것이 좋습니다. Hello를 눌러 toorun로 만들려면 DB 크기를 계속 진행 **모든 실행 취소** 옵션입니다.

### <a name="shorten-retention-period-for-run-history-data"></a>실행 기록 데이터에 대한 보존 기간 단축
이 단계는 여러 동기화 주기 후 hello 10GB 제한 문제를 일으키지 tooreduce hello 가능성이 있습니다.

1. 새 PowerShell 세션을 엽니다.

2. 실행 `Get-ADSyncScheduler` hello hello 현재 보존 기간을 지정 하는 PurgeRunHistoryInterval 속성을 기록 합니다.

3. 실행 `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset hello 보존 기간 tootwo 일 합니다. 적절 하 게 hello 보존 기간을 조정 합니다.

## <a name="long-term-solution--migrate-toofull-sql"></a>마이그레이션 toofull SQL 등 장기 솔루션
일반적으로 hello 문제는 10GB의 데이터베이스 크기는 더 이상 Azure AD Connect toosynchronize에 대 한 충분 한 온-프레미스 Active Directory tooAzure AD 합니다. Toousing hello 정식 버전의 SQL server 전환 하는 것이 좋습니다. 직접 sql hello 정식 버전의 hello 데이터베이스와 함께 기존 Azure AD Connect 배포의 LocalDB hello을 바꿀 수 없습니다. 대신, SQL의 hello 전체 버전을 사용 하 여 새 Azure AD Connect 서버를 배포 해야 합니다. 수행 하는 회전 마이그레이션 (SQL DB)와 함께 새 Azure AD Connect 서버 hello를 스테이징 서버에 다음 toohello 기존 Azure AD Connect 서버 (LocalDB)으로 배포 하는 것이 좋습니다. 
* 원격 SQL Azure AD Connect로 참조 하는 tooconfigure 방법에 대 한 tooarticle [Azure AD Connect의 사용자 지정 설치](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)합니다.
* Azure AD Connect 업그레이드가 회전 마이그레이션에 대 한 자세한 내용은 참조 tooarticle [Azure AD Connect:는 이전 버전 toohello 최신 버전에서 업그레이드](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration)합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
