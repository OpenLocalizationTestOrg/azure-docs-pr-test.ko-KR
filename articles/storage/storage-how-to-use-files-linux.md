---
title: "Linux에서 Azure File Storage 사용 | Microsoft Docs"
description: "Linux에서 SMB를 통해 Azure 파일 공유를 탑재하는 방법을 알아봅니다."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="50cfe-103">Linux에서 Azure File Storage 사용</span><span class="sxs-lookup"><span data-stu-id="50cfe-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="50cfe-104">[Azure File Storage](storage-dotnet-how-to-use-files.md)는 사용하기 쉬운 Microsoft 클라우드 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="50cfe-105">Azure 파일 공유는 [Samba 프로젝트](https://www.samba.org/)의 [cifs-utils 패키지](https://wiki.samba.org/index.php/LinuxCIFS_utils)를 사용하여 Linux 배포판에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="50cfe-106">이 문서에서는 Azure 파일 공유를 탑재하는 두 가지 방법을 보여 줍니다. 하나는 요청 시 `mount` 명령을 사용하여 탑재하고, 다른 하나는 `/etc/fstab`에 항목을 만들어 부팅 시 탑재하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="50cfe-107">온-프레미스 또는 다른 Azure 지역과 같이 에서 호스팅되는 Azure 지역 외부에 Azure 파일 공유를 탑재하려면 OS에서 SMB 3.0 암호화 기능을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="50cfe-108">Linux용 SMB 3.0에 대한 암호화 기능이 4.11 커널에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="50cfe-109">이 기능을 사용하면 온-프레미스 또는 다른 Azure 지역에서 Azure 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="50cfe-110">게시 시점에서 이 기능은 Ubuntu 16.04 이상으로 백포팅되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="50cfe-111">Linux 및 cifs-utils 패키지와 함께 Azure 파일 공유를 탑재하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="50cfe-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="50cfe-112">**cifs-utils 패키지를 설치할 수 있는 Linux 배포판을 선택합니다**. Azure 이미지 갤러리에서 권장되는 Linux 배포판은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="50cfe-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="50cfe-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="50cfe-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="50cfe-114">RHEL 7+</span></span>
    * <span data-ttu-id="50cfe-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="50cfe-115">CentOS 7+</span></span>
    * <span data-ttu-id="50cfe-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="50cfe-116">Debian 8</span></span>
    * <span data-ttu-id="50cfe-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="50cfe-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="50cfe-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="50cfe-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="50cfe-119"><a id="install-cifs-utils"></a>**cifs-utils 패키지가 설치됩니다**. cifs-utils는 원하는 Linux 배포판의 패키지 관리자를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="50cfe-120">**Ubuntu** 및 **Debian 기반** 배포판에서는 `apt-get` 패키지 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="50cfe-121">**RHEL** 및 **CentOS**에서는 `yum` 패키지 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="50cfe-122">**openSUSE**에서는 `zypper` 패키지 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="50cfe-123">다른 배포판에서는 적절한 패키지 관리자를 사용하거나 [소스에서 컴파일합니다](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="50cfe-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="50cfe-124">**탑재된 공유의 디렉터리/파일 권한을 결정합니다**. 아래 예제에서는 모든 사용자에게 읽기, 쓰기 및 실행 권한을 부여하기 위해 0777을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="50cfe-125">다른 [chmod 권한](https://en.wikipedia.org/wiki/Chmod)으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="50cfe-126">**저장소 계정 이름**: Azure 파일 공유를 탑재하려면 저장소 계정의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="50cfe-127">**저장소 계정 키**: Azure 파일 공유를 탑재하려면 기본(또는 보조) 저장소 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="50cfe-128">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="50cfe-129">**445 포트가 열려 있는지 확인합니다**. SMB는 445 TCP 포트를 통해 통신합니다. 방화벽이 클라이언트 컴퓨터에서 445 TCP 포트를 차단하고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="50cfe-130">요청 시 `mount`를 사용하여 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="50cfe-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="50cfe-131">**[Linux 배포판에 cifs-utils 패키지를 설치합니다](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="50cfe-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="50cfe-132">**탑재 지점에 대한 폴더를 만듭니다**. 이 작업은 파일 시스템의 어느 위치에서나 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="50cfe-133">**mount 명령을 사용하여 Azure 파일 공유를 탑재합니다**. `<storage-account-name>`, `<share-name>` 및 `<storage-account-key>`를 적절한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="50cfe-134">Azure 파일 공유를 사용하여 작업을 완료하면 `sudo umount ./mymountpoint`를 사용하여 공유를 탑재 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="50cfe-135">`/etc/fstab`을 사용하여 Azure 파일 공유에 대한 영구 탑재 지점 만들기</span><span class="sxs-lookup"><span data-stu-id="50cfe-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="50cfe-136">**[Linux 배포판에 cifs-utils 패키지를 설치합니다](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="50cfe-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="50cfe-137">**탑재 지점에 대한 폴더를 만듭니다**. 이 작업은 파일 시스템의 어느 위치에서나 수행할 수 있지만 폴더의 절대 경로를 기록해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="50cfe-138">다음 예제에서는 루트 아래에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="50cfe-139">**다음 명령을 사용하여 `/etc/fstab`에 다음 줄을 추가합니다**. `<storage-account-name>`, `<share-name>` 및 `<storage-account-key>`를 적절한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="50cfe-140">다시 부팅하는 대신 `/etc/fstab`을 편집한 후에 `sudo mount -a`를 사용하여 Azure 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="50cfe-141">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="50cfe-141">Feedback</span></span>
<span data-ttu-id="50cfe-142">Linux 사용자 여러분의 의견을 듣고 싶습니다!</span><span class="sxs-lookup"><span data-stu-id="50cfe-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="50cfe-143">Linux 사용자 그룹용 Azure 파일 저장소는 Linux에서 파일 저장소를 평가하고 채택할 때 피드백을 공유할 수 있도록 포럼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="50cfe-144">사용자 그룹에 참가하려면 [Azure File Storage Linux 사용자](mailto:azurefileslinuxusers@microsoft.com)에게 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="50cfe-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50cfe-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50cfe-145">Next steps</span></span>
<span data-ttu-id="50cfe-146">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="50cfe-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="50cfe-147">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="50cfe-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="50cfe-148">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="50cfe-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="50cfe-149">Microsoft Azure 저장소와 함께 AzCopy를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="50cfe-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="50cfe-150">Azure Storage에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="50cfe-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="50cfe-151">FAQ</span><span class="sxs-lookup"><span data-stu-id="50cfe-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="50cfe-152">문제 해결</span><span class="sxs-lookup"><span data-stu-id="50cfe-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
