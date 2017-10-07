---
title: "데이터 보호 전략을 정의 하는 aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-| Microsoft Docs"
description: "하이브리드 identity 솔루션 toomeet hello 비즈니스 요구 사항에 정의 된 hello 데이터 보호 전략을 정의 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>하이브리드 ID 솔루션에 대한 데이터 보호 전략 정의
이 태스크에서는 프로그램 하이브리드 id 솔루션 toomeet hello 비즈니스 요구 사항에 정의 된에 대 한 hello 데이터 보호 전략을 정의 합니다.

* [데이터 보호 요구 사항 결정](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [콘텐츠 관리 요구 사항 결정](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [액세스 제어 요구 사항 확인](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>데이터 보호 옵션 정의
[디렉터리 동기화 요구 사항 확인](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)에서 설명한 것처럼 Microsoft Azure AD는 온-프레미스에 있는 Active Directory 도메인 서비스(AD DS)와 동기화할 수 있습니다. 이 통합 tooaccess 기업 리소스 하려고 할 때 조직 tooleverage Azure AD tooverify 사용자 자격 증명을 수 있습니다. 두 시나리오 모두에 대 한이 작업을 수행할 수 있습니다: hello 클라우드와 rest 온-프레미스에서 데이터입니다.  Azure AD에서 액세스 toodata 보안 토큰 서비스 (STS)를 통해 사용자 인증이 필요합니다.

인증 되 면 hello 사용자 계정 이름 (UPN) hello 인증 토큰에서 읽기 및 hello 복제 파티션 및 컨테이너에 해당 되 면 toohello 사용자의 도메인 결정 됩니다. Hello 사용자의 존재 여부, 활성화 된 상태 및 역할에 대 한 정보는 hello 요청 된 액세스 toohello 대상 테 넌 트가이 세션에서이 사용자에 대 한 인증 여부 hello 권한 부여 시스템 toodetermine에서 사용 됩니다. 특정 권한 있는 작업 (특히, 사용자, 암호 재설정 만들기) 테 넌 트가 사용할 수 있는 감사 내역을 만들어 관리자 toomanage 준수 노력 또는 조사 합니다.

인터넷 연결을 통해 Azure 저장소로 온-프레미스 데이터 센터에서 데이터 이동을 항상 기한 toodata 볼륨, 대역폭 가용성 또는 기타 고려 사항 불가능 아닐 수 있습니다. hello [Azure 가져오기/내보내기 서비스](../storage/common/storage-import-export-service.md) 배치 하 고, 검색 데이터의 양이 많은 blob 저장소에 대 한 하드웨어 기반 옵션을 제공 합니다. Toosend 허용 [BitLocker로 암호화 된](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) tooan Azure 데이터 센터 클라우드 운영자가 hello 내용을 tooyour 저장소 계정에 업로드 하거나 Azure 데이터 tooyour 다운로드할 수 있는 드라이브 tooreturn 직접 하드 디스크 드라이브 tooyou 합니다. (Hello 서비스 자체 hello 작업 설치 중에 의해 생성 된 BitLocker 키 사용)이이 프로세스에 대 한 암호화 된 디스크에만 허용 됩니다. hello BitLocker 키를 제공 tooAzure 별도로 키 공유 대역 외에서 제공 합니다.

전송 중인 데이터를에서 다양 한 시나리오에서 수행할 수 있으므로 Microsoft Azure를 사용 하는 관련 tooknow 이기도 [가상 네트워킹](https://azure.microsoft.com/documentation/services/virtual-network/) 호스트 및 게스트 수준 같은 조치를 적용 하는 방법, 서로 tooisolate 테 넌 트의 트래픽 방화벽, IP 패킷 필터링, 포트를 차단 및 HTTPS 끝점입니다. 그러나 인프라간 및 인프라 및 고객(온-프레미스)을 포함하여 Azure의 내부 통신 대부분은 암호화됩니다. 또 다른 중요 한 시나리오는 Azure 데이터 센터; 내의 hello 통신 Microsoft은 네트워크 tooassure 없는 VM를 가장 하거나 다른 hello IP 주소를 가로챌 수 있는 관리 합니다. TLS/SSL은 Azure 저장소 서비스 또는 SQL 데이터베이스에 액세스할 때 또는 tooCloud 서비스에 연결할 때 사용 됩니다. 이 경우 고객이 관리자에 게는 TLS/SSL 인증서 얻기 및 tootheir 테 넌 트 인프라를 배포 하는 일을 담당 합니다. 가상 컴퓨터 간에 이동 하는 데이터 트래픽을 동일한 배포 hello 또는 Microsoft Azure 가상 네트워크를 통해 단일 배포에 테 넌 트 간에 HTTPS, SSL/TLS 같은 암호화 된 통신 프로토콜을 통해 보호할 수 있습니다.

Hello 질문에 답변 하는 방법에 따라 [데이터 보호 요구 사항을 확인](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), tooprotect 데이터를 원하는 방식과 hello 하이브리드 id 솔루션 도움이 그에 toodetermine 수 있어야 합니다. hello 테이블에는 각 데이터 보호 시나리오에 사용할 수 있는 Azure에서 지원 되는 hello 옵션이 나와 있습니다.

| 데이터 보호 옵션 | hello 클라우드 | 온-프레미스에서 휴지 상태 | 전송 중 |
| --- | --- | --- | --- |
| BitLocker 드라이브 암호화 |X |X | |
| SQL Server tooencrypt 데이터베이스 |X |X | |
| VM간 암호화 | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> 읽기 [기능별 준수](https://azure.microsoft.com/support/trust-center/services/) 에서 [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/) tooknow 각 Azure 서비스와 호환 되는 hello 인증에 대 한 자세한 합니다.
> 다중 계층 방식의 사용 하는 데이터 보호에 대 한 hello 옵션에는 이러한 옵션 간의 비교가이 작업에 대 한 적용 되지 않습니다. Hello 데이터 될 각 상태에 대해 사용할 수 있는 모든 옵션을 활용 하 고 있는지 확인 하십시오.
>
>

## <a name="define-content-management-options"></a>콘텐츠 관리 옵션 정의
Azure AD toomanage 하이브리드 id 인프라를 사용 하 여 한 가지 이점은 hello 프로세스 hello 최종 사용자의 관점에서 완전히 투명 하 게 된다는 점입니다. hello 사용자는 tooaccess 공유 리소스를 시도 하 고, hello 리소스는 인증이 필요 하 고, hello 사용자는 toosend 순서 tooobtain에서 인증 요청 tooAzure AD 토큰 hello 및 hello 리소스에 액세스 해야 합니다. 이 전체 프로세스는 사용자 개입 없이 백그라운드에서 발생합니다. 가능한 toogrant 권한 tooa 이기도 [그룹](active-directory-manage-groups.md#getting-started-with-access-management) tooallow 순서에서에서 사용자의 해당 tooperform 일반 특정 동작입니다.

데이터 정보 보호를 우려하는 조직은 일반적으로 해당 솔루션에 대한 데이터 분류가 필요합니다. 현재 온-프레미스 인프라 이미 데이터 분류를 사용 하 고, 가능한 tooleverage Azure AD 사용자의 id에 대 한 hello 기본 리포지토리로 됩니다. 데이터 분류 호출에 사용되는 온-프레미스인 일반적인 도구는 Windows Server 2012 R2에 대한 [데이터 분류 도구 키트](https://msdn.microsoft.com/library/Hh204743.aspx) 라고 합니다. 이 도구 tooidentify 도움이 수, 분류 및 사설 클라우드에 파일 서버에서 데이터를 보호 합니다. 가능한 tooleverage hello 이기도 [자동 파일 분류](https://technet.microsoft.com/library/hh831672.aspx) tooaccomplish Windows Server 2012에서에서이 있습니다.

Microsoft 데이터 분류 위치에 없는 조직 tooprotect 중요 한 파일을 새 서버 온-프레미스를 추가 하지 않고 필요한 경우 사용할 수 있습니다 [Azure 권한 관리 서비스](https://technet.microsoft.com/library/JJ585026.aspx)합니다.  Azure RMS는 파일 및 전자 메일에 보안 암호화, id 및 권한 부여 정책 toohelp를 사용 하 고 여러 장치에서 작동-휴대폰, 태블릿 및 Pc입니다. Azure RMS는 클라우드 서비스 이기 때문에 필요 하지 않습니다 tooexplicitly를 보호 된 콘텐츠를 공유 하기 전에 다른 조직과 트러스트를 구성 합니다. Office 365 또는 Azure AD 디렉터리가 이미 있는 경우 조직 간에 공동 작업은 자동으로 지원됩니다. 또한 hello 디렉터리 특성만 Azure RMS 요구에 toosupport 일반 id, 온-프레미스 Active Directory 계정을 Azure Active Directory 동기화 서비스 (AAD 동기화) 또는 Azure AD Connect를 사용 하 여 동기화 할 수 있습니다.

콘텐츠 관리의 필수 요소는 리소스에 액세스 하는 toounderstand, 따라서 풍부한 로깅 기능이 hello id 관리 솔루션에 대 한 중요 합니다. Azure AD에서는 다음을 포함하여 30일 이상 로그를 제공합니다.

* 역할 멤버 자격에서 변경 내용 (예: 사용자 추가 tooGlobal 관리자 역할)
* 자격 증명 업데이트(예: 암호 변경)
* 도메인 관리(예: 사용자 지정 도메인 확인, 도메인 제거)
* 응용 프로그램 추가 또는 제거
* 사용자 관리(예: 사용자 추가, 제거 또는 업데이트)
* 라이선스 추가 또는 제거

> [!NOTE]
> 읽기 [Microsoft Azure 보안 및 감사 로그 관리](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow Azure에서 로깅 기능에 대 한 자세한 합니다.
> Hello 질문에 답변 하는 방법에 따라 [콘텐츠 관리 요구 사항을 결정](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), 원하는 하이브리드 id 솔루션에서 관리 되는 콘텐츠 toobe hello 수 toodetermine 있어야 합니다. 표 6에 표시 된 모든 옵션은 Azure AD와 통합 될 수, 중요 한 toodefine 비즈니스 요구에 더 적합 하는 합니다.
>
>

| 콘텐츠 관리 옵션 | 장점 | 단점 |
| --- | --- | --- |
| 중앙 집중화된 온-프레미스(Active Directory Rights Management Server) |Hello 데이터를 분류 하는 일을 담당 hello 서버 인프라에 대 한 모든 권한 <br> Windows Server의 기본 제공 기능은 추가 라이선스 또는 구독에 필요하지 않습니다. <br> 하이브리드 시나리오에서 Azure AD와 통합될 수 있습니다. <br> Exchange Online, SharePoint Online, Office 365와 같은 Microsoft 온라인 서비스에서 정보 권한 관리(IRM) 기능을 지원합니다. <br> Exchange Server, SharePoint Server 및 Windows Server 및 파일 분류 인프라 (FCI)를 실행하는 파일 서버와 같은 온-프레미스 Microsoft 서버 제품을 지원합니다. |이후 이상 버전에서 유지 관리 (따르도록 업데이트, 구성 및 잠재적인 업그레이드), IT hello 서버를 소유 하 고 <br> 서버 인프라 온-프레미스가 필요합니다.<br> Azure 기능을 고유하게 활용하지 않습니다 |
| Hello 클라우드 (Azure RMS)에서 중앙 집중화 |보다 쉽게 비교할 toomanage toohello 온-프레미스 솔루션 <br> 하이브리드 시나리오에서 AD DS와 통합될 수 있습니다. <br>  Azure AD와 완벽하게 통합 <br> 에 서버가 필요 하지 않습니다 주문 toodeploy hello 서비스에서 온-프레미스 <br> Exchange Server, SharePoint Server 및 Windows Server 및 파일 분류 인프라(FCI)를 실행하는 파일 서버와 같은 온-프레미스 Microsoft 서버 제품을 지원합니다. <br> IT는 BYOK 기능을 가진 테넌트의 키를 완전히 제어할 수 있습니다. |조직에는 RMS를 지원하는 클라우드 구독이 있어야 합니다  <br> 조직은 RMS에 대 한 Azure AD 디렉터리 toosupport 사용자 인증을 있어야 합니다. |
| 하이브리드(온-프레미스 Active Directory Rights Management Server와 통합된 Azure RMS) |이 시나리오의 두 위치에서 모두 중앙 집중식된 온-프레미스 및 hello 클라우드에서 hello 장점을 누적합니다. |조직에는 RMS를 지원하는 클라우드 구독이 있어야 합니다  <br> 조직은 RMS에 대 한 Azure AD 디렉터리 toosupport 사용자 인증을 있어야 합니다. <br> Azure 클라우드 서비스와 온-프레미스 인프라 간의 연결이 필요합니다 |

## <a name="define-access-control-options"></a>액세스 제어 옵션 정의
Hello 인증을 활용 하 여 권한 부여 및 액세스 제어 수 tooenable 됩니다. Azure AD에서 사용할 수 있는 기능에 회사 toouse 중앙 id 리포지토리로 hello에 나와 있는 것 처럼 toouse single sign on (SSO) 사용자와 파트너를 허용 하면서 아래 그림:

![](./media/hybrid-id-design-considerations/centralized-management.png)

다른 디렉터리르 사용하는 중앙 집중화된 관리 및 완전한 통합

온-프레미스 웹 응용 프로그램 및 azure Active Directory SaaS 응용 프로그램의 single sign on toothousands를 제공 합니다. Hello를 읽어 보십시오 [Azure Active Directory 페더레이션 호환성 목록: tooimplement 사용된 될 수 있는 타사 id 공급자 single sign on](https://msdn.microsoft.com/library/azure/jj679342.aspx) SSO 다른 공급 업체에서 테스트 된 hello에 대 한 자세한 내용은 문서 Microsoft 합니다. 이 기능에서는 hello id 및 액세스 관리 제어를 유지 하면서 조직 tooimplement 다양 한 B2B 시나리오 있습니다. 그러나 hello B2B 프로세스를 디자인 하는 동안는 hello 파트너에 의해 사용 되 고이 메서드는 Azure에서 지원 되는지 유효성을 검사 하는 중요 한 toounderstand hello 인증 방법입니다. 현재 다음은 Azure AD에서 지원하는 방법입니다.

* SAML(Security Assertion Markup Language )
* OAuth
* Kerberos
* 토큰
* 인증서

> [!NOTE]
> 읽기 [Azure Active Directory 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow 각 프로토콜 및 Azure에서 해당 기능에 대해 더 자세히 설명 합니다.
>
>

회사 Active Directory 자격 증명으로 모바일 응용 프로그램에 동일한 쉽게 모바일 서비스 인증 경험 tooallow 직원 toosign hello hello Azure AD 지원, 모바일 비즈니스 응용 프로그램이 사용할 수 있습니다. 이 기능을 Azure AD는 hello로 함께 모바일 서비스에서 id 공급자로 지원 (Microsoft 계정, Facebook ID, Google ID 및 Twitter ID 포함) 있음 기타 id 공급자 이미 지원 합니다. Hello 온-프레미스 응용 프로그램을 사용 하 여 hello hello 회사 AD DS에 있는 사용자의 자격 증명, 경우에 파트너 및 hello 클라우드에서 오는 사용자 hello 액세스 투명 해야 합니다. 사용자의 조건부 액세스 제어 too(cloud-based) 웹 응용 프로그램, 웹 API, Microsoft 클라우드 서비스, 타사 SaaS 응용 프로그램, 및 기본 (모바일) 클라이언트 응용 프로그램을 관리 하 고 감사, 하나로 보고 보안을 hello 이점을 가질 수 있습니다. 배치 합니다. 그러나 비-프로덕션 환경에서 또는 제한 된 양의 사용자 toovalidate이 권장 합니다.

> [!TIP]
> 것이 중요 한 toomention Azure AD에 AD DS 그룹 정책을 포함 하지 않습니다. 에 장치에 대 한 순서 tooenforce 정책 해야 하는 모바일 장치 관리 솔루션 등 [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx)합니다.
>
>

Hello 사용자가 Azure AD를 사용 하 여 인증 되 면 tooevaluate hello 수준의 사용자 hello 액세스가 있어야 합니다. hello hello 사용자 액세스 수준을 갖습니다 리소스에 대해 다를 수 있습니다, 자체 hello 리소스 액세스 제어 목록도 있을 수 있음을 염두에 유지 해야 Azure AD 액세스 toosome 리소스를 제어 하 여 추가 보안 계층을 추가할 수 있는 반면 파일 서버에 있는 파일에 대 한 hello 액세스 제어 등을 별도로 합니다. 아래 hello 그림 hello 수준의 하이브리드 시나리오에서 적절 한 액세스 제어 요약 되어 있습니다.

![](./media/hybrid-id-design-considerations/accesscontrol.png)

각 상호 작용 X 그림에에서 표시 하는 hello 다이어그램에서 Azure AD에 의해 적용 되어야 하는 한 액세스 제어 시나리오를 나타냅니다. 아래에서 각 시나리오에 대해 설명합니다.

1. 조건부 액세스 tooapplications 있는 온-프레미스 호스팅: 응용 프로그램을 Windows Server 2012 r 2를 사용 하 여 toouse AD FS 구성에 대 한 액세스 정책을 사용 하 여 등록 된 장치를 사용할 수 있습니다. 온-프레미스에 대해 조건부 액세스를 설정하는 방법에 대한 자세한 내용은 [Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정](active-directory-conditional-access.md)을 참조하세요.

2. Azure 포털 액세스 제어 toohello: Azure 수도 있습니다 역할 기반 액세스 제어 (RBAC)를 사용 하 여 제어 액세스 toohello 포털). 이 메서드를 사용 하면 개별 hello Azure 포털에서에서 수행할 수 있는 작업의 hello 회사 toorestrict hello 양입니다. RBAC toocontrol 액세스 toohello 포털을 사용 하 여 IT 관리자가 다음 액세스 관리 방법 hello를 사용 하 여 액세스를 위임할 수 있습니다.:

* 그룹 기반 역할 할당: 로컬 Active Directory에서 대 한 액세스 동기화 할 수 있는 tooAzure AD 그룹을 할당할 수 있습니다. 이렇게 하면 도구 및 그룹 관리 하기 위한 프로세스에서 조직 변경한 tooleverage hello 기존 투자 있습니다. 또한 Azure AD Premium의 hello 위임 된 그룹 관리 기능을 사용할 수 있습니다.
* Azure에서 역할에 기본 제공 활용 하는 방법: 세 가지 역할을 사용할 수 있습니다-사용자 및 그룹 권한 toodo hello 작업만 toodo 업무 필요한 한지 소유자, 참가자 및 독자 tooensure 합니다.
* 세부적인 액세스 tooresources: 역할 toousers 및 특정 구독, 리소스 그룹 또는 웹 사이트 또는 데이터베이스와 같은 개별 Azure 리소스 그룹을 할당할 수 있습니다. 이러한 방식으로 필요한 tooall hello 리소스에 액세스 하 고 toomanage 필요 하지 않은 액세스 tooresources 없는 사용자가을 확인할 수 있습니다.

> [!NOTE]
> 응용 프로그램을 작성 하는 toocustomize hello 액세스 제어를 원하는 경우 권한 부여를 위해 Azure AD 응용 프로그램 역할의 가능한 toouse 이기도 합니다. 이 검토 [WebApp-RoleClaims-DotNet 예제](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) 방법에 toobuild 앱 toouse이이 기능입니다.
>
>

3. Microsoft Intune을 사용한 Office 365 응용 프로그램에 대 한 조건부 액세스: hello에서 동일한 시간 tooaccess hello 규격 장치에서 정보 근로자를 허용 하는 동안 IT 관리자는 다음 조건부 액세스 장치 정책을 toosecure 회사 리소스를 프로 비전 할 수 서비스입니다. 자세한 내용은 [Office 365 서비스에 대한 조건부 액세스 장치 정책](active-directory-conditional-access-device-policies.md)을 참조하세요.

4. Saas 앱에 대 한 조건부 액세스: [이 기능은](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) 있습니다 tooconfigure 응용 프로그램별 다단계 인증 액세스 규칙 및 hello 기능 tooblock 액세스 사용자에 대 한 신뢰할 수 있는 네트워크에 없습니다. Hello 다단계 인증 규칙 tooall toohello 응용 프로그램에 할당 된 사용자 또는 사용자가 지정 된 보안 그룹 내에서 사용자에 대해서만 적용할 수 있습니다. 사용자가 해당에 내부 IP 주소에서 hello 응용 프로그램 액세스 하는 hello 다단계 인증 요구 사항에서 제외 될 수 있습니다 조직의 네트워크 hello 합니다.

다중 계층 방식의 사용 하는 액세스 제어에 대 한 hello 옵션에는 이러한 옵션 간의 비교가이 작업에 대 한 적용 되지 않습니다. Toocontrol tooyour 리소스에 액세스 해야 하는 각 시나리오에 사용할 수 있는 모든 옵션을 활용 하 고 있는지 확인 합니다.

## <a name="define-incident-response-options"></a>인시던트 대응 옵션 정의
Azure AD는 사용자의 작업을 모니터링 하 여 hello 환경에서 보안 위험 활용 하 여 Azure AD 액세스 및 사용 보고서는 조직의 디렉터리의 hello 무결성 및 보안에 대 한 기능 toogain 가시성 잠재적인 IT tooidentity 도움이 될 수 있습니다. 이 정보를 IT 관리자의 수 보다 잘 결정 있는 가능한 보안 위험이 발생할 수 있습니다 적절 하 게 될 수 toomitigate 이러한 위험.  [Azure AD Premium 구독](active-directory-get-started-premium.md) IT tooobtain이이 정보를 사용할 수 있는 보안 보고서 집합이 있습니다. [Azure AD 보고서](active-directory-view-access-usage-reports.md)는 아래와 같이 분류됩니다.

* **비정상 보고서**: 로그인이 있음을 toobe 비정상적인 이벤트가 포함 됩니다. 목표는 toomake 이러한 활동을 인식 하 고 toobe 수 toomake 의심 스러운 이벤트 인지에 대 한 결정을 사용 합니다.
* **통합 응용 프로그램 보고서**: 클라우드 응용 프로그램이 조직에서 사용되는 방식을 파악할 수 있게 해줍니다. Azure Active Directory는 수천 개의 클라우드 응용 프로그램과 통합을 제공합니다.
* **오류 보고서**: 계정 tooexternal 응용 프로그램을 프로 비전 할 때 발생할 수 있는 오류를 나타냅니다.
* **사용자별 보고서**: 특정 사용자에 대한 장치/로그인 활동 데이터를 표시합니다.
* **활동 로그**: 마지막 30 일 전 부터는 뿐만 아니라 그룹 활동 변경 사항 및 암호 재설정 및 등록 활동 또는 hello 지난 24 시간, 최근 7 일 내에 감사 된 모든 이벤트의 레코드를 포함 합니다.

> [!TIP]
> Hello 사고 대응 팀 작업 하는 경우에도 도움이 될 수 있는 다른 보고서는 hello [유출 된 자격 증명이 있는 사용자](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) 보고서입니다.  이 보고서는 이러한 누수된 자격 증명 목록과 테넌트 간의 일치 항목을 표시합니다.
>
>

인시던트 대응 조사 중에 사용될 수 있는 다른 중요한 Azure AD의 기본 제공 보고서는 다음과 같습니다.

* **암호 재설정 활동**: admin 님 안녕하세요 hello 조직에서 암호 재설정을 사용 하는 빈도에 대 한 정보를 제공 합니다.
* **암호 재설정 등록 작업**: 어떤 사용자가 암호 재설정을 위해 해당 메서드를 등록했는지와 어떤 방법을 선택했는지에 대한 통찰력을 제공합니다.
* **그룹 활동**: 변경 내용 toohello 그룹 시도한 기록을 제공 (예: 사용자가 추가 또는 제거) hello 액세스 패널에서에서 시작 하는 합니다.

또한 toohello 핵심 보고 기능 또한 it 부서 수 있습니다는 사고 대응 조사 프로세스 중 활용할 수 있는 Azure AD Premium에서 사용할 수 있는 감사 보고서 tooobtain 정보 같은 활용 합니다.

* 역할 멤버 자격에서 변경 내용 (예: 사용자 추가 tooGlobal 관리자 역할)
* 자격 증명 업데이트(예: 암호 변경)
* 도메인 관리(예: 사용자 지정 도메인 확인, 도메인 제거)
* 응용 프로그램 추가 또는 제거
* 사용자 관리(예: 사용자 추가, 제거 또는 업데이트)
* 라이선스 추가 또는 제거

다중 계층 방식의 사용 하는 hello 옵션 인시던트 응답에 대 한 이러한 옵션 간의 비교가이 작업에 대 한 적용 되지 않습니다. 귀사의 사고 대응 프로세스의 일부로 toouse Azure AD 보고 기능을 요구 하는 각 시나리오에 사용할 수 있는 모든 옵션을 활용 하 고 있는지 확인 합니다.

## <a name="next-steps"></a>다음 단계
[하이브리드 ID 관리 작업 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)
