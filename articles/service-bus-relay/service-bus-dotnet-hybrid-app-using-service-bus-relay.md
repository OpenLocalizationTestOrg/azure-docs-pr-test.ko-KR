---
title: "aaaAzure WCF 릴레이 하이브리드에-프레미스/클라우드 응용 프로그램 (.NET) | Microsoft Docs"
description: "자세한 내용은 방법 Azure WCF 릴레이 사용 하는.NET에서-프레미스/클라우드 toocreate 혼성 응용 프로그램입니다."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="cf30a-103">Azure WCF 릴레이를 사용하는 .NET 온-프레미스/클라우드 하이브리드 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cf30a-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="cf30a-104">소개</span><span class="sxs-lookup"><span data-stu-id="cf30a-104">Introduction</span></span>

<span data-ttu-id="cf30a-105">이 문서에서는 toobuild 하이브리드 응용 프로그램을 Microsoft Azure 및 Visual Studio 클라우드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="cf30a-106">hello 자습서에서는 Azure를 사용 하 여 이전 본 경험이 없는 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="cf30a-107">30 분 이내에 여러 Azure 리소스를 사용 하는 응용 프로그램 및 hello 클라우드에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="cf30a-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-108">You will learn:</span></span>

* <span data-ttu-id="cf30a-109">어떻게 toocreate 또는 웹 솔루션에 의해 소비에 대 한 기존 웹 서비스를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="cf30a-110">어떻게 toouse hello Azure WCF 릴레이 서비스 tooshare 데이터는 Azure 응용 프로그램 및 웹 서비스 간에 다른 곳에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="cf30a-111">하이브리드 솔루션에 유용한 Azure 릴레이</span><span class="sxs-lookup"><span data-stu-id="cf30a-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="cf30a-112">비즈니스 솔루션은 일반적으로 새 tootackle로 작성 된 사용자 지정 코드 및 고유한 비즈니스 요구 사항 및 솔루션 및 시스템에에서 이미 준비 되어을 제공 하는 기존 기능 조합으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="cf30a-113">솔루션 설계자는 toouse hello 클라우드 운영 비용 절감 및 확장 요구 사항을 보다 쉽게 처리를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="cf30a-114">이 과정에서 hello 클라우드 솔루션에 기존 서비스 자산 만족할 만한 tooleverage가 솔루션에 대 한 구성 요소는 hello 사내 방화벽 내부와 외부로 쉽게 도달할 액세스용 있음을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="cf30a-115">많은 내부 서비스를 작성 또는 노출 될 수 있으므로 쉽게 hello 회사 네트워크 가장자리에 방식으로 호스트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="cf30a-116">[Azure 릴레이](https://azure.microsoft.com/services/service-bus/) 용인지 기존 Windows Communication Foundation (WCF) 웹 서비스의 사용 사례 hello 및 안전 하 게 액세스할 수 있는 toosolutions 필요 없이 hello 회사 경계 외부에 있는 서비스 만들어 개입 수준이 변경 toohello 회사 네트워크 인프라를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="cf30a-117">이러한 릴레이 서비스를 여전히 기존 환경 내 호스트 하지만 들어오는 세션 및 요청 toohello 클라우드에 호스트 된 릴레이 서비스에 대 한 수신을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="cf30a-118">또한 Azure Relay는 [SAS(공유 액세스 서명](../service-bus-messaging/service-bus-sas.md)) 인증을 사용하여 이러한 서비스에 무단으로 액세스하지 못하도록 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="cf30a-119">솔루션 시나리오</span><span class="sxs-lookup"><span data-stu-id="cf30a-119">Solution scenario</span></span>
<span data-ttu-id="cf30a-120">이 자습서에서는 toosee hello 제품 인벤토리 페이지에서 제품 목록을 수 있는 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="cf30a-121">hello 자습서에서는 기존 온-프레미스 시스템을 제품 정보를 유지 하 고 Azure 릴레이 tooreach를 사용 하 여 해당 시스템으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="cf30a-122">간단한 콘솔 응용 프로그램에서 실행되며 메모리 내 제품 집합에서 지원되는 웹 서비스에서 이를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="cf30a-123">수 toorun이 콘솔 응용 프로그램 컴퓨터의 수 및 hello 웹 역할을 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="cf30a-124">이렇게 하면 표시 됩니다는 컴퓨터에 실제로 호출 하는 hello Azure 데이터 센터에서에서 실행 중인 hello 웹 역할 방법을 컴퓨터 하나 이상 방화벽 및 네트워크 주소 변환 (NAT) 계층 뒤에 있는 대부분은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="cf30a-125">Hello 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="cf30a-125">Set up hello development environment</span></span>

<span data-ttu-id="cf30a-126">Azure 응용 프로그램 개발을 시작 하려면 먼저 hello 도구를 다운로드 하 고 개발 환경을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="cf30a-127">Hello SDK에서에서 hello Azure SDK for.NET 설치 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="cf30a-128">Hello에 **.NET** 열 hello 버전 [Visual Studio](http://www.visualstudio.com) 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="cf30a-129">이 자습서 사용 하 여 Visual Studio 2015에서에서 hello 실행 하지만 Visual Studio 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="cf30a-130">Toorun 라는 메시지가 표시 하거나 저장 hello 설치 관리자를 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="cf30a-131">Hello에 **웹 플랫폼 설치 관리자**, 클릭 **설치** hello 설치를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="cf30a-132">Hello 설치가 완료 되 면 할 모든 필요한 toostart toodevelop hello 앱.</span><span class="sxs-lookup"><span data-stu-id="cf30a-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="cf30a-133">hello SDK는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="cf30a-134">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="cf30a-134">Create a namespace</span></span>

<span data-ttu-id="cf30a-135">Azure에서 릴레이 기능 hello toobegin를 사용 하 여, 서비스 네임 스페이스를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="cf30a-136">네임스페이스는 응용 프로그램 내에서 Azure 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="cf30a-137">Hello에 따라 [여기에 지침이](relay-create-namespace-portal.md) toocreate 릴레이 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="cf30a-138">온-프레미스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cf30a-138">Create an on-premises server</span></span>

<span data-ttu-id="cf30a-139">먼저, (모의) 온-프레미스 제품 카탈로그 시스템을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="cf30a-140">것은 매우 간단 합니다. 이 त ु म toointegrate 완전 한 서비스 화면과 상호 제품 카탈로그는 실제 온-프레미스 시스템을 나타내는 것으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="cf30a-141">이 프로젝트는 Visual Studio 콘솔 응용 프로그램 및 hello를 사용 하 여 [Azure Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello 구성 설정 및 서비스 버스 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="cf30a-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="cf30a-142">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cf30a-142">Create hello project</span></span>

1. <span data-ttu-id="cf30a-143">관리자 권한을 사용하여 Microsoft Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="cf30a-144">toodo 따라서 hello Visual Studio 프로그램 아이콘을 마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="cf30a-145">Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="cf30a-146">**설치된 템플릿**의 **Visual C#**에 있는 **콘솔 앱(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="cf30a-147">Hello에 **이름** 상자 hello 이름을 입력 합니다 **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="cf30a-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="cf30a-148">클릭 **확인** toocreate hello **ProductsServer** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="cf30a-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="cf30a-149">Visual Studio 용 NuGet 패키지 관리자 hello를 이미 설치한 경우 toohello 다음 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="cf30a-150">그렇지 않으면 [NuGet][NuGet]을 방문하여 [NuGet 설치](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="cf30a-151">Hello 프롬프트 tooinstall hello NuGet 패키지 관리자에 따라 다음 Visual Studio를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="cf30a-152">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsServer** 프로젝트를 선택한 다음 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="cf30a-153">Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="cf30a-154">선택 hello **WindowsAzure.ServiceBus** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="cf30a-155">클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="cf30a-156">이제 클라이언트 어셈블리를 참조 하는 데 해당 hello 필요한 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="cf30a-157">제품 계약의 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-157">Add a new class for your product contract.</span></span> <span data-ttu-id="cf30a-158">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsServer** 프로젝트 **추가**, 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="cf30a-159">Hello에 **이름** 상자 hello 이름을 입력 합니다 **ProductsContract.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="cf30a-160">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-160">Then click **Add**.</span></span>
10. <span data-ttu-id="cf30a-161">**ProductsContract.cs**, hello 서비스에 대 한 hello 계약을 정의 하는 코드를 다음 hello hello 네임 스페이스 정의 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="cf30a-162">Program.cs에 hello 네임 스페이스 정을 hello 프로필 서비스와 그에 대 한 hello 호스트를 추가 하는 코드를 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="cf30a-163">솔루션 탐색기에서 hello를 두 번 클릭 **App.config** tooopen 파일 hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="cf30a-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="cf30a-164">Hello hello 맨 아래에 `<system.ServiceModel>` 요소 (하지만 안에서 `<system.ServiceModel>`), hello 다음 XML 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="cf30a-165">수 있는지 tooreplace *yourServiceNamespace* 여 네임 스페이스의 hello 이름의 및 *yourKey* hello 포털에서 이전 검색 hello SAS 키를 가진:</span><span class="sxs-lookup"><span data-stu-id="cf30a-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="cf30a-166">Hello에 App.config에 여전히 `<appSettings>` 요소, replace hello 연결 문자열 값 hello 포털에서 이전에 가져온 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="cf30a-167">키를 눌러 **Ctrl + Shift + B** 또는 hello **빌드** 메뉴를 클릭 **솔루션 빌드** toobuild hello 응용 프로그램 및 지금까지 진행 중인 작업의 hello 정확도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="cf30a-168">ASP.NET 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cf30a-168">Create an ASP.NET application</span></span>

<span data-ttu-id="cf30a-169">이 섹션에서는 제품 서비스에서 검색한 데이터를 표시하는 간단한 ASP.NET 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="cf30a-170">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cf30a-170">Create hello project</span></span>

1. <span data-ttu-id="cf30a-171">관리자 권한으로 Visual Studio 2013을 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="cf30a-172">Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="cf30a-173">**설치된 템플릿**에서 **Visual C#** 아래에 있는 **ASP.NET 웹 응용 프로그램(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="cf30a-174">이름 hello 프로젝트 **ProductsPortal**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="cf30a-175">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="cf30a-176">Hello에서 **ASP.NET 템플릿** hello 목록 **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 클릭 **MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="cf30a-177">Hello 클릭 **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="cf30a-178">Hello에 **인증 변경** 대화 상자에서 **인증 안 함** 을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="cf30a-179">이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="cf30a-180">Hello에 다시 **새 ASP.NET 웹 응용 프로그램** 대화 상자를 클릭 하 여 **확인** toocreate hello MVC 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="cf30a-181">이제 새 웹앱에 대한 Azure 리소스를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="cf30a-182">Hello에 hello 단계를 따라 [이 문서의 섹션 tooAzure 게시](../app-service-web/app-service-web-get-started-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="cf30a-183">그런 다음 toothis 자습서 돌아간 toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="cf30a-184">솔루션 탐색기에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="cf30a-185">Hello에 **이름** 상자 hello 이름을 입력 합니다 **Product.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="cf30a-186">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="cf30a-187">Hello 웹 응용 프로그램 수정</span><span class="sxs-lookup"><span data-stu-id="cf30a-187">Modify hello web application</span></span>

1. <span data-ttu-id="cf30a-188">Visual Studio에서 hello Product.cs 파일에서 코드 다음 hello로 hello 기존 네임 스페이스 정의 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="cf30a-189">솔루션 탐색기에서 확장 hello **컨트롤러** 폴더 hello를 두 번 클릭 한 다음 **HomeController.cs** tooopen 파일 Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="cf30a-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="cf30a-190">**HomeController.cs**, 코드 다음 hello hello 기존 네임 스페이스 정의 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="cf30a-191">솔루션 탐색기에서 hello Views\Shared 폴더를 확장 한 다음를 두 번 클릭 **_Layout.cshtml** tooopen hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="cf30a-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="cf30a-192">모든 항목을 변경 **내 ASP.NET 응용 프로그램** 너무**LITWARE의 제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="cf30a-193">Hello 제거 **홈**, **에 대 한**, 및 **연락처** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="cf30a-194">다음 예제는 hello, hello 강조 표시 된 코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="cf30a-195">솔루션 탐색기에서 hello Views\Home 폴더를 확장 한 다음를 두 번 클릭 **Index.cshtml** tooopen hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="cf30a-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="cf30a-196">Hello 파일의 전체 내용을 hello 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="cf30a-197">작업의 tooverify hello 정확도 지금까지 누르면 **Ctrl + Shift + B** toobuild hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="cf30a-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="cf30a-198">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="cf30a-198">Run hello app locally</span></span>

<span data-ttu-id="cf30a-199">작동 하는 hello 응용 프로그램 tooverify를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="cf30a-200">되도록 **ProductsPortal** 는 hello 활성 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="cf30a-201">솔루션 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="cf30a-202">Visual Studio에서 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="cf30a-203">응용 프로그램이 브라우저에 실행되는 것으로 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="cf30a-204">Hello 조각 준비</span><span class="sxs-lookup"><span data-stu-id="cf30a-204">Put hello pieces together</span></span>

<span data-ttu-id="cf30a-205">hello 다음 단계는 toohook hello ASP.NET 응용 프로그램으로 hello 온-프레미스 제품 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="cf30a-206">열려 있지 않으면 Visual Studio에서 다시 열고 hello **ProductsPortal** hello에서 만든 프로젝트 [ASP.NET 응용 프로그램 만들기](#create-an-aspnet-application) 섹션.</span><span class="sxs-lookup"><span data-stu-id="cf30a-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="cf30a-207">Hello "온-프레미스 서버 만들기" 섹션에서 유사한 toohello 단계가 hello NuGet 패키지 toohello 프로젝트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="cf30a-208">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 선택한 다음 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="cf30a-209">"서비스 버스" 및 선택 hello에 대 한 검색 **WindowsAzure.ServiceBus** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="cf30a-210">그런 다음 hello 설치를 완료 하 고이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="cf30a-211">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 선택한 다음 클릭 **추가**, 다음 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="cf30a-212">Toohello 이동 **ProductsContract.cs** hello에서 파일 **ProductsServer** 콘솔 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="cf30a-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="cf30a-213">Toohighlight ProductsContract.cs를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="cf30a-214">아래쪽 화살표는 hello 다음 너무 클릭**추가**, 클릭 **링크로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="cf30a-215">이제 hello 열 **HomeController.cs** hello Visual Studio 편집기에서 파일 및 코드 다음 hello hello 네임 스페이스 정의 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="cf30a-216">수 있는지 tooreplace *yourServiceNamespace* 서비스 네임 스페이스의 hello 이름의 및 *yourKey* SAS 키를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="cf30a-217">이렇게 하면 hello 클라이언트 toocall hello 온-프레미스 서비스 에서도 hello hello 호출 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="cf30a-218">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 솔루션 (확인 되었는지 tooright 클릭 hello 솔루션을 hello 프로젝트가 아닌).</span><span class="sxs-lookup"><span data-stu-id="cf30a-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="cf30a-219">**추가**를 클릭한 후 **기존 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="cf30a-220">Toohello 이동 **ProductsServer** hello를 두 번 클릭 한 다음 프로젝트를 **ProductsServer.csproj** 솔루션 파일 tooadd 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="cf30a-221">**ProductsServer** 주문 toodisplay hello 데이터에서 실행 되어야 합니다 **ProductsPortal**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="cf30a-222">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 솔루션과 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="cf30a-223">hello **속성 페이지** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="cf30a-224">왼쪽 hello, 클릭 **시작 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="cf30a-225">Hello 오른쪽 클릭 **여러 개의 시작 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="cf30a-226">되도록 **ProductsServer** 및 **ProductsPortal** 를 해당 순서로 함께 표시 **시작** 모두에 대 한 hello 동작으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="cf30a-227">Hello에 여전히 **속성** 대화 상자에서 클릭 **프로젝트 종속성** hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="cf30a-228">Hello에 **프로젝트** 목록에서 클릭 **ProductsServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="cf30a-229">**ProductsPortal**이 선택되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="cf30a-230">Hello에 **프로젝트** 목록에서 클릭 **ProductsPortal**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="cf30a-231">**ProductsServer**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="cf30a-232">클릭 **확인** hello에 **속성 페이지** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cf30a-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="cf30a-233">Hello 프로젝트를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="cf30a-233">Run hello project locally</span></span>

<span data-ttu-id="cf30a-234">눌러 Visual Studio에서 tootest hello 응용 프로그램을 로컬로 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="cf30a-235">hello 온-프레미스 서버 (**ProductsServer**), 첫 번째로 시작 해야 하 고 hello **ProductsPortal** 응용 프로그램이 브라우저 창에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="cf30a-236">이 이번에 표시 됩니다는 hello 제품 재고 hello 제품 서비스 온-프레미스 시스템에서 검색 된 데이터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="cf30a-237">키를 눌러 **새로 고침** hello에 **ProductsPortal** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cf30a-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="cf30a-238">때마다 hello 페이지를 새로 고침, 메시지를 표시 하는 hello 서버 응용 프로그램에 표시 됩니다 때 `GetProducts()` 에서 **ProductsServer** 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="cf30a-239">Toohello 다음 단계를 진행 하기 전에 두 응용 프로그램을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="cf30a-240">Hello ProductsPortal 프로젝트 tooan Azure 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="cf30a-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="cf30a-241">hello 다음 단계는 toorepublish hello Azure 웹 앱 **ProductsPortal** 프런트 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="cf30a-242">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-242">Do hello following:</span></span>

1. <span data-ttu-id="cf30a-243">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 마우스 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="cf30a-244">클릭 **게시** hello에 **게시** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cf30a-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cf30a-245">때 hello hello 브라우저 창에서 오류 메시지가 표시 될 수 있습니다 **ProductsPortal** 웹 프로젝트 hello 배포 후 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="cf30a-246">이 예상 된 하 고 있기 때문에 발생 hello **ProductsServer** 응용 프로그램이 아직 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="cf30a-247">Hello의 hello URL 복사 hello URL hello 다음 단계에서 필요 하므로 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="cf30a-248">또한 Visual Studio의 hello Azure 앱 서비스 활동 창에서이 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="cf30a-249">응용 프로그램을 실행 하는 hello 브라우저 창 toostop hello를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="cf30a-250">웹앱으로 ProductsPortal 설정</span><span class="sxs-lookup"><span data-stu-id="cf30a-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="cf30a-251">Hello 클라우드에서 실행 중인 hello 응용 프로그램을 하기 전에 확인 해야 **ProductsPortal** 웹 앱과 Visual Studio 내에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="cf30a-252">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="cf30a-253">Hello 왼쪽 열에서 클릭 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="cf30a-254">Hello에 **시작 작업** 섹션에서 hello **시작 URL** 단추 hello 텍스트 상자에 URL을 입력 hello; 이전에 배포 된 웹 앱에 대 한 예를 들어 `http://productsportal1234567890.azurewebsites.net/`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="cf30a-255">Hello에서 **파일** Visual Studio에서 메뉴를 클릭 **모두 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="cf30a-256">Visual Studio에서 hello 빌드 메뉴에서 클릭 **솔루션 다시 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="cf30a-257">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cf30a-257">Run hello application</span></span>

1. <span data-ttu-id="cf30a-258">F5 toobuild 누르고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="cf30a-259">hello 온-프레미스 서버 (hello **ProductsServer** 콘솔 응용 프로그램), 첫 번째로 시작 해야 하 고 hello **ProductsPortal** hello 화면 뒤에 나와 있는 것 처럼 응용 프로그램이 브라우저 창에서 시작 됩니다 샷 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="cf30a-260">해당 hello 제품 재고 hello 제품 서비스 온-프레미스 시스템에서 검색 된 데이터를 나열 하 고 hello 웹 응용 프로그램에서 해당 데이터를 표시 합니다. 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="cf30a-261">Hello URL toomake 있는지를 확인 하는 **ProductsPortal** hello 클라우드의 Azure 웹 앱으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="cf30a-262">hello **ProductsServer** 콘솔 응용 프로그램 실행 해야 하며 수 tooserve hello 데이터 toohello **ProductsPortal** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="cf30a-263">Hello 브라우저에 오류가 표시 되는 경우 더 많은 몇 초 정도 대기 **ProductsServer** tooload 및 다음 디스플레이 hello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="cf30a-264">다음 키를 누릅니다 **새로 고침** hello 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="cf30a-265">Hello 브라우저에서 다시 눌러 **새로 고침** hello에 **ProductsPortal** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cf30a-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="cf30a-266">때마다 hello 페이지를 새로 고침, 메시지를 표시 하는 hello 서버 응용 프로그램에 표시 됩니다 때 `GetProducts()` 에서 **ProductsServer** 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf30a-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="cf30a-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf30a-267">Next steps</span></span>

<span data-ttu-id="cf30a-268">toolearn Azure 릴레이 대 한 자세한 참조 리소스 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="cf30a-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="cf30a-269">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="cf30a-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="cf30a-270">Toouse 릴레이 하는 방법</span><span class="sxs-lookup"><span data-stu-id="cf30a-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
