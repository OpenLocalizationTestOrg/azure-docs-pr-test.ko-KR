---
title: "Azure 공용 클라우드 hello에 aaaIsolation | Microsoft Docs"
description: "다양 한 종류의 계산 인스턴스를 포함 하는 클라우드 기반 컴퓨팅 서비스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스에 알아봅니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Hello Azure 공용 클라우드에서 격리
##  <a name="introduction"></a>소개
### <a name="overview"></a>개요
tooassist 현재 및 향후 Azure 고객 이해 하 고 hello 활용 다양 한 보안 관련 기능에 사용할 수 있으며 주변 hello Azure 플랫폼, Microsoft는 일련의 백서, 보안 개요, 모범 사례를 개발 하 고 검사 목록입니다.
hello 항목 폭과 깊이 기준으로 다양 하 고 정기적으로 업데이트 됩니다. 이 문서는 다음 hello 추상 섹션에 요약 된 것 처럼 해당 시리즈의 일부는입니다.

### <a name="azure-platform"></a>Azure 플랫폼
Azure는 유연한 개방형 클라우드 서비스 플랫폼으로 hello 광범위 한 프로그래밍 언어, 프레임 워크, 도구, 데이터베이스 및 장치 운영 체제를 선택할 수입니다. 예를 들어 다음을 수행할 수 있습니다.
- Docker 통합으로 Linux 컨테이너를 실행합니다.
- JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드합니다.
- iOS, Android 및 Windows 장치용 백 엔드를 빌드합니다.

Microsoft Azure hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

클라우드 기반의 toomanage hello 보안을 제공 하 고, 사용 하는 조직의 능력 tooprotect 응용 프로그램 및 사용 하 여 데이터 서비스 및 hello 컨트롤 hello, 빌드 또는 공용 클라우드 서비스 공급자에 게 IT 자산을 마이그레이션하는 경우 자산에 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고 비즈니스는 고유한 보안 요구를 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 보안 toomeet hello 하면 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다. 이 문서는 이러한 요구 사항을 충족하는 데 도움이 됩니다.

### <a name="abstract"></a>요약

Microsoft Azure 하면 toorun 응용 프로그램 및 가상 컴퓨터 (Vm)에 있습니다 물리적 인프라를 공유 합니다. 클라우드 환경에서 hello 프라임 경제 동기 toorunning 응용 프로그램 중 하나에 여러 고객에 게 공유 리소스의 hello 기능 toodistribute hello 비용입니다. 이러한 다중 테넌트 방식은 저렴한 비용으로 서로 다른 고객 간에 리소스를 다중화함으로써 효율성을 향상시킵니다. 안타깝게도, 또한 중요 한 응용 프로그램 및 임의의 tooan 및 잠재적으로 악의적인 사용자가 속할 수 있는 Vm의 물리적 서버 및 기타 인프라 리소스 toorun 공유 hello 위험 도입 합니다.

이 문서에는 Microsoft Azure 악성 및 비 악의적인 사용자에 대 한 격리를 제공 하 고 다양 한 격리 선택 tooarchitects 제공 하 여 클라우드 솔루션 설계에 대 한 가이드로 사용 방식을 간략하게 설명 합니다. 이 백서 hello 기술 Azure 플랫폼 및 고객 관련 보안 제어를 중점적으로 다루며 tooaddress Sla, 모델 및 DevOps 사례 고려 사항 가격을 시도 하지 않습니다.

## <a name="tenant-level-isolation"></a>테넌트 수준 격리
Hello 클라우드 컴퓨팅 동시에 여러 고객 간에 공유 하 고 공용 인프라의 개념은, 앞에 tooeconomies 눈금의 주요 이점 중 하나입니다. 이 개념을 다중 테넌트라고 합니다. Microsoft는 Microsoft 클라우드 Azure의 hello 다중 테 넌 트 아키텍처 표준 보안, 기밀성, 개인 정보, 무결성 및 가용성을 지원 하는지 tooensure 지속적으로 있습니다.

Hello 클라우드 기반 작업 공간에서 테 넌 트 클라이언트 또는 소유 하 고 해당 클라우드 서비스의 특정 인스턴스를 관리 하는 조직으로 정의할 수 있습니다. Microsoft Azure에서 제공 되는 hello id 플랫폼, 테 넌 트 조직 수신 하 고 Microsoft 클라우드 서비스에 등록 하는 경우를 소유 하는 Azure Active Directory (Azure AD)의 전용된 인스턴스일 뿐 되며

각 Azure AD 디렉터리는 고유하며 다른 Azure AD 디렉터리와 구분됩니다. 기업의 사무실 건물이 마찬가지로 보안 자산 특정 tooonly 조직, Azure AD 디렉터리 서버가 있는 보안 자산만 조직에서 사용 하기 위해 디자인 된 toobe 이기도 합니다. hello Azure AD 아키텍처에서는 고객 데이터와 id 정보가 섞이지 않도록 격리 됩니다. 즉, 한 Azure AD 디렉터리의 사용자 및 관리자가 실수로 또는 악의적으로 다른 디렉터리의 데이터에 액세스할 수 없습니다.

### <a name="azure-tenancy"></a>Azure 테넌트
Azure 테 넌 트 지원 (Azure 구독)을 참조 tooa "고객/청구" 관계는 고유한 [테 넌 트](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) 에 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)합니다. Microsoft Azure의 테넌트 수준 격리는 Azure Active Directory 및 이 서비스에서 제공하는 [역할 기반 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)를 사용하여 이루어집니다. 각각의 Azure 구독은 하나의 Azure AD(Active Directory) 디렉터리와 연결됩니다.

사용자, 그룹 및 해당 디렉터리에서 응용 프로그램 hello Azure 구독에서에서 리소스를 관리할 수 있습니다. Hello Azure 포털, Azure 명령줄 도구 및 Azure 관리 Api를 사용 하 여 이러한 액세스 권한을 할당할 수 있습니다. Azure AD 테넌트는 보안 경계를 사용하여 논리적으로 격리되므로 어떤 고객도 악의적으로 또는 실수로 공동 테넌트에 액세스하거나 손상시킬 수 없습니다. Azure AD는 분리된 네트워크 세그먼트에서 격리된 "운영 체제 미설치(bare metal)" 서버에서 실행되며, 여기서 호스트 수준 패킷 필터링과 Windows 방화벽은 원하지 않는 연결과 트래픽을 차단합니다.

- 통해 사용자 인증을 요구 하는 Azure AD에서 액세스 toodata는 [보안 토큰 서비스 (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)합니다. Hello 사용자의 존재 여부, 활성화 된 상태 및 역할에 대 한 정보는 hello 요청 된 액세스 toohello 대상 테 넌 트가이 세션에서이 사용자에 대 한 인증 여부 hello 권한 부여 시스템 toodetermine에서 사용 됩니다.

![Azure 테넌트](./media/azure-isolation/azure-isolation-fig1.png)


- 테넌트는 각각 별개의 컨테이너이며, 이들 사이에 아무 관계가 없습니다.

- 테넌트 관리자가 페더레이션을 통해 권한을 부여하거나 다른 테넌트의 사용자 계정을 프로비전하지 않는 한 테넌트 간에 액세스할 수 없습니다.

- Hello Azure AD 서비스와 직접 액세스 tooAzure AD의 백 엔드 시스템을 구성 하는 물리적으로 액세스 tooservers 제한 되어 있습니다.

- Azure AD 사용자가 없는 toophysical 자산에 액세스 또는 위치를와 이러한 toobypass hello 논리 RBAC 정책 검사 명시 된 다음에 대 한 가능한 이므로 합니다.

진단 및 유지 관리 요구 사항에 따라 Just-In-Time 권한 상승 시스템을 사용하는 작업 모델이 필요하고 사용됩니다. 적격 admin hello 개념을 소개 하는 azure AD Privileged Identity Management (PIM) [적격 관리자](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)는 때때로 권한 있는 액세스 권한이 필요지만 매일 액세스할 필요가 없는 사용자여야 합니다. hello 사용자 액세스를 해야 하는 서로 정품 인증 프로세스를 완료 하 고 미리 결정 된 시간 동안 활성 관리 될 때까지 hello 역할이 활성화 되었습니다.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory와 정책 및 사용 권한의 tooand 전적으로 소유 하 고 hello 테 넌 트 별로 관리 hello 컨테이너 내에서 자체 보호 컨테이너에서 각 테 넌 트를 호스팅합니다.

테 넌 트 컨테이너 hello 개념이 아닙니다. 모든 계층에서 hello 디렉터리 서비스에 밀접 하 게 세분화 된 방식으로 toopersistent 저장소 hello 모든 포털에서 합니다.

여러 Azure Active Directory 테 넌 트의 메타 데이터에 저장 된 경우에 hello 같은 실제 디스크, hello 테 넌 트 관리자에 의해 결정 됩니다 hello 디렉터리 서비스에 의해 정의 된 것 이외의 hello 컨테이너 간에 관계가 있습니다.

### <a name="azure-role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어)
[Azure 역할 기반 액세스 제어 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) Azure에 대 한 세분화 된 액세스 관리를 제공 하 여 tooshare 하면 Azure 구독 내에서 사용할 수 있는 다양 한 구성 요소를 사용 합니다. Azure RBAC를 사용 하면 조직 내에서 toosegregate 의무 액세스 권한 부여 기준 및 사용자가 필요한 tooperform 작업 합니다. Azure 구독 또는 리소스에서 모든 사람에게 무제한 권한을 제공하는 대신 특정 작업만 허용할 수 있습니다.

Azure RBAC tooall 리소스 유형에 적용 되는 세 가지 기본 역할에 있습니다.

- **소유자** 에 대 한 모든 권한을 tooall 리소스가 hello 오른쪽 toodelegate 액세스 tooothers를 포함 합니다.

- **참가자** 수 만들고 모든 유형의 Azure 리소스를 관리할 수 있지만 tooothers 액세스 권한을 부여할 수 없습니다.

- **읽기 권한자** 는 기존 Azure 리소스를 볼 수 있습니다.

![Azure 역할 기반 액세스 제어](./media/azure-isolation/azure-isolation-fig3.png)

Azure의 hello RBAC 역할 hello 나머지 특정 Azure 리소스 관리를 허용 합니다. 예를 들어 hello 가상 컴퓨터 참가자 역할 hello 사용자 toocreate 허용 하 고 가상 컴퓨터를 관리 합니다. 제공 되지 않습니다 해당 액세스 toohello Azure 가상 네트워크 또는 가상 컴퓨터를 hello hello 서브넷에 연결 합니다.

[기본 제공 역할 RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) Azure에서 사용할 수 있는 hello 역할을 나열 합니다. Hello 작업과 toousers 각 기본 제공 역할에 부여 하는 범위를 지정 합니다. 찾고 있는 경우 toodefine 더 많은 컨트롤에 대 한 사용자 역할, 참조 방법을 toobuild [사용자 지정 역할에서 Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles)합니다.

Azure Active Directory의 몇 가지 다른 기능은 다음과 같습니다.
- Azure AD를 사용 하면 호스팅되는 위치에 관계 없이 SSO tooSaaS 응용 프로그램입니다. 응용 프로그램 일부는 Azure AD를 사용하여 페더레이션되고 나머지는 암호 SSO를 사용합니다. 또한 페더레이션된 응용 프로그램은 사용자 프로비전 및 [암호 보관](https://www.techopedia.com/definition/31415/password-vault)을 지원할 수도 있습니다.

- 에 대 한 액세스 toodata [Azure 저장소](https://azure.microsoft.com/services/storage/) 인증을 통해 제어 됩니다. 각 저장소 계정에 기본 키 ([저장소 계정 키](https://docs.microsoft.com/azure/storage/storage-create-storage-account), 또는 SAK)와 보조 비밀 키 (hello 공유 액세스 서명, 또는 SAS).

- Azure AD는 온-프레미스 디렉터리와 함께 [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), 동기화 및 복제를 사용하여 페더레이션을 통해 IaaS(Identity as a Service)를 제공합니다.

- [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) hello 다단계 인증 서비스 모바일 앱, 전화 통화 또는 문자 메시지를 사용 하 여 사용자가 tooverify 로그인입니다. Hello Azure Multi-factor Authentication 서버 및 사용자 지정 응용 프로그램 및 디렉터리 hello SDK를 사용 하 여과 Azure AD toohelp 안전한 온-프레미스 리소스와 사용할 수 있습니다.

- [Azure AD 도메인 서비스](https://azure.microsoft.com/services/active-directory-ds/) 도메인 컨트롤러를 배포 하지 않고 Azure 가상 컴퓨터 tooan Active Directory 도메인에 가입할 수 있습니다. 회사 Active Directory 자격 증명으로 toothese 가상 컴퓨터에 로그인 하 고 모든 Azure 가상 컴퓨터에 그룹 정책 tooenforce 보안 기준을 사용 하 여 도메인에 가입 된 가상 컴퓨터를 관리할 수 있습니다.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) toohundreds 수백만 id의 크기를 조정 하는 소비자 용 응용 프로그램에 대해 항상 사용 가능한 글로벌 id 관리 서비스를 제공 합니다. 이 서비스는 모바일 및 웹 플랫폼에 통합될 수 있습니다. 소비자 로그인 할 수 tooall 사용자 지정할 수 있는 환경을 통해 응용 프로그램의 기존 소셜 계정을 사용 하 여 하거나 자격 증명을 만들어 합니다.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Microsoft 관리자로부터 격리 및 데이터 삭제
Microsoft는 강력한 측정값 tooprotect 프로그램 또는 데이터를 부적절 한 액세스 권한이 없는 사용자가 사용 됩니다. 이러한 운영 프로세스 및 컨트롤 hello 뒷받침 [온라인 서비스 약관](http://aka.ms/Online-Services-Terms), tooyour 데이터 액세스를 제어 하는 계약의 노력과 헌신 제공 됩니다.

-   Microsoft 엔지니어가 hello 클라우드에서 tooyour 데이터를 액세스 하는 기본값을 갖지 않습니다. 대신 필요할 때만 관리 감독하에 액세스 권한이 부여됩니다. 이러한 액세스 권한은 신중하게 제어되고 로깅되며, 더 이상 필요하지 않게 되면 해지됩니다.

-   Microsoft 다른 회사 tooprovide 제한 된 서비스를 대신할 수 고용 하 고 있습니다. 하도급 고객 데이터만 toodeliver hello 서비스에는 액세스할 수 있습니다 이러한 tooprovide, 고용 있어야 하며 다른 용도로 사용 하 여 없습니다. 또한 고객의 정보를 계약 바인딩된 toomaintain hello 기밀로 됩니다.

감사 된 인증을 사용 하 여 비즈니스 서비스와 같은 ISO/IEC 27001 정기적으로 Microsoft에서 확인 되 고 accredited 감사 샘플 감사 tooattest을 수행 하는 기업, 적법 한 비즈니스 목적에 대해서만 액세스 하 합니다. 언제든지 어떤 이유로든 자신의 고객 데이터에 액세스할 수 있습니다.

모든 데이터를 삭제 하면 Microsoft Azure 캐시 되거나 백업 복사본을 모두 포함 하 여 hello 데이터를 삭제 합니다. 범위에서 서비스에 대 한 데이터를 hello 끝날 hello 보존 기간 후 90 일 이내에 발생 합니다. (범위에서 서비스의 hello 데이터 처리 조건 섹션에 정의 된 우리의 [온라인 서비스 약관](http://aka.ms/Online-Services-Terms).)

안전 하 게 되는 디스크 드라이브를 저장소에 사용 되는 하드웨어 오류가, 경우 [지워지거나 소멸](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) Microsoft 반환 toohello 제조업체에 대체 또는 복구 하기 전에. hello hello 드라이브에 데이터를 덮어씁니다 데이터 hello tooensure 어떤 방법으로 복구할 수 없습니다.

## <a name="compute-isolation"></a>Compute 격리
Microsoft Azure는 다양 한 클라우드 기반 컴퓨팅 등 서비스의 다양 한 종류의 계산 인스턴스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스를 제공 합니다. 이러한 계산 인스턴스 및 서비스 제공 여러 수준 toosecure 데이터에서 격리 hello 유연성 구성에 영향을 주지 않고 고객 요구 하 합니다.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>루트 VM과 게스트 VM 간 Hyper-V 및 루트 OS 격리
Azure의 계산 플랫폼은 Hyper-V 가상 컴퓨터에서 모든 고객 코드를 실행한다는 것을 의미하는 컴퓨터 가상화를 기반으로 합니다. 각 Azure 노드 (또는 네트워크 끝점)에 하이퍼바이저 hello 하드웨어에 대해 직접 실행 하 고 게스트 가상 컴퓨터 (Vm)의 여러 노드를 나눕니다.


![루트 VM과 게스트 VM 간 Hyper-V 및 루트 OS 격리](./media/azure-isolation/azure-isolation-fig4.jpg)


각 노드에 또한 특수 루트 VM 하나의 hello 호스트 운영 체제를 실행 하는 합니다. 중요 한 경계는 hello 게스트 Vm에서에서 VM hello 루트 및 상호 hello 하이퍼바이저와 hello 루트 OS에서 관리 하는 hello 게스트 Vm의 hello 격리입니다. Microsoft의 수십 운영 체제 보안 환경과 Microsoft의 Hyper-v에서는 게스트 Vm의 tooprovide 강력한 격리에서에서 최신 학습을 활용 hello 하이퍼바이저/루트 OS 쌍으로 연결 합니다.

hello Azure 플랫폼에는 가상화 된 환경을 사용합니다. 사용자 인스턴스 액세스 tooa 물리적 호스트 서버를 갖지 않는 독립 실행형 가상 컴퓨터와 작동 되지 않으며 실제 프로세서 (링-0/링-3) 권한 수준을 사용 하 여 이러한 격리 적용.

링 0은 가장 권한이 있는 고 3 hello hello 이상입니다. hello 게스트 OS는 낮은 권한의 링 1에서 실행 하 고 응용 프로그램에서 실행 hello 최소 권한이 지정 된 링 3 키를 누릅니다. 물리적 리소스의이 가상화 게스트 OS와 하이퍼바이저, 결과적으로 두 hello 간의 추가 보안 분리 간의 tooa 명확 하 게 분리를 안내 합니다.

hello Azure 하이퍼바이저 마이크로 커널 처럼 작동 및 VMBus를 호출 하는 공유 메모리 인터페이스를 사용 하 여 처리를 위해 게스트 가상 컴퓨터 toohello 호스트에서 모든 하드웨어 액세스 요청을 전달 합니다. 사용자가 원시 읽기/쓰기/실행 액세스 toohello 시스템 하지 못하도록 방지 하 고 hello의 시스템 리소스를 공유 하는 위험을 완화 합니다.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>고급 VM 배치 알고리즘 및 측면 채널 공격으로부터 보호
VM 간 공격에는 두 단계로 구성 되어 있습니다.: 동일한 호스트 hello 희생자 Vm 중 하나로 hello에 악의적 사용자 제어 하는 VM을 배치 하 고 다음 hello 격리 경계 tooeither 졌는 지 상태가 중요 한 정보를 도용 또는 greed 또는 파괴 하는 행위에 대 한 성능에 영향을 줄 합니다. Microsoft Azure는 고급 VM 배치 알고리즘을 사용하고 시끄러운 이웃 VM을 포함하여 알려진 모든 측면 채널 공격으로부터 보호함으로써 두 단계를 모두 보호합니다.

### <a name="hello-azure-fabric-controller"></a>hello Azure 패브릭 컨트롤러
hello Azure 패브릭 컨트롤러는 tootenant 작업 인프라 리소스를 할당 해야 하 고 toovirtual 컴퓨터를 호스트 하는 hello에서 단방향 통신을 관리 합니다. hello Azure 패브릭 컨트롤러의 hello VM 배치 알고리즘은 실제 호스트 수준으로 매우 정교 하 고 거의 없는 toopredict 있습니다.

![hello Azure 패브릭 컨트롤러](./media/azure-isolation/azure-isolation-fig5.png)

hello Azure 하이퍼바이저 메모리를 적용 하 고 프로세스 구분 하며 가상 컴퓨터 네트워크 트래픽 tooguest OS 테 넌 트를 안전 하 게 라우팅합니다. 이렇게 하면 VM 수준에서 측면 채널 공격의 가능성과 해당 공격을 제거합니다.

Azure의 hello 루트 VM은 특별: 강화 된 운영 체제를 hello 루트 OS 호출 (FA) 패브릭 에이전트를 호스팅하는 실행 합니다. FAs는 게스트 Os에 고객 Vm 내에서 설정 toomanage 게스트 에이전트 (GA)에 사용 됩니다. FA는 저장소 노드도 관리합니다.

hello Azure 하이퍼바이저의 컬렉션 루트 OS/FA 및 고객 Vm/가스 계산 노드를 구성 합니다. FA는 계산 및 저장소 노드 외부에 있는 FC(패브릭 컨트롤러)로 관리됩니다(계산 및 저장소 클러스터는 별도의 FC로 관리됨). 실행 되는 동안 응용 프로그램의 구성 파일을 업데이트 하는 고객, hello FC와 통신 가스, 그런 다음 관리자 hello FA, hello 구성 변경의 hello 응용 프로그램에 알리는입니다. 하드웨어 오류의 hello 이벤트에서 hello FC는 자동으로 사용 가능한 하드웨어 찾아 안녕 VM을 다시 시작 합니다.

![Azure 패브릭 컨트롤러](./media/azure-isolation/azure-isolation-fig6.jpg)

패브릭 컨트롤러 tooan 에이전트에서 통신이 단방향입니다. hello 에이전트만 toorequests hello 컨트롤러에서 응답 하는 SSL로 보호 서비스를 구현 합니다. 다른 권한 있는 내부 노드 또는 연결 toohello 컨트롤러 시작할 수 없습니다. hello FC 신뢰할 수 있는 것 처럼 모든 응답을 처리 합니다.


![패브릭 컨트롤러](./media/azure-isolation/azure-isolation-fig7.png)

격리는 hello 게스트 Vm에서 루트 VM 및 서로 hello 게스트 Vm에서 확장 됩니다. 또한 계산 노드는 보호를 강화하기 위해 저장소 노드로부터 격리됩니다.


hello 하이퍼바이저와 hello 호스트 운영 체제에 네트워크 패킷 제공-필터 toohelp 보장 신뢰할 수 없는 가상 컴퓨터 스푸핑된 트래픽이 생성 하거나 문제를 다루고 있지 트래픽 toothem, 트래픽 직접 tooprotected 인프라 끝점 또는 보내기/받기 수 없습니다. 부적절 한 브로드캐스트 트래픽을 합니다.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>패브릭 컨트롤러 에이전트 tooIsolate VM으로 추가 규칙 구성
기본적으로 hello 패브릭 컨트롤러 에이전트가 hello 패킷 tooadd 규칙 및 예외 권한이 tooallow 트래픽을 필터링을 구성 하는 다음 가상 컴퓨터를 만들 때 모든 트래픽을 차단 합니다.

프로그래밍되는 규칙에는 다음 두 가지 범주의 규칙이 있습니다.

-   **컴퓨터 구성 또는 인프라 규칙**: 기본적으로 모든 통신이 차단됩니다. 있습니다 예외 tooallow 가상 컴퓨터 toosend 되며 DHCP 및 DNS 트래픽을 수신 합니다. 가상 컴퓨터 트래픽 toohello "public" 인터넷 및 송신 트래픽 tooother 가상 컴퓨터 내에서 동일한 Azure 가상 네트워크를 hello 및 운영 체제 정품 인증 서버 hello 보낼 수도 있습니다. Azure 라우터 서브넷, Azure 관리 및 기타 Microsoft 속성에 허용 된 보내는 대상 hello 가상 컴퓨터의 목록이 포함 되지 않습니다.

-   **역할 구성 파일:** hello hello 테 넌 트의 서비스 모델에 따라 인바운드 액세스 제어 목록 (Acl)을 정의 합니다.

### <a name="vlan-isolation"></a>VLAN 격리
각 클러스터에는 다음과 같이 3개의 VLAN이 있습니다.

![VLAN 격리](./media/azure-isolation/azure-isolation-fig8.jpg)


-   hello 주 VLAN – 상호 연결이 신뢰할 수 없는 고객 노드

-   hello FC VLAN – 포함 신뢰할 수 있는 FCs 및 지원 시스템

-   장치 VLAN hello – 신뢰할 수 있는 네트워크 및 기타 인프라 장치를 포함 합니다.

Hello FC VLAN toohello에서 통신은 허용 주 VLAN 있지만 hello 주 VLAN toohello FC VLAN에서에서 시작할 수 없습니다. 통신도 hello 주 VLAN toohello 장치 VLAN에서에서 차단 되었습니다. 이렇게 하면 고객 코드를 실행 하는 노드로 손상 된 경우에 hello FC 또는 장치 Vlan 중 하나에 있는 노드를 공격할 수 없습니다 것입니다.

## <a name="storage-isolation"></a>저장소 격리
### <a name="logical-isolation-between-compute-and-storage"></a>Compute 및 저장소 간의 논리적 격리
기본 설계의 일부로 Microsoft Azure는 VM 기반 계산을 저장소로부터 분리합니다. 이렇게이 분리 하면 하지 계산 및 저장소 tooscale 독립적으로 격리 하 고 보다 쉽게 tooprovide 다중 테 넌 트 수 있도록 합니다.

따라서 네트워크 연결 tooAzure 없는와 별도 하드웨어에 대 한 Azure 저장소 실행 계산 제외 하 고 논리적으로 합니다. [이](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)는 가상 디스크를 만들 때 디스크 공간이 전체 용량으로 할당되지 않음을 의미합니다. 대신, 주소 hello 실제 디스크에서 가상 디스크 tooareas hello에 매핑하는 테이블을 만들 및 해당 테이블은 처음에 비어 있습니다. **hello 처음으로 고객 hello 실제 디스크 공간을 할당 하 고 포인터 tooit hello 테이블에 배치 됩니다 hello 가상 디스크에 데이터를 씁니다.**
### <a name="isolation-using-storage-access-control"></a>저장소 액세스 제어를 사용한 격리
**Azure Storage의 액세스 제어**에는 간단한 액세스 제어 모델이 있습니다. Azure 구독마다 하나 이상의 저장소 계정을 만들 수 있습니다. 각 저장소 계정에는 해당 저장소 계정에 사용 되는 toocontrol 액세스 tooall 데이터는 하나의 비밀 키입니다.

![저장소 액세스 제어를 사용한 격리](./media/azure-isolation/azure-isolation-fig9.png)

**(테이블 포함) tooAzure 저장소 데이터에 액세스** 통해 제어할 수 있습니다는 [SAS (공유 액세스 서명)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) 있는 권한을 부여 범위 액세스 토큰입니다. hello SAS를 통해 만들어지는 hello로 서명 하는 쿼리 템플릿 (URL) [SAK (저장소 계정 키)](https://msdn.microsoft.com/library/azure/ee460785.aspx)합니다. [URL 서명](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) tooanother 프로세스 (위임)이 표시 된 다음 hello 쿼리의 hello 세부 정보를 입력 하 고 변경할 수 hello hello 저장소 서비스 요청을 지정할 수 있습니다. SAS를 사용 하면 toogrant 시간 기반 액세스 tooclients hello 저장소 계정 비밀 키를 표시 하지 않고 있습니다.

hello SAS म 부여할 수 있는 클라이언트가 제한 된 사용 권한을, 시간 및 지정한 사용 권한 집합으로 지정 된 기간 동안이 저장소 계정에서 tooobjects 의미 합니다. Tooshare 계정 액세스 키 필요 없이 이러한 제한 된 권한을 부여할 수 있습니다.

### <a name="ip-level-storage-isolation"></a>IP 수준 저장소 격리
방화벽을 설정하고 신뢰할 수 있는 클라이언트에 대한 IP 주소 범위를 정의할 수 있습니다. IP 주소 범위를 정의 하는 hello 범위에 속하는 IP 주소를가지고 있는 유일한 클라이언트 너무 연결할 수 있습니다[Azure 저장소](https://docs.microsoft.com/azure/storage/storage-security-guide)합니다.

한 네트워킹 메커니즘을 사용 하는 tooallocate 트래픽 tooIP 저장소의 전용 또는 전용 터널을 통해 권한 없는 사용자 로부터 IP 저장소 데이터를 보호할 수 있습니다.

### <a name="encryption"></a>암호화
Azure에서는 다음 암호화 tooprotect 데이터의 유형을 제공합니다.
-   전송 중 암호화

-   휴지 상태의 암호화

#### <a name="encryption-in-transit"></a>전송 중 암호화
전송 중 암호화는 네트워크를 통해 전송되는 경우 데이터 보호의 메커니즘입니다. Azure Storage를 사용하면 다음을 사용하여 데이터를 보호할 수 있습니다.

-   [전송 수준 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit)(예: Azure 저장소 안팎으로 데이터를 전송하는 경우 HTTPS)

-   [실시간 암호화](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)(예: Azure 파일 공유에 대한 SMB 3.0 암호화)

-   [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello 데이터 저장소에서 전송 된 후 저장소 및 toodecrypt hello 데이터로 전송 될 때까지 합니다.

#### <a name="encryption-at-rest"></a>휴지 상태의 암호화
여러 조직에서 [미사용 데이터 암호화](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 는 데이터 프라이버시, 규정 준수 및 데이터 주권을 위한 필수 단계입니다. “휴지 상태”의 데이터 암호화를 제공하는 세 가지 Azure 기능이 있습니다.

-   [저장소 서비스 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) toorequest hello 저장소 서비스 tooAzure 저장소를 작성할 때 자동으로 데이터를 암호화를 사용 하면 됩니다.

-   [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) 미사용 데이터 암호화의 hello 기능을 사용 합니다.

-   [Azure 디스크 암호화](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) tooencrypt hello OS 디스크 및 데이터 디스크는 IaaS 가상 컴퓨터에서 사용 하는 사용자에 게 있습니다.

#### <a name="azure-disk-encryption"></a>Azure 디스크 암호화
VM(가상 컴퓨터)에 대해 [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)를 사용하면 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)에서 제어하는 키와 정책으로 VM 디스크(부팅 및 데이터 디스크 포함)를 암호화하여 조직의 보안 및 규정 준수 요구 사항을 처리할 수 있습니다.

Windows 용 디스크 암호화 솔루션 hello 기반 [Microsoft BitLocker 드라이브 암호화](https://technet.microsoft.com/library/cc732774.aspx), hello Linux 솔루션 기반을 [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt)합니다.

hello 솔루션 hello Microsoft Azure에서 설정 된 경우 IaaS Vm에 대 한 다음 시나리오를 지원 합니다.
-   Azure Key Vault와 통합

-   표준 계층 VM: A, D, DS, G, GS 등 계열의 IaaS VM

-   Windows 및 Linux IaaS VM에서 암호화 사용

-   Windows IaaS VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함

-   Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함

-   Windows 클라이언트 OS를 실행하는 IaaS VM에서 암호화 사용

-   탑재 경로가 있는 볼륨에서 암호화 사용

-   [mdadm](https://en.wikipedia.org/wiki/Mdadm)을 사용하여 디스크 스트라이프(RAID)로 구성된 Linux VM에서 암호화 사용

-   데이터 디스크에 대해 [LVM(논리 볼륨 관리자)](https://msdn.microsoft.com/library/windows/desktop/bb540532)을 사용하여 Linux VM에서 암호화 사용

-   저장소 공간을 사용하여 구성된 Windows VM에서 암호화 사용

-   모든 Azure 공용 지역 지원됨

hello 솔루션 시나리오, 기능 및 기술 hello 릴리스에서 다음 hello를 지원 하지 않습니다.

-   기본 계층 IaaS VM

-   Linux IaaS VM에 대한 OS 드라이브에서 암호화 사용 안 함

-   Hello 클래식 VM 만들기 방법을 사용 하 여 만들어진 IaaS Vm

-   온-프레미스 키 관리 서비스와의 통합

-   Azure 파일(공유 파일 시스템), NFS(네트워크 파일 시스템), 동적 볼륨, 소프트웨어 기반 RAID 시스템으로 구성된 Windows VM

## <a name="sql-azure-database-isolation"></a>SQL Azure Database 격리
SQL 데이터베이스는 hello Microsoft 클라우드의 hello 시장 선도적 Microsoft SQL Server 엔진을 토대로 및 중요 한 워크 로드를 처리할 수 있는 관계형 데이터베이스 서비스입니다. SQL Database는 계정 수준, 지리/지역 기반 및 네트워킹 기반의 예측 가능한 데이터 격리를 제공하며, 이러한 격리는 모두 거의 관리할 필요가 없습니다.

### <a name="sql-azure-application-model"></a>SQL Azure 응용 프로그램 모델

[Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) 데이터베이스는 SQL Server 기술로 구축된 클라우드 기반 관계형 데이터베이스 서비스입니다. Microsoft에서 호스팅하는 확장성 있는 고가용성 다중 테넌트 데이터베이스 서비스를 클라우드에 제공합니다.

SQL Azure 응용 프로그램 관점에서 hello 다음 계층을 제공: 각 수준에는 아래 수준의 다를 포함 합니다.

![SQL Azure 응용 프로그램 모델](./media/azure-isolation/azure-isolation-fig10.png)

hello 계정 및 구독에는 Microsoft Azure 플랫폼 개념 tooassociate 결제 및 관리 됩니다.

논리 서버와 데이터베이스는 SQL Azure 관련 개념이며, SQL Azure, 제공되는 OData 및 TSQL 인터페이스를 사용하거나 Azure Portal에 통합된 SQL Azure 포털을 통해 관리됩니다.

SQL Azure 서버는 물리적 또는 VM 인스턴스가 아니라 소위 "논리 마스터" 데이터베이스에 저장되는 관리 및 보안 정책을 공유하는 데이터베이스 모음입니다.

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

논리 마스터 데이터베이스에는 다음이 포함됩니다.

-   SQL 로그인 tooconnect toohello 서버 사용

-   방화벽 규칙

대금 청구 및 사용 관련 정보 hello에서 SQL Azure 데이터베이스에 대 한 동일한 논리 서버에는 없는 보장 toobe hello에 동일한 SQL Azure 클러스터의 실제 인스턴스 대신 응용 프로그램 이름을 제공 해야 hello 대상 데이터베이스 연결할 때.

고객 관점에서 논리 서버 hello 영역의 hello 클러스터 중 하나에서 발생 하는 hello 서버 hello 실제로 생성 하는 동안에 그래픽 지리적 지역에 생성 됩니다.

### <a name="isolation-through-network-topology"></a>네트워크 토폴로지를 통한 격리

논리 서버 만들어지고 해당 DNS 이름이 등록, hello DNS 이름 이므로 hello 서버 배치 된 hello 특정 데이터 센터에 있는 "게이트웨이 VIP" 주소를 호출할 toohello를 가리킵니다.

뒤에 hello VIP (가상 IP 주소), 게이트웨이 상태 비저장 서비스의 모음을 했습니다. 일반적으로 여러 데이터 원본(마스터 데이터베이스, 사용자 데이터베이스 등) 간에 조정이 필요한 경우 게이트웨이가 관련됩니다. 게이트웨이 서비스는 hello 다음을 구현 합니다.
-   **TDS 연결 프록시 사용** - Hello 백 엔드 클러스터의 사용자 데이터베이스를 찾고 hello 로그인 시퀀스를 구현 하 고 다음 전달 hello TDS 패킷 toohello 백 엔드 및 백이 포함 됩니다.

-   **데이터베이스 관리** - 여기에 워크플로 toodo CREATE/ALTER/DROP 데이터베이스 작업의 컬렉션 구현 합니다. hello 데이터베이스 작업 성이 TDS 패킷 또는 명시적 OData Api에서 호출할 수 있습니다.

-   CREATE/ALTER/DROP 로그인/사용자 작업

-   OData API를 통한 논리 서버 관리 작업

![네트워크 토폴로지를 통한 격리](./media/azure-isolation/azure-isolation-fig12.png)

hello 계층 hello 게이트웨이 뒤에 있는 "백 엔드" 라고 합니다. 이 항상 사용 가능한 방식으로 모든 hello 데이터가 저장 되는 합니다. 각 데이터 조각은 언급된 toobelong tooa "파티션을" 나 "장애 조치" 각 복제본 3 개 이상 필요 합니다. 복제본 저장 및 SQL Server 엔진에서 복제 되 고 장애 조치 불리 시스템 tooas "패브릭"에서 관리 됩니다.

일반적으로 hello 백 엔드 시스템 보안을 위해 아웃 바운드 tooother 시스템 통신 하지 않습니다. 이 hello 프런트 엔드 (게이트웨이) 계층에 있는 예약 된 toohello 시스템입니다. hello 게이트웨이 계층 컴퓨터 추가적인 보안 메커니즘으로 hello 백 엔드 컴퓨터 toominimize hello 공격 노출 영역에 대 한 권한이 제한 됩니다.

### <a name="isolation-by-machine-function-and-access"></a>시스템 함수 및 액세스 권한으로 격리
SQL Azure는 다른 시스템 함수에서 실행되는 서비스로 구성됩니다. SQL Azure "백 엔드" 클라우드 데이터베이스 및 하는 트래픽 전용 백 엔드 시작 및 종료 되지 일반적인 원칙 hello 사용 하 여 "프런트 엔드" (게이트웨이/관리) 환경으로 구분 됩니다. hello 프런트 엔드 환경 다른 서비스의 세계 외부 toohello 통신 하 고 일반적으로 제한 되는 유일한 (충분 한 toocall hello 진입점이 필요 tooinvoke) hello 백 엔드의 사용 권한.

## <a name="networking-isolation"></a>네트워킹 격리
Azure 배포에는 여러 계층의 네트워크 격리가 있습니다. hello 다음 다이어그램에서는 다양 한 Azure toocustomers에서 제공 하는 네트워크 격리 계층 이러한 계층은 hello 자체 Azure 플랫폼에서에서 네이티브 및 사용자 정의 기능 둘 다입니다. 인바운드 Azure DDoS hello 인터넷에서에서 Azure에 대 한 대규모 공격에 대 한 격리를 제공 합니다. hello 다음 격리 계층은 고객이 정의한 공용 IP 주소 (끝점) 사용 되는 toodetermine hello 클라우드 서비스 toohello 가상 네트워크를 통해 트래픽을 전달할 수 있는 합니다. 기본 Azure Virtual Network 격리를 통해 모든 타 네트워크를 격리하고 트래픽이 사용자가 구성한 경로 및 방법을 통해서만 전달되도록 할 수 있습니다. 이러한 경로 메서드는 Nsg, UDR, 및 네트워크 가상 어플라이언스 hello 보호 네트워크 사용된 toocreate 격리 경계 tooprotect hello 응용 프로그램 배포를 될 수 있는 hello 다음 계층.

![네트워킹 격리](./media/azure-isolation/azure-isolation-fig13.png)

**트래픽 격리:** A [가상 네트워크](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) hello Azure 플랫폼에 hello 트래픽 격리 경계입니다. 하나의 가상 네트워크의 가상 컴퓨터 (Vm)에 다른 가상 네트워크에서 두 가상 네트워크를 만든 경우에 tooVMs hello 동일한 고객 직접 통신할 수 없습니다. 격리는 고객 VM과 통신이 가상 네트워크 안에서 비공개 상태를 유지하는 데 있어 중요한 속성입니다.

[서브넷](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets)은 IP 범위를 기반으로 하는 가상 네트워크에서 추가 격리 계층을 제공합니다. Hello 가상 네트워크의 IP 주소를 가상 네트워크를 구성 및 보안에 대 한 여러 서브넷으로 나눌 수 있습니다. Vm 및 PaaS 역할 인스턴스를 배포 toosubnets (같거나 다른) VNet 내에서 추가 구성 없이 서로 통신할 수 있습니다. 구성할 수 있습니다 [네트워크 보안 그룹 (Nsg)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow 또는 NSG의 액세스 제어 목록 (ACL)에 구성 된 규칙에 따라 네트워크 트래픽 tooa VM 인스턴스를 거부 합니다. NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다. NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다.

## <a name="next-steps"></a>다음 단계

- [Microsoft Azure Virtual Network의 컴퓨터에 대한 네트워크 격리 옵션](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

특정 클라이언트 또는 다른 컴퓨터 tooconnect tooa 특정 끝점의 IP 주소 허용 목록에 따라 특정 백 엔드 네트워크 또는 하위 네트워크의 컴퓨터 허용만 수 클래식 프런트 엔드 및 백 엔드 시나리오 hello를 포함 합니다.

- [계산 격리](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure는 다양 한 클라우드 기반 컴퓨팅 등 서비스의 다양 한 종류의 계산 인스턴스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스를 제공 합니다.

- [저장소 격리](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure는 고객 VM 기반 계산을 저장소와 분리합니다. 이렇게이 분리 하면 하지 계산 및 저장소 tooscale 독립적으로 격리 하 고 보다 쉽게 tooprovide 다중 테 넌 트 수 있도록 합니다. 따라서 네트워크 연결 tooAzure 없는와 별도 하드웨어에 대 한 Azure 저장소 실행 계산 제외 하 고 논리적으로 합니다. 모든 요청은 고객의 선택에 따라 HTTP 또는 HTTPS를 통해 실행됩니다.

