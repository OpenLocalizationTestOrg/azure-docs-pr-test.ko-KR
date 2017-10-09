---
title: "aaaDeploy OpenShift 원점 tooAzure | Microsoft Docs"
description: "Toodeploy OpenShift 원점 tooAzure 가상 컴퓨터에 알아봅니다."
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="8e309-103">OpenShift 원점 tooAzure 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="8e309-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="8e309-104">[OpenShift Origin](https://www.openshift.org/)은 [Kubernetes](https://kubernetes.io/)를 기반으로 하는 오픈 소스 컨테이너 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="8e309-105">Hello 프로세스 배포를 확장 하 고 다중 테 넌 트 응용 프로그램을 운영을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="8e309-106">이 가이드에서는 Azure CLI 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure 가상 컴퓨터에서 OpenShift 원점 toodeploy hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="8e309-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e309-108">KeyVault toomanage hello OpenShift 클러스터에 대 한 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="8e309-109">Azure VM에 OpenShift 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="8e309-110">설치 및 구성 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="8e309-111">Hello OpenShift 배포를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="8e309-112">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="8e309-113">이 빠른 시작 hello Azure CLI 버전 2.0.8 필요 이상.</span><span class="sxs-lookup"><span data-stu-id="8e309-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="8e309-114">toofind hello 버전을 실행 `az --version`합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="8e309-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="8e309-116">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="8e309-116">Log in tooAzure</span></span> 
<span data-ttu-id="8e309-117">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 및 지시를 따른 hello 화면에 표시 하거나 클릭 **실습** toouse 클라우드 셸 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="8e309-118">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8e309-118">Create a resource group</span></span>

<span data-ttu-id="8e309-119">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8e309-120">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8e309-121">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="8e309-122">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="8e309-122">Create a Key Vault</span></span>
<span data-ttu-id="8e309-123">Hello로 KeyVault toostore hello hello 클러스터에 대 한 SSH 키를 만들기 [az keyvault 만들](/cli/azure/keyvault#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="8e309-124">SSH 키 만들기</span><span class="sxs-lookup"><span data-stu-id="8e309-124">Create an SSH key</span></span> 
<span data-ttu-id="8e309-125">SSH 키에는 필요한 toosecure 액세스 toohello OpenShift 원본 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="8e309-126">SSH 키 쌍 만들기 hello를 사용 하 여 `ssh-keygen` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="8e309-127">SSH 키 쌍 만들면 hello에 암호를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="8e309-128">Windows에서는 SSH 키에 대 한 자세한 내용은 [Windows에서 toocreate SSH 키는 어떻게](/azure/virtual-machines/linux/ssh-from-windows)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="8e309-129">Key Vault에 SSH 개인 키 저장</span><span class="sxs-lookup"><span data-stu-id="8e309-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="8e309-130">hello OpenShift 배포 toosecure 액세스 toohello OpenShift 마스터 만든 hello SSH 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="8e309-131">tooenable hello 배포 toosecurely hello SSH 키를 검색, 키 자격 증명 모음의 hello 다음 명령을 사용 하 여 hello 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="8e309-132">템플릿 배포를 위한 사용</span><span class="sxs-lookup"><span data-stu-id="8e309-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="8e309-133">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8e309-133">Create a service principal</span></span> 
<span data-ttu-id="8e309-134">OpenShift는 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="8e309-135">Azure 서비스 주체는 앱, 서비스 및 OpenShift와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="8e309-136">제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="8e309-137">제공 하는 것 사용자 이름 및 암호를 통해 tooimprove 보안,이 예제에서는 기본 서비스 보안 주체</span><span class="sxs-lookup"><span data-stu-id="8e309-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="8e309-138">서비스와 사용자 만들기 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) OpenShift 해야 하는 출력 hello 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="8e309-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="8e309-139">Hello 명령에서 반환 된 hello appId 속성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="8e309-140">안전하지 않은 암호를 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8e309-140">Don't create an insecure password.</span></span>  <span data-ttu-id="8e309-141">[Azure AD 암호 규칙 및 제한 사항](/azure/active-directory/active-directory-passwords-policy) 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8e309-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="8e309-142">서비스 주체에 대한 자세한 내용은 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e309-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="8e309-143">Hello OpenShift 원본 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="8e309-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="8e309-144">다음으로 Azure Resource Manager 템플릿을 사용하여 OpenShift Origin을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8e309-145">hello 다음 명령을 사용 하려면 CLI 2.0.8 az 이상.</span><span class="sxs-lookup"><span data-stu-id="8e309-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="8e309-146">확인할 수 있습니다 az CLI hello hello로 버전 `az --version` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="8e309-147">tooupdate hello CLI 버전 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="8e309-148">사용 하 여 hello `appId` hello에 대 한 이전에 만든 hello 서비스 보안 주체에서 값 `aadClientId` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="8e309-149">hello 배포 too20 분 toocomplete를 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="8e309-150">hello hello OpenShift 콘솔의 URL 및 hello의 DNS 이름을 OpenShift 마스터는 인쇄 toohello 터미널 hello 배포가 완료 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="8e309-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="8e309-151">Toohello OpenShift 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="8e309-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="8e309-152">Hello 배포가 완료 되 면 hello를 사용 하 여 hello 브라우저를 사용 하 여 toohello OpenShift 콘솔 연결 `OpenShift Console Uri`합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="8e309-153">또는 다음 명령을 hello를 사용 하 여 toohello OpenShift 마스터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="8e309-154">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="8e309-154">Clean up resources</span></span>
<span data-ttu-id="8e309-155">더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, OpenShift 클러스터 및 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8e309-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e309-156">Next steps</span></span>

<span data-ttu-id="8e309-157">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8e309-158">KeyVault toomanage hello OpenShift 클러스터에 대 한 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="8e309-159">Azure VM에 OpenShift 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="8e309-160">설치 및 구성 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="8e309-161">이제 해당 OpenShift Origin 클러스터가 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="8e309-162">OpenShift 자습서 toolearn 방법을 따를 수 있습니다 toodeploy 첫 번째 응용 프로그램 및 사용 하 여 hello OpenShift 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="8e309-163">참조 [OpenShift Origin 시작](https://docs.openshift.org/latest/getting_started/index.html) tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e309-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
