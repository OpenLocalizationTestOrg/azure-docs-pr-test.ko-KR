---
title: "Visual Studio WebApi 프로젝트에서 Azure AD 시작 | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 Azure AD를 만들거나 연결한 후에 WebApi 프로젝트에 Azure Active Directory를 사용하여 시작하는 방법입니다."
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="02334-103">Azure Active Directory 및 Visual Studio 연결 서비스 시작(WebApi 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="02334-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02334-104">시작</span><span class="sxs-lookup"><span data-stu-id="02334-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="02334-105">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="02334-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="02334-106">컨트롤러에 액세스하려면 인증 필요</span><span class="sxs-lookup"><span data-stu-id="02334-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="02334-107">프로젝트의 모든 컨트롤러는 **Authorize** 특성으로 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02334-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="02334-108">이 특성으로 인해 사용자가 인증해야만 이러한 컨트롤러에서 정의한 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02334-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="02334-109">컨트롤러에 익명으로 액세스할 수 있도록 하려면 컨트롤러에서 이 특성을 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="02334-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="02334-110">더 세부적인 수준에서 권한을 설정하려면 특성을 컨트롤러 클래스에 적용하는 대신 인증이 필요한 각 메서드에 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="02334-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02334-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02334-111">Next steps</span></span>
[<span data-ttu-id="02334-112">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="02334-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

