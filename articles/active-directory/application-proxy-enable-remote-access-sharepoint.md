---
title: "Azure AD 응용 프로그램 프록시 aaaEnable 원격 액세스 tooSharePoint | Microsoft Docs"
description: "방법에 대 한 hello 기본 사항에 설명 toointegrate Azure AD 응용 프로그램 프록시는 온-프레미스 SharePoint 서버입니다."
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
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>원격 액세스 tooSharePoint Azure AD 응용 프로그램 프록시를 사용 하도록 설정

이 문서에서는 어떻게 toointegrate Azure Active Directory (Azure AD) 응용 프로그램 프록시는 온-프레미스 SharePoint 서버입니다.

Azure AD 응용 프로그램 프록시 tooenable 원격 액세스 tooSharePoint 단계별이 문서의 hello 섹션을 따라 합니다.

## <a name="prerequisites"></a>필수 조건

이 문서에서는 사용자 환경에 SharePoint 2013 이상이 이미 있다고 가정합니다. 또한 hello 다음 필수 구성 요소를 고려 합니다.

* SharePoint에는 기본 Kerberos 지원을 포함합니다. 따라서 사용자가 Azure AD 응용 프로그램 프록시를 통해 내부 사이트를 원격으로 액세스 되는 단일 로그온 (SSO) 환경을 toohave를 가정할 수 있습니다.

* Toomake 몇 가지 구성 변경 내용을 tooyour SharePoint 서버가 필요 합니다. 스테이징 환경을 사용하는 것이 좋습니다. 이러한 방식으로 먼저 서버를 준비 하는 업데이트 tooyour 만들고 수 다음 프로덕션으로 옮기기 전에 테스트 주기를 용이 하 게 합니다.

* Hello에서 SSL URL을 게시 해야 하기 때문에 이미 설정한 SSL을 SharePoint에 대 한 가정 합니다. 내부 사이트 링크 전송/올바르게 매핑되어 있는지 tooensure toohave SSL을 사용 해야 합니다. SSL을 구성하지 않은 경우 지침에 대해서는 [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013)(SharePoint 2013용 SSL 구성)을 참조하세요. 또한 해야 해당 hello 커넥터 컴퓨터 트러스트 hello 인증서 발급 하는 합니다. (hello 인증서 공개적으로 발급 toobe 필요 하지 않습니다.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>1 단계: tooSharePoint single sign on 설정

고객이 원하는 최상의 SSO 환경을 고 백 엔드 응용 프로그램을 SharePoint 서버에 대 한이 예에서 hello 합니다. 이 일반적인 Azure AD 시나리오에서는 hello 사용자 다시 인증에 대 한 메시지가 표시 되지 것입니다 때문에 한 번만 인증 됩니다.

나 Windows 인증을 사용 해야 하는 온-프레미스 응용 프로그램에 대 한 hello Kerberos 인증 프로토콜 및 Kerberos 제한 위임 (KCD) 이라는 기능을 사용 하 여 SSO를 얻을 수 있습니다. KCD를 구성 하면 windows hello 응용 프로그램 프록시 커넥터 tooobtain 사용 하면 티켓/토큰 사용자가 hello 사용자 tooWindows에 직접 로그인 하지 않은 경우에 합니다. 에 대 한 KCD toolearn 참조 [Kerberos 제한 위임 개요](https://technet.microsoft.com/library/jj553400.aspx)합니다.

SharePoint 서버에서 다음 순차 섹션 hello에 hello 프로시저 사용에 대 한 KCD tooset:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>SharePoint가 서비스 계정으로 실행 중인지 확인

먼저 SharePoint가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스가 아닌 정의된 서비스 계정으로 실행 중인지 확인합니다. 서비스 사용자 이름 (Spn) tooa 올바른 계정을 연결할 수 있도록이 작업을 수행 합니다. Spn은 Kerberos 프로토콜 hello 서로 다른 서비스를 식별 하는 방법입니다. 계정 hello 필요는 및 이상 tooconfigure hello KCD 합니다.

사이트에 정의 된 서비스 계정에서 실행 되는 tooensure hello 다음 단계를 수행 합니다.

1. 열기 hello **SharePoint 2013 중앙 관리** 사이트입니다.
2. 너무 이동**보안** 선택 **서비스 계정 구성**합니다.
3. **웹 응용 프로그램 풀 – SharePoint – 80**을 선택합니다. hello 옵션 약간 달라질 수 있습니다 프로그램 웹 풀의 hello 이름에 따라 또는 웹 풀에서는 기본적으로 SSL을 사용 하는 경우 hello 합니다.

  ![서비스 계정 구성 옵션](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. 경우 **이 구성 요소에 대 한 계정을 선택** 은 **로컬 서비스** 또는 **네트워크 서비스**, toocreate 계정이 필요 합니다. 그렇지 않은 경우 작업이 완료 되 고 toohello 다음 섹션을 이동할 수 있습니다.
5. **새 관리되는 계정을 등록하세요.**를 선택합니다. 사용자 계정을 만든 후에 설정 해야 **웹 응용 프로그램 풀** 전에 hello 계정을 사용할 수 있습니다.

> [!NOTE]
이전에는 toohave 해야 hello 서비스에 대 한 Azure AD 계정을 만든 합니다. 자동 암호 변경을 허용하는 것이 좋습니다. 단계 및 문제 해결 hello 전체 집합에 대 한 자세한 내용은 참조 [SharePoint 2013의 자동 암호 변경 구성할](https://technet.microsoft.com/library/ff724280.aspx)합니다.

### <a name="configure-sharepoint-for-kerberos"></a>Kerberos용 SharePoint 구성

KCD tooperform single sign on toohello SharePoint 서버를 사용 하 고 Kerberos 에서만 작동 합니다.

tooconfigure Kerberos 인증에 대 한 SharePoint 사이트:

1. 열기 hello **SharePoint 2013 중앙 관리** 사이트입니다.
2. 너무 이동**응용 프로그램 관리**선택, **웹 응용 프로그램 관리**, SharePoint 사이트를 선택 합니다. 이 예제에서는 **SharePoint – 80**입니다.

  ![Hello SharePoint 사이트를 선택합니다.](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. 클릭 **인증 공급자** hello 도구 모음입니다.
4. Hello에 **인증 공급자** 상자 **기본 영역** tooview hello 설정 합니다.
5. Hello에 **인증 편집** 대화 상자, 표시 될 때까지 아래로 스크롤하여 **클레임 인증 유형** 되어 있는지 확인 하 고 둘 다 **Windows 인증 사용** 및  **Windows 통합 인증을** 선택 됩니다.
6. Hello 드롭다운 목록 상자에서 확인 **협상 (Kerberos)** 을 선택 합니다.

  ![인증 편집 대화 상자](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Hello hello 맨 아래에 **인증 편집** 대화 상자를 클릭 **저장**합니다.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Hello SharePoint 서비스 계정에 대 한 서비스 사용자 이름을 설정합니다

Hello KCD를 구성 하기 전에 tooidentify hello SharePoint 서비스를 구성한 경우 hello 서비스 계정으로 실행 해야 합니다. SPN을 설정하여 이 작업을 수행합니다. 자세한 내용은 [서비스 주체 이름](https://technet.microsoft.com/library/cc961723.aspx)을 참조하세요.

hello SPN 형식은 다음과 같습니다.

```
<service class>/<host>:<port>
```

Hello SPN 형식:

* _서비스 클래스_ hello 서비스에 대 한 고유 이름입니다. SharePoint의 경우 **HTTP**를 사용합니다.

* _호스트_ hello 정규화 된 도메인은 또는에서 실행 되 고 hello 서비스는 hello 호스트의 NetBIOS 이름입니다. SharePoint 사이트에 대 한이 텍스트 toobe hello 사이트의 URL을 hello 사용 하는 IIS의 hello 버전에 따라 할 수 있습니다.

* _포트_는 선택 사항입니다.

Hello hello SharePoint server의 FQDN 인 경우

```
sharepoint.demo.o365identity.us
```

Hello SPN는 합니다.

```
HTTP/ sharepoint.demo.o365identity.us demo
```

서버에서 특정 사이트에 대해 tooset Spn 할 수도 있습니다. 자세한 내용은 [Kerberos 인증 구성(Office SharePoint Server)](https://technet.microsoft.com/library/cc263449(v=office.12).aspx)을 참조하세요. 지불 주의 기울여야 toohello 섹션 "만들기 서비스 사용자 이름 Kerberos 인증을 사용 하 여 웹 응용 프로그램에 대 한 합니다."

hello tooset Spn에 대 한 가장 쉬운 방법은 toofollow hello SPN 형식에 대 한 사이트에 있을 수 이미 있는 경우 이러한 Spn tooregister hello 서비스 계정에 대해 복사 합니다. toodo이:

1. 다른 컴퓨터에서 SPN hello로 toohello 사이트를 탐색 합니다.
 Hello를 수행 하는 경우 Kerberos 티켓의 관련 집합 hello 컴퓨터에 캐시 됩니다. 이러한 티켓 hello 이동 하면 hello 대상 사이트의 SPN을 포함 합니다.

2. 라는 도구를 사용 하 여 해당 사이트에 대 한 SPN hello를 끌어올 수 [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html)합니다. Hello에서 실행 되는 명령 창 hello 브라우저에서 액세스 hello 사이트를 실행 하는 hello 사용자와 같은 컨텍스트에 다음 명령을 hello:
```
Klist
```
Klist의 대상 Spn hello 집합을 반환합니다. 이 예제에서는 강조 표시 하는 hello 값은 hello 필요한 SPN입니다.

  ![Klist 예제의 결과](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. SPN hello를가지고 toomake hello 웹 응용 프로그램의 이전 설정 하는 hello 서비스 계정에 대해 올바르게 구성 되어 있는지 필요 합니다. Hello hello 도메인의 관리자 권한으로 hello 명령 프롬프트에서 다음 명령을 실행 합니다.

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 이 명령은 집합 hello SharePoint 서비스에 대 한 SPN을 hello 계정으로 실행 중인 _demo\sp_svc_합니다.

 대체 _http/sharepoint.demo.o365identity.us_ 서버에 대 한 SPN hello로 및 _demo\sp_svc_ 환경의 hello 서비스 계정과 합니다. 추가 하기 전에 hello SPN hello Setspn 명령을 검색 합니다. 이 경우 **중복된 SPN 값** 오류가 표시될 수 있습니다. 이 오류를 표시 되 면 hello 값 hello 서비스 계정과 연결 되어 있는지 확인 합니다.

SPN hello-l 옵션과 함께 hello Setspn 명령을 실행 하 여 추가 된 해당 hello를 확인할 수 있습니다. 이 명령에 대 한 더 toolearn 참조 [Setspn](https://technet.microsoft.com/library/cc731241.aspx)합니다.

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Hello 커넥터에 신뢰할 수 있는 대리자 tooSharePoint로 설정 되어 있는지 확인

Hello Azure AD 응용 프로그램 프록시 서비스 사용자 identities toohello SharePoint 서비스에 위임할 수 있도록 hello KCD를 구성 합니다. 이렇게 하면 hello 응용 프로그램 프록시 커넥터를 사용 하 여 tooretrieve Kerberos 티켓에 대 한 Azure AD에서 인증 된 사용자입니다. 그런 다음 해당 서버 hello 컨텍스트 toohello 대상 응용 프로그램 또는 SharePoint이 경우 전달 합니다.

tooconfigure hello KCD 각 커넥터 컴퓨터에 대 한 단계를 수행 하는 반복 hello:

1. 도메인 관리자 tooa DC로 로그인 한 다음 엽니다 **Active Directory 사용자 및 컴퓨터**합니다.
2. 커넥터 hello 찾기 hello 컴퓨터에서 실행 됩니다. 이 예제에서는 동일한 hello에 SharePoint 서버입니다.
3. Hello 컴퓨터를 두 번 클릭 하 고 클릭 hello **위임** 탭 합니다.
4. Hello 위임 설정이 너무 설정 되어 있는지 확인**위임 toohello 지정에 대 한이 컴퓨터 트러스트 서비스만**를 선택한 후 **모든 인증 프로토콜을 사용 하 여**합니다.

  ![위임 설정](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Hello 클릭 **추가** 단추를 클릭 하 여 **사용자 또는 컴퓨터**, hello 서비스 계정을 찾습니다.

  ![Hello 서비스 계정에 대 한 추가 hello SPN](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Spn의 hello 목록의 hello hello 서비스 계정에 대해 이전에 만든 하나를 선택 합니다.
7. **확인**을 클릭합니다. 클릭 **확인** 다시 toosave hello 변경 합니다.

## <a name="step-2-enable-remote-access-toosharepoint"></a>2 단계: 원격 액세스 tooSharePoint 사용

Kerberos에 대 한 SharePoint 사용 하도록 설정 하 고 KCD를 구성 했으므로 single sign on tooSharePoint 준비 tooset 것입니다. 그런 다음 hello 커넥터에서 Azure AD 응용 프로그램 프록시를 통한 원격 액세스를 위한 hello SharePoint 팜에 게시할 수 있습니다.

tooperform hello toobe 조직의 Azure Active Directory 계정에 hello 전역 관리자 역할의 멤버인 다음 단계를 해야 합니다.

1. Toohello 로그인 [Azure 포털](https://manage.windowsazure.com) Azure AD 테 넌 트를 찾습니다.
2. **응용 프로그램**을 클릭한 다음 **추가**를 클릭합니다.
3. **네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시**를 선택합니다. 이 옵션을 표시 되지 않으면, 해야 Azure AD Basic 또는 Premium hello 테 넌 트에 설정 되어 있는지 확인 합니다.
4. 다음과 같이 각 hello 옵션을 완료 합니다.
 * **이름**: 원하는 임의 값을 사용합니다(예: **SharePoint**)
 * **내부 URL**:이 hello SharePoint 사이트의 hello URL 같이 내부적으로 **https://SharePoint/**합니다. 이 예제에서 확인 되었는지 toouse **https**합니다.
 * **사전 인증 방법**: **Azure Active Directory**를 선택합니다.

  ![응용 프로그램 추가 옵션](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Hello 앱을 게시 한 후 클릭 hello **구성** 탭 합니다.
6. Toohello 옵션 아래로 스크롤하여 **헤더에서 URL 변환**합니다. hello 기본값은 **예**합니다. 속성을 변경할**아니요**합니다.

 SharePoint는 hello _호스트 헤더_ 값 toolook hello 사이트를 설치 합니다. 이 값을 토대로 링크도 생성합니다. hello 한 순수 효과 toomake 링크는 SharePoint 생성 toouse hello 외부 URL을 올바르게 설정 되어 있는 게시 된 URL 인지 합니다. Hello 값을 너무 설정**예** 도 활성화 hello 커넥터 tooforward hello 요청 toohello 백 엔드 응용 프로그램입니다. 그러나 hello 값을 너무 설정**아니요** 커넥터 hello 의미 hello 내부 호스트 이름에 보내지 것입니다. 대신, hello 커넥터 hello URL toohello 백 엔드 응용 프로그램 게시 hello 호스트 헤더를 보냅니다.

 또한 tooensure이이 URL을 허용 하는 SharePoint, toocomplete hello SharePoint 서버에 하나의 추가 구성이 필요 합니다. Hello 다음 섹션에 있는 수행 합니다.

7. 변경 **내부 인증 방법** 너무**Windows 통합 인증**합니다. Azure AD 테 넌 트 UPN을 사용 하 여 hello UPN 온-프레미스와에서는 다른 hello 클라우드에서 하는 경우 기억 tooupdate **로그인 Id 위임** 도 합니다.
8. 설정 **내부 응용 프로그램 SPN** toohello 값 이전에 설정입니다. 예를 들어 **http/sharepoint.demo.o365identity.us**를 사용합니다.
9. Hello 응용 프로그램 tooyour 대상 사용자를 할당 합니다.

응용 프로그램에 다음 예제와 비슷한 toohello 같아야 합니다.

  ![완성된 응용 프로그램](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>3 단계: SharePoint hello 외부 URL에 대해 알고 있는지 확인 하십시오.

외부 URL을 기준으로 링크 렌더링할 수 있도록 SharePoint hello 외부 URL에 기반 하는 hello 사이트를 찾을 수 있는 프로그램 마지막 단계 tooensure 합니다. Hello SharePoint 사이트에 대 한 대체 액세스 매핑 구성 하 여이 작업을 수행 합니다.

1. 열기 hello **SharePoint 2013 중앙 관리** 사이트입니다.
2. **시스템 설정** 아래에서 **대체 액세스 매핑 구성**을 선택합니다.

 Hello 열립니다 **대체 액세스 매핑** 상자입니다.

  ![대체 액세스 매핑 상자](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. 옆에 있는 hello 드롭 다운 목록에서 **대체 액세스 매핑 컬렉션**선택, **대체 액세스 매핑 컬렉션 변경**합니다.
4. 사이트를 선택합니다(예: **SharePoint – 80**).

  ![사이트 선택](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Tooadd hello 내부 URL 또는 공용 URL로 URL을 게시를 선택할 수 있습니다. 이 예제는 hello 엑스트라넷으로 공용 URL을 사용합니다.
6. 클릭 **공용 Url 편집** hello에 **익스트라넷** 경로 선택한 다음 입력 hello에 대 한 hello 경로 hello 이전 단계에서 설명한 대로 응용 프로그램을 게시 합니다. 예를 들어 **https://sharepoint-iddemo.msappproxy.net**을 입력합니다.

  ![Hello 경로 입력](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. **Save**를 클릭합니다.

 이제 Azure AD 응용 프로그램 프록시를 통해 외부에서 hello SharePoint 사이트에 액세스할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)
- [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)
- [Azure AD 응용 프로그램 프록시를 통해 SharePoint 2016 및 Office Online Server 게시](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
