---
title: "CLI 스크립트 샘플-aaaAzure 템플릿을 배포 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 배포하는 샘플 스크립트"
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
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 5a94eedbd898ced29d67f8ce3023ca5c65f83af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="4e608-103">Azure Resource Manager 템플릿 배포 - Azure CLI 스크립트</span><span class="sxs-lookup"><span data-stu-id="4e608-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="4e608-104">이 스크립트는 구독에서 리소스 관리자 템플릿 tooa 리소스 그룹을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4e608-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4e608-105">Sample script</span></span>

```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --subscription $subscriptionId

#Check for existing RG
if [ $(az group exists --name $resourceGroupName) == 'false' ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
then
    echo "Template has been successfully deployed"
fi
```

## <a name="clean-up-deployment"></a><span data-ttu-id="4e608-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="4e608-106">Clean up deployment</span></span> 

<span data-ttu-id="4e608-107">실행된 hello 다음 tooremove hello 리소스 그룹 및 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4e608-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4e608-108">Script explanation</span></span>

<span data-ttu-id="4e608-109">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4e608-110">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4e608-111">명령</span><span class="sxs-lookup"><span data-stu-id="4e608-111">Command</span></span> | <span data-ttu-id="4e608-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4e608-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e608-113">az group exists</span><span class="sxs-lookup"><span data-stu-id="4e608-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="4e608-114">리소스 그룹이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="4e608-115">az group create</span><span class="sxs-lookup"><span data-stu-id="4e608-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4e608-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4e608-117">az group deployment create</span><span class="sxs-lookup"><span data-stu-id="4e608-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="4e608-118">배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="4e608-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="4e608-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="4e608-120">모든 리소스를 포함하여 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="4e608-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e608-121">Next steps</span></span>
* <span data-ttu-id="4e608-122">소개 toodeploying 서식 파일에 대 한 참조 [리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](resource-group-template-deploy-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-122">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="4e608-123">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-cli-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e608-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="4e608-124">서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-124">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="4e608-125">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e608-125">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

