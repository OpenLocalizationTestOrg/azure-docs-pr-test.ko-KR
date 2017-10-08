---
title: "MFA aaaAzure 로그인 2 단계 확인 | Microsoft Docs"
description: "이 페이지 있습니다 지침을 제공 합니다 여기서 toogo toosee hello 다양 한 로그인 방법이 Azure MFA를 사용할 수 있습니다."
keywords: "사용자 인증, 로그인 환경, 휴대폰으로 로그인, 사무실 전화로 로그인"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Azure Multi-factor authentication hello 로그인 환경
> [!NOTE]
> hello이 문서의 목적은 일반적인 로그인 환경을 통해 toowalk입니다. 로그인 또는 tootroubleshoot 문제 관련 도움말을 참조 [Azure Multi-factor Authentication에 문제가](multi-factor-authentication-end-user-troubleshoot.md)합니다.

## <a name="what-will-your-sign-in-experience-be"></a>어떤 로그인 환경이 제공되나요?
사용자 로그인 환경에 선택한 항목 toouse에 두 번째 요소로 따라 달라 집니다: 전화 통화, 인증 앱을 사용할지 아니면 텍스트입니다. 가장 잘 진행 중에 작업을 설명 하는 hello 옵션을 선택 합니다.

| 로그인하는 방법 | 
| --- |
| [전화 통화 toomy 휴대폰 / 사무실 전화](#signing-in-with-a-phone-call) |
| [Toomy 휴대폰 문자 사용](#signing-in-with-a-text-message)
| [Hello Microsoft 인증자 앱에서 알림](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Hello Microsoft 인증자 앱에서 확인 코드 사용](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [원하는 방법이 없으므로 다른 방법 사용](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>전화 통화를 사용하여 로그인
다음 정보는 hello 호출 tooyour 모바일 경험이 2 단계 확인 hello 또는 사무실 전화를 설명 합니다.

1. Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.  
2. Microsoft에서 전화를 합니다.  
3. Hello 전화에 답변 하 고 hello # 키를 누르십시오.  

## <a name="signing-in-with-a-text-message"></a>문자 메시지를 사용하여 로그인
다음 정보는 hello 메시지 tooyour 텍스트 휴대폰 경험이 2 단계 확인 hello를 설명 합니다.

1. Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다. 
2. Microsoft에서 숫자 코드를 포함하는 문자 메시지를 보냅니다. 
3. Hello 로그인 페이지에 제공 된 hello 상자에 hello 코드를 입력 합니다. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Hello Microsoft Authenticator 앱을 사용 하 여 로그인 
hello 다음 설명 hello Microsoft Authenticator 앱을 사용 하 여 2 단계 확인 작업에 대 한 hello 환경입니다. 두 가지 방법으로 toouse hello 앱 가지가 있습니다. 사용자의 장치에 푸시 알림을 받을 수 있습니다 또는 hello 앱 tooget 확인 코드를 열 수 있습니다.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>hello Microsoft 인증자 앱에서 알림 사용 하 여 toosign
1. Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.
2. Microsoft는 장치에서 알림 toohello Microsoft Authenticator 앱을 보냅니다.

  ![Microsoft가 알림을 보냄](./media/multi-factor-authentication-end-user-signin/notify.png)

3. 전화 및 선택 hello에 대 한 열기 hello 알림 **확인** 키입니다. 회사에서 PIN을 요구하는 경우 여기에 입력합니다.
4. 사용자가 로그인됩니다.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>확인 코드를 사용 하 여 hello Microsoft Authenticator 앱과 toosign

Hello Microsoft Authenticator 앱 tooget 확인 코드를 사용 하는 경우 다음 hello 앱을 열 때 표시 숫자 계정 이름. 이 수 동일 수를 두 번 hello를 사용 하지 않는 하도록 30 초 마다 변경 합니다. 확인 코드를 묻는 경우 hello 앱 열고 수에 관계 없이 현재 표시를 사용 합니다. 

1. Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.
2. Microsoft가 확인 코드를 요구합니다.

  ![확인 코드 입력](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. 휴대폰에서 hello Microsoft Authenticator 앱을 열고 hello 상자에 로그인 하는 위치에 hello 코드를 입력 합니다.

## <a name="signing-in-with-an-alternate-method"></a>다른 방법을 사용하여 로그인
경우에 따라 hello 전화 번호 또는 기본 설정된 확인 방법으로 설정 하는 장치 않아도 됩니다. 계정에 대해 백업 방법을 설정하도록 권장하는 것도 이 때문입니다. hello 다음 섹션에서는 기본 방법을 사용 하지 못할 경우 다른 방법 사용 하 여 toosign 합니다.

1. Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.
2. **다른 확인 옵션 사용**을 선택합니다. 설정한 수에 따라 다른 확인 옵션이 표시됩니다.
3. 대체 방법을 선택하고 로그인합니다.

  ![대체 방법 사용](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>다음 단계

2단계 확인을 사용하여 로그인하는 동안 문제가 발생하면 [Azure Multi-Factor Authentication에 문제가 있는 경우](multi-factor-authentication-end-user-troubleshoot.md)에서 자세한 정보를 확인하세요.

너무 방법에 대해 알아봅니다[2 단계 확인 설정 관리](multi-factor-authentication-end-user-manage-settings.md)합니다.

너무 방법을 보려면[hello Microsoft Authenticator 앱 시작](microsoft-authenticator-app-how-to.md) 알림 toosign, 텍스트 및 전화 통화가 대신 사용할 수 있도록 합니다. 
