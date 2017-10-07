---
title: "Azure AD Connect 동기화: 실수로 인한 삭제 방지 | Microsoft Docs"
description: "이 항목에서는 hello 설명 Azure AD Connect에서 실수로 삭제 (실수로 인 한 삭제를 방지) 기능을 방지 합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Azure AD Connect 동기화: 실수로 인한 삭제 방지
이 항목에서는 hello 설명 Azure AD Connect에서 실수로 삭제 (실수로 인 한 삭제를 방지) 기능을 방지 합니다.

실수로 방지 Azure AD Connect를 설치 하는 경우 기본적으로 활성화 되어 삭제 및 구성 된 toonot 500 개 이상의 삭제를 사용 하 여 한 내보내기 허용 합니다. 이 기능은 설계 된 tooprotect 실수로 구성에서 변경 되 고 많은 사용자 및 기타 개체에 영향을 주므로 tooyour 온-프레미스 디렉터리를 변경 합니다.

## <a name="what-is-prevent-accidental-deletes"></a>실수로 인한 삭제를 방지하는 기능
다수의 삭제가 다음을 포함하는 경우의 일반적인 시나리오입니다.

* 쪽 변경[필터링](active-directory-aadconnectsync-configure-filtering.md) 여기서 전체 [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) 또는 [도메인](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) 선택 하지 않으면 합니다.
* OU의 모든 개체가 삭제됩니다.
* OU 이름이 때문에 모든 개체는 동기화의 범위를 벗어나지만 toobe 간주 됩니다.

PowerShell과 함께 hello 기본값 500 개의 개체를 변경할 수 있습니다를 사용 하 여 `Enable-ADSyncExportDeletionThreshold`합니다. 조직의이 값 toofit hello 크기를 구성 해야 합니다. Hello 동기화 스케줄러에 30 분 마다 실행 되므로 hello 값은 30 분 내에서 볼 삭제 hello 수입니다.

있는 경우 너무 많은 스테이징 된 삭제가 toobe hello 내보내기 중단 되 고 전자 메일을 받게 다음과 같이 다음 tooAzure 광고를 내보냅니다.

![실수로 인한 삭제 방지 메일](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *안녕하세요. (기술 담당자). Hello Id 동기화 서비스 (시간) hello 수가 삭제 hello 구성된 삭제 임계값 (조직 이름)을 초과 했음을 검색 했습니다. 총 (개수)개 개체가 이 ID 동기화 실행에서 삭제를 위해 전송되었습니다. 이 도달 하거나 (number) 개체의 hello 구성 삭제 임계값을 초과 합니다. ु म ी tooprovide 확인 이러한 삭제 되어야 하는 처리 진행 됩니다. 이 전자 메일 메시지에 나열 된 hello 오류에 대 한 자세한 내용은 실수로 인 한 삭제를 방지 하는 hello를 참조 하십시오.*
>
> 

Hello 상태를 확인할 수도 있습니다 `stopped-deletion-threshold-exceeded` hello에서 볼 때 **동기화 서비스 관리자** hello 내보낸 프로필에 대 한 UI입니다.
![실수로 인한 삭제 방지 동기화 서비스 관리자 UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

예상된 경우가 아니라면 조사하여 수정 작업을 수행합니다. 개체가 toobe 삭제에 대 한 toosee 다음 hello지 않습니다.

1. 시작 **동기화 서비스** hello 시작 메뉴에서에서 합니다.
2. 너무 이동**커넥터**합니다.
3. 형식과 선택 hello 커넥터 **Azure Active Directory**합니다.
4. 아래 **동작** toohello 오른쪽, 선택 **커넥터 공간 검색**합니다.
5. 팝업 hello에 **범위**선택, **연결이 끊어진 이후** 고 hello 과거의 시간을 선택 합니다. **검색**을 클릭합니다. 이 페이지에서는 toobe 삭제에 대 한 모든 개체의 뷰를 제공 합니다. 각 항목을 클릭 하 여 hello 개체에 대 한 추가 정보를 얻을 수 있습니다. 클릭할 수도 있습니다 **열 설정** tooadd 추가 특성 toobe hello 표에 표시 합니다.

![커넥터 공간 검색](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

원하는 경우 모든 hello 삭제 한 다음 수행 hello 다음:

1. tooretrieve hello 현재 삭제 임계값을 hello PowerShell cmdlet을 실행 `Get-ADSyncExportDeletionThreshold`합니다. Azure AD 전역 관리자 계정 및 암호를 제공합니다. hello 기본값은 500입니다.
2. tootemporarily이이 보호를 사용 하지 않도록 설정 하 고 이러한 삭제 통과, hello PowerShell cmdlet을 실행 하도록: `Disable-ADSyncExportDeletionThreshold`합니다. Azure AD 전역 관리자 계정 및 암호를 제공합니다.
   ![자격 증명](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Azure Active Directory Connector가 선택 된 hello로 hello 작업을 선택 **실행** 선택 **내보내기**합니다.
4. hello 보호 toore 사용, hello PowerShell cmdlet을 실행: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`합니다. 500 hello 현재 삭제 임계값을 검색할 때 자신이 hello 값으로 대체 합니다. Azure AD 전역 관리자 계정 및 암호를 제공합니다.

## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
