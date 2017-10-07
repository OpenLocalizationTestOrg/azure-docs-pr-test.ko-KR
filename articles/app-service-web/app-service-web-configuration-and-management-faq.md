---
title: "Azure 웹 앱에 대 한 Faq aaaConfiguration | Microsoft Docs"
description: "Azure 앱 서비스의 hello 웹 응용 프로그램 기능에 대 한 구성 및 관리 문제에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Azure의 Web Apps에 대한 구성 및 관리 FAQ

이 문서는 질문과 대답 (Faq) 구성 및 관리 문제에 대 한 hello에 대 한 답변 toofrequently [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Toomove 앱 서비스 리소스를 원하는 경우 알고 있어야 합니까 제한 사항이 있습니까?

Toomove 앱 서비스 리소스 tooa 새 리소스 그룹이 나 구독을 하려면 많은 경우 몇 가지 제한 사항이 toobe를 인식 합니다. 자세한 내용은 [App Service 제한 사항](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)을 참조하세요.

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>내 웹앱에 대한 사용자 지정 도메인 이름을 어떻게 사용할 수 있나요?

Azure 웹 앱과 함께 사용자 지정 도메인 이름을 사용 하는 방법에 대 한 답변 toocommon 질문 우리의 7 분 분량의 비디오를 참조 하세요. [사용자 지정 도메인 이름을 추가](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name)합니다. 방법 보여 주는 연습을 제공 하는 비디오 hello tooadd 사용자 지정 도메인 이름입니다. 설명 방법을 toouse hello 대신 고유한 URL *. 앱 서비스 웹 앱과 함께 azurewebsites.net URL입니다. 상세 연습을 볼 수 [방법을 사용자 지정 도메인 이름 toomap](web-sites-custom-domain-name.md)합니다.


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>내 웹앱에 대한 새로운 사용자 지정 도메인을 어떻게 구매할 수 있나요?

toopurchase 및 설정 앱 서비스 웹 앱에 대 한 사용자 지정 도메인을 확인 하려면 어떻게 해야 toolearn [구매 및 앱 서비스에서 사용자 지정 도메인 이름을 구성](custom-dns-web-site-buydomains-web-app.md)합니다.


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>내 웹앱에 대한 기존 SSL 인증서를 어떻게 업로드 및 구성할 수 있나요?

tooupload 하 고 기존 사용자 지정 SSL 인증서를 설정의 참조 toolearn [기존 사용자 지정 SSL 인증서 tooan Azure 웹 앱을 바인딩할](app-service-web-tutorial-custom-ssl.md#upload)합니다.


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Azure에서 내 웹앱에 대한 새 SSL 인증서를 어떻게 구매 및 구성할 수 있나요?

toopurchase 및 앱 서비스 웹 앱에 대 한 SSL 인증서 설정을 확인 하려면 어떻게 해야 toolearn [SSL 인증서 tooyour 앱 서비스 앱 추가](web-sites-purchase-ssl-web-site.md)합니다.


## <a name="how-do-i-move-application-insights-resources"></a>Application Insights 리소스를 어떻게 이동할 수 있나요?

현재 Azure Application Insights hello 이동 작업을 지원 하지 않습니다. 원래 리소스 그룹에 Application Insights 리소스가 포함된 경우 해당 리소스를 이동할 수 없습니다. 앱 서비스 앱 toomove 려 할 때 hello Application Insights 리소스를 포함 하는 경우 전체 hello 이동 작업이 실패 합니다. 그러나 Application Insights 및 앱 서비스 계획에서 toobe 불필요 hello hello 앱 toofunction hello에 대 한 hello 응용 프로그램으로 동일한 리소스 그룹 올바르게 합니다.

자세한 내용은 [App Service 제한 사항](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)을 참조하세요.

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>어디에서 지침 검사 목록을 찾고 리소스 이동 작업을 알아볼 수 있나요?

[앱 서비스 제한 사항](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) 어떻게 toomove 리소스 tooeither 새 구독 또는 tooa 새 리소스 그룹 hello에 동일한 표시 구독 합니다. Hello 리소스 이동 검사 목록에 대 한 정보, 서비스는 hello 이동 작업을 지원 하 고 앱 서비스 제한 사항 및 기타 항목에 대 한 자세한 수 있습니다.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>웹 응용 프로그램에 대 한 hello 서버 표준 시간대를 설정 하려면 어떻게 합니까?

tooset hello 서버 표준 시간대에 대 한 웹 앱:

1. Hello 앱 서비스 구독에 Azure 포털에서에서 toohello 이동 **응용 프로그램 설정** 메뉴.
2. **앱 설정**에서 이 설정을 추가합니다.
    * 키 = WEBSITE_TIME_ZONE
    * 값 = *hello 사용할 표준 시간대*
3. **저장**을 선택합니다.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>내 연속 WebJobs가 때때로 실패하는 이유는 무엇인가요?

기본적으로 웹앱은 일정 기간 유휴 상태인 경우 언로드됩니다. Hello 시스템을 리소스를 절약할 수 있습니다. Hello를 켤 수 기본 및 표준 계획에 **Always On** hello 항상 로드 tookeep hello 웹 응용 프로그램을 설정 합니다. 웹 앱에서 연속 Webjob을 소모한 경우 스냅숏을 설정 해야 **Always On**, 또는 hello WebJobs 안정적으로 실행 되지 않을 수 있습니다. 자세한 내용은 [연속형 WebJob 만들기](web-sites-create-web-jobs.md#CreateContinuous)를 참조하세요.

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>웹 응용 프로그램에 대 한 hello 아웃 바운드 IP 주소 가져오기

웹 앱에 대 한 아웃 바운드 IP 주소의 tooget hello 목록:

1. Azure 포털에서 웹 앱 블레이드를 사용 하 여 hello 이동 toohello **속성** 메뉴.
2. **아웃바운드 IP 주소**를 검색합니다.

아웃 바운드 IP 주소의 hello 목록이 표시 됩니다.

웹 사이트에서에서 호스팅되는 경우 앱 서비스 환경 powerapps의 경우 toolearn 어떻게 tooget 아웃 바운드 IP 주소, 참조 [아웃 바운드 네트워크 주소](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses)합니다.

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>내 웹앱에 대한 예약되거나 전용인 인바운드 IP 주소를 어떻게 확인하나요?

tooset 전용 또는 예약 된 IP 주소에 대 한 인바운드 호출 tooyour Azure 응용 프로그램 웹 사이트를 설치 하 고 IP 기반 SSL 인증서를 구성 합니다.

해당 toouse 전용된 또는 인바운드 통화에 대 한 예약 된 IP 주소, 앱 서비스 계획은 기본 또는 더 높은 서비스 계획에 있어야 합니다.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>내보낼 수 있습니까 외부 Azure 앱 서비스 인증서 toouse 내 다른 곳에서 호스팅되는 웹 사이트에 대 한 같은? 

App Service Certificate는 Azure 리소스로 간주합니다. Azure 서비스 외부 의도 한 toouse 하지 않습니다. 이러한 Azure 외부 toouse를 내보낼 수 없습니다. 자세한 내용은 [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)(App Service Certificate 및 사용자 지정 도메인에 대한 FAQ)를 참조하세요.

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>내 앱 서비스 인증서 toouse 다른 Azure 클라우드 서비스와 함께 내보낼 수 있습니까?

hello 포털 Azure 키 자격 증명 모음 tooApp 서비스 응용 프로그램을 통해 한 앱 서비스 인증서를 배포 하기 위한 첫 번째 클래스 경험을 제공 합니다. 그러나 우리 받았다고 toouse 고객의에서 요청을 응용 프로그램 s 서비스 플랫폼 hello 외부 이러한 인증서 예를 들어 Azure 가상 컴퓨터와 함께 합니다. 다른 Azure 리소스와 hello 인증서를 사용할 수 있도록 toocreate 앱 서비스의 로컬 PFX 복사본의 인증서 방법을 toolearn 참조 [앱 서비스 인증서의 로컬 PFX 복사본을 만들](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/)합니다.

자세한 내용은 [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)(App Service Certificate 및 사용자 지정 도메인에 대한 FAQ)를 참조하세요.


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>웹 응용 프로그램을 tooback 하려고 하면 "부분적으로 성공 했습니다" hello 메시지 나타나는 이유는 무엇입니까?

백업 오류는 일반적인 원인은 hello 응용 프로그램에서 사용 중인 일부 파일입니다. 파일에서에서 사용 하는 hello 백업을 수행 하는 동안 잠깁니다. 이로 인해 이러한 파일이 백업되지 않아 “부분적으로 성공” 상태가 될 수 있습니다. Hello 백업 프로세스에서 파일을 제외 하 여 이러한 잠재적으로 방지할 수 있습니다. Tooback 필요한 것을 선택할 수 있습니다. 자세한 내용은 참조 [Azure 웹 앱을 사용 하 여 사이트의 중요 한 부분 hello 방금 백업](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/)합니다.

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Hello HTTP 응답에서에서 헤더를 제거 하려면 어떻게 합니까?

hello HTTP 응답에서에서 tooremove hello 헤더 사이트의 web.config 파일을 업데이트 합니다. 자세한 내용은 [Remove standard server headers on your Azure websites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)(Azure Websites에서 표준 서버 헤더 제거)를 참조하세요.

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>App Service는 PCI Standard 3.0 및 3.1 규격인가요?

현재 hello 웹 응용 프로그램의 Azure 앱 서비스 기능은 준수 PCI 데이터 보안 DSS (표준) 버전 3.0 수준 1입니다. PCI DSS 버전 3.1은 계획되어 있습니다. 계획은 이미 진행 되 고 최신 표준 hello 단기간 어떻게 진행 됩니다에 대 한 합니다.

PCI DSS 버전 3.1 인증을 적용하려면 TLS(전송 계층 보안) 1.0을 사용하지 않도록 설정해야 합니다. 현재 TLS 1.0을 사용하지 않도록 설정하는 것은 대부분 App Service 계획에 대한 옵션입니다. 그러나 앱 서비스 환경을 사용 하거나 여러 기꺼이 toomigrate 프로그램 작업 부하 tooApp 서비스 환경, 환경 제어를 강화를 얻을 수 있습니다. 여기에는 Azure 지원에 문의하여 TLS 1.0을 사용하지 않도록 설정하는 작업이 포함됩니다. 가까운 미래 hello, 이러한 설정에 액세스할 수 있는 toousers toomake 계획 했습니다.

자세한 내용은 [Microsoft Azure App Service web app compliance with PCI Standard 3.0 and 3.1](https://support.microsoft.com/help/3124528)(Microsoft Azure App Service 웹앱과 PCI Standard 3.0 및 3.1의 호환 여부)을 참조하세요.

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>환경 및 배포 슬롯을 준비 하는 hello를 사용 하려면 어떻게 해야 합니까?

웹 앱 tooApp 서비스를 배포할 때 표준 및 프리미엄 앱 서비스 계획에 toohello 기본 프로덕션 슬롯만 대신 별도 배포 슬롯 tooa를 배포할 수 있습니다. 배포 슬롯은 자체 호스트 이름을 갖춘 라이브 웹앱입니다. 웹 응용 프로그램 콘텐츠 및 구성 요소는 hello 프로덕션 슬롯을 포함 하 여 두 배포 슬롯 간에 교환할 수 있습니다.

배포 슬롯 사용에 대한 자세한 내용은 [App Service에서 스테이징 환경 설정](web-sites-staged-publishing.md)을 참조하세요.

## <a name="how-do-i-access-and-review-webjob-logs"></a>WebJob 로그에 액세스하고 이를 검토하려면 어떻게 해야 하나요?

tooreview WebJob을 기록합니다.

1. Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
2. Hello WebJob을 선택 합니다.
3. 선택 hello **토글 출력** 단추입니다.
4. toodownload hello 출력 파일을 선택 하는 hello **다운로드** 링크 합니다.
5. 개별 실행의 경우 **Individual Invoke**(개별 호출)를 선택합니다.
6. 선택 hello **토글 출력** 단추입니다.
7. 선택 hello 다운로드 링크입니다.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>SQL Server와 함께 toouse 하이브리드 연결 려 합니다. 표시 되는 이유 hello 메시지 "System.OverflowException: 산술 연산에서 오버플로가 발생 했습니다"?

하이브리드 연결 tooaccess SQL Server를 사용 하는 경우 2016 년 5 월 10 일에 대 한 Microsoft.NET 업데이트 연결 toofail을 발생할 수 있습니다. 다음 메시지가 표시될 수 있습니다.

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>해결 방법

이 문제 tooupdate 하이브리드 연결 관리자 toofix 했으며 중입니다. 해결 방법은 [Hybrid Connections error with SQL Server: System.OverflowException: Arithmetic operation resulted in an overflow](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/)(SQL Server의 하이브리드 연결 오류: System.OverflowException: 산술 연산으로 인해 오버플로가 발생했습니다.)를 참조하세요.

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>URL 다시 쓰기 규칙을 어떻게 추가하거나 편집할 수 있나요?

tooadd 또는 URL 다시 쓰기 규칙 편집:

1. 앱 서비스 웹 앱 tooyour 연결 되도록 인터넷 정보 서비스 (IIS) 관리자를 설정 합니다. tooconnect tooApp IIS 관리자 서비스를 확인 하려면 어떻게 toolearn [IIS 관리자를 사용 하 여 Azure 웹 사이트의 원격 관리](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/)합니다.
2. IIS 관리자에서 URL 다시 쓰기 규칙을 추가하거나 편집합니다. 어떻게 tooadd 또는 편집은 URL 다시 쓰기 규칙을 toolearn 참조 [hello URL에 대 한 다시 쓰기 규칙을 만들도록 재작성 모듈](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)합니다.

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>인바운드 트래픽을 tooApp 서비스를 제어 하는 방법

Hello 사이트 수준에서 인바운드 트래픽을 tooApp 서비스를 제어 하기 위한 두 가지 옵션을 선택할:

* 동적 IP 제한을 켭니다. 동적 IP 제한에서 tooturn 참조 toolearn [Azure 웹 사이트에 대 한 IP 및 도메인 제한](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/)합니다.
* 모듈 보안을 켭니다. 모듈 보안 tooturn 참조 toolearn [Azure 웹 사이트에서 웹 응용 프로그램 방화벽 ModSecurity](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/)합니다.

App Service Environment를 사용할 경우 [Barracuda 방화벽](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/)을 사용할 수 있습니다.

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>App Service 웹앱에서 포트를 어떻게 차단하나요?

Hello 앱 서비스 공유 테 넌 트 환경, 아니므로 가능한 tooblock 특정 포트 hello 인프라의 hello 특성으로 인해 합니다. Visual Studio 원격 디버깅을 위해 TCP 포트 4016, 4018 및 4020이 열릴 수도 있습니다.

App Service Environment에서는 인바운드 및 아웃바운드 트래픽을 완벽하게 제어할 수 있습니다. 네트워크 보안 그룹 toorestrict 또는 블록 특정 포트를 사용할 수 있습니다. App Service Environment에 대한 자세한 내용은 [Introducing App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/)(App Service Environment 소개)를 참조하세요.

## <a name="how-do-i-capture-an-f12-trace"></a>F12 추적을 어떻게 캡처하나요?

F12 추적을 캡처할 수 있는 두 가지 옵션이 있습니다.

* F12 HTTP 추적
* F12 콘솔 출력

### <a name="f12-http-trace"></a>F12 HTTP 추적

1. Internet Explorer에서 tooyour 웹 사이트를 이동 합니다. 것이 중요 한 toosign 전에 다음 단계를 hello 수행 합니다. 그렇지 않으면 hello F12 추적 중요 한 로그인 데이터를 캡처합니다.
2. F12 키를 누릅니다.
3. 해당 hello 확인 **네트워크** 탭을 선택한 다음 선택 hello 녹색 **재생** 단추입니다.
4. Hello 문제를 재현 하는 단계를 hello지 않습니다.
5. 빨간색 선택 hello **중지** 단추입니다.
6. 선택 hello **저장** (디스크 아이콘) 단추를 클릭 한 hello HAR 파일 (가장자리 고) 응용 프로그램에서 저장 *또는* hello HAR 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **콘텐츠로 HAR로 저장** 드 ( chrome).

### <a name="f12-console-output"></a>F12 콘솔 출력

1. 선택 hello **콘솔** 탭 합니다.
2. 0 개 이상의 항목이 포함 된 각 탭에 대 한 hello 탭을 선택 합니다 (**오류**, **경고**, 또는 **정보**). Hello 탭을 선택 하지 않으면 hello 탭 아이콘 인지 회색 검정 hello 그 밖으로 커서를 이동 합니다.
3. Hello 메시지 hello 창의 영역을 마우스 오른쪽 단추로 클릭 한 다음 선택 **모든 복사**합니다.
4. 붙여넣기 hello 파일에서 텍스트를 복사 하 고 hello 파일을 저장 합니다.

HAR 파일 tooview hello를 사용할 수 있습니다 [HAR 뷰어](http://www.softwareishard.com/har/viewer/)합니다.

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>왜 오류가 때 tooconnect 앱 서비스 웹 앱 tooa 가상 네트워크를 연결 된 tooExpressRoute?

Tooconnect는 Azure 웹 앱 tooa 가상 네트워크를 ExpressRoute tooAzure가 연결을 시도 하면 실패 합니다. hello 다음과 같은 메시지가 나타납니다. "게이트웨이 is (VPN 게이트웨이."

현재 지점-사이트 VPN 연결 tooa 가상 네트워크를 연결 된 tooExpressRoute 가질 수 없습니다. 지점-사이트 VPN 및 express 경로 공존할 수 없으며 hello에 대 한 동일한 가상 네트워크입니다. 자세한 내용은 [ExpressRoute 및 사이트 간 VPN 연결 제한 및 제한 사항](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations)을 참조하세요.

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>앱 서비스 웹 앱 tooa 가상 네트워크를 정적 라우팅 (정책 기반) 게이트웨이 연결 하는 방법

현재는 앱 서비스 웹 앱 tooa 가상 네트워크를 정적 라우팅 (정책 기반) 게이트웨이 연결도 지원 되지 않습니다. 대상 가상 네트워크가 이미 있는 경우 지점-사이트 VPN 먼저 사용 하도록 설정, 동적 라우팅 게이트웨이 통해 연결 된 tooan 앱이 될 수 있어야 합니다. 게이트웨이가 라우팅을 toostatic 설정 되 면 지점-사이트 VPN을 사용할 수 없습니다. 

자세한 내용은 [Azure 가상 네트워크에 앱 통합](web-sites-integrate-with-vnet.md#getting-started)을 참조하세요.

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>내 App Service Environment에서 두 명의 작업자를 사용할 수 있는데 하나의 App Service 계획만 만들 수 있는 이유는 무엇인가요?

tooprovide 내결함성, 앱 서비스 환경 각 작업자 풀에 추가 계산 리소스를 하나 이상 필요 함이 필요 합니다. 작업 hello 추가 계산 리소스를 할당할 수 없습니다.

자세한 내용은 참조 [어떻게 toocreate 앱 서비스 환경](app-service-web-how-to-create-an-app-service-environment.md)합니다.

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>앱 서비스 환경 toocreate 때 시간 제한을 나타나는 이유는 무엇입니까?

경우에 따라 App Service Environment 만들기에 실패합니다. 이 경우 hello 다음 hello 활동 로그에 오류가 표시 됩니다.
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve이 none hello 다음 조건을 충족 되는지 확인 하십시오.
* hello 서브넷이 너무 작습니다.
* hello 서브넷 비어 있지 않습니다.
* ExpressRoute 앱 서비스 환경의 hello 네트워크 연결 요구 사항을 방지합니다.
* 잘못 된 네트워크 보안 그룹에 앱 서비스 환경의 hello 네트워크 연결 요구 사항을 방지합니다.
* 강제 터널링이 켜져 있습니다.

자세한 내용은 [Frequent issues when deploying (creating) a new Azure App Service Environment](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/)(새 Azure App Service Environment를 배포할(만들) 때 자주 발생하는 문제)를 참조하세요.

## <a name="why-cant-i-delete-my-app-service-plan"></a>내 App Service 계획을 삭제할 수 없는 이유는 무엇인가요?

앱 서비스 계획 hello와 연결 된 모든 앱 서비스 앱 하는 경우 앱 서비스 계획을 삭제할 수 없습니다. 앱 서비스 계획을 삭제 하기 전에 hello 앱 서비스 계획에서에서 연결 된 모든 앱 서비스 앱을 제거 합니다.

## <a name="how-do-i-schedule-a-webjob"></a>WebJob을 예약하려면 어떻게 하나요?

Cron 식을 사용하여 예약된 WebJob을 만들 수 있습니다.

1. settings.job 파일을 만듭니다.
2. 이 JSON 파일에서 Cron 식을 사용하여 일정 속성을 포함합니다. 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

예약된 WebJob에 대한 자세한 내용은 [Cron 식을 사용하여 예약된 WebJob 만들기](web-sites-create-web-jobs.md#CreateScheduledCRON)를 참조하세요.

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>내 App Service 앱에 대한 침투 테스트를 수행하려면 어떻게 하나요?

tooperform 침투 테스트 [요청을 제출](https://security-forms.azure.com/penetration-testing/terms)합니다.

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Traffic Manager를 사용하는 App Service 웹앱에 대한 사용자 지정 도메인 이름을 구성하려면 어떻게 하나요?

toouse Azure 트래픽 관리자를 사용 하 여 부하 분산을 앱 서비스 앱과 사용자 지정 도메인 이름을 확인 하려면 어떻게 해야 toolearn [트래픽 관리자와 함께 Azure 웹 앱에 대 한 사용자 지정 도메인 이름 구성](web-sites-traffic-manager-custom-domain-name.md)합니다.

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>내 App Service Certificate에 사기 플래그가 지정되었습니다. 이 문제를 해결하려면 어떻게 해야 하나요?

앱 서비스 인증서 구매 hello 도메인 확인을 하는 동안 hello 메시지의 뒤에 표시 될 수 있습니다.

“인증서가 사기성이 있을 수 있다고 플래그 지정되었습니다. hello 요청 현재 검토 중입니다. 24 시간 이내 hello 인증서를 사용할 수 있는 상태가 되지 않는, 하십시오 Azure 지원에 문의 합니다. "

Hello 메시지 나타나듯이이 사기 행위 확인 프로세스 too24 시간 toocomplete 걸릴 수도 있습니다. 이 시간 동안 계속 해 서 toosee hello 메시지입니다.

앱 서비스 인증서 tooshow이이 메시지를 후 계속 24 시간 동안 hello 다음 PowerShell 스크립트를 실행 하십시오. hello 스크립트 연락처 hello [인증서 공급자](https://www.godaddy.com/) 직접 tooresolve hello 문제입니다.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>App Service에서 인증 및 권한 부여가 어떻게 작동하나요?

App Service의 인증 및 권한 부여에 대한 자세한 문서는 [App Service 보안](../app-service/app-service-security-readme.md)을 참조하세요. 또한 한 정보를 hello 설명서 공급자 로그인 식별 다양 한 앱 서비스 toouse 설정에 대 한:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Microsoft 계정](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>리디렉션하는 방법 hello 기본 *. azurewebsites.net 도메인 toomy Azure 웹 앱의 사용자 지정 도메인?

Azure에서 기본 웹 응용 프로그램을 사용 하 여 새 웹 사이트를 만들 때 *sitename*. azurewebsites.net 도메인이 tooyour 사이트를 할당 합니다. 사용자 지정 호스트 이름 tooyour 사이트를 추가 하 고 사용자의 기본 사용자 toobe 수 tooaccess 않을 *. azurewebsites.net 도메인 hello 기본 URL을 리디렉션할 수 있습니다. toolearn tooredirect 모든 웹 사이트의 기본 도메인 tooyour 사용자 지정 도메인에서 트래픽을 참조 [hello 기본 도메인 tooyour 사용자 지정의 리디렉션 도메인을 Azure 웹 앱](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/)합니다.

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>App Service에 어떤 .NET 버전이 설치되어 있는지 확인하려면 어떻게 하나요?

hello 가장 빠른 방법은 toofind hello 버전의 Microsoft.NET 응용 프로그램 서비스에 설치 된 hello Kudu 콘솔을 사용 하는 것입니다. Hello 포털 또는 앱 서비스 앱의 URL을 hello를 사용 하 여 hello Kudu 콘솔에 액세스할 수 있습니다. 자세한 내용은 참조 [Determine hello 설치 된.NET 버전 앱 서비스에서](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/)합니다.

## <a name="why-isnt-autoscale-working-as-expected"></a>자동 크기 조정이 예상대로 작동하지 않는 이유는 무엇인가요?

Azure 자동 크기 조정에서 확장 되지 않은 경우 원하는 대로 hello 웹 응용 프로그램 인스턴스를 확장할 실행 중일 수 있습니다 시나리오는 의도적으로 선택 되지 tooscale tooavoid 너무 "플 래핑." 인해 무한 루프에 이 문제는 일반적으로 적절 한 여백 hello 수평 확장 및 확장에서 임계값 사이의 없을 때 발생 합니다. tooavoid "플 래핑" 및 기타 자동 크기 조정 모범 사례에 대 한 tooread 참조 toolearn [자동 크기 조정에 대 한 유용한 정보](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices)합니다.

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>때때로 자동 크기 조정이 부분적으로만 크기를 조정하는 이유는 무엇인가요?

자동 크기 조정은 메트릭이 미리 구성된 경계를 초과할 경우 트리거됩니다. 경우에 따라 hello 용량 예상 비교 toowhat 부분적 으로만 채워지는지 나타날 수 있습니다. 원하는 인스턴스 hello 수를 사용할 수 없는 경우 발생할 수 있습니다. 이 시나리오에서 자동 크기 조정 부분적으로 hello 사용 가능한 인스턴스 수를 사용 하 여 채웁니다. 자동 크기 조정 실행 hello를 리 밸런스 논리 tooget 용량을 더 합니다. Hello 남은 인스턴스를 할당 합니다. 이 작업에는 몇 분이 걸릴 수 있습니다.

Hello 부분 다시 채우기가 충분 한 toobring hello 메트릭을 hello 경계 내 인스턴스 수가 예상 hello 보이지 않으면 몇 분 후 수 있습니다. 또는 자동 크기 조정 hello 하위 메트릭 경계에 도달 했으므로 축소 있을 수 있습니다.

이러한 조건 중 되지 않는 경우 hello 문제가 계속 되 면, 지원 요청을 제출 합니다.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>내 콘텐츠에 대해 HTTP 압축을 켜려면 어떻게 하나요?

정적 및 동적 콘텐츠 형식에 대 한 압축에 tooturn hello 다음 코드 toohello 응용 프로그램 수준 web.config 파일을 추가 합니다.

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

또한 특정 동적 hello를 지정할 수 하 고 정적 MIME toocompress 원하는 됩니다. 자세한 내용은 우리의 응답 tooa 포럼에 질문을 참조 하십시오. [간단한 Azure 웹 사이트에서 httpCompression 설정을](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview)합니다.

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>온-프레미스 환경 tooApp 서비스에서에서 마이그레이션하려면 어떻게 해야 합니까?

Windows 및 Linux 웹 서버 tooApp 서비스에서에서 toomigrate 사이트를 사용할 수 있습니다 Azure 앱 서비스 Migration Assistant. 필요에 따라 Azure에 웹 응용 프로그램 및 데이터베이스를 생성 하 고 hello 콘텐츠를 게시 하는 hello 마이그레이션 도구입니다. 자세한 내용은 [Azure App Service Migration Assistant](https://www.movemetothecloud.net/)를 참조하세요.
