---
title: "Azure RemoteApp용 사용자 지정 템플릿 이미지를 만드는 방법 | Microsoft 문서"
description: "Azure RemoteApp용 사용자 지정 템플릿 이미지를 만드는 방법에 대해 알아봅니다. 하이브리드 또는 클라우드 컬렉션에서 이 템플릿을 사용할 수 있습니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f529a5526f266c7dbac3c719b244d05ab7705941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-custom-template-image-for-azure-remoteapp"></a><span data-ttu-id="f2764-104">Azure RemoteApp용 사용자 지정 템플릿 이미지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f2764-104">How to create a custom template image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f2764-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f2764-106">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f2764-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f2764-107">Azure RemoteApp은 Windows Server 2012 R2 템플릿 이미지를 사용하여 사용자와 공유할 모든 프로그램을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-107">Azure RemoteApp uses a Windows Server 2012 R2 template image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="f2764-108">사용자 지정 RemoteApp 템플릿 이미지를 만들려면 기존 이미지에서 시작하거나 새 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-108">To create a custom RemoteApp template image, you can start with an existing image or create a new one.</span></span> 

> [!TIP]
> <span data-ttu-id="f2764-109">Azure VM에서 이미지를 만들 수 있다는 것을 알고 있나요?</span><span class="sxs-lookup"><span data-stu-id="f2764-109">Did you know you can create an image from an Azure VM?</span></span> <span data-ttu-id="f2764-110">이 방법을 사용하면 이미지를 가져오는 데 소요되는 시간을 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-110">True story, and it cuts down on the amount of time it takes to import the image.</span></span> <span data-ttu-id="f2764-111">[여기](remoteapp-image-on-azurevm.md)서 단계를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f2764-111">Check out the steps [here](remoteapp-image-on-azurevm.md).</span></span>
> 
> 

<span data-ttu-id="f2764-112">Azure RemoteApp과 사용하기 위해 업로드할 수 있는 이미지의 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-112">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="f2764-113">이미지 크기는 MB 단위의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-113">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="f2764-114">크기가 정확한 배수가 아닌 이미지는 업로드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-114">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="f2764-115">이미지 크기는 127GB 이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-115">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="f2764-116">VHD 파일에 있어야 합니다. VHDX 파일 [Hyper-V 가상 하드 드라이브]은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-116">It must be on a VHD file (VHDX files [Hyper-V virtual hard drives] are not currently supported).</span></span>
* <span data-ttu-id="f2764-117">VHD는 세대 2 가상 컴퓨터가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-117">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="f2764-118">VHD는 고정 크기이거나 동적으로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-118">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="f2764-119">고정 크기의 VHD 파일보다 Azure에 업로드하는 시간이 짧으므로 동적으로 확장되는 VHD가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-119">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="f2764-120">디스크는 MBR(마스터 부트 레코드) 파티션 스타일을 사용하여 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-120">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="f2764-121">GPT(GUID 파티션 테이블) 파티션 스타일은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-121">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="f2764-122">VHD는 Windows Server 2012 R2의 단일 설치를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-122">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="f2764-123">여러 볼륨을 포함할 수 있지만 한 볼륨만 Windows의 설치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-123">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="f2764-124">RDSH(원격 데스크톱 세션 호스트) 역할 및 데스크톱 경험 기능을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-124">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="f2764-125">원격 데스크톱 연결 브로커 역할은 설치하면 *안 됩니다* .</span><span class="sxs-lookup"><span data-stu-id="f2764-125">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="f2764-126">EFS(파일 시스템 암호화)를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-126">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="f2764-127">이미지는 **/oobe /generalize /shutdown** 매개 변수를 사용하여 SYSPREPed가 되어야 합니다. **/mode:vm** 매개 변수는 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f2764-127">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="f2764-128">스냅숏 체인으로부터의 VHD 업로드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-128">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="f2764-129">**시작하기 전에**</span><span class="sxs-lookup"><span data-stu-id="f2764-129">**Before you begin**</span></span>

<span data-ttu-id="f2764-130">서비스를 만들기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-130">You need to do the following before creating the service:</span></span>

* <span data-ttu-id="f2764-131">[등록](https://azure.microsoft.com/services/remoteapp/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-131">[Sign up](https://azure.microsoft.com/services/remoteapp/) for RemoteApp.</span></span>
* <span data-ttu-id="f2764-132">RemoteApp 서비스 계정으로 사용할 Active Directory의 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-132">Create a user account in Active Directory to use as the RemoteApp service account.</span></span> <span data-ttu-id="f2764-133">이 계정의 권한은 도메인에 컴퓨터를 가입시킬 수 있는 권한만으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-133">Restrict the permissions for this account so that it can only join machines to the domain.</span></span> <span data-ttu-id="f2764-134">자세한 내용은 [RemoteApp에 대해 Azure Active Directory 구성](remoteapp-ad.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2764-134">See [Configure Azure Active Directory for RemoteApp](remoteapp-ad.md) for more information.</span></span>
* <span data-ttu-id="f2764-135">온-프레미스 네트워크에 대한 정보 수집: IP 주소 정보 및 VPN 장치 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-135">Gather information about your on-premises network: IP address information and VPN device details.</span></span>
* <span data-ttu-id="f2764-136">[Azure PowerShell](/powershell/azure/overview) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-136">Install the [Azure PowerShell](/powershell/azure/overview) module.</span></span>
* <span data-ttu-id="f2764-137">액세스 권한을 부여할 사용자에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-137">Gather information about the users that you want to grant access to.</span></span> <span data-ttu-id="f2764-138">이 정보는 사용자의 Microsoft 계정 정보나 Active Directory 작업 계정 정보가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-138">This can be either Microsoft account information or Active Directory work account information for users.</span></span>

## <a name="create-a-template-image"></a><span data-ttu-id="f2764-139">템플릿 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="f2764-139">Create a template image</span></span>
<span data-ttu-id="f2764-140">다음은 처음부터 새 템플릿 이미지를 만드는 요약된 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-140">These are the high level steps to create a new template image from scratch:</span></span>

1. <span data-ttu-id="f2764-141">Windows Server 2012 R2 Update DVD 또는 ISO 이미지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-141">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="f2764-142">VHD 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-142">Create a VHD file.</span></span>
3. <span data-ttu-id="f2764-143">Windows Server 2012 R2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-143">Install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="f2764-144">RDSH(원격 데스크톱 세션 호스트) 역할 및 데스크톱 경험 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-144">Install the Remote Desktop Session Host (RDSH) role and the Desktop Experience feature.</span></span>
5. <span data-ttu-id="f2764-145">응용 프로그램에 필요한 추가 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-145">Install additional features required by your applications.</span></span>
6. <span data-ttu-id="f2764-146">응용 프로그램을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-146">Install and configure your applications.</span></span> <span data-ttu-id="f2764-147">앱을 더 쉽게 공유하려면 **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs에 있는 이미지의 **시작** 메뉴에 공유할 앱이나 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-147">To make sharing apps easier, add any apps or programs that you want to share to the **Start** menu of the image, specifically in **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span></span>
7. <span data-ttu-id="f2764-148">응용 프로그램에 필요한 추가 Windows 구성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-148">Perform any additional Windows configurations required by your applications.</span></span>
8. <span data-ttu-id="f2764-149">EFS(파일 시스템 암호화)를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-149">Disable the Encrypting File System (EFS).</span></span>
9. <span data-ttu-id="f2764-150">**필수:** Windows Update로 이동하여 모든 중요 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-150">**REQUIRED:** Go to Windows Update and install all important updates.</span></span>
10. <span data-ttu-id="f2764-151">이미지에 sysprep을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-151">SYSPREP the image.</span></span>

<span data-ttu-id="f2764-152">새 이미지를 만드는 자세한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-152">The detailed steps for creating a new image are:</span></span>

1. <span data-ttu-id="f2764-153">Windows Server 2012 R2 Update DVD 또는 ISO 이미지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-153">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="f2764-154">디스크 관리를 사용하여 VHD 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-154">Create a VHD file by using Disk Management.</span></span>
   
   1. <span data-ttu-id="f2764-155">디스크 관리(diskmgmt.msc)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-155">Launch Disk Management (diskmgmt.msc).</span></span>
   2. <span data-ttu-id="f2764-156">40GB 크기의 동적으로 확장되는 VHD를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-156">Create a dynamically expanding VHD of 40 GB or more in size.</span></span> <span data-ttu-id="f2764-157">Windows, 응용 프로그램 및 사용자 지정에 필요한 공간의 양을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-157">(Estimate the amount of space needed for Windows, your applications, and customizations.</span></span> <span data-ttu-id="f2764-158">RDSH 역할 및 데스크톱 경험 기능이 설치된 Windows Server를 사용하려면 약 10GB의 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-158">Windows Server with the RDSH role and Desktop Experience feature installed will require about 10 GB of space).</span></span>
      
      1. <span data-ttu-id="f2764-159">**작업 > VHD 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-159">Click **Action > Create VHD**.</span></span>
      2. <span data-ttu-id="f2764-160">위치, 크기 및 VHD 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-160">Specify the location, size, and VHD format.</span></span> <span data-ttu-id="f2764-161">**동적 확장**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-161">Select **Dynamically expanding**, and then click **OK**.</span></span>
      
      <span data-ttu-id="f2764-162">그러면 몇 초 정도 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-162">This will run for several seconds.</span></span> <span data-ttu-id="f2764-163">VHD 만들기가 완료되면 디스크 관리 콘솔에 "초기화 안 됨" 상태의 드라이브 문자가 없는 새로운 디스크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-163">When the VHD creation is complete, you should see a new disk without any drive letter and in “Not initialized" state in the Disk Management console.</span></span>
      
      * <span data-ttu-id="f2764-164">디스크(할당되지 않은 공간이 아닌)를 마우스 오른쪽 단추로 클릭한 다음 **디스크 초기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-164">Right-click the disk (not the unallocated space), and then click **Initialize Disk**.</span></span> <span data-ttu-id="f2764-165">파티션 스타일로 **MBR**(마스터 부트 레코드)을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-165">Select **MBR** (Master Boot Record) as the partition style, and then click **OK**.</span></span>
      * <span data-ttu-id="f2764-166">새 볼륨 만들기: 할당되지 않은 공간을 마우스 오른쪽 단추로 클릭한 다음 **새 단순 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-166">Create a new volume: right-click the unallocated space, and then click **New Simple Volume**.</span></span> <span data-ttu-id="f2764-167">마법사의 기본값을 그대로 사용하지만 템플릿 이미지를 업로드할 때 잠재적인 문제를 피할 수 있도록 드라이브 문자를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-167">You can accept the defaults in the wizard, but make sure you assign a drive letter to avoid potential problems when you upload the template image.</span></span>
      * <span data-ttu-id="f2764-168">디스크를 마우스 오른쪽 단추로 클릭한 다음 **VHD 분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-168">Right-click the disk, and then click **Detach VHD**.</span></span>
3. <span data-ttu-id="f2764-169">Windows Server 2012 R2 설치:</span><span class="sxs-lookup"><span data-stu-id="f2764-169">Install Windows Server 2012 R2:</span></span>
   
   1. <span data-ttu-id="f2764-170">새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-170">Create a new virtual machine.</span></span> <span data-ttu-id="f2764-171">Hyper-V 관리자 또는 클라이언트 Hyper-V에서 새 가상 컴퓨터 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-171">Use the New Virtual Machine Wizard in Hyper-V Manager or Client Hyper-V.</span></span>
      1. <span data-ttu-id="f2764-172">[세대 지정] 페이지에서 **1세대**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-172">On the Specify Generation page, choose  **Generation 1**.</span></span>
      2. <span data-ttu-id="f2764-173">가상 하드 디스크 연결 페이지에서 **기존 가상 하드 디스크 사용**을 선택하고 이전 단계에서 만든 VHD로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-173">On the Connect Virtual Hard Disk page, select **Use an existing virtual hard disk**, and browse to the VHD you created in the previous step.</span></span>
      3. <span data-ttu-id="f2764-174">설치 옵션 페이지에서 **부팅 CD/DVD-ROM에서 운영 체제 설치**를 선택한 다음 Windows Server 2012 R2 설치 미디어의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-174">On the Installation Options page, select **Install an operating system from a boot CD/DVD_ROM**, and then select the location of your Windows Server 2012 R2 installation media.</span></span>
      4. <span data-ttu-id="f2764-175">마법사에서 Windows 및 응용 프로그램을 설치하는 데 필요한 다른 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-175">Choose other options in the wizard necessary to install Windows and your applications.</span></span> <span data-ttu-id="f2764-176">마법사를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-176">Finish the wizard.</span></span>
   2. <span data-ttu-id="f2764-177">마법사를 마친 후 가상 컴퓨터의 설정을 편집하고 Windows 및 프로그램을 설치하는 데 필요한 기타 항목(예: 가상 프로세서의 수)을 변경한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-177">After the wizard finishes, edit the settings of the virtual machine and make any other changes necessary to install Windows and your programs, such as the number of virtual processors, and then click **OK**.</span></span>
   3. <span data-ttu-id="f2764-178">가상 컴퓨터에 연결하여 Windows Server 2012 R2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-178">Connect to the virtual machine and install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="f2764-179">다음과 같이 RDSH(원격 데스크톱 세션 호스트) 역할 및 데스크톱 경험 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-179">Install the Remote Desktop Session Host (RDSH) role and the Desktop Experience feature:</span></span>
   1. <span data-ttu-id="f2764-180">서버 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-180">Launch Server Manager.</span></span>
   2. <span data-ttu-id="f2764-181">시작 화면 또는 **관리** 메뉴에서 **역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-181">Click **Add Roles and features** on the Welcome screen or from the **Manage** menu.</span></span>
   3. <span data-ttu-id="f2764-182">시작하기 전에 페이지에서 **다음** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-182">Click **Next** on the Before You Begin page.</span></span>
   4. <span data-ttu-id="f2764-183">**역할 기반 또는 기능 기반 설치**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-183">Select **Role-based or feature-based installation**, and then click **Next**.</span></span>
   5. <span data-ttu-id="f2764-184">목록에서 로컬 컴퓨터를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-184">Select the local machine from the list, and then click **Next**.</span></span>
   6. <span data-ttu-id="f2764-185">**원격 데스크톱 서비스**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-185">Select **Remote Desktop Services**, and then click **Next**.</span></span>
   7. <span data-ttu-id="f2764-186">**사용자 인터페이스 및 인프라**를 확장하고 **데스크톱 환경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-186">Expand **User Interfaces and Infrastructure** and select **Desktop Experience**.</span></span>
   8. <span data-ttu-id="f2764-187">**기능 추가**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-187">Click **Add Features**, and then click **Next**.</span></span>
   9. <span data-ttu-id="f2764-188">원격 데스크톱 서비스 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-188">On the Remote Desktop Services page, click **Next**.</span></span>
   10. <span data-ttu-id="f2764-189">**원격 데스크톱 세션 호스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-189">Click **Remote Desktop Session Host**.</span></span>
   11. <span data-ttu-id="f2764-190">**기능 추가**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-190">Click **Add Features**, and then click **Next**.</span></span>
   12. <span data-ttu-id="f2764-191">[설치 선택 확인] 페이지에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 선택한 다음, 다시 시작 경고에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-191">On the Confirm installation selections page, select **Restart the destination server automatically if required**, and then click **Yes** on the restart warning.</span></span>
   13. <span data-ttu-id="f2764-192">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-192">Click **Install**.</span></span> <span data-ttu-id="f2764-193">컴퓨터가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-193">The computer will restart.</span></span>
5. <span data-ttu-id="f2764-194">.NET Framework 3.5와 같은 응용 프로그램에 필요한 추가 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-194">Install additional features required by your applications, such as the .NET Framework 3.5.</span></span> <span data-ttu-id="f2764-195">이 기능을 설치하려면 역할 및 기능 추가 마법사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-195">To install the features, run the Add Roles and Features Wizard.</span></span>
6. <span data-ttu-id="f2764-196">RemoteApp을 통해 게시할 프로그램 및 응용 프로그램을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-196">Install and configure the programs and applications you want to publish through RemoteApp.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2764-197">응용 프로그램을 설치하기 전에 RDSH 역할을 설치하여 RemoteApp에 이미지를 업로드하기 전에 응용 프로그램 호환성 문제가 검색되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-197">Install the RDSH role before installing applications to ensure that any issues with application compatibility are discovered before the image is uploaded to RemoteApp.</span></span>
> 
> <span data-ttu-id="f2764-198">응용 프로그램(**.lnk** 파일)에 대한 바로 가기가 모든 사용자의 **시작** 메뉴(%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs)에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-198">Make sure a shortcut to your application (**.lnk** file) appears in the **Start** menu for all users (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs).</span></span> <span data-ttu-id="f2764-199">또한 **시작** 메뉴에 표시되는 아이콘이 사용자에게 표시하려는 아이콘인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-199">Also ensure that the icon you see in the **Start** menu is what you want users to see.</span></span> <span data-ttu-id="f2764-200">그렇지 않으면 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-200">If not, change it.</span></span> <span data-ttu-id="f2764-201">응용 프로그램을 시작 메뉴에 추가하지 *않아도 되지만* 추가할 경우 훨씬 쉽게 RemoteApp에 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-201">(You do not *have* to add the application to the Start menu, but it makes it much easier to publish the application in RemoteApp.</span></span> <span data-ttu-id="f2764-202">그렇지 않으면 앱을 게시할 때 응용 프로그램의 설치 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-202">Otherwise, you have to provide the installation path for the application when you publish the app.)</span></span>
> 
> 

1. <span data-ttu-id="f2764-203">응용 프로그램에 필요한 추가 Windows 구성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-203">Perform any additional Windows configurations required by your applications.</span></span>
2. <span data-ttu-id="f2764-204">EFS(파일 시스템 암호화)를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-204">Disable the Encrypting File System (EFS).</span></span> <span data-ttu-id="f2764-205">관리자 권한 명령 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-205">Run the following command at an elevated command window:</span></span>
   
     <span data-ttu-id="f2764-206">Fsutil behavior set disableencryption 1</span><span class="sxs-lookup"><span data-stu-id="f2764-206">Fsutil behavior set disableencryption 1</span></span>
   
   <span data-ttu-id="f2764-207">또는 레지스트리에서 다음 DWORD 값을 설정하거나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-207">Alternatively, you can set or add the following DWORD value in the registry:</span></span>
   
     <span data-ttu-id="f2764-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span><span class="sxs-lookup"><span data-stu-id="f2764-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span></span>
3. <span data-ttu-id="f2764-209">Azure 가상 컴퓨터 내에 이미지를 빌드하는 경우 **\%windir%\Panther\Unattend.xml** 파일의 이름을 바꿉니다. 이름을 그대로 사용하면 나중에 사용하는 업로드 스크립트가 작동하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-209">If you are building your image inside an Azure virtual machine, rename the **\%windir%\Panther\Unattend.xml** file, as this will block the upload script used later from working.</span></span> <span data-ttu-id="f2764-210">배포를 원래대로 되돌려야 하는 경우 파일을 계속 사용할 수 있도록 파일의 이름을 Unattend.old로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-210">Change the name of this file to Unattend.old so that you will still have the file in case you need to revert your deployment.</span></span>
4. <span data-ttu-id="f2764-211">Windows Update로 이동하여 모든 중요 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-211">Go to Windows Update and install all important updates.</span></span> <span data-ttu-id="f2764-212">모든 업데이트를 가져오려면 여러 번 Windows Update를 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-212">You might need to run Windows Update multiple times to get all updates.</span></span> <span data-ttu-id="f2764-213">(경우에 따라 업데이트를 설치하며 자체 해당 업데이트는 업데이트 해야합니다.)</span><span class="sxs-lookup"><span data-stu-id="f2764-213">(Sometimes you install an update, and that update itself requires an update.)</span></span>
5. <span data-ttu-id="f2764-214">이미지에 sysprep을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-214">SYSPREP the image.</span></span> <span data-ttu-id="f2764-215">관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-215">At an elevated command prompt, run the following command:</span></span>
   
   <span data-ttu-id="f2764-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span><span class="sxs-lookup"><span data-stu-id="f2764-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span></span>
   
   <span data-ttu-id="f2764-217">**참고:** 가상 컴퓨터이더라도 SYSPREP 명령의 **/mode: vm** 스위치는 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f2764-217">**Note:** Do not use the **/mode:vm** switch of the SYSPREP command even though this is a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2764-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2764-218">Next steps</span></span>
<span data-ttu-id="f2764-219">사용자 지정 템플릿 이미지를 만들었으니 이제 RemoteApp 컬렉션에 해당 이미지를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-219">Now that you have your custom template image, you need to upload that image to your RemoteApp collection.</span></span> <span data-ttu-id="f2764-220">다음 문서의 정보를 사용하여 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2764-220">Use the information in the following articles to create your collection:</span></span>

* [<span data-ttu-id="f2764-221">RemoteApp의 하이브리드 컬렉션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f2764-221">How to create a hybrid collection of RemoteApp</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="f2764-222">RemoteApp의 클라우드 컬렉션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f2764-222">How to create a cloud collection of RemoteApp</span></span>](remoteapp-create-cloud-deployment.md)

