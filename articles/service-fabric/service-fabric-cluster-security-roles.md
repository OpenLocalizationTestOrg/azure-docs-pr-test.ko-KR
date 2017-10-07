---
title: "Service Fabric 클러스터 보안: 클라이언트 역할 | Microsoft Docs"
description: "이 문서에는 hello 두 클라이언트 역할 및 toohello 역할을 제공 하는 hello 권한에 대해 설명 합니다."
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
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a><span data-ttu-id="da224-103">서비스 패브릭 클라이언트용 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="da224-103">Role-based access control for Service Fabric clients</span></span>
<span data-ttu-id="da224-104">Azure 서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 유형을 지원: 관리자와 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="da224-104">Azure Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="da224-105">액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da224-105">Access control allows hello cluster administrator toolimit access toocertain cluster operations for different groups of users, making hello cluster more secure.</span></span>  

<span data-ttu-id="da224-106">**관리자** 기능이 대 한 모든 권한을 toomanagement (읽기/쓰기 기능만 포함).</span><span class="sxs-lookup"><span data-stu-id="da224-106">**Administrators** have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="da224-107">기본적으로 **사용자** 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스를 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da224-107">By default, **users** only have read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>

<span data-ttu-id="da224-108">각각에 대해 별도 인증서를 제공 하 여 클러스터 생성 hello 시 hello 두 클라이언트 역할 (관리자 및 클라이언트)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da224-108">You specify hello two client roles (administrator and client) at hello time of cluster creation by providing separate certificates for each.</span></span> <span data-ttu-id="da224-109">안전한 서비스 패브릭 클러스터를 설정하는 방법에 대한 자세한 내용은 [서비스 패브릭 클러스터 보안](service-fabric-cluster-security.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da224-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span></span>

## <a name="default-access-control-settings"></a><span data-ttu-id="da224-110">기본 액세스 제어 설정</span><span class="sxs-lookup"><span data-stu-id="da224-110">Default access control settings</span></span>
<span data-ttu-id="da224-111">hello 관리자 액세스 제어 형식에 대 한 모든 권한을 tooall hello FabricClient Api 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da224-111">hello administrator access control type has full access tooall hello FabricClient APIs.</span></span> <span data-ttu-id="da224-112">모든 읽기 및 쓰기 작업을 수행 하는 hello를 포함 하 여 hello 서비스 패브릭 클러스터에서 수행할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="da224-112">It can perform any reads and writes on hello Service Fabric cluster, including hello following operations:</span></span>

### <a name="application-and-service-operations"></a><span data-ttu-id="da224-113">응용 프로그램 및 서비스 작업</span><span class="sxs-lookup"><span data-stu-id="da224-113">Application and service operations</span></span>
* <span data-ttu-id="da224-114">**CreateService**: 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="da224-114">**CreateService**: service creation</span></span>                             
* <span data-ttu-id="da224-115">**CreateServiceFromTemplate**: 템플릿에서 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="da224-115">**CreateServiceFromTemplate**: service creation from template</span></span>                             
* <span data-ttu-id="da224-116">**UpdateService**: 서비스 업데이트</span><span class="sxs-lookup"><span data-stu-id="da224-116">**UpdateService**: service updates</span></span>                             
* <span data-ttu-id="da224-117">**DeleteService**: 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="da224-117">**DeleteService**: service deletion</span></span>                             
* <span data-ttu-id="da224-118">**ProvisionApplicationType**: 응용 프로그램 형식 프로비전</span><span class="sxs-lookup"><span data-stu-id="da224-118">**ProvisionApplicationType**: application type provisioning</span></span>                             
* <span data-ttu-id="da224-119">**CreateApplication**: 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="da224-119">**CreateApplication**: application creation</span></span>                               
* <span data-ttu-id="da224-120">**DeleteApplication**: 응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="da224-120">**DeleteApplication**: application deletion</span></span>                             
* <span data-ttu-id="da224-121">**UpgradeApplication**: 응용 프로그램 업그레이드 시작 또는 중단</span><span class="sxs-lookup"><span data-stu-id="da224-121">**UpgradeApplication**: starting or interrupting application upgrades</span></span>                             
* <span data-ttu-id="da224-122">**UnprovisionApplicationType**: 응용 프로그램 형식 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="da224-122">**UnprovisionApplicationType**: application type unprovisioning</span></span>                             
* <span data-ttu-id="da224-123">**MoveNextUpgradeDomain**: 명시적 업데이트 도메인으로 응용 프로그램 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="da224-124">**ReportUpgradeHealth**: hello 현재 업그레이드 진행률와 응용 프로그램 업그레이드를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-124">**ReportUpgradeHealth**: resuming application upgrades with hello current upgrade progress</span></span>                             
* <span data-ttu-id="da224-125">**ReportHealth**: 상태 보고</span><span class="sxs-lookup"><span data-stu-id="da224-125">**ReportHealth**: reporting health</span></span>                             
* <span data-ttu-id="da224-126">**PredeployPackageToNode**: 사전 배포 API</span><span class="sxs-lookup"><span data-stu-id="da224-126">**PredeployPackageToNode**: predeployment API</span></span>                            
* <span data-ttu-id="da224-127">**CodePackageControl**: 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-127">**CodePackageControl**: restarting code packages</span></span>                             
* <span data-ttu-id="da224-128">**RecoverPartition**: 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="da224-128">**RecoverPartition**: recovering a partition</span></span>                             
* <span data-ttu-id="da224-129">**RecoverPartitions**: 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="da224-129">**RecoverPartitions**: recovering partitions</span></span>                             
* <span data-ttu-id="da224-130">**RecoverServicePartitions**: 서비스 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="da224-130">**RecoverServicePartitions**: recovering service partitions</span></span>                             
* <span data-ttu-id="da224-131">**RecoverSystemPartitions**: 시스템 서비스 파티션 복구</span><span class="sxs-lookup"><span data-stu-id="da224-131">**RecoverSystemPartitions**: recovering system service partitions</span></span>                             

### <a name="cluster-operations"></a><span data-ttu-id="da224-132">클러스터 작업</span><span class="sxs-lookup"><span data-stu-id="da224-132">Cluster operations</span></span>
* <span data-ttu-id="da224-133">**ProvisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전</span><span class="sxs-lookup"><span data-stu-id="da224-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span></span>                             
* <span data-ttu-id="da224-134">**UpgradeFabric**: 클러스터 업그레이드 시작</span><span class="sxs-lookup"><span data-stu-id="da224-134">**UpgradeFabric**: starting cluster upgrades</span></span>                             
* <span data-ttu-id="da224-135">**UnprovisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="da224-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span></span>                         
* <span data-ttu-id="da224-136">**MoveNextFabricUpgradeDomain**: 명시적 업데이트 도메인으로 클러스터 업그레이드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="da224-137">**ReportFabricUpgradeHealth**: hello 현재 업그레이드 진행률와 클러스터 업그레이드를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with hello current upgrade progress</span></span>                             
* <span data-ttu-id="da224-138">**StartInfrastructureTask**: 인프라 작업 시작</span><span class="sxs-lookup"><span data-stu-id="da224-138">**StartInfrastructureTask**: starting infrastructure tasks</span></span>                             
* <span data-ttu-id="da224-139">**FinishInfrastructureTask**: 인프라 작업 완료</span><span class="sxs-lookup"><span data-stu-id="da224-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span></span>                             
* <span data-ttu-id="da224-140">**InvokeInfrastructureCommand**: 인프라 작업 관리 명령</span><span class="sxs-lookup"><span data-stu-id="da224-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span></span>                              
* <span data-ttu-id="da224-141">**ActivateNode**: 노드 활성화</span><span class="sxs-lookup"><span data-stu-id="da224-141">**ActivateNode**: activating a node</span></span>                             
* <span data-ttu-id="da224-142">**DeactivateNode**: 노드 비활성화</span><span class="sxs-lookup"><span data-stu-id="da224-142">**DeactivateNode**: deactivating a node</span></span>                             
* <span data-ttu-id="da224-143">**DeactivateNodesBatch**: 다중 노드 비활성화</span><span class="sxs-lookup"><span data-stu-id="da224-143">**DeactivateNodesBatch**: deactivating multiple nodes</span></span>                             
* <span data-ttu-id="da224-144">**RemoveNodeDeactivations**: 다중 노드에서 비활성화 되돌리기</span><span class="sxs-lookup"><span data-stu-id="da224-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span></span>                             
* <span data-ttu-id="da224-145">**GetNodeDeactivationStatus**: 비활성화 상태 확인</span><span class="sxs-lookup"><span data-stu-id="da224-145">**GetNodeDeactivationStatus**: checking deactivation status</span></span>                             
* <span data-ttu-id="da224-146">**NodeStateRemoved**: 노드 상태 제거됨 보고</span><span class="sxs-lookup"><span data-stu-id="da224-146">**NodeStateRemoved**: reporting node state removed</span></span>                             
* <span data-ttu-id="da224-147">**ReportFault**: 오류 보고</span><span class="sxs-lookup"><span data-stu-id="da224-147">**ReportFault**: reporting fault</span></span>                             
* <span data-ttu-id="da224-148">**FileContent**: 저장소 클라이언트 파일 전송 (외부 toocluster) 이미지</span><span class="sxs-lookup"><span data-stu-id="da224-148">**FileContent**: image store client file transfer (external toocluster)</span></span>                             
* <span data-ttu-id="da224-149">**FileDownload**: 저장소 클라이언트 파일 다운로드 시작 (외부 toocluster) 이미지</span><span class="sxs-lookup"><span data-stu-id="da224-149">**FileDownload**: image store client file download initiation (external toocluster)</span></span>                             
* <span data-ttu-id="da224-150">**InternalList**: 이미지 저장소 클라이언트 파일 목록 작업(내부)</span><span class="sxs-lookup"><span data-stu-id="da224-150">**InternalList**: image store client file list operation (internal)</span></span>                             
* <span data-ttu-id="da224-151">**Delete**: 이미지 저장소 클라이언트 삭제 작업</span><span class="sxs-lookup"><span data-stu-id="da224-151">**Delete**: image store client delete operation</span></span>                              
* <span data-ttu-id="da224-152">**Upload**: 이미지 저장소 클라이언트 업로드 작업</span><span class="sxs-lookup"><span data-stu-id="da224-152">**Upload**: image store client upload operation</span></span>                             
* <span data-ttu-id="da224-153">**NodeControl**: 노드 시작, 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="da224-153">**NodeControl**: starting, stopping, and restarting nodes</span></span>                             
* <span data-ttu-id="da224-154">**MoveReplicaControl**: 하나의 노드만 tooanother에서 복제 데이터베이스를 이동</span><span class="sxs-lookup"><span data-stu-id="da224-154">**MoveReplicaControl**: moving replicas from one node tooanother</span></span>                             

### <a name="miscellaneous-operations"></a><span data-ttu-id="da224-155">기타 작업</span><span class="sxs-lookup"><span data-stu-id="da224-155">Miscellaneous operations</span></span>
* <span data-ttu-id="da224-156">**Ping**: 클라이언트 Ping</span><span class="sxs-lookup"><span data-stu-id="da224-156">**Ping**: client pings</span></span>                             
* <span data-ttu-id="da224-157">**Query**: 허용된 모든 쿼리</span><span class="sxs-lookup"><span data-stu-id="da224-157">**Query**: all queries allowed</span></span>
* <span data-ttu-id="da224-158">**NameExists**: 이름 지정 URI 존재 확인</span><span class="sxs-lookup"><span data-stu-id="da224-158">**NameExists**: naming URI existence checks</span></span>                             

<span data-ttu-id="da224-159">hello 사용자 액세스 제어 형식, 기본적으로는 작업을 수행 하는 제한 된 toohello:</span><span class="sxs-lookup"><span data-stu-id="da224-159">hello user access control type is, by default, limited toohello following operations:</span></span> 

* <span data-ttu-id="da224-160">**EnumerateSubnames**: 이름 지정 URI 열거</span><span class="sxs-lookup"><span data-stu-id="da224-160">**EnumerateSubnames**: naming URI enumeration</span></span>                             
* <span data-ttu-id="da224-161">**EnumerateProperties**: 이름 지정 속성 열거</span><span class="sxs-lookup"><span data-stu-id="da224-161">**EnumerateProperties**: naming property enumeration</span></span>                             
* <span data-ttu-id="da224-162">**PropertyReadBatch**: 이름 지정 속성 읽기 작업</span><span class="sxs-lookup"><span data-stu-id="da224-162">**PropertyReadBatch**: naming property read operations</span></span>                             
* <span data-ttu-id="da224-163">**GetServiceDescription**: 긴 폴링 서비스 알림 및 서비스 설명 읽기</span><span class="sxs-lookup"><span data-stu-id="da224-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span></span>                             
* <span data-ttu-id="da224-164">**ResolveService**: 불만 기반 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="da224-164">**ResolveService**: complaint-based service resolution</span></span>                             
* <span data-ttu-id="da224-165">**ResolveNameOwner**: 이름 지정 URI 소유자 확인</span><span class="sxs-lookup"><span data-stu-id="da224-165">**ResolveNameOwner**: resolving naming URI owner</span></span>                             
* <span data-ttu-id="da224-166">**ResolvePartition**: 시스템 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="da224-166">**ResolvePartition**: resolving system services</span></span>                             
* <span data-ttu-id="da224-167">**ServiceNotifications**: 이벤트 기반 서비스 알림</span><span class="sxs-lookup"><span data-stu-id="da224-167">**ServiceNotifications**: event-based service notifications</span></span>                             
* <span data-ttu-id="da224-168">**GetUpgradeStatus**: 응용 프로그램 업그레이드 상태 폴링</span><span class="sxs-lookup"><span data-stu-id="da224-168">**GetUpgradeStatus**: polling application upgrade status</span></span>                             
* <span data-ttu-id="da224-169">**GetFabricUpgradeStatus**: 클러스터 업그레이드 상태 폴링</span><span class="sxs-lookup"><span data-stu-id="da224-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span></span>                             
* <span data-ttu-id="da224-170">**InvokeInfrastructureQuery**: 인프라 작업 쿼리</span><span class="sxs-lookup"><span data-stu-id="da224-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span></span>                             
* <span data-ttu-id="da224-171">**List**: 이미지 저장소 클라이언트 파일 목록 작업</span><span class="sxs-lookup"><span data-stu-id="da224-171">**List**: image store client file list operation</span></span>                             
* <span data-ttu-id="da224-172">**ResetPartitionLoad**: 장애 조치(failover) 단위에 대한 부하 초기화</span><span class="sxs-lookup"><span data-stu-id="da224-172">**ResetPartitionLoad**: resetting load for a failover unit</span></span>                             
* <span data-ttu-id="da224-173">**ToggleVerboseServicePlacementHealthReporting**: 자세한 정보 표시 서비스 배치 상태 보고 설정/해제</span><span class="sxs-lookup"><span data-stu-id="da224-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span></span>                             

<span data-ttu-id="da224-174">hello 관리자 액세스 제어는 액세스 toohello 작업 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da224-174">hello admin access control also has access toohello preceding operations.</span></span>

## <a name="changing-default-settings-for-client-roles"></a><span data-ttu-id="da224-175">클라이언트 역할의 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="da224-175">Changing default settings for client roles</span></span>
<span data-ttu-id="da224-176">Hello 클러스터 매니페스트 파일에 필요한 경우 관리 기능 toohello 클라이언트에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da224-176">In hello cluster manifest file, you can provide admin capabilities toohello client if needed.</span></span> <span data-ttu-id="da224-177">Toohello 이동 하 여 hello 기본값을 변경할 수 **패브릭 설정이** 중 옵션 [클러스터 만들기](service-fabric-cluster-creation-via-portal.md), hello hello 설정을 앞에 제공 하 고 **이름**, **admin**, **사용자**, 및 **값** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="da224-177">You can change hello defaults by going toohello **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing hello preceding settings in hello **name**, **admin**, **user**, and **value** fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da224-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da224-178">Next steps</span></span>
[<span data-ttu-id="da224-179">서비스 패브릭 클러스터 보안</span><span class="sxs-lookup"><span data-stu-id="da224-179">Service Fabric cluster security</span></span>](service-fabric-cluster-security.md)

[<span data-ttu-id="da224-180">서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="da224-180">Service Fabric cluster creation</span></span>](service-fabric-cluster-creation-via-portal.md)

