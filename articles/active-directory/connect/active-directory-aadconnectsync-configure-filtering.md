---
title: "Azure AD Connect 동기화: 필터링 구성 | Microsoft Docs"
description: "에 대해 설명 방법을 tooconfigure Azure AD Connect 동기화에서 필터링 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect 동기화 구성 필터링
필터링을 사용하여 온-프레미스 디렉터리에서 Azure Active Directory(Azure AD)에 표시할 개체를 제어할 수 있습니다. hello 기본 구성은 구성 하는 hello 포리스트의 모든 도메인에서 모든 개체를 사용합니다. 일반적으로 hello 권장 구성입니다. Exchange Online 및 비즈니스용 Skype 등의 Office 365 워크로드를 사용하면 완전한 전체 주소 목록이 도움이 되므로 모든 사람에게 메일을 보내거나 호출할 수 있습니다. Hello 기본 구성을 사용 하 여 hello 관계 없이 동일한 환경을 Exchange 또는 Lync 온-프레미스 구현 된 것을 갖게 됩니다.

경우에 따라 이라면 필요한 몇 가지 변경 내용이 toohello 기본 구성을 확인 하십시오. 다음은 몇 가지 예입니다.

* Toouse hello 계획 [여러 Azure AD 디렉터리 토폴로지](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant)합니다. 개체는 동기화 된 tooa 특정 Azure AD 디렉터리 필터 toocontrol tooapply가 필요 합니다.
* Azure AD의 사용자 하위 집합만 이용하여 Azure 또는 Office 365에 대한 파일럿을 실행합니다. Hello 소규모 파일럿 것이 중요 한 toohave는 완전 한 전체 주소 목록 toodemonstrate hello 기능 하지 않습니다.
* 많은 서비스 계정과 Azure AD에서 필요 없는 다른 비개인용 계정이 있습니다.
* 규정 준수를 위해 모든 사용자 계정 온-프레미스를 삭제하지 않습니다. 사용하지 않도록 설정하기만 합니다. 하지만 Azure AD에서 원하는 활성 계정을 toobe 존재 합니다.

이 문서에서는 어떻게 tooconfigure hello 다양 한 필터링 방법을 설명 합니다.

> [!IMPORTANT]
> Microsoft는 수정 또는 Azure AD Connect 동기화 공식적으로 문서화 된 hello 작업 외부에서 지원 하지 않습니다. 이러한 동작 중 하나는 Azure AD Connect 동기화의 불일치하거나 지원되지 않는 상태가 될 수 있습니다. 결과적으로, Microsoft는 해당 배포에 대해 기술 지원을 제공할 수 없습니다.

## <a name="basics-and-important-notes"></a>기본 사항 및 중요 참고 사항
Azure AD Connect 동기화에서 언제든지 필터링을 사용할 수 있습니다. 디렉터리 동기화의 기본 구성으로 시작 하 고 필터링을 구성 하는 경우 필터링 된 hello 개체는 더 이상 동기화 된 tooAzure AD입니다. 이 변경으로 인해 Azure AD에서 이전에 동기화되었지만 그 후에 필터링된 개체는 Azure AD에서 삭제됩니다.

변경 내용을 toofiltering 만들기를 시작 하기 전에 확인 하면 [hello 예약 된 작업을 사용 하지 않도록 설정](#disable-scheduled-task) toobe 올바른을 아직 확인 하지 않은 변경 내용을 실수로 하지 내보내면 하므로 합니다.

필터링 hello에 많은 개체를 제거할 수 있으므로 동일한 시간을 원하는 toomake 올바른지 새 필터 내보내기 하나를 시작 하기 전에 AD tooAzure 변경 합니다. Hello 구성 단계를 마친 후 반드시 좋습니다 hello를 따르는 [확인 단계](#apply-and-verify-changes) 전에 내보내고 변경 내용을 tooAzure AD 확인 합니다.

많은 삭제 개체가 실수로 hello tooprotect 기능 "[실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)"는 기본적으로 설정 합니다. 인해 많은 개체를 삭제 하는 경우 toofiltering (기본적으로 500)이 문서 tooallow hello에 toofollow hello 단계를 보려면 tooAzure AD 통해 toogo를 삭제 합니다.

2015 년 11 월 하기 전에 빌드를 사용 하는 경우 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) 변경 tooa 필터 구성을 확인 하 고 암호 동기화를 사용 하 여 hello 구성을 완료 한 후 tootrigger 모든 암호의 전체 동기화 해야 합니다. 암호 tootrigger 전체 동기화 하는 방법에 대 한 단계를 참조 하십시오. [모든 암호의 전체 동기화를 트리거할](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords)합니다. 빌드 1.0.9125에 이거나 이상 버전에서는 일반 hello 다음 **전체 동기화** 암호를 동기화 해야 하는지 여부 및이 추가 단계는 더 이상 필요 하는 경우에 작업 계산 합니다.

경우 **사용자** 필터링 오류로 인해 Azure AD에서 개체를 실수로 삭제, hello 사용자 개체 필터링 구성을 제거 하 여 Azure AD에서 다시 만들 수 있습니다. 그런 다음 디렉터리를 다시 동기화할 수 있습니다. 이 그러면 Azure AD에서 hello 휴지통에서 hello 사용자를 복원합니다. 그러나 다른 개체 형식을 삭제 취소할 수 없습니다. 예를 들어 보안 그룹을 실수로 삭제 되었으며 사용된 tooACL 리소스 hello 그룹 및 해당 Acl 복구할 수 없습니다.

Azure AD Connect만 범위에 toobe로 간주 한 번에 개체를 삭제 합니다. Azure AD의 개체가 다른 동기화 엔진으로 만들어졌으며 이러한 개체가 범위에 없는 경우 필터링을 추가해도 제거되지 않습니다. 예를 들어 Azure AD에 전체 디렉터리의 전체 복사본을 생성 하는 디렉터리 동기화 서버와 시작한 필터링이 hello 시작 부분에서 활성화 된 동시에 새 Azure AD Connect 동기화 서버를 설치 하는 경우 Azure AD Connect 제거 하지 않음 hello 추가 DirSync에 의해 생성 된 개체입니다.

설치 하거나 tooa 최신 버전의 Azure AD Connect 업그레이드 하는 경우 hello 필터링 구성이 보존 됩니다. 해당 항상 hello 구성 하는 모범 사례 tooverify hello 첫 번째 동기화 주기를 실행 하기 전에 새 버전 업그레이드 tooa 후 실수로 변경 되지 않았습니다.

둘 이상의 포리스트에 있는 경우이 항목 tooevery 포리스트에 설명 된 구성을 필터링 hello를 적용 해야 합니다 (동일한 hello를 선택한 경우 모든 대상에 대 한 구성).

### <a name="disable-hello-scheduled-task"></a>Hello 예약 된 작업을 사용 하지 않도록 설정
30 분 마다 동기화 주기를 트리거하는 toodisable hello 기본 제공 스케줄러는 다음이 단계를 따르십시오.

1. Tooa PowerShell 프롬프트를 이동 합니다.
2. 실행 `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable hello 스케줄러입니다.
3. 이 문서에서 설명 하는 hello 변경 내용을 확인 합니다.
4. 실행 `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable hello 스케줄러 다시 합니다.

**Azure AD Connect 1.1.105.0 전 빌드를 사용하는 경우**  
다음이 단계를 수행 하는 3 시간 마다 동기화 주기를 트리거하는 toodisable hello 예약 된 작업:

1. 시작 **작업 스케줄러** hello에서 **시작** 메뉴.
2. 바로 아래 **작업 스케줄러 라이브러리**, 라는 찾기 hello 작업이 **Azure AD Sync Scheduler**를 마우스 오른쪽 단추로 클릭 하 고 선택 **사용 하지 않도록 설정**합니다.  
   ![작업 스케줄러](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. 이제 구성을 변경 하 고 hello에서 hello 동기화 엔진을 수동으로 실행할 수 있습니다 **동기화 서비스 관리자** 콘솔.

변경 내용을 필터링를 마친 후에 다시 toocome 반드시 및 **사용** hello 작업을 다시 합니다.

## <a name="filtering-options"></a>필터링 옵션
Hello toohello 디렉터리 동기화 도구에 대 한 필터링의 구성 유형을 다음 적용할 수 있습니다.

* [**그룹 기반**](#group-based-filtering): 단일 그룹을 기반으로 필터링 구성 될 수 초기 설치 시 hello 설치 마법사를 사용 하 여 합니다.
* [**도메인 기반**](#domain-based-filtering):이 옵션을 사용 하 여 선택할 수 있습니다 어느 도메인 tooAzure AD를 동기화 합니다. 또한 추가 하 고 Azure AD Connect 동기화를 설치한 후 변경 내용을 tooyour 온-프레미스 인프라를 만들면 hello 동기화 엔진 구성에서 도메인을 제거할 수 있습니다.
* [**조직 구성 단위 (OU) – 기반**](#organizational-unitbased-filtering):이 옵션을 사용 하 여 있는 Ou를 선택할 수 있습니다 tooAzure AD를 동기화 합니다. 이 옵션은 선택된 OU의 모든 개체 형식에 대해 설정됩니다.
* [**특성 기반**](#attribute-based-filtering):이 옵션을 사용 하 여 hello 개체에 대 한 특성 값을 기반으로 하는 개체를 필터링 할 수 있습니다. 또한 다른 개체 형식별로 다르게 필터링할 수 있습니다.

여러 대의 필터링 옵션을 사용 하 여 hello에서 같은 시간입니다. OU 기반 필터링을 사용할 수는 예를 들어 tooonly 하나의 OU의 개체를 포함 합니다. At hello 동일 time, 특성 기반 필터링 toofilter hello 개체를 더 이상 사용할 수 있습니다. 여러 대의 필터링 방법을 사용 하는 경우 hello 필터 hello 필터 사이 논리 "AND"를 사용 합니다.

## <a name="domain-based-filtering"></a>도메인 기반 필터링
이 섹션 도메인 필터를 hello 단계 tooconfigure 제공합니다. 를 추가 하거나 Azure AD Connect를 설치 후 포리스트에서 도메인을 제거 하는 경우 tooupdate hello 필터링 구성 해야 합니다.

hello toochange 도메인 기반 필터링 hello 설치 마법사를 실행 하 고 변경 하 여이 방식으로 기본 설정 [도메인 및 OU 필터링](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)합니다. hello 설치 마법사는이 항목에 설명 되어 있는 모든 hello 작업을 자동화 합니다.

어떤 이유로 없습니다 toorun hello 설치 마법사는 경우에 다음이 단계를 수행 해야 합니다.

도메인 기반 필터링 구성은 다음 단계로 구성됩니다.

1. [Hello 도메인 선택](#select-domains-to-be-synchronized) tooinclude hello 동기화에서 되도록 합니다.
2. 각 추가 하 고 도메인 제거를 조정 hello [실행 프로필](#update-run-profiles)합니다.
3. [변경 사항을 적용하고 확인합니다](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>선택 hello 도메인 toobe 동기화
tooset hello 도메인 필터에서 다음 단계 hello지 않습니다.

1. Hello의 구성원 인 계정을 사용 하 여 Azure AD Connect 동기화를 실행 중인 toohello 서버 로그인 **ADSyncAdmins** 보안 그룹입니다.
2. 시작 **동기화 서비스** hello에서 **시작** 메뉴.
3. 선택 **커넥터**, 및 hello **커넥터** 목록에서 hello 형식과 hello 커넥터 **Active Directory 도메인 서비스**합니다. **작업**에서 **속성**을 선택합니다.  
   ![커넥터 속성](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. **디렉터리 파티션 구성**을 클릭합니다.
5. Hello에 **디렉터리 파티션 선택** 목록 선택 하 고 필요에 따라 도메인을 선택 취소 합니다. 원하는 toosynchronize만 hello 파티션을 선택 되어 있는지 확인 합니다.  
   ![파티션](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   사용자 온-프레미스 Active Directory 인프라를 변경 하 고 추가 하거나 hello 포리스트에서 도메인을 제거을 클릭 한 다음 hello **새로 고침** 단추 tooget 업데이트 된 목록입니다. 새로 고칠 때 자격 증명 요청 메시지가 표시됩니다. 읽기 액세스 tooWindows Server Active Directory와 자격 증명을 제공 합니다. Hello 대화 상자에서 미리 채워지는 toobe hello 사용자가 되어 있지 않습니다.  
   ![새로 고침 필요](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. 완료 되 면 닫습니다 hello **속성** 대화 상자를 클릭 하 여 **확인**합니다. Hello 포리스트에서 도메인을 제거 하는 경우 도메인 제거 되었으며 해당 구성을 정리할 수 팝업 메시지가 표시 됩니다.
7. Tooadjust hello 계속 [실행 프로필](#update-run-profiles)합니다.

### <a name="update-hello-run-profiles"></a>실행 하는 hello 프로필 업데이트
도메인 필터를 업데이트 한 경우 tooupdate hello 실행 프로필이 필요 합니다.

1. Hello에 **커넥터** 목록 hello 이전 단계에서 변경한 커넥터를 선택 하는 hello 되었는지 확인 합니다. **작업**에서 **실행 프로필 구성**을 선택합니다.  
   ![커넥터 실행 프로필 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. 찾아서 hello 다음 프로필을 식별 합니다.
    * 전체 가져오기
    * 전체 동기화
    * 델타 가져오기
    * 델타 동기화
    * 내보내기
3. 각 프로필에 대 한 hello 조정 **추가** 및 **제거** 도메인입니다.
    1. 각 5 hello 프로필에 대 한 않습니다 hello 다음 단계 각각에 대해 **추가** 도메인:
        1. Hello 실행 프로필을 선택 하 고 클릭 **새 단계**합니다.
        2. Hello에 **단계 구성** 페이지 hello **형식** 드롭 다운 메뉴에서 선택 hello 단계 유형으로 hello 프로필 이름과 같은 이름을 hello로 구성 하는 합니다. 그런 후 **Next**를 클릭합니다.  
        ![커넥터 실행 프로필 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Hello에 **커넥터 구성** 페이지 hello에서 **파티션** 드롭 다운 메뉴, 선택 hello 이름 hello 도메인 tooyour 도메인 필터를 추가 했습니다.  
        ![커넥터 실행 프로필 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. tooclose hello **실행 프로필 구성** 대화 상자를 클릭 하 여 **마침**합니다.
    2. 각 5 hello 프로필에 대 한 않습니다 hello 다음 단계 각각에 대해 **제거** 도메인:
        1. Hello 실행 프로필을 선택 합니다.
        2. 경우 hello **값** 의 hello **파티션** 특성은 GUID를 클릭 하 고 단계를 실행 하는 select hello **단계 삭제**합니다.  
        ![커넥터 실행 프로필 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. 변경 내용을 확인합니다. 각 도메인을 toosynchronize 각 실행된 프로필의 일환으로 나열 되어야 합니다.
4. tooclose hello **실행 프로필 구성** 대화 상자를 클릭 하 여 **확인**합니다.
5.  toocomplete hello 구성 해야 toorun는 **전체 가져오기** 및 **델타 동기화**합니다. Hello 섹션을 읽고 [적용 및 변경 확인](#apply-and-verify-changes)합니다.

## <a name="organizational-unitbased-filtering"></a>조직 구성 단위 기반 필터링
hello toochange OU 기반 필터링 hello 설치 마법사를 실행 하 고 변경 하 여이 방식으로 기본 설정 [도메인 및 OU 필터링](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)합니다. hello 설치 마법사는이 항목에 설명 되어 있는 모든 hello 작업을 자동화 합니다.

어떤 이유로 없습니다 toorun hello 설치 마법사는 경우에 다음이 단계를 수행 해야 합니다.

tooconfigure 조직 구성 단위 기반 필터링을 다음 단계 hello지 않습니다.

1. Hello의 구성원 인 계정을 사용 하 여 Azure AD Connect 동기화를 실행 중인 toohello 서버 로그인 **ADSyncAdmins** 보안 그룹입니다.
2. 시작 **동기화 서비스** hello에서 **시작** 메뉴.
3. 선택 **커넥터**, 및 hello **커넥터** 목록에서 hello 형식과 hello 커넥터 **Active Directory 도메인 서비스**합니다. **작업**에서 **속성**을 선택합니다.  
   ![커넥터 속성](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. 클릭 **디렉터리 파티션 구성**선택, hello 도메인 tooconfigure를 원하고 클릭 **컨테이너**합니다.
5. 메시지가 나타나면 읽기 액세스 tooyour 온-프레미스 Active Directory 자격 증명을 제공 합니다. Hello 대화 상자에서 미리 채워지는 toobe hello 사용자가 되어 있지 않습니다.
6. Hello에 **컨테이너 선택** 대화 상자, 일반 hello Ou hello 클라우드 디렉터리와 toosynchronize 원하는 및 클릭 하지 않는 **확인**합니다.  
   ![Hello 컨테이너 선택 대화 상자에 Ou](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * hello **컴퓨터** Windows 10 컴퓨터 toobe tooAzure AD를 동기화에 대 한 컨테이너를 선택 해야 합니다. 컴퓨터에 연결된 도메인이 다른 OU에 있는 경우 해당 사항이 선택되어 있는지 확인합니다.
   * hello **ForeignSecurityPrincipals** 트러스트 있는 여러 포리스트가 있는 경우 컨테이너를 선택 해야 합니다. 이 컨테이너에는 포리스트 간 보안 그룹 멤버 자격 toobe를 확인할 수 있습니다.
   * hello **RegisteredDevices** hello 장치 쓰기 저장 기능을 사용 하는 경우 OU를 선택 해야 합니다. 그룹 쓰기 저장 등 다른 쓰기 저장 기능을 사용하는 경우 이러한 위치를 선택해야 합니다.
   * 사용자, iNetOrgPersons, 그룹, 연락처 및 컴퓨터가 있는 다른 OU를 선택합니다. Hello 그림에서 이러한 모든 Ou는 hello ManagedObjects OU에에서 위치 합니다.
   * 그룹 기반 필터링을 사용 하는 경우 hello hello 그룹이 위치한 OU 포함 되어야 합니다.
   * Note hello 필터링 구성이 완료 된 후 추가 된 새 Ou 동기화 중이거나 동기화 되지 있는지 여부를 구성할 수 있습니다. Hello 대 한 자세한 내용은 다음 섹션을 참조 하십시오.
7. 완료 되 면 닫습니다 hello **속성** 대화 상자를 클릭 하 여 **확인**합니다.
8. toocomplete hello 구성 해야 toorun는 **전체 가져오기** 및 **델타 동기화**합니다. Hello 섹션을 읽고 [적용 및 변경 확인](#apply-and-verify-changes)합니다.

### <a name="synchronize-new-ous"></a>새 OU 동기화
필터링을 구성한 후 생성된 새 OU는 기본적으로 동기화되어 있습니다. 이 상태는 선택된 확인란으로 표시됩니다. 일부 하위 OU를 선택 취소할 수도 있습니다. tooget이이 동작을 흰색 확인 표시가 파란색 (기본 상태)가 될 때까지 hello 상자를 클릭 합니다. 그런 다음 모든 하위 Ou toosynchronize 하지 않으려면 선택을 취소 합니다.

모든 하위 Ou를 동기화 하는 경우 hello 상자는 파란색 확인 표시가 있는 흰색 있습니다.  
![모든 상자가 선택된 OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

일부 하위 Ou 선택 되지, 경우 hello 상자는 흰색 확인 표시가 있는 회색입니다.  
![일부 하위 OU가 선택 취소된 OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

이 구성을 사용하여 ManagedObjects에서 만든 새 OU가 동기화됩니다.

hello Azure AD Connect 설치 마법사는 항상이 구성을 만듭니다.

### <a name="dont-synchronize-new-ous"></a>새 OU 동기화 안 함
Hello 동기화를 구성할 수 있습니다 엔진 toonot hello 필터링 구성이 완료 된 후 새 Ou를 동기화 합니다. 이 상태는 hello hello 상자가 확인 표시가 사용 실선 회색 표시 되는 UI에에서 표시 됩니다. tooget이이 동작을 흰색 확인 표시가 없는 상태가 될 때까지 hello 상자를 클릭 합니다. 그런 다음 원하는 toosynchronize hello 하위 Ou를 선택 합니다.

![OU를 선택 취소할 hello 루트로](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

이 구성을 사용하여 ManagedObjects에서 만든 새 OU가 동기화되지 않습니다.

## <a name="attribute-based-filtering"></a>특성 기반 필터링
사용 하는 경우 hello 2015 년 11 월 있는지 확인 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) 또는 이후 빌드에서 이러한 toowork 단계입니다.

특성 기반 필터링 하는 것은 hello 가장 유연한 방식으로 toofilter 개체입니다. hello 기능을 사용할 수 있습니다 [선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol 개체 때의 거의 모든 측면 tooAzure AD를 동기화 합니다.

적용할 수 있습니다 [인바운드](#inbound-filtering) Active Directory toohello 메타 버스에서 필터링 및 [아웃 바운드](#outbound-filtering) hello 메타 버스 tooAzure AD에서에서 필터링 합니다. Hello 쉬운 toomaintain 이기 때문에 인바운드 필터링을 적용 하는 것이 좋습니다. Hello 평가 수행할 수 전에 둘 이상의 포리스트에서 toojoin 개체 필요로 하는 경우 아웃 바운드 필터링만 사용 해야 합니다.

### <a name="inbound-filtering"></a>인바운드 필터링
인바운드 필터링의 tooAzure AD 개체 hello 메타 버스 특성 cloudFiltered tooa 값 toobe 동기화를 설정 하지 있어야 hello 기본 구성을 사용 합니다. 이 특성의이 값이 너무 설정**True**, 다음 hello 개체 동기화 되지 않았습니다. 너무 설정 해서는 안됩니다**False**를 설계 합니다. toomake 다른 규칙이 있는 hello 기능 toocontribute 값 있는지,이 특성이 되어 toohave hello 값 **True** 또는 **NULL** (없음).

인바운드 필터링을 사용 하 여의 전원 hello **범위** toodetermine toosynchronize 개체 또는 동기화 되지 않습니다. 여기서 설정한 조정 toofit 사용자 조직의 요구 사항입니다. hello 범위 모듈에는 **그룹** 및 **절** toodetermine 동기화 규칙 범위에 있을 때. 그룹에 하나 이상의 절이 포함됩니다. 여러 절 간에는 논리적 “AND”가 있으며 여러 그룹 간에는 논리적 “OR”이 있습니다.

예:   
![범위](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
**(department = IT) OR (department = Sales AND c = US)**로 표시됩니다.

예제 및 단계를 따라 hello, 예를 들어 hello 사용자 개체를 사용 하지만 모든 개체 유형에 사용할 수 있습니다.

다음 예제는 hello, hello 우선 순위 값 50 시작 됩니다. 사용되지 않은 모든 숫자를 사용할 수 있지만 100보다는 작아야 합니다.

#### <a name="negative-filtering-do-not-sync-these"></a>부정 필터링: "다음을 동기화 안 함"
다음 예제는 hello에서 필터링 (동기화 되지 않습니다) 모든 사용자가 있는 **extensionAttribute15** hello 값이 **NoSync**합니다.

1. Hello의 구성원 인 계정을 사용 하 여 Azure AD Connect 동기화를 실행 중인 toohello 서버 로그인 **ADSyncAdmins** 보안 그룹입니다.
2. 시작 **동기화 규칙 편집기** hello에서 **시작** 메뉴.
3. **인바운드**가 선택되어 있는지 확인하고 **새 규칙 추가**를 클릭합니다.
4. 와 같은 hello 규칙 설명이 포함 된 이름을 지정 "*에서 from AD – User DoNotSyncFilter*"입니다. 선택 hello 올바른 포리스트, 선택 **사용자** hello로 **CS 개체 유형**를 선택 하 고 **사람** hello로 **MV 개체 유형**합니다. **링크 형식**에서 **조인**을 선택합니다. **우선 순위**에서 현재 다른 동기화 규칙에서 사용하지 않는 값(예: 50)을 입력한 후 **다음**을 클릭합니다.  
   ![인바운드 1 설명](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. **범위 지정 필터**에서 **그룹 추가**를 클릭하고 **절 추가**를 클릭합니다. **특성**에서 **ExtensionAttribute15**를 선택합니다. 다음 사항을 확인 **연산자** 너무 설정**같은**, hello 값을 입력 하 고 **NoSync** hello에 **값** 상자. **다음**을 누릅니다.  
   ![인바운드 2 범위](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Hello 둡니다 **조인** 빈, 규칙 및 클릭 **다음**합니다.
7. 클릭 **변환 추가**선택, hello **FlowType** 으로 **상수**를 선택 하 고 **cloudFiltered** hello로  **특성 대상**합니다. Hello에 **소스** 텍스트 상자에서 **True**합니다. 클릭 **추가** toosave hello 규칙입니다.  
   ![인바운드 3 변환](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. toocomplete hello 구성 해야 toorun는 **전체 동기화**합니다. Hello 섹션을 읽고 [적용 및 변경 확인](#apply-and-verify-changes)합니다.

#### <a name="positive-filtering-only-sync-these"></a>긍정 필터링: "다음만 동기화"
양수 필터링 표현 좀 더 어렵습니다 명백한 toobe 회의실 같은 동기화 되지 않은 tooconsider 개체 있으므로 될 수 있습니다. 에 있습니다. 또한 지속적인 toooverride hello 기본 필터 hello 기본적으로 규칙 **에서 from AD-User Join**합니다. 사용자 지정 필터를 만들 때 toonot Azure AD Connect에 대 한 중요 한 시스템 개체, 복제 충돌 개체, 특별 한 사서함 및 hello 서비스 계정을 포함 해야 합니다.

hello 양의 필터링 옵션에는 동기화 규칙 두 개 필요합니다. Hello 개체 toosynchronize의 올바른 범위를 가진 규칙을 하나 이상 필요 합니다. 아직 동기화해야 하는 개체로 식별되지 않은 모든 개체를 필터링하는 두 번째 포괄적인 동기화 규칙도 필요합니다.

다음 예제는 hello에 사용자 개체 hello 부서 특성에 hello 값이 동기화 **Sales**합니다.

1. Hello의 구성원 인 계정을 사용 하 여 Azure AD Connect 동기화를 실행 중인 toohello 서버 로그인 **ADSyncAdmins** 보안 그룹입니다.
2. 시작 **동기화 규칙 편집기** hello에서 **시작** 메뉴.
3. **인바운드**가 선택되어 있는지 확인하고 **새 규칙 추가**를 클릭합니다.
4. 와 같은 hello 규칙 설명이 포함 된 이름을 지정 "*from AD – 사용자 Sales 지침과 동기화*"입니다. 선택 hello 올바른 포리스트, 선택 **사용자** hello로 **CS 개체 유형**를 선택 하 고 **사람** hello로 **MV 개체 유형**합니다. **링크 형식**에서 **조인**을 선택합니다. **우선 순위**에서 현재 다른 동기화 규칙에서 사용하지 않는 값(예: 51)을 입력한 후 **다음**을 클릭합니다.  
   ![인바운드 4 설명](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. **범위 지정 필터**에서 **그룹 추가**를 클릭하고 **절 추가**를 클릭합니다. **특성**에서 **부서**를 선택합니다. 연산자 너무 설정 되어 있는지 확인**같은**, hello 값을 입력 하 고 **Sales** hello에 **값** 상자입니다. **다음**을 누릅니다.  
   ![인바운드 5 범위](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Hello 둡니다 **조인** 빈, 규칙 및 클릭 **다음**합니다.
7. 클릭 **변환 추가**선택, **상수** hello로 **FlowType**, 및 select hello **cloudFiltered** hello로  **특성 대상**합니다. Hello에 **소스** 상자에서 입력 **False**합니다. 클릭 **추가** toosave hello 규칙입니다.  
   ![인바운드 6 변환](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   이 특별 한 경우 명시적으로 설정한 cloudFiltered 너무**False**합니다.
8. Toocreate hello 포괄적인 동기화 규칙을 했습니다. 와 같은 hello 규칙 설명이 포함 된 이름을 지정 "*에서 from AD – 사용자 범용 필터*"입니다. 선택 hello 올바른 포리스트, 선택 **사용자** hello로 **CS 개체 유형**를 선택 하 고 **사람** hello로 **MV 개체 유형**합니다. **링크 형식**에서 **조인**을 선택합니다. **우선 순위**에서 현재 다른 동기화 규칙에서 사용하지 않는 값(예: 99)을 입력합니다. 선행 값 (낮은 보다 높은 우선 순위) hello 이전 동기화 규칙을 선택 했습니다. 하지만 toostart 추가 부서를 동기화 하려는 경우 더 이상 필터링 동기화 규칙 나중에 추가할 수 있도록 공간을 남겨 수도 있습니다. **다음**을 누릅니다.  
   ![인바운드 7 설명](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. **범위 지정 필터**를 비워 두고 **다음**을 클릭합니다. 빈 필터 hello 규칙은 적용 toobe tooall 개체를 나타냅니다.
10. Hello 둡니다 **조인** 빈, 규칙 및 클릭 **다음**합니다.
11. 클릭 **변환 추가**선택, **상수** hello로 **FlowType**를 선택 하 고 **cloudFiltered** hello로  **특성 대상**합니다. Hello에 **소스** 상자에서 입력 **True**합니다. 클릭 **추가** toosave hello 규칙입니다.  
    ![인바운드 3 변환](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. toocomplete hello 구성 해야 toorun는 **전체 동기화**합니다. Hello 섹션을 읽고 [적용 및 변경 확인](#apply-and-verify-changes)합니다.

해야 할 경우에 hello 동기화에 더 많은 개체를 포함할 경우 hello 첫 번째 종류의 더 많은 규칙을 만들 수 있습니다.

### <a name="outbound-filtering"></a>아웃바운드 필터링
일부 경우에는 필요한 toodo hello hello 개체 hello 메타 버스에 조인 된 후에 필터링 예를 들어 hello 리소스 포리스트에서 메일 특성 hello 및 개체를 동기화 해야 하는 경우 toodetermine hello 계정 포리스트의 userPrincipalName 특성 hello 필요한 toolook 수도 있습니다. 이러한 경우 hello 아웃 바운드 규칙을 필터링 하는 hello를 만들 수 있습니다.

이 예제에서는 변경할 있습니다 hello 필터링 하 여 사용자만 있는 메일와 userPrincipalName에서 끝나는 모두 @contoso.com 동기화 됩니다.

1. Hello의 구성원 인 계정을 사용 하 여 Azure AD Connect 동기화를 실행 중인 toohello 서버 로그인 **ADSyncAdmins** 보안 그룹입니다.
2. 시작 **동기화 규칙 편집기** hello에서 **시작** 메뉴.
3. **규칙 형식**에서 **아웃바운드**를 클릭합니다.
4. 이라는 찾기 hello 규칙 **tooAAD – User Join 아웃**를 클릭 하 고 **편집**합니다.
5. Hello 팝업에 대답 **예** toocreate hello 규칙의 복사본입니다.
6. Hello에 **설명** 페이지, 변경 **선행** tooan 50 같은 사용 되지 않는 값입니다.
7. 클릭 **범위 지정 필터** 왼쪽의 탐색 hello 되 고 클릭 **절 추가**합니다. **특성**에서 **메일**을 선택합니다. **연산자**에서 **ENDSWITH**를 선택합니다. **값**에서 **@contoso.com**를 입력하고 **절 추가**를 클릭합니다. **특성**에서 **userPrincipalName**을 선택합니다. **연산자**에서 **ENDSWITH**를 선택합니다. **값**에서**@contoso.com**을 입력합니다.
8. **Save**를 클릭합니다.
9. toocomplete hello 구성 해야 toorun는 **전체 동기화**합니다. Hello 섹션을 읽고 [적용 및 변경 확인](#apply-and-verify-changes)합니다.

## <a name="apply-and-verify-changes"></a>변경 사항을 적용하고 확인합니다
구성 변경, 변경한 후 hello 시스템에 이미 있는 toohello 개체 적용 해야 합니다. Hello 동기화 엔진에 현재 없는 hello 개체를 처리 하는 것 수도 있습니다 (hello 동기화 엔진이 tooread hello 소스 시스템 요구 사항 다시 tooverify 내용).

사용 하 여 hello 구성을 변경한 경우 **도메인** 또는 **조직 구성 단위** 필터링 toodo 필요는 **전체 가져오기**옵니다 **델타 동기화**합니다.

사용 하 여 hello 구성을 변경한 경우 **특성** 필터링 toodo 필요는 **전체 동기화**합니다.

다음 단계 hello 마십시오.

1. 시작 **동기화 서비스** hello에서 **시작** 메뉴.
2. **커넥터**를 선택합니다. Hello에 **커넥터** 목록 hello 이전 변경 하는 구성을 변경한 커넥터를 선택 합니다. **작업**에서 **실행**을 선택합니다.  
   ![커넥터 실행](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. **실행 프로필**, hello 작업 hello 이전 섹션에서 언급 한 것을 선택 합니다. Toorun 두 작업 해야 할 경우 hello 후 두 번째로 실행된 hello 첫 번째 완료 했습니다. (hello **상태** 열이 **Idle** 선택한 hello 커넥터에 대 한 합니다.)

Hello 동기화 후에 모든 변경 내용이 내보낸 준비 된 toobe 합니다. 실제로 hello 변경 전에 Azure ad에서를 원하는 tooverify 이러한 모든 변경이 내용이 정확한 지 확인 합니다.

1. 명령 프롬프트를 시작 하 고 이동 너무`%Program Files%\Microsoft Azure AD Sync\bin`합니다.
2. `csexport "Name of Connector" %temp%\export.xml /f:x`을 실행합니다.  
   hello 이름이 hello 커넥터의 동기화 서비스입니다. 에 이름이 비슷한 too"contoso.com – AAD" Azure AD에 대 한 합니다.
3. `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`을 실행합니다.
4. 이제 %temp%에 Microsoft Excel에서 검사할 수 있는 export.csv 라는 파일이 있습니다. 이 파일은 내보낸 toobe 거의 모든 hello 변경 내용을 포함 합니다.
5. Hello 필요한 변경을 toohello 데이터 또는 확인 구성 및 실행이 다시 (가져오기, 동기화 및 확인) 때까지이 단계 hello 된 내보낸 toobe에 대 한 변경 내용을 기대 합니다.

만족 스 러 우면 hello 변경 tooAzure AD 내보냅니다.

1. **커넥터**를 선택합니다. Hello에 **커넥터** 목록 hello Azure AD 커넥터를 선택 합니다. **작업**에서 **실행**을 선택합니다.
2. **실행 프로필**에서 **내보내기**를 선택합니다.
3. 구성 변경 내용을 많은 개체를 삭제 하는 경우 다음 있습니다 때 오류가 표시 hello 내보내기에서 hello 번호 (기본적으로 500) hello 구성 된 임계값 보다 큰 것입니다. 이 오류가 나타나는 경우 tootemporarily 사용 안 함 hello 필요 "[실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" 기능입니다.

이제입니다 시간 tooenable hello 스케줄러 다시입니다.

1. 시작 **작업 스케줄러** hello에서 **시작** 메뉴.
2. 바로 아래 **작업 스케줄러 라이브러리**, 라는 찾기 hello 작업 **Azure AD Sync Scheduler**를 마우스 오른쪽 단추로 클릭 하 고 선택 **사용**합니다.

## <a name="group-based-filtering"></a>그룹 기반 필터링
그룹 기반 필터링 hello를 사용 하 여 Azure AD Connect를 설치 하는 처음으로 구성할 수 있습니다 [사용자 지정 설치](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)합니다. 의도 소수의 개체 toobe 동기화 저장할 파일럿 배포에 대 한 합니다. 그룹 기반 필터링을 사용하지 않도록 설정하면 다시 사용하도록 설정할 수 없습니다. 있기 *지원 되지 않습니다* toouse 그룹 기반 사용자 지정 구성에서 필터링 합니다. 것에 지원 tooconfigure이이 기능은 hello 설치 마법사를 사용 하 여 합니다. 파일럿, 완료 한 다음이 항목의 다른 필터링 옵션 hello 중 하나 사용 합니다. 그룹 기반 필터링와 함께에서 OU 기반 필터링을 사용할 경우 hello hello 그룹 및 해당 멤버 있는 OU(s) 포함 되어야 합니다.

여러 AD 포리스트를 동기화할 경우 각 AD 커넥터에 서로 다른 그룹을 지정하여 그룹 기반 필터링을 구성할 수 있습니다. 그룹 기반 내 FSP 개체는 toosynchronize 한 AD 포리스트의 사용자를 원하는 및 hello 동일한 사용자에 게 하나 이상의 해당 FSP (외부 보안 주체가) 다른 AD 포리스트에서 개체 확인 해야 해당 hello 사용자 개체 및 모든 해당 하는 경우 범위를 필터링 합니다. 하나 이상의 hello FSP 개체는 그룹 기반 필터링으로 제외, hello 사용자 개체 동기화 된 tooAzure AD 보호 되지 않습니다.

## <a name="next-steps"></a>다음 단계
- [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.
- [Azure AD와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
