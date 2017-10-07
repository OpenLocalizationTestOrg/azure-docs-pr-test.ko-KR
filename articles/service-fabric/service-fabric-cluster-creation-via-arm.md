---
title: "서식 파일에서 aaaCreate Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "이 문서에서는 클라이언트 인증을 위해 Azure 리소스 관리자, Azure 주요 자격 증명 모음 및 Azure Active Directory (Azure AD)를 사용 하 여 Azure에서 클러스터를 보안 서비스 패브릭 tooset 방법을 설명 합니다."
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
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="03fb9-103">Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03fb9-104">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="03fb9-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="03fb9-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="03fb9-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="03fb9-106">Azure Resource Manager를 사용하여 Azure에 보안 Azure Service Fabric 클러스터를 설정하는 단계를 안내하는 단계별 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="03fb9-107">에서는 승인 해당 hello 문서 깁니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="03fb9-108">그럼에도 불구 하 고 않으면 hello 콘텐츠로 철저 하 게 알고 이미 있다면 수 있는지 toofollow 각 단계 신중 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="03fb9-109">hello 가이드에서는 다음 절차를 수행 하는 hello에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="03fb9-110">클러스터 및 응용 프로그램 보안에 대 한 Azure 키 자격 증명 모음 tooupload 인증서는 설정</span><span class="sxs-lookup"><span data-stu-id="03fb9-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="03fb9-111">Azure Resource Manager를 사용하여 Azure에 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="03fb9-112">클러스터 관리를 위해 Azure Active Directory(Azure AD)를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="03fb9-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="03fb9-113">보안 클러스터는 클러스터 무단된 액세스 toomanagement 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="03fb9-114">배포, 업그레이드 및 삭제 하는 중 응용 프로그램, 서비스 및 포함 된 hello 데이터 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="03fb9-115">보안 되지 않은 클러스터는 누구 든 지 tooat 언제 든 지 연결 고 관리 작업을 수행할 수는 클러스터.</span><span class="sxs-lookup"><span data-stu-id="03fb9-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="03fb9-116">가능한 toocreate 보안 되지 않은 클러스터는 아니지만 hello 처음부터 보안 클러스터를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="03fb9-117">비보안 클러스터는 나중에 보안 클러스터로 만들 수 없으므로 새 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="03fb9-118">hello 개념 만드는 보안 클러스터의 Linux 또는 Windows 클러스터 되었든 관계 없이 동일 하지만, hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="03fb9-119">자세한 내용 및 보안 Linux 클러스터 만들기를 위한 도우미 스크립트는 [Linux에서 보안 클러스터 만들기](#secure-linux-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03fb9-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="03fb9-120">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="03fb9-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="03fb9-121">이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="03fb9-122">새 PowerShell 세션을 시작할 때 tooyour Azure 계정에에서 로그인 하 고 Azure 명령을 실행 하기 전에 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="03fb9-123">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="03fb9-124">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="03fb9-125">Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="03fb9-125">Set up a key vault</span></span>
<span data-ttu-id="03fb9-126">이 섹션에서는 Azure에서 Service Fabric 클러스터에 대해서와 Service Fabric 응용 프로그램에 대해서 Key Vault를 만드는 단계를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="03fb9-127">완벽 가이드 tooAzure 주요 자격 증명 모음에 대 한 참조 toohello [키 자격 증명 모음 시작 가이드][key-vault-get-started]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="03fb9-128">서비스 패브릭 X.509 인증서 toosecure 클러스터를 사용 하 고 응용 프로그램 보안 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="03fb9-129">Azure에서 서비스 패브릭 클러스터에 대 한 주요 자격 증명 모음 toomanage 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="03fb9-130">Azure에서 클러스터를 배포 하는 경우 서비스 패브릭 클러스터 만들기를 담당 하는 hello Azure 리소스 공급자에서 키 자격 증명 모음 인증서를 끌어온 hello 클러스터 Vm에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="03fb9-131">hello 다음 다이어그램에서는 Azure 키 자격 증명 모음, 서비스 패브릭 클러스터 및 클러스터를 만들 때 주요 자격 증명 모음에 저장 된 인증서를 사용 하는 hello Azure 리소스 공급자 사이의 hello 관계 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![인증서 설치 다이어그램][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="03fb9-133">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-133">Create a resource group</span></span>
<span data-ttu-id="03fb9-134">hello 첫 번째 단계는 toocreate 주요 자격 증명 모음 용으로 특별히 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="03fb9-135">리소스 그룹에 hello 주요 자격 증명 모음을 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="03fb9-136">이 작업에는 hello 계산 및 저장소 리소스 그룹이 포함 된 그룹 키 및 암호를 손실 하지 않고 서비스 패브릭 클러스터를 포함 하는 hello 리소스 그룹을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="03fb9-137">주요 자격 증명 모음을 포함 하는 hello 리소스 그룹 _hello에 있어야 동일한 지역_ 가 사용 하는 hello 클러스터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="03fb9-138">여러 지역에서 toodeploy 클러스터를 계획 하는 경우 hello 키 자격 증명 모음에 속해 있는 영역을 표시 하는 방법 및 hello 리소스 그룹 이름을 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="03fb9-139">hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="03fb9-140">Hello 새 리소스 그룹에서 주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="03fb9-141">hello 주요 자격 증명 모음 _배포를 설정 해야_ tooallow에서 계산 리소스 공급자 tooget 인증서 hello 및 가상 컴퓨터 인스턴스에서 설치:</span><span class="sxs-lookup"><span data-stu-id="03fb9-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="03fb9-142">hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-142">hello output should look like this:</span></span>

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
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="03fb9-143">기존 Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="03fb9-143">Use an existing key vault</span></span>

<span data-ttu-id="03fb9-144">기존 키 자격 증명 모음, toouse 있습니다 _배포에 대 한 활성화 해야_ tooallow에서 계산 리소스 공급자 tooget 인증서 hello 및 클러스터 노드에 설치:</span><span class="sxs-lookup"><span data-stu-id="03fb9-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="03fb9-145">인증서 tooyour 자격 증명 모음 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="03fb9-146">인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="03fb9-147">Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오][service-fabric-cluster-security]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03fb9-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="03fb9-148">클러스터 및 서버 인증서(필수)</span><span class="sxs-lookup"><span data-stu-id="03fb9-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="03fb9-149">이 인증서는 필수 toosecure 클러스터 및 tooit 무단된 액세스를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="03fb9-150">다음 두 방법으로 클러스터 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="03fb9-151">클러스터 인증: 클러스터 페더레이션을 위해 노드 간 통신을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="03fb9-152">이 인증서와 함께 자신의 신분을 증명 노드만 hello 클러스터에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="03fb9-153">서버 인증: 알 수 있도록 hello 관리 클라이언트 toohello 실제 클러스터와 통신할 hello 클러스터 관리 끝점 tooa 관리 클라이언트를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="03fb9-154">이 인증서 또한 제공 SSL hello HTTPS 관리 API에 대 한 서비스 패브릭 탐색기에 대 한 HTTPS를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="03fb9-155">tooserve 이러한으로 hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="03fb9-156">hello 인증서 개인 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="03fb9-157">개인 정보 교환 (.pfx) 파일 tooa를 내보낼 수 있는 키 교환에 대 한 hello 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="03fb9-158">hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="03fb9-159">이 일치는 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="03fb9-160">Hello에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다. cloudapp.azure.com 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="03fb9-161">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="03fb9-162">CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="03fb9-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="03fb9-163">응용 프로그램 인증서(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="03fb9-163">Application certificates (optional)</span></span>
<span data-ttu-id="03fb9-164">응용 프로그램 보안을 위해 클러스터에 제한 없는 수의 인증서를 추가로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="03fb9-165">클러스터를 만들기 전에 hello 응용 프로그램 보안 시나리오를 같은 hello 노드에 설치 하는 인증서 toobe를 필요로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="03fb9-166">응용 프로그램 구성 값의 암호화 및 암호 해독</span><span class="sxs-lookup"><span data-stu-id="03fb9-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="03fb9-167">복제 중에 노드 간 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="03fb9-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="03fb9-168">Azure 리소스 공급자 사용을 위한 인증서 서식 지정</span><span class="sxs-lookup"><span data-stu-id="03fb9-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="03fb9-169">Key Vault를 통해 개인 키 파일(.pfx)을 직접 추가하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="03fb9-170">그러나 hello Azure 계산 리소스 공급자에는 특별 한 개체 JSON (JavaScript Notation) 형식으로 저장 된 키 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="03fb9-171">hello 형식에는 기본 64로 인코딩된 문자열 및 개인 키 암호 hello로 hello.pfx 파일로를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="03fb9-172">tooaccommodate hello JSON 문자열에 배치 하 고 "secrets" hello 키에로 저장 한 다음 키 해야 이러한 요구 사항을 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="03fb9-173">이 프로세스는 더 쉽게 toomake는 [PowerShell 모듈은 GitHub에서 사용할 수 있는][service-fabric-rp-helpers]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="03fb9-174">toouse hello 모듈 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="03fb9-175">로컬 디렉터리에 hello hello 리포지토리의 전체 콘텐츠를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="03fb9-176">Toohello 로컬 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="03fb9-177">PowerShell 창에 hello ServiceFabricRPHelpers 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="03fb9-178">hello `Invoke-AddCertToKeyVault` 이 PowerShell 모듈에서 명령을 자동으로 인증서 개인 키를 JSON 문자열로 서식을 지정 하 고 toohello 주요 자격 증명 모음에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="03fb9-179">Hello 명령 tooadd hello 클러스터 인증서 및 모든 추가 응용 프로그램 인증서 toohello 주요 자격 증명 모음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="03fb9-180">클러스터에 tooinstall 포함 하려는 경우 추가 인증서에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="03fb9-181">기존 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="03fb9-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="03fb9-182">여기에 표시 된 하나 hello 같은 오류가 발생할 경우에 일반적으로 리소스 URL 충돌이 있는지 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="03fb9-183">hello 주요 자격 증명 모음 이름 변경 tooresolve hello 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="03fb9-184">Hello 충돌을 해결 한 후 hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="03fb9-185">Hello 세 위의 문자열, CertificateThumbprint, SourceVault, 및 CertificateURL, tooset tooobtain 및 보안 서비스 패브릭 클러스터를 응용 프로그램 보안을 위해 사용 하 고 있는 모든 응용 프로그램 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="03fb9-186">Hello 문자열을 저장 하지 않으면 어려운 tooretrieve hello 키를 쿼리하여 해당 자격 증명 모음에 나중에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="03fb9-187">자체 서명 된 인증서를 만들고 toohello 주요 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="03fb9-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="03fb9-188">주요 자격 증명 인증서 toohello 모음을 이미 업로드 하는 경우이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="03fb9-189">이 단계는 tooyour 주요 자격 증명 모음에 업로드 하 고 새 자체 서명 된 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="03fb9-190">다음 스크립트는 hello hello 매개 변수를 변경 하 고 다음 실행 후 인증서 암호를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="03fb9-191">여기에 표시 된 하나 hello 같은 오류가 발생할 경우에 일반적으로 리소스 URL 충돌이 있는지 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="03fb9-192">tooresolve hello 충돌, hello 주요 자격 증명 모음 이름 변경, RG 이름 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="03fb9-193">Hello 충돌을 해결 한 후 hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="03fb9-194">Hello 세 위의 문자열, CertificateThumbprint, SourceVault, 및 CertificateURL, tooset tooobtain 및 보안 서비스 패브릭 클러스터를 응용 프로그램 보안을 위해 사용 하 고 있는 모든 응용 프로그램 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="03fb9-195">Hello 문자열을 저장 하지 않으면 어려운 tooretrieve hello 키를 쿼리하여 해당 자격 증명 모음에 나중에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="03fb9-196">이 시점에서 요소를에서 다음 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="03fb9-197">hello 주요 자격 증명 모음 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-197">hello key vault resource group.</span></span>
* <span data-ttu-id="03fb9-198">안녕 주요 자격 증명 모음 및 해당 URL (SourceVault hello PowerShell 출력 앞에).</span><span class="sxs-lookup"><span data-stu-id="03fb9-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="03fb9-199">hello 클러스터 서버 인증 인증서 및 hello 주요 자격 증명 모음에서 해당 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="03fb9-200">hello 응용 프로그램 인증서 및 hello 키 자격 증명 모음에 사이트의 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="03fb9-201">클라이언트 인증에 대한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="03fb9-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="03fb9-202">Azure AD 조직 (테 넌 트 라고) toomanage 사용자 액세스 tooapplications를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="03fb9-203">응용 프로그램은 웹 기반 로그인 UI를 갖는 항목과 네이티브 클라이언트 환경을 갖는 항목으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="03fb9-204">이 문서에서는 이미 테넌트를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="03fb9-205">하지 않은 경우 먼저 읽으십시오 [tooget Azure Active Directory 테 넌 트][active-directory-howto-tenant]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="03fb9-206">서비스 패브릭 클러스터는 웹 기반 hello를 포함 하 여 관리 기능을 몇 가지 항목 지점 tooits 제공 [서비스 패브릭 탐색기] [ service-fabric-visualizing-your-cluster] 및 [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="03fb9-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="03fb9-207">결과적으로, toocontrol 액세스 toohello 클러스터에 대 한 두 개의 Azure AD 응용 프로그램, 웹 응용 프로그램 및 한 네이티브 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="03fb9-208">서비스 패브릭 클러스터를 사용 하 여 Azure AD를 구성에 관련 hello 단계 중 일부는 toosimplify, Windows PowerShell 스크립트 집합을 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="03fb9-209">Hello hello 클러스터를 만들기 전에 다음 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="03fb9-210">Hello 스크립트에 예상 되는 클러스터 이름 및 끝점 때문에 hello 값 계획 해야 하 고 값을 이미 만든 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="03fb9-211">[Hello 스크립트 다운로드] [ sf-aad-ps-script-download] tooyour 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="03fb9-212">마우스 오른쪽 단추로 클릭 hello zip 파일을 선택 **속성**선택, hello **차단 해제** 확인란을 선택한 다음 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="03fb9-213">Hello zip 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="03fb9-214">실행 `SetupApplications.ps1`, hello TenantId를 ClusterName, 및 WebApplicationReplyUrl 매개 변수로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="03fb9-215">예:</span><span class="sxs-lookup"><span data-stu-id="03fb9-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="03fb9-216">Hello PowerShell 명령을 실행 하 여 프로그램 TenantId를 찾을 수 있습니다 `Get-AzureSubscription`합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="03fb9-217">모든 구독에 대 한 hello TenantId 표시이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="03fb9-218">ClusterName는 hello 스크립트에 의해 만들어진 사용 되는 tooprefix hello Azure AD 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="03fb9-219">않아도 toomatch hello 실제 클러스터 이름을 정확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="03fb9-220">것이 유일한 toomake 의도 한 것으로 사용 되는 보다 쉽게 Azure AD toomap 아티팩트 toohello 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="03fb9-221">WebApplicationReplyUrl은 Azure AD 로그인 후 tooyour 사용자가 반환 하는 hello 기본 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="03fb9-222">기본적으로 클러스터에 대 한 hello 서비스 패브릭 탐색기 끝점으로이 끝점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="03fb9-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="03fb9-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="03fb9-224">Hello Azure AD 테 넌 트에 대 한 관리자 권한이 있는 tooan 계정에서 증명된 toosign 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="03fb9-225">에 로그인 한 후 hello 스크립트가 만듭니다 hello 웹 및 네이티브 응용 프로그램 toorepresent 서비스 패브릭 클러스터.</span><span class="sxs-lookup"><span data-stu-id="03fb9-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="03fb9-226">Hello의 hello 테 넌 트의 응용 프로그램을 확인 하면 [Azure 클래식 포털][azure-classic-portal], 새 항목 두 개 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="03fb9-227">*ClusterName*\_클러스터</span><span class="sxs-lookup"><span data-stu-id="03fb9-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="03fb9-228">*ClusterName*\_클라이언트</span><span class="sxs-lookup"><span data-stu-id="03fb9-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="03fb9-229">hello 스크립트 hello Azure Resource Manager 템플릿에 좋습니다 tookeep hello PowerShell 창을 이므로 hello 다음 단원의 hello 클러스터를 만들 때 필요한 JSON 열 hello를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="03fb9-230">서비스 패브릭 클러스터 Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="03fb9-231">이 섹션에서는 hello 서비스 패브릭 클러스터 리소스 관리자 템플릿을 PowerShell 명령을 사용 하는 hello 앞의 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="03fb9-232">예제 리소스 관리자 템플릿을 hello에서 사용할 수 있는 [GitHub의 Azure 빠른 시작 템플릿 갤러리][azure-quickstart-templates]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="03fb9-233">이러한 템플릿은 클러스터 템플릿의 시작점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="03fb9-234">Hello 리소스 관리자 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="03fb9-235">이 가이드에서는 hello [5 노드 보안 클러스터] [ service-fabric-secure-cluster-5-node-1-nodetype] 예제 템플릿과 템플릿 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="03fb9-236">다운로드 `azuredeploy.json` 및 `azuredeploy.parameters.json` tooyour 컴퓨터 하 고 원하는 텍스트 편집기에서 두 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="03fb9-237">인증서 추가</span><span class="sxs-lookup"><span data-stu-id="03fb9-237">Add certificates</span></span>
<span data-ttu-id="03fb9-238">Hello 주요 자격 증명 모음 hello 인증서 키가 포함 된 참조 하 여 인증서 tooa 클러스터 리소스 관리자 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="03fb9-239">리소스 관리자 템플릿 매개 변수 파일에 키 자격 증명 모음 값 hello를 배치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="03fb9-240">이렇게 유지 hello 리소스 관리자 템플릿 파일 다시 사용할 수 있고 특정 tooa 배포 값이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="03fb9-241">모든 인증서 toohello 가상 컴퓨터 크기 집합 osProfile 추가</span><span class="sxs-lookup"><span data-stu-id="03fb9-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="03fb9-242">Hello 클러스터에 설치 된 모든 인증서는 hello 눈금 집합 리소스 (Microsoft.Compute/virtualMachineScaleSets)의 hello osProfile 섹션에 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="03fb9-243">이 작업에는 hello 리소스 공급자 tooinstall hello 인증서 hello Vm에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="03fb9-244">이 설치는 hello 클러스터 인증서와 응용 프로그램에 대 한 toouse를 계획 하는 모든 응용 프로그램 보안 인증서를 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

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

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="03fb9-245">Hello 서비스 패브릭 클러스터 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="03fb9-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="03fb9-246">두 hello 서비스 패브릭 클러스터 리소스 (Microsoft.ServiceFabric/clusters) hello 클러스터 인증 인증서로 구성 되어 있어야 하 고 hello 가상 컴퓨터 크기 조정 집합 리소스에 설정 하는 가상 컴퓨터 크기에 대 한 서비스 패브릭 확장 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="03fb9-247">이 정렬을 hello 서비스 패브릭 리소스 공급자 tooconfigure 사용 하면 클러스터 인증 및 관리 끝점에 대 한 서버 인증에 사용 하기 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="03fb9-248">가상 컴퓨터 확장 집합 리소스:</span><span class="sxs-lookup"><span data-stu-id="03fb9-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="03fb9-249">서비스 패브릭 리소스:</span><span class="sxs-lookup"><span data-stu-id="03fb9-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="03fb9-250">Azure AD 구성 삽입</span><span class="sxs-lookup"><span data-stu-id="03fb9-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="03fb9-251">Azure AD hello 구성 이전에 만든 서식 파일에 리소스 관리자에 직접 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="03fb9-252">그러나 먼저 매개 변수 파일 tookeep hello 리소스 관리자 템플릿 재사용에 hello 값을 추출 하는 값 특정 tooa 배포는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

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

### <span data-ttu-id="03fb9-253"><a "configure-arm" ></a>Resource Manager 템플릿 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="03fb9-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="03fb9-254">마지막으로 hello 주요 자격 증명 모음 및 Azure AD PowerShell 명령 toopopulate hello 매개 변수 파일에서 hello 출력 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

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
<span data-ttu-id="03fb9-255">이 시점에서 요소를에서 다음 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="03fb9-256">Key Vault 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="03fb9-256">Key vault resource group</span></span>
  * <span data-ttu-id="03fb9-257">주요 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="03fb9-257">Key vault</span></span>
  * <span data-ttu-id="03fb9-258">클러스터 서버 인증 인증서</span><span class="sxs-lookup"><span data-stu-id="03fb9-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="03fb9-259">데이터 암호화 인증서</span><span class="sxs-lookup"><span data-stu-id="03fb9-259">Data encipherment certificate</span></span>
* <span data-ttu-id="03fb9-260">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="03fb9-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="03fb9-261">웹 기반 관리 및 Service Fabric Explorer에 대한 Azure AD 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="03fb9-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="03fb9-262">네이티브 클라이언트 관리에 대한 Azure AD 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="03fb9-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="03fb9-263">사용자 및 할당된 역할</span><span class="sxs-lookup"><span data-stu-id="03fb9-263">Users and their assigned roles</span></span>
* <span data-ttu-id="03fb9-264">서비스 패브릭 클러스터 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="03fb9-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="03fb9-265">Key Vault를 통해 구성된 인증서</span><span class="sxs-lookup"><span data-stu-id="03fb9-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="03fb9-266">구성된 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03fb9-266">Azure Active Directory configured</span></span>

<span data-ttu-id="03fb9-267">다이어그램을 다음 hello 주요 자격 증명 모음 및 Azure AD 구성 리소스 관리자 서식 파일에 필요한 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![리소스 관리자 종속성 맵][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="03fb9-269">Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-269">Create hello cluster</span></span>
<span data-ttu-id="03fb9-270">현재 위치는 준비 toocreate hello 클러스터를 사용 하 여 [Azure 리소스 템플릿 배포][resource-group-template-deploy]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="03fb9-271">테스트</span><span class="sxs-lookup"><span data-stu-id="03fb9-271">Test it</span></span>
<span data-ttu-id="03fb9-272">다음 PowerShell 명령을 tootest hello를 리소스 관리자 템플릿을 사용 하 여 매개 변수 파일:</span><span class="sxs-lookup"><span data-stu-id="03fb9-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="03fb9-273">배포</span><span class="sxs-lookup"><span data-stu-id="03fb9-273">Deploy it</span></span>
<span data-ttu-id="03fb9-274">Hello 리소스 관리자 템플릿 테스트 통과 하는 경우 다음 PowerShell 명령을 toodeploy hello 사용자 리소스 관리자 템플릿을 사용 매개 변수 파일:</span><span class="sxs-lookup"><span data-stu-id="03fb9-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="03fb9-275">사용자가 tooroles 할당</span><span class="sxs-lookup"><span data-stu-id="03fb9-275">Assign users tooroles</span></span>
<span data-ttu-id="03fb9-276">Hello 응용 프로그램 toorepresent 클러스터를 만든 후 사용자가 서비스 패브릭에서 지 원하는 toohello 역할을 할당: 읽기 전용 및 관리자 Hello를 사용 하 여 hello 역할을 할당할 수 있습니다 [Azure 클래식 포털][azure-classic-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="03fb9-277">Hello Azure 포털에서에서 tooyour 테 넌 트를 선택한 후 선택 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="03fb9-278">Hello 웹 응용 프로그램을 선택 이름이 같은 `myTestCluster_Cluster`합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="03fb9-279">Hello 클릭 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="03fb9-280">사용자 tooassign를 선택 하 고 hello를 클릭 한 다음 **할당** hello hello 화면 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![할당 사용자 tooroles 단추][assign-users-to-roles-button]
5. <span data-ttu-id="03fb9-282">Hello 역할 tooassign toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-282">Select hello role tooassign toohello user.</span></span>

    !["사용자 지정" 대화 상자][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="03fb9-284">서비스 패브릭의 역할에 대한 자세한 내용은 [서비스 패브릭 클라이언트의 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03fb9-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="03fb9-285">Linux에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="03fb9-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="03fb9-286">제공 된 보다 쉽게 toomake hello 프로세스는 [도우미 스크립트](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="03fb9-287">이 도우미 스크립트를 사용하기 전에 먼저 Azure CLI(명령줄 인터페이스)를 설치했으며 해당 경로에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="03fb9-288">Hello 스크립트를 실행 하 여 사용 권한을 tooexecute에 있는지 확인 `chmod +x cert_helper.py` 다운로드 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="03fb9-289">hello 첫 번째 단계 hello로 CLI를 사용 하 여 toosign tooyour Azure 계정에에서는 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="03fb9-290">Tooyour Azure 계정이 로그인 한 후 해당 CA 사용 하 여 hello 도우미 스크립트 서명 된 인증서를 hello 다음 명령으로:</span><span class="sxs-lookup"><span data-stu-id="03fb9-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="03fb9-291">hello-ifile 매개 변수는 hello 인증서 종류 (pfx 또는 pem, 또는 자체 서명 된 인증서 경우 ss)을 입력으로.pfx 파일 또는.pem 파일 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="03fb9-292">hello 매개 변수-h hello 도움말 텍스트 한 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="03fb9-293">이 명령은 hello 세 개의 문자열 hello 출력으로 다음을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="03fb9-294">Hello에 대 한 hello id는 SourceVaultID를 생성 하는 새 KeyVault 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="03fb9-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="03fb9-295">Hello 인증서에 액세스 하기 위한 CertificateUrl</span><span class="sxs-lookup"><span data-stu-id="03fb9-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="03fb9-296">인증에 사용되는 CertificateThumbprint </span><span class="sxs-lookup"><span data-stu-id="03fb9-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="03fb9-297">다음 예제는 hello toouse 명령 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="03fb9-298">앞에 다음과 같은 세 개의 문자열을 hello 명령을 제공 하는 hello를 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="03fb9-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="03fb9-299">hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="03fb9-300">이 항목은 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="03fb9-301">Hello에 대 한 CA에서 SSL 인증서를 가져올 수 없습니다 `.cloudapp.azure.com` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="03fb9-302">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="03fb9-303">CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="03fb9-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="03fb9-304">주체 이름에 이러한 항목이 hello toocreate (Azure AD) 없이 보안 서비스 패브릭 클러스터를 필요에 설명 된 대로 [리소스 관리자 구성 템플릿 매개 변수](#configure-arm)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="03fb9-305">에 대 한 hello 지침에 따라 toohello 보안 클러스터를 연결할 수 있습니다 [클라이언트 액세스 tooa 클러스터 인증](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="03fb9-306">Linux 미리 보기 클러스터에서는 Azure AD 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="03fb9-307">Hello에 설명 된 대로 관리자 및 클라이언트 역할을 할당할 수 [역할 toousers 할당](#assign-roles) 섹션.</span><span class="sxs-lookup"><span data-stu-id="03fb9-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="03fb9-308">Linux 미리 보기 클러스터에 대 한 관리 및 클라이언트 역할을 지정 하면 인증에 인증서 지문을 tooprovide 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="03fb9-309">(제공 하지 않으면 hello 주체 이름 체인 유효성 검사 또는 해지 없습니다이 미리 보기 릴리스에서 수행 하므로.)</span><span class="sxs-lookup"><span data-stu-id="03fb9-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="03fb9-310">테스트를 위해 toouse 자체 서명 된 인증서를 원하는 경우 사용할 수 있습니다 하나는 동일한 스크립트 toogenerate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="03fb9-311">Hello 플래그를 제공 하 여 hello 인증서 tooyour 주요 자격 증명 모음을 업로드 한 다음 `ss` hello 인증서 경로 및 인증서 이름을 제공 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="03fb9-312">예를 들어 다음 명령을 만들고 자체 서명 된 인증서를 업로드 하기 위한 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="03fb9-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="03fb9-313">이 명령은 반환 동일한 세 개의 문자열 hello: SourceVault, CertificateUrl, 및 CertificateThumbprint 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="03fb9-314">보안 Linux 클러스터와 hello 자체 서명 된 인증서를 배치할 위치 모두에 hello 문자열 toocreate 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="03fb9-315">Hello 자체 서명 된 인증서 tooconnect toohello 클러스터를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="03fb9-316">에 대 한 hello 지침에 따라 toohello 보안 클러스터를 연결할 수 있습니다 [클라이언트 액세스 tooa 클러스터 인증](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="03fb9-317">hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="03fb9-318">이 항목은 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="03fb9-319">Hello에 대 한 CA에서 SSL 인증서를 가져올 수 없습니다 `.cloudapp.azure.com` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="03fb9-320">클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="03fb9-321">CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="03fb9-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="03fb9-322">Hello에 설명 된 대로 hello 도우미 스크립트 hello Azure 포털에서에서 hello 매개 변수를 채울 수 [hello Azure 포털에서에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) 섹션.</span><span class="sxs-lookup"><span data-stu-id="03fb9-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03fb9-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03fb9-323">Next steps</span></span>
<span data-ttu-id="03fb9-324">이제 Azure Active Directory를 사용하여 관리 인증을 제공하는 보안 클러스터가 생겨났습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="03fb9-325">그런 다음, [tooyour 클러스터 연결](service-fabric-connect-to-secure-cluster.md) 너무 방법을 알아봅니다[응용 프로그램 암호 관리](service-fabric-application-secret-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="03fb9-326">클라이언트 인증에 대한 Azure Active Directory 설정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="03fb9-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="03fb9-327">클라이언트 인증을 위해 Azure AD를 설정 하는 동안 문제를 실행 하면이 섹션의 hello 잠재적 해결 방법을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="03fb9-328">서비스 패브릭 탐색기 tooselect 인증서 라는 메시지가 표시</span><span class="sxs-lookup"><span data-stu-id="03fb9-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="03fb9-329">문제</span><span class="sxs-lookup"><span data-stu-id="03fb9-329">Problem</span></span>
<span data-ttu-id="03fb9-330">서비스 패브릭 탐색기에서 AD tooAzure 성공적으로 로그인 한 후에 hello 브라우저 toohello 홈 페이지를 반환 하지만 tooselect 인증서 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![SFX 인증서 선택 대화 상자][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="03fb9-332">이유</span><span class="sxs-lookup"><span data-stu-id="03fb9-332">Reason</span></span>
<span data-ttu-id="03fb9-333">hello 사용자 hello Azure AD 클러스터 응용 프로그램에서에서 역할을 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="03fb9-334">이 때문에 Service Fabric 클러스터에서 Azure AD 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="03fb9-335">서비스 패브릭 탐색기 대신 toocertificate 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="03fb9-336">해결 방법</span><span class="sxs-lookup"><span data-stu-id="03fb9-336">Solution</span></span>
<span data-ttu-id="03fb9-337">Azure AD를 설정 하기 위한 지침을 hello 하 고 사용자 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="03fb9-338">또한 "사용자 할당 필요 tooaccess app" 설정 하는 것이 `SetupApplications.ps1` 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="03fb9-339">PowerShell 사용한 연결 오류가 발생 하면서 실패: "hello 지정 된 자격 증명이 올바르지 않습니다".</span><span class="sxs-lookup"><span data-stu-id="03fb9-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="03fb9-340">문제</span><span class="sxs-lookup"><span data-stu-id="03fb9-340">Problem</span></span>
<span data-ttu-id="03fb9-341">오류가 발생 하 여 hello 연결이 실패 tooAzure AD 성공적으로 로그인 한 후에 "AzureActiveDirectory" 보안 모드를 사용 하 여 PowerShell tooconnect toohello 클러스터를 사용할 때는: "hello" 지정 된 자격 증명이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="03fb9-342">해결 방법</span><span class="sxs-lookup"><span data-stu-id="03fb9-342">Solution</span></span>
<span data-ttu-id="03fb9-343">이 솔루션은 hello 앞서 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="03fb9-344">로그인할 때 Service Fabric Explorer가 실패를 반환함: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="03fb9-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="03fb9-345">문제</span><span class="sxs-lookup"><span data-stu-id="03fb9-345">Problem</span></span>
<span data-ttu-id="03fb9-346">서비스 패브릭 탐색기에서 tooAzure AD에서에서 toosign을 시도할 때 hello 페이지에서 오류를 반환 하는: "AADSTS50011: 회신 주소 hello &lt;url&gt; hello 응용 프로그램으로 구성 된 hello 회신 주소와 일치 하지 않습니다: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="03fb9-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![SFX 회신 주소가 일치하지 않습니다.][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="03fb9-348">이유</span><span class="sxs-lookup"><span data-stu-id="03fb9-348">Reason</span></span>
<span data-ttu-id="03fb9-349">서비스 패브릭 탐색기를 나타내는 hello 클러스터 (웹) 응용 프로그램이 Azure AD에 대해 tooauthenticate를 시도 하 고 hello 리디렉션 반환 URL hello 요청의 일부로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="03fb9-350">Hello URL hello Azure AD 응용 프로그램에 나열 되지 않은 하지만 **회신 URL** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="03fb9-351">해결 방법</span><span class="sxs-lookup"><span data-stu-id="03fb9-351">Solution</span></span>
<span data-ttu-id="03fb9-352">Hello에 **구성** hello 탭 (웹) 응용 프로그램을 클러스터의 경우 추가 hello 서비스 패브릭 탐색기 URL toohello **회신 URL** 나열 하거나 hello hello 목록의 항목 중 하나를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="03fb9-353">마친 후 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-353">When you have finished, save your change.</span></span>

![웹 응용 프로그램 회신 URL][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="03fb9-355">PowerShell 통해 Azure AD 인증을 사용 하 여 hello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="03fb9-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="03fb9-356">서비스 패브릭 클러스터 tooconnect hello 다음 PowerShell 명령 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="03fb9-357">toolearn hello Connect-servicefabriccluster cmdlet에 대 한 참조 [Connect-servicefabriccluster](https://msdn.microsoft.com/library/mt125938.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="03fb9-358">여러 개의 클러스터에 hello 동일한 Azure AD 테 넌 트를 다시 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03fb9-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="03fb9-359">예.</span><span class="sxs-lookup"><span data-stu-id="03fb9-359">Yes.</span></span> <span data-ttu-id="03fb9-360">그러나 tooadd hello 서비스 패브릭 탐색기 URL tooyour 클러스터 (웹) 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="03fb9-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="03fb9-361">그러지 않으면 Service Fabric Explorer가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="03fb9-362">Azure AD가 사용되도록 설정된 경우에도 서버 인증서가 계속 필요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="03fb9-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="03fb9-363">FabricClient와 FabricGateway는 상호 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="03fb9-364">Azure AD 인증 하는 동안 Azure AD 통합 id toohello 서버는 클라이언트를 제공 하 고 hello 서버 인증서가 사용 되는 tooverify hello 서버 id입니다.</span><span class="sxs-lookup"><span data-stu-id="03fb9-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="03fb9-365">Service Fabric 인증서에 대한 자세한 내용은 [X.509 인증서 및 Service Fabric][x509-certificates-and-service-fabric]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03fb9-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

