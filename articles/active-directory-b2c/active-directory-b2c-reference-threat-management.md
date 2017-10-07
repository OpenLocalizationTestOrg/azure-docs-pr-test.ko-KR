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
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="a3ab4-103">Azure Active Directory B2C: 위협 관리</span><span class="sxs-lookup"><span data-stu-id="a3ab4-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="a3ab4-104">위협 관리에는 시스템 및 네트워크에 대한 공격으로부터 보호를 계획하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="a3ab4-105">서비스 거부 공격 toointended 사용할 수 없는 사용자가 리소스를 확보 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="a3ab4-106">암호 공격 리드 toounauthorized 액세스 tooresources 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="a3ab4-107">Azure AD B2C(Azure Active Directory B2C)에는 여러 가지 방법으로 이러한 위협으로부터 데이터를 보호할 수 있는 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="a3ab4-108">서비스 거부 공격</span><span class="sxs-lookup"><span data-stu-id="a3ab4-108">Denial-of-service attacks</span></span>

<span data-ttu-id="a3ab4-109">Azure AD B2C SYN 쿠키 및 속도 및 연결 제한 tooprotect 기본 서비스 거부 공격에 대 한 리소스와 같은 검색 및 완화 기법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="a3ab4-110">암호 공격</span><span class="sxs-lookup"><span data-stu-id="a3ab4-110">Password attacks</span></span>

<span data-ttu-id="a3ab4-111">또한 Azure AD B2C에는 암호 공격에 대한 완화 기술도 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="a3ab4-112">완화에는 무차별 암호 대입 공격 및 사전 암호 공격이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="a3ab4-113">사용자가 설정 된 암호는 필수 toobe 상당히 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="a3ab4-114">다양 한 신호를 사용 하 여 Azure AD B2C 요청의 hello 무결성을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="a3ab4-115">Azure AD B2C 기능은 toointelligently 해커 및 격리 한 봇 넷에서 의도 한 사용자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="a3ab4-116">Azure AD B2C 정교한 전략 toolock 계정을 기반으로 한 공격 가능성 hello에에서 입력 하는 hello 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="a3ab4-117">자세한 내용은 방문 hello [Microsoft 보안 센터](https://www.microsoft.com/trustcenter/security/threatmanagement)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ab4-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
