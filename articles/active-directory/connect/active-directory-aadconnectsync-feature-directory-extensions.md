---
title: "Azure AD Connect 동기화: 디렉터리 확장 | Microsoft Docs"
description: "이 항목에서 Azure AD Connect hello 디렉터리 확장 기능에 설명 합니다."
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
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="40c71-103">Azure AD Connect 동기화: 디렉터리 확장</span><span class="sxs-lookup"><span data-stu-id="40c71-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="40c71-104">디렉터리 확장 온-프레미스 Active Directory에서 사용자 지정 특성으로 Azure AD에 tooextend hello 스키마가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="40c71-105">이 기능은 특성 toomanage 온-프레미스를 계속 사용 toobuild LOB 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="40c71-106">이러한 특성은 [Azure AD Graph 디렉터리 확장](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) 또는 [Microsoft Graph](https://graph.microsoft.io/)를 통해 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="40c71-107">Hello 특성을 사용 하 여 볼 수 있습니다 [Azure AD 그래프 탐색기](https://graphexplorer.cloudapp.net) 및 [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) 각각.</span><span class="sxs-lookup"><span data-stu-id="40c71-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="40c71-108">현재 이 특성을 이용하는 Office 365 워크로드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="40c71-109">다른 특성을 구성할 toosynchronize hello 설치 마법사의 사용자 지정 설정 경로 hello에 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="40c71-110">![스키마 확장 마법사](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="40c71-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="40c71-111">hello 설치 hello 다음 유효한 후보는 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="40c71-112">사용자 및 그룹 개체 유형</span><span class="sxs-lookup"><span data-stu-id="40c71-112">User and Group object types</span></span>
* <span data-ttu-id="40c71-113">단일 값 특성: 문자열, 부울, 정수, 이진</span><span class="sxs-lookup"><span data-stu-id="40c71-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="40c71-114">다중 값 특성: 문자열, 이진</span><span class="sxs-lookup"><span data-stu-id="40c71-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="40c71-115">특성 목록이 hello Azure AD Connect 설치 중에 만들어진 hello 스키마 캐시에서 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="40c71-116">추가 특성을 가진 hello Active Directory 스키마를 확장 한 경우 다음 hello [스키마를 새로 고칠](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) 전에 새 이러한 특성은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="40c71-117">Azure AD에서 개체를 too100 디렉터리 확장 특성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="40c71-118">hello 최대 길이 250 자입니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-118">hello max length is 250 characters.</span></span> <span data-ttu-id="40c71-119">특성 값이 긴 경우 hello 동기화 엔진에 의해 잘립니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="40c71-120">Azure AD Connect를 설치하는 동안 이러한 특성을 사용할 수 있는 응용 프로그램이 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="40c71-121">Hello Azure 포털에서에서이 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-121">You can see this application in hello Azure portal.</span></span>  
![스키마 확장 앱](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="40c71-123">이제 이 특성은 Graph를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-123">These attributes are now available through Graph:</span></span>  
![그래프](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="40c71-125">hello 특성 확장명 접두사가 추가 되며\_{AppClientId}\_합니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="40c71-126">hello AppClientId hello 같은 Azure AD 테 넌 트의 모든 특성에 대 한 값에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c71-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40c71-127">Next steps</span></span>
<span data-ttu-id="40c71-128">Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="40c71-129">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40c71-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
