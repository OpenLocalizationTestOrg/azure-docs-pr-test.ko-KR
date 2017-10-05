---
title: "Azure AD v2.0 Windows 유니버설 앱 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정 둘 다로 사용자를 로그인하는 Windows 유니버설 앱을 빌드하는 방법입니다."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: d2c92b65-3c1d-46d1-81c8-88f32f6b2c4b
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.date: 02/20/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 369802f1a42b8720aa730d5ac7e5576ed20eeddf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-universal-app-using-the-v20-endpoint"></a><span data-ttu-id="d710f-103">v2.0 끝점을 사용하여 Windows 유니버설 앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="d710f-103">Add sign-in to a Windows Universal app using the v2.0 endpoint</span></span>
  <span data-ttu-id="d710f-104">Windows 유니버설 앱에 대한 빠른 시작 자습서는 완전히 준비되지 않았습니다. 나중에 다시 Twitter에서 @AzureAD를 다시 방문하여 업데이트를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d710f-104">The quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="d710f-105">일부 Azure Active Directory 시나리오 및 기능만 v2.0 끝점에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d710f-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d710f-106">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d710f-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="d710f-107">[이 페이지](https://technet.microsoft.com/security/dd252948) 를 방문해서 보안 공지 경고를 구독하여 보안 사건이 발생할 때 알림을 받는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d710f-107">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

