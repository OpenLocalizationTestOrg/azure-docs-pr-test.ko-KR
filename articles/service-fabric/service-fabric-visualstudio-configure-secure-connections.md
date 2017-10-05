---
title: "안전한 Azure Service Fabric 클러스터 연결 구성 | Microsoft Docs"
description: "Visual Studio를 사용하여 Azure 서비스 패브릭 클러스터에서 지원하는 보안 연결을 구성하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: dc07b2f38d6fd2de941ebbe99303f6e63cbf122d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-connections-to-a-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="1e260-103">Visual Studio에서 서비스 패브릭 클러스터에 대한 보안 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1e260-103">Configure secure connections to a Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="1e260-104">액세스 제어 정책이 구성되어 있는 Azure 서비스 패브릭 클러스터에 안전하게 액세스하기 위해 Visual Studio를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-104">Learn how to use Visual Studio to securely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="1e260-105">클러스터 연결 유형</span><span class="sxs-lookup"><span data-stu-id="1e260-105">Cluster connection types</span></span>
<span data-ttu-id="1e260-106">Azure Service Fabric 클러스터에서 지원되는 2가지 연결 형식: **비보안** 연결과 **x509 인증서 기반** 보안 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-106">Two types of connections are supported by the Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="1e260-107">(온-프레미스에 호스트된 Service Fabric 클러스터의 경우 **Windows** 및 **dSTS** 인증도 지원됩니다.) 클러스터를 만들 때 클러스터 연결 형식을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have to configure the cluster connection type when the cluster is being created.</span></span> <span data-ttu-id="1e260-108">만든 후에는 연결 형식을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-108">Once it's created, the connection type can’t be changed.</span></span>

<span data-ttu-id="1e260-109">Visual Studio 서비스 패브릭 도구는 게시할 클러스터에 연결하기 위한 모든 인증 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-109">The Visual Studio Service Fabric tools support all authentication types for connecting to a cluster for publishing.</span></span> <span data-ttu-id="1e260-110">보안 서비스 패브릭 클러스터를 설정하는 방법에 대한 지침은 [Azure Portal에서 서비스 패브릭 클러스터 설정](service-fabric-cluster-creation-via-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e260-110">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how to set up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="1e260-111">게시 프로필에서 클러스터 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1e260-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="1e260-112">Visual Studio에서 Service Fabric 프로젝트를 게시하는 경우 **Service Fabric 응용 프로그램 게시** 대화 상자에서 Azure Service Fabric 클러스터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-112">If you publish a Service Fabric project from Visual Studio, use the **Publish Service Fabric Application** dialog box to choose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="1e260-113">**연결 끝점** 아래의 해당 구독에서 기존 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![**Service Fabric 응용 프로그램 게시** 대화 상자를 사용하여 Service Fabric 연결을 구성합니다.][publishdialog]

<span data-ttu-id="1e260-115">**Service Fabric Cluster 선택** 대화 상자에서 자동으로 클러스터 연결의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-115">The **Publish Service Fabric Application** dialog box automatically validates the cluster connection.</span></span> <span data-ttu-id="1e260-116">메시지가 표시되면 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-116">If prompted, sign in to your Azure account.</span></span> <span data-ttu-id="1e260-117">유효성 검사에 통과하면 시스템에 클러스터를 안전하게 연결하기 위한 올바른 인증서가 설치되어 있거나 클러스터가 비보안이라는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-117">If validation passes, it means that your system has the correct certificates installed to connect to the cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="1e260-118">네트워크 문제가 있거나 시스템이 보안 클러스터에 연결하도록 올바르게 구성되지 않으면 유효성 검사가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-118">Validation failures can be caused by network issues or by not having your system correctly configured to connect to a secure cluster.</span></span>

![**Service Fabric 응용 프로그램 게시** 대화 상자가 기존의 정확히 구성된 Service Fabric 클러스터 연결의 유효성을 검사합니다.][selectsfcluster]

### <a name="to-connect-to-a-secure-cluster"></a><span data-ttu-id="1e260-120">보안 클러스터에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="1e260-120">To connect to a secure cluster</span></span>
1. <span data-ttu-id="1e260-121">대상 클러스터에서 신뢰하는 클라이언트 인증서 중 하나에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-121">Make sure you can access one of the client certificates that the destination cluster trusts.</span></span> <span data-ttu-id="1e260-122">인증서는 일반적으로 개인 정보 교환(.pfx) 파일로 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-122">The certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="1e260-123">클라이언트에 액세스를 허용하도록 서버를 구성하는 방법은 [Azure Portal에서 서비스 패브릭 클러스터 설정](service-fabric-cluster-creation-via-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e260-123">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for how to configure the server to grant access to a client.</span></span>
2. <span data-ttu-id="1e260-124">신뢰할 수 있는 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-124">Install the trusted certificate.</span></span> <span data-ttu-id="1e260-125">이를 위해 .pfx 파일을 두 번 클릭하거나 PowerShell 스크립트 Import-PfxCertificate를 사용하여 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-125">To do this, double-click the .pfx file, or use the PowerShell script Import-PfxCertificate to import the certificates.</span></span> <span data-ttu-id="1e260-126">인증서를 **Cert:\LocalMachine\My**에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-126">Install the certificate to **Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="1e260-127">인증서를 가져오는 동안 모든 기본 설정을 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-127">It's OK to accept all default settings while importing the certificate.</span></span>
3. <span data-ttu-id="1e260-128">프로젝트의 바로 가기 메뉴에서 **게시...** 명령을 선택하여 **Azure 응용 프로그램 게시** 대화 상자를 연 다음 대상 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-128">Choose the **Publish...** command on the shortcut menu of the project to open the **Publish Azure Application** dialog box and then select the target cluster.</span></span> <span data-ttu-id="1e260-129">도구가 자동으로 연결을 확인한 다음 게시 프로필에 보안 연결 매개 변수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-129">The tool automatically resolves the connection and saves the secure connection parameters in the publish profile.</span></span>
4. <span data-ttu-id="1e260-130">선택 사항: 게시 프로필을 편집하여 보안 클러스터 연결을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-130">Optional: You can edit the publish profile to specify a secure cluster connection.</span></span>
   
   <span data-ttu-id="1e260-131">게시 프로필 XML 파일을 수동으로 편집하여 인증서 정보를 지정하므로 인증서 저장소 이름, 저장소 위치 및 인증서 지문을 적어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-131">Since you're manually editing the Publish Profile XML file to specify the certificate information, be sure to note the certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="1e260-132">인증서 저장소 이름 및 저장소 위치에 이러한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-132">You'll need to provide these values for the certificate's store name and store location.</span></span> <span data-ttu-id="1e260-133">자세한 내용은 [방법: 인증서의 지문 검색](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e260-133">See [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="1e260-134">*ClusterConnectionParameters* 매개 변수를 사용하여 서비스 패브릭 클러스터에 연결할 때 사용할 PowerShell 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-134">You can use the *ClusterConnectionParameters* parameters to specify the PowerShell parameters to use when connecting to the Service Fabric cluster.</span></span> <span data-ttu-id="1e260-135">유효한 매개 변수는 Connect-ServiceFabricCluster cmdlet에서 허용하는 모든 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-135">Valid parameters are any that are accepted by the Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="1e260-136">사용 가능한 매개 변수 목록은 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e260-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="1e260-137">원격 클러스터에 게시하는 경우 해당 특정 클러스터에 적절한 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-137">If you’re publishing to a remote cluster, you need to specify the appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="1e260-138">다음은 비보안 클러스터에 연결하기 위한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-138">The following is an example of connecting to a non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="1e260-139">다음은 x509 인증서 기반 보안 클러스터에 연결하기 위한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-139">Here’s an example for connecting to an x509 certificate-based secure cluster:</span></span>
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. <span data-ttu-id="1e260-140">업그레이드 매개 변수 및 응용 프로그램 매개 변수 파일 위치와 같이 필요한 다른 설정을 편집한 다음 Visual Studio의 **서비스 패브릭 응용 프로그램 게시** 대화 상자에서 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1e260-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from the **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e260-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e260-141">Next steps</span></span>
<span data-ttu-id="1e260-142">서비스 패브릭 클러스터에 액세스하는 방법에 대한 자세한 내용은 [서비스 패브릭 탐색기를 사용하여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e260-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
