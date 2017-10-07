---
title: "aaaHow tooconfigure 응용 프로그램 프록시 응용 프로그램 toouse Kerberos 제한 위임 | Microsoft Docs"
description: "방법을 Azure AD 응용 프로그램 프록시 응용 프로그램에 대 한 Kerberos 제한 위임 tooconfigure 합니다."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>어떻게 tooconfigure 응용 프로그램 프록시 응용 프로그램 toouse Kerberos 제한 위임

hello 응용 프로그램 수 tooapplication 응용 프로그램 및 Azure 응용 프로그램 프록시 hello 초기 오른쪽을 제공 하는 hello 옵션 중 하나에서 다소 다를 SSO toopublished을 얻기 위해 사용할 수 있는 방법을 제한 된 위임 KCD (Kerberos)입니다. 여기서는 제한 구성된 tooperform kerberos 인증 toobackend 대신 응용 프로그램, 사용자가 커넥터 호스트입니다.

KCD를 사용 하기 위한 실제 프로시저 hello는 비교적 간단 하므로 및 일반적으로 다양 한 구성 요소 및 SSO를 용이 하 게 인증 흐름 hello에 대 한 기본적인 지식이 이내로 지정 해야 합니다. 정보 toohelp 곳 KCD SSO가 예상 대로 작동 하지 않는 여기서 시나리오 문제를 해결 찾기은 스파스 일 수 있습니다.

따라서이 문서는 tooprovide 자체 hello 흔히 볼 수 있는 가장 일반적인 문제 중 일부를 수정 하 고 문제를 해결에 도움이 되도록 참조의 단일 지점을 시도 합니다. Hello에서 진단에 대 한 동일한 시간 제품 추가 지침은 hello 더 복잡 하 고 구현의 높아 문제가 가장 많은.

이 문서는 hello 가정을 다음 참고:

-   Azure 응용 프로그램 프록시를 기준으로 배포 된 우리의 [설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) 하 고 일반 액세스 toonon KCD 응용 프로그램 정상적으로 작동 합니다.

-   hello 게시 된 대상 기반 응용 프로그램은 IIS와 Microsoft의 kerberos 구현 합니다.

-   hello 서버 및 응용 프로그램 호스트는 단일 Active Directory 도메인에 있어야합니다. 크로스 도메인 및 포리스트 시나리오에 대한 자세한 내용은 [KCD 백서](http://aka.ms/KCDPaper)에서 확인할 수 있습니다.

-   hello 주체 응용 프로그램이 게시 될 Azure에서 사용 하도록 설정 하는 사전 인증 된 테 넌 트 및 사용자가 되어야 양식을 통해 tooauthenticate tooAzure 기반 인증 합니다. 리치 클라이언트 인증 시나리오는이 문서에서 다루지 않는 있지만 어떤 시점 이후 hello에서 추가.

## <a name="prerequisites"></a>필수 조건

환경 및 hello 아키텍처 없겠죠 tooorganization 조직에서에서 다를 하거나 거의 모든 유형의 인프라에 azure 응용 프로그램 프록시를 배포할 수 있습니다. Hello KCD의 가장 일반적인 원인 중 하나 관련 문제는 자체 hello 환경 있지만 간단한 잘못 구성의 경우, 또는 일반 감독 합니다.

이러한 이유로 좋습니다 항상 toostart 우리의 main에서 배치 모든 hello 필수 조건을 충족 하는지 확인 하 여 [hello 응용 프로그램 프록시 문서와 KCD SSO를 사용 하 여](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) 문제 해결을 시작 하기 전에.

특히 hello 섹션에서 이전 버전의 Windows에서는 하지만 다른 몇 가지 사항을 고려해 야 하는 동안에 기본값과 다른 접근 방식을 tooconfiguring KCD를 사용 하는이 처럼 2012R2에서 KCD를 구성 합니다.

-   도메인 구성원 서버 tooopen 특정 도메인 컨트롤러는 보안 채널 대화 상자에 대 한 일반적이 지 않습니다. 그런 다음 있으므로 커넥터 호스트 일반적으로 되어서는 안 제한 toobeing 수 toocommunicate 특정 로컬 사이트 Dc와 지정된 된 시간에 tooanother 대화를 이동 합니다.

-   지점 위에 비슷한 toohello 도메인 간 시나리오 수 hello 로컬 네트워크 경계 외부에 있는 커넥터 호스트 tooDCs를 지시 하는 조회에 의존 합니다. 동일 하 게는이 시나리오에서 허용 하는 또한 트래픽을 위임 그렇지 다른 각 도메인을 나타내는 tooDCs 있는지 중요 toomake 실패 합니다.

-   가능한 경우에는 커넥터 호스트와 DC 사이에 활성 IPS/IDS 장치를 배치해서는 안 됩니다. 이러한 장치가 코어 RPC 트래픽을 방해할 수 있습니다.

Tooresolve 문제를 신속 하 게 싶습니다 하 고 효과적으로 시간이 걸리므로, 만큼 하므로 가능한 경우 시도 하 고 테스트 해야 위임 시나리오의 가장 간단한 hello에 있습니다. 더 다양 한 요인을 사용자 hello, hello 더 있을 수 있습니다와 toocontend 합니다. 예를 들어 테스트 tooa 단일 커넥터 제한 귀중 한 시간을 절약할 수 있습니다 및 hello 문제를 해결 한 후에 추가 커넥터를 추가할 수 있습니다.

일부 환경 요소 또한 일으킬 수 있습니다 tooan 문제를 다시 시도 하 고 hello 아키텍처 tooa 테스트에 필요한 최소 최소화 하는 가능한 경우. 잘못 구성 된 내부 방화벽 Acl 가지 형태가 예를 들어, 있으므로 가능 하면 모든 트래픽을 toohello Dc와 백 엔드 응용 프로그램을 통해 바로 허용 커넥터에서. 

실제로 hello 절대 최상의 위치 tooposition 커넥터의 가까운 tootheir 대상이 될 수 있습니다. 테스트가 진행되는 동안 방화벽을 인라인으로 배치하면 쓸데없이 복잡해져 검사가 지연될 수 있습니다.

KCD 문제가 되는 요소는 무엇인가요? 물론 있습니다 KCD SSO 문제점의 실패 및 hello 첫 번째 기호 일반적으로 나타날에 있는 여러 클래식 표시가 hello 브라우저.

   ![잘못된 KCD 구성 오류](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![권한 부여 toomissing 사용 권한 실패 했습니다.](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

약 hello tooperform SSO를 작동 하지 않으며 따라서 거부의 동일한 증상 모든 hello 사용자 액세스 toohello 응용 프로그램입니다.

## <a name="troubleshooting"></a>문제 해결

다음 문제 해결 hello 문제 및 관찰 된 증상에 따라 결정 됩니다. 모든 라인으로 전환 하기 전에 있습니다 가져올 수 없습니다. 아직가에서 유용한 정보를 포함 하, 링크를 따라 hello을 제안는 추가 합니다.

-   [응용 프로그램 프록시 문제 및 오류 메시지 문제 해결](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Kerberos 오류 및 증상](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [온-프레미스 및 클라우드 ID가 동일하지 않은 경우 SSO를 사용하여 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

수 있다면이 다음 hello 주요 문제 확실 하 게 존재 합니다. 아래 인 toodig 필요한 hello 흐름 문제를 해결할 수 있는 세 가지 고유 단계로 구분 하 여 시작 합니다.

**클라이언트 사전 인증** -hello 외부 사용자는 브라우저를 통해 tooAzure를 인증 합니다.

수 toopre 되-인증 tooAzure은 KCD SSO toofunction 필수적입니다. 문제가 있는 경우 먼저 테스트하고 해결해야 합니다. Hello 사전 인증 단계에 있는 관계 tooKCD 이나 hello 참고 응용 프로그램을 게시 합니다. 상당히 쉽게 toocorrect 불일치 온전성 hello 주체 계정을 검사 하 여 Azure에 있는 것이 고 아닌지 사용 안 함/차단 합니다. hello hello 브라우저에 대 한 오류 응답에는 일반적으로 알기 toounderstand hello 원인입니다. 확실 하지 않은 경우에 다른 문제 해결 문서 tooverify 우리의 확인할 수 있습니다.

**위임 서비스** -사용자가 대신 하 여 KDC (Kerberos 배포 센터)에서 kerberos 서비스 티켓을 가져오는 Azure 프록시 커넥터 hello 합니다.

클라이언트 hello와 hello Azure 프런트 엔드 간의 hello 외부 통신 이외의 보장 작동 하는 데 없이 KCD에 영향을 주지 않습니다 있어야 합니다. 이 hello Azure 모드 해제 프록시 서비스 사용된 tooobtain kerberos 티켓 수 있는 유효한 사용자 ID로 제공 될 수 있도록 합니다. 이 KCD가 없으면 불가능하며 실패할 것입니다.

앞에서 설명한 대로 hello 브라우저 오류 메시지는 일반적으로 몇 가지 좋은 힌트가 작업이 실패 한 이유를 제공 합니다. 이 수 toocorrelate hello 동작 tooactual 이벤트 hello Azure 프록시 이벤트 로그에 대로 hello에 대 한 응답 있는지 toonote hello 동작 ID 및 타임 스탬프를 확인 합니다.

   ![잘못된 KCD 구성 오류](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

되 고 13019 또는 12027 이벤트로 hello 해당 항목이 표시 hello 이벤트 로그를 표시 합니다. Hello 커넥터 이벤트 로그를 찾을 수 있습니다 **Applications and Services Logs** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **커넥터**&gt;**Admin**합니다.

   ![응용 프로그램 프록시 이벤트 로그의 이벤트 13019](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![응용 프로그램 프록시 이벤트 로그의 이벤트 12027](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   내부 DNS에 A 레코드를 사용 하 여 hello 응용 프로그램의 주소 및 CName 하지

-   해당 hello 커넥터 호스트에 지정 대상 계정의 SPN hello 권한 toodelegate toohello 부여를 다시 확인 **모든 인증 프로토콜을 사용 하 여** 을 선택 합니다. 자세한 내용은 주 [SSO 구성 문서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)에서 다룹니다.

-   실행 하 여 AD에 있는지에 hello SPN의 단일 인스턴스만 있는지 확인 한 **setspn-x** 모든 도메인 구성원 호스트의 cmd 프롬프트에서

-   도메인 정책이 되 고 있으면 toosee 적용 toolimit hello 확인 [최대 크기: 발급 된 kerberos 토큰](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/)경우 토큰을 가져오면에서이 사용 안 함 hello 커넥터 toobe 과도 하 게 찾을 수,

KDC는 도메인 및 hello 커넥터 호스트 간의 hello 교환을 캡처 네트워크 추적에는 다음 보다 낮은 수준에 대 한 정보의 hello 문제를 가져오는 다음 가장 효과적인 방법 hello 것입니다. 자세한 내용은 [심층 분석 문제 해결 문서](https://aka.ms/proxytshootpaper)를 참조하세요.

티켓 좋으면, 401 반환 toohello 응용 프로그램 인해 인증 실패를 알리는 hello 로그의 이벤트를 표시 되어야 합니다. 다음 단계를 수행 하는 hello 가장,이 일반적으로 해당 hello 대상 응용 프로그램 티켓을 거부를 나타냅니다.

**대상 응용 프로그램** -hello 커넥터에서 제공 하는 hello kerberos 티켓의 hello 소비자

이 스테이지 hello 커넥터에서 예상된 toohave가 보내집니다는 kerberos 서비스 티켓 toohello 백엔드 hello 첫 번째 응용 프로그램 요청 내에서 헤더로 합니다.

-   Hello 응용 프로그램을 사용 하 여 hello 포털에 정의 된 내부 URL hello 응용 프로그램에 hello 커넥터 호스트에 hello 브라우저에서 직접 액세스할 수 있는지 확인 합니다. 그런 다음 성공적으로 로그인할 수 있습니다. 이 작업에 대 한 내용은 hello 커넥터 문제 해결 페이지에 있습니다.

-   Hello 커넥터 호스트에 있는 hello 브라우저 간의 hello 인증을 확인 하 고 hello 응용 프로그램 hello 다음 중 하나를 수행 하 여 kerberos를 사용 합니다.

1.  개발 도구를 실행 (**F12**) Internet Explorer 또는 사용에 [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) hello 커넥터 호스트에서 합니다. Hello 내부 URL을 사용 하 여 toohello 응용 프로그램 및 hello 응용 프로그램에서 hello 응답에서 반환 된 WWW 인증 헤더를 제공 하는 hello 검사, kerberos 또는 협상 하거나 tooensure 있는지. 후속 kerberos blob hello 응답에서 반환 된 hello 브라우저 toohello에서 응용 프로그램 일반적으로로 시작 **YII**이므로 재생에서 되 고 kerberos의 상태입니다. NTLM hello에 다른 손 항상 시작 **TlRMTVNTUAAB**을 base 64에서 디코딩할 때 NTLMSSP을 읽습니다. 표시 되 면 **TlRMTVNTUAAB** hello blob의 hello 시작, 즉, Kerberos **하지** 사용할 수 있습니다. TlRMTVNTUAAB가 표시되지 않으면 Kerberos를 사용할 수 있습니다.

  * Note, Fiddler를 사용 하는 경우이 메서드를 일시적으로 IIS에서 hello 응용 프로그램의 구성에 대 한 확장 된 보호를 사용 하지 않도록 설정 해야 합니다.

     ![브라우저 네트워크 검사 창](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *그림:* TIRMTVNTUAAB로 시작하지 않기 때문에 Kerberos를 사용할 수 있습니다. 이는 YII로 시작하지 않는 Kerberos Blob의 예입니다.

2.  IIS 사이트 및 액세스 앱에서 직접 IE에서 커넥터 호스트에 hello 공급자 목록에서 NTLM을 일시적으로 제거 합니다. Hello 공급자 목록에 더 이상 NTLM, Kerberos를 사용 하 여만 수 tooaccess hello 응용 프로그램 있어야 합니다. 이 실패 하면 hello 응용 프로그램의 구성에 문제가 있다는 것을 제안 하는 경우 Kerberos 인증이 작동 하지 않습니다.

Kerberos를 사용할 수 없는 경우 IIS toomake 있는지에서 설정을 협상할 검사 hello 응용 프로그램의 인증 최상위 바로 아래 NTLM으로 나열 됩니다. (Negotiate:kerberos 또는 Negotiate:PKU2U 아님). Kerberos가 작동하는 경우에만 계속 진행합니다.

   ![Windows 인증 공급자](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Kerberos 및 NTLM 위치에서 사용 하 여 hello 포털에서 hello 응용 프로그램에 대 한 사전 인증 일시적으로 중단을 수 있습니다. 참조 하는 경우 hello에서 액세스할 수 있습니다 hello 외부 URL을 사용 하 여 인터넷 합니다. Tooauthenticate 입력 정보 요청된 해야 하 고 동일한 계정에 사용 되는 hello hello로 하므로 수 toodo 있어야 이전 단계입니다. 그렇지 않은 경우이 hello 백 엔드 응용 프로그램 및 KCD 하지에 문제가 전혀 나타냅니다.

-   이제 다시 hello 포털에서 사전 인증을 사용 하도록 설정 하 고 외부 URL 통해 tooconnect toohello 응용 프로그램을 시도 하 여 Azure를 통해 인증 합니다. SSO에 실패 한 경우 다음 표시 되어야 13022 hello 로그에 이벤트를 더한 hello 브라우저를 사용할 수 없는 오류 메시지:

    *Microsoft AAD 응용 프로그램 프록시 커넥터 hello 백 엔드 서버 응답 HTTP 401 오류와 함께 tooKerberos 인증 시도 하기 때문에 hello 사용자를 인증할 수 없습니다.*

    ![HTTTP 401 사용할 수 없음 오류](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Hello IIS 응용 프로그램 tooensure hello 구성 된 응용 프로그램 풀은 SPN hello 동일한 계정을 구성한에 대해 ad에서는 아래 그림과 같이 IIS에서 이동 하 여 구성 된 toouse hello 확인

    ![IIS 응용 프로그램 구성 창](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Hello identity 것을 알고 있다면이 계정에 SPN hello로 확실 하 게 구성 되어 있는지 cmd 프롬프트 toomake에서 hello 다음을 실행 합니다. 예를 들어 **setspn – q http/spn.wacketywack.com**을 실행합니다.

    ![SetSPN 명령 창](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Hello 포털의 hello 응용 프로그램의 설정에 대해 정의 된 SPN에 같은 SPN hello 응용 프로그램의 응용 프로그램 풀에서 사용 중인 hello 대상 AD 계정에 대해 구성 된 hello는 해당 hello를 확인 합니다.

   ![Azure Portal의 SPN 구성](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   IIS와 선택 hello로 이동 **구성 편집기** hello 응용 프로그램에 대 한 옵션을 너무 이동**system.webServer/security/authentication/windowsAuthentication** 있는지 toomake 해당 **UseAppPoolCredentials** tootrue 설정

   ![IIS 구성 앱 풀 자격 증명 옵션](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

하면서 Kerberos 작업의 hello 성능을 향상 시키는 데 유용 합니다 사용 하도록 설정 하는 커널 모드를 종료로 인해 hello 티켓 hello에 대 한 컴퓨터 계정을 사용 하 여 암호를 해독 하는 서비스 toobe를 요청 합니다. 이 집합 tootrue 중단 되므로 포함 된 hello 로컬 시스템, 라고도 KCD hello 응용 프로그램은 팜에 있는 여러 서버에서 호스트 되는 경우.

-   추가 검사를 할 수 있습니다 toodisable hello **확장** 보호 너무 합니다. 내용이 toobreak 매우 특수 한 구성에서 설정 된 경우 KCD를 입증 되었습니다이 발생 한 시나리오는 hello 기본 웹 사이트의 하위 폴더도 응용 프로그램을 게시 하는 위치입니다. 이 자체는 익명 인증이 구성 된만 자식 개체는 실제 설정이 상속 것을 제안 회색 hello 전체 대화 상자를 종료 합니다. 하지만 여기서는 항상 알아두어야이 옵션을 사용 가능한 하므로 이제 테스트,이 tooenabled toorestore를 잊지 마십시오.

이러한 추가 검사가를 설치 해야 하면 게시 된 응용 프로그램을 사용 하 여 추적 toostart 합니다. 계속 진행 수 및 스핀도 추가 커넥터를 구성 toodelegate, 되지만 작업은 더 이상 없으면 하는 경우는 권장 되는 사항은 자세한 기술 연습에 대 한 읽기 [문제를 해결 하는 Azure AD 응용 프로그램에 대 한 hello 완벽 가이드 프록시](https://aka.ms/proxytshootpaper)

인 경우 아직 없습니다 tooprogress 문제, 것 만족도 매우 tooassist 보다 큰 수 지원과 여기에서 계속 합니다. Hello 포털 내에서 직접 지원 티켓을 만들고 엔지니어가 tooyou 아웃 도달 하 게 됩니다.

## <a name="other-scenarios"></a>기타 시나리오

-   Azure 응용 프로그램 프록시는 해당 요청 tooan 응용 프로그램을 보내기 전에 Kerberos 티켓을 요청 합니다. 일부 타사 응용 프로그램 서버 Tableau와 같은 인증,이 메서드를 원하지 않는 및 보다 더 많은 기본 hello을 예상 협상 tootake 장소입니다. hello 첫 번째 요청은 익명 hello 응용 프로그램 toorespond 401을 통해 지원 되는 hello 인증 유형을 허용 합니다.

-   이중 홉 인증 - 일반적으로 SQL Reporting Services와 같이 인증이 필요한 백 엔드 및 프런트 엔드를 사용하여 응용 프로그램이 계층화된 시나리오에 사용됩니다.

## <a name="next-steps"></a>다음 단계
[관리되는 도메인에서 KCD(Kerberos 제한 위임) 구성](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
