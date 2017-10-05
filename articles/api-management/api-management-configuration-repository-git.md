---
title: "Git를 사용하여 API Management 서비스 구성 - Azure | Microsoft Docs"
description: "Git를 사용하여 API 관리 서비스 구성을 저장 및 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="9e16b-103">Git를 사용하여 API 관리 서비스 구성을 저장 및 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="9e16b-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="9e16b-104">각 API 관리 서비스 인스턴스는 구성에 관한 정보 및 서비스 인스턴스에 대한 메타데이터를 포함하고 있는 구성 데이터베이스를 유지관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="9e16b-105">PowerShell cmdlet을 사용하거나 REST API를 호출하여 게시자 포털의 설정을 변경하면 서비스 인스턴스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="9e16b-106">이러한 방법 이외에 다음과 같은 서비스 관리 시나리오를 통해 Git를 사용하여 서비스 인스턴스 구성을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="9e16b-107">구성 버전 관리 - 서비스 구성의 서로 다른 버전 다운로드 및 저장</span><span class="sxs-lookup"><span data-stu-id="9e16b-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="9e16b-108">대량 구성 변경 - 로컬 저장소에 있는 서비스 구성의 여러 부분을 변경하고 단일 작업으로 변경 내용을 서버에 다시 통합</span><span class="sxs-lookup"><span data-stu-id="9e16b-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="9e16b-109">친숙한 Git 도구 체인 및 워크플로 - 이미 익숙해진 Git 도구 및 워크플로 사용</span><span class="sxs-lookup"><span data-stu-id="9e16b-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="9e16b-110">다음 다이어그램에서는 API 관리 서비스 인스턴스를 구성하는 다양한 방법을 간략하게 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Git 구성][api-management-git-configure]

<span data-ttu-id="9e16b-112">게시자 포털, PowerShell cmdlet 또는 REST API를 사용하여 서비스를 변경할 때 다이어그램의 오른쪽과 같이 `https://{name}.management.azure-api.net` 끝점을 사용하여 서비스 구성 데이터베이스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="9e16b-113">다이어그램의 왼쪽은 `https://{name}.scm.azure-api.net`에 있는 서비스에 Git 및 Git 리포지토리를 사용하여 서비스 구성을 관리할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="9e16b-114">다음 단계는 Git를 이용한 API 관리 서비스 인스턴스 관리를 간략하게 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="9e16b-115">서비스의 Git 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="9e16b-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="9e16b-116">Git 리포지토리에 서비스 구성 데이터베이스 저장</span><span class="sxs-lookup"><span data-stu-id="9e16b-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="9e16b-117">로컬 컴퓨터에 Git 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="9e16b-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="9e16b-118">리포지토리를 로컬 컴퓨터에 풀하고 커밋한 다음 변경 내용을 리포지토리에 다시 푸시</span><span class="sxs-lookup"><span data-stu-id="9e16b-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="9e16b-119">리포지토리의 변경 내용을 서비스 구성 데이터베이스에 배포</span><span class="sxs-lookup"><span data-stu-id="9e16b-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="9e16b-120">이 문서에서는 Git를 사용하도록 설정하고 이를 사용하여 서비스 구성을 관리하는 방법을 설명하며 Git 리포지토리의 파일 및 폴더에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="9e16b-121">서비스의 Git 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="9e16b-121">Access Git configuration in your service</span></span>
<span data-ttu-id="9e16b-122">게시자 포털의 오른쪽 위 모서리의 Git 아이콘을 확인하여 Git 구성의 상태를 신속하게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="9e16b-123">이 예제에서 상태 메시지는 리포지토리에 대해 저장되지 않은 변경 내용이 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="9e16b-124">이는 API 관리 서비스 구성 데이터베이스가 리포지토리에 아직 저장되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Git 상태][api-management-git-icon-enable]

<span data-ttu-id="9e16b-126">Git 구성 설정을 확인 및 구성하려면 Git 아이콘을 클릭하거나 **보안** 메뉴를 클릭하고 **구성 리포지토리** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![GIT 사용][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="9e16b-128">속성으로 정의되지 않은 비밀은 리포지토리에 저장되며 Git 액세스를 사용하지 않도록 설정했다가 다시 사용하도록 설정할 때까지 기록에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="9e16b-129">속성은 모든 API 구성 및 정책에 대해 비밀을 포함한 상수 문자열 값을 관리하는 안전한 장소를 제공하므로 정책을 정책 설명에 직접 저장할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="9e16b-130">자세한 내용은 [Azure API 관리 정책에 속성을 사용하는 방법](api-management-howto-properties.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="9e16b-131">REST API를 사용하여 Git 액세스를 사용 또는 사용하지 않도록 설정하는 방법은 [REST API를 사용하여 Git 액세스를 사용 또는 사용하지 않도록 설정](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="9e16b-132">Git 리포지토리에 서비스 구성 저장</span><span class="sxs-lookup"><span data-stu-id="9e16b-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="9e16b-133">리포지토리를 복제하기 전에 수행할 첫 번째 단계는 서비스 구성의 현재 상태를 리포지토리에 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="9e16b-134">**리포지토리에 구성 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-134">Click **Save configuration to repository**.</span></span>

![구성 저장][api-management-save-configuration]

<span data-ttu-id="9e16b-136">확인 화면에서 원하는 대로 변경하고 **확인** 을 클릭하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![구성 저장][api-management-save-configuration-confirm]

<span data-ttu-id="9e16b-138">몇 분 후에 구성이 저장되며, 마지막 구성 변경 및 서비스 구성과 리포지토리 간 마지막 동기화의 날짜 및 시간을 비롯하여 리포지토리의 구성 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![구성 상태][api-management-configuration-status]

<span data-ttu-id="9e16b-140">구성이 리포지토리에 저장된 후 해당 구성을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="9e16b-141">REST API를 사용하여 이 작업을 수행하는 방법은 [REST API를 사용하여 구성 스냅숏 커밋](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="9e16b-142">로컬 컴퓨터에 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="9e16b-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="9e16b-143">리포지토리를 복제하려면 리포지토리에 대한 URL, 사용자 이름 및 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="9e16b-144">사용자 이름 및 URL이 **구성 리포지토리** 의 맨 위 부근에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Git 복제][api-management-configuration-git-clone]

<span data-ttu-id="9e16b-146">**구성 리포지토리** 의 맨 아래에 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![암호 생성][api-management-generate-password]

<span data-ttu-id="9e16b-148">암호를 생성하려면 먼저 **만료**가 원하는 만료 날짜 및 시간으로 설정되었는지 확인한 다음 **토큰 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![암호][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="9e16b-150">이 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-150">Make a note of this password.</span></span> <span data-ttu-id="9e16b-151">이 페이지를 떠나면 암호가 다시 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="9e16b-152">다음 예제에서는 [Windows용 Git](http://www.git-scm.com/downloads) 에서 Git Bash 도구를 사용하지만 현재 친숙한 아무 Git나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="9e16b-153">원하는 폴더에서 Git 도구를 열고 게시자 포털에서 제공한 다음 명령을 실행하여 Git 리포지토리를 로컬 컴퓨터에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9e16b-154">메시지가 표시되면 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="9e16b-155">오류가 발생하면 다음 예제와 같이 `git clone` 명령을 사용자 이름 및 암호를 포함하도록 수정해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9e16b-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9e16b-156">그래도 오류가 발생하면 명령의 암호 부분에 대해 URL 인코딩을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9e16b-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="9e16b-157">이렇게 하는 한 가지 빠른 방법은 Visual Studio를 열고 **직접 실행 창**에서 다음 명령을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="9e16b-158">**직접 실행 창**을 열려면 Visual Studio에서 솔루션 또는 프로젝트를 열고(또는 비어 있는 새 콘솔 응용 프로그램을 만들고) **디버그** 메뉴에서 **창**, **직접 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="9e16b-159">사용자 이름 및 리포지토리 위치와 함께 인코딩된 암호를 사용하여 Git 명령을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9e16b-160">리포지토리가 복제된 후 로컬 파일 시스템에서 이를 보고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="9e16b-161">자세한 내용은 [로컬 Git 리포지토리의 파일 및 폴더 구조 참조](#file-and-folder-structure-reference-of-local-git-repository)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="9e16b-162">최근 서비스 인스턴스 구성으로 로컬 리포지토리를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="9e16b-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="9e16b-163">게시자 포털에서 또는 REST API를 사용하여 API 관리 서비스 인스턴스를 변경하는 경우 변경 내용을 리포지토리에 저장해야 로컬 리포지토리를 최신 변경 내용으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="9e16b-164">이 작업을 수행하려면 게시자 포털의 **구성 리포지토리** 탭에서 **리포지토리에 구성 저장**을 클릭한 후 로컬 리포지토리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="9e16b-165">`git pull` 을 실행하기 전에 현재 로컬 리포지토리에 대한 폴더에 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="9e16b-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="9e16b-166">`git clone` 명령을 방금 완료한 경우 다음과 같은 명령을 실행하여 디렉터리를 리포지토리로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="9e16b-167">로컬 리포지토리의 변경 내용을 서버 리포지토리에 푸시하려면</span><span class="sxs-lookup"><span data-stu-id="9e16b-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="9e16b-168">로컬 리포지토리의 변경 내용을 서버 리포지토리에 푸시하려면 변경 내용을 커밋한 다음 이를 서버 리포지토리에 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="9e16b-169">변경 내용을 커밋하려면 Git 명령 도구를 열고 로컬 리포지토리의 디렉터리로 전환한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="9e16b-170">모든 커밋을 서버에 푸시하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="9e16b-171">서비스 구성 변경 내용을 API 관리 서비스 인스턴스에 배포하려면</span><span class="sxs-lookup"><span data-stu-id="9e16b-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="9e16b-172">로컬 변경 내용이 커밋되고 서버 리포지토리에 푸시된 후 이를 API 관리 서비스 인스턴스에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![배포][api-management-configuration-deploy]

<span data-ttu-id="9e16b-174">REST API를 사용하여 이 작업을 수행하는 방법은 [REST API를 사용하여 구성 데이터베이스에 Git 변경 내용 배포](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="9e16b-175">로컬 Git 리포지토리의 파일 및 폴더 구조 참조</span><span class="sxs-lookup"><span data-stu-id="9e16b-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="9e16b-176">로컬 Git 리포지토리의 파일 및 폴더에는 서비스 인스턴스에 관한 구성 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="9e16b-177">항목</span><span class="sxs-lookup"><span data-stu-id="9e16b-177">Item</span></span> | <span data-ttu-id="9e16b-178">설명</span><span class="sxs-lookup"><span data-stu-id="9e16b-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e16b-179">루트 api 관리 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-179">root api-management folder</span></span> |<span data-ttu-id="9e16b-180">서비스 인스턴스에 대한 최상의 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="9e16b-181">apis 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-181">apis folder</span></span> |<span data-ttu-id="9e16b-182">서비스 인스턴스의 apis에 대한 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="9e16b-183">groups 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-183">groups folder</span></span> |<span data-ttu-id="9e16b-184">서비스 인스턴스의 그룹에 대한 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="9e16b-185">policies 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-185">policies folder</span></span> |<span data-ttu-id="9e16b-186">서비스 인스턴스의 정책 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="9e16b-187">portalStyles 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-187">portalStyles folder</span></span> |<span data-ttu-id="9e16b-188">서비스 인스턴스의 개발자 포털 사용자 지정에 대한 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="9e16b-189">products 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-189">products folder</span></span> |<span data-ttu-id="9e16b-190">서비스 인스턴스의 제품에 대한 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="9e16b-191">templates 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-191">templates folder</span></span> |<span data-ttu-id="9e16b-192">서비스 인스턴스의 전자 메일 템플릿에 대한 구성 포함</span><span class="sxs-lookup"><span data-stu-id="9e16b-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="9e16b-193">각 폴더는 하나 이상의 파일 및 하나 이상의 폴더, 예를 들어 각 API, 제품 또는 그룹에 대한 폴더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="9e16b-194">각 폴더 내의 파일은 폴더 이름에 의해 설명된 엔터티 유형에 대해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="9e16b-195">파일 형식</span><span class="sxs-lookup"><span data-stu-id="9e16b-195">File type</span></span> | <span data-ttu-id="9e16b-196">목적</span><span class="sxs-lookup"><span data-stu-id="9e16b-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="9e16b-197">json :</span><span class="sxs-lookup"><span data-stu-id="9e16b-197">json</span></span> |<span data-ttu-id="9e16b-198">해당 엔터티에 관한 구성 정보</span><span class="sxs-lookup"><span data-stu-id="9e16b-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="9e16b-199">html</span><span class="sxs-lookup"><span data-stu-id="9e16b-199">html</span></span> |<span data-ttu-id="9e16b-200">대개 개발자 포털에 표시되는 엔터티에 관한 설명</span><span class="sxs-lookup"><span data-stu-id="9e16b-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="9e16b-201">xml</span><span class="sxs-lookup"><span data-stu-id="9e16b-201">xml</span></span> |<span data-ttu-id="9e16b-202">정책 설명</span><span class="sxs-lookup"><span data-stu-id="9e16b-202">Policy statements</span></span> |
| <span data-ttu-id="9e16b-203">css</span><span class="sxs-lookup"><span data-stu-id="9e16b-203">css</span></span> |<span data-ttu-id="9e16b-204">개발자 포털 사용자 지정에 대한 스타일 시트</span><span class="sxs-lookup"><span data-stu-id="9e16b-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="9e16b-205">이 파일을 로컬 파일 시스템에서 생성, 삭제, 편집 및 관리할 수 있으며 변경 내용을 API 관리 서비스 인스턴스에 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="9e16b-206">다음 엔터티는 Git 리포지토리에 포함되지 않으며 Git를 사용하여 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="9e16b-207">사용자</span><span class="sxs-lookup"><span data-stu-id="9e16b-207">Users</span></span>
> * <span data-ttu-id="9e16b-208">구독</span><span class="sxs-lookup"><span data-stu-id="9e16b-208">Subscriptions</span></span>
> * <span data-ttu-id="9e16b-209">속성</span><span class="sxs-lookup"><span data-stu-id="9e16b-209">Properties</span></span>
> * <span data-ttu-id="9e16b-210">스타일 이외의 개발자 포털 엔터티</span><span class="sxs-lookup"><span data-stu-id="9e16b-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="9e16b-211">루트 api 관리 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-211">Root api-management folder</span></span>
<span data-ttu-id="9e16b-212">루트 `api-management` 폴더에는 다음과 같은 형식의 서비스 인스턴스에 관한 최상위 정보를 포함하고 있는 `configuration.json` 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="9e16b-213">처음 네 설정(`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` 및 `UserRegistrationTermsConsentRequired`)은 **보안** 섹션의 **ID** 탭에 있는 다음과 같은 설정에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="9e16b-214">Id 설정</span><span class="sxs-lookup"><span data-stu-id="9e16b-214">Identity setting</span></span> | <span data-ttu-id="9e16b-215">매핑 대상</span><span class="sxs-lookup"><span data-stu-id="9e16b-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="9e16b-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="9e16b-216">RegistrationEnabled</span></span> |<span data-ttu-id="9e16b-217">**로그인 페이지로 익명 사용자 리디렉션** 확인란</span><span class="sxs-lookup"><span data-stu-id="9e16b-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="9e16b-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="9e16b-218">UserRegistrationTerms</span></span> |<span data-ttu-id="9e16b-219">**사용자 등록 시 사용 약관** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="9e16b-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="9e16b-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="9e16b-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="9e16b-221">**등록 페이지에 사용 약관 표시** 확인란</span><span class="sxs-lookup"><span data-stu-id="9e16b-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="9e16b-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="9e16b-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="9e16b-223">**동의 필요** 확인란</span><span class="sxs-lookup"><span data-stu-id="9e16b-223">**Require consent** checkbox</span></span> |

![Id 설정][api-management-identity-settings]

<span data-ttu-id="9e16b-225">처음 네 설정(`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` 및 `DelegationValidationKey`)은 **보안** 섹션의 **위임** 탭에 있는 다음과 같은 설정에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="9e16b-226">위임 설정</span><span class="sxs-lookup"><span data-stu-id="9e16b-226">Delegation setting</span></span> | <span data-ttu-id="9e16b-227">매핑 대상</span><span class="sxs-lookup"><span data-stu-id="9e16b-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="9e16b-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="9e16b-228">DelegationEnabled</span></span> |<span data-ttu-id="9e16b-229">**로그인 및 등록 위임** 확인란</span><span class="sxs-lookup"><span data-stu-id="9e16b-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="9e16b-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="9e16b-230">DelegationUrl</span></span> |<span data-ttu-id="9e16b-231">**위임 끝점 URL** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="9e16b-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="9e16b-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="9e16b-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="9e16b-233">**제품 구독 위임** 확인란</span><span class="sxs-lookup"><span data-stu-id="9e16b-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="9e16b-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="9e16b-234">DelegationValidationKey</span></span> |<span data-ttu-id="9e16b-235">**유효성 검사 키 위임** 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="9e16b-235">**Delegate Validation Key** textbox</span></span> |

![위임 설정][api-management-delegation-settings]

<span data-ttu-id="9e16b-237">마지막 설정 `$ref-policy`은 서비스 인스턴스에 대한 전역 정책 설명 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="9e16b-238">apis 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-238">apis folder</span></span>
<span data-ttu-id="9e16b-239">`apis` 폴더에는 다음 항목을 포함한 서비스 인스턴스의 각 API에 대한 폴더가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="9e16b-240">`apis\<api name>\configuration.json` - API에 대한 구성이며 백 엔드 서비스 URL 및 작업에 관한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="9e16b-241">이는 `application/json` 형식의 `export=true`을 사용한 [특정 API 가져오기](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI)를 호출하려는 경우 반환되는 것과 같은 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="9e16b-242">`apis\<api name>\api.description.html` - API에 대한 설명이며 [API 엔터티](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)의 `description` 속성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="9e16b-243">`apis\<api name>\operations\` - 이 폴더는 작업을 API에 매핑하는 `<operation name>.description.html` 파일을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="9e16b-244">각 파일은 REST API에서 [작업 엔터티](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties)의 `description` 속성에 매핑되는 API의 단일 작업에 대한 설명을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="9e16b-245">groups 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-245">groups folder</span></span>
<span data-ttu-id="9e16b-246">`groups` 폴더는 서비스 인스턴스에 정의된 각 그룹에 대한 폴더를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="9e16b-247">`groups\<group name>\configuration.json` - 그룹에 대한 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="9e16b-248">이는 [특정 그룹 가져오기](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) 를 호출하려는 경우 반환되는 것과 같은 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="9e16b-249">`groups\<group name>\description.html` - 그룹에 대한 설명이며 [그룹 엔터티](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)의 `description` 속성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="9e16b-250">policies 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-250">policies folder</span></span>
<span data-ttu-id="9e16b-251">`policies` 폴더에는 서비스 인스턴스에 대한 정책 설명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="9e16b-252">`policies\global.xml` -서비스 인스턴스에 대 한 전역 범위에 정의된 정책을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="9e16b-253">`policies\apis\<api name>\` -API 범위에 정책을 정의 한 경우 해당 정책이 이 폴더에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="9e16b-254">`policies\apis\<api name>\<operation name>\` 폴더 - 작업 범위에 정책을 정의한 경우 해당 정책은 각 작업에 대한 정책 설명에 매핑되는 이 폴더의 `<operation name>.xml` 파일에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="9e16b-255">`policies\products\` - 제품 범위에 정책을 정의한 경우 해당 정책은 각 제품에 대한 정책 설명에 매핑되는 이 폴더의 `<product name>.xml` 파일에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="9e16b-256">portalStyles 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-256">portalStyles folder</span></span>
<span data-ttu-id="9e16b-257">`portalStyles` 폴더에는 서비스 인스턴스에 대한 개발자 포털 사용자 지정에 대한 구성 및 스타일 시트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="9e16b-258">`portalStyles\configuration.json` - 개발자 포털에서 사용하는 스타일 시트의 이름이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="9e16b-259">`portalStyles\<style name>.css` - 각 `<style name>.css` 파일에는 개발자 포털에 대한 스타일(기본적으로 `Preview.css` 및 `Production.css`)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="9e16b-260">products 폴더</span><span class="sxs-lookup"><span data-stu-id="9e16b-260">products folder</span></span>
<span data-ttu-id="9e16b-261">`products` 폴더는 서비스 인스턴스에 정의된 각 제품에 대한 폴더를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="9e16b-262">`products\<product name>\configuration.json` - 제품에 대한 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="9e16b-263">이는 [특정 제품 가져오기](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) 를 호출하려는 경우 반환되는 것과 같은 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="9e16b-264">`products\<product name>\product.description.html` - 제품에 대한 설명이며 REST API에서 [제품 엔터티](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product)의 `description` 속성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="9e16b-265">템플릿</span><span class="sxs-lookup"><span data-stu-id="9e16b-265">templates</span></span>
<span data-ttu-id="9e16b-266">`templates` 폴더에는 서비스 인스턴스의 [전자 메일 템플릿](api-management-howto-configure-notifications.md) 에 대한 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="9e16b-267">`<template name>\configuration.json` - 전자 메일 템플릿에 대한 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="9e16b-268">`<template name>\body.html` - 전자 메일 템플릿의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="9e16b-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e16b-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e16b-269">Next steps</span></span>
<span data-ttu-id="9e16b-270">서비스 인스턴스를 관리하는 다른 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e16b-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="9e16b-271">다음 PowerShell cmdlet을 사용하여 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="9e16b-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="9e16b-272">서비스 배포 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="9e16b-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="9e16b-273">서비스 관리 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="9e16b-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="9e16b-274">게시자 포털에서 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="9e16b-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="9e16b-275">첫 번째 API 관리</span><span class="sxs-lookup"><span data-stu-id="9e16b-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="9e16b-276">REST API를 사용하여 서비스 인스턴스 관리</span><span class="sxs-lookup"><span data-stu-id="9e16b-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="9e16b-277">API 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="9e16b-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="9e16b-278">비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="9e16b-278">Watch a video overview</span></span>
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




