---
title: "클라우드 서비스 리소스에 Azure 응용 프로그램 통찰력 프로파일러 aaaEnable | Microsoft Docs"
description: "ASP.NET 응용 프로그램의 hello 프로파일러를 tooset Azure 클라우드 서비스 리소스를 호스트 하는 방법을 알아봅니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="b493d-103">Azure Cloud Services 리소스에서 Application Insights Profiler를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b493d-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="b493d-104">이 연습에서는 ASP.NET 응용 프로그램에서 Azure 응용 프로그램 통찰력 프로파일러 tooenable Azure 클라우드 서비스 리소스를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="b493d-105">hello 예로 Azure 가상 컴퓨터, 가상 컴퓨터 크기 집합 및 Azure Service Fabric에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="b493d-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="b493d-106">hello 예제에서는 모두 hello Azure 리소스 관리자 배포 모델을 지 원하는 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b493d-107">Hello 배포 모델에 대 한 자세한 내용은 검토 [Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello](/azure-resource-manager/resource-manager-deployment-model)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="b493d-108">개요</span><span class="sxs-lookup"><span data-stu-id="b493d-108">Overview</span></span>

<span data-ttu-id="b493d-109">다음 다이어그램 hello Azure 클라우드 서비스 리소스에 대 한 hello 프로파일러 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="b493d-110">예로 Azure Virtual Machine을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="b493d-111">![개요](./media/enable-profiler-compute/overview.png) toocollect 정보 처리 및 표시를 위해 Azure 포털 hello hello Azure 클라우드 서비스 리소스에 대 한 hello 진단 에이전트 구성 요소를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="b493d-112">hello hello 연습의 나머지 부분에 지침을 제공 방법을 tooinstall 및 hello 진단 에이전트 tooenable 응용 프로그램 통찰력 프로파일러를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="b493d-113">Hello 연습에 대 한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="b493d-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="b493d-114">Hello Vm에 hello 프로파일러 에이전트를 설치 하는 배포 리소스 관리자 템플릿을 ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) 또는 집합을 비율 크기 조정 ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="b493d-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="b493d-115">프로파일링을 위해 Application Insights 인스턴스가 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="b493d-116">자세한 내용은 [hello 프로필 설정](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="b493d-117">.NET framework 4.6.1 또는 나중에 설치 된 hello 대상 Azure 클라우드 서비스 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="b493d-118">Azure 구독에서 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b493d-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="b493d-119">다음 예제는 hello toocreate 리소스는 PowerShell 스크립트를 사용 하 여 그룹화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="b493d-120">Hello 리소스 그룹에 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="b493d-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="b493d-121">Hello에 **Application Insights** 블레이드에서이 예제와 같이 리소스에 대 한 hello 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Application Insights 블레이드](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="b493d-123">Hello Azure 리소스 관리자 서식 파일에는 Application Insights 계측 키를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="b493d-124">Hello 템플릿을 아직 다운로드 하지 않은 경우 다운로드에서 [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="b493d-125">Hello Application Insights 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-125">Find hello Application Insights key.</span></span>
   
   ![Hello 키의 위치](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="b493d-127">Hello 템플릿 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-127">Replace hello template value.</span></span>
   
   ![Hello 서식 파일에서 대체 값](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="b493d-129">Azure VM toohost hello 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b493d-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="b493d-130">보안 문자열 toosave hello 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="b493d-131">Hello Azure 리소스 관리자 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="b493d-132">리소스 관리자 템플릿이 포함 된 hello PowerShell 콘솔 toohello 폴더에 hello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="b493d-133">다음 명령을 hello 실행 toodeploy hello 템플릿:</span><span class="sxs-lookup"><span data-stu-id="b493d-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="b493d-134">라는 VM 찾아야 hello 스크립트 성공적으로 실행 된 후 **MyWindowsVM** 리소스 그룹에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="b493d-135">Hello VM에 웹 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="b493d-136">Visual Studio에서 웹 응용 프로그램을 게시할 수 있도록 VM에서 웹 배포가 사용하도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="b493d-137">WebPI 통해 수동으로 VM에 Web Deploy tooinstall 참조 [IIS 8.0 또는 나중에 웹 배포 구성 및 설치](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="b493d-138">방법의 예에 대 한 웹 배포를 설치 하는 Azure 리소스 관리자 템플릿을 사용 하 여 tooautomate 참조 [만들기, 구성 및 웹 응용 프로그램 tooan Azure VM 배포](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="b493d-139">ASP.NET MVC 응용 프로그램을 배포 하는 경우 이동 tooServer 관리자를 선택 **역할 및 기능 추가** > **웹 서버 (IIS)** > **웹 서버**  >  **응용 프로그램 개발**, 서버에 ASP.NET 4.5를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![ASP.NET 추가](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="b493d-141">프로젝트에 대 한 hello Azure Application Insights SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="b493d-142">Visual Studio에서 ASP.NET 웹 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="b493d-143">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **연결 된 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="b493d-144">**Application Insights**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="b493d-145">Hello 페이지 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="b493d-146">이전에 만든 hello Application Insights 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="b493d-147">선택 hello **등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="b493d-148">Hello 프로젝트 tooan Azure VM을 게시</span><span class="sxs-lookup"><span data-stu-id="b493d-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="b493d-149">응용 프로그램 tooan Azure VM은 여러 가지 방법으로 toopublish 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="b493d-150">한 가지 방법은 Visual Studio 2017 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="b493d-151">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="b493d-152">선택 **Microsoft Azure 가상 컴퓨터** hello로 대상 게시 하 고 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="b493d-154">응용 프로그램에 대해 부하 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-154">Run a load test against your application.</span></span> <span data-ttu-id="b493d-155">Hello Application Insights 인스턴스 포털 웹 페이지에 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="b493d-156">Hello 프로파일러를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b493d-156">Enable hello profiler</span></span>
1. <span data-ttu-id="b493d-157">Application Insights tooyour 이동 **성능** 블레이드에 대 한 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![구성 아이콘](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="b493d-159">**프로파일러 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-159">Select **Enable Profiler**.</span></span>
   
   ![프로파일러 사용 아이콘](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="b493d-161">성능 테스트 tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b493d-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="b493d-162">응용 프로그램 통찰력 프로파일러에 표시 된 몇 가지 샘플 데이터 toobe 수집한 수 있도록 다음이 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="b493d-163">이전에 만든 toohello Application Insights 리소스를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="b493d-164">Toohello 이동 **가용성** 블레이드 웹 요청 tooyour 응용 프로그램 URL에서 전송 하는 성능 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![성능 테스트 추가](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="b493d-166">성능 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="b493d-166">View your performance data</span></span>

1. <span data-ttu-id="b493d-167">Hello 프로파일러 toocollect 10-15 분을 기다리십시오 하 고 hello 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="b493d-168">Toohello 이동 **성능** 블레이드 Application Insights 리소스 및 응용 프로그램 부하 상태의 경우 수행 되는 방법을 보기.</span><span class="sxs-lookup"><span data-stu-id="b493d-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![성능 보기](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="b493d-170">아래에서 선택 hello 아이콘 **예제** tooopen hello **추적 보기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Hello 추적 보기 블레이드 열기](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="b493d-172">기존 템플릿으로 작업</span><span class="sxs-lookup"><span data-stu-id="b493d-172">Work with an existing template</span></span>

1. <span data-ttu-id="b493d-173">배포 템플릿에 hello Azure 진단 리소스 선언을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="b493d-174">선언에 없으면 다음 예제는 hello에 hello 선언과 유사한 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="b493d-175">Hello에서 hello 템플릿을 업데이트할 수 있습니다 [Azure 리소스 탐색기 웹사이트](https://resources.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="b493d-176">변경 hello 게시자 `Microsoft.Azure.Diagnostics` 너무`AIP.Diagnostics.Test`합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="b493d-177">`typeHandlerVersion`의 경우 `0.0`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="b493d-178">다음 사항을 확인 `autoUpgradeMinorVersion` 너무 설정`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="b493d-179">새 hello 추가 `ApplicationInsightsProfiler` hello에서 싱크 인스턴스 `WadCfg` hello 다음 예제와 같이 설정 개체:</span><span class="sxs-lookup"><span data-stu-id="b493d-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="b493d-180">가상 컴퓨터 크기 집합에 hello 프로파일러를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b493d-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="b493d-181">toosee tooenable hello 프로파일러, 방법 다운로드 hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="b493d-182">Hello 동일한 변경 hello 가상 컴퓨터 크기 집합에 대 한 VM 템플릿 toohello 진단 확장 리소스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="b493d-183">Hello 크기 집합의 각 인스턴스에 액세스 toohello 있는지 확인 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="b493d-184">hello 프로파일러 에이전트 hello 수집 된 샘플 tooApplication Insights 표시 및 분석을 위해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="b493d-185">서비스 패브릭 응용 프로그램에 hello 프로파일러를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b493d-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="b493d-186">서비스 패브릭 클러스터 toohave hello Azure 진단 확장 hello 프로파일러 에이전트를 설치 하는 hello를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="b493d-187">Hello 프로젝트에서 hello Application Insights SDK를 설치 하 고 hello Application Insights 키를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="b493d-188">응용 프로그램 코드 tooinstrument 원격 분석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="b493d-189">프로 비전 hello 서비스 패브릭 클러스터 toohave hello hello 프로파일러 에이전트를 설치 하는 Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="b493d-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="b493d-190">Service Fabric 클러스터는 보안 또는 비보안일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="b493d-191">설정할 수 있습니다 하나 게이트웨이 클러스터 toobe 비보안 때문 액세스용 인증서 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="b493d-192">비즈니스 논리와 데이터를 호스트하는 클러스터는 안전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="b493d-193">Hello 프로파일러 안전 하면서 안전 하지 않은 서비스 패브릭 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="b493d-194">이 연습에서 사용 하는 안전 하지 않은 클러스터 예제 tooexplain 변경 내용이 필요한 tooenable hello 프로파일러 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="b493d-195">Hello에서 보안 클러스터를 프로 비전 할 수 같은 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="b493d-196">[ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="b493d-197">VM 및 가상 컴퓨터 확장 집합과 동일하게 `Application_Insights_Key`를 Application Insights 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="b493d-198">PowerShell 스크립트를 사용 하 여 hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="b493d-199">Hello 프로젝트에서 hello Application Insights SDK를 설치 하 고 hello Application Insights 키를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="b493d-200">Hello에서 hello Application Insights SDK를 설치 [NuGet 패키지](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="b493d-201">안정적인 버전 2.3 이상을 설치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="b493d-202">프로젝트에 Application Insights를 구성하는 방법에 대한 정보는 [Application insights를 통해 Service Fabric 사용](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b493d-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="b493d-203">응용 프로그램 코드 tooinstrument 원격 분석 추가</span><span class="sxs-lookup"><span data-stu-id="b493d-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="b493d-204">Tooinstrument 되도록 코드 조각을, 추가 사용 하는 것에 대 한 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="b493d-205">다음 예제는 hello에서 hello `RunAsync` 메서드는 몇 가지 작업을 수행 하 고 hello `telemetryClient` 클래스 시작 된 후 hello 원격 분석을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="b493d-206">hello 이벤트 hello 응용 프로그램에서 한 고유 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="b493d-207">응용 프로그램 toohello 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="b493d-208">Hello 앱 toorun 10 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="b493d-209">향상의 효과 대 한 hello 앱에서 부하 테스트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="b493d-210">이동 toohello Application Insights 포털 **성능** 블레이드에서 하 고 나타나는, 프로 파일링 추적의 예에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="b493d-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b493d-211">Next steps</span></span>

- <span data-ttu-id="b493d-212">[프로파일러 문제 해결](app-insights-profiler.md#troubleshooting)에서 프로파일러 문제 해결에 대한 도움말을 찾아 보세요.</span><span class="sxs-lookup"><span data-stu-id="b493d-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="b493d-213">Hello 프로파일러에 대 한 자세한 설명 [응용 프로그램 통찰력 프로파일러](app-insights-profiler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b493d-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
