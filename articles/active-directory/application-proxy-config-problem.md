---
title: "응용 프로그램 프록시 응용 프로그램을 만들 때 문제 발생 | Microsoft 문서"
description: "Azure AD 관리 포털에서 응용 프로그램 프록시 응용 프로그램을 만들 때 발생하는 문제를 해결하는 방법"
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="9c1b6-103">응용 프로그램 프록시 응용 프로그램을 만들 때 문제 발생</span><span class="sxs-lookup"><span data-stu-id="9c1b6-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="9c1b6-104">다음은 새로운 응용 프로그램 프록시 응용 프로그램을 만들 때 발생하는 몇 가지 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="9c1b6-105">권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="9c1b6-105">Recommended documents</span></span> 

<span data-ttu-id="9c1b6-106">관리 포털을 통해 응용 프로그램 프록시 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="9c1b6-107">해당 문서의 단계에 따라 응용 프로그램을 만드는 중 오류가 발생하면 오류 세부 정보에서 응용 프로그램 문제 해결 방법에 대한 정보 및 제안 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="9c1b6-108">대부분의 오류 메시지에는 제안 수정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="9c1b6-109">확인할 항목</span><span class="sxs-lookup"><span data-stu-id="9c1b6-109">Specific things to check</span></span>

<span data-ttu-id="9c1b6-110">일반적인 오류를 방지하려면 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="9c1b6-111">응용 프로그램 프록시 응용 프로그램을 만들 수 있는 권한을 가진 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="9c1b6-112">내부 URL이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-112">The internal URL is unique</span></span>

-   <span data-ttu-id="9c1b6-113">외부 URL이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-113">The external URL is unique</span></span>

-   <span data-ttu-id="9c1b6-114">URL이 http 또는 https로 시작하고 "/"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="9c1b6-115">URL은 IP 주소가 아닌 도메인 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="9c1b6-116">응용 프로그램을 만들 때 오류 메시지가 오른쪽 상단 모서리에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="9c1b6-117">알림 아이콘을 선택하여 오류 메시지를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c1b6-117">You can also select the notification icon to see the error messages.</span></span>

   ![알림 프롬프트](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="9c1b6-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c1b6-119">Next steps</span></span>
[<span data-ttu-id="9c1b6-120">Azure Portal에서 응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="9c1b6-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
