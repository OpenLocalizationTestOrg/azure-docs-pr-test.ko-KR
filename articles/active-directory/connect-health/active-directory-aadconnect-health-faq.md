---
title: "Azure Active Directory 연결 상태 FAQ-aaaAzure | Microsoft Docs"
description: "이 FAQ는 Azure AD Connect Health에 대한 질문에 답변합니다. 이 FAQ에서는 청구 모델, 기능, 제한 사항 및 지원 hello를 포함 하 여 hello 서비스를 사용 하는 방법에 대 한 질문을 다룹니다."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Azure AD Connect Health에 대한 질문과 대답
이 문서는 질문과 대답 (Faq) (Azure AD) Azure Active Directory Connect Health에 대 한 답변 toofrequently 포함 되어 있습니다. 이 Faq toouse 청구 모델, 기능, 제한 사항 및 지원 hello를 포함 하는 서비스를 hello 하는 방법에 대 한 질문을 다룹니다.

## <a name="general-questions"></a>일반적인 질문
**Q: 여러 Azure AD 디렉터리를 관리합니다. Azure Active Directory Premium가 toohello 전환 어떻게 해야 하나요?**

tooswitch 서로 다른 Azure AD 테 넌 트에서, 선택 hello 현재 로그인 **사용자 이름** 오른쪽 위 모서리 hello 되 고 hello 적절 한 계정을 선택 합니다. Hello 계정 여기 나열 되지 않으면 경우 선택 **로그 아웃**, 한 후 Azure Active Directory Premium에는 hello 디렉터리의 hello 전역 관리자 자격 증명 사용에 toosign를 사용 합니다.

**Q: Azure AD Connect Health에서 어떤 버전의 ID 역할을 지원하나요?**

hello 다음 표에서 hello 역할 고 지원 되는 운영 체제 버전입니다.

|역할| 운영 체제/버전|
|--|--|
|AD FS(Active Directory Federation Services)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | 버전 1.0.9125 이상|
|AD DS(Active Directory Domain Services)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

참고 hello 서비스에서 제공 하는 hello 기능 다를 수 있습니다는 hello 역할과 hello 운영 체제를 기반으로 수행 합니다. 즉, 모든 hello 기능 모든 운영 체제 버전에 대 한 제공 되지 않을 수 있습니다. 자세한 내용은 hello 기능 설명을 참조 하십시오.

**Q: 라이선스 수 않는 내 인프라 toomonitor 필요 합니까?**

* hello 첫 번째 Connect Health Agent 하나 이상의 Azure AD Premium 라이선스가 필요합니다.
* 등록된 추가 에이전트에는 각각 25개의 추가 Azure AD Premium 라이선스가 필요합니다.
* 에이전트 수에는 모든 모니터링 대상 역할 (AD FS, Azure AD Connect 및/또는 AD DS) 등록 되어 있는 에이전트의 해당 toohello 총 수입니다.

Hello에서 라이선스 정보를 찾을 수 또한 [Azure AD 가격 책정 페이지](https://aka.ms/aadpricing)합니다.

예제:

| 등록된 에이전트 | 필요한 라이선스 | 모니터링 구성 예제 |
| ------ | --------------- | --- |
| 1 | 1 | Azure AD Connect 서버 1개 |
| 2 | 26| Azure AD Connect 서버 1개 및 도메인 컨트롤러 1개 |
| 3 | 51 | AD FS(Active Directory Federation Services) 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 1개 |
| 4 | 76 | AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개 |
| 5 | 101 | Azure AD Connect 서버 1개, AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개 |


## <a name="installation-questions"></a>설치 관련 질문

**Q: 개별 서버에 설치 하는 hello Azure AD Connect Health Agent의 hello 영향 란 무엇입니까?**

hello Microsoft Azure AD Connect Health Agent를 AD FS 웹 응용 프로그램 프록시 서버, Azure AD Connect (동기화) 서버, 도메인 컨트롤러 설치의 hello 영향 존중 toohello CPU, 메모리 사용, 네트워크 대역폭 및 저장소와 최소화 됩니다.

숫자 다음 hello는 근사값:

* CPU 사용량: 1-5% 증가
* 메모리 사용량: hello 전체 시스템 메모리 중 too10 %를 차지 합니다.

> [!NOTE]
> Hello 에이전트는 Azure와 통신할 수 없는, hello 에이전트 로컬로 정의 된 최대 한도 대 한 hello 데이터를 저장 합니다. hello 에이전트 hello "캐시 된" "서비스 least recently"에 따라 데이터를 덮어씁니다.
>
>

* Azure AD Connect Health 에이전트의 로컬 버퍼 저장소: ~20MB.
* AD FS 서버를 프로 비전 1, 024MB (1GB)의 디스크 공간에 대 한 Azure AD Connect Health Agent tooprocess hello AD FS 감사 채널에 대 한 모든 hello 감사 데이터는 덮어쓰기 전에 것이 좋습니다.

**Q: 해야 합니까 tooreboot 내 서버 hello hello Azure AD Connect Health Agent 설치 하는 동안?**

아니요. hello 에이전트의 hello 설치 tooreboot hello 서버를 요구 하지 않습니다. 하지만, 일부 필수 단계가 설치 hello 서버를 다시 부팅을 해야 합니다.

예를 들어 Windows Server 2008 R2에 .NET 4.5 Framework를 설치하는 경우 서버를 재부팅해야 합니다.

**Q: Azure AD Connect Health는 통과 HTTP 프록시를 통해 작동하나요?**

예. 진행 중인 작업에 대 한 hello Health Agent toouse는 HTTP 프록시 tooforward 아웃 바운드 HTTP 요청을 구성할 수 있습니다.
[Health 에이전트에 대한 HTTP 프록시 구성](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)을 자세히 읽어보세요.

에이전트 등록 하는 동안 프록시 tooconfigure 해야 할 경우 해야 toomodify Internet Explorer 프록시 설정을 미리 합니다.

1. Internet Explorer > **설정** > **인터넷 옵션** > **연결** > **LAN 설정**으로 이동합니다.
2. **사용자 LAN의 프록시 서버 사용**을 선택합니다.
3. HTTP 및 HTTPS/보안의 프록시 포트가 다른 경우 **고급**을 선택합니다.

**Q: tooHTTP 프록시를 연결할 때 Azure AD Connect Health 기본 인증을 지원 합니까?**

아니요. 메커니즘 toospecify 임의의 사용자 이름 및 기본 인증에 대 한 암호를 현재 지원 되지 않습니다.

**Q: 방화벽 포트 수행할 tooopen hello Azure AD Connect Health Agent toowork 필요 합니까?**

Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) hello 목록이 방화벽 포트 및 기타 연결 요구 사항에 대 한 합니다.

**Q: 두 서버 hello Azure AD Connect Health 포털에서 이름과 같은 이름을 hello로 나타나는 이유는 무엇입니까?**

서버에서 에이전트를 제거 하면 hello 서버 hello Azure AD Connect Health 포털에서 자동으로 제거 되지 않습니다. 수동으로 서버에서 에이전트를 제거 하거나 hello 서버 자체를 제거, toomanually hello Azure AD Connect Health 포털에서 hello 서버 항목 삭제 해야 합니다.

서버를 이미지로 다시 설치 하거나 동일한 정보 (예: 컴퓨터 이름) hello로 새 서버를 만들 수 있습니다. Hello로 두 개의 항목에 표시 될 수 hello Azure AD Connect Health 포털에서 hello 이미 등록 된 서버를 제거 하지 않은 새 서버 hello에 hello 에이전트를 설치 하는 경우 동일한 이름입니다.

Toohello 이전 버전의 서버에 속하는 hello 항목을이 경우 수동으로 삭제 합니다. 이 서버에 대 한 hello 데이터 만료 이어야 합니다.

## <a name="health-agent-registration-and-data-freshness"></a>Health Agent 등록 및 데이터 새로 고침

**Q: 정의 hello 상태 에이전트 등록 오류에 대 한 일반적인 이유 및 문제를 해결 하려면 어떻게 합니까?**

hello 상태 에이전트 못하는 toohello 다음 인해 tooregister 가능한 이유:

* 방화벽에서 트래픽이 차단 hello 에이전트 hello 필요한 끝점와 통신할 수 없습니다. 특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다. 아웃 바운드 통신 toohello 필요한 끝점 및 포트를 허용 하지 있는지 확인 합니다. Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) 대 한 자세한 내용은 합니다.
* 아웃 바운드 통신이 hello 네트워크 계층으로 발전 하 여 tooan SSL 검사 됩니다. 그러면 hello 인증서 hello 에이전트가 toobe hello 검사 서버/엔터티, 교체를 사용 하 고 hello 단계 toocomplete hello 에이전트 등록에 실패 합니다.
* hello 사용자 액세스 tooperform hello 등록 hello 에이전트의가 수 없습니다. 전역 관리자는 기본적으로 액세스 권한이 있습니다. 사용할 수 있습니다 [역할 기반 액세스 제어](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate 액세스 tooother 사용자입니다.

**Q: am 가져오는 경고를 발생 "상태 관리 서비스 데이터 아닌지 toodate를." Hello 문제를 해결 하려면 어떻게 해야 합니까?**

Azure AD Connect Health 수신 되지 않으면 모든 hello 데이터 요소 hello에 대 한 hello 서버에서 마지막 2 시간 hello 경고를 생성 합니다. 이 경고가 발생하는 여러 이유가 있을 수 있습니다.

* 방화벽에서 트래픽이 차단 hello 에이전트 hello 필요한 끝점와 통신할 수 없습니다. 특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다. 아웃 바운드 통신 toohello 필요한 끝점 및 포트를 허용 하지 있는지 확인 합니다. Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) 대 한 자세한 내용은 합니다.
* 아웃 바운드 통신이 hello 네트워크 계층으로 발전 하 여 tooan SSL 검사 됩니다. 그러면 hello 인증서 hello 에이전트가 toobe hello 검사 서버/엔터티, 교체를 사용 하 고 hello 프로세스 tooupload 데이터 toohello Azure AD Connect Health 서비스는 실패 합니다.
* Hello 에이전트에 기본 제공 되는 hello 연결 명령을 사용할 수 있습니다. [자세히 알아보기](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* 또한 hello 에이전트 인증 되지 않은 HTTP 프록시를 통해 아웃 바운드 연결을 지원합니다. [자세히 알아보기](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>작업 관련 질문
**Q: 웹 응용 프로그램 프록시 서버 hello에 대 한 감사 tooenable 필요 합니까?**

아니요, 감사 toobe hello 웹 응용 프로그램 프록시 서버에서 활성화 필요 하지 않습니다.

**Q: Azure AD Connect Health 경고는 어떻게 해결하나요?**

Azure AD Connect Health 경고는 성공 조건에서 해결됩니다. Azure AD Connect Health Agent 탐지 및 hello 성공 조건 toohello 서비스를 정기적으로 보고 합니다. 몇 가지 경고에 대 한 hello 억제 (suppression)은 시간 기반입니다. 즉, hello 동일한 오류가 발견 되지 않으면 경고 생성에서 72 시간 이내, hello 경고가 자동으로 해결 합니다.

**Q: am 가져오는 경고를 발생 시킬 "테스트 인증 요청 (가상 트랜잭션) 못했음을 tooobtain 토큰입니다." Hello 문제를 해결 하려면 어떻게 해야 합니까?**

AD FS에 대 한 azure AD Connect Health hello 상태 에이전트는 AD FS 서버에 설치 된 hello 상태 에이전트에 의해 시작 되는 가상 트랜잭션의 일부로 tooobtain 토큰을 실패 한 경우이 경고를 생성 합니다. hello Health agent hello 로컬 시스템 컨텍스트를 사용 하 고 자체 신뢰 당사자에 대 한 tooget 토큰을 시도 합니다. 이 AD FS 토큰을 발급의 상태에 있는 범용 테스트 tooensure입니다.

가장 자주 hello Health Agent는 없습니다 tooresolve hello AD FS 팜 이름 때문에이 테스트에 실패 합니다. 이 오류는 hello AD FS 서버는 네트워크 부하 분산 장치 뒤에 hello 요청이 가져옵니다 (부하 분산 장치 hello 앞에 있는 일반 클라이언트 것과 반대로 tooa)으로 hello 부하 분산 장치 뒤에 있는 노드에서 시작 하는 경우에 발생할 수 있습니다. 이 hello AD FS 팜 이름 (예: sts.contoso.com)에 대 한 hello "호스트"에 있는 파일에 "C:\Windows\System32\drivers\etc" hello AD FS 서버의 tooinclude hello IP 주소 또는 루프백 IP 주소 (127.0.0.1)를 업데이트 하 여 해결할 수 있습니다. Hello 호스트 파일을 추가 합니다 단락 (short-circuit) hello 네트워크 호출을 hello Health Agent tooget hello 토큰 수 있도록 합니다.

**Q: 내 컴퓨터 hello 최근 ransomeware 공격에 대 한 패치가 적용 되지 않은 표시 된 전자 메일을 수신 합니다. 이 전자 메일을 받은 이유는 무엇인가요?**

Azure AD Connect Health 서비스 tooensure hello 필요한 패치를 모니터링 하는 컴퓨터에 설치 된 모든 hello를 검색 합니다. 하나 이상의 컴퓨터에 중요 한 패치 hello 없는 hello 전자 메일 toohello 테 넌 트 관리자를 보냈습니다. 다음 논리 hello 사용된 toomake이이 결정 했습니다.
1. Hello 컴퓨터에 설치 된 모든 hello 핫픽스를 찾습니다.
2. 현재 인지 hello에서 핫픽스 hello 중 하나 이상 정의 목록을 확인 합니다.
3. 그렇다면 hello 컴퓨터 보호 됩니다. 그렇지 않은 경우 hello 컴퓨터 hello 공격에 대 한 위험에 노출 됩니다.

수동으로 진행할 수 있습니다 다음 PowerShell 스크립트 tooperform hello이이 검사 합니다. Hello 위에 논리를 구현합니다.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>관련 링크
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 에이전트 설치](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)
