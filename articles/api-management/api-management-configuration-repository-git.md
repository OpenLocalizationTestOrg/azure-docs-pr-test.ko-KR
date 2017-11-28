---
title: "aaaConfigure Git-Azure를 사용 하 여 API 관리 서비스 | Microsoft Docs"
description: "자세한 내용은 방법 toosave 및 Git를 사용 하 여 API 관리 서비스 구성에 구성 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="b83fa-103">어떻게 toosave 및 Git를 사용 하 여 API 관리 서비스 구성 구성</span><span class="sxs-lookup"><span data-stu-id="b83fa-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="b83fa-104">각 API 관리 서비스 인스턴스 hello 구성과 hello 서비스 인스턴스에 대 한 메타 데이터에 대 한 정보를 포함 하는 구성 데이터베이스를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="b83fa-105">변경 내용은 hello 게시자 포털의 설정 변경, PowerShell cmdlet을 사용 하 여 또는 REST API를 호출 하 여 toohello 서비스 인스턴스에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="b83fa-106">또한 toothese 메서드를 관리할 수도 있습니다 Git를 사용 하 여, 서비스 관리 시나리오를 같은 활성화 서비스 인스턴스 구성:</span><span class="sxs-lookup"><span data-stu-id="b83fa-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="b83fa-107">구성 버전 관리 - 서비스 구성의 서로 다른 버전 다운로드 및 저장</span><span class="sxs-lookup"><span data-stu-id="b83fa-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="b83fa-108">대량으로 구성 변경-서비스 구성의 toomultiple 부분에서에서 변경한 로컬 리포지토리를 hello 변경 내용을 다시 toohello 서버를 한 번의 작업와 통합</span><span class="sxs-lookup"><span data-stu-id="b83fa-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="b83fa-109">Hello Git 도구 및 워크플로 이미 잘 알고 있다면 친숙 한 Git 도구 체인 및 워크플로-사용</span><span class="sxs-lookup"><span data-stu-id="b83fa-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="b83fa-110">다음 다이어그램 hello 해당 API 관리 서비스 인스턴스에 hello 다양 한 방법 tooconfigure의 개요를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Git 구성][api-management-git-configure]

<span data-ttu-id="b83fa-112">Hello를 사용 하 여 서비스 구성 데이터베이스를 관리 하는 hello 게시자 포털, PowerShell cmdlet 또는 REST API hello를 사용 하 여 tooyour 서비스를 변경할 때 `https://{name}.management.azure-api.net` hello hello 다이어그램의 오른쪽에 표시 된 것 처럼 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="b83fa-113">hello 다이어그램의 왼쪽 hello Git를 사용 하 여 서비스 구성 관리 하는 방법을 설명 하 고에 있는 서비스에 대 한 Git 리포지토리 `https://{name}.scm.azure-api.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="b83fa-114">단계를 수행 하는 hello Git을 사용 하 여 API 관리 서비스 인스턴스 관리의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="b83fa-115">서비스의 Git 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="b83fa-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="b83fa-116">서비스 구성 데이터베이스 tooyour Git 리포지토리를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="b83fa-117">Hello tooyour 로컬 컴퓨터 Git 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="b83fa-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="b83fa-118">끌어오기 tooyour 로컬 컴퓨터를 최신 리포지토리 hello 및 커밋하고 푸시할 변경 내용 다시 tooyour 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b83fa-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="b83fa-119">사용자의 리포지토리의 hello 변경 내용을 서비스 구성 데이터베이스에 배포</span><span class="sxs-lookup"><span data-stu-id="b83fa-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="b83fa-120">이 문서에서는 설명 방법을 tooenable 및 Git toomanage 서비스 구성을 사용 하 여 hello 파일 및 폴더 hello Git 리포지토리에 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="b83fa-121">서비스의 Git 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="b83fa-121">Access Git configuration in your service</span></span>
<span data-ttu-id="b83fa-122">Hello 게시자 포털의 오른쪽 위 모서리 hello에에서 hello Git 아이콘을 확인 하 여 Git 구성 hello 상태를 신속 하 게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="b83fa-123">이 예제에서는 hello 상태 메시지 toohello 리포지토리에 저장 되지 않은 변경 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="b83fa-124">Hello API 관리 서비스 구성 데이터베이스 저장 되지 않은 아직 toohello 리포지토리 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Git 상태][api-management-git-icon-enable]

<span data-ttu-id="b83fa-126">tooview 및 Git 구성 설정을 구성, hello Git 아이콘을 클릭 하거나 클릭 hello **보안** 메뉴 toohello 이동 **구성 리포지토리의** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![GIT 사용][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="b83fa-128">정의 되지 않은 속성 hello 저장소에 저장 되 고에 남습니다. 그 역사 할 때까지 모든 암호 비활성화 및 다시 Git 액세스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="b83fa-129">속성 안전한 곳 toomanage toostore 없는 모든 API 구성 및 정책에서 비밀 정보를 포함 한 상수 문자열 값이 제공 정책 문을에서 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="b83fa-130">자세한 내용은 참조 [어떻게 Azure API 관리 정책에 toouse 속성](api-management-howto-properties.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="b83fa-131">활성화 또는 비활성화 hello REST API를 사용 하 여 Git 액세스에 대 한 자세한 내용은 참조 [Git 액세스 hello REST API를 사용 하 여 설정 하거나 해제](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="b83fa-132">toosave hello 서비스 구성 toohello Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b83fa-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="b83fa-133">hello 리포지토리 복제 하기 전에 hello 첫 번째 단계는 toosave hello hello 서비스 구성 toohello 저장소의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="b83fa-134">클릭 **구성 toorepository 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-134">Click **Save configuration toorepository**.</span></span>

![구성 저장][api-management-save-configuration]

<span data-ttu-id="b83fa-136">Hello 확인 화면에 원하는 대로 변경 하 고 클릭 **확인** toosave 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![구성 저장][api-management-save-configuration-confirm]

<span data-ttu-id="b83fa-138">몇 분 후 hello 구성이 저장 되 고 마지막 구성 변경 hello 및 hello 서비스 구성 및 hello 간의 hello 마지막 동기화의 hello 날짜 및 시간을 포함 하 여 hello 리포지토리 hello 구성 상태가 표시 됩니다. 정보 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![구성 상태][api-management-configuration-status]

<span data-ttu-id="b83fa-140">Hello 구성은 toohello 리포지토리에 저장 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="b83fa-141">Hello REST API를 사용 하 여이 작업 수행에 대 한 자세한 내용은 참조 하십시오. [hello REST API를 사용 하 여 스냅숏 커밋 구성](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="b83fa-142">tooclone hello 리포지토리 tooyour 로컬 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="b83fa-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="b83fa-143">저장소 tooclone hello URL tooyour 저장소, 사용자 이름 및 암호를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="b83fa-144">hello 사용자 이름 및 URL 표시 hello의 hello 위쪽 **구성 리포지토리의** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Git 복제][api-management-configuration-git-clone]

<span data-ttu-id="b83fa-146">hello 암호가 hello hello 맨 아래에 생성 됩니다 **구성 리포지토리의** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![암호 생성][api-management-generate-password]

<span data-ttu-id="b83fa-148">해당 hello를 먼저 확인 하는 암호를 toogenerate **만료** toohello 필요한 만료 날짜 및 시간을 설정 하 고 클릭 **토큰 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![암호][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="b83fa-150">이 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-150">Make a note of this password.</span></span> <span data-ttu-id="b83fa-151">두면 되 면이 페이지 hello 암호 다시 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="b83fa-152">사용 하 여 hello Git Bash 예제 따르는 hello 도구 [Windows 용 Git](http://www.git-scm.com/downloads) 하지만 익숙한 모든 Git 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="b83fa-153">Hello 원하는 폴더의 Git 도구를 열고 다음 명령 tooclone hello git 리포지토리 tooyour 로컬 컴퓨터, hello 게시자 포털에서 제공 하는 hello 명령을 사용 하 여 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="b83fa-154">Hello 사용자 이름 및 메시지가 표시 되 면 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="b83fa-155">오류를 수신할 경우 수정 하세요 프로그램 `git clone` tooinclude hello 사용자 이름 및 암호를 hello 다음 예제와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="b83fa-156">오류가 발생 하면 URL 인코딩 hello 명령 hello 암호 부분을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="b83fa-157">한 신속 하 게 toodo tooopen Visual Studio 이며 hello에 문제 hello 다음 명령은 **직접 실행 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="b83fa-158">tooopen hello **직접 실행 창**, Visual Studio에서 모든 솔루션이 나 프로젝트를 엽니다 (또는 새 비어 있는 콘솔 응용 프로그램 만들기)을 선택 하 고 **Windows**, **직접 실행** 에서 hello **디버그** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="b83fa-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="b83fa-159">사용자 이름 및 저장소 위치 tooconstruct hello git 명령 함께 hello 인코딩된 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="b83fa-160">Hello 리포지토리 복제 되 면 볼 수 있으며 로컬 파일 시스템에서 작업.</span><span class="sxs-lookup"><span data-stu-id="b83fa-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="b83fa-161">자세한 내용은 [로컬 Git 리포지토리의 파일 및 폴더 구조 참조](#file-and-folder-structure-reference-of-local-git-repository)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b83fa-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="b83fa-162">tooupdate hello 가장 최근 서비스 인스턴스 구성 사용 하 여 로컬 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b83fa-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="b83fa-163">Hello 게시자 포털 또는 hello REST API를 사용 하 여 변경 내용을 tooyour API 관리 서비스 인스턴스를 확인 하는 경우에 hello 최신 변경 내용으로 로컬 리포지토리를 업데이트 하기 전에 이러한 변경 내용을 toohello 저장소를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="b83fa-164">toodo이를 클릭 하이 여 **구성 toorepository 저장** hello에 **구성 리포지토리의** hello 게시자 포털을 탭 한 다음 다음 로컬 저장소에서 명령을 hello를 발행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="b83fa-165">실행 하기 전에 `git pull` 로컬 저장소에 대 한 hello 폴더에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b83fa-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="b83fa-166">Hello를 방금 완료 한 경우 `git clone` 명령, hello 다음과 같은 명령을 실행 하 여 hello 디렉터리 tooyour 리포지토리를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="b83fa-167">로컬 리포지토리에 toohello 서버 리포지토리에서 toopush 변경</span><span class="sxs-lookup"><span data-stu-id="b83fa-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="b83fa-168">로컬 리포지토리 toohello 서버 리포지토리에서 toopush 변경 변경 내용을 적용 하 고 toohello 서버 리포지토리 푸시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="b83fa-169">toocommit 변경 내용을 로컬 리포지토리 및 명령을 다음 문제 hello 스위치 toohello 디렉터리, 프로그램 Git 명령 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="b83fa-170">모든 hello 커밋합니다 toohello 서버에서 실행 되는 toopush 다음 명령을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="b83fa-171">toodeploy 모든 서비스 구성 변경 내용 toohello API 관리 서비스 인스턴스</span><span class="sxs-lookup"><span data-stu-id="b83fa-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="b83fa-172">로컬 변경 내용이 커밋된 블록과 푸시된 toohello 서버 저장소, 되 면 tooyour API 관리 서비스 인스턴스에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![배포][api-management-configuration-deploy]

<span data-ttu-id="b83fa-174">Hello REST API를 사용 하 여이 작업 수행에 대 한 자세한 내용은 참조 하십시오. [Git 배포 hello REST API를 사용 하 여 tooconfiguration 데이터베이스 변경](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="b83fa-175">로컬 Git 리포지토리의 파일 및 폴더 구조 참조</span><span class="sxs-lookup"><span data-stu-id="b83fa-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="b83fa-176">hello hello 로컬 git 리포지토리에서 파일 및 폴더 hello 구성 정보가 hello 서비스 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="b83fa-177">항목</span><span class="sxs-lookup"><span data-stu-id="b83fa-177">Item</span></span> | <span data-ttu-id="b83fa-178">설명</span><span class="sxs-lookup"><span data-stu-id="b83fa-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b83fa-179">루트 api 관리 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-179">root api-management folder</span></span> |<span data-ttu-id="b83fa-180">Hello 서비스 인스턴스에 대 한 최상위 구성을 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="b83fa-181">apis 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-181">apis folder</span></span> |<span data-ttu-id="b83fa-182">Hello 서비스 인스턴스의 hello api에 대 한 hello 구성을 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="b83fa-183">groups 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-183">groups folder</span></span> |<span data-ttu-id="b83fa-184">Hello 서비스 인스턴스의 hello 그룹에 대 한 hello 구성을 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="b83fa-185">policies 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-185">policies folder</span></span> |<span data-ttu-id="b83fa-186">Hello 서비스 인스턴스의 hello 정책이 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="b83fa-187">portalStyles 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-187">portalStyles folder</span></span> |<span data-ttu-id="b83fa-188">Hello 서비스 인스턴스의 hello 개발자 포털 사용자 지정에 대 한 hello 구성 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="b83fa-189">products 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-189">products folder</span></span> |<span data-ttu-id="b83fa-190">Hello 서비스 인스턴스의 hello 제품에 대 한 hello 구성을 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="b83fa-191">templates 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-191">templates folder</span></span> |<span data-ttu-id="b83fa-192">Hello 서비스 인스턴스의 hello 전자 메일 템플릿 hello 구성을 포함</span><span class="sxs-lookup"><span data-stu-id="b83fa-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="b83fa-193">각 폴더는 하나 이상의 파일 및 하나 이상의 폴더, 예를 들어 각 API, 제품 또는 그룹에 대한 폴더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="b83fa-194">각 폴더 내의 hello 파일 hello 폴더 이름으로 설명 된 hello 엔터티 형식에 대 한 사항은 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="b83fa-195">파일 형식</span><span class="sxs-lookup"><span data-stu-id="b83fa-195">File type</span></span> | <span data-ttu-id="b83fa-196">목적</span><span class="sxs-lookup"><span data-stu-id="b83fa-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="b83fa-197">json :</span><span class="sxs-lookup"><span data-stu-id="b83fa-197">json</span></span> |<span data-ttu-id="b83fa-198">Hello 해당 엔터티에 대 한 구성 정보</span><span class="sxs-lookup"><span data-stu-id="b83fa-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="b83fa-199">html</span><span class="sxs-lookup"><span data-stu-id="b83fa-199">html</span></span> |<span data-ttu-id="b83fa-200">종종 hello 개발자 포털에 표시 되는 hello 엔터티에 대 한 설명</span><span class="sxs-lookup"><span data-stu-id="b83fa-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="b83fa-201">xml</span><span class="sxs-lookup"><span data-stu-id="b83fa-201">xml</span></span> |<span data-ttu-id="b83fa-202">정책 설명</span><span class="sxs-lookup"><span data-stu-id="b83fa-202">Policy statements</span></span> |
| <span data-ttu-id="b83fa-203">css</span><span class="sxs-lookup"><span data-stu-id="b83fa-203">css</span></span> |<span data-ttu-id="b83fa-204">개발자 포털 사용자 지정에 대한 스타일 시트</span><span class="sxs-lookup"><span data-stu-id="b83fa-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="b83fa-205">이러한 파일 만들고 사용할 수 있는, 삭제, 편집, 로컬 파일 시스템에서 관리 하 고 hello 변경 내용은 뒤로 toohello API 관리 서비스 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="b83fa-206">hello 다음 엔터티 hello Git 리포지토리에 포함 되지 않은 및 Git를 사용 하 여 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="b83fa-207">사용자</span><span class="sxs-lookup"><span data-stu-id="b83fa-207">Users</span></span>
> * <span data-ttu-id="b83fa-208">구독</span><span class="sxs-lookup"><span data-stu-id="b83fa-208">Subscriptions</span></span>
> * <span data-ttu-id="b83fa-209">속성</span><span class="sxs-lookup"><span data-stu-id="b83fa-209">Properties</span></span>
> * <span data-ttu-id="b83fa-210">스타일 이외의 개발자 포털 엔터티</span><span class="sxs-lookup"><span data-stu-id="b83fa-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="b83fa-211">루트 api 관리 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-211">Root api-management folder</span></span>
<span data-ttu-id="b83fa-212">hello 루트 `api-management` 폴더에는 `configuration.json` 형식에 따라 hello에 hello 서비스 인스턴스에 대 한 최상위 정보가 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="b83fa-213">hello 처음 네 개의 설정 (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, 및 `UserRegistrationTermsConsentRequired`)에 나오는 설정에 따라 hello toohello 매핑할 **Identities** hello 탭 **보안** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b83fa-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="b83fa-214">Id 설정</span><span class="sxs-lookup"><span data-stu-id="b83fa-214">Identity setting</span></span> | <span data-ttu-id="b83fa-215">너무 맵</span><span class="sxs-lookup"><span data-stu-id="b83fa-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="b83fa-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="b83fa-216">RegistrationEnabled</span></span> |<span data-ttu-id="b83fa-217">**익명 사용자에 게 toosign 옵트인 페이지 리디렉션** 확인란</span><span class="sxs-lookup"><span data-stu-id="b83fa-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="b83fa-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="b83fa-218">UserRegistrationTerms</span></span> |<span data-ttu-id="b83fa-219">**사용자 등록 시 사용 약관** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="b83fa-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="b83fa-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="b83fa-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="b83fa-221">**등록 페이지에 사용 약관 표시** 확인란</span><span class="sxs-lookup"><span data-stu-id="b83fa-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="b83fa-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="b83fa-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="b83fa-223">**동의 필요** 확인란</span><span class="sxs-lookup"><span data-stu-id="b83fa-223">**Require consent** checkbox</span></span> |

![Id 설정][api-management-identity-settings]

<span data-ttu-id="b83fa-225">다음 네 개의 설정을 hello (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, 및 `DelegationValidationKey`)에 나오는 설정에 따라 hello toohello 매핑할 **위임** hello 탭 **보안** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b83fa-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="b83fa-226">위임 설정</span><span class="sxs-lookup"><span data-stu-id="b83fa-226">Delegation setting</span></span> | <span data-ttu-id="b83fa-227">너무 맵</span><span class="sxs-lookup"><span data-stu-id="b83fa-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="b83fa-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="b83fa-228">DelegationEnabled</span></span> |<span data-ttu-id="b83fa-229">**로그인 및 등록 위임** 확인란</span><span class="sxs-lookup"><span data-stu-id="b83fa-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="b83fa-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="b83fa-230">DelegationUrl</span></span> |<span data-ttu-id="b83fa-231">**위임 끝점 URL** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="b83fa-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="b83fa-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="b83fa-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="b83fa-233">**제품 구독 위임** 확인란</span><span class="sxs-lookup"><span data-stu-id="b83fa-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="b83fa-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="b83fa-234">DelegationValidationKey</span></span> |<span data-ttu-id="b83fa-235">**유효성 검사 키 위임** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="b83fa-235">**Delegate Validation Key** textbox</span></span> |

![위임 설정][api-management-delegation-settings]

<span data-ttu-id="b83fa-237">마지막 설정은 hello `$ref-policy`, hello 서비스 인스턴스에 대 한 글로벌 정책 문을 파일 toohello 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="b83fa-238">apis 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-238">apis folder</span></span>
<span data-ttu-id="b83fa-239">hello `apis` 폴더 hello 다음 항목을 포함 하는 hello 서비스 인스턴스의 각 API에 대 한 폴더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="b83fa-240">`apis\<api name>\configuration.json`-hello API에 대 한 hello 구성 이며 hello 백 엔드 서비스 URL 및 hello 작업에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="b83fa-241">이 hello toocall 인 경우 반환 되는 동일한 정보 [특정 API 가져오기](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) 와 `export=true` 에 `application/json` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="b83fa-242">`apis\<api name>\api.description.html`-hello API에 대 한 hello 설명을 이므로 toohello 해당 `description` hello 속성 [API 엔터티](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="b83fa-243">`apis\<api name>\operations\`-이 폴더에 들어 `<operation name>.description.html` toohello 작업 hello API에에서 매핑하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="b83fa-244">각 파일 hello toohello 매핑하는 API에는 단일 작업에 대 한 hello 설명을 포함 `description` hello 속성 [작업 엔터티에](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) hello REST API에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="b83fa-245">groups 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-245">groups folder</span></span>
<span data-ttu-id="b83fa-246">hello `groups` 폴더 hello 서비스 인스턴스에 정의 된 각 그룹에 대 한 폴더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="b83fa-247">`groups\<group name>\configuration.json`-이 hello 그룹에 대 한 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="b83fa-248">이 hello toocall hello 인 경우 반환 되는 동일한 정보 [특정 그룹 가져오기](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="b83fa-249">`groups\<group name>\description.html`-hello 그룹의 설명을 hello 이므로 해당 toohello `description` hello 속성 [엔터티 그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="b83fa-250">policies 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-250">policies folder</span></span>
<span data-ttu-id="b83fa-251">hello `policies` 폴더에는 서비스 인스턴스에 대 한 hello 정책 문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="b83fa-252">`policies\global.xml` -서비스 인스턴스에 대 한 전역 범위에 정의된 정책을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="b83fa-253">`policies\apis\<api name>\` -API 범위에 정책을 정의 한 경우 해당 정책이 이 폴더에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="b83fa-254">`policies\apis\<api name>\<operation name>\`폴더에이 폴더에 포함 된 작업 범위에서 정의 된 모든 정책이 있는 경우 `<operation name>.xml` 각 작업에 대 한 정책 문을 toohello 매핑하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="b83fa-255">`policies\products\`-포함 하는이 폴더에 포함 된 제품 범위에서 정의 된 모든 정책이 있는 경우 `<product name>.xml` 각 제품에 대 한 정책 문을 toohello 매핑하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="b83fa-256">portalStyles 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-256">portalStyles folder</span></span>
<span data-ttu-id="b83fa-257">hello `portalStyles` 폴더 hello 서비스 인스턴스에 대 한 개발자 포털 사용자 지정에 대 한 구성 및 스타일 시트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="b83fa-258">`portalStyles\configuration.json`-hello 개발자 포털에서 사용 하는 hello 스타일 시트의 hello 이름이 포함 된</span><span class="sxs-lookup"><span data-stu-id="b83fa-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="b83fa-259">`portalStyles\<style name>.css`-각 `<style name>.css` hello 개발자 포털에 대 한 스타일을 포함 하는 파일 (`Preview.css` 및 `Production.css` 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="b83fa-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="b83fa-260">products 폴더</span><span class="sxs-lookup"><span data-stu-id="b83fa-260">products folder</span></span>
<span data-ttu-id="b83fa-261">hello `products` 폴더 hello 서비스 인스턴스에 정의 된 각 제품에 대 한 폴더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="b83fa-262">`products\<product name>\configuration.json`-이 hello 제품에 대 한 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="b83fa-263">이 hello toocall hello 인 경우 반환 되는 동일한 정보 [특정 제품 가져오기](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="b83fa-264">`products\<product name>\product.description.html`-hello 제품의 hello 설명 이므로 toohello 해당 `description` hello 속성 [product 엔터티](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) hello REST API에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="b83fa-265">템플릿</span><span class="sxs-lookup"><span data-stu-id="b83fa-265">templates</span></span>
<span data-ttu-id="b83fa-266">hello `templates` hello에 대 한 구성 폴더에 포함 되어 [전자 메일 템플릿을](api-management-howto-configure-notifications.md) hello 서비스 인스턴스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="b83fa-267">`<template name>\configuration.json`-이 hello 전자 메일 템플릿의 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="b83fa-268">`<template name>\body.html`-hello hello 전자 메일 템플릿의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="b83fa-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b83fa-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b83fa-269">Next steps</span></span>
<span data-ttu-id="b83fa-270">다른 방법으로 toomanage에 대 한 내용은 해당 서비스 인스턴스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b83fa-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="b83fa-271">Hello 다음 PowerShell cmdlet을 사용 하 여 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="b83fa-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="b83fa-272">서비스 배포 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="b83fa-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="b83fa-273">서비스 관리 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="b83fa-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="b83fa-274">Hello 게시자 포털에서 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="b83fa-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="b83fa-275">첫 번째 API 관리</span><span class="sxs-lookup"><span data-stu-id="b83fa-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="b83fa-276">Hello REST API를 사용 하 여 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="b83fa-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="b83fa-277">API 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="b83fa-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="b83fa-278">비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="b83fa-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




