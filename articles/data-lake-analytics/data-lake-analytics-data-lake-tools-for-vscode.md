---
title: "Azure Data Lake Tools: Azure Data Lake Tools for Visual Studio Code 사용 | Microsoft Docs"
description: "Toouse Azure 데이터 레이크 Tools for Visual Studio Code toocreate 테스트 및 U-SQL 스크립트 실행 방법에 대해 알아봅니다. "
Keywords: "VScode, Azure 데이터 레이크 도구, 로컬 실행 로컬 디버그, 디버깅, 로컬 미리 보기 저장소 파일 업로드 toostorage 경로"
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
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="efe33-104">Azure Data Lake Tools for Visual Studio Code 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="efe33-105">Toouse Azure 데이터 레이크 Tools for Visual Studio Code (VS Code) toocreate 테스트 및 U-SQL 스크립트 실행 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="efe33-106">hello 정보 비디오를 따라 hello에 대해서는:</span><span class="sxs-lookup"><span data-stu-id="efe33-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="efe33-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="efe33-107">Prerequisites</span></span>

<span data-ttu-id="efe33-108">데이터 레이크 도구는 VS Code에서 지 원하는 hello 플랫폼에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="efe33-109">Windows, Linux 및 MacOS hello 지원 플랫폼에는 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="efe33-110">hello 다른 플랫폼에는 다음 필수 구성 요소는 hello:</span><span class="sxs-lookup"><span data-stu-id="efe33-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="efe33-111">Windows</span><span class="sxs-lookup"><span data-stu-id="efe33-111">Windows</span></span>

    - <span data-ttu-id="efe33-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="efe33-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="efe33-113">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="efe33-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="efe33-114">Hello java.exe 경로 toohello 시스템 환경 변수 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="efe33-115">구성 지침은 [또는 하는 방법 설정 hello 경로 시스템 변수를 변경?]( https://www.java.com/download/help/path.xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="efe33-116">hello 경로가 tooC:\Program Files\Java\jdk1.8.0_77\jre\bin 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="efe33-117">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="efe33-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="efe33-118">Linux(Ubuntu 14.04 LTS 권장)</span><span class="sxs-lookup"><span data-stu-id="efe33-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="efe33-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="efe33-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="efe33-120">tooinstall 코드 hello를 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="efe33-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/)</span><span class="sxs-lookup"><span data-stu-id="efe33-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="efe33-122">tooupdate hello deb 패키지 원본 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="efe33-123">모노, tooinstall hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="efe33-124">Mono 4.6은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="efe33-125">4.2.x 버전을 설치하기 전에 먼저 4.6 버전을 완전히 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="efe33-126">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="efe33-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="efe33-127">설치 지침은 hello [Java에 대 한 Linux 64 비트 설치 지침]( https://java.com/en/download/help/linux_x64_install.xml) 페이지.</span><span class="sxs-lookup"><span data-stu-id="efe33-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="efe33-128">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="efe33-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="efe33-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="efe33-129">MacOS</span></span>

    - <span data-ttu-id="efe33-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="efe33-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="efe33-131">[Mono 4.2.4.x](http://download.mono-project.com/archive/4.2.4/macos-10-x86/)</span><span class="sxs-lookup"><span data-stu-id="efe33-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="efe33-132">[Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) -</span><span class="sxs-lookup"><span data-stu-id="efe33-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="efe33-133">설치 지침은 hello [Java에 대 한 Linux 64 비트 설치 지침](https://java.com/en/download/help/mac_install.xml) 페이지.</span><span class="sxs-lookup"><span data-stu-id="efe33-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="efe33-134">[.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="efe33-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="efe33-135">Data Lake Tools 설치</span><span class="sxs-lookup"><span data-stu-id="efe33-135">Install Data Lake Tools</span></span>

<span data-ttu-id="efe33-136">Hello 필수 구성 요소를 설치한 후에 VS Code에 대 한 데이터 레이크 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="efe33-137">**데이터 레이크 도구 tooinstall**</span><span class="sxs-lookup"><span data-stu-id="efe33-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="efe33-138">Visual Studio Code를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="efe33-139">Ctrl + P를 선택 하 고 다음 명령을 hello를 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="efe33-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="efe33-140">Visual Studio 코드 확장 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="efe33-141">그 중 하나는 **Azure Data Lake Tools**입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="efe33-142">선택 **설치** 다음 너무**Azure 데이터 레이크 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="efe33-143">몇 초 후 hello **설치** 너무 변경 단추**다시 로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="efe33-144">선택 **다시 로드** tooactivate hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="efe33-145">선택 **확인** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="efe33-146">Hello에서 Azure 데이터 레이크 도구를 볼 수 있듯이 **확장** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="efe33-147">![Data Lake Tools for Visual Studio Code 확장 창](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="efe33-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="efe33-148">Azure Data Lake 도구 활성화</span><span class="sxs-lookup"><span data-stu-id="efe33-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="efe33-149">새.usql 파일을 만들거나 기존.usql 파일 tooactivate hello 확장을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="efe33-150">TooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="efe33-150">Connect tooAzure</span></span>

<span data-ttu-id="efe33-151">컴파일 및 Data Lake 분석 U-SQL 스크립트를 실행할 수 있습니다, 전에 tooyour Azure 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="efe33-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="efe33-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="efe33-153">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="efe33-154">**ADL: Login**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="efe33-155">hello에 hello 로그인 정보가 표시 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="efe33-156">![Data Lake Tools for Visual Studio Code 명령 팔레트](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 장치 로그인 정보](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="efe33-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="efe33-157">선택 Ctrl + 클릭 hello 로그인 URL: https://aka.ms/devicelogin tooopen hello 로그인 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="efe33-158">Hello 코드를 입력 **G567LX42V** hello 텍스트 상자를 선택한 후에 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Data Lake Tools for Visual Studio Code 로그인 코드 붙여넣기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="efe33-160">지침 toosign hello hello 웹 페이지에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="efe33-161">Azure 계정 이름은 hello의 hello 왼쪽 아래 모서리에 hello 상태 표시줄에 표시 연결 되었을 때 **VS Code** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="efe33-162">계정에 활성화된 두 가지 요인이 있는 경우 PIN을 사용하는 것보다 전화 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="efe33-163">hello 명령을 입력 하는 아웃 toosign **ADL: 로그 아웃**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="efe33-164">Data Lake Analytics 계정 나열</span><span class="sxs-lookup"><span data-stu-id="efe33-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="efe33-165">Data Lake 분석 계정 목록이 가져오기 tootest hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="efe33-166">**Azure 구독에서 toolist hello Data Lake 분석 계정**</span><span class="sxs-lookup"><span data-stu-id="efe33-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="efe33-167">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="efe33-168">**ADL: List Accounts**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="efe33-169">hello에 hello 계정 표시 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="efe33-170">열기 hello 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="efe33-170">Open hello sample script</span></span>
<span data-ttu-id="efe33-171">명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 열기 예제 스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="efe33-172">그러면 이 샘플의 다른 인스턴스가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-172">This opens another instance of this sample.</span></span> <span data-ttu-id="efe33-173">이 인스턴스에서 스크립트를 편집, 구성, 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="efe33-174">U-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-174">Work with U-SQL</span></span>

<span data-ttu-id="efe33-175">U-SQL 파일 또는 폴더 toowork U-SQL으로 열 필요 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="efe33-176">**tooopen U-SQL 프로젝트에 대 한 폴더**</span><span class="sxs-lookup"><span data-stu-id="efe33-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="efe33-177">Visual Studio Code에서 선택 hello **파일** 메뉴를 선택한 후 **폴더 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="efe33-178">폴더를 지정한 다음 **폴더 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="efe33-179">선택 hello **파일** 메뉴를 선택한 후 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="efe33-180">제목 없음 1 파일 toohello 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="efe33-181">Hello hello 제목 없음 1 파일에 코드를 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-181">Enter hello following code into hello Untitled-1 file:</span></span>

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

    <span data-ttu-id="efe33-182">hello 스크립트 hello /output 폴더에 포함 된 일부 데이터 departments.csv 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="efe33-183">Hello 파일으로 저장 **myUSQL.usql** hello 폴더 열렸습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="efe33-184">Adltools_settings.json 구성 파일에는 toohello 프로젝트도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="efe33-185">페이지를 열고 다음과 같은 속성 hello를 사용 하 여 adltools_settings.json를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="efe33-186">Account: Azure 구독에 있는 Data Lake Analytics 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="efe33-187">Database: 사용자 계정의 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-187">Database: A database under your account.</span></span> <span data-ttu-id="efe33-188">hello 기본값은 **마스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-188">hello default is **master**.</span></span>
    - <span data-ttu-id="efe33-189">Schema: 데이터베이스의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-189">Schema: A schema under your database.</span></span> <span data-ttu-id="efe33-190">hello 기본값은 **dbo**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="efe33-191">선택적 설정</span><span class="sxs-lookup"><span data-stu-id="efe33-191">Optional settings:</span></span>
        - <span data-ttu-id="efe33-192">우선 순위: hello 우선 순위 범위는 1부터 1 too1000에서 hello 가장 높은 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="efe33-193">hello 기본값은 **1000**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="efe33-194">병렬 처리: 1 too150에서 hello 병렬 처리 수준 범위가입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="efe33-195">hello 기본값은 hello 최대 병렬 처리 Azure Data Lake 분석 계정에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="efe33-196">Hello 설정이 유효 하지 않은 경우 hello 기본값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Data Lake Tools for Visual Studio Code 구성 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="efe33-198">Data Lake 분석 계정이 계산 필요 toocompile U-SQL 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="efe33-199">컴파일 및 U-SQL 작업을 실행 하기 전에 hello 컴퓨터 계정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="efe33-200">Hello 구성 저장 된 후 hello 계정, 데이터베이스 및 스키마 정보 hello 해당.usql 파일의 hello 왼쪽 아래 모퉁이에 hello 상태 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="efe33-201">비교 tooopening 하면 폴더를 열 때 파일:</span><span class="sxs-lookup"><span data-stu-id="efe33-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="efe33-202">코드 숨김 파일 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-202">Use a code-behind file.</span></span> <span data-ttu-id="efe33-203">코드 숨김은 hello 단일 파일 모드에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="efe33-204">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-204">Use a configuration file.</span></span> <span data-ttu-id="efe33-205">폴더를 열 때 hello 작업 폴더의에서 hello 스크립트는 단일 구성 파일을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="efe33-206">U-SQL 스크립트 hello hello Data Lake 분석 서비스를 통해 원격으로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="efe33-207">Hello를 실행 하면 **컴파일** 명령, hello U-SQL 스크립트 tooyour Data Lake 분석 계정에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="efe33-208">이상 버전에서는 Visual Studio Code hello 컴파일 결과를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="efe33-209">Toohello 원격 컴파일 인해 Visual Studio Code hello 구성 파일에 tooconnect tooyour Data Lake 분석 계정 hello 정보를 표시 하는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="efe33-210">**toocompile는 U-SQL 스크립트**</span><span class="sxs-lookup"><span data-stu-id="efe33-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="efe33-211">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="efe33-212">**ADL:Compile Script**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="efe33-213">hello 컴파일 결과에 표시 hello **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="efe33-214">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭 하 고 다음 선택 **ADL: 컴파일 스크립트** toocompile는 U-SQL 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="efe33-215">hello에 hello 컴파일 결과 표시 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="efe33-216">**toosubmit는 U-SQL 스크립트**</span><span class="sxs-lookup"><span data-stu-id="efe33-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="efe33-217">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="efe33-218">**ADL:Submit Job**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="efe33-219">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Submit Job**을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="efe33-220">Hello에 hello 전송 로그 표시 U-SQL 작업을 제출 하면 **출력** VS Code의 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="efe33-221">Hello 제출 되 면 hello 작업 URL이도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="efe33-222">웹 브라우저 tootrack hello 실시간 작업 상태에 hello 작업 URL을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="efe33-223">hello 작업 세부 정보의 tooenable hello 출력 설정 **jobInformationOutputPath** hello에 **vs hello u sql_settings.json에 대 한 코드** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="efe33-224">코드 숨김 파일 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-224">Use a code-behind file</span></span>

<span data-ttu-id="efe33-225">코드 숨김 파일은 단일 U-SQL 스크립트와 연결되는 C# 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="efe33-226">스크립트 전용 tooUDO, UDA, UDT 및 UDF hello 코드 숨김 파일에서 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="efe33-227">hello UDO, UDA, UDT 및 UDF 용도 hello 스크립트에서 직접 hello 어셈블리를 먼저 등록 하지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="efe33-228">hello 코드 숨김 파일에에서 저장 됩니다 hello 동일 피어 링 U-SQL 스크립트 파일과 해당 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="efe33-229">Hello 스크립트 xxx.usql 이름이 이면 hello 코드 숨김 xxx.usql.cs로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="efe33-230">Hello 코드 숨김 파일을 수동으로 삭제 하면 관련된 U-SQL 스크립트에 대 한 코드 숨김 기능 hello 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="efe33-231">U-SQL 스크립트의 고객 코드 만들기에 대한 자세한 내용은 [U-SQL에서 사용자 지정 코드 만들기 및 사용: 사용자 정의 함수]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="efe33-232">toosupport 코드 숨김을 작업 폴더를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="efe33-233">**toogenerate 코드 숨김 파일**</span><span class="sxs-lookup"><span data-stu-id="efe33-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="efe33-234">원본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-234">Open a source file.</span></span> 
2. <span data-ttu-id="efe33-235">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="efe33-236">**ADL:Generate Code Behind**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="efe33-237">코드 숨김 파일을 만들 hello에 동일한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="efe33-238">또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Generate Code Behind**를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="efe33-239">toocompile 및 코드 숨김 파일과 함께 U-SQL 스크립트 hello 독립 실행형 U-SQL 스크립트 파일 같은 hello은 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="efe33-240">다음 두 가지 스크린샷입니다 hello 코드 숨김 파일 및 관련된 U-SQL 스크립트 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 코드 숨김 스크립트 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="efe33-243">어셈블리 사용</span><span class="sxs-lookup"><span data-stu-id="efe33-243">Use assemblies</span></span>

<span data-ttu-id="efe33-244">어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="efe33-245">Hello Data Lake 분석 카탈로그에 데이터 레이크 도구 tooregister 사용자 지정 코드 어셈블리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="efe33-246">**tooregister 어셈블리**</span><span class="sxs-lookup"><span data-stu-id="efe33-246">**tooregister an assembly**</span></span>

<span data-ttu-id="efe33-247">Hello 통해 hello 어셈블리를 등록할 수 **ADL: 어셈블리 등록** 또는 **ADL: 구성을 통해 어셈블리 등록** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="efe33-248">**hello ADL 통해 tooregister: 어셈블리 등록 명령**</span><span class="sxs-lookup"><span data-stu-id="efe33-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="efe33-249">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="efe33-250">**ADL:Register Assembly**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="efe33-251">Hello 로컬 어셈블리 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="efe33-252">Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="efe33-253">데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-253">Select a database.</span></span>

<span data-ttu-id="efe33-254">결과: hello 포털 브라우저에서 열 및 hello 어셈블리 등록 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="efe33-255">다른 편리 tootrigger hello **ADL: 어셈블리 등록** 명령 파일 탐색기에서 tooright 클릭 hello.dll 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="efe33-256">**tooregister에 있지만 ADL hello: 구성 명령을 통해 어셈블리 등록**</span><span class="sxs-lookup"><span data-stu-id="efe33-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="efe33-257">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="efe33-258">**ADL: Register Assembly through Configuration**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="efe33-259">Hello 로컬 어셈블리 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="efe33-260">hello JSON 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-260">hello JSON file is displayed.</span></span> <span data-ttu-id="efe33-261">검토 하 고 필요한 경우 hello 어셈블리 종속성 및 리소스 매개 변수를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="efe33-262">지침은 hello에 표시 됩니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="efe33-263">tooproceed toohello 어셈블리 등록 (Ctrl + S) hello JSON 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="efe33-265">어셈블리 종속성: Azure 데이터 레이크 도구 autodetects hello DLL의 모든 종속 관계에 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="efe33-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="efe33-266">감지 된 hello 종속성 hello JSON 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="efe33-267">리소스: hello 어셈블리 등록의 일부로 DLL 리소스 (예:.txt,.png, 및.csv)을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="efe33-268">또 다른 방법은 tootrigger hello **ADL: 구성을 통해 어셈블리 등록** 명령 파일 탐색기에서 tooright 클릭 hello.dll 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="efe33-269">hello U-SQL 코드 다음 방법을 보여 줍니다. 방법을 toocall 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="efe33-270">Hello 샘플 hello 어셈블리 이름은 *테스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-270">In hello sample, hello assembly name is *test*.</span></span>

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
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="efe33-271">액세스 hello Data Lake 분석 카탈로그</span><span class="sxs-lookup"><span data-stu-id="efe33-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="efe33-272">TooAzure에 연결한 후 다음 단계 tooaccess hello U-SQL 카탈로그 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="efe33-273">**tooaccess hello Azure Data Lake 분석 메타 데이터**</span><span class="sxs-lookup"><span data-stu-id="efe33-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="efe33-274">Ctrl+Shift+P를 선택한 다음 **ADL: List Tables**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="efe33-275">Hello Data Lake 분석 계정 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="efe33-276">Hello Data Lake 분석 데이터베이스 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="efe33-277">Hello 스키마 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-277">Select one of hello schemas.</span></span> <span data-ttu-id="efe33-278">테이블의 hello 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="efe33-279">Data Lake Analytics 작업 보기</span><span class="sxs-lookup"><span data-stu-id="efe33-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="efe33-280">**tooview Data Lake 분석 작업**</span><span class="sxs-lookup"><span data-stu-id="efe33-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="efe33-281">명령 팔레트 hello (Ctrl + Shift + P)를 열고 선택 **ADL: 표시할 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="efe33-282">Data Lake Analytics 또는 로컬 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="efe33-283">계정 tooappear hello에 대 한 hello 작업 목록에 대 한 대기입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="efe33-284">작업 목록에서 작업을 선택, 데이터 레이크 도구 hello Azure 포털에서에서 작업 세부 정보를 hello 열리고 VS Code의 hello JobInfo 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="efe33-286">Azure Data Lake Storage 통합</span><span class="sxs-lookup"><span data-stu-id="efe33-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="efe33-287">다음 작업에 Azure Data Lake Storage 관련 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="efe33-288">Hello Azure 데이터 레이크 저장소 리소스를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="efe33-289">미리 보기 hello Azure 데이터 레이크 저장소 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="efe33-290">Hello 업로드 VS 코드에서 직접 tooAzure 데이터 레이크 저장소 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="efe33-291">목록 hello 저장소 경로</span><span class="sxs-lookup"><span data-stu-id="efe33-291">List hello storage path</span></span> 
<span data-ttu-id="efe33-292">마우스 오른쪽 단추 클릭 또는 hello 명령 팔레트 통해 hello 저장소 경로 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="efe33-293">**hello 명령 팔레트를 통한 toolist hello 저장소 경로**</span><span class="sxs-lookup"><span data-stu-id="efe33-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="efe33-294">명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 목록 저장소 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="efe33-296">Hello 저장소 경로 나열 하기 위한 기본적인된 방법 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="efe33-297">이 구절에서는 **Enter a path**를 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-297">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio 코드는 한 가지 방법은 toolist hello 저장 경로 대 한 데이터 레이크 도구](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="efe33-299">VS Code 모든 Data Lake 분석 계정에 마지막으로 방문한 경로 hello를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="efe33-300">예: /tt/ss</span><span class="sxs-lookup"><span data-stu-id="efe33-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="efe33-301">브라우저에서 루트 경로: 선택한 Data Lake 분석 계정 또는 로컬 경로에서 hello 목록 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="efe33-302">경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="efe33-303">Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code more 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="efe33-305">선택 **자세한** toolist 자세한 Data Lake 분석 계정 및 Data Lake 분석 계정 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="efe33-307">Azure 저장소 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-307">Enter an Azure storage path.</span></span> <span data-ttu-id="efe33-308">예: /output</span><span class="sxs-lookup"><span data-stu-id="efe33-308">For example, /output.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="efe33-310">결과: hello 명령 팔레트에서 hello 경로 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 결과 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="efe33-312">Hello를 통해 toolist hello에 대 한 상대 경로 보다 쉽게 단추로 상황에 맞는 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="efe33-313">**toolist hello 저장 경로 통해 마우스 오른쪽 단추로 클릭**</span><span class="sxs-lookup"><span data-stu-id="efe33-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="efe33-314">경로 문자열 tooselect hello를 마우스 오른쪽 단추로 클릭 **목록 저장소 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="efe33-316">상대 경로 선택된 하는 hello hello 명령 팔레트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-316">hello selected relative path appears in hello command palette.</span></span>

   ![Data Lake Tools for Visual Studio Code에서 선택한 상대 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="efe33-318">Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="efe33-320">결과: hello 명령 팔레트 hello 폴더와 hello 현재 경로 대 한 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Hello 현재 경로에서 Visual Studio 코드 목록에 대 한 데이터 레이크 도구](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="efe33-322">미리 보기 hello 저장소 파일</span><span class="sxs-lookup"><span data-stu-id="efe33-322">Preview hello storage file</span></span>
<span data-ttu-id="efe33-323">마우스 오른쪽 단추 클릭 또는 hello 명령 팔레트 통해 hello 저장소 파일을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="efe33-324">**명령 팔레트 hello 통해 toopreview hello 저장소 파일**</span><span class="sxs-lookup"><span data-stu-id="efe33-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="efe33-325">명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 미리 보기 저장소 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 저장소 파일 미리 보기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="efe33-327">Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 계정 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="efe33-329">선택 **자세한** toolist 자세한 Data Lake 분석 계정 및 Data Lake 분석 계정 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="efe33-331">Azure 저장소 경로 또는 파일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="efe33-332">예: /output/SearchLog.txt</span><span class="sxs-lookup"><span data-stu-id="efe33-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 저장소 경로 및 파일 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="efe33-334">결과: hello 명령 팔레트에서 hello 경로 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="efe33-336">**toolist hello 저장 경로 통해 마우스 오른쪽 단추로 클릭**</span><span class="sxs-lookup"><span data-stu-id="efe33-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="efe33-337">파일을 toopreview 단추로 hello 파일 경로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-337">toopreview a file, right-click hello file path.</span></span>

   ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="efe33-339">Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="efe33-341">결과: VS Code hello hello 파일의 결과 미리 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="efe33-343">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="efe33-343">Upload a file</span></span> 

<span data-ttu-id="efe33-344">Hello 명령을 입력 하 여 파일을 업로드할 수 **ADL: 파일 업로드** 또는 **ADL: 구성을 통해 파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="efe33-345">**tooupload 파일은 있지만 ADL hello: 파일 업로드 명령**</span><span class="sxs-lookup"><span data-stu-id="efe33-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="efe33-346">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 하거나 hello 스크립트 편집기를 마우스 오른쪽 단추로 클릭 하 고 다음을 입력 **파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="efe33-347">tooupload hello 파일에서 로컬 경로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-347">tooupload hello file, enter a local path.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 로컬 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="efe33-349">목록 hello 저장소 경로 hello 방법 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="efe33-350">이 구절에서는 **Enter a path**를 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="efe33-352">VS Code 모든 Data Lake 분석 계정에 마지막으로 방문한 경로 hello를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="efe33-353">예: /tt/ss</span><span class="sxs-lookup"><span data-stu-id="efe33-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="efe33-354">브라우저에서 루트 경로: 선택한 Data Lake 분석 계정 또는 로컬 경로에서 hello 목록 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="efe33-355">경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="efe33-356">Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 저장소를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="efe33-358">Azure 저장소 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-358">Enter an Azure storage path.</span></span> <span data-ttu-id="efe33-359">예: /output</span><span class="sxs-lookup"><span data-stu-id="efe33-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="efe33-360">Azure 저장소 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-360">Find your Azure storage path.</span></span> <span data-ttu-id="efe33-361">**Choose current folder**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools for Visual Studio Code에서 폴더 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="efe33-363">결과: hello **출력** hello 파일 업로드 상태 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="efe33-365">**tooupload 파일은 있지만 ADL hello: 구성 명령을 통해 파일 업로드**</span><span class="sxs-lookup"><span data-stu-id="efe33-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="efe33-366">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 하거나 hello 스크립트 편집기를 마우스 오른쪽 단추로 클릭 하 고 다음을 입력 **구성을 통해 파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="efe33-367">VS Code에서 JSON 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="efe33-368">파일 경로 입력 하 고 hello에 여러 파일을 업로드할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="efe33-369">지침은 hello에 표시 됩니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="efe33-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="efe33-370">tooproceed tooupload hello 파일 (Ctrl + S) hello JSON 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Data Lake Tools for Visual Studio Code 파일 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="efe33-372">결과: hello **출력** hello 파일 업로드 상태 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="efe33-374">또 다른 방법은 tooupload 파일 toostorage hello 방식은 단추로 hello 파일의 전체 경로 또는 hello 파일의 상대 경로 hello 스크립트 편집기에 대 한 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="efe33-375">Hello 로컬 파일 경로 입력 한 다음 hello 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="efe33-376">hello **출력** hello 업로드 상태 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="efe33-377">Azure Storage Explorer 열기</span><span class="sxs-lookup"><span data-stu-id="efe33-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="efe33-378">열 수 **Azure 저장소 탐색기** hello 명령을 입력 하 여 **ADL: 웹 Azure 저장소 탐색기 열기** hello 오른쪽 클릭 상황에 맞는 메뉴에서 선택 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="efe33-379">**Azure 저장소 탐색기 tooopen**</span><span class="sxs-lookup"><span data-stu-id="efe33-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="efe33-380">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="efe33-381">입력 **열려 있는 웹 Azure 저장소 탐색기** 또는 상대 경로 또는 hello hello 스크립트 편집기에서 전체 경로 마우스 오른쪽 단추로 클릭 한 다음 선택 **열려 있는 웹 Azure 저장소 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="efe33-382">Data Lake Analytics 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="efe33-383">데이터 레이크 도구 hello Azure 포털에서에서 hello Azure 저장소 경로를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="efe33-384">Hello 경로 미리 보기 hello hello 웹 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="efe33-385">Windows 사용자에 대한 로컬 실행 및 로컬 디버그</span><span class="sxs-lookup"><span data-stu-id="efe33-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="efe33-386">로컬 데이터를 테스트 하 고 코드를 게시 된 tooData Lake 분석 하기 전에 로컬에서 스크립트의 유효성을 검사 하는 U-SQL 로컬 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="efe33-387">hello 로컬 디버그 기능을 사용 하면 있습니다 toocomplete hello 코드 되기 전에 작업을 다음 tooData Lake 분석을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="efe33-388">C# 코드 숨김을 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="efe33-389">Hello 코드를 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-389">Step through hello code.</span></span> 
- <span data-ttu-id="efe33-390">로컬에서 스크립트의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-390">Validate your script locally.</span></span>

<span data-ttu-id="efe33-391">로컬 실행 및 로컬 디버그에 대한 지침은 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="efe33-392">추가 기능</span><span class="sxs-lookup"><span data-stu-id="efe33-392">Additional features</span></span>

<span data-ttu-id="efe33-393">VS Code에 대 한 데이터 레이크 도구 hello 같은 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="efe33-394">IntelliSense 자동 완성: 키워드, 메서드 및 변수와 같은 제안이 항목 주위의 팝업 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="efe33-395">서로 다른 아이콘이 다양 한 유형의 hello 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="efe33-396">Scala 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="efe33-396">Scala data type</span></span>
    - <span data-ttu-id="efe33-397">복합 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="efe33-397">Complex data type</span></span>
    - <span data-ttu-id="efe33-398">기본 제공 UDT</span><span class="sxs-lookup"><span data-stu-id="efe33-398">Built-in UDTs</span></span>
    - <span data-ttu-id="efe33-399">.NET 컬렉션 및 클래스</span><span class="sxs-lookup"><span data-stu-id="efe33-399">.NET collection and classes</span></span>
    - <span data-ttu-id="efe33-400">C# 식</span><span class="sxs-lookup"><span data-stu-id="efe33-400">C# expressions</span></span>
    - <span data-ttu-id="efe33-401">기본 제공 C# UDF, UDO 및 UDAAG</span><span class="sxs-lookup"><span data-stu-id="efe33-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="efe33-402">U-SQL 함수</span><span class="sxs-lookup"><span data-stu-id="efe33-402">U-SQL functions</span></span>
    - <span data-ttu-id="efe33-403">U-SQL 창 작업 함수</span><span class="sxs-lookup"><span data-stu-id="efe33-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="efe33-405">데이터 레이크 분석 메타 데이터에 자동 완성 IntelliSense: 데이터 레이크 도구 hello Data Lake 분석 메타 데이터 정보를 로컬로 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="efe33-406">hello IntelliSense 기능은 자동으로 hello 데이터베이스, 스키마, 테이블, 뷰, 테이블 반환 함수, 프로시저 및 hello Data Lake 분석 메타 데이터에서 C# 어셈블리를 포함 하 여 개체를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 메타데이터](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="efe33-408">IntelliSense 오류 표식: 데이터 레이크 도구 U-SQL 및 C#에 대 한 오류를 편집 하는 hello에 밑줄을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="efe33-409">구문 강조 표시: 변수, 키워드, 데이터 형식 및 함수 등의 서로 다른 색 toodifferentiate 항목을 사용 하 여 데이터 레이크 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="efe33-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools for Visual Studio Code 구문 강조 표시](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="efe33-411">다음 단계</span><span class="sxs-lookup"><span data-stu-id="efe33-411">Next steps</span></span>

- <span data-ttu-id="efe33-412">Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그는 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="efe33-413">Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="efe33-414">Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="efe33-415">어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efe33-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



