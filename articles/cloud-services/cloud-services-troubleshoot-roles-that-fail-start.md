---
title: "시작에 실패한 역할의 문제 해결 | Microsoft Docs"
description: "클라우드 서비스 역할이 시작에 실패한 이유에 대한 몇 가지 일반적인 원인은 다음과 같습니다. 또한 이러한 문제에 대한 솔루션이 제공됩니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="7a9a6-104">시작에 실패한 클라우드 서비스 역할의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7a9a6-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="7a9a6-105">시작에 실패한 Azure 클라우드 서비스 역할에 관련된 일반적인 문제 및 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="7a9a6-106">DLL 또는 종속성 누락</span><span class="sxs-lookup"><span data-stu-id="7a9a6-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="7a9a6-107">응답하지 않는 역할 및 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하는 역할은 누락된 DLL 또는 어셈블리 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="7a9a6-108">누락된 DLL 또는 어셈블리의 증상은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="7a9a6-109">역할 인스턴스가 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="7a9a6-110">역할 인스턴스가 **준비** 로 이동했지만 웹 응용 프로그램을 탐색하면 페이지가 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="7a9a6-111">이러한 문제를 조사하기 위해 권장되는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="7a9a6-112">웹 역할에서 누락된 DLL 문제 진단</span><span class="sxs-lookup"><span data-stu-id="7a9a6-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="7a9a6-113">웹 역할에 배포된 웹 사이트로 이동하고 브라우저가 다음과 유사한 서버 오류를 표시하는 경우 DLL이 없음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

!['/' 응용 프로그램의 서버 오류.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="7a9a6-115">사용자 지정 오류를 해제하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="7a9a6-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="7a9a6-116">웹 역할에 대해 web.config가 사용자 지정 오류 모드를 꺼짐으로 설정하고 서비스를 다시 배포하도록 구성하여 오류 정보를 더 자세하게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="7a9a6-117">원격 데스크톱을 사용하지 않고 오류를 더 자세하게 보려면</span><span class="sxs-lookup"><span data-stu-id="7a9a6-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="7a9a6-118">Microsoft Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="7a9a6-119">**솔루션 탐색기**에서 web.config 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="7a9a6-120">Web.config 파일에서 system.web 섹션을 찾아서 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="7a9a6-121">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-121">Save the file.</span></span>
5. <span data-ttu-id="7a9a6-122">서비스를 다시 패키지하고 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="7a9a6-123">서비스가 다시 배포되면 누락된 어셈블리나 DLL의 이름으로 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="7a9a6-124">원격으로 오류를 확인하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="7a9a6-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="7a9a6-125">원격 데스크톱을 사용하여 역할에 액세스하고 원격으로 오류 정보를 더 자세하게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="7a9a6-126">원격 데스크톱을 사용하여 오류를 보려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="7a9a6-127">Azure SDK 1.3 이상이 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="7a9a6-128">Visual Studio를 사용하여 솔루션을 배포하는 동안 "원격 데스크톱 연결 구성..."을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="7a9a6-129">원격 데스크톱 연결 구성에 대한 자세한 내용은 [Azure 역할과 함께 원격 데스크톱 사용](../vs-azure-tools-remote-desktop-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="7a9a6-130">Microsoft Azure 클래식 포털에서 인스턴스 상태가 **준비**로 표시되면 역할 인스턴스 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="7a9a6-131">리본의 **원격 액세스** 영역에서 **연결** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="7a9a6-132">원격 데스크톱을 구성하는 동안 지정한 자격 증명을 사용하여 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="7a9a6-133">명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-133">Open a command window.</span></span>
7. <span data-ttu-id="7a9a6-134">`IPconfig`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="7a9a6-135">IPV4 주소 값을 적습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="7a9a6-136">Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="7a9a6-137">웹 응용 프로그램의 주소 및 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="7a9a6-138">예: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="7a9a6-139">웹 사이트를 탐색하면 이제 더 구체적인 오류 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="7a9a6-140">'/' 응용 프로그램의 서버 오류.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="7a9a6-141">설명: 현재 웹 요청을 실행하는 동안 처리되지 않은 예외가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="7a9a6-142">오류에 대한 자세한 내용 및 코드에서 어디에 기반하는지는 스택 추적을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="7a9a6-143">예외 세부 정보: System.IO.FIleNotFoundException: 파일이나 어셈블리를 로드할 수 없습니다 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ 또는 해당 종속성 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="7a9a6-144">시스템은 지정된 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="7a9a6-145">예:</span><span class="sxs-lookup"><span data-stu-id="7a9a6-145">For example:</span></span>

!['/' 응용 프로그램의 명시적 서버 오류](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="7a9a6-147">계산 에뮬레이터를 사용하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="7a9a6-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="7a9a6-148">Microsoft Azure 계산 에뮬레이터를 사용하여 누락된 종속성 및 web.config 오류 문제를 진단하고 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="7a9a6-149">이 진단 방법을 사용하여 최상의 결과가 발생한 경우 Windows 새로 설치한 컴퓨터 또는 가상 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="7a9a6-150">Azure 환경을 가장 잘 시뮬레이션하려면 Windows Server 2008 R2 x64를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="7a9a6-151">[Azure SDK](https://azure.microsoft.com/downloads/)의 독립 실행형 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="7a9a6-152">개발 컴퓨터에서 클라우드 서비스 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="7a9a6-153">Windows Explorer에서 클라우드 서비스 프로젝트의 bin\debug 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="7a9a6-154">문제를 디버깅하는 데 사용하는 컴퓨터에 .csx 폴더와.cscfg 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="7a9a6-155">클린 컴퓨터에서 Azure SDK 명령 프롬프트 창을 열고 `csrun.exe /devstore:start`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="7a9a6-156">명령 프롬프트에 `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="7a9a6-157">역할이 시작될 때 Internet Explorer에서 자세한 오류 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="7a9a6-158">또한 표준 Windows 문제해결 도구를 사용하여 추가로 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="7a9a6-159">IntelliTrace를 사용하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="7a9a6-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="7a9a6-160">.NET Framework 4를 사용하는 작업자 및 웹 역할의 경우 Microsoft Visual Studio Enterprise에서 사용 가능한 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="7a9a6-161">IntelliTrace를 사용하는 서비스를 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="7a9a6-162">Azure SDK 1.3 이상이 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="7a9a6-163">Visual Studio를 사용하여 솔루션을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="7a9a6-164">배포하는 동안 **.NET 4 역할에 IntelliTrace 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="7a9a6-165">인스턴스가 시작되면 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="7a9a6-166">**Azure\\클라우드 서비스** 노드를 확장하고 배포를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="7a9a6-167">역할 인스턴스를 확인할 때까지 배포를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="7a9a6-168">마우스 오른쪽 단추로 인스턴스 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="7a9a6-169">**IntelliTrace 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="7a9a6-170">**IntelliTrace 요약** 이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="7a9a6-171">요약의 예외 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="7a9a6-172">예외가 있는 경우 해당 섹션이 **예외 데이터**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="7a9a6-173">**예외 데이터**를 확장하고 다음과 비슷한 **System.IO.FileNotFoundException** 오류를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![예외 데이터, 파일 또는 어셈블리 누락](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="7a9a6-175">누락된 DLL 및 어셈블리 주소 지정</span><span class="sxs-lookup"><span data-stu-id="7a9a6-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="7a9a6-176">누락된 DLL 및 어셈블리 오류에 주소를 지정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="7a9a6-177">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="7a9a6-178">**솔루션 탐색기**에서 **참조** 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="7a9a6-179">오류에서 식별된 어셈블리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="7a9a6-180">**속성** 창에서 **복사 로컬 속성**을 찾아 값을 **True**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="7a9a6-181">클라우드 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="7a9a6-182">모든 오류가 수정되었다고 확인되면 **.NET 4 역할에 IntelliTrace 사용** 확인란을 선택하지 않고 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a9a6-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a9a6-183">Next steps</span></span>
<span data-ttu-id="7a9a6-184">클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="7a9a6-185">Azure PaaS 컴퓨터 진단 데이터를 사용하여 클라우드 서비스 역할 문제를 해결하는 방법을 알아보려면 [Kevin Williamson의 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9a6-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
