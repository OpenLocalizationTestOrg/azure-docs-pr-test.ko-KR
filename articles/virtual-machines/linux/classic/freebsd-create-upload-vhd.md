---
title: "aaaCreate 및 업로드 FreeBSD VM 이미지 | Microsoft Docs"
description: "Toocreate 알아보고 hello FreeBSD 운영 체제 toocreate Azure 가상 컴퓨터를 포함 하는 가상 하드 디스크 (VHD)를 업로드 합니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="4309b-103">만들기 및 업로드 FreeBSD VHD tooAzure</span><span class="sxs-lookup"><span data-stu-id="4309b-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="4309b-104">이 문서에서는 어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello FreeBSD 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="4309b-105">를 업로드 한 후에 사용자 고유의 이미지 toocreate Azure에서 가상 컴퓨터 (VM)으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4309b-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4309b-107">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4309b-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4309b-109">Hello 리소스 관리자 모델을 사용 하 여 VHD를 업로드 하는 방법에 대 한 내용은 [여기](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4309b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4309b-110">Prerequisites</span></span>
<span data-ttu-id="4309b-111">이 문서에서는 다음 항목 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="4309b-112">**Azure 구독**- 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="4309b-113">MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4309b-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="4309b-114">그렇지 않은 경우 너무 방법을 알아보려면[무료 평가판 계정을 만들](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="4309b-115">**Azure PowerShell 도구**-hello Azure PowerShell 모듈을 설치 해야 하 고 toouse Azure 구독을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="4309b-116">toodownload hello 모듈 참조 [Azure 다운로드](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="4309b-117">에 대해 설명 하는 자습서는 어떻게 tooinstall 구성 및 여기 hello 모듈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="4309b-118">사용 하 여 hello [Azure 다운로드](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="4309b-119">**.Vhd 파일에 설치 된 FreeBSD 운영 체제**tooa 가상 하드 디스크-는 FreeBSD 운영 체제에서 지원 되는 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="4309b-120">여러 도구 toocreate.vhd 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="4309b-121">예를 들어 Hyper-v toocreate hello.vhd 파일 등 가상화 솔루션을 사용 하 고 hello 운영 체제를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="4309b-122">Tooinstall 및 Hyper-v를 사용 하 여 참조 하는 방법에 대 한 지침은 [Hyper-v 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4309b-123">Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="4309b-124">Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 cmdlet hello 수 [convert vhd](https://technet.microsoft.com/library/hh848454.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="4309b-125">또한는 [방법에 대 한 MSDN에서 자습서 toouse hyper-v FreeBSD](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="4309b-126">이 태스크는 다섯 단계를 수행 하는 hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="4309b-127">1 단계: 업로드에 대 한 hello 이미지 준비</span><span class="sxs-lookup"><span data-stu-id="4309b-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="4309b-128">Hello FreeBSD 운영 체제를 설치한 hello 가상 컴퓨터에서 다음 절차를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="4309b-129">DHCP를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="4309b-130">SSH를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-130">Enable SSH.</span></span>

    <span data-ttu-id="4309b-131">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="4309b-132">FreeBSD 디스크에서 설치 후에는 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="4309b-133">직렬 콘솔을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="4309b-134">sudo를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-134">Install sudo.</span></span>

    <span data-ttu-id="4309b-135">Azure의 hello 루트 계정이 비활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="4309b-136">즉, tooutilize sudo 상승 된 권한으로는 권한 없는 사용자 toorun 명령에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="4309b-137">Azure 에이전트에 대한 필수 조건.</span><span class="sxs-lookup"><span data-stu-id="4309b-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="4309b-138">Azure 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-138">Install Azure Agent.</span></span>

    <span data-ttu-id="4309b-139">hello hello Azure 에이전트의 최신 릴리스에 항상에 있습니다 [github](https://github.com/Azure/WALinuxAgent/releases)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="4309b-140">버전 2.0.10 hello + FreeBSD & 10.1, 버전과 10 hello 2.1.4 + (2.2. x 포함) 정식으로 지 원하는 FreeBSD 10.2 및 이상 릴리스를 공식적으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="4309b-141">2.0의 경우 2.0.16을 예로 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="4309b-142">2.1의 경우 2.1.4를 예로 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="4309b-143">Azure 에이전트를 설치한 후 실행 하는 것이 좋습니다 tooverify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="4309b-144">Hello 시스템을 프로 비전 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-144">Deprovision hello system.</span></span>

    <span data-ttu-id="4309b-145">프로 비전 해제 하 고 확인 시스템 tooclean hello 다시 프로 비전에 대 한 적합 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="4309b-146">hello 다음 명령은 삭제 hello 마지막 프로 비전 된 사용자 계정과 연결 된 hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="4309b-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="4309b-147">이제 VM을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="4309b-148">2단계: Azure에서 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4309b-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="4309b-149">사용 되는 toocreate 가상 컴퓨터를 사용할 수 있도록 해야 Azure tooupload.vhd 파일의에서 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="4309b-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="4309b-150">Hello Azure 클래식 포털 toocreate 저장소 계정 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="4309b-151">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4309b-152">Hello 명령 모음에서 선택 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="4309b-153">**데이터 서비스** > **저장소** > **빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![저장소 계정 빠른 생성](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="4309b-155">Hello 필드를 다음과 같이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="4309b-156">Hello에 **URL** 필드 hello 저장소 계정 URL에 하위 도메인 이름 toouse를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="4309b-157">hello 항목 3 ~ 24 숫자 및 소문자에서 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="4309b-158">이 이름은 사용 되는 tooaddress Azure Blob 저장소, Azure 큐 저장소 또는 Azure 테이블 저장소 리소스 hello 구독에 대 한 hello URL에서 hello 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="4309b-159">Hello에 **위치/선호도 그룹** 드롭 다운 메뉴에서 선택 hello **위치 또는 선호도 그룹** hello 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="4309b-160">선호도 그룹 hello에 클라우드 서비스 및 저장소를 배치 하면 동일한 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="4309b-161">Hello에 **복제** 필드, 결정 여부 toouse **지리적 중복** hello 저장소 계정에 대 한 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="4309b-162">지역에서 복제는 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="4309b-163">이 옵션에 데이터 tooa 보조 위치에 없는 비용 tooyou 복제, hello 기본 위치의 저장소 장애 toothat 위치 하는 경우 오류가 발생 한 조치를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="4309b-164">hello 보조 위치는 자동으로 할당 됩니다 및 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="4309b-165">기한 toolegal 요구 사항 또는 조직 구성 정책에 클라우드 기반 저장소의 hello 위치 보다 자세히 제어 해야 할 경우 지리적 복제를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="4309b-166">그러나 수는 나중에 지리적 복제를 설정 하는 경우 청구 됩니다 일회성 데이터 전송 요금이 tooreplicate 기존 데이터 toohello 보조 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="4309b-167">지역에서 복제를 사용하지 않는 저장소 서비스는 할인하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="4309b-168">저장소 계정의 지역에서 복제를 관리하는 방법에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/common/storage-redundancy.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![저장소 계정 세부 정보 입력](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="4309b-170">**저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="4309b-171">hello 계정 아래에 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-171">hello account now appears under **storage**.</span></span>

    ![저장소 계정을 성공적으로 만들었음](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="4309b-173">다음으로 업로드된 .vhd 파일의 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="4309b-174">Hello 저장소 계정 이름을 선택한 다음 선택 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="4309b-176">**컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-176">Select **Create a Container**.</span></span>

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="4309b-178">Hello에 **이름** 필드 컨테이너에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="4309b-179">그런 다음, hello **액세스** 드롭 다운 메뉴에서 원하는 액세스 정책의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![컨테이너 이름](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="4309b-181">기본적으로 hello 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="4309b-182">tooallow 공용 읽기 액세스 권한을 toohello blob을 hello 컨테이너 하지만 하지 toohello 컨테이너 속성과 메타 데이터를 사용 하 여 hello **공용 Blob** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="4309b-183">hello 컨테이너 및 blob를 사용 하 여 hello tooallow 전체 공용 읽기 권한 **공용 컨테이너** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="4309b-184">3 단계: hello 연결 tooAzure 준비</span><span class="sxs-lookup"><span data-stu-id="4309b-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="4309b-185">.Vhd 파일을 업로드 하려면 먼저 컴퓨터와 Azure 구독 간에 tooestablish 보안 연결이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="4309b-186">Hello Azure Active Directory (Azure AD) 메서드를 사용 하거나 인증서 메서드 toodo hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="4309b-187">Azure AD hello 메서드 tooupload.vhd 파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4309b-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="4309b-188">Azure PowerShell 콘솔을 열고 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="4309b-189">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="4309b-190">이 명령은 직장 또는 학교 계정으로 로그인할 수 있는 로그인 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell 창](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="4309b-192">Azure를 인증 하 고 hello 자격 증명 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="4309b-193">Hello 창이 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="4309b-194">Hello 인증서 메서드 tooupload.vhd 파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4309b-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="4309b-195">Azure PowerShell 콘솔을 열고 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="4309b-196">입력: `Get-AzurePublishSettingsFile`</span><span class="sxs-lookup"><span data-stu-id="4309b-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="4309b-197">브라우저 창이 열리고 toodownload hello.publishsettings 제출 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="4309b-198">이 파일에는 Azure 구독에 대한 정보와 인증서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![브라우저 다운로드 페이지](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="4309b-200">Hello.publishsettings 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="4309b-201">형식: `Import-AzurePublishSettingsFile <PathToFile>`여기서 `<PathToFile>` hello toohello.publishsettings 파일 전체 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="4309b-202">자세한 내용은 [Azure Cmdlets 시작](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4309b-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="4309b-203">설치 하 고 PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="4309b-204">4 단계: hello.vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4309b-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="4309b-205">Hello.vhd 파일을 업로드 하는 경우 Blob 저장소 내의 아무 곳 이나 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="4309b-206">다음은 몇 가지 용어 hello 파일을 업로드할 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="4309b-207">**BlobStorageURL** 2 단계에서에서 만든 hello 저장소 계정에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="4309b-208">**YourImagesFolder** 은 Blob 저장소 내의 컨테이너 hello toostore 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="4309b-209">**VHDName** hello Azure 클래식 포털 tooidentify hello 가상 하드 디스크에 표시 되는 hello 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="4309b-210">**PathToVHDFile** hello 전체 경로 및 hello.vhd 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="4309b-211">Hello 이전 단계에서 사용한 hello Azure PowerShell 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="4309b-212">5 단계: hello 업로드 한.vhd 파일로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="4309b-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="4309b-213">Hello.vhd 파일을 업로드 한 후에 구독에 연결 되며이 사용자 지정 이미지와 가상 컴퓨터를 만들 수 있는 사용자 지정 이미지의 이미지 toohello 목록으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="4309b-214">Hello 이전 단계에서 사용한 hello Azure PowerShell 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="4309b-215">Linux를 사용 하 여 hello OS 유형으로.</span><span class="sxs-lookup"><span data-stu-id="4309b-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="4309b-216">현재 Azure PowerShell 버전 hello "Linux" 또는 "Windows" 매개 변수로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="4309b-217">Hello를 선택 하면 hello 새 이미지를 나열 된 hello 이전 단계를 완료 한 후 **이미지** hello Azure 클래식 포털에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![이미지 선택](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="4309b-219">Hello 갤러리에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="4309b-220">이제 **내 이미지**에서 이 새 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="4309b-221">Hello 새 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-221">Select hello new image.</span></span> <span data-ttu-id="4309b-222">다음으로 hello 메시지 tooset 호스트 이름, 암호, SSH 키를 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![사용자 지정 이미지](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="4309b-224">Hello를 프로 비전을 완료 한 후에 Azure에서 실행 중인 FreeBSD VM 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4309b-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Azure의 FreeBSD 이미지](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
