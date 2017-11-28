---
title: "aaaConfigure Azure 서비스 패브릭 클러스터 연결의 보안 | Microsoft Docs"
description: "Visual Studio tooconfigure toouse hello Azure 서비스 패브릭 클러스터에서 지원 되는 연결의 보안 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="63fd1-103">Visual Studio에서 보안 연결 tooa 서비스 패브릭 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-103">Configure secure connections tooa Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="63fd1-104">Visual Studio toosecurely toouse 구성 된 액세스 제어 정책을 사용 하 여 Azure 서비스 패브릭 클러스터에 액세스 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-104">Learn how toouse Visual Studio toosecurely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="63fd1-105">클러스터 연결 유형</span><span class="sxs-lookup"><span data-stu-id="63fd1-105">Cluster connection types</span></span>
<span data-ttu-id="63fd1-106">두 가지 유형의 연결 hello Azure 서비스 패브릭 클러스터에 의해 지원 됩니다: **비보안** 연결 및 **x509 인증서 기반** 연결 보안을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-106">Two types of connections are supported by hello Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="63fd1-107">(온-프레미스에 호스트된 Service Fabric 클러스터의 경우 **Windows** 및 **dSTS** 인증도 지원됩니다.) Hello 클러스터를 만드는 중 tooconfigure hello 클러스터 연결 유형을 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have tooconfigure hello cluster connection type when hello cluster is being created.</span></span> <span data-ttu-id="63fd1-108">카탈로그 항목이 생성 되 면 hello 연결 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-108">Once it's created, hello connection type can’t be changed.</span></span>

<span data-ttu-id="63fd1-109">hello Visual Studio 서비스 패브릭 도구에는 게시에 대 한 연결 tooa 클러스터에 대 한 모든 인증 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-109">hello Visual Studio Service Fabric tools support all authentication types for connecting tooa cluster for publishing.</span></span> <span data-ttu-id="63fd1-110">참조 [hello Azure 포털에서에서 서비스 패브릭 클러스터를 설정할](service-fabric-cluster-creation-via-portal.md) 방법에 대 한 보안 서비스 패브릭 클러스터를 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-110">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how tooset up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="63fd1-111">게시 프로필에서 클러스터 연결 구성</span><span class="sxs-lookup"><span data-stu-id="63fd1-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="63fd1-112">Hello를 사용 하 여 Visual Studio에서 서비스 패브릭 프로젝트를 게시 하면 **서비스 패브릭 응용 프로그램 게시** 대화 상자 toochoose Azure 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-112">If you publish a Service Fabric project from Visual Studio, use hello **Publish Service Fabric Application** dialog box toochoose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="63fd1-113">**연결 끝점** 아래의 해당 구독에서 기존 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![hello * * 게시 서비스 패브릭 응용 프로그램 * * 대화 상자를 사용 하는 tooconfigure 서비스 패브릭 연결 합니다.][publishdialog]

<span data-ttu-id="63fd1-115">hello **서비스 패브릭 응용 프로그램 게시** hello 클러스터 연결 대화 상자를 자동으로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-115">hello **Publish Service Fabric Application** dialog box automatically validates hello cluster connection.</span></span> <span data-ttu-id="63fd1-116">메시지가 표시 되 면 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-116">If prompted, sign in tooyour Azure account.</span></span> <span data-ttu-id="63fd1-117">유효성 검사에 통과 하는 경우 시스템에 올바른 인증서를 안전 하 게 tooconnect toohello 클러스터를 설치 하거나 클러스터는 안전 하지 않은 hello를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-117">If validation passes, it means that your system has hello correct certificates installed tooconnect toohello cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="63fd1-118">유효성 검사에 실패 하지 않아서 잘못 구성 된 시스템 tooconnect tooa 보안 클러스터 또는 네트워크 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-118">Validation failures can be caused by network issues or by not having your system correctly configured tooconnect tooa secure cluster.</span></span>

![hello * * 게시 서비스 패브릭 응용 프로그램 * * 대화 상자는 기존 유효성을 검사 올바르게 구성 된 서비스 패브릭 클러스터를 연결 합니다.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a><span data-ttu-id="63fd1-120">tooconnect tooa 보안 클러스터</span><span class="sxs-lookup"><span data-stu-id="63fd1-120">tooconnect tooa secure cluster</span></span>
1. <span data-ttu-id="63fd1-121">대상 클러스터 트러스트 hello hello 클라이언트 인증서 중 하나에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-121">Make sure you can access one of hello client certificates that hello destination cluster trusts.</span></span> <span data-ttu-id="63fd1-122">hello 인증서는 일반적으로 개인 정보 교환 (.pfx) 파일로 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-122">hello certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="63fd1-123">참조 [hello Azure 포털에서에서 서비스 패브릭 클러스터를 설정할](service-fabric-cluster-creation-via-portal.md) tooconfigure hello 서버 toogrant tooa 클라이언트를 액세스 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-123">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for how tooconfigure hello server toogrant access tooa client.</span></span>
2. <span data-ttu-id="63fd1-124">Hello 신뢰할 수 있는 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-124">Install hello trusted certificate.</span></span> <span data-ttu-id="63fd1-125">toodo hello.pfx 파일을 두 번이, 또는 hello PowerShell 스크립트 Import-pfxcertificate tooimport hello 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-125">toodo this, double-click hello .pfx file, or use hello PowerShell script Import-PfxCertificate tooimport hello certificates.</span></span> <span data-ttu-id="63fd1-126">너무 hello 인증서 설치**Cert: \LocalMachine\My**합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-126">Install hello certificate too**Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="63fd1-127">확인 tooaccept는 hello 인증서를 가져오는 동안 모든 기본 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-127">It's OK tooaccept all default settings while importing hello certificate.</span></span>
3. <span data-ttu-id="63fd1-128">Hello 선택 **게시...**  hello 프로젝트 tooopen hello hello 바로 가기 메뉴에서 명령을 **Azure 응용 프로그램 게시** 대화 상자와 대상 클러스터를 선택한 후 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-128">Choose hello **Publish...** command on hello shortcut menu of hello project tooopen hello **Publish Azure Application** dialog box and then select hello target cluster.</span></span> <span data-ttu-id="63fd1-129">hello 도구는 자동으로 hello 연결을 확인 하 고 hello 보안 연결 hello에 대 한 매개 변수 게시 프로필을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-129">hello tool automatically resolves hello connection and saves hello secure connection parameters in hello publish profile.</span></span>
4. <span data-ttu-id="63fd1-130">선택 사항: hello 편집할 수 있습니다 게시 프로필 toospecify 보안 클러스터 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-130">Optional: You can edit hello publish profile toospecify a secure cluster connection.</span></span>
   
   <span data-ttu-id="63fd1-131">Hello 게시 프로필 XML 파일 toospecify hello 인증서 정보를 수동으로 편집 하 수 있는지 toonote hello 인증서 저장소 이름, 저장소, 위치 및 인증서 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-131">Since you're manually editing hello Publish Profile XML file toospecify hello certificate information, be sure toonote hello certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="63fd1-132">Tooprovide hello 인증서 저장소에 대 한 이러한 값 이름을 지정 하 고 위치를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-132">You'll need tooprovide these values for hello certificate's store name and store location.</span></span> <span data-ttu-id="63fd1-133">참조 [하는 방법: 인증서의 지문 검색 hello](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-133">See [How to: Retrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="63fd1-134">Hello를 사용할 수 있습니다 *ClusterConnectionParameters* 매개 변수 toospecify hello PowerShell 매개 변수 toouse toohello 서비스 패브릭 클러스터를 연결할 때.</span><span class="sxs-lookup"><span data-stu-id="63fd1-134">You can use hello *ClusterConnectionParameters* parameters toospecify hello PowerShell parameters toouse when connecting toohello Service Fabric cluster.</span></span> <span data-ttu-id="63fd1-135">유효한 매개 변수는 해당 하는 hello Connect-servicefabriccluster cmdlet에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-135">Valid parameters are any that are accepted by hello Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="63fd1-136">사용 가능한 매개 변수 목록은 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63fd1-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="63fd1-137">원격 클러스터 tooa, 게시 하려는 경우 해당 클러스터 toospecify hello 적절 한 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-137">If you’re publishing tooa remote cluster, you need toospecify hello appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="63fd1-138">hello 다음은 연결 tooa 안전 하지 않은 클러스터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-138">hello following is an example of connecting tooa non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="63fd1-139">연결 tooan x509 인증서 기반 보안 클러스터 포함에 대 한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63fd1-139">Here’s an example for connecting tooan x509 certificate-based secure cluster:</span></span>
   
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
5. <span data-ttu-id="63fd1-140">모든 필요한 등의 설정은 업그레이드 매개 변수 및 응용 프로그램 매개 변수 파일 위치를 편집 하 고 다음 hello에서 응용 프로그램을 게시할 **서비스 패브릭 응용 프로그램 게시** Visual Studio에서 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="63fd1-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from hello **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63fd1-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63fd1-141">Next steps</span></span>
<span data-ttu-id="63fd1-142">서비스 패브릭 클러스터에 액세스하는 방법에 대한 자세한 내용은 [서비스 패브릭 탐색기를 사용하여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63fd1-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
