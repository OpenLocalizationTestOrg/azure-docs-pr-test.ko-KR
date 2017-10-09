---
title: Windows VHD tooupload tooAzure aaaPrepare | Microsoft Docs
description: "어떻게 tooprepare Windows VHD 또는 VHDX tooAzure 업로드 하기 전에"
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
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a><span data-ttu-id="01f35-103">Windows VHD 또는 VHDX tooupload tooAzure 준비</span><span class="sxs-lookup"><span data-stu-id="01f35-103">Prepare a Windows VHD or VHDX tooupload tooAzure</span></span>
<span data-ttu-id="01f35-104">온-프레미스 tooMicrosoft Azure에서에서 Windows 가상 컴퓨터 (VM)를 업로드 하기 전에 hello 가상 하드 디스크 (VHD 또는 VHDX)를 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-104">Before you upload a Windows  virtual machines (VM) from on-premises tooMicrosoft Azure, you must prepare hello virtual hard disk (VHD or VHDX).</span></span> <span data-ttu-id="01f35-105">Azure는 hello VHD 파일 형식으로 고정된 크기 디스크를 포함 하는 1 세대 Vm 에서만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-105">Azure supports only generation 1 VMs that are in hello VHD file format and have a fixed sized disk.</span></span> <span data-ttu-id="01f35-106">hello 최대 허용 크기 hello에 대 한 VHD는 1, 023 GB입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-106">hello maximum size allowed for hello VHD is 1,023 GB.</span></span> <span data-ttu-id="01f35-107">한 세대 VHDX hello에서 1 VM 시스템 tooVHD 파일 및 toofixed 크기의 디스크를 동적 확장에서 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-107">You can convert a generation 1 VM from hello VHDX file system tooVHD and from a dynamically expanding disk toofixed-sized.</span></span> <span data-ttu-id="01f35-108">하지만 VM의 세대는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-108">But you can't change a VM's generation.</span></span> <span data-ttu-id="01f35-109">자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 합니까?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01f35-109">For more information, see [Should I create a generation 1 or 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>

<span data-ttu-id="01f35-110">Azure VM에 대 한 hello 지원 정책에 대 한 자세한 내용은 참조 [Microsoft Azure Vm에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-110">For more information about hello support policy for Azure VM, see [Microsoft server software support for Microsoft Azure VMs](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).</span></span>

> [!Note]
> <span data-ttu-id="01f35-111">이 문서의 지침 hello toohello 64 비트 버전의 Windows Server 2008 R2 및 이후 Windows server 운영 체제 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-111">hello instructions in this article apply toohello 64-bit version of Windows Server 2008 R2 and later Windows server operating system.</span></span> <span data-ttu-id="01f35-112">Azure에서 실행 중인 32비트 버전 운영 체제에 대한 정보는 [Azure 가상 컴퓨터에서 32비트 운영 체제 지원](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01f35-112">For information about running 32-bit version of operating system in Azure, see [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).</span></span>

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a><span data-ttu-id="01f35-113">가상 디스크 tooVHD hello와 고정된 크기 디스크 변환</span><span class="sxs-lookup"><span data-stu-id="01f35-113">Convert hello virtual disk tooVHD and fixed size disk</span></span> 
<span data-ttu-id="01f35-114">Tooconvert 필요한 경우 가상 디스크 toohello 형식 Azure를 사용 하 여가이 섹션의 hello 방법 중 하나에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-114">If you need tooconvert your virtual disk toohello required format for Azure, use one of hello methods in this section.</span></span> <span data-ttu-id="01f35-115">Hello 가상 디스크의 변환 프로세스를 실행 하 고 Windows VHD hello 로컬 서버에서 제대로 작동 하는 hello 있는지 확인 하기 전에 VM hello를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-115">Back up hello VM before you run hello virtual disk conversion process and make sure that hello Windows VHD works correctly on hello local server.</span></span> <span data-ttu-id="01f35-116">Tooconvert 시도 하거나 tooAzure 업로드 하기 전에 hello VM 자체 내에서 모든 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-116">Resolve any errors within hello VM itself before you try tooconvert or upload it tooAzure.</span></span>

<span data-ttu-id="01f35-117">Hello 디스크를 변환한 후 변환 하는 hello 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-117">After you convert hello disk, create a VM that uses hello converted disk.</span></span> <span data-ttu-id="01f35-118">시작 하 고 업로드에 대 한 hello VM 준비 toohello VM toofinish에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-118">Start and sign in toohello VM toofinish preparing hello VM for upload.</span></span>

### <a name="convert-disk-using-hyper-v-manager"></a><span data-ttu-id="01f35-119">Hyper-V 관리자를 사용하여 디스크 변환</span><span class="sxs-lookup"><span data-stu-id="01f35-119">Convert disk using Hyper-V Manager</span></span>
1. <span data-ttu-id="01f35-120">Hyper-v 관리자를 열고 hello 왼쪽에 로컬 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-120">Open Hyper-V Manager and select your local computer on hello left.</span></span> <span data-ttu-id="01f35-121">Hello hello 컴퓨터 목록 위의 메뉴에서 **동작** > **디스크 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-121">In hello menu above hello computer list, click **Action** > **Edit Disk**.</span></span>
2. <span data-ttu-id="01f35-122">Hello에 **가상 하드 디스크 찾기** 화면을 찾아서 가상 디스크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-122">On hello **Locate Virtual Hard Disk** screen, locate and select your virtual disk.</span></span>
3. <span data-ttu-id="01f35-123">Hello에 **작업 선택** 화면에서 선택한 후 **변환** 및 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-123">On hello **Choose Action** screen, and then select **Convert** and **Next**.</span></span>
4. <span data-ttu-id="01f35-124">Tooconvert VHDX에서 필요한 경우에 선택 **VHD** 클릭 하 고 **다음**</span><span class="sxs-lookup"><span data-stu-id="01f35-124">If you need tooconvert from VHDX, select **VHD** and then click **Next**</span></span>
5. <span data-ttu-id="01f35-125">동적 확장 디스크에서 tooconvert 필요한 경우에 선택 **고정 크기** 클릭 하 고 **다음**</span><span class="sxs-lookup"><span data-stu-id="01f35-125">If you need tooconvert from a dynamically expanding disk, select **Fixed size** and then click **Next**</span></span>
6. <span data-ttu-id="01f35-126">찾아 경로 toosave hello 새 VHD 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-126">Locate and select a path toosave hello new VHD file to.</span></span>
7. <span data-ttu-id="01f35-127">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-127">Click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="01f35-128">이 문서의 hello 명령은 관리자 권한 PowerShell 세션에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-128">hello commands in this article must be run on an elevated PowerShell session.</span></span>

### <a name="convert-disk-by-using-powershell"></a><span data-ttu-id="01f35-129">PowerShell을 사용한 디스크 변환</span><span class="sxs-lookup"><span data-stu-id="01f35-129">Convert disk by using PowerShell</span></span>
<span data-ttu-id="01f35-130">Hello를 사용 하 여 가상 디스크를 변환할 수 [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) Windows PowerShell에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-130">You can convert a virtual disk by using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) command in Windows PowerShell.</span></span> <span data-ttu-id="01f35-131">PowerShell을 시작할 때 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-131">Select **Run as administrator** when you start PowerShell.</span></span> 

<span data-ttu-id="01f35-132">hello 다음 예제 명령은 VHDX tooVHD에서 인스턴스 간에 변환 동적 확장 디스크 toofixed-크기:</span><span class="sxs-lookup"><span data-stu-id="01f35-132">hello following example command converts from VHDX tooVHD, and from a dynamically expanding disk toofixed-size:</span></span>

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
<span data-ttu-id="01f35-133">이 명령에 대 한 hello 값을 대체 "-경로" hello 경로 toohello 가상 하드 디스크를 원하는 tooconvert 및 hello 값에 대 한 "-DestinationPath" hello 새 경로 및 이름 hello로 디스크를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-133">In this command, replace hello value for "-Path" with hello path toohello virtual hard disk that you want tooconvert and hello value for "-DestinationPath" with hello new path and name of hello converted disk.</span></span>

### <a name="convert-from-vmware-vmdk-disk-format"></a><span data-ttu-id="01f35-134">VMware VMDK 디스크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="01f35-134">Convert from VMware VMDK disk format</span></span>
<span data-ttu-id="01f35-135">Windows VM 이미지를 hello에 있는 경우 [VMDK 파일 형식](https://en.wikipedia.org/wiki/VMDK), hello를 사용 하 여 tooa VHD 변환 [Microsoft VM 변환기](https://www.microsoft.com/download/details.aspx?id=42497)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-135">If you have a Windows VM image in hello [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it tooa VHD by using hello [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span></span> <span data-ttu-id="01f35-136">자세한 내용은 hello 블로그 게시물을 참조 하십시오. [어떻게 tooConvert VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-136">For more information, see hello blog article [How tooConvert a VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span></span>

## <a name="set-windows-configurations-for-azure"></a><span data-ttu-id="01f35-137">Azure에 대한 Windows 구성 설정</span><span class="sxs-lookup"><span data-stu-id="01f35-137">Set Windows configurations for Azure</span></span>

<span data-ttu-id="01f35-138">VM hello hello 다음에서 모든 명령을 실행 하는 tooupload tooAzure 단계에서 한 [관리자 권한 명령 프롬프트 창을](https://technet.microsoft.com/library/cc947813.aspx):</span><span class="sxs-lookup"><span data-stu-id="01f35-138">On hello VM that you plan tooupload tooAzure, run all commands in hello following steps from an [elevated Command Prompt window](https://technet.microsoft.com/library/cc947813.aspx):</span></span>

1. <span data-ttu-id="01f35-139">Hello 라우팅 테이블에 모든 정적 영구 경로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-139">Remove any static persistent route on hello routing table:</span></span>
   
   * <span data-ttu-id="01f35-140">실행 tooview hello 경로 테이블 `route print` hello 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-140">tooview hello route table, run `route print` at hello command prompt.</span></span>
   * <span data-ttu-id="01f35-141">Hello 확인 **지 속성 경로** 섹션.</span><span class="sxs-lookup"><span data-stu-id="01f35-141">Check hello **Persistence Routes** sections.</span></span> <span data-ttu-id="01f35-142">사용 하 여 일관 된 경로 이면 [경로 삭제](https://technet.microsoft.com/library/cc739598.apx) tooremove 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-142">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) tooremove it.</span></span>
2. <span data-ttu-id="01f35-143">Hello WinHTTP 프록시를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-143">Remove hello WinHTTP proxy:</span></span>
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. <span data-ttu-id="01f35-144">너무 hello 디스크 SAN 정책을 설정[Onlineall](https://technet.microsoft.com/library/gg252636.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-144">Set hello disk SAN policy too[Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span></span> 
   
    ```PowerShell
    diskpart 
    ```
    <span data-ttu-id="01f35-145">Hello open 명령 프롬프트 창에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-145">In hello open Command Prompt window, type hello following commands:</span></span>

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. <span data-ttu-id="01f35-146">Windows에 대 한 utc (협정 세계시) 시간을 설정 하 고 hello (w32time) Windows 시간 서비스의 시작 유형을 너무 hello**자동으로**:</span><span class="sxs-lookup"><span data-stu-id="01f35-146">Set Coordinated Universal Time (UTC) time for Windows and hello startup type of hello Windows Time (w32time) service too**Automatically**:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. <span data-ttu-id="01f35-147">Hello 전원 프로필 toohello 설정 **고성능**:</span><span class="sxs-lookup"><span data-stu-id="01f35-147">Set hello power profile toohello **High Performance**:</span></span>

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a><span data-ttu-id="01f35-148">Windows 서비스의 hello 확인</span><span class="sxs-lookup"><span data-stu-id="01f35-148">Check hello Windows services</span></span>
<span data-ttu-id="01f35-149">각 Windows 서비스를 수행 하는 hello toohello 설정 되어 있는지 확인 **Windows 기본값**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-149">Make sure that each of hello following Windows services is set toohello **Windows default values**.</span></span> <span data-ttu-id="01f35-150">이들은 hello toomake 해당 hello VM에 연결 되어 있는지를 설정 해야 하는 서비스의 최소 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-150">These are hello minimum numbers of services that must be set up toomake sure that hello VM has connectivity.</span></span> <span data-ttu-id="01f35-151">tooreset hello 시작 설정, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-151">tooreset hello startup settings, run hello following commands:</span></span>
   
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

## <a name="update-remote-desktop-registry-settings"></a><span data-ttu-id="01f35-152">원격 데스크톱 레지스트리 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="01f35-152">Update Remote Desktop registry settings</span></span>
<span data-ttu-id="01f35-153">원격 데스크톱 연결에 대 한 설정에 따라 해당 hello 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-153">Make sure that hello following settings are configured correctly for remote desktop connection:</span></span>

>[!Note] 
><span data-ttu-id="01f35-154">Hello를 실행할 때 오류 메시지가 나타날 수 있습니다 **Set-itemproperty-경로 ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal 서비스-이름 &lt;개체 이름&gt; &lt;값&gt;** 다음이 단계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-154">You may receive an error message when you run hello **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;object name&gt; &lt;value&gt;** in these steps.</span></span> <span data-ttu-id="01f35-155">hello 오류 메시지는 무시 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-155">hello error message can be safely ignored.</span></span> <span data-ttu-id="01f35-156">해당 hello 도메인은 그룹 정책 개체를 통해 해당 구성을 보내지 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-156">It means only that hello domain is not pushing that configuration through a Group Policy object.</span></span>
>
>

1. <span data-ttu-id="01f35-157">RDP(원격 데스크톱 프로토콜)이 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-157">Remote Desktop Protocol (RDP) is enabled:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. <span data-ttu-id="01f35-158">hello RDP 포트가 제대로 설정 (기본 포트 3389):</span><span class="sxs-lookup"><span data-stu-id="01f35-158">hello RDP port is set up correctly (Default port 3389):</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    <span data-ttu-id="01f35-159">VM을 배포할 때 포트 3389에 대해 hello 기본 규칙 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-159">When you deploy a VM, hello default rules are created against port 3389.</span></span> <span data-ttu-id="01f35-160">Toochange hello 포트 번호를 수행 하는 hello VM이 Azure에 배포 된 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-160">If you want toochange hello port number,  do that after hello VM is deployed in Azure.</span></span>

3. <span data-ttu-id="01f35-161">hello 수신기가 모든 네트워크 인터페이스에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-161">hello listener is listening in every network interface:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. <span data-ttu-id="01f35-162">Hello RDP 연결에 대 한 hello 네트워크 수준 인증 모드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-162">Configure hello Network Level Authentication mode for hello RDP connections:</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. <span data-ttu-id="01f35-163">Hello 유지 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-163">Set hello keep-alive value：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. <span data-ttu-id="01f35-164">다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-164">Reconnect：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. <span data-ttu-id="01f35-165">Hello 동시 연결 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-165">Limit hello number of concurrent connections：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. <span data-ttu-id="01f35-166">자체 서명 된 인증서 toohello RDP 수신기 연결 되어 있는 경우 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-166">If there are any self-signed certificates tied toohello RDP listener, remove them:</span></span>
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    <span data-ttu-id="01f35-167">이 hello VM을 배포할 때 hello 시작 부분에 연결할 수 있는지 toomake입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-167">This is toomake sure that you can connect at hello beginning when you deploy hello VM.</span></span> <span data-ttu-id="01f35-168">또한에서 검토할 수 있습니다이 이후 단계 후 필요한 경우 Azure에서 VM을 배포 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-168">You can also review this on a later stage after hello VM is deployed in Azure if needed.</span></span>

9. <span data-ttu-id="01f35-169">Hello VM 도메인의 일부가 인 경우 모든 hello 설정을 toomake hello 이전 설정은 되돌려지지 않습니다 있는지 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-169">If hello VM will be part of a Domain, check all hello following settings toomake sure that hello former settings are not reverted.</span></span> <span data-ttu-id="01f35-170">확인 해야 하는 hello 정책을 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-170">hello policies that must be checked are hello following:</span></span>
    
    - <span data-ttu-id="01f35-171">RDP 활성화됨:</span><span class="sxs-lookup"><span data-stu-id="01f35-171">RDP is enabled:</span></span>

         <span data-ttu-id="01f35-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="01f35-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span>
         
         <span data-ttu-id="01f35-173">**원격 데스크톱을 사용 하 여 사용자가 tooconnect를 원격으로 허용**</span><span class="sxs-lookup"><span data-stu-id="01f35-173">**Allow users tooconnect remotely by using Remote Desktop**</span></span>

    - <span data-ttu-id="01f35-174">NLA 그룹 정책:</span><span class="sxs-lookup"><span data-stu-id="01f35-174">NLA group policy:</span></span>

        <span data-ttu-id="01f35-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span><span class="sxs-lookup"><span data-stu-id="01f35-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span></span> 
        
        <span data-ttu-id="01f35-176">**네트워크 수준 인증을 사용한 원격 연결에 대해 사용자 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="01f35-176">**Require user Authentication for remote connections by using Network Level Authentication**</span></span>
    
    - <span data-ttu-id="01f35-177">연결 유지 설정:</span><span class="sxs-lookup"><span data-stu-id="01f35-177">Keep Alive settings:</span></span>

        <span data-ttu-id="01f35-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="01f35-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="01f35-179">**연결 유지 연결 간격 구성**</span><span class="sxs-lookup"><span data-stu-id="01f35-179">**Configure keep-alive connection interval**</span></span>

    - <span data-ttu-id="01f35-180">다시 연결 설정:</span><span class="sxs-lookup"><span data-stu-id="01f35-180">Reconnect settings:</span></span>

        <span data-ttu-id="01f35-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="01f35-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="01f35-182">**자동 다시 연결**</span><span class="sxs-lookup"><span data-stu-id="01f35-182">**Automatic reconnection**</span></span>

    - <span data-ttu-id="01f35-183">연결 설정의 hello 수 제한:</span><span class="sxs-lookup"><span data-stu-id="01f35-183">Limit hello number of connections settings:</span></span>

        <span data-ttu-id="01f35-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span><span class="sxs-lookup"><span data-stu-id="01f35-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="01f35-185">**연결 수 제한**</span><span class="sxs-lookup"><span data-stu-id="01f35-185">**Limit number of connections**</span></span>

## <a name="configure-windows-firewall-rules"></a><span data-ttu-id="01f35-186">Windows 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="01f35-186">Configure Windows Firewall rules</span></span>
1. <span data-ttu-id="01f35-187">세 hello 프로필 (도메인, Standard 및 공용)에서 Windows 방화벽을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-187">Turn on Windows Firewall on hello three profiles (Domain, Standard, and Public):</span></span>

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. <span data-ttu-id="01f35-188">Hello 다음 (도메인, 개인 및 공용) hello 3 개의 방화벽 프로필을 통해 PowerShell tooallow WinRM에서에서 명령을 실행 하 고 hello PowerShell 원격 서비스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-188">Run hello following command in PowerShell tooallow WinRM through hello three firewall profiles (Domain, Private, and Public) and enable hello PowerShell Remote service:</span></span>
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. <span data-ttu-id="01f35-189">다음 방화벽 규칙 tooallow hello RDP 트래픽 hello를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="01f35-189">Enable hello following firewall rules tooallow hello RDP traffic</span></span> 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. <span data-ttu-id="01f35-190">Hello VM 응답할 수 있도록 hello 가상 네트워크 내 tooa ping 명령을 hello 파일 및 프린터 공유 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-190">Enable hello File and Printer Sharing rule so that hello VM can respond tooa ping command inside hello Virtual Network:</span></span>

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. <span data-ttu-id="01f35-191">Hello VM 도메인의 일부가 인 경우 hello 설정을 toomake hello 이전 설정은 되돌려지지 않습니다 있는지 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-191">If hello VM  will be part of a Domain, check hello following settings toomake sure that hello former settings are not reverted.</span></span> <span data-ttu-id="01f35-192">확인 해야 하는 hello AD 정책을 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-192">hello AD policies that must be checked are hello following:</span></span>

    - <span data-ttu-id="01f35-193">Hello Windows 방화벽 프로필을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="01f35-193">Enable hello Windows Firewall profiles</span></span>

        <span data-ttu-id="01f35-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **모든 네트워크 연결 보호**</span><span class="sxs-lookup"><span data-stu-id="01f35-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Protect all network connections**</span></span>

       <span data-ttu-id="01f35-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **모든 네트워크 연결 보호**</span><span class="sxs-lookup"><span data-stu-id="01f35-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Protect all network connections**</span></span>

    - <span data-ttu-id="01f35-196">RDP를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="01f35-196">Enable RDP</span></span> 

        <span data-ttu-id="01f35-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="01f35-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

        <span data-ttu-id="01f35-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **인바운드 원격 데스크톱 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="01f35-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

    - <span data-ttu-id="01f35-199">ICMP-V4를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="01f35-199">Enable ICMP-V4</span></span>

        <span data-ttu-id="01f35-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **ICMP 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="01f35-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

        <span data-ttu-id="01f35-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **ICMP 예외 허용**</span><span class="sxs-lookup"><span data-stu-id="01f35-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a><span data-ttu-id="01f35-202">VM이 정상 상태이고 안전하며 RDP로 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="01f35-202">Verify VM is healthy, secure, and accessible with RDP</span></span> 
1. <span data-ttu-id="01f35-203">toomake 있는지 hello 디스크가 정상 상태이 고 일관 된 hello 다음 VM 다시 시작 시 검사 디스크 작업을 실행:</span><span class="sxs-lookup"><span data-stu-id="01f35-203">toomake sure hello disk is healthy and consistent, run a check disk operation at hello next VM restart:</span></span>

    ```PowerShell
    Chkdsk /f
    ```
    <span data-ttu-id="01f35-204">Hello  명확 하 고 정상 디스크 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-204">Make sure that hello report shows a clean and healthy disk.</span></span>

2. <span data-ttu-id="01f35-205">Hello 데이터 BCD (부팅 구성) 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-205">Set hello Boot Configuration Data (BCD) settings.</span></span> 

    > [!Note]
    > <span data-ttu-id="01f35-206">이러한 명령을 PowerShell이 **아닌** 관리자 권한 CMD 창에서 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-206">Make sure you run these commands on an elevated CMD window and **NOT** on PowerShell:</span></span>
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. <span data-ttu-id="01f35-207">일관성이 해당 hello Windows 관리 Instrumentations 리포지토리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-207">Verify that hello Windows Management Instrumentations repository is consistent.</span></span> <span data-ttu-id="01f35-208">tooperform 다음 명령이 실행된이, hello:</span><span class="sxs-lookup"><span data-stu-id="01f35-208">tooperform this, run hello following command:</span></span>

    ```PowerShell
    winmgmt /verifyrepository
    ```
    <span data-ttu-id="01f35-209">Hello 저장소 손상 된 경우 참조 [WMI: 저장소 손상 여부](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-209">If hello repository is corrupted, see [WMI: Repository Corruption, or Not](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).</span></span>

4. <span data-ttu-id="01f35-210">다른 모든 응용 프로그램 hello 포트 3389를 사용 하지 않는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-210">Make sure that any other application is not using hello port 3389.</span></span> <span data-ttu-id="01f35-211">이 포트는 hello Azure의 RDP 서비스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-211">This port is used for hello RDP service in Azure.</span></span> <span data-ttu-id="01f35-212">실행할 수 있습니다 **netstat-anob** toosee 사용 되는 포트에 hello VM에서:</span><span class="sxs-lookup"><span data-stu-id="01f35-212">You can run **netstat -anob** toosee which ports are in used on hello VM:</span></span>

    ```PowerShell
    netstat -anob
    ```

5. <span data-ttu-id="01f35-213">Hello tooupload 되도록 Windows VHD 도메인 컨트롤러인 경우에 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-213">If hello Windows VHD that you want tooupload is a domain controller, then follow these steps:</span></span>

    <span data-ttu-id="01f35-214">A.</span><span class="sxs-lookup"><span data-stu-id="01f35-214">A.</span></span> <span data-ttu-id="01f35-215">에 따라 [이러한 추가 단계](https://support.microsoft.com/kb/2904015) tooprepare hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="01f35-215">Follow [these extra steps](https://support.microsoft.com/kb/2904015) tooprepare hello disk.</span></span>

    <span data-ttu-id="01f35-216">B.</span><span class="sxs-lookup"><span data-stu-id="01f35-216">B.</span></span> <span data-ttu-id="01f35-217">Toostart hello VM DSRM에서 특정 시점에 있을 경우 hello DSRM 암호를 알고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-217">Make sure that you know hello DSRM password in case you have toostart hello VM in DSRM at some point.</span></span> <span data-ttu-id="01f35-218">Toorefer toothis tooset hello를 연결 하는 것이 좋습니다 [DSRM 암호](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-218">You may want toorefer toothis link tooset hello [DSRM password](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).</span></span>

6. <span data-ttu-id="01f35-219">Tooyou hello 기본 제공 관리자 계정 및 암호 정상 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-219">Make sure that hello Built-in Administrator account and password are known tooyou.</span></span> <span data-ttu-id="01f35-220">Hello RDP 연결을 통해 tooWindows에이 계정을 toosign를 사용할 수 있는지 확인 하 고 tooreset hello 현재 로컬 관리자 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-220">You may want tooreset hello current local administrator password and make sure that you can use this account toosign in tooWindows through hello RDP connection.</span></span> <span data-ttu-id="01f35-221">이 액세스 권한은 hello "로그온 허용 원격 데스크톱 서비스를 통해" 그룹 정책 개체에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-221">This access permission is controlled by hello "Allow log on through Remote Desktop Services" Group Policy object.</span></span> <span data-ttu-id="01f35-222">Hello 로컬 그룹 정책 편집기에서에서이 개체를 볼 수 있습니다에서:</span><span class="sxs-lookup"><span data-stu-id="01f35-222">You can view this object in hello Local Group Policy Editor under:</span></span>

    <span data-ttu-id="01f35-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span><span class="sxs-lookup"><span data-stu-id="01f35-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span></span>

7. <span data-ttu-id="01f35-224">다음 AD hello 정책을 toomake RDP를 통해 또는 hello 네트워크에서 RDP 액세스를 차단 하지 않는지 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-224">Check hello following AD polices toomake sure that you are not blocking your RDP access through RDP nor from hello network:</span></span>

    - <span data-ttu-id="01f35-225">Hello 네트워크에서 컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 Assignment\Deny 액세스 toothis 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="01f35-225">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access toothis computer from hello network</span></span>

    - <span data-ttu-id="01f35-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span><span class="sxs-lookup"><span data-stu-id="01f35-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span></span>


8. <span data-ttu-id="01f35-227">Windows가 아직 정상 상태가 되었는지 다시 시작 hello VM toomake hello RDP 연결을 사용 하 여 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-227">Restart hello VM toomake sure that Windows is still healthy can be reached by using hello RDP connection.</span></span> <span data-ttu-id="01f35-228">이 시점에서 수 있습니다 toocreate VM에서 사용자 로컬 Hyper-v toomake 있는지 hello VM이 완전히 시작 중임을 다음 RDP 연결할 수 인지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-228">At this point, you may want toocreate a VM in your local Hyper-V toomake sure hello VM is starting completely and then test whether it is RDP reachable.</span></span>

9. <span data-ttu-id="01f35-229">TCP 패킷 또는 추가 방화벽을 분석하는 소프트웨어와 같은 추가 전송 드라이버 인터페이스 필터를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-229">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets or extra firewalls.</span></span> <span data-ttu-id="01f35-230">또한에서 검토할 수 있습니다이 이후 단계 후 필요한 경우 Azure에서 VM을 배포 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-230">You can also review this on a later stage after hello VM is deployed in Azure if needed.</span></span>

10. <span data-ttu-id="01f35-231">제 3 자 소프트웨어 및 관련된 toophysical 구성 요소 또는 다른 가상화 기술 되는 드라이버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-231">Uninstall any other third-party software and driver that is related toophysical components or any other virtualization technology.</span></span>

### <a name="install-windows-updates"></a><span data-ttu-id="01f35-232">Windows 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="01f35-232">Install Windows Updates</span></span>
<span data-ttu-id="01f35-233">hello 이상적인 구성은 너무**hello hello 최신 버전에 있는 컴퓨터의 hello 패치 수준이**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-233">hello ideal configuration is too**have hello patch level of hello machine at hello latest**.</span></span> <span data-ttu-id="01f35-234">없는 경우 업데이트를 수행 하는 hello 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-234">If this is not possible, make sure that hello following updates are installed:</span></span>

|                       |                   |           |                                       <span data-ttu-id="01f35-235">최소 파일 버전 x64</span><span class="sxs-lookup"><span data-stu-id="01f35-235">Minimum file version x64</span></span>       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| <span data-ttu-id="01f35-236">구성 요소</span><span class="sxs-lookup"><span data-stu-id="01f35-236">Component</span></span>               | <span data-ttu-id="01f35-237">이진</span><span class="sxs-lookup"><span data-stu-id="01f35-237">Binary</span></span>            | <span data-ttu-id="01f35-238">Windows 7 및 Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="01f35-238">Windows 7 & Windows Server 2008 R2</span></span> | <span data-ttu-id="01f35-239">Windows 8 및 Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="01f35-239">Windows 8 & Windows Server 2012</span></span>             | <span data-ttu-id="01f35-240">Windows 8.1 및 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="01f35-240">Windows 8.1 & Windows Server 2012 R2</span></span> | <span data-ttu-id="01f35-241">Windows 10 & Windows Server 2016 RS1</span><span class="sxs-lookup"><span data-stu-id="01f35-241">Windows 10 & Windows Server 2016 RS1</span></span> | <span data-ttu-id="01f35-242">Windows 10 RS2</span><span class="sxs-lookup"><span data-stu-id="01f35-242">Windows 10 RS2</span></span>             |
| <span data-ttu-id="01f35-243">저장소</span><span class="sxs-lookup"><span data-stu-id="01f35-243">Storage</span></span>                 | <span data-ttu-id="01f35-244">disk.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-244">disk.sys</span></span>          | <span data-ttu-id="01f35-245">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-245">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="01f35-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span></span> | <span data-ttu-id="01f35-247">6.3.9600.18203 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="01f35-247">6.3.9600.18203 - KB3137061</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="01f35-248">storport.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-248">storport.sys</span></span>      | <span data-ttu-id="01f35-249">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-249">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span><span class="sxs-lookup"><span data-stu-id="01f35-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span></span> | <span data-ttu-id="01f35-251">6.3.9600.18573 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-251">6.3.9600.18573 - KB4022726</span></span>           | <span data-ttu-id="01f35-252">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-252">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="01f35-253">10.0.15063.332</span><span class="sxs-lookup"><span data-stu-id="01f35-253">10.0.15063.332</span></span>             |
|                         | <span data-ttu-id="01f35-254">ntfs.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-254">ntfs.sys</span></span>          | <span data-ttu-id="01f35-255">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-255">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span><span class="sxs-lookup"><span data-stu-id="01f35-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span></span> | <span data-ttu-id="01f35-257">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-257">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="01f35-258">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-258">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="01f35-259">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="01f35-259">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="01f35-260">Iologmsg.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-260">Iologmsg.dll</span></span>      | <span data-ttu-id="01f35-261">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-261">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-262">6.2.9200.16384 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="01f35-262">6.2.9200.16384 - KB2995387</span></span>                  | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="01f35-263">Classpnp.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-263">Classpnp.sys</span></span>      | <span data-ttu-id="01f35-264">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-264">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="01f35-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span></span> | <span data-ttu-id="01f35-266">6.3.9600.18334 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="01f35-266">6.3.9600.18334 - KB3172614</span></span>           | <span data-ttu-id="01f35-267">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-267">10.0.14393.953 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="01f35-268">Volsnap.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-268">Volsnap.sys</span></span>       | <span data-ttu-id="01f35-269">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-269">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span><span class="sxs-lookup"><span data-stu-id="01f35-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span></span> | <span data-ttu-id="01f35-271">6.3.9600.18265 - KB3145384</span><span class="sxs-lookup"><span data-stu-id="01f35-271">6.3.9600.18265 - KB3145384</span></span>           | -                                    | <span data-ttu-id="01f35-272">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-272">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-273">partmgr.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-273">partmgr.sys</span></span>       | <span data-ttu-id="01f35-274">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-274">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-275">6.2.9200.16681 - KB2877114</span><span class="sxs-lookup"><span data-stu-id="01f35-275">6.2.9200.16681 - KB2877114</span></span>                  | <span data-ttu-id="01f35-276">6.3.9600.17401 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="01f35-276">6.3.9600.17401 - KB3000850</span></span>           | <span data-ttu-id="01f35-277">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-277">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="01f35-278">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-278">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-279">volmgr.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-279">volmgr.sys</span></span>        |                                    |                                             |                                      |                                      | <span data-ttu-id="01f35-280">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-280">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-281">Volmgrx.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-281">Volmgrx.sys</span></span>       | <span data-ttu-id="01f35-282">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-282">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | <span data-ttu-id="01f35-283">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-283">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-284">Msiscsi.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-284">Msiscsi.sys</span></span>       | <span data-ttu-id="01f35-285">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-285">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-286">6.2.9200.21006 - KB2955163</span><span class="sxs-lookup"><span data-stu-id="01f35-286">6.2.9200.21006 - KB2955163</span></span>                  | <span data-ttu-id="01f35-287">6.3.9600.18624 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-287">6.3.9600.18624 - KB4022726</span></span>           | <span data-ttu-id="01f35-288">10.0.14393.1066 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-288">10.0.14393.1066 - KB4022715</span></span>          | <span data-ttu-id="01f35-289">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="01f35-289">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="01f35-290">Msdsm.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-290">Msdsm.sys</span></span>         | <span data-ttu-id="01f35-291">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-291">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-292">6.2.9200.21474 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="01f35-292">6.2.9200.21474 - KB3046101</span></span>                  | <span data-ttu-id="01f35-293">6.3.9600.18592 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-293">6.3.9600.18592 - KB4022726</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="01f35-294">Mpio.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-294">Mpio.sys</span></span>          | <span data-ttu-id="01f35-295">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-295">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-296">6.2.9200.21190 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="01f35-296">6.2.9200.21190 - KB3046101</span></span>                  | <span data-ttu-id="01f35-297">6.3.9600.18616 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-297">6.3.9600.18616 - KB4022726</span></span>           | <span data-ttu-id="01f35-298">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-298">10.0.14393.1198 - KB4022715</span></span>          | -                          |
|                         | <span data-ttu-id="01f35-299">Fveapi.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-299">Fveapi.dll</span></span>        | <span data-ttu-id="01f35-300">6.1.7601.23311 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-300">6.1.7601.23311 - KB3125574</span></span>         | <span data-ttu-id="01f35-301">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="01f35-301">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="01f35-302">6.3.9600.18294 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="01f35-302">6.3.9600.18294 - KB3172614</span></span>           | <span data-ttu-id="01f35-303">10.0.14393.576 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-303">10.0.14393.576 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="01f35-304">Fveapibase.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-304">Fveapibase.dll</span></span>    | <span data-ttu-id="01f35-305">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-305">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-306">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="01f35-306">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="01f35-307">6.3.9600.17415 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="01f35-307">6.3.9600.17415 - KB3172614</span></span>           | <span data-ttu-id="01f35-308">10.0.14393.206 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-308">10.0.14393.206 - KB4022715</span></span>           | -                          |
| <span data-ttu-id="01f35-309">네트워크</span><span class="sxs-lookup"><span data-stu-id="01f35-309">Network</span></span>                 | <span data-ttu-id="01f35-310">netvsc.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-310">netvsc.sys</span></span>        | -                                  | -                                           | -                                    | <span data-ttu-id="01f35-311">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-311">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="01f35-312">10.0.15063.250 - KB4020001</span><span class="sxs-lookup"><span data-stu-id="01f35-312">10.0.15063.250 - KB4020001</span></span> |
|                         | <span data-ttu-id="01f35-313">mrxsmb10.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-313">mrxsmb10.sys</span></span>      | <span data-ttu-id="01f35-314">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="01f35-314">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="01f35-315">6.2.9200.22108 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-315">6.2.9200.22108 - KB4022724</span></span>                  | <span data-ttu-id="01f35-316">6.3.9600.18603 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-316">6.3.9600.18603 - KB4022726</span></span>           | <span data-ttu-id="01f35-317">10.0.14393.479 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-317">10.0.14393.479 - KB4022715</span></span>           | <span data-ttu-id="01f35-318">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="01f35-318">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="01f35-319">mrxsmb20.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-319">mrxsmb20.sys</span></span>      | <span data-ttu-id="01f35-320">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="01f35-320">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="01f35-321">6.2.9200.21548 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-321">6.2.9200.21548 - KB4022724</span></span>                  | <span data-ttu-id="01f35-322">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-322">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="01f35-323">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-323">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="01f35-324">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="01f35-324">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="01f35-325">mrxsmb.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-325">mrxsmb.sys</span></span>        | <span data-ttu-id="01f35-326">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="01f35-326">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="01f35-327">6.2.9200.22074 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-327">6.2.9200.22074 - KB4022724</span></span>                  | <span data-ttu-id="01f35-328">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-328">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="01f35-329">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-329">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="01f35-330">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-330">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-331">tcpip.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-331">tcpip.sys</span></span>         | <span data-ttu-id="01f35-332">6.1.7601.23761 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="01f35-332">6.1.7601.23761 - KB4022722</span></span>         | <span data-ttu-id="01f35-333">6.2.9200.22070 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-333">6.2.9200.22070 - KB4022724</span></span>                  | <span data-ttu-id="01f35-334">6.3.9600.18478 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-334">6.3.9600.18478 - KB4022726</span></span>           | <span data-ttu-id="01f35-335">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-335">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="01f35-336">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="01f35-336">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="01f35-337">http.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-337">http.sys</span></span>          | <span data-ttu-id="01f35-338">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-338">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-339">6.2.9200.17285 - KB3042553</span><span class="sxs-lookup"><span data-stu-id="01f35-339">6.2.9200.17285 - KB3042553</span></span>                  | <span data-ttu-id="01f35-340">6.3.9600.18574 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-340">6.3.9600.18574 - KB4022726</span></span>           | <span data-ttu-id="01f35-341">10.0.14393.251 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-341">10.0.14393.251 - KB4022715</span></span>           | <span data-ttu-id="01f35-342">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="01f35-342">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="01f35-343">vmswitch.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-343">vmswitch.sys</span></span>      | <span data-ttu-id="01f35-344">6.1.7601.23727 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="01f35-344">6.1.7601.23727 - KB4022719</span></span>         | <span data-ttu-id="01f35-345">6.2.9200.22117 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-345">6.2.9200.22117 - KB4022724</span></span>                  | <span data-ttu-id="01f35-346">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-346">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="01f35-347">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-347">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="01f35-348">10.0.15063.138</span><span class="sxs-lookup"><span data-stu-id="01f35-348">10.0.15063.138</span></span>             |
| <span data-ttu-id="01f35-349">코어</span><span class="sxs-lookup"><span data-stu-id="01f35-349">Core</span></span>                    | <span data-ttu-id="01f35-350">ntoskrnl.exe</span><span class="sxs-lookup"><span data-stu-id="01f35-350">ntoskrnl.exe</span></span>      | <span data-ttu-id="01f35-351">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="01f35-351">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="01f35-352">6.2.9200.22170 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="01f35-352">6.2.9200.22170 - KB4022718</span></span>                  | <span data-ttu-id="01f35-353">6.3.9600.18696 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-353">6.3.9600.18696 - KB4022726</span></span>           | <span data-ttu-id="01f35-354">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-354">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="01f35-355">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="01f35-355">10.0.15063.483</span></span>             |
| <span data-ttu-id="01f35-356">원격 데스크톱 서비스</span><span class="sxs-lookup"><span data-stu-id="01f35-356">Remote Desktop Services</span></span> | <span data-ttu-id="01f35-357">rdpcorets.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-357">rdpcorets.dll</span></span>     | <span data-ttu-id="01f35-358">6.2.9200.21506 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="01f35-358">6.2.9200.21506 - KB4022719</span></span>         | <span data-ttu-id="01f35-359">6.2.9200.22104 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="01f35-359">6.2.9200.22104 - KB4022724</span></span>                  | <span data-ttu-id="01f35-360">6.3.9600.18619 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-360">6.3.9600.18619 - KB4022726</span></span>           | <span data-ttu-id="01f35-361">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-361">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="01f35-362">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-362">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-363">termsrv.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-363">termsrv.dll</span></span>       | <span data-ttu-id="01f35-364">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-364">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="01f35-365">6.2.9200.17048 - KB2973501</span><span class="sxs-lookup"><span data-stu-id="01f35-365">6.2.9200.17048 - KB2973501</span></span>                  | <span data-ttu-id="01f35-366">6.3.9600.17415 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="01f35-366">6.3.9600.17415 - KB3000850</span></span>           | <span data-ttu-id="01f35-367">10.0.14393.0 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-367">10.0.14393.0 - KB4022715</span></span>             | <span data-ttu-id="01f35-368">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="01f35-368">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="01f35-369">termdd.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-369">termdd.sys</span></span>        | <span data-ttu-id="01f35-370">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-370">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="01f35-371">win32k.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-371">win32k.sys</span></span>        | <span data-ttu-id="01f35-372">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="01f35-372">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="01f35-373">6.2.9200.22168 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="01f35-373">6.2.9200.22168 - KB4022718</span></span>                  | <span data-ttu-id="01f35-374">6.3.9600.18698 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="01f35-374">6.3.9600.18698 - KB4022726</span></span>           | <span data-ttu-id="01f35-375">10.0.14393.594 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="01f35-375">10.0.14393.594 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="01f35-376">rdpdd.dll</span><span class="sxs-lookup"><span data-stu-id="01f35-376">rdpdd.dll</span></span>         | <span data-ttu-id="01f35-377">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-377">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="01f35-378">rdpwd.sys</span><span class="sxs-lookup"><span data-stu-id="01f35-378">rdpwd.sys</span></span>         | <span data-ttu-id="01f35-379">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="01f35-379">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
| <span data-ttu-id="01f35-380">보안</span><span class="sxs-lookup"><span data-stu-id="01f35-380">Security</span></span>                | <span data-ttu-id="01f35-381">기한 tooWannaCrypt</span><span class="sxs-lookup"><span data-stu-id="01f35-381">Due tooWannaCrypt</span></span> | <span data-ttu-id="01f35-382">KB4012212</span><span class="sxs-lookup"><span data-stu-id="01f35-382">KB4012212</span></span>                          | <span data-ttu-id="01f35-383">KB4012213</span><span class="sxs-lookup"><span data-stu-id="01f35-383">KB4012213</span></span>                                   | <span data-ttu-id="01f35-384">KB4012213</span><span class="sxs-lookup"><span data-stu-id="01f35-384">KB4012213</span></span>                            | <span data-ttu-id="01f35-385">KB4012606</span><span class="sxs-lookup"><span data-stu-id="01f35-385">KB4012606</span></span>                            | <span data-ttu-id="01f35-386">KB4012606</span><span class="sxs-lookup"><span data-stu-id="01f35-386">KB4012606</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="01f35-387">KB4012216</span><span class="sxs-lookup"><span data-stu-id="01f35-387">KB4012216</span></span>                                   |                                      | <span data-ttu-id="01f35-388">KB4013198</span><span class="sxs-lookup"><span data-stu-id="01f35-388">KB4013198</span></span>                            | <span data-ttu-id="01f35-389">KB4013198</span><span class="sxs-lookup"><span data-stu-id="01f35-389">KB4013198</span></span>                  |
|                         |                   | <span data-ttu-id="01f35-390">KB4012215</span><span class="sxs-lookup"><span data-stu-id="01f35-390">KB4012215</span></span>                          | <span data-ttu-id="01f35-391">KB4012214</span><span class="sxs-lookup"><span data-stu-id="01f35-391">KB4012214</span></span>                                   | <span data-ttu-id="01f35-392">KB4012216</span><span class="sxs-lookup"><span data-stu-id="01f35-392">KB4012216</span></span>                            | <span data-ttu-id="01f35-393">KB4013429</span><span class="sxs-lookup"><span data-stu-id="01f35-393">KB4013429</span></span>                            | <span data-ttu-id="01f35-394">KB4013429</span><span class="sxs-lookup"><span data-stu-id="01f35-394">KB4013429</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="01f35-395">KB4012217</span><span class="sxs-lookup"><span data-stu-id="01f35-395">KB4012217</span></span>                                   |                                      | <span data-ttu-id="01f35-396">KB4013429</span><span class="sxs-lookup"><span data-stu-id="01f35-396">KB4013429</span></span>                            | <span data-ttu-id="01f35-397">KB4013429</span><span class="sxs-lookup"><span data-stu-id="01f35-397">KB4013429</span></span>                  |
       
### <span data-ttu-id="01f35-398">때 toouse sysprep<a id="step23"></a></span><span class="sxs-lookup"><span data-stu-id="01f35-398">When toouse sysprep <a id="step23"></a></span></span>    

<span data-ttu-id="01f35-399">Sysprep는 hello 시스템의 hello 설치를 다시 설정 됩니다 하는 "hello 초기 경험" 모든 개인 데이터를 제거 하 고 여러 구성 요소가 다시 설정 하 여를 제공 하는 windows 설치로 실행 될 수 있는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-399">Sysprep is a process that you could run into a windows installation that will reset hello installation of hello system and will provide an “out of hello box experience” by removing all personal data and resetting several components.</span></span> <span data-ttu-id="01f35-400">일반적으로 이렇게 하면 toocreate 하려는 경우 템플릿을 특정 구성에 있는 다른 여러 Vm을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-400">You typically do this if you want toocreate a template from which you can deploy several other VMs that have a specific configuration.</span></span> <span data-ttu-id="01f35-401">이를 **일반화된 이미지**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-401">This is called a **generalized image**.</span></span>

<span data-ttu-id="01f35-402">대신 하나 유일한 toocreate 하려는 경우 VM 한 디스크에서 toouse sysprep 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-402">If, instead, you want only toocreate one VM from one disk, you don’t have toouse sysprep.</span></span> <span data-ttu-id="01f35-403">이 경우에만 만들 수 있습니다 VM과 라고 하는 hello는 **특수 이미지**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-403">In this situation, you can just create hello VM from what is known as a **specialized image**.</span></span>

<span data-ttu-id="01f35-404">Toocreate 특수 한 디스크에서 VM 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은:</span><span class="sxs-lookup"><span data-stu-id="01f35-404">For more information about how toocreate a VM from a specialized disk, see:</span></span>

- [<span data-ttu-id="01f35-405">특수화된 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="01f35-405">Create a VM from a specialized disk</span></span>](create-vm-specialized.md)
- [<span data-ttu-id="01f35-406">특수화된 VHD 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="01f35-406">Create a VM from a specialized VHD disk</span></span>](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

<span data-ttu-id="01f35-407">Toocreate 일반화 된 이미지를 원하는 경우 toorun sysprep을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-407">If you want toocreate a generalized image, you need toorun sysprep.</span></span> <span data-ttu-id="01f35-408">Sysprep에 대 한 자세한 내용은 참조 [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-408">For more information about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> 

<span data-ttu-id="01f35-409">Windows 기반 컴퓨터에 설치된 모든 역할 또는 응용 프로그램이 이 일반화를 지원하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-409">Not every role or application that’s installed on a Windows-based computer supports this generalization.</span></span> <span data-ttu-id="01f35-410">이 절차를 실행, toohello 문서 toomake 있는지 다음을 참조 되기 전에 해당 컴퓨터의 해당 hello 역할 sysprep에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-410">So before you run this procedure, refer toohello following article toomake sure that hello role of that computer is supported by sysprep.</span></span> <span data-ttu-id="01f35-411">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01f35-411">For more information, [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

### <a name="steps-toogeneralize-a-vhd"></a><span data-ttu-id="01f35-412">단계 toogeneralize VHD</span><span class="sxs-lookup"><span data-stu-id="01f35-412">Steps toogeneralize a VHD</span></span>

>[!NOTE]
> <span data-ttu-id="01f35-413">다음 단계에 지정 된 hello로 sysprep.exe를 실행 한 후 VM hello 끈 수행 하지 다시 설정에서 Azure에서 이미지를 만들 때까지.</span><span class="sxs-lookup"><span data-stu-id="01f35-413">After you run sysprep.exe as specified  in hello following steps, turn off hello VM, and do not turn it back on until you create an image from it in Azure.</span></span>

1. <span data-ttu-id="01f35-414">Toohello Windows VM에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-414">Sign in toohello Windows VM.</span></span>
2. <span data-ttu-id="01f35-415">관리자 권한으로 **명령 프롬프트**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-415">Run **Command Prompt** as an administrator.</span></span> 
3. <span data-ttu-id="01f35-416">Hello 디렉터리를 변경 하려면: **%windir%\system32\sysprep**, 한 다음 실행 **sysprep.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-416">Change hello directory to: **%windir%\system32\sysprep**, and then run **sysprep.exe**.</span></span>
3. <span data-ttu-id="01f35-417">Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-417">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>

    ![시스템 준비 도구](media/prepare-for-upload-vhd-image/syspre.png)
4. <span data-ttu-id="01f35-419">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-419">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="01f35-420">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-420">Click **OK**.</span></span>
6. <span data-ttu-id="01f35-421">Sysprep이 완료 되 면 VM hello를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-421">When Sysprep completes, shut down hello VM.</span></span> <span data-ttu-id="01f35-422">사용 하지 마십시오 **다시 시작** tooshut hello VM 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-422">Do not use **Restart** tooshut down hello VM.</span></span>
7. <span data-ttu-id="01f35-423">이제 hello VHD가 준비 toobe 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-423">Now hello VHD is ready toobe uploaded.</span></span> <span data-ttu-id="01f35-424">Toocreate 일반화 된 디스크에서 VM 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [일반화 된 VHD를 업로드 하 고 Azure에서 새 Vm toocreate 사용](sa-upload-generalized.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-424">For more information about how toocreate a VM from a generalized disk, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](sa-upload-generalized.md).</span></span>


## <a name="complete-recommended-configurations"></a><span data-ttu-id="01f35-425">권장된 구성 완료</span><span class="sxs-lookup"><span data-stu-id="01f35-425">Complete recommended configurations</span></span>
<span data-ttu-id="01f35-426">다음 설정을 hello VHD 업로드 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-426">hello following settings do not affect VHD uploading.</span></span> <span data-ttu-id="01f35-427">단, 반드시 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-427">However, we strongly recommend that you configured them.</span></span>

* <span data-ttu-id="01f35-428">Hello 설치 [Azure Vm 에이전트](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-428">Install hello [Azure VMs Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="01f35-429">그런 다음 VM 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-429">Then you can enable VM extensions.</span></span> <span data-ttu-id="01f35-430">hello VM 확장을 수도 toouse RDP를 구성 하 여 vm 암호를 재설정 같은 있으며 등 hello 중요 한 기능을 대부분을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-430">hello VM extensions implement most of hello critical functionality that you might want toouse with your VMs such as resetting passwords, configuring RDP, and so on.</span></span> <span data-ttu-id="01f35-431">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01f35-431">For more information, see:</span></span>

    - [<span data-ttu-id="01f35-432">VM 에이전트 및 확장 - 1부</span><span class="sxs-lookup"><span data-stu-id="01f35-432">VM Agent and Extensions – Part 1</span></span>](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [<span data-ttu-id="01f35-433">VM 에이전트 및 확장 - 2부</span><span class="sxs-lookup"><span data-stu-id="01f35-433">VM Agent and Extensions – Part 2</span></span>](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* <span data-ttu-id="01f35-434">hello 덤프 로그 Windows 충돌 문제를 해결 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-434">hello Dump log can be helpful in troubleshooting Windows crash issues.</span></span> <span data-ttu-id="01f35-435">Hello 덤프 로그 수집을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-435">Enable hello Dump log collection:</span></span>
  
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
    <span data-ttu-id="01f35-436">표시 되 면이 문서의 단계를 hello 절차적 동안 모든 오류, hello 레지스트리 키 이미 존재 한다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-436">If you receive any errors during any of hello procedural steps in this article, this means that hello registry keys already exists.</span></span> <span data-ttu-id="01f35-437">이러한 상황에서 명령 대신 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-437">In this situation, use hello following commands instead:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  <span data-ttu-id="01f35-438">Azure의 hello VM을 만든 후에 hello "임시 드라이브" 볼륨 tooimprove 성능에 hello 페이지 파일을 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-438">After hello VM is created in Azure, we recommend that you put hello pagefile on hello ”Temporal drive” volume tooimprove performance.</span></span> <span data-ttu-id="01f35-439">이 작업은 다음과 같이 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-439">You can set up this as follows:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
<span data-ttu-id="01f35-440">연결 된 toohello VM이 있는 모든 데이터 디스크 이면 hello 임시 드라이브 볼륨의 드라이브 문자는 일반적으로 "4".</span><span class="sxs-lookup"><span data-stu-id="01f35-440">If there’s any data disk that is attached toohello VM, hello Temporal drive volume's drive letter is typically "D."</span></span> <span data-ttu-id="01f35-441">이 지정 hello 사용 가능한 드라이브 수 및 설정한 hello 설정에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f35-441">This designation could be different, depending on hello number of available drives and hello settings that you  make.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f35-442">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01f35-442">Next steps</span></span>
* [<span data-ttu-id="01f35-443">리소스 관리자 배포에 대 한 Windows VM 이미지 tooAzure 업로드</span><span class="sxs-lookup"><span data-stu-id="01f35-443">Upload a Windows VM image tooAzure for Resource Manager deployments</span></span>](upload-generalized-managed.md)

