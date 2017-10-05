---
title: "Azure Active Directory의 관리 단위 관리 미리 보기"
description: "Azure Active Directory에서 보다 세부적인 권한 위임을 위해 관리 단위 사용"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: e12a0aea8264b1ea67c26294ec5bbe9c404a171e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="9dde6-103">Azure AD의 관리 단위 관리 - 공용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="9dde6-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="9dde6-104">이 문서에서는 사용자의 하위 집합에 대해 관리 권한을 위임하고 사용자의 하위 집합에 정책을 적용하는 데 사용할 수 있는 리소스의 새로운 Azure Active Directory 컨테이너인 관리 단위에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span></span> <span data-ttu-id="9dde6-105">Azure Active Directory에서 관리 단위를 통해 중앙 관리자는 지역 관리자에게 권한을 위임하거나 세부적인 수준에서 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span></span>

<span data-ttu-id="9dde6-106">이는 각각 독립된 많은 자치 학교(경영대학, 공과대학 등)로 구성된 종합 대학교와 같이 독립된 부서가 있는 조직에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="9dde6-107">그러한 부서는 자체 IT 관리자를 통해 액세스를 제어하고, 사용자를 관리하고, 특히 부서에 대한 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="9dde6-108">중앙 관리자는 특정 부서의 사용자에게 부서 관리자 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span></span> <span data-ttu-id="9dde6-109">이 예를 통해 보다 구체적으로 설명하자면, 중앙 관리자는 특정 학교(경영대학)에 대해 관리 단위를 만들고 경영대학 사용자만 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span></span> <span data-ttu-id="9dde6-110">그런 다음 중앙 관리자는 경영대학 IT 직원을 범위 역할에 추가할 수 있습니다. 즉, IT 직원의 경영대학 관리 권한을 경영대학 관리 단위에만 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dde6-111">Azure Active Directory Premium을 사용하도록 설정한 경우에만 관리 단위 범위가 지정된 관리자 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="9dde6-112">자세한 내용은 [Azure AD Premium 시작을 참조하세요](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="9dde6-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="9dde6-113">중앙 관리자의 관점에서 관리 단위는 리소스로 생성하고 채울 수 있는 디렉터리 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="9dde6-114">**이 미리 보기 릴리스에서는 사용자만 이 리소스가 될 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="9dde6-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="9dde6-115">관리 단위가 생성되고 채워지면, 관리 단위에 포함된 리소스에게만 권한을 부여하도록 제한하는 범위로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="9dde6-116">관리 단위 관리</span><span class="sxs-lookup"><span data-stu-id="9dde6-116">Managing administrative units</span></span>
<span data-ttu-id="9dde6-117">이 미리 보기 릴리스에서 Windows PowerShell cmdlet용 Azure Active Directory 모듈을 사용하는 관리 단위를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dde6-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="9dde6-118">이 방법에 대한 자세한 내용은 [관리 단위 작업](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dde6-118">To learn more about how to do that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="9dde6-119">소프트웨어 요구 사항 및 Azure AD 모듈 설치에 대한 자세한 내용과 구문, 매개 변수 설명 및 예제 등 관리 단위를 관리하기 위한 Azure AD 모듈 cmdlet에 대한 내용은 [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dde6-119">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dde6-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dde6-120">Next steps</span></span>
[<span data-ttu-id="9dde6-121">Azure Active Directory 버전</span><span class="sxs-lookup"><span data-stu-id="9dde6-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
