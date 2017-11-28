---
title: "Azure에 업로드할 Windows VHD 준비 | Microsoft Docs"
description: "Azure에 업로드하기 전에 Windows VHD 또는 VHDX를 준비하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: aa1cec2ef11da6aa8a8c4089be36994ab5f61682
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-to-upload-to-azure"></a><span data-ttu-id="b9c9f-103">Azure에 업로드할 Windows VHD 또는 VHDX 준비</span><span class="sxs-lookup"><span data-stu-id="b9c9f-103">Prepare a Windows VHD or VHDX to upload to Azure</span></span>
<span data-ttu-id="b9c9f-104">온-프레미스에서 Microsoft Azure로 Windows VM(가상 컴퓨터)을 업로드하려면 먼저 VHD(가상 하드 디스크) 또는 VHDX를 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-104">Before you upload a Windows  virtual machines (VM) from on-premises to Microsoft Azure, you must prepare the virtual hard disk (VHD or VHDX).</span></span> <span data-ttu-id="b9c9f-105">Azure에서는 VHD 파일 형식의 고정된 크기의 디스크를 가진 1세대 VM만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-105">Azure supports only generation 1 VMs that are in the VHD file format and have a fixed sized disk.</span></span> <span data-ttu-id="b9c9f-106">VHD에 허용되는 최대 크기는 1,023GB입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-106">The maximum size allowed for the VHD is 1,023 GB.</span></span> <span data-ttu-id="b9c9f-107">1세대 VM을 VHDX 파일 시스템에서 VHD로, 동적 확장 디스크에서 고정 크기로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-107">You can convert a generation 1 VM from the VHDX file system to VHD and from a dynamically expanding disk to fixed-sized.</span></span> <span data-ttu-id="b9c9f-108">하지만 VM의 세대는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-108">But you can't change a VM's generation.</span></span> <span data-ttu-id="b9c9f-109">자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 합니까?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-109">For more information, see [Should I create a generation 1 or 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>

<span data-ttu-id="b9c9f-110">Azure VM을 위한 지원 정책에 대한 자세한 내용은 [Microsoft Azure VM을 위한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-110">For more information about the support policy for Azure VM, see [Microsoft server software support for Microsoft Azure VMs](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).</span></span>

> [!Note]
> <span data-ttu-id="b9c9f-111">이 문서의 지침은 Windows Server 2008 R2 이상 Windows Server 운영 체제의 64비트 버전에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-111">The instructions in this article apply to the 64-bit version of Windows Server 2008 R2 and later Windows server operating system.</span></span> <span data-ttu-id="b9c9f-112">Azure에서 실행 중인 32비트 버전 운영 체제에 대한 정보는 [Azure 가상 컴퓨터에서 32비트 운영 체제 지원](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-112">For information about running 32-bit version of operating system in Azure, see [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).</span></span>

## <a name="convert-the-virtual-disk-to-vhd-and-fixed-size-disk"></a><span data-ttu-id="b9c9f-113">가상 디스크를 VHD 및 고정된 크기 디스크로 변환</span><span class="sxs-lookup"><span data-stu-id="b9c9f-113">Convert the virtual disk to VHD and fixed size disk</span></span> 
<span data-ttu-id="b9c9f-114">가상 디스크를 Azure에 필요한 형식으로 변환해야 할 경우 이 섹션의 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-114">If you need to convert your virtual disk to the required format for Azure, use one of the methods in this section.</span></span> <span data-ttu-id="b9c9f-115">가상 디스크 변환 프로세스를 실행하기 전에 VM을 백업하고 Windows VHD가 로컬 서버에서 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-115">Back up the VM before you run the virtual disk conversion process and make sure that the Windows VHD works correctly on the local server.</span></span> <span data-ttu-id="b9c9f-116">Azure로 변환하거나 업로드하기 전에 VM 자체 내에서 오류를 해결해 보세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-116">Resolve any errors within the VM itself before you try to convert or upload it to Azure.</span></span>

<span data-ttu-id="b9c9f-117">디스크를 변환한 후 변환된 디스크를 사용하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-117">After you convert the disk, create a VM that uses the converted disk.</span></span> <span data-ttu-id="b9c9f-118">시작하고 VM에 로그인하여 업로드를 위한 VM 준비를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-118">Start and sign in to the VM to finish preparing the VM for upload.</span></span>

### <a name="convert-disk-using-hyper-v-manager"></a><span data-ttu-id="b9c9f-119">Hyper-V 관리자를 사용하여 디스크 변환</span><span class="sxs-lookup"><span data-stu-id="b9c9f-119">Convert disk using Hyper-V Manager</span></span>
1. <span data-ttu-id="b9c9f-120">Hyper-V 관리자를 열고 왼쪽에서 로컬 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-120">Open Hyper-V Manager and select your local computer on the left.</span></span> <span data-ttu-id="b9c9f-121">컴퓨터 목록 위의 메뉴에서 **작업** > **디스크 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-121">In the menu above the computer list, click **Action** > **Edit Disk**.</span></span>
2. <span data-ttu-id="b9c9f-122">**가상 하드 디스크 찾기** 화면에서 가상 디스크를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-122">On the **Locate Virtual Hard Disk** screen, locate and select your virtual disk.</span></span>
3. <span data-ttu-id="b9c9f-123">**작업 선택** 화면에서 **변환** 및 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-123">On the **Choose Action** screen, and then select **Convert** and **Next**.</span></span>
4. <span data-ttu-id="b9c9f-124">VHDX에서 변환해야 하는 경우 **VHD**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-124">If you need to convert from VHDX, select **VHD** and then click **Next**</span></span>
5. <span data-ttu-id="b9c9f-125">동적 확장 디스크에서 변환해야 하는 경우 **고정 크기**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-125">If you need to convert from a dynamically expanding disk, select **Fixed size** and then click **Next**</span></span>
6. <span data-ttu-id="b9c9f-126">새 VHD 파일을 저장할 경로를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-126">Locate and select a path to save the new VHD file to.</span></span>
7. <span data-ttu-id="b9c9f-127">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-127">Click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="b9c9f-128">이 문서의 명령은 상승된 PowerShell 세션에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-128">The commands in this article must be run on an elevated PowerShell session.</span></span>

### <a name="convert-disk-by-using-powershell"></a><span data-ttu-id="b9c9f-129">PowerShell을 사용한 디스크 변환</span><span class="sxs-lookup"><span data-stu-id="b9c9f-129">Convert disk by using PowerShell</span></span>
<span data-ttu-id="b9c9f-130">Windows PowerShell의 [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) 명령을 사용하여 가상 디스크를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-130">You can convert a virtual disk by using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) command in Windows PowerShell.</span></span> <span data-ttu-id="b9c9f-131">PowerShell을 시작할 때 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-131">Select **Run as administrator** when you start PowerShell.</span></span> 

<span data-ttu-id="b9c9f-132">다음 예제 명령은 VHDX에서 VHD로, 동적 확장 디스크에서 고정된 크기로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-132">The following example command converts from VHDX to VHD, and from a dynamically expanding disk to fixed-size:</span></span>

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
<span data-ttu-id="b9c9f-133">이 명령에서 “-Path” 값을 변환하려는 가상 하드 디스크에 대한 경로로 바꾸고 “-DestinationPath” 값을 변환된 디스크에 대한 새 경로 및 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-133">In this command, replace the value for "-Path" with the path to the virtual hard disk that you want to convert and the value for "-DestinationPath" with the new path and name of the converted disk.</span></span>

### <a name="convert-from-vmware-vmdk-disk-format"></a><span data-ttu-id="b9c9f-134">VMware VMDK 디스크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="b9c9f-134">Convert from VMware VMDK disk format</span></span>
<span data-ttu-id="b9c9f-135">[VMDK 파일 형식](https://en.wikipedia.org/wiki/VMDK)의 Windows VM 이미지가 있는 경우 [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497)를 사용하여 VHD로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-135">If you have a Windows VM image in the [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it to a VHD by using the [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span></span> <span data-ttu-id="b9c9f-136">자세한 내용은 블로그 문서 [VMware VMDK를 Hyper-V VHD로 변환하는 방법](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-136">For more information, see the blog article [How to Convert a VMware VMDK to Hyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span></span>

## <a name="set-windows-configurations-for-azure"></a><span data-ttu-id="b9c9f-137">Azure에 대한 Windows 구성 설정</span><span class="sxs-lookup"><span data-stu-id="b9c9f-137">Set Windows configurations for Azure</span></span>

<span data-ttu-id="b9c9f-138">Azure에 업로드하려는 VM에서 다음 단계의 모든 명령을 [관리자 권한 명령 프롬프트 창](https://technet.microsoft.com/library/cc947813.aspx)에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-138">On the VM that you plan to upload to Azure, run all commands in the following steps from an [elevated Command Prompt window](https://technet.microsoft.com/library/cc947813.aspx):</span></span>

1. <span data-ttu-id="b9c9f-139">라우팅 테이블에서 정적 영구 경로를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-139">Remove any static persistent route on the routing table:</span></span>
   
   * <span data-ttu-id="b9c9f-140">경로 테이블을 보려면 명령 프롬프트에서 `route print`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-140">To view the route table, run `route print` at the command prompt.</span></span>
   * <span data-ttu-id="b9c9f-141">**지속성 경로** 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-141">Check the **Persistence Routes** sections.</span></span> <span data-ttu-id="b9c9f-142">지속성 경로가 있는 경우 [경로 삭제](https://technet.microsoft.com/library/cc739598.apx)를 사용하여 경로를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-142">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) to remove it.</span></span>
2. <span data-ttu-id="b9c9f-143">WinHTTP 프록시를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-143">Remove the WinHTTP proxy:</span></span>
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. <span data-ttu-id="b9c9f-144">디스크 SAN 정책을 [Onlineall](https://technet.microsoft.com/library/gg252636.aspx)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-144">Set the disk SAN policy to [Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span></span> 
   
    ```PowerShell
    diskpart 
    ```
    <span data-ttu-id="b9c9f-145">명령 프롬프트 열기 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-145">In the open Command Prompt window, type the following commands:</span></span>

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. <span data-ttu-id="b9c9f-146">Windows에 대해 UTC(협정 세계시) 시간을 설정하고 Windows Time(w32time) 서비스의 시작 형식을 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-146">Set Coordinated Universal Time (UTC) time for Windows and the startup type of the Windows Time (w32time) service to **Automatically**:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. <span data-ttu-id="b9c9f-147">전원 프로필을 **고성능**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-147">Set the power profile to the **High Performance**:</span></span>

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-the-windows-services"></a><span data-ttu-id="b9c9f-148">Windows 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="b9c9f-148">Check the Windows services</span></span>
<span data-ttu-id="b9c9f-149">각 Windows 서비스가 **Windows 기본값**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-149">Make sure that each of the following Windows services is set to the **Windows default values**.</span></span> <span data-ttu-id="b9c9f-150">이들은 VM이 연결되었는지 확인하려면 반드시 설정해야 하는 최소 서비스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-150">These are the minimum numbers of services that must be set up to make sure that the VM has connectivity.</span></span> <span data-ttu-id="b9c9f-151">시작 설정을 재설정하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-151">To reset the startup settings, run the following commands:</span></span>
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a><span data-ttu-id="b9c9f-152">원격 데스크톱 레지스트리 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="b9c9f-152">Update Remote Desktop registry settings</span></span>
<span data-ttu-id="b9c9f-153">원격 데스크톱 연결에 대해 다음 설정이 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-153">Make sure that the following settings are configured correctly for remote desktop connection:</span></span>

>[!Note] 
><span data-ttu-id="b9c9f-154">이러한 단계에서 **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;object name&gt; &lt;value&gt;**를 실행할 때 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-154">You may receive an error message when you run the **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;object name&gt; &lt;value&gt;** in these steps.</span></span> <span data-ttu-id="b9c9f-155">오류 메시지는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-155">The error message can be safely ignored.</span></span> <span data-ttu-id="b9c9f-156">이는 도메인이 그룹 정책 개체를 통해 해당 구성을 푸시하지 않는다는 점만을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-156">It means only that the domain is not pushing that configuration through a Group Policy object.</span></span>
>
>

1. <span data-ttu-id="b9c9f-157">RDP(원격 데스크톱 프로토콜)이 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-157">Remote Desktop Protocol (RDP) is enabled:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. <span data-ttu-id="b9c9f-158">RDP 포트가 올바르게 설정되어 있습니다(기본 포트 3389).</span><span class="sxs-lookup"><span data-stu-id="b9c9f-158">The RDP port is set up correctly (Default port 3389):</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    <span data-ttu-id="b9c9f-159">VM을 배포할 때 기본 규칙은 포트 3389에 대해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-159">When you deploy a VM, the default rules are created against port 3389.</span></span> <span data-ttu-id="b9c9f-160">포트 번호를 변경하려는 경우 Azure에서 VM을 배포한 후에 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-160">If you want to change the port number,  do that after the VM is deployed in Azure.</span></span>

3. <span data-ttu-id="b9c9f-161">수신기가 모든 네트워크 인터페이스에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-161">The listener is listening in every network interface:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. <span data-ttu-id="b9c9f-162">RDP 연결에 대한 네트워크 수준 인증 모드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-162">Configure the Network Level Authentication mode for the RDP connections:</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. <span data-ttu-id="b9c9f-163">연결 유지 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-163">Set the keep-alive value：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. <span data-ttu-id="b9c9f-164">다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-164">Reconnect：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. <span data-ttu-id="b9c9f-165">동시 연결 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-165">Limit the number of concurrent connections：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. <span data-ttu-id="b9c9f-166">RDP 수신기에 연결된 자체 서명 인증서가 있는 경우 다음과 같이 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-166">If there are any self-signed certificates tied to the RDP listener, remove them:</span></span>
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    <span data-ttu-id="b9c9f-167">VM을 배포할 때 시작 부분에 연결할 수 있는지 확인하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-167">This is to make sure that you can connect at the beginning when you deploy the VM.</span></span> <span data-ttu-id="b9c9f-168">필요한 경우 Azure에서 VM을 배포한 후 나중에도 이 항목을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-168">You can also review this on a later stage after the VM is deployed in Azure if needed.</span></span>

9. <span data-ttu-id="b9c9f-169">VM이 도메인의 일부가 될 경우 다음 설정을 모두 확인하여 이전 설정이 되돌려지지 않도록 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-169">If the VM will be part of a Domain, check all the following settings to make sure that the former settings are not reverted.</span></span> <span data-ttu-id="b9c9f-170">확인이 필요한 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-170">The policies that must be checked are the following:</span></span>
    
    - <span data-ttu-id="b9c9f-171">RDP 활성화됨:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-171">RDP is enabled:</span></span>

         <span data-ttu-id="b9c9f-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span>
         
         <span data-ttu-id="b9c9f-173">**사용자가 원격 데스크톱을 사용하여 원격으로 연결하도록 허용**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-173">**Allow users to connect remotely by using Remote Desktop**</span></span>

    - <span data-ttu-id="b9c9f-174">NLA 그룹 정책:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-174">NLA group policy:</span></span>

        <span data-ttu-id="b9c9f-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span></span> 
        
        <span data-ttu-id="b9c9f-176">**네트워크 수준 인증을 사용한 원격 연결에 대해 사용자 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-176">**Require user Authentication for remote connections by using Network Level Authentication**</span></span>
    
    - <span data-ttu-id="b9c9f-177">연결 유지 설정:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-177">Keep Alive settings:</span></span>

        <span data-ttu-id="b9c9f-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b9c9f-179">**연결 유지 연결 간격 구성**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-179">**Configure keep-alive connection interval**</span></span>

    - <span data-ttu-id="b9c9f-180">다시 연결 설정:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-180">Reconnect settings:</span></span>

        <span data-ttu-id="b9c9f-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b9c9f-182">**자동 다시 연결**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-182">**Automatic reconnection**</span></span>

    - <span data-ttu-id="b9c9f-183">연결 수 제한 설정:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-183">Limit the number of connections settings:</span></span>

        <span data-ttu-id="b9c9f-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="b9c9f-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b9c9f-185">**연결 수 제한**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-185">**Limit number of connections**</span></span>

## <a name="configure-windows-firewall-rules"></a><span data-ttu-id="b9c9f-186">Windows 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="b9c9f-186">Configure Windows Firewall rules</span></span>
1. <span data-ttu-id="b9c9f-187">세 개 프로필(도메인, 표준 및 공용)에서 Windows 방화벽을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-187">Turn on Windows Firewall on the three profiles (Domain, Standard, and Public):</span></span>

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. <span data-ttu-id="b9c9f-188">PowerShell에서 다음 명령을 실행하여 세 개의 방화벽 프로필(도메인, 개인 및 공용)을 통한 WinRM을 허용하고 PowerShell 원격 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-188">Run the following command in PowerShell to allow WinRM through the three firewall profiles (Domain, Private, and Public) and enable the PowerShell Remote service:</span></span>
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. <span data-ttu-id="b9c9f-189">다음 방화벽 규칙을 사용하도록 설정하여 RDP 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-189">Enable the following firewall rules to allow the RDP traffic</span></span> 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. <span data-ttu-id="b9c9f-190">VM이 Virtual Network 내의 ping 명령에 응답할 수 있도록 파일 및 프린터 공유 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-190">Enable the File and Printer Sharing rule so that the VM can respond to a ping command inside the Virtual Network:</span></span>

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. <span data-ttu-id="b9c9f-191">VM이 도메인의 일부가 될 경우 다음 설정을 확인하여 이전 설정이 되돌려지지 않도록 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-191">If the VM  will be part of a Domain, check the following settings to make sure that the former settings are not reverted.</span></span> <span data-ttu-id="b9c9f-192">확인이 필요한 AD 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-192">The AD policies that must be checked are the following:</span></span>

    - <span data-ttu-id="b9c9f-193">Windows 방화벽 프로필을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b9c9f-193">Enable the Windows Firewall profiles</span></span>

        <span data-ttu-id="b9c9f-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **모든 네트워크 연결 보호**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Protect all network connections**</span></span>

       <span data-ttu-id="b9c9f-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **모든 네트워크 연결 보호**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Protect all network connections**</span></span>

    - <span data-ttu-id="b9c9f-196">RDP를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b9c9f-196">Enable RDP</span></span> 

        <span data-ttu-id="b9c9f-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

        <span data-ttu-id="b9c9f-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

    - <span data-ttu-id="b9c9f-199">ICMP-V4를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b9c9f-199">Enable ICMP-V4</span></span>

        <span data-ttu-id="b9c9f-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **ICMP 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

        <span data-ttu-id="b9c9f-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **ICMP 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="b9c9f-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a><span data-ttu-id="b9c9f-202">VM이 정상 상태이고 안전하며 RDP로 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="b9c9f-202">Verify VM is healthy, secure, and accessible with RDP</span></span> 
1. <span data-ttu-id="b9c9f-203">디스크가 정상이고 일관되도록 하려면 다음 VM이 다시 시작할 때 디스크 검사 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-203">To make sure the disk is healthy and consistent, run a check disk operation at the next VM restart:</span></span>

    ```PowerShell
    Chkdsk /f
    ```
    <span data-ttu-id="b9c9f-204">보고서에 정리되어 있고 정상인 디스크가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-204">Make sure that the report shows a clean and healthy disk.</span></span>

2. <span data-ttu-id="b9c9f-205">BCD(부팅 구성 데이터) 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-205">Set the Boot Configuration Data (BCD) settings.</span></span> 

    > [!Note]
    > <span data-ttu-id="b9c9f-206">이러한 명령을 PowerShell이 **아닌** 관리자 권한 CMD 창에서 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-206">Make sure you run these commands on an elevated CMD window and **NOT** on PowerShell:</span></span>
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. <span data-ttu-id="b9c9f-207">Windows Management Instrumentations 리포지토리가 일관되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-207">Verify that the Windows Management Instrumentations repository is consistent.</span></span> <span data-ttu-id="b9c9f-208">이를 수행하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-208">To perform this, run the following command:</span></span>

    ```PowerShell
    winmgmt /verifyrepository
    ```
    <span data-ttu-id="b9c9f-209">리포지토리가 손상된 경우 [WMI: 리포지토리 손상 여부](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-209">If the repository is corrupted, see [WMI: Repository Corruption, or Not](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).</span></span>

4. <span data-ttu-id="b9c9f-210">타사 응용 프로그램이 포트 3389를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-210">Make sure that any other application is not using the port 3389.</span></span> <span data-ttu-id="b9c9f-211">이 포트는 Azure의 RDP 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-211">This port is used for the RDP service in Azure.</span></span> <span data-ttu-id="b9c9f-212">**netstat-anob**를 실행하여 VM에서 사용되는 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-212">You can run **netstat -anob** to see which ports are in used on the VM:</span></span>

    ```PowerShell
    netstat -anob
    ```

5. <span data-ttu-id="b9c9f-213">업로드하려는 Windows VHD가 도메인 컨트롤러인 경우 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-213">If the Windows VHD that you want to upload is a domain controller, then follow these steps:</span></span>

    <span data-ttu-id="b9c9f-214">A.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-214">A.</span></span> <span data-ttu-id="b9c9f-215">[이러한 추가 단계](https://support.microsoft.com/kb/2904015)에 따라 디스크를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-215">Follow [these extra steps](https://support.microsoft.com/kb/2904015) to prepare the disk.</span></span>

    <span data-ttu-id="b9c9f-216">B.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-216">B.</span></span> <span data-ttu-id="b9c9f-217">특정 시점에 DSRM에서 VM을 시작해야 하는 경우 DSRM 암호를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-217">Make sure that you know the DSRM password in case you have to start the VM in DSRM at some point.</span></span> <span data-ttu-id="b9c9f-218">이 링크를 참조하여 [DSRM 암호](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx)를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-218">You may want to refer to this link to set the [DSRM password](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).</span></span>

6. <span data-ttu-id="b9c9f-219">기본 제공 관리자 계정 및 암호를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-219">Make sure that the Built-in Administrator account and password are known to you.</span></span> <span data-ttu-id="b9c9f-220">현재 로컬 관리자 암호를 다시 설정하고, 이 계정을 사용하여 RDP 연결을 통해 Windows에 로그인할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-220">You may want to reset the current local administrator password and make sure that you can use this account to sign in to Windows through the RDP connection.</span></span> <span data-ttu-id="b9c9f-221">이 액세스 권한은 "원격 데스크톱 서비스를 통한 로그온 허용" 그룹 정책 개체에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-221">This access permission is controlled by the "Allow log on through Remote Desktop Services" Group Policy object.</span></span> <span data-ttu-id="b9c9f-222">이 개체는 다음 위치에 있는 로컬 그룹 정책 편집기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-222">You can view this object in the Local Group Policy Editor under:</span></span>

    <span data-ttu-id="b9c9f-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span><span class="sxs-lookup"><span data-stu-id="b9c9f-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span></span>

7. <span data-ttu-id="b9c9f-224">다음 AD 정책을 확인하여 RDP를 통해 또는 네트워크에서 RDP 액세스를 차단하지는 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-224">Check the following AD polices to make sure that you are not blocking your RDP access through RDP nor from the network:</span></span>

    - <span data-ttu-id="b9c9f-225">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access to this computer from the network</span><span class="sxs-lookup"><span data-stu-id="b9c9f-225">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access to this computer from the network</span></span>

    - <span data-ttu-id="b9c9f-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span><span class="sxs-lookup"><span data-stu-id="b9c9f-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span></span>


8. <span data-ttu-id="b9c9f-227">VM을 다시 시작하여 Windows가 여전히 정상 상태인지와 RDP 연결을 사용하여 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-227">Restart the VM to make sure that Windows is still healthy can be reached by using the RDP connection.</span></span> <span data-ttu-id="b9c9f-228">이 시점에서 사용자 로컬 Hyper-V에서 VM을 만들고, VM이 완벽히 시작되고 있는지 확인한 다음, RDP가 연결 가능한 상태인지 여부를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-228">At this point, you may want to create a VM in your local Hyper-V to make sure the VM is starting completely and then test whether it is RDP reachable.</span></span>

9. <span data-ttu-id="b9c9f-229">TCP 패킷 또는 추가 방화벽을 분석하는 소프트웨어와 같은 추가 전송 드라이버 인터페이스 필터를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-229">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets or extra firewalls.</span></span> <span data-ttu-id="b9c9f-230">필요한 경우 Azure에서 VM을 배포한 후 나중에도 이 항목을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-230">You can also review this on a later stage after the VM is deployed in Azure if needed.</span></span>

10. <span data-ttu-id="b9c9f-231">실제 구성 요소 또는 다른 가상화 기술과 관련된 다른 타사 소프트웨어 및 드라이버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-231">Uninstall any other third-party software and driver that is related to physical components or any other virtualization technology.</span></span>

### <a name="install-windows-updates"></a><span data-ttu-id="b9c9f-232">Windows 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="b9c9f-232">Install Windows Updates</span></span>
<span data-ttu-id="b9c9f-233">이상적인 구성은 **최신 컴퓨터의 패치 수준을 갖추는 것**입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-233">The ideal configuration is to **have the patch level of the machine at the latest**.</span></span> <span data-ttu-id="b9c9f-234">가능하지 않은 경우 다음 업데이트가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-234">If this is not possible, make sure that the following updates are installed:</span></span>

|                       |                   |           |                                       <span data-ttu-id="b9c9f-235">최소 파일 버전 x64</span><span class="sxs-lookup"><span data-stu-id="b9c9f-235">Minimum file version x64</span></span>       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| <span data-ttu-id="b9c9f-236">구성 요소</span><span class="sxs-lookup"><span data-stu-id="b9c9f-236">Component</span></span>               | <span data-ttu-id="b9c9f-237">이진</span><span class="sxs-lookup"><span data-stu-id="b9c9f-237">Binary</span></span>            | <span data-ttu-id="b9c9f-238">Windows 7 및 Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="b9c9f-238">Windows 7 & Windows Server 2008 R2</span></span> | <span data-ttu-id="b9c9f-239">Windows 8 및 Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b9c9f-239">Windows 8 & Windows Server 2012</span></span>             | <span data-ttu-id="b9c9f-240">Windows 8.1 및 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b9c9f-240">Windows 8.1 & Windows Server 2012 R2</span></span> | <span data-ttu-id="b9c9f-241">Windows 10 & Windows Server 2016 RS1</span><span class="sxs-lookup"><span data-stu-id="b9c9f-241">Windows 10 & Windows Server 2016 RS1</span></span> | <span data-ttu-id="b9c9f-242">Windows 10 RS2</span><span class="sxs-lookup"><span data-stu-id="b9c9f-242">Windows 10 RS2</span></span>             |
| <span data-ttu-id="b9c9f-243">저장소</span><span class="sxs-lookup"><span data-stu-id="b9c9f-243">Storage</span></span>                 | <span data-ttu-id="b9c9f-244">disk.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-244">disk.sys</span></span>          | <span data-ttu-id="b9c9f-245">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-245">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="b9c9f-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span></span> | <span data-ttu-id="b9c9f-247">6.3.9600.18203 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="b9c9f-247">6.3.9600.18203 - KB3137061</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="b9c9f-248">storport.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-248">storport.sys</span></span>      | <span data-ttu-id="b9c9f-249">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-249">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span><span class="sxs-lookup"><span data-stu-id="b9c9f-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span></span> | <span data-ttu-id="b9c9f-251">6.3.9600.18573 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-251">6.3.9600.18573 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-252">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-252">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-253">10.0.15063.332</span><span class="sxs-lookup"><span data-stu-id="b9c9f-253">10.0.15063.332</span></span>             |
|                         | <span data-ttu-id="b9c9f-254">ntfs.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-254">ntfs.sys</span></span>          | <span data-ttu-id="b9c9f-255">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-255">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span><span class="sxs-lookup"><span data-stu-id="b9c9f-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span></span> | <span data-ttu-id="b9c9f-257">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-257">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-258">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-258">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-259">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b9c9f-259">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b9c9f-260">Iologmsg.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-260">Iologmsg.dll</span></span>      | <span data-ttu-id="b9c9f-261">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-261">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-262">6.2.9200.16384 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="b9c9f-262">6.2.9200.16384 - KB2995387</span></span>                  | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b9c9f-263">Classpnp.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-263">Classpnp.sys</span></span>      | <span data-ttu-id="b9c9f-264">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-264">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="b9c9f-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span></span> | <span data-ttu-id="b9c9f-266">6.3.9600.18334 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b9c9f-266">6.3.9600.18334 - KB3172614</span></span>           | <span data-ttu-id="b9c9f-267">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-267">10.0.14393.953 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b9c9f-268">Volsnap.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-268">Volsnap.sys</span></span>       | <span data-ttu-id="b9c9f-269">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-269">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span><span class="sxs-lookup"><span data-stu-id="b9c9f-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span></span> | <span data-ttu-id="b9c9f-271">6.3.9600.18265 - KB3145384</span><span class="sxs-lookup"><span data-stu-id="b9c9f-271">6.3.9600.18265 - KB3145384</span></span>           | -                                    | <span data-ttu-id="b9c9f-272">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-272">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-273">partmgr.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-273">partmgr.sys</span></span>       | <span data-ttu-id="b9c9f-274">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-274">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-275">6.2.9200.16681 - KB2877114</span><span class="sxs-lookup"><span data-stu-id="b9c9f-275">6.2.9200.16681 - KB2877114</span></span>                  | <span data-ttu-id="b9c9f-276">6.3.9600.17401 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="b9c9f-276">6.3.9600.17401 - KB3000850</span></span>           | <span data-ttu-id="b9c9f-277">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-277">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b9c9f-278">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-278">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-279">volmgr.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-279">volmgr.sys</span></span>        |                                    |                                             |                                      |                                      | <span data-ttu-id="b9c9f-280">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-280">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-281">Volmgrx.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-281">Volmgrx.sys</span></span>       | <span data-ttu-id="b9c9f-282">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-282">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | <span data-ttu-id="b9c9f-283">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-283">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-284">Msiscsi.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-284">Msiscsi.sys</span></span>       | <span data-ttu-id="b9c9f-285">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-285">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-286">6.2.9200.21006 - KB2955163</span><span class="sxs-lookup"><span data-stu-id="b9c9f-286">6.2.9200.21006 - KB2955163</span></span>                  | <span data-ttu-id="b9c9f-287">6.3.9600.18624 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-287">6.3.9600.18624 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-288">10.0.14393.1066 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-288">10.0.14393.1066 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-289">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b9c9f-289">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b9c9f-290">Msdsm.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-290">Msdsm.sys</span></span>         | <span data-ttu-id="b9c9f-291">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-291">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-292">6.2.9200.21474 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="b9c9f-292">6.2.9200.21474 - KB3046101</span></span>                  | <span data-ttu-id="b9c9f-293">6.3.9600.18592 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-293">6.3.9600.18592 - KB4022726</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="b9c9f-294">Mpio.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-294">Mpio.sys</span></span>          | <span data-ttu-id="b9c9f-295">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-295">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-296">6.2.9200.21190 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="b9c9f-296">6.2.9200.21190 - KB3046101</span></span>                  | <span data-ttu-id="b9c9f-297">6.3.9600.18616 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-297">6.3.9600.18616 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-298">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-298">10.0.14393.1198 - KB4022715</span></span>          | -                          |
|                         | <span data-ttu-id="b9c9f-299">Fveapi.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-299">Fveapi.dll</span></span>        | <span data-ttu-id="b9c9f-300">6.1.7601.23311 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-300">6.1.7601.23311 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-301">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="b9c9f-301">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="b9c9f-302">6.3.9600.18294 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b9c9f-302">6.3.9600.18294 - KB3172614</span></span>           | <span data-ttu-id="b9c9f-303">10.0.14393.576 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-303">10.0.14393.576 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b9c9f-304">Fveapibase.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-304">Fveapibase.dll</span></span>    | <span data-ttu-id="b9c9f-305">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-305">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-306">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="b9c9f-306">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="b9c9f-307">6.3.9600.17415 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b9c9f-307">6.3.9600.17415 - KB3172614</span></span>           | <span data-ttu-id="b9c9f-308">10.0.14393.206 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-308">10.0.14393.206 - KB4022715</span></span>           | -                          |
| <span data-ttu-id="b9c9f-309">네트워크</span><span class="sxs-lookup"><span data-stu-id="b9c9f-309">Network</span></span>                 | <span data-ttu-id="b9c9f-310">netvsc.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-310">netvsc.sys</span></span>        | -                                  | -                                           | -                                    | <span data-ttu-id="b9c9f-311">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-311">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-312">10.0.15063.250 - KB4020001</span><span class="sxs-lookup"><span data-stu-id="b9c9f-312">10.0.15063.250 - KB4020001</span></span> |
|                         | <span data-ttu-id="b9c9f-313">mrxsmb10.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-313">mrxsmb10.sys</span></span>      | <span data-ttu-id="b9c9f-314">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b9c9f-314">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b9c9f-315">6.2.9200.22108 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-315">6.2.9200.22108 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-316">6.3.9600.18603 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-316">6.3.9600.18603 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-317">10.0.14393.479 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-317">10.0.14393.479 - KB4022715</span></span>           | <span data-ttu-id="b9c9f-318">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b9c9f-318">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b9c9f-319">mrxsmb20.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-319">mrxsmb20.sys</span></span>      | <span data-ttu-id="b9c9f-320">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b9c9f-320">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b9c9f-321">6.2.9200.21548 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-321">6.2.9200.21548 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-322">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-322">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-323">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-323">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b9c9f-324">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b9c9f-324">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b9c9f-325">mrxsmb.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-325">mrxsmb.sys</span></span>        | <span data-ttu-id="b9c9f-326">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b9c9f-326">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b9c9f-327">6.2.9200.22074 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-327">6.2.9200.22074 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-328">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-328">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-329">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-329">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b9c9f-330">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-330">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-331">tcpip.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-331">tcpip.sys</span></span>         | <span data-ttu-id="b9c9f-332">6.1.7601.23761 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b9c9f-332">6.1.7601.23761 - KB4022722</span></span>         | <span data-ttu-id="b9c9f-333">6.2.9200.22070 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-333">6.2.9200.22070 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-334">6.3.9600.18478 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-334">6.3.9600.18478 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-335">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-335">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-336">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b9c9f-336">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b9c9f-337">http.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-337">http.sys</span></span>          | <span data-ttu-id="b9c9f-338">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-338">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-339">6.2.9200.17285 - KB3042553</span><span class="sxs-lookup"><span data-stu-id="b9c9f-339">6.2.9200.17285 - KB3042553</span></span>                  | <span data-ttu-id="b9c9f-340">6.3.9600.18574 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-340">6.3.9600.18574 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-341">10.0.14393.251 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-341">10.0.14393.251 - KB4022715</span></span>           | <span data-ttu-id="b9c9f-342">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b9c9f-342">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b9c9f-343">vmswitch.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-343">vmswitch.sys</span></span>      | <span data-ttu-id="b9c9f-344">6.1.7601.23727 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b9c9f-344">6.1.7601.23727 - KB4022719</span></span>         | <span data-ttu-id="b9c9f-345">6.2.9200.22117 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-345">6.2.9200.22117 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-346">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-346">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-347">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-347">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-348">10.0.15063.138</span><span class="sxs-lookup"><span data-stu-id="b9c9f-348">10.0.15063.138</span></span>             |
| <span data-ttu-id="b9c9f-349">코어</span><span class="sxs-lookup"><span data-stu-id="b9c9f-349">Core</span></span>                    | <span data-ttu-id="b9c9f-350">ntoskrnl.exe</span><span class="sxs-lookup"><span data-stu-id="b9c9f-350">ntoskrnl.exe</span></span>      | <span data-ttu-id="b9c9f-351">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b9c9f-351">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="b9c9f-352">6.2.9200.22170 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="b9c9f-352">6.2.9200.22170 - KB4022718</span></span>                  | <span data-ttu-id="b9c9f-353">6.3.9600.18696 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-353">6.3.9600.18696 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-354">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-354">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-355">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b9c9f-355">10.0.15063.483</span></span>             |
| <span data-ttu-id="b9c9f-356">원격 데스크톱 서비스</span><span class="sxs-lookup"><span data-stu-id="b9c9f-356">Remote Desktop Services</span></span> | <span data-ttu-id="b9c9f-357">rdpcorets.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-357">rdpcorets.dll</span></span>     | <span data-ttu-id="b9c9f-358">6.2.9200.21506 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b9c9f-358">6.2.9200.21506 - KB4022719</span></span>         | <span data-ttu-id="b9c9f-359">6.2.9200.22104 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b9c9f-359">6.2.9200.22104 - KB4022724</span></span>                  | <span data-ttu-id="b9c9f-360">6.3.9600.18619 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-360">6.3.9600.18619 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-361">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-361">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b9c9f-362">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-362">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-363">termsrv.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-363">termsrv.dll</span></span>       | <span data-ttu-id="b9c9f-364">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-364">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b9c9f-365">6.2.9200.17048 - KB2973501</span><span class="sxs-lookup"><span data-stu-id="b9c9f-365">6.2.9200.17048 - KB2973501</span></span>                  | <span data-ttu-id="b9c9f-366">6.3.9600.17415 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="b9c9f-366">6.3.9600.17415 - KB3000850</span></span>           | <span data-ttu-id="b9c9f-367">10.0.14393.0 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-367">10.0.14393.0 - KB4022715</span></span>             | <span data-ttu-id="b9c9f-368">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b9c9f-368">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b9c9f-369">termdd.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-369">termdd.sys</span></span>        | <span data-ttu-id="b9c9f-370">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-370">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b9c9f-371">win32k.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-371">win32k.sys</span></span>        | <span data-ttu-id="b9c9f-372">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b9c9f-372">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="b9c9f-373">6.2.9200.22168 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="b9c9f-373">6.2.9200.22168 - KB4022718</span></span>                  | <span data-ttu-id="b9c9f-374">6.3.9600.18698 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b9c9f-374">6.3.9600.18698 - KB4022726</span></span>           | <span data-ttu-id="b9c9f-375">10.0.14393.594 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b9c9f-375">10.0.14393.594 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b9c9f-376">rdpdd.dll</span><span class="sxs-lookup"><span data-stu-id="b9c9f-376">rdpdd.dll</span></span>         | <span data-ttu-id="b9c9f-377">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-377">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b9c9f-378">rdpwd.sys</span><span class="sxs-lookup"><span data-stu-id="b9c9f-378">rdpwd.sys</span></span>         | <span data-ttu-id="b9c9f-379">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b9c9f-379">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
| <span data-ttu-id="b9c9f-380">보안</span><span class="sxs-lookup"><span data-stu-id="b9c9f-380">Security</span></span>                | <span data-ttu-id="b9c9f-381">WannaCrypt 기한</span><span class="sxs-lookup"><span data-stu-id="b9c9f-381">Due to WannaCrypt</span></span> | <span data-ttu-id="b9c9f-382">KB4012212</span><span class="sxs-lookup"><span data-stu-id="b9c9f-382">KB4012212</span></span>                          | <span data-ttu-id="b9c9f-383">KB4012213</span><span class="sxs-lookup"><span data-stu-id="b9c9f-383">KB4012213</span></span>                                   | <span data-ttu-id="b9c9f-384">KB4012213</span><span class="sxs-lookup"><span data-stu-id="b9c9f-384">KB4012213</span></span>                            | <span data-ttu-id="b9c9f-385">KB4012606</span><span class="sxs-lookup"><span data-stu-id="b9c9f-385">KB4012606</span></span>                            | <span data-ttu-id="b9c9f-386">KB4012606</span><span class="sxs-lookup"><span data-stu-id="b9c9f-386">KB4012606</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="b9c9f-387">KB4012216</span><span class="sxs-lookup"><span data-stu-id="b9c9f-387">KB4012216</span></span>                                   |                                      | <span data-ttu-id="b9c9f-388">KB4013198</span><span class="sxs-lookup"><span data-stu-id="b9c9f-388">KB4013198</span></span>                            | <span data-ttu-id="b9c9f-389">KB4013198</span><span class="sxs-lookup"><span data-stu-id="b9c9f-389">KB4013198</span></span>                  |
|                         |                   | <span data-ttu-id="b9c9f-390">KB4012215</span><span class="sxs-lookup"><span data-stu-id="b9c9f-390">KB4012215</span></span>                          | <span data-ttu-id="b9c9f-391">KB4012214</span><span class="sxs-lookup"><span data-stu-id="b9c9f-391">KB4012214</span></span>                                   | <span data-ttu-id="b9c9f-392">KB4012216</span><span class="sxs-lookup"><span data-stu-id="b9c9f-392">KB4012216</span></span>                            | <span data-ttu-id="b9c9f-393">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b9c9f-393">KB4013429</span></span>                            | <span data-ttu-id="b9c9f-394">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b9c9f-394">KB4013429</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="b9c9f-395">KB4012217</span><span class="sxs-lookup"><span data-stu-id="b9c9f-395">KB4012217</span></span>                                   |                                      | <span data-ttu-id="b9c9f-396">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b9c9f-396">KB4013429</span></span>                            | <span data-ttu-id="b9c9f-397">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b9c9f-397">KB4013429</span></span>                  |
       
### <span data-ttu-id="b9c9f-398">Sysprep를 사용하는 경우 <a id="step23"></a></span><span class="sxs-lookup"><span data-stu-id="b9c9f-398">When to use sysprep <a id="step23"></a></span></span>    

<span data-ttu-id="b9c9f-399">Sysprep는 모든 개인 데이터를 제거하고 여러 구성 요소를 다시 설정함으로써 시스템의 설치를 다시 설정하고 “첫 실행 경험”을 제공하는 Windows 설치를 실행할 수 있는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-399">Sysprep is a process that you could run into a windows installation that will reset the installation of the system and will provide an “out of the box experience” by removing all personal data and resetting several components.</span></span> <span data-ttu-id="b9c9f-400">일반적으로 특정 구성이 있는 다른 여러 VM을 배포할 수 있는 템플릿을 만들려는 경우 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-400">You typically do this if you want to create a template from which you can deploy several other VMs that have a specific configuration.</span></span> <span data-ttu-id="b9c9f-401">이를 **일반화된 이미지**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-401">This is called a **generalized image**.</span></span>

<span data-ttu-id="b9c9f-402">대신에 한 디스크에서 하나의 VM만 만들려는 경우 Sysprep를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-402">If, instead, you want only to create one VM from one disk, you don’t have to use sysprep.</span></span> <span data-ttu-id="b9c9f-403">이 경우 **특수화된 이미지**에서 VM을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-403">In this situation, you can just create the VM from what is known as a **specialized image**.</span></span>

<span data-ttu-id="b9c9f-404">특수화된 디스크에서 VM을 만드는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-404">For more information about how to create a VM from a specialized disk, see:</span></span>

- [<span data-ttu-id="b9c9f-405">특수화된 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b9c9f-405">Create a VM from a specialized disk</span></span>](create-vm-specialized.md)
- [<span data-ttu-id="b9c9f-406">특수화된 VHD 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b9c9f-406">Create a VM from a specialized VHD disk</span></span>](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

<span data-ttu-id="b9c9f-407">일반화된 이미지를 만들려는 경우 Sysprep를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-407">If you want to create a generalized image, you need to run sysprep.</span></span> <span data-ttu-id="b9c9f-408">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-408">For more information about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> 

<span data-ttu-id="b9c9f-409">Windows 기반 컴퓨터에 설치된 모든 역할 또는 응용 프로그램이 이 일반화를 지원하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-409">Not every role or application that’s installed on a Windows-based computer supports this generalization.</span></span> <span data-ttu-id="b9c9f-410">따라서 이 절차를 실행하기 전, 다음 문서를 참조하여 해당 컴퓨터의 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-410">So before you run this procedure, refer to the following article to make sure that the role of that computer is supported by sysprep.</span></span> <span data-ttu-id="b9c9f-411">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-411">For more information, [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

### <a name="steps-to-generalize-a-vhd"></a><span data-ttu-id="b9c9f-412">VHD를 일반화하는 단계</span><span class="sxs-lookup"><span data-stu-id="b9c9f-412">Steps to generalize a VHD</span></span>

>[!NOTE]
> <span data-ttu-id="b9c9f-413">다음 단계에 지정된 대로 sysprep.exe를 실행한 후 VM을 끕니다. Azure에서 이미지를 만든 후에 다시 켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-413">After you run sysprep.exe as specified  in the following steps, turn off the VM, and do not turn it back on until you create an image from it in Azure.</span></span>

1. <span data-ttu-id="b9c9f-414">Windows VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-414">Sign in to the Windows VM.</span></span>
2. <span data-ttu-id="b9c9f-415">관리자 권한으로 **명령 프롬프트**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-415">Run **Command Prompt** as an administrator.</span></span> 
3. <span data-ttu-id="b9c9f-416">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 **sysprep.exe**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-416">Change the directory to: **%windir%\system32\sysprep**, and then run **sysprep.exe**.</span></span>
3. <span data-ttu-id="b9c9f-417">**시스템 준비 도구** 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-417">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>

    ![시스템 준비 도구](media/prepare-for-upload-vhd-image/syspre.png)
4. <span data-ttu-id="b9c9f-419">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-419">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="b9c9f-420">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-420">Click **OK**.</span></span>
6. <span data-ttu-id="b9c9f-421">Sysprep가 완료되면 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-421">When Sysprep completes, shut down the VM.</span></span> <span data-ttu-id="b9c9f-422">VM을 종료할 때 **다시 시작**을 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-422">Do not use **Restart** to shut down the VM.</span></span>
7. <span data-ttu-id="b9c9f-423">이제 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-423">Now the VHD is ready to be uploaded.</span></span> <span data-ttu-id="b9c9f-424">일반화된 디스크에서 VM을 만드는 방법에 대한 자세한 내용은 [일반화된 VHD를 업로드하고 Azure에서 새 VM 만들기](sa-upload-generalized.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-424">For more information about how to create a VM from a generalized disk, see [Upload a generalized VHD and use it to create a new VMs in Azure](sa-upload-generalized.md).</span></span>


## <a name="complete-recommended-configurations"></a><span data-ttu-id="b9c9f-425">권장된 구성 완료</span><span class="sxs-lookup"><span data-stu-id="b9c9f-425">Complete recommended configurations</span></span>
<span data-ttu-id="b9c9f-426">다음 설정은 VHD 업로드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-426">The following settings do not affect VHD uploading.</span></span> <span data-ttu-id="b9c9f-427">단, 반드시 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-427">However, we strongly recommend that you configured them.</span></span>

* <span data-ttu-id="b9c9f-428">[Azure VM 에이전트](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-428">Install the [Azure VMs Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b9c9f-429">그런 다음 VM 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-429">Then you can enable VM extensions.</span></span> <span data-ttu-id="b9c9f-430">VM 확장은 암호 재설정, RDP 구성 등 VM에서 사용하려는 대부분의 중요 기능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-430">The VM extensions implement most of the critical functionality that you might want to use with your VMs such as resetting passwords, configuring RDP, and so on.</span></span> <span data-ttu-id="b9c9f-431">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-431">For more information, see:</span></span>

    - [<span data-ttu-id="b9c9f-432">VM 에이전트 및 확장 - 1부</span><span class="sxs-lookup"><span data-stu-id="b9c9f-432">VM Agent and Extensions – Part 1</span></span>](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [<span data-ttu-id="b9c9f-433">VM 에이전트 및 확장 - 2부</span><span class="sxs-lookup"><span data-stu-id="b9c9f-433">VM Agent and Extensions – Part 2</span></span>](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* <span data-ttu-id="b9c9f-434">덤프 로그는 Windows 충돌 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-434">The Dump log can be helpful in troubleshooting Windows crash issues.</span></span> <span data-ttu-id="b9c9f-435">덤프 로그 수집을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-435">Enable the Dump log collection:</span></span>
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    <span data-ttu-id="b9c9f-436">이 문서에 나온 모든 절차 단계에서 오류를 수신하는 경우 레지스트리 키가 이미 존재한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-436">If you receive any errors during any of the procedural steps in this article, this means that the registry keys already exists.</span></span> <span data-ttu-id="b9c9f-437">이 경우 다음 명령을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-437">In this situation, use the following commands instead:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  <span data-ttu-id="b9c9f-438">Azure에서 VM을 만든 후에 성능 향상을 위해 “임시 드라이브” 볼륨에 페이지 파일을 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-438">After the VM is created in Azure, we recommend that you put the pagefile on the ”Temporal drive” volume to improve performance.</span></span> <span data-ttu-id="b9c9f-439">이 작업은 다음과 같이 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-439">You can set up this as follows:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
<span data-ttu-id="b9c9f-440">VM에 연결된 데이터 디스크가 있는 경우 Temporal 드라이브 볼륨의 드라이브 문자는 일반적으로 “D”입니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-440">If there’s any data disk that is attached to the VM, the Temporal drive volume's drive letter is typically "D."</span></span> <span data-ttu-id="b9c9f-441">이 지정은 사용 가능한 드라이브 수 및 사용자가 지정한 설정에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9c9f-441">This designation could be different, depending on the number of available drives and the settings that you  make.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9c9f-442">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9c9f-442">Next steps</span></span>
* [<span data-ttu-id="b9c9f-443">Resource Manager 배포를 위해 Azure에 Windows VM 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="b9c9f-443">Upload a Windows VM image to Azure for Resource Manager deployments</span></span>](upload-generalized-managed.md)

