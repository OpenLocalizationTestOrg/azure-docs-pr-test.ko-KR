---
title: "aaaTroubleshooting 하이브리드 Azure Active Directory 가입 Windows 10 및 Windows Server 2016 장치 | Microsoft Docs"
description: "Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결 

이 항목은 적용 가능한 toohello 다음 클라이언트:

-   Windows 10
-   Windows Server 2016

다른 Windows 클라이언트의 경우 [하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-legacy.md)을 참조하세요.

이 항목에서는 있다고 가정 [구성 된 하이브리드 Azure Active Directory 가입 장치](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello 다음 시나리오:

- 장치 기반 조건부 액세스

- [엔터프라이즈 설정 로밍](active-directory-windows-enterprise-state-roaming-overview.md)

- [비즈니스용 Windows Hello](active-directory-azureadjoin-passport-deployment.md)


이 문서에 어떻게 tooresolve 잠재적 문제 해결 지침을 제공 합니다. 


Azure Active Directory join 지원 hello Windows 하이브리드 Windows 10 및 Windows Server 2016에 대 한 10 2015 년 11 월 업데이트 이상. Hello Anniversary 업데이트를 사용 하는 것이 좋습니다.

## <a name="step-1-retrieve-hello-join-status"></a>1 단계: hello 조인 상태를 검색 합니다. 

**tooretrieve hello 조인 상태:**

1. 관리자 권한으로 명령 프롬프트를 열고 hello

2. **dsregcmd /status**를 입력합니다.



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: DeviceId 없음: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 지문: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 플랫폼 암호화 공급자 TpmProtected: 예 KeySignTest:: tootest 상승 된 실행 해야 합니다.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>2 단계: hello 조인 상태를 평가 합니다. 

Hello 다음 필드를 검토 하 고 hello 예상 값을 갖는지 확인 하십시오.

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

이 필드는 hello 장치가 Azure AD와 연결 되 고 있는지 여부를 나타냅니다. Hello 값이 **아니요**, hello 조인 tooAzure AD 아직 완료 되지 않았습니다. 

**가능한 원인:**

- 조인에 대 한 hello 컴퓨터의 인증에 실패 했습니다.

- Hello 컴퓨터도 찾을 수 없습니다 hello 조직 중인 HTTP 프록시

- hello 컴퓨터 등록에 대 한 Azure AD tooauthenticate 또는 Azure DRS에 연결할 수 없습니다.

- hello 컴퓨터 아닐 hello 조직의 내부 네트워크 또는 VPN의 직선 tooan와 온-프레미스 AD 도메인 컨트롤러입니다.

- Hello 컴퓨터에서 TPM을 잘못 된 상태에 수 있습니다.

- Hello 서비스에서 잘못 된 구성 앞에서 기록한 hello 문서에 다시 tooverify를 필요 함이 있을 수 있습니다. 일반적인 예제는 다음과 같습니다.

    - 페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.

    - 페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않습니다.

    - Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없는

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

이 필드는 hello 장치가 가입 된 여부 tooan 온-프레미스 Active Directory 여부를 나타냅니다. Hello 값이 **아니요**, hello 장치는 Azure AD 하이브리드 조인을 수행할 수 없습니다.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

이 필드 hello 장치를 개인 장치로 Azure AD에 등록 되었는지 여부를 나타냅니다 (로 표시 된 *작업 공간 연결*). 이 값은 하이브리드 Azure AD 조인된 도메인에 가입된 컴퓨터에 대해 **아니요**이어야 합니다. Hello 값이 **예**, 회사 또는 학교 계정을 hello Azure AD 하이브리드 조인의 이전 toohello 완료 추가 되었습니다. 이 경우 hello 계정은 Windows 10 (1607)의 hello Anniversary 업데이트 버전을 사용 하는 경우 무시 됩니다.

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES 및 AzureADPrt : YES
  
이러한 필드는 hello 사용자 tooAzure AD가 성공적으로 인증 여부를 나타내는 toohello 장치에 로그인 할 때입니다. Hello 값이 **아니요**, 때문일 수 있습니다.

- 등록 (확인 hello KeySignTest 높은 실행 하는 동안) 시 hello 장치와 연결 된 TPM의 잘못 된 저장소 키 (STK)입니다.

- 대체 로그인 ID

- HTTP 프록시를 찾을 수 없음

## <a name="next-steps"></a>다음 단계

질문에 대 한 참조 hello [장치 관리 FAQ](device-management-faq.md) 
