---
title: "Azure에 대 한 빌드 aaaCommand 줄 | Microsoft Docs"
description: "Azure에 대한 명령줄 빌드"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a><span data-ttu-id="52f7b-103">Hello 명령줄에서 Azure 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="52f7b-103">Building Azure projects from hello command line</span></span>
<span data-ttu-id="52f7b-104">Microsoft Build Engine (MSBuild) hello를 사용 하 여 Visual Studio가 설치 되지 않은 빌드 랩 환경에서 제품을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-104">Using hello Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="52f7b-105">MSBuild는 Microsoft에서 확장 가능하고 완전히 지원되는 프로젝트 파일에 대한 XML 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="52f7b-106">Hello MSBuild 파일 형식을 사용 하 여 설명할 수 있습니다 항목 하나 이상의 플랫폼 및 구성에 대해 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-106">Using hello MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="52f7b-107">이 항목에서는 그 방법을 설명 하 고 hello 명령줄에서 MSBuild를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-107">You can also run MSBuild at hello command line, and this topic describes that approach.</span></span> <span data-ttu-id="52f7b-108">Hello 명령줄에서 속성을 설정 하면 프로젝트의 특정 구성을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-108">By setting properties on hello command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="52f7b-109">마찬가지로, MSBuild에서 작성 하는 hello 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-109">Similarly, you can also define hello targets that MSBuild builds.</span></span> <span data-ttu-id="52f7b-110">명령줄 매개 변수 및 MSBuild에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52f7b-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="52f7b-111">MSBuild 매개 변수</span><span class="sxs-lookup"><span data-stu-id="52f7b-111">MSBuild parameters</span></span>
<span data-ttu-id="52f7b-112">hello 가장 간단한 방법은 toocreate 패키지는 hello로 MSBuild toorun `/t:Publish` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-112">hello simplest way toocreate a package is toorun MSBuild with hello `/t:Publish` option.</span></span> <span data-ttu-id="52f7b-113">기본적으로이 명령은 디렉터리에에서 만듭니다 hello 프로젝트에 대 한 관계 toohello 루트 폴더와 같은 `<ProjectDirectory>\bin\Configuration\app.publish\`합니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-113">By default, this command creates a directory in relation toohello root folder for hello project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="52f7b-114">Azure 프로젝트를 빌드할 때 두 파일이 생성 됩니다: 패키지 파일 자체와 해당 구성 파일 hello hello:</span><span class="sxs-lookup"><span data-stu-id="52f7b-114">When you build an Azure project, two files are generated: hello package file itself and hello accompanying configuration file:</span></span>

* <span data-ttu-id="52f7b-115">패키지 파일(`project.cspkg`)</span><span class="sxs-lookup"><span data-stu-id="52f7b-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="52f7b-116">구성 파일(`ServiceConfiguration.TargetProfile.cscfg`)</span><span class="sxs-lookup"><span data-stu-id="52f7b-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="52f7b-117">기본적으로 각 Azure 프로젝트에는 로컬(디버깅) 빌드용 서비스 구성 파일 하나와 클라우드(스테이징 또는 프로덕션) 빌드용 서비스 구성 파일 하나가 포함되지만</span><span class="sxs-lookup"><span data-stu-id="52f7b-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="52f7b-118">필요에 따라 서비스 구성 파일을 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="52f7b-119">Visual Studio 내에서 패키지를 빌드할 때 hello 패키지와 함께 어떤 서비스 구성 파일 tooinclude를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-119">When you build a package within Visual Studio, you are asked which service-configuration file tooinclude alongside hello package.</span></span> <span data-ttu-id="52f7b-120">MSBuild를 사용 하 여 패키지를 빌드할 때 hello 로컬 서비스 구성 파일은 기본적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-120">When you build a package by using MSBuild, hello local service-configuration file is included by default.</span></span> <span data-ttu-id="52f7b-121">tooinclude 서로 다른 서비스 구성 파일을 집합 hello `TargetProfile` hello MSBuild 명령의 속성 (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span><span class="sxs-lookup"><span data-stu-id="52f7b-121">tooinclude a different service-configuration file, set hello `TargetProfile` property of hello MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="52f7b-122">패키지 및 구성 파일을 hello를 사용 하 여 hello 경로 설정 hello에 대 한 다른 디렉터리에 저장 된 toouse 하려는 경우 `/p:PublishDir=Directory\` hello 후행 백슬래시 구분 기호를 포함 하 여 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-122">If you want toouse an alternate directory for hello stored package and configuration files, set hello path by using hello `/p:PublishDir=Directory\` option, including hello trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52f7b-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52f7b-123">Next steps</span></span>
<span data-ttu-id="52f7b-124">Hello 패키지를 만든 후 tooAzure 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-124">After hello package is built, you can deploy it tooAzure.</span></span> <span data-ttu-id="52f7b-125">설명 하는 자습서에 대 한 tooautomate 처리 하는 참조 [Azure에서 클라우드 서비스에 대 한 지속적인 업데이트](./cloud-services/cloud-services-dotnet-continuous-delivery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52f7b-125">For a tutorial that demonstrates how tooautomate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>

