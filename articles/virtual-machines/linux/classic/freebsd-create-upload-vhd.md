---
title: "FreeBSD VM 이미지 만들기 및 업로드 | Microsoft Docs"
description: "FreeBSD 운영 체제가 포함된 VHD(가상 하드 디스크)를 만들고 업로드하여 Azure 가상 컴퓨터를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="15853-103">FreeBSD VHD를 만들어서 Azure에 업로드</span><span class="sxs-lookup"><span data-stu-id="15853-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="15853-104">이 문서에서는 FreeBSD 운영 체제가 포함된 VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="15853-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="15853-105">VHD를 업로드한 후에는 VHD를 사용자 고유의 이미지로 사용하여 Azure에서 VM(가상 컴퓨터)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="15853-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="15853-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="15853-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="15853-109">Resource Manager 모델을 사용하여 VHD을 업로드하는 방법에 대한 정보는 [여기](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15853-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="15853-110">Prerequisites</span></span>
<span data-ttu-id="15853-111">이 문서에서는 사용자에게 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="15853-112">**Azure 구독**- 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="15853-113">MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="15853-114">그렇지 않으면 [무료 평가판 계정 만들기](https://azure.microsoft.com/pricing/free-trial/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="15853-115">**Azure PowerShell 도구**- Azure PowerShell 모듈이 설치되어 있고 Azure 구독을 사용하도록 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="15853-116">모듈을 다운로드하려면 [Azure 다운로드](https://azure.microsoft.com/downloads/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="15853-117">모듈 설치 및 구성 방법을 설명한 자습서는 여기에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="15853-118">[Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet을 사용하여 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="15853-119">**.vhd 파일에 설치된 FreeBSD 운영 체제**- 가상 하드 디스크에 지원되는 FreeBSD 운영 체제를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="15853-120">.vhd 파일을 만드는 도구는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="15853-121">예를 들어 Hyper-V와 같은 가상화 솔루션을 사용하여 .vhd 파일을 만들고 운영 체제를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="15853-122">Hyper-V를 설치하고 사용하는 방법에 대한 자세한 내용은 [Hyper-V 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="15853-123">새 VHDX 형식은 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="15853-124">Hyper-V 관리자 또는 [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx)cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="15853-125">뿐만 아니라 [Hyper-V에 FreeBSD를 사용하는 방법에 대한 MSDN 자습서](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="15853-126">이 작업에는 다음 5단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="15853-127">1단계: 업로드할 이미지 준비</span><span class="sxs-lookup"><span data-stu-id="15853-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="15853-128">FreeBSD 운영 체제를 설치한 가상 컴퓨터에서 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="15853-129">DHCP를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="15853-130">SSH를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-130">Enable SSH.</span></span>

    <span data-ttu-id="15853-131">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="15853-132">FreeBSD 디스크에서 설치 후에는 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="15853-133">직렬 콘솔을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="15853-134">sudo를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-134">Install sudo.</span></span>

    <span data-ttu-id="15853-135">Azure에서 root 계정이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="15853-136">다시 말해서 상승된 권한으로 명령을 실행하려면 권한 없는 사용자로 sudo를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="15853-137">Azure 에이전트에 대한 필수 조건.</span><span class="sxs-lookup"><span data-stu-id="15853-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="15853-138">Azure 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-138">Install Azure Agent.</span></span>

    <span data-ttu-id="15853-139">언제든지 최신 버전의 Azure 에이전트를 [github](https://github.com/Azure/WALinuxAgent/releases)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="15853-140">버전 2.0.10 이상은 FreeBSD 10 및 10.1을 공식적으로 지원하며, 버전 2.1.4 이상(2.2.x 포함)은 FreeBSD 10.2 이상 릴리스를 공식적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="15853-141">2.0의 경우 2.0.16을 예로 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="15853-142">2.1의 경우 2.1.4를 예로 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="15853-143">Azure 에이전트를 설치한 후 에이전트가 실행 중인지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="15853-144">시스템을 프로비전 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-144">Deprovision the system.</span></span>

    <span data-ttu-id="15853-145">시스템을 프로비전 해제하여 다시 프로비전하기에 적합한 상태로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="15853-146">다음 명령은 마지막으로 프로비전된 사용자 계정 및 관련 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="15853-147">이제 VM을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="15853-148">2단계: Azure에서 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="15853-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="15853-149">가상 컴퓨터를 만드는 데 사용할 수 있도록 .vhd 파일을 업로드하려면 Azure에 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="15853-150">Azure 클래식 포털을 사용하여 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="15853-151">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="15853-152">명령 모음에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="15853-153">**데이터 서비스** > **저장소** > **빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![저장소 계정 빠른 생성](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="15853-155">다음과 같이 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="15853-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="15853-156">**URL** 필드에서 저장소 계정의 URL에 사용할 하위 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="15853-157">3-24자의 숫자와 소문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="15853-158">이 이름은 구독에 대한 Azure Blob 저장소, Azure 큐 저장소 또는 Azure 테이블 저장소 리소스의 주소를 지정하는 데 사용되는 URL 내의 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="15853-159">**위치/선호도 그룹** 드롭다운 메뉴에서 저장소 계정의 **위치 또는 선호도 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="15853-160">선호도 그룹을 사용하면 클라우드 서비스와 저장소를 동일한 데이터 센터에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="15853-161">**복제** 필드에서, 저장소 계정에 **지역 중복** 복제를 사용할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="15853-162">지역에서 복제는 기본적으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="15853-163">이 옵션을 사용하면 추가 비용 없이 보조 위치로 데이터를 복제하므로 기본 위치에서 심각한 장애가 발생하는 경우 저장소에서 보조 위치로 장애 조치(Failover)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="15853-164">보조 위치는 자동으로 할당되며 변경될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="15853-165">법적 필요 또는 조직 정책에 따라 클라우드 기반 저장소의 위치를 더 엄격하게 제어해야 하는 경우 지역에서 복제를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="15853-166">그러나 나중에 지역에서 복제를 설정하는 경우 기존 데이터를 대체 위치로 복제하는 데 일회성 데이터 전송 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="15853-167">지역에서 복제를 사용하지 않는 저장소 서비스는 할인하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="15853-168">저장소 계정의 지역에서 복제를 관리하는 방법에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/common/storage-redundancy.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![저장소 계정 세부 정보 입력](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="15853-170">**저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="15853-171">이제 계정이 **저장소**아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="15853-171">The account now appears under **storage**.</span></span>

    ![저장소 계정을 성공적으로 만들었음](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="15853-173">다음으로 업로드된 .vhd 파일의 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15853-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="15853-174">저장소 계정 이름을 선택하고 **컨테이너**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-174">Select the storage account name, and then select **Containers**.</span></span>

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="15853-176">**컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-176">Select **Create a Container**.</span></span>

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="15853-178">**이름** 필드에 컨테이너의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="15853-179">그런 다음 **액세스** 드롭 다운 메뉴에서 원하는 액세스 정책 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![컨테이너 이름](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="15853-181">기본적으로 컨테이너는 전용이며 해당 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="15853-182">컨테이너 속성 및 메타데이터는 제외하고 컨테이너에 있는 Blob에 대한 공용 읽기 권한을 허용하려면 **공용 Blob** 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="15853-183">컨테이너 및 Blob에 대한 전체 공용 읽기 권한을 허용하려면 **공용 컨테이너** 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="15853-184">3단계: Azure 연결 준비</span><span class="sxs-lookup"><span data-stu-id="15853-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="15853-185">.vhd 파일을 업로드하려면 컴퓨터와 Azure 구독 간에 보안 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="15853-186">이를 위해 Azure AD(Azure Active Directory) 방법이나 인증서 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="15853-187">Azure AD 방법을 사용하여 .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="15853-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="15853-188">Azure PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15853-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="15853-189">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="15853-190">이 명령은 직장 또는 학교 계정으로 로그인할 수 있는 로그인 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15853-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell 창](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="15853-192">Azure가 자격 증명 정보를 인증하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="15853-193">그런 다음 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="15853-194">인증서 방법을 사용하여 .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="15853-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="15853-195">Azure PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15853-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="15853-196">입력: `Get-AzurePublishSettingsFile`</span><span class="sxs-lookup"><span data-stu-id="15853-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="15853-197">브라우저 창이 열리고 .publishsettings 파일을 다운로드하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="15853-198">이 파일에는 Azure 구독에 대한 정보와 인증서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![브라우저 다운로드 페이지](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="15853-200">.publishsettings 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="15853-201">입력: `Import-AzurePublishSettingsFile <PathToFile>`, 여기서 `<PathToFile>`은 .publishsettings 파일의 전체 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="15853-202">자세한 내용은 [Azure Cmdlets 시작](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="15853-203">PowerShell 설치 및 구성에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15853-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="15853-204">4단계: .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="15853-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="15853-205">.vhd 파일을 업로드할 때 Blob 저장소 내 임의의 위치에 .vhd 파일을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="15853-206">다음은 파일을 업로드할 때 사용되는 몇 가지 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="15853-207">**BlobStorageURL**은 2단계에서 만든 저장소 계정의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="15853-208">**YourImagesFolder**는 이미지를 저장하려는 Blob 저장소 내 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="15853-209">**VHDName**은 가상 하드 디스크를 식별하기 위해 Azure 클래식 포털에 표시되는 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="15853-210">**PathToVHDFile**은 .vhd 파일의 전체 경로 및 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="15853-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="15853-211">이전 단계에서 사용한 Azure PowerShell 창에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="15853-212">5단계: 업로드한 .vhd 파일로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="15853-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="15853-213">.vhd 파일을 업로드한 후에는 구독과 연결된 사용자 지정 이미지 목록에 .vhd 파일을 이미지로 추가하고 이 사용자 지정 이미지를 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="15853-214">이전 단계에서 사용한 Azure PowerShell 창에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="15853-215">OS 유형으로 Linux를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-215">Use Linux as the OS type.</span></span> <span data-ttu-id="15853-216">Azure PowerShell 최신 버전은 매개 변수로 "Linux" 또는 "Windows"만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="15853-217">이전 단계를 완료한 후 Azure 클래식 포털에서 **이미지** 탭을 선택하면 새 이미지가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![이미지 선택](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="15853-219">갤러리에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15853-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="15853-220">이제 **내 이미지**에서 이 새 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15853-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="15853-221">새 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-221">Select the new image.</span></span> <span data-ttu-id="15853-222">다음으로 메시지에 따라 호스트 이름, 암호, SSH 키 등을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="15853-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![사용자 지정 이미지](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="15853-224">프로비전이 완료되면 FreeBSD VM이 Azure에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="15853-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Azure의 FreeBSD 이미지](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
