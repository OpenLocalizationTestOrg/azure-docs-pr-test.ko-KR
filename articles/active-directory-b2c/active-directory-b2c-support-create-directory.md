---
title: "Azure Active Directory B2C: 테넌트 생성 문제 해결 | Microsoft Docs"
description: "Azure Active Directory 또는 Azure Active Directory B2C 테넌트 생성과 관련된 문제 및 해결 방법입니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Azure Active Directory 또는 Azure Active Directory B2C 테넌트 생성 문제 해결 

## <a name="create-an-azure-ad-tenant"></a>Azure AD 테넌트 만들기
Hello 첫 번째 시도에서 Azure Active Directory (Azure AD) 테 넌 트를 만들 수 없는 경우 다시 시도 하십시오. Hello 문제가 계속 되 면 Azure 지원에 문의 합니다.

## <a name="create-an-azure-ad-b2c-tenant"></a>Azure AD B2C 테넌트 만들기
문제가 발생 한 경우 때 있습니다 [Azure Active Directory B2C 만들기 (Azure AD B2C) 테 넌 트](active-directory-b2c-get-started.md), 시도 hello 다음 옵션:

* Hello Azure AD B2C 테 넌 트의 테 넌 트가 목록에 표시 되지 않습니다 경우 toocreate hello 테 넌 트 다시 시도 합니다.
* Hello Azure AD B2C 테 넌 트가 테 넌 트의 목록에 표시 하는 경우 다음과 같은 오류 메시지가 hello를 참조 hello 테 넌 트를 삭제 하 고 다시 만드십시오.

    "Hello B2C 테 넌 트 'contosob2c' hello 만들기를 완료 하지 못했습니다. 자세한 지침을 보려면 이 [링크](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)를 방문하세요."
* 알려진 문제는 기존 Azure AD B2C를 삭제 하는 경우 테 넌 트 및 hello를 사용 하 여 다시 만들 동일한 도메인 이름입니다. 새 Azure AD B2C 테넌트를 만들 때는 다른 도메인 이름을 사용해야 합니다.
* 이러한 해결 방법이 효과가 없으면 Azure 지원에 문의하세요. 자세한 내용은 [Azure AD B2C에 대한 파일 지원 요청](active-directory-b2c-support.md)을 참조하세요.

