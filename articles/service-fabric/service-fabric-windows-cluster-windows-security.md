---
title: "Windows 보안을 사용하여 Windows에서 실행되는 클러스터 보안 | Microsoft Docs"
description: "Windows 보안을 사용하여 Windows에서 실행되는 독립 실행형 클러스터에서 노드 간 및 클라이언트-노드 보안을 구성하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: e093a631b0cf81195981a8e3d345504ebce02723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="17600-103">Windows 보안을 사용하여 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="17600-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="17600-104">Service Fabric 클러스터에 대한 무단 액세스를 방지하려면 클러스터를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="17600-105">클러스터에서 프로덕션 작업을 실행하는 경우 특히 보안이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="17600-106">이 문서에서는 *ClusterConfig.JSON* 파일에서 Windows 보안을 사용하여 노드 간 및 클라이언트-노드 간 보안을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="17600-107">이 프로세스는 보안[Windows에서 실행되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)의 보안 단계 구성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="17600-108">Service Fabric에서 Windows 보안을 사용하는 방법에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17600-109">보안 방식을 바꾸는 동안 클라이언트 업그레이드가 수행되지 않으므로 노드 간 보안을 선택할 때는 신중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="17600-110">보안 선택을 변경하려면 전체 클러스터를 다시 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="17600-111">gMSA를 사용하여 Windows 보안 구성</span><span class="sxs-lookup"><span data-stu-id="17600-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="17600-112"><seg>
  [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) 독립 실행형 클러스터 패키지와 함께 다운로드된 샘플 *ClusterConfig.gMSA.Windows.MultiMachine.JSON* 구성 파일은 [gMSA(그룹 관리 서비스 계정)](https://technet.microsoft.com/library/hh831782.aspx)를 사용하여 Windows 보안 구성을 위한 템플릿을 포함합니다.</seg></span><span class="sxs-lookup"><span data-stu-id="17600-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="17600-113">**구성 설정**</span><span class="sxs-lookup"><span data-stu-id="17600-113">**Configuration Setting**</span></span> | <span data-ttu-id="17600-114">**설명**</span><span class="sxs-lookup"><span data-stu-id="17600-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="17600-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="17600-115">WindowsIdentities</span></span> |<span data-ttu-id="17600-116">클러스터와 클라이언트 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="17600-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="17600-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="17600-118">노드 간 보안을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-118">Configures node-to-node security.</span></span> <span data-ttu-id="17600-119">그룹 관리 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="17600-119">A group managed service account.</span></span> |  
| <span data-ttu-id="17600-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="17600-120">ClusterSPN</span></span> |<span data-ttu-id="17600-121">gMSA 계정에 대한 정규화된 도메인 SPN</span><span class="sxs-lookup"><span data-stu-id="17600-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="17600-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="17600-122">ClientIdentities</span></span> |<span data-ttu-id="17600-123">클라이언트-노드 보안을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-123">Configures client-to-node security.</span></span> <span data-ttu-id="17600-124">클라이언트 사용자 계정의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="17600-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="17600-125">ID</span><span class="sxs-lookup"><span data-stu-id="17600-125">Identity</span></span> |<span data-ttu-id="17600-126">클라이언트 ID, 도메인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="17600-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="17600-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="17600-127">IsAdmin</span></span> |<span data-ttu-id="17600-128">도메인 사용자가 관리자 클라이언트 액세스 권한을 갖는 경우 true이며, 사용자 클라이언트 액세스 권한을 갖는 경우 false를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="17600-129">[노드 간 보안](service-fabric-cluster-security.md#node-to-node-security)은 서비스 패브릭이 gMSA에서 실행되어야 하는 경우 **ClustergMSAIdentity**를 설정하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="17600-130">노드 간의 신뢰 관계를 구축하기 위해 서로를 인식하도록 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="17600-131">이 작업은 두 가지 방법으로 수행할 수 있습니다. 클러스터의 모든 노드를 포함하는 그룹 관리 서비스 계정을 지정하거나 클러스터의 모든 노드를 포함하는 도메인 컴퓨터 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="17600-132">특히 노드가 10개보다 많은 대형 클러스터 또는 확장되거나 축소될 수 있는 클러스터의 경우에는 [gMSA(그룹 관리 서비스 계정)](https://technet.microsoft.com/library/hh831782.aspx) 방식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="17600-133">이 접근 방법에서는 클러스터 관리자에게 멤버를 추가하고 제거하는 액세스 권한을 부여하기 위해 도메인 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="17600-134">이러한 계정은 자동 암호 관리에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="17600-135">자세한 내용은 [그룹 관리 서비스 계정 시작](http://technet.microsoft.com/library/jj128431.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="17600-136">[클라이언트 및 노드 간 보안](service-fabric-cluster-security.md#client-to-node-security)은 **ClientIdentities**를 사용하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="17600-137">클라이언트와 클러스터 간에 트러스트를 설정하기 위해 신뢰할 수 있는 클라이언트 ID를 파악하도록 클러스터를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="17600-138">이 작업은 두 가지 방법으로 수행할 수 있습니다. 연결할 수 있는 도메인 그룹 사용자를 지정하거나 연결할 수 있는 도메인 노드 사용자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="17600-139">서비스 패브릭은 서비스 패브릭 클러스터에 연결된 클라이언트에 대해 관리자 및 사용자 액세스 제어 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="17600-140">액세스 제어는 클러스터 관리자가 사용자 그룹마다 특정 형식의 클러스터 작업에 대한 액세스를 제한하는 기능을 제공하여 클러스터의 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="17600-141">관리자는 관리 기능(읽기/쓰기 기능만 포함)에 대한 모든 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="17600-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="17600-142">사용자는 기본적으로 관리 기능(예: 쿼리 기능)에 대한 읽기 권한 및 응용 프로그램과 서비스를 확인하는 기능만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="17600-143">액세스 제어에 대한 자세한 내용은 [Service Fabric 클라이언트의 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="17600-144">다음 예제 **security** 섹션에서는 gMSA를 사용하는 Windows 보안을 구성하고 *ServiceFabric.clusterA.contoso.com* gMSA의 컴퓨터가 클러스터의 일부이며 *CONTOSO\usera*에 관리자 클라이언트 액세스 권한이 있음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="17600-145">컴퓨터 그룹을 사용하여 Windows 보안 구성</span><span class="sxs-lookup"><span data-stu-id="17600-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="17600-146"><seg>
  [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) 독립 실행형 클러스터 패키지와 함께 다운로드된 샘플 *ClusterConfig.Windows.MultiMachine.JSON* 구성 파일은 Windows 보안 구성을 위한 템플릿을 포함합니다.</seg></span><span class="sxs-lookup"><span data-stu-id="17600-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="17600-147">**Properties** 섹션에서 다음과 같이 Windows 보안을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-147">Windows security is configured in the **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="17600-148">**구성 설정**</span><span class="sxs-lookup"><span data-stu-id="17600-148">**Configuration setting**</span></span> | <span data-ttu-id="17600-149">**설명**</span><span class="sxs-lookup"><span data-stu-id="17600-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="17600-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="17600-150">ClusterCredentialType</span></span> |<span data-ttu-id="17600-151">ClusterIdentity가 Active Directory 컴퓨터 그룹 이름을 지정하는 경우 **ClusterCredentialType**은 *Windows*로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="17600-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="17600-152">ServerCredentialType</span></span> |<span data-ttu-id="17600-153">클라이언트에 대해 Windows 보안을 사용하도록 설정하려면 *Windows*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="17600-154">클러스터의 클라이언트와 클러스터 자체를 가리키며 Active Directory 도메인 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="17600-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="17600-155">WindowsIdentities</span></span> |<span data-ttu-id="17600-156">클러스터와 클라이언트 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="17600-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="17600-157">ClusterIdentity</span></span> |<span data-ttu-id="17600-158">컴퓨터 그룹 domain\machinegroup을 사용하여 노드 간 보안을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="17600-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="17600-159">ClientIdentities</span></span> |<span data-ttu-id="17600-160">클라이언트-노드 보안을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-160">Configures client-to-node security.</span></span> <span data-ttu-id="17600-161">클라이언트 사용자 계정의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="17600-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="17600-162">ID</span><span class="sxs-lookup"><span data-stu-id="17600-162">Identity</span></span> |<span data-ttu-id="17600-163">클라이언트 ID로 도메인 사용자인 domain\username을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="17600-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="17600-164">IsAdmin</span></span> |<span data-ttu-id="17600-165">도메인 사용자가 관리자 클라이언트 액세스 권한을 갖는 경우 true로 설정하고, 사용자 클라이언트 액세스 권한을 갖는 경우 false를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="17600-166">Active Directory 도메인 내에서 컴퓨터 그룹을 사용하려는 경우 [노드 간 보안](service-fabric-cluster-security.md#node-to-node-security)은 **ClusterIdentity** 사용을 설정하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="17600-167">자세한 내용은 [Active Directory에 컴퓨터 그룹 만들기](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="17600-168">[클라이언트-노드 간 보안](service-fabric-cluster-security.md#client-to-node-security)은 **ClientIdentities**를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="17600-169">클라이언트와 클러스터 간에 트러스트를 설정하기 위해 클라이언트가 신뢰할 수 있는 클라이언트 ID를 파악하도록 클러스터를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="17600-170">다음 두 가지 방법으로 트러스트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="17600-171">연결할 수 있는 도메인 그룹 사용자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="17600-172">연결할 수 있는 도메인 노드 사용자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="17600-173">서비스 패브릭은 서비스 패브릭 클러스터에 연결된 클라이언트에 대해 관리자 및 사용자 액세스 제어 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="17600-174">액세스 제어는 클러스터 관리자가 사용자 그룹마다 특정 형식의 클러스터 작업에 대한 액세스를 제한할 수 있도록 하여 클러스터의 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="17600-175">관리자는 관리 기능(읽기/쓰기 기능만 포함)에 대한 모든 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="17600-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="17600-176">사용자는 기본적으로 관리 기능(예: 쿼리 기능)에 대한 읽기 권한 및 응용 프로그램과 서비스를 확인하는 기능만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="17600-177">다음 예제 **security** 섹션에서는 Windows 보안을 구성하고 *ServiceFabric/clusterA.contoso.com*의 컴퓨터가 클러스터의 일부이며 *CONTOSO\usera*에 관리자 클라이언트 액세스 권한이 있음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="17600-178">도메인 컨트롤러에 Service Fabric을 배포해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17600-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="17600-179">컴퓨터 그룹 또는 gMSA(그룹 관리 서비스 계정)을 사용할 때 ClusterConfig.json에는 도메인 컨트롤러의 IP 주소가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17600-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="17600-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17600-180">Next steps</span></span>
<span data-ttu-id="17600-181">*ClusterConfig.JSON* 파일에서 Windows 보안을 구성한 후에 [Windows에서 실행되는 독립 실행형 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)에 나와 있는 클러스터 만들기 프로세스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17600-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="17600-182">노드 간 보안, 클라이언트 및 노드 간 보안 및 역할 기반 액세스 제어 방법에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="17600-183">PowerShell 또는 FabricClient를 사용한 연결에 대한 예제는 [보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17600-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
