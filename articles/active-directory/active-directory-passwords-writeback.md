---
title: "비밀번호 쓰기 저장을 사용하는 Azure AD SSPR | Microsoft Docs"
description: "Azure AD와 Azure AD Connect를 사용하여 온-프레미스 디렉터리에 대한 비밀번호 쓰기 저장"
services: active-directory
keywords: "Active Directory 암호 관리, 암호 관리, Azure AD 셀프 서비스 암호 재설정"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: e460e734973622fb0d5745adfc4c1aa0178dd22e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="password-writeback-overview"></a>암호 쓰기 저장 개요

비밀번호 쓰기 저장을 사용하면 암호를 온-프레미스 Active Directory에 쓸 수 있도록 Azure AD를 구성할 수 있습니다. 복잡한 온-프레미스 셀프 서비스 암호 재설정 솔루션을 설정 및 관리할 필요가 없게 되며 사용자가 어디에 있든 상관 없이 온-프레미스 암호를 재설정할 수 있는 편리한 클라우드 기반 방법을 제공합니다. 비밀번호 쓰기 저장은 [Azure Active Directory 버전](active-directory-editions.md)의 현재 구독자가 설정하여 사용할 수 있는 [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) 구성 요소입니다.

비밀번호 쓰기 저장에서 제공하는 기능은 다음과 같습니다.

* **지연 피드백 없음** - 비밀번호 쓰기 저장은 동기식 작업입니다. 사용자의 암호가 정책에 맞지 않거나 어떤 이유로든 재설정 또는 변경할 수 없는 경우 즉시 사용자에게 알려줍니다.
* **AD FS 또는 다른 페더레이션 기술을 사용하는 사용자에게 암호 재설정 지원** - 페더레이션된 사용자 계정이 Azure AD 테넌트로 동기화되는 동안 비밀번호 쓰기 저장을 사용하여 온-프레미스 AD 암호를 클라우드에서 관리할 수 있습니다.
* **[암호 해시 동기화](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)를 사용하는 사용자에게 암호 재설정 지원** - 암호 재설정 서비스에서 동기화된 사용자 계정을 암호 해시 동기화에 사용할 수 있음을 감지하면 이 계정의 온-프레미스 및 클라우드 암호를 동시에 재설정합니다.
* **액세스 패널 및 Office 365에서 암호 변경 지원** - 페더레이션 또는 암호가 동기화된 사용자가 만료되었거나 만료되지 않은 암호를 변경하면 해당 암호를 로컬 AD 환경에 다시 씁니다.
* **Azure Portal에서 관리자가 암호를 재설정할 때 비밀번호 쓰기 저장 지원** - 사용자가 페더레이션 또는 암호가 동기화된 경우 관리자가 [Azure Portal](https://portal.azure.com)에서 해당 사용자의 암호를 재설정할 때마다 로컬 AD에서 관리자가 선택하는 암호도 설정합니다. 이 기능은 현재 Office 관리자 포털에서 지원되지 않습니다.
* **온-프레미스 AD 암호 정책 적용** - 사용자가 자신의 암호를 재설정하는 경우 해당 디렉터리에 커밋하기 전에 온-프레미스 AD 정책에 맞는지 확인합니다. 여기에는 기록, 복잡성, 나이, 암호 필터 및 로컬 AD에서 사용자가 정의한 기타 암호 제한 사항이 포함됩니다.
* **인바운드 방화벽 규칙 필요 없음** - 비밀번호 쓰기 저장 기능은 기본 통신 채널로 Azure Service Bus Relay를 사용합니다. 따라서 이 기능이 작동하기 위해 방화벽에서 인바운드 포트를 열 필요가 없습니다.
* **온-프레미스 Active Directory에서 보호된 그룹이 내에 존재하지 않는 사용자 계정에 대해 지원되지 않습니다** - 보호된 그룹에 대한 자세한 내용은 [Active Directory의 보호된 계정 및 그룹](https://technet.microsoft.com/library/dn535499.aspx)을 참조하세요.

## <a name="how-password-writeback-works"></a>암호 쓰기 저장의 작동 원리

페더레이션 또는 암호 해시 동기화된 사용자가 클라우드에서 자신의 암호를 재설정하거나 변경하려고 하면 다음이 수행됩니다.

1. 사용자가 어떤 종류의 암호를 가지고 있는지 확인합니다.
    * 확인하면 암호는 온-프레미스에서 관리됩니다.
        * 쓰기 저장 서비스를 사용 중인지 확인하고 사용 중인 경우 계속 진행합니다.
        * 쓰기 저장 서비스를 사용하지 않으면 사용자가 자신의 암호를 지금 재설정할 수 없다고 알려줍니다.
2. 다음으로, 사용자는 적절한 인증 게이트를 통과하여 암호 재설정 화면에 도달합니다.
3. 사용자는 새 암호를 선택하고 다시 확인합니다.
4. 제출을 클릭하면 쓰기 저장 설정 과정에서 만든 대칭 키로 일반 텍스트 암호를 암호화합니다.
5. 암호를 암호화한 후 HTTPS 채널을 통해 테넌트별 Service Bus Relay(쓰기 저장 설정 과정 중에 설정될 수도 있음)로 전송되는 페이로드에 해당 암호를 포함시킵니다. 이 릴레이는 온-프레미스 설치만 알고 있는 임의로 생성된 암호에 의해 보호됩니다.
6. 메시지가 서비스 버스에 도달하면 암호 재설정 끝점이 자동으로 절전 모드에서 해제되어 보류 중인 재설정 요청이 있는지 확인합니다.
7. 그런 다음, 서비스에서 클라우드 앵커 특성을 사용하여 해당 사용자를 찾습니다. 이 조회가 성공하려면:

    * 사용자 개체가 AD 커넥터 공간에 있어야 합니다.
    * 사용자 개체개 해당 MV 개체에 연결되어야 합니다.
    * 사용자 개체개 해당 AAD 커넥터에 연결되어야 합니다.
    * AD 커넥터 개체에서 MV로의 링크에는 동기화 규칙 `Microsoft.InfromADUserAccountEnabled.xxx`이 있어야 합니다. <br> <br>
    클라우드에서 호출이 들어오면 동기화 엔진이 cloudAnchor 특성을 사용하여 AAD 커넥터 공간 개체를 조회한 후 MV 개체로 링크를 다시 따라가고 AD 개체로 다시 링크를 따라갑니다. 동일한 사용자에 대해 여러 AD 개체(다중 포리스트)가 있을 수 있기 때문에 동기화 엔진은 `Microsoft.InfromADUserAccountEnabled.xxx` 링크에 의존하여 정확한 개체를 선택합니다.

    > [!Note]
    > 이 논리의 결과로 Azure AD Connect는 비밀 번호 쓰기 저장이 작동하기 위해 PDC 에뮬레이터와 통신할 수 있어야 합니다. 이 기능을 수동으로 사용하도록 설정하는 경우 Active Directory 동기화 커넥터의 **속성**을 마우스 오른쪽 단추로 클릭하고 **디렉터리 파티션 구성**을 선택하여 Azure AD Connect를 PDC 에뮬레이터에 연결할 수 있습니다. 여기에서 **도메인 컨트롤러 연결 설정** 섹션을 찾고 **기본 설정 도메인 컨트롤러만 사용**이라는 상자를 선택합니다. 기본 설정된 DC가 PDC 에뮬레이터가 아닌 경우더라도 Azure AD Connect는 비밀번호 쓰기 저장의 PDC에 연결을 시도합니다.

8. 사용자 계정을 찾은 후에는 적절한 AD 포리스트에서 직접 암호를 재설정합니다.
9. 암호 설정 작업에 성공한 경우 사용자에게 암호가 변경되었음을 알려줍니다.
    > [!NOTE]
    > 사용자 암호가 암호 동기화를 통해 Azure AD에 동기화되는 경우 온-프레미스 암호 정책이 클라우드 암호 정책보다 약할 수 있습니다. 이 경우 온-프레미스 정책이 무엇이든 이를 적용하고 암호 해시 동기화가 해당 암호의 해시를 동기화하도록 허용합니다. 이렇게 하면 Single Sign-On을 제공하는 데 암호 동기화를 사용하든, 페더레이션을 사용하든 관계없이 온-프레미스 정책이 클라우드에서 적용됩니다.

10. 암호 설정 작업에 실패한 경우는 사용자에게 오류를 반환하고 다시 시도하라고 알려줍니다.
    * 작업은 다음과 같은 이유로 실패할 수 있습니다.
        * 서비스가 종료되었습니다.
        * 선택한 암호가 조직 정책을 충족하지 못했습니다.
        * 사용자를 로컬 AD에서 찾을 수 없습니다.

    이러한 경우를 위한 특정 메시지가 있어서 문제를 해결하기 위해 어떤 작업을 수행할 수 있는지 사용자에게 알려줍니다.

## <a name="configuring-password-writeback"></a>비밀번호 쓰기 저장 구성

비밀번호 쓰기 저장을 사용하려는 경우 [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)의 자동 업데이트 기능을 사용하는 것이 좋습니다.

DirSync와 Azure AD Sync는 비밀번호 쓰기 저장을 사용하는 방법으로 더 이상 지원되지 않습니다. [DirSync 및 Azure AD Sync에서 업그레이드](connect/active-directory-aadconnect-dirsync-deprecated.md) 문서에는 전환에 도움이 되는 정보가 있습니다.

아래 단계에서는 사용자 환경에서 [기본](./connect/active-directory-aadconnect-get-started-express.md) 또는 [사용자 지정](./connect/active-directory-aadconnect-get-started-custom.md) 설정을 사용하여 Azure AD Connect를 이미 구성했다고 가정합니다.

1. 비밀번호 쓰기 저장을 구성하고 사용하도록 설정하려면 Azure AD Connect 서버에 로그인하고 **Azure AD Connect** 구성 마법사를 시작합니다.
2. [시작] 화면에서 **구성**을 클릭합니다.
3. 추가 작업 화면에서 **동기화 옵션 사용자 지정**을 클릭한 후 **다음**을 선택합니다.
4. [Azure AD에 연결] 화면에서 전역 관리자 자격 증명을 입력하고 **다음**을 선택합니다.
5. [디렉터리 연결] 및 [도메인 및 OU 필터링] 화면에서 **다음**을 선택하면 됩니다.
6. 선택적 기능 화면에서 **비밀번호 쓰기 저장** 옆에 있는 상자를 선택하고 **다음**을 클릭합니다.
   ![Azure AD Connect에서 비밀번호 쓰기 저장 사용][Writeback]
7. [구성 준비 완료] 화면에서 **구성**을 클릭하고 프로세스가 완료될 때까지 기다립니다.
8. [구성 완료]가 표시되면 **종료**를 클릭하면 됩니다.

## <a name="licensing-requirements-for-password-writeback"></a>비밀번호 쓰기 저장에 대한 라이선스 요구 사항

라이선스에 대한 정보는 [비밀번호 쓰기 저장에 필요한 라이선스](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) 항목 또는 다음 사이트를 참조하세요.

* [Azure Active Directory 가격 책정 사이트](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되는 온-프레미스 인증 모드

비밀번호 쓰기 저장은 다음 사용자 암호 유형에 사용할 수 있습니다.

* **클라우드 전용 사용자**: 온-프레미스 암호가 없기 때문에 비밀번호 쓰기 저장은 이 상황에서 적용되지 않음
* **암호 동기화된 사용자**: 비밀번호 쓰기 저장이 지원됨
* **페더레이션된 사용자**: 비밀번호 쓰기 저장이 지원됨
* **통과 인증 사용자**: 비밀번호 쓰기 저장이 지원됨

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되는 사용자 및 관리자 작업

암호는 다음과 같은 경우에 모두 다시 기록됩니다.

* **지원되는 최종 사용자 작업**
  * 모든 최종 사용자 셀프 서비스 자발적 변경 암호 작업
  * 모든 최종 사용자 셀프 서비스 적용 변경 암호 작업(예: 암호 만료)
  * [암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 시작되는 모든 최종 사용자 셀프 서비스 암호 재설정
* **지원되는 관리자 작업**
  * 모든 관리자 셀프 서비스 자발적 변경 암호 작업
  * 모든 관리자 셀프 서비스 적용 변경 암호 작업(예: 암호 만료)
  * [암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 시작되는 모든 관리자 셀프 서비스 암호 재설정
  * [Azure 클래식 포털](https://manage.windowsazure.com)에서 관리자 시작 최종 사용자 암호 재설정
  * [Azure Portal](https://portal.azure.com)에서 관리자 시작 최종 사용자 암호 재설정

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되지 않는 사용자 및 관리자 작업

암호는 다음과 같은 경우에 다시 기록되지 **않습니다**.

* **지원되지 않는 최종 사용자 작업**
  * PowerShell v1, v2 또는 Azure AD Graph API를 사용하여 자신의 암호를 재설정하는 최종 사용자
* **지원되지 않는 관리자 작업**
  * [Office 관리 포털](https://portal.office.com)에서 관리자 시작 최종 사용자 암호 재설정
  * PowerShell v1, v2 또는 Azure AD Graph API에서 관리자 시작 최종 사용자 암호 재설정

이러한 제한을 제거하기 위해 노력하고 있지만 아직 공유할 수 있는 일정은 없습니다.

## <a name="password-writeback-security-model"></a>암호 쓰기 저장 보안 모델

비밀번호 쓰기 저장은 매우 안전한 서비스입니다.  사용자 정보를 확실하게 보호하려면 아래에서 설명하는 4계층 보안 모델을 사용합니다.

* **테넌트별 Service Bus Relay**
  * 사용자가 이 서비스를 설정하면 임의로 생성된 강력한 암호에 의해 보호되는 테넌트별 Service Bus Relay가 설정됩니다. 이때 해당 암호는 Microsoft에도 전혀 액세스 권한이 없습니다.
* **잠겨 있는 강력한 암호 암호화 키**
  * Service Bus Relay를 만든 후 회선을 통해 도착하는 암호를 암호화하는 데 사용할 강력한 대칭 키를 만듭니다. 이 키는 클라우드의 회사의 암호 저장소에만 존재하며 디렉터리의 암호와 마찬가지로 강력하게 잠겨 있고 감사됩니다.
* **업계 표준 TLS**
  1. 클라우드에서 암호 재설정 또는 변경 작업을 수행하면 일반 텍스트 암호를 가져와서 공용 키로 암호화합니다.
  2. 그런 다음, Microsoft의 SSL 인증서를 사용하여 암호화된 채널을 통해 Service Bus Relay로 전송되는 HTTPS 메시지에 해당 암호를 삽입합니다.
  3. Service Bus에 메시지가 도착한 후에 온-프레미스 에이전트가 시작하고 이전에 생성된 강력한 암호를 사용하여 Service Bus에 인증합니다.
  4. 온-프레미스 에이전트는 암호화된 메시지를 선택하고 생성된 개인 키를 사용하여 암호를 해독합니다.
  5. 온-프레미스 에이전트는 AD DS SetPassword API를 통해 암호를 설정하려고 합니다.
     * 이 단계에서는 클라우드에서 AD 온-프레미스 암호 정책(복잡성, 나이, 기록, 필터 등)을 적용할 수 있습니다.
* **메시지 만료 정책** 
  * 온-프레미스 서비스가 종료되었기 때문에 메시지가 Service Bus에 남아 있는 경우 시간이 초과되고 몇 분 후에 제거되어 보안을 더욱 강화합니다.

### <a name="password-writeback-encryption-details"></a>비밀번호 쓰기 저장 암호화 세부 정보

사용자가 암호 재설정 요청을 전송한 이후부터 온-프레미스 환경에 도달하기 전까지 최대 서비스 안정성 및 보안을 보장하기 위해 진행되는 암호화 단계를 아래에서 설명합니다.

* **1단계 - 2048비트 RSA 키를 사용한 암호 암호화** - 사용자가 온-프레미스에 다시 작성된 암호를 제출하면 먼저 제출된 암호 자체를 2048비트 RSA 키로 암호화합니다.
* **2단계 - AES-GCM을 사용한 패키지 수준 암호화** - AES-GCM을 사용하여 전체 패키지(암호 + 필수 메타데이터)를 암호화합니다. 그러면 기본 Service Bus 채널에 대한 직접 액세스 권한을 가진 사용자가 콘텐츠를 보기/변조하지 않도록 방지합니다.
* **3단계 - 모든 통신이 TLS/SSL에 발생** - Service Bus와 모든 통신은 SSL/TLS 채널에서 발생합니다. 권한이 없는 제3자에게서 콘텐츠를 보호합니다.
* **6개월마다 자동 키 롤오버** - 자동으로 6개월마다 또는 비밀번호 쓰기 저장을 Azure AD Connect에서 사용/다시 사용할 때마다 이러한 키를 모두 롤오버하여 최대 서비스의 보안 및 안전을 보장합니다.

### <a name="password-writeback-bandwidth-usage"></a>비밀번호 쓰기 저장 대역폭 사용

비밀번호 쓰기 저장은 다음과 같은 경우에만 온-프레미스 에이전트로 요청을 다시 보내는 낮은 대역폭 서비스입니다.

1. 기능을 활성화 또는 비활성화할 때 Azure AD Connect를 통해 두 개의 메시지를 전송했습니다.
2. 서비스가 실행되는 동안 한 메시지를 서비스 하트 비트로 5분마다 한 번씩 전송합니다.
3. 두 개의 메시지는 새 암호를 전송할 때 각각 전송됩니다.
    * 첫 번째 메시지는 작업을 수행하는 요청입니다.
    * 두 번째 메시지는 작업의 결과를 포함하고 다음과 같은 경우에 전송됩니다.
        * 사용자 셀프 서비스 비밀번호 다시 설정 중에 새 비밀번호가 제출될 때마다
        * 사용자 비밀번호 변경 작업 중에 새 비밀번호가 제출될 때마다
        * 관리자가 시작한 사용자 비밀번호 재설정 중에 새 비밀번호가 제출될 때마다(Azure 관리 포털에서만)

#### <a name="message-size-and-bandwidth-considerations"></a>메시지 크기 및 대역폭 고려 사항

위에서 설명한 각 메시지의 크기는 일반적으로 1Kb 미만입니다. 극단적인 부하에서도 비밀번호 쓰기 저장 서비스 자체에서 초당 몇 Kb의 대역폭을 소비합니다. 각 메시지가 비밀번호 업데이트 작업에서 요구할 때만 실시간으로 전송되고 메시지 크기가 너무 작기 때문에 쓰기 저장 기능의 대역폭 사용은 실제 측정 가능한 영향을 미치기에는 실질적으로 너무 작습니다.

## <a name="next-steps"></a>다음 단계

다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해
* [**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포
* [**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? - 많은 분들이 항상 묻는 질문에 대한 답변입니다.
* [**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Azure AD Connect에서 비밀번호 쓰기 저장 사용"
