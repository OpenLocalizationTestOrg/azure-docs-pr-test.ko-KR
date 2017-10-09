---
title: "Azure 보안 센터에서 유형별 aaaSecurity 경고 | Microsoft Docs"
description: "이 문서에서는 hello 다른 종류의 Azure 보안 센터에서 사용할 수 있는 보안 경고를 설명 합니다."
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
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Azure Security Center에서 보안 경고 이해
이 문서는 toounderstand hello 다양 한 유형의 보안 경고 및 Azure 보안 센터에서 사용할 수 있는 관련된 insights는 유용 합니다. Toomanage 알림 및 인시던트를 참조 하는 방법에 대 한 자세한 내용은 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.

> [!NOTE]
> tooset 고급 검색을 업그레이드 tooAzure 보안 센터 표준입니다. 무료 60일 평가판을 사용할 수 있습니다. tooupgrade, **가격 책정 계층** hello에 [보안 정책](security-center-policies.md)합니다. toolearn hello을 더 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/security-center/)합니다.
>

## <a name="what-type-of-alerts-are-available"></a>어떤 유형의 경고를 사용할 수 있습니까?
Azure 보안 센터의 다양 한 사용 하 여 [검색 기능이](security-center-detection-capabilities.md) tooalert 고객 toopotential 공격 환경을 대상으로 지정 합니다. 이러한 경고 hello 알림을 hello 리소스, 대상 및 소스 hello 공격의 hello 트리거된 항목 hello에 대 한 중요 한 정보를 포함 합니다. 경고에 포함 된 hello 정보 사용 분석 toodetect hello 위협 hello 유형에 따라 달라 집니다. 인시던트는 위협을 조사할 때 유용할 수 있는 추가 컨텍스트 정보를 포함할 수도 있습니다.  이 문서는 경고 유형에 따라 hello에 대 한 정보를 제공 합니다.

* VMBA(가상 컴퓨터 동작 분석)
* 네트워크 분석
* 리소스 분석
* 컨텍스트 정보

## <a name="virtual-machine-behavioral-analysis"></a>VMBA(가상 컴퓨터 동작 분석)
Azure 보안 센터의 가상 컴퓨터 이벤트 로그 분석에 따라 동작 분석 손상 tooidentify 리소스를 사용할 수 있습니다. 예를 들어 프로세스 만들기 이벤트 및 로그인 이벤트가 있습니다. 또한 광범위 한 캠페인의 증거를 지원 하기 위한 다른 신호 toocheck와의 상관 관계는 합니다.

> [!NOTE]
> Security Center 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참조하세요.
>

### <a name="crash-analysis"></a>충돌 분석
크래시 덤프 메모리 분석을 사용 하는 방법 toodetect 정교한 맬웨어 수 tooevade 기존 보안 솔루션입니다. 다양 한 형태의 맬웨어 tooreduce hello 가능성이 되지 toodisk를 작성 하 여 또는 toodisk 작성 하는 소프트웨어 구성 요소를 암호화 하 여 바이러스 백신 제품에서 검색 하는 시도 합니다. 따라서 기존 맬웨어 방지 접근 방식을 사용 하 여 hello 맬웨어 어려운 toodetect 있습니다. 그러나 이러한 종류의 맬웨어 맬웨어 순서 toofunction 메모리에 추적을 유지 해야 하기 때문에 메모리 분석을 사용 하 여 검색할 수 있습니다.

소프트웨어 충돌, 크래시 덤프는 hello 충돌 hello 시 메모리의 일부를 캡처합니다. hello 크래시 맬웨어, 일반 응용 프로그램 또는 시스템 문제로 인해 발생할 수 있습니다. Hello 크래시 덤프의 hello 메모리를 분석 하 여 보안 센터 수 tooexploit 취약점 소프트웨어에서 사용 하는 기술을 검색, 기밀 데이터를 액세스 및 부정적 손상 된 컴퓨터 내에서 유지 합니다. 이 hello 분석은 보안 센터 다시 종료 hello 수행한 것으로 최소 성능 영향 toohosts 수행 됩니다.

다음 필드는 hello은 일반적인 toohello 크래시 덤프 경고 예가이 문서의 뒷부분에 나오는 나타나는:

* Hello 크래시 덤프 파일의 덤프 파일: 이름입니다.
* Hello 충돌 프로세스의 PROCESSNAME: 이름입니다.
* 프로세스 충돌 하는 hello의 PROCESSVERSION: 버전입니다.

### <a name="shellcode-discovered"></a>Shellcode 검색
Shellcode는 소프트웨어 취약점을 악용 하는 맬웨어 후 실행 되는 hello 페이로드입니다. 이 경고는 크래시 덤프 분석이 악의적인 페이로드에서 일반적으로 수행되는 동작을 표시하는 실행 코드를 감지했음을 나타냅니다. 악의적이지 않은 소프트웨어가 이 동작을 수행할 수 있지만 보통 소프트웨어 개발 방법으로서는 일반적이지 않습니다.

hello Shellcode 경고 예 hello를 다음 추가 필드를 제공 합니다.

* Hello shellcode의 메모리 주소: hello 위치입니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![Shellcode 경고](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>모듈 하이재킹 검색
Windows 동적 연결 라이브러리 (Dll) tooallow 소프트웨어 tooutilize 공통 Windows 시스템 기능을 사용합니다. DLL 하이재킹 변경 될 때 발생 맬웨어 hello DLL 로드 순서 tooload 악의적인 페이로드 메모리에 임의의 코드를 실행할 수 있습니다. 이 경고 hello 크래시 덤프를 분석 두 개의 서로 다른 경로에서 로드 된 유사한 이름의 모듈 있음을 나타냅니다. 로드 하는 hello 패스 중 하나의 공통 Windows 시스템 이진 위치에서 제공 됩니다.

소프트웨어의 합법적인 개발자는 가끔 계측, 확장 hello Windows 운영 체제 또는 Windows 응용 프로그램을 확장 하는 등의 악의적인 내용이 이유로 hello DLL 로드 순서를 변경 합니다. toohelp 취급 악의적인 및 잠재적으로 심각 하지 않은 변경 내용 toohello DLL 로드 순서, Azure 보안 센터 로드 된 모듈 tooa 의심 스러운 프로필 준수 여부를 확인 합니다. 이 검사의 결과 hello hello 경고의 hello "서명" 필드에 따라 표시 되 고 hello 심각도 hello 경고, 경고 설명 및 경고 문제 해결 단계에 반영 됩니다. tooresearch 올 바르 거 나 악성 hello 모듈 인지 모듈을 하이재킹 하는 hello의 디스크 복사본에 대해 hello를 분석 합니다. 예를 들어 바이러스 검사를 실행 하거나 hello 파일의 디지털 서명을 확인할 수 있습니다.

또한 hello 이전 "Shellcode 검색" 섹션에 설명 된 공통 필드 toohello이이 경고 필드를 다음 hello 제공:

* 서명: 모듈을 하이재킹 하는 hello tooa 의심 스러운 동작 프로필을 준수 하는 경우를 나타냅니다.
* HIJACKEDMODULE: hello의 hello 이름을 하이재킹 Windows 시스템 모듈입니다.
* HIJACKEDMODULEPATH: hello의 hello 경로 Windows 시스템 모듈을 하이재킹입니다.
* Hello 하이재킹 모듈의 HIJACKINGMODULEPATH: hello 경로입니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![모듈 하이재킹 경고](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>위장 Windows 모듈 감지
맬웨어는 Windows 시스템 이진 파일 (예를 들어 다음과 같이 SVCHOST의 일반 이름을 사용할 수 있습니다. EXE) 또는 모듈 (예를 들어 NTDLL 합니다. DLL) 너무*조화* 및 시스템 관리자에 게 hello 악성 소프트웨어의 hello 특성을 모호 합니다. 이 경고는 hello 크래시 덤프를 분석이 해당 hello 크래시 덤프 파일에 Windows 시스템 모듈 이름을 사용 하지만 Windows 모듈의 일반적인 하는 다른 조건을 충족 하지 않는 모듈이 감지 했음을 나타냅니다. 디스크 복사본을 hello 가상 모듈 분석 hello이이 모듈의 hello 올 바르 거 나 악성 특성에 대 한 자세한 정보를 제공할 수 있습니다. 분석은 다음을 포함할 수 있습니다.

* 소프트웨어의 합법적인 패키지의 일부로 제공 되는 hello 해당 파일에 확인 합니다.
* Hello 파일의 디지털 서명을 확인 합니다.
* Hello 파일에 대해 바이러스 검사를 실행 합니다.

또한 toohello 공통 필드 hello "Shellcode 검색" 섹션의 앞부분에서 설명한이 경고는 hello 추가 필드를 다음을 제공:

* 세부 정보: hello 모듈의 메타 데이터가 유효 하 고 hello 모듈이 시스템 경로에서 로드 되는 여부를 설명 합니다.
* 이름: hello hello 가상 Windows 모듈의 이름입니다.
* 경로: hello 경로 toohello 가상 Windows 모듈입니다.

이 경고 또한 추출 하 고 "CHECKSUM" 및 "TIMESTAMP"와 같은 hello 모듈의 PE 헤더에서 특정 필드를 표시 합니다. 이러한 필드는 hello 필드 hello 모듈에 있는 경우에 표시 됩니다. Hello 참조 [Microsoft PE 및 COFF 사양](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) 이러한 필드에 대 한 자세한 내용은 합니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![가상 Windows 경고](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>수정된 시스템 이진 파일 검색
맬웨어 순서 toocovertly 데이터 액세스에서에서 핵심 시스템 이진 파일을 수정 또는 부정적 손상된 된 시스템에 유지 될 수 있습니다. 이 경고 메모리 나 디스크에 핵심 Windows OS 바이너리 수정 된 hello 크래시 덤프를 분석에 검색을 나타냅니다.

때때로 합법적인 소프트웨어 개발자는 Detours 등 응용 프로그램 호환성을 위해 악의적이지 않은 이유로 메모리에서 자유롭게 시스템 모듈을 수정합니다. toohelp 취급 악의적인 및 잠재적으로 합법적인 모듈, Azure 보안 센터 hello 수정 된 모듈 tooa 의심 스러운 프로필 준수 여부를 확인 합니다. 이 검사의 결과 hello hello 심각도 hello 경고, 경고 설명 및 경고 업데이트 관리 단계가 표시 됩니다.

또한 toohello 공통 필드 hello "Shellcode 검색" 섹션의 앞부분에서 설명한이 경고는 hello 추가 필드를 다음을 제공:

* MODULENAME: hello의 이름을 시스템 바이너리를 수정 합니다.
* MODULEVERSION: 버전의 hello 시스템 바이너리를 수정 합니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![시스템 이진 경고](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>의심스러운 프로세스 실행
보안 센터 hello 대상 가상 컴퓨터에서 실행 되 고 다음 경고를 트리거하는 의심 스러운 프로세스를 식별 합니다. hello 검색 hello 특정 이름에 대 한 व ै 있지만 hello 실행 파일의 매개 변수를 찾고지 않습니다. 따라서 hello 공격자가 hello 실행 파일 이름을 바꾸거나, 경우에 보안 센터 hello 의심 스러운 프로세스를 계속 검색할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![의심스러운 프로세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>여러 도메인 계정 쿼리
보안 센터 여러 tooquery Active Directory 도메인 계정에이 시도 감지할 수 공격자가 네트워크 검사 하는 동안 일반적으로 수행 합니다. 공격자가이 기술은 tooquery hello 도메인 tooidentify hello 사용자 활용 하 여, hello 도메인 관리자 계정을 식별, hello 컴퓨터를 확인 하는 도메인 컨트롤러와도 다른 도메인과 hello 잠재적 도메인 트러스트 관계를 파악할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![여러 도메인 계정 경고](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>로컬 관리자 그룹 구성원이 열거됨

Windows Server 2016 및 Windows 10의 보안 이벤트 hello 4798, 하나의 트리거되는 경우 보안 센터 tootrigger 경고 하려고 합니다. 로컬 관리자 그룹이 열거될 때 발생하며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다. 공격자는이 기술을 tooquery hello 관리 권한 가진 사용자의 id를 활용할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![로컬 관리자](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>대/소문자의 비정상적인 혼합

보안 센터 대문자 및 소문자 hello 명령줄에서는 hello 사용 감지 되 면 경고가 트리거됩니다. 해시 기반 컴퓨터 규칙 또는 일부 공격자가에서 대/소문자 구분이 기술은 toohide를 사용할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![비정상적인 혼합](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>의심스러운 Kerberos Golden Ticket 공격

공격에 노출 된 [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) 공격자가 toocreate Kerberos "골든 티켓," hello 공격자가 tooimpersonate 하려는 모든 사용자 허용 하 여 키를 사용할 수 있습니다. 보안 센터 이러한 유형의 활동을 감지 하면 경고 tootrigger를 하려고 합니다.

> [!NOTE] 
> Kerberos Golden Ticket에 대한 자세한 내용은 [Windows 10 자격 증명 도난 방지 가이드](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)(영문)를 참조하세요.

이러한 유형의 경고 예제는 다음과 같습니다.

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>의심스러운 계정 생성

Security Center는 기존의 기본 제공 관리 권한 계정과 매우 유사한 계정을 만들 때 경고를 트리거합니다. 이 기술은 공격자가 toocreate 악의적 tooavoid 휴먼 확인 하 여 알림 메시지를 고려 하 여 사용할 수 있습니다.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![의심스러운 계정](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>의심스러운 방화벽 규칙 생성됨

공격자가 명령 및 컨트롤을 사용 하 여 사용자 지정 방화벽 규칙 tooallow 악성 응용 프로그램이 toocommunicate 만들어 toocircumvent 호스트 보안 보십시오 또는 hello 통해 hello 네트워크를 통해 toolaunch 공격 손상 호스트 합니다. Security Center는 의심스러운 위치의 실행 파일에서 새 방화벽 규칙이 생성된 것을 감지하면 경고를 트리거합니다.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![방화벽 규칙](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>HTA 및 PowerShell의 의심스러운 조합

Security Center는 Microsoft HTML Application Host(HTA)에서 PowerShell 명령이 실행되는 것을 감지하면 경고를 트리거합니다. 이 공격자가 toolaunch 악의적인 PowerShell 스크립트에서 사용 하는 방법.
 
이러한 유형의 경고 예제는 다음과 같습니다.

![HTA 및 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>네트워크 분석
Security Center 네트워크 위협 감지는 Azure IPFIX(인터넷 프로토콜 흐름 정보 내보내기)에서 보안 정보를 자동으로 수집하여 작동합니다. 이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다.

### <a name="suspicious-outgoing-traffic-detected"></a>의심스러운 나가는 트래픽 감지
네트워크 장치 검색 및 많은 hello에서 프로 파일링 수 동일한 방식으로 다른 유형의 시스템. 공격자는 일반적으로 포트 검색 또는 포트 비우기를 시작합니다. Hello 다음 예제에서는 의심 스러운 SSH (보안 셸) 트래픽을 VM에서 사용할 수 있습니다. 이 시나리오에서는 외부 리소스에 대한 SSH 무작위 공격 또는 포트 비우기 공격이 가능합니다.

![의심스러운 나가는 트래픽 경고](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

이 경고는 사용할 수 있는 tooidentify hello 리소스의 사용된 tooinitiate이이 공격 하는 정보를 제공 합니다. 이 경고는 또한 tooidentify hello 손상 컴퓨터, hello 검색 시간 및 hello 프로토콜 및 포트에 사용 된 정보를 제공 합니다. 이 블레이드 또한 있습니다 수 있는 수정 단계 목록을 사용 하는 toomitigate이이 문제가 발생할 수 있습니다.

### <a name="network-communication-with-a-malicious-machine"></a>악의적인 컴퓨터와 네트워크 통신
Azure Security Center는 Microsoft 위협 인텔리전스 피드를 활용하여 악성 IP 주소와 통신하는 손상된 컴퓨터를 검색할 수 있습니다. 대부분의 경우에서 hello 악의적인 주소가 명령 및 제어 센터 없습니다. 이 경우 보안 센터 감지 hello 통신 조랑말 로더 맬웨어를 사용 하 여 수행 된 (라고도 [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![네트워크 통신 경고](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

이 경고를 사용 하는 tooinitiate tooidentify hello 리소스를 사용할 수 있는 정보를이 공격 제공, 리소스, hello 희생자 IP, hello 공격자가 IP 및 hello 검색 시간 hello 공격입니다.

> [!NOTE]
> 라이브 IP 주소는 개인 정보 보호 목적을 위해 이 스크린샷에서 제거되었습니다.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>가능한 발신 서비스 거부 공격 감지
하나의 가상 컴퓨터에서 시작 된 비정상적인 네트워크 트래픽 보안 센터 tootrigger는 잠재적 서비스 거부 유형의 공격 발생할 수 있습니다.

이러한 유형의 경고 예제는 다음과 같습니다.

![발신 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>리소스 분석
보안 센터 리소스 분석에 중점을 두고 플랫폼 hello로 hello 통합 같은 서비스 (PaaS) 서비스로 [Azure SQL 데이터베이스 위협 검색](../sql-database/sql-database-threat-detection.md) 기능입니다. 이러한 영역의 hello 분석 결과에 따라 보안 센터 리소스 관련 경고를 트리거합니다.

### <a name="potential-sql-injection"></a>잠재적인 SQL 삽입
SQL 삽입은 악성 코드가 구문 분석 및 실행에 대 한 SQL Server 인스턴스의 tooan 나중 전달 되는 문자열은 삽입 공격입니다. SQL Server가 수신하는 모든 구문상 유효한 쿼리를 실행하기 때문에 SQL 문을 생성하는 모든 프로시저에 삽입 취약성이 있는지 검토해야 합니다. 기계 학습, 동작 분석 및 비정상 탐지 toodetermine 의심 스러운 이벤트 Azure SQL 데이터베이스의 현재 위치를 차지 하는 SQL 위협 검색을 사용 하 여 합니다. 예:

* 이전 직원이 데이터베이스 액세스 시도
* SQL 삽입 공격
* 집에서 사용자 로부터 비정상적인 액세스 tooa 프로덕션 데이터베이스

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

이 경고의 hello 정보는 사용 되는 tooidentify 공격 hello 리소스, hello 검색 시간 및 hello 상태 hello 공격을 받을 수 있습니다. 링크 toofurther 조사 단계도 제공합니다.

### <a name="vulnerability-toosql-injection"></a>취약점 tooSQL 삽입
데이터베이스에서 응용 프로그램 오류가 검색될 때 이 경고가 트리거됩니다. 이 경고는 취약해 지지 tooSQL 주입 공격을 나타낼 수 있습니다.

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>알 수 없는 위치에서 비정상적인 액세스
이 경고는 액세스 이벤트 생소 한 IP 주소를 찾을 수 없으며 hello에서 마지막 기간은 hello 서버에서 검색 되었을 때 트리거됩니다.

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>컨텍스트 정보
한 조사 하는 동안 분석가 할 추가 컨텍스트 tooreach hello 위협의 hello 특성에 대 한 한 결과 방법을 toomitigate 것입니다.  예를 들어 네트워크 변칙 검색 되었지만 이해 하지 못하면 다른 일어나는 hello 네트워크 또는 관계의 대상 toohello 리소스와 그 다음 모든 하드 toounderstand 어떤 작업 tootake 됩니다. 와 tooaid, 보안 문제가 발생 한 아티팩트, 관련된 이벤트 및 hello 에이전트용 유용한 정보를 포함할 수 있습니다. hello 추가 정보의 가용성에 따라 달라 집니다 위협이 검색 유형의 hello 및 hello 사용자 환경의 구성 되 고 모든 보안 문제에 대해 제공 됩니다.

추가 정보를 사용할 수 있는 경우 경고의 hello 목록 아래의 hello 보안 사고에에서 표시 됩니다. 이는 다음과 같은 정보를 포함할 수 있습니다.

- 로그 지우기 이벤트
- 알 수 없는 장치에서 연결된 PNP 장치
- 실행 가능하지 않은 경고 

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>참고 항목
이 문서에서는 서로 다른 유형의 보안 센터에서 보안 경고를 hello에 대 한 알아보았습니다. 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure Security Center에서 보안 인시던트 처리](security-center-incident.md)
* [Azure Security Center 감지 기능](security-center-detection-capabilities.md)
* [Azure Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)
* [Azure 보안 센터 FAQ](security-center-faq.md): 찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/): Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
