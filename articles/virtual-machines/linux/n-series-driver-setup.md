---
title: "Linux용 Azure N 시리즈 드라이버 설치 | Microsoft Docs"
description: "Azure에서 Linux를 실행하는 N 시리즈 VM의 NVIDIA GPU 드라이버를 설정하는 방법"
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
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="f20da-103">Linux를 실행하는 N 시리즈 VM의 NVIDIA GPU 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="f20da-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="f20da-104">Linux를 실행하는 Azure N 시리즈 VM의 GPU 기능을 이용하려면 지원되는 NVIDIA 그래픽 드라이버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="f20da-105">이 문서에서는 N 시리즈 VM을 배포한 후의 드라이버 설치 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="f20da-106">[Windows VM](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 대한 드라이버 설치 정보도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="f20da-107">N 시리즈 VM 사양, 저장소 용량 및 디스크 세부 정보는 [GPU Linux VM 크기](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20da-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="f20da-108">NV VM용 GRID 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="f20da-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="f20da-109">NVIDIA GRID 드라이버를 NV VM에 설치하려면 각 VM에 대한 SSH 연결을 확인하고 Linux 배포에 필요한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f20da-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f20da-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="f20da-111">`lspci` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-111">Run the `lspci` command.</span></span> <span data-ttu-id="f20da-112">NVIDIA M60 카드가 PCI 장치로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="f20da-113">업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="f20da-114">NVIDIA 드라이버와 호환되지 않는 Nouveau 커널 드라이버를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="f20da-115">(NV VM에서 NVIDIA 드라이버만 사용합니다.) 이를 수행하려면 다음 콘텐츠가 포함된 `nouveau.conf`라고 하는 `/etc/modprobe.d `에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="f20da-116">VM을 다시 부팅하고 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="f20da-117">X 서버를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="f20da-118">GRID 드라이버를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="f20da-119">X 구성 파일을 업데이트할 nvidia-xconfig 유틸리티를 실행할 것인지 여부를 묻는 메시지가 표시되면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="f20da-120">설치가 완료되면 /etc/nvidia/gridd.conf.template을 /etc/nvidia/ 위치의 새 파일 gridd.conf에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="f20da-121">다음 줄을 `/etc/nvidia/gridd.conf`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="f20da-122">VM 다시 부팅하고 계속해서 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f20da-123">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f20da-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="f20da-124">커널 및 DKMS를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="f20da-125">NVIDIA 드라이버와 호환되지 않는 Nouveau 커널 드라이버를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="f20da-126">(NV VM에서 NVIDIA 드라이버만 사용합니다.) 이를 수행하려면 다음 콘텐츠가 포함된 `nouveau.conf`라고 하는 `/etc/modprobe.d `에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="f20da-127">VM을 다시 부팅하고, 다시 연결한 후, Hyper-V에 대한 최신 Linux 통합 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="f20da-128">VM에 다시 연결하고 `lspci` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="f20da-129">NVIDIA M60 카드가 PCI 장치로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="f20da-130">GRID 드라이버를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="f20da-131">X 구성 파일을 업데이트할 nvidia-xconfig 유틸리티를 실행할 것인지 여부를 묻는 메시지가 표시되면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="f20da-132">설치가 완료되면 /etc/nvidia/gridd.conf.template을 /etc/nvidia/ 위치의 새 파일 gridd.conf에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="f20da-133">다음 줄을 `/etc/nvidia/gridd.conf`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="f20da-134">VM 다시 부팅하고 계속해서 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="f20da-135">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="f20da-135">Verify driver installation</span></span>


<span data-ttu-id="f20da-136">GPU 장치 상태를 쿼리하려면 VM에 대해 SSH를 실행하고 드라이버와 설치된 [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="f20da-137">그러면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-137">Output similar to the following appears:</span></span>

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="f20da-139">X11 서버</span><span class="sxs-lookup"><span data-stu-id="f20da-139">X11 server</span></span>
<span data-ttu-id="f20da-140">NV VM에 대한 원격 연결을 위해 X11 서버가 필요한 경우 그래픽의 하드웨어 가속화가 가능하기 때문에 [x11vnc](http://www.karlrunge.com/x11vnc/)가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="f20da-141">M60 장치의 BusID는 xconfig 파일에 수동으로 추가해야 합니다(Ubuntu 16.04 LTS의 `etc/X11/xorg.conf`, CentOS 7.3의 `/etc/X11/XF86config` 또는 Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="f20da-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="f20da-142">다음과 유사한 `"Device"` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="f20da-143">또한 `"Screen"` 섹션을 업데이트하여 이 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="f20da-144">실행하여 BusID를 찾을 수 있음</span><span class="sxs-lookup"><span data-stu-id="f20da-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="f20da-145">BusID는 VM이 다시 할당되거나 다시 부팅될 때를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="f20da-146">따라서 스크립트를 사용하여 VM이 다시 부팅될 때 X11 구성에서 BusID를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="f20da-147">예:</span><span class="sxs-lookup"><span data-stu-id="f20da-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="f20da-148">이 파일은 `/etc/rc.d/rc3.d`에서 이에 대한 항목을 만들면 부팅에 대한 루트로 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="f20da-149">NC VM용 NVIDIA 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="f20da-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="f20da-150">NVIDIA CUDA 도구 키트 8.0에서 Linux NC VM에 NVIDIA 드라이버를 설치하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="f20da-151">경우에 따라 C 및 C++ 개발자는 GPU 가속 응용 프로그램을 빌드하기 위해 전체 도구 키트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="f20da-152">자세한 내용은 [CUDA 설치 가이드](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20da-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="f20da-153">여기에 제공된 CUDA 드라이버 다운로드 링크는 게시 시점에 최신 링크였습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="f20da-154">최신 CUDA 드라이버에 대해서는 [NVIDIA](http://www.nvidia.com/) 웹 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20da-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="f20da-155">CUDA 도구 키트를 설치하려면 각 VM에 SSH 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="f20da-156">시스템에 CUDA 호환 GPU가 있는지 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="f20da-157">다음 예제와 비슷한 출력이 표시됩니다(NVIDIA Tesla K80 카드 표시).</span><span class="sxs-lookup"><span data-stu-id="f20da-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![lspci 명령 출력](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="f20da-159">그런 다음 배포 관련 특정 설치 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f20da-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f20da-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="f20da-161">CUDA 드라이버를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="f20da-162">설치에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="f20da-163">필요에 따라 전체 CUDA 도구 키트를 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="f20da-164">VM 다시 부팅하고 계속해서 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f20da-165">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f20da-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="f20da-166">업데이트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="f20da-167">VM에 다시 연결하고 Hyper-V에 대한 최신 Linux 통합 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f20da-168">NC24r VM에서 CentOS 기반 HPC 이미지를 설치한 경우 3단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="f20da-169">Azure RDMA 드라이버 및 Linux 통합 서비스는 이미지에 사전 설치되어 있으므로 LIS는 업그레이드하지 않아야 하며 커널 업데이트는 기본적으로 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="f20da-170">VM에 다시 연결하고 다음 명령을 사용하여 설치를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-170">Reconnect to the VM and continue installation with the following commands:</span></span>

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

  <span data-ttu-id="f20da-171">설치에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="f20da-172">필요에 따라 전체 CUDA 도구 키트를 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="f20da-173">VM 다시 부팅하고 계속해서 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="f20da-174">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="f20da-174">Verify driver installation</span></span>


<span data-ttu-id="f20da-175">GPU 장치 상태를 쿼리하려면 VM에 대해 SSH를 실행하고 드라이버와 설치된 [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="f20da-176">그러면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-176">Output similar to the following appears:</span></span>

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="f20da-178">CUDA 드라이버 업데이트</span><span class="sxs-lookup"><span data-stu-id="f20da-178">CUDA driver updates</span></span>

<span data-ttu-id="f20da-179">배포 후에 CUDA 드라이버를 정기적으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f20da-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f20da-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f20da-181">CentOS 기반 7.3 또는 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f20da-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="f20da-182">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f20da-182">Troubleshooting</span></span>

* <span data-ttu-id="f20da-183">Ubuntu 16.04 LTS에서 4.4.0-75 Linux 커널을 실행하는 Azure N 시리즈 VM의 CUDA 드라이버에 알려진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="f20da-184">이전 커널 버전에서 업그레이드하는 경우 커널 버전 4.4.0-77 이상으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="f20da-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="f20da-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f20da-185">Next steps</span></span>

* <span data-ttu-id="f20da-186">N 시리즈 VM의 NVIDIA GPU에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20da-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="f20da-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html)(Azure NC VM용)</span><span class="sxs-lookup"><span data-stu-id="f20da-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="f20da-188">[NVIDIA 테슬라 M60](http://www.nvidia.com/object/tesla-m60.html) (Azure NV VM 용)</span><span class="sxs-lookup"><span data-stu-id="f20da-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="f20da-189">설치한 NVIDIA 드라이버와 함께 Linux VM 이미지를 캡처하려면 [Linux 가상 컴퓨터를 일반화하고 캡처하는 방법](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20da-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
