---
title: "템플릿에서 Azure Service Fabric 클러스터 만들기 | Microsoft Docs"
description: "이 문서에서는 클라이언트 인증에 Azure Resource Manager, Azure Key Vault, Azure Active Directory(Azure AD)를 사용하여 Azure에 보안 Service Fabric 클러스터를 설정하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="b2386-103">Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2386-104">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b2386-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="b2386-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b2386-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="b2386-106">Azure Resource Manager를 사용하여 Azure에 보안 Azure Service Fabric 클러스터를 설정하는 단계를 안내하는 단계별 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="b2386-107">이 문서는 깁니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="b2386-108">그렇지만 아직 이 내용에 익숙하지 않다면 각 단계를 세심히 따라보시기 바랍니다. </span><span class="sxs-lookup"><span data-stu-id="b2386-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="b2386-109">이 가이드에서는 다음 절차를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="b2386-110">클러스터 및 응용 프로그램 보안을 위한 인증서 업로드를 위해 Azure Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="b2386-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="b2386-111">Azure Resource Manager를 사용하여 Azure에 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="b2386-112">클러스터 관리를 위해 Azure Active Directory(Azure AD)를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="b2386-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="b2386-113">보안 클러스터는 관리 작업에 대한 무단 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="b2386-114">여기에는 응용 프로그램, 서비스 및 포함된 데이터의 배포, 업그레이드 및 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="b2386-115">비보안 클러스터란 언제라도 누구든지 연결하여 관리 작업을 수행할 수 있는 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="b2386-116">비보안 클러스터를 만들 수도 있지만 처음부터 보안 클러스터를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="b2386-117">비보안 클러스터는 나중에 보안 클러스터로 만들 수 없으므로 새 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="b2386-118">Linux나 Windows 클러스터 모두 보안 클러스터를 만드는 개념은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="b2386-119">자세한 내용 및 보안 Linux 클러스터 만들기를 위한 도우미 스크립트는 [Linux에서 보안 클러스터 만들기](#secure-linux-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="b2386-120">Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="b2386-120">Sign in to your Azure account</span></span>
<span data-ttu-id="b2386-121">이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="b2386-122">새로 PowerShell 세션을 시작하려면 Azure 계정에 로그인한 후 Azure 명령을 실행하기 전에 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="b2386-123">Azure 계정 로그인:</span><span class="sxs-lookup"><span data-stu-id="b2386-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b2386-124">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="b2386-125">Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="b2386-125">Set up a key vault</span></span>
<span data-ttu-id="b2386-126">이 섹션에서는 Azure에서 Service Fabric 클러스터에 대해서와 Service Fabric 응용 프로그램에 대해서 Key Vault를 만드는 단계를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="b2386-127">Azure Key Vault에 대한 완전한 가이드는 [Key Vault 시작 가이드][key-vault-get-started]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="b2386-128">서비스 패브릭은 클러스터에 보안 적용을 하고 응용 프로그램 보안 기능을 제공하기 위해 X.509 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="b2386-129">Key Vault는 Azure에서 Service Fabric 클러스터에 대한 인증서를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="b2386-130">클러스터를 Azure에 배포할 때 Service Fabric 클러스터 생성을 담당하는 Azure 리소스 공급자는 Key Vault에서 인증서를 가져와 클러스터 VM에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="b2386-131">다음 다이어그램은 Azure Key Vault, Service Fabric 클러스터 및 클러스터를 만들 때 Key Vault에 저장된 인증서를 사용하는 Azure 리소스 공급자 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![인증서 설치 다이어그램][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="b2386-133">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-133">Create a resource group</span></span>
<span data-ttu-id="b2386-134">첫 번째 단계는 Key Vault 전용 리소스 그룹을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="b2386-135">Key Vault를 자체 리소스 그룹에 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="b2386-136">이렇게 하면 키 및 암호는 유실하지 않고 Service Fabric 클러스터가 있는 리소스 그룹과 같은 계산 및 저장소 리소스 그룹을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="b2386-137">사용자 Key Vault를 포함하는 리소스 그룹은 해당 그룹을 사용하는 클러스터와 _동일한 지역에 있어야_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="b2386-138">여러 지역에 클러스터를 배포하려는 경우 리소스 그룹과 Key Vault를 해당 항목이 속한 지역을 표시하는 방식으로 명명하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="b2386-139">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="b2386-140">새 리소스 그룹에 Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="b2386-141">연산 리소스 공급자가 인증서를 가져와 가상 컴퓨터 인스턴스에 설치할 수 있도록 Key Vault를 _배포에 대해 사용하도록 설정해야 합니다_.</span><span class="sxs-lookup"><span data-stu-id="b2386-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="b2386-142">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-142">The output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="b2386-143">기존 Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="b2386-143">Use an existing key vault</span></span>

<span data-ttu-id="b2386-144">기존 Key Vault를 사용하려면 연산 리소스 공급자가 인증서를 가져와 클러스터 노드에 설치할 수 있도록 Key Vault를 _배포에 대해 사용하도록 설정해야 합니다_.</span><span class="sxs-lookup"><span data-stu-id="b2386-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="b2386-145">Key Vault에 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="b2386-145">Add certificates to your key vault</span></span>

<span data-ttu-id="b2386-146">인증서는 서비스 패브릭에서 클러스터 및 해당 응용 프로그램의 다양한 측면을 보호하기 위해 인증 및 암호화를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="b2386-147">Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오][service-fabric-cluster-security]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="b2386-148">클러스터 및 서버 인증서(필수)</span><span class="sxs-lookup"><span data-stu-id="b2386-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="b2386-149">이 인증서는 클러스터를 보호하고 무단 액세스를 방지하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="b2386-150">다음 두 방법으로 클러스터 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="b2386-151">클러스터 인증: 클러스터 페더레이션을 위해 노드 간 통신을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="b2386-152">이 인증서로 자신의 신분을 증명할 수 있는 노드만 클러스터에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="b2386-153">서버 인증: 관리 클라이언트에 클러스터 관리 끝점을 인증하여 관리 클라이언트기 실제 클러스터와 통신하는지 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="b2386-154">이 인증은 HTTPS 관리 API 및 HTTPS를 통한 Service Fabric Explorer용 SSL도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="b2386-155">이를 위해 인증서는 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="b2386-156">인증서에 개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="b2386-157">키 교환을 위해 인증서를 만들어야 합니다. 이 인증서는 개인 정보 교환(.pfx) 파일로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="b2386-158">인증서의 주체 이름은 Service Fabric 클러스터 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="b2386-159">클러스터의 HTTPS 관리 끝점 및 Service Fabric Explorer에 대해 SSL을 제공하려면 이렇게 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b2386-160">.cloudapp.azure.com 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다. </span><span class="sxs-lookup"><span data-stu-id="b2386-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="b2386-161">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b2386-162">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 클러스터에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="b2386-163">응용 프로그램 인증서(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2386-163">Application certificates (optional)</span></span>
<span data-ttu-id="b2386-164">응용 프로그램 보안을 위해 클러스터에 제한 없는 수의 인증서를 추가로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="b2386-165">클러스터를 만들기 전에, 다음과 같이 노드에 인증서를 설치하도록 요구하는 응용 프로그램 보안 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="b2386-166">응용 프로그램 구성 값의 암호화 및 암호 해독</span><span class="sxs-lookup"><span data-stu-id="b2386-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="b2386-167">복제 중에 노드 간 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="b2386-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="b2386-168">Azure 리소스 공급자 사용을 위한 인증서 서식 지정</span><span class="sxs-lookup"><span data-stu-id="b2386-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="b2386-169">Key Vault를 통해 개인 키 파일(.pfx)을 직접 추가하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="b2386-170">그러나 Azure 계산 리소스 공급자에는 특수 JSON(JavaScript Object Notation) 형식으로 저장된 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="b2386-171">이 형식에는 기본 64 인코딩 문자열형태의 .pfx 파일과 개인 키 암호가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="b2386-172">이러한 요구를 수용하기 위해 키를 JSON 문자열에 배치한 후 Key Vault에 “암호”로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="b2386-173">이 프로세스를 보다 쉽게 수행할 수 있도록 하기 위해 PowerShell 모듈이 [GitHub에서 사용할 수 있게 제공됩니다][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="b2386-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="b2386-174">모듈을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="b2386-175">리포지토리의 전체 콘텐츠를 로컬 디렉터리에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="b2386-176">로컬 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-176">Go to the local directory.</span></span>
2. <span data-ttu-id="b2386-177">PowerShell 창에서 ServiceFabricRPHelpers 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="b2386-178">이 PowerShell 모듈의 `Invoke-AddCertToKeyVault` 명령은 자동으로 인증서 개인 키 서식을 JSON 문자열에 지정하고 Key Vault에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="b2386-179">이 명령을 사용하여 클러스터 인증서 및 추가 응용 프로그램 인증서를 Key Vault에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="b2386-180">클러스터에 설치하려는 모든 추가 인증서에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="b2386-181">기존 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="b2386-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="b2386-182">아래와 같은 오류가 나타나면 보통은 리소스 URL 충돌을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="b2386-183">이 충돌을 해결하려면 Key Vault 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="b2386-184">충돌이 해결된 후의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="b2386-185">보안 Service Fabric 클러스터를 설정하고 응용 프로그램 보안에 사용할 수 있는 모든 응용 프로그램 인증서를 가져오려면 이전 세 문자열, CertificateThumbprint, SourceVault 및 CertificateURL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="b2386-186">이 문자열을 저장하지 않은 경우 나중에 Key Vault를 쿼리하여 검색하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="b2386-187">자체 서명된 인증서를 만들어 Key Vault에 업로드</span><span class="sxs-lookup"><span data-stu-id="b2386-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="b2386-188">이미 인증서를 Key Vault에 업로드한 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="b2386-189">이 단계는 새로운 자체 서명 인증서를 생성하여 Key Vault에 업로드하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="b2386-190">다음 스크립트의 매개 변수를 변경하여 실행한 다음에는 인증서 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="b2386-191">아래와 같은 오류가 나타나면 보통은 리소스 URL 충돌을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="b2386-192">이 충돌을 해결하려면 Key Vault 이름, RG 이름 등을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="b2386-193">충돌이 해결된 후의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="b2386-194">보안 Service Fabric 클러스터를 설정하고 응용 프로그램 보안에 사용할 수 있는 모든 응용 프로그램 인증서를 가져오려면 이전 세 문자열, CertificateThumbprint, SourceVault 및 CertificateURL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="b2386-195">이 문자열을 저장하지 않은 경우 나중에 Key Vault를 쿼리하여 검색하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="b2386-196">이 시점에 다음과 같은 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="b2386-197">Key Vault 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="b2386-197">The key vault resource group.</span></span>
* <span data-ttu-id="b2386-198">Key Vault 및 해당 URL(이전 PowerShell 출력의 SourceVault)</span><span class="sxs-lookup"><span data-stu-id="b2386-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="b2386-199">클러스터 서버 인증 인증서 및 Key Vault의 해당 URL</span><span class="sxs-lookup"><span data-stu-id="b2386-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="b2386-200">응용 프로그램 인증서 및 Key Vault의 해당 URL</span><span class="sxs-lookup"><span data-stu-id="b2386-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="b2386-201">클라이언트 인증에 대한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="b2386-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="b2386-202">조직(테넌트)에서는 Azure AD를 사용하여 응용 프로그램에 대한 사용자 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="b2386-203">응용 프로그램은 웹 기반 로그인 UI를 갖는 항목과 네이티브 클라이언트 환경을 갖는 항목으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="b2386-204">이 문서에서는 이미 테넌트를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="b2386-205">그러지 않은 경우 [Azure Active Directory 테넌트를 얻는 방법][active-directory-howto-tenant]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="b2386-206">Service Fabric 클러스터는 웹 기반 [Service Fabric Explorer][service-fabric-visualizing-your-cluster] 및 [Visual Studio][service-fabric-manage-application-in-visual-studio]를 포함하여 관리 기능에 대한 여러 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="b2386-207">결과적으로 두 개의 Azure AD 응용 프로그램(웹 응용 프로그램과 네이티브 응용 프로그램)을 만들어 클러스터에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="b2386-208">Service Fabric 클러스터로 Azure AD를 구성하는 데 포함되는 일부 단계를 단순화하기 위해 Windows PowerShell 스크립트 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="b2386-209">클러스터를 만들기 전에 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="b2386-210">스크립트는 클러스터 이름과 끈점을 예상하므로 이 값을 계획해야 하며, 이 값은 이미 만든 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="b2386-211">컴퓨터에 [스크립트를 다운로드][sf-aad-ps-script-download]합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="b2386-212">zip 파일을 마우스 오른쪽 단추로 클릭하고 **속성**, **차단 해제** 확인란을 차례로 선택한 다음 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="b2386-213">zip 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-213">Extract the zip file.</span></span>
4. <span data-ttu-id="b2386-214">`SetupApplications.ps1`을 실행하고 TenantId, ClusterName 및 WebApplicationReplyUrl을 매개 변수로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="b2386-215">예:</span><span class="sxs-lookup"><span data-stu-id="b2386-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="b2386-216">PowerShell 명령 `Get-AzureSubscription`을 실행하여 TenantId를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="b2386-217">이 명령을 실행하면 모든 구독에 대한 TenantId가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="b2386-218">ClusterName은 스크립트로 만든 Azure AD 응용 프로그램에 접두사를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="b2386-219">실제 클러스터 이름과 정확히 일치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="b2386-220">단순히 Azure AD 아티팩트를, 함께 사용할 Service Fabric 패브릭 클러스터에 쉽게 매핑하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="b2386-221">WebApplicationReplyUrl은 로그인을 마친 후 Azure AD가 사용자를 돌려보낼 기본 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="b2386-222">이 끝점을 기본적으로 다음과 같은 클러스터에 대한 Service Fabric Explorer 끝점으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="b2386-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="b2386-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="b2386-224">Azure AD 테넌트에 대한 관리자 권한이 있는 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="b2386-225">로그인한 후에는 스크립트가 Service Fabric 클러스터를 나타내는 웹 및 네이티브 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="b2386-226">[Azure 클래식 포털][azure-classic-portal]에서 테넌트의 응용 프로그램을 보면 두 개의 새 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="b2386-227">*ClusterName*\_클러스터</span><span class="sxs-lookup"><span data-stu-id="b2386-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="b2386-228">*ClusterName*\_클라이언트</span><span class="sxs-lookup"><span data-stu-id="b2386-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="b2386-229">다음 섹션에서 클러스터를 만들 때 스크립트는 Azure Resource Manager 템플릿에서 필요한 JSON을 인쇄하므로 PowerShell 창을 계속 열어 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="b2386-230">서비스 패브릭 클러스터 Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="b2386-231">이 섹션에서는 이전 PowerShell 명령의 출력이 Service Fabric Cluster Resource Manager 템플릿에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="b2386-232">샘플 Resource Manager 템플릿은 [GitHub의 Azure 빠른 시작 템플릿 갤러리][azure-quickstart-templates]에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="b2386-233">이러한 템플릿은 클러스터 템플릿의 시작점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="b2386-234">리소스 관리자 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-234">Create the Resource Manager template</span></span>
<span data-ttu-id="b2386-235">이 가이드에서는 [5 노드 보안 클러스터][service-fabric-secure-cluster-5-node-1-nodetype] 예제 템플릿과 템플릿 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="b2386-236">`azuredeploy.json`와 `azuredeploy.parameters.json`을 컴퓨터에 다운로드하고 선호하는 텍스트 편집기로 두 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="b2386-237">인증서 추가</span><span class="sxs-lookup"><span data-stu-id="b2386-237">Add certificates</span></span>
<span data-ttu-id="b2386-238">인증서 키를 포함하는 Key Vault 참조하여 Cluster Resource Manager 템플릿에 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="b2386-239">Resource Manager 템플릿 파일에 Key Vault 값을 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="b2386-240">이렇게 하면 Resource Manager 템플릿을 계속 재사용할 수 있고 배포에 특정한 값이 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="b2386-241">가상 컴퓨터 확장 집합 osProfile에 모든 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="b2386-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="b2386-242">클러스터에 설치된 모든 인증서는 확장 집합 리소스(Microsoft.Compute/virtualMachineScaleSets)의 osProfile 섹션에 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="b2386-243">이 작업은 리소스 공급자에게 인증서를 VM에 설치하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="b2386-244">이 설치에는 클러스터 인증서와, 응용 프로그램에 사용하려는 모든 응용 프로그램 보안 인증서가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="b2386-245">Service Fabric 클러스터 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="b2386-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="b2386-246">또한 클러스터 인증 인증서는 서비스 패브릭 클러스터 리소스(Microsoft.ServiceFabric/clusters)와, 가상 컴퓨터 확장 집합 리소스의 가상 컴퓨터 확장 집합에 대해 Service Fabric 확장에서 모두 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="b2386-247">이렇게 해야 Service Fabric 리소스 공급자는 클러스터 인증에 대한 사용 및 관리 끝점에 대한 서버 인증을 위해 그것을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="b2386-248">가상 컴퓨터 확장 집합 리소스:</span><span class="sxs-lookup"><span data-stu-id="b2386-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="b2386-249">서비스 패브릭 리소스:</span><span class="sxs-lookup"><span data-stu-id="b2386-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="b2386-250">Azure AD 구성 삽입</span><span class="sxs-lookup"><span data-stu-id="b2386-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="b2386-251">이전에 만든 Azure AD 구성을 Resource Manager 템플릿에 직접 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="b2386-252">그러나 Resource Manager 템플릿을 계속 재사용하고 배포에 특정한 값이 없도록 하기 위해 먼저 값을 매개 변수 파일에 추출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="b2386-253"><a "configure-arm" ></a>Resource Manager 템플릿 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="b2386-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="b2386-254">마지막으로, Key Vault 및 Azure AD PowerShell 명령의 출력 값을 매개 변수 파일을 채우는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="b2386-255">이 시점에 다음과 같은 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="b2386-256">Key Vault 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="b2386-256">Key vault resource group</span></span>
  * <span data-ttu-id="b2386-257">주요 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="b2386-257">Key vault</span></span>
  * <span data-ttu-id="b2386-258">클러스터 서버 인증 인증서</span><span class="sxs-lookup"><span data-stu-id="b2386-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="b2386-259">데이터 암호화 인증서</span><span class="sxs-lookup"><span data-stu-id="b2386-259">Data encipherment certificate</span></span>
* <span data-ttu-id="b2386-260">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="b2386-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="b2386-261">웹 기반 관리 및 Service Fabric Explorer에 대한 Azure AD 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b2386-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="b2386-262">네이티브 클라이언트 관리에 대한 Azure AD 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b2386-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="b2386-263">사용자 및 할당된 역할</span><span class="sxs-lookup"><span data-stu-id="b2386-263">Users and their assigned roles</span></span>
* <span data-ttu-id="b2386-264">서비스 패브릭 클러스터 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="b2386-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="b2386-265">Key Vault를 통해 구성된 인증서</span><span class="sxs-lookup"><span data-stu-id="b2386-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="b2386-266">구성된 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2386-266">Azure Active Directory configured</span></span>

<span data-ttu-id="b2386-267">다음 다이어그램은 Key Vault 및 Azure AD 구성이 Resource Manager 템플릿 어디에 적합한지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![리소스 관리자 종속성 맵][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="b2386-269">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-269">Create the cluster</span></span>
<span data-ttu-id="b2386-270">이제 [Azure 리소스 템플릿 배포][resource-group-template-deploy]를 사용하여 클러스터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="b2386-271">테스트</span><span class="sxs-lookup"><span data-stu-id="b2386-271">Test it</span></span>
<span data-ttu-id="b2386-272">매개 변수 파일로 Resource Manager 템플릿을 테스트하려면 다음 PowerShell 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="b2386-273">배포</span><span class="sxs-lookup"><span data-stu-id="b2386-273">Deploy it</span></span>
<span data-ttu-id="b2386-274">Resource Manager 템플릿 테스트를 통과했다면 매개 변수 파일로 Resource Manager 템플릿을 배포하기 위해 다음 PowerShell 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="b2386-275">역할에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b2386-275">Assign users to roles</span></span>
<span data-ttu-id="b2386-276">클러스터를 나타내는 응용 프로그램을 만들었으면 사용자를 Service Fabric에서 지원하는 역할(읽기 전용 및 관리자)에 할당합니다. [Azure 클래식 포털][azure-classic-portal]을 사용하여 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="b2386-277">Azure Portal에서 테넌트로 이동한 다음 **응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="b2386-278">이름이 `myTestCluster_Cluster` 같은 웹 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="b2386-279">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="b2386-280">할당할 사용자를 선택하고 화면 아래쪽에 있는 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![역할에 사용자 할당 단추][assign-users-to-roles-button]
5. <span data-ttu-id="b2386-282">사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-282">Select the role to assign to the user.</span></span>

    !["사용자 지정" 대화 상자][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="b2386-284">서비스 패브릭의 역할에 대한 자세한 내용은 [서비스 패브릭 클라이언트의 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="b2386-285">Linux에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b2386-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="b2386-286">작업 편의를 위해 [도우미 스크립트](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="b2386-287">이 도우미 스크립트를 사용하기 전에 먼저 Azure CLI(명령줄 인터페이스)를 설치했으며 해당 경로에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="b2386-288">다운로드한 후 `chmod +x cert_helper.py` 를 실행하여 스크립트에 실행할 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="b2386-289">첫 번째 단계에서는 `azure login` 명령으로 CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="b2386-290">Azure 계정에 로그인한 후 다음 명령에 표시된 것처럼 CA 서명된 인증서로 도우미 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="b2386-291">-ifile 매개 변수는 입력으로 .pfx 파일 또는 .pem 파일과 인증서 형식(pfx나 pem 또는 자체 서명 인증서의 경우 ss)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="b2386-292">-h 매개 변수는 도움말 텍스트를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="b2386-293">이 명령은 출력으로 다음 3개의 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="b2386-294">SourceVaultID - 사용자를 위해 생성된 새로운 KeyVault ResourceGroup의 ID </span><span class="sxs-lookup"><span data-stu-id="b2386-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="b2386-295">인증서에 액세스하기 위한 CertificateUrl</span><span class="sxs-lookup"><span data-stu-id="b2386-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="b2386-296">인증에 사용되는 CertificateThumbprint </span><span class="sxs-lookup"><span data-stu-id="b2386-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="b2386-297">다음 예제에서는 명령을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="b2386-298">위의 명령을 실행하면 다음과 같이 3가지 문자열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="b2386-299">인증서의 주체 이름은 Service Fabric 클러스터 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="b2386-300">클러스터의 HTTPS 관리 끝점 및 Service Fabric Explorer에 대해 SSL을 제공하려면 이렇게 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b2386-301">`.cloudapp.azure.com` 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="b2386-302">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b2386-303">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 클러스터에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="b2386-304">이 주체 이름은 [Resource Manager 템플릿 매개 변수 구성](#configure-arm)에 설명된 대로 보안 Service Fabric 클러스터(Azure AD 없음)를 만드는 데 필요한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="b2386-305">[클러스터에 대한 클라이언트 액세스 인증](service-fabric-connect-to-secure-cluster.md)을 위한 다음 지침을 통해 보안 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="b2386-306">Linux 미리 보기 클러스터에서는 Azure AD 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="b2386-307">[사용자에게 역할 할당](#assign-roles) 섹션에 설명된 대로 관리 및 클라이언트 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="b2386-308">Linux 미리 보기 클러스터에 대해 관리자 및 클라이언트 역할을 지정할 때는 인증에 대한 인증서 지문을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="b2386-309">이 미리 보기 릴리스에서는 체인 유효성 검사나 해지가 수행되지 않으므로 주체 이름은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="b2386-310">자체 서명 인증서를 테스트에 사용하려는 경우 같은 스크립트를 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="b2386-311">그런 다음 인증서 경로와 인증서 이름 대신 `ss` 플래그를 제공하여 Key Vault에 해당 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="b2386-312">예를 들어 자체 서명된 인증서를 만들고 업로드하는 다음 명령을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="b2386-313">이 명령은 동일한 3개의 문자열 SourceVault, CertificateUrl 및 CertificateThumbprint를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="b2386-314">그런 다음 문자열을 사용하여 보안 Linux 클러스터와, 자체 서명 인증서가 있는 위치를 모두 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="b2386-315">클러스터에 연결하려면 자체 서명 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="b2386-316">[클러스터에 대한 클라이언트 액세스 인증](service-fabric-connect-to-secure-cluster.md)을 위한 다음 지침을 통해 보안 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="b2386-317">인증서의 주체 이름은 Service Fabric 클러스터 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="b2386-318">클러스터의 HTTPS 관리 끝점 및 Service Fabric Explorer에 대해 SSL을 제공하려면 이렇게 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b2386-319">`.cloudapp.azure.com` 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="b2386-320">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b2386-321">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 클러스터에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="b2386-322">[Azure Portal에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) 섹션에서 설명한 대로 Azure Portal에서 도우미 스크립트를 통해 매개 변수를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2386-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2386-323">Next steps</span></span>
<span data-ttu-id="b2386-324">이제 Azure Active Directory를 사용하여 관리 인증을 제공하는 보안 클러스터가 생겨났습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="b2386-325">다음으로, [클러스터에 연결](service-fabric-connect-to-secure-cluster.md)하고 [응용 프로그램 암호를 관리](service-fabric-application-secret-management.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="b2386-326">클라이언트 인증에 대한 Azure Active Directory 설정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b2386-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="b2386-327">클라이언트 인증을 위한 Azure AD를 설정하는 동안 문제가 발생할 경우 이 섹션에서 가능한 해결 방법을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="b2386-328">Service Fabric Explorer에 인증서를 선택하라는 메시지가 표시 </span><span class="sxs-lookup"><span data-stu-id="b2386-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="b2386-329">문제</span><span class="sxs-lookup"><span data-stu-id="b2386-329">Problem</span></span>
<span data-ttu-id="b2386-330">Service Fabric Explorer에서 Azure AD에 로그인한 후 브라우저가 홈 페이지로 돌아가지만 인증서를 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![SFX 인증서 선택 대화 상자][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="b2386-332">이유</span><span class="sxs-lookup"><span data-stu-id="b2386-332">Reason</span></span>
<span data-ttu-id="b2386-333">Azure AD 클러스터 응용 프로그램에서 사용자에게 역할이 할당되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="b2386-334">이 때문에 Service Fabric 클러스터에서 Azure AD 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="b2386-335">Service Fabric Explorer는 인증서 인증으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="b2386-336">해결 방법</span><span class="sxs-lookup"><span data-stu-id="b2386-336">Solution</span></span>
<span data-ttu-id="b2386-337">Azure AD 설정 지침을 따르고 사용자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="b2386-338">또한 `SetupApplications.ps1`에서처럼 “앱에 액세스하려면 사용자 할당 필요”를 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="b2386-339">“지정된 자격 증명이 올바르지 않다”는 오류가 표시되면서 PowerShell 연결 실패</span><span class="sxs-lookup"><span data-stu-id="b2386-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="b2386-340">문제</span><span class="sxs-lookup"><span data-stu-id="b2386-340">Problem</span></span>
<span data-ttu-id="b2386-341">PowerShell을 사용하여 “AzureActiveDirectory”보안 모드로 클러스터에 연결할 때, Azure AD 로그인 후 연결이 실패하고 “지정된 자격 증명이 올바르지 않다"는 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="b2386-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="b2386-342">해결 방법</span><span class="sxs-lookup"><span data-stu-id="b2386-342">Solution</span></span>
<span data-ttu-id="b2386-343">이 솔루션은 이전과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="b2386-344">로그인할 때 Service Fabric Explorer가 실패를 반환함: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="b2386-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="b2386-345">문제</span><span class="sxs-lookup"><span data-stu-id="b2386-345">Problem</span></span>
<span data-ttu-id="b2386-346">Service Fabric Explorer에서 Azure AD에 로그인할 때 페이지가 "AADSTS50011: 회신 주소 &lt;url&gt;이 응용 프로그램 &lt;guid&gt;에 대해 구성된 회신 주소와 일치하지 않습니다.”라는 실패를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![SFX 회신 주소가 일치하지 않습니다.][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="b2386-348">이유</span><span class="sxs-lookup"><span data-stu-id="b2386-348">Reason</span></span>
<span data-ttu-id="b2386-349">Service Fabric Explorer를 나타내는 클러스터(웹) 응용 프로그램이 Azure AD에 대해 인증을 시도하며, 해당 요청의 일부로 리디렉션 반환 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="b2386-350">그렇지만 Azure AD 응용 프로그램 **REPLY URL** 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="b2386-351">해결 방법</span><span class="sxs-lookup"><span data-stu-id="b2386-351">Solution</span></span>
<span data-ttu-id="b2386-352">클러스터(웹) 응용 프로그램의 **Configure** 탭에서 **REPLY URL** 목록에 Service Fabric Explorer URL을 추가하거나 목록의 항목 중 하나를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="b2386-353">마친 후 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-353">When you have finished, save your change.</span></span>

![웹 응용 프로그램 회신 URL][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="b2386-355">PowerShell 통해 Azure AD 인증을 사용하여 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="b2386-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="b2386-356">Service Fabric 클러스터에 연결하려면 다음 PowerShell 명령 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="b2386-357">Connect-ServiceFabricCluster cmdlet에 대해 알아보려면 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="b2386-358">여러 클러스터에서 동일한 Azure AD테넌트를 다시 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b2386-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="b2386-359">예.</span><span class="sxs-lookup"><span data-stu-id="b2386-359">Yes.</span></span> <span data-ttu-id="b2386-360">그렇지만 Service Fabric Explorer의 URL을 클러스터(웹) 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="b2386-361">그러지 않으면 Service Fabric Explorer가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="b2386-362">Azure AD가 사용되도록 설정된 경우에도 서버 인증서가 계속 필요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b2386-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="b2386-363">FabricClient와 FabricGateway는 상호 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="b2386-364">Azure AD 인증 중에는 Azure AD 통합은 서버에 클라이언트 ID를 제공하고 서버 인증서가 서버 ID를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2386-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="b2386-365">Service Fabric 인증서에 대한 자세한 내용은 [X.509 인증서 및 Service Fabric][x509-certificates-and-service-fabric]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2386-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

