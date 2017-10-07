---
title: "hello Azure AD 동기화 서비스 관리자 UI에서에서 aaaConnectors | Microsoft Docs"
description: "Azure AD Connect에 대 한 hello 커넥터 탭에서 hello 동기화 서비스 관리자를 이해 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>커넥터를 사용 하 여 Azure AD Connect 동기화 서비스 관리자 hello로

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

hello 커넥터 탭을 사용 하는 toomanage 모든 시스템 hello 동기화 엔진에 연결 되어 있습니다.

## <a name="connector-actions"></a>커넥터 작업
| 작업 | 주석 |
| --- | --- |
| 생성 |사용 안 함. Tooadditional AD 포리스트를 연결 하기 위한 hello 설치 마법사를 사용 합니다. |
| properties |모든 도메인 및 OU 필터링에 사용 |
| [삭제](#delete) |사용 되는 tooeither hello 커넥터 공간 또는 포리스트에서 toodelete 연결 tooa hello 데이터를 삭제 합니다. |
| [실행 프로필 구성](#configure-run-profiles) |아무 것도 필터링 하는 도메인을 제외한 tooconfigure 여기 합니다. 이 작업을 사용할 수 있습니다 toosee 이미 구성 된 실행 프로필. |
| 실행 |Toostart 일회용 프로필의 실행을 사용 합니다. |
| 중지 |현재 프로필을 실행하는 커넥터 중지 |
| 커넥터 내보내기 |사용 안 함. |
| 커넥터 가져오기 |사용 안 함. |
| 커넥터 업데이트 |사용 안 함. |
| 스키마 새로 고침 |Hello 캐시 된 스키마를 새로 고칩니다. 기본 toouse hello 옵션 이므로 hello 설치 마법사에서 대신는 이후에 업데이트 동기화 규칙입니다. |
| [커넥터 공간 검색](#search-connector-space) |사용 되는 toofind 개체 및 너무[개체 및 hello 시스템을 통해 해당 데이터에 따라](#follow-an-object-and-its-data-through-the-system)합니다. |

### <a name="delete"></a>삭제
hello 삭제 동작이 서로 구분에 사용 됩니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

옵션 hello **커넥터 공간에만 삭제** 유지 hello 구성 하지만 모든 데이터를 제거 합니다.

옵션 hello **커넥터를 삭제 하 고 커넥터 공간** hello 데이터와 hello 구성 제거 합니다. 이 옵션은 tooconnect tooa 포리스트를 더 이상 원하지 않는 경우 사용 됩니다.

두 옵션 모두 모든 개체를 동기화 하 고 hello 메타 버스 개체를 업데이트 합니다. 이 작업은 장기 실행 작업입니다.

### <a name="configure-run-profiles"></a>실행 프로필 구성
이 옵션을 사용 toosee hello를 실행 프로필 커넥터에 대해 구성 되어 있습니다.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>커넥터 공간 검색
hello 검색 커넥터 공간 작업은 유용한 toofind 개체 및 데이터 문제를 해결 합니다.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

먼저 **범위**를 선택합니다. (RDN, DN 앵커, 하위 트리)에 따라 데이터를 검색할 수 있습니다 또는 hello 개체 (다른 모든 옵션의 경우)의 상태입니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
예를 들어 하위 트리 검색을 수행하는 경우 모든 개체를 하나의 OU로 가져옵니다.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
이 표에서 개체를 선택, 선택 수 **속성**, 및 [뒤](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) hello 메타 버스를 통해 hello 원본 커넥터 공간 및 toohello 대상 커넥터 공간에서 합니다.

### <a name="changing-hello-ad-ds-account-password"></a>Hello AD DS 계정 암호 변경
Hello 계정 암호를 변경 하는 경우 동기화 서비스 hello 됩니다 수 tooimport/내보내기 변경 tooon 온-프레미스 AD 합니다.   Hello 다음을 표시 될 수 있습니다.

- hello AD 커넥터에 대 한 hello 가져오기/내보내기 단계 "-시작-자격 증명 없음" 오류와 함께 실패 합니다.
- 아래의 Windows 이벤트 뷰어 hello 응용 프로그램 이벤트 로그에 이벤트 ID 6000 및 메시지와 함께 오류 "hello 자격 증명이 잘못 되었기 때문에 관리 에이전트"contoso.com"실패 toorun hello."

tooresolve hello 실행 hello 다음을 사용 하 여 hello AD DS 사용자 계정 업데이트 합니다.


1. Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Toohello 이동 **커넥터** 탭 합니다.
3. Hello 구성된 toouse hello AD DS 계정에는 AD 커넥터를 선택 합니다.
4. 작업 아래에서 **속성**을 선택합니다.
5. Hello 팝업 대화 상자에서 연결 tooActive Directory 포리스트를 선택 합니다.
6. hello 포리스트 이름 나타냅니다 hello 해당 온-프레미스 AD 합니다.
7. hello 사용자 이름은 hello AD DS 계정 동기화 사용을 나타냅니다.
8. Hello 암호 텍스트 상자에 hello hello AD DS 계정의 새 암호를 입력 ![Azure AD 연결 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. 확인 toosave hello에 대 한 새 암호를 클릭 하 고 hello 동기화 서비스 tooremove hello에서에서 이전 암호 메모리 캐시를 다시 시작 합니다.



## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
