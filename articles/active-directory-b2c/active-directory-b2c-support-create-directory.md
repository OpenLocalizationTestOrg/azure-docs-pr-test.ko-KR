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
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="034d7-103">Azure Active Directory 또는 Azure Active Directory B2C 테넌트 생성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="034d7-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="034d7-104">Azure AD 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="034d7-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="034d7-105">Hello 첫 번째 시도에서 Azure Active Directory (Azure AD) 테 넌 트를 만들 수 없는 경우 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="034d7-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="034d7-106">Hello 문제가 계속 되 면 Azure 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="034d7-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="034d7-107">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="034d7-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="034d7-108">문제가 발생 한 경우 때 있습니다 [Azure Active Directory B2C 만들기 (Azure AD B2C) 테 넌 트](active-directory-b2c-get-started.md), 시도 hello 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="034d7-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="034d7-109">Hello Azure AD B2C 테 넌 트의 테 넌 트가 목록에 표시 되지 않습니다 경우 toocreate hello 테 넌 트 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="034d7-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="034d7-110">Hello Azure AD B2C 테 넌 트가 테 넌 트의 목록에 표시 하는 경우 다음과 같은 오류 메시지가 hello를 참조 hello 테 넌 트를 삭제 하 고 다시 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="034d7-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="034d7-111">"Hello B2C 테 넌 트 'contosob2c' hello 만들기를 완료 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="034d7-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="034d7-112">자세한 지침을 보려면 이 [링크](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)를 방문하세요."</span><span class="sxs-lookup"><span data-stu-id="034d7-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="034d7-113">알려진 문제는 기존 Azure AD B2C를 삭제 하는 경우 테 넌 트 및 hello를 사용 하 여 다시 만들 동일한 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="034d7-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="034d7-114">새 Azure AD B2C 테넌트를 만들 때는 다른 도메인 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034d7-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="034d7-115">이러한 해결 방법이 효과가 없으면 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="034d7-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="034d7-116">자세한 내용은 [Azure AD B2C에 대한 파일 지원 요청](active-directory-b2c-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="034d7-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

