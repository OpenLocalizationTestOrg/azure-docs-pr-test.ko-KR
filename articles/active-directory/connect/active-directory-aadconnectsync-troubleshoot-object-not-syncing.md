---
title: "aaaTroubleshoot tooAzure AD 동기화 되지 않은 개체 | Microsoft Docs"
description: "개체 tooAzure AD 동기화 되지 않는 이유를 해결 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>TooAzure AD를 동기화 하는 개체 문제 해결

개체가 예상된 tooAzure AD로 동기화 되지 않고, 여러 가지 이유로 인해 수 있습니다. Azure AD에서 오류 전자 메일을 받은 또는 Azure AD Connect Health에서 hello 오류를 참조 하는 경우 다음 읽을 [내보내기 오류 문제 해결](active-directory-aadconnect-troubleshoot-sync-errors.md) 대신 합니다. 하지만 hello 개체 된 Azure AD에서 문제를 해결 하는 경우 다음이 항목은 있습니다. Toofind 오류 hello 온-프레미스 구성 요소 Azure AD Connect에서 동기화 하는 방법을 설명 합니다.

toofind hello 오류 toolook 순서에 따라 hello에서 몇 가지 다른 위치에 보아야 합니다.

1. hello [작업 로그](#operations) 가져오기 및 동기화 중 hello 동기화 엔진에 의해 식별 된 오류를 찾기 위한 합니다.
2. hello [커넥터 공간](#connector-space-object-properties) 누락 된 개체 및 동기화 오류를 찾기 위한 합니다.
3. hello [메타 버스](#metaverse-object-properties) 데이터 관련 문제를 찾기 위한 합니다.

이러한 단계를 시작하기 전에 [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)를 시작합니다.

## <a name="operations"></a>작업
hello 동기화 서비스 관리자의에서 작업 탭 hello 문제 해결를 시작 하는 데 해야입니다. 작업 탭 hello hello 가장 최근 작업에서 hello 결과 보여 줍니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

hello 위쪽 절반 모든 실행 순간적인 순서가 표시 됩니다. 기본적으로 hello 작업 로그 정보를 유지 관리 hello에 대 한 지난 7 일 하지만 hello로이 설정을 변경할 수 있습니다 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md)합니다. 성공 상태를 표시 하지 않는 모든 실행에 대 한 toolook을 원하는 합니다. Hello hello 머리글을 클릭 하 여 정렬을 변경할 수 있습니다.

hello **상태** 열이 hello 가장 중요 한 정보 및 실행에 대해 가장 심각한 문제를 hello 보여 줍니다. 간단히 요약 한 hello 가장 일반적인 상태 tooinvestigate 우선 순위 순서 대로 다음과 같습니다 (여기서 * 나타내는 여러 가지 가능한 오류 문자열)입니다.

| 가동 상태 | 주석 |
| --- | --- |
| stopped-* |hello 실행을 완료할 수 없습니다. 예를 들어 경우 hello 원격 시스템 다운 되어에 연결할 수 없습니다. |
| stopped-error-limit |5000개보다 많은 오류가 있습니다. 실행 하는 hello toohello 오류가 많이 인해 자동으로 중지 되었습니다. |
| completed-\*-errors |hello 실행을 완료 하지만 조사 해야 하는 오류 (미만 5000). |
| completed-\*-warnings |실행 하는 hello 완료 되었지만 일부 데이터가 예상 hello 상태에 있지 않습니다. 오류가 발생하는 경우 이 메시지는 일반적으로 증상일 뿐입니다. 오류를 해결할 때까지 경고를 조사하지 않습니다. |
| 성공 |문제가 없습니다. |

행을 선택 하면 hello 아래쪽의를 실행 하는 tooshow hello 세부 정보를 업데이트 합니다. toohello hello 아래쪽의 맨 왼쪽, 목록 라는 해야할 **단계 #**합니다. 이 목록은 각 도메인을 단계로 나타내는 포리스트에 여러 도메인이 있는 경우에만 표시됩니다. hello 도메인 이름은 hello 머리글 아래에서 찾을 수 있습니다 **파티션**합니다. 아래 **동기화 통계**, 처리 된 변경 내용 수 hello에 대 한 자세한 정보를 찾을 수 있습니다. Hello 링크 tooget hello 변경 개체의 목록을 클릭 수 있습니다. 오류가 있는 개체가 있으면 해당 오류는 **동기화 오류**아래에 표시됩니다.

### <a name="troubleshoot-errors-in-operations-tab"></a>작업 탭에서 오류 문제 해결
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
오류가 발생 하는 경우 두 hello와 개체에 오류 hello 오류 자체는 자세한 정보를 제공 하는 링크입니다.

Hello 오류 문자열을 클릭 하 여 시작 (**동기화 규칙-오류-함수-트리거** hello 그림에). 먼저 hello 개체에 대해 간략하게 표시 됩니다. toosee hello 실제 오류 hello 단추 클릭 **스택 추적**합니다. 이 추적은 hello 오류에 대 한 디버그 수준 정보를 제공합니다.

Hello에서 마우스 오른쪽 단추로 클릭 수 **호출 스택 정보가** 상자 **모두 선택**, 및 **복사**합니다. Hello 스택을 복사 고 선호 하는 편집기, 메모장과 같은 hello 오류에서 확인 합니다.

* Hello 오류가에서 이면 **SyncRulesEngine**, hello 호출 스택 정보는 먼저 모든 특성의 목록을 hello 개체에는 합니다. Hello 머리글 표시 될 때까지 아래로 스크롤하여 **InnerException = >**합니다.  
  ![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  hello 선 표시 hello 오류 후입니다. 위의 hello 그림에서 생성 하는 사용자 지정 동기화 규칙 Fabrikam에서 hello 오류는 합니다.

Hello 오류 자체는 충분 한 정보를 제공 하지 않습니다, 시간 toolook hello 데이터 자체에 것입니다. Hello 개체 식별자를 가진 hello 링크를 클릭 하 고 계속 hello 해결 [커넥터 공간 가져온된 개체](#cs-import)합니다.

## <a name="connector-space-object-properties"></a>커넥터 공간 개체 속성
Hello에서 발견 된 오류 있는지 [작업](#operations) hello 다음 단계는 Active Directory, toohello 메타 버스 및 tooAzure AD에서 toofollow hello 커넥터 공간 개체 탭 합니다. 이 경로에 hello 문제는 위치를 찾아야 합니다.

### <a name="search-for-an-object-in-hello-cs"></a>Hello CS에서에서 개체 검색

**동기화 서비스 관리자**, 클릭 **커넥터**, 선택 hello Active Directory Connector 및 **커넥터 공간 검색**합니다.

**범위**선택, **RDN** (하려는 경우 hello CN 특성에 toosearch) 또는 **DN 또는 앵커** (하려는 경우 toosearch hello 고유 이름 특성에). 값을 입력하고 **검색**을 클릭합니다.  
![커넥터 공간 검색](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Hello 개체를 찾지 않을 경우 찾고, 다음와 필터링 된 것 수 [도메인 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) 또는 [OU 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)합니다. 읽기 hello [필터링 구성](active-directory-aadconnectsync-configure-filtering.md) 필터링 hello 항목 tooverify 예상 대로 구성 되어 있습니다.

또 다른 유용한 검색을 tooselect hello Azure AD 커넥터 **범위** 선택 **보류 중인 가져오기**, 및 select hello **추가** 확인란을 선택 합니다. 이 검색은 온-프레미스 개체와 연결될 수 없는 Azure AD의 모든 동기화된 개체를 제공합니다.  
![커넥터 공간 검색 고아](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
이러한 개체는 다른 동기화 엔진 또는 다른 필터링 구성을 갖는 동기화 엔진에서 만들어졌습니다. 이 보기는 더 이상 관리되지 않는 **고아** 개체 목록입니다. 이 목록을 검토 하 고 hello를 사용 하 여 이러한 개체를 제거 하는 것이 좋습니다. 해야 [Azure AD PowerShell](http://aka.ms/aadposh) cmdlet.

### <a name="cs-import"></a>CS 가져오기
Cs 개체를 열 때 hello 위쪽에 여러 탭 있습니다. hello **가져올** 가져오기 후 준비 된 hello 데이터 탭에 표시 합니다.  
![CS 개체](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
hello **이전 값** 현재 저장 된 항목의 연결 및 hello 표시 **새 값** hello 원본 시스템에서 수신 되었습니다 대상과 아직 적용 되지 않았습니다. Hello 개체에 오류가 발생 하는 경우 변경 내용이 처리 되지 않습니다.

**오류**  
![CS 개체](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
hello **동기화 오류** 탭만 hello 개체와 문제가 있는 경우에 표시 됩니다. 자세한 내용은 [동기화 오류 해결](#troubleshoot-errors-in-operations-tab)을 참조하세요.

### <a name="cs-lineage"></a>CS 계보
hello 계보 탭 hello 커넥터 공간 개체 관련된 toohello 메타 버스 개체를가 하는 방식을 보여 줍니다. 연결 된 시스템 hello 및 적용 된 규칙의 데이터를 toopopulate hello 메타 버스 hello 커넥터 마지막에서 변경 된 내용을 가져올 때 볼 수 있습니다.  
![CS 계보](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
Hello에 **동작** 열 하나씩을 볼 수 있습니다 **인바운드** hello 액션과 동기화 규칙 **프로 비전**합니다. 이 커넥터 공간 개체가 있는으로 hello 메타 버스 개체 하 게 유지 되도록 나타내는입니다. 동기화 규칙 hello 목록 대신 방향 사용 하는 동기화 규칙을 표시 하는 경우 **아웃 바운드** 및 **프로 비전**, 나타냅니다 hello 메타 버스 개체가 삭제 될 때이 개체를 삭제 합니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Hello에서 확인할 수 있습니다 **PasswordSync** hello 인바운드 커넥터 공간 열 하나의 동기화 규칙 hello 값이 있으므로 변경 내용을 toohello 암호 기여할 수 있는 **True**합니다. 이 암호 tooAzure AD hello 아웃 바운드 규칙을 통해 전송 됩니다.

Hello 계보 탭에서을 클릭 하 여 toohello 메타 버스를 얻을 수 [메타 버스 개체 속성](#mv-attributes)합니다.

모든 탭 hello 맨 아래에 두 개의 단추가: **미리 보기** 및 **로그**합니다.

### <a name="preview"></a>미리 보기
hello 미리 보기 페이지는 사용 되는 toosynchronize 하나 단일 개체입니다. 일부 사용자 지정 동기화 규칙을 해결 하는 단일 개체에 대 한 변경의 toosee hello 결과 줄이려는 경우에 유용 합니다. **전체 동기화**와 **델타 동기화** 중에서 선택할 수 있습니다. 간에 선택할 수 있습니다 **미리 보기 생성**, 메모리에 hello 변경만 유지 및 **커밋 미리 보기**, hello 메타 버스는 업데이트 및 모든 단계 tootarget 커넥터 공간을 변경 합니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Hello 개체 및 특정 특성 흐름에 대 한 규칙 적용을 검사할 수 있습니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>로그
hello 로그 페이지에 사용 되는 toosee hello 암호 동기화 상태 및 기록을 있습니다. 자세한 내용은 [암호 동기화 문제 해결](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)을 참조하세요.

## <a name="metaverse-object-properties"></a>메타버스 개체 속성
일반적으로 더 나은 toostart hello 원본 Active Directory에서에서 검색 되었기 [커넥터 공간](#connector-space)합니다. 하지만 hello 메타 버스에서 검색을 시작할 수도 있습니다.

### <a name="search-for-an-object-in-hello-mv"></a>Hello MV의에서 개체 검색
**Synchronization Service Manager**에서 **메타버스 검색**을 클릭합니다. 찾습니다 hello 사용자를 알고 있는 쿼리를 만듭니다. accountName(sAMAccountName) 및 UserPrincipalName 등의 일반적인 특성을 검색할 수 있습니다. 자세한 내용은 [메타버스 검색](active-directory-aadconnectsync-service-manager-ui-mvsearch.md)을 참조하세요.
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

Hello에 **검색 결과** 창의 hello 개체를 클릭 합니다.

Hello 개체를 찾지 않았습니다 다음 아직 도달 하지 hello 메타 버스입니다. Hello 개체에 대 한 toosearch hello Active Directory에서에서 계속 [커넥터 공간](#connector-space-object-properties)합니다. 향후 toohello 메타 버스의 개체를 hello를 차단 하는 동기화에서 오류가 있을 수 또는 적용 된 필터가 있을 수 있습니다.

### <a name="mv-attributes"></a>MV 특성
Hello 특성 탭 hello 값을 볼 수 있습니다 하 고 어떤 커넥터를 제공한 것입니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

개체를 동기화 할 경우 hello hello 메타 버스 특성에 따라 다음 확인 합니다.
- 속성이 있는 hello **cloudFiltered** 너무 설정**true**? 인 경우의 toohello 단계에 따라 필터링 된가 [특성 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering)합니다.
- 속성이 있는 hello **sourceAnchor** 존재? 없으면 계정-리소스 포리스트 토폴로지가 있나요? 개체는 연결된 된 사서함으로 확인 되 면 (hello 특성 **msExchRecipientTypeDetails** 에 hello 값 2), 활성화 된 Active Directory 계정으로 hello 포리스트에서 hello sourceAnchor를 제공 합니다. Hello 마스터 계정 가져오고 올바르게 동기화 되어 있는지 확인 합니다. hello 마스터 계정 hello에 나열 되어야 합니다 [커넥터](#mv-connectors) hello 개체에 대 한 합니다.

### <a name="mv-connectors"></a>MV 커넥터
hello 커넥터 탭 hello 개체의 표시 하는 모든 커넥터 공간 표시 됩니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
다음에 대한 커넥터가 있어야 합니다.

- 각 Active Directory 포리스트 hello 사용자가 표시 됩니다. 이 표시에는 foreignSecurityPrincipals 및 Contact 개체가 포함될 수 있습니다.
- Azure AD의 커넥터.

Hello 커넥터 tooAzure AD 없으면 다음 읽을 [MV 특성](#MV-attributes) 되기 위한 tooverify hello 조건을 tooAzure AD 사용자를 프로 비전 합니다.

이 탭도 있습니다 toonavigate toohello [커넥터 공간 개체](#connector-space-object-properties)합니다. 행을 선택하고 **속성**을 클릭합니다.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
