---
title: "일괄 처리에서 응용 프로그램을 추가 하는 CLI 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch로 응용 프로그램 추가"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="7ab94-103">응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="7ab94-104">이 스크립트에서는 어떻게 tooset Azure 배치 풀 또는 작업와 함께 사용할 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="7ab94-105">응용 프로그램을 tooset 패키지.zip 파일에 모든 종속 파일을 함께 실행 파일.</span><span class="sxs-lookup"><span data-stu-id="7ab94-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="7ab94-106">이 예제에서는 hello 실행 파일인 zip 파일은 라고 ' 내-응용 프로그램-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="7ab94-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ab94-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7ab94-107">Prerequisites</span></span>

- <span data-ttu-id="7ab94-108">설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7ab94-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="7ab94-109">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="7ab94-110">참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7ab94-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="7ab94-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="7ab94-112">응용 프로그램 정리</span><span class="sxs-lookup"><span data-stu-id="7ab94-112">Clean up application</span></span>

<span data-ttu-id="7ab94-113">Hello 위의 샘플 스크립트를 실행 한 후 응용 프로그램 및 해당 업로드 된 응용 프로그램 패키지의 모든 명령을 tooremove 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7ab94-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="7ab94-114">Script explanation</span></span>

<span data-ttu-id="7ab94-115">이 스크립트는 응용 프로그램 및 응용 프로그램 패키지 업로드 명령을 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="7ab94-116">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7ab94-117">명령</span><span class="sxs-lookup"><span data-stu-id="7ab94-117">Command</span></span> | <span data-ttu-id="7ab94-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7ab94-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7ab94-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="7ab94-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="7ab94-120">응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-120">Creates an application.</span></span>  |
| [<span data-ttu-id="7ab94-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="7ab94-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="7ab94-122">응용 프로그램의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="7ab94-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="7ab94-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="7ab94-124">지정 하는 응용 프로그램 패키지 toohello 추가 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7ab94-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ab94-125">Next steps</span></span>

<span data-ttu-id="7ab94-126">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7ab94-127">추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab94-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
