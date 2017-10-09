---
title: "CLI hello에서 aaaReset Linux VM 암호 및 SSH 키 | Microsoft Docs"
description: "Toouse hello hello Azure 명령줄 인터페이스 (CLI) tooreset Linux VM 암호 또는 SSH 키에서 VMAccess 확장 hello SSH 구성을 수정 하 고 디스크 일관성을 검사 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="e450f-103">Tooreset Linux VM 암호 또는 SSH 키를 hello SSH 구성을 수정 하 고 hello VMAccess 확장을 사용 하 여 디스크 일관성 검사 방법</span><span class="sxs-lookup"><span data-stu-id="e450f-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="e450f-104">Hello 작업에서는 VMAccessForLinux 확장을 사용 하 여 hello Azure CLI tooreset hello 암호 또는 SSH 키와 암호를 잊은 경우, 잘못 된 SSH (보안 셸) 키 또는 hello SSH 구성 문제가 때문에 Azure에서 tooa Linux 가상 컴퓨터를 연결할 수 없는 경우, 수정 SSH 구성을 hello 및 디스크 일관성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="e450f-105">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e450f-106">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e450f-107">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e450f-108">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="e450f-109">Hello를 사용 하면 Azure CLI hello로 **azure vm 확장 집합** 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트) tooaccess 명령에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="e450f-110">자세한 확장 사용을 보려면 **azure help vm extension set** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="e450f-111">Azure CLI hello로 할 수 있는 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="e450f-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="e450f-112">Hello 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="e450f-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="e450f-113">Hello SSH 키를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="e450f-114">Hello 암호 및 hello SSH 키를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="e450f-115">새 sudo 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e450f-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="e450f-116">Hello SSH 구성을 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="e450f-117">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="e450f-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="e450f-118">Hello VMAccess 확장의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="e450f-119">추가된 디스크의 일관성 검사</span><span class="sxs-lookup"><span data-stu-id="e450f-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="e450f-120">Linux VM에서 추가된 디스크 복구</span><span class="sxs-lookup"><span data-stu-id="e450f-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="e450f-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e450f-121">Prerequisites</span></span>
<span data-ttu-id="e450f-122">Toodo hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="e450f-123">너무 해야[hello Azure CLI를 설치](../../../cli-install-nodejs.md) 및 [tooyour 구독을 연결](../../../xplat-cli-connect.md) toouse Azure 계정과 연결 된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="e450f-124">Hello 명령 프롬프트에서 hello 다음을 입력 하 여 hello hello 클래식 배포 모델에 대 한 올바른 모드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="e450f-125">Tooreset 둘 중 하나를 원하는 경우 새 암호 또는 SSH 키 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="e450f-126">Tooreset hello SSH 구성을 하려는 경우 이러한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="e450f-127"><a name="pwresetcli"></a>Hello 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="e450f-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="e450f-128">다음 줄을 사용하여 PrivateConf.json이라는 파일을 로컬 컴퓨터에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="e450f-129">**myUserName** 및 **myP@ssW0rd**를 고유한 사용자 이름과 암호로 바꾸고 만료 날짜를 고유하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="e450f-130">에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="e450f-131"><a name="sshkeyresetcli"></a>Hello SSH 키를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="e450f-132">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="e450f-133">Hello 대체 **: myUserName** 및 **mySSHKey** 고유한 정보가 포함 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="e450f-134">에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="e450f-135"><a name="resetbothcli"></a>Hello 암호와 hello SSH 키를 모두 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="e450f-136">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="e450f-137">Hello 대체 **: myUserName**, **mySSHKey** 및  **myP@ssW0rd**  고유한 정보가 포함 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="e450f-138">에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="e450f-139"><a name="createnewsudocli"></a>새 sudo 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e450f-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="e450f-140">사용자 이름을 잊은 경우 hello sudo 권한이로 새 레코드 toocreate VMAccess를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="e450f-141">이 경우 기존 사용자 이름 hello 및 암호는 수정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="e450f-142">암호 액세스를 사용 하 여 hello 스크립트에 있는 새 sudo 사용자 toocreate [hello 암호 재설정](#pwresetcli) hello 새 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="e450f-143">SSH 키 액세스를 사용 하 여 hello 스크립트에 있는 새 sudo 사용자 toocreate [hello SSH 키 재설정](#sshkeyresetcli) hello 새 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="e450f-144">사용할 수도 있습니다 [hello 암호 및 hello SSH 키 재설정](#resetbothcli) toocreate 암호 및 SSH 키 액세스 권한을 모두 사용 하 여 새 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="e450f-145"><a name="sshconfigresetcli"></a>Hello SSH 구성을 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e450f-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="e450f-146">Hello SSH 구성이 원치 않는 상태가 되 면 액세스 toohello VM을 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="e450f-147">Hello VMAccess 확장 tooreset hello 구성 tooits 기본 상태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="e450f-148">toodo 따라서 하기만 하면 tooset hello "reset_ssh" 키 너무 "True"입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="e450f-149">hello 확장 hello SSH 서버를 다시 시작을 열고 hello SSH 포트를 VM에는 hello SSH 구성 toodefault 값 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="e450f-150">hello 사용자 계정 (이름, 암호 또는 SSH 키)은 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="e450f-151">다시 설정 됩니다. hello SSH 구성 파일은 /etc/ssh/sshd_config에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="e450f-152">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="e450f-153">에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="e450f-154"><a name="deletecli"></a>사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="e450f-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="e450f-155">사용자 계정을 직접 toohello VM에 로그인 하지 않고도 toodelete 하려는 경우이 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="e450f-156">이 콘텐츠를 대체에 대 한 사용자 이름 tooremove hello와 PrivateConf.json 라는 파일을 만들어 **removeUserName**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="e450f-157">에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령을 실행 **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="e450f-158"><a name="statuscli"></a>Hello VMAccess 확장의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="e450f-159">이 명령을 실행 하는 hello VMAccess 확장의 toodisplay hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="e450f-160"><a name='checkdisk'></a>추가된 디스크의 일관성 검사</span><span class="sxs-lookup"><span data-stu-id="e450f-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="e450f-161">Linux 가상 컴퓨터의 모든 디스크에서 toorun fsck, toodo hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="e450f-162">이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="e450f-163">디스크 검사 toocheck 디스크 연결 tooyour 가상 컴퓨터 여부는 부울 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="e450f-164">실행에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령 tooexecute **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="e450f-165"><a name='repairdisk'></a>디스크 복구</span><span class="sxs-lookup"><span data-stu-id="e450f-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="e450f-166">Linux 가상 컴퓨터에 hello VMAccess 확장 tooreset hello 탑재 구성을 사용 하는 toorepair 하거나 디스크를 탑재 하 탑재 구성 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="e450f-167">이때 hello 이름에 대 한 디스크의 **myDisk**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="e450f-168">이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="e450f-169">실행에 대 한 가상 컴퓨터의 hello 이름을 대체 하 여이 명령 tooexecute **myVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="e450f-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e450f-170">Next steps</span></span>
* <span data-ttu-id="e450f-171">Toouse Azure PowerShell cmdlet 또는 Azure 리소스 관리자 템플릿 tooreset hello 암호 또는 SSH 키를 원하는 경우 hello SSH 구성을 수정 하 고 디스크 일관성 검사, hello 참조 [GitHub에서 VMAccess 확장 문서](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="e450f-172">Hello를 사용할 수도 있습니다 [Azure 포털](https://portal.azure.com) tooreset hello 암호 또는 SSH 키는 Linux VM의 hello 클래식 배포 모델에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="e450f-173">현재 hello 리소스 관리자 배포 모델에 배포 된 Linux VM에 대 한 hello 포털 do toothis를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e450f-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="e450f-174">Azure 가상 컴퓨터에 VM 확장을 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e450f-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

