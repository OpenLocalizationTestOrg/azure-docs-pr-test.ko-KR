---
title: "Azure SDK for .NET 2.9 릴리스 정보"
description: "Azure SDK for .NET 2.9 릴리스 정보"
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
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="50f0a-103">Azure SDK for .NET 2.9 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="50f0a-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="50f0a-104">이 항목에는 Azure SDK for .NET 버전 2.9 및 2.9.6에 대한 릴리스 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="50f0a-105">Azure SDK for .NET 2.9.6 릴리스 요약</span><span class="sxs-lookup"><span data-stu-id="50f0a-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="50f0a-106">릴리스 날짜: 11/16/2016</span><span class="sxs-lookup"><span data-stu-id="50f0a-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="50f0a-107">Azure SDK 2.9의 새로운 변경 내용은 이번 릴리스에 도입되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="50f0a-108">기존 클라우드 서비스 프로젝트에서 이 SDK를 활용하는 데 필요한 업그레이드 프로세스도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="50f0a-109">Visual Studio 2017 릴리스 후보</span><span class="sxs-lookup"><span data-stu-id="50f0a-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="50f0a-110">Visual Studio 2017 RC에서는 이 Azure SDK for .NET 릴리스가 Azure 워크로드에 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="50f0a-111">Azure 개발을 수행하는 데 필요한 모든 도구는 앞으로 Visual Studio 2017 RC에 포함될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="50f0a-112">Visual Studio 2015 및 Visual Studio 2013의 경우 해당 SDK는 계속 WebPI를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="50f0a-113">Visual Studio 2017이 최종 제품으로 출시될 때는 Visual Studio 2013용 Azure SDK for .NET 릴리스가 중단될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="50f0a-114">Visual Studio 2017 RC를 다운로드하려면 https://www.visualstudio.com/vs/visual-studio-2017-rc/ 링크를 따라 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="50f0a-115">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="50f0a-115">Azure Diagnostics</span></span>

- <span data-ttu-id="50f0a-116">이 동작은 키가 클라우드 서비스 진단 저장소 연결 문자열에 대한 토큰으로 교체되어 부분 연결 문자열만 저장하는 방식으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="50f0a-117">이제 실제 저장소 키가 액세스를 제어할 수 있도록 사용자 프로필 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="50f0a-118">Visual Studio는 로컬 디버깅 및 게시 프로세스에 대한 사용자 프로필 폴더에서 저장소 키를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="50f0a-119">위에 설명된 변경에 대한 응답으로, Visual Studio Online 팀은 사용자가 연속 통합 및 배포에서 Azure에 게시할 때 진단 확장을 설정하기 위한 저장소 키를 지정할 수 있도록 Azure 클라우드 서비스 배포 작업 템플릿을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="50f0a-120">작업 환경 간 구성 문제를 해결하는 데 도움을 주기 위해 Azure 진단(WAD)에 대한 보안 연결 문자열 및 토큰화를 저장할 수 있게 했습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="50f0a-121">Windows Server 2016 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="50f0a-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="50f0a-122">이제 Visual Studio에서는 OS 제품군 5(Windows Server 2016) 가상 컴퓨터에 클라우드 서비스를 배포하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="50f0a-123">기존 클라우드 서비스의 경우, 새 OS 제품군을 대상으로 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="50f0a-124">새 클라우드 서비스를 만들 때 .NET 4.6 이상을 사용하여 서비스를 만들려면 선택하는 경우 기본적으로 서비스는 OS 제품군 5를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="50f0a-125">자세한 내용은 [게스트 OS 제품군 지원 테이블](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="50f0a-126">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="50f0a-126">Known issues</span></span>

- <span data-ttu-id="50f0a-127">Azure .NET SDK 2.9.6에는 지원되지 않는 .NET framework(예: .NET 4.6)를 사용하여 프로젝트를 OS 제품군 5 미만으로 배포하는 것을 차단하는 제한 사항이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="50f0a-128">해결 방법이 [여기](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="50f0a-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="50f0a-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="50f0a-130">Azure In-Role Cache에 대한 지원은 2016년 11월 30일에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="50f0a-131">자세한 내용을 보려면 [여기](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="50f0a-132">Azure Stack용 Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="50f0a-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="50f0a-133">Azure Resource Manager 템플릿에 대한 배포 대상으로 Azure Stack을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="50f0a-134">Azure SDK for .NET 2.9 요약</span><span class="sxs-lookup"><span data-stu-id="50f0a-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="50f0a-135">개요</span><span class="sxs-lookup"><span data-stu-id="50f0a-135">Overview</span></span>
<span data-ttu-id="50f0a-136">이 문서에는 Azure SDK for .NET 2.9 릴리스의 릴리스 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="50f0a-137">이 릴리스의 업데이트에 대한 자세한 정보는 [Azure SDK 2.9 발표 게시물](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="50f0a-138">Visual Studio 2015 업데이트 2 및 Visual Studio "15" Preview용 Azure SDK 2.9</span><span class="sxs-lookup"><span data-stu-id="50f0a-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="50f0a-139">이 업데이트는 다음 버그 수정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="50f0a-140">"알 수 없는 형식" 문자열이 코드 생성 폴더의 이름 및/또는 생성된 코드에 포함될 네임스페이스 이름으로 나타나는 REST API 클라이언트 생성과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="50f0a-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="50f0a-141">인증 정보가 스케줄러 프로비전 프로세스로 전달되지 못하는 예약된 WebJobs와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="50f0a-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="50f0a-142">이 업데이트는 다음 새로운 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="50f0a-143">앱 서비스 프로비전 대화 상자의 "서비스" 탭에서 보조 앱 서비스에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="50f0a-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="50f0a-144">Visual Studio 2015 업데이트 2용 Azure Data Lake 도구</span><span class="sxs-lookup"><span data-stu-id="50f0a-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="50f0a-145">이 업데이트는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-145">This updates includes the following:</span></span>

* <span data-ttu-id="50f0a-146">**Azure Data Lake 도구** 가 Azure SDK for .NET 릴리스에 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="50f0a-147">이 도구는 Azure SDK를 설치할 때 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="50f0a-148">이 도구는 자주 업데이트되며 업데이트를 받으려면 [여기](http://aka.ms/datalaketool) 로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="50f0a-149">**서버 탐색기** 를 통해 모든 항목을 보고 일부 U-SQL 메타데이터 엔터티를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="50f0a-150">자세한 내용은 [이 블로그](https://azure.microsoft.com/documentation/services/data-lake-analytics/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50f0a-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="50f0a-151">HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="50f0a-151">HDInsight Tools</span></span>
<span data-ttu-id="50f0a-152">**HDInsight 도구** 에서 Tez 그래프 표시 및 기타 언어 수정을 포함하여 HDInsight 버전 3.3을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="50f0a-153">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="50f0a-153">Azure Resource Manager</span></span>
<span data-ttu-id="50f0a-154">이 릴리스는 Resource Manager 템플릿에 대한 [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="50f0a-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="50f0a-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="50f0a-155">See also</span></span>
[<span data-ttu-id="50f0a-156">Azure SDK 2.9 발표 게시물</span><span class="sxs-lookup"><span data-stu-id="50f0a-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

