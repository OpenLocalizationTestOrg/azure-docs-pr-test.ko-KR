---
title: "Azure WCF Relay 하이브리드 온-프레미스/클라우드 응용 프로그램(.NET) | Microsoft Docs"
description: "Azure WCF 릴레이를 사용하여 .NET 온-프레미스/클라우드 하이브리드 응용 프로그램을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="f3f46-103">Azure WCF 릴레이를 사용하는 .NET 온-프레미스/클라우드 하이브리드 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="f3f46-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="f3f46-104">소개</span><span class="sxs-lookup"><span data-stu-id="f3f46-104">Introduction</span></span>

<span data-ttu-id="f3f46-105">이 문서에서는 Microsoft Azure 및 Visual Studio로 하이브리드 클라우드 응용 프로그램을 구축하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="f3f46-106">이 자습서에서는 이전에 Azure를 사용한 경험이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="f3f46-107">30분 이내에 여러 Azure 리소스를 사용하는 응용 프로그램을 클라우드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="f3f46-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-108">You will learn:</span></span>

* <span data-ttu-id="f3f46-109">웹 서비스를 만들거나 기존 웹 서비스를 웹 솔루션에서 사용할 수 있도록 변경하는 방법</span><span class="sxs-lookup"><span data-stu-id="f3f46-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="f3f46-110">Azure WCF 릴레이 서비스를 사용하여 Azure 응용 프로그램과 다른 위치에서 호스트되는 웹 서비스 사이에 데이터를 공유하는 방법</span><span class="sxs-lookup"><span data-stu-id="f3f46-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="f3f46-111">하이브리드 솔루션에 유용한 Azure 릴레이</span><span class="sxs-lookup"><span data-stu-id="f3f46-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="f3f46-112">비즈니스 솔루션은 일반적으로 새로운 고유 비즈니스 요구 사항에 부합하도록 작성된 사용자 지정 코드와 이미 있는 솔루션 및 시스템에서 제공하는 기존 기능의 조합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="f3f46-113">솔루션 설계자는 확장 요구 사항을 더 간편하게 처리하고 운영 비용을 낮추기 위해 클라우드를 사용하기 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="f3f46-114">클라우드를 사용하면 솔루션의 구성 요소로 활용할 기존 서비스 자산이 회사 방화벽 내부에 위치하게 되며 클라우드 솔루션에서 이 자산에 쉽게 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="f3f46-115">다수의 내부 서비스는 회사 네트워크 가장자리에서 쉽게 노출될 수 있는 방식으로 빌드되거나 호스트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="f3f46-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/)는 회사 네트워크 인프라에 대한 침입적인 변경 없이도 회사 범위 외부에 있는 솔루션에서 기존 WCF(Windows Communication Foundation) 웹 서비스에 안전하게 액세스할 수 있게 만드는 사용 사례를 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="f3f46-117">이러한 릴레이 서비스는 기존 환경 내에 계속 호스트되지만 클라우드 호스트 릴레이 서비스에 들어오는 세션 및 요청에 대한 수신을 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="f3f46-118">또한 Azure Relay는 [SAS(공유 액세스 서명](../service-bus-messaging/service-bus-sas.md)) 인증을 사용하여 이러한 서비스에 무단으로 액세스하지 못하도록 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="f3f46-119">솔루션 시나리오</span><span class="sxs-lookup"><span data-stu-id="f3f46-119">Solution scenario</span></span>
<span data-ttu-id="f3f46-120">이 자습서에서는 제품 재고 페이지에 제품 목록을 표시할 수 있는 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="f3f46-121">이 자습서는 기존 온-프레미스 시스템에 제품 정보가 있으며 해당 시스템에 도달하는 데 Azure 릴레이를 사용하는 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="f3f46-122">간단한 콘솔 응용 프로그램에서 실행되며 메모리 내 제품 집합에서 지원되는 웹 서비스에서 이를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="f3f46-123">개발자는 자신의 컴퓨터에서 이 콘솔 응용 프로그램을 실행하여 Azure에 웹 역할을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="f3f46-124">이렇게 함으로써, 개발자의 컴퓨터가 하나 이상의 방화벽 및 NAT(Network Address Translation) 계층 뒤에 위치하는 것이 거의 확실한 경우에도 Azure 데이터 센터에서 실행 중인 웹 역할이 실제로 개발자의 컴퓨터에 호출되는 것을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="f3f46-125">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f3f46-125">Set up the development environment</span></span>

<span data-ttu-id="f3f46-126">Azure 응용 프로그램 개발을 시작하려면 먼저 도구를 다운로드하고 개발 환경을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="f3f46-127">SDK [다운로드 페이지](https://azure.microsoft.com/downloads/)에서 .NET용 Azure SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f3f46-128">**.NET** 열에서 사용 중인 [Visual Studio](http://www.visualstudio.com) 버전을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="f3f46-129">이 자습서의 단계에서는 Visual Studio 2015를 사용하지만 Visual Studio 2017에도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="f3f46-130">설치 관리자를 실행할지 또는 저장할지를 묻는 메시지가 표시되면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="f3f46-131">**웹 플랫폼 설치 관리자**에서 **설치**를 클릭하여 설치를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="f3f46-132">설치가 완료되면 앱을 개발하기 시작하는 데 필요한 내용이 모두 준비된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="f3f46-133">SDK에는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="f3f46-134">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f46-134">Create a namespace</span></span>

<span data-ttu-id="f3f46-135">Azure에서 릴레이 기능 사용을 시작하려면 먼저 서비스 네임스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="f3f46-136">네임스페이스는 응용 프로그램 내에서 Azure 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="f3f46-137">[여기의 지침](relay-create-namespace-portal.md)을 따라 릴레이 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="f3f46-138">온-프레미스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f46-138">Create an on-premises server</span></span>

<span data-ttu-id="f3f46-139">먼저, (모의) 온-프레미스 제품 카탈로그 시스템을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="f3f46-140">매우 간단합니다. 통합하려는 전체 서비스 표면이 있는 실제 온-프레미스 제품 카탈로그 시스템을 나타내는 것으로 생각하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="f3f46-141">이 프로젝트는 Visual Studio 콘솔 응용 프로그램으로, [Azure Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)를 사용하여 Service Bus 라이브러리 및 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="f3f46-142">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f46-142">Create the project</span></span>

1. <span data-ttu-id="f3f46-143">관리자 권한을 사용하여 Microsoft Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="f3f46-144">이렇게 하려면 Visual Studio 프로그램 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="f3f46-145">Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="f3f46-146">**설치된 템플릿**의 **Visual C#**에 있는 **콘솔 앱(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="f3f46-147">**이름** 상자에서 이름을 **ProductsServer**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="f3f46-148">**확인**을 클릭하여 **ProductsServer** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="f3f46-149">Visual Studio용 NuGet 패키지 관리자를 이미 설치한 경우 다음 단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="f3f46-150">그렇지 않으면 [NuGet][NuGet]을 방문하여 [NuGet 설치](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="f3f46-151">나타나는 메시지에 따라 NuGet 패키지 관리자를 설치한 후 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="f3f46-152">솔루션 탐색기에서 **ProductsServer** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="f3f46-153">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f3f46-154">**WindowsAzure.ServiceBus** 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="f3f46-155">**설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="f3f46-156">필요한 클라이언트 어셈블리가 이제 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="f3f46-157">제품 계약의 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-157">Add a new class for your product contract.</span></span> <span data-ttu-id="f3f46-158">솔루션 탐색기에서 **ProductsServer** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="f3f46-159">**이름** 상자에서 이름을 **ProductsContract.cs**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="f3f46-160">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-160">Then click **Add**.</span></span>
10. <span data-ttu-id="f3f46-161">**ProductsContract.cs**에서 네임스페이스 정의를 다음 코드로 바꿉니다. 이 코드는 서비스의 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="f3f46-162">Program.cs에서 네임스페이스 정의를 다음 코드로 바꿉니다. 이 코드는 프로필 서비스 및 그에 대한 호스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="f3f46-163">솔루션 탐색기에서 **App.config** 파일을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="f3f46-164">`<system.ServiceModel>` 요소의 아래쪽에서(여전히 `<system.ServiceModel>` 내에 있음) 다음 XML 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="f3f46-165">*yourServiceNamespace*를 네임스페이스의 이름으로 바꾸고 *yourKey*를 앞에서 포털에서 검색한 SAS 키로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="f3f46-166">계속 App.config의 `<appSettings>` 요소에서 연결 문자열 값을 포털에서 이전에 얻은 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="f3f46-167">**Ctrl+Shift+B** 키를 누르거나 **빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 응용 프로그램을 빌드한 후 지금까지 진행한 작업의 정확도를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="f3f46-168">ASP.NET 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f46-168">Create an ASP.NET application</span></span>

<span data-ttu-id="f3f46-169">이 섹션에서는 제품 서비스에서 검색한 데이터를 표시하는 간단한 ASP.NET 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="f3f46-170">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f46-170">Create the project</span></span>

1. <span data-ttu-id="f3f46-171">관리자 권한으로 Visual Studio 2013을 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="f3f46-172">Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="f3f46-173">**설치된 템플릿**에서 **Visual C#** 아래에 있는 **ASP.NET 웹 응용 프로그램(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="f3f46-174">프로젝트의 이름을 **ProductsPortal**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="f3f46-175">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="f3f46-176">**새 ASP.NET 웹 응용 프로그램** 대화 상자의 **ASP.NET 템플릿** 목록에서 **MVC**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="f3f46-177">**인증 변경** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="f3f46-178">**인증 변경** 대화 상자에서 **인증 없음**을 선택했는지 확인한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="f3f46-179">이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="f3f46-180">**새 ASP.NET 웹 응용 프로그램** 대화 상자로 돌아와서 **확인**을 클릭하여 MVC 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="f3f46-181">이제 새 웹앱에 대한 Azure 리소스를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="f3f46-182">[이 문서의 Azure 섹션에 게시](../app-service-web/app-service-web-get-started-dotnet.md)의 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="f3f46-183">그런 다음, 이 자습서로 돌아가 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="f3f46-184">솔루션 탐색기에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="f3f46-185">**이름** 상자에서 이름을 **Product.cs**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="f3f46-186">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="f3f46-187">웹 응용 프로그램 수정</span><span class="sxs-lookup"><span data-stu-id="f3f46-187">Modify the web application</span></span>

1. <span data-ttu-id="f3f46-188">Visual Studio의 Product.cs 파일에서 기존 네임스페이스 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="f3f46-189">솔루션 탐색기에서 **컨트롤러** 폴더를 확장하고 **HomeController.cs**를 두 번 클릭하여 Visual Studio에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="f3f46-190">**HomeController.cs**에서 기존 네임스페이스 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="f3f46-191">솔루션 탐색기에서 Views\Shared 폴더를 확장하고 **_Layout.cshtml**을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="f3f46-192">**내 ASP.NET 응용 프로그램**의 모든 항목을 **LITWARE 제품**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="f3f46-193">**홈**, **정보** 및 **연락처** 링크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="f3f46-194">다음 예제에서 강조 표시된 코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="f3f46-195">솔루션 탐색기에서 Views\Home 폴더를 확장하고 **Index.cshtml**을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="f3f46-196">파일의 전체 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="f3f46-197">지금까지 진행한 작업의 정확도를 확인하려면 **Ctrl+Shift+B**를 눌러 프로젝트를 빌드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="f3f46-198">로컬에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="f3f46-198">Run the app locally</span></span>

<span data-ttu-id="f3f46-199">응용 프로그램을 실행하여 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="f3f46-200">**ProductsPortal**이 활성 프로젝트인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="f3f46-201">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="f3f46-202">Visual Studio에서 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="f3f46-203">응용 프로그램이 브라우저에 실행되는 것으로 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="f3f46-204">부분 연결</span><span class="sxs-lookup"><span data-stu-id="f3f46-204">Put the pieces together</span></span>

<span data-ttu-id="f3f46-205">다음 단계는 온-프레미스 제품 서버를 ASP.NET 응용 프로그램과 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="f3f46-206">아직 열려 있지 않은 경우 [ASP.NET 응용 프로그램 만들기](#create-an-aspnet-application) 섹션에서 만든 **ProductsPortal** 프로젝트를 Visual Studio에서 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="f3f46-207">"온-프레미스 서버 만들기" 섹션의 단계와 비슷하게 프로젝트 참조에 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="f3f46-208">솔루션 탐색기에서 **ProductsPortal** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="f3f46-209">"Service Bus"를 검색하고 **WindowsAzure.ServiceBus** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="f3f46-210">그런 다음 설치를 완료하고 이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="f3f46-211">솔루션 탐색기에서 **ProductsPortal** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="f3f46-212">**ProductsServer** 콘솔 프로젝트에서 **ProductsContract.cs** 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="f3f46-213">ProductsContract.cs를 클릭하여 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="f3f46-214">**추가** 옆의 아래쪽 화살표를 클릭한 다음 **링크로 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="f3f46-215">이제 Visual Studio 편집기에서 **HomeController.cs** 파일을 열고 네임스페이스 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="f3f46-216">*yourServiceNamespace*를 서비스 네임스페이스의 이름으로 바꾸고 *yourKey*를 SAS 키로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="f3f46-217">이렇게 하면 클라이언트에서 온-프레미스 서비스를 호출하여 호출 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="f3f46-218">솔루션 탐색기에서 **ProductsPortal** 솔루션을 마우스 오른쪽 단추로 클릭합니다(프로젝트가 아닌 솔루션을 마우스 오른쪽 단추로 클릭해야 함).</span><span class="sxs-lookup"><span data-stu-id="f3f46-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="f3f46-219">**추가**를 클릭한 후 **기존 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="f3f46-220">**ProductsServer** 프로젝트로 이동한 후 **ProductsServer.csproj** 솔루션 파일을 두 번 클릭하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="f3f46-221">**ProductsPortal**에 데이터를 표시하기 위해서는 **ProductsServer**가 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="f3f46-222">솔루션 탐색기에서 **ProductsPortal** 솔루션을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="f3f46-223">**속성 페이지** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="f3f46-224">왼쪽에서 **시작 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="f3f46-225">오른쪽에서 **여러 시작 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="f3f46-226">**ProductsServer** 및 **ProductsPortal** 모두에 대한 작업으로 **시작**이 설정되어 순서대로 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="f3f46-227">**속성** 대화 상자에서 왼쪽에 있는 **프로젝트 종속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="f3f46-228">**프로젝트** 목록에서 **ProductsServer**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="f3f46-229">**ProductsPortal**이 선택되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="f3f46-230">**프로젝트** 목록에서 **ProductsPortal**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="f3f46-231">**ProductsServer**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="f3f46-232">**속성 페이지** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="f3f46-233">로컬로 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="f3f46-233">Run the project locally</span></span>

<span data-ttu-id="f3f46-234">응용 프로그램을 로컬로 테스트하려면 Visual Studio에서 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="f3f46-235">온-프레미스 서버(**ProductsServer**)가 먼저 시작된 후 브라우저 창에서 **ProductsPortal** 응용 프로그램이 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="f3f46-236">이제 제품 서비스 온-프레미스 시스템에서 검색된 제품 재고 목록 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="f3f46-237">**ProductsPortal** 페이지에서 **새로 고침**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="f3f46-238">페이지를 새로 고칠 때마다 **ProductsServer**에서 `GetProducts()`가 호출되면 서버 앱에 메시지가 표시되는 것을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="f3f46-239">다음 단계를 진행하기 전에 응용 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="f3f46-240">Azure 웹앱에 ProductsPortal 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="f3f46-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="f3f46-241">다음 단계는 **ProductsPortal** 프런트 엔드를 Azure 웹앱으로 다시 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="f3f46-242">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-242">Do the following:</span></span>

1. <span data-ttu-id="f3f46-243">솔루션 탐색기에서 **ProductsPortal** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="f3f46-244">**게시** 페이지에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f3f46-245">배포 후 **ProductsPortal** 웹 프로젝트가 자동으로 시작되면 브라우저 창에 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="f3f46-246">예상된 동작이며 **ProductsServer** 응용 프로그램이 아직 실행되지 않기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="f3f46-247">다음 단계에서 URL이 필요하므로 배포된 웹앱의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="f3f46-248">또한 Visual Studio의 Azure 앱 서비스 활동 창에서 이 URL을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="f3f46-249">실행 중인 응용 프로그램을 중지하려면 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="f3f46-250">웹앱으로 ProductsPortal 설정</span><span class="sxs-lookup"><span data-stu-id="f3f46-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="f3f46-251">클라우드에서 응용 프로그램을 실행하기 전에 Visual Studio 내에서 **ProductsPortal**이 웹앱으로 시작되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="f3f46-252">Visual Studio에서 **ProductsPortal** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="f3f46-253">왼쪽 열에서 **웹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="f3f46-254">**작업 시작** 섹션에서 **시작 URL** 단추를 클릭하고 텍스트 상자에 이전에 배포한 웹앱의 URL을 입력합니다(예: `http://productsportal1234567890.azurewebsites.net/`).</span><span class="sxs-lookup"><span data-stu-id="f3f46-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="f3f46-255">Visual Studio의 **파일** 메뉴에서 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="f3f46-256">Visual Studio의 빌드 메뉴에서 **솔루션 다시 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f3f46-257">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f3f46-257">Run the application</span></span>

1. <span data-ttu-id="f3f46-258">F5를 눌러 응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="f3f46-259">온-프레미스 서버(**ProductsServer** 콘솔 응용 프로그램)가 먼저 시작된 후에 아래 스크린샷과 같이 **ProductsPortal** 응용 프로그램이 브라우저 창에서 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="f3f46-260">다시, 제품 재고에 제품 서비스 온-프레미스 시스템에서 검색된 데이터가 나열되며 해당 데이터가 웹앱에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="f3f46-261">URL을 확인하여 **ProductsPortal**이 클라우드에서 Azure 웹앱으로 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="f3f46-262">**ProductsServer** 콘솔 응용 프로그램이 실행 중이어야 하며 **ProductsPortal** 응용 프로그램에 데이터를 제공할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="f3f46-263">브라우저에 오류가 표시되면 **ProductsServer**가 다음 메시지를 로드하고 표시할 때까지 몇 초 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="f3f46-264">그런 다음 브라우저에서 **새로 고침**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="f3f46-265">브라우저로 돌아가 **ProductsPortal** 페이지에서 **새로 고침**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="f3f46-266">페이지를 새로 고칠 때마다 **ProductsServer**에서 `GetProducts()`가 호출되면 서버 앱에 메시지가 표시되는 것을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3f46-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="f3f46-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3f46-267">Next steps</span></span>

<span data-ttu-id="f3f46-268">Azure 릴레이에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f46-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="f3f46-269">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="f3f46-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="f3f46-270">릴레이 사용 방법</span><span class="sxs-lookup"><span data-stu-id="f3f46-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
