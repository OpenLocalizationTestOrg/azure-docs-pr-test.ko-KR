---
title: "Azure Kubernetes 클러스터의 서비스 주체 | Microsoft 문서"
description: "Azure Container Service에서 Kubernetes 클러스터에 대한 Azure Active Directory 서비스 주체를 만들고 관리합니다."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="2510e-103">Container Service에서 Kubernetes 클러스터에 대한 Azure AD 서비스 주체 설정</span><span class="sxs-lookup"><span data-stu-id="2510e-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="2510e-104">Azure Container Service에서 Kubernetes 클러스터는 Azure API와 상호 작용하기 위해 [Azure Active Directory 서비스 주체](../../active-directory/develop/active-directory-application-objects.md)를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="2510e-105">서비스 주체는 [사용자 정의 경로](../../virtual-network/virtual-networks-udr-overview.md) 및 [계층 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md)와 같은 리소스를 동적으로 관리하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="2510e-106">이 문서에서는 Kubernetes 클러스터에 대한 서비스 주체를 설정하기 위한 다양한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="2510e-107">예를 들어 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 설정한 경우 [`az acs create`](/cli/azure/acs#create) 명령을 실행하여 Kubernetes 클러스터와 서비스 주체를 동시에 만들 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="2510e-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="2510e-108">서비스 주체에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2510e-108">Requirements for the service principal</span></span>

<span data-ttu-id="2510e-109">다음 요구 사항을 충족하는 기존 Azure AD 서비스 주체를 사용하거나 새 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="2510e-110">**범위**: Kubernetes 클러스터 배포에 사용되는 구독의 리소스 그룹 또는 클러스터 배포에 사용되는 구독(덜 제한적으로)</span><span class="sxs-lookup"><span data-stu-id="2510e-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="2510e-111">**역할**: **참여자**</span><span class="sxs-lookup"><span data-stu-id="2510e-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="2510e-112">**클라이언트 암호**: 암호여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="2510e-113">현재 인증서 인증을 위해 설정된 서비스 주체는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2510e-114">서비스 주체를 만들려면 Azure AD 테넌트에 응용 프로그램을 등록하고 구독의 역할에 해당 응용 프로그램을 할당할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="2510e-115">필요한 권한이 있는지 확인하려면 [포털에서 확인합니다](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="2510e-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="2510e-116">옵션 1: Azure AD에서 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="2510e-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="2510e-117">Kubernetes 클러스터를 배포하기 전에 Azure AD 서비스 주체를 만들려는 경우 Azure에서 여러 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="2510e-118">다음 예제 명령은 [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)을 사용하여 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="2510e-119">또는 [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), [포털](../../azure-resource-manager/resource-group-create-service-principal-portal.md) 또는 다른 방법을 사용하여 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="2510e-120">출력은 다음과 비슷합니다(여기서는 수정된 내용이 표시됨).</span><span class="sxs-lookup"><span data-stu-id="2510e-120">Output is similar to the following (shown here redacted):</span></span>

![서비스 주체 만들기](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="2510e-122">클러스터 배포에 대한 서비스 주체 매개 변수로 사용하는 **클라이언트 ID**(`appId`) 및 **클라이언트 비밀**(`password`)이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="2510e-123">Kubernetes 클러스터를 만들 때 서비스 주체 지정</span><span class="sxs-lookup"><span data-stu-id="2510e-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="2510e-124">Kubernetes 클러스터를 만들 때 기존 서비스 주체의 **클라이언트 ID**(응용 프로그램 ID의 경우 `appId`라고도 함) 및 **클라이언트 비밀**(`password`)을 매개 변수로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="2510e-125">서비스 주체가 이 문서의 시작 부분에 나오는 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="2510e-126">포털, [Azure CLI(명령줄 인터페이스) 2.0](container-service-kubernetes-walkthrough.md), [Azure Portal](../dcos-swarm/container-service-deployment.md) 또는 다른 방법을 사용하여 Kubernetes 클러스터를 배포할 때 이러한 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="2510e-127">**클라이언트 ID**를 지정하는 경우 서비스 주체의 `ObjectId`가 아니라 `appId`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="2510e-128">다음 예제에서는 Azure CLI 2.0에서 매개 변수를 전달하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="2510e-129">여기서는 [Kubernetes 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="2510e-130">GitHub에서 템플릿 매개 변수 파일 `azuredeploy.parameters.json`을 [다운로드](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="2510e-131">서비스 주체를 지정하려면 파일에 `servicePrincipalClientId` 및 `servicePrincipalClientSecret`의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="2510e-132">(또한 `dnsNamePrefix` 및 `sshRSAPublicKey`에 대한 고유한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="2510e-133">후자는 클러스터에 액세스하기 위한 SSH 공개 키입니다.) 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![서비스 주체 매개 변수 전달](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="2510e-135">`--parameters`를 사용하여 azuredeploy.parameters.json 파일의 경로를 설정하는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="2510e-136">이 명령은 미국 서부 지역에서 `myResourceGroup`이라고 만든 리소스 그룹의 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="2510e-137">옵션 2: `az acs create`를 사용하여 클러스터를 만들 때 서비스 주체 생성</span><span class="sxs-lookup"><span data-stu-id="2510e-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="2510e-138">[`az acs create`](/cli/azure/acs#create) 명령을 실행하여 Kubernetes 클러스터를 만드는 경우 자동으로 서비스 주체를 생성하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="2510e-139">다른 Kubernetes 클러스터 만들기 옵션과 마찬가지로 `az acs create`를 실행할 때 기존 서비스 주체에 대한 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="2510e-140">그러나 이러한 매개 변수를 생략하면 Container Service에서 사용할 수 있도록 Azure CLI에서 하나의 서비스 주체를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="2510e-141">이는 배포 중에 투명하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="2510e-142">다음 명령은 Kubernetes 클러스터를 만들고 SSH 키와 서비스 주체 자격 증명을 모두 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="2510e-143">계정에 Azure AD 및 서비스 주체를 만들 수 있는 구독 권한이 없는 경우 명령은 `Insufficient privileges to complete the operation.`과 비슷한 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="2510e-144">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2510e-144">Additional considerations</span></span>

* <span data-ttu-id="2510e-145">구독에 서비스 주체를 만들 수 있는 권한이 없는 경우 Azure AD 또는 구독 관리자에게 필요한 권한을 할당하도록 요청하거나 Azure Container Service에서 사용할 서비스 주체를 요청해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="2510e-146">Kubernetes에 대한 서비스 주체는 클러스터 구성의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="2510e-147">그러나 클러스터를 배포하는 데에는 이 ID를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2510e-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="2510e-148">모든 서비스 주체는 Azure AD 응용 프로그램과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="2510e-149">Kubernetes 클러스터에 대한 서비스 주체는 유효한 모든 Azure AD 응용 프로그램 이름(예: `https://www.contoso.org/example`)과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="2510e-150">응용 프로그램에 대한 URL은 실제 끝점일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="2510e-151">서비스 주체 **클라이언트 ID**를 지정하는 경우 `appId`(이 문서에서 표시한 대로) 또는 해당되는 `name` 서비스 주체(예: `https://www.contoso.org/example`)의 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="2510e-152">Kubernetes 클러스터의 마스터 및 에이전트 VM에서 서비스 주체 자격 증명은 /etc/kubernetes/azure.json 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="2510e-153">`az acs create` 명령을 사용하여 서비스 주체를 자동으로 생성하는 경우 서비스 주체 자격 증명은 명령을 실행하는 데 사용되는 컴퓨터의 ~/.azure/acsServicePrincipal.json 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="2510e-154">`az acs create` 명령을 사용하여 자동으로 서비스 주체를 생성하는 경우 서비스 주체는 동일한 구독에서 만들어진 [Azure 컨테이너 레지스트리](../../container-registry/container-registry-intro.md)를 사용하여 인증할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2510e-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="2510e-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2510e-155">Next steps</span></span>

* <span data-ttu-id="2510e-156">컨테이너 서비스 클러스터에서 [Kubernetes를 시작합니다](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2510e-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="2510e-157">Kubernetes에 대한 서비스 주체 문제를 해결하려면 [ACS 엔진 설명서](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2510e-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


