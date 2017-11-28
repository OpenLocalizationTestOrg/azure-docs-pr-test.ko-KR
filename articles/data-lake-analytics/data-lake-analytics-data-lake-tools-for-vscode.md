---
title: "Azure Data Lake Tools: Azure Data Lake Tools for Visual Studio Code 사용 | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio Code를 사용하여 U-SQL 스크립트를 만들고, 테스트하고, 실행하는 방법에 대해 알아봅니다. "
Keywords: "VScode,Azure Data Lake Tools,로컬 실행,로컬 디버그,로컬 디버그,저장소 파일 미리 보기,저장소 경로로 업로드"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="5aca7-104">Azure Data Lake Tools for Visual Studio Code 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="5aca7-105">Azure Data Lake Tools for Visual Studio Code(VS Code)를 사용하여 U-SQL 스크립트를 만들고, 테스트하고, 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="5aca7-106">정보는 또한 다음 비디오에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="5aca7-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5aca7-107">Prerequisites</span></span>

<span data-ttu-id="5aca7-108">Data Lake Tools는 VS Code에서 지원하는 플랫폼에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="5aca7-109">지원되는 플랫폼에는 Windows, Linux 및 MacOS가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="5aca7-110">다른 플랫폼에는 다음 필수 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="5aca7-111">Windows</span><span class="sxs-lookup"><span data-stu-id="5aca7-111">Windows</span></span>

    - <span data-ttu-id="5aca7-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="5aca7-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5aca7-113">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="5aca7-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5aca7-114">java.exe 경로를 시스템 환경 변수 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="5aca7-115">구성 지침에 대해서는 [Path 시스템 변수를 설정 또는 변경하는 방법]( https://www.java.com/download/help/path.xml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="5aca7-116">경로는 C:\Program Files\Java\jdk1.8.0_77\jre\bin과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="5aca7-117">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5aca7-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="5aca7-118">Linux(Ubuntu 14.04 LTS 권장)</span><span class="sxs-lookup"><span data-stu-id="5aca7-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="5aca7-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="5aca7-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="5aca7-120">코드를 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="5aca7-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/)</span><span class="sxs-lookup"><span data-stu-id="5aca7-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="5aca7-122">deb 패키지 원본을 업데이트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="5aca7-123">Mono를 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="5aca7-124">Mono 4.6은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="5aca7-125">4.2.x 버전을 설치하기 전에 먼저 4.6 버전을 완전히 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="5aca7-126">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="5aca7-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5aca7-127">설치에 대한 지침은 [Java에 대한 Linux 64비트 설치 지침]( https://java.com/en/download/help/linux_x64_install.xml) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="5aca7-128">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5aca7-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="5aca7-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="5aca7-129">MacOS</span></span>

    - <span data-ttu-id="5aca7-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="5aca7-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5aca7-131">[Mono 4.2.4.x](http://download.mono-project.com/archive/4.2.4/macos-10-x86/)</span><span class="sxs-lookup"><span data-stu-id="5aca7-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="5aca7-132">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="5aca7-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5aca7-133">설치에 대한 지침은 [Java에 대한 Linux 64비트 설치 지침](https://java.com/en/download/help/mac_install.xml) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="5aca7-134">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5aca7-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="5aca7-135">Data Lake Tools 설치</span><span class="sxs-lookup"><span data-stu-id="5aca7-135">Install Data Lake Tools</span></span>

<span data-ttu-id="5aca7-136">필수 구성 요소를 설치한 후에 Data Lake Tools for VS Code를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="5aca7-137">**Data Lake Tools를 설치하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="5aca7-138">Visual Studio Code를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="5aca7-139">Ctrl+P를 선택한 후 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="5aca7-140">Visual Studio 코드 확장 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="5aca7-141">그 중 하나는 **Azure Data Lake Tools**입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="5aca7-142">**Azure Data Lake Tools** 옆에 있는 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="5aca7-143">몇 초 후에 **설치** 단추가 **다시 로드**로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="5aca7-144">**다시 로드**를 선택하여 확장을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="5aca7-145">**확인**을 선택하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-145">Select **OK** to confirm.</span></span> <span data-ttu-id="5aca7-146">**확장** 창에서 Azure Data Lake Tools를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="5aca7-147">![Data Lake Tools for Visual Studio Code 확장 창](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="5aca7-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="5aca7-148">Azure Data Lake 도구 활성화</span><span class="sxs-lookup"><span data-stu-id="5aca7-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="5aca7-149">새 .usql 파일을 만들거나 기존 .usql 파일을 열어 확장을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="5aca7-150">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="5aca7-150">Connect to Azure</span></span>

<span data-ttu-id="5aca7-151">Data Lake Analytics에서 U-SQL 스크립트를 컴파일하고 실행하기 전에 먼저 Azure 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="5aca7-152">**Azure에 연결하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="5aca7-153">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="5aca7-154">**ADL: Login**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="5aca7-155">로그인 정보가 **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="5aca7-156">![Data Lake Tools for Visual Studio Code 명령 팔레트](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 장치 로그인 정보](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="5aca7-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="5aca7-157">Ctrl 키를 누른 채 로그인 URL: https://aka.ms/devicelogin을 클릭하여 선택하여 로그인 웹 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="5aca7-158">텍스트 상자에 코드 **G567LX42V**를 입력한 다음 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Data Lake Tools for Visual Studio Code 로그인 코드 붙여넣기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="5aca7-160">지침에 따라 웹 페이지에서 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="5aca7-161">연결되면 Azure 계정 이름이 **VS Code** 창의 왼쪽 아래 모서리에 있는 상태 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="5aca7-162">계정에 활성화된 두 가지 요인이 있는 경우 PIN을 사용하는 것보다 전화 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="5aca7-163">로그아웃하려면 **ADL: Logout** 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="5aca7-164">Data Lake Analytics 계정 나열</span><span class="sxs-lookup"><span data-stu-id="5aca7-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="5aca7-165">연결을 테스트하려면 Data Lake Analytics 계정의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="5aca7-166">**Azure 구독**에서 Data Lake Analytics 계정을 나열하려면</span><span class="sxs-lookup"><span data-stu-id="5aca7-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="5aca7-167">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="5aca7-168">**ADL: List Accounts**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="5aca7-169">계정이 **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="5aca7-170">샘플 스크립트 열기</span><span class="sxs-lookup"><span data-stu-id="5aca7-170">Open the sample script</span></span>
<span data-ttu-id="5aca7-171">명령 팔레트(Ctrl+Shift+P)를 열고 **ADL: Open Sample Script**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="5aca7-172">그러면 이 샘플의 다른 인스턴스가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-172">This opens another instance of this sample.</span></span> <span data-ttu-id="5aca7-173">이 인스턴스에서 스크립트를 편집, 구성, 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="5aca7-174">U-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-174">Work with U-SQL</span></span>

<span data-ttu-id="5aca7-175">U-SQL을 사용하려면 U-SQL 파일이나 폴더를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="5aca7-176">**U-SQL 프로젝트 폴더를 열려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="5aca7-177">Visual Studio Code에서 **파일** 메뉴를 선택한 다음 **폴더 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="5aca7-178">폴더를 지정한 다음 **폴더 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="5aca7-179">**파일** 메뉴를 선택한 다음 **새 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="5aca7-180">제목 없음-1 파일이 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="5aca7-181">다음 코드를 제목 없음-1 파일에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-181">Enter the following code into the Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="5aca7-182">스크립트는 /output 폴더에 일부 데이터가 포함된 departments.csv 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="5aca7-183">열린 폴더에서 파일을 **myUSQL.usql**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="5aca7-184">adltools_settings.json 구성 파일도 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="5aca7-185">adltools_settings.json을 열고 다음 속성을 사용하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="5aca7-186">Account: Azure 구독에 있는 Data Lake Analytics 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="5aca7-187">Database: 사용자 계정의 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-187">Database: A database under your account.</span></span> <span data-ttu-id="5aca7-188">기본은 **master**입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-188">The default is **master**.</span></span>
    - <span data-ttu-id="5aca7-189">Schema: 데이터베이스의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-189">Schema: A schema under your database.</span></span> <span data-ttu-id="5aca7-190">기본은 **dbo**입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="5aca7-191">선택적 설정</span><span class="sxs-lookup"><span data-stu-id="5aca7-191">Optional settings:</span></span>
        - <span data-ttu-id="5aca7-192">Priority: 우선 순위의 범위는 1-1000이며, 가장 높은 우선 순위는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="5aca7-193">기본값은 **1000**입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="5aca7-194">Parallelism: 병렬 처리의 범위는 1-150입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="5aca7-195">기본값은 Azure Data Lake Analytics 계정에 허용되는 최대 병렬 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="5aca7-196">설정이 유효하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-196">If the settings are invalid, the default values are used.</span></span>

    ![Data Lake Tools for Visual Studio Code 구성 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="5aca7-198">Data Lake Analytics 계산 계정은 U-SQL 작업을 컴파일하고 실행하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="5aca7-199">U-SQL 작업을 컴파일하고 실행하려면 먼저 컴퓨터 계정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="5aca7-200">구성이 저장되면 계정, 데이터베이스 및 스키마 정보가 해당 .usql 파일의 왼쪽 아래 모서리에 있는 상태 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="5aca7-201">파일 열기와 비교하여 폴더를 열 때 다음이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="5aca7-202">코드 숨김 파일 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-202">Use a code-behind file.</span></span> <span data-ttu-id="5aca7-203">단일 파일 모드에서는 코드 숨김이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="5aca7-204">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-204">Use a configuration file.</span></span> <span data-ttu-id="5aca7-205">폴더를 열면 작업 폴더의 스크립트에서 단일 구성 파일을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="5aca7-206">U-SQL 스크립트는 Data Lake Analytics 서비스를 통해 원격으로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="5aca7-207">**컴파일** 명령을 실행하면 U-SQL 스크립트를 Data Lake Analytics 계정으로 전송하며,</span><span class="sxs-lookup"><span data-stu-id="5aca7-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="5aca7-208">Visual Studio Code에서는 컴파일 결과를 늦게 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="5aca7-209">원격 컴파일로 인해 Visual Studio Code에는 구성 파일의 Data Lake Analytics 계정에 연결되는 정보를 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="5aca7-210">**U-SQL 스크립트를 컴파일하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="5aca7-211">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="5aca7-212">**ADL:Compile Script**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="5aca7-213">컴파일 결과는 **출력** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="5aca7-214">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Compile Script**를 선택하여 U-SQL 작업을 컴파일할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="5aca7-215">컴파일 결과가 **출력** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="5aca7-216">**U-SQL 스크립트를 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="5aca7-217">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="5aca7-218">**ADL:Submit Job**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="5aca7-219">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Submit Job**을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="5aca7-220">U-SQL 작업을 제출한 후 전송 로그가 VS Code의 **출력** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="5aca7-221">성공적으로 제출되면 작업 URL도 함께 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="5aca7-222">웹 브라우저에서 작업 URL을 열어 실시간 작업 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="5aca7-223">작업 세부 정보의 출력을 활성화하려면 **vs code for u-sql_settings.json** 파일에서 **jobInformationOutputPath**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="5aca7-224">코드 숨김 파일 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-224">Use a code-behind file</span></span>

<span data-ttu-id="5aca7-225">코드 숨김 파일은 단일 U-SQL 스크립트와 연결되는 C# 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="5aca7-226">코드 숨김 파일에서는 UDO, UDA, UDT 및 UDF 전용 스크립트를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="5aca7-227">먼저 어셈블리를 등록하지 않고도 스크립트에서 UDO, UDA, UDT 및 UDF를 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="5aca7-228">코드 숨김 파일은 피어링 U-SQL 스크립트 파일과 동일한 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="5aca7-229">스크립트 파일 이름이 xxx.usql이면 코드 숨김 파일 이름은 xxx.usql.cs가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="5aca7-230">코드 숨김 파일을 수동으로 삭제하면 연결된 U-SQL 스크립트의 코드 숨김 기능을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="5aca7-231">U-SQL 스크립트의 고객 코드 만들기에 대한 자세한 내용은 [U-SQL에서 사용자 지정 코드 만들기 및 사용: 사용자 정의 함수]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="5aca7-232">코드 숨김을 지원하려면 작업 폴더를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="5aca7-233">**코드 숨김 파일을 생성하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="5aca7-234">원본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-234">Open a source file.</span></span> 
2. <span data-ttu-id="5aca7-235">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="5aca7-236">**ADL:Generate Code Behind**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="5aca7-237">코드 숨김 파일이 동일한 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="5aca7-238">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Generate Code Behind**를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="5aca7-239">코드 숨김을 사용하여 U-SQL 스크립트를 컴파일하고 제출하는 것은 독립 실행형 U-SQL 스크립트 파일과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="5aca7-240">다음 두 스크린샷에서는 코드 숨김 파일 및 연결된 U-SQL 스크립트 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 코드 숨김 스크립트 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="5aca7-243">어셈블리 사용</span><span class="sxs-lookup"><span data-stu-id="5aca7-243">Use assemblies</span></span>

<span data-ttu-id="5aca7-244">어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="5aca7-245">Data Lake Tools를 사용하여 사용자 지정 코드 어셈블리를 Data Lake Analytics 카탈로그에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="5aca7-246">**어셈블리를 등록하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-246">**To register an assembly**</span></span>

<span data-ttu-id="5aca7-247">**ADL: Register Assembly** 또는 **ADL: Register Assembly through Configuration** 명령을 통해 어셈블리를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="5aca7-248">**ADL: Register Assembly 명령을 통해 등록하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="5aca7-249">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="5aca7-250">**ADL:Register Assembly**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="5aca7-251">로컬 어셈블리 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="5aca7-252">Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="5aca7-253">데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-253">Select a database.</span></span>

<span data-ttu-id="5aca7-254">결과: 포털이 브라우저에서 열리고 어셈블리 등록 프로세스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="5aca7-255">**ADL: Register Assembly** 명령을 트리거하는 다른 편리한 방법은 파일 탐색기에서 .dll 파일을 마우스 오른쪽 단추로 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="5aca7-256">**ADL: Register Assembly through Configuration 명령을 통해 등록하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="5aca7-257">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="5aca7-258">**ADL: Register Assembly through Configuration**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="5aca7-259">로컬 어셈블리 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="5aca7-260">JSON 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-260">The JSON file is displayed.</span></span> <span data-ttu-id="5aca7-261">필요한 경우 어셈블리 종속성 및 리소스 매개 변수를 검토하고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="5aca7-262">지침이 **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="5aca7-263">어셈블리 등록을 계속하려면 JSON 파일을 저장(Ctrl+S)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="5aca7-265">어셈블리 종속성: Azure Data Lake Tools는 DLL에 종속성이 있는지 여부를 자동으로 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="5aca7-266">종속성이 감지되면 JSON 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="5aca7-267">리소스: 어셈블리 등록의 일환으로 DLL 리소스(예: txt, .png 및 .csv)를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="5aca7-268">**ADL: Register Assembly through Configuration** 명령을 트리거하는 다른 방법은 파일 탐색기에서 .dll 파일을 마우스 오른쪽 단추로 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="5aca7-269">다음 U-SQL 코드는 어셈블리를 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="5aca7-270">이 샘플에서 어셈블리 이름은 *test*입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-270">In the sample, the assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="5aca7-271">Data Lake Analytics 카탈로그 액세스</span><span class="sxs-lookup"><span data-stu-id="5aca7-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="5aca7-272">Azure에 연결한 후에는 다음 단계를 사용하여 U-SQL 카탈로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="5aca7-273">**Azure Data Lake Analytics 메타데이터에 액세스하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="5aca7-274">Ctrl+Shift+P를 선택한 다음 **ADL: List Tables**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="5aca7-275">Data Lake Analytics 계정 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="5aca7-276">Data Lake Analytics 데이터베이스 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="5aca7-277">스키마 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-277">Select one of the schemas.</span></span> <span data-ttu-id="5aca7-278">테이블의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="5aca7-279">Data Lake Analytics 작업 보기</span><span class="sxs-lookup"><span data-stu-id="5aca7-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="5aca7-280">**Data Lake Analytics 작업을 보려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="5aca7-281">명령 팔레트(Ctrl+Shift+P)를 열고 **ADL: Show Job**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="5aca7-282">Data Lake Analytics 또는 로컬 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="5aca7-283">계정의 작업 목록이 표시되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="5aca7-284">작업 목록에서 작업을 선택하고 Data Lake Tools는 Azure Portal에서 작업 세부 정보를 열고 VS Code에서 JobInfo 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="5aca7-286">Azure Data Lake Storage 통합</span><span class="sxs-lookup"><span data-stu-id="5aca7-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="5aca7-287">다음 작업에 Azure Data Lake Storage 관련 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="5aca7-288">Azure Data Lake Storage 리소스 찾기</span><span class="sxs-lookup"><span data-stu-id="5aca7-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="5aca7-289">Azure Data Lake Storage 파일 미리 보기</span><span class="sxs-lookup"><span data-stu-id="5aca7-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="5aca7-290">VS Code의 Azure Data Lake Storage에 직접 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5aca7-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="5aca7-291">저장소 경로 나열</span><span class="sxs-lookup"><span data-stu-id="5aca7-291">List the storage path</span></span> 
<span data-ttu-id="5aca7-292">명령 팔레트 또는 마우스 오른쪽 단추 클릭을 통해 저장소 경로를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="5aca7-293">**명령 팔레트를 통해 저장소 경로를 나열하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="5aca7-294">명령 팔레트(Ctrl+Shift+P)를 열고 **ADL: List Storage Path**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="5aca7-296">저장소 경로를 나열하는 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="5aca7-297">이 구절에서는 **Enter a path**를 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로를 나열하는 한 가지 방법](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="5aca7-299">VS Code는 모든 Data Lake Analytics 계정에 마지막으로 방문한 경로를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5aca7-300">예: /tt/ss</span><span class="sxs-lookup"><span data-stu-id="5aca7-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5aca7-301">루트 경로의 브라우저: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 루트 경로 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5aca7-302">경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="5aca7-303">로컬 경로 또는 Data Lake Analytics 계정에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code more 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="5aca7-305">**자세히**를 선택하여 더 많은 Data Lake Analytics 계정을 나열한 다음 Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="5aca7-307">Azure 저장소 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-307">Enter an Azure storage path.</span></span> <span data-ttu-id="5aca7-308">예: /output</span><span class="sxs-lookup"><span data-stu-id="5aca7-308">For example, /output.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="5aca7-310">결과: 명령 팔레트는 항목에 따라 경로 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 결과 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="5aca7-312">상대 경로를 나열하는 더 편리한 다른 방법은 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="5aca7-313">**마우스 오른쪽 단추 클릭을 통해 저장소 경로를 나열하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="5aca7-314">경로 문자열을 마우스 오른쪽 단추로 클릭하여 **저장소 경로 나열**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="5aca7-316">명령 팔레트에 선택한 상대 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-316">The selected relative path appears in the command palette.</span></span>

   ![Data Lake Tools for Visual Studio Code에서 선택한 상대 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="5aca7-318">로컬 경로 또는 Data Lake Analytics 계정에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="5aca7-320">결과: 명령 팔레트는 현재 경로에 대한 폴더 및 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 현재 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="5aca7-322">저장소 파일 미리 보기</span><span class="sxs-lookup"><span data-stu-id="5aca7-322">Preview the storage file</span></span>
<span data-ttu-id="5aca7-323">명령 팔레트 또는 마우스 오른쪽 단추 클릭을 통해 저장소 파일을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="5aca7-324">**명령 팔레트를 통해 저장소 파일을 미리 보려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="5aca7-325">명령 팔레트(Ctrl+Shift+P)를 열고 **ADL: Preview Storage File**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 저장소 파일 미리 보기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="5aca7-327">로컬 경로 또는 Data Lake Analytics 계정에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 계정 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5aca7-329">**자세히**를 선택하여 더 많은 Data Lake Analytics 계정을 나열한 다음 Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="5aca7-331">Azure 저장소 경로 또는 파일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="5aca7-332">예: /output/SearchLog.txt</span><span class="sxs-lookup"><span data-stu-id="5aca7-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 저장소 경로 및 파일 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="5aca7-334">결과: 명령 팔레트는 항목에 따라 경로 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="5aca7-336">**마우스 오른쪽 단추 클릭을 통해 저장소 경로를 나열하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="5aca7-337">파일을 미리 보려면 파일 경로를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-337">To preview a file, right-click the file path.</span></span>

   ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="5aca7-339">로컬 경로 또는 Data Lake Analytics 계정에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5aca7-341">결과: VS Code는 파일의 미리 보기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="5aca7-343">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5aca7-343">Upload a file</span></span> 

<span data-ttu-id="5aca7-344">**ADL: Upload File** 또는 **ADL: Upload File through Configuration** 명령을 입력하여 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="5aca7-345">**ADL: Upload File 명령을 통해 파일을 업로드하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="5aca7-346">Ctrl+Shift+P를 선택하여 명령 팔레트를 열거나 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **Upload File**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="5aca7-347">파일을 업로드하려면 로컬 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-347">To upload the file, enter a local path.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 로컬 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="5aca7-349">저장소 경로를 나열하는 방법 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="5aca7-350">이 구절에서는 **Enter a path**를 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="5aca7-352">VS Code는 모든 Data Lake Analytics 계정에 마지막으로 방문한 경로를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5aca7-353">예: /tt/ss</span><span class="sxs-lookup"><span data-stu-id="5aca7-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5aca7-354">루트 경로의 브라우저: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 루트 경로 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5aca7-355">경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="5aca7-356">로컬 경로 또는 Data Lake Analytics 계정에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="5aca7-358">Azure 저장소 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-358">Enter an Azure storage path.</span></span> <span data-ttu-id="5aca7-359">예: /output</span><span class="sxs-lookup"><span data-stu-id="5aca7-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="5aca7-360">Azure 저장소 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-360">Find your Azure storage path.</span></span> <span data-ttu-id="5aca7-361">**Choose current folder**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 폴더 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="5aca7-363">결과: **출력** 창은 파일 업로드 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="5aca7-365">**ADL: Upload File through Configuration 명령을 통해 파일을 업로드하려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="5aca7-366">Ctrl+Shift+P를 선택하여 명령 팔레트는 열거나 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **Upload File through Configuration**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="5aca7-367">VS Code에서 JSON 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="5aca7-368">파일 경로를 입력하고 여러 파일을 동시에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="5aca7-369">지침이 **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="5aca7-370">파일 업로드를 계속하려면 JSON 파일을 저장(Ctrl+S)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="5aca7-372">결과: **출력** 창은 파일 업로드 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="5aca7-374">저장소에 파일을 업로드하는 다른 방법은 스크립트 편집기에서 파일의 전체 경로 또는 파일의 상대 경로의 오른쪽 클릭 메뉴를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="5aca7-375">로컬 파일 경로를 입력한 다음 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="5aca7-376">**출력** 창은 업로드 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="5aca7-377">Azure Storage Explorer 열기</span><span class="sxs-lookup"><span data-stu-id="5aca7-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="5aca7-378">**ADL: Open Web Azure Storage Explorer** 명령을 입력하거나 마우스 오른쪽 단추 클릭 바로 가기 메뉴에서 선택하여 **Azure Storage Explorer**를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="5aca7-379">**Azure Storage Explorer를 열려면**</span><span class="sxs-lookup"><span data-stu-id="5aca7-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="5aca7-380">Ctrl+Shift+P를 선택하여 명령 팔레트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="5aca7-381">**Open Web Azure Storage Explorer**를 입력하거나 스크립트 편집기에서 상대 경로 또는 전체 경로를 마우스 오른쪽 단추로 클릭한 다음 **Open Web Azure Storage Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="5aca7-382">Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="5aca7-383">Data Lake Tools가 Azure Portal에서 Azure 저장소 경로를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="5aca7-384">경로를 찾고 웹에서 파일을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="5aca7-385">Windows 사용자에 대한 로컬 실행 및 로컬 디버그</span><span class="sxs-lookup"><span data-stu-id="5aca7-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="5aca7-386">U-SQL 로컬 실행은 Data Lake Analytics에 코드가 게시되기 전에 로컬 데이터를 테스트하고 로컬에서 스크립트의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="5aca7-387">로컬 디버그 기능을 사용하면 Data Lake Analytics에 코드를 전송하기 전에 다음 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="5aca7-388">C# 코드 숨김을 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="5aca7-389">코드를 단계별로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-389">Step through the code.</span></span> 
- <span data-ttu-id="5aca7-390">로컬에서 스크립트의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-390">Validate your script locally.</span></span>

<span data-ttu-id="5aca7-391">로컬 실행 및 로컬 디버그에 대한 지침은 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="5aca7-392">추가 기능</span><span class="sxs-lookup"><span data-stu-id="5aca7-392">Additional features</span></span>

<span data-ttu-id="5aca7-393">Data Lake Tools for VSCode에서 지원하는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="5aca7-394">IntelliSense 자동 완성: 키워드, 메서드 및 변수와 같은 제안이 항목 주위의 팝업 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="5aca7-395">다음과 같이 다양한 아이콘이 여러 형식의 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="5aca7-396">Scala 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="5aca7-396">Scala data type</span></span>
    - <span data-ttu-id="5aca7-397">복합 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="5aca7-397">Complex data type</span></span>
    - <span data-ttu-id="5aca7-398">기본 제공 UDT</span><span class="sxs-lookup"><span data-stu-id="5aca7-398">Built-in UDTs</span></span>
    - <span data-ttu-id="5aca7-399">.NET 컬렉션 및 클래스</span><span class="sxs-lookup"><span data-stu-id="5aca7-399">.NET collection and classes</span></span>
    - <span data-ttu-id="5aca7-400">C# 식</span><span class="sxs-lookup"><span data-stu-id="5aca7-400">C# expressions</span></span>
    - <span data-ttu-id="5aca7-401">기본 제공 C# UDF, UDO 및 UDAAG</span><span class="sxs-lookup"><span data-stu-id="5aca7-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="5aca7-402">U-SQL 함수</span><span class="sxs-lookup"><span data-stu-id="5aca7-402">U-SQL functions</span></span>
    - <span data-ttu-id="5aca7-403">U-SQL 창 작업 함수</span><span class="sxs-lookup"><span data-stu-id="5aca7-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="5aca7-405">Data Lake Analytics 메타데이터의 IntelliSense 자동 완성: Data Lake Tools는 Data Lake Analytics 메타데이터 정보를 로컬로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="5aca7-406">IntelliSense 기능은 Data Lake Analytics 메타데이터에서 데이터베이스, 스키마, 테이블, 보기, 테이블 반환 함수, 프로시저 및 C# 어셈블리 등의 개체를 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 메타데이터](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="5aca7-408">IntelliSense 오류 마커: Data Lake Tools는 U-SQL 및 C#의 편집 오류에 밑줄을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="5aca7-409">구문 강조 표시: Data Lake Tools는 변수, 키워드, 데이터 형식 및 함수 등의 항목을 구분하기 위해 서로 다른 색을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aca7-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools for Visual Studio Code 구문 강조 표시](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="5aca7-411">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5aca7-411">Next steps</span></span>

- <span data-ttu-id="5aca7-412">Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그는 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="5aca7-413">Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="5aca7-414">Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="5aca7-415">어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5aca7-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



