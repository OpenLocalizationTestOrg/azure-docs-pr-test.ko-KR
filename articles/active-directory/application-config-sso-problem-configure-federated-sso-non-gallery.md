---
title: "페더레이션된 single sign-on 구성 갤러리가 아닌 응용 프로그램에 대 한 aaaProblem | Microsoft Docs"
description: "페더레이션된 single sign on tooyour 사용자 지정 SAML 응용 프로그램 나열 되어 있지 않은 hello Azure AD 응용 프로그램 갤러리에서에서 구성할 때 발생 하는 hello 일반적인 문제 중 일부를 해결합니다"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>비갤러리 응용 프로그램에 대해 비갤러리 Single Sign-On 구성 문제

응용 프로그램을 구성할 때 문제가 발생 할 경우. Hello 문서의 모든 hello 단계를 따랐는지 확인 [single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성 합니다.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Hello 응용 프로그램의 다른 인스턴스를 추가할 수 없습니다.

응용 프로그램의 두 번째 인스턴스 tooadd 필요한 toobe 수 있습니다:

-   Hello 두 번째 인스턴스에 대 한 고유 식별자를 구성 합니다. 동일한 식별자 사용에 대 한 hello 첫 번째 인스턴스 수 tooconfigure hello 수 없습니다.

-   첫 번째 인스턴스 hello에 대 한 사용 되는 hello와 다른 인증서를 구성 합니다.

경우 hello 응용 프로그램 hello 위의 중 하나를 지원 하지 않습니다. 그런 다음 두 번째 인스턴스 수 tooconfigure 수 없습니다.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Hello EntityID (사용자 식별자) 형식을 설정 하는 위치

Azure AD는 hello에 대 한 응답 toohello 응용 프로그램 사용자 인증 후 보냅니다 수 tooselect hello EntityID (사용자 식별자) 형식 수 없습니다.

Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다. 자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello 섹션 NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>여기서 얻는 hello 응용 프로그램 메타 데이터 또는 인증서 Azure AD에서

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
