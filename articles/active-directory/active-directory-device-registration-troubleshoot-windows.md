---
title: "Windows 10 및 Windows Server 2016 용 aaaTroubleshooting hello 자동 등록의 Azure AD 도메인 연결 컴퓨터 | Microsoft Docs"
description: "Windows 10 및 Windows Server 2016에 대 한 연결 컴퓨터를 Azure AD 도메인의 hello 자동 등록 문제를 해결 합니다."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>가입 된 컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016 도메인의 자동 등록 문제 해결

이 항목은 적용 가능한 toohello 다음 클라이언트:

-   Windows 10
-   Windows Server 2016

다른 Windows 클라이언트에 대 한 참조 [Windows 하위 클라이언트에 대 한 컴퓨터 tooAzure AD 가입 된 도메인의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows-legacy.md)합니다.

이 항목에서는 구성 자동 등록의 도메인에 가입 된 장치에서 설명한 대로 설명 된 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-device-registration-get-started.md) 다음 시나리오는 toosupport hello:

- [장치 기반 조건부 액세스](active-directory-conditional-access-automatic-device-registration-setup.md)

- [엔터프라이즈 설정 로밍](active-directory-windows-enterprise-state-roaming-overview.md)

- [비즈니스용 Windows Hello](active-directory-azureadjoin-passport-deployment.md)


이 문서에 어떻게 tooresolve 잠재적 문제 해결 지침을 제공 합니다. 

hello 등록은 지원 hello windows에서 10 2015 년 11 월 업데이트 이상.  
위의 hello 시나리오를 사용 하기 위한 hello Anniversary 업데이트를 사용 하는 것이 좋습니다.

## <a name="step-1-retrieve-hello-registration-status"></a>1 단계: hello 등록 상태를 검색 합니다. 

**tooretrieve hello 등록 상태:**

1. 관리자 권한으로 hello 명령 프롬프트를 엽니다.

2. **dsregcmd /status**를 입력합니다.



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: DeviceId 없음: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 지문: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 플랫폼 암호화 공급자 TpmProtected: 예 KeySignTest:: tootest 상승 된 실행 해야 합니다.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>2 단계: hello 등록 상태를 평가 합니다. 

Hello 다음 필드를 검토 하 고 hello 예상 값을 갖는지 확인 하십시오.

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

이 필드는 hello 장치가 Azure AD에 등록 되었는지 여부를 표시 합니다. Hello 값 '아니요'로 표시 되 면 등록 완료 되지 않았습니다. 

**가능한 원인:**

- 등록에 대 한 hello 컴퓨터의 인증에 실패 했습니다.

- Hello 컴퓨터도 찾을 수 없습니다 hello 조직 중인 HTTP 프록시

- 인증을 위해 Azure AD 또는 등록에 대 한 Azure DRS hello 컴퓨터에 연결할 수 없습니다.

- hello 컴퓨터 아닐 hello 조직의 내부 네트워크 또는 VPN의 직선 tooan와 온-프레미스 AD 도메인 컨트롤러입니다.

- Hello 컴퓨터에 TPM이 있으면 잘못 된 상태에 수도 있습니다.

- 서비스에서 잘못 된 구성 앞에서 기록한 hello 문서에 다시 tooverify를 필요 함이 있을 수 있습니다. 일반적인 예제는 다음과 같습니다.

    - 페더레이션 서버에서 Ws-Trust 끝점이 사용되도록 설정되어 있지 않습니다.

    - 페더레이션 서버는 Windows 통합 인증을 사용한 네트워크 컴퓨터에서의 인바운드 인증을 허용하지 않을 수 있습니다.

    - Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없는

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

이 필드는 hello 장치 조인된 tooan 온-프레미스 Active Directory 인지 여부를 표시 합니다. Hello 값으로 표시 되 면 **아니요**, hello 장치 없습니다 자동 등록을 Azure AD와 합니다. 해당 hello 장치 조인 toohello 온-프레미스 Active Directory와 Azure AD에 등록할 수 전에 먼저 확인 합니다. Hello 컴퓨터 tooAzure AD 직접 추가 하기 위해 원하는 경우 Azure Active Directory Join의 기능에 대해 tooLearn 이동 하세요.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

이 필드는 hello 장치를 Azure AD와 있지만 개인 장치 (작업 공간 연결로 표시)로 등록 되었는지 여부를 표시 합니다. 그러나이 값은 Azure AD에 등록 된 도메인에 가입 된 컴퓨터에 대 한 '아니요'로 표시 해야 하면, 됨을 의미 하는 예로 표시 되는 경우 회사 또는 학교 계정을 추가 된 이전 toohello 컴퓨터 완료 등록 합니다. 이 경우 hello 계정은 Windows 10 (1607 때 '실행' 창 또는 명령 프롬프트 창의 hello hello WinVer 명령에서 실행)의 hello Anniversary 업데이트 버전을 사용 하는 경우 무시 됩니다.

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES 및 AzureADPrt : YES
  
이러한 필드에 해당 hello 사용자가 AD tooAzure toohello 장치 로그인 시 인증 성공적으로 나타납니다. 표시 하는 경우 '아니요' hello 다음 원인은 다음과 같습니다.

- 등록 (확인 hello KeySignTest 높은 실행 하는 동안) 시 hello 장치와 연결 된 TPM의 잘못 된 저장소 키 (STK)입니다.

- 대체 로그인 ID

- HTTP 프록시를 찾을 수 없음

## <a name="next-steps"></a>다음 단계

자세한 내용은 참조 hello [자동 장치 등록 FAQ](active-directory-device-registration-faq.md) 
