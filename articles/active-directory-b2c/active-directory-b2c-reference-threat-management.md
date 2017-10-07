---
title: "Azure Active Directory B2C: 위협 관리 | Microsoft Docs"
description: "Azure Active Directory B2C에서 서비스 거부 공격 및 암호 공격에 대한 검색 및 완화 기법을 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C: 위협 관리

위협 관리에는 시스템 및 네트워크에 대한 공격으로부터 보호를 계획하는 작업이 포함됩니다. 서비스 거부 공격 toointended 사용할 수 없는 사용자가 리소스를 확보 될 수 있습니다. 암호 공격 리드 toounauthorized 액세스 tooresources 합니다. Azure AD B2C(Azure Active Directory B2C)에는 여러 가지 방법으로 이러한 위협으로부터 데이터를 보호할 수 있는 기본 제공 기능이 있습니다.

## <a name="denial-of-service-attacks"></a>서비스 거부 공격

Azure AD B2C SYN 쿠키 및 속도 및 연결 제한 tooprotect 기본 서비스 거부 공격에 대 한 리소스와 같은 검색 및 완화 기법을 사용 합니다.

## <a name="password-attacks"></a>암호 공격

또한 Azure AD B2C에는 암호 공격에 대한 완화 기술도 제공되어 있습니다. 완화에는 무차별 암호 대입 공격 및 사전 암호 공격이 포함됩니다. 사용자가 설정 된 암호는 필수 toobe 상당히 복잡 합니다. 다양 한 신호를 사용 하 여 Azure AD B2C 요청의 hello 무결성을 분석 합니다. Azure AD B2C 기능은 toointelligently 해커 및 격리 한 봇 넷에서 의도 한 사용자를 구분 합니다. Azure AD B2C 정교한 전략 toolock 계정을 기반으로 한 공격 가능성 hello에에서 입력 하는 hello 암호를 제공 합니다.

자세한 내용은 방문 hello [Microsoft 보안 센터](https://www.microsoft.com/trustcenter/security/threatmanagement)합니다.
