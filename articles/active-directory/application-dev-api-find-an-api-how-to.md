---
title: "사용자 지정 개발 응용 프로그램에 대해 필요한 특정 API를 찾는 방법 | Microsoft Docs"
description: "사용자 지정 개발 Azure AD 응용 프로그램에서 특정 API에 액세스하는 데 필요한 권한을 구성하는 방법"
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="c156c-103">사용자 지정 개발 응용 프로그램에 대해 필요한 특정 API를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="c156c-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="c156c-104">API에 액세스하려면 액세스 범위 및 역할을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c156c-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="c156c-105">클라이언트 응용 프로그램에 리소스 응용 프로그램 웹 API를 표시하려는 경우 API에 대한 액세스 범위 및 역할을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c156c-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="c156c-106">클라이언트 응용 프로그램에서 웹 API에 액세스하도록 하려면 앱 등록에서 API에 액세스하기 위한 권한을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c156c-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="c156c-107">웹 API를 공개하는 리소스 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c156c-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="c156c-108">웹 API를 표시할 때, 권한을 앱 등록에 추가하면 API가 **API 선택** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c156c-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="c156c-109">액세스 범위를 추가하려면 [리소스 응용 프로그램에 액세스 범위 추가](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application)에 설명된 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c156c-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="c156c-110">웹 API에 액세스하는 클라이언트 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c156c-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="c156c-111">앱 등록에 권한을 추가할 때 표시된 웹 API에 **API 액세스 권한을 추가**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c156c-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="c156c-112">웹 API에 액세스하려면 [웹 API에 액세스할 수 있는 자격 증명 또는 권한 추가](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis)에 설명된 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c156c-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c156c-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c156c-113">Next steps</span></span>

-   [<span data-ttu-id="c156c-114">Azure Active Directory와 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="c156c-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="c156c-115">Azure Active Directory 응용 프로그램 매니페스트 이해</span><span class="sxs-lookup"><span data-stu-id="c156c-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


