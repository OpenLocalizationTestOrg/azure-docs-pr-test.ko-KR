---
title: "Azure CLI 스크립트 샘플 - 함수 앱에 사용자 지정 SSL 인증서 바인딩 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure의 함수 앱에 사용자 지정 SSL 인증서 바인딩"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="a9a86-103">함수 앱에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="a9a86-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="a9a86-104">이 샘플 스크립트는 해당 관련된 리소스를 사용하여 App Service에서 함수 앱을 만든 다음 사용자 지정 도메인 이름의 SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="a9a86-105">이 샘플에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-105">For this sample, you need:</span></span>

* <span data-ttu-id="a9a86-106">도메인 등록 기관의 DNS 구성 페이지 액세스</span><span class="sxs-lookup"><span data-stu-id="a9a86-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="a9a86-107">업로드하고 바인딩하려는 SSL 인증서에 사용할 유효한 .PFX 파일 및 암호</span><span class="sxs-lookup"><span data-stu-id="a9a86-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="a9a86-108">SSL 인증서를 바인딩하려면 함수 앱이 소비 계획이 아니라 App Service 계획에서 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9a86-109">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9a86-110">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="a9a86-111">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9a86-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a9a86-112">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a9a86-112">Sample script</span></span>

<span data-ttu-id="a9a86-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "웹앱에 사용자 지정 SSL 인증서 바인딩")]</span><span class="sxs-lookup"><span data-stu-id="a9a86-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a9a86-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a9a86-114">Script explanation</span></span>

<span data-ttu-id="a9a86-115">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-115">This script uses the following commands.</span></span> <span data-ttu-id="a9a86-116">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a9a86-117">명령</span><span class="sxs-lookup"><span data-stu-id="a9a86-117">Command</span></span> | <span data-ttu-id="a9a86-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a9a86-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9a86-119">az group create</span><span class="sxs-lookup"><span data-stu-id="a9a86-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a9a86-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9a86-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a9a86-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a9a86-122">SSL 인증서를 바인딩하는 데 필요한 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="a9a86-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="a9a86-123">az functionapp create</span></span>]() | <span data-ttu-id="a9a86-124">함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-124">Creates a function app.</span></span> |
| [<span data-ttu-id="a9a86-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="a9a86-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="a9a86-126">함수 앱에 사용자 지정 도메인을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="a9a86-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="a9a86-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="a9a86-128">함수 앱에 SSL 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="a9a86-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="a9a86-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="a9a86-130">함수 앱에 업로드한 SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9a86-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9a86-131">Next steps</span></span>

<span data-ttu-id="a9a86-132">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9a86-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9a86-133">추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서]()에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a86-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
