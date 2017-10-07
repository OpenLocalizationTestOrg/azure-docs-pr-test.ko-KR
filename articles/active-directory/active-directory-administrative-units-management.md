---
title: "Azure Active Directory에서 aaaAdministrative 단위 관리 미리 보기"
description: "Azure Active Directory에서 보다 세부적인 권한 위임을 위해 관리 단위 사용"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Azure AD의 관리 단위 관리 - 공용 미리 보기
이 문서에서는 새 Azure Active Directory 컨테이너에 관리 권한을 위임 하 고 일부 사용자 및 사용자의 적용 정책 tooa 하위 집합을 통해 사용할 수 있는 리소스의 관리 단위를 설명 합니다. Azure Active Directory에서 관리 단위 중앙 관리자 toodelegate 권한 tooregional 관리자 또는 세부적인 수준에서 tooset 정책을 사용합니다.

이는 각각 독립된 많은 자치 학교(경영대학, 공과대학 등)로 구성된 종합 대학교와 같이 독립된 부서가 있는 조직에서 유용합니다. 그러한 부서는 자체 IT 관리자를 통해 액세스를 제어하고, 사용자를 관리하고, 특히 부서에 대한 정책을 설정합니다. 중앙 관리자에는 특정 부문의 사용자 hello로 toobe 수 grant 이러한 부문 관리자 권한을 사용 하려고 합니다. 보다 구체적으로,이 예제를 사용 하면 중앙 관리자 수 예를 들어, 특정 학교 (경영 대학원)에 대 한 관리 단위를 만들고 경영 대학원 사용자만 hello 채웁니다. 그런 다음 중앙 관리자 hello 경영 대학원 IT 직원 tooa 범위가 지정 된 역할, 역할 즉, grant hello IT 직원의 비즈니스 학교 hello 경영 대학원 관리 단위에 대해서만 관리 권한 추가할 수 있습니다.

> [!IMPORTANT]
> Azure Active Directory Premium을 사용하도록 설정한 경우에만 관리 단위 범위가 지정된 관리자 역할을 할당할 수 있습니다. 자세한 내용은 [Azure AD Premium 시작을 참조하세요](active-directory-get-started-premium.md).
>


Hello 중앙 관리자의 관점에서 관리 단위 만들고 데이터를 자원으로 채울 수 있는 디렉터리 개체입니다. **이 미리 보기 릴리스에서는 사용자만 이 리소스가 될 수 있습니다.** 만들어지고 채워지며, 되 면 hello 관리 단위에 포함 된 리소스에 대해서만 권한 부여 범위 toorestrict hello로 hello 관리 단위를 사용할 수 있습니다.

## <a name="managing-administrative-units"></a>관리 단위 관리
이 미리 보기 릴리스에서 수 만들고 hello Azure Active Directory 모듈에 대 한 Windows PowerShell cmdlet을 사용 하 여 관리 단위 관리 합니다. toolearn 방법에 대 한 자세한 참조 하는 toodo [관리 단위 작업](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Hello 구문, 매개 변수 설명 및 예제를 포함 하 여 관리 단위를 관리 하기 위한 Azure AD 모듈 cmdlet에 대 한 내용은 및 소프트웨어 요구 사항 및 설치 hello Azure AD 모듈에 대 한 자세한 내용은 참조 [Azure Active PowerShell 디렉터리](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0)합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory 버전](active-directory-editions.md)
