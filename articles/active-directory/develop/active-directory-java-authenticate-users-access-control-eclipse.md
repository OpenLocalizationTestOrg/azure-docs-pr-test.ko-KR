---
title: "aaaHow toouse 액세스 제어 (Java) | Microsoft Docs"
description: "자세한 내용은 toodevelop 및 사용 하 여 액세스를 제어 하는 방법 Azure에서 Java 합니다."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>어떻게 tooAuthenticate Azure 액세스 제어 서비스를 사용 하 여 Eclipse 웹 사용자를
이 가이드 toouse hello Azure Toolkit for Eclipse 내에서 Azure 서비스 ACS (액세스 제어)를 hello 하는 방법에 표시 됩니다. ACS에 대 한 자세한 내용은 참조 hello [다음 단계](#next_steps) 섹션.

> [!NOTE]
> hello Azure 액세스 서비스 제어 필터는 community technology preview 합니다. 이 필터는 시험판 소프트웨어로서 Microsoft에서 공식적으로 지원되지 않습니다.
> 
> 

## <a name="what-is-acs"></a>ACS 정의
대부분의 개발자는 ID 전문가가 아니며 일반적으로 해당 응용 프로그램과 서비스에 대한 인증 및 권한 부여 메커니즘을 직접 개발하려고 하지 않습니다. ACS는 tooaccess 웹 응용 프로그램 해야 하는 사용자를 인증 하는 쉬운 방법을 제공 하는 Azure 서비스 및 코드에 복잡 한 인증 논리 toofactor 필요 없이 서비스입니다.

같은 기능 hello ACS에서 제공 됩니다.

* WIF(Windows Identity Foundation)와 통합
* Windows Live ID, Google, Yahoo! 및 Facebook을 비롯한 인기 있는 웹 IP(ID 공급자) 지원
* AD FS(Active Directory Federation Services) 2.0 지원
* 개방형 데이터 프로토콜 (OData)-tooACS 설정을 프로그래밍 방식 액세스를 제공 하는 관리 서비스를 기반으로 합니다.
* Toohello ACS 설정을 관리 액세스를 허용 하는 관리 포털입니다.

ACS에 대한 자세한 내용은 [Access Control Service 2.0][Access Control Service 2.0]을 참조하세요.

## <a name="concepts"></a>개념
Azure ACS 일관적인 접근 방식 toocreating 인증 메커니즘 또는 hello 클라우드에서 온-프레미스를 실행 중인 응용 프로그램에 대 한 클레임 기반 id-hello 주체를 기반으로 합니다. 클레임 기반 id 응용 프로그램 및 서비스 tooacquire hello 인터넷 및 다른 조직에서 조직 내 사용자에 대 한 필요한 id 정보는 일반적인 방법을 제공 합니다.

이 가이드의 toocomplete hello 작업 hello 다음 개념을 이해 해야:

**클라이언트** -이 방법을 tooguide의 hello 컨텍스트에서 toogain 액세스 tooyour 웹 응용 프로그램을 시도 하는 브라우저입니다.

**신뢰 당사자 (RP) 응용 프로그램** -는 RP 응용 프로그램은 웹 사이트 또는 서비스 인증 tooone 외부 기관 아웃소싱하입니다. Identity 특수 용어에서 해당 hello RP 해당 기관의 신뢰을 말합니다. 이 가이드에서는 설명 방법을 tooconfigure 프로그램 응용 프로그램 tootrust ACS 합니다.

**토큰** - 토큰은 일반적으로 사용자의 인증 성공 시 발급되는 보안 데이터 컬렉션입니다. 집합이 포함 되어 *클레임*, 사용자를 인증 하는 hello의 특성입니다. 클레임은 사용자 이름, 사용자가 속한 역할의 식별자, 사용자 연령 등을 나타낼 수 있습니다. 토큰을 일반적으로 디지털 서명 되었는지 즉, 백 tooits 소싱 발급자를 항상 수 있으며 해당 내용을 변경할 수 없습니다. 사용자 향상 액세스 tooa RP 응용 프로그램 hello RP 응용 프로그램에서 신뢰 하는 기관에서 발급 한 유효한 토큰을 제공 하 여 합니다.

**IP(ID 공급자)** - IP는 사용자 ID를 인증하고 보안 토큰을 발급하는 기관입니다. 발급 토큰의 실제 작업 시간 hello 하지만 보안 토큰 서비스 (STS)를 호출 하는 특별 한 서비스 구현 됩니다. IP의 일반적인 예로는 Windows Live ID, Facebook, 비즈니스 사용자 리포지토리(예: Active Directory) 등이 있습니다.
ACS 구성된 tootrust IP 이면 hello 시스템 받아들이고 해당 IP에서 발급 한 토큰의 유효성을 검사 합니다. ACS는 여러 Ip를 한 번에 인증 된 사용자 대신 해당 ACS Ip를 신뢰 하는 모든 hello에서는 사용자는 응용 프로그램에서 ACS를 신뢰 하는 경우 즉시를 제공할 수 있습니다 프로그램 응용 프로그램 tooall hello 의미 있는 신뢰할 수 있습니다.

**FP(페더레이션 공급자)** - IP는 사용자 정보를 직접 보유하고 해당 자격 증명을 통해 사용자를 인증하며 사용자에 대해 알고 있는 내용에 대한 클레임을 발급합니다. FP(페더레이션 공급자)는 다른 종류의 기관입니다. FP는 사용자를 직접 인증하는 대신 한 RP와 하나 이상의 IP 사이에서 중간자 역할을 하며 이 둘 사이의 인증을 조정합니다. IP와 FP 둘 다 STS(보안 토큰 서비스)를 사용하므로 둘 다 보안 토큰을 발급합니다. ACS는 하나의 FP입니다.

**ACS 규칙 엔진** -신뢰할 수 있는 Ip tootokens의 들어오는 토큰을 사용 하는 tootransform toobe RP hello를 사용한 간단한 형태의에서 체계화 의미 hello 논리 클레임 변환 규칙이 있습니다. ACS는 RP에 대해 지정한 변환 논리에 상관없이 해당 변환 논리 적용을 제어하는 규칙 엔진을 특징으로 합니다.

**ACS 네임스페이스** - 설정을 구성하는 데 사용하는 ACS의 최상위 파티션인 네임스페이스입니다. 네임 스페이스를 신뢰 하는 Ip의 목록, tooserve, 있어야 하는 hello 규칙 원하는 hello RP 응용 프로그램 hello 규칙 엔진 tooprocess 들어오는 토큰 및에 있습니다. 네임 스페이스 수 있는 다양 한 끝점을 노출 hello 응용 프로그램 및 개발자 tooget ACS tooperform에서 해당 기능을 사용 합니다.

hello 다음 그림에서는 방법을 보여 줍니다 ACS 인증 웹 응용 프로그램:

![ACS 흐름 다이어그램][acs_flow]

1. hello 클라이언트 (이 경우에는 브라우저) hello RP에서에서 페이지를 요청합니다.
2. Hello 요청이 아직 인증 되지 않은, 이후 hello RP에서 신뢰 하는 hello 사용자 toohello 기관을 ACS을 리디렉션합니다. hello ACS이이 RP에 대 한 지정 된 Ip의 hello choice가 있는 hello 사용자를 표시 합니다. hello 사용자 hello 적절 한 IP를 선택합니다.
3. 클라이언트 hello toohello IP의 인증 페이지에서는 이동한에 라는 사용자 toolog hello 메시지를 표시 합니다.
4. Hello 클라이언트 (예: 자격 증명을 입력 하는 hello identity) 인증 되 면 hello IP 보안 토큰을 발급 합니다.
5. 보안 토큰을 발급 한 후 hello IP hello 클라이언트 tooACS 리디렉션하고 hello 클라이언트 IP tooACS hello에서 발급 한 hello 보안 토큰을 전송 합니다.
6. ACS는 hello IP, hello id hello ACS 규칙 엔진에이 토큰의 클레임, hello 출력 id 클레임을 계산 및 이러한 출력 클레임이 포함 된 새 보안 토큰을 발급 하는 입력에서 발급 하는 hello 보안 토큰의 유효성을 검사 합니다.
7. ACS는 hello 클라이언트 toohello를 RP로 리디렉션합니다. 클라이언트 hello ACS toohello RP에서 발급 한 hello 새 보안 토큰을 보냅니다. RP hello ACS에서 발급 된 hello 보안 토큰에 hello 서명의 유효성을 검사 하 고,이 토큰의 hello 클레임의 유효성을 검사, 원래 요청 된 hello 페이지를 반환 합니다.

## <a name="prerequisites"></a>필수 조건
이 가이드의 toocomplete hello 작업 hello 다음이 필요 합니다.

* JDK(Java 개발자 키트), v 1.6 이상
* Eclipse IDE for Java EE Developers, Indigo 이상. <http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다. 
* Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: Apache Tomcat, GlassFish, JBoss Application Server 또는 Jetty)
* Azure 구독은 <http://www.microsoft.com/windowsazure/offers/>에서 구입할 수 있습니다.
* hello Azure Toolkit for Eclipse, 2014 년 4 월 릴리스 이상. 자세한 내용은 참조 [Azure Toolkit for Eclipse 설치 hello](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx)합니다.
* X.509 인증서는 응용 프로그램과 함께 toouse 합니다. 이 인증서는 공용 인증서(.cer)와 개인 정보 교환(.PFX) 형식 둘 다로 필요합니다. (이 인증서를 만들기 위한 옵션은 이 자습서의 뒷부분에 설명되어 있음)
* 익숙한 hello Azure 계산 에뮬레이터 및 배포 기술에 설명 된 [Eclipse에서 Azure 용 Hello World 응용 프로그램을 만드는](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx)합니다.

## <a name="create-an-acs-namespace"></a>ACS 네임스페이스 만들기
azure에서 서비스 ACS (액세스 제어)를 사용 하 여 toobegin ACS 네임 스페이스를 만들어야 합니다. hello 네임 스페이스는 응용 프로그램 내에서 ACS 리소스를 해결 하기 위한 고유한 범위를 제공 합니다.

1. Hello에 로그인 [Azure 관리 포털][Azure Management Portal]합니다.
2. **Active Directory**를 클릭합니다. 
3. toocreate 새 액세스 제어 네임 스페이스를 클릭 **새로**, 클릭 **응용 프로그램 서비스**, 클릭 **액세스 제어**, 클릭 하 고 **빠른 생성** . 
4. Hello 네임 스페이스에 대 한 이름을 입력 합니다. Azure는 hello 이름이 고유함을 확인 합니다.
5. hello 네임 스페이스를 사용 하는 hello 지역을 선택 합니다. 최상의 성능을 얻으려면 hello에 대 한 응용 프로그램을 배포 하는 hello 영역을 사용 합니다.
6. 둘 이상의 구독을 보유 하는 경우 hello ACS 네임 스페이스에 대 한 toouse 되도록 hello 구독을 선택 합니다.
7. **만들기**를 클릭합니다.

Azure 만들고 hello 네임 스페이스를 활성화 합니다. Hello 새 네임 스페이스의 hello 상태가 될 때까지 기다린 **활성** 계속 하기 전에. 

## <a name="add-identity-providers"></a>ID 공급자 추가
이 태스크에서는 인증을 위해 RP 응용 프로그램과 함께 Ip toouse를 추가합니다. 설명을 위해이 작업 방법을 tooadd IP, 있지만으로 Windows Live에 hello hello ACS 관리 포털에에서 나열 된 Ip를 사용할 수 보여 줍니다.

1. Hello에 [Azure 관리 포털][Azure Management Portal], 클릭 **Active Directory**액세스 제어 네임 스페이스를 선택한 다음 클릭 **관리**합니다. hello ACS 관리 포털을 엽니다.
2. Hello hello ACS 관리 포털의 왼쪽된 탐색 창에서 클릭 **Id 공급자**합니다.
3. Windows Live ID가 기본적으로 사용하도록 설정되어 있으며 삭제할 수 없습니다. 이 자습서에서는 Windows Live ID만 사용됩니다. 이 화면에서는 인데 hello를 클릭 하 여 다른 Ip를 추가할 수 있는 **추가** 단추입니다.

현재 Windows Live ID가 ACS 네임스페이스에 대한 IP로 사용하도록 설정되어 있습니다. Java 웹 응용 프로그램 (나중에 만들어진 toobe)를 지정 하는 다음으로, RP로 합니다.

## <a name="add-a-relying-party-application"></a>신뢰 당사자 응용 프로그램 추가
이 태스크에서는 ACS toorecognize Java 웹 응용 프로그램으로 구성한 올바른 RP 응용 프로그램입니다.

1. Hello ACS 관리 포털에서 클릭 **신뢰 당사자 응용 프로그램**합니다.
2. Hello에 **신뢰 당사자 응용 프로그램** 페이지 **추가**합니다.
3. Hello에 **신뢰 당사자 응용 프로그램 추가** 페이지에서 다음 hello지 않습니다.
   
   1. **이름**, hello RP의 형식 hello 이름입니다. 이 자습서에서는 **Azure Web App**을 입력합니다.
   2. **모드**에서 **수동으로 설정 입력**을 선택합니다.
   3. **영역**, ACS에서 발급 형식 hello URI toowhich hello 보안 토큰에 적용 됩니다. 이 작업의 경우 **http://localhost:8080/**을 입력합니다.
      ![계산 에뮬레이터에 사용할 신뢰 당사자 영역][relying_party_realm_emulator]
   4. **반환 URL** 형식 hello URL toowhich ACS hello 보안 토큰을 반환 합니다. 이 작업의 경우 **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![계산 에뮬레이터에 사용할 신뢰 당사자 반환 URL][relying_party_return_url_emulator]를 입력합니다.
   5. Hello 기본값 hello 나머지 hello 필드에에서 적용 합니다.
4. **Save**를 클릭합니다.

이제 성공적으로 구성한 Java 웹 응용 프로그램 hello Azure 계산 에뮬레이터에서 실행 될 때 (http://localhost:8080에 /) toobe ACS 네임 스페이스에 있는 RP 합니다. 하는 hello 규칙을 다음으로 만들기 ACS hello RP에 대 한 tooprocess 클레임을 사용 합니다.

## <a name="create-rules"></a>규칙 만들기
이 태스크에서는 Ip tooyour RP에서에서 전달 되 클레임을 구동 하는 hello 규칙을 정의 합니다. 이 가이드의 hello 목적으로 단순히 구성 ACS toocopy hello 입력된 클레임 유형 및 값 hello 출력 토큰에서 직접 수정 하거나 필터링 하지 않고 합니다.

1. Hello ACS 관리 포털 기본 페이지에서 클릭 **규칙 그룹**합니다.
2. Hello에 **규칙 그룹** 페이지 **Azure 웹 앱에 대 한 기본 규칙 그룹**합니다.
3. Hello에 **규칙 그룹 편집** 페이지 **생성**합니다.
4. Hello에 **규칙 생성: Azure 웹 앱에 대 한 기본 규칙 그룹** 페이지, Windows Live ID가 확인 한 다음 클릭 **생성**합니다.    
5. Hello에 **규칙 그룹 편집** 페이지 **저장**합니다.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>인증서 tooyour ACS 네임 스페이스를 업로드 합니다.
이 태스크에서는 업로드 한 합니다. PFX 인증서 ACS 네임 스페이스에서 만든 toosign 사용 되는 토큰 요청 수입니다.

1. Hello ACS 관리 포털 기본 페이지에서 클릭 **인증서 및 키**합니다.
2. Hello에 **인증서 및 키** 페이지 **추가** 위에 **토큰 서명**합니다.
3. Hello에 **추가 토큰 서명 인증서 또는 키** 페이지:
   1. Hello에 **에 사용 되는** 섹션에서 클릭 **신뢰 당사자 응용 프로그램** 선택 **Azure 웹 앱** (이전에 신뢰 당사자 응용 프로그램의 hello 이름으로 설정)입니다.
   2. Hello에 **형식** 섹션에서 **X.509 인증서**합니다.
   3. Hello에 **인증서** 섹션 hello 찾아보기 단추를 클릭 하 고 원하는 toouse toohello X.509 인증서 파일을 이동 합니다. 이 파일은 .PFX 파일입니다. Hello 파일 선택를 클릭 **열려**, 다음 hello에 hello 인증서 암호를 입력 하 고 **암호** 입력란. 테스트 목적으로 자체 서명된 인증서를 사용할 수 있습니다. toocreate 자체 서명 된 인증서를 사용 하 여 hello **새로** hello에서 단추 **ACS 필터 라이브러리** 대화 (뒤쪽) 하거나 hello를 사용 하 여 **encutil.exe** hello 에서에서유틸리티[프로젝트 웹 사이트] [ project website] hello Java 용 Azure 시작 키트입니다.
   4. **Make Primary** 가 선택되어 있는지 확인합니다. 프로그램 **추가 토큰 서명 인증서 또는 키** 페이지에는 비슷한 toohello 다음과 같아야 합니다.
       ![토큰 서명 인증서 추가][add_token_signing_cert]
   5. 클릭 **저장** toosave 설정 및 닫기 hello **추가 토큰 서명 인증서 또는 키** 페이지.

그런 다음가 필요 합니다 tooconfigure Java 웹 응용 프로그램 toouse ACS hello 응용 프로그램 통합 페이지 및 복사 hello URI의에서 hello 정보를 검토 합니다.

## <a name="review-hello-application-integration-page"></a>검토 hello 응용 프로그램 통합 페이지
ACS로 toowork 하 여 Java 웹 응용 프로그램 (RP 응용 프로그램 hello) hello ACS 관리 포털의 hello 응용 프로그램 통합 페이지에서 모든 hello 정보와 hello 코드 필요한 tooconfigure 찾을 수 있습니다. 페더레이션 인증에 대해 Java 웹 응용 프로그램을 구성할 때 이 정보가 필요합니다.

1. Hello ACS 관리 포털에서 클릭 **응용 프로그램 통합**합니다.  
2. Hello에 **응용 프로그램 통합** 페이지 **로그인 페이지**합니다.
3. Hello에 **로그인 페이지 통합** 페이지 **Azure 웹 앱**합니다.

Hello에 **로그인 페이지 통합: Azure 웹 앱** 페이지에 나열 된 hello URL **옵션 1: 링크 tooan ACS 호스팅 로그인 페이지** Java 웹 응용 프로그램에서 사용 됩니다. Hello Azure 액세스 제어 서비스 필터 라이브러리 tooyour Java 응용 프로그램을 추가 하면이 값이 필요 합니다.

## <a name="create-a-java-web-application"></a>Java 웹 응용 프로그램 만들기
1. Eclipse 내에서 hello 메뉴를 클릭 **파일**, 클릭 **새로**, 클릭 하 고 **동적 웹 프로젝트**합니다. (표시 되지 않으면 **동적 웹 프로젝트** 클릭 한 후 사용 가능한 프로젝트로 표시 **파일**, **새로**, 수행가 다음를 hello 다음: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트**, 확장 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고  **그런 다음**.) 이 자습서에서는 이름을 hello 프로젝트 **MyACSHelloWorld**합니다. (확인이 이름을 사용 하 여,이 자습서의 이후 단계 예상 MyACSHelloWorld 라는 프로그램 WAR 파일 toobe). 화면에는 비슷한 toohello 다음 표시 됩니다.
   
    ![ACS용 Hello World 프로젝트 만들기 예제][create_acs_hello_world]
   
    **마침**을 클릭합니다.
2. Eclipse의 Project Explorer 뷰 내에서 **MyACSHelloWorld**를 확장합니다. **WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.
3. Hello에 **JSP 파일 새로** 대화 상자에서 이름 hello 파일 **index.jsp**합니다. Hello 다음과 같이 MyACSHelloWorld/WebContent hello 부모 폴더를 유지 합니다.
   
    ![ACS용 JSP 파일 추가 예제][add_jsp_file_acs]
   
    **다음**을 누릅니다.
4. Hello에 **JSP 템플릿 선택** 대화 상자에서 **새 JSP 파일 (html)** 클릭 **마침**합니다.
5. Eclipse에서 index.jsp 파일이 hello를 열면 텍스트 toodisplay에서 추가 **ACS는 Hello World!** hello 기존 내 `<body>` 요소입니다. 업데이트 한 후 `<body>` 콘텐츠가 hello 다음과 같이 표시 되어야 합니다.
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    index.jsp를 저장합니다.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Hello ACS 필터 라이브러리 tooyour 응용 프로그램 추가
1. Eclipse의 Project Explorer에서 **MyACSHelloWorld**를 마우스 오른쪽 단추로 클릭하고 **Build Path**를 클릭한 후 **Configure Build Path**를 클릭합니다.
2. Hello에 **Java 빌드 경로** 대화 상자에서 hello 클릭 **라이브러리** 탭 합니다.
3. **Add Library**를 클릭합니다.
4. **Azure Access Control Services Filter (by MS Open Tech)**를 클릭한 후 **Next**를 클릭합니다. hello **Azure 액세스 제어 서비스 필터** 대화 상자가 표시 됩니다.  (hello **위치** 필드 Eclipse 설치 위치에 따라 다른 경로 있을 수 있습니다 및 hello 버전 번호는 소프트웨어 업데이트에 따라 달라질 수 있습니다.)
   
    ![ACS Filter 라이브러리 추가][add_acs_filter_lib]
5. Toohello 열 브라우저를 사용 하 여 **로그인 페이지 통합** hello에 나열 된 hello URL 복사 hello 관리 포털의 페이지 **옵션 1: 링크 tooan ACS 호스팅 로그인 페이지** 필드 및 hello에붙여**ACS 인증 끝점** hello Eclipse 대화의 필드입니다.
6. Toohello 열 브라우저를 사용 하 여 **신뢰 당사자 응용 프로그램 편집** hello에 나열 된 hello URL 복사 hello 관리 포털의 페이지 **영역** 필드 및 hello에 붙여 **신뢰 당사자 영역**  hello Eclipse 대화의 필드입니다.
7. Hello 내 **보안** 섹션에 있는 hello Eclipse 대화 상자에서 기존 인증서를 toouse 하려는 경우의 클릭 **찾아보기**, 원하는 toouse,을 선택 하 고 클릭 toohello 인증서 이동  **열기**합니다. Toocreate 새 인증서를 클릭 또는 **새로** toodisplay hello **새 인증서** 대화 상자에서 다음 hello 암호, hello.cer 파일의 이름 및 새 hello에 대 한 hello.pfx 파일의 이름 지정 인증서입니다.
8. 확인 **hello WAR 파일에 포함 hello 인증서**합니다. 이러한 방식 포함 hello 인증서 포함 하지 않고 배포에 toomanually로 추가 구성 요소입니다. (대신를 저장 해야 인증서 외부에서 WAR 파일의 경우 역할 구성 요소로 hello 인증서를 추가 하 고의 선택을 취소 수 **hello WAR 파일에 포함 hello 인증서**.)
9. [옵션] **Require HTTPS connections** 를 선택된 상태로 둡니다. 이 옵션을 설정 하면 hello HTTPS 프로토콜을 사용 하 여 응용 프로그램 tooaccess가 필요 합니다. Toorequire HTTPS 연결을 사용 하지 않으려면이 옵션의 선택을 취소 합니다.
10. 배포에 대 한 toohello 계산 에뮬레이터를 프로그램 **Azure ACS 필터** 설정이 비슷한 toohello 다음에 표시 됩니다.
    
    ![배포 toohello에 대 한 azure ACS 필터 설정을 계산 에뮬레이터][add_acs_filter_lib_emulator]
11. **마침**을 클릭합니다.
12. web.xml 파일이 만들어진다는 내용이 표시된 대화 상자가 나타나면 **Yes** 를 클릭합니다.
13. 클릭 **확인** tooclose hello **Java 빌드 경로** 대화 상자.

## <a name="deploy-toohello-compute-emulator"></a>Toohello 계산 에뮬레이터에 배포
1. Eclipse의 Project Explorer에서 **MyACSHelloWorld**를 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 후 **Package for Azure**를 클릭합니다.
2. **Project name**에 **MyAzureACSProject**를 입력하고 **Next**를 클릭합니다.
3. JDK 및 응용 프로그램 서버를 선택합니다. (이러한 단계는 hello에 자세히 설명 되어 [Eclipse에서 Azure 용 Hello World 응용 프로그램을 만드는](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) 자습서).
4. **마침**을 클릭합니다.
5. Hello 클릭 **Azure 에뮬레이터에서 실행** 단추입니다.
6. Hello 계산 에뮬레이터에서 Java 웹 응용 프로그램이 시작 된 후 (있도록 ACS 로그인 테스트와 함께 모든 현재 브라우저 세션을 방해 하지 않습니다) 브라우저의 모든 인스턴스를 닫습니다.
7. 브라우저에서 <http://localhost:8080/MyACSHelloWorld/>(또는 **Require HTTPS connections**를 선택한 경우 <https://localhost:8080/MyACSHelloWorld/>)를 열어 응용 프로그램을 실행합니다. Windows Live ID 로그인에 대 한 메시지가 표시 되어야 다음 신뢰 당사자 응용 프로그램에 대해 지정 된 toohello 반환 URL 수행 해야 합니다.
8. 응용 프로그램을 보는 했으면 클릭 hello **Azure 에뮬레이터 재설정** 단추입니다.

## <a name="deploy-tooazure"></a>TooAzure 배포
toodeploy tooAzure toochange hello 신뢰 당사자 영역 및 반환 URL ACS 네임 스페이스에 대 한 필요 합니다.

1. Hello에 hello Azure 관리 포털 내에서 **신뢰 당사자 응용 프로그램 편집** 페이지에서 수정할 **영역** 배포 된 사이트의 toobe hello URL입니다. 대체 **예제** 배포에 대해 지정한 hello DNS 이름으로 합니다.
   
    ![프로덕션에 사용할 신뢰 당사자 영역][relying_party_realm_production]
2. 수정 **반환 URL** 응용 프로그램의 toobe hello URL입니다. 대체 **예제** 배포에 대해 지정한 hello DNS 이름으로 합니다.
   
    ![프로덕션에 사용할 신뢰 당사자 반환 URL][relying_party_return_url_production]
3. 클릭 **저장** toosave 업데이트 된 신뢰 당사자 영역 및 반환 URL 변경 합니다.
4. Hello 유지 **로그인 페이지 통합** 페이지 브라우저에서 열고, 여기에서 toocopy 곧 필요 합니다.
5. Eclipse의 Project Explorer에서 **MyACSHelloWorld**를 마우스 오른쪽 단추로 클릭하고 **Build Path**를 클릭한 후 **Configure Build Path**를 클릭합니다.
6. Hello 클릭 **라이브러리** 탭을 클릭 **Azure 액세스 제어 서비스 필터**, 클릭 하 고 **편집**합니다.
7. Toohello 열 브라우저를 사용 하 여 **로그인 페이지 통합** hello에 나열 된 hello URL 복사 hello 관리 포털의 페이지 **옵션 1: 링크 tooan ACS 호스팅 로그인 페이지** 필드 및 hello에붙여**ACS 인증 끝점** hello Eclipse 대화의 필드입니다.
8. Toohello 열 브라우저를 사용 하 여 **신뢰 당사자 응용 프로그램 편집** hello에 나열 된 hello URL 복사 hello 관리 포털의 페이지 **영역** 필드 및 hello에 붙여 **신뢰 당사자 영역**  hello Eclipse 대화의 필드입니다.
9. Hello 내 **보안** 섹션에 있는 hello Eclipse 대화 상자에서 기존 인증서를 toouse 하려는 경우의 클릭 **찾아보기**, 원하는 toouse,을 선택 하 고 클릭 toohello 인증서 이동  **열기**합니다. Toocreate 새 인증서를 클릭 또는 **새로** toodisplay hello **새 인증서** 대화 상자에서 다음 hello 암호, hello.cer 파일의 이름 및 새 hello에 대 한 hello.pfx 파일의 이름 지정 인증서입니다.
10. 유지 **hello WAR 파일에 포함 hello 인증서** 체크 hello WAR 파일의 tooembed hello 인증서 한다고 가정 합니다.
11. [옵션] **Require HTTPS connections** 를 선택된 상태로 둡니다. 이 옵션을 설정 하면 hello HTTPS 프로토콜을 사용 하 여 응용 프로그램 tooaccess가 필요 합니다. Toorequire HTTPS 연결을 사용 하지 않으려면이 옵션의 선택을 취소 합니다.
12. 배포 tooAzure에 대 한 Azure ACS 필터 설정을 비슷한 toohello 다음 보입니다.
    
    ![프로덕션 배포의 Azure ACS Filter 설정][add_acs_filter_lib_production]
13. 클릭 **마침** tooclose hello **라이브러리 편집** 대화 상자.
14. 클릭 **확인** tooclose hello **MyACSHelloWorld에 대 한 속성** 대화 상자.
15. Eclipse에서 클릭 hello **tooAzure 클라우드 게시** 단추입니다. Hello에서와 같이 유사한 toohello 프롬프트 응답 **toodeploy 응용 프로그램 tooAzure** hello 섹션 [Eclipse에서 Azure 용 Hello World 응용 프로그램을 만드는](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) 항목입니다. 

웹 응용 프로그램을 배포한 모든 열려 있는 브라우저 세션에서 웹 응용 프로그램을 실행 하는 닫고 하 고 메시지가 표시 되어야 후 toosign toohello 송신할 뒤의 Windows Live ID 자격 증명을 사용 하 여 신뢰 당사자 응용 프로그램의 URL을 반환 합니다.

완료 되 면 toodelete hello 배포 기억 ACS Hello World 응용 프로그램을 사용 하 여 (학습할 수 있는 방법을 toodelete hello에 배포 [Eclipse에서 Azure 용 Hello World 응용 프로그램을 만드는](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) 항목).

## <a name="next_steps"></a>다음 단계
SAML Security Assertion Markup Language () ACS tooyour 응용 프로그램에 의해 반환 된 hello에 대 한 검사를 참조 하십시오. [tooview SAML hello Azure 액세스 제어 서비스에서 반환 하는 방법을][How tooview SAML returned by hello Azure Access Control Service]합니다. toofurther ACS의 기능 및 보다 복잡 한 시나리오와 tooexperiment 탐색을 참조 하십시오. [액세스 제어 서비스 2.0][Access Control Service 2.0]합니다.

또한이 사용 되는 예제 hello **hello WAR 파일에 포함 hello 인증서** 옵션입니다. 이 옵션을 사용 하면 간단한 toodeploy hello 인증서입니다. 대신 원하는 tookeep 서명 인증서 WAR 파일에서 별도 다음 기술 hello를 사용할 수 있습니다.

1. Hello 내 **보안** hello 섹션 **Azure 액세스 제어 서비스 필터** 대화 상자에서 형식 **${env 합니다. JAVA_HOME}/mycert.cer** 의 선택을 취소 **hello WAR 파일에 포함 hello 인증서**합니다. (인증서 파일 이름이 다른 경우 mycert.cer을 조정합니다.) 클릭 **마침** tooclose hello 대화 상자.
2. 배포에 구성 요소로 복사 hello 인증서: Eclipse의 프로젝트 탐색기에서 확장 **MyAzureACSProject**를 마우스 오른쪽 단추로 클릭 **WorkerRole1**, 클릭 **속성** 를 확장 하 고 **Azure 역할**를 클릭 하 고 **구성 요소**합니다.
3. **추가**를 클릭합니다.
4. Hello 내 **구성 요소 추가** 대화 상자:
   
   1. Hello에 **가져오기** 섹션:
      1. 사용 하 여 hello **파일** toouse를 원하는 단추 toonavigate toohello 인증서입니다. 
      2. **Method**의 경우 **copy**를 선택합니다.
   2. 에 대 한 **이름을**hello 텍스트 상자 클릭 하 고 hello 기본 이름을 적용 합니다.
   3. Hello에 **배포** 섹션:
      1. **Method**의 경우 **copy**를 선택합니다.
      2. 에 대 한 **toodirectory**, 형식 **% JAVA_HOME %**합니다.
   4. 프로그램 **구성 요소 추가** 대화 비슷한 toohello 다음과 같아야 합니다.
      
       ![인증서 구성 요소 추가][add_cert_component]
   5. **확인**을 클릭합니다.

이때 인증서가 배포에 포함됩니다. 참고 하 든 hello 인증서 hello WAR 파일에 포함할 구성 요소 tooyour 배포로 추가 하 고, 필요한 tooupload hello 인증서 tooyour 네임 스페이스 hello에 설명 된 대로 [인증서 tooyour ACS 네임 스페이스업로드] [ Upload a certificate tooyour ACS namespace] 섹션.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

