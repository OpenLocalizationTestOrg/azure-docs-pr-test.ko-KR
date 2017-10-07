---
title: "ie GPO를 사용 하 여 Azure 액세스 패널 확장이 aaaDeploy | Microsoft Docs"
description: "어떻게 toouse 정책 toodeploy hello Internet Explorer 추가 기능 hello My Apps 포털에 대 한 그룹입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="28ce2-103">그룹 정책을 사용 하 여 Internet Explorer에 대 한 tooDeploy 액세스 패널 확장이 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="28ce2-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="28ce2-104">이 자습서에서는 어떻게 toouse 그룹 정책 tooremotely hello 액세스 패널에 확장을 설치 Internet Explorer에 대 한 사용자의 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="28ce2-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="28ce2-105">이 확장은 toosign를 사용 하 여 구성 된 앱에 필요한 Internet Explorer 사용자에 대 한 필요한 [암호 기반 single sign on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="28ce2-106">Admins이이 확장의 hello 배포를 자동화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="28ce2-107">그렇지 않으면 사용자 toodownload가 확장 및 설치 hello 자체 발생 하기 쉬운 toouser 오류가 발생 하 고 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="28ce2-108">이 자습서에서는 그룹 정책을 사용하여 소프트웨어 배포를 자동화하는 한 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="28ce2-109">그룹 정책에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="28ce2-110">액세스 패널 확장 hello는 가능 [크롬](https://go.microsoft.com/fwLink/?LinkID=311859) 및 [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), 둘 중 필요한 관리자 권한을 tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28ce2-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="28ce2-111">Prerequisites</span></span>
* <span data-ttu-id="28ce2-112">설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="28ce2-113">Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="28ce2-114">기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="28ce2-115">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="28ce2-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="28ce2-116">1 단계: hello 배포 지점 만들기</span><span class="sxs-lookup"><span data-stu-id="28ce2-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="28ce2-117">첫째, hello 설치 관리자 패키지 tooremotely 설치 hello 확장에 가져오려는 hello 컴퓨터에서 액세스할 수 있는 네트워크 위치에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="28ce2-118">toodo이를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="28ce2-119">관리자 권한으로 toohello 서버에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="28ce2-120">Hello에 **서버 관리자** 창 너무 이동**파일 및 저장소 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="28ce2-122">Toohello 이동 **공유** 탭 합니다. 그런 다음 **태스크** > **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="28ce2-124">전체 hello **새 공유 마법사** 및 설정 권한 tooensure 사용자의 컴퓨터에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="28ce2-125">공유에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="28ce2-126">Microsoft Windows Installer 패키지 (.msi 파일)를 수행 하는 hello 다운로드: [액세스 패널 Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="28ce2-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="28ce2-127">Hello hello 공유에서 설치 관리자 패키지 tooa 원하는 위치에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Hello.msi 파일 toohello 공유에 복사 합니다.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="28ce2-129">클라이언트 컴퓨터 수 tooaccess hello 공유에서 설치 관리자 패키지를 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="28ce2-130">2 단계: hello 그룹 정책 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="28ce2-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="28ce2-131">Active Directory 도메인 서비스 (AD DS) 설치를 호스팅하는 toohello 서버에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="28ce2-132">Hello 서버 관리자에서에서 이동 너무**도구** > **그룹 정책 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![TooTools 이동 > 그룹 정책 관리](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="28ce2-134">Hello hello의 왼쪽된 창에서 **그룹 정책 관리** 창 조직 구성 단위 (OU) 계층 구조를 확인 하 고는 범위에서 원하는 tooapply hello 그룹 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="28ce2-135">예를 들어, 테스트를 위해 작은 OU toodeploy tooa toopick 몇몇 사용자가 결정할 수 있습니다 또는 최상위 OU toodeploy tooyour 전체 조직을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28ce2-136">Toocreate 같은 조직 단위 (Ou)를 편집 하거나, 백 toohello 서버 관리자를 전환 하 고 이동 너무**도구** > **Active Directory 사용자 및 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="28ce2-137">OU를 선택한 후에 마우스 오른쪽 단추로 클릭하고 **이 도메인에서 GPO를 만들고 여기에 연결...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![새 GPO 만들기](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="28ce2-139">Hello에 **새 GPO** , 프롬프트에 대 한 이름 입력 hello 새 그룹 정책 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Hello 새 GPO 이름](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="28ce2-141">마우스 오른쪽 단추로 클릭 하 고 사용자가 만든 선택 그룹 정책 개체 hello **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Hello 새 GPO를 편집 합니다.](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="28ce2-143">3 단계: 할당 hello 설치 패키지</span><span class="sxs-lookup"><span data-stu-id="28ce2-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="28ce2-144">에 따라 toodeploy hello 확장 하는지 여부를 결정 **컴퓨터 구성** 또는 **사용자 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="28ce2-145">사용 하는 경우 [컴퓨터 구성](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello 확장 프로그램에 관계 없이 사용자가 로그온 tooit hello 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="28ce2-146">와 [사용자 구성](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), 사용자가 로그온 하는 컴퓨터에 관계 없이 설치 하는 hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="28ce2-147">Hello hello의 왼쪽된 창에서 **그룹 정책 관리 편집기** hello 폴더 경로, 선택한 구성의 유형에 따라 다음의 이동 tooeither 창:</span><span class="sxs-lookup"><span data-stu-id="28ce2-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="28ce2-148">**소프트웨어 설치**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **패키지...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![새 소프트웨어 설치 패키지 만들기](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="28ce2-150">Hello 설치 관리자 패키지를 포함 하는 공유 폴더를 이동 toohello [1 단계: hello 배포 지점 만들기](#step-1-create-the-distribution-point)hello.msi 파일을 선택 하 고 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="28ce2-151">Hello 공유를 동일한 서버에 있는 경우 hello.msi를 액세스 하는 hello 로컬 파일 경로 대신 hello 네트워크 파일 경로 통해 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Hello 공유 폴더에서 hello 설치 패키지를 선택 합니다.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="28ce2-153">Hello에 **소프트웨어 배포** 프롬프트를 선택 **Assigned** 배포 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="28ce2-154">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-154">Then click **OK**.</span></span>
   
    ![할당됨을 선택하고 확인을 클릭합니다.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="28ce2-156">배포 된 toohello 선택한 OU hello 확장이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="28ce2-157">그룹 정책 소프트웨어 설치에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="28ce2-158">4 단계: 자동 사용 hello Internet Explorer에 대 한 확장</span><span class="sxs-lookup"><span data-stu-id="28ce2-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="28ce2-159">또한 Internet Explorer에 대 한 모든 확장 toorunning hello 설치 관리자 사용 하려면 먼저 명시적으로 활성화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="28ce2-160">Tooenable 아래 hello 단계 수행 hello 그룹 정책을 사용 하 여 액세스 패널 확장:</span><span class="sxs-lookup"><span data-stu-id="28ce2-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="28ce2-161">Hello에 **그룹 정책 관리 편집기** 창에서 선택한 구성의 유형에 따라 경로 따라 hello의 이동 tooeither [3 단계: 할당 hello 설치 패키지](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="28ce2-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="28ce2-162">**추가 기능 목록**을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="28ce2-163">![추가 기능 목록을 편집합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="28ce2-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="28ce2-164">Hello에 **추가 기능 목록** 창에서 **Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="28ce2-165">그런 다음 hello **옵션** 섹션에서 클릭 **표시...** .</span><span class="sxs-lookup"><span data-stu-id="28ce2-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![사용을 클릭한 다음 표시...를 클릭합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="28ce2-167">Hello에 **내용 표시** 창의 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="28ce2-168">Hello 첫 번째 열에 대 한 (hello **값 이름** 필드), 복사 및 붙여넣기 hello 다음 클래스 ID:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="28ce2-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="28ce2-169">Hello 두 번째 열에 대 한 (hello **값** 필드), hello 다음 값 입력:`1`</span><span class="sxs-lookup"><span data-stu-id="28ce2-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="28ce2-170">클릭 **확인** tooclose hello **내용 표시** 창.</span><span class="sxs-lookup"><span data-stu-id="28ce2-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Hello 값 위에 지정 된 대로 입력 합니다.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="28ce2-172">클릭 **확인** tooapply은 변경 내용 및 닫기 hello **추가 기능 목록** 창.</span><span class="sxs-lookup"><span data-stu-id="28ce2-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="28ce2-173">hello 확장 이제 설정할지 hello 컴퓨터 선택 hello에 대 한 OU입니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="28ce2-174">그룹 정책 tooenable 사용에 대 한 자세한 내용을 보거나 Internet Explorer 추가 기능을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="28ce2-175">5단계(선택 사항): “암호 저장" 프롬프트 비활성화</span><span class="sxs-lookup"><span data-stu-id="28ce2-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="28ce2-176">사용자가 로그인 toowebsites hello 액세스 패널 확장을 사용 하 여, Internet Explorer 수 표시 hello 다음 묻는 "보 시겠습니까 toostore 암호?" 라는</span><span class="sxs-lookup"><span data-stu-id="28ce2-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="28ce2-177">사용자가이 프롬프트를 보지 못하도록 tooprevent을 원할 경우 이사 암호에서 자동 완성 tooprevent 아래 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="28ce2-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="28ce2-178">Hello에 **그룹 정책 관리 편집기** 창, 이동 toohello 경로 아래에 나열 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="28ce2-179">이 구성 설정은 **사용자 구성**에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="28ce2-180">명명 된 hello 설정의 찾을 **hello forms에 사용자 이름 및 암호에 대 한 자동 완성 기능을 켤**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28ce2-181">이전 버전의 Active Directory hello 이름으로이 설정을 나열할 수 있습니다 **자동 완성 toosave 암호를 허용 하지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="28ce2-182">해당 설정에 대 한 hello 구성 hello 설정을이 자습서에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![사용자 설정에서이 대 한 toolook를 기억 합니다.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="28ce2-184">Hello 설정 위에 마우스 오른쪽 단추로 클릭 하 고 선택 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="28ce2-185">이라는 hello 창에서 **hello forms에 사용자 이름 및 암호에 대 한 자동 완성 기능을 설정**선택, **비활성화 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![사용 안함 선택](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="28ce2-187">클릭 **확인** tooapply 이러한 변경 내용 및 닫기 hello 창.</span><span class="sxs-lookup"><span data-stu-id="28ce2-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="28ce2-188">사용자는 더 이상 수 toostore 자격 증명 수 또는 자동 완성 tooaccess 이전에 저장 된 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="28ce2-189">그러나이 정책에서 허용 사용자 toocontinue toouse 검색 필드 등의 양식 필드의 다른 형식에 대 한 자동 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="28ce2-190">이 정책은 하는 사용자가 선택한 toostore 일부 자격 증명 후이 정책을 사용 하는 경우 *하지* 이미 저장 되어 있는 hello 자격 증명의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="28ce2-191">6 단계: 테스트 배포 문자열</span><span class="sxs-lookup"><span data-stu-id="28ce2-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="28ce2-192">Hello 확장 배포에 성공 하면 tooverify 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="28ce2-193">사용 하 여 배포한 경우 **컴퓨터 구성**, toohello에서 선택한 OU에 속하는 클라이언트 컴퓨터에 로그인 [2 단계: hello 그룹 정책 개체 만들기](#step-2-create-the-group-policy-object)합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="28ce2-194">사용 하 여 배포한 경우 **사용자 구성**에 있는지 toosign toothat OU에 속한 사용자로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="28ce2-195">몇 가지 기호 걸릴 수 있습니다이 컴퓨터 toofully 업데이트 hello 그룹 정책에 대 한 기능을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="28ce2-196">열기 tooforce hello 업데이트는 **명령 프롬프트** 창과 다음 명령이 실행된 hello:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="28ce2-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="28ce2-197">Hello 설치 tootake 위 hello 컴퓨터를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="28ce2-198">부팅 시 hello 확장 하는 동안 일반적인 설치 보다 훨씬 더 많은 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="28ce2-199">다시 시작한 후 **Internet Explorer**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="28ce2-200">Hello hello 창의 오른쪽 위 모서리를 클릭 **도구** (hello 기어 아이콘)을 선택한 후 **추가 기능을 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="28ce2-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![TooTools 이동 > 추가 기능 관리](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="28ce2-202">Hello에 **추가 기능 관리** 창 해당 hello 확인 **액세스 패널 확장** 가 설치 되어 있는지 해당 **상태** 너무 설정 된**사용**.</span><span class="sxs-lookup"><span data-stu-id="28ce2-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![액세스 패널 확장이 설치 및 활성화 되어 해당 hello를 확인 합니다.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="28ce2-204">관련 문서</span><span class="sxs-lookup"><span data-stu-id="28ce2-204">Related Articles</span></span>
* [<span data-ttu-id="28ce2-205">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="28ce2-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="28ce2-206">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="28ce2-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="28ce2-207">Internet Explorer에 대 한 hello 액세스 패널 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="28ce2-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

