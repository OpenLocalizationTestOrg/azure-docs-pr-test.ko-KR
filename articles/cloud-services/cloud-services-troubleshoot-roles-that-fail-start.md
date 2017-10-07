---
title: "toostart 못하는 aaaTroubleshoot 역할 | Microsoft Docs"
description: "클라우드 서비스 역할 toostart 못할 이유 몇 가지 일반적인 원인은 다음과 같습니다. 솔루션 toothese 문제 제공 됩니다."
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
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="dd150-104">Toostart 실패 하는 클라우드 서비스 역할 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dd150-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="dd150-105">다음은 몇 가지 일반적인 문제와 toostart 실패 하는 솔루션 관련된 tooAzure 클라우드 서비스 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="dd150-106">DLL 또는 종속성 누락</span><span class="sxs-lookup"><span data-stu-id="dd150-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="dd150-107">응답하지 않는 역할 및 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하는 역할은 누락된 DLL 또는 어셈블리 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="dd150-108">누락된 DLL 또는 어셈블리의 증상은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="dd150-109">역할 인스턴스가 **초기화 중**, **사용 중** 및 **중지** 상태를 반복하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="dd150-110">역할 인스턴스에 너무 이동**준비** 하지만 tooyour 웹 응용 프로그램을 이동 하는 경우 hello 페이지가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="dd150-111">이러한 문제를 조사하기 위해 권장되는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="dd150-112">웹 역할에서 누락된 DLL 문제 진단</span><span class="sxs-lookup"><span data-stu-id="dd150-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="dd150-113">웹 역할에 배포 된 tooa 웹 사이트를 탐색 하 고 hello 브라우저 표시 서버 오류와 비슷한 toohello 다음을를 DLL이 누락 된 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

!['/' 응용 프로그램의 서버 오류.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="dd150-115">사용자 지정 오류를 해제하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="dd150-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="dd150-116">Hello 웹 역할 tooset hello 사용자 지정 오류 모드 tooOff에 대 한 hello web.config를 구성 하 고 hello 서비스를 다시 배포 하 여 자세한 오류 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="dd150-117">더 tooview 원격 데스크톱을 사용 하지 않고 오류를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="dd150-118">Microsoft Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="dd150-119">Hello에 **솔루션 탐색기**을 hello web.config 파일을 찾아서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="dd150-120">Hello web.config 파일에서 hello system.web 섹션을 찾아서 hello 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="dd150-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="dd150-121">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-121">Save hello file.</span></span>
5. <span data-ttu-id="dd150-122">패키지에 포함 시키고 hello 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="dd150-123">Hello 서비스를 다시 배포 되 면 hello 누락 된 어셈블리 또는 DLL의 hello 이름으로 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="dd150-124">원격으로 hello 오류를 확인 하 여 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="dd150-125">원격 데스크톱 tooaccess hello 역할을 사용 하 고 자세한 오류 정보를 원격으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="dd150-126">원격 데스크톱을 사용 하 여 다음 단계 tooview hello 오류 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="dd150-127">Azure SDK 1.3 이상이 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="dd150-128">Visual Studio를 사용 하 여 hello 솔루션의 hello 배포 하는 동안 선택 너무 "원격 데스크톱 연결 구성...".</span><span class="sxs-lookup"><span data-stu-id="dd150-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="dd150-129">Hello 원격 데스크톱 연결 구성에 대 한 자세한 내용은 참조 하십시오. [Azure 역할과 함께 원격 데스크톱 사용 하 여](../vs-azure-tools-remote-desktop-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="dd150-130">Hello Microsoft Azure 클래식 포털에서 hello 인스턴스 상태가 표시 되 면 **준비**, hello 역할 인스턴스 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="dd150-131">Hello 클릭 **연결** hello 아이콘 **원격 액세스** hello 리본 메뉴의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="dd150-132">Hello 원격 데스크톱 구성 중에 지정 된 hello 자격 증명을 사용 하 여 toohello 가상 컴퓨터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="dd150-133">명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-133">Open a command window.</span></span>
7. <span data-ttu-id="dd150-134">`IPconfig`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="dd150-135">참고 hello IPV4 주소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="dd150-136">Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="dd150-137">Hello 주소와 hello hello 웹 응용 프로그램 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="dd150-138">예: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="dd150-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="dd150-139">웹 사이트를 탐색 toohello 하 더 구체적인 오류 메시지가 이제 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="dd150-140">'/' 응용 프로그램의 서버 오류.</span><span class="sxs-lookup"><span data-stu-id="dd150-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="dd150-141">설명: hello 현재 웹 요청 hello 실행 하는 동안 처리 되지 않은 예외가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="dd150-142">Hello 오류에 대 한 자세한 내용은 hello 스택 추적 및 hello 코드에서 발생 한 위치를 검토 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dd150-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="dd150-143">예외 세부 정보: System.IO.FIleNotFoundException: 파일이나 어셈블리를 로드할 수 없습니다 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ 또는 해당 종속성 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="dd150-144">hello 시스템 지정 된 hello 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="dd150-145">예:</span><span class="sxs-lookup"><span data-stu-id="dd150-145">For example:</span></span>

!['/' 응용 프로그램의 명시적 서버 오류](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="dd150-147">Hello 계산 에뮬레이터를 사용 하 여 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="dd150-148">Microsoft Azure 계산 에뮬레이터 toodiagnose hello를 사용 하 여 수 있으며의 누락 된 종속성 및 web.config 오류 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="dd150-149">이 진단 방법을 사용하여 최상의 결과가 발생한 경우 Windows 새로 설치한 컴퓨터 또는 가상 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="dd150-150">toobest은 hello Azure 환경을 시뮬레이션, Windows Server 2008 R2 x64 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="dd150-151">독립 실행형 버전의 hello hello 설치 [Azure SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dd150-152">Hello 개발 컴퓨터에서 hello 클라우드 서비스 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="dd150-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="dd150-153">Windows 탐색기에서 hello 클라우드 서비스 프로젝트의 toohello bin\debug 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="dd150-154">Hello.csx 폴더와.cscfg 파일 toohello 컴퓨터 toodebug hello 문제를 사용 하 고 있는지를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="dd150-155">클린 컴퓨터 hello에서 유형과 Azure SDK 명령 프롬프트 창을 엽니다 `csrun.exe /devstore:start`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="dd150-156">Hello 명령 프롬프트에서 입력 `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="dd150-157">Hello 역할 시작 될 때 Internet Explorer에 자세한 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="dd150-158">표준 Windows 문제 해결 도구를 사용할 수도 있습니다 toofurther hello 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="dd150-159">IntelliTrace를 사용하여 문제 진단</span><span class="sxs-lookup"><span data-stu-id="dd150-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="dd150-160">.NET Framework 4를 사용하는 작업자 및 웹 역할의 경우 Microsoft Visual Studio Enterprise에서 사용 가능한 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="dd150-161">사용 하도록 설정 하는 IntelliTrace에서 이러한 단계 toodeploy hello 서비스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="dd150-162">Azure SDK 1.3 이상이 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="dd150-163">Visual Studio를 사용 하 여 hello 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="dd150-164">배포 하는 동안 확인 hello **.NET 4 역할에 대해 IntelliTrace 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="dd150-165">Hello 인스턴스가 시작 되 면 hello 열어 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="dd150-166">Hello 확장 **Azure\\클라우드 서비스** 노드 hello 배포를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="dd150-167">Hello 배포를 확장 하 고 hello 역할 인스턴스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dd150-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="dd150-168">Hello 인스턴스 중 하나를 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="dd150-169">**IntelliTrace 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="dd150-170">hello **IntelliTrace 요약** 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="dd150-171">Hello 요약의 hello 예외 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="dd150-172">Hello 섹션 표시 되는 예외가 있으면 **예외 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="dd150-173">Hello 확장 **예외 데이터** 를 찾아서 **System.IO.FileNotFoundException** 비슷한 toohello 다음 오류:</span><span class="sxs-lookup"><span data-stu-id="dd150-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![예외 데이터, 파일 또는 어셈블리 누락](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="dd150-175">누락된 DLL 및 어셈블리 주소 지정</span><span class="sxs-lookup"><span data-stu-id="dd150-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="dd150-176">DLL 및 어셈블리 오류 누락 tooaddress 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="dd150-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="dd150-177">Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="dd150-178">**솔루션 탐색기**개방형 hello **참조** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="dd150-179">Hello 오류에서 확인 된 hello 어셈블리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="dd150-180">Hello에 **속성** 창 찾기 **로컬 복사 속성** 너무 hello 값을 설정 하 고**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="dd150-181">Hello 클라우드 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="dd150-182">모든 오류가 오류를 확인 한 후 hello를 검사 하지 않고 hello 서비스를 배포할 수 있습니다 **.NET 4 역할에 대해 IntelliTrace 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd150-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd150-183">Next steps</span></span>
<span data-ttu-id="dd150-184">클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="dd150-185">Azure PaaS 컴퓨터 진단 데이터를 사용 하 여 tootroubleshoot 클라우드 서비스 역할을 발급 하는 방법을 toolearn 참조 [Kevin Williamson 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd150-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
