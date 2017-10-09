---
title: "Azure 파일 저장소와 Linux aaaUse | Microsoft Docs"
description: "Linux에서 SMB를 통한 toomount Azure 파일을 공유 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="0097b-103">Linux에서 Azure File Storage 사용</span><span class="sxs-lookup"><span data-stu-id="0097b-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="0097b-104">[Azure 파일 저장소](../storage-dotnet-how-to-use-files.md) 는 Microsoft의 쉬운 toouse 클라우드 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="0097b-105">Hello를 사용 하 여 Linux 배포에서 azure 파일 공유를 탑재할 수 [cifs 유틸리티 패키지](https://wiki.samba.org/index.php/LinuxCIFS_utils) hello에서 [Samba 프로젝트](https://www.samba.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="0097b-106">이 문서에서는 두 가지 방법으로 toomount Azure 파일 공유: hello로 주문형 `mount` 명령 및에서 항목을 만들어 부팅에 `/etc/fstab`합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="0097b-107">순서 toomount hello 외부의 경우 Azure 파일 공유에에서는 다른 Azure 지역의 hello OS 또는 온-프레미스 등,에 호스팅된 Azure 지역 SMB 3.0의 hello 암호화 기능을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="0097b-108">Linux용 SMB 3.0에 대한 암호화 기능이 4.11 커널에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="0097b-109">이 기능을 사용하면 온-프레미스 또는 다른 Azure 지역에서 Azure 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="0097b-110">게시의 hello 시이 기능은 backported tooUbuntu 이상 16.04에서 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="0097b-111">Linux 및 hello cifs 유틸리티 패키지와 함께 Azure 파일 탑재에 대 한 필수 공유</span><span class="sxs-lookup"><span data-stu-id="0097b-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="0097b-112">**Hello cifs 유틸리티 패키지 설치를 가질 수 있는 Linux 배포판 선택**: hello hello Azure 이미지 갤러리의 Linux 배포판을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="0097b-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="0097b-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="0097b-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="0097b-114">RHEL 7+</span></span>
    * <span data-ttu-id="0097b-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="0097b-115">CentOS 7+</span></span>
    * <span data-ttu-id="0097b-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="0097b-116">Debian 8</span></span>
    * <span data-ttu-id="0097b-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="0097b-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="0097b-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="0097b-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="0097b-119"><a id="install-cifs-utils"></a>**hello cifs 유틸리티 패키지가 설치 되어**: hello 패키지 관리자를 사용 하 여 사용자가 선택한 hello Linux 배포판에 hello cifs 유틸리티를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="0097b-120">**Ubuntu** 및 **Debian 기반** 배포를 사용 하 여 hello `apt-get` 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="0097b-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="0097b-121">**RHEL** 및 **CentOS**, hello를 사용 하 여 `yum` 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="0097b-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="0097b-122">**openSUSE**, hello를 사용 하 여 `zypper` 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="0097b-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="0097b-123">Hello 적절 한 패키지 관리자를 사용 하 여 다른 배포 또는 [소스에서 컴파일하여](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="0097b-124">**Hello 탑재 된 공유의 hello 디렉터리/파일 사용 권한을 결정**: hello 아래 예제에서는 사용 하 여, 0777 toogive 읽기, 쓰기 및 실행 tooall 사용자 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0097b-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="0097b-125">다른 [chmod 권한](https://en.wikipedia.org/wiki/Chmod)으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="0097b-126">**저장소 계정 이름**: toomount Azure 파일 공유, hello 저장소 계정의 이름을 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="0097b-127">**저장소 계정 키**: toomount Azure 파일 공유, 기본 (또는 보조) 저장소 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="0097b-128">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="0097b-129">**포트 445가 열려 있는지 확인**: 방화벽에서 TCP를 차단 하면 toosee 포트 445 클라이언트 컴퓨터에서 확인 SMB TCP 포트 445-를 통해 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="0097b-130">Azure 파일 공유와 요청 시 hello 탑재`mount`</span><span class="sxs-lookup"><span data-stu-id="0097b-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="0097b-131">**[Linux 배포판에 대 한 hello cifs 유틸리티 패키지 설치](#install-cifs-utils)**합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="0097b-132">**Hello 탑재 지점에 대 한 폴더를 만들고**: hello 파일 시스템에서 아무 곳 이나 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="0097b-133">**사용 하 여 hello 탑재 명령 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, 및 `<storage-account-key>` hello 적절 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="0097b-134">완료 되 면 Azure 파일 공유를 hello를 사용 하 여, 사용할 수 있습니다 `sudo umount ./mymountpoint` toounmount hello 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="0097b-135">Azure 파일 공유를 hello에 대 한 영구 탑재 지점 만들기`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="0097b-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="0097b-136">**[Linux 배포판에 대 한 hello cifs 유틸리티 패키지 설치](#install-cifs-utils)**합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="0097b-137">**Hello 탑재 지점에 대 한 폴더를 만들고**: hello 파일 시스템에서 아무 곳 이나 수행할 수 있습니다 하지만 toonote hello hello 폴더의 절대 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="0097b-138">다음 예제는 hello 루트 아래에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="0097b-139">**사용 하 여 hello 다음 명령은 다음 줄을 너무 tooappend hello`/etc/fstab`**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, 및 `<storage-account-key>` hello 적절 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="0097b-140">사용할 수 있습니다 `sudo mount -a` 편집한 후 toomount hello Azure 파일 공유 `/etc/fstab` 다시 부팅 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="0097b-141">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="0097b-141">Feedback</span></span>
<span data-ttu-id="0097b-142">Linux 사용자를 toohear 원하는!</span><span class="sxs-lookup"><span data-stu-id="0097b-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="0097b-143">Linux 사용자 그룹에 대 한 Azure 파일 저장소 hello 위한 포럼을 제공 하면 tooshare 피드백 평가 하 고 Linux에서 파일 저장소를 채택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="0097b-144">전자 메일 [Azure 파일 저장소 Linux 사용자](mailto:azurefileslinuxusers@microsoft.com) toojoin hello 사용자의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0097b-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0097b-145">Next steps</span></span>
<span data-ttu-id="0097b-146">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0097b-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="0097b-147">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="0097b-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="0097b-148">어떻게 toouse AzCopy Microsoft Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="0097b-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="0097b-149">Hello Azure CLI를 사용 하 여 Azure 저장소와</span><span class="sxs-lookup"><span data-stu-id="0097b-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="0097b-150">FAQ</span><span class="sxs-lookup"><span data-stu-id="0097b-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="0097b-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0097b-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
