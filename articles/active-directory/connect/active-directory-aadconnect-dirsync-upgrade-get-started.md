---
title: "Azure AD Connect: DirSync에서 업그레이드 | Microsoft Docs"
description: "자세한 방법을 DirSync tooAzure AD에서에서 tooupgrade 연결 합니다. 이 문서에서는 AD Connect 디렉터리 동기화 tooAzure에서 업그레이드 하기 위한 hello 단계를 설명 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: DirSync에서 업그레이드
Azure AD Connect hello 후속 tooDirSync입니다. 알게 hello 방법으로이 항목의 디렉터리 동기화에서 업그레이드할 수 있습니다. 다음 단계는 Azure AD Connect의 다른 버전 또는 Azure AD Sync에서 업그레이드하는 경우에 작동하지 않습니다.

Azure AD Connect 설치를 시작 하기 전에 있어야 너무[Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771) 및 전체 hello 필수 단계를 [Azure AD Connect: 하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다. 특히, 이러한 영역 DirSync에서 다르기 때문 hello 다음에 대 한 tooread를 보겠습니다.

* 필요한 버전의.Net 및 PowerShell hello입니다. 최신 버전은 디렉터리 동기화의 필요한 보다 hello 서버에 필요한 toobe입니다.
* hello 프록시 서버 구성입니다. 프록시 서버 tooreach를 사용 하는 경우 인터넷 hello, 업그레이드 하기 전에이 설정을 구성 해야 합니다. 디렉터리 동기화를 설치 하는 hello 사용자에 대해 구성 된 hello 프록시 서버를 항상 사용 하지만 Azure AD Connect 사용 하 여 컴퓨터 설정 대신 합니다.
* hello Url 필요한 toobe hello 프록시 서버에서 엽니다. 기본 시나리오의 경우 디렉터리 동기화를 통해서도 한 시나리오에 대 한 hello 요구 사항은 동일 hello으로 사용 합니다. 원하는 toouse Azure AD Connect에 포함 된 hello 새로운 기능 몇 가지 새 Url은 열어야 합니다.

> [!NOTE]
> 에 새 Azure AD Connect 서버 toostart 동기화 중 변경 내용을 tooAzure AD 활성화 하지 롤백해야 toousing DirSync 또는 Azure AD Sync 합니다. 디렉터리 동기화 및 Azure AD Sync를 포함 하 여 Azure AD Connect toolegacy 클라이언트에서 다운 그레이드는 지원 되지 않으며 tooissues 데이터 손실 등 Azure AD에서 발생할 수 있습니다.

DirSync에서 업그레이드하지 않는 경우 다른 시나리오에 대한 [관련 설명서](#related-documentation) 를 참조하세요.

## <a name="upgrade-from-dirsync"></a>DirSync에서 업그레이드
현재 디렉터리 동기화 배포에 따라 가지 hello 업그레이드에 대 한 다른 옵션이 있습니다. Hello 업그레이드 시간은 3 시간 미만으로 예상 된다면 hello 권장은 toodo 전체 업그레이드 합니다. Hello 업그레이드 시간은 3 시간 이상으로 예상 된다면 hello 권장 사항 toodo 다른 서버에 대 한 병렬 배포 됩니다. 50, 000 개 이상의 개체가 있는 경우 걸린다는 점을 toodo hello 업그레이드 3 시간 이상 예상 됩니다.

| 시나리오 |
| --- | --- |
| [전체 업그레이드](#in-place-upgrade) |
| [병렬 배포](#parallel-deployment) |

> [!NOTE]
> 디렉터리 동기화 tooAzure AD에서에서 tooupgrade를 계획 하는 경우 연결을 제거 하지 않으면 디렉터리 동기화 직접 hello 업그레이드 하기 전에. Azure AD Connect 및 DirSync에서 hello 구성을 마이그레이션할 읽고 hello 서버를 검사 한 후 제거.

**전체 업그레이드**  
hello 예상 시간 toocomplete hello 업그레이드 hello 마법사가 표시 됩니다. 이 예상치는 hello 가정 하는 데 걸리는 3 시간 toocomplete (사용자, 연락처 및 그룹)의 개체를 50, 000을 사용 하 여 데이터베이스에 대 한 업그레이드를 기반으로 합니다. Hello 데이터베이스의에서 개체 수가 50, 000 보다 작은 경우, Azure AD Connect의 전체 업그레이드가 권장 합니다. Toocontinue 결정 한 경우 현재 설정을 자동으로 업그레이드 하는 동안 적용 됩니다 및 서버에 현재 동기화를 자동으로 다시 시작 합니다.

원하는 구성 마이그레이션을 toodo 병렬 배포를 수행 하는 경우 hello 내부 업그레이드 권장 사항을 재정의할 수 있습니다. 예를 들어 hello 기회 toorefresh hello 하드웨어 및 운영 체제 걸릴 수 있습니다. 자세한 내용은 참조 hello [배포 병렬](#parallel-deployment) 섹션.

**병렬 배포**  
50,000개 이상의 개체가 있는 경우 병렬 배포를 사용하는 것이 좋습니다. 이 배포는 사용자에게 운영 지연이 발생하지 않도록 방지합니다. Azure AD Connect 설치 hello hello 업그레이드에 대 한 tooestimate hello 가동 중지 시간 하지만 자신의 경험 가능성이 toobe hello 최선의 가이드는 hello 이전에 DirSync를 업그레이드 한, 경우.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>지원 되는 디렉터리 동기화 구성 toobe 업그레이드
hello 구성 변경 내용을 다음 업그레이드 된 DirSync로 지원 됩니다.

* 도메인 및 OU 필터링
* 대체 ID(UPN)
* 암호 동기화 및 Exchange 하이브리드 설정
* 포리스트/도메인 및 Azure AD 설정
* 사용자 특성에 기반하여 필터링

변경 하는 hello는 업그레이드할 수 없습니다. 이 구성을 사용할 경우 hello 업그레이드가 차단 됩니다.

* 지원되지 않는 DirSync 변경 내용, 예: 제거된 특성 및 사용자 지정 확장 DLL 사용

![업그레이드 차단](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

이러한 경우에 hello 권장 tooinstall 새 Azure AD Connect의 서버인 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode) 확인 hello 이전 디렉터리 동기화 및 새 Azure AD Connect 구성 합니다. [Azure AD Connect 동기화 사용자 지정 구성](active-directory-aadconnectsync-whatis.md)에서 설명한 대로 사용자 지정 구성을 사용하여 변경 내용을 다시 적용합니다.

hello 서비스 계정에 DirSync에 의해 사용 되는 hello 암호를 검색할 수 없습니다 및 마이그레이션되지 않습니다. Hello 업그레이드 하는 동안 이러한 암호 다시 설정 됩니다.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>AD Connect 디렉터리 동기화 tooAzure에서 업그레이드 하기 위한 개략적인 단계
1. 시작 tooAzure AD 연결
2. 현재 DirSync 구성 분석
3. Azure AD 전역 관리자 암호 수집
4. (Azure AD Connect의 hello 설치 중에 사용)만 엔터프라이즈 관리자 계정에 대 한 자격 증명을 수집 합니다.
5. Azure AD Connect 설치
   * DirSync 제거(또는 일시적으로 사용 안 함)
   * Azure AD Connect 설치
   * (선택 사항) 동기화 시작

다음과 같은 경우에 추가 단계가 필요합니다.

* 현재 로컬 또는 원격으로 전체 SQL Server를 사용 중임
* 동기화 범위에 50,000개가 넘는 개체가 있음

## <a name="in-place-upgrade"></a>전체 업그레이드
1. Hello Azure AD Connect installer (MSI)를 시작 합니다.
2. 검토 하 고 toolicense 약관 및 개인 정보 취급 방침을 동의 해야 합니다.  
   ![TooAzure AD 시작](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. 기존 DirSync 설치의 다음 toobegin 분석을 클릭 합니다.  
   ![기존 디렉터리 동기화 설치 분석](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. 방법에 hello 권장 사항을 참조 하십시오 hello 분석 완료 되 면 tooproceed 합니다.  
   * SQL Server Express를 사용 하 고 개체 50, 000 보다 작은 경우 hello 다음 화면이 표시 됩니다.  
     ![분석이 완료 준비 tooupgrade DirSync에서](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * DirSync에 전체 SQL Server를 사용하는 경우 대신 다음 페이지가 표시됩니다.  
     ![분석이 완료 준비 tooupgrade DirSync에서](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     hello 기존 SQL Server 데이터베이스 서버 관련 디렉터리 동기화에서 사용 하 고 hello 정보가 표시 됩니다. 필요한 경우 적절하게 조정합니다. 클릭 **다음** toocontinue hello 설치 합니다.
   * 50,000개 이상의 개체가 있는 경우 대신 다음 화면이 표시됩니다.  
     ![분석이 완료 준비 tooupgrade DirSync에서](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     현재 위치 업그레이드를 하면 tooproceed hello 확인란 다음 toothis 메시지를 클릭 합니다.: **계속이 컴퓨터에 DirSync를 업그레이드 합니다.**
     toodo는 [배포 병렬](#parallel-deployment) 대신 hello 디렉터리 동기화 구성 설정 내보내기 및 hello 구성 toohello 새 서버를 이동 합니다.
5. 현재 tooconnect tooAzure AD를 사용 하는 hello 계정에 대 한 hello 암호를 제공 합니다. 현재 디렉터리 동기화를 사용 하는 hello 계정 이어야 합니다.  
   ![Azure AD 자격 증명 입력](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   오류가 발생하고 연결에 문제가 있는 경우 [연결 문제 해결](active-directory-aadconnect-troubleshoot-connectivity.md)을 참조하세요.
6. Active Directory에 대한 엔터프라이즈 관리자 계정을 지정합니다.  
   ![ADDS 자격 증명 입력](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. 이제 준비 tooconfigure 것입니다. **업그레이드**를 클릭하면 DirSync가 제거되고 Azure AD Connect가 구성되어 동기화를 시작합니다.  
   ![준비 tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Hello 설치가 완료 되 면 로그 아웃 한 동기화 규칙 편집기 동기화 서비스 관리자를 사용 하거나 toomake 다른 구성 변경을 시도 하기 전에 다시 tooWindows에 로그인 합니다.

## <a name="parallel-deployment"></a>병렬 배포
### <a name="export-hello-dirsync-configuration"></a>Hello 디렉터리 동기화 구성 내보내기
**50,000개 이상의 개체를 가진 병렬 배포**

50, 000 개 이상의 개체를 다음 hello 경우 Azure AD Connect 설치 병렬 배포를 권장 합니다.

화면 비슷한 toohello 다음 표시 됩니다.  
![분석 완료](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

병렬 배포와 tooproceed 하려는 경우 tooperform hello 단계를 수행 해야 합니다.

* Hello 클릭 **설정 내보내기** 단추입니다. 별도 서버에 Azure AD Connect를 설치 하는 경우 이러한 설정은 현재 DirSync tooyour 새 Azure AD Connect 설치에서 마이그레이션됩니다.

설정을 성공적으로 내보낸 후 hello DirSync 서버 hello Azure AD Connect 마법사를 종료할 수 있습니다. 너무 hello 다음 단계를 계속[별도 서버에 Azure AD Connect를 설치 합니다.](#installation-of-azure-ad-connect-on-separate-server)

**50,000개 미만의 개체를 가진 병렬 배포**

개체 50, 000 보다 작은 toodo 병렬 배포를 사용할 수 있지만 다음 않습니다 hello 다음:

1. Hello Azure AD Connect 설치 (MSI) 실행 합니다.
2. Hello 표시 되 면 **시작 tooAzure AD Connect** 화면 hello 창의 hello 맨 위 오른쪽 모서리에서 hello "X"를 클릭 하 여 hello 설치 마법사를 종료 합니다.
3. 명령 프롬프트를 엽니다.
4. Hello에서 Azure AD Connect의 위치를 설치 (기본값: C:\Program Files\Microsoft Azure Active Directory Connect) hello 다음 명령을 실행: `AzureADConnect.exe /ForceExport`합니다.
5. Hello 클릭 **설정 내보내기** 단추입니다. 별도 서버에 Azure AD Connect를 설치 하는 경우 이러한 설정은 현재 DirSync tooyour 새 Azure AD Connect 설치에서 마이그레이션됩니다.

![분석 완료](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

설정을 성공적으로 내보낸 후 hello DirSync 서버 hello Azure AD Connect 마법사를 종료할 수 있습니다. 너무 hello 다음 단계를 계속[별도 서버에 Azure AD Connect 설치](#installation-of-azure-ad-connect-on-separate-server)합니다.

### <a name="install-azure-ad-connect-on-separate-server"></a>별도 서버에 Azure AD Connect 설치
새 서버에 Azure AD Connect를 설치 하면 hello 가정 tooperform Azure AD Connect의 새로 설치를 지정 하는입니다. Toouse hello DirSync 구성을 지정할 것 이므로 몇 가지 추가 단계 tootake 가지가 있습니다.

1. Hello Azure AD Connect 설치 (MSI) 실행 합니다.
2. Hello 표시 되 면 **시작 tooAzure AD Connect** 화면 hello 창의 hello 맨 위 오른쪽 모서리에서 hello "X"를 클릭 하 여 hello 설치 마법사를 종료 합니다.
3. 명령 프롬프트를 엽니다.
4. Hello에서 Azure AD Connect의 위치를 설치 (기본값: C:\Program Files\Microsoft Azure Active Directory Connect) hello 다음 명령을 실행: `AzureADConnect.exe /migrate`합니다.
   시작 하 고 하는 hello 화면에 다음을 제공 하는 hello Azure AD Connect 설치 마법사:  
   ![Azure AD 자격 증명 입력](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. DirSync 설치에서 내보낸 hello 설정 파일을 선택 합니다.
6. 다음을 포함한 고급 옵션을 구성합니다.
   * Azure AD Connect에 대한 사용자 지정 설치 위치
   * 기존 SQL Server 인스턴스(기본값: Azure AD Connect는 SQL Server 2012 Express를 설치함) Hello를 사용 하지 않는 디렉터리 동기화 서버와 동일한 데이터베이스 인스턴스에 있습니다.
   * 서비스 계정 (SQL Server 데이터베이스인 경우 원격이 계정에 도메인 서비스 계정 이어야 합니다.) tooconnect tooSQL 서버를 사용 합니다.
     이러한 옵션은 이 화면에서 볼 수 있습니다.  
     ![Azure AD 자격 증명 입력](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. **다음**을 누릅니다.
8. Hello에 **준비 tooconfigure** 페이지에서 hello **hello 구성이 완료 되는 즉시 hello 동기화 프로세스를 시작** 확인 합니다. hello 서버는 이제 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode) 되므로 변경 내용이 내보낸된 tooAzure AD 하지 않습니다.
9. **Install**을 클릭합니다.
10. Hello 설치가 완료 되 면 로그 아웃 한 동기화 규칙 편집기 동기화 서비스 관리자를 사용 하거나 toomake 다른 구성 변경을 시도 하기 전에 다시 tooWindows에 로그인 합니다.

> [!NOTE]
> Windows Server Active Directory와 Azure Active Directory 간의 동기화를 시작 하지만 변경이 내보낸된 tooAzure AD 합니다. 하나의 동기화 도구만이 변경 내용을 한 번에 내보낼 수 있습니다. 이 상태를 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)라고 합니다.

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Azure AD Connect 동기화 준비 toobegin 인지 확인
Azure AD Connect 디렉터리 동기화를 통해 준비 tootake 되 tooverify, 해야 tooopen **동기화 서비스 관리자** hello 그룹에서 **Azure AD Connect** hello 시작 메뉴에서 합니다.

Hello 응용 프로그램에서 이동 toohello **작업** 탭 합니다. 이 탭에서 작업을 다음 해당 hello 완료를 확인 합니다.

* Hello AD 커넥터에서 가져오기
* Hello Azure AD 커넥터에서 가져오기
* Hello AD 커넥터에서 전체 동기화
* Hello Azure AD 커넥터에서 전체 동기화

![가져오기 및 동기화 완료](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

이러한 작업에서 hello 결과 검토 하 고 오류가 없는지 확인 합니다.

원하는 toosee 내보낸 toobe tooAzure AD에 대 한 된 hello 변경 내용을 검사 하는 경우 다음 읽을 어떻게 tooverify hello에 속하는 구성 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)합니다. 예상하지 못한 것이 나타나지 않을 때까지 필요한 구성을 변경합니다.

디렉터리 동기화 tooAzure 이러한 단계를 완료 하 고 hello 결과에 만족 하는 AD에서에서 준비 tooswitch 됩니다.

### <a name="uninstall-dirsync-old-server"></a>DirSync 제거(이전 서버)
* **프로그램 및 기능**에서 **Microsoft Azure Active Directory 동기화 도구** 찾기
* **Microsoft Azure Active Directory 동기화 도구**
* hello 제거 too15 분 toocomplete 걸릴 수도 있습니다.

나중 toouninstall DirSync를 선호 하는 경우 또한 일시적으로 hello 서버를 종료 하거나 hello 서비스를 사용 하지 않도록 설정할 수 있습니다. 이 메서드 toore 사용은 문제가 발생할 경우 있습니다 것입니다. 그러나는 대신이 필요 하지 않습니다 되므로 해당 hello 다음 단계가 실패 합니다.

디렉터리 동기화 비활성화 또는 제거 tooAzure AD 내보내기 활성 서버가 됩니다. hello 다음 단계 tooenable Azure AD Connect는 온-프레미스 Active Directory에 변경 내용을 동기화 toobe tooAzure AD를 계속 하기 전에 완료 되어야 합니다.

### <a name="enable-azure-ad-connect-new-server"></a>Azure AD Connect 사용(새 서버)
Azure AD를 닫은 후 연결, 설치 후 추가 구성 변경 내용이 toomake를 허용 합니다. 시작 **Azure AD Connect** hello 바탕 화면에서 바로 가기 hello 또는 hello 시작 메뉴에서 합니다. Toorun hello MSI 다시 설치 하지 마십시오 있는지 확인 합니다.

Hello 다음을 표시 되어야 합니다.  
![추가 작업](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* **준비 모드 구성**을 선택합니다.
* 선택을 취소 hello로 준비 하지 않으려면 **사용 준비 모드** 확인란을 선택 합니다.

![Azure AD 자격 증명 입력](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Hello 클릭 **다음** 단추
* Hello 확인 페이지에서 클릭 hello **설치** 단추입니다.

Azure AD Connect은 현재 활성 서버 하 고 하지 전환 해야 백 toousing 기존 DirSync 서버 키를 누릅니다.

## <a name="next-steps"></a>다음 단계
Azure AD Connect를 설치 했으므로 다음을 할 수 있습니다 [hello 설치 되었는지 확인 하 고 라이선스를 할당](active-directory-aadconnect-whats-next.md)합니다.

Hello 설치를 사용 하도록 설정 된 이러한 새 기능에 대 한 자세한 정보: [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md), [실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), 및 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)합니다.

이러한 공통 항목에 대 한 자세한 정보: [스케줄러와 tootrigger 동기화 방법을](active-directory-aadconnectsync-feature-scheduler.md)합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
