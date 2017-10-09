---
title: "aaaData 보안 및 암호화에 대 한 유용한 정보 | Microsoft Docs"
description: "이 문서에서는 기본 제공 Azure 기능을 사용한 데이터 보안 및 암호화 모범 사례를 제공합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Azure 데이터 보안 및 암호화 모범 사례
데이터 발생할 수 있는 및 해당 상태에 대해 사용할 수 있는 컨트롤의 hello 가능한 상태에 대 한 회계는 hello 클라우드에서 hello 키 toodata 보호 중 하나입니다. Azure 데이터 보안 및 암호화 모범 사례 hello 목적을 위해 데이터의 상태가 다음 hello 주위 hello 권장 됩니다.

* 저장: 모든 정보 저장 개체, 컨테이너 및 물리적 미디어(자기 또는 광 디스크)에 정적으로 존재하는 유형이 여기에 포함됩니다.
* 전송 중인: 때 데이터 사이 전송 될 구성 요소, 위치 또는 프로그램을와 같은 hello 네트워크를 통해 (온-프레미스 toocloud 반대의 ExpressRoute와 같은 하이브리드 연결을 포함 하 여)에서 서비스 버스를 통해 또는 입력/출력 하는 동안 프로세스 생각 됩니다의 것으로 동작 합니다.

이 문서에서는 Azure 데이터 보안 및 암호화 모범 사례 컬렉션에 대해 설명합니다. 이들 모범 사례는 Azure 데이터 보안 경험에서 파생 된 및 명의 고객이 직접 암호화 및 hello 발생 합니다.

각 모범 사례에 대해 다음 사항을 설명하겠습니다.

* 어떤 hello 것이 좋습니다.
* 이유는 tooenable 최선의 방법을
* Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
* 가능한 대안 toohello 모범 사례
* Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

이 Azure 데이터 보안 및 암호화에 대 한 유용한 정보 문서는 합의 의견 및 Azure 플랫폼 기능 및 기능 집합에 기초이 문서가 작성 된 hello 시 존재 합니다. 의견 및 기술 시간이 지남에 따라 변경 하 고이 문서 됩니다. 이러한 변경 내용을 정기적으로 tooreflect에서 업데이트 합니다.

이 문서에서 다루는 Azure 데이터 보안 및 암호화 모범 사례에는 다음이 포함됩니다.

* Multi-Factor Authentication 적용
* RBAC(역할 기반 액세스 제어) 사용
* Azure 가상 컴퓨터 암호화
* 하드웨어 보안 모델 사용
* 보안 워크스테이션을 사용하여 관리
* SQL 데이터 암호화 활성화
* 전송 중인 데이터 보호
* 파일 수준 데이터 암호화 적용

## <a name="enforce-multi-factor-authentication"></a>Multi-Factor Authentication 적용
데이터 액세스의 첫 번째 단계 hello 및 Microsoft Azure에서 제어 tooauthenticate hello 사용자입니다. [Azure MFA(Multi-Factor Authentication)](../multi-factor-authentication/multi-factor-authentication.md)는 사용자 이름 및 암호 이외의 다른 수단을 사용하여 사용자의 ID를 확인하는 방법입니다. 이 인증 방법을 간단 로그인에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다.

사용자를 위해 Azure MFA를 사용 하 여 두 번째 계층을 보안 toouser 로그인 및 트랜잭션에 추가 됩니다. 이 경우 트랜잭션이 파일 서버 또는 SharePoint Online에 있는 문서에 액세스할 수 있습니다. Azure MFA는 손상 된 자격 증명 액세스 tooorganization 데이터를 포함 하는 IT tooreduce hello 가능성도 도움이 됩니다.

예: 사용자를 위해 Azure MFA를 적용 하 고 구성 toouse 전화 통화 또는 문자 메시지 확인으로 hello 사용자의 자격 증명 손상 되는 경우 공격자가 hello 없습니다 되므로 수 tooaccess 리소스 액세스 toouser 전화 사용할 수 없습니다. Id 보호 이러한 추가 계층을 추가 하지 않는 조직에서는 toodata 손상을 야기할 수 있는 자격 증명 도난 공격에 보다 민감한 있습니다.

한 가지 대안은 tookeep hello 인증 제어 하려는 조직에 온-프레미스 않았습니다 toouse [Azure Multi-factor Authentication 서버](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), MFA 온-프레미스 라고도 합니다. 이 방법을 사용 하 여 hello MFA 서버 온-프레미스를 유지 하면서 수 tooenforce multi-factor authentication을 수 있습니다.

Azure MFA에 대 한 자세한 내용은 hello 문서를 참조 하세요 [hello 클라우드에서 Azure Multi-factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)합니다.

## <a name="use-role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어) 사용
Hello에 따라 액세스를 제한할 [tooknow 필요](https://en.wikipedia.org/wiki/Need_to_know) 및 [최소 권한](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 보안 원칙입니다. 데이터 액세스를 위한 보안 정책 tooenforce 하려는 조직에 필수적입니다. Azure 역할 기반 액세스 제어 (RBAC) 사용 하는 tooassign 권한 toousers, 그룹 및 특정 범위의 응용 프로그램 수 있습니다. 역할 할당의 hello 범위는 구독, 리소스 그룹 또는 단일 리소스 될 수 있습니다.

활용할 수 있는 [기본 제공 RBAC 역할](../active-directory/role-based-access-built-in-roles.md) Azure에서 tooassign 권한 toousers 합니다. 사용 하는 것이 좋습니다 *저장소 계정 참가자* toomanage 저장소 계정이 필요로 하는 클라우드 운영자에 대 한 및 *클래식 저장소 계정을 참가자* 역할 toomanage 클래식 저장소 계정을 합니다. 필요한 toomanage Vm 및 저장소 계정을 클라우드 연산자에 대 한 너무 추가한 것이 좋습니다*가상 컴퓨터 참가자* 역할입니다.

RBAC 같은 기능을 활용하여 데이터 액세스 제어를 적용하지 않는 조직은 사용자에게 필요 이상으로 많은 권한을 부여하게 될 수 있습니다. Hello 먼저에서 하면 안 되는 액세스 toodata 있는 일부 사용자가 포함 하면 toodata 손상이 발생할 수 있습니다.

Hello 문서를 참조 하 여 Azure RBAC에 대해 자세히 알아보십시오 [신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.

## <a name="encrypt-azure-virtual-machines"></a>Azure 가상 컴퓨터 암호화
여러 조직에서 [미사용 데이터 암호화](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/)는 데이터 프라이버시, 규정 준수 및 데이터 주권을 위한 필수 단계입니다. Azure 디스크 암호화는 IT 관리자가 tooencrypt Windows 및 Linux IaaS 가상 컴퓨터 (VM) 디스크를 사용합니다. Azure 디스크 암호화는 windows hello 업계 표준 BitLocker 기능 및 운영 체제 hello에 대 한 Linux tooprovide 볼륨 암호화의 hello DM 암호화 기능 및 hello 데이터 디스크를 활용합니다.

Azure 디스크 암호화를 활용할 수 있습니다 toohelp 보호를 보호 하 고 데이터 toomeet 조직 보안 및 규정 준수 요구 사항입니다. 조직에서는 암호화를 사용 하 여 고려해 야 toohelp 관련된 toounauthorized 데이터 액세스 위험을 완화 합니다. 또한 이전 toowriting 중요 한 데이터 toothem 드라이브를 암호화 하는 것이 좋습니다.

Azure 저장소 계정에 저장 된 상태의 순서 tooprotect 데이터에서 있는지 tooencrypt VM의 데이터 볼륨과 부팅 볼륨을 확인 합니다. 활용 하 여 hello 암호화 키 및 암호 보호 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md)합니다.

온-프레미스 Windows 서버를 사용 하 여 hello를 암호화 최선의 구현 방법을 고려해 보십시오.

* [BitLocker](https://technet.microsoft.com/library/dn306081.aspx)를 사용하여 데이터 암호화
* AD DS에 복구 정보를 저장합니다.
* BitLocker 키가 손상 되었거나 고려 이면 hello 드라이브 tooremove hello 드라이브 또는 했는지 hello BitLocker 메타 데이터의 모든 인스턴스가 암호를 해독 하 고 hello 전체 드라이브를 다시 암호화 하거나 포맷 하는 것이 좋습니다.

데이터 암호화를 실행 하지 않는 조직에서는 가능성이 더 노출 toobe toodata 악의적 이거나 rogue 사용자 데이터를 도용 같은 무결성 문제는 되 고 서식 지우기에 대 한 무단된 액세스 toodata 인하여 계정을 손상 합니다. 이러한 위험 외에도 이러한 노력를 hello 올바른 보안 컨트롤 tooenhance 데이터 보안을 사용 하는 업계 규정 toocomply 일반 기업 증명 해야 합니다.

Hello 문서를 참조 하 여 Azure 디스크 암호화에 대해 자세히 알아보십시오 [Azure 디스크 암호화에 대 한 Windows 및 Linux IaaS Vm](azure-security-disk-encryption.md)합니다.

## <a name="use-hardware-security-modules"></a>하드웨어 보안 모듈 사용
업계 암호화 솔루션 tooencrypt 데이터 비밀 키를 사용합니다. 따라서 이러한 키를 안전하게 보관해야 합니다. 키 관리 사용된 toostore 비밀 키를 사용 되는 tooencrypt 데이터는 것 때문에 반드시 필요한 부분이 데이터 보호 됩니다.

Azure 디스크 암호화를 사용 하 여 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) toohelp 제어 및 관리 디스크 암호화 키 및 비밀 키 자격 증명 모음 구독에서 Azure의 hello 가상 컴퓨터 디스크에서 모든 데이터가 암호화 되는 동시에 저장소입니다. Azure 키 자격 증명 모음 tooaudit 키 및 정책 사용 현황을 사용 해야 합니다.

데이터 위치 tooprotect hello 비밀 키를 사용 하는 tooencrypt에 적절 한 보안 제어를 포함 많은 위험이 관련된 toonot 가지가 있습니다. 공격자가 액세스할 있으면 toohello 비밀 키 수 toodecrypt hello 데이터 수를 잠재적으로 없는 tooconfidential 정보에 액세스 합니다.

Hello 문서를 참조 하 여 Azure에서 인증서 관리에 대 한 일반 권장 사항에 대 한 자세히 알아볼 수 있습니다 [Azure 관리 인증서: 관련 하 여 수행](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)합니다.

Azure 키 자격 증명 모음에 대한 자세한 내용은 [Azure 키 자격 증명 모음 시작](../key-vault/key-vault-get-started.md)을 참조하세요.

## <a name="manage-with-secure-workstations"></a>보안 워크스테이션을 사용하여 관리
Hello 포함 된 대부분의 hello 공격 대상 hello 최종 사용자, 이후 hello 끝점 공격의 hello 기본 지점 중 하나 됩니다. 공격자가 hello 끝점을 침해할 경우 hello 사용자의 자격 증명 toogain 액세스 tooorganization 데이터를 활용할 수 그 합니다. 대부분 끝점 공격은 hello 팩트 최종 사용자가 자신의 로컬 워크스테이션에서 관리자 수 tootake 활용 합니다.

보안 관리 워크스테이션을 사용하면 이러한 위험을 줄일 수 있습니다. 사용 하는 것이 좋습니다는 [권한 있는 액세스 워크스테이션 PAW ()](https://technet.microsoft.com/library/mt634654.aspx) 워크스테이션의 tooreduce hello 공격 노출 합니다. 보안 관리 워크스테이션은 이러한 공격 위험 중 일부를 완화하여 데이터를 안전하게 보호하는 데 도움이 됩니다. 워크스테이션 아래로 있는지 toouse PAW tooharden 및 잠금 확인 하십시오. 이 중요 한 계정 작업 및 데이터 보호에 대 한 중요 한 단계 tooprovide 높음 보증입니다.

끝점 보호 부족 수 데이터를 위험에 빠트릴, 있는지 tooenforce 보안 정책을 hello 데이터 위치 (클라우드 또는 온-프레미스)에 관계 없이 사용 되는 tooconsume 데이터는 모든 장치에서.

Hello 문서를 참조 하 여 워크스테이션에 액세스할 권한이 대해 자세히 알아볼 수 있습니다 [권한 있는 액세스 보안](https://technet.microsoft.com/library/mt631194.aspx)합니다.

## <a name="enable-sql-data-encryption"></a>SQL 데이터 암호화 활성화
[Azure SQL 데이터베이스 투명 한 데이터 암호화](https://msdn.microsoft.com/library/dn948096.aspx) (TDE)는의 hello 데이터베이스에 연결 된 백업, 실시간 암호화 / 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 하 고 트랜잭션 로그 파일 없이 미사용 필요한 변경 내용 toohello 응용 프로그램입니다.  TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다.

Hello 전체 저장소를 암호화 한 경우에 반드시 tooalso 자체 데이터베이스를 암호화 합니다. Hello 철저 한 방어 데이터 보호 방법은의 구현입니다. 사용 중인 경우 [Azure SQL 데이터베이스](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) tooprotect 중요 한 데이터를 보려면 예: 신용 카드 또는 주민 등록 번호를 암호화할 수 있습니다 FIPS 사용 하 여 데이터베이스의 많은 hello 요구 사항을 충족 하는 140-2의 유효성이 검사 된 256 비트 AES 암호화 산업 표준 (예: HIPAA, PCI).

파일 관련 너무 중요 한 toounderstand는[버퍼 풀 확장](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) TDE를 사용 하 여 데이터베이스를 암호화 하는 경우 암호화 하지 않습니다. BitLocker 또는 hello와 같은 파일 시스템 수준 암호화 도구를 사용 해야 [파일 시스템 암호화](https://technet.microsoft.com/library/cc700811.aspx) (EFS) BPE 관련 파일입니다.

이후 권한 있는 사용자는 보안 관리자 또는 데이터베이스 관리자가 hello 데이터베이스가 암호화 TDE를 사용 하는 경우에 hello 데이터를 액세스할 수와 같은 hello 권장 사항도 따라야 아래:

* Hello 데이터베이스 수준에서 SQL 인증
* RBAC 역할을 사용하여 Azure AD 인증
* 사용자와 응용 프로그램에는 별도 계정을 tooauthenticate를 사용 해야 합니다. 이러한 방식으로 toousers 및 응용 프로그램에 부여 하는 hello 사용 권한을 제한 하 고 악의적인 활동의 hello 위험을 줄일 수 있습니다
* 구현 데이터베이스 수준 보안 (예: db_datareader, db_datawriter) 고정된 데이터베이스 역할 또는 있습니다를 사용 하 여 응용 프로그램 toogrant에 대 한 사용자 지정 역할 명시적 사용 권한을 tooselected 데이터베이스 개체를 만들 수 있습니다.

데이터베이스 수준 암호화를 사용하지 않는 조직은 SQL 데이터베이스에 있는 데이터를 손상시키는 공격에 취약할 수 있습니다.

Hello 문서를 참조 하 여 자세한 SQL TDE 암호화에 대 한 내용은 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx)합니다.

## <a name="protect-data-in-transit"></a>전송 중인 데이터 보호
전송 중인 데이터 보호는 데이터 보호 전략에서 절대 빠질 수 없는 핵심입니다. 데이터는 여러 위치에서 앞뒤로 이동 됩니다, hello 일반적인 권장 사항은 이므로 다른 위치에서 SSL/TLS 프로토콜 tooexchange 데이터 항상 사용. 일부 경우에 온-프레미스와 클라우드 간의 tooisolate hello 전체 통신 채널을 사용할 수 있습니다 가상 사설망 (VPN)을 사용 하 여 인프라입니다.

온-프레미스 인프라와 Azure 사이를 이동하는 데이터의 경우 HTTPS 또는 VPN처럼 적절한 안전 장치를 고려해야 합니다.

여러 워크스테이션 온-프레미스 tooAzure에서 toosecure 액세스 해야 하는 조직에서 사용 하 여 [Azure 사이트 간 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)합니다.

한 워크스테이션에서 toosecure 액세스 해야 하는 조직에서는 온-프레미스 tooAzure를 사용 하 여 64 \ [지점 및 사이트 간 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)합니다.

대용량 데이터 집합은 [Express 경로](https://azure.microsoft.com/services/expressroute/) 같은 전용 고속 WAN 링크를 통해 이동할 수 있습니다. 또한 사용 하 여 hello 응용 프로그램 수준에서 hello 데이터를 암호화할 수 toouse express 경로 선택 하면 [SSL/TLS](https://support.microsoft.com/kb/257591) 또는 추가적인된 보호를 위해 다른 프로토콜입니다.

Hello Azure 포털을 통해 Azure 저장소와 상호 작용 하는, 하는 경우 HTTPS를 통해 모든 트랜잭션이 발생 합니다. [저장소 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS를 통해 수도 있습니다를 사용 하는 toointeract [Azure 저장소](https://azure.microsoft.com/services/storage/) 및 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/)합니다.

Tooprotect 데이터 전송 중에 실패 하는 조직에 보다 민감한는 [중간자 개입 공격](https://technet.microsoft.com/library/gg195821.aspx), [도청](https://technet.microsoft.com/library/gg195641.aspx) 및 세션 하이재킹입니다. 이러한 공격은 tooconfidential 데이터에 액세스 하지 못하도록 hello 첫 번째 단계 수 있습니다.

Hello 문서를 참조 하 여 Azure VPN 옵션에 대 한 자세히 알아볼 수 있습니다 [계획 및 디자인 VPN 게이트웨이에 대 한](../vpn-gateway/vpn-gateway-plan-design.md)합니다.

## <a name="enforce-file-level-data-encryption"></a>파일 수준 데이터 암호화 적용
또 다른 hello 데이터에 대 한 보안 수준을 높일 수 있는 보호 계층 hello 파일 자체를 hello 파일 위치와 상관 없이 암호화 합니다.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) 사용 하 여 암호화, id 및 권한 부여 정책 toohelp 보안 여 파일과 전자 메일을 설정 합니다. Azure RMS는 조직 내부와 조직 외부에서 휴대폰, 태블릿 및 PC와 같은 여러 장치를 보호합니다. 이 기능은 Azure RMS는 조직의 경계를 벗어나 더라도 hello 데이터를 계속 보호 수준을 추가 하기 때문에 가능 합니다.

Azure RMS tooprotect 파일을 사용 하는 업계 표준 암호화의 완벽 하 게 지원 [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html)합니다. 복사한 toostorage의 hello 제어 하지 않는 경우에 hello 파일 hello 보호가 유지 됩니다. hello 보증 있는 Azure RMS를 활용 하 여 데이터를 보호 하는 경우 클라우드 저장소 서비스 등 IT 합니다. hello 동일 하 게 실행 전자 메일을 통해 공유 하는 파일에 대 한 hello 파일을 첨부 tooan 전자 메일 메시지 보호와, 지침이 포함 된 방법을 tooopen hello 보호 된 첨부 파일입니다.

Azure RMS 채택을 계획할 때 다음을 hello 좋습니다.

* Hello 설치 [RMS 공유 앱](https://technet.microsoft.com/library/dn339006.aspx)합니다. 이 앱은 사용자가 간편하게 파일을 직접 보호할 수 있도록 Office 추가 기능을 설치하여 Office와 통합됩니다.
* 응용 프로그램 및 서비스 toosupport Azure RMS 구성
* 비즈니스 요구 사항을 반영하는 [사용자 지정 템플릿](https://technet.microsoft.com/library/dn642472.aspx) 만들기. 예: 모든 극비 관련 전자 메일에 적용해야 하는 극비 데이터 템플릿.

약한에 있는 조직이 [데이터 분류](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 파일 보호 보다 민감한 toodata 유출을 수 있습니다. 적절 한 파일 보호 없이 조직 않습니다 수 tooobtain 비즈니스 통찰력, 남용 모니터링 하며 방지의 악의적인 액세스 toofiles 합니다.

Hello 문서를 참조 하 여 Azure RMS에 대해 자세히 알아볼 수 있습니다 [Azure 권한 관리 시작](https://technet.microsoft.com/library/jj585016.aspx)합니다.
