---
title: "GPO를 사용하여 IE에 대한 Azure 액세스 패널 확장 배포 | Microsoft Docs"
description: "그룹 정책을 사용하여 My Apps 포털용 Internet Explorer 추가 기능을 배포하는 방법"
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
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="0ef7c-103">그룹 정책을 사용하여 Internet Explorer용 액세스 패널 확장을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="0ef7c-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="0ef7c-104">이 자습서에서는 그룹 정책을 사용하여 사용자의 컴퓨터에 Internet Explorer용 액세스 패널 확장을 원격 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="0ef7c-105">이 확장은 [암호 기반 Single Sign-On](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)을 사용하여 구성된 앱에 로그인하는 Internet Explorer 사용자에게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="0ef7c-106">관리자는 이 확장의 배포를 자동화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="0ef7c-107">그렇지 않은 경우 사용자가 직접 확장을 다운로드하여 설치해야 하기 때문에 사용자 오류가 발생하기 쉽고 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="0ef7c-108">이 자습서에서는 그룹 정책을 사용하여 소프트웨어 배포를 자동화하는 한 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="0ef7c-109">그룹 정책에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="0ef7c-110">액세스 패널 확장은 [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) 및 [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998)에도 사용할 수 있으며 설치에 관리자 권한이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ef7c-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0ef7c-111">Prerequisites</span></span>
* <span data-ttu-id="0ef7c-112">[Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)를 설정하고, 사용자 컴퓨터를 도메인에 가입시킨 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="0ef7c-113">그룹 정책 개체(GPO)를 편집하는 "설정 편집" 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="0ef7c-114">기본적으로 도메인 관리자, 엔터프라이즈 관리자 및 그룹 정책 작성자/소유자 보안 그룹의 멤버에게 이 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="0ef7c-115">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="0ef7c-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="0ef7c-116">1단계: 배포 지점 만들기</span><span class="sxs-lookup"><span data-stu-id="0ef7c-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="0ef7c-117">먼저 원격으로 확장을 설치할 컴퓨터에서 액세스할 수 있는 네트워크 위치에 설치 관리자 패키지를 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="0ef7c-118">이렇게 하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="0ef7c-119">관리자 권한으로 서버에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="0ef7c-120">**서버 관리자** 창에서 **파일 및 저장소 서비스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="0ef7c-122">**공유** 탭으로 이동합니다. 그런 다음 **태스크** > **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="0ef7c-124">**새 공유 마법사** 를 완료하고 사용자의 컴퓨터에서 액세스할 수 있게 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="0ef7c-125">공유에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="0ef7c-126">Windows Installer 패키지(.msi 파일)[Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="0ef7c-127">설치 관리자 패키지를 공유의 원하는 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![.msi 파일을 공유에 복사합니다.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="0ef7c-129">클라이언트 컴퓨터가 공유에서 설치 관리자 패키지에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="0ef7c-130">2단계: 그룹 정책 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="0ef7c-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="0ef7c-131">Active Directory 도메인 서비스(ADDS) 설치를 호스팅하는 서버에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="0ef7c-132">서버 관리자에서 **도구** > **그룹 정책 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![도구 > 그룹 정책 관리로 이동](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="0ef7c-134">**그룹 정책 관리** 창의 왼쪽 창에서 조직 구성 단위(OU) 계층 구조를 확인하고 그룹 정책을 적용할 범위를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="0ef7c-135">예를 들어, 테스트를 위해 소수의 사용자에게 소규모 OU를 배포하거나, 전 조직에 배포하기 위해 최상위 OU를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ef7c-136">조직 단위(OU)를 만들거나 편집하려면 서버 관리자로 다시 전환하여 **도구** > **Active Directory 사용자 및 컴퓨터**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="0ef7c-137">OU를 선택한 후에 마우스 오른쪽 단추로 클릭하고 **이 도메인에서 GPO를 만들고 여기에 연결...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![새 GPO 만들기](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="0ef7c-139">**새 GPO** 프롬프트에 새 그룹 정책 개체의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![새 GPO 이름 지정 ](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="0ef7c-141">만든 그룹 정책 개체를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![새 GPO 편집](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="0ef7c-143">3단계: 설치 패키지를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="0ef7c-144">확장을 **컴퓨터 구성** 또는 **사용자 구성**을 기준으로 배포할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="0ef7c-145">[컴퓨터 구성](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx)을 사용할 경우 사용자가 로그인했는지와 관계없이 컴퓨터에 확장이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="0ef7c-146">[사용자 구성](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx)의 경우 사용자가 로그온한 컴퓨터인지와 관계없이 사용자에게 확장이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="0ef7c-147">**그룹 정책 관리 편집기** 창의 왼쪽에서 선택한 구성의 유형에 따라 다음 폴더 경로 중 하나로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="0ef7c-148">**소프트웨어 설치**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **패키지...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![새 소프트웨어 설치 패키지 만들기](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="0ef7c-150">[1단계: 배포 지점 만들기](#step-1-create-the-distribution-point)에서 만든 설치 관리자 패키지가 들어 있는 공유  폴더로 이동하고 .msi 파일을 선택한 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0ef7c-151">공유가 같은 서버에 있는 경우 로컬 파일 경로가 아닌 네트워크 파일 경로를 통해 .msi에 액세스하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![공유 폴더에서 설치 패키지를 선택합니다.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="0ef7c-153">**소프트웨어 배포** 프롬프트에서 배포 방법으로 **할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="0ef7c-154">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-154">Then click **OK**.</span></span>
   
    ![할당됨을 선택하고 확인을 클릭합니다.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="0ef7c-156">이제 확장이 선택한OU에 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="0ef7c-157">그룹 정책 소프트웨어 설치에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="0ef7c-158">4단계: Internet Explorer용 확장 자동 활성화</span><span class="sxs-lookup"><span data-stu-id="0ef7c-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="0ef7c-159">설치 프로그램을 실행하는 것 외에도 모든 Internet Explorer용 확장을 명시적으로 활성화해야 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="0ef7c-160">다음 단계에 따라 그룹 정책을 사용하여 액세스 패널 확장을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="0ef7c-161">**그룹 정책 관리 편집기** 창에서, [3단계: 설치 패키지](#step-3-assign-the-installation-package)에서 선택한 구성 유형에 따라 다음 폴더 경로 중 하나로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="0ef7c-162">**추가 기능 목록**을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="0ef7c-163">![추가 기능 목록을 편집합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="0ef7c-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="0ef7c-164">**추가 기능 목록** 창에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="0ef7c-165">그런 다음 **옵션** 섹션에서 **표시...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![사용을 클릭한 다음 표시...를 클릭합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="0ef7c-167">**내용 표시** 창에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="0ef7c-168">첫번째 열(**값 이름** 필드)에 클래스 ID `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`를 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="0ef7c-169">두번째 열(**값** 필드)에 `1` 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="0ef7c-170">**확인**을 클릭하여 **내용 표시** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![위에서 지정한 대로 값을 입력합니다.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="0ef7c-172">**확인**을 클릭하여 변경 내용을 저장하고 **추가 기능 목록** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="0ef7c-173">이제 선택한 OU의 컴퓨터에서 확장이 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="0ef7c-174">그룹 정책을 사용하여 Internet Explorer 추가 기능을 활성화 또는 비활성화하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="0ef7c-175">5단계(선택 사항): “암호 저장" 프롬프트 비활성화</span><span class="sxs-lookup"><span data-stu-id="0ef7c-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="0ef7c-176">사용자가 액세스 패널 확장을 사용하여 웹 사이트에 로그인하면 Internet Explorer에 “암호를 저장하시겠습니까?”라고 묻는 프롬프트가 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="0ef7c-177">사용자에게 이 프롬프트가 표시되지 않도록 하려면 아래 단계에 따라서 자동 완성이 암호를 저장하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="0ef7c-178">**그룹 정책 관리 편집기** 창에서 아래 나열된 경로로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="0ef7c-179">이 구성 설정은 **사용자 구성**에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="0ef7c-180">이름이 **양식의 사용자 이름과 암호에 자동 완성 기능 사용**인 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ef7c-181">이전 버전의 Active Directory에는 이 설정의 이름이 **Do not allow auto-complete to save passwords**(자동 완성이 암호를 저장하도록 허용 안 함)으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="0ef7c-182">해당 설정에 대한 구성은 이 자습서에 설명되어 있는 설정마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![사용자 설정에서 이 내용을 찾아야 합니다.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="0ef7c-184">위 설정을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="0ef7c-185">**양식의 사용자 이름과 암호에 자동 완성 기능 사용** 창에서 **사용 안함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![사용 안함 선택](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="0ef7c-187">**확인** 을 클릭하여 변경 사항을 적용하고 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="0ef7c-188">사용자는 더 이상 자신의 자격 증명을 저장하거나 자동 완성을 사용하여 이전에 저장된 자격 증명에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="0ef7c-189">하지만 이 정책은 검색 필드와 같은 다른 유형의 양식 필드에는 자동 완성 기능을 계속 사용하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="0ef7c-190">사용자가 자격 증명을 저장하도록 선택한 후에 이 정책을 사용하도록 설정하면, 이 정책은 이미 저장된 자격 증명을 지우지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="0ef7c-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="0ef7c-191">6단계: 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="0ef7c-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="0ef7c-192">다음 단계에 따라 확장 배포가 성공적으로 이루어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="0ef7c-193">**컴퓨터 구성**을 사용하여 배포한 경우 [2단계: 그룹 정책 개체 만들기](#step-2-create-the-group-policy-object)에서 선택한 OU에 속한 클라이언트 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="0ef7c-194">**사용자 구성**을 사용하여 배포한 경우 해당 OU에 속한 사용자로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="0ef7c-195">그룹 정책 변경 내용이 해당 컴퓨터를 완전히 업데이트하기 위해 몇 번의 로그인이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="0ef7c-196">업데이트를 강제 실행하려면 **명령 프롬프트** 창을 열고 터미널 창을 열고 `gpupdate /force` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="0ef7c-197">설치를 적용하려면 컴퓨터를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="0ef7c-198">확장 설치 중에는 부팅 시간이 상대적으로 더 오래 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="0ef7c-199">다시 시작한 후 **Internet Explorer**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="0ef7c-200">창의 오른쪽 위 모퉁이에서 **도구**(기어 아이콘)를 클릭한 다음 **추가 기능 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![도구 > 추가 기능 관리로 이동](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="0ef7c-202">**추가 기능 관리** 창에서 **액세스 패널 확장**이 설치되었으며 그 **상태**가 **사용**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![액세스 패널 확장이 설치되었으며 활성화되었는지 확인합니다.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="0ef7c-204">관련 문서</span><span class="sxs-lookup"><span data-stu-id="0ef7c-204">Related Articles</span></span>
* [<span data-ttu-id="0ef7c-205">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="0ef7c-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0ef7c-206">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0ef7c-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0ef7c-207">Internet Explorer용 액세스 패널 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0ef7c-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

