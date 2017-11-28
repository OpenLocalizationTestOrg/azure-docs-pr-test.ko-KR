---
title: "SAS 토큰 및 Azure CLI Azure 템플릿 aaaDeploy | Microsoft Docs"
description: "보호 되는 서식 파일에서 Azure 리소스 관리자 및 Azure CLI toodeploy 리소스 tooAzure SAS 토큰으로 사용 합니다."
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
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="d3a4a-103">SAS 토큰과 Azure CLI를 사용하여 개인 Resource Manager 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="d3a4a-104">서식 파일에는 저장소 계정에 있는 access toohello 서식 파일을 제한할 수 있으며 공유 액세스 서명 (SAS) 토큰을 배포 하는 동안 제공 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="d3a4a-105">이 항목에서는 설명 어떻게 toouse Azure PowerShell 리소스 관리자 템플릿 tooprovide 배포 하는 동안 SAS 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="d3a4a-106">개인 템플릿 toostorage 계정 추가</span><span class="sxs-lookup"><span data-stu-id="d3a4a-106">Add private template toostorage account</span></span>

<span data-ttu-id="d3a4a-107">템플릿 tooa 저장소 계정 추가 및 SAS 토큰과 함께 배포 하는 동안 toothem 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3a4a-108">다음 hello 단계를 따라 hello 서식 파일을 포함 하는 hello blob 액세스 가능한 tooonly hello 계정 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="d3a4a-109">그러나 hello blob에 대 한 SAS 토큰을 만들 때 hello blob은 해당 URI로 액세스할 수 있는 tooanyone 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="d3a4a-110">다른 사용자 hello URI를 가로채는 경우 해당 사용자 수 tooaccess hello 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="d3a4a-111">SAS 토큰을 사용 하 여 access tooyour 서식 파일을 제한 하는 좋은 방법 이지만 hello 서식 파일에 직접 암호 같은 중요 한 데이터를 포함 하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="d3a4a-112">hello 다음 예제에서는 개인 저장소 계정 컨테이너를 설정 하는 고 서식 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="d3a4a-113">배포하는 동안 SAS 토큰 제공</span><span class="sxs-lookup"><span data-stu-id="d3a4a-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="d3a4a-114">저장소 계정에 개인 템플릿 toodeploy SAS 토큰을 생성 및 hello 서식 파일에 대 한 hello URI에에서 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="d3a4a-115">Hello 만료 시간 tooallow 충분 한 시간 toocomplete hello 배포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
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

<span data-ttu-id="d3a4a-116">연결된 템플릿에 SAS 토큰을 사용하는 예제는 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3a4a-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3a4a-117">Next steps</span></span>
* <span data-ttu-id="d3a4a-118">소개 toodeploying 서식 파일에 대 한 참조 [리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](resource-group-template-deploy-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="d3a4a-119">템플릿을 배포하는 전체 샘플 스크립트는 [Resource Manager 템플릿 배포 스크립트](resource-manager-samples-cli-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="d3a4a-120">서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="d3a4a-121">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a4a-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
