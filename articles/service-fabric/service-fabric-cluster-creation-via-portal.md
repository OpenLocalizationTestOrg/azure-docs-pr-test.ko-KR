---
title: "Azure Portal에서 Service Fabric 만들기 | Microsoft Docs"
description: "이 문서에서는 Azure 포털 및 Azure 주요 자격 증명 모음을 사용하여 Azure에 보안 서비스 패브릭 클러스터를 설정하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="8a1db-103">Azure 포털을 사용하여 Azure에서 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1db-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a1db-104">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8a1db-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="8a1db-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8a1db-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="8a1db-106">Azure 포털을 사용하여 Azure에 보안 서비스 패브릭 클러스터를 설정하는 단계를 안내하는 단계별 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="8a1db-107">이 가이드에서는 다음 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="8a1db-108">클러스터 보안에 대한 키를 관리할 주요 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="8a1db-109">Azure 포털을 통해 Azure에서 보안 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="8a1db-110">인증서를 사용하여 관리자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="8a1db-111">Azure Active Directory를 사용한 사용자 인증 및 응용 프로그램 보안에 대한 인증서 설정 등의 고급 보안 옵션을 사용하려면 [Azure Resource Manager를 사용하여 클러스터를 만듭니다][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="8a1db-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="8a1db-112">보안 클러스터란 응용 프로그램, 서비스 및 포함된 데이터를 배포, 업그레이드 및 삭제하는 관리 작업에 무단 액세스하는 것을 방지하는 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="8a1db-113">비보안 클러스터란 언제라도 누구든지 연결하여 관리 작업을 수행할 수 있는 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="8a1db-114">비보안 클러스터를 만드는 것이 가능하지만 **보안 클러스터를 만드는 것이 좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="8a1db-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="8a1db-115">비보안 클러스터는 **나중를 보안될 수 없습니다** -새 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="8a1db-116">Linux 또는 Windows 클러스터인지 여부에 관계없이 보안 클러스터 만들기에 대한 개념은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="8a1db-117">자세한 내용 및 보안 Linux 클러스터 만들기를 위한 도우미 스크립트는 [Linux에서 보안 클러스터 만들기](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="8a1db-118">제공된 도우미 스크립트에서 얻은 매개 변수는 [Azure 포털에서 클러스터 만들기](#create-cluster-portal)섹션에 설명된 대로 포털에 직접 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="8a1db-119">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="8a1db-119">Log in to Azure</span></span>
<span data-ttu-id="8a1db-120">이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="8a1db-121">새로 PowerShell 세션을 시작하려면 Azure 계정에 로그인한 후 Azure 명령을 실행하기 전에 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="8a1db-122">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8a1db-123">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="8a1db-124">주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="8a1db-124">Set up Key Vault</span></span>
<span data-ttu-id="8a1db-125">가이드의 이 부분에서는 Azure에서 서비스 패브릭 클러스터에 대해서와 서비스 패브릭 응용 프로그램에 대해서 주요 자격 증명 모음을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="8a1db-126">Key Vault에 대한 완전한 가이드는 [Key Vault 시작 가이드][key-vault-get-started]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="8a1db-127">서비스 패브릭은 X.509 인증서를 사용하여 클러스터에 보안을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="8a1db-128">Azure 주요 자격 증명 모음은 Azure에서 서비스 패브릭 클러스터에 대한 인증서를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="8a1db-129">클러스터를 Azure에 배포할 때 서비스 패브릭 클러스터 생성을 담당하는 Azure 리소스 공급자는 주요 자격 증명 모음에서 인증서를 가져와 클러스터 VM에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="8a1db-130">다음 다이어그램은 주요 자격 증명 모음, 서비스 패브릭 클러스터 및 클러스터를 만들 때 주요 자격 증명 모음에 저장된 인증서를 사용하는 Azure 리소스 공급자 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![인증서 설치][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="8a1db-132">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1db-132">Create a Resource Group</span></span>
<span data-ttu-id="8a1db-133">첫 번째 단계는 특히 주요 자격 증명 모음에 대한 새로운 리소스 그룹을 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="8a1db-134">주요 자격 증명 모음을 자체 리소스 그룹에 두어 키 및 암호는 유실하지 않고 서비스 패브릭 클러스터가 있는 리소스 그룹과 같은 계산 및 저장소 리소스 그룹을 제거하도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="8a1db-135">사용자의 주요 자격 증명 모음을 가진 리소스 그룹은 그것을 사용 중인 클러스터와 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="8a1db-136">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1db-136">Create Key Vault</span></span>
<span data-ttu-id="8a1db-137">새 리소스 그룹에 주요 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="8a1db-138">서비스 패브릭 리소스 공급자가 인증서를 가져와 클러스터 노드에 설치하도록 허용하기 위해 주요 자격 증명 모음을 **배포에 대해 사용하도록 설정해야 합니다** .</span><span class="sxs-lookup"><span data-stu-id="8a1db-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="8a1db-139">기존 주요 자격 증명 모음이 있는 경우라면 Azure CLI를 사용하여 배포에 대해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="8a1db-140">주요 자격 증명 모음에 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="8a1db-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="8a1db-141">인증서는 서비스 패브릭에서 클러스터 및 해당 응용 프로그램의 다양한 측면을 보호하기 위해 인증 및 암호화를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="8a1db-142">Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오][service-fabric-cluster-security]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="8a1db-143">클러스터 및 서버 인증서(필수)</span><span class="sxs-lookup"><span data-stu-id="8a1db-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="8a1db-144">이 인증서는 클러스터를 보호하고 무단 액세스를 방지하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="8a1db-145">다음 몇 가지 방법으로 클러스터 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="8a1db-146">**클러스터 인증:** 클러스터 페더레이션에 대한 노드 간 통신을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="8a1db-147">이 인증서로 자신의 신분을 증명할 수 있는 노드만 클러스터에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="8a1db-148">**서버 인증:** 관리 클라이언트에 클러스터 관리 끝점을 인증하여 관리 클라이언트기 실제 클러스터와 통신하는지 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="8a1db-149">이 인증서는 HTTPS 관리 API 및 HTTPS를 통한 Service Fabric Explorer에 대해 SSL도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="8a1db-150">이를 위해 인증서는 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="8a1db-151">인증서에 개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="8a1db-152">개인 정보 교환(.pfx) 파일로 내보낼 수 있는 키 교환용 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="8a1db-153">인증서의 주체 이름은 서비스 패브릭 클러스터 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="8a1db-154">클러스터의 HTTPS 관리 끝점 및 Service Fabric Explorer에 대해 SSL을 제공하려면 이러한 조건이 충족되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="8a1db-155">`.cloudapp.azure.com` 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="8a1db-156">클러스터에 대한 사용자 지정 도메인 이름을 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="8a1db-157">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 클러스터에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="8a1db-158">클라이언트 인증 인증서</span><span class="sxs-lookup"><span data-stu-id="8a1db-158">Client authentication certificates</span></span>
<span data-ttu-id="8a1db-159">추가 클라이언트 인증서가 클러스터 관리 작업을 위해 관리자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="8a1db-160">서비스 패브릭은 **관리자** 및 **읽기 전용 사용자**의 두 가지 액세스 수준을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="8a1db-161">최소한 관리 액세스에 대해 단일 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="8a1db-162">추가 사용자 수준 액세스를 위해서는 별도 인증서를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="8a1db-163">액세스 역할에 대한 자세한 내용은 [Service Fabric 클라이언트의 역할 기반 액세스 제어][service-fabric-cluster-security-roles]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="8a1db-164">Service Fabric을 사용하기 위해 클라이언트 인증 인증서를 Key Vault에 업로드할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="8a1db-165">이러한 인증서는 클러스터 관리 권한이 있는 사용자에게 제공하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="8a1db-166">Azure Active Directory는 클러스터의 관리 작업을 위해 클라이언트를 인증하기 위한 권장 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="8a1db-167">Azure Active Directory를 사용하려면 [Azure Resource Manager를 사용하여 클러스터를 만들어야][create-cluster-arm] 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="8a1db-168">응용 프로그램 인증서(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8a1db-168">Application certificates (optional)</span></span>
<span data-ttu-id="8a1db-169">응용 프로그램 보안을 위해 클러스터에 제한 없는 수의 인증서를 추가로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="8a1db-170">클러스터를 만들기 전에, 다음과 같이 노드에 인증서를 설치하도록 요구하는 응용 프로그램 보안 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="8a1db-171">응용 프로그램 구성 값의 암호화 및 암호 해독</span><span class="sxs-lookup"><span data-stu-id="8a1db-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="8a1db-172">복제 중에 노드 간 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="8a1db-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="8a1db-173">Azure 포털을 통해 클러스터를 만들 때 응용 프로그램 인증서를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="8a1db-174">클러스터 설치 시에 응용 프로그램 인증서를 구성하려면 [Azure Resource Manager를 사용하여 클러스터를 만들어야][create-cluster-arm] 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="8a1db-175">만든 클러스터에 응용 프로그램 인증서를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="8a1db-176">Azure 리소스 공급자 사용을 위한 인증서 서식 지정</span><span class="sxs-lookup"><span data-stu-id="8a1db-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="8a1db-177">개인 키 파일(.pfx)을 추가하고 주요 자격 증명 모음을 통해 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="8a1db-178">그렇지만 Azure 리소스 공급자에서는 .pfx를 base-64로 인코딩된 문자열 상태로 포함하고 개인 키 암호를 포함하는 특수한 JSON 형식으로 키를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="8a1db-179">이러한 요구를 수용하기 위해 키를 JSON 문자열에 배치한 후 주요 자격 증명 모음에 *암호* 로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="8a1db-180">이 프로세스를 보다 쉽게 수행할 수 있도록 하기 위해 PowerShell 모듈이 [GitHub에서 사용할 수 있게 제공됩니다][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="8a1db-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="8a1db-181">모듈을 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="8a1db-182">리포지토리의 전체 콘텐츠를 로컬 디렉터리에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="8a1db-183">PowerShell 창으로 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="8a1db-184">이 PowerShell 모듈의 `Invoke-AddCertToKeyVault` 명령은 자동으로 인증서 개인 키 서식을 JSON 문자열에 지정하고 주요 자격 증명 모음에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="8a1db-185">이를 사용하여 클러스터 인증서 및 추가 응용 프로그램 인증서를 주요 자격 증명 모음에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="8a1db-186">클러스터에 설치하려는 모든 추가 인증서에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="8a1db-187">노드 인증, 관리 끝점 보안 및 인증, X.509 인증서를 사용하는 모든 추가 응용 프로그램 보안 기능에 대한 인증서를 설치하는 서비스 패브릭 클러스터 Resource Manager 템플릿을 구성하기 위해 주요 자격 증명 모음에 대해 이러한 작업이 선행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="8a1db-188">이제 Azure에는 다음과 같은 설정이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="8a1db-189">주요 자격 증명 모음 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="8a1db-189">Key Vault resource group</span></span>
  * <span data-ttu-id="8a1db-190">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="8a1db-190">Key Vault</span></span>
    * <span data-ttu-id="8a1db-191">클러스터 서버 인증 인증서</span><span class="sxs-lookup"><span data-stu-id="8a1db-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="8a1db-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="8a1db-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="8a1db-193">Azure 포털에서 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1db-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="8a1db-194">서비스 패브릭 클러스터 리소스 검색</span><span class="sxs-lookup"><span data-stu-id="8a1db-194">Search for the Service Fabric cluster resource</span></span>
![Azure 포털에서 서비스 패브릭 클러스터 템플릿을 검색합니다.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="8a1db-196">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="8a1db-197">**새로 만들기** 를 클릭하여 새 리소스 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="8a1db-198">**마켓플레이스**의 **모두**에서 Service Fabric 클러스터 템플릿을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="8a1db-199">목록에서 **서비스 패브릭 클러스터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="8a1db-200">**Service Fabric 클러스터** 블레이드로 이동하여 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="8a1db-201">**Service Fabric 클러스터 만들기** 블레이드는 다음 4단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="8a1db-202">1. 기본 사항</span><span class="sxs-lookup"><span data-stu-id="8a1db-202">1. Basics</span></span>
![새 리소스 그룹 만들기 스크린샷][CreateRG]

<span data-ttu-id="8a1db-204">기본 사항 블레이드에서는 클러스터에 대한 기본 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="8a1db-205">클러스터 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="8a1db-206">VM용 원격 데스크톱의 **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="8a1db-207">클러스터가 배포될 **구독**을 선택합니다. 특히 구독이 여러 개인 경우 반드시 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="8a1db-208">**새 리소스 그룹**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-208">Create a **new resource group**.</span></span> <span data-ttu-id="8a1db-209">클러스터 이름과 같은 이름을 사용하면 나중에 쉽게 찾을 수 있으며 특히 배포를 변경하거나 클러스터를 삭제하려고 할 때 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a1db-210">기존 리소스 그룹을 사용해도 되지만 새 리소스 그룹을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="8a1db-211">이렇게 하면 필요하지 않은 클러스터를 쉽게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="8a1db-212">클러스터를 만들려는 **지역** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="8a1db-213">주요 자격 증명 모음이 있는 동일한 지역을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="8a1db-214">2. 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="8a1db-214">2. Cluster configuration</span></span>
![노드 형식 만들기][CreateNodeType]

<span data-ttu-id="8a1db-216">클러스터 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-216">Configure your cluster nodes.</span></span> <span data-ttu-id="8a1db-217">노드 유형에서 VM 크기, VM 수 및 VM 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="8a1db-218">클러스터는 둘 이상의 노드 형식을 가질 수 있지만 주 노드 형식(포털에서 정의하는 첫 번째 노드)에는 최소한 5개의 VM이 있어야 하며, 서비스 패브릭 시스템 서비스가 배치된 노드 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="8a1db-219">"NodeTypeName"의 기본 배치 속성은 자동으로 추가되므로 **배치 속성** 을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="8a1db-220">여러 노드 형식 사용에 대한 일반적인 시나리오는 프런트 엔드 서비스 및 백 엔드 서비스를 포함하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="8a1db-221">인터넷에 열려 있는 포트를 포함하고 비교적 작은 VM(D2 같은 VM 크기)에 프런트 엔드 서비스를 배치하고, 열려 있는 인터넷 연결 포트가 없고 비교적 큰 VM(D4, D6, D15 등과 같은 VM 크기)에 백 엔드 서비스를 배치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="8a1db-222">노드 유형에 대한 이름(문자와 숫자만을 포함하는 1~12자)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="8a1db-223">주 노드 형식에 대한 최소 VM **크기**는 클러스터에 대해 선택한 **내구성** 계층에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="8a1db-224">내구성 계층에 대한 기본값은 브론즈입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="8a1db-225">내구성에 대한 자세한 내용은 [Service Fabric 클러스터 안정성 및 내구성 선택 방법][service-fabric-cluster-capacity]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="8a1db-226">VM 크기 및 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="8a1db-227">D 시리즈 VM에는 SSD 드라이브가 있으므로 특히 상태 저장 응용 프로그램에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="8a1db-228">부분 코어가 있거나 사용 가능한 디스크 용량이 7GB 미만인 VM SKU를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="8a1db-229">주 노드 형식에 대한 최소 VM **수**는 선택한 **안정성** 계층에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="8a1db-230">안정성 계층에 대한 기본값은 실버입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="8a1db-231">안정성에 대한 자세한 내용은 [Service Fabric 클러스터 안정성 및 내구성 선택 방법][service-fabric-cluster-capacity]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="8a1db-232">노드 유형에 대한 VM 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="8a1db-233">나중에 노드 형식의 VM 수를 늘리거나 줄일 수 있지만 주 노드 형식에서는 선택한 안정성 수준에 따라 최소 개수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="8a1db-234">다른 노드 유형은 VM이 1대만 있어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="8a1db-235">사용자 지정 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-235">Configure custom endpoints.</span></span> <span data-ttu-id="8a1db-236">이 필드를 사용하면 Azure Load Balancer를 통해 응용 프로그램에 대한 공용 인터넷에 노출하려고 하는 쉼표로 구분된 포트 목록을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="8a1db-237">예를 들어 클러스터에 웹 응용 프로그램을 배포하려는 경우 여기에 "80"을 입력하여 포트 80의 트래픽이 클러스터로 이동되도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="8a1db-238">끝점에 대한 자세한 내용은 [응용 프로그램과 통신][service-fabric-connect-and-communicate-with-services]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="8a1db-239">클러스터 **진단**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="8a1db-240">기본적으로 문제 해결을 돕기 위해 클러스터에서 진단이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="8a1db-241">진단을 사용하지 않으려면 **상태** 토글을 **사용 안 함**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="8a1db-242">진단을 끄지 **않는** 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="8a1db-243">클러스터를 설정할 패브릭 업그레이드 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="8a1db-244">시스템이 사용 가능한 최신 버전을 자동으로 선택하고 클러스터를 최신 버전으로 업그레이드하도록 하려면 **자동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="8a1db-245">지원되는 버전을 선택하려는 경우 모드를 **수동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="8a1db-246">지원되는 버전의 Service Fabric이 실행되는 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="8a1db-247">**수동** 모드를 선택하면 사용자가 직접 클러스터를 지원되는 버전으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="8a1db-248">패브릭 업그레이드 모드에 대한 자세한 내용은 [service-fabric-cluster-upgrade 문서][service-fabric-cluster-upgrade]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="8a1db-249">3. 보안</span><span class="sxs-lookup"><span data-stu-id="8a1db-249">3. Security</span></span>
![Azure 포털의 보안 구성 스크린샷][SecurityConfigs]

<span data-ttu-id="8a1db-251">최종 단계는 앞서 생성된 주요 자격 증명 모음 및 인증서 정보를 사용하여 클러스터를 보호할 수 있도록 인증서 정보를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="8a1db-252">`Invoke-AddCertToKeyVault` PowerShell 명령을 사용하여 주요 자격 증명 모음에 **클러스터 인증서**를 업로드하여 획득한 출력으로 기본 인증서 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="8a1db-253">**고급 설정 구성** 확인란을 선택하여 **관리 클라이언트** 및 **읽기 전용 클라이언트**에 대한 클라이언트 인증서를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="8a1db-254">이러한 필드에는 관리 클라이언트 인증서의 지문과 읽기 전용 사용자 클라이언트 인증서의 지문을 입력하면 됩니다(해당하는 경우).</span><span class="sxs-lookup"><span data-stu-id="8a1db-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="8a1db-255">관리자가 클러스터에 연결하려고 할 경우, 여기에 입력한 지문 값과 일치하는 지문을 포함하는 인증서가 있어야만 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="8a1db-256">4. 요약</span><span class="sxs-lookup"><span data-stu-id="8a1db-256">4. Summary</span></span>
![<span data-ttu-id="8a1db-257">“배포 서비스 패브릭 클러스터”를 표시하는 시작 보드 스크린샷</span><span class="sxs-lookup"><span data-stu-id="8a1db-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="8a1db-258">클러스터 만들기를 완료하려면 **요약** 을 클릭하여 제공된 구성을 참조하거나 클러스터를 배포하는 데 사용할 Azure Resource Manager 템플릿을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="8a1db-259">필수 설정을 입력하면 **확인** 단추가 녹색이 되고 이를 클릭하여 클러스터 만들기 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="8a1db-260">알림에서 만들기 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="8a1db-261">(화면 오른쪽 위의 상태 표시줄 근처에 있는 "종" 모양 아이콘을 클릭합니다.) 클러스터를 만드는 동안 **시작 보드에 고정**을 클릭하면 **Service Fabric 클러스터 배포 중**이 **시작** 보드에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="8a1db-262">클러스터 상태 보기</span><span class="sxs-lookup"><span data-stu-id="8a1db-262">View your cluster status</span></span>
![대시보드의 클러스터 세부 정보 스크린샷][ClusterDashboard]

<span data-ttu-id="8a1db-264">클러스터를 만들면 포털에서 클러스터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="8a1db-265">**찾아보기**로 이동하고 **Service Fabric 클러스터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="8a1db-266">클러스터를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="8a1db-267">이제 대시보드에서 클러스터의 공용 끝점 및 Service Fabric Explorer에 대한 링크를 포함한 클러스터 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="8a1db-268">클러스터 대시보드 블레이드의 **노드 모니터** 섹션에 정상 및 비정상 상태인 VM 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="8a1db-269">클러스터 상태에 대한 자세한 내용은 [Service Fabric 상태 모델 소개][service-fabric-health-introduction]에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="8a1db-270">가용성을 유지하고 상태를 보존하기 위해 Service Fabric 클러스터에서 특정 수의 노드가 항상 작동 상태를 유지해야 하며, 이 숫자를 "유지 관리 쿼럼"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="8a1db-271">따라서 [상태 전체 백업][service-fabric-reliable-services-backup-restore]을 처음으로 수행하는 경우 외에는 일반적으로 클러스터의 모든 컴퓨터를 종료하는 것은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="8a1db-272">가상 컴퓨터 확장 집합 인스턴스 또는 클러스터 노드에 원격 연결</span><span class="sxs-lookup"><span data-stu-id="8a1db-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="8a1db-273">클러스터에서 지정한 각 NodeType에 따라 가상 컴퓨터 확장 집합이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="8a1db-274">자세한 내용은 [가상 컴퓨터 확장 집합 인스턴스 또는 클러스터 노드에 원격 연결][remote-connect-to-a-vm-scale-set]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1db-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a1db-275">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a1db-275">Next steps</span></span>
<span data-ttu-id="8a1db-276">이제 관리 인증을 위해 인증서를 사용하는 보안 클러스터가 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="8a1db-277">다음으로, [클러스터에 연결](service-fabric-connect-to-secure-cluster.md)하고 [응용 프로그램 암호를 관리](service-fabric-application-secret-management.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="8a1db-278">또한 [Service Fabric 지원 옵션](service-fabric-support.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a1db-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
