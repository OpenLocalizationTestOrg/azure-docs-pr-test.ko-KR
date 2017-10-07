---
title: "페더레이션된 single sign-on 구성 Azure AD 갤러리 응용 프로그램에 대 한 aaaProblem | Microsoft Docs"
description: "단일 페더레이션 구성할 때 발생할 수 있는 hello 일반적인 문제 중 일부를 해결 hello Azure AD 응용 프로그램 갤러리에에서 나와 있는 응용 프로그램에 대 한 SAML을 사용 하 여 sign-on"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성할 때 발생하는 문제

응용 프로그램을 구성할 때 문제가 발생 할 경우. Hello 응용 프로그램에 대 한 hello 자습서의 모든 hello 단계를 따랐는지 확인 하십시오. Hello 응용 프로그램의 구성에서 어떻게 tooconfigure hello 응용 프로그램에 대 한 인라인 문서가 수 있습니다. 또한 hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 세부 단계별 지침에 대 한 합니다.

## <a name="cant-add-another-instance-of-hello-application"></a>Hello 응용 프로그램의 다른 인스턴스를 추가할 수 없습니다.

응용 프로그램의 두 번째 인스턴스 tooadd 필요한 toobe 수 있습니다:

-   Hello 두 번째 인스턴스에 대 한 고유 식별자를 구성 합니다. 동일한 식별자 사용에 대 한 hello 첫 번째 인스턴스 수 tooconfigure hello 수 없습니다.

-   첫 번째 인스턴스 hello에 대 한 사용 되는 hello와 다른 인증서를 구성 합니다.

경우 hello 응용 프로그램 hello 위의 중 하나를 지원 하지 않습니다. 그런 다음 두 번째 인스턴스 수 tooconfigure 수 없습니다.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Hello 식별자를 추가 하거나 회신 URL hello 수 없습니다.

하지 수 tooconfigure hello 식별자 이거나 hello 회신 URL을 hello 식별자를 확인 하 고 회신 URL 값이 hello 응용 프로그램에 대해 미리 구성 하는 hello 패턴 일치 합니다.

tooknow hello 패턴 hello 응용 프로그램에 대해 미리 구성:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자** Toostep 7 이동 합니다. 이미 있다면 hello 응용 프로그램의 구성 블레이드에서 Azure AD에 있습니다.

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.

9.  Toohello 이동 **식별자** 또는 **회신 URL** hello 아래 텍스트 상자 **도메인 및 Url 섹션입니다.**

10. Hello 응용 프로그램에 tooknow 지원 hello 패턴은 다음 세 가지 방법:

   * Hello 텍스트 자리 표시자로 hello 지원 케이스 참조 *예제:* <https://contoso.com>합니다.

   * hello 패턴이 지원 되지 않는 hello 텍스트 상자의 tooenter hello 값 려 할 때 빨간색 느낌표가 표시 됩니다. Hello 빨간색 느낌표가 표시 위로 마우스를 가져가면 지원 hello 패턴을 파악 합니다.

   * Hello 응용 프로그램에 대 한 hello 자습서에서는 지원 되는 hello 패턴에 대 한 정보를 가져올 수 있습니다. Hello에서 **Azure AD single sign-on 구성** 섹션. Hello 아래에 구성 된 hello 값에 대 한 이동 toohello 단계 **도메인 및 Url** 섹션.

경우 hello 값은 Azure AD에 미리 구성 된 hello 패턴과 일치 하지 않습니다. 다음을 수행할 수 있습니다.

-   Azure AD에 미리 구성 된 hello 패턴과 일치 하는 hello 응용 프로그램 공급 업체 tooget 값 사용

-   Azure AD 팀에 문의할 수 있습니다 또는 < aadapprequest@microsoft.com > hello 응용 프로그램에 대 한 지원 hello 패턴의 hello 자습서 toorequest hello 업데이트에 의견을 남겨 또는

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Hello EntityID (사용자 식별자) 형식을 설정 하는 위치

Azure AD는 hello에 대 한 응답 toohello 응용 프로그램 사용자 인증 후 보냅니다 수 tooselect hello EntityID (사용자 식별자) 형식 수 없습니다.

Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다. 자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello 섹션 NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Hello 응용 프로그램과 hello Azure AD 메타 데이터 toocomplete hello 구성을 찾을 수 없습니다.

toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Single sign on 구성한 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다. 어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.

Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다. hello 메타 데이터를 XML 파일로 검색할 수 있습니다.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Toocustomize SAML 클레임 tooan 응용 프로그램을 전송 하는 방법을 알 수 없습니다

toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
