---
title: "자습서: Azure Portal을 사용한 DevOps | Microsoft Docs"
description: "Azure 포털에서 다양한 DevOps 워크플로에 대해 알아봅니다."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="a0088-103">자습서: Azure 포털을 사용한 DevOps</span><span class="sxs-lookup"><span data-stu-id="a0088-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="a0088-104">Azure 플랫폼은 유연한 DevOps 워크플로를 담고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="a0088-105">이 자습서에서는 Azure 포털의 기능을 활용하여 실행 중인 응용 프로그램을 개발, 테스트, 배포, 문제 해결, 모니터링 및 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="a0088-106">이 자습서는 다음에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="a0088-107">웹앱 만들기 및 지속적인 배포 사용</span><span class="sxs-lookup"><span data-stu-id="a0088-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="a0088-108">앱 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0088-108">Develop and test an app</span></span>
3. <span data-ttu-id="a0088-109">앱 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a0088-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="a0088-110">일반 응용 프로그램 관리 작업</span><span class="sxs-lookup"><span data-stu-id="a0088-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="a0088-111">웹앱 만들기 및 지속적인 배포 사용</span><span class="sxs-lookup"><span data-stu-id="a0088-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="a0088-112">[Azure 앱 서비스](https://azure.microsoft.com/services/app-service/)를 사용하여 웹앱을 만들고 이 자습서의 뒷부분에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="a0088-113">실행 중인 Azure 환경에 소스 코드 리포지토리의 지속적인 배포를 처음부터 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="a0088-114">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="a0088-115">**App Services** &gt; **추가 아이콘**을 차례로 선택하고, 이름을 입력하며, 구독을 선택한 다음 새 리소스 그룹을 만들어 서비스를 위한 컨테이너로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="a0088-116">리소스 그룹을 사용하면 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)를 통해 단일 그룹으로 청구, 배포 및 모니터링과 같은 솔루션의 다양한 양상을 모두 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="a0088-118">앱 서비스는 몇 분 후에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="a0088-119">포털에서 서비스에 대한 다양한 메뉴 옵션을 탐색하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="a0088-121">URL을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-121">Click the URL.</span></span> <span data-ttu-id="a0088-122">도구 및 리포지토리에 대해 사용할 수 있는 선택은 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="a0088-123">또한 .NET, Java, Ruby 등 선택한 언어와 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="a0088-125">Azure 포털에서 연속 배포는 몇 가지 간단한 단계를 수행해야 하는 쉬운 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="a0088-126">Azure 포털의 방금 만든 앱 서비스에 대한 아이콘에서 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="a0088-128">오른쪽에 열리는 블레이드에서 게시 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="a0088-130">다음으로 앱에 연속 배포를 사용하도록 설정하는 일부 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="a0088-131">배포 원본을 클릭한 다음 원본 선택을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="a0088-132">리포지토리 원본에 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="a0088-134">이 예제에서는 GitHub를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-134">For this example choose GitHub.</span></span> <span data-ttu-id="a0088-135">원하는 경우 사용자가 선택한 리포지토리를 선택하고 권한 부여 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="a0088-137">리포지토리에 권한을 부여한 후에 배포할 프로젝트 및 분기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="a0088-138">여러 가상 샘플 예제가 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="a0088-140">프로젝트 및 분기를 선택하면 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="a0088-141">배포 알림이 표시되기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="a0088-143">GitHub로 다시 이동하여 Azure와 원본 제어 리포지토리를 통합하도록 만든 웹후크를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="a0088-144">Azure Portal을 사용하면 간단한 단계를 통해 GitHub와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="a0088-146">연속 배포를 보여주려면 리포지토리에 일부 콘텐츠를 신속하게 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="a0088-147">간단한 예제의 경우 GitHub 리포지토리에 샘플 텍스트 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="a0088-148">앱 서비스로 .NET, Ruby, Python 또는 기타 다른 유형의 응용 프로그램을 자유롭게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="a0088-149">텍스트 파일, ASP.NET MVC, Java 또는 Ruby 응용 프로그램을 선택한 리포지토리에 추가해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="a0088-151">리포지토리에 변경 내용을 커밋한 후에 포털 알림 영역에서 새 배포 시작을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="a0088-152">리포지토리에 커밋한 후에 변경 내용을 신속하게 표시하지 않으면 동기화를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="a0088-154">이 시점에서 앱 서비스에 대한 페이지를 사용해보고 로드하는 경우 403 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="a0088-155">이 예제에서는 index.htm 또는 default.html과 같은 파일 등 페이지에 일반적인 기본 문서가 설정되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="a0088-156">Azure 포털의 도구를 사용하여 이 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="a0088-157">Azure Portal에서 설정 &gt; 응용 프로그램 설정을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="a0088-159">응용 프로그램 설정을 위한 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-159">A blade opens for application settings.</span></span> <span data-ttu-id="a0088-160">"SamplePage.html" 페이지의 이름을 입력하고 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="a0088-161">다른 설정을 탐색하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="a0088-163">필요에 따라 브라우저 URL을 새로 고쳐서 필요한 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="a0088-164">이 경우에 간단한 텍스트가 페이지를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="a0088-165">리포지토리에 추가 변경 사항이 있을 때마다 새 자동 배포가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="a0088-167">Azure 포털을 사용하여 연속 배포를 사용하면 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="a0088-168">더 복잡한 릴리스 파이프라인을 구축하고 기존 원본 제어와 연속 통합 시스템을 사용하여 다른 여러 가지 기술을 사용하여 Azure에 배포할 수도 있습니다(예: 자동화된 구축 및 릴리스 관리 시스템 활용).</span><span class="sxs-lookup"><span data-stu-id="a0088-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="a0088-169">앱 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0088-169">Develop and test an app</span></span>
<span data-ttu-id="a0088-170">다음으로, 코드 기본을 변경하고 이러한 변경 내용을 신속하게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="a0088-171">또한 웹앱에 대한 일부 성능 테스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="a0088-172">Azure 포털의 탐색 창에서 앱 서비스를 선택하고 해당 앱 서비스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="a0088-174">도구를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="a0088-176">도구에서 개발 범주를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="a0088-177">여러 가지 유용한 도구를 사용하여 Azure 포털에서 나가지 않고 앱으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="a0088-178">콘솔을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="a0088-180">콘솔 창에서 앱에 대한 라이브 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="a0088-181">dir 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="a0088-182">상승된 권한이 필요한 명령은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="a0088-184">개발 범주로 다시 이동하고 Visual Studio Online을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="a0088-185">참고: Visual Studio Online은 이제 Visual Studio Team Services로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="a0088-187">앱에 대한 브라우저 내 편집 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="a0088-189">앱에 웹 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-189">A web extension installs for your app.</span></span> <span data-ttu-id="a0088-190">확장은 기능을 쉽고 빠르게 Azure의 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="a0088-191">기타 확장 형식 중 일부를 다음 스크린샷에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="a0088-193">Visual Studio Online 확장을 설치하면 이동을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="a0088-195">브라우저에서 직접 개발 IDE를 표시한 위치에 브라우저 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="a0088-196">아래 환경은 Chrome에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="a0088-198">파일 편집 ,파일 및 폴더 추가 및 라이브 사이트에서 콘텐츠를 다운로드 등 여러 가지 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="a0088-199">SamplePage.html 파일에 빠른 편집을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="a0088-201">몇 분 내에 변경 내용은 자동으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="a0088-202">페이지로 다시 이동하면 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="a0088-203">다음과 같은 라이브 편집이 프로덕션 환경에 적합하지 않다는 점을 염두에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="a0088-204">그러나 도구를 사용하면 개발 및 테스트 환경을 쉽고 빠르게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="a0088-207">도구 블레이드로 다시 이동하고 개발 범주에서 성능 테스트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="a0088-209">팀 서비스 계정을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-209">You need to set a team services account.</span></span> <span data-ttu-id="a0088-210">자세한 내용을 보려면 [팀 서비스 계정 만들기](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="a0088-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="a0088-211">새로 만들기를 클릭하여 성능 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="a0088-213">다양한 값을 구성하고 대화 상자 맨 아래에서 테스트 실행을 클릭하여 성능 테스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="a0088-216">테스트가 실행되기 시작하면 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="a0088-218">테스트가 완료되면 결과를 클릭하여 자세한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="a0088-220">이 예제에서는 제한된 데이터를 분석하도록 작은 테스트를 실행하기도 하지만 다양한 메트릭을 확인할 뿐만 아니라 이 보기에서 테스트를 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="a0088-221">Azure 포털을 통해 웹 성능 테스트를 쉽게 만들고, 실행 및 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="a0088-222">아래 스크린샷은 성능 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="a0088-226">앱 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a0088-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="a0088-227">Azure는 실행 중인 응용 프로그램을 모니터링하고 문제를 해결하는 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="a0088-228">Azure 포털에서 웹앱에 대한 도구를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="a0088-230">문제 해결 범주에서 사용하는 도구를 다양하게 선택하여 실행 중인 앱과 관련된 잠재적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="a0088-231">HTTP 라이브 트래픽 모니터링, 자체 치유 사용, 로그 보기 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="a0088-233">사이트 메트릭을 선택하여 몇 가지 HTTP 코드를 신속하게 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="a0088-235">서비스로서의 진단을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="a0088-236">응용 프로그램 형식을 선택한 다음 실행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="a0088-238">컬렉션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="a0088-240">적절한 로그를 선택하여 잠재적인 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="a0088-241">로깅을 사용하도록 설정하여 HTTP 로그 등 사용 가능한 데이터 옵션을 모두 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="a0088-243">메모리 덤프 파일을 클릭하여 잠재적인 문제를 찾는 데 도움이 되는 DebugDiag 분석 보고서를 다운로드하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="a0088-245">더 많은 데이터를 보려면 추가 로깅을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="a0088-246">Azure 포털에서 웹앱으로 이동하고 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="a0088-248">기능 범주까지 아래로 스크롤한 다음 진단 로그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="a0088-250">로깅에 대한 다양한 옵션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-250">Notice the various options for logging.</span></span> <span data-ttu-id="a0088-251">웹 서버 로깅을 설정하고 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="a0088-253">앱에 대한 도구 영역으로 다시 이동하여 서비스로서의 진단을 선택한 다음 실행을 클릭하여 데이터 수집을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="a0088-255">HTTP 로깅 설정을 사용하면 이제 HTTP 로그에 수집된 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="a0088-257">HTML 파일 로그를 클릭하여 추가로 조사할 풍부한 브라우저 기반 보고서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="a0088-259">앱에 대한 Azure 포털의 도구 섹션으로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="a0088-260">도구 섹션으로 스크롤한 다음 프로세스 탐색기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="a0088-262">프로세스 탐색기를 선택하여 프로세스를 실행하는 방법에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="a0088-263">아래에서 프로세스를 자세히 살펴보고 나서 Azure 포털에서 모든 프로세스를 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="a0088-266">왼쪽의 설정 블레이드로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="a0088-267">새 지원 요청을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="a0088-269">오른쪽에 블레이드에서 문제에 대한 세부 정보를 채우고 연락처 정보를 입력하고 나서 진단 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="a0088-270">Azure 포털을 통해 Microsoft로 작업하면 원활한 환경을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="a0088-273">Azure 포털 도움말은 강력하고 친숙한 도구 환경을 제공하여 실행 중인 응용 프로그램을 모니터링하고 문제를 해결하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="a0088-274">프로세스 재활용, 다양한 데이터 컬렉션 사용 및 사용 안 함, Microsoft 전문 지원과 통합 등의 작업을 수행하여 신속하게 조치를 취할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="a0088-275">일반 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="a0088-275">General Application Management</span></span>
<span data-ttu-id="a0088-276">응용 프로그램을 관리하는 경우, 백업 전략 구성, ID 공급자 구현과 관리 및 역할 기반 액세스 제어 구성과 같은 작업을 수행해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="a0088-277">기타 DevOps 환경과 마찬가지로 Azure 플랫폼에서는 이러한 작업을 포털에 직접 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="a0088-278">웹앱을 데이터 손실로부터 안전하게 지키려면 백업을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="a0088-279">웹앱의 설정 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="a0088-281">오른쪽에 블레이드에서 기능 범주로 스크롤을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="a0088-283">백업을 선택하면 오른쪽에 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="a0088-285">구성을 클릭하고 오른쪽의 블레이드에서 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="a0088-287">이제 백업을 저장할 저장소 컨테이너를 만들고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="a0088-288">블레이드 하단의 만들기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="a0088-289">그런 다음 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="a0088-291">컨테이너를 선택하면 데이터베이스에 대한 설치 백업 뿐만 아니라 일정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="a0088-292">이 시나리오에서 저장 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="a0088-294">저장한 후에 백업에 대한 왼쪽의 블레이드로 다시 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="a0088-295">응용 프로그램을 백업하려면 지금 백업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="a0088-297">몇 분 내에 만든 백업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="a0088-298">스크린샷에 있는 지금 복원 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="a0088-300">지금 복원을 클릭하고 오른쪽의 블레이드에서 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="a0088-301">적절한 백업을 선택하고 쉽게 필요에 따라 이전 상태로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="a0088-302">Azure 포털은 앱에 간단한 재해 복구 전략을 손쉽게 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="a0088-304">왼쪽에서 설정 블레이드로 다시 이동하고 기능에서 인증/권한 부여를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="a0088-306">오른쪽의 블레이드에서 앱 서비스 인증을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="a0088-307">인기 있는 공급자를 통해 구성할 수 있는 다양한 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="a0088-309">선택한 공급자를 선택하고 범위에 대한 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="a0088-310">앱 ID 및 앱 암호를 제공하고 앱에 Facebook 인증을 빠르게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="a0088-311">Azure 포털을 통해 앱에 대한 턴키 솔루션으로 인증을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="a0088-313">설정 블레이드로 다시 이동하고 리소스 관리 범주에서 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="a0088-315">오른쪽의 블레이드에서 역할 및 사용자를 추가하기 위한 다양한 옵션을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="a0088-316">Azure 포털을 사용하면 응용 프로그램에서 RBAC(역할 기반 액세스 제어)를 쉽게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="a0088-318">요약</span><span class="sxs-lookup"><span data-stu-id="a0088-318">Summary</span></span>
<span data-ttu-id="a0088-319">이 자습서에서는 웹앱에 신속하게 연속 배포를 사용하고 다양한 개발을 수행하며 작업을 테스트하고 라이브 앱을 모니터링하며 문제를 해결하고 마지막으로 중요한 전략(예: 재해 복구, ID 및 역할 기반 액세스 제어)을 관리함으로써 Azure 플랫폼을 사용하는 장점 중 일부를 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="a0088-320">Azure 플랫폼을 사용하면 이러한 DevOps 워크플로에 대한 통합된 환경을 사용할 수 있고 현재 작업에 컨텍스트를 유지하여 효율적으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0088-321">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0088-321">Next steps</span></span>
* <span data-ttu-id="a0088-322">Azure Resource Manager는 Azure 플랫폼에서 DevOps를 사용하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0088-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="a0088-323">자세한 내용을 알아보려면 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="a0088-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="a0088-324">Azure 앱 서비스 배포에 대한 자세한 내용을 알아보려면 [Azure 앱 서비스에 앱 배포](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="a0088-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
