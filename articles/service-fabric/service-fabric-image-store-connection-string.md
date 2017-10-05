---
title: "Azure Service Fabric 이미지 저장소 연결 문자열 | Microsoft Docs"
description: "이미지 저장소 연결 문자열 이해"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: f497006a8ba48da0032b82113702d8014952ca20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="understand-the-imagestoreconnectionstring-setting"></a><span data-ttu-id="cfd3e-103">ImageStoreConnectionString 설정 이해</span><span class="sxs-lookup"><span data-stu-id="cfd3e-103">Understand the ImageStoreConnectionString setting</span></span>

<span data-ttu-id="cfd3e-104">일부 문서에서 의미를 설명하지 않고 "ImageStoreConnectionString"라는 매개 변수가 있는지 간단하게 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-104">In some of our documentation, we briefly mention the existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span></span> <span data-ttu-id="cfd3e-105">[PowerShell을 사용하여 응용 프로그램 배포 및 제거][10]와 같은 문서를 완료한 후에 대상 클러스터의 클러스터 매니페스트에 표시된 대로 값을 복사/붙여넣기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste the value as it appears in the cluster manifest of the target cluster.</span></span> <span data-ttu-id="cfd3e-106">따라서 설정은 클러스터당 구성될 수 있지만 [Azure Portal][11]을 통해 클러스터를 만드는 경우 이 설정을 구성하는 옵션이 없고 "fabric:ImageStore"은 항상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-106">So the setting must be configurable per cluster, but when you create a cluster through the [Azure portal][11], there's no option to configure this setting and it's always "fabric:ImageStore".</span></span> <span data-ttu-id="cfd3e-107">이 설정의 용도는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cfd3e-107">What's the purpose of this setting then?</span></span>

![클러스터 매니페스트][img_cm]

<span data-ttu-id="cfd3e-109">Service Fabric은 다양한 팀에서 내부 Microsoft 사용을 위한 플랫폼으로 시작되었습니다. 따라서 "이미지 저장소"와 같은 일부 측면은 자유롭게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - the "Image Store" is one such aspect.</span></span> <span data-ttu-id="cfd3e-110">기본적으로, 이미지 저장소는 응용 프로그램 패키지를 저장하기 위한 플러그형 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-110">Essentially, the Image Store is a pluggable repository for storing application packages.</span></span> <span data-ttu-id="cfd3e-111">응용 프로그램을 클러스터의 노드에 배포할 경우 해당 노드는 이미지 저장소에서 응용 프로그램 패키지의 콘텐츠를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-111">When your application is deployed to a node in the cluster, that node downloads the contents of your application package from the Image Store.</span></span> <span data-ttu-id="cfd3e-112">ImageStoreConnectionString은 클라이언트와 노드 모두에 필요한 정보를 모두 포함하는 설정으로 지정된 클러스터에 대한 올바른 이미지 저장소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-112">The ImageStoreConnectionString is a setting that includes all the necessary information for both clients and nodes to find the correct Image Store for a given cluster.</span></span>

<span data-ttu-id="cfd3e-113">현재 세 가지 종류의 가능한 이미지 저장소 공급자가 있고 해당하는 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span></span>

1. <span data-ttu-id="cfd3e-114">이미지 저장소 서비스: "fabric:ImageStore"</span><span class="sxs-lookup"><span data-stu-id="cfd3e-114">Image Store Service: "fabric:ImageStore"</span></span>

2. <span data-ttu-id="cfd3e-115">파일 시스템: "file:[file system path]"</span><span class="sxs-lookup"><span data-stu-id="cfd3e-115">File System: "file:[file system path]"</span></span>

3. <span data-ttu-id="cfd3e-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span><span class="sxs-lookup"><span data-stu-id="cfd3e-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span></span>

<span data-ttu-id="cfd3e-117">프로덕션에 사용되는 공급자 유형은 이미지 저장소 서비스이며 Service Fabric Explorer에서 확인할 수 있는 지속형 상태 저장 시스템 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-117">The provider type used in production is the Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span></span> 

![이미지 저장소 서비스][img_is]

<span data-ttu-id="cfd3e-119">클러스터 자체 내의 시스템 서비스에서 이미지 저장소를 호스팅하면 패키지 리포지토리에 대한 외부 종속성을 제거하고 저장소의 위치를 제어할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-119">Hosting the Image Store in a system service within the cluster itself eliminates external dependencies for the package repository and gives us more control over the locality of storage.</span></span> <span data-ttu-id="cfd3e-120">단독으로 그렇지 않으면 이미지 저장소에 대한 향후 개선은 먼저 이미지 저장소 공급자를 대상으로 할 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-120">Future improvements around the Image Store are likely to target the Image Store provider first, if not exclusively.</span></span> <span data-ttu-id="cfd3e-121">클라이언트가 대상 클러스터에 이미 연결되어 있으므로 이미지 저장소 서비스 공급자에 대한 연결 문자열에는 고유한 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-121">The connection string for the Image Store Service provider doesn't have any unique information since the client is already connected to the target cluster.</span></span> <span data-ttu-id="cfd3e-122">클라이언트는 시스템 서비스를 대상으로 하는 프로토콜을 사용해야 함을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-122">The client only needs to know that protocols targeting the system service should be used.</span></span>

<span data-ttu-id="cfd3e-123">개발 중에 one-box 로컬 클러스터에 이미지 저장소 서비스가 아닌 파일 시스템 공급자를 사용하여 클러스터를 약간 더 빠르게 부트스트랩합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-123">The File System provider is used instead of the Image Store Service for local one-box clusters during development to bootstrap the cluster slightly faster.</span></span> <span data-ttu-id="cfd3e-124">차이점은 일반적으로 작지만 개발 중인 사용자 대부분에게 유용한 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-124">The difference is typically small, but it's a useful optimization for most folks during development.</span></span> <span data-ttu-id="cfd3e-125">다른 저장소 공급자 유형도 one-box 로컬 클러스터를 배포할 수 있지만 개발/테스트 워크플로가 공급자에 관계 없이 동일하게 유지되기 때문에 일반적으로 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-125">It's possible to deploy a local one-box cluster with the other storage provider types as well, but there's usually no reason to do so since the develop/test workflow remains the same regardless of provider.</span></span> <span data-ttu-id="cfd3e-126">이 사용법 이외에 파일 시스템 및 Azure Storage 공급자는 레거시 지원을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-126">Other than this usage, the File System and Azure Storage providers only exist for legacy support.</span></span>

<span data-ttu-id="cfd3e-127">따라서 ImageStoreConnectionString을 구성 가능하지만 일반적으로 기본 설정만을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-127">So while the ImageStoreConnectionString is configurable, you generally just use the default setting.</span></span> <span data-ttu-id="cfd3e-128">[Visual Studio][12]를 통해 Azure에 게시할 경우 매개 변수가 적절하게 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-128">When publishing to Azure through [Visual Studio][12], the parameter is automatically set for you accordingly.</span></span> <span data-ttu-id="cfd3e-129">Azure에서 호스트된 클러스터에 프로그래밍 방식으로 배포하는 경우 연결 문자열은 항상 "fabric:ImageStore"입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-129">For programmatic deployment to clusters hosted in Azure, the connection string is always "fabric:ImageStore".</span></span> <span data-ttu-id="cfd3e-130">확실하지 않은 경우에도 [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx) 또는 [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest)에서 클러스터 매니페스트를 검색하여 해당 값을 언제든지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-130">Though when in doubt, its value can always be verified by retrieving the cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span></span> <span data-ttu-id="cfd3e-131">온-프레미스 테스트 및 프로덕션 클러스터는 모두 항상 이미지 저장소 서비스 공급자를 사용하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd3e-131">Both on-premises test and production clusters should always be configured to use the Image Store Service provider as well.</span></span>

### <a name="next-steps"></a><span data-ttu-id="cfd3e-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfd3e-132">Next steps</span></span>
<span data-ttu-id="cfd3e-133">[PowerShell을 사용하여 응용 프로그램 배포 및 제거][10]</span><span class="sxs-lookup"><span data-stu-id="cfd3e-133">[Deploy and remove applications using PowerShell][10]</span></span>

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
