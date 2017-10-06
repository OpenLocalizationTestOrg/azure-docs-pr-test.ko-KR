---
title: "aaaUpgrade PhoneFactor tooAzure MFA 서버 | Microsoft Docs"
description: "시작 Azure MFA 서버 hello 이전 phonefactor agent에서 업그레이드 하세요."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Hello PhoneFactor Agent tooAzure Multi-factor Authentication 서버를 업그레이드 합니다.
tooupgrade hello PhoneFactor Agent v5.x 또는 이전 tooAzure Multi-factor Authentication 서버를 제거한 hello PhoneFactor Agent 구성 요소를 먼저 등록 합니다. 다음 Multi-factor Authentication 서버 hello 및 관련된 구성 요소를 설치할 수 있습니다.

## <a name="uninstall-hello-phonefactor-agent"></a>Hello PhoneFactor Agent를 제거 합니다.

1. 첫째, hello PhoneFactor 데이터 파일을 백업 합니다. hello 기본 설치 위치는 C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata입니다.

2. Hello 사용자 포털이 설치 된 경우:
  1. Toohello 설치 폴더를 이동 하 고 hello web.config 파일을 백업 합니다. hello 기본 설치 위치는 C:\inetpub\wwwroot\PhoneFactor입니다.

  2. Toohello 포털 사용자 지정 테마를 추가한 경우 hello C:\inetpub\wwwroot\PhoneFactor\App_Themes 디렉터리 아래의 사용자 지정 폴더를 백업 합니다.

  3. Hello 사용자 포털을 통해 PhoneFactor Agent hello 제거 (hello에 설치 된 경우에 사용할 수와 같은 서버 hello PhoneFactor Agent) 또는 Windows 프로그램 및 기능입니다.

3. Hello 모바일 앱 웹 서비스가 설치 된 경우:

  1. Toohello 설치 폴더를 이동 하 고 hello web.config 파일을 백업 합니다. hello 기본 설치 위치는 C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService입니다.

  2. Hello Windows 프로그램 및 기능을 통해 모바일 앱 웹 서비스를 제거 합니다.

4. Hello 웹 서비스 SDK가 설치 되어 제거 hello PhoneFactor Agent 또는 Windows 프로그램 및 기능을 통해 합니다.

5. Hello Windows 프로그램 및 기능을 통해 PhoneFactor Agent를 제거 합니다.

## <a name="install-hello-multi-factor-authentication-server"></a>Hello Multi-factor Authentication 서버를 설치 합니다.

hello 설치 경로에서 선택 되었습니다 hello 레지스트리 hello 이전 PhoneFactor Agent 설치에서 설치 되도록 hello에 동일한 위치 (예: C:\Program Files\PhoneFactor). 새 설치는 다른 기본 설치 경로(예: C:\Program Files\multi-factor Authentication Server)를 갖게 됩니다. 안녕 hello 이전 하므로 사용자 및 설정이 여전히 있습니다를 설치한 후 새 Multi-factor Authentication 서버 hello PhoneFactor 에이전트를 설치 하는 동안 업그레이드 해야 남긴 데이터 파일.

1. 메시지가 표시 되 면 hello Multi-factor Authentication 서버를 활성화 하 고 toohello 올바른 복제 그룹에 할당 되었는지 확인 합니다.

2. 웹 서비스 SDK hello 이전에 설치한 경우 설치 hello hello Multi-factor Authentication 서버 사용자 인터페이스를 통해 새 웹 서비스 SDK입니다.

  기본 가상 디렉터리 이름은 이제는 hello **MultiFactorAuthWebServiceSdk** 대신 **PhoneFactorWebServiceSdk**합니다. Toouse hello 이전 이름 하려는 경우 설치 하는 동안 hello hello 가상 디렉터리 이름을 변경 해야 합니다. 그렇지 않으면 hello 설치 toouse hello 새 기본 이름을 허용 하면 toochange hello URL 모든 응용 프로그램에서 해당 참조 hello (예: hello 사용자 포털 및 모바일 앱 웹 서비스) 웹 서비스 SDK toopoint 위치에 있는 hello 올바른 합니다.

3. 사용자 포털이 PhoneFactor 에이전트 서버 hello에 이전에 설치 된 hello 설치 하는 경우 hello hello Multi-factor Authentication 서버 사용자 인터페이스를 통해 새 Multi-factor Authentication 사용자 포털입니다.

  기본 가상 디렉터리 이름은 이제는 hello **MultiFactorAuth** 대신 **PhoneFactor**합니다. Toouse hello 이전 이름 하려는 경우 설치 하는 동안 hello hello 가상 디렉터리 이름을 변경 해야 합니다. 그렇지 않으면 hello 설치 toouse hello 새 기본 이름을 허용 하면 Multi-factor Authentication 서버 hello에 hello 사용자 포털 아이콘을 클릭 하 고 hello 설정 탭에서 사용자 포털 URL hello 업데이트할 해야 있습니다.

4. Hello 사용자 포털 및/또는 모바일 앱 웹 서비스에서 다른 서버에 이전에 설치 된 경우 PhoneFactor Agent hello:

  1. Toohello 설치 위치 (예: C:\Program Files\PhoneFactor)로 이동 하 고 설치 관리자 toohello 하나 이상의 다른 서버에 복사 합니다. Hello 사용자 포털 및 모바일 앱 웹 서비스 모두에 대 한 32 비트 및 64 비트 설치 관리자가 있습니다. 이러한 설치 관리자는 MultiFactorAuthenticationUserPortalSetupXX.msi 및 MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi입니다.

  2. hello 웹 서버의 tooinstall hello 사용자 포털 관리자 권한으로 명령 프롬프트를 열고 MultiFactorAuthenticationUserPortalSetupXX.msi를 실행 합니다.

    기본 가상 디렉터리 이름은 이제는 hello **MultiFactorAuth** 대신 **PhoneFactor**합니다. Toouse hello 이전 이름 하려는 경우 설치 하는 동안 hello hello 가상 디렉터리 이름을 변경 해야 합니다. 그렇지 않으면 hello 설치 toouse hello 새 기본 이름을 허용 하면 Multi-factor Authentication 서버 hello에 hello 사용자 포털 아이콘을 클릭 하 고 hello 설정 탭에서 사용자 포털 URL hello 업데이트할 해야 있습니다. 기존 사용자 hello 새 URL에 대 한 안내 toobe가 필요 합니다.

  3. Toohello 사용자 포털 설치 위치 (예: C:\inetpub\wwwroot\MultiFactorAuth) 이동한 다음 hello web.config 파일을 편집 합니다. Hello 새 web.config 파일로 hello 업그레이드 하기 전에 백업 했던 원래 web.config 파일에서 hello appSettings 및 applicationSettings 섹션의 hello 값을 복사 합니다. Hello 웹 서비스 SDK를 설치할 때 hello 새 기본 가상 디렉터리 이름을 유지, hello applicationSettings 섹션 toopoint toohello 올바른 위치에 hello URL을 변경 합니다. 다른 기본값 hello 이전 web.config 파일에서 변경 된 경우 이러한 동일한 변경 내용을 toohello 새 web.config 파일을 적용 합니다.

  4. hello 웹 서버에서 모바일 앱 웹 서비스 tooinstall hello는 관리자 권한으로 명령 프롬프트를 열고 MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi hello를 실행 합니다.

    기본 가상 디렉터리 이름은 이제는 hello **MultiFactorAuthMobileAppWebService** 대신 **PhoneFactorPhoneAppWebService**합니다. Toouse hello 이전 이름 하려는 경우 설치 하는 동안 hello hello 가상 디렉터리 이름을 변경 해야 합니다. 짧은 이름 toomake toochoose 할 수 있습니다에 모바일 장치에 최종 사용자에 게 tootype 한 것을 쉽게 합니다. 그렇지 않으면 hello 설치 toouse hello 새 기본 이름을 허용 하면 Multi-factor Authentication 서버 hello에 hello 모바일 앱 아이콘을 클릭 하 고 hello 모바일 앱 웹 서비스 URL을 업데이트할 해야 있습니다.

  5. Toohello 모바일 앱 웹 서비스 설치 위치 (예: C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) 이동한 다음 hello web.config 파일을 편집 합니다. Hello 새 web.config 파일로 hello 업그레이드 하기 전에 백업 했던 원래 web.config 파일에서 hello appSettings 및 applicationSettings 섹션의 hello 값을 복사 합니다. Hello 웹 서비스 SDK를 설치할 때 hello 새 기본 가상 디렉터리 이름을 유지, hello applicationSettings 섹션 toopoint toohello 올바른 위치에 hello URL을 변경 합니다. 다른 기본값 hello 이전 web.config 파일에서 변경 된 경우 이러한 동일한 변경 내용을 toohello 새 web.config 파일을 적용 합니다.

## <a name="next-steps"></a>다음 단계

- [Hello 사용자 포털 설치](multi-factor-authentication-get-started-portal.md) hello Azure Multi-factor Authentication 서버에 대 한 합니다.

- 응용 프로그램에 대한 [Windows 인증](multi-factor-authentication-get-started-server-windows.md)을 구성합니다. 
