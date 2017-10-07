---
title: "Azure AD tooan 갤러리 응용 프로그램 프로 비전 aaaUser은 기록 시간 이상이 | Microsoft Docs"
description: "이유 tooyour 응용 프로그램 프로 비전 수 있습니다 수 보다 오래 걸리는 경우 아웃 toofind 예상 하는 방법"
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Azure AD tooan 갤러리 응용 프로그램 프로 비전 하는 사용자가 기록 시간 이상

응용 프로그램에 대 한 자동 배포를 처음 설정할 경우 초기 동기화 hello hello Azure AD 디렉터리와 hello 사용자 프로 비전에 대 한 범위에가 수의 hello 크기에 따라 20 분 tooseveral 시간에서 아무 곳 이나 걸릴 수 있습니다. 

Hello 초기 동기화 후 후속 동기화 서비스를 프로 비전 하는 hello 후속 동기화 성능을 향상 시킬 수 hello 초기 동기화 후 두 시스템의 hello 상태를 나타내는 워터 마크를 저장 하는 대로 속도가 더 빨라지며 합니다.

## <a name="how-tooimprove-provisioning-performance"></a>어떻게 tooimprove 성능 프로 비전

Hello 초기 동기화에는 여러 시간 소요 되 면 tooimprove 성능 할 수 있는 한 가지 것입니다.

-   **사용자 범위 지정 필터** 범위 지정 필터를 사용 하면 사용자가 특정 특성 값을 기반으로 필터링 하 여 Azure AD에서 프로 비전 서비스 추출 hello toofine 조정 hello 데이터입니다. 범위 지정 필터에 대한 자세한 내용은 [범위 지정 필터를 사용한 특성 기반 응용 프로그램 프로비전](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)

