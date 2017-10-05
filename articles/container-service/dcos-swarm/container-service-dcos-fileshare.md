---
title: "Azure DC/OS 클러스터용 파일 공유| Microsoft Docs"
description: "Azure Container Service에서 DC/OS 클러스터에 파일 공유 만들기 및 탑재"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 549b52bfb0a0268f754da26c6a374b267861f6d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="a7d00-104">DC/OS 클러스터에 파일 공유 만들기 및 탑재</span><span class="sxs-lookup"><span data-stu-id="a7d00-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="a7d00-105">이 문서에서는 Azure에서 파일 공유를 만들어서 DC/OS 클러스터의 각 에이전트 및 마스터에 탑재하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-105">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="a7d00-106">파일 공유를 설정하면 구성, 액세스, 로그 등과 같은 클러스터 전반에서 파일을 간편하게 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="a7d00-107">이 자습서에서는 다음 태스크를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-107">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7d00-108">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d00-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="a7d00-109">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d00-109">Create a file share</span></span>
> * <span data-ttu-id="a7d00-110">DC/OS 클러스터에 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="a7d00-110">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="a7d00-111">이 자습서의 단계를 완료하려면 ACS DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="a7d00-112">필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="a7d00-113">이 자습서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a7d00-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="a7d00-115">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7d00-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="a7d00-116">Microsoft Azure에서 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d00-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="a7d00-117">ACS DC/OS 클러스터에서 Azure 파일 공유를 사용하기 전에 저장소 계정 및 파일 공유를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-117">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="a7d00-118">다음 스크립트를 실행하여 저장소 및 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-118">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="a7d00-119">사용자 환경에서 해당 항목으로 매개 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-119">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="a7d00-120">클러스터에 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="a7d00-120">Mount the share in your cluster</span></span>

<span data-ttu-id="a7d00-121">다음으로 파일 공유는 클러스터 내 모든 가상 컴퓨터에 탑재되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-121">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="a7d00-122">cifs 도구/프로토콜을 사용하여 이 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-122">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="a7d00-123">클러스터의 각 노드에서 수동으로 또는 스크립트를 실행하여 탑재 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-123">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="a7d00-124">이 예제에서는 Azure 파일 공유에 탑재되는 스크립트 및 DC/OS 클러스터의 각 노드에서 이 스크립트를 실행하는 스크립트와 같이 두 개의 스크립트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-124">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="a7d00-125">먼저, Azure Storage 계정 이름과 선택키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-125">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="a7d00-126">다음 명령을 실행하여 이 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-126">Run the following commands to get this information.</span></span> <span data-ttu-id="a7d00-127">이러한 값을 이후 단계에서 사용하도록 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="a7d00-128">저장소 계정 이름:</span><span class="sxs-lookup"><span data-stu-id="a7d00-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="a7d00-129">저장소 계정 선택키:</span><span class="sxs-lookup"><span data-stu-id="a7d00-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="a7d00-130">다음으로 DC/OS 마스터의 FQDN을 가져와서 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-130">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="a7d00-131">마스터 노드에 개인 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-131">Copy your private key to the master node.</span></span> <span data-ttu-id="a7d00-132">이 키는 클러스터의 모든 노드와 SSH 연결을 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-132">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="a7d00-133">클러스터를 만들 때 기본값이 아닌 값이 사용된 경우 사용자 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-133">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="a7d00-134">DC/OS 기반 클러스터의 마스터(또는 첫 번째 마스터)와의 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-134">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="a7d00-135">클러스터를 만들 때 기본값이 아닌 값이 사용된 경우 사용자 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-135">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="a7d00-136">**cifsMount.sh**라는 파일을 만들어서 여기에 다음과 같은 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-136">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="a7d00-137">이 스크립트는 Azure 파일 공유를 탑재하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-137">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="a7d00-138">`STORAGE_ACCT_NAME` 및 `ACCESS_KEY` 변수를 이전에 수집한 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-138">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="a7d00-139">**getNodesRunScript.sh**라는 두 번째 파일을 만들고 파일에 다음 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-139">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="a7d00-140">이 스크립트는 모든 클러스터 노드를 검색한 다음 **cifsMount.sh** 스크립트를 실행하여 각 노드에 파일 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-140">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="a7d00-141">스크립트를 실행하여 클러스터의 모든 노드에서 Azure 파일 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-141">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="a7d00-142">이제 클러스터의 각 노드에 있는 `/mnt/share/dcosshare`에서 파일 공유에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-142">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7d00-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7d00-143">Next steps</span></span>

<span data-ttu-id="a7d00-144">이 자습서에서는 다음 단계를 사용하여 DC/OS 클러스터에 Azure 파일 공유를 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-144">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7d00-145">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d00-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="a7d00-146">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d00-146">Create a file share</span></span>
> * <span data-ttu-id="a7d00-147">DC/OS 클러스터에 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="a7d00-147">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="a7d00-148">다음 자습서로 넘어가서 Azure에서 DC/OS와 Azure Container Registry를 통합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d00-148">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7d00-149">부하 분산 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a7d00-149">Load balance applications</span></span>](container-service-dcos-acr.md)