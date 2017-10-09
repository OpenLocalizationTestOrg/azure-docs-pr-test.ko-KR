---
title: "Sipi 테스트 파일 | Microsoft Docs"
description: "테스트 파일 toocheck ReadyForTest 종속성"
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
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Sipi 테스트 파일

이 Quickstart를 통해 몇 분 이내에 Microsoft Azure Active Directory(Azure AD) B2C 테넌트에서 응용 프로그램을 등록할 수 있습니다. 완료 되 면 hello Azure B2C 테 넌 트에 사용 하기 위해 응용 프로그램 등록 됩니다.

## <a name="prerequisites"></a>필수 조건

toobuild 소비자를 등록 및 로그인을 허용 하는 응용 프로그램을 먼저 tooregister hello 응용 프로그램을 Azure Active Directory B2C 테 넌 트에 있습니다. 에 설명 된 hello 단계를 사용 하 여 자신의 테 넌 트 가져오기 [Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다.

Hello에서 hello Azure 포털에서에서 Azure AD B2C hello 블레이드에서 만든 응용 프로그램을 관리 해야 동일한 위치입니다. PowerShell 또는 다른 포털을 사용 하 여 hello B2C 응용 프로그램을 편집 하는 경우 지원 되지 않는 되며 Azure AD B2C 작동 하지 않습니다. Hello에 대 한 자세한 내용을 보려면 [응용 프로그램 오류가 발생 한](#faulted-apps) 섹션. 

## <a name="navigate-toob2c-settings"></a>TooB2C 설정 이동

Toohello 로그인 [Azure 포털](https://portal.azure.com/) 대로 hello hello B2C 테 넌 트의 전역 관리자 여야 합니다. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

등록 하는 hello 응용 프로그램 종류에 따라 다음 단계를 선택 합니다.
