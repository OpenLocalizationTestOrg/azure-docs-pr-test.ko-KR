---
title: "CLI에서 Linux VM 암호 및 SSH 키 재설정 | Microsoft Docs"
description: "Azure 명령줄 인터페이스(CLI)에서 VMAccess 확장을 사용하여 Linux VM 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하는 방법"
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
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="1a60d-103">VMAccess 확장을 사용하여 Linux VM 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="1a60d-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="1a60d-104">암호를 잊었거나 SSH(보안 셸) 키가 맞지 않거나 SSH 구성에 문제가 생겨서 Azure에서 Linux 가상 컴퓨터에 연결할 수 없는 경우 VMAccessForLinux 확장과 Azure CLI를 사용하여 암호 또는 SSH 키를 재설정하고 SSH 구성을 수정하며 디스크 일관성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="1a60d-105">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1a60d-106">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1a60d-107">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1a60d-108">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="1a60d-109">Azure CLI에서는 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 **azure vm extension set** 명령을 사용하여 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="1a60d-110">자세한 확장 사용을 보려면 **azure help vm extension set** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="1a60d-111">Azure CLI를 사용하여, 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="1a60d-112">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="1a60d-113">SSH 키 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="1a60d-114">암호 및 SSH 키 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="1a60d-115">새 sudo 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1a60d-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="1a60d-116">SSH 구성 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="1a60d-117">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="1a60d-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="1a60d-118">VMAccess 확장 상태 표시</span><span class="sxs-lookup"><span data-stu-id="1a60d-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="1a60d-119">추가된 디스크의 일관성 검사</span><span class="sxs-lookup"><span data-stu-id="1a60d-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="1a60d-120">Linux VM에서 추가된 디스크 복구</span><span class="sxs-lookup"><span data-stu-id="1a60d-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="1a60d-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1a60d-121">Prerequisites</span></span>
<span data-ttu-id="1a60d-122">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-122">You will need to do the following:</span></span>

* <span data-ttu-id="1a60d-123">[Azure CLI를 설치](../../../cli-install-nodejs.md)하고 [구독에 연결](../../../xplat-cli-connect.md)해야만 계정과 연결된 Azure 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="1a60d-124">명령 프롬프트에서 다음을 입력하여 클래식 배포 모델에 대한 올바른 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="1a60d-125">새 암호 또는 SSH 키 집합(둘 중 하나를 다시 설정하려는 경우).</span><span class="sxs-lookup"><span data-stu-id="1a60d-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="1a60d-126">SSH 구성을 다시 설정하려는 경우에는 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="1a60d-127"><a name="pwresetcli"></a>암호 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="1a60d-128">다음 줄을 사용하여 PrivateConf.json이라는 파일을 로컬 컴퓨터에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="1a60d-129">**myUserName** 및 **myP@ssW0rd**를 고유한 사용자 이름과 암호로 바꾸고 만료 날짜를 고유하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="1a60d-130">이 명령을 실행하여 **myVM**에 대한 가상 컴퓨터의 이름을 대체합니다</span><span class="sxs-lookup"><span data-stu-id="1a60d-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="1a60d-131"><a name="sshkeyresetcli"></a>SSH 키 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="1a60d-132">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="1a60d-133">**myUserName** 및 **mySSHKey** 값을 자신의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="1a60d-134">이 명령을 실행하여 **myVM**에 대한 가상 컴퓨터의 이름을 대체합니다</span><span class="sxs-lookup"><span data-stu-id="1a60d-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="1a60d-135"><a name="resetbothcli"></a>암호 및 SSH 키 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="1a60d-136">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="1a60d-137">**myUserName**, **mySSHKey** 및 **myP@ssW0rd** 값을 자신의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="1a60d-138">이 명령을 실행하여 **myVM**에 대한 가상 컴퓨터의 이름을 대체합니다</span><span class="sxs-lookup"><span data-stu-id="1a60d-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="1a60d-139"><a name="createnewsudocli"></a>새 sudo 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1a60d-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="1a60d-140">사용자 이름을 잊은 경우 sudo 기관으로 새 레코드를 만들려면 VMAccess를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="1a60d-141">이 경우 기존 사용자 이름 및 암호는 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="1a60d-142">암호 액세스가 있는 새 sudo 사용자를 만들려면, [암호 재설정](#pwresetcli) 에서 스크립트를 사용하여 새 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="1a60d-143">SSH 키 액세스가 있는 새 sudo 사용자를 만들려면, [SSH 키 재설정](#sshkeyresetcli) 에서 스크립트를 사용하여 새 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="1a60d-144">[암호 및 SSH 키 재설정](#resetbothcli) 을 사용하여 암호 및 SSH 키 액세스 모두가 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="1a60d-145"><a name="sshconfigresetcli"></a>SSH 구성 재설정</span><span class="sxs-lookup"><span data-stu-id="1a60d-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="1a60d-146">SSH 구성이 원치 않는 상태인 경우, VM에 대한 액세스도 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="1a60d-147">구성을 기본 상태로 다시 설정하려면 VMAccess 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="1a60d-148">이렇게 하려면 "reset_ssh" 키를 "True"로 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="1a60d-149">확장에서 SSH 서버를 다시 시작하고, VM에서 SSH 포트를 연 다음, SSH 구성을 기본값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="1a60d-150">사용자 계정(이름, 암호 또는 SSH 키)은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="1a60d-151">재설정된 SSH 구성 파일은 /etc/ssh/sshd_config에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="1a60d-152">이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="1a60d-153">이 명령을 실행하여 **myVM**에 대한 가상 컴퓨터의 이름을 대체합니다</span><span class="sxs-lookup"><span data-stu-id="1a60d-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="1a60d-154"><a name="deletecli"></a>사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="1a60d-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="1a60d-155">VM에 직접 로그인하지 않고 사용자 계정을 삭제하려면 이 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="1a60d-156">이 콘텐츠를 사용하여 PrivateConf.json이라는 파일을 만들고 제거할 사용자 이름을 **removeUserName**로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="1a60d-157">이 명령을 실행하여 **myVM**에 대한 가상 컴퓨터의 이름을 대체합니다</span><span class="sxs-lookup"><span data-stu-id="1a60d-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="1a60d-158"><a name="statuscli"></a>VMAccess 확장 상태 표시</span><span class="sxs-lookup"><span data-stu-id="1a60d-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="1a60d-159">VMAccess 확장 상태를 표시하려면, 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="1a60d-160"><a name='checkdisk'></a>추가된 디스크의 일관성 검사</span><span class="sxs-lookup"><span data-stu-id="1a60d-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="1a60d-161">Linux 가상 컴퓨터의 모든 디스크에 fsck를 실행하려면, 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="1a60d-162">이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="1a60d-163">디스크 검사는 부울 함수를 통해 가상 컴퓨터에 연결되어 있는 디스크를 검사할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="1a60d-164">**myVM**에 가상 컴퓨터 이름을 지정하여 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="1a60d-165"><a name='repairdisk'></a>디스크 복구</span><span class="sxs-lookup"><span data-stu-id="1a60d-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="1a60d-166">탑재가 되지 않거나 탑재 구성 오류가 있는 디스크를 복구하려면, VMAccess 확장을 사용하여 Linux 가상 컴퓨터의 탑재 구성을 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="1a60d-167">**myDisk**에 디스크 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="1a60d-168">이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="1a60d-169">**myVM**에 가상 컴퓨터 이름을 지정하여 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="1a60d-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a60d-170">Next steps</span></span>
* <span data-ttu-id="1a60d-171">Azure PowerShell cmdlet 또는 Azure Resource Manager 템플릿을 사용하여 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하려면 [GitHub의 VMAccess 확장 문서](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a60d-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="1a60d-172">또한 [Azure 포털](https://portal.azure.com) 을 사용하여 클래식 배포 모델에서 배포된 Linux VM의 암호 또는 SSH 키를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="1a60d-173">현재는 이 포털을 사용하여 Resource Manager 배포 모델에 배포된 Linux VM에 대해 이 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a60d-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="1a60d-174">Azure 가상 컴퓨터에 VM 확장을 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a60d-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

