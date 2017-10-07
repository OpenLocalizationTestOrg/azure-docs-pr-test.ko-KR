---
title: "aaaCloud App Discovery 보안 및 개인 정보 고려 사항 | Microsoft Docs"
description: "이 항목에서는 hello 보안 및 개인 정보 고려 사항 관련된 tooCloud App Discovery에 설명 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>클라우드 앱 보안 및 개인정보 취급 방침 고려 사항
Microsoft는 커밋된 tooprotecting 개인 정보 데이터, 소프트웨어 및 서비스를 제공 하는 동안 유용한 정보와 hello 조직의 보안을 관리할 수 있습니다.  
데이터 tooothers 맡길 때 해당 신뢰 필요 함을 상당한 보안 엔지니어링 투자 및 전문 지식 tooback 것입니다.
Microsoft 보안 소프트웨어 개발 수명 주기 사례 toooperating 서비스에서에서 toostrict 규정 준수 및 보안 지침을 따릅니다.  
데이터 보안 및 보호는 Microsoft의 최우선 과제입니다.

이 항목에서는 Azure Active Directory 클라우드 앱 검색 내에서 데이터 수집, 처리 및 보안 방법에 대해 설명합니다.

## <a name="overview"></a>개요
클라우드 앱 검색은 Azure AD의 기능이며 Microsoft Azure에서 호스트됩니다.  
hello Cloud App Discovery endpoint agent는 IT 관리 컴퓨터에서 사용 되는 toocollect 응용 프로그램 검색 데이터입니다.  
hello 수집 데이터는 전송 안전 하 게 암호화 된 채널 toohello Azure AD Cloud App Discovery 서비스를 통해 합니다.  
그런 다음 hello 조직에 대 한 Cloud App Discovery 데이터 hello Azure 포털에에서 표시 됩니다. 

![클라우드 앱 검색 작동 방법](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

hello 다음 섹션에서는 정보의 흐름 hello 따르고 조직 toohello Cloud App Discovery 서비스 및 궁극적으로 toohello Cloud App Discovery 포털로에서 이동할 때 데이터 보호 방식에 대해 설명 합니다.

## <a name="collecting-data-from-your-organization"></a>조직에서 데이터 수집
Toofirst 해야 순서 toouse Azure Active Directory의 클라우드 앱 검색 기능 tooget insights 조직의 직원이 사용 하는 hello 응용 프로그램으로, hello Azure AD Cloud App Discovery 끝점 에이전트 toomachines 조직에 배포 합니다.

Hello Azure Active Directory 테 넌 트 (또는 해당 대리자)의 관리자 hello Azure 포털에서에서 hello 에이전트 설치 패키지를 다운로드할 수 있습니다. hello 에이전트 수 수동으로 설치 하거나 SCCM 또는 그룹 정책을 사용 하 여 hello 조직에서 여러 컴퓨터에서 설치 합니다.

배포 옵션에 대한 자세한 지침은 [클라우드 앱 검색 그룹 정책 배포 가이드](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)를 참조하십시오.


### <a name="data-collected-by-hello-agent"></a>Hello 에이전트에 의해 수집 된 데이터
hello 목록 아래에 설명 된 hello 정보는 연결 tooa 웹 응용 프로그램을 만들 때 hello 에이전트에 의해 수집 됩니다. hello만 수집 되는 해당 응용 프로그램 관리자에 게 해당 검색에 대 한 구성 했습니다.  
Hello Microsoft Cloud App Discovery 블레이드 hello 통해 에이전트를 모니터링 hello 하는 클라우드 응용 프로그램의 hello 목록을 편집할 수 있습니다 [Azure 포털](https://portal.azure.com/)아래 **설정**->**데이터 컬렉션**->**앱 컬렉션 목록**합니다. 자세한 내용은 [클라우드 앱 검색 시작](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**정보 범주**: 사용자 정보  
**설명**:  
요청 toohello 대상 웹 응용 프로그램을 만든 hello 프로세스의 hello Windows 사용자 이름 (예:: 도메인 \ 사용자 이름) hello hello 사용자의 Windows 보안 식별자 (SID) 뿐 아니라 합니다.

**정보 범주**: 프로세스 정보  
**설명**:  
hello 요청 toohello 대상 웹 응용 프로그램을 만든 hello 프로세스의 hello 이름 (예:: "iexplore.exe")

**정보 범주**: 컴퓨터 정보  
**설명**:  
에이전트가 설치 된 어떤 hello hello 컴퓨터 NetBIOS 이름입니다.

**정보 범주**: 앱 트래픽 정보  
**설명**: 

다음 연결 정보는 hello:

* hello 원본 (로컬 컴퓨터) 및 대상 IP 주소와 포트 번호
* hello 공용 IP 주소는 hello를 통해 요청 외부로 이동 하는 hello 조직입니다.
* hello hello 요청 시간
* 보내고 받은 트래픽의 hello 볼륨
* hello IP 버전 (4 또는 6)
* TLS 연결에: hello 서버 이름 표시 확장 또는 hello 서버 인증서 hello 대상 호스트 이름입니다.

다음 HTTP 정보 hello:

* 메서드(GET, POST 등)
* 프로토콜(HTTP/1.1 등).
* 사용자 에이전트 문자열
* 호스트 이름
* 대상 URI (쿼리 문자열 제외)
* 콘텐츠 형식 정보
* 참조 페이지 URL 정보(쿼리 문자열 제외)

> [!NOTE]
> hello 위의 HTTP 정보는 암호화 되지 않은 모든 연결에 대해 수집 됩니다.
> 이 정보가 TLS 연결에 대 한 hello 포털에서 hello ' 자세한 검사 ' 설정이 켜져 있을 때만 캡처됩니다. hello 설정은 기본적으로 'ON'입니다.
> 자세한 내용은 아래 내용과 [클라우드 앱 검색 시작](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

또한 toohello hello 에이전트에 수집 하는 데이터 hello 네트워크 활동에 대 한, 또한 hello 소프트웨어 및 하드웨어 구성, 오류 보고서 및 hello 에이전트의 사용 방법에 대 한 정보에 대 한 익명 정보를 수집 합니다.


### <a name="how-hello-agent-works"></a>Hello 에이전트의 작동 원리
hello 에이전트 설치는 두 가지 구성 요소가 포함 되어 있습니다.

* 사용자 모드 구성 요소
* 커널 모드 드라이버 구성 요소(Windows 필터링 플랫폼 드라이버)

컴퓨터별 신뢰할 수 있는 인증서를 저장 hello 에이전트를 처음 설치 하는 경우 hello 컴퓨터에 있는 다음 사용 하 여 보안 연결 tooestablish hello Cloud App Discovery 서비스와 합니다.  
hello 에이전트 정책 구성 hello Cloud App Discovery 서비스에서에서이 보안 연결을 통해 정기적으로 검색합니다.  
hello 정책에는 클라우드 응용 프로그램 toomonitor에 대 한 정보 및 여부 자동 업데이트를 사용 하도록 무엇 보다도 포함 됩니다.

웹 트래픽을 전달 하 고 Internet Explorer 및 Chrome에서 hello 컴퓨터에 수신 하는 대로 hello Cloud App Discovery 에이전트 hello 트래픽을 분석 하 고 추출 hello 관련 메타 데이터 (참조 hello **hello 에이전트에서 데이터 수집** 섹션 위).  
1 분 마다 hello 에이전트 암호화 된 채널을 통해 메타 데이터 toohello hello 수집 Cloud App Discovery 서비스에 업로드합니다.

암호화 된 트래픽을 hello hello 암호화 된 스트림으로 자체를 삽입 하는 hello 드라이버 구성 요소 절편입니다. Hello에 대 한 자세한 내용은 **암호화 된 연결 (자세한 검사)에서 데이터를 가로채** 아래 섹션.

### <a name="respecting-user-privacy"></a>사용자 개인정보 존중
목표는 tooprovide 관리자 hello 도구 tooset hello 간의 균형 조직에 맞게 응용 프로그램 사용 현황 및 사용자 개인 정보에 대 한 자세한 표시 합니다. 노브 hello hello 포털 설정 페이지에서 다음 hello 제공 toothat 끝:

* **데이터 수집**: 관리자는 응용 프로그램 또는 응용 프로그램 범주 tooget 검색 데이터에서 원하는 toospecify를 선택할 수 있습니다.
* **자세한 검사**: hello 에이전트가 SSL/TLS 연결에 대 한 HTTP 트래픽을 수집할지 하는 경우 관리자 toospecify를 선택할 수 (즉, **' 자세한 검사 '**). 이 hello 다음 섹션에서 자세히 살펴보겠습니다.
* **옵션 동의**: 여부 관리자 hello Cloud App Discovery 포털 toochoose 사용 하 여 hello 에이전트를 사용 하 여 hello 데이터 컬렉션의 toonotify 사용자 toorequire 사용자 hello 에이전트 사용자 데이터 수집을 시작 하기 전에 동의 여부와 합니다.

hello Cloud App Discovery 끝점 에이전트만 ַ ׁ ֱ hello hello에 설명 된 **hello 에이전트에서 데이터 수집** 위의 섹션.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>암호화된 연결에서 데이터 가로채기(자세히 검사)
에서 설명한 것 처럼 관리자 hello 에이전트 toomonitor 데이터 암호화 된 연결 ('자세한 검사')를에서 구성할 수 있습니다. TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) 중 하나입니다. hello hello 인터넷에서 사용에서 하는 가장 일반적인 프로토콜 오늘 합니다. 클라이언트 수는 웹 서버;와 안전 하 고 개인 통신 채널을 설정 하는 데 TLS와의 통신을 암호화 하 여 TLS 인증 자격 증명을 전달 하기 위한 필수 보호 기능을 제공 하 고 중요 한 정보의 hello 공개 되지 않도록 합니다.

Hello 종단 간 보안 암호화 된 채널에서 TLS 제공을 통해 중요 한 보안 및 개인 정보 보호, 동안 hello 프로토콜은 악의적 이거나 악의적인 목적 악용 되기도 합니다. 따라서 훨씬 "프로토콜 유니버설 방화벽 바이패스" tooas hello 참조 TLS 종종는 실제로 합니다. hello 문제의 hello 루트 그는 대부분의 방화벽 없습니다 tooinspect TLS 통신 하므로 hello 응용 프로그램 계층 데이터는 SSL로 암호화 됩니다. 이 알고 있으면 공격자가 자주 활용 하 여 TLS toodeliver 악의적인 페이로드 tooa 사용자도 hello 가장 지능형 응용 프로그램 계층 방화벽은 완전히 시력 tooTLS 값과 호스트 간의 TLS 통신을 릴레이 단순히 해야 합니다. 최종 사용자가 자신의 회사 방화벽 및 프록시 서버를 tooconnect toopublic 프록시를 사용 하 여 및 터널링 정책에 의해 차단 될 수 있습니다 hello 방화벽을 통해-TLS 프로토콜에 대 한 강제 적용 하는 TLS toobypass 액세스 제어를 자주 활용 합니다.

자세한 검사는 신뢰할 수 있는 중간자-에-개입으로 hello Cloud App Discovery 에이전트 tooact을 수 있습니다. 클라이언트 요청이 만들어질 때 HTTPS tooaccess 보호 된 리소스, hello 끝점 에이전트 드라이버 hello 연결을 차단 하 고 새 연결 toohello 대상 서버 tooretrieves hello 클라이언트를 대신해 서 해당 SSL 인증서를 설정 합니다. hello 인증서 수를 신뢰 (것가 해지 되었는지 여부를 확인 하 고 다른 인증서 검사를 수행), 및 전달 이러한 hello Endpoint Agent 다음 hello 정보에서에서 복사 hello 서버 인증서를 자체 만듭니다 hello 에이전트 확인 합니다. 서버 인증서-해당 정보를 사용 하는 인터 셉 션 인증서-라고 합니다. hello 인터 셉 션 인증서는 서명 된에 즉시 hello Windows 신뢰할 수 있는 인증서 저장소에 설치 된 루트 인증서로 hello 끝점 에이전트에 의해입니다. 이 자체 서명 된 루트 인증서는 내보낼 수 없는 표시 되어 있으며 ACL tooadministrators 했습니다. 포함 된 의도 한 toonever leave hello 컴퓨터 작성 된 합니다. Hello 최종 사용자의 클라이언트 응용 프로그램 hello 인터 셉 션 인증서를 받으면 것의 유효성을 검사 hello 인증서 체인 모든 hello 방식으로 toohello 루트 인증서 때문에 그 신뢰할 수 있습니다. 이 프로세스는 주로 최종 사용자의 관점에서 아래에 설명된 몇 가지 주의 사항을 명확히 밝힙니다.

자세히 검사를 사용 하 여 hello Cloud App Discovery Endpoint Agent 수 암호를 해독 하 고 hello 서비스 tooreduce 노이즈를 허용 하는 TLS 암호화 통신을 검사 및 암호화 hello 클라우드 응용 프로그램의 hello 사용에 대 한 통찰력을 제공 합니다.

#### <a name="a-word-of-caution"></a>주의 사항
자세히 검사를 설정 하기 전에 것이 좋습니다 의도 tooyour 법률 및 인사 부서를 전달할의 동의 구하는 하 합니다. 최종 사용자의 개인 암호화 통신을 검사하는 것은 분명히 민감한 사인일 수 있습니다. 전에 프로덕션 롤아웃 자세한 검사 확인 하면 회사 보안 및 사용 제한 정책이 업데이트 되었습니다. 암호화 된 통신 tooindicate 검사 합니다. 사용자 알림 및 중요 사이트 (예: 은행 및 의료 보험 사이트)의 예외 해야 할 수도 있습니다 Cloud App Discovery toomonitor를 구성 하는 경우 해당 합니다. 위에서 설명 했 듯이 관리자 사용 하 여 hello Cloud App Discovery 포털 toochoose 여부 hello 에이전트를 사용 하 여 hello 데이터 컬렉션의 toonotify 사용자 toorequire 사용자 hello 에이전트 사용자 데이터 수집을 시작 하기 전에 동의 여부와 합니다.

### <a name="known-issues-and-drawbacks"></a>알려진 문제 및 단점
TLS 인터 셉 션 hello 최종 사용자 환경 영향을 줄 수는 있는 경우도 있습니다.

* 확장된 유효성 검사 (EV) 인증서는 신뢰할 수 있는 웹 사이트를 방문 하는 스위치 hello 웹 브라우저 녹색 tooact의 hello 주소 표시줄을 렌더링 합니다. TLS 검사 EV 인증서를 사용 하는 웹 사이트는 정상적으로 동작 하므로 toohello 클라이언트 발급 hello 인증서에 EV 달라 야 하지만 hello 주소 표시줄에 녹색 표시 되지 않습니다.  
* 디자인 된 공용 키 고정 (고정 인증서도 함) toohelp 사용자가 중간자 개입 공격 으로부터 보호 하 고 인증 기관 rogue 합니다. 고정 된 사이트에 대 한 hello 루트 인증서와 일치 하는 알려진 좋은 CA의 hello이 없으면 hello 브라우저 오류가 발생 하 여 hello 연결을 거부 합니다. 실제로 TLS 가로채기는 메시지 가로채기(man-in-the-middle) 공격이므로 이러한 연결은 실패합니다.
* 사용자가 hello 자물쇠 아이콘이 hello 브라우저 주소 표시줄 브라우저 tooinspect hello 사이트 정보를 클릭 하는 경우 었 표시 되지 않습니다 toosign hello 웹 사이트 인증서를 사용 하는 hello 인증서 기관에서 종료 체인 있지만 인증서 체인으로 끝나는 Windows hello 하는 대신 신뢰할 수 있는 인증서 저장소입니다.

이러한 문제의 tooreduce hello 발생에서는 추적 클라우드 서비스 및 toouse 알려진 클라이언트 응용 프로그램 확장 유효성 검사 또는 공개 키를 고정 하 고 영향을 받는 연결을 차단 하는 hello Endpoint Agent tooavoid을 지시 합니다. 이 경우에도 이러한 클라우드 응용 프로그램의 hello 사용 및 전송 되는 데이터의 hello 볼륨 보고서 받아 볼 수 있습니다 하지만 hello 앱 사용 된 방법에 대 한 세부 정보가 없습니다 가능 하지 않으므로 전체 검사 합니다.

## <a name="sending-data-toocloud-app-discovery"></a>보내는 데이터 tooCloud App Discovery
메타 데이터를 hello 에이전트에 의해 수집 되 면 hello tooone 분을 컴퓨터에 캐시 됩니다 또는 hello 될 때까지 캐시 된 데이터 크기가 5mb입니다. 그런 다음 압축 되며 보안 연결 toohello Cloud App Discovery 서비스를 통해 전송 됩니다.

Hello 에이전트 어떤 이유로 든 Cloud App Discovery 서비스 hello로 없습니다 toocommunicate 이면 hello 수집 된 메타 데이터에에서 저장 됩니다 (예: hello 관리자 그룹) hello 컴퓨터에서 권한이 있는 사용자만 액세스할 수 있는 로컬 파일 캐시.  
hello 에이전트 자동으로 시도 tooresend hello 캐시 된 메타 데이터에 성공적으로 hello Cloud App Discovery 서비스에서 수신 될 때까지 합니다.

## <a name="receiving-hello-data-at-hello-service-end"></a>Hello 서비스 쪽에서 hello 데이터 받기
hello 에이전트 toohello hello 컴퓨터 특정 클라이언트 인증 인증서를 사용 하 여 서비스 앞서 설명 된 데이터를 전달 된 암호화 된 채널을 통해 Cloud App Discovery를 인증 합니다.  
hello Cloud App Discovery 서비스의 분석 파이프라인 프로세스 메타 데이터 각 고객에 대해 개별적으로 논리적으로 hello 분석 파이프라인의 모든 단계를 통해 분할 하 여입니다.
hello 메타 데이터 드라이브 hello는 hello 포털에서 다양 한 보고서를 분석합니다.

처리 되지 않은 메타 데이터를 hello 및 too180 일 수를 분석 하는 hello 메타 데이터에 대 한 저장 됩니다. 또한 고객 자신이 선택한 Azure blob 저장소 계정에서 toocapture 분석 hello 메타 데이터를 선택할 수 있습니다.
이 hello 데이터를 더 오래 보존할 뿐만 아니라 메타 데이터의 오프 라인 분석에 유용 합니다.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Azure 포털 hello를 사용 하 여 hello 데이터에 액세스
노력 tookeep hello 수집 된 메타 데이터에 보안을 기본적으로 hello 테 넌 트의 전역 관리자만 적용 액세스 toohello Cloud App Discovery 기능 hello Azure 포털의.  
그러나 관리자는이 액세스 tooother 사용자 또는 그룹 toodelegate 선택할 수 있습니다.

> [!NOTE]
> 자세한 내용은 [클라우드 앱 검색 시작](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Azure AD Premium 라이선스가 hello 포털에서 사용자 액세스 hello 데이터를 받아야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [조직 내에서 사용되고 있는 허용되지 않은 클라우드 앱을 검색하는 방법](active-directory-cloudappdiscovery-whatis.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

