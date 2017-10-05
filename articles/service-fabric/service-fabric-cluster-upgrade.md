---
title: "Azure Service Fabric 클러스터 업그레이드 | Microsoft Docs"
description: "클러스터 업데이트 모드 설정, 인증서 업그레이드, 응용 프로그램 포트 추가, OS 패치 수행 등을 포함하는 Service Fabric 클러스터를 실행하는 Service Fabric 코드 및/또는 구성을 업그레이드합니다. 업그레이드를 수행할 때 예상할 수 있는 것은 무엇입니까?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 7ea71ab891583c51b3c07a4d0a9f0b4f54e56669
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="70038-104">Azure Service Fabric 클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="70038-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70038-105">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="70038-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="70038-106">독립 실행형 클러스터</span><span class="sxs-lookup"><span data-stu-id="70038-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="70038-107">최신 시스템의 경우 업그레이드 기능 디자인이 제품의 장기적 성공 달성의 비결입니다.</span><span class="sxs-lookup"><span data-stu-id="70038-107">For any modern system, designing for upgradability is key to achieving long-term success of your product.</span></span> <span data-ttu-id="70038-108">Azure 서비스 패브릭 클러스터는 개인이 소유하지만 Microsoft에서 부분적으로 관리하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="70038-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="70038-109">이 문서는 자동으로 관리되는 것과 스스로 구성할 수 있는 것을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-the-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="70038-110">클러스터에서 실행되는 패브릭 버전 제어</span><span class="sxs-lookup"><span data-stu-id="70038-110">Controlling the fabric version that runs on your Cluster</span></span>
<span data-ttu-id="70038-111">Microsoft에서 자동 패브릭 업그레이드를 릴리스하면 클러스터가 수신하도록 설정할 수 있습니다. 또는 클러스터를 배치하려는 지원되는 패브릭 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-111">You can set your cluster to receive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster to be on.</span></span>

<span data-ttu-id="70038-112">포털에서 "upgradeMode" 클러스터를 설정하거나 라이브 클러스터 생성 시 또는 나중에 Resource Manager를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-112">You do this by setting the "upgradeMode" cluster configuration on the portal or using Resource Manager at the time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="70038-113">클러스터에서 지원되는 패브릭 버전이 항상 실행되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-113">Make sure to keep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="70038-114">새로운 버전의 서비스 패브릭 릴리스를 발표하면 이전 버전은 해당 날짜부터 최소 60일 후 지원 종료되는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-114">As and when we announce the release of a new version of service fabric, the previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="70038-115">새로운 릴리스는 [서비스 패브릭 팀 블로그](https://blogs.msdn.microsoft.com/azureservicefabric/)에서 발표됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-115">the  The new releases are announced [on the service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="70038-116">그러면 새로운 릴리스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-116">The new release is available to choose then.</span></span> 
> 
> 

<span data-ttu-id="70038-117">클러스터가 실행되는 릴리스가 만료되기 14일 전에, 클러스터를 경고 성능 상태로 전환하는 상태 이벤트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-117">14 days prior to the expiry of the release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="70038-118">지원되는 패브릭 버전으로 업그레이드할 때까지 클러스터는 경고 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-118">The cluster remains in a warning state until you upgrade to a supported fabric version.</span></span>

### <a name="setting-the-upgrade-mode-via-portal"></a><span data-ttu-id="70038-119">포털을 통해 업그레이드 모드 설정</span><span class="sxs-lookup"><span data-stu-id="70038-119">Setting the upgrade mode via portal</span></span>
<span data-ttu-id="70038-120">클러스터를 만들 때 클러스터를 자동 또는 수동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-120">You can set the cluster to automatic or manual when you are creating the cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="70038-122">라이브 클러스터인 경우 관리 환경을 사용하여 클러스터를 자동 또는 수동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-122">You can set the cluster to automatic or manual when on a live cluster, using the manage experience.</span></span> 

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-portal"></a><span data-ttu-id="70038-123">포털을 통해 수동 모드로 설정된 클러스터에서 새 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="70038-123">Upgrading to a new version on a cluster that is set to Manual mode via portal.</span></span>
<span data-ttu-id="70038-124">새 버전으로 업그레이드하려면 드롭다운 목록에서 사용 가능한 버전을 선택하고 저장하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-124">To upgrade to a new version, all you need to do is select the available version from the dropdown and save.</span></span> <span data-ttu-id="70038-125">패브릭 업그레이드는 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-125">The Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="70038-126">클러스터 상태 정책(노드 상태 및 클러스터에서 실행 중인 모든 응용 프로그램의 상태 조합)은 업그레이드의 기간을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-126">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="70038-127">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-127">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="70038-128">이 문서를 아래로 스크롤하여 사용자 지정 상태 정책을 설정하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="70038-128">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="70038-129">롤백을 일으킨 문제를 수정했으면 이전과 동일한 단계에 따라 업그레이드를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-129">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-the-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="70038-131">Resource Manager 템플릿을 통해 업그레이드 모드 설정</span><span class="sxs-lookup"><span data-stu-id="70038-131">Setting the upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="70038-132">아래 표시된 것처럼 "upgradeMode" 구성을 Microsoft.ServiceFabric/clusters 리소스 정의에 추가하고 "clusterCodeVersion"을 지원되는 패브릭 버전 중 하나로 설정한 후 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-132">Add the "upgradeMode" configuration to the Microsoft.ServiceFabric/clusters resource definition and set the "clusterCodeVersion" to one of the supported fabric versions as shown below and then deploy the template.</span></span> <span data-ttu-id="70038-133">"upgradeMode"에 대해 유효한 값은 "Manual" 또는 "Automatic"입니다.</span><span class="sxs-lookup"><span data-stu-id="70038-133">The valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-a-resource-manager-template"></a><span data-ttu-id="70038-135">Resource Manager 템플릿을 통해 수동 모드로 설정된 클러스터에서 새 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="70038-135">Upgrading to a new version on a cluster that is set to Manual mode via a Resource Manager template.</span></span>
<span data-ttu-id="70038-136">클러스터가 수동 모드인 경우 새 버전으로 업그레이드하려면 "clusterCodeVersion"을 지원되는 버전으로 변경하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-136">When the cluster is in Manual mode, to upgrade to a new version, change the "clusterCodeVersion" to a supported version and deploy it.</span></span> <span data-ttu-id="70038-137">템플릿의 배포 시 패브릭 업그레이드는 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-137">The deployment of the template, kicks of the Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="70038-138">클러스터 상태 정책(노드 상태 및 클러스터에서 실행 중인 모든 응용 프로그램의 상태 조합)은 업그레이드의 기간을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-138">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="70038-139">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-139">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="70038-140">이 문서를 아래로 스크롤하여 사용자 지정 상태 정책을 설정하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="70038-140">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="70038-141">롤백을 일으킨 문제를 수정했으면 이전과 동일한 단계에 따라 업그레이드를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-141">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="70038-142">지정된 구독의 모든 환경에 대해 사용 가능한 모든 버전 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="70038-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="70038-143">다음 명령을 실행하면 다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-143">Run the following command, and you should get an output similar to this.</span></span>

<span data-ttu-id="70038-144">"supportExpiryUtc"는 지정된 릴리스가 만료되거나 이미 만료되었음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70038-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="70038-145">최신 릴리스는 유효한 날짜를 포함하지 않으며 "9999-12-31T23:59:59.9999999" 값을 포함합니다. 이는 만료 날짜가 아직 설정되지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-145">The latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that the expiry date is not yet set.</span></span>

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-the-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="70038-146">클러스터 업그레이드 모드가 자동인 경우 패브릭 업그레이드 동작</span><span class="sxs-lookup"><span data-stu-id="70038-146">Fabric upgrade behavior when the cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="70038-147">Microsoft는 Azure 클러스터에서 실행하는 패브릭 코드 및 구성을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-147">Microsoft maintains the fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="70038-148">필요한 기준으로 소프트웨어에 자동 모니터링된 업그레이드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-148">We perform automatic monitored upgrades to the software on an as-needed basis.</span></span> <span data-ttu-id="70038-149">이러한 업그레이드는 코드, 구성 또는 둘 모두가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="70038-150">응용 프로그램이 이러한 업그레이드로 인해 영향이 없거나 최소한의 영향이 있는지 확인하기 위해 다음 단계로 업그레이드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-150">To make sure that your application suffers no impact or minimal impact due to these upgrades, we perform the upgrades in the following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="70038-151">1단계: 모든 클러스터 상태 정책을 사용하여 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="70038-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="70038-152">이 단계 동안 업그레이드는 한 번에 하나의 업그레이드 도메인을 진행하고 클러스터에서 실행 중이던 응용 프로그램은 가동 중지 시간 없이 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-152">During this phase, the upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="70038-153">클러스터 상태 정책(노드 상태 및 클러스터에서 실행 중인 모든 응용 프로그램의 상태 조합)은 업그레이드의 기간을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-153">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="70038-154">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-154">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="70038-155">그런 다음 구독 소유자에게 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-155">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="70038-156">전자 메일에는 다음 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-156">The email contains the following information:</span></span>

* <span data-ttu-id="70038-157">클러스터 업그레이드를 롤백해야 했다는 알림.</span><span class="sxs-lookup"><span data-stu-id="70038-157">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="70038-158">권장 수정 작업(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="70038-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="70038-159">2단계를 실행할 때까지 일 수(n)</span><span class="sxs-lookup"><span data-stu-id="70038-159">The number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="70038-160">인프라 이유로 업그레이드가 실패한 경우 동일한 업그레이드를 몇 번 더 실행하기 위해 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-160">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="70038-161">전자 메일이 전송된 날짜에서 n일 후 2단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-161">After the n days from the date the email was sent, we proceed to Phase 2.</span></span>

<span data-ttu-id="70038-162">클러스터 상태 정책이 충족하는 경우 업그레이드가 성공한 것으로 간주하고 완료로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-162">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="70038-163">이는 초기 업그레이드 또는 이 단계의 업그레이드 다시 실행 중 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-163">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="70038-164">성공적 실행에 대한 전자 메일 확인은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="70038-165">너무 많은 전자 메일을 전송하지 않도록 하며 전자 메일 수신은 정상에 대한 예외로 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-165">This is to avoid sending you too many emails--receiving an email should be seen as an exception to normal.</span></span> <span data-ttu-id="70038-166">클러스터 업그레이드가 응용 프로그램 가용성에 영향을 주지 않고 성공되기를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-166">We expect most of the cluster upgrades to succeed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="70038-167">2단계: 기본 상태 정책만을 사용하여 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="70038-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="70038-168">이 단계의 상태 정책은 업그레이드 시작 시 정상 상태가 업그레이드 프로세스의 기간 동안 동일하게 유지되는 응용 프로그램의 수 방식으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-168">The health policies in this phase are set in such a way that the number of applications that were healthy at the beginning of the upgrade remains the same for the duration of the upgrade process.</span></span> <span data-ttu-id="70038-169">1단계와 마찬가지로 2단계 업그레이드는 한 번에 하나의 업그레이드 도메인을 진행하고 클러스터에서 실행 중이던 응용 프로그램은 가동 중지 시간 없이 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-169">As in Phase 1, the Phase 2 upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="70038-170">클러스터 상태 정책(노드 상태 및 클러스터에서 실행 중인 모든 응용 프로그램의 상태 조합)은 업그레이드의 기간을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-170">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to for the duration of the upgrade.</span></span>

<span data-ttu-id="70038-171">적용되는 클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-171">If the cluster health policies in effect are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="70038-172">그런 다음 구독 소유자에게 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-172">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="70038-173">전자 메일에는 다음 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-173">The email contains the following information:</span></span>

* <span data-ttu-id="70038-174">클러스터 업그레이드를 롤백해야 했다는 알림.</span><span class="sxs-lookup"><span data-stu-id="70038-174">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="70038-175">권장 수정 작업(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="70038-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="70038-176">3단계를 실행할 때까지 일 수(n)</span><span class="sxs-lookup"><span data-stu-id="70038-176">The number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="70038-177">인프라 이유로 업그레이드가 실패한 경우 동일한 업그레이드를 몇 번 더 실행하기 위해 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-177">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="70038-178">미리 알림 전자 메일은 n일이 끝나기 몇 일 전에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="70038-179">전자 메일이 전송된 날짜에서 n일 후 3단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-179">After the n days from the date the email was sent, we proceed to Phase 3.</span></span> <span data-ttu-id="70038-180">2단계에서 전송한 전자 메일은 심각하게 받아들여져야 하며 수정 작업이 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-180">The emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="70038-181">클러스터 상태 정책이 충족하는 경우 업그레이드가 성공한 것으로 간주하고 완료로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-181">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="70038-182">이는 초기 업그레이드 또는 이 단계의 업그레이드 다시 실행 중 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-182">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="70038-183">성공적 실행에 대한 전자 메일 확인은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="70038-184">3단계: 까다로운 상태 정책을 사용하여 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="70038-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="70038-185">이 단계의 이러한 상태 정책은 응용 프로그램의 상태보다 업그레이드 완료에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="70038-185">These health policies in this phase are geared towards completion of the upgrade rather than the health of the applications.</span></span> <span data-ttu-id="70038-186">이 단계에서 매우 적은 클러스터 업그레이드가 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="70038-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="70038-187">클러스터가 이 단계에 도달하는 경우 응용 프로그램이 비정상이 되고/되거나 가용성이 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-187">If your cluster gets to this phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="70038-188">다른 두 단계와 마찬가지로 3단계 업그레이드는 한 번에 하나의 업그레이드 도메인을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-188">Similar to the other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="70038-189">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-189">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="70038-190">인프라 이유로 업그레이드가 실패한 경우 동일한 업그레이드를 몇 번 더 실행하기 위해 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-190">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="70038-191">그런 다음 지원 및/또는 업그레이드를 더 이상 받지 않도록 클러스터가 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-191">After that, the cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="70038-192">이 정보가 있는 메일이 수정 작업과 함께 구독 소유자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-192">An email with this information is sent to the subscription owner, along with the remedial actions.</span></span> <span data-ttu-id="70038-193">3단계가 실패된 상태로 클러스터가 도달하지 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70038-193">We do not expect any clusters to get into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="70038-194">클러스터 상태 정책이 충족하는 경우 업그레이드가 성공한 것으로 간주하고 완료로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-194">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="70038-195">이는 초기 업그레이드 또는 이 단계의 업그레이드 다시 실행 중 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-195">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="70038-196">성공적 실행에 대한 전자 메일 확인은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="70038-197">사용자가 제어하는 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="70038-197">Cluster configurations that you control</span></span>
<span data-ttu-id="70038-198">클러스터 업그레이드 모드를 설정하는 기능 외에도 라이브 클러스터에서 변경할 수 있는 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-198">In addition to the ability to set the cluster upgrade mode, Here are the configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="70038-199">인증서</span><span class="sxs-lookup"><span data-stu-id="70038-199">Certificates</span></span>
<span data-ttu-id="70038-200">포털을 통해 클러스터 및 클라이언트에 대한 인증서를 쉽게 새로 추가하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-200">You can add new or delete certificates for the cluster and client via the portal easily.</span></span> <span data-ttu-id="70038-201">[자세한 지침은 이 문서](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="70038-201">Refer to [this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![Azure 포털의 인증서 지문을 보여 주는 스크린샷][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="70038-203">응용 프로그램 포트</span><span class="sxs-lookup"><span data-stu-id="70038-203">Application ports</span></span>
<span data-ttu-id="70038-204">노드 유형에 연결된 부하 분산 장치 리소스 속성을 변경하여 응용 프로그램 포트를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-204">You can change application ports by changing the Load Balancer resource properties that are associated with the node type.</span></span> <span data-ttu-id="70038-205">포털을 사용하거나 리소스 관리자 PowerShell을 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-205">You can use the portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="70038-206">노드 유형에서 모든 VM의 새 포트를 열려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-206">To open a new port on all VMs in a node type, do the following:</span></span>

1. <span data-ttu-id="70038-207">적절한 부하 분산 장치에 새 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-207">Add a new probe to the appropriate load balancer.</span></span>
   
    <span data-ttu-id="70038-208">포털을 사용하여 클러스터를 배포한 경우 부하 분산 장치는 각 노드 형식에 대해 "LB-name of the Resource group-NodeTypename"으로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-208">If you deployed your cluster by using the portal, the load balancers are named "LB-name of the Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="70038-209">부하 분산 장치 이름은 리소스 그룹에만 고유하므로 특정 리소스 그룹 아래에 대해 검색하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-209">Since the load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![포털에서 부하 분산 장치에 프로브 추가를 보여 주는 스크린샷][AddingProbes]
2. <span data-ttu-id="70038-211">부하 분산 장치에 새 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-211">Add a new rule to the load balancer.</span></span>
   
    <span data-ttu-id="70038-212">이전 단계에서 만든 프로브를 사용하여 동일한 부하 분산 장치에 새 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-212">Add a new rule to the same load balancer by using the probe that you created in the previous step.</span></span>
   
    ![포털에서 부하 분산 장치에 새 규칙 추가.][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="70038-214">배치 속성</span><span class="sxs-lookup"><span data-stu-id="70038-214">Placement properties</span></span>
<span data-ttu-id="70038-215">각 노드 유형의 경우 사용하려는 사용자 지정 배치 속성을 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-215">For each of the node types, you can add custom placement properties that you want to use in your applications.</span></span> <span data-ttu-id="70038-216">NodeType은 명시적으로 추가하지 않고 사용할 수 있는 기본 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="70038-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="70038-217">배치 제약 조건과 노드 속성 사용 및 정의 방법에 대한 자세한 내용은 서비스 패브릭 클러스터 리소스 관리자 문서의 [클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)에 있는 "배치 제약 조건 및 노드 속성" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70038-217">For details on the use of placement constraints, node properties, and how to define them, refer to the section "Placement Constraints and Node Properties" in the Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="70038-218">용량 메트릭</span><span class="sxs-lookup"><span data-stu-id="70038-218">Capacity metrics</span></span>
<span data-ttu-id="70038-219">각 노드 유형의 경우 부하를 보고하도록 사용하려는 사용자 용량 메트릭을 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-219">For each of the node types, you can add custom capacity metrics that you want to use in your applications to report load.</span></span> <span data-ttu-id="70038-220">부하를 보고하는 용량 메트릭 사용에 대한 자세한 내용은 서비스 패브릭 클러스터 리소스 관리자 설명서에서 [클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md) 및 [메트릭 및 부하](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70038-220">For details on the use of capacity metrics to report load, refer to the Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="70038-221">패브릭 업그레이드 설정 - 상태 정책</span><span class="sxs-lookup"><span data-stu-id="70038-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="70038-222">패브릭 업그레이드에 대한 사용자 지정 상태 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="70038-223">클러스터를 자동 패브릭 업그레이드로 설정한 경우 이러한 정책은 자동 패브릭 업그레이드의 1단계에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-223">If you have set your cluster to Automatic fabric upgrades, then these policies get applied to the Phase-1 of the automatic fabric upgrades.</span></span>
<span data-ttu-id="70038-224">클러스터를 수동 패브릭 업그레이드로 설정한 경우 이러한 정책은 새 버전을 선택할 때마다 적용되며 그러면 시스템이 클러스터에서 패브릭 업그레이드를 시작하도록 트리거링합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering the system to kick off the fabric upgrade in your cluster.</span></span> <span data-ttu-id="70038-225">정책을 재정의하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70038-225">If you do not override the policies, the defaults are used.</span></span>

<span data-ttu-id="70038-226">사용자 지정 상태 정책을 지정하거나 "패브릭 업그레이드" 블레이드 아래에서 고급 업그레이드 설정을 선택하여 현재 설정을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-226">You can specify the custom health policies or review the current settings under the "fabric upgrade" blade, by selecting the advanced upgrade settings.</span></span> <span data-ttu-id="70038-227">다음 그림은 이 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70038-227">Review the following picture on how to.</span></span> 

![사용자 지정 상태 정책 관리][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="70038-229">클러스터에 대한 패브릭 설정 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="70038-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="70038-230">설정에 대한 내용과 설정을 사용자 지정하는 방법은 [서비스 패브릭 클러스터 패브릭 설정](service-fabric-cluster-fabric-settings.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70038-230">Refer to [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="70038-231">클러스터를 구성하는 VM의 OS 패치</span><span class="sxs-lookup"><span data-stu-id="70038-231">OS patches on the VMs that make up the cluster</span></span>
<span data-ttu-id="70038-232">[패치 오케스트레이션 응용 프로그램](service-fabric-patch-orchestration-application.md)을 참조하세요. 그러면 오케스트레이션된 방식으로 Windows 업데이트에서 패치를 설치하도록 클러스터에 배포할 수 있으므로 서비스를 항상 사용할 수 있도록 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-232">Refer to [Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster to install patches from Windows Update in an orchestrated manner, keeping the services available all the time.</span></span> 

### <a name="os-upgrades-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="70038-233">클러스터를 구성하는 VM의 OS 업그레이드</span><span class="sxs-lookup"><span data-stu-id="70038-233">OS upgrades on the VMs that make up the cluster</span></span>
<span data-ttu-id="70038-234">클러스터의 가상 컴퓨터의 OS 이미지를 업그레이드해야 하는 경우 한 번에 하나의 VM에 이 작업을 수행하고 이 업그레이드에 대한 책임을 져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70038-234">If you must upgrade the OS image on the virtual machines of the cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="70038-235">현재 자동화 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70038-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70038-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70038-236">Next steps</span></span>
* <span data-ttu-id="70038-237">[서비스 패브릭 클러스터 패브릭 설정](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="70038-237">Learn how to customize some of the [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="70038-238">[클러스터를 확장 및 축소하는](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="70038-238">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="70038-239">[응용 프로그램 업그레이드](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="70038-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
