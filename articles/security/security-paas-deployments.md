---
title: "aaaSecuring PaaS 배포 | Microsoft Docs"
description: " 다른 클라우드 서비스 모델와 PaaS의 보안 이점을 hello를 이해 하 고 Azure PaaS 배포 보안에 대 한 권장 되는 방법에 알아봅니다. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>PaaS 배포 보안

이 문서에서 제공하는 유용한 정보는 다음과 같습니다.

- Hello 클라우드에서 응용 프로그램 호스팅의 hello 보안 이점을 이해합니다
- 및 기타 클라우드 서비스 모델 서비스 (PaaS) 플랫폼의 보안 이점을 hello 평가
- 네트워크 중심 tooan identity 중심 경계 보안 방식에서 보안 포커스 변경
- 일반적인 PaaS 보안 모범 사례 권장 구현

## <a name="cloud-security-advantages"></a>클라우드 보안 이점
보안 이점 toobeing hello 클라우드에 있습니다. 조직 가능성이 있는 온-프레미스 환경에서 충족 되지 않은 책임과 제한 된 리소스를 사용할 수 있는 tooinvest 보안으로 공격자가 있는 모든 계층에서 수 tooexploit 취약성 환경을 만듭니다.

![클라우드 시대의 보안 이점][1]

조직에서는 공급자의 클라우드 기반 보안 기능 및 클라우드 intelligence를 사용 하 여 수 tooimprove은 자신의 위협 요소 탐지 및 응답 시간입니다.  책임 toohello 클라우드 공급자를 이동 하 여 조직 tooreallocate 보안 리소스 및 예산 tooother 비즈니스 우선 순위 수 있게 해 주는 자세한 보안 검사를 가져올 수 있습니다.

## <a name="division-of-responsibility"></a>책임 분담
사용자와 Microsoft 간의 책임의 중요 한 toounderstand hello 부서는 온-프레미스에 hello 전체 스택을가지고 있지만 몇 가지 책임 tooMicrosoft 전송 toohello 클라우드를 이동 합니다. hello 다음 책임 매트릭스 hello 영역의 표시 hello 스택을 담당 하는 SaaS, PaaS 및 IaaS 배포에서 하 고 Microsoft을 담당 합니다.

![책임 영역][2]

모든 클라우드 배포 유형에 대해 사용자는 고유의 데이터와 ID를 소유합니다. Hello 보안 데이터와 id를 온-프레미스 리소스 보호에 대 한 책임이 했으며 hello 제어 하는 클라우드 구성 요소 (서비스 유형별로 다르며)

배포의 hello 유형에 관계 없이 사용자가 항상 유지 되는 사항이 있습니다.

- Data
- Endpoints
- 계좌
- 액세스 관리

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>PaaS 클라우드 서비스 모델의 보안 이점
동일한 책임 매트릭스 보겠습니다 hello를 사용 하 여 온-프레미스와 Azure PaaS 배포의 보안 이점을 hello 살펴봅니다.

![PaaS의 보안 이점][3]

일반적인 위험 및 책임을 Microsoft 완화 hello hello 실제 인프라, hello 스택의 맨 아래에서 시작 합니다. Microsoft는 Microsoft 클라우드 hello는 지속적으로 모니터링 하 고, 이므로 하드 tooattack 합니다. 바람직하지 않습니다 공격자가 toopursue hello Microsoft cloud에 대 한 대상으로 합니다. Hello 공격자가 money 및 리소스, hello 공격자가 많은 되지 않는 가능성이 toomove tooanother 대상입니다.  

Hello 스택의 hello 중간에서 PaaS 배포와 온-프레미스 간의 차이가 있습니다. Hello 응용 프로그램 계층 및 hello 계정 및 액세스 관리 계층에서 비슷한 위험을 갖습니다. Hello 다음 단계 섹션이 문서에서 우리는 안내 toobest 사례를 제거 하거나 이러한 위험을 최소화 합니다.

Hello 스택, 데이터 거 버 넌 스 및 권한 관리의 hello 위쪽 키 관리를 통해 완화할 수 있는 위험을 하나에서 수행 합니다. (키 관리는 모범 사례에서 설명합니다.) 키 관리는 추가 처리를 더 이상 있다고 toomanage tookey 관리 리소스를 이동할 수 있도록 PaaS 배포에서 영역 있으면 없습니다.

hello Azure 플랫폼 또한 이렇게 하면 강력한 DDoS 보호 네트워크를 기반으로 다양 한 기술을 사용 하 여 합니다. 하지만 모든 유형의 네트워크 기반 DDoS 보호 방법에는 링크별 및 데이터 센터별로 제한이 있습니다. toohelp 큰 DDoS 공격의 hello 영향을 방지, tooquickly 및 toodefend DDoS 공격에 대 한 확장을 자동으로 활용할 수 있게 해 주는의 핵심 클라우드 기능을 Azure의 걸릴 수 있습니다. Hello 권장 하는 사례 문서에서에서이 수행할 수는 방법에 좀 더 자세히 검토 합니다.

## <a name="modernizing-hello-defenders-mindset"></a>현대화 hello defender의 태도 나타냅니다.
Paas 배포에 있는 프로그램 전반적인 접근 방식 toosecurity 근무조를 제공 됩니다. 모든 toocontrol 않아도 이동 toosharing 책임 Microsoft와 직접 합니다.

또 다른 중요 한 차이점 PaaS 및 기존 온-프레미스 배포의 hello 기본 보안 경계를 정의 하는 내용 새 뷰입니다. 지금까지 hello 기본 온-프레미스 보안 경계 네트워크에 인시던트 였으며 가장 온-프레미스 보안의 주요 보안 피벗으로 사용 하 여 hello 네트워크 디자인. PaaS 배포에 대 한 더 잘 identity toobe hello 기본 보안 경계를 고려 하 여 구현 됩니다.

## <a name="identity-as-hello-primary-security-perimeter"></a>Hello 기본 보안 경계와 id
클라우드 컴퓨팅 네트워크 중심 낮추는 광범위 한 네트워크 액세스의 hello 다섯 가지 필수적인 특성 중 하나를 혼동 관련성이 줄어들었습니다. 클라우드 컴퓨팅의 tooallow 사용자 tooaccess 리소스 위치에 관계 없이 대부분의 hello 목표입니다. 대부분 사용자에 게 해당 위치 진행 되는 toobe 어딘가에 hello 인터넷 합니다.

hello 다음 그림은 네트워크 경계 tooan identity 경계에서 hello 보안 경계가 발전 하는 방법. 보안은 네트워크 보호 하는 방법에 대 한 작은 및 더에 대 한 데이터를 방어 하 고으로 hello 보안 응용 프로그램 및 사용자 관리 됩니다. hello 주요 차이점은 toopush 보안 자세히 toowhat 중요 tooyour 회사 한다는 것입니다.

![새로운 보안 경계로서의 ID][4]

초기에는 Azure PaaS 서비스(예: 웹 역할 및 Azure SQL)에서 기존의 네트워크 경계 방어를 거의 또는 전혀 제공하지 않았습니다. Hello 요소의 용도 노출 toobe toohello 인터넷 (웹 역할) 및 해당 인증 (예를 들어 BLOB 또는 SQL Azure) hello 새 경계를 제공 합니다.이 확인 않았습니다.

최신의 보안 사례 해당 hello 악의적 사용자 hello 네트워크 경계 위반을 가정 합니다. 따라서 방어 최신 사례 tooidentity를 옮겼습니다. 조직은 강력한 인증 및 권한 부여(모범 사례)로 ID 기반 보안 경계를 설정해야 합니다.

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Hello identity 경계를 관리 하기 위한 권장 사항

원칙 및 hello 네트워크 경계에 대 한 패턴 년 제공 되었습니다. 반면, hello 업계 상대적으로 적은 경험이 hello 기본 보안 경계도 id를 사용 하는 합니다. 이와 더불어 충분 한 경험 tooprovide hello 필드에 입증 하는 몇 가지 일반적인 권장 누적 우리 고 tooalmost PaaS 서비스를 모두 적용 합니다.

hello 다음 일반적인 모범 사례 접근 방식 toomanaging identity 경계를 요약 되어 있습니다.

- **키 또는 자격 증명 잃지** 필수 toosecure PaaS 배포에는 키 및 자격 증명을 보호 합니다. 키와 자격 증명을 잃어 버리는 것은 일반적인 문제입니다. 한 가지 좋은 해결은 키와 암호를 하드웨어 보안 모듈 (HSM)에 저장 될 수 있는 toouse 중앙된 솔루션입니다. Azure에서 hello 클라우드의 HSM 제공 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md)합니다.
- **소스 코드 또는 GitHub 자격 증명 및 기타 암호 넣지 마세요** 만 일 나빠지는 키 및 자격 증명 손실 얻을 권한이 없는 사용자는 데 보다 액세스할 toothem hello 합니다. 공격자가 봇 기술 toofind 키 및 GitHub와 같은 코드 저장소에 저장 된 암호 수 tootake 활용 됩니다. 따라서 공개 원본 코드 리포지토리에 키와 비밀 정보를 넣지 두면 안됩니다.
- **하이브리드 PaaS 및 IaaS 서비스에서 VM 관리 인터페이스를 보호합니다.** IaaS 및 PaaS 서비스는 VM(가상 컴퓨터)에서 실행됩니다. 서비스의 hello 유형에 따라 여러 가지 관리 인터페이스를 사용할 수 있도록 tooremote 이러한 Vm을 직접 관리 합니다. [SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell), [RDP(원격 데스크톱 프로토콜)](https://support.microsoft.com/kb/186607) 및 [원격 PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting)과 같은 원격 관리 프로토콜을 사용할 수 있습니다. 일반적으로 hello 인터넷에서에서 직접 원격 액세스 tooVMs 사용 하지 않는 것이 좋습니다. 가능하다면 Azure 가상 네트워크에 가상 사설망을 사용하는 것과 같은 다른 방법을 사용해야 합니다. 다른 방법을 사용할 수 없는 경우 복잡한 암호 구문을 사용하고, 가능한 경우 2단계 인증(예: [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md))을 사용해야 합니다.
- **강력한 인증 및 권한 부여 플랫폼을 사용합니다.**

  - 사용자 지정 사용자 저장소 대신 Azure AD의 페더레이션 ID를 사용합니다. 페더레이션된 id를 사용 하면 플랫폼 기반 접근 방식의 활용할 수 있습니다 및 권한 있는 identities tooyour 파트너의 hello 관리를 위임 합니다. 페더레이션된 id 방법은 직원은 종료를 정보 toobe를 해야 하는 내용이 반영 경우 여러 id 및 권한 부여를 통해 시스템 시나리오에서 특히 중요 합니다.
  - 사용자 지정 코드 대신 플랫폼에서 제공하는 인증 및 권한 부여 메커니즘을 사용합니다. hello 이유는 사용자 지정 인증 코드를 개발 오류가 발생할 수 있습니다. 대부분의 개발자에 게 보안 전문가 않으며으 나 가능성이 toobe hello 미묘한 및 인증 및 권한 부여에 hello 최신 개발 됩니다. 상용 코드(예: Microsoft 개발 코드)는 종종 광범위하게 보안을 검토되고 있습니다.
  - 다단계 인증을 사용합니다. Multi-factor authentication은 hello 현재 사용자 이름 및 암호 인증 유형의에 내재 된 hello 보안 약점을 방지 하기 때문에 인증 및 권한 부여 표준입니다. 디자인 해야 toouse 구성 액세스 tooboth hello Azure 관리 (포털/원격 PowerShell) 인터페이스 및 서비스 toocustomer [Azure Multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md)합니다.
  - OAuth2 및 Kerberos와 같은 표준 인증 프로토콜을 사용합니다. 이러한 프로토콜은 광범위하게 검토되었으며 인증 및 권한 부여를 위한 플랫폼 라이브러리의 일부로 구현될 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 Azure PaaS 배포의 보안 이점을 집중적으로 설명했습니다. 그런 다음 PaaS 웹 및 모바일 솔루션 보안을 위한 권장 사례에 대해 알아보았습니다. 이제는 Azure App Service, Azure SQL Database, Azure SQL Data Warehouse로 시작하겠습니다. 사용할 수 있는 다른 Azure 서비스에 대 한 권장 되는 방법에 대 한 문서 해지면 hello 목록 다음에 링크를 제공 합니다.

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database 및 Azure SQL Data Warehouse](security-paas-applications-using-sql.md)
- Azure 저장소
- Azure REDIS Cache
- Azure 서비스 버스
- 웹 응용 프로그램 방화벽

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
