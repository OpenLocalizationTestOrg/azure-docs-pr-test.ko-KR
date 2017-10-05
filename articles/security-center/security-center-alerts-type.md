---
title: "Azure Security Center에서 유형별 보안 경고 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center에서 사용할 수 있는 다양한 종류의 보안 경고를 설명합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: 19f71e0d5a8a4642b86ae60a3ab2a4042fa2990e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Azure Security Center에서 보안 경고 이해
이 문서를 통해 Azure Security Center에서 사용할 수 있는 다양한 유형의 보안 경고 및 관련된 정보를 이해할 수 있습니다. 경고 및 인시던트를 관리하는 방법에 대한 자세한 내용은 [Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)을 참조하세요.

> [!NOTE]
> 고급 감지를 설정하려면 Azure Security Center 표준으로 업그레이드합니다. 무료 60일 평가판을 사용할 수 있습니다. 업그레이드하려면 [보안 정책](security-center-policies.md)에서 **가격 책정 계층**을 선택합니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/security-center/)를 참조하세요.
>

## <a name="what-type-of-alerts-are-available"></a>어떤 유형의 경고를 사용할 수 있습니까?
Azure Security Center는 다양한 [검색 기능](security-center-detection-capabilities.md)을 사용하여 고객에게 환경을 대상으로 하는 잠재적인 공격에 대해 경고합니다. 이러한 경고는 트리거한 경고, 대상 리소스 및 공격의 출처에 대한 중요한 정보를 포함합니다. 경고에 포함된 정보는 위협을 검색하는 데 사용되는 분석의 유형에 따라 달라집니다. 인시던트는 위협을 조사할 때 유용할 수 있는 추가 컨텍스트 정보를 포함할 수도 있습니다.  이 문서는 다음 경고 유형에 대한 정보를 제공합니다.

* VMBA(가상 컴퓨터 동작 분석)
* 네트워크 분석
* 리소스 분석
* 컨텍스트 정보

## <a name="virtual-machine-behavioral-analysis"></a>VMBA(가상 컴퓨터 동작 분석)
Azure Security Center는 동작 분석을 사용하여 가상 컴퓨터 이벤트 로그의 분석에 따라 손상된 리소스를 식별할 수 있습니다. 예를 들어 프로세스 만들기 이벤트 및 로그인 이벤트가 있습니다. 또한 광범위한 캠페인의 증거 지원을 확인하는 다른 신호와의 상관 관계가 있습니다.

> [!NOTE]
> Security Center 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참조하세요.
>

### <a name="crash-analysis"></a>충돌 분석
크래시 덤프 메모리 분석은 기존 보안 솔루션을 피할 수 있는 정교한 맬웨어를 감지하는 데 사용되는 방법입니다. 다양한 형식의 맬웨어는 디스크에 작성하지 않거나 디스크에 작성된 소프트웨어 구성 요소를 암호화하여 바이러스 백신 제품에서 탐지되지 않으려 합니다. 따라서 맬웨어는 기존 맬웨어 방지 방법을 사용하여 감지하기 어렵게 됩니다. 그러나 이러한 종류의 맬웨어는 작동하기 위해 메모리에 추적을 남겨야 하므로 메모리 분석을 사용하여 검색될 수 있습니다.

소프트웨어가 충돌할 때 크래시 덤프는 충돌 시 메모리의 일부를 캡처합니다. 충돌은 맬웨어, 일반 응용 프로그램 또는 시스템 문제로 인해 발생할 수 있습니다. 크래시 덤프의 메모리를 분석하여 Security Center는 소프트웨어에서 취약점을 악용하고 기밀 데이터에 액세스하고 손상된 컴퓨터에서 은밀하게 유지하는 데 사용되는 기술을 감지할 수 있습니다. 분석이 Security Center 백 엔드에 의해 수행되므로 호스트에 대한 최소 성능에 영향을 주게 됩니다.

다음 필드는 이 문서의 뒷부분에 나타나는 크래시 덤프 경고 예제에 공통적으로 적용됩니다.

* DUMPFILE: 크래시 덤프 파일의 이름입니다.
* PROCESSNAME: 충돌하는 프로세스의 이름입니다.
* PROCESSVERSION: 충돌하는 프로세스의 버전입니다.

### <a name="shellcode-discovered"></a>Shellcode 검색
Shellcode는 맬웨어가 소프트웨어 취약점을 악용한 후에 실행되는 페이로드입니다. 이 경고는 크래시 덤프 분석이 악의적인 페이로드에서 일반적으로 수행되는 동작을 표시하는 실행 코드를 감지했음을 나타냅니다. 악의적이지 않은 소프트웨어가 이 동작을 수행할 수 있지만 보통 소프트웨어 개발 방법으로서는 일반적이지 않습니다.

이 Shellcode 경고 예제는 다음과 같은 추가 필드를 제공합니다.

* ADDRESS: shellcode의 메모리에 있는 위치입니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![Shellcode 경고](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>모듈 하이재킹 검색
Windows는 DLL(동적 링크 라이브러리)을 사용하여 소프트웨어가 일반적인 Windows 시스템 기능을 활용할 수 있도록 합니다. DLL 하이재킹은 맬웨어가 DLL 로드 순서를 변경시켜 악의적인 페이로드를 임의 코드를 실행할 수 있는 메모리에 로드할 때 발생합니다. 이 경고는 크래시 덤프 분석이 서로 다른 두 경로에서 로드되는 이름이 비슷한 모듈을 감지했음을 나타냅니다. 로드된 경로 중 하나는 일반적인 Windows 시스템 이진 위치에서 제공됩니다.

합법적인 소프트웨어 개발자는 종종 Windows OS를 조율하고 확장하거나 Windows 응용 프로그램을 확장하는 등 악의적이지 않은 이유로 DLL 로드 순서를 변경합니다. DLL 로드 순서에 대한 악의적인 변경 내용과 잠재적으로 심각하지 않은 변경 내용을 구분하기 위해 Azure Security Center는 로드된 모듈이 의심스러운 프로필을 준수하는지를 확인합니다. 이 검사의 결과는 경고의 "서명" 필드에 의해 나타나고 경고, 경고 설명 및 경고 문제 해결 단계의 심각도에 반영됩니다. 모듈이 합법적이거나 악성 여부를 조사하려면 하이재킹 모듈의 온 디스크 복사본을 분석합니다. 예를 들어 파일의 디지털 서명을 확인하거나 바이러스 백신 검사를 실행할 수 있습니다.

이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 필드를 제공합니다.

* SIGNATURE: 하이재킹 모듈이 의심스러운 동작 프로필을 준수하는 경우를 나타냅니다.
* HIJACKEDMODULE: 하이재킹된 Windows 시스템 모듈의 이름입니다.
* HIJACKEDMODULEPATH: 하이재킹된 Windows 시스템 모듈의 경로입니다.
* HIJACKINGMODULEPATH: 하이재킹된 모듈의 경로입니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![모듈 하이재킹 경고](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>위장 Windows 모듈 감지
맬웨어는 시스템 관리자로부터 악성 소프트웨어의 특성을 *섞고* 가리기 위해 Windows 시스템 이진 파일(예: SVCHOST.EXE) 또는 모듈(예: NTDLL.DLL)의 일반적인 이름을 사용할 수 있습니다. 이 경고는 크래시 덤프 파일이 Windows 시스템 모듈 이름을 사용하는 모듈을 포함하지만 Windows 모듈의 일반적인 다른 조건을 만족하지 않는다는 점을 크래시 덤프 분석에서 감지했음을 나타냅니다. 위장 모듈의 온 디스크 복사본에 대해 분석하면 이 모듈의 합법적인 또는 악의적인 특성에 대한 자세한 정보를 제공할 수 있습니다. 분석은 다음을 포함할 수 있습니다.

* 문제의 파일이 합법적인 소프트웨어 패키지의 일부로 제공되고 있는지 확인합니다.
* 파일의 디지털 서명을 확인합니다.
* 파일에 대해 바이러스 백신 검사를 실행합니다.

이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 추가 필드를 제공합니다.

* DETAILS: 모듈의 메타데이터가 유효한지와 모듈이 시스템 경로에서 로드되는지 여부를 설명합니다.
* NAME: 위장 Windows 모듈의 이름입니다.
* PATH: 위장 Windows 모듈의 경로

또한 이 경고는 "CHECKSUM" 및 "TIMESTAMP"와 같은 모듈의 PE 헤더에서 특정 필드를 추출하고 표시합니다. 이러한 필드는 모듈에 있는 경우에만 표시됩니다. 이러한 필드에 대한 자세한 내용은 [Microsoft PE 및 COFF 사양](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) 을 참조하세요.

이러한 유형의 경고 예제는 다음과 같습니다.

![가상 Windows 경고](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>수정된 시스템 이진 파일 검색
맬웨어는 은밀하게 데이터에 액세스하거나 손상된 시스템 상에 몰래 지속되기 위해 핵심 시스템 이진 파일을 수정할 수 있습니다. 이 경고는 핵심 Windows OS 이진 파일이 메모리나 디스크에서 수정된 것을 크래시 덤프 분석에서 감지했음을 나타냅니다.

때때로 합법적인 소프트웨어 개발자는 Detours 등 응용 프로그램 호환성을 위해 악의적이지 않은 이유로 메모리에서 자유롭게 시스템 모듈을 수정합니다. 악의적인 모듈과 잠재적으로 합법적인 모듈을 구분하기 위해 Azure Security Center는 수정된 모듈이 의심스러운 프로필을 준수하는지를 확인합니다. 이 검사의 결과는 경고, 경고 설명 및 경고 문제 해결 단계의 심각도 별로 표시됩니다.

이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 추가 필드를 제공합니다.

* MODULENAME: 수정된 시스템 이진 파일의 이름입니다.
* MODULEVERSION: 수정된 시스템 이진 파일의 버전입니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![시스템 이진 경고](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>의심스러운 프로세스 실행
Security Center는 대상 가상 컴퓨터에서 실행되는 의심스러운 프로세스를 식별한 다음 경고를 트리거합니다. 검색은 특정 이름을 찾지 않지만 실행 파일의 매개 변수를 찾습니다. 따라서 공격자가 실행 파일의 이름을 바꾸더라도 Security Center는 여전히 의심스러운 프로세스를 검색할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![의심스러운 프로세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>여러 도메인 계정 쿼리
Security Center는 Active Directory 도메인 계정을 쿼리하는 여러 시도를 감지할 수 있으며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다. 공격자는 이 기술을 활용하여 사용자를 식별하고 도메인 관리자 계정을 식별하고 도메인 컨트롤러인 컴퓨터를 식별하고 다른 도메인과 잠재적인 도메인 트러스트 관계가 있는지를 식별하는 도메인을 쿼리할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![여러 도메인 계정 경고](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>로컬 관리자 그룹 구성원이 열거됨

Security Center는 Windows Server 2016 및 Windows 10에서 보안 이벤트 4798이 트리거될 때 경고를 트리거합니다. 로컬 관리자 그룹이 열거될 때 발생하며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다. 공격자는 이 기술을 활용하여 관리자 권한을 가진 사용자의 ID를 쿼리합니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![로컬 관리자](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>대/소문자의 비정상적인 혼합

Security Center는 명령줄에서 대/소문자 혼합이 사용된 것을 감지하면 경고를 트리거합니다. 일부 공격자는 이 기술을 사용하여 대/소문자 또는 해시 기반 컴퓨터 규칙을 숨길 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![비정상적인 혼합](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>의심스러운 Kerberos Golden Ticket 공격

공격자는 Kerberos "Golden Ticket"을 만들기 위해 손상된 [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) 키를 사용하여 공격자가 원하는 사용자를 가장할 수 있습니다. Security Center에서 이 활동 유형을 감지할 때 경고를 트리거합니다.

> [!NOTE] 
> Kerberos Golden Ticket에 대한 자세한 내용은 [Windows 10 자격 증명 도난 방지 가이드](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)(영문)를 참조하세요.

이러한 유형의 경고 예제는 다음과 같습니다.

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>의심스러운 계정 생성

Security Center는 기존의 기본 제공 관리 권한 계정과 매우 유사한 계정을 만들 때 경고를 트리거합니다. 이 기술은 사용자 검증으로 알아 채지 못하도록 하기 위해 공격자가 악의적인 계정을 만드는 데 사용할 수 있습니다.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![의심스러운 계정](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>의심스러운 방화벽 규칙 생성됨

공격자는 악의적 응용 프로그램이 명령 및 컨트롤과 통신할 수 있도록 사용자 지정 방화벽 규칙을 만들어 호스트 보안을 우회하거나 손상된 호스트를 통해 네트워크로 공격을 시도할 수 있습니다. Security Center는 의심스러운 위치의 실행 파일에서 새 방화벽 규칙이 생성된 것을 감지하면 경고를 트리거합니다.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![방화벽 규칙](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>HTA 및 PowerShell의 의심스러운 조합

Security Center는 Microsoft HTML Application Host(HTA)에서 PowerShell 명령이 실행되는 것을 감지하면 경고를 트리거합니다. 공격자가 악의적인 PowerShell 스크립트를 실행하기 위해 사용하는 기법입니다.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![HTA 및 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>네트워크 분석
Security Center 네트워크 위협 감지는 Azure IPFIX(인터넷 프로토콜 흐름 정보 내보내기)에서 보안 정보를 자동으로 수집하여 작동합니다. 위협을 식별하도록 종종 여러 소스의 정보를 상호 연결하는 이 정보를 분석합니다.

### <a name="suspicious-outgoing-traffic-detected"></a>의심스러운 나가는 트래픽 감지
다른 유형의 시스템과 거의 동일한 방법으로 네트워크 장치를 검색하고 프로파일링할 수 있습니다. 공격자는 일반적으로 포트 검색 또는 포트 비우기를 시작합니다. 다음 예제에서는 VM에서 의심스러운 SSH(Secure Shell) 트래픽을 갖습니다. 이 시나리오에서는 외부 리소스에 대한 SSH 무작위 공격 또는 포트 비우기 공격이 가능합니다.

![의심스러운 나가는 트래픽 경고](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

이 경고는 이 공격을 시작하는 데 사용된 리소스를 식별하는 데 사용할 수 있는 정보를 제공합니다. 이 경고는 또한 손상된 컴퓨터, 검색 시간 및 사용된 프로토콜 및 포트를 식별하는 정보를 제공합니다. 이 블레이드는 이 문제를 완화하기 위해 사용할 수 있는 수정 단계 목록도 제공합니다.

### <a name="network-communication-with-a-malicious-machine"></a>악의적인 컴퓨터와 네트워크 통신
Azure Security Center는 Microsoft 위협 인텔리전스 피드를 활용하여 악성 IP 주소와 통신하는 손상된 컴퓨터를 검색할 수 있습니다. 많은 경우 악성 주소는 명령 및 제어 센터입니다. 이 경우에 Security Center는 Pony Loader 맬웨어([Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)라고도 함)를 사용하여 실행된 통신을 감지했습니다.

![네트워크 통신 경고](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

이 경고는 이 공격을 시작하는 데 사용된 리소스, 공격을 받는 리소스, 공격 대상 IP, 공격자 IP 및 감지 시간을 식별할 수 있는 정보를 제공합니다.

> [!NOTE]
> 라이브 IP 주소는 개인 정보 보호 목적을 위해 이 스크린샷에서 제거되었습니다.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>가능한 발신 서비스 거부 공격 감지
하나의 가상 컴퓨터에서 발생하는 비정상적인 네트워크 트래픽으로 인해 Security Center에서 잠재적 서비스 거부 유형의 공격을 트리거할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![발신 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>리소스 분석
Security Center 리소스 분석은 [Azure SQL Database 위협 요소 탐지](../sql-database/sql-database-threat-detection.md) 기능과의 통합 같은 PaaS(Platform as a Service) 서비스에 집중합니다. 이러한 영역에서 분석의 결과에 따라 Security Center는 리소스 관련 경고를 트리거합니다.

### <a name="potential-sql-injection"></a>잠재적인 SQL 삽입
SQL 삽입은 구문 분석 및 실행을 위해 나중에 SQL Server의 인스턴스로 전달된 문자열에 악성 코드를 삽입한 공격입니다. SQL Server가 수신하는 모든 구문상 유효한 쿼리를 실행하기 때문에 SQL 문을 생성하는 모든 프로시저에 삽입 취약성이 있는지 검토해야 합니다. SQL 위협 요소 탐지는 기계 학습, 동작 분석 및 이상 탐지를 사용하여 Azure SQL Databases에서 발생할 수 있는 의심스러운 이벤트를 확인합니다. 예:

* 이전 직원이 데이터베이스 액세스 시도
* SQL 삽입 공격
* 집에 있는 사용자로부터 프로덕션 데이터베이스에 대한 비정상적인 액세스

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

공격을 받는 리소스, 감지 시간 및 공격의 상태를 식별하는 데 이 경고의 정보를 사용할 수 있습니다. 또한 추가 조사 단계에 대한 링크를 제공합니다.

### <a name="vulnerability-to-sql-injection"></a>SQL 삽입에 대한 취약점
데이터베이스에서 응용 프로그램 오류가 검색될 때 이 경고가 트리거됩니다. 이 경고는 SQL 삽입 공격에 대한 가능한 취약점을 나타낼 수 있습니다.

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>알 수 없는 위치에서 비정상적인 액세스
알 수 없는 IP 주소에서 액세스 이벤트가 서버에서 감지된 경우 이 경고가 트리거되며 이는 마지막 기간에서는 확인할 수 없습니다.

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>컨텍스트 정보
조사 중 분석가는 위협의 원인 및 완화하는 방법에 대한 결과에 도달하기 위해 추가 컨텍스트가 필요합니다.  예를 들어 네트워크가 변칙적으로 검색되었지만 네트워크에서 또는 대상 리소스와 관련하여 발생하는 다른 작업에 대한 이해 없이는 다음으로 수행할 작업을 이해하기가 어렵습니다. 이를 방지하기 위해 보안 인시던트는 수집기에 도움을 줄 수 있는 아티팩트, 관련된 이벤트 및 정보를 포함할 수 있습니다. 추가 정보의 가용성은 검색된 위협의 종류 및 사용자 환경의 구성에 따라 달라지며 모든 보안 인시던트에 사용할 수 없습니다.

추가 정보를 사용할 수 있는 경우 경고 목록 아래의 보안 인시던트에 표시됩니다. 이는 다음과 같은 정보를 포함할 수 있습니다.

- 로그 지우기 이벤트
- 알 수 없는 장치에서 연결된 PNP 장치
- 실행 가능하지 않은 경고 

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>참고 항목
이 문서에서는 Security Center에서 발생하는 다양한 종류의 보안 경고에 대해 알아보았습니다. 보안 센터에 대한 자세한 내용은 다음을 참조하세요.

* [Azure Security Center에서 보안 인시던트 처리](security-center-incident.md)
* [Azure Security Center 감지 기능](security-center-detection-capabilities.md)
* [Azure Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)
* [Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/): Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
