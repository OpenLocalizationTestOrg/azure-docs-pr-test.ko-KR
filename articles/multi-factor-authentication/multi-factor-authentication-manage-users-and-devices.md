---
title: "사용자 및 장치-Azure MFA aaaAdmins 관리 | Microsoft Docs"
description: "이 방법을 hello 사용자 toodo 강제 적용 하는 등 사용자 설정을 toochange 안녕 증명 프로세스를 설명 합니다."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Hello 클라우드에서 Azure Multi-factor authentication 사용자 설정 관리
관리자는 다음 사용자 및 장치 설정을 hello를 관리할 수 있습니다.

* 사용자가 tooprovide 연락 방법을 다시 필요
* 앱 암호 삭제
* 모든 신뢰할 수 있는 장치에서 MFA 요청 

## <a name="require-users-tooprovide-contact-methods-again"></a>사용자가 tooprovide 연락 방법을 다시 필요
이 설정을 강제로 hello 사용자 toocomplete hello 등록 프로세스를 다시 수행합니다. 비 브라우저 앱 hello 사용자에에 대 한 앱 암호는 toowork를 계속 합니다.  선택 하 여 hello 사용자가 앱 암호를 삭제할 수 있습니다 **hello 선택한 사용자가 생성 하는 모든 기존 앱 암호 삭제**합니다.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>어떻게 toorequire 사용자 tooprovide 연락 방법 다시
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽에서 선택 **Azure Active Directory** > **사용자 및 그룹** > **모든 사용자에 게**합니다.
3. **Multi-Factor Authentication**을 선택합니다. hello 다단계 인증 페이지가 열립니다. 
4. Hello 상자 다음 toohello 사용자 또는 사용자가 원하는 toomanage 확인 합니다. 빠른 단계 옵션 목록이 hello 오른쪽에 나타납니다. 
5. **Manage user settings**(사용자 설정 관리)를 선택합니다.
6. 에 대 한 hello 확인란 **선택한 사용자가 연락 방법을 다시 tooprovide**합니다.
   ![연락처 메서드 제공](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. **저장**을 클릭합니다.
8. **닫기**를 클릭합니다.

## <a name="delete-users-existing-app-passwords"></a>사용자 기존 앱 암호 삭제
이 설정은 모든 사용자가 만든 hello 앱 암호를 삭제 합니다. 이러한 앱 암호와 연결된 브라우저가 아닌 앱은 새 앱 암호가 생성될 때까지 작동 중지됩니다.

### <a name="how-toodelete-users-existing-app-passwords"></a>어떻게 toodelete 사용자가 기존 앱 암호
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽에서 선택 **Azure Active Directory** > **사용자 및 그룹** > **모든 사용자에 게**합니다.
3. **Multi-Factor Authentication**을 선택합니다. hello 다단계 인증 페이지가 열립니다. 
6. Hello 상자 다음 toohello 사용자 또는 사용자가 원하는 toomanage 확인 합니다. 빠른 단계 옵션 목록이 hello 오른쪽에 나타납니다. 
7. **Manage user settings**(사용자 설정 관리)를 선택합니다.
8. 에 대 한 hello 확인란 **hello 선택한 사용자가 생성 하는 모든 기존 앱 암호 삭제**합니다.
   ![앱 암호 삭제](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. **저장**을 클릭합니다.
10. **닫기**를 클릭합니다.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>사용자에 대해 기억된 모든 장치에서 MFA 복원
Hello 옵션 toomark 장치 장치를 신뢰할 수 있는 사용자에 게 부여는 Azure Multi-factor Authentication의 hello 구성 가능한 기능 중 하나입니다. 자세한 내용은 [Azure Multi-Factor Authentication 설정 구성](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust)을 참조하세요.

사용자는 일반 장치에서 구성 가능한 일 수 동안 2단계 인증을 옵트아웃(opt out)할 수 있습니다. 계정이 손상 되는 신뢰할 수 있는 장치를 분실, toobe 수 tooremove hello 신뢰할 수 있는 상태 필요 하 고 다시 2 단계 인증을 요구 합니다.

hello **모든 기억 된 장치에서 multi-factor authentication 복원** 설정은 의미 된 hello 수 문제가 tooperform 2 단계 확인 hello 다음 toomark을 선택 여부에 관계 없이,에 로그인 할 때 자신의 신뢰할 수 있는 장치입니다. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>어떻게 MFA toorestore 사용자에 대 한 모든 일시 중단 된 장치에서
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽에서 선택 **Azure Active Directory** > **사용자 및 그룹** > **모든 사용자에 게**합니다.
3. **Multi-Factor Authentication**을 선택합니다. hello 다단계 인증 페이지가 열립니다. 
6. Hello 상자 다음 toohello 사용자 또는 사용자가 원하는 toomanage 확인 합니다. 빠른 단계 옵션 목록이 hello 오른쪽에 나타납니다. 
7. **Manage user settings**(사용자 설정 관리)를 선택합니다.
8. 에 대 한 hello 확인란 **모든 기억 된 장치에서 multi-factor authentication 복원**
   ![앱 암호 삭제](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. **저장**을 클릭합니다.
10. **닫기**를 클릭합니다.

## <a name="next-steps"></a>다음 단계

- 방법에 대 한 자세한 정보를 너무 가져오기[Azure Multi-factor Authentication 구성 설정](multi-factor-authentication-whats-next.md)

- 사용자에 게 도움이 필요한 경우 가리킵니다에 hello [2 단계 인증에 대 한 사용자 가이드](./end-user/multi-factor-authentication-end-user.md)
