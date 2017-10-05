---
title: "웹 사이트에서 ReportViewer 사용 | Microsoft Docs"
description: "이 항목에서는 Microsoft Azure 가상 컴퓨터에 저장된 보고서를 표시하는 Visual Studio ReportViewer 컨트롤을 사용하여 Microsoft Azure 웹 사이트를 빌드하는 방법에 대해 설명합니다."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e54c3bc484b0b3b81cc495e54c17e8ef448abe91
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a><span data-ttu-id="d5324-103">Azure에서 호스트되는 웹 사이트에서 ReportViewer 사용</span><span class="sxs-lookup"><span data-stu-id="d5324-103">Use ReportViewer in a Web Site Hosted in Azure</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d5324-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d5324-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d5324-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d5324-107">Microsoft Azure 가상 컴퓨터에 저장된 보고서를 표시하는 Visual Studio ReportViewer 컨트롤과 함께 Microsoft Azure 웹 사이트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-107">You can build a Microsoft Azure Web site with the Visual Studio ReportViewer control that displays a report stored on an Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="d5324-108">ReportViewer 컨트롤은 ASP.NET 웹 응용 프로그램 템플릿을 사용하여 빌드하는 웹 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-108">The ReportViewer control is in a Web application that you build using the ASP.NET Web application template.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5324-109">ASP.NET MVC 웹 응용 프로그램 템플릿은 ReportViewer 컨트롤을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-109">The ASP.NET MVC Web Application templates do not support the ReportViewer control.</span></span>

<span data-ttu-id="d5324-110">Microsoft Azure 웹 사이트에 ReportViewer를 통합하려면 다음 작업을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-110">To incorporate ReportViewer into your Microsoft Azure Web site, you need to complete the following tasks.</span></span>

* <span data-ttu-id="d5324-111">**추가** </span><span class="sxs-lookup"><span data-stu-id="d5324-111">**Add** Assemblies to the Deployment Package</span></span>
* <span data-ttu-id="d5324-112">**구성** </span><span class="sxs-lookup"><span data-stu-id="d5324-112">**Configure** Authentication and Authorization</span></span>
* <span data-ttu-id="d5324-113">**게시** </span><span class="sxs-lookup"><span data-stu-id="d5324-113">**Publish** the ASP.NET Web application to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5324-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d5324-114">Prerequisites</span></span>
<span data-ttu-id="d5324-115">[Azure 가상 컴퓨터의 SQL Server Business Intelligence](../classic/ps-sql-bi.md)에서 "일반 권장 사항 및 모범 사례" 섹션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-115">Review the “General recommendation and best practices” section in [SQL Server Business Intelligence in Azure Virtual Machines](../classic/ps-sql-bi.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d5324-116">ReportViewer 컨트롤은 Visual Studio Standard Edition 이상 버전과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-116">ReportViewer controls are shipped with Visual Studio, Standard Edition or above.</span></span> <span data-ttu-id="d5324-117">Web Developer Express Edition을 사용하려면 [MICROSOFT REPORT VIEWER 2012 런타임](https://www.microsoft.com/download/details.aspx?id=35747) 을 설치하여 ReportViewer 런타임 기능을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-117">If you are using the Web Developer Express Edition, you must install the [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) to use the ReportViewer runtime features.</span></span>
> 
> <span data-ttu-id="d5324-118">로컬 처리 모드에서 구성된 ReportViewer는 Microsoft Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-118">ReportViewer configured in local processing mode is not supported in Microsoft Azure.</span></span>

## <a name="adding-assemblies-to-the-deployment-package"></a><span data-ttu-id="d5324-119">배포 패키지에 어셈블리 추가</span><span class="sxs-lookup"><span data-stu-id="d5324-119">Adding Assemblies to the Deployment Package</span></span>
<span data-ttu-id="d5324-120">ASP.NET 응용 프로그램 온-프레미스를 호스트할 때 ReportViewer 어셈블리는 Visual Studio를 설치하는 동안 IIS 서버의 GAC(전역 어셈블리 캐시)에 일반적으로 직접 설치되고 응용 프로그램에서 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-120">When you host your ASP.NET application on-premises, the ReportViewer assemblies are usually installed directly in the global assembly cache (GAC) of the IIS server during Visual Studio installation, and can be accessed directly by the application.</span></span> <span data-ttu-id="d5324-121">그러나 클라우드에서 ASP.NET 응용 프로그램을 호스트할 때는 Microsoft Azure가 GAC에 어떤 것도 설치할 수 없도록 하기 때문에 ReportViewer 어셈블리가 응용 프로그램에 대해 로컬로 사용 가능한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-121">However, when you host your ASP.NET application in the cloud, Microsoft Azure does not allow anything to be installed into the GAC, so you must make sure the ReportViewer assemblies are available locally for your application.</span></span> <span data-ttu-id="d5324-122">프로젝트에서 ReportViewer 어셈블리에 대한 참조를 추가하여 이 작업을 수행할 수 있으며 로컬로 복사하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-122">You can do this by adding references to them in your project and configure them to be copied locally.</span></span>

<span data-ttu-id="d5324-123">원격 처리 모드에서 ReportViewer 컨트롤은 다음 어셈블리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-123">In remote processing mode, the ReportViewer control uses the following assemblies:</span></span>

* <span data-ttu-id="d5324-124">**Microsoft.ReportViewer.WebForms.dll**: 페이지에서 ReportViewer를 사용하는 데 필요한 ReportViewer 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-124">**Microsoft.ReportViewer.WebForms.dll**: Contains the ReportViewer code, which you need to use ReportViewer in your page.</span></span> <span data-ttu-id="d5324-125">프로젝트의 ASP.NET 페이지로 ReportViewer 컨트롤을 끌어 놓으면 이 어셈블리에 대한 참조가 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-125">A reference for this assembly is added to your project when you drop a ReportViewer control onto an ASP.NET page in your project.</span></span>
* <span data-ttu-id="d5324-126">**Microsoft.ReportViewer.Common.dll**: 런타임 시 ReportViewer 컨트롤에서 사용하는 클래스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-126">**Microsoft.ReportViewer.Common.dll**: Contains classes used by the ReportViewer control at run time.</span></span> <span data-ttu-id="d5324-127">프로젝트에 자동으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-127">It is not automatically added to your project.</span></span>

### <a name="to-add-a-reference-to-microsoftreportviewercommon"></a><span data-ttu-id="d5324-128">Microsoft.ReportViewer.Common에 대한 참조를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="d5324-128">To add a reference to Microsoft.ReportViewer.Common</span></span>
* <span data-ttu-id="d5324-129">프로젝트의 **참조** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택한 다음 .NET 탭에서 어셈블리를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-129">Right-click your project’s **References** node and select **Add Reference**, select the assembly in the .NET tab, and click **OK**.</span></span>

### <a name="to-make-the-assemblies-locally-accessible-by-your-aspnet-application"></a><span data-ttu-id="d5324-130">ASP.NET 응용 프로그램에서 어셈블리를 로컬로 액세스할 수 있도록 하려면</span><span class="sxs-lookup"><span data-stu-id="d5324-130">To make the assemblies locally accessible by your ASP.NET application</span></span>
1. <span data-ttu-id="d5324-131">**참조** 폴더에서 Microsoft.ReportViewer.Common 어셈블리를 클릭하여 해당 속성을 속성 창에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-131">In the **References** folder, click the Microsoft.ReportViewer.Common assembly so that its properties appear in the Properties pane.</span></span>
2. <span data-ttu-id="d5324-132">속성 창에서 **로컬 복사** 를 True로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-132">In the Properties pane, set **Copy Local** to True.</span></span>
3. <span data-ttu-id="d5324-133">Microsoft.ReportViewer.WebForms에 대해 1단계 및 2단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-133">Repeat steps 1 and 2 for Microsoft.ReportViewer.WebForms.</span></span>

### <a name="to-get-reportviewer-language-pack"></a><span data-ttu-id="d5324-134">ReportViewer 언어 팩을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="d5324-134">To get ReportViewer Language Pack</span></span>
1. <span data-ttu-id="d5324-135">[Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=317386)에서 적절한 Microsoft Report Viewer 2012 런타임 재배포 가능 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-135">Install the appropriate Microsoft Report Viewer 2012 Runtime redistributable package from [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).</span></span>
2. <span data-ttu-id="d5324-136">드롭다운 목록에서 언어를 선택하면 페이지가 해당 다운로드 센터 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-136">Select the language from the dropdown list and the page gets redirected to the corresponding download center page.</span></span>
3. <span data-ttu-id="d5324-137">**다운로드** 를 클릭하여 ReportViewerLP.exe의 다운로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-137">Click **Download** to start the download of ReportViewerLP.exe.</span></span>
4. <span data-ttu-id="d5324-138">ReportViewerLP.exe를 다운로드한 후 **실행**을 클릭하여 즉시 설치하거나 **저장**을 클릭하여 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-138">After you download ReportViewerLP.exe, click **Run** to install immediately, or click **Save** to save it to your computer.</span></span> <span data-ttu-id="d5324-139">**저장**을 클릭하는 경우 파일을 저장하는 폴더의 이름을 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="d5324-139">If you click **Save**, remember the name of the folder where you save the file.</span></span>
5. <span data-ttu-id="d5324-140">파일을 저장한 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-140">Locate the folder where you saved the file.</span></span> <span data-ttu-id="d5324-141">ReportViewerLP.exe를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭한 다음 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-141">Right-click ReportViewerLP.exe, click **Run as administrator**, and then click **Yes**.</span></span>
6. <span data-ttu-id="d5324-142">ReportViewerLP.exe를 실행하면 c:\windows\assembly에서 리소스 파일 **Microsoft.ReportViewer.Webforms.Resources** 및 **Microsoft.ReportViewer.Common.Resources**를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-142">After running ReportViewerLP.exe, you will see the c:\windows\assembly has the resource files **Microsoft.ReportViewer.Webforms.Resources** and **Microsoft.ReportViewer.Common.Resources**.</span></span>

### <a name="to-configure-for-localized-reportviewer-control"></a><span data-ttu-id="d5324-143">지역화된 ReportViewer 컨트롤을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="d5324-143">To configure for localized ReportViewer control</span></span>
1. <span data-ttu-id="d5324-144">위에서 지정한 지침에 따라 Microsoft Report Viewer 2012 런타임 재배포 가능 패키지를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-144">Download and install the Microsoft Report Viewer 2012 Runtime redistributable package by following the above specified instructions.</span></span>
2. <span data-ttu-id="d5324-145">프로젝트에 <language> 폴더를 만들어 관련 리소스 어셈블리 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-145">Create <language> folder in the project and copy the associated resource assembly files there.</span></span> <span data-ttu-id="d5324-146">복사할 리소스 어셈블리 파일은 **Microsoft.ReportViewer.Webforms.Resources.dll** 및 **Microsoft.ReportViewer.Common.Resources.dll**입니다. 리소스 어셈블리 파일을 선택하고 속성 창에서 **출력 디렉터리에 복사**를 “**항상 복사**”로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-146">The resource assembly files to be copied are: **Microsoft.ReportViewer.Webforms.Resources.dll** and **Microsoft.ReportViewer.Common.Resources.dll**.Select the resource assembly files, and in the Properties pane, set **Copy to Output Directory** to “**Copy always**”.</span></span>
3. <span data-ttu-id="d5324-147">웹 프로젝트의 문화권 및 UI 문화권을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-147">Set the Culture & UICulture for the web project.</span></span> <span data-ttu-id="d5324-148">ASP.NET 웹 페이지의 문화권 및 UI 문화권을 설정하는 방법에 대한 자세한 내용은 [ASP.NET 웹 페이지 세계화를 위해 문화권 및 UI 문화권 설정 방법](http://go.microsoft.com/fwlink/?LinkId=237461)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5324-148">For more information about how to set the Culture and UI Culture for an ASP.NET Web page, see [How to: Set the Culture and UI Culture for ASP.NET Web Page Globalization](http://go.microsoft.com/fwlink/?LinkId=237461).</span></span>

## <a name="configuring-authentication-and-authorization"></a><span data-ttu-id="d5324-149">인증 및 권한 부여 구성</span><span class="sxs-lookup"><span data-stu-id="d5324-149">Configuring Authentication and Authorization</span></span>
<span data-ttu-id="d5324-150">ReportViewer는 적절한 자격 증명을 사용하여 보고서 서버로 인증해야 하고 원하는 보고서에 액세스하는 보고서 서버에서 자격 증명의 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-150">The ReportViewer needs to use proper credentials to authenticate with the report server, and the credentials must be authorized by the report server to access the reports you want.</span></span> <span data-ttu-id="d5324-151">인증에 대한 자세한 내용은 [Reporting Services 보고서 뷰어 컨트롤 및 Microsoft Azure 가상 컴퓨터 기반 보고서 서버](https://msdn.microsoft.com/library/azure/dn753698.aspx)백서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5324-151">For information on authentication, see the white paper [Reporting Services report viewer control and Microsoft Azure virtual machine based report servers](https://msdn.microsoft.com/library/azure/dn753698.aspx).</span></span>

## <a name="publish-the-aspnet-web-application-to-azure"></a><span data-ttu-id="d5324-152">Azure에 ASP.NET 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d5324-152">Publish the ASP.NET Web application to Azure</span></span>
<span data-ttu-id="d5324-153">Azure에 ASP.NET 웹 응용 프로그램을 게시하기 위한 지침은 [Visual Studio에서 Azure에 웹 응용 프로그램 마이그레이션 및 게시 방법](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) 및 [Web Apps 및 ASP.NET 시작](../../../app-service-web/app-service-web-get-started-dotnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5324-153">For instructions on publishing an ASP.NET Web application to Azure, see [How to: Migrate and Publish a Web Application to Azure from Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) and [Get started with Web Apps and ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5324-154">Azure 배포 프로젝트 추가 또는 Azure 클라우드 서비스 프로젝트 추가 명령이 솔루션 탐색기의 바로 가기 메뉴에 나타나지 않으면 프로젝트에 대한 대상 프레임워크를 .NET Framework 4로 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-154">If the Add Azure Deployment Project or Add Azure Cloud Service Project command does not appear in the shortcut menu in Solution Explorer, you may need to change the Target framework for the project to .NET Framework 4.</span></span>
> 
> <span data-ttu-id="d5324-155">두 명령은 근본적으로 동일한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-155">The two commands provide essentially the same functionality.</span></span> <span data-ttu-id="d5324-156">설치한 Microsoft Azure SDK의 버전에 따라 바로 가기 메뉴에 두 명령 중 하나가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5324-156">One or the other command will appear in the shortcut menu depending on which version of the Microsoft Azure SDK you have installed.</span></span>
> 
> 

## <a name="resources"></a><span data-ttu-id="d5324-157">리소스</span><span class="sxs-lookup"><span data-stu-id="d5324-157">Resources</span></span>
[<span data-ttu-id="d5324-158">Microsoft 보고서</span><span class="sxs-lookup"><span data-stu-id="d5324-158">Microsoft Reports</span></span>](http://go.microsoft.com/fwlink/?LinkId=205399)

[<span data-ttu-id="d5324-159">Azure 가상 컴퓨터의 SQL Server Business Intelligence</span><span class="sxs-lookup"><span data-stu-id="d5324-159">SQL Server Business Intelligence in Azure Virtual Machines</span></span>](../classic/ps-sql-bi.md)

[<span data-ttu-id="d5324-160">PowerShell을 사용하여 기본 모드 보고서 서버로 Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d5324-160">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>](../classic/ps-sql-report.md)

