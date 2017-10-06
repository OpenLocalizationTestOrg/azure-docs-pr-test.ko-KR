---
title: "Azure AD 응용 프로그램 프록시를 통해 원격 데스크톱 aaaPublish | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항에 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 원격 데스크톱 게시

이 문서에서는 어떻게 toodeploy 서비스 RDS (원격 데스크톱) 응용 프로그램 프록시를 통해 원격 사용자 생산성 이루어질 수 있도록 합니다.

이 문서에 대 한 대상 그룹은 대상 사용자는 hello.
- 현재 Azure AD 응용 프로그램 프록시 하려는 고객 toooffer 더 많은 응용 프로그램 tootheir 최종 사용자가 원격 데스크톱 서비스를 통해 온-프레미스 응용 프로그램을 게시 하 여 합니다.
- Azure AD 응용 프로그램 프록시를 사용 하 여 배포의 tooreduce hello 공격 노출 하려는 현재 원격 데스크톱 서비스 고객 합니다. 이 시나리오에서는 2 단계 인증의 제한 된 집합을 제공 하 고 조건부 액세스 tooRDS를 제어 합니다.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>응용 프로그램 프록시 hello 표준 RDS 배포에 적용 되는 방식

표준 RDS 배포에는 Windows Server에서 실행되는 다양한 원격 데스크톱 역할 서비스가 포함됩니다. Hello를 살펴보면 [원격 데스크톱 서비스 아키텍처](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), 여러 배포 옵션이 있습니다. 가장 눈에 띄는 차이점 hello hello [Azure AD 응용 프로그램 프록시 RDS 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (hello 다음 다이어그램에에서 표시) hello 다른 배포 옵션은 해당 hello 응용 프로그램 프록시 시나리오에는 영구적이 아웃 바운드 및 hello 커넥터 서비스를 실행 하는 hello 서버에서 연결입니다. 기타 배포에서는 부하 분산 장치를 통해 열린 인바운드 연결을 유지합니다.

![RDS VM hello와 공용 인터넷 hello 간 응용 프로그램 프록시가 위치](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

RDS 배포에서 hello RD 웹 역할 및 hello RD 게이트웨이 역할 인터넷 연결 컴퓨터에서 실행 됩니다. 이러한 끝점은 다음의 이유로 hello에 노출 됩니다.
- 보기 hello 다양 한 온-프레미스 응용 프로그램 및 데스크톱에 액세스할 수 있습니다 및 RD 웹의 공용 끝점 toosign hello 사용자를 제공 합니다. 리소스를 선택 하면 hello 네이티브 앱을 사용 하 여 hello 운영 체제에 대 한 RDP 연결 생성 됩니다.
- RD 게이트웨이 사용자가 hello RDP 연결 되 면 hello 그림으로 도착 합니다. RD 게이트웨이 hello hello 인터넷을 통해 들어오는 hello 암호화 RDP 트래픽을 처리 및 toohello 사용자 hello 온-프레미스 서버를 통해 연결 하는 변환입니다. 이 시나리오에서는 RD 게이트웨이 받고 hello 트래픽 hello hello Azure AD 응용 프로그램 프록시에서에서 제공 됩니다.

>[!TIP]
>이전에 RDS를 배포 하지 않은 하거나 시작 하기 전에 자세한 정보를 원하는 경우 너무 방법을 알아보려면[원활 하 게 Azure 리소스 관리자 및 Azure 마켓플레이스와 RDS 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)합니다.

## <a name="requirements"></a>요구 사항

- RD 웹 hello 둘 다 및 끝점에 위치 해야 하는 RD 게이트웨이 hello 시스템과 공통 루트와 동일 합니다. RD 게이트웨이 및 RD 웹 hello 두 응용 프로그램 간에 single sign-on 환경을 가질 수 있도록 단일 응용 프로그램으로 게시 됩니다.

- 이미 [RDS를 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)하고 [응용 프로그램 프록시를 사용하도록 설정](active-directory-application-proxy-enable.md)했어야 합니다.

- 이 시나리오 hello RD 웹 페이지를 통해 연결 하는 Windows 7 또는 Windows 10 데스크톱에서 최종 사용자가 Internet Explorer를 통해 이동 하는 것으로 가정 합니다. 다른 운영 체제 toosupport 해야 할 경우 참조 [다른 클라이언트 구성에 대 한 지원을](#support-for-other-client-configurations)합니다.

  >[!NOTE]
  >Windows 10 Creator's Update는 현재 지원되지 않습니다.

- Internet Explorer에서 hello RDS ActiveX 추가 기능을 활성화 합니다.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Hello joint RDS 및 응용 프로그램 프록시 시나리오를 배포 합니다.

RDS 및 사용자 환경에 대 한 Azure AD 응용 프로그램 프록시를 설정한 후 hello 단계 toocombine hello 두 가지 솔루션을 따릅니다. 이러한 단계는 응용 프로그램으로 hello 두 개의 웹 RDS 끝점 (RD 웹 및 RD 게이트웨이)을 게시 하 고 다음 응용 프로그램 프록시를 통해 프로그램 RDS toogo에 트래픽을 보내는 안내 합니다.

### <a name="publish-hello-rd-host-endpoint"></a>Hello RD 호스트 끝점을 게시

1. [새 응용 프로그램 프록시 응용 프로그램 게시](application-proxy-publish-azure-portal.md) 다음 값에는 hello로:
   - 내부 URL: https://\<rdhost\>.com / 여기서 \<rdhost\> RD 게이트웨이 및 RD 웹 공유 하는 hello 공통 루트입니다.
   - 외부 URL:이 필드는 자동으로 채워지며 hello 응용 프로그램의 hello 이름에 따라 있지만 수정할 수 있습니다. Rds.에 액세스할 때 사용자에 게 toothis URL 되돌려집니다.
   - 사전 인증 방법: Azure Active Directory
   - URL 헤더 변환: 아니요
2. 사용자 할당 toohello RD 응용 프로그램을 게시 합니다. 액세스 tooRDS 너무가 모두 있는지 확인 합니다.
3. Hello single sign-on 방법으로 hello 응용 프로그램에 대 한 둡니다 **Azure AD에서 single sign-on 사용 하지 않도록 설정**합니다. Tooauthenticate 프로그램 사용자에 게 요청 하 고 나면 AD tooAzure를 한 번 tooRD 웹, 하지만 single sign on tooRD 게이트웨이 합니다.
4. 너무 이동**Azure Active Directory** > **앱 등록** > *응용 프로그램* > **설정**.
5. 선택 **속성** 및 업데이트 hello **홈 페이지 URL** 필드 toopoint tooyour RD 웹 끝점 (https:// 같은\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>직접 RDS 트래픽 tooApplication 프록시

관리자 권한으로 toohello RDS 배포를 연결 하 고 hello 배포에 대 한 hello RD 게이트웨이 서버 이름을 변경 합니다. 이렇게 하면 연결 hello Azure AD 응용 프로그램 프록시를 통과 합니다.

1. Hello RD 연결 브로커 역할을 실행 하는 toohello RDS 서버를 연결 합니다.
2. **서버 관리자**를 시작합니다.
3. 선택 **원격 데스크톱 서비스** hello hello 왼쪽 창에서.
4. **개요**를 선택합니다.
5. 배포 개요 섹션 hello에서 hello 드롭다운 메뉴를 선택 하 고 선택 **배포 속성 편집**합니다.
6. Hello RD 게이트웨이 탭에서 변경 hello **서버 이름** 필드 toohello hello RD 호스트 끝점 응용 프로그램 프록시에 대해 설정 하는 외부 URL입니다.
7. 변경 hello **메서드 로그온** 너무 필드**암호 인증**합니다.

  ![RDS의 배포 속성 화면](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. 각 컬렉션에 대 한 hello 다음 명령을 실행 합니다. *\<yourcollectionname\>* 및 *\<proxyfrontendurl\>*을 사용자 고유의 정보로 바꿉니다. 이 명령은 RD 웹과 RD 게이트웨이 간에 Single Sign-On을 사용하도록 설정하고 성능을 최적화합니다.

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **예:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. hello 다음 명령을 실행 하는이 컬렉션에 대해 RDWeb에서 다운로드할 수 있는 보기 hello RDP 파일 내용을 뿐만 아니라 사용자 지정 RDP 속성 hello tooverify hello 수정:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

원격 데스크톱을 구성 했으므로, Azure AD 응용 프로그램 프록시로 전송.rds 입니다의 hello 인터넷 구성 요소로 제거할 수 있습니다 hello RD 웹 및 RD 게이트웨이 컴퓨터에서 다른 공용 인터넷 연결 끝점입니다.

## <a name="test-hello-scenario"></a>테스트 hello 시나리오

Windows 7 또는 10 컴퓨터에서 Internet Explorer로 hello 시나리오를 테스트 합니다.

1. Toohello 외부 URL을 설정 하거나 hello에 응용 프로그램을 찾고 [MyApps 패널](https://myapps.microsoft.com)합니다.
2. Tooauthenticate tooAzure Active Directory는 단계가 있습니다. Toohello 응용 프로그램을 할당 하는 계정을 사용 합니다.
3. Tooauthenticate tooRD 웹은 단계가 있습니다.
4. RDS 인증이 성공 하면 hello 데스크톱 또는 응용 프로그램 및 ְ ֳ  선택할 수 있습니다.

## <a name="support-for-other-client-configurations"></a>다른 클라이언트 구성에 대한 지원

이 문서에 설명 된 hello 구성은 Windows 7 또는 10, Internet Explorer 및 hello RDS ActiveX 추가 기능에서 사용자입니다. 그러나 필요한 경우 다른 운영 체제 또는 브라우저를 지원할 수 있습니다. hello 인증 방법을 사용 하는 hello 다릅니다.

| 인증 방법 | 지원되는 클라이언트 구성 |
| --------------------- | ------------------------------ |
| 사전 인증    | Internet Explorer + RDS ActiveX 추가 기능을 사용하는 Windows 7/10 |
| 통과 | Hello Microsoft 원격 데스크톱 응용 프로그램을 지 원하는 다른 운영 체제 |

hello 사전 인증 흐름 hello 통과 흐름 보다 많은 보안 혜택을 제공 합니다. 사전 인증을 사용하면 온-프레미스 리소스에 대해 Single Sign-On, 조건부 액세스 및 2단계 인증과 같은 Azure AD 인증 기능을 활용할 수 있습니다. 또한 인증된 트래픽만 네트워크에 도달하도록합니다.

toouse 통과 인증, 있습니다이 문서에 나열 된 두 가지 수정 사항을 toohello 단계:
1. [hello RD 호스트 끝점을 게시](#publish-the-rd-host-endpoint) 1 단계, 너무 hello 사전 인증 방법을 설정**통과**합니다.
2. [직접 RDS tooApplication 프록시 트래픽](#direct-rds-traffic-to-application-proxy), 완전히 8 단계를 건너뜁니다.

## <a name="next-steps"></a>다음 단계

[원격 액세스 tooSharePoint Azure AD 응용 프로그램 프록시를 사용 하도록 설정](application-proxy-enable-remote-access-sharepoint.md)  
[Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항](application-proxy-security-considerations.md)
