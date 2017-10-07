---
title: "aaaUnderstand Azure AD 응용 프로그램 프록시 커넥터 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항에 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Azure AD 응용 프로그램 프록시 커넥터 이해

커넥터는 Azure AD 응용 프로그램 프록시를 가능하게 만듭니다. 간단 하 고 쉬운 toodeploy 및 유지 관리 되며 슈퍼 강력 합니다. 이 문서에서는 작동 방식, 어떤 커넥터는 고 방법에 대 한 몇 가지 제안 사항 toooptimize 배포 합니다. 

## <a name="what-is-an-application-proxy-connector"></a>응용 프로그램 프록시 커넥터란

커넥터는 온-프레미스 sit hello 아웃 바운드 연결 toohello 응용 프로그램 프록시 서비스를 용이 하 게 하는 경량 에이전트입니다. 커넥터에 대 한 액세스 toohello 백 엔드 응용 프로그램이 Windows 서버에 설치 되어야 합니다. 커넥터를 커넥터 그룹 트래픽 toospecific 응용 프로그램을 처리 하는 각 그룹으로 구성할 수 있습니다. 커넥터를 부하 분산, 자동으로 toooptimize 네트워크 구조 도움이 될 수 있습니다. 

## <a name="requirements-and-deployment"></a>요구 사항 및 배포

응용 프로그램 프록시 toodeploy 성공적으로 커넥터가 하나 이상 필요 하지만 큰 복원 력을 대 한 두 개 이상의 것이 좋습니다. Hello 커넥터는 Windows Server 2012 R2 또는 2016 컴퓨터에 설치 합니다. hello 커넥터 toobe 수 toocommunicate hello 응용 프로그램 프록시 서비스 뿐 아니라 게시 하는 hello 온-프레미스 응용 프로그램에 필요 합니다. 

커넥터 서버 hello에 대 한 hello 네트워크 요구 사항에 대 한 자세한 내용은 참조 [응용 프로그램 프록시를 시작 하 고 커넥터를 설치](active-directory-application-proxy-enable.md)합니다.

## <a name="maintenance"></a>유지 관리
hello 커넥터 및 hello 서비스 작업을 처리할 모든 hello 고가용성 합니다. 동적으로 추가하거나 제거할 수 있습니다. 새 요청이 수신 될 때마다 현재 사용할 수 있는 라우트된 tooone hello 커넥터의 것 합니다. 커넥터를 일시적으로 사용할 수 없는 경우 toothis 트래픽을 응답 하지 않는 것입니다.

hello 커넥터는 상태 비저장 있고 hello 컴퓨터에 구성 데이터가 없습니다. hello 데이터만 저장 하 고이 hello 설정을 hello 서비스 및 해당 인증 인증서를 연결 하기 위한 합니다. Toohello 서비스 연결 될 때 모든 필수 hello 구성 데이터를 끌어옵니다 하며 몇 분 마다 새로 고칩니다.

커넥터에도 hello 서버 toofind 있는지 여부를 폴링할 hello 커넥터의 새 버전이 있습니다. 개체를 찾은 경우 hello 커넥터는 자신을 업데이트 합니다.

Hello 이벤트 로그 및 성능 카운터 중 하나를 사용 하 여, 실행 중인 hello 컴퓨터에서 커넥터를 모니터링할 수 있습니다. 또는 hello Azure 포털의 hello 응용 프로그램 프록시 페이지에서 해당 상태를 볼 수 있습니다.

 ![AzureAD 응용 프로그램 프록시 커넥터](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

사용 하지 않은 커넥터를 삭제 하는 toomanually가 필요는 없습니다. 커넥터가 실행 되 고 toohello 서비스를 연결로 활성 남아 있습니다. 사용되지 않는 커넥터는 _비활성_으로 태그가 지정되고 비활성 상태가 된 지 10일 후에 제거됩니다. 않으려면 toouninstall 커넥터, hello 커넥터 서비스와 hello 업데이트 프로그램 서비스 hello 서버에서 제거 하지만 합니다. 컴퓨터 toofully 제거 hello 서비스를 다시 시작 합니다.

## <a name="automatic-updates"></a>자동 업데이트

Azure AD는 배포 하는 모든 hello 커넥터에 대해 자동 업데이트를 제공 합니다. Hello 응용 프로그램 프록시 커넥터 업데이트 프로그램 서비스를 실행 상태로 커넥터 자동 업데이트 됩니다. 서버에서 커넥터 업데이트 프로그램 서비스 hello, 너무 해야 하는 경우 표시 되지 않으면[커넥터를 다시 설치](active-directory-application-proxy-enable.md) tooget 업데이트 합니다. 

자동 업데이트 toocome tooyour 커넥터에 대 한 toowait 않으려면 수동 업그레이드를 수행할 수 있습니다. Toohello 이동 [커넥터 다운로드 페이지](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) 커넥터 찾아서 선택 인 hello 서버의 **다운로드**합니다. 이 프로세스 hello 로컬 커넥터에 대 한 업그레이드를 시작합니다. 

여러 명의 커넥터가 있는 테 넌 트에 대 한 hello 자동 업데이트를 대상으로 첫 번째 커넥터 환경에서 각 그룹 tooprevent 중단 시간에 한 번에. 

다음과 같은 경우 커넥터를 업데이트할 때 가동 중지 시간이 발생할 수 있습니다.  
- 하나의 커넥터만 있습니다. tooavoid이 작동 중단이 시간 고가용성을 개선 하 고 두 번째 커넥터를 설치 하는 것이 좋습니다 및 [커넥터 그룹을 만들](active-directory-application-proxy-connectors-azure-portal.md)합니다.  
- 커넥터가 했습니다. 트랜잭션 hello 가운데에 hello 업데이트를 시작 했습니다. Hello 초기 트랜잭션이 손실 되어도 브라우저 hello 작업이 자동으로 다시 시도 하거나, 페이지를 새로 고칠 수 있습니다. Hello 요청을 다시 보냅니다 때 hello 트래픽은 라우트된 tooa 백업 커넥터입니다.

## <a name="creating-connector-groups"></a>커넥터 그룹 만들기

커넥터 그룹 tooassign 특정 커넥터 tooserve 특정 응용 프로그램을 사용합니다. 커넥터의 수를 함께 그룹화 하 고 각 응용 프로그램 tooa 그룹을 할당할 수 있습니다. 

커넥터 그룹을 보다 쉽게 toomanage 대규모 배포 사용 하면 됩니다. 위치 기반 커넥터 그룹 tooserve만 로컬 응용 프로그램을 만들 수 있기 때문에 서로 다른 지역에서 호스팅되는 응용 프로그램에 있는 테 넌 트에 대 한 대기 시간을 향상 시킬 합니다. 

커넥터 그룹에 대해 자세히 toolearn 참조 [별도 네트워크 및 커넥터 그룹을 사용 하 여 위치에서 응용 프로그램을 게시](active-directory-application-proxy-connectors-azure-portal.md)합니다.

## <a name="security-and-networking"></a>보안 및 네트워킹

Toosend 요청 toohello 응용 프로그램 프록시 서비스 수 있게 해 주는 hello 네트워크에서 아무 곳 이나 커넥터를 설치할 수 있습니다. 중요 한 점은 역시 hello 커넥터를 실행 하는 hello 컴퓨터에 액세스 tooyour 앱입니다. 회사 네트워크 내부 또는 hello 클라우드에서 실행 되는 가상 컴퓨터에서 커넥터를 설치할 수 있습니다. 커넥터를 완충 영역(DMZ) 내에서 실행할 수는 있지만 꼭 그래야 하는 것은 아닙니다. 모든 트래픽이 아웃바운드이므로 네트워크 보안이 유지되기 때문입니다.

커넥터는 아웃바운드 요청만 보냅니다. toohello 응용 프로그램 프록시 서비스 및 toohello hello 아웃 바운드 트래픽이 전송 응용 프로그램을 게시 합니다. 트래픽 세션이 설정 되 면 두 가지 방식으로 이동 하므로 인바운드 포트 tooopen이 필요는 없습니다. Hello 커넥터 간의 부하 분산을 tooset 했거나 방화벽을 통해 인바운드 액세스를 구성 하지 않습니다. 

아웃바운드 방화벽 규칙 구성에 대한 자세한 내용은 [기존 온-프레미스 프록시 서버 작업](application-proxy-working-with-proxy-servers.md)을 참조하세요.

사용 하 여 hello [Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify 커넥터 hello 응용 프로그램 프록시 서비스에 연결할 수 있습니다. 여기에 최소한 hello 중앙 미국 지역과 hello 지역 가장 가까운 tooyou는 모두 녹색 확인 표시가 있는지를 확인 합니다. 그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다. 

## <a name="performance-and-scalability"></a>성능 및 확장성

응용 프로그램 프록시 서비스 hello에 대 한 크기 조정 투명 하 게 않으며 소수 자릿수는 커넥터에 대 한 비율입니다. Toohave 커넥터 toohandle 최대 트래픽 충분 해야합니다. 그러나 tooconfigure 부하 분산 커넥터 그룹 내에서 모든 커넥터 자동으로 부하를 분산 하기 때문에 필요 하지 않습니다.

커넥터 상태 비저장 이므로 hello 사용자 또는 세션 수로 적용 되지 않습니다. 대신, 응답 하지 않는 요청 및 페이로드 크기 toohello 수 있습니다. 표준 웹 트래픽으로 평균적인 컴퓨터는 초당 몇 천 개의 요청을 처리할 수 있습니다. hello 특정 용량 hello 정확한 컴퓨터 특성에 따라 달라 집니다. 

hello 커넥터 성능 CPU 및 네트워킹에서 바인딩되어 있습니다. 네트워킹 중요 tooget 신속한 연결 toohello 응용 프로그램 및 Azure의 hello 온라인 서비스는 SSL 암호화 및 암호 해독에 대 한 CPU 성능 필요 합니다.

반면, 커넥터에서는 메모리가 중요하지 않습니다. 대부분의 hello 처리 및 인증 되지 않은 모든 트래픽 hello 온라인 서비스를 담당합니다. Hello 클라우드에서 수행할 수 있는 모든 작업은 hello 클라우드에서 수행 됩니다. 

성능에 영향을 주는 또 다른 요소를 비롯 하 여 hello 커넥터 간의 hello 네트워킹의 hello 품질은: 

* **온라인 서비스 hello**: 느리거나 지연 시간이 긴 연결 toohello Azure 영향 hello 커넥터 성능에 대 한 응용 프로그램 프록시 서비스입니다. 최상의 성능을 얻으려면 hello에 대 한 조직 tooAzure Express 경로와 연결 합니다. 그렇지 않으면 해당 연결 tooAzure 최대한 효율적으로 처리 되는지 확인할 네트워킹 팀을 해야 합니다. 
* **백 엔드 응용 프로그램 hello**: 일부 경우에는 hello 커넥터 사이의 저하 또는 연결 하지 못하도록 차단할 수 있는 hello 백 엔드 응용 프로그램 프록시를 더 합니다. tootroubleshoot이이 시나리오에서는 hello 커넥터 서버에서 브라우저를 열고 tooaccess hello 응용 프로그램을 시도 합니다. Azure의 hello 커넥터를 실행 하는 경우 hello 응용 프로그램은 온-프레미스 hello 환경을 사용자에 게 예상과 아닐 수 있습니다.
* **도메인 컨트롤러를 hello**: hello 요청 toohello 백 엔드를 보내기 전에 hello 도메인 컨트롤러를 연결할 수 있을 hello 커넥터 Kerberos 제한 위임을 사용 하 여 SSO를 수행 합니다. hello 커넥터 Kerberos 티켓의 캐시에는 있지만 사용 중인 환경에서 hello 응답성 hello 도메인 컨트롤러의 성능이 떨어질 수 있습니다. 이 문제는 Azure에서 실행되지만 온-프레미스 도메인 컨트롤러와 통신하는 커넥터에서 좀 더 자주 발생합니다. 

네트워크 최적화에 대한 자세한 내용은 [Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항](application-proxy-network-topology-considerations.md)을 참조하세요.

## <a name="domain-joining"></a>도메인 가입

도메인 가입되지 않은 컴퓨터에서 커넥터를 실행할 수 있습니다. 그러나 원하는 single sign on (SSO) tooapplications 통합 IWA (Windows 인증)를 사용 하는 도메인에 가입 된 컴퓨터가 필요 합니다. 이 경우 hello 커넥터 컴퓨터에서 수행할 수 있는 조인된 tooa 도메인 있어야 [Kerberos](https://web.mit.edu/kerberos) hello에 대 한 hello 사용자를 대신해 서 제한 된 위임에 응용 프로그램을 게시 합니다.

조인 된 toodomains 또는 부분 신뢰 또는 tooread 전용 도메인 컨트롤러를 갖고 있는 포리스트가 커넥터 될 수도 있습니다.

## <a name="connector-deployments-on-hardened-environments"></a>강화된 환경에 커넥터 배포

일반적으로 커넥터 배포는 매우 간단하며 특별한 구성이 필요하지 않습니다. 그러나 고려해야 할 몇 가지 고유한 조건이 있습니다.

* Hello 아웃 바운드 트래픽을 제한 하는 조직은 해야 [필요한 포트를 열고](active-directory-application-proxy-enable.md#open-your-ports)합니다.
* FIPS 규격 컴퓨터 필요한 toochange 수 자신의 구성 tooallow 커넥터 프로세스 toogenerate hello 및 인증서를 저장 합니다.
* 잠글 hello 프로세스에 따라 해당 환경 요청 네트워킹 문제 hello 해당 하는 조직은 toomake 두 커넥터 서비스를 활성화 tooaccess 모든 필요한 포트 및 Ip를가지고 있습니다.
* 경우에 따라 앞으로 아웃 바운드 프록시 hello 양방향 인증서 인증을 중단 하 고 hello 통신 toofail 발생할 수 있습니다.

## <a name="connector-authentication"></a>커넥터 인증

보안 서비스 tooprovide 커넥터 tooauthenticate hello 서비스 방향으로 다르고 hello 서비스 tooauthenticate hello 커넥터에 대. 이 인증을 수행할지 hello 커넥터 hello 연결을 시작 하는 경우 클라이언트 및 서버 인증서를 사용 하 여 합니다. 이 방식으로 hello 관리자의 사용자 이름 및 암호 hello 커넥터 컴퓨터에 저장 되지 않습니다.

사용 하는 hello 인증서는 특정 toohello 응용 프로그램 프록시 서비스입니다. Hello 초기 등록 하는 동안 작성 하며 자동으로 몇 개월 마다 hello 커넥터에서 권한이 갱신 합니다. 

커넥터에 연결 되어 있지 않으면 toohello 서비스 몇 개월까지 해당 인증서에 대 한 오래 된 상태일 수 있습니다. 이 경우 제거 하 고 hello 커넥터 tootrigger 등록을 다시 설치 하십시오. Hello 다음 PowerShell 명령을 실행할 수 있습니다.

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Hello 내부적

대부분의 Windows 이벤트 로그를 포함 하 여 관리 도구 같은 hello 갖추고 있으므로 커넥터 Windows Server 웹 응용 프로그램 프록시 기반

 ![Hello 이벤트 뷰어를 사용 하 여 이벤트 로그 관리](./media/application-proxy-understand-connectors/event-view-window.png)

및 Windows 성능 카운터 

 ![Hello 성능 모니터 카운터 toohello 커넥터를 추가 합니다.](./media/application-proxy-understand-connectors/performance-monitor.png)

hello 커넥터 관리 및 세션에는 로그입니다. hello 관리 로그 키 및 해당 오류에 포함 됩니다. hello 세션 로그 모든 hello 트랜잭션 및 처리 세부 정보를 포함 합니다. 

toosee hello 로그, 이벤트 뷰어를 열고 hello toohello 이동 **보기** 메뉴를 사용 하도록 설정한 **분석 및 디버그 로그 표시**합니다. 그런 다음 할 toostart 이벤트를 수집 합니다. 이러한 로그 hello 커넥터는 보다 최신 버전을 기반으로 Windows Server 2012 r 2에서 웹 응용 프로그램 프록시에 표시 되지 않습니다.

Hello 서비스 창에서 hello 서비스의 hello 상태를 검사할 수 있습니다. 두 개의 Windows 서비스를 구성 하는 hello 커넥터: hello 실제 커넥터 및 hello updater 합니다. 둘 모두 hello 항상을 실행 해야 합니다.

 ![AzureAD 서비스 로컬](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>다음 단계


* [커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시](active-directory-application-proxy-connectors-azure-portal.md)
* [기존 온-프레미스 프록시 서버 작업](application-proxy-working-with-proxy-servers.md)
* [응용 프로그램 프록시 및 커넥터 오류 문제 해결](active-directory-application-proxy-troubleshoot.md)
* [Toosilently hello Azure AD 응용 프로그램 프록시 커넥터를 설치 하는 방법](active-directory-application-proxy-silent-installation.md)

