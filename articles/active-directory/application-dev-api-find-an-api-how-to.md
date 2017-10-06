---
title: "사용자 지정 개발 응용 프로그램에 필요한 특정 API aaaHow toofind | Microsoft Docs"
description: "사용자 지정에는 특정 API tooaccess 필요한 tooconfigure hello 사용 권한을 Azure AD 응용 프로그램을 개발 하는 방식"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>사용자 지정 개발 응용 프로그램에 toofind 특정 API 필요한 하는 방법

액세스 tooAPIs 액세스 범위 및 역할의 구성이 필요합니다. 리소스 응용 프로그램 웹 Api tooclient 응용 프로그램 tooexpose을 원하는 경우 hello API에 대 한 tooconfigure 액세스 범위 및 역할 필요 합니다. 클라이언트 응용 프로그램 tooaccess web API 사용 하도록 하려는 경우 tooconfigure hello 응용 프로그램 등록에 사용 권한을 tooaccess hello API 해야 합니다.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>리소스 응용 프로그램 tooexpose 웹 Api를 구성합니다.

Web API를 노출 하면 hello API hello에 표시할 **API 선택** tooan 앱 등록 권한을 추가할 때 나열 합니다. tooadd 액세스 범위에 설명 된 hello 단계에 따라 [tooyour 리소스 응용 프로그램의 범위가 액세스 권한 추가](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application)합니다.

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>클라이언트 응용 프로그램 tooaccess 웹 Api를 구성합니다.

사용 권한을 tooyour 응용 프로그램 등록을 추가 하는 경우 다음을 할 수 있습니다 **API 액세스 추가** tooexposed 웹 Api입니다. tooaccess 웹 Api에 설명 된 hello 단계를 수행 하십시오 [자격 증명이 나 권한을 tooaccess 웹 Api 추가](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis)합니다.

## <a name="next-steps"></a>다음 단계

-   [Azure Active Directory와 응용 프로그램 통합](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Hello Azure Active Directory 응용 프로그램 매니페스트 이해](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


