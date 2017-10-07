---
title: "aaaManage 2 단계 확인 설정을 | Microsoft Docs"
description: "연락처 정보를 변경하거나 장치를 구성하는 등 Azure Multi-Factor Authentication을 사용하는 방법을 관리합니다."
services: multi-factor-authentication
keywords: "다단계 인증 클라이언트, 인증 문제, 상관관계 ID"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>2단계 인증을 위한 설정 관리
이 문서는 방법에 대 한 질문에 대답 2 단계 확인 또는 multi-factor authentication에 대 한 tooupdate 설정 합니다. Tooyour 계정에 로그인 하는 데 문제가 있는 경우 참조 너무[2 단계 인증에 문제가](multi-factor-authentication-end-user-troubleshoot.md) 문제 해결 도움말에 대 한 합니다.

## <a name="where-toofind-hello-settings-page"></a>여기서 toofind hello 설정 페이지
회사에서 Azure Multi-Factor Authentication을 설정하는 방법에 따라 전화 번호와 같은 설정을 변경할 수 있는 몇 가지 위치가 있습니다.

IT 관리자는 특정 URL 또는 단계 toomanage 2 단계 인증을 보내는 경우 이러한 지침을 따릅니다. 그렇지 않으면도 다른 모든 사용자에 대 한 지침을 진행 하는 hello 작동 해야 합니다. 다음이 단계를 수행 해도 표시 되지 않는 경우 회사 또는 학교 자신의 포털을 사용자 지정한 것을 의미 하는 동일한 옵션 hello 합니다. Hello 링크 tooyour Azure Multi-factor Authentication 포털 관리자에 게 요청 합니다.

1. 역시 로그인[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. 오른쪽 위 hello에에서 계정 이름을 선택 하 고 선택 **프로필**합니다.  
3. **추가 보안 인증**을 선택합니다.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. hello 추가 보안 인증 페이지 설정을 로드합니다.

    ![검사](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>원하는 toochange 내 전화 번호를 I 또는 보조 번호 추가
중요 한 tooconfigure 보조 인증 전화 번호를 사용 하는 경우  기본 전화 번호 및 모바일 앱 때문에 아마도 hello에 동일한 전화, hello 보조 전화 번호는 hello 유일한 방법은 전화기를 분실 하거나 도난당 하는 경우 사용자의 계정으로 다시 수 tooget를 수 있습니다.

> [!NOTE]
> 액세스 tooyour 기본 전화 번호 tooyour 계정에서 시작 하는 데 도움이 필요한 있지 않을 경우이 도움말 항목을 참조 [2 단계 인증에 문제가](multi-factor-authentication-end-user-troubleshoot.md)합니다.  

**toochange 기본 전화 번호:**  

1. Hello 추가 보안 확인 페이지에서 현재 전화 번호로 hello 텍스트 상자를 선택 하 고 새 전화 번호와 편집 합니다.  
2. **저장**을 선택합니다.  
3. 기본 확인 옵션에 대해 사용 하는 hello 번호를 저장 하기 전에 tooverify hello 새 여러를 가지입니다.  

**tooadd 보조 전화 번호:**  

1. Hello 추가 보안 확인 페이지에서 확인란 hello 다음 너무**대체 인증 전화 합니다.**  
2. Hello 텍스트 상자에 보조 전화 번호를 입력 합니다.  
3. **저장**을 선택하면 변경 내용이 완료됩니다.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>신뢰할 수 있는 것으로 표시된 장치에서 2단계 인증이 다시 필요

조직 설정에 따라 브라우저에서 2단계 인증을 수행할 때 "**X**일 동안 다시 묻지 않음"이라는 확인란이 포함될 수 있습니다. 이 확인란을 선택 하 고 다음 장치 분실 또는 사용자 계정이 손상 되 생각 하는 경우에 장치를 2 단계 확인 tooall 복원 해야 합니다. 

1. Hello 추가 보안 확인 페이지에서 선택 **이전에 신뢰할 수 있는 장치에서 multi-factor authentication 복원**합니다.
2. hello 다음에 모든 장치에서 로그인 할 수 증명된 tooperform 2 단계 인증 수 있습니다. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>어떻게 오래 된 장치에서 Microsoft 인증자를 정리 하 고 새 tooa 이동?
Hello 앱 장치나 hello 재설정 한 장치를 제거 해도 hello 백 엔드에서 hello 정품 인증을 제거 하지 않습니다. 자세한 내용은 [Microsoft Authenticator](microsoft-authenticator-app-how-to.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
* [2단계 인증에 문제 발생](multi-factor-authentication-end-user-troubleshoot.md)에 대한 문제 해결 팁 및 도움말 얻기
* 2단계 인증을 지원하지 않는 앱에 대해 [앱 암호](multi-factor-authentication-end-user-app-passwords.md) 설정.
