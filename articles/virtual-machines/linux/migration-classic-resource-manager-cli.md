---
title: "Azure CLI를 사용하여 Resource Manager로 VM 마이그레이션 | Microsoft Docs"
description: "이 문서에서는 플랫폼 지원 방식의 Azure CLI를 사용하여 클래식에서 Azure Resource Manager로 리소스를 마이그레이션하는 과정을 안내합니다."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="d2760-103">Azure CLI를 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2760-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="d2760-104">이러한 단계에서는 Azure CLI(명령줄 인터페이스) 명령을 사용하여 클래식 배포 모델의 laaS(Infrastructure as a Service) 리소스를 Azure Resource Manager 배포 모델로 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d2760-105">이 문서는 [Azure CLI](../../cli-install-nodejs.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d2760-106">여기에 설명된 모든 작업은 idempotent 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="d2760-107">지원되지 않는 기능 또는 구성 오류 이외의 문제가 발생하는 경우 준비, 중단 또는 커밋 작업을 다시 시도하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="d2760-108">그러면 플랫폼에서 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="d2760-109">다음은 마이그레이션 프로세스 중에 단계를 실행해야 하는 순서를 나타내는 순서도입니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="d2760-111">1단계: 마이그레이션 준비</span><span class="sxs-lookup"><span data-stu-id="d2760-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="d2760-112">클래식에서 Resource Manager로 IaaS 리소스 마이그레이션을 평가하는 몇 가지 모범 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="d2760-113">[지원되지 않는 구성 또는 기능 목록](../windows/migration-classic-resource-manager-overview.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="d2760-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="d2760-114">지원되지 않는 구성 또는 기능을 사용하는 가상 컴퓨터가 있다면, 해당 기능/구성 지원이 발표되기를 기다리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="d2760-115">아니면, 필요에 맞을 경우 마이그레이션이 가능하도록 해당 기능을 제거하거나 해당 구성을 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="d2760-116">현재 인프라 및 응용 프로그램을 배포하는 스크립트를 자동화한 경우 마이그레이션을 위해 해당 스크립트를 사용하여 유사한 테스트 설정을 만들어봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="d2760-117">또는 Azure 포털을 사용하여 샘플 환경을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2760-118">Application Gateway는 현재 클래식에서 Resource Manager로 마이그레이션될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="d2760-119">Application Gateway를 사용하여 클래식 가상 네트워크를 마이그레이션하려면 준비 작업을 실행하여 네트워크를 이동하기 전에 게이트웨이를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="d2760-120">마이그레이션을 완료한 후 Azure Resource Manager에서 게이트웨이를 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="d2760-121">다른 구독에서 ExpressRoute 회로에 연결하는 ExpressRoute 게이트웨이를 자동으로 마이그레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="d2760-122">이러한 경우에 ExpressRoute 게이트웨이를 제거하고 가상 네트워크를 마이그레이션한 다음 게이트웨이를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="d2760-123">자세한 내용은 [클래식에서 Resource Manager 배포 모델로 ExpressRoute 회로 및 연결된 가상 네트워크 마이그레이션](../../expressroute/expressroute-migration-classic-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2760-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="d2760-124">2단계: 구독 설정 및 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="d2760-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="d2760-125">마이그레이션 시나리오의 경우 클래식 및 Resource Manager에 대한 환경을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="d2760-126">[Azure CLI를 설치](../../cli-install-nodejs.md)하고 [구독을 선택](../../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="d2760-127">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="d2760-128">다음 명령을 사용하여 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="d2760-129">등록은 일회용 단계이지만 마이그레이션 전에 한 번 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="d2760-130">등록하지 않으면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="d2760-131">*BadRequest : 구독이 마이그레이션에 대해 등록되지 않았습니다.*</span><span class="sxs-lookup"><span data-stu-id="d2760-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="d2760-132">다음 명령을 사용하여 마이그레이션 리소스 공급자에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="d2760-133">일부 경우에 이 명령이 시간 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="d2760-134">그러나 등록은 성공적으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="d2760-135">등록이 완료될 때까지 5분 정도 기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="d2760-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="d2760-136">다음 명령을 사용하여 승인 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="d2760-137">계속 진행하기 전에 RegistrationState가 `Registered` 인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="d2760-138">이제 CLI를 `asm` 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="d2760-139">3단계: 현재 배포의 Azure 지역 또는 VNET에 Azure Resource Manager 가상 컴퓨터 코어가 충분한지 확인</span><span class="sxs-lookup"><span data-stu-id="d2760-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="d2760-140">이 단계를 위해 `arm` 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="d2760-141">다음 명령을 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="d2760-142">다음 CLI 명령을 사용하여 Azure Resource Manager에 있는 현재 코어 양을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="d2760-143">코어 할당량에 대한 자세한 내용은 [제한 및 Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2760-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="d2760-144">이 단계의 확인이 끝나면 `asm` 모드로 다시 전환해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="d2760-145">4단계: 옵션 1 - 클라우드 서비스에서 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2760-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="d2760-146">다음 명령을 사용하여 클라우드 서비스 목록을 가져와서 마이그레이션할 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="d2760-147">클라우드 서비스의 VM이 가상 네트워크이거나 VM에 웹/작업자 역할이 있으면, 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="d2760-148">다음 명령을 실행하여 자세하게 출력된 정보에서 클라우드 서비스에 대한 배포 이름을 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="d2760-149">대부분의 경우, 배포 이름은 클라우드 서비스 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="d2760-150">먼저 다음 명령을 사용하여 클라우드 서비스를 마이그레이션할 수 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="d2760-151">마이그레이션을 위해 클라우드 서비스의 가상 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="d2760-152">두 가지 옵션 중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-152">You have two options to choose from.</span></span>

<span data-ttu-id="d2760-153">VM을 플랫폼에서 만든 가상 네트워크에 마이그레이션하려면, 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="d2760-154">Resource Manager 배포 모델에서 기존 가상 네트워크로 마이그레이션하려면, 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="d2760-155">준비 작업이 완료되면 자세한 정보 출력을 확인하여 VM의 마이그레이션 상태를 가져오고 `Prepared` 상태인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="d2760-156">CLI 또는 Azure 포털을 사용하여 준비된 리소스에 대한 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="d2760-157">마이그레이션할 준비가 되지 않았으며 이전 상태로 되돌아가려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="d2760-158">준비된 구성이 양호하면 계속 진행하고 다음 명령을 사용하여 리소스를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="d2760-159">4단계: 옵션 2 - 가상 네트워크에서 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2760-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="d2760-160">마이그레이션할 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="d2760-161">가상 네트워크에 웹/작업자 역할이 포함되어 있거나 지원되지 않는 구성을 포함하는 VM이 있으면, 유효성 검사 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="d2760-162">다음 명령을 사용하여 구독의 모든 가상 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="d2760-163">출력은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-163">The output will look something like this:</span></span>

![전체 가상 네트워크 이름이 강조 표시된 명령줄의 스크린샷.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="d2760-165">위의 예제에서 **virtualNetworkName**은 전체 이름 **"Group classicubuntu16 classicubuntu16"**입니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="d2760-166">먼저 다음 명령을 사용하여 가상 네트워크를 마이그레이션할 수 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="d2760-167">다음 명령을 사용하여 마이그레이션을 위해 선택한 가상 네트워크를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="d2760-168">CLI 또는 Azure 포털을 사용하여 준비된 가상 컴퓨터에 대한 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="d2760-169">마이그레이션할 준비가 되지 않았으며 이전 상태로 되돌아가려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="d2760-170">준비된 구성이 양호하면 계속 진행하고 다음 명령을 사용하여 리소스를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="d2760-171">5단계: 저장소 계정 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2760-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="d2760-172">가상 컴퓨터 마이그레이션이 완료되면 저장소 계정을 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="d2760-173">다음 명령을 사용하여 마이그레이션을 위한 저장소 계정을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="d2760-174">CLI 또는 Azure 포털을 사용하여 준비된 저장소 계정에 대한 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="d2760-175">마이그레이션할 준비가 되지 않았으며 이전 상태로 되돌아가려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="d2760-176">준비된 구성이 양호하면 계속 진행하고 다음 명령을 사용하여 리소스를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d2760-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="d2760-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2760-177">Next steps</span></span>

* [<span data-ttu-id="d2760-178">클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션 개요</span><span class="sxs-lookup"><span data-stu-id="d2760-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2760-179">클래식에서 Azure Resource Manager로의 플랫폼 지원 마이그레이션에 대한 기술 정보</span><span class="sxs-lookup"><span data-stu-id="d2760-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2760-180">클래식에서 Azure Resource Manager로 IaaS 리소스의 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="d2760-180">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2760-181">PowerShell을 사용하여 클래식에서 Azure Resource Manager로 IaaS 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2760-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d2760-182">클래식에서 Azure Resource Manager로의 IaaS 리소스 마이그레이션을 지원하기 위한 커뮤니티 도구</span><span class="sxs-lookup"><span data-stu-id="d2760-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d2760-183">가장 일반적인 마이그레이션 오류 검토</span><span class="sxs-lookup"><span data-stu-id="d2760-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2760-184">클래식에서 Azure Resource Manager로의 IaaS 리소스 마이그레이션과 관련된 가장 자주 묻는 질문 검토</span><span class="sxs-lookup"><span data-stu-id="d2760-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
