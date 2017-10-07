---
title: "응용 프로그램 프록시 응용 프로그램 toouse PingAccess aaaHow tooconfigure | Microsoft Docs"
description: "어떻게 toouse PingAccess tooextend hello 헤더 기반 인증을 사용 하 여 응용 프로그램 프록시 tooapplications의 이점에 알아봅니다"
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
ms.openlocfilehash: fa4c9747b7bf5a135425be270e4f7eadf95248fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-pingaccess"></a><span data-ttu-id="c4ee6-103">어떻게 응용 프로그램 프록시 응용 프로그램 toouse PingAccess tooconfigure</span><span class="sxs-lookup"><span data-stu-id="c4ee6-103">How tooconfigure an Application Proxy application toouse PingAccess</span></span>

<span data-ttu-id="c4ee6-104">이제 공동 PingAccess로 우리의 tooextend hello 활용을 헤더 기반 인증을 사용 하 여 응용 프로그램 프록시 tooapplications 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ee6-104">Our collaboration with PingAccess now allows you tooextend hello benefits of Application Proxy tooapplications using header-based authentication.</span></span> <span data-ttu-id="c4ee6-105">헤더를 사용하지 않는 응용 프로그램의 경우 [Single Sign-on 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)에서 다른 옵션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ee6-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="c4ee6-106">단계 개요 및 권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="c4ee6-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="c4ee6-107">tooconfigure PingAccess와 응용 프로그램의 4 단계:</span><span class="sxs-lookup"><span data-stu-id="c4ee6-107">tooconfigure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="c4ee6-108">응용 프로그램 프록시 커넥터 구성</span><span class="sxs-lookup"><span data-stu-id="c4ee6-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="c4ee6-109">Azure AD 응용 프로그램 프록시 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c4ee6-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="c4ee6-110">PingAccess 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="c4ee6-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="c4ee6-111">PingAccess에서 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c4ee6-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="c4ee6-112">이러한 각 단계에 대한 자세한 내용은 [Single Sign-On과 헤더 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ee6-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
