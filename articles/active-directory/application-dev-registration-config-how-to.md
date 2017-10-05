---
title: "지정된 API에 대한 사용 권한을 선택하는 방법 | Microsoft Docs"
description: "개발 중이거나 Azure AD에 등록 중인 사용자 지정 응용 프로그램의 인증 끝점을 찾는 방법입니다."
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="b8c88-103">지정된 API에 대한 사용 권한을 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="b8c88-103">How to select permissions for a given API</span></span>

<span data-ttu-id="b8c88-104">[Azure Portal](https://portal.azure.com)에서 응용 프로그램의 인증 끝점을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="b8c88-105">[Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="b8c88-106">왼쪽 탐색 창에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="b8c88-107">**앱 등록**을 클릭하고 **끝점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="b8c88-108">그러면 테넌트의 모든 인증 끝점이 나열되는 **끝점** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="b8c88-109">응용 프로그램 ID와 함께 사용하는 인증 프로토콜에 해당하는 끝점을 사용하여 응용 프로그램에 해당하는 인증 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8c88-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8c88-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8c88-110">Next steps</span></span>
[<span data-ttu-id="b8c88-111">Azure Active Directory 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="b8c88-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
