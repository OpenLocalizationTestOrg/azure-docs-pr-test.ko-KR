---
title: "Azure AD Connect 동기화: 디렉터리 확장 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect의 디렉터리 확장 기능을 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="51a6c-103">Azure AD Connect 동기화: 디렉터리 확장</span><span class="sxs-lookup"><span data-stu-id="51a6c-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="51a6c-104">디렉터리 확장을 사용하면 온-프레미스 Active Directory의 사용자 고유 특성을 사용하여 Azure AD에서 스키마를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="51a6c-105">이 기능을 통해 온-프레미스를 계속 관리하는 특성을 이용하는 LOB 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="51a6c-106">이러한 특성은 [Azure AD Graph 디렉터리 확장](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) 또는 [Microsoft Graph](https://graph.microsoft.io/)를 통해 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="51a6c-107">각각 [Azure AD Graph 탐색기](https://graphexplorer.cloudapp.net) 및 [Microsoft Graph 탐색기](https://graphexplorer2.azurewebsites.net/)를 통해 사용할 수 있는 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="51a6c-108">현재 이 특성을 이용하는 Office 365 워크로드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="51a6c-109">설치 마법사의 사용자 지정 설정 경로에서 동기화할 추가 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="51a6c-110">![스키마 확장 마법사](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="51a6c-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="51a6c-111">설치 시 다음과 같은 특성이 표시됩니다. 이러한 특성은 유효한 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="51a6c-112">사용자 및 그룹 개체 유형</span><span class="sxs-lookup"><span data-stu-id="51a6c-112">User and Group object types</span></span>
* <span data-ttu-id="51a6c-113">단일 값 특성: 문자열, 부울, 정수, 이진</span><span class="sxs-lookup"><span data-stu-id="51a6c-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="51a6c-114">다중 값 특성: 문자열, 이진</span><span class="sxs-lookup"><span data-stu-id="51a6c-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="51a6c-115">특성 목록은 Azure AD Connect 설치 도중에 만들어진 스키마 캐시에서 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="51a6c-116">추가 특성을 사용하여 Active Directory 스키마를 확장한 경우 [스키마를 새로 고쳐야](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) 이러한 새 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="51a6c-117">Azure AD의 개체에는 최대 100개의 디렉터리 확장 특성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="51a6c-118">최대 길이는 250자입니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-118">The max length is 250 characters.</span></span> <span data-ttu-id="51a6c-119">특성 값이 더 긴 경우 동기화 엔진에 의해 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="51a6c-120">Azure AD Connect를 설치하는 동안 이러한 특성을 사용할 수 있는 응용 프로그램이 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="51a6c-121">Azure 포털에서 다음 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-121">You can see this application in the Azure portal.</span></span>  
![스키마 확장 앱](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="51a6c-123">이제 이 특성은 Graph를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-123">These attributes are now available through Graph:</span></span>  
![그래프](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="51a6c-125">특성은 extension\_{AppClientId}\_를 접두사로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="51a6c-126">AppClientId는 Azure AD 테넌트의 모든 특성에 대해 동일한 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51a6c-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51a6c-127">Next steps</span></span>
<span data-ttu-id="51a6c-128">[Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="51a6c-129">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="51a6c-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
