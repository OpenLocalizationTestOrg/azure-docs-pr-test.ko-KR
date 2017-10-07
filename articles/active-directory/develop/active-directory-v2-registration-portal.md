---
title: "등록 포털 도움말 항목 aaaApp | Microsoft Docs"
description: "Hello Microsoft 응용 프로그램 등록 포털의 다양 한 기능에 대 한 설명"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>앱 등록 참조
컨텍스트 및 다양 한 기능 hello Microsoft 응용 프로그램 등록 포털에 대 한 설명은이 문서에서는 [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)합니다.

## <a name="my-applications"></a>내 응용 프로그램
이 목록에는 hello Azure AD v2.0 끝점에서 사용 하도록 등록 하 여 응용 프로그램의 모든 포함 합니다.  이러한 응용 프로그램이 두 개인 계정에서 Microsoft 계정 및 Azure Active Directory에서 작업/학교 계정이 있는 사용자의 hello 기능 toosign를 갖습니다.  Azure AD hello v2.0 끝점에 대해 자세히 toolearn 참조 우리의 [v2.0 개요](active-directory-appmodel-v2-overview.md)합니다.  이러한 응용 프로그램 hello Microsoft 계정 인증 끝점에 사용 되는 toointegrate 수도 있습니다 `https://login.live.com`합니다.

## <a name="live-sdk-applications"></a>Live SDK 응용 프로그램
이 목록에는 Microsoft 계정으로만 사용하도록 등록된 모든 응용 프로그램이 포함되어 있습니다.  Azure Active Directory로 사용할 방법은 전혀 없습니다.  이이 hello MSA 개발자 포털에서 이전에 등록 하는 모든 응용 프로그램을 찾을 수 있는 `https://account.live.com/developers/applications`합니다.  이전에 `https://account.live.com/developers/applications`에서 수행한 모든 함수를 이제 이 새 포털 `https://apps.dev.microsoft.com`에서 수행할 수 있습니다.  Microsoft 계정 응용 프로그램에 대한 추가적인 질문이 있으면 문의하세요.

## <a name="application-secrets"></a>응용 프로그램 암호
응용 프로그램 암호는 응용 프로그램 tooperform 신뢰할 수 있는 허용 하는 자격 증명 [클라이언트 인증](http://tools.ietf.org/html/rfc6749#section-2.3) Azure AD와 합니다.  OAuth 및 OpenID Connect, 응용 프로그램 암호는 일반적으로 참조 tooas는 `client_secret`합니다.  Hello v2.0 프로토콜 웹 주소 지정 가능한 위치에서 보안 토큰을 수신 하는 모든 응용 프로그램에서에서 (사용 하는 `https` 구성표) 자체 응용 프로그램 보안 tooidentify 해당 보안 토큰의 상환 시 tooAzure AD를 사용 해야 합니다.  또한 모든 네이티브 클라이언트 응용 프로그램 보안 tooperform 클라이언트 인증, toodiscourage를 사용 하 여 장치에서 받는 토큰을 금지 됩니다는 hello 안전 하지 않은 환경에서 암호를 저장 합니다.

각 앱에는 해당 시점에 유효한 두 개의 응용 프로그램 암호가 포함될 수 있습니다.  두 개의 비밀을 유지 하 여 응용 프로그램의 전체 환경 전체 hello ablilty tooperform 정기적인 키 롤오버를 할 수 있습니다.  Hello 전체 응용 프로그램 tooa 새 암호를 마이그레이션한 후 hello 이전 암호가 삭제 및 새 프로 비전 할 수 있습니다.

이때 두 가지 유형의 응용 프로그램 암호는 hello 응용 프로그램 등록 포털에서 허용 됩니다.  선택 **새 암호를 생성할** 생성 하 고 응용 프로그램에서 사용할 수 있는 hello 각 데이터 저장소에 공유 암호를 저장 합니다.  선택 **새 키 쌍 생성** 다운로드 되어 클라이언트 인증 tooAzure AD에 사용 될 수 있는 새 공개/개인 키 쌍을 만듭니다.

## <a name="profile"></a>프로필
hello 응용 프로그램 등록 포털의 hello 프로필 섹션 수 응용 프로그램에 대 한 페이지에 toocustomize hello 기호를 사용 합니다.  이 이번에 hello 로그인 페이지의 응용 프로그램 로고가, 서비스 URL 및 개인정보취급방침 약관을 변경할 수 있습니다.  hello 로고 이어야 합니다는 15KB GIF, PNG 또는 JPEG 파일에 투명 한 48 x 48 또는 50 x 50 픽셀 이미지 또는 작게 합니다.  Hello 값과 로그인 페이지 결과 보기 hello를 변경해 보세요!

## <a name="live-sdk-support"></a>Live SDK 지원
"라이브 SDK 지원"을 사용 하도록 설정 하면 모든 응용 프로그램을 만들면 비밀 hello Azure AD 및 Microsoft 계정 데이터 모두에 프로 비전 할 저장 합니다.  이렇게 하면 hello (login.live.com) Microsoft 계정 서비스와 직접 응용 프로그램 toointegrate 프로그램.  Microsoft 계정을 사용 하 여 직접 (것과 반대로 toousing hello Azure AD v2.0 끝점으로) 앱 toobuild을 원할 경우 라이브 SDK 지원 활성화 되어 있는지 확인 해야 합니다.

라이브 SDK 지원을 사용 하지 않도록 설정 하면 해당 hello 응용 프로그램 암호 hello Azure AD 데이터 저장소에 기록 됩니다.  Azure AD hello 데이터 저장소 FISMA 규정 준수 등의 특정 표준 toomeet 허용 되는 엔터프라이즈급 규정을 통합 합니다.  Live SDK 지원을 사용하도록 설정하면 응용 프로그램이 이러한 일부 표준을 준수하지 못할 수 있습니다.

Toouse hello Azure AD v2.0 끝점만 하려는 경우에 Live SDK 지원을 안전 하 게 해제할 수 있습니다.

