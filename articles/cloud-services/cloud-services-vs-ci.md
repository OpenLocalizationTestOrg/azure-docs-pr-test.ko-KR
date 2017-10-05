---
title: "Visual Studio Online을 사용한 클라우드 서비스의 지속적인 전송 | Microsoft Docs"
description: "서비스 구성 파일에 진단 저장소 키를 저장하지 않고 Azure 클라우드 앱에 대해 지속적인 전송을 설정하는 방법 알아보기"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="68f63-103">Visual Studio Online을 사용하여 클라우드 서비스 진단 저장소 키를 안전하게 저장하고 Azure에 대한 지속적인 통합 및 배포 설정</span><span class="sxs-lookup"><span data-stu-id="68f63-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="68f63-104">이 방법은 오늘날의 오픈 소스 프로젝트에 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="68f63-105">구성 파일에 응용 프로그램 암호를 저장하는 방식은 암호가 공개 소스 제어에서 유출되어 보안 취약점에 노출되므로 더 이상 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="68f63-106">클라우드 환경에서 빌드 서버가 공유되는 리소스일 수 있으므로 지속적인 통합 파이프라인의 파일에 일반 텍스트로 암호를 저장하는 것은 안전하지 않은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="68f63-107">이 문서에서는 개발 및 지속적인 통합 프로세스 중에 Visual Studio 및 Visual Studio Online이 보안 문제를 완화시키는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="68f63-108">프로젝트 구성 파일에서 진단 저장소 키 암호 제거</span><span class="sxs-lookup"><span data-stu-id="68f63-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="68f63-109">클라우드 서비스 진단 확장에서는 진단 결과를 저장하기 위해 Azure Storage가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="68f63-110">이전에는 저장소 연결 문자열이 클라우드 서비스 구성(.cscfg) 파일에 지정되었으며 소스 제어에서 확인할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="68f63-111">최신 Azure SDK 릴리스에서는 키가 토큰으로 교체되어 부분 연결 문자열만 저장하는 방식으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="68f63-112">다음 단계에서는 새 클라우드 서비스 도구 작동 원리에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="68f63-113">1. 역할 디자이너 열기</span><span class="sxs-lookup"><span data-stu-id="68f63-113">1. Open the Role designer</span></span>
* <span data-ttu-id="68f63-114">클라우드 서비스 역할을 두 번 클릭하거나 마우스 오른쪽 단추로 클릭하여 역할 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![역할 디자이너 열기][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="68f63-116">2. 진단 섹션에 새 확인란 "프로젝트에서 저장소 키 암호를 제거하지 마세요."가 추가됨</span><span class="sxs-lookup"><span data-stu-id="68f63-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="68f63-117">로컬 저장소 에뮬레이터를 사용하는 경우 로컬 연결 문자열 UseDevelopmentStorage=true에 대해 관리할 암호가 없으므로 이 확인란이 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![로컬 저장소 에뮬레이터 연결 문자열은 암호가 아님][1]

* <span data-ttu-id="68f63-119">새 프로젝트를 만드는 경우 기본적으로 이 확인란이 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="68f63-120">이로 인해 선택된 저장소 연결 문자열의 저장소 키 섹션이 토큰으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="68f63-121">토큰 값은 현재 사용자의 AppData Roaming 폴더(예: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="68f63-122">user\AppData 폴더는 사용자 로그인에 의해 액세스가 제어되며 개발 비밀 정보를 저장할 안전한 곳으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![저장소 키가 사용자 프로필 폴더에 저장됨][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="68f63-124">3. 진단 저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="68f63-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="68f63-125">"..." 단추를 클릭하여 시작된 대화 상자에서 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="68f63-126">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-126">button.</span></span> <span data-ttu-id="68f63-127">생성된 저장소 연결 문자열에 저장소 계정 키가 어떻게 포함되지 않는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="68f63-128">예: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="68f63-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="68f63-129">4.    프로젝트 디버그</span><span class="sxs-lookup"><span data-stu-id="68f63-129">4.    Debugging the project</span></span>
* <span data-ttu-id="68f63-130">Visual Studio에서 F5 키를 눌러 디버그를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="68f63-131">모든 과정이 이전과 같은 방식으로 진행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="68f63-132">![로컬로 디버그 시작][3]</span><span class="sxs-lookup"><span data-stu-id="68f63-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="68f63-133">5. Visual Studio에서 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="68f63-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="68f63-134">게시 대화 상자를 시작하고 로그인 지침에 따라 진행하여 Azure에 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="68f63-135">6. 추가 정보</span><span class="sxs-lookup"><span data-stu-id="68f63-135">6. Additional information</span></span>
> <span data-ttu-id="68f63-136">참고: 역할 디자이너의 설정 패널은 당분간 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="68f63-137">진단에 대해 암호 관리 기능을 사용하려는 경우 구성 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![설정 추가][4]

> <span data-ttu-id="68f63-139">참고: 사용하도록 설정되면 Application Insights 키가 일반 텍스트로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="68f63-140">이 키는 중요한 데이터 손상될 위험이 없도록 업로드된 콘텐츠에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="68f63-141">Visual Studio Online 작업 템플릿을 사용하여 클라우드 서비스 프로젝트 빌드 및 게시</span><span class="sxs-lookup"><span data-stu-id="68f63-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="68f63-142">다음 단계에서는 Visual Studio Online 작업을 사용하여 클라우드 서비스 프로젝트에 대해 지속적인 통합을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="68f63-143">1.    VSO 계정 얻기</span><span class="sxs-lookup"><span data-stu-id="68f63-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="68f63-144">[Visual Studio Online 계정을 만들] [ Create Visual Studio Online account] 없는 이미 있는 경우</span><span class="sxs-lookup"><span data-stu-id="68f63-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="68f63-145">[팀 프로젝트 만들기] [ Create team project] Visual Studio online 계정에서</span><span class="sxs-lookup"><span data-stu-id="68f63-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="68f63-146">2.    Visual Studio에서 소스 제어 설정</span><span class="sxs-lookup"><span data-stu-id="68f63-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="68f63-147">팀 프로젝트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-147">Connect to a team project</span></span>

![팀 프로젝트에 연결][5]

![연결할 팀 프로젝트 선택][6]

* <span data-ttu-id="68f63-150">소스 제어에 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-150">Add your project to source control</span></span>

![소스 제어에 프로젝트 추가][7]

![소스 제어 폴더에 프로젝트 매핑][8]

* <span data-ttu-id="68f63-153">팀 탐색기에서 프로젝트 체크 인</span><span class="sxs-lookup"><span data-stu-id="68f63-153">Check in your project from Team Explorer</span></span>

![소스 제어에 프로젝트 체크 인][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="68f63-155">3.    빌드 프로세스 구성</span><span class="sxs-lookup"><span data-stu-id="68f63-155">3.    Configure Build process</span></span>
* <span data-ttu-id="68f63-156">팀 프로젝트를 찾고 새 빌드 프로세스 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-156">Browse to your team project and add a new build process Templates</span></span>

![새 빌드 추가][10]

* <span data-ttu-id="68f63-158">빌드 작업 선택</span><span class="sxs-lookup"><span data-stu-id="68f63-158">Select build task</span></span>

![빌드 작업 추가][11]

![Visual Studio 빌드 작업 템플릿 선택][12]

* <span data-ttu-id="68f63-161">빌드 작업 입력을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-161">Edit build task input.</span></span> <span data-ttu-id="68f63-162">필요에 따라 빌드 매개 변수를 사용자 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="68f63-162">Please customize the build parameters according to your need</span></span>

![빌드 작업 구성][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="68f63-164">빌드 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-164">Configure build variables</span></span>

![빌드 변수를 구성합니다.][14]

* <span data-ttu-id="68f63-166">빌드 저장 위치를 업로드하는 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-166">Add a task to upload build drop</span></span>

![빌드 저장 위치 게시 작업 선택][15]

![빌드 저장 위치 게시 작업 구성][16]

* <span data-ttu-id="68f63-169">빌드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-169">Run the build</span></span>

![새 빌드 큐 대기][17]

![빌드 요약 보기][18]

* <span data-ttu-id="68f63-172">빌드가 성공하는 경우 아래와 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-172">if the build is successful you will see a result similar to below</span></span>

![빌드 결과][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="68f63-174">4.    릴리스 프로세스 구성</span><span class="sxs-lookup"><span data-stu-id="68f63-174">4.    Configure Release process</span></span>
* <span data-ttu-id="68f63-175">새 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-175">Create a new release</span></span>

![새 릴리스 만들기][20]

* <span data-ttu-id="68f63-177">Azure 클라우드 서비스 배포 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-177">Select the Azure Cloud Services Deployment task</span></span>

![Azure 클라우드 서비스 배포 작업 선택][21]

* <span data-ttu-id="68f63-179">저장소 계정 키가 소스 제어에서 체크 인되지 않으므로 진단 확장을 설정하기 위한 비밀 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="68f63-180">**새 서비스 만들기에 대한 고급 옵션** 섹션을 확장하고 **진단 저장소 계정 키** 매개 변수 입력을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="68f63-181">이 입력은 **[RoleName]:$(StorageAccountKey)** 형식의 여러 줄의 키-값 쌍을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="68f63-182">참고: 진단 저장소 계정이 클라우드 서비스 응용 프로그램을 게시하는 동일한 구독에 포함되면 배포 작업 입력에 키를 입력할 필요가 없습니다. 배포는 구독에서 프로그래밍 방식으로 저장소 정보를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![클라우드 서비스 배포 작업 구성][22]

* <span data-ttu-id="68f63-184">암호 빌드 변수를 사용하여 저장소 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="68f63-185">변수를 암호로 마스크하려면 변수 입력 오른쪽에 있는 잠금 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![암호 빌드 변수에 저장소 키 저장][23]

* <span data-ttu-id="68f63-187">릴리스를 만들고 Azure에 프로젝트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="68f63-187">Create a release and deploy your project to Azure</span></span>

![새 릴리스 만들기][24]

## <a name="next-steps"></a><span data-ttu-id="68f63-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68f63-189">Next steps</span></span>
<span data-ttu-id="68f63-190">Azure 클라우드 서비스에 대 한 진단 확장을 설정 하는 방법에 대 한 자세한 내용은 참조 하십시오 [PowerShell을 사용 하 여 Azure 클라우드 서비스에서 진단 사용][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="68f63-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
