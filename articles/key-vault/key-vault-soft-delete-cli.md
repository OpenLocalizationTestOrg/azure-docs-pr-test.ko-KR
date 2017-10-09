---
ms.assetid: 
title: "키 자격 증명 모음 aaaAzure-CLI와 toouse 소프트 삭제 하는 방법"
description: "CLI 코드 캡처를 통한 일시 삭제의 사용 사례 예제"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="39d60-103">CLI 키 자격 증명 모음 toouse 소프트-삭제 방법</span><span class="sxs-lookup"><span data-stu-id="39d60-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="39d60-104">Azure Key Vault의 일시 삭제 기능을 사용하면 삭제된 자격 증명 모음 및 자격 증명 모음 개체를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="39d60-105">특히, 소프트 삭제 주소 hello 다음 시나리오:</span><span class="sxs-lookup"><span data-stu-id="39d60-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="39d60-106">Key Vault의 복구 가능한 삭제 지원</span><span class="sxs-lookup"><span data-stu-id="39d60-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="39d60-107">Key Vault 개체(예: 키, 비밀 및 인증서)의 복구 가능한 삭제를 지원</span><span class="sxs-lookup"><span data-stu-id="39d60-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39d60-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="39d60-108">Prerequisites</span></span>

- <span data-ttu-id="39d60-109">Azure CLI 2.0 - 사용자 환경에 이 단계가 없는 경우 [CLI 2.0을 사용한 Key Vault 관리](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39d60-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="39d60-110">CLI에 대한 Key Vault 관련 특정 참조 정보는 [Azure CLI 2.0 Key Vault 참조](https://docs.microsoft.com/cli/azure/keyvault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39d60-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="39d60-111">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="39d60-111">Required permissions</span></span>

<span data-ttu-id="39d60-112">Key Vault 작업은 RBAC(역할 기반 액세스 제어) 권한을 통해 다음과 같이 별도로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="39d60-113">작업</span><span class="sxs-lookup"><span data-stu-id="39d60-113">Operation</span></span> | <span data-ttu-id="39d60-114">설명</span><span class="sxs-lookup"><span data-stu-id="39d60-114">Description</span></span> | <span data-ttu-id="39d60-115">사용자 권한</span><span class="sxs-lookup"><span data-stu-id="39d60-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="39d60-116">나열</span><span class="sxs-lookup"><span data-stu-id="39d60-116">List</span></span>|<span data-ttu-id="39d60-117">삭제된 Key Vault를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="39d60-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="39d60-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="39d60-119">복구</span><span class="sxs-lookup"><span data-stu-id="39d60-119">Recover</span></span>|<span data-ttu-id="39d60-120">삭제된 Key Vault를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="39d60-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="39d60-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="39d60-122">제거</span><span class="sxs-lookup"><span data-stu-id="39d60-122">Purge</span></span>|<span data-ttu-id="39d60-123">삭제된 Key Vault 및 모든 콘텐츠를 영구적으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="39d60-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="39d60-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="39d60-125">권한 및 액세스 제어에 대한 자세한 내용은 [Key Vault 보안](key-vault-secure-your-key-vault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39d60-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="39d60-126">일시 삭제를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="39d60-126">Enabling soft-delete</span></span>

<span data-ttu-id="39d60-127">toobe 수 toorecover 키에 저장 된 개체 또는 삭제 된 키 자격 증명 모음 자격 증명 모음, 해당 키 자격 증명 모음에 대 한 일시 삭제를 먼저 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="39d60-128">기존 Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="39d60-128">Existing key vault</span></span>

<span data-ttu-id="39d60-129">ContosoVault라는 기존 Key Vault의 경우 다음과 같이 일시 삭제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="39d60-130">Toouse Azure 리소스 관리자 리소스 조작 toodirectly 쓰기 hello 필요한 현재 *enableSoftDelete* 속성 toohello 주요 자격 증명 모음 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="39d60-131">새로운 Key Vault</span><span class="sxs-lookup"><span data-stu-id="39d60-131">New key vault</span></span>

<span data-ttu-id="39d60-132">새 키 자격 증명 모음에 대 한 일시 삭제를 사용 하도록 설정 이루어집니다 hello 소프트 삭제 사용 플래그를 추가 하 여 생성 시 tooyour 만들기 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="39d60-133">일시 삭제 사용 확인</span><span class="sxs-lookup"><span data-stu-id="39d60-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="39d60-134">실행된 hello 주요 자격 증명 모음에 소프트 삭제가 활성화 tooverify *표시* ' 소프트 삭제 됨 ' hello에 대 한 찾은 명령</span><span class="sxs-lookup"><span data-stu-id="39d60-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="39d60-135">특성과 해당 설정(true 또는 false)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="39d60-136">일시 삭제로 보호되는 Key Vault 삭제</span><span class="sxs-lookup"><span data-stu-id="39d60-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="39d60-137">hello 명령 toodelete (또는 제거) hello 동일 하지만 해당 동작 변경 내용 설정 여부에 따라 소프트 삭제 여부 주요 자격 증명 모음에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="39d60-138">소프트 삭제 사용 하도록 설정 하지 않은 키 자격 증명 모음에 대 한 hello 이전 명령을 실행 하면이 주요 자격 증명 모음 및 복구에 대 한 옵션 없이 모든 내용이 영구적으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="39d60-139">일시 삭제가 Key Vault를 보호하는 방식</span><span class="sxs-lookup"><span data-stu-id="39d60-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="39d60-140">활성화된 일시 삭제 사용:</span><span class="sxs-lookup"><span data-stu-id="39d60-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="39d60-141">키 자격 증명 모음 삭제 되 면 리소스 그룹에서 제거 하 고만 예약된 된 네임 스페이스에 배치 되는 만들어진 hello 위치와 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="39d60-142">개체 삭제 된 키에 액세스할 수 없는 키, 암호, 인증서, 같은 자격 증명 모음 및가 포함 된 주요 자격 증명 모음 삭제 hello 상태인 동안 서 항상 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="39d60-143">주요 자격 증명 모음 삭제 된 상태에서에 대 한 hello DNS 이름 이므로 계속 예약 되어, 동일한 이름 가진는 새 주요 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="39d60-144">다음 명령을 hello를 사용 하 여 삭제 된 상태 키 자격 증명 모음에 연결 된 구독을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="39d60-145">hello *리소스 ID* 출력 hello에서이 자격 증명 모음의 toohello 원래 리소스 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="39d60-146">이제 이 Key Vault가 삭제된 상태로 있으므로 해당 리소스 ID를 사용하는 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="39d60-147">hello *Id* 필드에는 사용 되는 tooidentify hello 리소스, 복구 또는 제거 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="39d60-148">hello *제거 날짜 예약* 필드 나타냅니다 경우 hello 자격 증명 모음 영구적으로 삭제 됩니다 (삭제) 아무 작업도이 삭제 된 자격 증명 모음에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="39d60-149">hello 기본 보존 기간으로 사용 하는 toocalculate hello *제거 날짜 예약*, 90 일입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="39d60-150">Key Vault 복구</span><span class="sxs-lookup"><span data-stu-id="39d60-150">Recovering a key vault</span></span>

<span data-ttu-id="39d60-151">주요 자격 증명 모음 toorecover toospecify hello 주요 자격 증명 모음 이름, 리소스 그룹 및 위치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="39d60-152">주요 자격 증명 모음 복구 프로세스에 대 한 이러한 필요에 따라 키 자격 증명 모음 삭제 하는 hello의 참고 hello 위치와 hello 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="39d60-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="39d60-153">Hello 결과 hello 주요 자격 증명 모음의 원래 리소스 ID 사용 하 여 새 리소스는 주요 자격 증명 모음을 복구 하는 경우</span><span class="sxs-lookup"><span data-stu-id="39d60-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="39d60-154">Hello 주요 자격 증명 모음 존재 했던 hello 리소스 그룹을 제거한 경우 같은 이름의 새 리소스 그룹 만들어야 hello 주요 자격 증명 모음을 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="39d60-155">Key Vault 개체 및 일시 삭제</span><span class="sxs-lookup"><span data-stu-id="39d60-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="39d60-156">일시 삭제가 활성화되어 있는 ‘ContosoVault’라는 Key Vault의 ‘ContosoFirstKey’ 키의 경우 여기에 어떻게 해당 키를 삭제하는지가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="39d60-157">일시 삭제가 활성화되어 있는 Key Vault를 사용하면 삭제된 키를 명시적으로 나열하거나 검색할 때 외에는 삭제된 키가 여전히 삭제된 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="39d60-158">Hello 삭제 된 상태에서 키에서 대부분의 작업은 삭제 된 키를 나열, 복구 또는 제거 하는 제외 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="39d60-159">예를 들어, 주요 자격 증명 모음에 있는 toorequest 삭제 toolist 키 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="39d60-160">전환 상태</span><span class="sxs-lookup"><span data-stu-id="39d60-160">Transition state</span></span> 

<span data-ttu-id="39d60-161">소프트 삭제 사용 하도록 설정 된 키 자격 증명 모음에 키를 삭제 하면 hello 전환 toocomplete 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="39d60-162">이 전환 상태 hello 활성 상태 또는 삭제 하는 hello 상태에 해당 hello 키가이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="39d60-163">이 명령은 ‘ContosoVault’라는 Key Vault에 있는 모든 삭제된 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="39d60-164">Key Vault 개체를 통해 일시 삭제 사용</span><span class="sxs-lookup"><span data-stu-id="39d60-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="39d60-165">키 자격 증명 모음 키를 삭제 된 처럼 암호 또는 인증서에에서 유지 됩니다 too90 (일) 삭제 된 상태에 대 한 복구 하거나 제거 하지 않으면.</span><span class="sxs-lookup"><span data-stu-id="39d60-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="39d60-166">구성</span><span class="sxs-lookup"><span data-stu-id="39d60-166">Keys</span></span>

<span data-ttu-id="39d60-167">toorecover 삭제 된 키:</span><span class="sxs-lookup"><span data-stu-id="39d60-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="39d60-168">toopermanently 키 삭제:</span><span class="sxs-lookup"><span data-stu-id="39d60-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="39d60-169">키 제거는 키를 영구적으로 삭제하며 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="39d60-170">hello **복구** 및 **제거** 동작 사용 권한이 자신의 주요 자격 증명 모음 액세스 정책에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="39d60-171">사용자 또는 서비스 보안 주체 toobe 수 tooexecute에 대 한 한 **복구** 또는 **제거** 작업 hello 주요 자격 증명 모음 액세스 정책에서 해당 개체 (키 또는 암호)에 대 한 해당 권한을 hello을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="39d60-172">기본적으로 hello **제거** hello 'all' 바로 가기는 사용 되는 toogrant 때 권한이 tooa 주요 자격 증명 모음의 액세스 정책 추가 되지 않습니다 모든 사용 권한 tooa 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="39d60-173">**제거** 권한을 명시적으로 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="39d60-174">예를 들어 다음 명령은 부여 hello user@contoso.com 권한 tooperform 키에 대 한 여러 작업 *ContosoVault* 포함 하 여 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="39d60-175">Key Vault 액세스 정책 설정</span><span class="sxs-lookup"><span data-stu-id="39d60-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="39d60-176">이제 막 일시 삭제 활성화되도록 기존 Key Vault를 설정한 경우 **복구** 및 **제거** 권한이 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="39d60-177">비밀</span><span class="sxs-lookup"><span data-stu-id="39d60-177">Secrets</span></span>

<span data-ttu-id="39d60-178">키와 마찬가지로 Key Vault의 비밀도 자체 명령으로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="39d60-179">다음, 삭제, 나열, 복구 및 암호의 한 제거에 대 한 hello 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="39d60-180">SQLPassword라는 비밀 삭제:</span><span class="sxs-lookup"><span data-stu-id="39d60-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="39d60-181">Key Vault의 모든 삭제된 비밀 나열:</span><span class="sxs-lookup"><span data-stu-id="39d60-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="39d60-182">Hello 삭제 상태에 암호 복구:</span><span class="sxs-lookup"><span data-stu-id="39d60-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="39d60-183">삭제된 상태의 비밀 제거:</span><span class="sxs-lookup"><span data-stu-id="39d60-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="39d60-184">비밀 제거는 비밀을 영구적으로 삭제하며 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="39d60-185">제거 및 Key Vault</span><span class="sxs-lookup"><span data-stu-id="39d60-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="39d60-186">Key Vault 개체</span><span class="sxs-lookup"><span data-stu-id="39d60-186">Key vault objects</span></span>

<span data-ttu-id="39d60-187">키, 비밀 또는 인증서 제거는 해당 항목을 영구적으로 삭제하며 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="39d60-188">그러나 다른 모든 개체에 hello 주요 자격 증명 모음 됩니다에 hello 주요 자격 증명 모음 삭제 hello 개체를 포함 하는 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="39d60-189">컨테이너로써의 Key Vault</span><span class="sxs-lookup"><span data-stu-id="39d60-189">Key vaults as containers</span></span>
<span data-ttu-id="39d60-190">Key Vault를 제거하면 키, 비밀 및 인증서를 포함한 모든 콘텐츠가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="39d60-191">hello를 사용 하 여 주요 자격 증명 모음 toopurge `az keyvault purge` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="39d60-192">구독 삭제 된 키 자격 증명 모음 hello 명령을 사용 하 여 hello 위치를 찾을 수 있습니다 `az keyvault list-deleted`합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="39d60-193">Key Vault 제거는 영구적으로 삭제하며 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="39d60-194">제거 권한 필요</span><span class="sxs-lookup"><span data-stu-id="39d60-194">Purge permissions required</span></span>
- <span data-ttu-id="39d60-195">삭제 된 키 자격 증명 모음 toopurge hello 자격 증명 모음 및 모든 내용이 영구적으로 제거 되도록 hello 사용자에 게 필요한 권한이 tooperform RBAC는 *Microsoft.KeyVault/locations/deletedVaults/purge/action* 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="39d60-196">toolist 삭제 hello 키 hello 사용자 자격 증명 모음 필요한 RBAC 사용 권한을 tooperform *Microsoft.KeyVault/deletedVaults/read* 권한.</span><span class="sxs-lookup"><span data-stu-id="39d60-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="39d60-197">기본적으로 구독 관리자만 이러한 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="39d60-198">예약된 제거</span><span class="sxs-lookup"><span data-stu-id="39d60-198">Scheduled purge</span></span>

<span data-ttu-id="39d60-199">키 자격 증명 모음을 삭제 된 개체가 나열 schedled toobe 키 자격 증명 모음에서 제거 되 면 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="39d60-200">hello *제거 날짜 예약* 필드 이면 경우 키 자격 증명 모음 개체를 영구적으로 삭제 됩니다, 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="39d60-201">기본적으로 키 자격 증명 모음을 삭제 된 개체에 대 한 보존 기간 hello은 90 일입니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="39d60-202">해당 *예약된 제거 날짜* 필드에 의해 트리거되는 제거된 자격 증명 모음 개체가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="39d60-203">복구할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39d60-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="39d60-204">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="39d60-204">Other resources</span></span>

- <span data-ttu-id="39d60-205">Key Vault의 일시 삭제 기능에 대한 자세한 내용은 [Azure Key Vault 일시 삭제 개요](key-vault-ovw-soft-delete.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39d60-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="39d60-206">Azure Key Vault 사용의 일반적인 개요는 [Azure Key Vault 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39d60-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

