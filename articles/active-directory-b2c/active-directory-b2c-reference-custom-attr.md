---
title: "Azure Active Directory B2C: 사용자 지정 특성 | Microsoft Docs"
description: "소비자에 대 한 Azure Active Directory B2C toocollect 정보에 toouse 사용자 지정 특성 하는 방법"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active Directory B2C: 소비자에 대 한 사용자 지정 특성 toocollect 정보를 사용 합니다.
Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호 등 기본 제공 정보(특성) 집합이 함께 제공됩니다. 그러나 모든 소비자 용 응용 프로그램에 어떤 특성 toogather는 소비자에 고유한 요구 사항이 있습니다. Azure AD B2C hello 각 소비자 계정에 저장 하는 특성 집합을 확장할 수 있습니다. Hello에 사용자 지정 특성을 만들 수 있습니다 [Azure 포털](https://portal.azure.com/) 아래와 같이 등록 정책에 사용 합니다. 또한 읽고 수 hello를 사용 하 여 이러한 특성을 쓸 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)합니다.

> [!NOTE]
> 사용자 지정 특성은 [Azure AD Graph API 디렉터리 스키마 확장](https://msdn.microsoft.com/library/azure/dn720459.aspx)을 사용합니다.
> 
> 

## <a name="create-a-custom-attribute"></a>사용자 지정 특성 만들기
1. [이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.
2. **사용자 특성**을 클릭합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 제공 된 **이름** hello 사용자 지정 특성 (예: "ShoeSize") 및 필요에 따라는 **설명**합니다. **만들기**를 클릭합니다.
   
   > [!NOTE]
   > 만 "문자열" hello **데이터 형식** 를 현재 사용할 수 있습니다.
   > 
   > 

hello 사용자 지정 특성은 현재 hello 목록이 **사용자 특성**, 되며 등록 정책에 사용할 수 있습니다.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>등록 정책에 사용자 지정 특성 사용
1. [이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.
2. **등록 정책**을 클릭합니다.
3. 등록 정책 (예: "B2C_1_SiUp") tooopen 클릭 것입니다. 클릭 **편집** hello hello 블레이드 위쪽에 있습니다.
4. 클릭 **등록 특성** 및 선택 hello 사용자 지정 특성 (예: "ShoeSize"). **확인**을 클릭합니다.
5. 클릭 **응용 프로그램 클레임** 및 선택 hello 사용자 지정 특성입니다. **확인**을 클릭합니다.
6. 클릭 **저장** hello hello 블레이드 위쪽에 있습니다.

Hello 정책 tooverify hello 소비자 경험에 hello "지금 실행" 기능을 사용할 수 있습니다. 이제 "ShoeSize" 소비자를 등록 하는 동안 수집 된 특성의 hello 목록에서 참조 하 고 hello 토큰 보낸된 백 tooyour 응용 프로그램에서 참조 해야 합니다.

## <a name="notes"></a>참고 사항
* 등록 정책과 함께 등록 또는 로그인 정책 및 프로필 편집 정책에서 사용자 지정 특성을 사용할 수도 있습니다.
* 사용자 지정 특성의 알려진 제한 사항이 있습니다. Hello 처음으로 사용 되는 정책에서 만든 에게만 고 toohello 목록을 추가할 때가 아니라 **사용자 특성**합니다.

