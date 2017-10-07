---
title: "사용자 지정 개발 응용 프로그램에 대 한 특정 필드 aaaHow toofill | Microsoft Docs"
description: "설명서 관련 아웃 toofill 때 필드 어떻게에 Azure AD와 사용자 지정 개발 된 응용 프로그램 등록 하는"
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
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>어떻게 toofill 개발 된 응용 프로그램에 대 한 특정 필드

이 문서에서 hello 응용 프로그램 등록 양식에 나와 있는 모든 hello 사용 가능한 필드에 대 한 간단한 설명은에서 알려 hello [Azure 포털](https://portal.azure.com)합니다.

## <a name="register-a-new-application"></a>새 응용 프로그램 등록

-   새 응용 프로그램을 tooregister 이동 toohello [Azure 포털](https://portal.azure.com)합니다.

-   Hello 왼쪽된 탐색 창에서 클릭 **Azure Active Directory 합니다.**

-   **앱 등록**을 선택하고 **추가**를 클릭합니다.

-   응용 프로그램 등록 양식에 나와 hello 열고 합니다.

## <a name="fields-in-hello-application-registration-form"></a>응용 프로그램 등록 양식에 나와 hello의 필드


| 필드            | 설명                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| 이름             | hello 응용 프로그램의 hello 이름입니다. 최소 4자 이상이어야 합니다.                |
| 응용 프로그램 형식 | **웹앱/웹 API**: 웹 응용 프로그램, 웹 API 또는 둘 다를 나타내는 응용 프로그램 
| |**네이티브**: 사용자 장치 또는 컴퓨터에 설치할 수 있는 응용 프로그램           |
| 로그온 URL      | 사용자가 로그인 수 있는 toouse에 응용 프로그램 hello URL                                  |

Hello 응용 프로그램 hello Azure 포털에에서 등록 되며 리디렉션할 수 필드 위에 hello를 입력 했으면 toohello 응용 프로그램 페이지. hello **설정을** hello 응용 프로그램 창에서 단추 응용 프로그램 있는 더 많은 필드를 toocustomize hello 설정 페이지를 엽니다. hello 표에서 hello 설정 페이지의 모든 hello 필드를 설명합니다. 웹 응용 프로그램을 만들었는지 네이티브 응용 프로그램을 만들었는지 여부에 따라 이러한 필드의 하위 집합만 표시됩니다.

| 필드           | 설명                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 응용 프로그램 UI  | 응용 프로그램을 등록하면 Azure AD에서 응용 프로그램에 응용 프로그램 ID를 할당합니다. hello 응용 프로그램 ID를 사용할 수 있습니다 toouniquely hello Graph API와 같은 tooaccess 리소스를 비롯 하 여 인증 요청 tooAzure AD에 응용 프로그램을 식별 합니다.                                                          |
| 앱 ID URI      | 이 hello 폼의 일반적으로 고유 URI 이어야 합니다 **https://&lt;테 넌 트\_이름&gt;/&lt;응용 프로그램\_이름&gt;합니다.** 이 대 한 hello 토큰을 발급 해야 고유 식별자 toospecify hello 리소스로 hello 권한 부여 흐름 이라고 하는 동안 사용 됩니다. 또한 aud' hello' 클레임 발급 hello 액세스 토큰에 됩니다. |
| 새 로고 업로드 | 응용 프로그램에 대 한이 tooupload 로고를 사용할 수 있습니다. hello 로고.bmp,.jpg 또는.png 형식 이어야 하 고 hello 파일 크기는 100KB 보다 작아야 이어야 합니다. hello hello 이미지 크기는 94x94 픽셀의 중앙 이미지 크기와 215x215 픽셀 이어야 합니다.                                                       |
| 홈페이지 URL   | 이 hello 로그온 URL 응용 프로그램 등록 중에 지정 합니다.                                                                                                                                                                                                                                              |
| 로그아웃 URL      | 이 hello single sign-out 로그 아웃 URL입니다. Azure AD에서 로그 아웃 요청 toothis URL hello 사용자 Azure AD와의 세션의 선택을 취소 사용 하 여 보냅니다 다른 등록된 응용 프로그램입니다.                                                                                                                                       |
| 다중 테넌트  | 이 스위치는 여러 테 넌 트에서 hello 응용 프로그램을 사용할 수 있는지 여부를 지정 합니다. 이 경우 일반적으로 외부 조직의 테 넌 트에 등록 및 액세스 tootheir 조직의 데이터를 부여 하 여 응용 프로그램을 사용할 수 있습니다.                                                                   |
| 회신 URL      | hello 회신 Url은 Azure AD 응용 프로그램을 요청 하는 모든 토큰을 반환 하는 위치 hello 끝점입니다.                                                                                                                                                                                                          |
| 리디렉션 URI   | 네이티브 응용 프로그램에 대 한 hello 사용자 권한 부여 성공 하는 보낸된 toofollowing 여야 하는 위치입니다. Hello 하는 azure AD 검사 리디렉션 URI hello OAuth 2.0으로에서 프로그램 응용 프로그램 공급 요청 hello 포털에서 등록 된 hello 값 중 하 나와 일치 합니다.                                                            |
| 구성            | 키 tooprogrammatically web Api에 액세스 사용자 개입 없이 Azure AD에서 보호를 만들 수 있습니다. Hello에서 \* \*키\* \* 페이지 키 설명 및 hello 만료 날짜를 입력 하 고 toogenerate hello 키를 저장 합니다. 수 tooaccess 됩니다 어딘가에 secure 있는지 toosave 조화 나중입니다.             |

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
