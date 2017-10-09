---
title: "Azure 역할과 함께 원격 데스크톱 aaaUsing | Microsoft Docs"
description: "Azure 역할과 함께 원격 데스크톱 사용"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="2b244-103">Azure 역할과 함께 원격 데스크톱 사용</span><span class="sxs-lookup"><span data-stu-id="2b244-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="2b244-104">Hello Azure SDK 및 원격 데스크톱 서비스를 사용 하 여 Azure 역할 및 Azure에서 호스트 되는 가상 컴퓨터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="2b244-105">Visual Studio에서 Azure 클라우드 서비스 프로젝트에서 원격 데스크톱 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="2b244-106">tooenable 원격 데스크톱 서비스, 하나 이상의 역할을 포함 하는 작업 중인 프로젝트를 만들고 tooAzure 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b244-107">문제 해결 또는 개발 목적으로만 Azure 역할에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="2b244-108">각 가상 컴퓨터의 목적은 hello toorun 하지 toorun Azure 응용 프로그램에서 특정 역할에 다른 클라이언트 응용 프로그램은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="2b244-109">Toouse Azure toohost 목적을 위해 사용할 수 있는 가상 컴퓨터를 원하는 경우 서버 탐색기에서 Azure 가상 컴퓨터에 액세스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b244-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="2b244-110">tooenable 및 Azure 역할에 대 한 원격 데스크톱 사용</span><span class="sxs-lookup"><span data-stu-id="2b244-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="2b244-111">솔루션 탐색기에서 클라우드 서비스 프로젝트에 대 한 hello 바로 가기 메뉴를 열고 선택한 후 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="2b244-112">hello **Azure 응용 프로그램 게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![클라우드 서비스 프로젝트에 대한 명령 게시](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="2b244-114">Hello 맨 아래에 **Microsoft Azure 게시 설정** 선택 hello hello 마법사의 페이지 **원격 데스크톱 사용** 모든 역할 확인란에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="2b244-115">hello **원격 데스크톱 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="2b244-116">Hello hello 맨 아래에 **원격 데스크톱 구성** 대화 상자에서 선택 하는 hello **기타 옵션** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="2b244-117">원격 데스크톱을 통해 연결 시 자격 증명 정보를 암호화할 수 있도록 인증서를 만들거나 선택할 수 있는 드롭다운 목록 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="2b244-118">Hello 드롭다운 목록에서 선택  **&lt;만들기 >**, 하거나 hello 목록에서 기존 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="2b244-119">기존 인증서를 선택 하면 hello 다음 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2b244-120">hello 필요한 인증서는 원격 데스크톱 연결에 대 한 다른 Azure 작업에 사용 하는 hello 인증서와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="2b244-121">hello 원격 액세스 인증서에 개인 키를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="2b244-122">hello **Create Certificate** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="2b244-123">Hello 새 인증서에 대 한 이름을 제공 하 고 hello를 눌러 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="2b244-124">새 인증서 hello hello 드롭다운 목록 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="2b244-125">Hello에 **원격 데스크톱 구성** 대화 상자에서 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="2b244-126">기존 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-126">You can’t use an existing account.</span></span> <span data-ttu-id="2b244-127">관리자 hello 새 계정에 대 한 hello 사용자 이름으로 지정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2b244-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2b244-128">Hello 암호 hello 복잡성 요구 사항을 충족 하지 않는 다음 toohello 암호 텍스트 상자 빨간색 아이콘이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="2b244-129">hello 암호는 대문자, 소문자 및 숫자 또는 기호에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="2b244-130">에 hello 계정이 만료 및 원격 데스크톱 연결이 차단 됩니다 이후 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="2b244-131">모든 필요한 정보를 hello 제공를 한 후 선택 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="2b244-132">원격 액세스 서비스를 사용 하도록 설정 하는 여러 설정이.cscfg 및.csdef 파일 toohello 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="2b244-133">Hello에 **Microsoft Azure 게시 설정** 마법사 hello 선택 **확인** 했으면 단추 toopublish 클라우드 서비스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="2b244-134">준비 toopublish 모르겠으면 선택 hello **취소** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="2b244-135">hello 구성 설정이 저장 되 고 나중에 클라우드 서비스를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="2b244-136">원격 데스크톱을 사용 하 여 tooan Azure 역할 연결</span><span class="sxs-lookup"><span data-stu-id="2b244-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="2b244-137">Azure에서 클라우드 서비스를 게시 한 후 Azure에서 호스팅되는 hello 가상 컴퓨터에 서버 탐색기 toolog 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="2b244-138">서버 탐색기에서 확장 hello **Azure** 노드를 확장 한 다음 클라우드 서비스와 해당 역할 toodisplay 인스턴스 목록 중 하나에 대 한 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="2b244-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="2b244-139">인스턴스 노드에 대 한 hello 바로 가기 메뉴를 열고 **를 사용 하 여 원격 데스크톱 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![원격 데스크톱을 통해 연결](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="2b244-141">Hello 사용자 이름 및 이전에 만든 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="2b244-142">이제 원격 세션에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b244-142">You are now logged into your remote session.</span></span>

