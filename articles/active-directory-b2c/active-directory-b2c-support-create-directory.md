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
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="a75b9-103">Azure Active Directory 또는 Azure Active Directory B2C 테넌트 생성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a75b9-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="a75b9-104">Azure AD 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="a75b9-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="a75b9-105">첫 번째 시도에서 Azure AD(Azure Active Directory) 테넌트를 만들 수 없는 경우 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="a75b9-106">문제가 지속되면 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="a75b9-107">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="a75b9-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="a75b9-108">[Azure AD B2C(Azure Active Directory B2C) 테넌트를 만드는](active-directory-b2c-get-started.md) 동안 문제가 발생할 경우 다음 옵션을 시도해보세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="a75b9-109">Azure AD B2C 테넌트가 테넌트 목록에 표시되지 않는 경우 다시 테넌트를 만들어 보세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="a75b9-110">Azure AD B2C 테넌트가 테넌트 목록에 표시되지만 다음과 같은 오류 메시지가 나타나는 경우 테넌트를 삭제하고 다시 만드세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="a75b9-111">"B2C 테넌트 'contosob2c' 생성을 완료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a75b9-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="a75b9-112">자세한 지침을 보려면 이 [링크](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)를 방문하세요."</span><span class="sxs-lookup"><span data-stu-id="a75b9-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="a75b9-113">기존 Azure AD B2C 테넌트를 삭제하고 동일한 도메인 이름으로 다시 만들 때 발생하는 알려진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75b9-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="a75b9-114">새 Azure AD B2C 테넌트를 만들 때는 다른 도메인 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75b9-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="a75b9-115">이러한 해결 방법이 효과가 없으면 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="a75b9-116">자세한 내용은 [Azure AD B2C에 대한 파일 지원 요청](active-directory-b2c-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a75b9-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

