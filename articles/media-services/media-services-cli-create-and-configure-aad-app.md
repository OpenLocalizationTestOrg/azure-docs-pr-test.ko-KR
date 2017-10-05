---
title: "CLI 2.0을 사용하여 Azure AD 앱 만들기 및 Azure Media Services API 액세스 구성 | Microsoft Docs"
description: "이 항목에서는 CLI 2.0을 사용하여 Azure AD 앱을 만들고 Azure Media Services API에 액세스하도록 구성하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 01a2bb6d99776feec936315bc882c3097ce832d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-cli-20-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="f2c33-103">CLI 2.0을 사용하여 AAD 앱 만들기 및 Azure Media Services API 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="f2c33-103">Use CLI 2.0 to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="f2c33-104">이 항목에서는 CLI 2.0을 사용하여 Azure Media Services 리소스에 액세스하기 위한 Azure AD(Azure Active Directory) 응용 프로그램 및 서비스 주체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-104">This topic shows you how to use CLI 2.0 to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f2c33-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2c33-105">Prerequisites</span></span>

- <span data-ttu-id="f2c33-106">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f2c33-106">An Azure account.</span></span> <span data-ttu-id="f2c33-107">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c33-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="f2c33-108">미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="f2c33-108">A Media Services account.</span></span> <span data-ttu-id="f2c33-109">자세한 내용은 [Azure Portal을 사용하여 Azure Media Services 계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c33-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="f2c33-110">Azure Cloud Shell 사용</span><span class="sxs-lookup"><span data-stu-id="f2c33-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="f2c33-111">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f2c33-112">포털의 위쪽 탐색 창에서 Cloud Shell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="f2c33-114">자세한 내용은 [Azure Cloud Shell 개요](../cloud-shell/overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c33-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-cli-20"></a><span data-ttu-id="f2c33-115">CLI 2.0으로 Azure AD 앱 만들기 및 미디어 계정에 대한 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="f2c33-115">Create an Azure AD app and configure access to the media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="f2c33-116">예:</span><span class="sxs-lookup"><span data-stu-id="f2c33-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="f2c33-117">이 예제에서 **scope**는 미디어 서비스 계정에 대한 전체 리소스 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="f2c33-118">하지만 **scope**는 모든 수준에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="f2c33-119">예를 들어 다음 수준 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c33-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="f2c33-120">**구독** 수준.</span><span class="sxs-lookup"><span data-stu-id="f2c33-120">The **subscription** level.</span></span>
* <span data-ttu-id="f2c33-121">**리소스 그룹** 수준.</span><span class="sxs-lookup"><span data-stu-id="f2c33-121">The **resource group** level.</span></span>
* <span data-ttu-id="f2c33-122">**리소스** 수준(예: 미디어 계정).</span><span class="sxs-lookup"><span data-stu-id="f2c33-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="f2c33-123">자세한 내용은 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c33-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="f2c33-124">또한 [Azure 명령줄 인터페이스를 사용하여 역할 기반 액세스 제어 관리](../active-directory/role-based-access-control-manage-access-azure-cli.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c33-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f2c33-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2c33-125">Next steps</span></span>

<span data-ttu-id="f2c33-126">[계정에 파일 업로드](media-services-portal-upload-files.md) 시작</span><span class="sxs-lookup"><span data-stu-id="f2c33-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
