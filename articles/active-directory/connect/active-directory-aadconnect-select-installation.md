---
title: "Azure AD Connect: 설치 유형 선택 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect에 대 한 tooselect hello 설치 toouse 입력 하는 방법"
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
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Azure AD Connect에 대 한 설치 유형을 toouse 어떤 선택
Azure AD Connect에서는 새 설치에 대해 기본 및 사용자 지정의 두 가지 설치 유형을 제공합니다. 이 항목 toouse 옵션을 설치 하는 동안 toodecide 수 있습니다.

## <a name="express"></a>Express
Express는 hello 가장 일반적인 옵션이 며 모든 새 설치의 약 90%에서 사용 됩니다. 디자인 된 tooprovide hello 가장 일반적인 고객 시나리오에 적합 한 구성이 있었습니다.

이 옵션에서는 다음과 같이 전제합니다.

- 단일 Active Directory 포리스트 온-프레미스가 있습니다.
- 사용자에 게 엔터프라이즈 관리자 계정이 hello 설치에 사용할 수 있습니다.
- 온-프레미스 Active Directory에 100,000개 미만의 개체가 있습니다.

다음 기능을 사용할 수 있습니다.

- [암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 에서 single sign on에 대 한 온-프레미스 tooAzure AD.
- [사용자, 그룹, 연락처 및 Windows 10 컴퓨터](active-directory-aadconnectsync-understanding-default-configuration.md)를 동기화하는 구성
- 모든 도메인 및 모든 OU에 포함된 적합한 모든 개체의 동기화
- [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 활성화 toomake hello 사용 가능한 최신 버전을 항상 사용 됩니다.

기본을 계속 사용할 수 있는 경우의 옵션:

- 하지 않을 경우 toosynchronize 모든 Ou, Express를 사용 하 고 수 있습니다를 hello 마지막 페이지에서 선택 취소 **hello 동기화 프로세스를 시작 중...** *. Hello 설치 마법사를 다시 실행 하 고 변경의 hello Ou [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) 예약 된 동기화를 사용 하도록 설정 합니다.
- 암호 쓰기 저장 등 tooenable hello Azure AD Premium 기능 중 하나 사용 하는 것이 좋습니다. Express tooget hello 초기 설치가 완료를 먼저 거치지 합니다. Hello 설치 마법사를 다시 실행 하 고 hello 변경 [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)합니다.

## <a name="custom"></a>사용자 지정
사용자 지정 된 경로 hello express 보다 더 많은 옵션을 허용합니다. Express에 대 한 이전 섹션에서 설명 하는 hello 구성을 조직에 대 한 대표 하지 않은 모든 경우에 사용 해야 합니다.

사용하는 경우:

- Active Directory에 액세스 tooan 엔터프라이즈 관리자 계정이 없는 합니다.
- 둘 이상의 포리스트 했거나 toosynchronize 이후 hello에서 둘 이상의 포리스트를 계획 합니다.
- Hello 연결 서버와에서 연결할 수 없는 포리스트 내의 도메인 해야합니다.
- Toouse 페더레이션 또는 사용자 로그인에 대 한 통과 인증을 계획 합니다.
- 100, 000 개 이상의 개체에 있고 toouse 전체 SQL Server 필요 합니다.
- 확인할 계획 toouse 그룹 기반 필터링 및 뿐만 아니라 도메인 이나 OU 기반 필터링 합니다.

## <a name="upgrade-from-dirsync"></a>DirSync에서 업그레이드
현재 디렉터리 동기화를 사용 하는 경우 다음에서 다음과 같이 hello [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade 기존 구성 합니다. 업그레이드 옵션에는 다음 두 가지가 있습니다.

- 동일한 hello의 현재 위치 업그레이드 tooinstall 연결할 서버입니다.
- 기존 DirSync 서버 hello 계속 작동 하는 동안 새 서버에 배포 tooinstall Connect와 유사 합니다.

## <a name="upgrade-from-azure-ad-sync"></a>Azure AD Sync에서 업그레이드
현재 Azure AD Sync를 사용 하는 경우 hello 참고할 수 [동일한 단계](active-directory-aadconnect-upgrade-previous-version.md) 으로 하나의 연결 버전 tooa 최신에서 업그레이드 하는 경우. 업그레이드 옵션에는 다음 두 가지가 있습니다.

- 동일한 hello의 현재 위치 업그레이드 tooinstall 연결할 서버입니다.
- 기존 Azure AD Sync 서버 hello 하는 동안 새 서버에서 마이그레이션 회전 tooinstall 연결도 계속 실행 합니다.

## <a name="migrate-from-fim2010-or-mim2016"></a>FIM2010 또는 MIM2016에서 마이그레이션
사용 중인 경우 현재 Forefront Identity Manager 2010 또는 Microsoft Identity Manager 2016 hello Azure AD 커넥터 있는 유일한 옵션은 마이그레이션. 에 설명 된 hello 단계에 따라 [회전 마이그레이션](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)합니다. Hello 단계에서는 Azure AD Sync의 모든 댓글을 FIM2010/MIM2016 바꿉니다.

## <a name="next-steps"></a>다음 단계
Toouse hello 옵션에 따라 선택한, hello 테이블을 사용 하 여 hello로 문서 콘텐츠 toohello 왼쪽된 toofind의 자세한 단계입니다.
