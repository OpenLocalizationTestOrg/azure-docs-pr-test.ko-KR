---
title: "aaaProblems tooan 개발 된 응용 프로그램에 서명 | Microsoft Docs"
description: "일반적인 인해 발생할 수 있습니다 있습니다 toonot Azure AD로 개발한 응용 프로그램에 수 toosign 수"
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
ms.openlocfilehash: cc302e68ae6c129b74387c6fc5ba4fb45ccb8fb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-custom-developed-application"></a><span data-ttu-id="64377-103">Tooan 개발 된 응용 프로그램에 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="64377-103">Problems signing in tooan custom-developed application</span></span>

<span data-ttu-id="64377-104">여러 오류를 일으킬 수 있는 있습니다 toonot는 응용 프로그램에 수 toosign 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64377-104">There are several errors that could be causing you toonot be able toosign into an app.</span></span> <span data-ttu-id="64377-105">사용자는이 문제가 발생 하는 hello 가장 큰 이유는 잘못 구성 된 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="64377-105">hello biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-too-misconfigured-apps"></a><span data-ttu-id="64377-106">오류 관련 너무 잘못 구성 된 앱</span><span class="sxs-lookup"><span data-stu-id="64377-106">Errors related too misconfigured apps</span></span>

* <span data-ttu-id="64377-107">두 hello 구성 hello 포털에서 앱에 있는 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64377-107">Verify both hello configurations in hello portal match what you have in your app.</span></span> <span data-ttu-id="64377-108">특히, 클라이언트/응용 프로그램 ID, 회신 URL, 클라이언트 비밀/키 및 앱 ID URI를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="64377-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="64377-109">Hello에 hello 구성 된 권한으로 액세스 tooin 코드를 요청 하는 hello 리소스 비교 **필요한 리소스** 만 리소스를 요청 되었는지 탭 toomake 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64377-109">Compare hello resource you’re requesting access tooin code with hello configured permissions in hello **Required Resources** tab toomake sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="64377-110">유사한 오류 또는 문제는 [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64377-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64377-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64377-111">Next steps</span></span>

[<span data-ttu-id="64377-112">Azure AD 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="64377-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="64377-113">승인 및 앱 통합 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="64377-113">Consent and Integrating Apps tooAzure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="64377-114">Azure AD v2.0 수렴형 앱에 대한 동의 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="64377-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="64377-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="64377-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
