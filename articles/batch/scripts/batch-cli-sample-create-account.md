---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리 계정 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 배치 계정 만들기"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="d2e5f-103">Hello Azure CLI로 일괄 처리 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d2e5f-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="d2e5f-104">이 스크립트는 Azure 배치 계정을 만들고 고 hello 계정의 다양 한 속성을 쿼리할 업데이트 하 고 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2e5f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2e5f-105">Prerequisites</span></span>

<span data-ttu-id="d2e5f-106">설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="d2e5f-107">배치 계정 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d2e5f-107">Batch account sample script</span></span>

<span data-ttu-id="d2e5f-108">일괄 처리 계정을 만들 때 기본적으로는 계산 노드 할당 내부적으로 hello 일괄 처리 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="d2e5f-109">할당 된 계산 노드 제목 tooa 별도 코어 할당량 되며 hello 계정 공유 키 자격 증명 또는 Azure Active Dirctory 토큰을 통해 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="d2e5f-110">사용자 구독을 사용하는 배치 계정 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d2e5f-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="d2e5f-111">선택할 수 있습니다 일괄 처리 toohave Azure 구독에서의 계산 노드 만들기.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="d2e5f-112">계정을 할당 하는 노드를 구독으로 Azure Active Directory 토큰을 통해 인증 되어야 하며 현재 구독 할당량이 진행할 할당 된 hello 계산 노드 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="d2e5f-113">이 모드에서는 계정 toocreate hello 계정을 만들 때 자격 증명 모음 키 참조를 지정 해야 하나 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d2e5f-114">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d2e5f-114">Clean up deployment</span></span>

<span data-ttu-id="d2e5f-115">Hello 위의 예제 스크립트를 실행 한 후 리소스 그룹과 관련 된 모든 리소스 (일괄 처리 계정, Azure 저장소 계정 및 Azure 키 자격 증명 모음은 포함) hello 명령 tooremove 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d2e5f-116">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d2e5f-116">Script explanation</span></span>

<span data-ttu-id="d2e5f-117">이 스크립트 명령 toocreate 리소스 그룹, 일괄 처리 계정 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="d2e5f-118">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d2e5f-119">명령</span><span class="sxs-lookup"><span data-stu-id="d2e5f-119">Command</span></span> | <span data-ttu-id="d2e5f-120">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d2e5f-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d2e5f-121">az group create</span><span class="sxs-lookup"><span data-stu-id="d2e5f-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d2e5f-122">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d2e5f-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="d2e5f-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="d2e5f-124">Hello 일괄 처리 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="d2e5f-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="d2e5f-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="d2e5f-126">일괄 처리 계정 hello의 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="d2e5f-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="d2e5f-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="d2e5f-128">일괄 처리 계정을 지정 하는 hello의 검색 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="d2e5f-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="d2e5f-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="d2e5f-130">일괄 처리 계정을 지정 하는 hello의 hello 선택 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="d2e5f-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d2e5f-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="d2e5f-132">지정 된 hello에 대 한 인증 계정을 더 이상의 CLI 상호 작용에 대 한 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="d2e5f-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="d2e5f-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d2e5f-134">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="d2e5f-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="d2e5f-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="d2e5f-136">키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="d2e5f-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="d2e5f-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="d2e5f-138">Hello 지정 된 키 자격 증명 모음의 hello 보안 정책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="d2e5f-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="d2e5f-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d2e5f-140">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2e5f-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2e5f-141">Next steps</span></span>

<span data-ttu-id="d2e5f-142">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d2e5f-143">추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e5f-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
