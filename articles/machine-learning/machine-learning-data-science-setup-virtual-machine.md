---
title: "가상 컴퓨터를 IPython Notebook 서버로 설정 | Microsoft Docs"
description: "고급 분석용 IPython 서버와 함께 데이터 과학 환경에서 사용할 Azure 가상 컴퓨터를 설정합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 66fd9e5573390ac6faeb82ad5b0f7ddb18d50a77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="9c6c9-103">고급 분석을 위해 Azure 가상 컴퓨터를 IPython Notebook으로 설정</span><span class="sxs-lookup"><span data-stu-id="9c6c9-103">Set up an Azure virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="9c6c9-104">이 토픽에서는 데이터 과학 환경의 일부로 사용할 수 있는 고급 분석용 Azure 가상 컴퓨터를 프로비전 및 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-104">This topic shows how to provision and configure an Azure virtual machine for advanced analytics that can be used as part of a data science environment.</span></span> <span data-ttu-id="9c6c9-105">Windows 가상 컴퓨터는 IPython Notebook, Azure Storage Explorer 및 AzCopy와 같은 지원 도구뿐만 아니라 고급 분석 프로젝트에 유용한 기타 유틸리티로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, AzCopy, as well as other utilities that are useful for advanced analytics projects.</span></span> <span data-ttu-id="9c6c9-106">예를 들어 Azure 저장소 탐색기와 AzCopy는 로컬 컴퓨터에서 Azure Blob 저장소로 데이터를 업로드하거나 Blob 저장소에서 로컬 컴퓨터로 데이터를 다운로드하는 데 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure blob storage from your local machine or to download it to your local machine from blob storage.</span></span>

## <span data-ttu-id="9c6c9-107"><a name="create-vm"></a>1단계: 범용 Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="9c6c9-107"><a name="create-vm"></a>Step 1: Create a general-purpose Azure virtual machine</span></span>
<span data-ttu-id="9c6c9-108">Azure 가상 컴퓨터가 이미 있는 경우 여기에서 IPython Notebook 서버를 설정하려면 이 단계를 건너뛰고 [2단계: 기존 가상 컴퓨터에 IPython Notebook에 대한 끝점 추가](#add-endpoint)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-108">If you already have an Azure virtual machine and just want to set up an IPython Notebook server on it, you can skip this step and proceed to [Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine](#add-endpoint).</span></span>

<span data-ttu-id="9c6c9-109">Azure에서 가상 컴퓨터를 만드는 프로세스를 시작하기 전에 해당 프로젝트에 대한 데이터를 처리하는 데 필요한 컴퓨터의 크기를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-109">Before starting the process of creating a virtual machine on Azure, you need to determine the size of the machine that is needed to process the data for their project.</span></span> <span data-ttu-id="9c6c9-110">컴퓨터가 작을수록 메모리가 작고 CPU 코어 수가 적지만 비용도 적게 듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-110">Smaller machines have less memory and fewer CPU cores than larger machines, but they are also less expensive.</span></span> <span data-ttu-id="9c6c9-111">컴퓨터 유형 및 가격 목록은 <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">가상 컴퓨터 가격</a> 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-111">For a list of machine types and prices, see the <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">Virtual Machines Pricing </a> page</span></span>

1. <span data-ttu-id="9c6c9-112"><a href="https://manage.windowsazure.com" target="_blank">Azure 클래식 포털</a>에 로그인하여 왼쪽 아래에서 **새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-112">Log in to <a href="https://manage.windowsazure.com" target="_blank">Azure classic portal</a>, and click **New** in the bottom left corner.</span></span> <span data-ttu-id="9c6c9-113">팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-113">A window will pop up.</span></span> <span data-ttu-id="9c6c9-114">**계산** -> **가상 컴퓨터** -> **갤러리에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-114">Select **COMPUTE** -> **VIRTUAL MACHINE** -> **FROM GALLERY**.</span></span>
   
    ![작업 영역 만들기][24]
2. <span data-ttu-id="9c6c9-116">다음 이미지 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-116">Choose one of the following images:</span></span>
   
   * <span data-ttu-id="9c6c9-117">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="9c6c9-117">Windows Server 2012 R2 Datacenter</span></span>
   * <span data-ttu-id="9c6c9-118">Windows Server Essentials Experience(Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="9c6c9-118">Windows Server Essentials Experience (Windows Server 2012 R2)</span></span>
     
     <span data-ttu-id="9c6c9-119">그런 다음 오른쪽 아래에서 오른쪽 화살표를 클릭하여 다음 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-119">Then, click the arrow pointing right at the lower right to go the next configuration page.</span></span>
     
     ![작업 영역 만들기][25]
3. <span data-ttu-id="9c6c9-121">만들려는 가상 컴퓨터의 이름을 입력하고, 컴퓨터에서 처리할 데이터의 크기 및 컴퓨터의 성능(메모리 크기 및 계산 코어 수)에 따라 컴퓨터의 크기(기본값: A3)를 선택한 후 컴퓨터의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-121">Enter a name for the virtual machine you want to create, select the size of the machine (Default: A3) based on the size of the data the machine is going to process and how powerful you want the machine to be (memory size and the number of compute cores), enter a user name and password for the machine.</span></span> <span data-ttu-id="9c6c9-122">그런 다음 오른쪽 화살표를 클릭하여 다음 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-122">Then, click the arrow pointing right to go to the next configuration page.</span></span>
   
    ![작업 영역 만들기][26]
4. <span data-ttu-id="9c6c9-124">이 가상 컴퓨터에 사용할 **저장소 계정**이 포함된 **지역/선호도 그룹/가상 네트워크**를 선택한 후 해당 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-124">Select the **REGION/AFFINITY GROUP/VIRTUAL NETWORK** that contains the **STORAGE ACCOUNT** that you are planning to use for this virtual machine, and then select that storage account.</span></span> <span data-ttu-id="9c6c9-125">끝점의 이름(여기에서는 "IPython")을 입력하여 **끝점** 필드의 맨 아래에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-125">Add an endpoint at the bottom in the **ENDPOINTS**  field by entering the name of the endpoint ("IPython" here).</span></span> <span data-ttu-id="9c6c9-126">원하는 문자열을 끝점의 **이름**으로 선택할 수 있으며 **사용 가능한** 0에서 65536 사이의 모든 정수를 **공용 포트**로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-126">You can choose any string as the **NAME** of the end point, and any integer between 0 and 65536 that is **available** as the **PUBLIC PORT**.</span></span> <span data-ttu-id="9c6c9-127">**개인 포트**는 **9999**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-127">The **PRIVATE PORT** has to be **9999**.</span></span> <span data-ttu-id="9c6c9-128">사용자는 인터넷 서비스에 이미 할당된 공용 포트를 사용해서는 **안 됩니다** .</span><span class="sxs-lookup"><span data-stu-id="9c6c9-128">You should **avoid** using public ports that have already been assigned for internet services.</span></span> <span data-ttu-id="9c6c9-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">인터넷 서비스용 포트</a>에서는 이미 할당되어 사용해서는 안 되는 포트 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Ports for Internet Services</a> provides a list of ports that have been assigned and should be avoided.</span></span>
   
    ![작업 영역 만들기][27]
5. <span data-ttu-id="9c6c9-131">확인 표시를 클릭하여 가상 컴퓨터 프로비저닝 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-131">Click the check mark to start the virtual machine provisioning process.</span></span>
   
    ![작업 영역 만들기][28]

<span data-ttu-id="9c6c9-133">가상 컴퓨터 프로비저닝 프로세스를 완료하는 데 15~25분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-133">It may take 15-25 minutes to complete the virtual machine provisioning process.</span></span> <span data-ttu-id="9c6c9-134">가상 컴퓨터를 만든 후에는 이 컴퓨터의 상태가 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-134">After the virtual machine has been created, the status of this machine should show as **Running**.</span></span>

![작업 영역 만들기][29]

## <span data-ttu-id="9c6c9-136"><a name="add-endpoint"></a>2단계: 기존 가상 컴퓨터에 IPython Notebook에 대한 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="9c6c9-136"><a name="add-endpoint"></a>Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine</span></span>
<span data-ttu-id="9c6c9-137">1단계의 지침에 따라 가상 컴퓨터를 만든 경우 IPython Notebook에 대한 끝점이 이미 추가되었으므로 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-137">If you created the virtual machine by following the instructions in Step 1, then the endpoint for IPython Notebook has already been added and this step can be skipped.</span></span>

<span data-ttu-id="9c6c9-138">가상 컴퓨터가 이미 있는 경우 아래의 3단계에서 설치할 IPython Notebook에 대한 끝점을 추가하려면 먼저 Azure 클래식 포털에 로그인하여 가상 컴퓨터를 선택하고 IPython Notebook 서버에 대한 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-138">If the virtual machine already exists, and you need to add an endpoint for IPython Notebook that you will install in Step 3 below, first login to Azure classic portal, select the virtual machine, and add the endpoint for IPython Notebook server.</span></span> <span data-ttu-id="9c6c9-139">다음 그림에는 IPython Notebook에 대한 끝점이 Windows 가상 컴퓨터에 추가된 후의 포털에 대한 스크린샷이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-139">The following figure contains a screen shot of the portal after the endpoint for IPython Notebook has been added to a Windows virtual machine.</span></span>

![작업 영역 만들기][17]

## <span data-ttu-id="9c6c9-141"><a name="run-commands"></a>3단계: IPython Notebook 및 기타 지원 도구 설치</span><span class="sxs-lookup"><span data-stu-id="9c6c9-141"><a name="run-commands"></a>Step 3: Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="9c6c9-142">가상 컴퓨터를 만들 후 RDP(원격 데스크톱 프로토콜)를 사용하여 Windows 가상 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-142">After the virtual machine is created, use Remote Desktop Protocol (RDP) to log on to the Windows virtual machine.</span></span> <span data-ttu-id="9c6c9-143">지침은 [Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-143">For instructions, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="9c6c9-144">**관리자** 권한으로 **명령 프롬프트**(**Powershell 명령 창이 아님**)를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-144">Open the **Command Prompt** (**Not the Powershell command window**) as an **Administrator** and run the following command.</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="9c6c9-145">설치가 완료되면 *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* 디렉터리에서 IPython Notebook 서버가 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-145">When the installation completes, the IPython Notebook server is launched automatically in the *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* directory.</span></span>

<span data-ttu-id="9c6c9-146">메시지가 표시되면 IPython Notebook의 암호화 컴퓨터 관리자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-146">When prompted, enter a password for the IPython Notebook and the password of the machine administrator.</span></span> <span data-ttu-id="9c6c9-147">그러면 IPython Notebook을 컴퓨터에서 서비스로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-147">This enables the IPython Notebook to run as a service on the machine.</span></span>

## <span data-ttu-id="9c6c9-148"><a name="access"></a>4단계: 웹 브라우저에서 IPython Notebook 액세스</span><span class="sxs-lookup"><span data-stu-id="9c6c9-148"><a name="access"></a>Step 4: Access IPython Notebooks from a web browser</span></span>
<span data-ttu-id="9c6c9-149">IPython Notebook 서버에 액세스하려면 웹 브라우저를 열고 URL 텍스트 상자에 *https://&#60;virtual machine DNS name>:&#60;public port number>*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-149">To access the IPython Notebook server, open a web browser, and input *https://&#60;virtual machine DNS name>:&#60;public port number>* in the URL text box.</span></span> <span data-ttu-id="9c6c9-150">여기서 *&#60;public port number>*는 IPython Notebook 끝점을 추가할 때 지정한 포트 번호여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-150">Here, the *&#60;public port number>* should  be the port number you specified when the IPython Notebook endpoint was added.</span></span>

<span data-ttu-id="9c6c9-151">*&#60;virtual machine DNS name>*은 Azure 클래식 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-151">The *&#60;virtual machine DNS name>* can be found at the Azure classic portal.</span></span> <span data-ttu-id="9c6c9-152">클래식 포털에 로그인한 후 **가상 컴퓨터**를 클릭하고, 사용자가 만든 컴퓨터를 선택한 후 **대시보드**를 선택합니다. 그러면 DNS 이름이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-152">After logging in to the classic portal, click **VIRTUAL MACHINES**, select the machine you created, and then select **DASHBOARD**, the DNS name will be shown as follows:</span></span>

![작업 영역 만들기][19]

<span data-ttu-id="9c6c9-154">다음 그림과 같이 *이 웹 사이트의 보안 인증서에 문제가 있습니다*(Internet Explorer) 또는 *사용자 연결은 전용이 아닙니다*(Chrome)이라는 경고가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-154">You will encounter a warning stating that *There is a problem with this website's security certificate* (Internet Explorer) or *Your connection is not private* (Chrome), as shown in the following figures.</span></span> <span data-ttu-id="9c6c9-155">**이 웹 사이트를 계속 탐색합니다(권장하지 않음)**(Internet Explorer)를 클릭하거나 **고급**, **&#60;*DNS 이름*>을 진행합니다(안전하지 않음)**(Chrome)를 차례로 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-155">Click **Continue to this website (not recommended)** (Internet Explorer) or **Advanced** and then **Proceed to &#60;*DNS Name*> (unsafe)** (Chrome) to continue.</span></span> <span data-ttu-id="9c6c9-156">그런 다음 이전에 지정한 암호를 입력하여 IPython Notebook에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-156">Then input the password you specified earlier to access the IPython Notebooks.</span></span>

<span data-ttu-id="9c6c9-157">**Internet Explorer:**
![작업 영역 만들기][20]</span><span class="sxs-lookup"><span data-stu-id="9c6c9-157">**Internet Explorer:**
![Create workspace][20]</span></span>

<span data-ttu-id="9c6c9-158">**Chrome:**
![작업 영역 만들기][21]</span><span class="sxs-lookup"><span data-stu-id="9c6c9-158">**Chrome:**
![Create workspace][21]</span></span>

<span data-ttu-id="9c6c9-159">IPython Notebook에 로그온하면 *DataScienceSamples* 디렉터리가 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-159">After you log on to the IPython Notebook, a directory *DataScienceSamples* will show on the browser.</span></span> <span data-ttu-id="9c6c9-160">이 디렉터리에는 사용자가 데이터 과학 작업을 수행하도록 도와주기 위해 Microsoft에서 공유하는 샘플 IPython Notebook이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-160">This directory contains sample IPython Notebooks that are shared by Microsoft to help users conduct data science tasks.</span></span> <span data-ttu-id="9c6c9-161">이러한 샘플 IPython Notebook은 IPython Notebook 서버 설정 프로세스 중에 [**GitHub 리포지토리**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)에서 가상 컴퓨터로 체크 아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-161">These sample IPython Notebooks are checked out from [**GitHub repository**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) to the virtual machines during the IPython Notebook server setup process.</span></span> <span data-ttu-id="9c6c9-162">Microsoft는 이 리포지토리를 유지 관리하고 자주 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-162">Microsoft maintains and updates this repository frequently.</span></span> <span data-ttu-id="9c6c9-163">사용자는 GitHub 리포지토리를 방문하여 최근에 업데이트된 샘플 IPython Notebook을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-163">Users may visit the GitHub repository to get the most recently updated sample IPython Notebooks.</span></span>
<span data-ttu-id="9c6c9-164">![작업 영역 만들기][18]</span><span class="sxs-lookup"><span data-stu-id="9c6c9-164">![Create workspace][18]</span></span>

## <span data-ttu-id="9c6c9-165"><a name="upload"></a>5단계: 로컬 컴퓨터에서 IPython Notebook 서버로 기존 IPython Notebook 업로드</span><span class="sxs-lookup"><span data-stu-id="9c6c9-165"><a name="upload"></a>Step 5: Upload an existing IPython Notebook from a local machine to the IPython Notebook server</span></span>
<span data-ttu-id="9c6c9-166">IPython Notebook은 사용자가 로컬 컴퓨터에 있는 기존 IPython Notebook을 가상 컴퓨터의 IPython Notebook 서버로 쉽게 업로드할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-166">IPython Notebooks provide an easy way for users to upload an existing IPython Notebook on their local machines to the IPython Notebook server on the virtual machines.</span></span> <span data-ttu-id="9c6c9-167">웹 브라우저에서 IPython Notebook에 로그온한 후 IPython Notebook을 업로드할 **디렉터리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-167">After you log on to the IPython Notebook in a web browser, click into the **directory** that the IPython Notebook will be uploaded to.</span></span> <span data-ttu-id="9c6c9-168">그런 다음 **파일 탐색기**를 사용하여 로컬 컴퓨터에서 업로드할 IPython Notebook .ipynb 파일을 선택한 후 웹 브라우저에서 IPython Notebook 디렉터리로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-168">Then, select an IPython Notebook .ipynb file to upload from the local machine in the **File Explorer**, and drag and drop it to the IPython Notebook directory on the web browser.</span></span> <span data-ttu-id="9c6c9-169">**업로드** 단추를 클릭하여 .ipynb 파일을 IPython Notebook 서버에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-169">Click the **Upload** button, to upload the .ipynb file to the IPython Notebook server.</span></span> <span data-ttu-id="9c6c9-170">이제 다른 사용자가 자신의 웹 브라우저에서 이 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-170">Other users can then start using it in from their web browsers.</span></span>

![작업 영역 만들기][22]

![작업 영역 만들기][23]

## <span data-ttu-id="9c6c9-173"><a name="shutdown"></a>사용하지 않을 때 가상 컴퓨터 종료 및 할당 해제</span><span class="sxs-lookup"><span data-stu-id="9c6c9-173"><a name="shutdown"></a>Shut down and de-allocate virtual machine when not in use</span></span>
<span data-ttu-id="9c6c9-174">Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-174">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="9c6c9-175">가상 컴퓨터를 사용하지 않을 때 비용이 청구되지 않도록 하려면 **중지(할당 해제)** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-175">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state when not in use.</span></span>

> [!NOTE]
> <span data-ttu-id="9c6c9-176">Windows 전원 옵션을 사용하여 VM 내부에서 가상 컴퓨터를 종료하면 VM이 중지되지만 여전히 할당된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-176">If you shut down the virtual machine from inside the VM (using Windows power options), the VM is stopped but remains allocated.</span></span> <span data-ttu-id="9c6c9-177">비용이 계속 청구되지 않도록 하려면 항상 [Azure 클래식 포털](http://manage.windowsazure.com/)에서 가상 컴퓨터를 중지하세요.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-177">To ensure you do not continue to be billed, always stop virtual machines from the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="9c6c9-178">"PostShutdownAction"이 "StoppedDeallocated"와 동일한 **ShutdownRoleOperation** 을 호출하여 Powershell을 통해 VM을 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-178">You can also stop the VM through Powershell by calling **ShutdownRoleOperation** with "PostShutdownAction" equal to "StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="9c6c9-179">가상 컴퓨터를 종료하고 할당을 해제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-179">To shut down and deallocate the virtual machine:</span></span>

1. <span data-ttu-id="9c6c9-180">사용자 계정을 사용하여 [Azure 클래식 포털](http://manage.windowsazure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-180">Log in to the [Azure classic portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="9c6c9-181">왼쪽 탐색 모음에서 **가상 컴퓨터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-181">Select **VIRTUAL MACHINES** from the left navigation bar.</span></span>
3. <span data-ttu-id="9c6c9-182">가상 컴퓨터 목록에서 가상 컴퓨터의 이름을 클릭하여 **대시보드** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-182">In the list of virtual machines, click on the name of your virtual machine then go to the **DASHBOARD** page.</span></span>
4. <span data-ttu-id="9c6c9-183">페이지 아래쪽에서 **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-183">At the bottom of the page, click **SHUTDOWN**.</span></span>

![VM 종료][15]

<span data-ttu-id="9c6c9-185">가상 컴퓨터가 할당 해제되지만 삭제되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-185">The virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="9c6c9-186">Azure 클래식 포털에서 언제든지 가상 컴퓨터를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-186">You may restart your virtual machine at any time from the Azure classic portal.</span></span>

## <a name="your-azure-vm-is-ready-to-use-whats-next"></a><span data-ttu-id="9c6c9-187">Azure VM을 사용할 준비가 되었습니다. 다음 단계는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9c6c9-187">Your Azure VM is ready to use: what's next?</span></span>
<span data-ttu-id="9c6c9-188">이제 데이터 과학 연습에서 가상 컴퓨터를 사용할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-188">Your virtual machine is now ready to use in your data science exercises.</span></span> <span data-ttu-id="9c6c9-189">또한 데이터 탐색 및 처리, Azure 기계 학습 및 팀 데이터 과학 프로세스와 함께 수행할 다른 작업 등에 가상 컴퓨터를 IPython Notebook 서버로 사용할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-189">The virtual machine is also ready for use as an IPython Notebook server for the exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and the Team Data Science Process.</span></span>

<span data-ttu-id="9c6c9-190">팀 데이터 과학 프로세스의 다음 단계는 [학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 에서 매핑되며, 데이터를 HDInsight로 이동한 후 Azure 기계 학습에서 데이터를 통해 학습할 준비를 수행하면서 데이터를 처리 및 샘플링하는 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c6c9-190">The next steps in the Team Data Science Process are mapped in the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
