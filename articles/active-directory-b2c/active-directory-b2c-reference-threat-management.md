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
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="97698-103">Azure Active Directory B2C: 위협 관리</span><span class="sxs-lookup"><span data-stu-id="97698-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="97698-104">위협 관리에는 시스템 및 네트워크에 대한 공격으로부터 보호를 계획하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="97698-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="97698-105">서비스 거부 공격은 의도한 사용자가 리소스를 사용할 수 없게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97698-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="97698-106">암호 공격으로 인해 리소스에 대한 무단 액세스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97698-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="97698-107">Azure AD B2C(Azure Active Directory B2C)에는 여러 가지 방법으로 이러한 위협으로부터 데이터를 보호할 수 있는 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97698-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="97698-108">서비스 거부 공격</span><span class="sxs-lookup"><span data-stu-id="97698-108">Denial-of-service attacks</span></span>

<span data-ttu-id="97698-109">Azure AD B2C는 SYN 쿠키, 속도 및 연결 제한과 같은 검색 및 완화 기술을 사용하여 서비스 거부 공격으로부터 기본 리소스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="97698-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="97698-110">암호 공격</span><span class="sxs-lookup"><span data-stu-id="97698-110">Password attacks</span></span>

<span data-ttu-id="97698-111">또한 Azure AD B2C에는 암호 공격에 대한 완화 기술도 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97698-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="97698-112">완화에는 무차별 암호 대입 공격 및 사전 암호 공격이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="97698-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="97698-113">사용자가 설정한 암호는 적절한 복잡성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97698-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="97698-114">다양한 신호를 사용하여 Azure AD B2C는 요청의 무결성을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="97698-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="97698-115">Azure AD B2C는 의도한 사용자와 해커 및 봇네트 간을 지능적으로 구분하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97698-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="97698-116">Azure AD B2C는 공격 가능성이 있을 때 입력된 암호에 따라 계정을 잠그는 정교한 전략을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97698-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="97698-117">자세한 내용은 [Microsoft 보안 센터](https://www.microsoft.com/trustcenter/security/threatmanagement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97698-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
