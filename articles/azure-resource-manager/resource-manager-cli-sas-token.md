---
title: "SAS 토큰 및 Azure CLI로 Azure 템플릿 배포 | Microsoft Docs"
description: "Azure Resource Manager와 Azure CLI를 사용하여 SAS 토큰으로 보호되는 템플릿에서 Azure로 리소스를 배포합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="82ca4-103">SAS 토큰과 Azure CLI를 사용하여 개인 Resource Manager 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="82ca4-104">템플릿이 저장소 계정에 상주하는 경우, 템플릿에 대한 액세스를 제한하고 배포 중에 공유 액세스 서명(SAS) 토큰을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="82ca4-105">이 항목에서는 Resource Manager 템플릿과 함께 Azure PowerShell을 사용하여 배포 중에 SAS 토큰을 제공하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="82ca4-106">저장소 계정에 개인 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="82ca4-106">Add private template to storage account</span></span>

<span data-ttu-id="82ca4-107">SAS 토큰으로 배포 중에 저장소 계정에 템플릿을 추가하고 이를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82ca4-108">아래 단계를 따르면 템플릿을 포함한 blob은 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="82ca4-109">그러나 blob용 SAS 토큰을 생성하면 해당 blob은 해당 URI를 가진 사람이면 누구나 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="82ca4-110">다른 사용자가 URI를 가로채는 경우, 그 사용자가 템플릿에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="82ca4-111">SAS 토큰을 사용하는 것은 템플릿에 액세스를 제한하는 좋은 방법이지만 템플릿에 암호와 같은 민감한 데이터를 직접 입력하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="82ca4-112">다음 예제에서는 개인 저장소 계정 컨테이너를 설정하고 템플릿을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="82ca4-113">배포하는 동안 SAS 토큰 제공</span><span class="sxs-lookup"><span data-stu-id="82ca4-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="82ca4-114">저장소 계정에 개인 템플릿을 배포하려면 SAS 토큰을 생성하고 해당 템플릿의 URI에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="82ca4-115">배포를 완료할 만큼 충분한 여유를 두고 만료 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="82ca4-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="82ca4-116">연결된 템플릿에 SAS 토큰을 사용하는 예제는 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ca4-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82ca4-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82ca4-117">Next steps</span></span>
* <span data-ttu-id="82ca4-118">템플릿 배포에 대한 소개는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ca4-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="82ca4-119">템플릿을 배포하는 전체 샘플 스크립트는 [Resource Manager 템플릿 배포 스크립트](resource-manager-samples-cli-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ca4-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="82ca4-120">템플릿에서 매개 변수를 정의하려면 [템플릿 작성](resource-group-authoring-templates.md#parameters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ca4-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="82ca4-121">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ca4-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
