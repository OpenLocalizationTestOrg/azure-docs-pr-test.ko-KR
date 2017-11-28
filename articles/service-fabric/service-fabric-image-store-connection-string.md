---
title: "서비스 패브릭 이미지 저장소 연결 문자열 aaaAzure | Microsoft Docs"
description: "Hello 이미지 저장소 연결 문자열을 이해"
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
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a><span data-ttu-id="6d49b-103">Hello ImageStoreConnectionString 설정 이해</span><span class="sxs-lookup"><span data-stu-id="6d49b-103">Understand hello ImageStoreConnectionString setting</span></span>

<span data-ttu-id="6d49b-104">설명서의 일부 간략하게 언급 hello 존재 "ImageStoreConnectionString" 매개 변수의 의미를 설명 하지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-104">In some of our documentation, we briefly mention hello existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span></span> <span data-ttu-id="6d49b-105">와 같은 문서가 완료 된 후 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램][10], 하기만 하면 같이 hello 대상의 hello 클러스터 매니페스트에 표시 된 대로 복사/붙여넣기 hello 값은 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste hello value as it appears in hello cluster manifest of hello target cluster.</span></span> <span data-ttu-id="6d49b-106">클러스터당 구성 가능한 hello 설정할 수 있지만 hello 통해 클러스터를 만들 때 [Azure 포털][11], 없습니다 옵션 tooconfigure이 설정 및 해당 항상 "fabric: ImageStore"는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-106">So hello setting must be configurable per cluster, but when you create a cluster through hello [Azure portal][11], there's no option tooconfigure this setting and it's always "fabric:ImageStore".</span></span> <span data-ttu-id="6d49b-107">이 설정은 다음의 hello 목적은 이란?</span><span class="sxs-lookup"><span data-stu-id="6d49b-107">What's hello purpose of this setting then?</span></span>

![클러스터 매니페스트][img_cm]

<span data-ttu-id="6d49b-109">서비스 패브릭 내부 Microsoft 소비 하기 위한 플랫폼으로 의해 시작 많은 다양 한 팀의 일부 측면은 고도로 사용자 지정 가능한-hello "Image Store"는 이러한 한 가지 측면인 하므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - hello "Image Store" is one such aspect.</span></span> <span data-ttu-id="6d49b-110">기본적으로, hello 이미지 저장소는 응용 프로그램 패키지를 저장 하기 위한 플러그형 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-110">Essentially, hello Image Store is a pluggable repository for storing application packages.</span></span> <span data-ttu-id="6d49b-111">Hello 클러스터의 노드에 배포 된 tooa 응용 프로그램을 사용 하는 경우 해당 노드는 응용 프로그램 패키지의 hello 내용을 hello 이미지 저장소에서에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-111">When your application is deployed tooa node in hello cluster, that node downloads hello contents of your application package from hello Image Store.</span></span> <span data-ttu-id="6d49b-112">hello ImageStoreConnectionString은 클라이언트와 노드 toofind hello 올바른 이미지 저장소에 지정된 된 클러스터에 대 한 모든 hello 필요한 정보를 포함 하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-112">hello ImageStoreConnectionString is a setting that includes all hello necessary information for both clients and nodes toofind hello correct Image Store for a given cluster.</span></span>

<span data-ttu-id="6d49b-113">현재 세 가지 종류의 가능한 이미지 저장소 공급자가 있고 해당하는 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span></span>

1. <span data-ttu-id="6d49b-114">이미지 저장소 서비스: "fabric:ImageStore"</span><span class="sxs-lookup"><span data-stu-id="6d49b-114">Image Store Service: "fabric:ImageStore"</span></span>

2. <span data-ttu-id="6d49b-115">파일 시스템: "file:[file system path]"</span><span class="sxs-lookup"><span data-stu-id="6d49b-115">File System: "file:[file system path]"</span></span>

3. <span data-ttu-id="6d49b-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span><span class="sxs-lookup"><span data-stu-id="6d49b-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span></span>

<span data-ttu-id="6d49b-117">프로덕션 환경에서 사용 하는 hello 공급자 유형은 hello 이미지 저장소 서비스를 상태 저장 지속형된 시스템 서비스는 서비스 패브릭 탐색기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-117">hello provider type used in production is hello Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span></span> 

![이미지 저장소 서비스][img_is]

<span data-ttu-id="6d49b-119">Hello 패키지 저장소에 대 한 외부 종속성을 제거 하 고 hello 집약성이 저장소를 보다 상세하게 제공 하는 hello 클러스터 자체 내에서 시스템 서비스에서 호스팅 hello 이미지 저장소.</span><span class="sxs-lookup"><span data-stu-id="6d49b-119">Hosting hello Image Store in a system service within hello cluster itself eliminates external dependencies for hello package repository and gives us more control over hello locality of storage.</span></span> <span data-ttu-id="6d49b-120">Hello 이미지 저장소 주위 향후 개선 사항도 하지 않은 경우 단독으로 가능성이 tootarget hello 이미지 저장소 공급자를 먼저는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-120">Future improvements around hello Image Store are likely tootarget hello Image Store provider first, if not exclusively.</span></span> <span data-ttu-id="6d49b-121">hello 이미지 저장소 서비스 공급자에 대 한 연결 문자열 hello hello 클라이언트는 이미 연결 된 toohello 대상 클러스터 고유 정보가 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-121">hello connection string for hello Image Store Service provider doesn't have any unique information since hello client is already connected toohello target cluster.</span></span> <span data-ttu-id="6d49b-122">클라이언트 hello는 hello 시스템 서비스를 대상으로 하는 프로토콜을 사용 해야 함을 tooknow만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-122">hello client only needs tooknow that protocols targeting hello system service should be used.</span></span>

<span data-ttu-id="6d49b-123">hello 파일 시스템 공급자 대신 사용 됩니다 hello 이미지 저장소 서비스가 로컬 하나 상자 클러스터에 대 한 개발 toobootstrap hello 클러스터 하는 동안 약간 더 빠르게.</span><span class="sxs-lookup"><span data-stu-id="6d49b-123">hello File System provider is used instead of hello Image Store Service for local one-box clusters during development toobootstrap hello cluster slightly faster.</span></span> <span data-ttu-id="6d49b-124">hello 차이점은 일반적으로 짧지만 이지만 개발 하는 동안 대부분 사람들에 대 한 유용한 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-124">hello difference is typically small, but it's a useful optimization for most folks during development.</span></span> <span data-ttu-id="6d49b-125">가능한 toodeploy 인 클러스터를 로컬 하나 상자도 다른 저장소 공급자 유형을 hello 하지만 없는 이유는 일반적으로 toodo 하므로 hello 개발/테스트 워크플로 하 게 유지 되므로 hello 동일한 공급자에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-125">It's possible toodeploy a local one-box cluster with hello other storage provider types as well, but there's usually no reason toodo so since hello develop/test workflow remains hello same regardless of provider.</span></span> <span data-ttu-id="6d49b-126">이 사용법 이외의 hello Azure 저장소 및 파일 시스템 공급자만 레거시 지원에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-126">Other than this usage, hello File System and Azure Storage providers only exist for legacy support.</span></span>

<span data-ttu-id="6d49b-127">따라서 hello ImageStoreConnectionString 구성 가능한 이지만, 일반적으로 방금 hello 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-127">So while hello ImageStoreConnectionString is configurable, you generally just use hello default setting.</span></span> <span data-ttu-id="6d49b-128">TooAzure를 통해 게시할 때 [Visual Studio][12], hello 매개 변수는 자동으로 설정 하면 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-128">When publishing tooAzure through [Visual Studio][12], hello parameter is automatically set for you accordingly.</span></span> <span data-ttu-id="6d49b-129">Azure에서 호스트 되는 프로그래밍 방식 배포를 tooclusters, hello 연결 문자열은 항상 "fabric: ImageStore"입니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-129">For programmatic deployment tooclusters hosted in Azure, hello connection string is always "fabric:ImageStore".</span></span> <span data-ttu-id="6d49b-130">의문이 있는 경우 해당 값 항상 확인할 수 있습니다 하 여 hello 클러스터 매니페스트를 검색 하 여 있지만 [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), 또는 [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-130">Though when in doubt, its value can always be verified by retrieving hello cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span></span> <span data-ttu-id="6d49b-131">온-프레미스 테스트 및 프로덕션 클러스터에서 구성 된 toouse hello 이미지 저장소 서비스 공급자도 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d49b-131">Both on-premises test and production clusters should always be configured toouse hello Image Store Service provider as well.</span></span>

### <a name="next-steps"></a><span data-ttu-id="6d49b-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d49b-132">Next steps</span></span>
<span data-ttu-id="6d49b-133">[PowerShell을 사용하여 응용 프로그램 배포 및 제거][10]</span><span class="sxs-lookup"><span data-stu-id="6d49b-133">[Deploy and remove applications using PowerShell][10]</span></span>

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
