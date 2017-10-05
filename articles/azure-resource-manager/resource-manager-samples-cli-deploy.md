---
title: "Azure CLI 스크립트 샘플 - 템플릿 배포 | Microsoft Docs"
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
ms.openlocfilehash: 974230f349aec46fde58e69658e05a13bff4296f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="6be40-103">Azure Resource Manager 템플릿 배포 - Azure CLI 스크립트</span><span class="sxs-lookup"><span data-stu-id="6be40-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="6be40-104">이 스크립트에서는 Resource Manager 템플릿을 구독의 리소스 그룹에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6be40-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="6be40-105">Sample script</span></span>

```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="clean-up-deployment"></a><span data-ttu-id="6be40-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="6be40-106">Clean up deployment</span></span> 

<span data-ttu-id="6be40-107">다음 명령을 실행하여 리소스 그룹과 모든 관련 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-107">Run the following command to remove the resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6be40-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="6be40-108">Script explanation</span></span>

<span data-ttu-id="6be40-109">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="6be40-110">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6be40-111">명령</span><span class="sxs-lookup"><span data-stu-id="6be40-111">Command</span></span> | <span data-ttu-id="6be40-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6be40-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6be40-113">az group exists</span><span class="sxs-lookup"><span data-stu-id="6be40-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="6be40-114">리소스 그룹이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="6be40-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6be40-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6be40-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6be40-117">az group deployment create</span><span class="sxs-lookup"><span data-stu-id="6be40-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="6be40-118">배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="6be40-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="6be40-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6be40-120">모든 리소스를 포함하여 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6be40-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="6be40-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6be40-121">Next steps</span></span>
* <span data-ttu-id="6be40-122">템플릿 배포에 대한 소개는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be40-122">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="6be40-123">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-cli-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be40-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="6be40-124">템플릿에서 매개 변수를 정의하려면 [템플릿 작성](resource-group-authoring-templates.md#parameters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be40-124">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="6be40-125">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be40-125">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

