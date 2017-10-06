---
title: "자습서: Central Desktop와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Central Desktop toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>자습서: Central Desktop와 Azure Active Directory 통합
hello이이 자습서는 Azure와 Central Desktop tooshow hello 통합 합니다. 이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Central desktop single sign on가 설정된 구독 / Central desktop 테넌트

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

* Central Desktop에 대 한 hello 응용 프로그램 통합 사용
* SSO(Single Sign-On) 구성
* 사용자 프로비전 구성
* 사용자 할당

![시나리오](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "시나리오")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Central Desktop에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정
hello이이 섹션의 목적은 toooutline 어떻게 Central Desktop에 대 한 tooenable hello 응용 프로그램 통합 합니다.

**Central Desktop에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Central Desktop**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Central Desktop**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCentral 데스크톱 hello SAML 프로토콜에 따라 하는 방법입니다.

이 절차의 일부로 필수 tooupload e-64로 인코딩된 인증서 tooyour Central Desktop 테 넌 트 됩니다.  
이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Central Desktop** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooCentral 바탕 화면에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Single Sign-On 구성")
3. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**: 
   
   1. Hello에 **중앙 데스크톱 로그인 URL** textbox Central Desktop 테 넌 트의 hello URL 입력 (예:: *http://contoso.centraldesktop.com*).
   2. Hello Central Desktop 회신 URL 텍스트 상자에 Central Desktop AssertionConsumerService URL (예:: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Hello central desktop 메타 데이터에서 hello 값을 가져올 수 있습니다 (예:: *http://contoso.centraldesktop.com*).
   >  
   
   ![앱 URL 구성](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "앱 URL 구성")
4. Hello에 **Central Desktop에서 single sign on 구성** 페이지, toodownload 인증서를 클릭 하 여 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.
   
  ![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Single Sign-On 구성")
5. Tooyour 로그인 **Central Desktop** 테 넌 트입니다.
6. 너무 이동**설정**, 클릭 **고급**, 클릭 하 고 **Single Sign On**합니다.
   
  ![설정 - 고급](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "설정 - 고급")
7. Hello에 **Single Sign-on 설정** 페이지 hello 다음 단계를 수행 합니다.
   
  ![Single Sign On 설정](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On 설정")
   
  1. **SAML v2 Single Sign-On 사용**을 선택합니다.
  2. Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO URL** 텍스트 상자에 붙여넣습니다.
  3. Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO 로그인 URL**텍스트 상자에 붙여넣습니다.
  4. Hello hello에 Azure 클래식 포털에서에서 **Central Desktop에서 single sign on 구성** 페이지, 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **SSO로그아웃URL** 텍스트 상자에 붙여넣습니다.
8. Hello에 **메시지 서명 확인 방법** 섹션를 hello 다음 단계를 수행 합니다.
   
   ![메시지 서명 확인 방법](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "메시지 서명 확인 방법")
   
  1. **인증서**를 선택합니다.
  2. Hello에서 **SSO 인증서** 목록에서 **RSH SHA256**합니다.
  3. 인증서 다운로드 hello hello 텍스트 파일의 콘텐츠 복사 hello에서에서 텍스트 파일을 만들고 hello에 붙여 넣습니다 **SSO 인증서** 필드입니다.  
     >[!TIP]
     >자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. 선택 **링크 tooyour SAMLv2 로그인 페이지를 표시**합니다.
9. **업데이트**를 클릭합니다.
10. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
    
    ![Single Sign-On 구성](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Single Sign-On 구성")
    
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

AAD 사용자 toobe 수 toosign에서, 프로 비전 된 toohello Central Desktop 응용 프로그램 수 있어야 합니다. 이 섹션에서는 Central Desktop에서 toocreate AAD 사용자 계정을 하는 방법을 설명 합니다.

**tooprovision 사용자 계정 tooCentral 바탕 화면:**
1. Central Desktop 테 넌 트 tooyour에 로그인 합니다.
2. 너무 이동**사람 \> 내부 멤버**합니다.
3. **내부 멤버 추가**를 클릭합니다.
   
  ![사람](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "사람")
4. Hello에 **새 멤버의 전자 메일 주소** textbox tooprovision을 차례로 클릭 AAD 계정을 입력 **다음**합니다.
   
  ![새 멤버의 전자 메일 주소](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "새 멤버의 전자 메일 주소")
5. **내부 멤버 추가**를 클릭합니다.
   
  ![내부 멤버 추가](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "내부 멤버 추가")
   
   >[!NOTE]
   >추가한 hello 사용자 tooclick tooactivate hello 계정 필요한 확인 링크를 포함 하는 메일을 받게 됩니다.
   > 

>[!NOTE]
>다른 Central Desktop 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Central Desktop에서 제공 된 Api
>  

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooCentral 바탕 화면 hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 **Central Desktop** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

