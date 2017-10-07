---
title: "Azure Active Directory B2C: 셀프 서비스 암호 재설정 | Microsoft Docs"
description: "Azure Active Directory B2C에 소비자에 대 한 tooset 셀프 서비스 암호를 다시 설정 하는 방법을 보여 주는 항목"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: 소비자를 위해 셀프 서비스 암호 재설정 설정
Hello로 셀프 서비스 암호 재설정 기능, 소비자 (로컬 계정에 등록 한)가 자체적으로 암호를 재설정할 수 있습니다. 특히 응용 프로그램에 수백만 정기적으로 사용 하는 소비자의 경우 지원 담당자의 부담을 hello 상당히 감소 합니다. 현재 검증된 전자 메일 주소를 지원 복구 방법으로 사용하여 지원합니다. 추가 복구 방법 (예: 확인 된 전화 번호, 보안 질문, 등) hello 미래에 추가 합니다.

> [!NOTE]
> 이 문서 적용 tooself 서비스 암호 재설정 로그인 정책 hello 축을 사용 합니다. 완전히 사용자 지정 가능한 암호 재설정 정책이 앱에서 호출되어야 하는 경우 [이 문서](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)를 참조하세요.
> 
> 

기본적으로 디렉터리는 셀프 서비스 암호 재설정을 설정하지 않습니다. 사용 하 여 hello 단계 tooturn 다음 그에:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 구독 관리자 hello으로 합니다. 이 hello 회사 또는 학교 계정 또는 같은 Microsoft 계정을 사용 하 여 toocreate 디렉터리 hello 동일 합니다.
2. Hello 왼쪽에 표시 되는 hello 탐색 모음의 toohello Active Directory 확장을 이동 합니다.
3. Hello에서 디렉터리 찾기 **디렉터리** 탭을 클릭 합니다.
4. Hello 클릭 **구성** 탭 합니다.
5. Toohello 아래로 스크롤하여 **사용자 암호 재설정 정책** 섹션, 토글 hello **암호 재설정을 위해 사용할 수 있는 사용자** 옵션**예**합니다. 해당 hello 확인 **대체 전자 메일 주소** 그대로 둡니다; 옵션을 선택 합니다.
   
    ![셀프 서비스 암호 재설정](./media/active-directory-b2c-reference-sspr/sspr.png)
6. 클릭 **저장** hello hello 페이지 맨 아래에 있습니다. 완료되었습니다!

tootest에 로컬 계정이 id 공급자로 모든 로그인 정책에서 사용 하 여 hello "지금 실행" 기능입니다. Hello 로컬 계정 로그인 페이지 (입력할 수 있는 전자 메일 주소 및 암호 또는 사용자 이름 및 암호)를 클릭 하 여 **계정에 액세스할 수 있습니까?** tooverify hello 소비자 경험 합니다.

> [!NOTE]
> hello 셀프 서비스 암호 재설정 페이지 사용자 지정 하는 hello를 사용 하 여 [회사 브랜딩 기능](../active-directory/active-directory-add-company-branding.md)합니다.
> 
> 

