---
title: "IPython 노트북 서버와 가상 컴퓨터를 aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a><span data-ttu-id="74ebd-103">고급 분석을 위해 Azure 가상 컴퓨터를 IPython Notebook으로 설정</span><span class="sxs-lookup"><span data-stu-id="74ebd-103">Set up an Azure virtual machine as an IPython Notebook server for advanced analytics</span></span>
<span data-ttu-id="74ebd-104">이 항목에서는 방법을 tooprovision 및 데이터 과학 환경의 일부로 사용할 수 있는 고급 분석을 위해 Azure 가상 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-104">This topic shows how tooprovision and configure an Azure virtual machine for advanced analytics that can be used as part of a data science environment.</span></span> <span data-ttu-id="74ebd-105">IPython 노트북, Azure 저장소 탐색기, AzCopy를 뿐 아니라 프로젝트 고급 분석에 유용한 기타 유틸리티와 같은 도구를 지 원하는 hello Windows 가상 컴퓨터 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-105">hello Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, AzCopy, as well as other utilities that are useful for advanced analytics projects.</span></span> <span data-ttu-id="74ebd-106">Azure 저장소 탐색기 및 AzCopy를 예를 들어 편리 하 게 방법 tooupload 데이터 저장소를 제공할 tooAzure blob에서 로컬 컴퓨터 또는 toodownload 것 tooyour blob 저장소에서 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways tooupload data tooAzure blob storage from your local machine or toodownload it tooyour local machine from blob storage.</span></span>

## <span data-ttu-id="74ebd-107"><a name="create-vm"></a>1단계: 범용 Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="74ebd-107"><a name="create-vm"></a>Step 1: Create a general-purpose Azure virtual machine</span></span>
<span data-ttu-id="74ebd-108">Azure 가상 컴퓨터가 이미 있는 tooset에 IPython 노트북 서버를 원하는 경우 있습니다 수이 단계를 건너뛰고 너무[2 단계: IPython 노트북 tooan 기존 가상 컴퓨터에 대 한 끝점을 추가](#add-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-108">If you already have an Azure virtual machine and just want tooset up an IPython Notebook server on it, you can skip this step and proceed too[Step 2: Add an endpoint for IPython Notebooks tooan existing virtual machine](#add-endpoint).</span></span>

<span data-ttu-id="74ebd-109">Hello Azure에서 가상 컴퓨터를 만드는 과정을 시작 하기 전에 해당 프로젝트에 대 한 필요한 tooprocess hello 데이터가 된 hello 컴퓨터의 toodetermine hello 크기를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-109">Before starting hello process of creating a virtual machine on Azure, you need toodetermine hello size of hello machine that is needed tooprocess hello data for their project.</span></span> <span data-ttu-id="74ebd-110">컴퓨터가 작을수록 메모리가 작고 CPU 코어 수가 적지만 비용도 적게 듭니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-110">Smaller machines have less memory and fewer CPU cores than larger machines, but they are also less expensive.</span></span> <span data-ttu-id="74ebd-111">컴퓨터 종류 및 가격 목록, 참조 hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">가상 컴퓨터 가격 </a> 페이지</span><span class="sxs-lookup"><span data-stu-id="74ebd-111">For a list of machine types and prices, see hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">Virtual Machines Pricing </a> page</span></span>

1. <span data-ttu-id="74ebd-112">로그 너무<a href="https://manage.windowsazure.com" target="_blank">Azure 클래식 포털</a>를 클릭 하 고 **새로** hello 하단 왼쪽된 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-112">Log in too<a href="https://manage.windowsazure.com" target="_blank">Azure classic portal</a>, and click **New** in hello bottom left corner.</span></span> <span data-ttu-id="74ebd-113">팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-113">A window will pop up.</span></span> <span data-ttu-id="74ebd-114">**계산** -> **가상 컴퓨터** -> **갤러리에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-114">Select **COMPUTE** -> **VIRTUAL MACHINE** -> **FROM GALLERY**.</span></span>
   
    ![작업 영역 만들기][24]
2. <span data-ttu-id="74ebd-116">다음 이미지는 hello 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-116">Choose one of hello following images:</span></span>
   
   * <span data-ttu-id="74ebd-117">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="74ebd-117">Windows Server 2012 R2 Datacenter</span></span>
   * <span data-ttu-id="74ebd-118">Windows Server Essentials Experience(Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="74ebd-118">Windows Server Essentials Experience (Windows Server 2012 R2)</span></span>
     
     <span data-ttu-id="74ebd-119">그런 다음 낮은 오른쪽 toogo hello hello 다음 구성 페이지에서 오른쪽을 가리키는 hello 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-119">Then, click hello arrow pointing right at hello lower right toogo hello next configuration page.</span></span>
     
     ![작업 영역 만들기][25]
3. <span data-ttu-id="74ebd-121">이름을 입력 toocreate, hello 컴퓨터의 선택 hello 크기 hello 가상 컴퓨터에 대 한 원하는 (기본값: A3) hello 데이터 hello 컴퓨터의 hello 크기에 따라 진행 중인 tooprocess 얼마나 강한 사용자가 hello 컴퓨터 toobe (메모리 크기와 hello 수 계산 코어) 를 hello 컴퓨터에 대 한 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-121">Enter a name for hello virtual machine you want toocreate, select hello size of hello machine (Default: A3) based on hello size of hello data hello machine is going tooprocess and how powerful you want hello machine toobe (memory size and hello number of compute cores), enter a user name and password for hello machine.</span></span> <span data-ttu-id="74ebd-122">그런 다음 오른쪽 toogo toohello 다음 구성 페이지를 가리키는 hello 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-122">Then, click hello arrow pointing right toogo toohello next configuration page.</span></span>
   
    ![작업 영역 만들기][26]
4. <span data-ttu-id="74ebd-124">선택 hello **지역/선호도 그룹/가상 네트워크** hello를 포함 하는 **저장소 계정** toouse이 가상 컴퓨터에 대 한 계획 하 고 해당 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-124">Select hello **REGION/AFFINITY GROUP/VIRTUAL NETWORK** that contains hello **STORAGE ACCOUNT** that you are planning toouse for this virtual machine, and then select that storage account.</span></span> <span data-ttu-id="74ebd-125">Hello에 hello 맨 아래에 끝점 추가 **끝점** hello 끝점 ("IPython" 여기)의 hello 이름을 입력 하 여 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-125">Add an endpoint at hello bottom in hello **ENDPOINTS**  field by entering hello name of hello endpoint ("IPython" here).</span></span> <span data-ttu-id="74ebd-126">Hello에 따라 모든 문자열을 선택할 수 있습니다 **이름** hello 끝점 및은 0에서 65536 사이의 임의의 정수 **사용 가능한** hello로 **공용 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-126">You can choose any string as hello **NAME** of hello end point, and any integer between 0 and 65536 that is **available** as hello **PUBLIC PORT**.</span></span> <span data-ttu-id="74ebd-127">hello **개인 포트** toobe가 **9999**합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-127">hello **PRIVATE PORT** has toobe **9999**.</span></span> <span data-ttu-id="74ebd-128">사용자는 인터넷 서비스에 이미 할당된 공용 포트를 사용해서는 **안 됩니다** .</span><span class="sxs-lookup"><span data-stu-id="74ebd-128">You should **avoid** using public ports that have already been assigned for internet services.</span></span> <span data-ttu-id="74ebd-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">인터넷 서비스용 포트</a>에서는 이미 할당되어 사용해서는 안 되는 포트 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-129"><a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Ports for Internet Services</a> provides a list of ports that have been assigned and should be avoided.</span></span>
   
    ![작업 영역 만들기][27]
5. <span data-ttu-id="74ebd-131">Hello 확인 표시가 toostart hello 가상 컴퓨터 프로 비전 프로세스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-131">Click hello check mark toostart hello virtual machine provisioning process.</span></span>
   
    ![작업 영역 만들기][28]

<span data-ttu-id="74ebd-133">15-25 분 toocomplete hello 가상 컴퓨터 프로 비전 프로세스 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-133">It may take 15-25 minutes toocomplete hello virtual machine provisioning process.</span></span> <span data-ttu-id="74ebd-134">이 컴퓨터의 상태 hello로 표시 해야 hello 가상 컴퓨터를 만든 후 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-134">After hello virtual machine has been created, hello status of this machine should show as **Running**.</span></span>

![작업 영역 만들기][29]

## <span data-ttu-id="74ebd-136"><a name="add-endpoint"></a>2 단계: IPython 노트북 tooan 기존 가상 컴퓨터에 대 한 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="74ebd-136"><a name="add-endpoint"></a>Step 2: Add an endpoint for IPython Notebooks tooan existing virtual machine</span></span>
<span data-ttu-id="74ebd-137">1 단계에서에서 hello 지침에 따라 hello 가상 컴퓨터를 만든 경우 hello 끝점 IPython 노트북을 이미 추가 되어 하 고이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-137">If you created hello virtual machine by following hello instructions in Step 1, then hello endpoint for IPython Notebook has already been added and this step can be skipped.</span></span>

<span data-ttu-id="74ebd-138">Hello 가상 컴퓨터가 이미 있는 경우 tooadd 끝점 아래 3 단계에서에서 설치한 IPython 전자 필기장에 필요한 첫 번째 로그인 tooAzure 클래식 포털 hello 가상 컴퓨터를 선택 및 IPython 노트북 서버에 대 한 hello 끝점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-138">If hello virtual machine already exists, and you need tooadd an endpoint for IPython Notebook that you will install in Step 3 below, first login tooAzure classic portal, select hello virtual machine, and add hello endpoint for IPython Notebook server.</span></span> <span data-ttu-id="74ebd-139">hello 다음 그림 hello 포털의 스크린 샷을 후 포함 IPython 전자 필기장에 대 한 hello 끝점이 tooa Windows 가상 컴퓨터 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-139">hello following figure contains a screen shot of hello portal after hello endpoint for IPython Notebook has been added tooa Windows virtual machine.</span></span>

![작업 영역 만들기][17]

## <span data-ttu-id="74ebd-141"><a name="run-commands"></a>3단계: IPython Notebook 및 기타 지원 도구 설치</span><span class="sxs-lookup"><span data-stu-id="74ebd-141"><a name="run-commands"></a>Step 3: Install IPython Notebook and other supporting tools</span></span>
<span data-ttu-id="74ebd-142">Hello 가상 컴퓨터를 만든 후 원격 데스크톱 프로토콜 (RDP) toolog toohello Windows 가상 컴퓨터에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-142">After hello virtual machine is created, use Remote Desktop Protocol (RDP) toolog on toohello Windows virtual machine.</span></span> <span data-ttu-id="74ebd-143">자세한 내용은 [어떻게 tooLog tooa Windows Server를 실행 하는 가상 컴퓨터에](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-143">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="74ebd-144">열기 hello **명령 프롬프트** (**Powershell 명령 창이 아닌 hello**)으로 **관리자** 다음 명령이 실행된 하는 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-144">Open hello **Command Prompt** (**Not hello Powershell command window**) as an **Administrator** and run hello following command.</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="74ebd-145">Hello 설치가 완료 되 면, IPython 노트북 서버 hello에 자동으로 시작 하는 hello *c:\\사용자\\\<사용자 이름\>\\문서\\IPython 노트북* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-145">When hello installation completes, hello IPython Notebook server is launched automatically in hello *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* directory.</span></span>

<span data-ttu-id="74ebd-146">메시지가 표시 되 면 hello IPython 전자 필기장에 대 한 암호 및 관리자에 게 컴퓨터의 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-146">When prompted, enter a password for hello IPython Notebook and hello password of hello machine administrator.</span></span> <span data-ttu-id="74ebd-147">그러면 hello 컴퓨터에서 서비스로 hello IPython 노트북 toorun 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-147">This enables hello IPython Notebook toorun as a service on hello machine.</span></span>

## <span data-ttu-id="74ebd-148"><a name="access"></a>4단계: 웹 브라우저에서 IPython Notebook 액세스</span><span class="sxs-lookup"><span data-stu-id="74ebd-148"><a name="access"></a>Step 4: Access IPython Notebooks from a web browser</span></span>
<span data-ttu-id="74ebd-149">tooaccess hello IPython 노트북 서버를 열고 웹 브라우저 및 입력 *https://&#60;virtual 컴퓨터 DNS 이름 >: &#60; 공용 포트 번호 >* hello URL 텍스트 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-149">tooaccess hello IPython Notebook server, open a web browser, and input *https://&#60;virtual machine DNS name>:&#60;public port number>* in hello URL text box.</span></span> <span data-ttu-id="74ebd-150">여기에서 hello *&#60; 공용 포트 번호 >* hello IPython 노트북 끝점을 추가할 때 지정한 hello 포트 번호 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-150">Here, hello *&#60;public port number>* should  be hello port number you specified when hello IPython Notebook endpoint was added.</span></span>

<span data-ttu-id="74ebd-151">hello *&#60; 가상 컴퓨터 DNS 이름 >* hello Azure 클래식 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-151">hello *&#60;virtual machine DNS name>* can be found at hello Azure classic portal.</span></span> <span data-ttu-id="74ebd-152">Toohello 클래식 포털에 로그인 한 후 클릭 **가상 컴퓨터**선택, hello 컴퓨터를 만든 하 고 선택 하면 **대시보드**, hello DNS 이름을 다음과 같이 표시 됩니다:</span><span class="sxs-lookup"><span data-stu-id="74ebd-152">After logging in toohello classic portal, click **VIRTUAL MACHINES**, select hello machine you created, and then select **DASHBOARD**, hello DNS name will be shown as follows:</span></span>

![작업 영역 만들기][19]

<span data-ttu-id="74ebd-154">않는다는 경고가 발생 하 게 *이 웹사이트 보안 인증서에 문제가* (Internet Explorer) 또는 *사용자 연결이 비공개입니다.* (Chrome), hello 다음과 같이 숫자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-154">You will encounter a warning stating that *There is a problem with this website's security certificate* (Internet Explorer) or *Your connection is not private* (Chrome), as shown in hello following figures.</span></span> <span data-ttu-id="74ebd-155">클릭 **(권장 하지 않음) 계속 toothis 웹 사이트** (Internet Explorer) 또는 **고급** 차례로  **너무 계속 &#60;* DNS 이름*> (안전 하지 않은) * * (Chrome) toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-155">Click **Continue toothis website (not recommended)** (Internet Explorer) or **Advanced** and then **Proceed too&#60;*DNS Name*> (unsafe)** (Chrome) toocontinue.</span></span> <span data-ttu-id="74ebd-156">IPython 노트북을 hello 하면 지정 된 이전 tooaccess hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-156">Then input hello password you specified earlier tooaccess hello IPython Notebooks.</span></span>

<span data-ttu-id="74ebd-157">**Internet Explorer:**
![작업 영역 만들기][20]</span><span class="sxs-lookup"><span data-stu-id="74ebd-157">**Internet Explorer:**
![Create workspace][20]</span></span>

<span data-ttu-id="74ebd-158">**Chrome:**
![작업 영역 만들기][21]</span><span class="sxs-lookup"><span data-stu-id="74ebd-158">**Chrome:**
![Create workspace][21]</span></span>

<span data-ttu-id="74ebd-159">Toohello IPython 노트북, 디렉터리에 로그인 하면 *DataScienceSamples* hello 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-159">After you log on toohello IPython Notebook, a directory *DataScienceSamples* will show on hello browser.</span></span> <span data-ttu-id="74ebd-160">이 디렉터리는 Microsoft toohelp 사용자 행위 데이터 과학 작업을 통해 공유 되는 샘플 IPython 노트북을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-160">This directory contains sample IPython Notebooks that are shared by Microsoft toohelp users conduct data science tasks.</span></span> <span data-ttu-id="74ebd-161">이러한 샘플 IPython 노트북을에서 체크 아웃 [ **GitHub 리포지토리** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) hello IPython 노트북 서버 설치 프로세스 중에 toohello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="74ebd-161">These sample IPython Notebooks are checked out from [**GitHub repository**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello virtual machines during hello IPython Notebook server setup process.</span></span> <span data-ttu-id="74ebd-162">Microsoft는 이 리포지토리를 유지 관리하고 자주 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-162">Microsoft maintains and updates this repository frequently.</span></span> <span data-ttu-id="74ebd-163">사용자가 hello GitHub 리포지토리 tooget hello 가장 최근에 업데이트 된 예제 IPython 노트북을 방문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-163">Users may visit hello GitHub repository tooget hello most recently updated sample IPython Notebooks.</span></span>
<span data-ttu-id="74ebd-164">![작업 영역 만들기][18]</span><span class="sxs-lookup"><span data-stu-id="74ebd-164">![Create workspace][18]</span></span>

## <span data-ttu-id="74ebd-165"><a name="upload"></a>5 단계: 로컬 컴퓨터 toohello IPython 노트북 서버에서에서 기존 IPython 전자 필기장 업로드</span><span class="sxs-lookup"><span data-stu-id="74ebd-165"><a name="upload"></a>Step 5: Upload an existing IPython Notebook from a local machine toohello IPython Notebook server</span></span>
<span data-ttu-id="74ebd-166">IPython 노트북 사용자 tooupload 자신의 로컬 컴퓨터 toohello hello 가상 컴퓨터에서 IPython 노트북 서버에 기존 IPython 전자 필기장에 대 한는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-166">IPython Notebooks provide an easy way for users tooupload an existing IPython Notebook on their local machines toohello IPython Notebook server on hello virtual machines.</span></span> <span data-ttu-id="74ebd-167">Hello에 웹 브라우저에서 toohello IPython 노트북에 로그인 하면 클릭 **디렉터리** 해당 hello IPython 노트북 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-167">After you log on toohello IPython Notebook in a web browser, click into hello **directory** that hello IPython Notebook will be uploaded to.</span></span> <span data-ttu-id="74ebd-168">그런 다음 선택 하 여 IPython 노트북.ipynb 파일 tooupload hello hello에 로컬 컴퓨터에서 **파일 탐색기**를 끌어서 toohello IPython 노트북 디렉터리 hello 웹 브라우저에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-168">Then, select an IPython Notebook .ipynb file tooupload from hello local machine in hello **File Explorer**, and drag and drop it toohello IPython Notebook directory on hello web browser.</span></span> <span data-ttu-id="74ebd-169">Hello 클릭 **업로드** 단추 tooupload hello.ipynb 파일 toohello IPython 노트북 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-169">Click hello **Upload** button, tooupload hello .ipynb file toohello IPython Notebook server.</span></span> <span data-ttu-id="74ebd-170">이제 다른 사용자가 자신의 웹 브라우저에서 이 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-170">Other users can then start using it in from their web browsers.</span></span>

![작업 영역 만들기][22]

![작업 영역 만들기][23]

## <span data-ttu-id="74ebd-173"><a name="shutdown"></a>사용하지 않을 때 가상 컴퓨터 종료 및 할당 해제</span><span class="sxs-lookup"><span data-stu-id="74ebd-173"><a name="shutdown"></a>Shut down and de-allocate virtual machine when not in use</span></span>
<span data-ttu-id="74ebd-174">Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-174">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="74ebd-175">되 고 있지 tooensure toobe hello에가 가상 컴퓨터를 사용 하지 않는 경우 대금 청구를 **중지 (할당 취소)** 없으면에서 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-175">tooensure that you are not being billed when not using your virtual machine, it has toobe in hello **Stopped (Deallocated)** state when not in use.</span></span>

> [!NOTE]
> <span data-ttu-id="74ebd-176">Hello 가상 컴퓨터를 종료 하는 경우에서 hello VM (Windows 전원 옵션 사용), 내부 hello VM 중지 하지만 할당 된 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-176">If you shut down hello virtual machine from inside hello VM (using Windows power options), hello VM is stopped but remains allocated.</span></span> <span data-ttu-id="74ebd-177">tooensure toobe 대금 청구를 계속 하지 않으면 항상 hello에서 가상 컴퓨터를 중지 [Azure 클래식 포털](http://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-177">tooensure you do not continue toobe billed, always stop virtual machines from hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="74ebd-178">호출 하 여 hello Powershell 통해 VM을 중지할 수도 있습니다 **ShutdownRoleOperation** "PostShutdownAction"와 같은 너무 "StoppedDeallocated" 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-178">You can also stop hello VM through Powershell by calling **ShutdownRoleOperation** with "PostShutdownAction" equal too"StoppedDeallocated".</span></span>
> 
> 

<span data-ttu-id="74ebd-179">tooshut 한 hello 가상 컴퓨터 할당 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-179">tooshut down and deallocate hello virtual machine:</span></span>

1. <span data-ttu-id="74ebd-180">Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/) 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-180">Log in toohello [Azure classic portal](http://manage.windowsazure.com/) using your account.</span></span>  
2. <span data-ttu-id="74ebd-181">선택 **가상 컴퓨터** hello 왼쪽된 탐색 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-181">Select **VIRTUAL MACHINES** from hello left navigation bar.</span></span>
3. <span data-ttu-id="74ebd-182">가상 컴퓨터의 hello 목록에서 가상 컴퓨터 아니면 이동 toohello hello 이름을 클릭 **대시보드** 페이지.</span><span class="sxs-lookup"><span data-stu-id="74ebd-182">In hello list of virtual machines, click on hello name of your virtual machine then go toohello **DASHBOARD** page.</span></span>
4. <span data-ttu-id="74ebd-183">Hello hello 페이지의 아래쪽에 있는 클릭 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-183">At hello bottom of hello page, click **SHUTDOWN**.</span></span>

![VM 종료][15]

<span data-ttu-id="74ebd-185">hello 가상 컴퓨터를 할당 취소 되지만 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-185">hello virtual machine will be deallocated but not deleted.</span></span> <span data-ttu-id="74ebd-186">Hello Azure 클래식 포털에서에서 언제 든 지 가상 컴퓨터를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-186">You may restart your virtual machine at any time from hello Azure classic portal.</span></span>

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a><span data-ttu-id="74ebd-187">Azure VM은 준비 toouse: 다음 내용은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="74ebd-187">Your Azure VM is ready toouse: what's next?</span></span>
<span data-ttu-id="74ebd-188">가상 컴퓨터가 데이터 과학 연습에서 준비 toouse 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-188">Your virtual machine is now ready toouse in your data science exercises.</span></span> <span data-ttu-id="74ebd-189">hello 가상 컴퓨터를 Azure 기계 학습 및 hello 팀 데이터 과학 프로세스 hello 탐색 및 데이터의 처리에 대 한 IPython 노트북 서버와 함께에서 다른 작업으로 사용 하기 위해 준비 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-189">hello virtual machine is also ready for use as an IPython Notebook server for hello exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and hello Team Data Science Process.</span></span>

<span data-ttu-id="74ebd-190">hello hello에 매핑된 팀 데이터 과학 프로세스의에서 다음 단계를 hello [학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) HDInsight, 프로세스에 데이터를 이동 하 고 Azure 컴퓨터와 것이 있으면 hello 데이터 로부터 학습을 위한 준비 과정에서 샘플링 하는 단계를 포함할 수 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ebd-190">hello next steps in hello Team Data Science Process are mapped in hello [Learning Path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

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
