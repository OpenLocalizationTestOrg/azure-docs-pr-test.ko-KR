---
title: ".NET을 사용하여 미디어 서비스 개발을 위한 컴퓨터를 설정하는 방법"
description: "미디어 서비스 .NET SDK를 사용하는 미디어 서비스에 대한 일반적인 필수 구성 요소에 대해 알아봅니다. 또한 Visual Studio 앱을 만드는 방법에 대해서도 알아봅니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="37538-104">.NET을 사용한 미디어 서비스 개발</span><span class="sxs-lookup"><span data-stu-id="37538-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="37538-105">이 항목에서는.NET을 사용하여 미디어 서비스 응용 프로그램 개발을 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="37538-106">**Azure 미디어 서비스 .NET SDK** 라이브러리를 사용하면 .NET을 사용하여 미디어 서비스를 프로그래밍 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="37538-107">.NET을 사용한 개발을 더욱 쉽게 도와주는 **Azure 미디어 서비스 .NET SDK 확장** 라이브러리가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37538-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="37538-108">이 라이브러리는 .NET 코드를 단순화하는 일련의 확장 방법 및 도우미 함수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="37538-109">두 라이브러리 모두 **NuGet** 및 **GitHub**를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37538-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="37538-110">Prerequisites</span></span>
* <span data-ttu-id="37538-111">신규 또는 기존 Azure 구독의 미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="37538-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="37538-112">[Media Services 계정을 만드는 방법](media-services-portal-create-account.md) 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37538-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="37538-113">운영 체제: Windows 10, Windows 7, Windows 2008 R2 또는 Windows 8.</span><span class="sxs-lookup"><span data-stu-id="37538-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="37538-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="37538-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="37538-115">있습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="37538-116">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="37538-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="37538-117">이 섹션에서는 Visual Studio에서 프로젝트를 생성하고 미디어 서비스 개발에 대해 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="37538-118">이 경우에 프로젝트는 C# Windows 콘솔 응용 프로그램이지만 여기에 설명된 설정 방법은 Media Services 응용 프로그램에 생성할 수 있는 다른 프로젝트 유형에도 그대로 적용됩니다(예: Windows Forms 응용 프로그램 또는 ASP.NET 웹 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="37538-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="37538-119">이 섹션에서는 Media Services .NET SDK 확장 추가를 위한 **NuGet** 을 사용하는 방법과 기타 종속된 라이브러리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37538-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="37538-120">또는 GitHub에서 최신 Media Services .NET SDK 비트를 가져오고([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) 또는 [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) 솔루션을 빌드하고 클라이언트 프로젝트에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="37538-121">필요한 종속성은 모두 자동으로 다운로드되고 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="37538-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="37538-122">Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37538-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="37538-123">**이름**, **위치** 및 **솔루션 이름**을 입력하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="37538-124">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="37538-124">Build the solution.</span></span>
3. <span data-ttu-id="37538-125">**NuGet**을 사용하여 **Azure Media Services .NET SDK Extensions**(**windowsazure.mediaservices.extensions**)를 설치한 후 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="37538-126">이 패키지를 설치하면 **미디어 서비스 .NET SDK** 도 설치되고 다른 모든 필수 종속성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="37538-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="37538-127">최신 버전의 NuGet이 설치 되어있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="37538-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="37538-128">자세한 내용 및 설치 지침은 [NuGet](http://nuget.codeplex.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37538-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="37538-129">솔루션 Explorer에서 프로젝트의 이름을 마우스 오른쪽 단추를 클릭하고 [NuGet 패키지 관리]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="37538-130">NuGet 패키지 관리 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37538-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="37538-131">온라인 갤러리에서 Azure 미디어 서비스 확장에 대한 검색하여 Azure 미디어 서비스 .NET SDK 확장을 선택한 다음 설치 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="37538-132">프로젝트가 수정되고 Media Services .NET SDK 확장, Media Services .NET SDK 및 기타 종속 어셈블리에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="37538-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="37538-133">클리너 개발 환경의 수준을 올릴 NuGet 패키지 복원을 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="37538-134">자세한 내용은 [NuGet 패키지 복원"](http://docs.nuget.org/consume/package-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37538-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="37538-135">**System.Configuration** 어셈블리에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="37538-136">이 어셈블리는 구성 파일(예: App.config)에 액세스하는 데 사용되는 System.Configuration.**ConfigurationManager** 클래스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="37538-137">참조 관리 대화 상자를 사용하여 참조를 추가하려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="37538-138">그런 다음 추가 및 참조를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="37538-139">참조 관리 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37538-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="37538-140">.NET framework 어셈블리에서 찾아 System.Configuration 어셈블리를 찾아 선택하고 확인을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37538-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="37538-141">App.config 파일을 열고 파일에 *appSettings* 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="37538-142">Media Services API에 연결하는 데 필요한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="37538-143">자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37538-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="37538-144">[사용자 인증](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication)을 사용 중인 경우 구성 파일에 Azure AD 테넌트 도메인과 AMS REST API 끝점에 대한 값이 포함되어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37538-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="37538-145">Azure Media Services 설명서 모음의 코드 샘플은 대부분 사용자(대화형) 유형의 인증을 사용하여 AMS API에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="37538-146">이 인증 방법은 네이티브 앱(모바일 앱, Windows 앱 및 콘솔 응용 프로그램)의 관리 또는 모니터링에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="37538-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="37538-147">이 인증 방법은 서버, 웹 서비스, API 유형의 응용 프로그램에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="37538-148">자세한 내용은 [Azure AD 인증을 사용하여 AMS API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37538-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="37538-149">다음 코드를 사용하여 Program.cs 파일의 앞부분에 있는 기존 **using** 문을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="37538-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="37538-150">이제 미디어 서비스 응용 프로그램 개발을 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="37538-151">예제</span><span class="sxs-lookup"><span data-stu-id="37538-151">Example</span></span>

<span data-ttu-id="37538-152">다음은 AMS API에 연결하고 사용 가능한 모든 미디어 프로세서를 나열하는 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="37538-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="37538-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37538-153">Next steps</span></span>

<span data-ttu-id="37538-154">이제 [AMS API에 연결하고](media-services-use-aad-auth-to-access-ams-api.md) [개발](media-services-dotnet-get-started.md)을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37538-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="37538-155">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="37538-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="37538-156">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="37538-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

