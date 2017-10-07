---
title: "자습서: SAP HANA Cloud Platform과 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 SAP HANA Cloud Platform toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>자습서: SAP HANA Cloud Platform과 Azure Active Directory 통합
hello이이 자습서는 Azure와 SAP HANA Cloud Platform tooshow hello 통합 합니다.

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* SAP HANA Cloud Platform 계정

이 자습서를 완료 한 후 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 기호 HANA Cloud Platform 됩니다 tooSAP를 할당 한 Azure AD 사용자 hello [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

>[!IMPORTANT]
>Toodeploy 사용자의 응용 프로그램 또는 단일 계정 tootest 로그온 하 여 SAP HANA Cloud Platform에 tooan 응용 프로그램을 구독 합니다. 이 자습서에서는 응용 프로그램은 hello 계정에 배포 됩니다.
> 
> 

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. SAP HANA Cloud Platform에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 역할 tooa 사용자 지정
4. 사용자 할당

![시나리오](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "시나리오")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>SAP HANA Cloud Platform에 대 한 hello 응용 프로그램 통합 사용
이 섹션의 hello 목표 toooutline를 어떻게는 SAP HANA Cloud Platform에 대 한 tooenable hello 응용 프로그램 통합 합니다.

**SAP HANA Cloud Platform에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Azure 관리 포털 hello hello 왼쪽된 탐색 창에서 클릭 **Active Directory**합니다.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 추가](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **SAP HANA Cloud Platform**합니다.
   
    ![응용 프로그램 갤러리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **SAP HANA Cloud Platform**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSAP HANA Cloud Platform hello SAML 프로토콜에 따라 하는 방법입니다.

이 절차의 일부로, 필요한 tooupload e-64로 인코딩된 인증서 tooyour SAP HANA Cloud Platform 테 넌 트가 됩니다.  

이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **SAP HANA Cloud Platform** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성**대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooSAP HANA Cloud Platform에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Single Sign-On 구성")
3. 다른 웹 브라우저 창에서 https://account에서 toohello SAP HANA Cloud Platform Cockpit에 로그인 합니다. \<가로 호스트\>.ondemand.com/cockpit (예:: *https://account.hanatrial.ondemand.com/cockpit*).
4. Hello 클릭 **신뢰** 탭 합니다.
   
    ![신뢰](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "신뢰")
5. 트러스트 관리 섹션에서 단계를 수행 하는 hello를 수행 합니다.
   
    ![메타 데이터 가져오기](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "메타 데이터 가져오기")
   
   1. Hello 클릭 **Local Service Provider** 탭 합니다.
   2. toodownload hello SAP HANA Cloud Platform 메타 데이터 파일을 클릭 하 여 **Get Metadata**합니다.
6. Hello 활성 Azure 클래식 포털 hello **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "앱 URL 구성")
   
   1. Hello에 **로그온 URL** 텍스트 상자에 사용자가 toosign 프로그램에서 사용 하는 hello URL 입력 하면 **SAP HANA Cloud Platform** 응용 프로그램입니다. SAP HANA Cloud Platform 응용 프로그램에서 보호 된 리소스의 hello 계정별 URL입니다. hello URL 기반으로 패턴 hello: *https://\<applicationName\>\<accountName\>.\< 가로 호스트\>.ondemand.com/\<경로\_를\_보호\_리소스\>*  (예:: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Hello 사용자 tooauthenticate 필요한 SAP HANA Cloud Platform 응용 프로그램에 hello URL입니다.
     > 

   2. Hello 다운로드 한 SAP HANA Cloud Platform 메타 데이터 파일을 열고 찾은 후 hello **ns3:** 태그입니다.
   3. Hello의 hello 값을 복사 **위치** 특성을 선택한 다음 hello에 붙여 넣을 **SAP HANA Cloud Platform 회신 URL** 텍스트 상자에 붙여넣습니다.

7. Hello에 **SAP HANA Cloud Platform에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Single Sign-On 구성")
8. Hello에 SAP HANA Cloud Platform Cockpit hello에 **Local Service Provider** 섹션를 hello 다음 단계를 수행 합니다.
   
    ![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "신뢰 관리")
   
  1. **편집**을 클릭합니다.
  2. **구성 유형**으로 **사용자 지정**을 선택합니다.
  3. 으로 **Local Provider Name**, hello 기본값을 그대로 둡니다.
  4. toogenerate는 **서명 키** 및 **서명 인증서** 키 쌍을 클릭 **Generate Key Pair**합니다.
  5. **주 전파**로 **사용 안 함**을 선택합니다.
  6. **강제 인증**으로 **사용 안 함**을 선택합니다.
  7. **Save**를 클릭합니다.

9. Hello 클릭 **Trusted Identity Provider** 탭을 클릭 한 다음 **Add Trusted Identity Provider**합니다.
   
    ![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "신뢰 관리")
   
    >[!NOTE]
    >신뢰할 수 있는 id 공급자의 toomanage hello 목록 toohave hello Local Service Provider 섹션에서에서 Custom 구성 유형을 hello를 선택 해야 합니다. Default 구성 유형의 편집할 수 없는 암시적인 트러스트가 toohello SAP ID 서비스 구조가 있습니다. 없음의 경우 신뢰 설정이 필요 없습니다.
    > 
    > 

10. Hello 클릭 **일반** 탭을 클릭 한 다음 **찾아보기** tooupload hello 메타 데이터 파일을 다운로드 합니다.
    
    ![신뢰 관리](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "신뢰 관리")
    
    >[!NOTE]
    >Hello 메타 데이터 파일을 업로드 한 후 hello에 대 한 값 **Single Sign on URL**, **단일 로그 아웃 URL** 및 **서명 인증서** 가 자동으로 채워집니다.
    > 
    > 

11. Hello 클릭 **특성** 탭 합니다.
12. Hello에 **특성** 탭 hello 다음 단계를 수행 하십시오.
    
    ![특성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "특성") 
  * 클릭 **add assertion-based Attribute**, 다음 hello 다음 어설션 기반 특성을 추가 합니다.
       
    | 어설션 특성 | 보안 주체 특성 |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >hello 특성의 hello 구성 방법을 HCP hello 응용 프로그램이 개발 되는, 즉 hello SAML 응답에서에서 예상 되는 이름 (Principal Attribute)에 액세스할 hello 코드에서이 특성 및 특성에 따라 달라 집니다.
     > 
     >  

    1.  hello **Default Attribute** hello 스크린샷은 단지 설명을 위해 됩니다. 없으면 toomake hello 시나리오 작업에 필요 합니다.   
    2.  이름 및 값에 대 한 hello **Principal Attribute** hello에 표시 된 스크린 샷 hello 응용 프로그램을 개발 하는 방법에 따라 달라 집니다. 응용 프로그램에 다른 매핑이 필요할 수 있습니다.
     
13. Hello hello에 Azure 클래식 포털에서에서 **SAP HANA Cloud Platform에서 single sign on 구성** 대화 상자 페이지 hello single sign on 구성 확인을 선택한 다음 **완료**합니다.
    
    ![Single Sign-On 구성](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Single Sign-On 구성")

###<a name="assertion-based-groups"></a>어설션 기반 그룹
선택적 단계로, Azure Active Directory ID 공급자에 대한 어설션 기반 그룹을 구성할 수 있습니다.

SAP HANA Cloud Platform의 그룹을 사용 하면 하나 toodynamically 할당 아니면 더 많은 사용자가 tooone 또는 SAP HANA Cloud Platform 응용 프로그램에서 더 많은 역할 결정 hello SAML 특성의 값으로 2.0 어설션 합니다. 

예를 들어 hello 어설션이 있으면 hello 특성 "*계약 임시 =*", 모든 영향을 받는 사용자 toobe 추가 toohello 그룹 경우가"*임시*"입니다. hello 그룹 "*임시*" SAP HANA Cloud Platform 계정에 배포 된 하나 이상의 응용 프로그램에서 하나 이상의 역할을 포함할 수 있습니다.
 
사용 하 여 어설션 기반 그룹 toosimultaneously 하려는 경우 여러 사용자가 tooone 또는 SAP HANA Cloud Platform 계정에서 응용 프로그램의 추가 역할을 할당 합니다. Tooassign만 한 명 또는 소수의 사용자 toospecific 역할 수를 원하는 경우 hello에 직접 할당 하는 것이 좋습니다 "**권한 부여**" hello SAP HANA Cloud Platform cockpit의 탭 합니다.

## <a name="assign-a-role-tooa-user"></a>역할 tooa 사용자 지정
Tooenable Azure AD 사용자가 toolog SAP HANA Cloud Platform에 주문 하 고, SAP HANA Cloud Platform toothem hello에에서 대 한 역할을 할당 해야 합니다.

**역할 tooa 사용자 tooassign hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **SAP HANA Cloud Platform** 환경을 제공 합니다.
2. Hello 다음을 수행 합니다.
   
   ![권한 부여](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "권한 부여")
   
  1. **권한 부여**를 클릭합니다.
  2. Hello 클릭 **사용자** 탭 합니다.
  3. Hello에 **사용자** 형식 hello 사용자의 전자 메일 주소 텍스트 상자입니다.
  4. 클릭 **할당** tooassign hello 사용자 tooa 역할입니다.
  5. **Save**를 클릭합니다.

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooSAP HANA Cloud Platform hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 **SAP HANA Cloud Platform** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "예")

SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

