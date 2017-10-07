---
title: "Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함 | Microsoft Docs"
description: "Toodisable 소비자 Azure Active Directory B2C에 등록 하는 동안 확인 메일 하는 방법을 보여 주는 항목"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함
사용 하도록 설정 하면 소비자 (Azure AD) Azure Active Directory B2C 제공 전자 메일 주소를 제공 하 여 로컬 계정을 만들어 응용 프로그램에 대해 기능 toosign을 hello 합니다. Azure AD B2C 소비자 tooverify 요구 하 여 유효한 전자 메일 주소를 사용 하면 hello 등록 프로세스 중에 해당 합니다. 또한 악성 자동화 된 프로세스를에서 hello 응용 프로그램에 대 한 가짜 계정을 생성할 수 없습니다.

일부 응용 프로그램 개발자가 선호 하는 hello 등록 프로세스 동안 tooskip 전자 메일 확인 하 고 소비자도 대신 나중에 hello 전자 메일 주소를 확인 합니다. 이 Azure AD B2C 수 toosupport 수 구성된 toodisable 전자 메일을 확인 합니다. 이렇게 원활 하 게 등록 프로세스를 생성 하 고 적용 되지 않은 이러한 소비자에서 메일 주소를 확인 하는 hello 유연성 toodifferentiate hello 소비자에서는 개발자가 있습니다.

기본적으로 등록 정책에는 전자 메일 확인 기능이 켜져 있습니다. 사용 하 여 hello 단계 tooturn 다음 그 오프:

1. [이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.
2. 등록 구성 방식에 따라 **등록 정책** 또는 **등록 또는 로그인 정책**을 클릭합니다.
3. 정책 (예: "B2C_1_SiUp") tooopen 클릭 것입니다. 클릭 **편집** hello hello 블레이드 위쪽에 있습니다.
4. **페이지 UI 사용자 지정**을 클릭합니다.
5. **로컬 계정 등록 페이지**를 클릭합니다.
6. 클릭 **전자 메일 주소** hello에 **이름** hello 아래의 열 **등록 특성** 섹션.
7. 설정/해제 hello **영역에 있는 모든** 옵션**아니요**합니다.
8. 클릭 **확인** hello에 도달할 때까지 hello 아래쪽 **정책 편집** 블레이드입니다.
9. 클릭 **저장** hello hello 블레이드 위쪽에 있습니다. 완료되었습니다!

> [!NOTE]
> Hello 등록 프로세스에서 전자 메일 확인을 사용 하지 않도록 설정 하면 toospam을 발생할 수 있습니다. Hello 기본을 비활성화 하면 사용자 고유의 인증 시스템을 추가 하는 것이 좋습니다.
> 
> 

우리는 항상 열려 toofeedback 및 제안을! 이 항목에 문제가 발생 하거나이 콘텐츠를 개선 하기 위한 권장 사항이 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다. 기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.
