---
title: "Azure AD Connect: 기본 설정을 사용하여 시작 | Microsoft Docs"
description: "Toodownload를 설치 하 고 Azure AD Connect에 대 한 hello 설치 마법사를 실행 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>기본 설정을 사용하여 Azure AD Connect 시작
인증을 위한 단일 포리스트 토폴로지 및 **암호 동기화**가 있는 경우 Azure AD Connect [Express 설정](active-directory-aadconnectsync-implement-password-synchronization.md)을 사용합니다. **고속 설정** hello 기본 옵션이 며 가장 일반적으로 배포 된 hello 시나리오에 사용 됩니다. 하면 온-프레미스 디렉터리 toohello 클라우드만 몇 번의 클릭 짧은 트래버스하여 tooextend 됩니다.

Azure AD Connect 설치를 시작 하기 전에 있어야 너무[Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771) 및 전체 hello 필수 단계를 [Azure AD Connect: 하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다.

Express 설정이 토폴로지와 일치하지 않는 경우 다른 시나리오는 [관련 설명서](#related-documentation) 를 참조하세요.

## <a name="express-installation-of-azure-ad-connect"></a>Azure AD Connect의 빠른 설치
Hello에 대 한 작업에서 다음이 단계를 확인할 수 있습니다 [비디오](#videos) 섹션.

1. Azure AD Connect tooinstall에 원하는 로컬 관리자 toohello 서버에 로그인 합니다. Hello 서버에서이 작업을 수행 해야 toobe hello 동기화 서버를 선택 합니다.
2. Tooand 두 번 클릭 탐색 **AzureADConnect.msi**합니다.
3. Hello 시작 화면에 hello 상자 합의 toohello 라이선스 조건을 선택 하 고 클릭 **계속**합니다.  
4. Hello Express 설정 화면에서 클릭 **기본 설정 사용**합니다.  
   ![시작 tooAzure AD 연결](./media/active-directory-aadconnect-get-started-express/express.png)
5. Hello 연결 tooAzure AD 화면에서 Azure AD에 대 한 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다. **다음**을 누릅니다.  
   ![TooAzure AD 연결](./media/active-directory-aadconnect-get-started-express/connectaad.png) 오류가 발생 하 고 연결에 문제가 있을 경우 다음 참조 [연결 문제를 해결](active-directory-aadconnect-troubleshoot-connectivity.md)합니다.
6. Hello 연결 tooAD DS 화면에는 엔터프라이즈 관리자 계정에 대 한 hello 사용자 이름 및 암호를 입력 합니다. Hello 도메인 부분, 즉 FABRIKAM\administrator 또는 fabrikam.com\administrator NetBios 또는 FQDN 형식으로 입력할 수 있습니다. **다음**을 누릅니다.  
   ![DS tooAD 연결](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. hello [ **Azure AD 로그인 구성** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) 페이지 완료 하지 않은 경우 표시 [도메인 확인](../active-directory-add-domain.md) hello에 [필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다.
   ![확인되지 않은 도메인](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   이 페이지를 표시하는 경우 **추가되지 않음** 및 **확인되지 않음**으로 표시된 모든 도메인을 검토합니다. 사용한 해당 도메인을 Azure AD에서 확인하도록 합니다. 도메인을 확인 한 경우 hello 새로 고침 기호를 클릭 합니다.
8. Hello 준비 tooconfigure 화면 클릭 **설치**합니다.
   * 필요에 따라 hello 준비 tooconfigure 페이지에서 선택 취소할 수 있습니다 hello **구성이 완료 되는 즉시 hello 동기화 프로세스를 시작** 확인란을 선택 합니다. 와 같은 toodo의 추가 구성을 사용 하려는 경우이 확인란 선택을 취소 해야 [필터링](active-directory-aadconnectsync-configure-filtering.md)합니다. 이 옵션의 선택을 취소 하면 hello 마법사 동기화 구성 되지만 hello 스케줄러를 사용 하지 않도록 설정 합니다. 수동으로 설정할 때까지 실행 되지 않습니다 [hello 설치 마법사를 다시 실행](active-directory-aadconnectsync-installation-wizard.md)합니다.
   * Exchange 온-프레미스 Active Directory에 있는 경우 옵션 tooenable 있습니다 [ **Exchange 하이브리드 배포**](https://technet.microsoft.com/library/jj200581.aspx)합니다. 계획 toohave Exchange 사서함 모두 hello 클라우드 및 온-프레미스 hello에 동일 하는 경우이 옵션을 사용 하도록 설정 시간입니다.
     ![Azure AD Connect tooconfigure 준비 됨](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Hello 설치가 완료 되 면 클릭 **종료**합니다.
10. Hello 설치가 완료 된 후 로그 오프 하 고 동기화 서비스 관리자 또는 동기화 규칙 편집기를 사용 하기 전에 다시 로그인 합니다.

## <a name="videos"></a>비디오
Hello 빠른 설치를 사용 하 여 관련 한 비디오를 참조 하세요.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>다음 단계
Azure AD Connect를 설치 했으므로 다음을 할 수 있습니다 [hello 설치 되었는지 확인 하 고 라이선스를 할당](active-directory-aadconnect-whats-next.md)합니다.

Hello 설치를 사용 하도록 설정 된 이러한 기능에 대 한 자세한 정보: [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md), [실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), 및 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)합니다.

이러한 공통 항목에 대 한 자세한 정보: [스케줄러와 tootrigger 동기화 방법을](active-directory-aadconnectsync-feature-scheduler.md)합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

## <a name="related-documentation"></a>관련 설명서
| 항목 |
| --- | --- |
| Azure AD Connect 개요 |
| 사용자 지정된 설정을 사용하여 설치 |
| DirSync에서 업그레이드 |
| 설치에 사용되는 계정 |

