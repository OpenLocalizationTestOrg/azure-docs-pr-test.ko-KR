---
title: "aaaAzure CLI 스크립트 샘플-바인딩 사용자 지정 SSL 인증서 tooa 함수 앱 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Azure에는 사용자 지정 SSL 인증서 tooa 함수 앱 바인딩"
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
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="f03ee-103">사용자 지정 SSL 인증서 tooa 함수 앱 바인딩</span><span class="sxs-lookup"><span data-stu-id="f03ee-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="f03ee-104">이 샘플 스크립트과 해당 관련된 리소스 응용 프로그램 서비스에서 함수 응용 프로그램을 만듭니다 다음 사용자 지정 도메인 이름 tooit의 hello SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="f03ee-105">이 샘플에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-105">For this sample, you need:</span></span>

* <span data-ttu-id="f03ee-106">Tooyour 도메인 등록자의 DNS 구성 페이지에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="f03ee-107">유효 합니다. PFX 파일 및 SSL hello에 대 한 암호 인증서 tooupload 원하고 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="f03ee-108">SSL 인증서 toobind 소비 계획 아니라 앱 서비스 계획에 함수 앱을 만들 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f03ee-109">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f03ee-110">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f03ee-111">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f03ee-112">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f03ee-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f03ee-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f03ee-113">Script explanation</span></span>

<span data-ttu-id="f03ee-114">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-114">This script uses hello following commands.</span></span> <span data-ttu-id="f03ee-115">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f03ee-116">명령</span><span class="sxs-lookup"><span data-stu-id="f03ee-116">Command</span></span> | <span data-ttu-id="f03ee-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f03ee-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f03ee-118">az group create</span><span class="sxs-lookup"><span data-stu-id="f03ee-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f03ee-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f03ee-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f03ee-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f03ee-121">앱 서비스 계획이 필요 toobind SSL 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="f03ee-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f03ee-122">az functionapp create</span></span>]() | <span data-ttu-id="f03ee-123">함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-123">Creates a function app.</span></span> |
| [<span data-ttu-id="f03ee-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="f03ee-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="f03ee-125">사용자 지정 도메인 toohello 함수 응용 프로그램을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="f03ee-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="f03ee-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="f03ee-127">SSL 인증서 tooa 함수 앱을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="f03ee-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="f03ee-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="f03ee-129">업로드 된 SSL 인증서 tooa 함수 앱에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f03ee-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f03ee-130">Next steps</span></span>

<span data-ttu-id="f03ee-131">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f03ee-132">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서]()합니다.</span><span class="sxs-lookup"><span data-stu-id="f03ee-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
