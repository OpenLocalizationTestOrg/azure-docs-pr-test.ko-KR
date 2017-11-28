---
title: "Azure 아키텍처 디자인에 aaaIntegrate 보안 | Microsoft Docs"
description: " 이 문서에 Azure toomake hello 응용 프로그램 및 서비스 아키텍처를 이해 하는 데 도움이 됩니다 것 디자인 및 구현에 보다 쉽게 toointegrate 보안 합니다. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="915b3-103">Azure 상의 응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="915b3-103">Application architecture on Azure</span></span>
<span data-ttu-id="915b3-104">toohelp 강력한 아키텍처 foundation은 중요 한 Microsoft Azure에서 클라우드 기반 솔루션을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="915b3-105">설계자, 디자이너 및 구현자는 모두 응용 프로그램 및 서비스 아키텍처의 풍부한 지식을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="915b3-106">이 기본 기술 자료를 사용 하면 클라우드 기반 솔루션의 모든 hello 구성 요소를 이해 하 고 디자인 및 구현 하는 모든 정보를 보다 쉽게 toointegrate 보안을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="915b3-107">우리는 안녕하세요 toohelp 다음 조사 아키텍처 및 디자인:</span><span class="sxs-lookup"><span data-stu-id="915b3-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="915b3-108">아키텍처 Infographics</span><span class="sxs-lookup"><span data-stu-id="915b3-108">Architectural infographics</span></span>
* <span data-ttu-id="915b3-109">아키텍처 청사진</span><span class="sxs-lookup"><span data-stu-id="915b3-109">Architectural blueprints</span></span>
* <span data-ttu-id="915b3-110">클라우드 및 엔터프라이즈 기호 집합</span><span class="sxs-lookup"><span data-stu-id="915b3-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="915b3-111">3D 청사진 Visio 템플릿</span><span class="sxs-lookup"><span data-stu-id="915b3-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="915b3-112">아키텍처 Infographics</span><span class="sxs-lookup"><span data-stu-id="915b3-112">Architectural infographics</span></span>
<span data-ttu-id="915b3-113">Microsoft에서는 포스터/Infographics 관련 아키텍처를 여러 개 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="915b3-114">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-114">They include:</span></span>

* [<span data-ttu-id="915b3-115">실제 클라우드 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="915b3-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="915b3-116">클라우드 서비스를 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="915b3-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="915b3-117">아키텍처 청사진</span><span class="sxs-lookup"><span data-stu-id="915b3-117">Architectural blueprints</span></span>
<span data-ttu-id="915b3-118">Microsoft가 높은 수준의 집합이 게시 [아키텍처 청사진](http://aka.ms/azblueprints) 보여 주는 방법을 toobuild 특정 형식의 Microsoft 제품을 사용 하는 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="915b3-119">각 청사진에는 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="915b3-120">사용자가 다운로드하여 수정할 수 있는 플랫 2D Visio 2003 기반 파일</span><span class="sxs-lookup"><span data-stu-id="915b3-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="915b3-121">다양 한 색 3D 큐브 PDF 파일 toointroduce hello 청사진 tooless 전문가 대상</span><span class="sxs-lookup"><span data-stu-id="915b3-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="915b3-122">Hello 3D 버전 안내 비디오</span><span class="sxs-lookup"><span data-stu-id="915b3-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="915b3-123">클라우드 및 엔터프라이즈 기호 집합</span><span class="sxs-lookup"><span data-stu-id="915b3-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="915b3-124">[Hello Visio 및 비디오 교육 기호 볼](http://aka.ms/CnESymbolsVideo) 차례로 [hello 클라우드 및 엔터프라이즈 기호 집합을 다운로드](http://aka.ms/CnESymbols) toohelp Azure, Windows Server, SQL Server을 설명 하는 기술 자료를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="915b3-125">Hello 책 트레인 사람 toouse Microsoft 제품 경우 hello 기호 아키텍처 다이어그램, 교육 자료, 프레젠테이션, 데이터 시트, 인포 그래픽, 백서 및 제 3 자 설명서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="915b3-126">하지만 사용자 인터페이스에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="915b3-127">3D 청사진 Visio 템플릿</span><span class="sxs-lookup"><span data-stu-id="915b3-127">3D blueprint Visio template</span></span>
<span data-ttu-id="915b3-128">3D 버전의 hello hello [Microsoft 아키텍처 청사진](http://aka.ms/azblueprints) 타사 도구에서 처음 생성 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="915b3-129">새로운 Visio 2013(및 이상) 템플릿은 [EDX.ORG에 분산된 Microsoft 아키텍처 인증 과정](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course)의 일부로 2015년 8월 5일 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="915b3-130">hello 템플릿 hello 과정 외부에서 사용할 수 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="915b3-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="915b3-131">[Hello 학습 비디오 보기](http://aka.ms/3dBlueprintTemplateVideo) 수행할 수 있는 작업을 확인할 수 있도록 하는 첫 번째</span><span class="sxs-lookup"><span data-stu-id="915b3-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="915b3-132">Hello 다운로드 [Microsoft 3d 청사진 Visio 템플릿](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="915b3-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="915b3-133">Hello 다운로드 [클라우드 및 엔터프라이즈 기호](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse hello 3D 템플릿 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="915b3-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
