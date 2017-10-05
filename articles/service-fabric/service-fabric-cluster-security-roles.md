---
title: "Service Fabric 클러스터 보안: 클라이언트 역할 | Microsoft Docs"
description: "이 문서에서는 두 개의 클라이언트 역할 및 역할에 제공된 사용 권한을 설명합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 85935e60bba4b27972282700e2e9c9a22b403bdb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a><span data-ttu-id="5b703-103">서비스 패브릭 클라이언트용 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="5b703-103">Role-based access control for Service Fabric clients</span></span>
<span data-ttu-id="5b703-104">Azure 서비스 패브릭은 서비스 패브릭 클러스터에 연결된 클라이언트 즉, 관리자 및 사용자에 대한 액세스 제어 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-104">Azure Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="5b703-105">액세스 제어를 사용하면 클러스터 관리자가 사용자 그룹마다 특정 클러스터 작업에 대한 액세스를 제한하여 클러스터의 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-105">Access control allows the cluster administrator to limit access to certain cluster operations for different groups of users, making the cluster more secure.</span></span>  

<span data-ttu-id="5b703-106">**관리자** 는 관리 기능(읽기/쓰기 기능만 포함)에 대한 모든 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-106">**Administrators** have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="5b703-107">기본적으로 **사용자** 는 관리 기능(예: 쿼리 기능)에 대한 읽기 권한 및 응용 프로그램과 서비스를 확인하는 기능만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-107">By default, **users** only have read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>

<span data-ttu-id="5b703-108">클러스터 생성 시 각각에 대해 개별 인증서를 제공하여 두 개의 클라이언트 역할(관리자 및 클라이언트)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-108">You specify the two client roles (administrator and client) at the time of cluster creation by providing separate certificates for each.</span></span> <span data-ttu-id="5b703-109">안전한 서비스 패브릭 클러스터를 설정하는 방법에 대한 자세한 내용은 [서비스 패브릭 클러스터 보안](service-fabric-cluster-security.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b703-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span></span>

## <a name="default-access-control-settings"></a><span data-ttu-id="5b703-110">기본 액세스 제어 설정</span><span class="sxs-lookup"><span data-stu-id="5b703-110">Default access control settings</span></span>
<span data-ttu-id="5b703-111">관리자 액세스 제어 형식에는 모든 FabricClient API에 대한 전체 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-111">The administrator access control type has full access to all the FabricClient APIs.</span></span> <span data-ttu-id="5b703-112">다음 작업을 포함하여 서비스 패브릭 클러스터에 대해 읽기 및 쓰기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-112">It can perform any reads and writes on the Service Fabric cluster, including the following operations:</span></span>

### <a name="application-and-service-operations"></a><span data-ttu-id="5b703-113">응용 프로그램 및 서비스 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-113">Application and service operations</span></span>
* <span data-ttu-id="5b703-114">**CreateService**: 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5b703-114">**CreateService**: service creation</span></span>                             
* <span data-ttu-id="5b703-115">**CreateServiceFromTemplate**: 템플릿에서 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5b703-115">**CreateServiceFromTemplate**: service creation from template</span></span>                             
* <span data-ttu-id="5b703-116">**UpdateService**: 서비스 업데이트</span><span class="sxs-lookup"><span data-stu-id="5b703-116">**UpdateService**: service updates</span></span>                             
* <span data-ttu-id="5b703-117">**DeleteService**: 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="5b703-117">**DeleteService**: service deletion</span></span>                             
* <span data-ttu-id="5b703-118">**ProvisionApplicationType**: 응용 프로그램 형식 프로비전</span><span class="sxs-lookup"><span data-stu-id="5b703-118">**ProvisionApplicationType**: application type provisioning</span></span>                             
* <span data-ttu-id="5b703-119">**CreateApplication**: 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="5b703-119">**CreateApplication**: application creation</span></span>                               
* <span data-ttu-id="5b703-120">**DeleteApplication**: 응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="5b703-120">**DeleteApplication**: application deletion</span></span>                             
* <span data-ttu-id="5b703-121">**UpgradeApplication**: 응용 프로그램 업그레이드 시작 또는 중단</span><span class="sxs-lookup"><span data-stu-id="5b703-121">**UpgradeApplication**: starting or interrupting application upgrades</span></span>                             
* <span data-ttu-id="5b703-122">**UnprovisionApplicationType**: 응용 프로그램 형식 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="5b703-122">**UnprovisionApplicationType**: application type unprovisioning</span></span>                             
* <span data-ttu-id="5b703-123">**MoveNextUpgradeDomain**: 명시적 업데이트 도메인으로 응용 프로그램 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="5b703-124">**ReportUpgradeHealth**: 현재 업그레이드 진행으로 응용 프로그램 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-124">**ReportUpgradeHealth**: resuming application upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="5b703-125">**ReportHealth**: 상태 보고</span><span class="sxs-lookup"><span data-stu-id="5b703-125">**ReportHealth**: reporting health</span></span>                             
* <span data-ttu-id="5b703-126">**PredeployPackageToNode**: 사전 배포 API</span><span class="sxs-lookup"><span data-stu-id="5b703-126">**PredeployPackageToNode**: predeployment API</span></span>                            
* <span data-ttu-id="5b703-127">**CodePackageControl**: 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-127">**CodePackageControl**: restarting code packages</span></span>                             
* <span data-ttu-id="5b703-128">**RecoverPartition**: 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="5b703-128">**RecoverPartition**: recovering a partition</span></span>                             
* <span data-ttu-id="5b703-129">**RecoverPartitions**: 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="5b703-129">**RecoverPartitions**: recovering partitions</span></span>                             
* <span data-ttu-id="5b703-130">**RecoverServicePartitions**: 서비스 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="5b703-130">**RecoverServicePartitions**: recovering service partitions</span></span>                             
* <span data-ttu-id="5b703-131">**RecoverSystemPartitions**: 시스템 서비스 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="5b703-131">**RecoverSystemPartitions**: recovering system service partitions</span></span>                             

### <a name="cluster-operations"></a><span data-ttu-id="5b703-132">클러스터 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-132">Cluster operations</span></span>
* <span data-ttu-id="5b703-133">**ProvisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전</span><span class="sxs-lookup"><span data-stu-id="5b703-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span></span>                             
* <span data-ttu-id="5b703-134">**UpgradeFabric**: 클러스터 업그레이드 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-134">**UpgradeFabric**: starting cluster upgrades</span></span>                             
* <span data-ttu-id="5b703-135">**UnprovisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="5b703-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span></span>                         
* <span data-ttu-id="5b703-136">**MoveNextFabricUpgradeDomain**: 명시적 업데이트 도메인으로 클러스터 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="5b703-137">**ReportFabricUpgradeHealth**: 현재 업그레이드 프로세스로 클러스터 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with the current upgrade progress</span></span>                             
* <span data-ttu-id="5b703-138">**StartInfrastructureTask**: 인프라 작업 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-138">**StartInfrastructureTask**: starting infrastructure tasks</span></span>                             
* <span data-ttu-id="5b703-139">**FinishInfrastructureTask**: 인프라 작업 완료</span><span class="sxs-lookup"><span data-stu-id="5b703-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span></span>                             
* <span data-ttu-id="5b703-140">**InvokeInfrastructureCommand**: 인프라 작업 관리 명령</span><span class="sxs-lookup"><span data-stu-id="5b703-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span></span>                              
* <span data-ttu-id="5b703-141">**ActivateNode**: 노드 활성화</span><span class="sxs-lookup"><span data-stu-id="5b703-141">**ActivateNode**: activating a node</span></span>                             
* <span data-ttu-id="5b703-142">**DeactivateNode**: 노드 비활성화</span><span class="sxs-lookup"><span data-stu-id="5b703-142">**DeactivateNode**: deactivating a node</span></span>                             
* <span data-ttu-id="5b703-143">**DeactivateNodesBatch**: 다중 노드 비활성화</span><span class="sxs-lookup"><span data-stu-id="5b703-143">**DeactivateNodesBatch**: deactivating multiple nodes</span></span>                             
* <span data-ttu-id="5b703-144">**RemoveNodeDeactivations**: 다중 노드에서 비활성화 되돌리기</span><span class="sxs-lookup"><span data-stu-id="5b703-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span></span>                             
* <span data-ttu-id="5b703-145">**GetNodeDeactivationStatus**: 비활성화 상태 확인</span><span class="sxs-lookup"><span data-stu-id="5b703-145">**GetNodeDeactivationStatus**: checking deactivation status</span></span>                             
* <span data-ttu-id="5b703-146">**NodeStateRemoved**: 노드 상태 제거됨 보고</span><span class="sxs-lookup"><span data-stu-id="5b703-146">**NodeStateRemoved**: reporting node state removed</span></span>                             
* <span data-ttu-id="5b703-147">**ReportFault**: 오류 보고</span><span class="sxs-lookup"><span data-stu-id="5b703-147">**ReportFault**: reporting fault</span></span>                             
* <span data-ttu-id="5b703-148">**FileContent**: 이미지 저장소 클라이언트 파일 전송(클러스터 외부)</span><span class="sxs-lookup"><span data-stu-id="5b703-148">**FileContent**: image store client file transfer (external to cluster)</span></span>                             
* <span data-ttu-id="5b703-149">**FileDownload**: 이미지 저장소 클라이언트 파일 다운로드 시작(클러스터 외부)</span><span class="sxs-lookup"><span data-stu-id="5b703-149">**FileDownload**: image store client file download initiation (external to cluster)</span></span>                             
* <span data-ttu-id="5b703-150">**InternalList**: 이미지 저장소 클라이언트 파일 목록 작업(내부)</span><span class="sxs-lookup"><span data-stu-id="5b703-150">**InternalList**: image store client file list operation (internal)</span></span>                             
* <span data-ttu-id="5b703-151">**Delete**: 이미지 저장소 클라이언트 삭제 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-151">**Delete**: image store client delete operation</span></span>                              
* <span data-ttu-id="5b703-152">**Upload**: 이미지 저장소 클라이언트 업로드 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-152">**Upload**: image store client upload operation</span></span>                             
* <span data-ttu-id="5b703-153">**NodeControl**: 노드 시작, 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5b703-153">**NodeControl**: starting, stopping, and restarting nodes</span></span>                             
* <span data-ttu-id="5b703-154">**MoveReplicaControl**: 노드 간 복제본 이동</span><span class="sxs-lookup"><span data-stu-id="5b703-154">**MoveReplicaControl**: moving replicas from one node to another</span></span>                             

### <a name="miscellaneous-operations"></a><span data-ttu-id="5b703-155">기타 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-155">Miscellaneous operations</span></span>
* <span data-ttu-id="5b703-156">**Ping**: 클라이언트 Ping</span><span class="sxs-lookup"><span data-stu-id="5b703-156">**Ping**: client pings</span></span>                             
* <span data-ttu-id="5b703-157">**Query**: 허용된 모든 쿼리</span><span class="sxs-lookup"><span data-stu-id="5b703-157">**Query**: all queries allowed</span></span>
* <span data-ttu-id="5b703-158">**NameExists**: 이름 지정 URI 존재 확인</span><span class="sxs-lookup"><span data-stu-id="5b703-158">**NameExists**: naming URI existence checks</span></span>                             

<span data-ttu-id="5b703-159">사용자 액세스 제어 형식은 기본적으로 다음 작업으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-159">The user access control type is, by default, limited to the following operations:</span></span> 

* <span data-ttu-id="5b703-160">**EnumerateSubnames**: 이름 지정 URI 열거</span><span class="sxs-lookup"><span data-stu-id="5b703-160">**EnumerateSubnames**: naming URI enumeration</span></span>                             
* <span data-ttu-id="5b703-161">**EnumerateProperties**: 이름 지정 속성 열거</span><span class="sxs-lookup"><span data-stu-id="5b703-161">**EnumerateProperties**: naming property enumeration</span></span>                             
* <span data-ttu-id="5b703-162">**PropertyReadBatch**: 이름 지정 속성 읽기 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-162">**PropertyReadBatch**: naming property read operations</span></span>                             
* <span data-ttu-id="5b703-163">**GetServiceDescription**: 긴 폴링 서비스 알림 및 서비스 설명 읽기</span><span class="sxs-lookup"><span data-stu-id="5b703-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span></span>                             
* <span data-ttu-id="5b703-164">**ResolveService**: 불만 기반 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="5b703-164">**ResolveService**: complaint-based service resolution</span></span>                             
* <span data-ttu-id="5b703-165">**ResolveNameOwner**: 이름 지정 URI 소유자 확인</span><span class="sxs-lookup"><span data-stu-id="5b703-165">**ResolveNameOwner**: resolving naming URI owner</span></span>                             
* <span data-ttu-id="5b703-166">**ResolvePartition**: 시스템 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="5b703-166">**ResolvePartition**: resolving system services</span></span>                             
* <span data-ttu-id="5b703-167">**ServiceNotifications**: 이벤트 기반 서비스 알림</span><span class="sxs-lookup"><span data-stu-id="5b703-167">**ServiceNotifications**: event-based service notifications</span></span>                             
* <span data-ttu-id="5b703-168">**GetUpgradeStatus**: 응용 프로그램 업그레이드 상태 폴링</span><span class="sxs-lookup"><span data-stu-id="5b703-168">**GetUpgradeStatus**: polling application upgrade status</span></span>                             
* <span data-ttu-id="5b703-169">**GetFabricUpgradeStatus**: 클러스터 업그레이드 상태 폴링</span><span class="sxs-lookup"><span data-stu-id="5b703-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span></span>                             
* <span data-ttu-id="5b703-170">**InvokeInfrastructureQuery**: 인프라 작업 쿼리</span><span class="sxs-lookup"><span data-stu-id="5b703-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span></span>                             
* <span data-ttu-id="5b703-171">**List**: 이미지 저장소 클라이언트 파일 목록 작업</span><span class="sxs-lookup"><span data-stu-id="5b703-171">**List**: image store client file list operation</span></span>                             
* <span data-ttu-id="5b703-172">**ResetPartitionLoad**: 장애 조치(failover) 단위에 대한 부하 초기화</span><span class="sxs-lookup"><span data-stu-id="5b703-172">**ResetPartitionLoad**: resetting load for a failover unit</span></span>                             
* <span data-ttu-id="5b703-173">**ToggleVerboseServicePlacementHealthReporting**: 자세한 정보 표시 서비스 배치 상태 보고 설정/해제</span><span class="sxs-lookup"><span data-stu-id="5b703-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span></span>                             

<span data-ttu-id="5b703-174">또한 관리자 액세스 제어는 앞의 작업에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-174">The admin access control also has access to the preceding operations.</span></span>

## <a name="changing-default-settings-for-client-roles"></a><span data-ttu-id="5b703-175">클라이언트 역할의 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="5b703-175">Changing default settings for client roles</span></span>
<span data-ttu-id="5b703-176">클러스터 매니페스트 파일에서는 필요한 경우 클라이언트에 대한 관리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-176">In the cluster manifest file, you can provide admin capabilities to the client if needed.</span></span> <span data-ttu-id="5b703-177">[클러스터 생성](service-fabric-cluster-creation-via-portal.md) 중 **패브릭 설정** 옵션으로 이동하고 **이름**, **관리**, **사용자** 및 **값** 필드에 앞의 설정을 제공하여 기본값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b703-177">You can change the defaults by going to the **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing the preceding settings in the **name**, **admin**, **user**, and **value** fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b703-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b703-178">Next steps</span></span>
[<span data-ttu-id="5b703-179">서비스 패브릭 클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="5b703-179">Service Fabric cluster security</span></span>](service-fabric-cluster-security.md)

[<span data-ttu-id="5b703-180">서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="5b703-180">Service Fabric cluster creation</span></span>](service-fabric-cluster-creation-via-portal.md)

