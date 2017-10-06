---
title: "Azure Active Directory B2C: Azure Active Directory B2C 테넌트 만들기 | Microsoft Docs"
description: "Toocreate Azure Active Directory B2C 테 넌 트의 항목을"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Hello Azure 포털에서에서 Azure Active Directory B2C 테 넌 트 만들기

Sipi가 편집 합니다.

이 Quickstart를 통해 몇 분 이내에 Microsoft Azure AD(Azure Active Directory) B2C 테넌트를 만들 수 있습니다. 완료 되 면 B2C 응용 프로그램을 등록 하기 위한 B2C 테 넌 트 toouse를 해야 합니다.

## <a name="prerequisites"></a>필수 조건

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>TooAzure 로그인

Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

## <a name="create-an-azure-ad-b2c-tenant"></a>Azure AD B2C 테넌트 만들기

B2C 기능은 기존 테넌트에 사용할 수 없습니다. Azure AD B2C 테 넌 트 toocreate가 필요합니다.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

축하합니다. Azure Active Directory B2C 테넌트를 만들었습니다. Hello 테 넌 트의 전역 관리자가. 필요에 따라 다른 전역 관리자를 추가할 수 있습니다. tooswitch tooyour 새 테 넌 트를 hello 클릭 *새로운 테 넌 트 연결 관리*합니다.

![새 테넌트 연결 관리](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Toouse 프로덕션 응용 프로그램에 대 한 B2C 테 넌 트가 계획에 hello 문서를 읽어 보세요. [미리 보기 B2C 테 넌 트 및 프로덕션 규모](active-directory-b2c-reference-tenant-type.md)합니다. 알려진 문제 기존 B2C를 삭제 하는 경우 테 넌 트 및 다시 hello로 만드는 동일한 도메인 이름입니다. 다른 도메인 이름의 B2C 테 넌 트 toocreate가 필요합니다.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>테 넌 트 tooyour 구독 연결

Toolink 해야 Azure AD B2C 테 넌 트 tooyour Azure 구독 tooenable 모든 B2C 기능 및 사용 요금에 대 한 비용을 지불 합니다. toolearn 더 읽기 [이 여기서](active-directory-b2c-how-to-enable-billing.md)합니다. Azure AD B2C 테 넌 트 tooyour Azure 구독을 연결 하지 않는 경우 일부 기능이 액세스가 차단 되 고 ("연결 된 toothis B2C 테 넌 트 또는 구독 hello 구독이 필요 주의.") hello B2C 설정에서 경고 메시지가 표시 됩니다. 프로덕션에 앱을 전달하기 전에 이 단계를 수행해야 합니다.

## <a name="easy-access-toosettings"></a>쉽게 액세스할 수 있도록 toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

입력 하 여 hello 블레이드에 액세스할 수도 있습니다 `Azure AD B2C` 에 **리소스 검색** hello 위쪽 hello 포털의. Hello 결과 목록에서 선택 **Azure AD B2C** tooaccess hello B2C 설정 블레이드에서 합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [B2C 테넌트에 B2C 응용 프로그램 등록](active-directory-b2c-app-registration.md)
