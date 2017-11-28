---
title: "Linux와 Windows 간의 Azure Service Fabric 차이점 | Microsoft Docs"
description: "Linux의 Azure Service Fabric 미리 보기와 Windows의 Azure Service Fabric의 차이점입니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7b80bb7d4a4e6a1b4cf47ce87200f47339785c53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="71a96-103">Linux(미리 보기)와 Windows(일반적으로 사용 가능)의 Service Fabric 간의 차이점</span><span class="sxs-lookup"><span data-stu-id="71a96-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="71a96-104">Linux의 Service Fabric이 미리 보기이므로 일부 기능은 Windows에서는 지원되지만 Linux에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="71a96-105">결국 Linux의 Service Fabric이 일반적으로 사용할 수 있게 되는 경우 기능 집합이 동등해 집니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="71a96-106">향후 릴리스에서는 이 기능 차이가 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="71a96-107">제공되는 최신 릴리스(즉, Windows에서 버전 5.6 및 Linux에서 버전 5.5) 간에는 다음과 같은 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-107">The following differences exist between the latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="71a96-108">Reliable Collections(및 Reliable Stateful Services)</span><span class="sxs-lookup"><span data-stu-id="71a96-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="71a96-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="71a96-109">ReverseProxy</span></span> 
* <span data-ttu-id="71a96-110">독립 실행형 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="71a96-110">Standalone installer</span></span> 
* <span data-ttu-id="71a96-111">매니페스트 파일에 대한 XML 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="71a96-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="71a96-112">콘솔 리디렉션</span><span class="sxs-lookup"><span data-stu-id="71a96-112">Console redirection</span></span> 
* <span data-ttu-id="71a96-113">FAS(오류 분석 서비스)</span><span class="sxs-lookup"><span data-stu-id="71a96-113">The Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="71a96-114">Docker Compose 및 볼륨, 컨테이너에 대한 로깅 드라이버</span><span class="sxs-lookup"><span data-stu-id="71a96-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="71a96-115">컨테이너 및 서비스에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="71a96-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="71a96-116">DNS 서비스</span><span class="sxs-lookup"><span data-stu-id="71a96-116">DNS service</span></span>
* <span data-ttu-id="71a96-117">Azure Active Directory 지원</span><span class="sxs-lookup"><span data-stu-id="71a96-117">Azure Active Directory support</span></span>
* <span data-ttu-id="71a96-118">특정 Powershell 명령에 있는 동일한 CLI 명령</span><span class="sxs-lookup"><span data-stu-id="71a96-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="71a96-119">PowerShell 명령의 하위 집합만을 (다음 섹션에서 확장된 대로) Linux 클러스터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span></span>

>[!NOTE]
><span data-ttu-id="71a96-120">콘솔 리디렉션은 Windows의 경우에도 프로덕션 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="71a96-121">Windows와 Linux의 개발 도구도 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="71a96-122">VisualStudio, Powershell, VSTS 및 ETW는 Windows에서 사용되고 Yeoman, Eclipse, Jenkins 및 LTTng는 Linux에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a96-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="71a96-123">Linux Service Fabric 클러스터에서 작동하지 않는 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="71a96-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="71a96-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="71a96-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="71a96-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="71a96-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="71a96-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="71a96-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="71a96-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="71a96-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="71a96-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="71a96-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="71a96-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="71a96-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="71a96-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="71a96-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="71a96-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="71a96-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="71a96-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="71a96-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="71a96-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="71a96-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="71a96-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="71a96-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="71a96-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="71a96-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="71a96-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="71a96-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="71a96-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="71a96-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="71a96-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="71a96-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="71a96-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="71a96-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="71a96-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="71a96-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="71a96-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="71a96-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="71a96-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="71a96-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="71a96-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="71a96-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="71a96-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="71a96-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="71a96-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="71a96-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="71a96-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="71a96-146">Cmd</span></span>
* <span data-ttu-id="71a96-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="71a96-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="71a96-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="71a96-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="71a96-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="71a96-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="71a96-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="71a96-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="71a96-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="71a96-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="71a96-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="71a96-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="71a96-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="71a96-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="71a96-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="71a96-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="71a96-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="71a96-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="71a96-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="71a96-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="71a96-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="71a96-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="71a96-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="71a96-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="71a96-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="71a96-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="71a96-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="71a96-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="71a96-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="71a96-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="71a96-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="71a96-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="71a96-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="71a96-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="71a96-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="71a96-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="71a96-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="71a96-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="71a96-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="71a96-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="71a96-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="71a96-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="71a96-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="71a96-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="71a96-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="71a96-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71a96-177">Next steps</span></span>
* [<span data-ttu-id="71a96-178">Linux에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="71a96-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="71a96-179">OSX에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="71a96-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="71a96-180">Yeoman을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="71a96-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="71a96-181">Eclipse용 Service Fabric 플러그 인을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="71a96-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="71a96-182">Linux에서 첫 번째 CSharp 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="71a96-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="71a96-183">Service Fabric CLI를 사용하여 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="71a96-183">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
