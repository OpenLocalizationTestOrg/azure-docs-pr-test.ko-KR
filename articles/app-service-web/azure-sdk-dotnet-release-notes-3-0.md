---
title: "Azure SDK for .NET 3.0 릴리스 정보 | Microsoft 문서"
description: "Azure SDK for .NET 3.0 릴리스 정보"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: eea4e569ac2d0192ed7872d2fcb9bed03614832b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="55913-103">Azure SDK for .NET 3.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="55913-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="55913-104">이 항목에는 Azure SDK for .NET 버전 3.0에 대한 릴리스 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="55913-105">Azure SDK for .NET 3.0 릴리스 요약</span><span class="sxs-lookup"><span data-stu-id="55913-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="55913-106">릴리스 날짜: 03/07/2017</span><span class="sxs-lookup"><span data-stu-id="55913-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="55913-107">Azure SDK 3.0의 새로운 변경 내용은 이번 릴리스에 도입되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="55913-108">기존 클라우드 서비스 프로젝트에서 이 SDK를 활용하는 데 필요한 업그레이드 프로세스도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="55913-109">업그레이드 프로세스를 요구하지 않고 Azure SDK 3.0의 사용을 허용하려면 Azure SDK 3.0은 Azure SDK 2.9와 같은 디렉터리에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55913-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="55913-110">대부분의 구성 요소는 2.9에서 주 버전을 변경하지 않았지만 대신 빌드 번호로 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="55913-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="55913-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="55913-112">Visual Studio 2017에서는 이 Azure SDK for .NET 릴리스가 Azure 워크로드에 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="55913-113">Azure 개발을 수행하는 데 필요한 모든 도구는 앞으로 Visual Studio 2017에 포함될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="55913-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="55913-114">Visual Studio 2015의 경우 해당 SDK는 계속 WebPI를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="55913-115">이제 Visual Studio 2017이 릴리스되었으므로 Visual Studio 2013용 Azure SDK for .NET 릴리스는 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="55913-116">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="55913-116">Azure Diagnostics</span></span>

- <span data-ttu-id="55913-117">이 동작은 키가 클라우드 서비스 진단 저장소 연결 문자열에 대한 토큰으로 교체되어 부분 연결 문자열만 저장하는 방식으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="55913-118">이제 실제 저장소 키가 액세스를 제어할 수 있도록 사용자 프로필 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="55913-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="55913-119">Visual Studio는 로컬 디버깅 및 게시 프로세스에 대한 사용자 프로필 폴더에서 저장소 키를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="55913-120">위에 설명된 변경에 대한 응답으로, Visual Studio Online 팀은 사용자가 연속 통합 및 배포에서 Azure에 게시할 때 진단 확장을 설정하기 위한 저장소 키를 지정할 수 있도록 Azure 클라우드 서비스 배포 작업 템플릿을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="55913-121">작업 환경 간 구성 문제를 해결하는 데 도움을 주기 위해 Azure 진단(WAD)에 대한 보안 연결 문자열 및 토큰화를 저장할 수 있게 했습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="55913-122">Windows Server 2016 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="55913-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="55913-123">이제 Visual Studio에서는 OS 제품군 5(Windows Server 2016) 가상 컴퓨터에 클라우드 서비스를 배포하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="55913-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="55913-124">기존 클라우드 서비스의 경우, 새 OS 제품군을 대상으로 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="55913-125">새 클라우드 서비스를 만들 때 .NET 4.6 이상을 사용하여 서비스를 만들려면 선택하는 경우 기본적으로 서비스는 OS 제품군 5를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55913-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="55913-126">자세한 내용은 [게스트 OS 제품군 지원 테이블](../cloud-services/cloud-services-guestos-update-matrix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55913-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="55913-127">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="55913-127">Known issues</span></span>

- <span data-ttu-id="55913-128">Azure .NET SDK 3.0에는 Visual Studio 2015와의 병렬 구성에서 Visual Studio 2017을 제거할 경우 문제가 소개되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="55913-129">Visual Studio 2015용 Azure SDK가 설치되어 있는 경우 Visual Studio 2017을 제거하면 Microsoft Azure Storage 에뮬레이터 및 Microsoft Azure 계산 에뮬레이터가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="55913-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="55913-130">이로 인해 Visual Studio 2015에서 새 클라우드 서비스 프로젝트를 만들고 디버그할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="55913-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="55913-131">이 문제를 수정하려면 웹 플랫폼 설치 관리자에서 Azure SDK를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55913-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="55913-132">이 문제는 Visual Studio 2017 업데이트에서 해결된 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="55913-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="55913-133">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55913-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="55913-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="55913-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="55913-135">Azure In-Role Cache에 대한 지원은 2016년 11월 30일에 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55913-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="55913-136">자세한 내용을 보려면 [여기](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="55913-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




