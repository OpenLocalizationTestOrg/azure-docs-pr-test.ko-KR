---
title: "Linux 용 aaaAzure N 시리즈 드라이버 설치 | Microsoft Docs"
description: "어떻게 tooset Azure에서 Linux를 실행 하는 N 시리즈 Vm에 대 한 NVIDIA GPU 드라이버를"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="9ab25-103">Linux를 실행하는 N 시리즈 VM의 NVIDIA GPU 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="9ab25-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="9ab25-104">N 시리즈 Azure의 hello GPU 기능을 활용 tootake Linux를 실행 하는 Vm 설치 NVIDIA 그래픽 드라이버를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="9ab25-105">이 문서에서는 N 시리즈 VM을 배포한 후의 드라이버 설치 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="9ab25-106">[Windows VM](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 대한 드라이버 설치 정보도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="9ab25-107">N 시리즈 VM 사양, 저장소 용량 및 디스크 세부 정보는 [GPU Linux VM 크기](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab25-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="9ab25-108">NV VM용 GRID 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="9ab25-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="9ab25-109">NV Vm에서 tooinstall NVIDIA 그리드 드라이버 SSH 연결 tooeach VM을 확인 하 고 Linux 배포판에 대 한 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9ab25-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9ab25-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="9ab25-111">Hello 실행 `lspci` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-111">Run hello `lspci` command.</span></span> <span data-ttu-id="9ab25-112">Hello NVIDIA M60 카드 또는 카드 PCI 장치로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="9ab25-113">업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="9ab25-114">Hello NVIDIA 드라이버와 호환 되지 않는 hello Nouveau 커널 드라이버를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="9ab25-115">(만 사용 하 여 hello NVIDIA 드라이버 NV Vm.) toodo이에서 파일을 만들 `/etc/modprobe.d `라는 `nouveau.conf` 내용을 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="9ab25-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="9ab25-116">Hello VM을 다시 부팅 하 고 다시 연결.</span><span class="sxs-lookup"><span data-stu-id="9ab25-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="9ab25-117">X 서버를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="9ab25-118">다운로드 및 hello 그리드 드라이버 설치:</span><span class="sxs-lookup"><span data-stu-id="9ab25-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="9ab25-119">사용할지 toorun hello nvidia xconfig 유틸리티 tooupdate X 구성 파일 묻는 경우 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="9ab25-120">설치가 완료 된 후에 위치 /etc/nvidia//etc/nvidia/gridd.conf.template tooa 새 파일 gridd.conf 복사</span><span class="sxs-lookup"><span data-stu-id="9ab25-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="9ab25-121">Hello 너무 다음 추가`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="9ab25-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="9ab25-122">VM hello를 재부팅 하 고 tooverify hello 설치를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9ab25-123">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9ab25-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="9ab25-124">Hello 커널 및 DKMS 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="9ab25-125">Hello NVIDIA 드라이버와 호환 되지 않는 hello Nouveau 커널 드라이버를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="9ab25-126">(만 사용 하 여 hello NVIDIA 드라이버 NV Vm.) toodo이에서 파일을 만들 `/etc/modprobe.d `라는 `nouveau.conf` 내용을 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="9ab25-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="9ab25-127">Hello VM 다시 부팅 하 고 다시 연결 하 고, 설치 hello HYPER-V에 대해 최신 Linux 통합 서비스</span><span class="sxs-lookup"><span data-stu-id="9ab25-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="9ab25-128">Toohello VM을 다시 연결 하 고 hello 실행 `lspci` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="9ab25-129">Hello NVIDIA M60 카드 또는 카드 PCI 장치로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="9ab25-130">다운로드 및 hello 그리드 드라이버 설치:</span><span class="sxs-lookup"><span data-stu-id="9ab25-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="9ab25-131">사용할지 toorun hello nvidia xconfig 유틸리티 tooupdate X 구성 파일 묻는 경우 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="9ab25-132">설치가 완료 된 후에 위치 /etc/nvidia//etc/nvidia/gridd.conf.template tooa 새 파일 gridd.conf 복사</span><span class="sxs-lookup"><span data-stu-id="9ab25-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="9ab25-133">Hello 너무 다음 추가`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="9ab25-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="9ab25-134">VM hello를 재부팅 하 고 tooverify hello 설치를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="9ab25-135">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="9ab25-135">Verify driver installation</span></span>


<span data-ttu-id="9ab25-136">tooquery hello GPU 장치 상태, SSH toohello VM 및 실행된 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티 hello 드라이버와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="9ab25-137">유사한 toohello 다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-137">Output similar toohello following appears:</span></span>

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="9ab25-139">X11 서버</span><span class="sxs-lookup"><span data-stu-id="9ab25-139">X11 server</span></span>
<span data-ttu-id="9ab25-140">X11 해야 할 경우 원격 연결 tooan NV VM에 대 한 서버 [x11vnc](http://www.karlrunge.com/x11vnc/) 그래픽 하드웨어 가속 수 있기 때문에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="9ab25-141">hello hello M60 장치의 BusID 수동으로 추가 해야 toohello xconfig 파일 (`etc/X11/xorg.conf` Ubuntu 16.04 LTS에 `/etc/X11/XF86config` CentOS 7.3 또는 Red Hat Enterprise Server 7.3에).</span><span class="sxs-lookup"><span data-stu-id="9ab25-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="9ab25-142">추가 `"Device"` 비슷한 toohello 다음 섹션:</span><span class="sxs-lookup"><span data-stu-id="9ab25-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="9ab25-143">또한 업데이트 프로그램 `"Screen"` toouse이이 장치 섹션.</span><span class="sxs-lookup"><span data-stu-id="9ab25-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="9ab25-144">실행 하 여 hello BusID 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="9ab25-145">VM 다시 할당 하거나 다시 부팅 가져옵니다 hello BusID 변경 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="9ab25-146">따라서 VM 다시 부팅 될 때 toouse 스크립트 tooupdate hello BusID hello X11 구성에서 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="9ab25-147">예:</span><span class="sxs-lookup"><span data-stu-id="9ab25-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="9ab25-148">이 파일은 `/etc/rc.d/rc3.d`에서 이에 대한 항목을 만들면 부팅에 대한 루트로 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="9ab25-149">NC VM용 NVIDIA 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="9ab25-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="9ab25-150">Hello NVIDIA CUDA 도구 키트 8.0에서에서 Linux NC Vm에서 단계 tooinstall NVIDIA 드라이버는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="9ab25-151">C 및 c + + 개발자 수 필요에 따라 hello 전체 Toolkit toobuild GPU accelerated 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="9ab25-152">자세한 내용은 참조 hello [CUDA 설치 가이드](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="9ab25-153">여기에 제공된 CUDA 드라이버 다운로드 링크는 게시 시점에 최신 링크였습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="9ab25-154">최신 CUDA 드라이버 hello에 대 한 방문 hello [NVIDIA](http://www.nvidia.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="9ab25-155">tooinstall CUDA Toolkit SSH 연결 tooeach VM을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="9ab25-156">시스템 hello tooverify에 hello 다음 명령을 실행 CUDA 호환 GPU가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="9ab25-157">다음 예에서는 (NVIDIA 테슬라 K80 카드 표시 됨) 출력 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![lspci 명령 출력](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="9ab25-159">그런 다음 배포 관련 특정 설치 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9ab25-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9ab25-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="9ab25-161">다운로드 하 여 hello CUDA 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="9ab25-162">hello 설치는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="9ab25-163">toooptionally 설치 hello 완료 CUDA toolkit, 유형:</span><span class="sxs-lookup"><span data-stu-id="9ab25-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="9ab25-164">VM hello를 재부팅 하 고 tooverify hello 설치를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9ab25-165">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9ab25-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="9ab25-166">업데이트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="9ab25-167">Toohello VM을 다시 연결 하 고 설치 hello Hyper-v에 대 한 최신 Linux 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9ab25-168">NC24r VM에서 HPC CentOS 기반 이미지를 설치한 경우 tooStep 3을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="9ab25-169">Azure RDMA 드라이버 및 Linux 통합 서비스는 hello 이미지에 설치 되어 미리, LIS을 업그레이드할 수 없습니다, 및 커널 업데이트는 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="9ab25-170">Toohello VM을 다시 연결 하 고 다음 명령을 hello로 설치를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="9ab25-171">hello 설치는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="9ab25-172">toooptionally 설치 hello 완료 CUDA toolkit, 유형:</span><span class="sxs-lookup"><span data-stu-id="9ab25-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="9ab25-173">VM hello를 재부팅 하 고 tooverify hello 설치를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="9ab25-174">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="9ab25-174">Verify driver installation</span></span>


<span data-ttu-id="9ab25-175">tooquery hello GPU 장치 상태, SSH toohello VM 및 실행된 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티 hello 드라이버와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="9ab25-176">유사한 toohello 다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-176">Output similar toohello following appears:</span></span>

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="9ab25-178">CUDA 드라이버 업데이트</span><span class="sxs-lookup"><span data-stu-id="9ab25-178">CUDA driver updates</span></span>

<span data-ttu-id="9ab25-179">배포 후에 CUDA 드라이버를 정기적으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9ab25-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9ab25-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9ab25-181">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9ab25-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="9ab25-182">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9ab25-182">Troubleshooting</span></span>

* <span data-ttu-id="9ab25-183">Hello 4.4.0-75 Linux 커널을 16.04 Ubuntu LTS에서 실행 되는 Azure N 시리즈 Vm에서 CUDA 드라이버는 알려진된 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="9ab25-184">이전 커널 버전에서 업그레이드 하는 경우 업그레이드 tooat 최소 커널 버전 4.4.0-77 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="9ab25-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ab25-185">Next steps</span></span>

* <span data-ttu-id="9ab25-186">Hello N 시리즈 Vm에서 NVIDIA Gpu hello에 대 한 자세한 내용은 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="9ab25-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html)(Azure NC VM용)</span><span class="sxs-lookup"><span data-stu-id="9ab25-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="9ab25-188">[NVIDIA 테슬라 M60](http://www.nvidia.com/object/tesla-m60.html) (Azure NV VM 용)</span><span class="sxs-lookup"><span data-stu-id="9ab25-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="9ab25-189">toocapture Linux VM 이미지를 사용 하 여 설치 된 NVIDIA 드라이버와 함께 참조 [어떻게 toogeneralize 및 Linux 가상 컴퓨터를 캡처](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab25-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
