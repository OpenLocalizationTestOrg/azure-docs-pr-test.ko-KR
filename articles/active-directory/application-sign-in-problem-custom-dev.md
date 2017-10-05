---
title: "사용자 지정 개발 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "Azure AD를 사용하여 개발한 응용 프로그램에 로그인하지 못하게 되는 결과를 발생시킬 수 있는 일반적인 오류"
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="46c3a-103">사용자 지정 개발 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="46c3a-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="46c3a-104">앱에 로그인하지 못하게 될 수 있는 여러 가지 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c3a-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="46c3a-105">이 문제가 발생하는 가장 큰 이유는 앱이 잘못 구성되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3a-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="46c3a-106">잘못 구성된 앱과 관련된 오류</span><span class="sxs-lookup"><span data-stu-id="46c3a-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="46c3a-107">포털의 구성이 앱의 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3a-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="46c3a-108">특히, 클라이언트/응용 프로그램 ID, 회신 URL, 클라이언트 비밀/키 및 앱 ID URI를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3a-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="46c3a-109">구성한 리소스만을 요청하기 위해 **필요한 리소스** 탭에서 구성된 권한이 있는 코드에서 액세스를 요청하는 리소스를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3a-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="46c3a-110">유사한 오류 또는 문제는 [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46c3a-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46c3a-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46c3a-111">Next steps</span></span>

[<span data-ttu-id="46c3a-112">Azure AD 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="46c3a-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="46c3a-113">동의 및 Azure AD와 앱 통합</span><span class="sxs-lookup"><span data-stu-id="46c3a-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="46c3a-114">Azure AD v2.0 수렴형 앱에 대한 동의 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="46c3a-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="46c3a-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="46c3a-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
