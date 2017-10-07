---
title: "Azure 및 Microsoft 계정 로그인-전화 aaaMicrosoft 인증자 | Microsoft Docs"
description: "전화 toosign tooyour 암호를 입력 하는 대신 Microsoft 계정에에서 사용 합니다. 이 문서에서는 이 기능에 대한 FAQ를 제공합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>암호가 아닌 휴대폰을 사용하여 로그인

hello Microsoft Authenticator 앱을 사용 하 여 계정의 암호를 입력 한 후 2 단계 인증을 수행 하 여 보안을 유지 수 있습니다. 하지만 것을 아십니까 것 개인 Microsoft 계정에 대 한 hello 암호를 완전히 바꿀 수 있습니까? 

이 기능은 iOS 및 Android 장치에서 사용할 수 있으며 개인 Microsoft 계정에서 작동합니다. 

## <a name="how-it-works"></a>작동 방법

여러분 중 많은 tooyour Microsoft 계정에에서 로그인 할 때 2 단계 인증에 대 한 hello Microsoft Authenticator 앱을 사용 합니다. 하면 암호를 입력 한 다음 이동 toohello 앱 tooeither 알림을 승인 하거나 확인 코드를 가져오세요. 전화 로그인 사용 hello 암호 건너뛰고 휴대폰에 모두 id 확인을 수행 합니다. 전화 로그인 2 단계 인증 유형의 이기 때문에 보내야 tooprovide 알고 있는 것와 tooverify 본인을 해야 하는 것입니다. hello 전화 여전히 hello 줄 일, 하며 휴대폰의 PIN 또는 생체 인식 키가 hello 것을 알고 있습니다. 

## <a name="how-tooget-started"></a>Tooget 시작 하는 방법

toosign tooyour 휴대폰 개인 Microsoft 계정에서 다음이 단계를 따르십시오. 

1. 계정에 대해 휴대폰 로그인을 사용하도록 설정합니다. 

  - 아직 설치 하 고 hello에서 toohello 단계에 따라 개인 Microsoft 계정을 추가 hello Microsoft Authenticator 앱 없으면 [Microsoft Authenticator 페이지](microsoft-authenticator-app-how-to.md)합니다. 좋은 toogo 있으므로 새로 추가 된 계정은 자동으로 활성화 됩니다.

  - 2 단계 인증에 대 한 Microsoft 인증자를 이미 사용 하는 경우 hello 응용 프로그램 홈 페이지에서 사용자 계정을 선택 하 고 선택 **전화 로그인 사용** hello 드롭 다운 메뉴에서 합니다.

  >[!NOTE] 
  >tooprotect 계정에는 PIN 또는 생체 인식 잠금을 장치에 필요 합니다. 잠금 해제 휴대폰을 유지 하는 경우 전화 로그인 사용 하기 전에 잠금을를 tooset 하 라는 요청 hello 앱 설명이 나타납니다. 

3. Microsoft 계정 암호를 정상적으로 입력하는 페이지에는 대부분의 **대신 앱 사용**이라는 링크가 있습니다. 이 링크 toosign 휴대폰을 사용 하 여 선택 합니다. 

4. Microsoft는 알림 tooyour 전화를 보냅니다. Hello 알림 toosign tooyour 계정에서 승인 합니다.   

## <a name="faq"></a>FAQ 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>휴대폰에 암호를 입력하는 것보다 안전하게 로그인할 수 있나요?  

오늘날 대부분의 사람들이 tooweb 사이트 또는 사용자 이름 및 암호를 사용 하 여 앱에 로그인 합니다.  그러나 암호를 종종 분실하거나 도난당하거나 해커가 추측하게 됩니다. Microsoft Authenticator 앱 toosign hello 설정할 때 계정의 잠금을 해제할 수 있는 휴대폰의 키를 생성 합니다. Hello PIN로이 키를 보호 하거나 이미 사용 하는 휴대폰에서 생체 인식 합니다.  이 키가 두 개의로 안전 하 게 본인 요소 – hello 사용 되는 tooprove 휴대폰으로 로그인 할 때 자체 전화 및 기능 toounlock 것입니다. 

사용 되는 hello 키 Windows Hello 및 hello FIDO Alliance UAF 사양에 사용 되는 비슷한 toohello 키입니다. 에서만 데이터를 프로그램 약력 tooprotect hello 키를 로컬로 사용 하 고는, 보내거나 hello 클라우드에 저장 합니다. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>사용할 수 있는 합니까 내 전화 tooreplace 암호를 하 고 여기서 여전히 필요한 hello 암호?  

오늘날 hello 전화 로그인 기능이 개인 Microsoft 계정, iOS 또는 개인 Microsoft 계정을 사용 하는 Android 앱 및 Windows 10에서 개인 Microsoft 계정을 사용 하는 앱에서 구동 되는 웹 앱과 서비스와만 작동 합니다. 이러한 웹 사이트 또는 응용 프로그램의 tooone에 로그인 할 때 일반적으로 암호를 입력할 hello 페이지에 없는 링크는 **응용 프로그램을 대신 사용**합니다. 

전화 로그인 일 수 없습니다 사용된 toounlock Windows PC, XBOX 또는 프로그램 오피스 응용 프로그램 등 Microsoft 응용 프로그램의 데스크톱 버전을 모두이 이번에 있습니다. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>이 기능이 2단계 인증을 대체하나요? 기능을 꺼야 하나요?   

때때로 그렇습니다. 전화 로그인의 hello 범위를 확장 하는 중 있지만 지금은 아직도 hello Microsoft 에코 시스템에서 지원 되지 않는 위치 합니다. 해당 위치에서 안전한 로그인을 위해 2단계 인증을 사용합니다. 이런 이유로 인해 아니요, 계정에 대해 2단계 인증을 해제해서는 안됩니다. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>알겠습니다 내 계정에 대해 켜 2 단계 인증 치 려 있는 두 개의 알림을 tooapprove?

아니요, 그렇지 않습니다. 2 단계 인증으로 계산 tooyour 휴대폰으로 Microsoft 계정에에서 로그인 합니다. 암호를 입력 하지 않고 다음 신분을 확인 하 여 증명 알림을 승인 어떻게 toounlock 전화를 하 고 다음 알림을 승인 합니다. 두 번째 알림 tooapprove를 보내지 않습니다.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>내 휴대폰을 분실하거나 휴대하지 않은 경우 내 계정에 액세스하려면 어떻게 해야 하나요?  

클릭할 수 있는 항상 **대신 암호를 사용 하 여** 에서 hello 로그인 페이지 tooswitch 백업 toousing 암호입니다. 2 단계 인증을 사용 하는 경우 여전히 할 두 번째 메서드 tooverify 로그인에 염두에서에 둬야 합니다. 바로 이러한 이유로 좋습니다 toomake 회원님 계정에 추가 하 고 최신 보안 정보 한지 확인 합니다. https://account.live.com/proofs/manage에서 보안 정보를 관리할 수 있습니다. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>어떻게이 기능을 사용 하 여 중지 하 고 돌아가서 tooentering 암호?

로그인할 때 **대신 암호 사용**을 클릭합니다. 가장 최근에 선택한 기억 하 고 제공 하는 기본 hello로 다음에 로그인 할 때입니다. 휴대폰을 사용 하 여 수정할 toogo 백 toosigning 클릭 **응용 프로그램을 대신 사용**합니다. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>사용할 수 있습니까 hello 앱 toosign tooall에 내 계정 Microsoft?   
이 기능은이 이번에 개인 Microsoft 계정에만 사용할 수 있습니다. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>내 휴대폰을 사용하여 내 PC에 로그인할 수 있나요?  
사용자 PC의 경우 Windows 10의 Windows Hello에서 얼굴, 지문 또는 PIN을 사용하여 로그인하는 것이 좋습니다.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>내 Windows Phone에서 로그인할 수 있나요?  
이때 Windows Phone Microsoft Authenticator hello에 대 한이 기능을 개발 하지 않는 했습니다. 

## <a name="next-steps"></a>다음 단계
Hello Microsoft Authenticator 앱을 다운로드 하지 않은 경우 체크 아웃 합니다. hello 앱 ´ ü ± [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), 전화 로그인에 대 한 hello Microsoft 인증자 앱에서 사용할 수는 [Android](http://go.microsoft.com/fwlink/?Linkid=825072) 및 [IOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다.

Hello 앱에 대 한 질문 일반적 있으면 살펴보세요 hello [Microsoft 인증자 Faq](microsoft-authenticator-app-faq.md)
