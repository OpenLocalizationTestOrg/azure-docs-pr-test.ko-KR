---
title: aaaAzure RemoteApp FAQ | Microsoft Docs
description: "Azure RemoteApp에 대 한 대답 toohello 가장 자주 묻는 질문에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Azure RemoteApp FAQ
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

에서는 Azure RemoteApp에 대 한 질문을 따라 hello를 적입니다. 다른 질문이 있을 경우 Hello 방문 [RemoteApp 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) 알려주세요 무엇 tooknow, 필요 하거나 주석을 아래 드롭다운 목록입니다.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>원하는 항목을 찾을 수 없나요? 답하지 않은 질문이 있나요?
Hello 정보를 찾을 수 없는 경우 필요한 또는 म 여기 설명 하지는 하는 추가 질문이, toohello 이동 하십시오 [Azure a p p 포럼](http://aka.ms/araforum) 질문에 게 요청 합니다. 여기에 더 많은 답을 추가할 수 있습니다.

## <a name="what-is-azure-remoteapp"></a>Azure RemoteApp이란?
* **Azure RemoteApp이란?** RemoteApp은 Azure 서비스를 사용 하면 다양 한 사용자 장치에서 안전 하 게 원격 액세스 tooapplications를 제공 합니다. [Azure RemoteApp](remoteapp-whatis.md)에 대해 더 알아봅니다.
* **Hello 배포 옵션은 무엇입니까?** RemoteApp 컬렉션의 두 가지 종류는 클라우드 및 하이브리드입니다. 도메인 가입을 해야 하는지 여부와 같은 요인에 따라 필요한 것이 달라집니다. [여기](remoteapp-collections.md)에서 이러한 모든 결정에 대해 이야기합니다.

## <a name="quick-tips-on-using-azure-remoteapp"></a>Azure RemoteApp 사용에 대한 빠른 팁
* **연결이 끊길 때까지 시간이 얼마나 남았나요? 시간 내가 수 유휴 필자가 hello 부팅 전에 무엇입니까?** 4시간입니다. 사용자 또는 사용자 일부가 4시간 동안 유휴 상태인 경우 Azure RemoteApp에서 자동으로 로그아웃됩니다. 체크 아웃의 다른 기본 설정 hello [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)합니다.
* **이 서비스를 무료로 사용해 볼 수 있나요?** 예. 30일 동안 사용할 수 있는 평가판이 있습니다. Hello 평가판이 만료 된 후 유료 계정 (프로덕션 환경에서 사용할 수 있습니다) 또는 hello 서비스를 사용 하 여 중지 tooa를 전환할 수 있습니다. 너무 이동 하 여 무료 평가판 시작[portal.azure.com](http://portal.azure.com) -RemoteApp의 새 인스턴스를 만듭니다. Hello 무료 평가판으로 인스턴스당 10 명의 사용자가 RemoteApp의 2 개의 인스턴스를 만들 수 있습니다. 이 평가판은 30일 동안만 사용할 수 있습니다.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Azure RemoteApp 구독 세부 정보
* **Hello 서비스 제한 사항은 무엇입니까?** Hello 기본 설정을 확인 하 고 서비스에서 Azure RemoteApp의 제한 수 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)합니다. 추가 질문이 있으면 알려주세요.
* **사용자 수 수행 toohave 있습니까?** 최소 20명의 사용자입니다. 직접 toobe super 지우기-hello 최소는 20을 반복 합니다. 20명에 대한 비용이 청구됩니다. 
* **RemoteApp 비용은 얼마인가요?** [Azure RemoteApp 가격 정보 ](https://azure.microsoft.com/pricing/details/remoteapp/)에 대한 더 알아봅니다.
* **한 가지 형식의 컬렉션이 다른 것 보다 비용이 듭니까?** 예, 컬렉션 요구 사항에 따라 다를 수 있습니다. Azure RemoteApp tooyour 온-프레미스 네트워크에서 연결을 해야 하는 하이브리드 컬렉션입니다. 기존 VNET/Express 경로를 사용하면 추가 비용이 없습니다. 청구 hello에 대 한 됩니다 새 Azure VNET 및 게이트웨이 또는 Express 경로 사용 하지만 [VPN 게이트웨이](https://azure.microsoft.com/pricing/details/vpn-gateway) 또는 [Express 경로](https://azure.microsoft.com/pricing/details/expressroute/)합니다. (Hello 링크에 자세히 설명)이이 비용은 월별 Azure RemoteApp 프로그램 맨 위에 비용.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>컬렉션 - 사용해야 하는 지원되는 기능 및 기타 기능
* **사용자 지정 LOB(기간 업무) 응용 프로그램이 지원되나요?** 예. toouse Azure RemoteApp에서 사용자 지정 응용 프로그램 만들기는 [사용자 지정 템플릿 이미지](remoteapp-create-custom-image.md), toohello RemoteApp 컬렉션 업로드 합니다.
* **사용자 지정 LOB 응용 프로그램은 Azure RemoteApp에서 작동 합니까?**  를 tootest 가장 좋은 방법은 toofigure hello 것입니다. 체크 아웃 hello [RD 호환성 센터](http://www.rdcompatibility.com/compatibility/default.aspx)합니다.
* **어느 배포 메서드(클라우드 또는 하이브리드)가 내 조직에 가장 적합한가요?** 하이브리드 컬렉션 경우 안전한 온-프레미스 네트워크 연결을 single sign on (SSO)와 완벽 하 게 통합을 원한다 면 hello 가장 완벽 경험을 제공 합니다. 클라우드 컬렉션 agile 쉽고 tooisolate 배포 여러 인증 방법을 사용 하 여 제공 합니다. Hello에 대 한 자세한 [배포 옵션](remoteapp-whatis.md)합니다.
* **SQL 또는 다른 데이터베이스가 온-프레미스나 Azure에 있습니다. 어떤 배포 유형을 사용해야 하나요?** SQL 또는 백 엔드 데이터베이스의 위치에 따라 달라집니다. Hello 데이터베이스 개인 네트워크에 있으면 hello 하이브리드 컬렉션을 사용 합니다. Hello 데이터베이스는 노출 된 toohello 인터넷 클라이언트 연결 tooconnect tooit 허용을 hello 클라우드 컬렉션을 사용할 수 있습니다.
* **드라이브 매핑, USB 및 직렬 포트, 클립보드 공유 및 프린터 리디렉션이란 무엇인가요?** 모든 해당 기능은 Azure RemoteApp에서 지원됩니다. 클립보드 공유 및 프린터 리디렉션은 기본적으로 설정되어 있습니다. 리디렉션에 대해 [여기](remoteapp-redirection.md)에서 더 알아볼 수 있습니다. 

## <a name="template-images"></a>템플릿 이미지
* **사용할 수 있습니까 기존 가상 컴퓨터 또는 클라우드 hello 템플릿으로 내 RemoteApp 컬렉션에 대 한?** 예! 기반으로 하는 Azure VM 이미지를 만들 하 구독에 포함 된 hello 이미지 중 하나를 사용 하거나 사용자 지정 이미지를 만들 수 있습니다. 체크 아웃 hello [RemoteApp 이미지 옵션](remoteapp-imageoptions.md)합니다.

## <a name="network-options"></a>네트워크 옵션
* **hello 하이브리드 컬렉션 VNET 필요합니다. 기존 VNET을 사용할 수 있습니까?** Hello 기존 VNET이 Azure VNET 할 수 있습니다. 참조 "1 단계: 가상 네트워크를 설정" hello에 [하이브리드 컬렉션 지침](remoteapp-create-hybrid-deployment.md) 자세한 정보에 대 한 합니다.
* **VNET 클라우드 컬렉션과 함께 사용할 수 있습니까?** 할 수 있습니다. [클라우드 컬렉션 만들기](remoteapp-create-cloud-deployment.md), 특히 자세한 내용은 1단계를 확인합니다.

## <a name="authentication-options"></a>인증 옵션
* **인증은 어떻게 처리되나요? 메서드를 지원 하나요?**  hello 클라우드 컬렉션은 Microsoft 계정과 Azure Active Directory 계정에 Office 365 계정에도 지원 합니다. hello 하이브리드 컬렉션은 Azure Active Directory 계정에 동기화 된만 지원 합니다 (같은 도구를 사용 하 여 [Azure Active Directory 동기화](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)); Windows Server Active Directory 배포에서 특히 하거나 동기화 된 hello로 암호 동기화 옵션을 구성 하는 Active Directory Federation Services (AD FS) 페더레이션과 함께 동기화 된 또는 합니다. [MFA(Multi-Factor Authentication)](https://azure.microsoft.com/services/multi-factor-authentication/)를 구성할 수도 있습니다.

> [!NOTE]
> hello Azure Active Directory 사용자 구독와 관련 된 hello 테 넌 트에서 이어야 합니다. (보고 하 고 hello에 가입 내용을 수정 **설정을** hello 포털에서 탭 합니다. 참조 [변경 hello Azure Active Directory 테 넌 트가 RemoteApp에서 사용 하는](remoteapp-changetenant.md) 자세한 정보에 대 한 합니다.)
> 
> 

* **내 Azure Active Directory 계정 액세스를 지정할 수는 이유**  hello Azure Active Directory 사용자 구독와 관련 된 hello 디렉터리에서 이어야 합니다. 확인 하거나 hello 포털에서 hello 설정 탭에서 해당 디렉터리를 수정할 수 있습니다. 참조 [변경 hello Azure Active Directory 테 넌 트가 RemoteApp에서 사용 하는](remoteapp-changetenant.md) 자세한 정보에 대 한 합니다.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>클라이언트-어떤 장치 수 tooaccess Azure RemoteApp을 사용 합니까?
Hello에 서로 다른 클라이언트를 설치 하기 위한 단계를 포함 하는 좋은 클라이언트 정보를 찾을 수 있습니다 [Azure RemoteApp에 앱 액세스](remoteapp-clients.md)합니다.

* **장치 및 운영 체제 hello 클라이언트 응용 프로그램 지원 합니까?**
  첫 번째, hello 컴퓨터 및 태블릿: 
  
  * Windows 10 (클라이언트 미리 보기)
  * Windows 8.1 및 Windows 8
  * Windows 7 서비스 팩 1
  * Mac OS X
  * Windows RT
  * Android 태블릿
  * iPad

    및 hello 전화:
  * iPhone
  * Android 휴대폰
  * Windows Phone
    
    지금 RemoteApp 클라이언트를 [다운로드](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx)하세요.
* **Azure RemoteApp은 씬 클라이언트를 지원하나요?** 예, hello 다음 Windows Embedded 씬 클라이언트 지원 됩니다.
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **어떤 버전의 Windows Server hello RDSH 원격 데스크톱 세션 호스트 ()을 사용할 수 있습니까?** Windows Server 2012 R2입니다.

## <a name="support-and-feedback"></a>지원 및 피드백
* **RemoteApp에 대 한 지원 계획 hello 이란?** 청구 및 구독 관리 지원은 무료로 제공됩니다. 기술 지원은 hello를 통해 제공 됩니다 [Azure 서비스 계획](https://azure.microsoft.com/support/plans/)합니다. [Azure 토론 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp)을 통해 커뮤니티 지원을 무료로 이용할 수도 있습니다. 
* **사용자 의견을 제출하려면 어떻게 해야 하나요?** Hello 방문 [피드백 포럼](https://feedback.azure.com/forums/247748-azure-remoteapp/)합니다.
* **Azure RemoteApp에 대 한 자세한 toolearn와 통신?** 또한 tooour에서 [토론 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp)을 만드는데 좋은 곳 toopost 질문, 매주 hello를 조인할 수 있습니다 [hello 전문가 웹 세미나 요청](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html)RemoteApp 모든 것에 대 한 논의할 합니다.
* **RemoteApp 설명서는 어떤가요?** 질문해 주셔서 감사합니다. 또한 toohello 도움말 hello 포털 도움말 서랍에 콘텐츠 (hello 클릭 **?** 모든 페이지 hello 포털에서), hello 문서 다음에 사용할 수 있는 tooteach RemoteApp에 대 한 있습니다.
  
  * **시작:**
    * [RemoteApp이란?](remoteapp-whatis.md)
    * [Hello RemoteApp 템플릿 이미지에는 무엇입니까?](remoteapp-images.md)
    * [라이선스 작동 방식](remoteapp-licensing.md)
    * [RemoteApp과 Office가 함께 작동하는 방식](remoteapp-o365.md)
    * [RemoteApp에서 리디렉션이 작동하는 방식](remoteapp-redirection.md)
  * **배포:**
    * [사용자 지정 템플릿 이미지 만들기](remoteapp-create-custom-image.md)
    * [하이브리드 컬렉션 만들기](remoteapp-create-hybrid-deployment.md)
    * [클라우드 컬렉션 만들기](remoteapp-create-cloud-deployment.md)
    * [RemoteApp에 대해 Azure Active Directory 구성](remoteapp-ad.md)
    * [RemoteApp에 앱 게시](remoteapp-publish.md)
  * **관리:**
    
    * [사용자 추가](remoteapp-user.md)
    * [RemoteApp 구성 및 사용 모범 사례](remoteapp-bestpractices.md)    
    
    동영상! RemoteApp에 대한 많은 동영상도 있습니다. 일부 문서에서는 소개 ([소개 tooAzure RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) 다른 과정을 단계별로 배포 하는 동안 ([배포 클라우드](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) 및 [하이브리드 배포](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). 지금 확인해 보세요.

### <a name="help-us-help-you"></a>의견 보내기
또한 toorating에이 문서 및 설명 아래로 아래 변경할 수 있는 변경 내용을 toohello 문서 자체 알고 계십니까? 누락된 부분이 있나요? 잘못된 부분이 있나요? 혼동을 줄 수 있는 부분이 있나요? 위로 스크롤 및 클릭 **GitHub에서 편집** toomake 변경-것 나올지 검토를 위해 toous를 다음에 로그 오프 했습니다 되 면 확인할 수 있습니다 프로그램 변경 및 향상 바로 여기 합니다.

