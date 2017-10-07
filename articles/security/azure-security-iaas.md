---
title: "Azure에서 작업 IaaS를 위한 aaaSecurity 모범 사례 | Microsoft Docs"
description: " 작업 부하 tooAzure IaaS의 hello 마이그레이션을 제공 기회 tooreevaluate 설계 "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Azure의 IaaS 작업에 대한 보안 모범 사례

서비스 (IaaS)로 이동 작업 tooAzure 인프라에 대해 생각을 시작 하면 아마도 실현 몇 가지 고려 사항은 친숙 한. 이미 가상 환경 보안을 설정해본 적이 있을 수 있습니다. TooAzure IaaS를 이동 하면 가상 환경 보안 설정에 대 한 전문 지식이 적용 하 고 사용 하 여 새로운 집합이 옵션 toohelp 보안 자산 수 있습니다.

म 기대 하지 toobring 온-프레미스 리소스 일대일 tooAzure로 한다는 것으로 시작 하겠습니다. 새로운 과제가 hello 및 hello 새 옵션 bring 기회 tooreevaluate 기존의 deigns, 도구 및 처리 합니다.

보안에 대 한 사용자의 책임 hello 유형의 클라우드 서비스를 기반으로 합니다. hello 다음 차트에 요약 Microsoft와 사용자에 대 한 책임의 hello 균형 같습니다.


![책임 영역](./media/azure-security-iaas/sec-cloudstack-new.png)


조직의 보안 요구 사항을 충족 하는 데 도움이 되는 Azure에서 사용할 수 있는 hello 옵션 중 일부에 대해 설명 합니다. 다양한 유형의 작업에 대한 보안 요구 사항이 다를 수 있는 점을 염두에 두십시오. 이러한 모범 사례 중 어떤 것도 혼자서는 시스템 보안을 유지할 수는 없습니다. 보안의 다른 요소와 toochoose hello에 대 한 적절 한 옵션에 있고 어떻게 hello 솔루션 보충할 수 있습니다 서로 보완 하 여 참조 합니다.

## <a name="use-privileged-access-workstations"></a>권한 있는 액세스 워크스테이션 사용

조직에서는 자주 희생 toocyberattacks 관리자 관리자 권한을 가진 계정을 사용 하는 동안 작업을 수행 합니다. 일반적으로 이러한 공격은 악의적이기 보다는 기존 구성 및 프로세스에서 허용하기 때문에 초래됩니다. 대부분의 이러한 사용자가 개념적 관점에서 이러한 작업의 hello 위험성을 이해 되지만 toodo 선택할 해당 합니다.

전자 메일을 확인 하 고 hello 인터넷 검색 충분히 문제 없는 것 처럼 작업을 진행 합니다. 하지만 검색 활동, 특수 하 게 작성 된 전자 메일 또는 기타 기술 toogain 액세스 tooyour enterprise를 사용할 수 있는 악의적인 행위자가 상승 된 계정이 toocompromise를 노출할 수도 있습니다. Hello 사용 하 여를 보안 관리 워크스테이션의 tooaccidental 손상 가능성을 줄이는 방법으로 모든 Azure 관리 작업을 수행 하기 위한 매우 좋습니다.

PAW(권한 있는 액세스 워크스테이션)는 인터넷 공격 및 위협 벡터로부터 보호되는 전용 운영 체제를 중요한 작업을 위해 제공합니다. 이러한 중요 한 작업 및에서 계정을 구분 매일 사용 하 여 워크스테이션 hello 및 피싱 공격, 응용 프로그램 및 OS 취약점, 다양 한 가장 공격 및 같은 키 자격 증명 도난 공격에서 강력한 보호를 제공 하는 장치 로깅,-Pass-the-hash, 및 티켓을 전달 합니다.

hello PAW 접근 방식 잘 설정 된 hello의 확장 이며 연습 toouse 표준 사용자 계정을와 별개인 개별적으로 할당 된 관리자 계정 권장 합니다. PAW는 이러한 중요한 계정에 대해 신뢰할 수 있는 워크스테이션을 제공합니다.

자세한 내용 및 구현 지침에 대해서는 [권한 있는 액세스 워크스테이션](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations)을 참조하세요.

## <a name="use-multi-factor-authentication"></a>Multi-Factor Authentication 사용

지난 hello, 네트워크 경계에는 사용 되는 toocontrol toocorporate 데이터에 액세스 했습니다. 클라우드-먼저, 모바일 중심 세계에서 id가 hello 제어 평면: 모든 장치에서 toocontrol 액세스 tooIaaS 서비스를 사용 합니다. 또한 사용할 있습니다 tooget 표시 유형 및 사용자 데이터가 사용 되는 위치 및 방법에 대 한 정보. Hello Azure 사용자의 디지털 id 보호 하는 것은 id 도용에서 구독 및 기타 cybercrimes 보호의 hello 토대입니다.

수행할 수 있는 toosecure 계정을 hello 가장 효율적인 단계 중 하나 tooenable 2 단계 인증입니다. 2 단계 인증은 추가 tooa 암호에 수준의 암호화를 사용 하 여 인증 하는 방법입니다. Tooget를 관리 하는 사용자가 액세스의 hello 위험 완화를 쉽게 다른 사용자의 암호입니다.

[Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) 되지 보호 액세스 toodata 및 응용 프로그램 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 합니다. 전화 통화, 문자 메시지 또는 모바일 앱 확인과 같은 다양한 손쉬운 확인 옵션을 통해 강력한 인증을 전달합니다. 사용자가 선호 하는 hello 메서드를 선택 합니다.

hello 가장 쉬운 방법은 toouse Multi-factor Authentication은 Windows, iOS 및 Android를 실행 하는 모바일 장치에 사용할 수 있는 hello Microsoft Authenticator 모바일 앱입니다. Azure Active Directory (Azure AD)와 온-프레미스 Active Directory 통합 hello 및 Windows 10의 최신 릴리스를 hello [비즈니스용 Windows Hello](../active-directory/active-directory-azureadjoin-passport-deployment.md) 원활한 single sign on tooAzure 리소스에 사용할 수 있습니다. 이 경우 hello Windows 10 장치 인증에 대 한 hello 두 번째 요소로 사용 됩니다.

Azure 구독을 관리 하는 계정에 대 한 하 고 toovirtual 컴퓨터에 로그인 할 수 있는 계정에 대해, Multi-factor Authentication을 사용 하 여 제공 훨씬 더 높은 수준의 보안만 암호를 사용 하는 것입니다. 다른 형식의 2단계 인증을 사용하는 것도 가능하지만 아직 프로덕션 환경이 아니라면 배포하기가 복잡할 수 있습니다.

hello 다음 스크린샷은 hello Azure Multi-factor Authentication에 대해 사용할 수 있는 옵션 중 일부:

![Multi-Factor Authentication 옵션](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>관리 액세스 제한

Azure 구독을 관리할 수 있는 hello 계정 보호 하는 것이 매우 중요 합니다. 계정이 손상 hello hello 값의 모든 hello tooensure hello 기밀성 및 무결성이 보장 수행할 수 있는 다른 단계를 부정 합니다. Hello 예와 같이 최근에 [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) 누수 분류 된 정보 내부 공격 내포할 거 대 한 위협 toohello 모든 조직의 전반적인 보안 합니다.

다음 조건 비슷한 toothese 하 여 관리 권한을 개별 사용자를 평가:

- 관리자 권한이 필요한 작업을 수행하고 있나요?
- Hello 작업을 수행 하는 빈도
- 특별 한 이유가를 대신해 다른 관리자가 hello 작업을 수행할 수 없습니다 이유는 무엇입니까?

다른 모든 알려진된 방법이 toogranting hello 권한 및 각 사용할 수 없는 이유를 문서화 합니다.

just-in-time 관리의 hello 사용에는 해당 권한이 필요 하지 않은 기간 동안 상승 된 권한 가진 계정 hello 불필요 한 있는지를 수 없습니다. 관리자가 해당 작업을 수행할 수 있게 제한된 시간 동안 계정 권한이 상승됩니다. 그런 다음 이러한 권한이 시프트 또는 작업이 완료 되 면 hello 끝에서 제거 됩니다.

사용할 수 있습니다 [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, 모니터 및 컨트롤에는 조직에 액세스 합니다. 조직에서 개인용 수행할 hello 작업 깨달을 쉽습니다. 또한 적격 admins hello 개념을 도입 하 여 적시에 관리 tooAzure 광고를 제공 합니다. 이들은 있는 hello 잠재적인 toobe 있는 계정 관리 권한이 부여 된 개인용입니다. 이러한 유형의 사용자는 활성화 프로세스를 진행할 수 있으며 제한된 시간 동안 관리 권한이 부여됩니다.


## <a name="use-devtest-labs"></a>DevTest Lab 사용

랩 및 개발 환경에 대 한 Azure를 사용 하 여 하드웨어 조달 소개 하는 라인 트래버스하여 hello 지연 여 개발 및 테스트에 조직 toogain 민첩을 수 있습니다. Azure 또는 desire toohelp 익숙하다고 부족 도입을 촉진 하는 반면 hello 관리자 toobe 지나치게 허용 권한 할당이 발생할 수 있습니다. 이러한 위험 hello 조직 toointernal 공격 실수로 노출 될 수 있습니다. 일부 사용자는 필요한 것보다 더 많은 권한을 부여받을 수 있습니다.

hello [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) 서비스 사용 [신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-what-is.md) (RBAC). RBAC를 사용 하 여 업무만 hello 수준의 사용자 toodo에 필요한 액세스를 부여 하는 역할에 팀 내에서 의무를 분리 합니다. RBAC에는 미리 정의된 역할(소유자, 실습 사용자 및 참가자)이 제공됩니다. 이러한 역할 tooassign 권한 tooexternal 파트너를 사용 하 여 수 있으며, 공동 작업을 훨씬 간소화할 수 있습니다.

DevTest Labs RBAC를 사용 되므로 추가 가능한 toocreate [사용자 정의 역할](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md)합니다. DevTest Labs hello 사용 권한 관리를 간소화할 뿐 아니라, 사용자를 프로 비전 하는 환경 가져오는 hello 과정을 간소화 합니다. 또한 개발 및 테스트 환경에서 작업하는 팀의 전형적인 문제점들을 처리하는 데도 도움이 됩니다. 몇 가지 준비 하는데 hello 장기적으로 것은 쉽게 팀입니다.

Azure DevTest Lab의 기능은 다음과 같습니다.

- 옵션의 사용 가능한 toousers hello에 대 한 관리 제어 합니다. 관리자에 게 허용 되는 VM 크기, 최대 수의 Vm 및 Vm 시작 될 때, 종료 등의 작업을 중앙에서 관리할 수 있습니다.
- 실습 환경 생성 자동화
- 비용 추적
- 임시 공동 작업을 위한 간편한 VM 배포
- 템플릿을 사용 하 여 사용자가 tooprovision 여 랩에서 수 있는 셀프 서비스.
- 사용량 관리 및 제한

![DevTest Labs toocreate 랩을 사용 하 여](./media/azure-security-iaas/devtestlabs.png)

추가 비용 없이 DevTest Labs hello 사용 하 여 연결 됩니다. labs, 정책, 템플릿 및 아티팩트 hello 만들기는 무료입니다. 가상 컴퓨터, 저장소 계정 및 가상 네트워크와 같은 환경에서 사용 하는 Azure 리소스만 hello에 대 한 지불 합니다.



## <a name="control-and-limit-endpoint-access"></a>끝점 액세스 제어 및 제한

호스팅 랩 또는 Azure에서 프로덕션 시스템에 시스템이 필요 하며 toobe hello 인터넷에서에서 액세스할 수 있는 의미 합니다. 기본적으로 새 Windows 가상 컴퓨터를 hello RDP 포트 hello 인터넷에서에서 액세스할 수 있으며 Linux 가상 컴퓨터에 있는 hello SSH 포트를 엽니다. 무단된 액세스의 필요한 toominimize hello 위험은 toolimit 노출 된 끝점의 단계를 수행 합니다.

Azure의 기술 hello 액세스 toothose 관리 끝점을 제한할 수 있습니다. Azure에서는 [NSG](../virtual-network/virtual-networks-nsg.md)(네트워크 보안 그룹)을 사용할 수 있습니다. Azure 리소스 관리자를 사용 하 여 배포에 대 한 Nsg에서 모든 네트워크 toojust hello 관리 끝점 (RDP 또는 SSH) hello 접근을 제한 합니다. NSG와 관련해서는 라우터 ACL을 떠올려보세요. 사용할 수 있습니다 프로그램 Azure 네트워크의 다양 한 세그먼트 사이의 tootightly hello 네트워크 통신을 제어 합니다. 다른 격리 된 네트워크 또는 경계 네트워크에 비슷한 toocreating 네트워크입니다. Hello 트래픽 검사 하지 하지만 네트워크 구분 기능 도움말지 않습니다.


Azure에서는 온-프레미스 네트워크에서 [사이트 간 VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)을 구성할 수 있습니다. 사이트 간 VPN을 온-프레미스 네트워크 toohello 클라우드를 확장합니다. 이렇게 하면 다른 기회 toouse Nsg, 또한 hello Nsg toonot을 수정할 수 있으므로 hello 로컬 네트워크가 아닌 다른 곳에서 액세스를 허용 합니다. 다음에서 첫 번째 연결 toohello VPN 통해 Azure 네트워크 관리 수행 되도록 요구할 수 있습니다.

hello 사이트 간 VPN 옵션은 Azure에서 온-프레미스 리소스와 밀접 하 게 통합 하는 프로덕션 시스템을 호스팅하는 경우에 가장 유용한 수 있습니다.

Hello 또는 사용할 수 있습니다 [지점 및 사이트](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) tooon 온-프레미스 리소스에 액세스할 필요 하지 않는 toomanage 시스템 보여 주려는 경우에는 옵션입니다. 이러한 시스템은 자체 Azure Virtual Network에 격리될 수 있습니다. Hello Azure에 대 한 VPN 관리자 수 환경 관리 자신의 워크스테이션에서 호스팅됩니다.

>[!NOTE]
>Hello Nsg toonot에 Acl hello 인터넷에서에서 액세스 toomanagement 끝점을 사용 하거나 VPN 옵션 tooreconfigure hello를 사용할 수 있습니다.

고려해야 할 또 다른 옵션은 [원격 데스크톱 게이트웨이](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md) 배포입니다. 이 배포를 사용할 수 있습니다 toosecurely toothose 연결 제어 하는 보다 자세한 적용 동안 HTTPS를 통해 tooRemote 데스크톱 서버를 연결 합니다.

Tooinclude에 액세스 해야 하는 기능:

- 관리자는 특정 시스템에서 toolimit 연결 toorequests를 옵션입니다.
- 스마트 카드 인증 또는 Azure Multi-Factor Authentication
- 누군가가 toovia hello 게이트웨이 연결할 수 있는 시스템을 통해 제어 합니다.
- 장치 및 디스크 리디렉션 제어

## <a name="use-a-key-management-solution"></a>키 관리 솔루션 사용

보안 키 관리는 hello 클라우드의 필수적인 tooprotecting 데이터입니다. [Azure Key Vault](../key-vault/key-vault-whatis.md)을 사용하면 HSM(하드웨어 보안 모듈)에서 암호와 같은 작은 비밀과 암호화 키를 안전하게 저장할 수 있습니다. 추가된 보증을 위해, HSM에서 키를 생성하거나 가져올 수 있습니다.

Microsoft는 FIPS 140-2 Level 2 유효성 검사가 적용된 HSM(하드웨어 및 펌웨어)에서 키를 처리합니다. Azure 로깅으로 키 사용 모니터링 및 감사: 로그를 Azure 또는 SIEM(보안 정보 및 이벤트 관리) 시스템으로 파이프하여 추가 분석 및 위협 검색을 수행합니다.

Azure를 구독하는 사용자는 Key Vault를 만들고 사용할 수 있습니다. Key Vault에는 개발자와 보안 관리자의 혜택이 있지만, 조직에서 Azure 서비스를 관리하는 관리자가 구현하고 관리할 수 있습니다.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>가상 디스크 및 디스크 저장소 암호화

[Azure 디스크 암호화](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) 주소 hello 데이터 도용 또는 노출을 디스크를 이동 하는 무단된 액세스 로부터 위협을 합니다. hello 디스크에는 다른 보안 제어를 무시 하는 방법으로 연결 된 tooanother 시스템 일 수 있습니다. 암호화 사용 하 여 디스크 [BitLocker](https://technet.microsoft.com/library/hh831713) Windows 및 Linux tooencrypt 운영 체제와 데이터 드라이브 DM 암호화 합니다. Azure 디스크 암호화는 키 자격 증명 모음 toocontrol 뿐 아니라 통합 하 고 hello 암호화 키를 관리 합니다. 표준 VM 및 Premium Storage가 있는 VM에 이 기능을 사용할 수 있습니다.

자세한 내용은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](azure-security-disk-encryption.md)을 참조하세요.

[Azure Storage 서비스 암호화](../storage/common/storage-service-encryption.md)는 미사용 데이터를 보호합니다. Hello 저장소 계정 수준에서 설정 됩니다. 데이터 센터에 기록될 때 데이터를 암호화하고, 사용자가 액세스할 때 자동으로 암호가 해독됩니다. Hello 다음 시나리오를 지원 합니다.

- 블록 Blob, 추가 Blob 및 페이지 Blob의 암호화
- 보관 된 Vhd 및 서식 파일의 암호화 온-프레미스에서 tooAzure 가져온
- VHD를 사용하여 만든 IaaS VM에 대한 데이터 디스크 및 기본 OS 암호화

Azure Storage 암호화를 계속 진행하기 전에 다음 두 가지 제한 사항에 유의해야 합니다.

- 클래식 저장소 계정에서는 사용할 수 없습니다.
- 암호화가 사용되도록 설정한 후에 기록된 데이터만 암호화합니다.

## <a name="use-a-centralized-security-management-system"></a>중앙 집중식 보안 관리 시스템 사용

서버 toobe 패치, 구성, 이벤트 및의 보안 우려 사항 간주 될 수 있는 활동에 대 한 모니터링 해야 합니다. 사용할 수 있습니다 tooaddress 관여 하는 것을 [보안 센터](https://azure.microsoft.com/services/security-center/) 및 [Operations Management Suite 보안 및 규정 준수](https://azure.microsoft.com/services/security-center/)합니다. 두이 옵션 모두 hello 운영 체제에서 hello 구성 외 이동합니다. 또한 hello 구성의 기본 네트워크 구성과 가상 어플라이언스 사용 등의 인프라 hello에 대 한 모니터링을 제공 합니다.

## <a name="manage-operating-systems"></a>운영 체제 관리

IaaS 배포에서 사용자는 여전히 다른 서버 또는 워크스테이션 사용자 환경에서와 마찬가지로, 배포 하는 hello 시스템의 hello 관리에 대 한. 패치, 강화, 권한 할당 및 다른 활동 관련 toohello 시스템 유지 관리 중인 사용자의 책임입니다. 온-프레미스 리소스와 밀접 하 게 통합 되어 있는 시스템에서는 할 수 있습니다 toouse hello 동일한 도구 및 바이러스 백신 소프트웨어, 맬웨어 방지, 패치 및 백업 등을 위한 온-프레미스를 사용 하는 절차입니다.

### <a name="harden-systems"></a>시스템 보안 강화
설치 된 hello 응용 프로그램에 필요한 서비스 끝점만 노출 되도록 Azure IaaS에서 모든 가상 컴퓨터를 강화 해야 합니다. Windows 가상 컴퓨터에 대 한 Microsoft hello에 대 한 기준으로 게시 하는 hello 권장 사항을 따르십시오 [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) 솔루션입니다.

Security Compliance Manager는 무료 도구입니다. Tooquickly 사용 하려면 구성 하 고 그룹 정책 및 System Center Configuration Manager를 사용 하 여 데스크톱, 일반 데이터 센터 및 사설 및 공용 클라우드를 관리 합니다.

Security Compliance Manager는 테스트를 마친 배포 준비가 완료된 정책 및 Desired Configuration Management 구성 팩을 제공합니다. 이러한 기준은 [Microsoft 보안 지침](https://technet.microsoft.com/en-us/library/cc184906.aspx) 권장 사항 및 업계 모범 사례를 토대로 합니다. 또한 구성 드리프트를 관리하고, 규정 준수 요구 사항을 해결하고, 보안 위험을 줄이는 데 도움이 됩니다.

두 가지 방법을 사용 하 여 컴퓨터의 Security Compliance Manager tooimport hello 현재 구성을 사용할 수 있습니다. 먼저 Active Directory 기반 그룹 정책을 가져올 수 있습니다. 둘째, "골든 master"의 hello 구성을 가져올 수 있습니다 hello를 사용 하 여 참조 컴퓨터 [LocalGPO 도구](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback hello 로컬 그룹 정책입니다. Hello 로컬 그룹 정책 Security Compliance Manager로 가져올 수 있습니다.

표준 tooindustry 모범 사례를 비교 하 고, 사용자 지정 새 정책을 만들고 Desired Configuration Management 구성 팩. Windows 10 1주년 업데이트 및 Windows Server 2016을 포함하여 지원되는 모든 운영 체제에 대한 기준이 게시되었습니다.


### <a name="install-and-manage-antimalware"></a>맬웨어 설치 및 관리

프로덕션 환경에서 개별적으로 호스트 되는 환경에 대 한 맬웨어 방지 확장 toohelp를 사용할 수 있습니다 및 클라우드 서비스를 가상 컴퓨터를 보호 합니다. 이 확장은 [Azure Security Center](../security-center/security-center-intro.md)에 통합됩니다.


[Microsoft 맬웨어 방지 프로그램](azure-security-antimalware.md)에는 실시간 보호, 예약된 검색, 맬웨어 치료, 서명 업데이트, 엔진 업데이트, 샘플 보고, 제외 이벤트 컬렉션 및 [PowerShell 지원](https://msdn.microsoft.com/library/dn771715.aspx)과 같은 기능이 포함됩니다.

![Azure 맬웨어 방지](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Hello 최신 보안 업데이트 설치
고객의 tooAzure 이동 hello 첫 번째 작업 부하의 일부는 랩 및 외부 지향 시스템입니다. 호스 티 드 Azure 가상 컴퓨터에서 응용 프로그램 또는 toobe 액세스할 수 있는 toohello 인터넷 해야 하는 서비스를 호스트 하는 경우에 패치를 적용 하는 방법에 대 한 경계 해야 합니다. Hello 운영 체제 패치 합니다. 타사 응용 프로그램에 패치가 적용 되지 않은 취약성 좋은 패치 관리 위치에 있으면 서 없앨 수 있는 tooproblems가 될 수도 있습니다.

### <a name="deploy-and-test-a-backup-solution"></a>백업 솔루션 배포 및 테스트

백업, 보안 업데이트와 동일 하 게 처리 toobe hello를 필요한 다른 모든 작업을 처리 하는 동일한 방식으로 합니다. 프로덕션 환경의 toohello 클라우드 확장의 일부인 시스템에 해당 됩니다. Test 및 dev 시스템 익숙한 경험에 온-프레미스 환경에 따라 증가 된 유사한 toowhat 사용자 복원 기능을 제공 하는 백업 전략을 준수 해야 합니다.

프로덕션 작업 이동 tooAzure을 가능 하면 기존 백업 솔루션에 통합 해야 합니다. 사용할 수 있습니다 또는 [Azure 백업](../backup/backup-azure-arm-vms.md) toohelp 백업 요구 사항을 해결 합니다.


## <a name="monitor"></a>모니터

[보안 센터](../security-center/security-center-intro.md) tooidentify 잠재적인 보안 취약점 지속적인 Azure 리소스의 hello 보안 상태 평가 제공 합니다. 권장 사항 목록 hello 필요한 컨트롤을 구성 과정을 안내 합니다.

예를 들면 다음과 같습니다.

- 맬웨어 방지 프로 비전 toohelp 식별 하 고 악성 소프트웨어를 제거 합니다.
- 네트워크 보안 그룹 및 규칙 toocontrol 트래픽 toovirtual 컴퓨터를 구성 합니다.
- 웹 응용 프로그램 방화벽 toohelp 웹 응용 프로그램을 대상으로 하는 공격을 방어할 프로 비전 합니다.
- 누락된 시스템 업데이트 배포
- Hello와 일치 하지 않는 운영 체제 구성을 주소 지정 기준을 것이 좋습니다.

hello 다음 그림에서는 일부 보안 센터에서 사용할 수 있는 hello 옵션

![Azure Security Center 정책](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. Operations Management Suite는 클라우드 기반 서비스로 구현되므로 인프라 서비스에 대한 최소한의 투자로 빠르게 배포할 수 있습니다.

새로운 기능이 자동으로 제공되므로 지속적 유지 관리 및 업그레이드 비용을 절감할 수 있습니다. Operations Management Suite는 System Center Operations Manager와도 통합됩니다. 포함 하 여 Azure 워크 로드를 보다 잘 관리 하는 다양 한 구성 요소 toohelp 있기는 [보안 및 규정 준수](../operations-management-suite/oms-security-getting-started.md) 모듈입니다.

Operations Management Suite tooview 정보에서 리소스에 대 한 hello 보안 및 규정 준수 기능을 사용할 수 있습니다. hello 정보는 4 개의 주요 범주로 구성 됩니다.

- **보안 도메인**: 시간별 보안 기록을 추가로 탐색합니다. 보안 이벤트를 사용하여 맬웨어 평가, 업데이트 평가, 네트워크 보안 정보, ID 및 액세스 정보, 컴퓨터에 액세스합니다. 빠른 액세스 toohello Azure 보안 센터 대시보드의 활용 합니다.
- **주목할 만한 문제**: 빠르게 hello 수가 활성 문제를 파악 하 고 이러한 문제의 심각도 hello 합니다.
- **감지(미리 보기)**: 리소스에 대해 수행한 대로 보안 경고를 시각화하여 공격 패턴을 식별할 수 있습니다.
- **위협 인텔리전스**: 공격 식별 hello 총 아웃 바운드 악성 IP 트래픽이 있는 서버 수를 시각화 하 여 패턴 hello 악의적인 위협 유형 및 이러한 Ip에서 생성 되는 위치를 보여 주는 지도입니다.
- **일반적인 보안 쿼리**: hello 가장 일반적인 보안 목록을 사용할 수 있는 toomonitor 환경 쿼리를 참조 하십시오. 이러한 쿼리 중 하나를 클릭 하면 hello **검색** 블레이드가 열리고 해당 쿼리에 대 한 hello 결과 보여 줍니다.

hello 다음 스크린샷은 Operations Management Suite를 표시할 수 있는 hello 정보의 예입니다.

![Operations Management Suite 보안 기준](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>다음 단계


* [Azure 보안 팀 블로그](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft 보안 대응 센터](https://technet.microsoft.com/library/dn440717.aspx)
* [Azure 보안 모범 사례 및 패턴](security-best-practices-and-patterns.md)
