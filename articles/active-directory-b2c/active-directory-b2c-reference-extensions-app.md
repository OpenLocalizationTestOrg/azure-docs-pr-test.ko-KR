---
title: "확장 앱 - Azure AD B2C | Microsoft Docs"
description: "Hello b2c 확장 앱을 복원"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: 확장 앱

Azure AD B2C 디렉터리를 만든 경우 앱 호출할 `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` hello 새 디렉터리 안에 자동으로 만들어집니다. 이 응용 프로그램, 참조 tooas hello **b2c 확장 앱**에서 볼 수 *앱 등록*합니다. 사용자 및 사용자 지정 특성에 대 한 Azure AD B2C 서비스 toostore 정보 hello에서 사용 됩니다. Hello 앱을 삭제 하는 경우 Azure AD B2C 제대로 작동 하지 않 및 프로덕션 환경에 영향을 받게 됩니다.

> [!IMPORTANT]
> Tooimmediately delete 테 넌 트 계획 하지 않는 한 hello b2c 확장 앱을 삭제 하지 마십시오. 30 일에 대 한 hello 앱 삭제 된 상태인 경우 사용자 정보를 영구적으로 손실 됩니다.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Hello 확장 앱 있는지 확인 하는 중

b2c 확장 앱 hello tooverify이 있음:

1. Azure AD B2C 테 넌 트 내에서 클릭 **더 많은 서비스** hello 왼쪽 탐색 메뉴에 있습니다.
1. **앱 등록**을 검색하여 엽니다.
1. **b2c-extensions-app**으로 시작하는 앱을 찾습니다.

## <a name="recover-hello-extensions-app"></a>Hello 확장 응용 프로그램을 복구 합니다.

30 일 toorecover hello b2c-확장-app를 실수로 삭제 한 경우 있는 것입니다. Hello Graph API를 사용 하 여 hello 응용 프로그램을 복원할 수 있습니다.

1. 너무 찾아보기[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)합니다.
1. Toorestore 삭제 hello 응용 프로그램에 대 한 원하는 hello Azure AD B2C 디렉터리에 대 한 전역 관리자 toohello 사이트에 로그인 합니다.
1. Hello URL에 대해 HTTP GET 발급 `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api 버전 1.6 = 합니다. 있는지 tooreplace 확인 `{tenantName}` 을 테 넌 트 이름입니다. 이 작업에는 지난 30 일간 hello 내에서 삭제 하는 hello 응용 프로그램의 모든 나열 됩니다.
1. Hello 응용 프로그램에서 hello 이름 ' b2c 확장 app' 및 복사로 시작 하는 hello 목록에서 찾을 해당 `objectid` 속성 값입니다.
1. Hello URL에 대해 HTTP POST 발급 `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`합니다. Hello 대체 `{OBJECTID}` hello로 hello URL의 일부 `objectid` hello 이전 단계에서 합니다. 

이제 있어야 너무[앱이 복원 hello](#verifying-that-the-extensions-app-is-present) hello Azure 포털의에서.

> [!NOTE]
> 응용 프로그램 삭제 되어 hello 내에서 지난 30 일 경우에 복원할 수 있습니다. 30일이 지난 경우 데이터는 영구적으로 손실됩니다. 추가 지원이 필요한 경우 지원 티켓을 파일로 저장합니다.
