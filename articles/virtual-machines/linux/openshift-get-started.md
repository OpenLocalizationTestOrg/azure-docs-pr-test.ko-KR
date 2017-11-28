---
title: "Azure에 OpenShift Origin 배포 | Microsoft Docs"
description: "Azure 가상 컴퓨터에 OpenShift Origin을 배포하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="ae9c4-103">Azure 가상 컴퓨터에 OpenShift Origin 배포</span><span class="sxs-lookup"><span data-stu-id="ae9c4-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="ae9c4-104">[OpenShift Origin](https://www.openshift.org/)은 [Kubernetes](https://kubernetes.io/)를 기반으로 하는 오픈 소스 컨테이너 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="ae9c4-105">다중 테넌트 응용 프로그램의 배포, 크기 조정 및 운영 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="ae9c4-106">이 가이드에서는 Azure CLI 및 Azure Resource Manager 템플릿을 사용하여 OpenShift Origin을 Azure Virtual Machines에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="ae9c4-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae9c4-108">OpenShift 클러스터에 대한 SSH 키를 관리하는 KeyVault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="ae9c4-109">Azure VM에 OpenShift 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="ae9c4-110">[OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index)를 설치 및 구성하여 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="ae9c4-111">OpenShift 배포를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="ae9c4-112">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="ae9c4-113">이 빠른 시작을 위해서는 Azure CLI 버전 2.0.8 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="ae9c4-114">버전을 찾으려면 `az --version`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="ae9c4-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="ae9c4-116">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ae9c4-116">Log in to Azure</span></span> 
<span data-ttu-id="ae9c4-117">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따르거나 **시도**를 클릭하여 Cloud Shell을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="ae9c4-118">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ae9c4-118">Create a resource group</span></span>

<span data-ttu-id="ae9c4-119">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ae9c4-120">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ae9c4-121">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="ae9c4-122">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="ae9c4-122">Create a Key Vault</span></span>
<span data-ttu-id="ae9c4-123">[az keyvault create](/cli/azure/keyvault#create) 명령을 사용하여 클러스터에 대한 SSH 키를 저장할 KeyVault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="ae9c4-124">SSH 키 만들기</span><span class="sxs-lookup"><span data-stu-id="ae9c4-124">Create an SSH key</span></span> 
<span data-ttu-id="ae9c4-125">SSH 키는 OpenShift Origin 클러스터에 대한 액세스를 보호하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="ae9c4-126">`ssh-keygen` 명령을 사용하여 SSH 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="ae9c4-127">만드는 SSH 키 쌍에는 암호를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="ae9c4-128">Windows에서의 SSH 키에 대한 자세한 내용은 [Windows에서 SSH 키를 만드는 방법](/azure/virtual-machines/linux/ssh-from-windows)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="ae9c4-129">Key Vault에 SSH 개인 키 저장</span><span class="sxs-lookup"><span data-stu-id="ae9c4-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="ae9c4-130">OpenShift 배포는 사용자가 만든 SSH 키를 사용하여 OpenShift 마스터에 대한 액세스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="ae9c4-131">SSH 키를 안전하게 검색하기 위해 배포를 사용하도록 설정하려면 다음 명령을 사용하여 Key Vault에 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="ae9c4-132">템플릿 배포를 위한 사용</span><span class="sxs-lookup"><span data-stu-id="ae9c4-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="ae9c4-133">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ae9c4-133">Create a service principal</span></span> 
<span data-ttu-id="ae9c4-134">OpenShift는 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="ae9c4-135">Azure 서비스 주체는 앱, 서비스 및 OpenShift와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="ae9c4-136">서비스 주체가 Azure에서 수행할 수 있는 작업에 대한 사용 권한은 사용자가 제어하고 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="ae9c4-137">사용자 이름 및 암호를 입력하는 것 이상으로 보안을 강화하기 위해 이 예제에서는 기본 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="ae9c4-138">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)를 사용하여 서비스 주체를 만들고 OpenShift가 필요로 하는 자격 증명을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="ae9c4-139">명령에서 반환되는 appId 속성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="ae9c4-140">안전하지 않은 암호를 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-140">Don't create an insecure password.</span></span>  <span data-ttu-id="ae9c4-141">[Azure AD 암호 규칙 및 제한 사항](/azure/active-directory/active-directory-passwords-policy) 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="ae9c4-142">서비스 주체에 대한 자세한 내용은 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="ae9c4-143">OpenShift Origin 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="ae9c4-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="ae9c4-144">다음으로 Azure Resource Manager 템플릿을 사용하여 OpenShift Origin을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ae9c4-145">다음 명령은 az CLI 2.0.8 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="ae9c4-146">`az --version` 명령으로 az CLI 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="ae9c4-147">CLI 버전을 업데이트하려면 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="ae9c4-148">`aadClientId` 매개 변수에 대해 이전에 만든 서비스 주체에서 `appId` 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="ae9c4-149">배포가 완료되는 데 최대 20분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="ae9c4-150">배포가 완료되면 OpenShift 콘솔의 URL과 OpenShift 마스터의 DNS 이름이 터미널에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="ae9c4-151">OpenShift 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="ae9c4-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="ae9c4-152">배포가 완료되면 브라우저에서 `OpenShift Console Uri`를 사용하여 OpenShift 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="ae9c4-153">또는 다음 명령을 사용하여 OpenShift 마스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="ae9c4-154">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="ae9c4-154">Clean up resources</span></span>
<span data-ttu-id="ae9c4-155">더 이상 필요하지 않은 경우 [az group delete](/cli/azure/group#delete) 명령을 사용하여 리소스 그룹, OpenShift 클러스터 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ae9c4-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae9c4-156">Next steps</span></span>

<span data-ttu-id="ae9c4-157">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ae9c4-158">OpenShift 클러스터에 대한 SSH 키를 관리하는 KeyVault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="ae9c4-159">Azure VM에 OpenShift 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="ae9c4-160">[OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index)를 설치 및 구성하여 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="ae9c4-161">이제 해당 OpenShift Origin 클러스터가 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="ae9c4-162">OpenShift 자습서를 수행하여 첫 번째 응용 프로그램을 배포하고 OpenShift 도구를 사용하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="ae9c4-163">시작하려면 [OpenShift Origin 시작](https://docs.openshift.org/latest/getting_started/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae9c4-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
