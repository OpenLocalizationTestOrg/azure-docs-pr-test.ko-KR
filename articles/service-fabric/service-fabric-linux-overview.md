---
title: "Linux의 Azure Service Fabric | Microsoft Docs"
description: "Service Fabric 클러스터는 Linux 및 Java를 지원하므로 Linux에서 Java 및 C#으로 작성된 Service Fabric 응용 프로그램을 배포 및 호스트할 수 있습니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="9f4cd-103">Linux의 서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="9f4cd-103">Service Fabric on Linux</span></span>
<span data-ttu-id="9f4cd-104">Linux의 서비스 패브릭 미리 보기를 사용하면 Windows에서와 마찬가지로 Linux에서도 서비스 패브릭을 통해 해당 환경에서 가용성 및 확장성이 뛰어난 응용 프로그램을 빌드, 배포 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="9f4cd-105">Service Fabric 프레임워크(Reliable Services 및 Reliable Actors) 는 C#(.NET Core) 뿐만 아니라 Linux의 Java로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="9f4cd-106">어떤 언어 또는 프레임워크에서도 [게스트 실행 서비스](service-fabric-deploy-existing-app.md) 를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="9f4cd-107">또한, 미리 보기는 Docker 컨테이너 오케스트레이션도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="9f4cd-108">Docker 컨테이너는 게스트 실행 파일 또는 Service Fabric 프레임워크를 사용하는 네이티브 Service Fabric 서비스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="9f4cd-109">Linux의 서비스 패브릭은 Windows의 서비스 패브릭과 개념적으로 동일합니다(OS 사양 및 프로그래밍 언어 지원 제외).</span><span class="sxs-lookup"><span data-stu-id="9f4cd-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="9f4cd-110">따라서 대부분의 [기존 설명서](http://aka.ms/servicefabricdocs) 를 통해 이 기술을 익힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="9f4cd-111">지원되는 운영 체제 및 프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="9f4cd-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="9f4cd-112">제한된 미리 보기에서는 Ubuntu Server 16.04를 실행하는 Azure에서 통합 개발 클러스터 및 다중 컴퓨터 클러스터 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="9f4cd-113">미리 보기는 게스트 실행 파일뿐만 아니라 Java 및 C#으로 작성된 Reliable Actors 및 Reliable Stateless Services 프레임워크를 지원하며 Docker 컨테이너 오케스트레이션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="9f4cd-114">신뢰할 수 있는 컬렉션은 Linux에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="9f4cd-115">독립 실행형 클러스터 역시 지원 되지 않습니다 미리 보기에서는 one box 및 Azure Linux 다중 컴퓨터 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="9f4cd-116">지원되는 도구</span><span class="sxs-lookup"><span data-stu-id="9f4cd-116">Supported tooling</span></span>
<span data-ttu-id="9f4cd-117">미리 보기는 Service Fabric CLI를 통해 클러스터와의 상호 작용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="9f4cd-118">Java 개발자를 위해 Linux 및 OSX에서 지원되는 Eclipse에 Eclipse 및 Yeoman과의 통합이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="9f4cd-119">OSX 통합은 Vagrant를 통해 내부에서 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="9f4cd-120">C# 개발자를 위해 Yeoman과의 통합이 응용 프로그램 템플릿을 생성하도록 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f4cd-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f4cd-121">Next steps</span></span>

* <span data-ttu-id="9f4cd-122">[Reliable Actors](service-fabric-reliable-actors-introduction.md) 및 [Reliable Services](service-fabric-reliable-services-introduction.md) 프로그래밍 프레임워크에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f4cd-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="9f4cd-123">Linux에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="9f4cd-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="9f4cd-124">OSX에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="9f4cd-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="9f4cd-125">Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9f4cd-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="9f4cd-126">Jenkins 및 GitHub로 Setup Service Fabric 연속 통합 및 배포 설정</span><span class="sxs-lookup"><span data-stu-id="9f4cd-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="9f4cd-127">Service Fabric Windows/Linux 간 차이점</span><span class="sxs-lookup"><span data-stu-id="9f4cd-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
