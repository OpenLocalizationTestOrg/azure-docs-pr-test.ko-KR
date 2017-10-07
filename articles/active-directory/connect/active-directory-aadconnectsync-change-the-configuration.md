---
title: "Azure AD Connect 동기화: Azure AD Connect 동기화의 구성 변경 | Microsoft Docs"
description: "Azure AD Connect에서 구성 하는 변경 toohello 동기화 하는 toomake 방법을 보여 줍니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Azure AD Connect 동기화: 방법 변경 toohello toomake 기본 구성
이 항목의 hello 목적은 toowalk toomake toohello 기본 구성으로 Azure AD Connect 동기화를 변경 하는 방법을 안내 합니다. 몇 가지 일반적인 시나리오를 위한 단계를 제공합니다. 이 정보를 사용자 고유의 비즈니스 규칙에 따라 구성을 소유 하는 몇 가지 간단한 변경 사항이 tooyour 수 toomake 있어야 합니다.

## <a name="synchronization-rules-editor"></a>동기화 규칙 편집기
hello 동기화 규칙 편집기에 사용 되는 toosee 및 변경 hello 기본 구성입니다. Hello 아래 hello 시작 메뉴에서에서 찾을 수 있습니다 **Azure AD Connect** 그룹입니다.  
![동기화 규칙 편집기를 사용 하여 메뉴 시작](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

을 열 때 hello 기본 기본적으로 규칙을 참조 합니다.

![동기화 규칙 편집기](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Hello 편집기에서 탐색
hello 편집기의 hello 위쪽 hello 드롭다운 tooquickly 찾기 특정 규칙을 허용 합니다. 예를 들어 hello 특성 proxyAddresses 포함 되는지 toosee hello 규칙을 사용 하도록 하려는 경우 다음과 같이 변경 hello 드롭다운 toohello 다음  
![SRE 필터링](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
tooreset 필터링 하 고 새 구성 로드 키를 눌러 **F5** hello 키보드에서.

단추가 있는 toohello 오른쪽 위, **새 규칙 추가**합니다. 이 단추는 사용 되는 toocreate 사용자 고유의 사용자 지정 규칙입니다.

Hello 맨 아래에 선택 된 동기화 규칙에 대해 작업을 수행 하는 단추가 있습니다. **편집** 및 **삭제** 단추를 누르면 해당 작업이 수행됩니다. **내보내기** hello 동기화 규칙을 다시 만드는 것에 대 한 PowerShell 스크립트를 생성 합니다. 이 절차에서 하나의 서버 tooanother 동기화 규칙 toomove가 있습니다.

## <a name="create-your-first-custom-rule"></a>첫 번째 사용자 지정 규칙 만들기
hello 가장 일반적인 변경은 변경 toohello 특성 흐름입니다. hello 데이터 원본 디렉터리에 Azure AD에서와 같이 아닐 수 있습니다. 이 섹션의 hello 예제에서는 사용자의 hello 지정 된 이름에 항상는 toomake 원하는 **올바른 대/소문자**합니다.

### <a name="disable-hello-scheduler"></a>Hello 스케줄러를 사용 하지 않도록 설정
hello [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) 기본적으로 30 분 마다 실행 합니다. 변경 하는 새 규칙의 문제를 해결 하는 동안 시작 되지 않으면 있는지 toomake 사용 하는 것이 좋습니다. tootemporarily는 hello 스케줄러를 해제, PowerShell을 시작 및 실행`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Hello 스케줄러를 사용 하지 않도록 설정](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Hello 규칙 만들기
1. **새 규칙 추가**를 클릭합니다.
2. Hello에 **설명** 페이지 hello 다음을 입력 합니다.  
   ![인바운드 규칙 필터링](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * 이름: hello 규칙을 설명 하는 이름을 지정 합니다.
   * 설명:에 대 한 다른 사용자가 어떤 hello 규칙을 이해할 수 있도록 일부 설명은입니다.
   * 시스템 연결: hello 시스템 hello 개체에서 찾을 수 있습니다. 이 경우 hello Active Directory Connector를 선택 합니다.
   * 연결된 시스템/메타버스 개체 유형: **사용자**와 **사람**을 각각 선택합니다.
   * 링크 형식:이 값을 너무 변경**조인**합니다.
   * 우선 순위: hello 시스템에서 고유한 값을 제공 합니다. 숫자 값이 낮을수록 높은 우선 순위를 나타냅니다.
   * 태그: 비워 둡니다. Microsoft의 기본 규칙으로만 이 상자에 값을 채워야 합니다.
3. Hello에 **범위 지정 필터** 페이지에서 입력 **givenName ISNOTNULL**합니다.  
   ![인바운드 규칙 범위 지정 필터](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   이 섹션은 사용 되는 toodefine 어떤 개체 hello 규칙을 적용 해야 합니다. 비워 두면 hello 규칙은 tooall 사용자 개체에 적용 됩니다. 하지만 여기에는 회의실, 서비스 계정 및 기타 사람이 아닌 사용자 개체가 포함됩니다.
4. Hello에 **조인 규칙**를 비워 두세요.
5. Hello에 **변환** 페이지, 너무 hello FlowType 변경**식**합니다. 대상 특성 선택 hello **givenName**, 소스에 입력 `PCase([givenName])`합니다.
   ![인바운드 규칙 변환](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   hello 동기화 엔진은 hello 함수 이름과 hello 특성의 이름을 hello에에서 대/소문자 구분입니다. 잘못 된 텍스트를 입력 하지 hello 규칙을 추가할 때 경고가 표시 됩니다. hello 편집기 toosave 있으며 tooreopen hello 규칙 및 올바른 hello 규칙 해야 하므로 계속 합니다.
6. 클릭 **추가** toosave hello 규칙입니다.

새 사용자 지정 규칙에는 다른 hello로 표시 되어야 합니다. hello 시스템에서 규칙을 동기화 합니다.

### <a name="verify-hello-change"></a>Hello 변경 내용을 확인합니다
이러한 새로운 변경으로 인해 toomake 예상 대로 작동 하 고 오류를 throw 할 수 있습니다. 사용자가 개체에 hello 수에 따라 있는 경우 두 가지 방법으로 toodo이이 단계

1. 모든 개체에서 전체 동기화 실행
2. 단일 개체에서 미리 보기 및 전체 동기화 실행

시작 **동기화 서비스** hello 시작 메뉴에서 합니다. 이 섹션의 hello 단계는이 도구에 모두 있습니다.

1. **모든 개체에서 전체 동기화**  
   선택 **커넥터** hello 위쪽에 있습니다. Hello 변경 tooin hello 이전 섹션을 변경한 커넥터를 확인 합니다.이 경우 Active Directory 도메인 서비스 hello 하 고 선택. 작업에서 **실행**을 선택하고 **전체 동기화**와 **확인**을 선택합니다.
   ![전체 동기화](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   hello 개체 hello 메타 버스에서 이제 업데이트 됩니다. 이제 toolook hello 메타 버스의 hello 개체에 원하는합니다.
2. **단일 개체에서 미리 보기 및 전체 동기화**  
   선택 **커넥터** hello 위쪽에 있습니다. Hello 변경 tooin hello 이전 섹션을 변경한 커넥터를 확인 합니다.이 경우 Active Directory 도메인 서비스 hello 하 고 선택. **커넥터 공간 검색**을 선택합니다. 범위 toofind toouse tootest hello 변경 하려는 개체를 사용 합니다. Hello 개체를 선택 하 고 클릭 **미리 보기**합니다. Hello 새 화면에서 선택 **커밋 미리 보기**합니다.  
   ![커밋 미리 보기](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   커밋된 toohello 메타 버스 hello 변경이 되었습니다.

**Hello 메타 버스의 hello 개체 확인**  
이제 원하는 toopick 몇 가지 샘플 개체 toomake 있는지 hello 값이 필요 하 고 해당 hello 규칙을 적용 합니다. 선택 **메타 버스 검색** hello 위에서 합니다. Toofind hello 관련 개체가 필요한 모든 필터를 추가 합니다. Hello 검색 결과에서 개체를 엽니다. Hello 특성 값을 살펴보고 하 고 hello에 인지도 확인할 **동기화 규칙** hello 규칙이 제대로 적용 된 열입니다.  
![메타 버스 검색](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Hello 스케줄러를 사용 하도록 설정
이면 모든 항목이 예상 대로 hello 스케줄러를 다시 설정할 수 있습니다. PowerShell에서 `Set-ADSyncScheduler -SyncCycleEnabled $true`을(를) 실행합니다.

## <a name="other-common-attribute-flow-changes"></a>기타 일반적인 특성 흐름 변경
이전 섹션 hello toomake tooan 특성 흐름을 변경 하는 방법을 설명 합니다. 이 섹션에서는 몇 가지 추가 예제가 제공됩니다. toocreate hello 동기화 규칙은 약어 하는 방법에 대 한 hello 단계 있지만 hello 이전 단원의 hello 전체 단계를 찾을 수 있습니다.

### <a name="use-another-attribute-than-hello-default"></a>Hello 기본값과 다른 특성을 사용 하 여
Fabrikam,에 지정 된 이름, 성 및 표시 이름에 대 한 로컬 알파벳 hello 사용 되는 위치 하는 포리스트입니다. 이러한 특성의 라틴 문자 표현을 hello hello 확장 특성에서 찾을 수 있습니다. Azure AD의 hello 전체 주소 목록을 작성할 때 및 Office 365 hello 조직이 이러한 특성 toobe 대신 사용 합니다.

기본 구성을 사용 하 여 hello 로컬 포리스트의 개체는 다음과 같이 보입니다.  
![특성 흐름 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

다른 특성 흐름을 사용 하는 규칙 toocreate 다음 hello지 않습니다.

* 시작 **동기화 규칙 편집기** hello 시작 메뉴에서 합니다.
* 와 **인바운드** 여전히 선택한 toohello hello 단추 클릭, **새 규칙 추가**합니다.
* 이름 및 설명을 hello 규칙을 지정 합니다. Hello 온-프레미스 Active Directory와 hello 관련 개체 유형을 선택 합니다. **링크 형식**에서 **조인**을 선택합니다. 우선 순위로 다른 규칙에서 사용하지 않은 숫자를 선택합니다. 기본적으로 규칙 hello hello 값 50이 예에서 사용할 수 있도록 100로 시작 합니다.
  ![특성 흐름 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* 빈 범위를 벗어나면 (즉, 적용 해야 tooall 사용자 포리스트의 개체에 hello).
* (즉, 모든 조인 규칙의 기본 핸들을 hello 사용)는 조인 규칙 빈 상태로 둡니다.
* 변환에서 hello 다음 흐름을 만듭니다.  
  ![특성 흐름 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* 클릭 **추가** toosave hello 규칙입니다.
* 너무 이동**동기화 서비스 관리자**합니다. **커넥터**, 선택 hello 커넥터 hello 규칙을 추가 했습니다. **실행**을 선택한 다음 **전체 동기화**를 선택합니다. 전체 동기화는 hello 현재 규칙을 사용 하 여 모든 개체를 다시 계산 합니다.

다음은이 사용자 지정 규칙으로 동일한 개체 hello에 대 한 hello 결과입니다.  
![특성 흐름 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>특성의 길이
문자열 특성은 기본 집합 toobe 인덱싱 가능으로 및 hello 최대 길이 448 자입니다. 자세히 포함 될 수 있는 문자열 특성을 사용 하는 경우 다음 hello 특성 흐름에서 있는지 tooinclude hello 다음을 확인 합니다.  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Hello userPrincipalSuffix 변경
Active Directory의 userPrincipalName 특성 hello 항상 hello 사용자가 인식 되지 않으며 맞지 않을 때 hello 로그인 id입니다. hello Azure AD Connect sync 설치 마법사는 서로 다른 특성을 선택할 수 있습니다. 예를 들어 메일 합니다. 하지만 일부 경우 hello에 특성을 계산 해야 합니다. 예를 들어 hello 회사 Contoso에 Azure AD 디렉터리를 두 개, 하나는 프로덕션 및 테스트에 대 한 있습니다. 원하는 hello 사용자의 테스트에서 테 넌 트 toouse hello 로그인 ID에 다른 접미사  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

이 식에서 먼저 hello의 왼쪽 모든 내용이 @-sign (Word) 및 고정 문자열과 연결 합니다.

### <a name="convert-a-multi-value-tooa-single-value"></a>다중 값 tooa 단일 값으로 변환
Active Directory의 일부 특성은 보이지만 단일 Active Directory 사용자 및 컴퓨터에 값이 hello 스키마에 다중 값. 예는 hello 설명 특성입니다.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

이 식 hello 특성에 값이 hello 특성 hello 첫 번째 항목 (항목)를 수행 하는 경우 선행 및 후행 공백 (Trim)를 제거한 후 유지 hello hello 문자열에서 처음 448 자 (왼쪽).

### <a name="do-not-flow-an-attribute"></a>특성을 전달하지 않습니다.
이 섹션에 대 한 hello 시나리오에 대 한 배경, 참조 [hello 특성 흐름 프로세스 제어](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process)합니다.

두 가지 방법으로 toonot 특성 흐름. hello 먼저 hello 설치 마법사에서 사용할 수 알리고 너무[선택한 특성을 제거](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering)합니다. 이 옵션은 하기 전에 hello 특성을 동기화 하지 않은 경우 작동 합니다. 그러나 toosynchronize이이 특성 시작 되 고 나중에이 기능을 제거 하는 경우 다음 hello 동기화 엔진이 중지 hello 특성을 관리 하 고 hello 기존 값은 Azure AD에 남아 있습니다.

특성의 값이 tooremove hello 하려면 hello 나중에 이동 하지 않는 있는지 확인 하는 경우 대신 사용자 지정 규칙을 만들 필요 있습니다.

Fabrikam, 우리 할 필요성이 않을 중 일부는 특성 toohello 동기화에서는 클라우드 hello 해야 하지 수 있습니다. Toomake 이러한 특성은 Azure AD에서 제거 되었는지 확인할 수 있습니다.  
![잘못된 확장 특성](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* 새 인바운드 동기화 규칙을 만들고 채울 hello 설명 ![설명](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* 형식의 특성 흐름을 만들고 **식** 및 hello 원본과 **AuthoritativeNull**합니다. 리터럴 hello **AuthoritativeNull** 해야 함을 나타내는 hello 값 hello MV에서에서 빈 낮은 우선 순위 동기화 규칙 toopopulate hello 값을 시도 하는 경우에 합니다.
  ![확장 특성을 위한 변환](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Hello 동기화 규칙을 저장 합니다. 시작 **동기화 서비스**hello 커넥터, 선택, **실행**, 및 **전체 동기화**합니다. 이 단계는 모든 특성 흐름을 다시 계산합니다.
* Hello 커넥터 공간 검색 하 여 내보낸 toobe에 대 한 변경 내용이 해당 hello 의도 확인 합니다.
  ![단계적 삭제](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>PowerShell로 규칙 만들기
Hello 동기화 규칙 편집기를 사용 하 여 몇 가지 변경 내용을 toomake만 있는 경우 제대로 작동 합니다. Toomake을 많은 변경이 필요한 경우 PowerShell 방법이 더 나을 수 있습니다. 일부 고급 기능은 PowerShell에서만 사용할 수 있습니다.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Hello PowerShell 스크립트는 기본적으로 규칙에 대 한 가져오기
toosee hello hello 동기화에는 기본적으로 규칙, 선택 hello 규칙을 생성 하는 PowerShell 스크립트 편집기와 클릭 규칙 **내보내기**합니다. 이 작업에서는 PowerShell hello 만든된 hello 규칙을 스크립팅 합니다.

### <a name="advanced-precedence"></a>고급 우선 순위
hello 기본 제공 동기화 규칙 우선 순위 값은 100로 시작 합니다. 포리스트 수 있고 toomake를 필요한 많은 사용자 지정 변경 내용을 다음 99 동기화 규칙 수 충분 합니다.

동기화 엔진 hello 기본적으로 규칙 앞에 삽입 하는 추가 규칙을 hello를 지시할 수 있습니다. tooget이이 동작을 다음이 단계를 수행 합니다.

1. 표시 hello 첫 번째 기본 제공 동기화 규칙 (이 규칙은 hello **에서 AD-User Join에서**) hello 동기화 규칙 편집기 및 선택 **내보내기**합니다. Hello SR 식별자 값을 복사 합니다.  
![변경 전 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Hello 새 동기화 규칙을 만듭니다. 동기화 규칙 편집기 toocreate hello를 사용할 수 있습니다 것입니다. Hello 규칙 tooa PowerShell 스크립트를 내보냅니다.
3. Hello 속성에 **PrecedenceBefore**, hello 기본적으로 규칙에서 hello 식별자 값을 삽입 합니다. 집합 hello **선행** 너무**0**합니다. Hello 식별자 특성은 고유 하 고 다른 규칙에서 GUID를 다시 사용 되지 있는지 확인 합니다. 또한 되도록 해당 hello **ImmutableTag** 속성이 설정 되어 있지 않으면이 속성의 기본 규칙에 대 한만 설정 해야 합니다. Hello PowerShell 스크립트를 저장 하 고 실행 합니다. hello 결과 사용자 지정 규칙 hello 우선 순위 값이 100 할당 하 고 다른 모든 기본 제공 규칙 증가입니다.  
![변경 후 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

있습니다 수 있는 많은 사용자 지정 동기화 규칙은 사용 하 여 동일한 hello **PrecedenceBefore** 필요할 때 값입니다.


## <a name="enable-synchronization-of-preferreddatalocation"></a>PreferredDataLocation 동기화 사용
Azure AD Connect hello의 동기화를 지원 **PreferredDataLocation** 특성 **사용자** 1.1.524.0 버전에서 및 이후 개체입니다. 구체적으로 다음과 같은 변경 내용이 도입되었습니다.

* hello 개체 유형의 hello 스키마 **사용자** hello Azure AD 커넥터를 문자열 형식의 단일 값 tooinclude PreferredDataLocation 특성 확장 됩니다.

* hello 개체 유형의 hello 스키마 **사람** hello 메타 버스 tooinclude PreferredDataLocation 특성 문자열 형식이 단일 값 이며 확장 됩니다.

기본적으로 hello PreferredDataLocation 특성이 활성화 되지 않은 동기화를 위해 온-프레미스 Active Directory에 PreferredDataLocation 특성 이므로 합니다. 동기화를 사용하도록 수동으로 설정해야 합니다.

> [!IMPORTANT]
> 현재, Azure AD에 동기화 된 사용자 개체와 클라우드 둘 다 직접 Azure AD PowerShell을 사용 하 여를 구성 하는 사용자 개체 toobe hello PreferredDataLocation 특성을 허용 합니다. Hello PreferredDataLocation 특성의 동기화를 설정한 후에 Azure AD PowerShell tooconfigure hello 특성을 사용 하 여 중지 해야 **사용자 개체를 동기화** Azure AD Connect로 보다 우선 하 게 기반 온-프레미스 Active Directory의 hello 소스 특성 값입니다.

> [!IMPORTANT]
> 1 2017 년 1 년 9 월에 Azure AD는 더 이상 hello PreferredDataLocation 특성에서 허용 **사용자 개체를 동기화** toobe 직접 Azure AD PowerShell을 사용 하 여를 구성 합니다. tooconfigure PreferredLocation 특성에 사용자 개체를 동기화, Azure AD Connect를 사용 해야 합니다.

Hello PreferredDataLocation 특성의 동기화를 활성화 하기 전에 다음을 수행 해야 합니다.

 * 먼저, hello 원본 특성으로 사용 하는 온-프레미스 Active Directory 특성 toobe를 결정 합니다. 이 특성은 **문자열** 형식의 **단일 값**이어야 합니다.

 * Azure AD PowerShell을 사용 하 여 Azure ad에서 사용자 개체를 동기화 기존 hello PreferredDataLocation 특성에 이전에 구성 된 경우, 해야 **backport** hello 특성 값 toohello 해당 사용자 개체 온-프레미스 Active directory 의미 합니다.
 
    > [!IMPORTANT]
    > Azure AD Connect가 hello PreferredDataLocation 특성에 대 한 동기화가 되는 Azure AD의 hello 기존 특성 값을 제거 합니다 backport hello 특성 값 toohello 해당 사용자 개체가 아니라 온-프레미스 Active Directory의 경우 사용할 수 있습니다.

 * Hello 원본 특성 구성 하는 것이 좋습니다 적어도 몇 가지 온-프레미스 AD 사용자 개체, 나중에 확인을 위해 사용할 수 있는 합니다.
 
hello PreferredDataLocation 특성의 hello 단계 tooenable 동기화 다음과 같이 요약할 수 있습니다.

1. 동기화 스케줄러를 비활성화하고 진행 중인 동기화가 없는지 확인합니다.

2. Hello 소스 특성 toohello 온-프레미스 AD 커넥터 추가 스키마

3. PreferredDataLocation toohello Azure AD 커넥터 스키마 추가

4. 온-프레미스 Active Directory에서 인바운드 동기화 규칙 tooflow hello 특성 값 만들기

5. 아웃 바운드 동기화 규칙 tooflow hello 특성 값 tooAzure AD 만들기

6. 전체 동기화 주기 실행

7. 동기화 스케줄러를 사용하도록 설정

> [!NOTE]
> 이 섹션의 hello 나머지 부분에서는 세부 정보에서 이러한 단계를 설명합니다. 단일 포리스트 토폴로지를 사용 하 고 사용자 지정 동기화 규칙이 없는 Azure AD 배포의 hello 컨텍스트에서 설명 합니다. 다중 포리스트 토폴로지를 사용 하도록 설정한 경우 사용자 지정 동기화 규칙 구성 않았거나 스테이징 서버, tooadjust hello 단계를 적절 하 게 해야 합니다.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>1단계: 동기화 스케줄러 비활성화 및 진행 중인 동기화가 없는지 확인
동기화를 업데이트 하는 hello 중간에 있는 동안 발생 하는 동기화 확인 규칙 tooavoid 의도 하지 않은 변경 되 고 AD tooAzure 내보낸 합니다. toodisable hello 기본 제공 동기화 스케줄러:

 1. Hello Azure AD Connect 서버에서 PowerShell 세션을 시작 합니다.

 2. cmdlet을 실행하여 예약된 동기화 비활성화: `Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Hello 시작 **동기화 서비스 관리자** tooSTART → 라인으로 전환 하 여 동기화 서비스입니다.
 
 4. Toohello 이동 **작업** 탭 및 상태는 작업이 확인 *"에서"진행 중입니다.*

![동기화 서비스 관리자 - 진행 중인 작업이 없는지 확인](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>2 단계: 추가 hello 소스 특성 toohello 온-프레미스 AD 커넥터 스키마
모든 AD 특성에 가져와집니다 hello 온-프레미스 AD 커넥터 공간입니다. hello tooadd hello 소스 특성 toohello 목록 특성 가져올 수 있습니다.

 1. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.
 
 2. Hello를 마우스 오른쪽 단추로 클릭 **온-프레미스 AD 커넥터** 선택 **속성**합니다.
 
 3. Hello 팝업 대화 상자에서 이동 toohello **특성 선택** 탭 합니다.
 
 4. Hello 원본 특성 hello 특성 목록에서 선택 했는지 확인 합니다.
 
 5. 클릭 **확인** toosave 합니다.

![추가 원본 특성 tooon 온-프레미스 AD 커넥터 스키마](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>3 단계: PreferredDataLocation toohello Azure AD 커넥터 스키마를 추가 합니다.
기본적으로 hello PreferredDataLocation 특성이 Azure AD Connect 공간 hello에 가져와서 않습니다. tooadd hello PreferredDataLocation 특성 toohello 목록 가져온 특성:

 1. Toohello 이동 **커넥터** hello 동기화 서비스 관리자에서에서 탭 합니다.

 2. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD 커넥터** 선택 **속성**합니다.

 3. Hello 팝업 대화 상자에서 이동 toohello **특성 선택** 탭 합니다.

 4. Hello PreferredDataLocation 특성 hello 특성 목록에서 선택 했는지 확인 합니다.

 5. 클릭 **확인** toosave 합니다.

![원본 특성 tooAzure AD 커넥터 스키마를 추가 합니다.](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>4 단계: 온-프레미스 Active Directory에서 인바운드 동기화 규칙 tooflow hello 특성 값 만들기
hello 특성 값 tooflow hello 원본 온-프레미스 Active Directory toohello 메타 버스 특성에서 허용 하는 hello 인바운드 동기화 규칙:

1. Hello 시작 **동기화 규칙 편집기** tooSTART → 라인으로 전환 하 여 동기화 규칙 편집기입니다.

2. Hello 검색 필터 설정 **방향** toobe **인바운드**합니다.

3. 클릭 **새 규칙 추가** 단추 toocreate 새 인바운드 규칙입니다.

4. Hello에서 **설명** 탭에서 같은 구성이 hello를 제공 합니다.
 
    | 특성 | 값 | 세부 정보 |
    | --- | --- | --- |
    | 이름 | *이름 제공* | 예: *"AD에서 인바운드 - 사용자 PreferredDataLocation"* |
    | 설명 | *설명 제공* |  |
    | 연결된 시스템 | *선택 hello 온-프레미스 AD 커넥터* |  |
    | 연결된 시스템 개체 유형 | **User** |  |
    | 메타버스 개체 유형 | **Person** |  |
    | 링크 형식 | **Join** |  |
    | 우선 순위 | *1-99 사이의 숫자 선택* | 1-99는 사용자 지정 동기화 규칙을 위해 예약되어 있습니다. 다른 동기화 규칙에서 사용하는 값은 선택하지 않습니다. |

5. Toohello 이동 **범위 지정 필터** 탭 및 추가 **절 뒤 hello로 단일 범위 지정 필터 그룹**:
 
    | 특성 | 연산자 | 값 |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | 사용자\_ | 
 
    범위 지정 필터는 이 인바운드 동기화 규칙이 적용되는 온-프레미스 AD 개체를 결정합니다. 이 예제에서는 사용 하 여 hello로 사용 되는 동일한 범위 지정 필터 *"에서 from AD – 사용자 공통"* hello 동기화 규칙 되지 않도록 방지 OOB 동기화 규칙 Azure AD 사용자 쓰기 저장을 통해 생성 된 tooUser 개체를 적용 합니다. 기능입니다. Azure AD Connect 배포 tooyour에 따라 tootweak hello 범위 지정 필터를 할 수 있습니다.

6. Toohello 이동 **변환 탭** 하 고 변환 규칙을 따르는 hello를 구현 합니다.
 
    | 흐름 형식 | 대상 특성 | 원본 | 한 번 적용 | 병합 종류 |
    | --- | --- | --- | --- | --- |
    | 직접 | PreferredDataLocation | Hello 원본 특성을 선택 합니다. | 선택 취소됨 | 업데이트 |

7. 클릭 **추가** toocreate hello 인바운드 규칙입니다.

![인바운드 동기화 규칙 만들기](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>5 단계: 만들기는 아웃 바운드 동기화 규칙 tooflow hello 특성 값 tooAzure AD
Azure AD의 hello 메타 버스 toohello PreferredDataLocation 특성에서 특성 값 tooflow hello를 허용 하는 hello 아웃 바운드 동기화 규칙:

1. Toohello 이동 **동기화 규칙** 편집기입니다.

2. Hello 검색 필터 설정 **방향** toobe **아웃 바운드**합니다.

3. **새 규칙 추가** 단추를 클릭합니다.

4. Hello에서 **설명** 탭에서 같은 구성이 hello를 제공 합니다.

    | 특성 | 값 | 세부 정보 |
    | --- | --- | --- |
    | 이름 | *이름 제공* | 예를 들어 "Out tooAAD 사용자 PreferredDataLocation" |
    | 설명 | *설명 제공* |
    | 연결된 시스템 | *Hello AAD 커넥터를 선택 합니다.* |
    | 연결된 시스템 개체 유형 | 사용자 ||
    | 메타버스 개체 유형 | **Person** ||
    | 링크 형식 | **Join** ||
    | 우선 순위 | *1-99 사이의 숫자 선택* | 1-99는 사용자 지정 동기화 규칙을 위해 예약되어 있습니다. 다른 동기화 규칙에서 사용하는 값은 선택하지 않습니다. |

5. Toohello 이동 **범위 지정 필터** 탭 및 추가 **두 절과 함께 범위 지정 필터 그룹을 단일**:
 
    | 특성 | 연산자 | 값 |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | 사용자 |
    | cloudMastered | NOTEQUAL | True |

    범위 지정 필터는 이 아웃바운드 동기화 규칙이 적용되는 Azure AD 개체를 결정합니다. 이 예제에서는 사용 하 여 hello "아웃 tooAD – 사용자 Id"에서 동일한 범위 지정 필터 OOB 동기화 규칙입니다. Hello 동기화 규칙이 적용된 tooUser 개체 있는 온-프레미스 Active Directory에서 동기화 되지 않은 못하게 할 수 없습니다. Azure AD Connect 배포 tooyour에 따라 tootweak hello 범위 지정 필터를 할 수 있습니다.
    
6. Toohello 이동 **변환** 탭 하 고 변환 규칙을 따르는 hello를 구현 합니다.

    | 흐름 형식 | 대상 특성 | 원본 | 한 번 적용 | 병합 종류 |
    | --- | --- | --- | --- | --- |
    | 직접 | PreferredDataLocation | PreferredDataLocation | 선택 취소됨 | 업데이트 |

7. 닫기 **추가** toocreate hello에 대 한 아웃 바운드 규칙입니다.

![아웃바운드 동기화 규칙 만들기](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>6단계: 전체 동기화 주기 실행
일반적으로 새 특성 tooboth hello AD와 Azure AD 커넥터 스키마를 추가 했으며 사용자 지정 동기화 규칙에 도입 된 이후 전체 동기화 주기는 필요 합니다. AD tooAzure를 내보내기 전에 hello 변경 내용을 확인 하는 것이 좋습니다. Hello 전체 동기화 주기를 구성 하는 hello 단계를 수동으로 실행 하는 동안 단계 tooverify hello 변경 이후에 사용할 수 있습니다. 

1. 실행 **전체 가져오기** hello에서 단계 **온-프레미스 AD 커넥터**:

   1. Toohello 이동 **작업** hello 동기화 서비스 관리자에서에서 탭 합니다.

   2. Hello를 마우스 오른쪽 단추로 클릭 **온-프레미스 AD 커넥터** 선택 **실행...**

   3. Hello 팝업 대화 상자에서 선택 **전체 가져오기** 클릭 **확인**합니다.
    
   4. 작업 toocomplete 될 때까지 기다립니다.

    > [!NOTE]
    > 전체 가져오기 건너뛰어도 hello 경우 온-프레미스 AD 커넥터 hello 원본 특성 hello 가져온된 특성 목록에 이미 포함 되어 있습니다. 즉, 하지 않은 toomake 변경 하는 동안 [2 단계: hello 소스 특성 toohello 온-프레미스 AD 커넥터 추가 스키마](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema)합니다.

2. 실행 **전체 가져오기** hello에서 단계 **Azure AD 커넥터**:

   1. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD 커넥터** 선택 **실행...**

   2. Hello 팝업 대화 상자에서 선택 **전체 가져오기** 클릭 **확인**합니다.
   
   3. 작업 toocomplete 될 때까지 기다립니다.

3. 기존 사용자 개체에 hello 동기화 규칙 변경 내용을 확인 합니다.

온-프레미스 Active Directory와 Azure AD에서 PreferredDataLocation 가져왔는지에 hello 원본 특성에 해당 커넥터 공간 hello 합니다. 전체 동기화 단계를 계속 하기 전에 것을 수행 하는 **미리 보기** 기존 사용자에서 개체에 hello 온-프레미스 AD 커넥터 공간입니다. 선택한 hello 개체 hello 원본 특성을 채울 있어야 합니다. 성공적인 **미리 보기** hello hello 메타 버스에에서 채워진 PreferredDataLocation는 hello 동기화 규칙을 올바르게 구성 했는지 나타내는 좋은 지표로 합니다. 방법에 대 한 내용은 toodo는 **미리 보기**, toosection 참조 [hello 변경 내용을 확인](#verify-the-change)합니다.

4. 실행 **전체 동기화** hello에서 단계 **온-프레미스 AD 커넥터**:

   1. Hello를 마우스 오른쪽 단추로 클릭 **온-프레미스 AD 커넥터** 선택 **실행...**
  
   2. Hello 팝업 대화 상자에서 선택 **전체 동기화** 클릭 **확인**합니다.
   
   3. 작업 toocomplete 될 때까지 기다립니다.

5. 확인 **보류 중인 내보내기** tooAzure AD:

   1. Hello를 마우스 오른쪽 단추로 클릭 **Azure AD 커넥터** 선택 **커넥터 공간 검색**합니다.

   2. Hello 커넥터 공간 검색 팝업 대화 상자:

      1. 설정 **범위** 너무**보류 중인 내보내기**합니다.
      
      2. **추가, 수정 및 삭제**를 포함한 세 개의 확인란을 모두 선택합니다.
      
      3. Hello 클릭 **검색** 내보낼 변경 내용이 toobe 가진 개체 목록이 tooget hello 단추입니다. 지정된 된 개체에 대 한 tooexamine hello 변경 hello 개체를 두 번 클릭 합니다.
      
      4. 확인는 hello 변경 작업이 필요 합니다.

6. 실행 **내보내기** hello에서 단계 **Azure AD 커넥터**
      
   1. 마우스 오른쪽 단추로 클릭 hello **Azure AD 커넥터** 선택 **실행...**
   
   2. Hello 커넥터 실행 팝업 대화 상자에서 선택 **내보내기** 클릭 **확인**합니다.
   
   3. 내보내기 tooAzure AD toocomplete 될 때까지 기다립니다.

> [!NOTE]
> Hello 전체 동기화 단계와 hello Azure AD 커넥터에서 내보내기 단계 hello 단계가 포함 되어 있는지 확인할 수 있습니다. 온-프레미스 Active Directory tooAzure AD만에서 이동 하는 hello 특성 값 이후 hello 단계가 필요 하지 않습니다.

### <a name="step-7-re-enable-sync-scheduler"></a>7단계: 동기화 스케줄러를 다시 사용하도록 설정
Hello 기본 제공 동기화 스케줄러에 다시 사용 하도록 설정 합니다.

1. PowerShell 세션을 시작합니다.

2. cmdlet을 실행하여 예약된 동기화 다시 활성화: `Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>다음 단계
* Hello 구성 모델에 대해 자세히 읽어보세요 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.
* Hello 식 언어에 대 한 자세한 설명 [선언적 프로비저닝 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)합니다.

**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
