---
title: "aaaHow tooSet를 컴퓨터에.net 미디어 서비스 개발"
description: ".NET 용 미디어 서비스 SDK hello를 사용 하 여 미디어 서비스에 대 한 hello 필수 구성 요소에 알아봅니다. 또한 학습 방법을 toocreate Visual Studio 응용 프로그램입니다."
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="da2e7-104">.NET을 사용한 미디어 서비스 개발</span><span class="sxs-lookup"><span data-stu-id="da2e7-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="da2e7-105">이 항목에서는 방법을 toostart 개발 미디어 서비스.NET을 사용 하 여 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="da2e7-106">hello **Azure 미디어 서비스.NET SDK** 라이브러리를 사용 하면.NET을 사용 하 여 미디어 서비스에 대해 tooprogram 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="da2e7-107">것에.net을 보다 쉽게 toodevelop hello toomake **Azure 미디어 서비스.NET SDK Extensions** 라이브러리가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="da2e7-108">이 라이브러리는 .NET 코드를 단순화하는 일련의 확장 방법 및 도우미 함수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="da2e7-109">두 라이브러리 모두 **NuGet** 및 **GitHub**를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da2e7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da2e7-110">Prerequisites</span></span>
* <span data-ttu-id="da2e7-111">신규 또는 기존 Azure 구독의 미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="da2e7-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="da2e7-112">Hello에 대 한 지침은 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="da2e7-113">운영 체제: Windows 10, Windows 7, Windows 2008 R2 또는 Windows 8.</span><span class="sxs-lookup"><span data-stu-id="da2e7-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="da2e7-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="da2e7-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="da2e7-115">있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="da2e7-116">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="da2e7-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="da2e7-117">이 섹션에서는 Visual Studio에서 프로젝트 toocreate 미디어 서비스 개발을 위해 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="da2e7-118">이 경우 hello 프로젝트는 C# Windows 콘솔 응용 프로그램 있지만 hello 여기에 표시 된 같은 설정 단계 적용 tooother 유형의 프로젝트 (예: Windows Forms 응용 프로그램 또는 ASP.NET 웹 응용 프로그램) 미디어 서비스 응용 프로그램에 대해 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="da2e7-119">이 섹션에서는 방법을 toouse **NuGet** tooadd 미디어 서비스.NET SDK extensions와 다른 종속 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="da2e7-120">또는 GitHub에서 hello 최신 미디어 서비스.NET SDK 비트를 얻을 수 있습니다 ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) 또는 [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) hello 솔루션을 빌드하고 hello 참조 toohello 클라이언트 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="da2e7-121">모든 hello 필요한 종속성을 다운로드 하 고 자동으로 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="da2e7-122">Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="da2e7-123">Hello 입력 **이름**, **위치**, 및 **솔루션 이름**, 한 다음 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="da2e7-124">Hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="da2e7-124">Build hello solution.</span></span>
3. <span data-ttu-id="da2e7-125">사용 하 여 **NuGet** tooinstall 추가 **Azure 미디어 서비스.NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="da2e7-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="da2e7-126">이 패키지를 설치하면 **미디어 서비스 .NET SDK** 도 설치되고 다른 모든 필수 종속성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="da2e7-127">Hello 최신 버전의 NuGet이 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="da2e7-128">자세한 내용 및 설치 지침은 [NuGet](http://nuget.codeplex.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da2e7-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="da2e7-129">솔루션 탐색기에서 hello hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 관리 하는 NuGet 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="da2e7-130">hello NuGet 패키지 관리 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="da2e7-131">Azure MediaServices Extensions 검색 hello 온라인 갤러리에서 Azure 미디어 서비스.NET SDK Extensions를 선택 하 고 hello 설치 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="da2e7-132">hello 프로젝트가 수정 되 고 toohello 미디어 서비스.NET SDK Extensions, 미디어 서비스.NET SDK를 참조 하 고 다른 종속 어셈블리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="da2e7-133">toopromote 클리너 개발 환경에서는 NuGet 패키지 복원을 활성화 하십시오.</span><span class="sxs-lookup"><span data-stu-id="da2e7-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="da2e7-134">자세한 내용은 [NuGet 패키지 복원"](http://docs.nuget.org/consume/package-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da2e7-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="da2e7-135">참조를 너무 추가**System.Configuration** 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="da2e7-136">이 어셈블리는 hello System.Configuration을 포함합니다. **ConfigurationManager** 클래스 즉 tooaccess 사용 되는 구성 파일 (예를 들어 App.config).</span><span class="sxs-lookup"><span data-stu-id="da2e7-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="da2e7-137">hello 참조 관리 대화 상자를 사용 하 여 tooadd 참조 hello 솔루션 탐색기에서에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="da2e7-138">그런 다음 추가 및 참조를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="da2e7-139">hello 참조 관리 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="da2e7-140">.NET framework 어셈블리에서 hello System.Configuration 어셈블리 찾기 선택한 확인 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="da2e7-141">Hello App.config 파일을 열고 추가 된 *appSettings* 섹션 toohello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="da2e7-142">Hello 값을 필요한 tooconnect toohello 미디어 서비스 API를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="da2e7-143">자세한 내용은 참조 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="da2e7-144">사용 중인 경우 [사용자 인증](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) 구성 파일은 Azure AD 테 넌 트 도메인에 대 한 값 및 hello AMS REST API 끝점 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="da2e7-145">대부분의 코드 샘플 hello Azure 미디어 서비스 설명서에에서 설정, 인증 tooconnect toohello AMS API의 사용자 (대화형) 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="da2e7-146">이 인증 방법은 네이티브 앱(모바일 앱, Windows 앱 및 콘솔 응용 프로그램)의 관리 또는 모니터링에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="da2e7-147">이 인증 방법은 서버, 웹 서비스, API 유형의 응용 프로그램에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="da2e7-148">자세한 내용은 참조 [Azure AD 인증 액세스 hello AMS API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="da2e7-149">Hello 기존 파일 덮어쓰기 **를 사용 하 여** hello 시작 부분에 코드 다음 hello로 hello Program.cs 파일의 문입니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="da2e7-150">이 시점에서 미디어 서비스 응용 프로그램을 개발 하는 준비 toostart 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="da2e7-151">예제</span><span class="sxs-lookup"><span data-stu-id="da2e7-151">Example</span></span>

<span data-ttu-id="da2e7-152">Toohello AMS API를 연결 하 고 사용 가능한 모든 미디어 프로세서를 나열 하는 작은 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="da2e7-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da2e7-153">Next steps</span></span>

<span data-ttu-id="da2e7-154">이제 [toohello AMS API를 연결할 수 있습니다](media-services-use-aad-auth-to-access-ams-api.md) 시작 [개발](media-services-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da2e7-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="da2e7-155">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="da2e7-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="da2e7-156">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="da2e7-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

