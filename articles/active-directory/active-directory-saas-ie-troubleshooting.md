---
title: "IE에 대 한 Azure 액세스 패널 확장이 aaaTroubleshooting hello | Microsoft Docs"
description: "어떻게 toouse 정책 toodeploy hello Internet Explorer 추가 기능 hello My Apps 포털에 대 한 그룹입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Internet Explorer에 대 한 hello 액세스 패널 확장 문제 해결
이 문서에서는 hello 다음 문제를 해결 하는 데:

* 있습니다 수 없습니다 tooaccess hello My Apps 포털을 통해 앱 Internet Explorer를 사용 하는 동안 하 합니다.
* Hello hello 소프트웨어를 이미 설치한 경우에 "소프트웨어 설치" 메시지가 표시 됩니다.

관리자 인 경우 참고 항목: [tooDeploy 그룹 정책을 사용 하 여 Internet Explorer에 대 한 액세스 패널 확장을 hello 하는 방법](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Hello 진단 도구 실행
다운로드 및 hello 액세스 패널에 대 한 진단 도구를 실행 하 여 액세스 패널 확장이 hello로 설치 문제를 진단할 수 있습니다.

1. [여기 toodownload hello 진단 도구를 클릭 하십시오.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. 열기 hello 파일 및 키를 눌러 **압축 풀기** 단추입니다.
   
    ![모두 추출 누르기](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Hello 키를 누릅니다 **추출** 단추 toocontinue 합니다.
   
    ![추출 누르기](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. toorun hello 도구를 마우스 오른쪽 단추로 클릭 hello 파일인 **AccessPanelExtensionDiagnosticTool**을 선택한 후 **연결 프로그램 > Microsoft Windows 스크립트 호스트 기반**합니다.
   
    ![열기 > Microsoft Windows 기반 스크립트 호스트](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. 그런 다음 잘못 설치 된 것을 설명 하는 진단 창을 다음 hello를 나타납니다.
   
    ![Hello 진단 창의 샘플](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. 클릭 하 여 "**예**" toolet hello 프로그램 hello 관련 문제를 해결할 발견 되었습니다.
7. 이러한 변경 사항은 toosave 모든 Internet Explorer 창을 닫고 Internet Explorer를 다시 엽니다.<br />여전히 앱에 액세스할 수 없으면 다음 hello 단계를 시도 하십시오.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>액세스 패널 확장이 설정 되어 있으면 해당 hello를 확인 합니다.
액세스 패널 확장이 hello tooverify Internet Explorer에서 사용 됩니다.

1. Internet Explorer에서 클릭 hello **기어 아이콘** hello 창의 hello 위 오른쪽 모서리에 있습니다. 그런 다음 **인터넷 옵션**을 선택합니다.<br />이전 버전의 Internet Explorer에서는 **도구 > 인터넷 옵션** 아래에서 찾을 수 있습니다.
   
    ![TooTools 이동 > 인터넷 옵션](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Hello 클릭 **프로그램** 탭을 선택한 다음 hello **추가 기능을 관리** 단추입니다.
   
    ![추가 기능 관리 클릭](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. 이 대화 상자에서 선택 **액세스 패널 확장이** hello를 클릭 한 다음 **사용** 단추입니다.
   
    ![사용 클릭](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. 이러한 변경 사항은 toosave 모든 Internet Explorer 창을 닫고 Internet Explorer를 다시 엽니다.

## <a name="enable-extensions-for-inprivate-browsing"></a>InPrivate 브라우징에 확장 사용
Hello InPrivate 브라우징 모드 사용 중인 경우:

1. Internet Explorer에서 클릭 hello **기어 아이콘** hello 창의 hello 위 오른쪽 모서리에 있습니다. 그런 다음 **인터넷 옵션**을 선택합니다.<br />이전 버전의 Internet Explorer에서는 **도구 > 인터넷 옵션** 아래에서 찾을 수 있습니다.
   
    ![Hello 진단 창의 샘플](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Toohello 이동 **개인 정보 보호** 탭 한 다음 **의 선택을 취소** 확인란 hello **InPrivate 브라우징 시작 될 때 도구 모음 및 확장 사용 안 함**</p>
   
    ![InPrivate 브라우징 시작 시 도구 모음 및 확장 프로그램 사용 안 함](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. 이러한 변경 사항은 toosave 모든 Internet Explorer 창을 닫고 Internet Explorer를 다시 엽니다.

## <a name="uninstall-hello-access-panel-extension"></a>Hello 액세스 패널 확장 제거
toouninstall hello 컴퓨터에서 액세스 패널 확장:

1. 키보드에서 hello 키를 누릅니다. **Windows 키** tooopen hello 시작 메뉴. 아무 것도 입력할 수 hello 메뉴를 연 toodo 검색 합니다. "제어판"를 입력 한 다음 hello 엽니다 **제어판** hello 검색 결과에 표시 되 면입니다.
   
    ![제어판 검색](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. Hello의 오른쪽 위 모서리 hello 제어판, 변경 hello **하 여 볼** 옵션**큰 아이콘**합니다. 다음 찾아 hello 클릭 **프로그램 및 기능** 단추입니다.
   
    ![파일과 변경 hello 보기 tooshow 큰 아이콘](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Hello 목록에서 선택 **액세스 패널 확장이**, hello hello를 클릭 하 고 **제거** 단추입니다.
   
    ![제거 클릭](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. 그런 다음 연습할 수 tooinstall hello 확장 hello 문제가 해결 되 면 다시 toosee 합니다.

Hello 확장 문제가 발생 하는 경우를 제거할 수도 있습니다 hello를 사용 하 여 [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) 도구입니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)
* [그룹 정책을 사용 하 여 Internet Explorer에 대 한 tooDeploy 액세스 패널 확장이 hello 하는 방법](active-directory-saas-ie-group-policy.md)

