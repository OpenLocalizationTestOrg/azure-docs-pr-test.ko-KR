---
title: "Azure CLI 스크립트 샘플 - 배치 계정 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="d4e42-103">Azure CLI로 배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d4e42-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="d4e42-104">이 스크립트는 Azure 배치 계정을 만들고 계정의 다양한 속성을 쿼리 및 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4e42-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4e42-105">Prerequisites</span></span>

<span data-ttu-id="d4e42-106">아직 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)에 있는 지침을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="d4e42-107">배치 계정 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d4e42-107">Batch account sample script</span></span>

<span data-ttu-id="d4e42-108">배치 계정을 만들 때 기본적으로 계산 노드가 Batch 서비스에 내부적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="d4e42-109">할당된 계산 노드에는 별도의 코어 할당량이 적용되며 공유 키 자격 증명 또는 Azure Active Dirctory 토큰을 통해 계정을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="d4e42-110">[!code-azurecli[메인](../../../cli_scripts/batch/create-account/create-account.sh "계정 만들기")]</span><span class="sxs-lookup"><span data-stu-id="d4e42-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="d4e42-111">사용자 구독을 사용하는 배치 계정 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d4e42-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="d4e42-112">Batch에서 사용자 고유의 Azure 구독에 계산 노드를 만들도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="d4e42-113">계산 노드를 구독에 할당한 계정은 Azure Active Directory 토큰을 통해 인증되어야 하며 할당된 계산 노드는 구독 할당량에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="d4e42-114">이 모드에서 계정을 만들려면 계정을 만들 때 Key Vault를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="d4e42-115">[!code-azurecli[메인](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "사용자 구독을 사용하여 계정 만들기")]</span><span class="sxs-lookup"><span data-stu-id="d4e42-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d4e42-116">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d4e42-116">Clean up deployment</span></span>

<span data-ttu-id="d4e42-117">위의 샘플 스크립트 중 하나를 실행한 후 다음 명령을 실행하여 리소스 그룹 및 관련된 모든 리소스(배치 계정, Azure Storage 계정 및 Azure Key Vault)를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d4e42-118">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d4e42-118">Script explanation</span></span>

<span data-ttu-id="d4e42-119">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 배치 계정 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="d4e42-120">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d4e42-121">명령</span><span class="sxs-lookup"><span data-stu-id="d4e42-121">Command</span></span> | <span data-ttu-id="d4e42-122">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d4e42-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4e42-123">az group create</span><span class="sxs-lookup"><span data-stu-id="d4e42-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d4e42-124">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4e42-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="d4e42-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="d4e42-126">배치 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="d4e42-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="d4e42-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="d4e42-128">배치 계정의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="d4e42-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="d4e42-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="d4e42-130">지정된 배치 계정의 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="d4e42-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="d4e42-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="d4e42-132">지정된 배치 계정의 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="d4e42-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d4e42-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="d4e42-134">추가 CLI 상호 작용을 위해 지정된 배치 계정에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="d4e42-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="d4e42-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d4e42-136">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="d4e42-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="d4e42-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="d4e42-138">키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="d4e42-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="d4e42-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="d4e42-140">지정된 주요 자격 증명 모음의 보안 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="d4e42-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="d4e42-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d4e42-142">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4e42-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4e42-143">Next steps</span></span>

<span data-ttu-id="d4e42-144">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4e42-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d4e42-145">추가 Batch CLI 스크립트 샘플은 [Azure Batch CLI 설명서](../batch-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4e42-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
