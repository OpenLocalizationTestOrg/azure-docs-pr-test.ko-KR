---
title: "aaaAzure 함수 런타임 설치 | Microsoft Docs"
description: "TooInstall은 Azure 함수 런타임 hello 하는 방법"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="9bfdd-103">Hello Azure 함수 런타임 미리 보기 설치</span><span class="sxs-lookup"><span data-stu-id="9bfdd-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="9bfdd-104">Tooinstall hello Azure 함수 런타임 미리 보기를 원하는 경우 이러한 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="9bfdd-105">컴퓨터 전달 hello 최소 요구 사항을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="9bfdd-106">Hello 다운로드 [Azure 함수 런타임 Preview 설치 관리자](https://aka.ms/azafr)합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="9bfdd-107">Hello Azure 함수 런타임 미리 보기 설치</span><span class="sxs-lookup"><span data-stu-id="9bfdd-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="9bfdd-108">Hello Azure 함수 런타임 미리 보기의 전체 hello 구성</span><span class="sxs-lookup"><span data-stu-id="9bfdd-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bfdd-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9bfdd-109">Prerequisites</span></span>

<span data-ttu-id="9bfdd-110">Hello Azure 함수 런타임 미리 보기를 설치 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="9bfdd-111">Microsoft Windows Server 2016 또는 Microsoft Windows 10 작성자 업데이트(Professional 또는 Enterprise Edition)를 실행하는 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9bfdd-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="9bfdd-112">네트워크 내에서 실행되는 SQL Server 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="9bfdd-113">최소 버전 요구 사항은 SQL Server Express입니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="9bfdd-114">Hello Azure 함수 런타임 미리 보기 설치</span><span class="sxs-lookup"><span data-stu-id="9bfdd-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="9bfdd-115">hello Azure 함수 런타임 preview 설치 관리자 hello Azure 함수 런타임 미리 보기 관리 및 작업자 역할의 hello 설치 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="9bfdd-116">가능한 tooinstall hello 관리 되며 작업자 역할 hello에 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="9bfdd-117">그러나 다른 함수를 추가 하면 배포한 toobe 수 tooscale 추가 컴퓨터에 더 많은 작업자 역할에 여러 worker 함수.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="9bfdd-118">Hello에 hello 관리 및 작업자 역할을 설치 동일한 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9bfdd-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="9bfdd-119">Hello Azure 함수 런타임 Preview 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions 런타임 미리 보기 설치 관리자][1]

1. <span data-ttu-id="9bfdd-121">**다음을 클릭** hello 설치 관리자의 첫 번째 단계 hello 지난 사전</span><span class="sxs-lookup"><span data-stu-id="9bfdd-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="9bfdd-122">Hello hello 약관을 읽은 후 **EULA**, **hello 확인란** tooaccept hello 용어 및 **다음 클릭** tooadvance 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="9bfdd-123">이 컴퓨터에 tooinstall 원하는 선택 hello 역할 이제 **함수 관리 역할** 및/또는 **함수 작업자 역할** 및 **"다음" 클릭**</span><span class="sxs-lookup"><span data-stu-id="9bfdd-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions 런타임 미리 보기 설치 관리자 - 역할 선택][3]

    > [!NOTE]
    > <span data-ttu-id="9bfdd-125">Hello를 설치할 수 있습니다 **함수 작업자 역할** 다른 많은 컴퓨터 toodo에서, 다음이 지침에 따라 한만 선택 **함수 작업자 역할** hello 설치 관리자에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="9bfdd-126">**다음을 클릭** toohave hello **Azure 함수에 대 한 런타임 설치 관리자** 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="9bfdd-127">전체 hello 설치 관리자가 hello 시작 되 면 **Azure 함수 런타임 구성 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions 런타임 미리 보기 설치 관리자 완료][5]

    > [!NOTE]
    > <span data-ttu-id="9bfdd-129">에 설치 하는 경우 **Windows 10** 및 hello **컨테이너** 기능이 활성화 되지 않은 이전에, hello **Azure 함수 런타임** 설치 관리자 묻는 tooreboot 컴퓨터 toocomplete hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="9bfdd-130">Hello Azure 함수 런타임 구성</span><span class="sxs-lookup"><span data-stu-id="9bfdd-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="9bfdd-131">toocomplete hello Azure 함수 런타임 설치 hello 구성을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="9bfdd-132">hello **Azure 함수 런타임 구성 도구** 컴퓨터에 설치 된 역할을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure Functions 런타임 미리 보기 구성 도구][6]

1. <span data-ttu-id="9bfdd-134">Hello 클릭 **데이터베이스** 탭을 hello 입력 **SQL Server 인스턴스에 대 한 연결 세부 정보** 및 **적용을 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="9bfdd-135">이 순서 toohello Azure 함수 런타임 toocreate 데이터베이스 toosupport hello 런타임 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Azure Functions 런타임 미리 보기 데이터베이스 구성][7]

1. <span data-ttu-id="9bfdd-137">Hello 클릭 **자격 증명** 탭 합니다.  이 화면에서 모든 Azure Functions를 호스트하기 위해 FileShare에서 사용할 2개의 새 자격 증명을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="9bfdd-138">**사용자 이름 및 암호 지정** hello에 대 한 조합을 **파일 공유 소유자** 및 hello에 대 한 **파일 공유 사용자** 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Azure Functions 런타임 미리 보기 자격 증명][8]

1. <span data-ttu-id="9bfdd-140">Hello 클릭 **파일 공유** 탭 합니다.  이 화면에서의 hello hello 세부 정보를 지정 해야 **파일 공유 위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="9bfdd-141">이 위치가 자동으로 생성될 수도 있고 기존 파일 공유를 사용하고 **적용**을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="9bfdd-142">새 파일 공유 위치를 선택 하는 경우에 hello Azure 함수 런타임 하 여 사용에 대 한 디렉터리를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Azure Functions 런타임 미리 보기 파일 공유][9]

1. <span data-ttu-id="9bfdd-144">Hello 클릭 **IIS** 탭 합니다.  이 탭에는 Azure 함수 런타임 설치 만듭니다 해당 hello IIS에서 hello 웹 사이트의 hello 세부 정보 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="9bfdd-145">**적용을 클릭** toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-145">**Click Apply** toocomplete.</span></span>

    ![Azure Functions 런타임 미리 보기 IIS][10]

1. <span data-ttu-id="9bfdd-147">Hello 클릭 **서비스** 탭 합니다.  이 탭 Azure 함수 런타임 설치에서 hello 서비스의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfdd-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="9bfdd-148">초기 구성 hello after **Azure 함수 호스트 정품 인증 서비스** 클릭을 실행 하지 않는 **서비스 시작**</span><span class="sxs-lookup"><span data-stu-id="9bfdd-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure Functions 런타임 미리 보기 구성 완료][11]

1. <span data-ttu-id="9bfdd-150">마지막으로 toohello 찾아보기 **Azure 함수 런타임 포털** 으로`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="9bfdd-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Azure Functions 런타임 미리 보기 포털][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png