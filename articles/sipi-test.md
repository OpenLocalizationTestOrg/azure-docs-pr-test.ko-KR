---
title: "Sipi 테스트 파일 | Microsoft Docs"
description: "ReadyForTest 종속성을 확인 하는 파일을 테스트"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Sipi 테스트 파일

이 Quickstart를 통해 몇 분 이내에 Microsoft Azure Active Directory(Azure AD) B2C 테넌트에서 응용 프로그램을 등록할 수 있습니다. 완료되면 Azure B2C 테넌트에서 사용할 수 있도록 응용 프로그램이 등록됩니다.

## <a name="prerequisites"></a>필수 조건

소비자 등록 및 로그인을 수락하는 응용 프로그램을 만들려면 먼저 Azure Active Directory B2C 테넌트를 사용하여 해당 응용 프로그램을 등록해야 합니다. [Azure AD B2C 테넌트 만들기](active-directory-b2c-get-started.md)에 요약한 단계를 사용하여 자신의 테넌트를 가져옵니다.

Azure Portal의 Azure AD B2C 블레이드에서 만든 응용 프로그램은 동일한 위치에서 관리되어야 합니다. PowerShell 또는 다른 포털을 사용하여 B2C 응용 프로그램을 편집할 경우 지원을 받을 수 없게 되며 Azure AD B2C에 작동하지 않습니다. [오류가 발생한 앱](#faulted-apps) 섹션에서 자세한 내용을 참조하세요. 

## <a name="navigate-to-b2c-settings"></a>B2C 설정으로 이동

B2C 테넌트의 전역 관리자로 [Azure Portal](https://portal.azure.com/)에 로그인합니다. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

등록하려는 응용 프로그램 형식에 따라 다음 단계를 선택합니다.
