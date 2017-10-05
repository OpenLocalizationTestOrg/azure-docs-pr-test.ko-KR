---
title: "PingAccess를 사용하도록 응용 프로그램 프록시 응용 프로그램을 구성하는 방법 | Microsoft 문서"
description: "PingAccess를 사용하여 응용 프로그램 프록시의 이점을 헤더 기반 인증을 사용하는 응용 프로그램으로 확장하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="a4f64-103">PingAccess를 사용하도록 응용 프로그램 프록시 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="a4f64-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="a4f64-104">이제 PingAccess를 사용하여 응용 프로그램 프록시의 이점을 헤더 기반 인증을 사용하는 응용 프로그램으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f64-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="a4f64-105">헤더를 사용하지 않는 응용 프로그램의 경우 [Single Sign-on 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)에서 다른 옵션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4f64-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="a4f64-106">단계 개요 및 권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="a4f64-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="a4f64-107">PingAccess를 사용하도록 응용 프로그램을 구성하는 작업은 네 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4f64-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="a4f64-108">응용 프로그램 프록시 커넥터 구성</span><span class="sxs-lookup"><span data-stu-id="a4f64-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="a4f64-109">Azure AD 응용 프로그램 프록시 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a4f64-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="a4f64-110">PingAccess 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="a4f64-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="a4f64-111">PingAccess에서 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a4f64-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="a4f64-112">이러한 각 단계에 대한 자세한 내용은 [Single Sign-On과 헤더 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4f64-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
