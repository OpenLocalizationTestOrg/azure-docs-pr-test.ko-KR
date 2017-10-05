---
title: "Azure Backup Server를 사용하여 VMware 서버 백업 | Microsoft Docs"
description: "Azure Backup Server를 사용하여 VMware vCenter/ESXi 서버를 Azure 또는 디스크에 백업합니다. 이 문서에서는 VMware 워크로드를 백업(또는 보호)하기 위한 단계별 지침을 제공합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="0be87-104">Azure에 VMware 서버 백업</span><span class="sxs-lookup"><span data-stu-id="0be87-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="0be87-105">이 문서에서는 VMware 서버 워크로드를 보호하기 위해 Azure Backup Server를 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="0be87-106">이 문서에서는 Azure Backup Server가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="0be87-107">Azure Backup Server가 설치되어 있지 않은 경우 [Azure Backup Server를 사용하여 워크로드 백업 준비](backup-azure-microsoft-azure-backup.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0be87-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="0be87-108">Azure Backup Server는 VMware vCenter Server 버전 6.5, 6.0 및 5.5를 백업하거나 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="0be87-109">vCenter Server에 대한 보안 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="0be87-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="0be87-110">기본적으로 Azure Backup Server는 HTTPS 채널을 통해 각 vCenter Server와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="0be87-111">보안 통신을 설정하려면 Azure Backup Server에 VMware CA(인증 기관) 인증서를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="0be87-112">보안 통신이 필요하지 않고 HTTPS 요구 사항을 비활성화하려는 경우 [보안 통신 프로토콜 사용 안 함](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0be87-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="0be87-113">Azure Backup Server와 vCenter Server 간에 보안 연결을 만들려면 Azure Backup Server에서 신뢰할 수 있는 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="0be87-114">일반적으로 Azure Backup Server 컴퓨터의 브라우저를 사용하여 vSphere Web Client를 통해 vCenter Server에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="0be87-115">처음 Azure Backup Server 브라우저를 사용하여 vCenter Server에 연결하면 연결 보안이 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="0be87-116">다음 이미지에서는 보안이 설정되지 않은 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-116">The following image shows the unsecured connection.</span></span>

![VMware 서버에 대한 안전하지 않은 연결의 예](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="0be87-118">이 문제를 해결하고 보안 연결을 만들려면 신뢰할 수 있는 루트 CA 인증서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="0be87-119">Azure Backup Server의 브라우저에 vSphere Web Client에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="0be87-120">vSphere Web Client 로그인 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-120">The vSphere Web Client login page appears.</span></span>

    ![vSphere Web Client](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="0be87-122">관리자 및 개발자를 위한 정보 아래쪽에 **신뢰할 수 있는 루트 CA 인증서 다운로드** 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![신뢰할 수 있는 루트 CA 인증서 다운로드 링크](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="0be87-124">vSphere Web Client 로그인 페이지가 표시되지 않으면 브라우저의 프록시 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="0be87-125">**신뢰할 수 있는 루트 CA 인증서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="0be87-126">vCenter Server가 로컬 컴퓨터에 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="0be87-127">파일 이름은 **download**입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-127">The file's name is named **download**.</span></span> <span data-ttu-id="0be87-128">브라우저에 따라 파일을 열거나 저장할 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![인증서 다운로드 시 나타나는 다운로드 메시지](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="0be87-130">파일을 Azure Backup Server의 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="0be87-131">파일을 저장할 때 .zip 파일 이름 확장명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="0be87-132">이 파일은 인증서에 대한 정보가 들어 있는 .zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="0be87-133">.zip 확장명으로 압축 풀기 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="0be87-134">**download.zip**을 마우스 오른쪽 단추로 클릭한 다음 **모두 압축 풀기**를 선택하여 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="0be87-135">.zip 파일의 콘텐츠가 **certs** 폴더에 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="0be87-136">certs 폴더에 두 가지 형식의 파일이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="0be87-137">루트 인증서 파일은 .0 및 .1과 같은 숫자가 매겨진 시퀀스로 시작하는 확장명을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="0be87-138">CRL 파일은 .r0 또는 .r1과 같은 시퀀스로 시작하는 확장명을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="0be87-139">CRL 파일은 인증서와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="0be87-140">로컬로 추출된 다운로드 파일</span><span class="sxs-lookup"><span data-stu-id="0be87-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="0be87-141">**certs** 폴더에서 루트 인증서 파일을 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="0be87-142">루트 인증서 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="0be87-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="0be87-143">루트 인증서의 확장명을 .crt로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="0be87-144">확장명을 변경할지 묻는 메시지가 표시되는 경우 **예** 또는 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="0be87-145">그렇지 않은 경우 파일의 대상 기능을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="0be87-146">파일 아이콘이 루트 인증서를 나타내는 아이콘으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="0be87-147">루트 인증서를 마우스 오른쪽 단추로 클릭하고 팝업 메뉴에서 **인증서 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="0be87-148">**인증서 가져오기 마법사** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="0be87-149">**인증서 가져오기 마법사** 대화 상자에서 **로컬 컴퓨터**를 인증서에 대한 대상으로 선택한 후 **다음**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="0be87-150">인증서 저장소 대상 옵션</span><span class="sxs-lookup"><span data-stu-id="0be87-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="0be87-151">컴퓨터 변경을 허용할지 묻는 메시지가 표시되면 모든 변경 사항에 대해 **예** 또는 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="0be87-152">**인증서 저장소** 페이지에서 **모든 인증서를 다음 저장소에 저장**을 선택한 다음 **찾아보기**를 클릭하여 인증서 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![특정 저장소 위치에 인증서 저장](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="0be87-154">**인증서 저장소 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![인증서 저장소 폴더 계층 구조](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="0be87-156">인증서 대상 폴더로 **신뢰할 수 있는 루트 인증 기관**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![인증서 대상 폴더](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="0be87-158">**신뢰할 수 있는 루트 인증 기관** 폴더가 인증서 저장소로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="0be87-159">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-159">Click **Next**.</span></span>

    ![인증서 저장소 폴더](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="0be87-161">**인증서 가져오기 마법사 완료** 페이지에서 인증서가 원하는 폴더에 있는지 확인한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![인증서가 적절한 폴더에 있는지 확인](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="0be87-163">대화 상자가 나타나고 성공적인 인증서 가져오기가 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="0be87-164">vCenter Server에 로그인하여 연결이 안전한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="0be87-165">인증서 가져오기에 실패하고 보안 연결을 설정할 수 없는 경우 VMware vSphere 설명서의 [서버 인증서 가져오기](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0be87-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="0be87-166">조직 내에서 보안 경계가 있고 HTTPS 프로토콜을 사용하지 않으려는 경우 다음 절차를 사용하여 보안 통신을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="0be87-167">보안 통신 프로토콜 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="0be87-167">Disable secure communication protocol</span></span>

<span data-ttu-id="0be87-168">조직에서 HTTPS 프로토콜이 필요하지 않은 경우 다음 단계를 사용하여 HTTPS를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="0be87-169">기본 동작을 사용하지 않으려면 기본 동작을 무시하는 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="0be87-170">다음 텍스트를 복사하여 .txt 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="0be87-171">파일을 Azure Backup Server 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="0be87-172">파일 이름의 경우 DisableSecureAuthentication.reg를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="0be87-173">레지스트리 항목을 활성화하려면 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="0be87-174">vCenter Server에서 역할 및 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0be87-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="0be87-175">vCenter Server에서 역할은 미리 정의된 권한 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="0be87-176">vCenter Server 관리자는 역할을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="0be87-177">사용 권한을 할당하려면 관리자는 사용자 계정을 역할로 쌍을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="0be87-178">vCenter Server 컴퓨터를 백업하는 데 필요한 사용자 자격 증명을 설정하려면 특정 권한이 있는 역할을 만든 다음 사용자 계정을 역할과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="0be87-179">Azure Backup Server는 사용자 이름과 암호를 사용하여 vCenter Server를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="0be87-180">Azure Backup Server는 이러한 자격 증명을 모든 백업 작업에 대한 인증으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="0be87-181">백업 관리자에 대한 vCenter Server 역할 및 해당 권한을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="0be87-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="0be87-182">VCenter 서버에 로그인한 다음 vCenter Server **탐색기** 패널에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![vCenter Server 탐색기 패널의 관리 옵션](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="0be87-184">**관리**에서 **역할**을 선택한 다음 **역할** 패널에서 역할 추가 아이콘(+ 기호)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![역할 추가](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="0be87-186">**역할 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-186">The **Create Role** dialog box appears.</span></span>

    ![역할 만들기](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="0be87-188">**역할 만들기** 대화 상자의 **역할 이름** 상자에 *BackupAdminRole*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="0be87-189">역할 이름은 원하는 대로 사용할 수 있지만 이름은 역할의 목적에 대해 쉽게 인식할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="0be87-190">해당 vCenter 버전에 대한 권한을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="0be87-191">다음 표에는 vCenter 6.0 및 vCenter 5.5에 필요한 권한이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="0be87-192">권한을 선택할 때 부모 레이블 옆의 아이콘을 클릭하여 부모를 확장하고 자식 권한을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="0be87-193">VirtualMachine 권한을 선택하려면 부모 자식 계층으로 여러 개의 수준을 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="0be87-194">부모 권한 내 모든 자식 권한을 선택하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![부모 자식 권한 계층 구조](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="0be87-196">**확인**을 클릭하면 새 역할이 역할 패널에 있는 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="0be87-197">vCenter 6.0에 대한 권한</span><span class="sxs-lookup"><span data-stu-id="0be87-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="0be87-198">vCenter 5.5에 대한 권한</span><span class="sxs-lookup"><span data-stu-id="0be87-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="0be87-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="0be87-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="0be87-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="0be87-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="0be87-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="0be87-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="0be87-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="0be87-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="0be87-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="0be87-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="0be87-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="0be87-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="0be87-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="0be87-205">Network.Assign</span></span> |
|<span data-ttu-id="0be87-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="0be87-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="0be87-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="0be87-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="0be87-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="0be87-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="0be87-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="0be87-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="0be87-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="0be87-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="0be87-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="0be87-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="0be87-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="0be87-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="0be87-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="0be87-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="0be87-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="0be87-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="0be87-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="0be87-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="0be87-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="0be87-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="0be87-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="0be87-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="0be87-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="0be87-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="0be87-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="0be87-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="0be87-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="0be87-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="0be87-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="0be87-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="0be87-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="0be87-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="0be87-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="0be87-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="0be87-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="0be87-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="0be87-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="0be87-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="0be87-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="0be87-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="0be87-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="0be87-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="0be87-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="0be87-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="0be87-229">vCenter Server 사용자 계정 및 사용 권한 만들기</span><span class="sxs-lookup"><span data-stu-id="0be87-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="0be87-230">권한이 있는 역할이 설정된 후 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="0be87-231">사용자 계정에는 이름과 암호가 있으며 이는 인증에 사용되는 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="0be87-232">사용자 계정을 만들려면 vCenter Server **탐색기** 패널에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![사용자 및 그룹 옵션](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="0be87-234">**vCenter 사용자 및 그룹** 패널이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter 사용자 및 그룹 패널](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="0be87-236">**vCenter 사용자 및 그룹** 패널에서 **사용자** 탭을 선택한 다음 사용자 추가 아이콘(+ 기호)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="0be87-237">**새 사용자** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="0be87-238">**새 사용자** 대화 상자에서 사용자의 정보를 추가한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="0be87-239">이 절차에서 사용자 이름은 BackupAdmin입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-239">In this procedure, the username is BackupAdmin.</span></span>

    ![새 사용자 대화 상자](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="0be87-241">새 사용자 계정이 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="0be87-242">사용자 계정을 역할과 연결하려면 **탐색기** 패널에서 **전역 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="0be87-243">**전역 권한** 패널에서 **관리** 탭을 선택한 다음 추가 아이콘(+ 기호)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![전역 권한 패널](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="0be87-245">**전역 권한 루트 - 권한 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="0be87-246">**전역 권한 루트 - 권한 추가** 대화 상자에서 **추가**를 클릭하여 사용자 또는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![사용자 또는 그룹 선택](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="0be87-248">**사용자/그룹 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="0be87-249">**사용자/그룹 선택** 대화 상자에서 **BackupAdmin**을 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="0be87-250">**사용자**에서 *domain\username* 형식이 사용자 계정에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="0be87-251">다른 도메인을 사용하려면 **도메인** 목록에서 원하는 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![BackupAdmin 사용자 추가](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="0be87-253">**확인**을 클릭하여 선택한 사용자를 **권한 추가** 대화 상자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="0be87-254">이제 사용자를 식별하였으므로 사용자를 역할에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="0be87-255">**할당된 역할**의 드롭다운 목록에서 **BackupAdminRole**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![사용자를 역할에 할당](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="0be87-257">**전역 권한** 패널의 **관리** 탭에서 새 사용자 계정 및 연결된 역할이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="0be87-258">Azure Backup Server에서 vCenter Server 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="0be87-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="0be87-259">Azure Backup Server에 VMware 서버를 추가하기 전에 [Azure Backup Server용 업데이트 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="0be87-260">Azure Backup Server를 열려면 Azure Backup Server 바탕 화면에서 아이콘을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Azure Backup Server 아이콘](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="0be87-262">데스크톱에서 아이콘을 찾을 수 없는 경우 설치된 앱 목록에서 Azure Backup Server를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="0be87-263">Azure Backup Server 앱 이름은 Microsoft Azure Backup입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="0be87-264">Azure Backup Server 콘솔에서 **관리**를 클릭하고 **프로덕션 서버**를 클릭한 다음 도구 리본에서 **VMware 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Azure Backup Server 콘솔](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="0be87-266">**자격 증명 관리** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="0be87-268">**자격 증명 관리** 대화 상자에서 **추가**를 클릭하여 **자격 증명 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="0be87-269">**자격 증명 추가** 대화 상자에서 새 자격 증명에 대한 이름 및 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="0be87-270">그런 다음 사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-270">Then specify the username and password.</span></span> <span data-ttu-id="0be87-271">이름(*Contoso Vcenter 자격 증명*)은 다음 절차에서 자격 증명을 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="0be87-272">vCenter Server에서 사용되는 것과 동일한 사용자 이름과 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="0be87-273">vCenter Server와 Azure Backup Server가 동일한 도메인에 없는 경우 **사용자 이름**에서 도메인을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Azure Backup Server 자격 증명 추가 대화 상자](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="0be87-275">**추가**를 클릭하여 Azure Backup Server에 새 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="0be87-276">새 자격 증명이 **자격 증명 관리** 대화 상자의 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="0be87-278">**자격 증명 관리** 대화 상자를 닫으려면 오른쪽 위 모서리에 있는 **X**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="0be87-279">Azure Backup Server에 vCenter Server 추가</span><span class="sxs-lookup"><span data-stu-id="0be87-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="0be87-280">프로덕션 서버 추가 마법사를 사용하여 Azure Backup Server에 vCenter Server를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="0be87-281">프로덕션 서버 추가 마법사를 열려면 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="0be87-282">Azure Backup Server 콘솔에서 **관리**, **프로덕션 서버**를 차례로 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![프로덕션 서버 추가 마법사 열기](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="0be87-284">**프로덕션 서버 추가 마법사** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![프로덕션 서버 추가 마법사](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="0be87-286">**프로덕션 서버 형식 선택** 페이지에서 **VMware 서버**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="0be87-287">**서버 이름/IP 주소**에서 VMware 서버의 FQDN(정규화된 도메인 이름) 또는 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="0be87-288">모든 ESXi 서버를 동일한 vCenter가 관리하는 경우 vCenter 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![VMware 서버 FQDN 또는 IP 주소 지정](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="0be87-290">**SSL 포트**에서 VMware 서버와 통신하는 데 사용되는 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="0be87-291">다른 포트가 필요하지 않는 한 기본 포트인 포트 443을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="0be87-292">**자격 증명 지정**에서 이전에 만든 자격 증명을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![자격 증명 지정](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="0be87-294">**추가**를 클릭하여 VMware 서버를 **추가된 VMware 서버** 목록에 추가하고 **다음**을 클릭하여 마법사에서 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![VMWare 서버 및 자격 증명 추가](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="0be87-296">**요약** 페이지에서 **추가**를 클릭하여 지정된 VMware 서버를 Azure Backup Server에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Azure Backup Server에 VMware 서버 추가](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="0be87-298">VMware 서버 백업은 에이전트 없이 진행되는 백업이며 새 서버가 즉시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="0be87-299">**마침** 페이지에 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-299">The **Finish** page shows you the results.</span></span>

  ![마침 페이지](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="0be87-301">VCenter Server의 여러 인스턴스를 Azure Backup Server에 추가하려면 이 섹션의 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="0be87-302">Azure Backup Server에 vCenter Server를 추가한 후 다음 단계로 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="0be87-303">보호 그룹은 단기 또는 장기 보존에 대한 다양한 세부 정보를 지정하며, 사용자가 백업 정책을 정의 및 적용하는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="0be87-304">백업 정책은 백업이 발생하는 시기 및 백업되는 항목에 대한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="0be87-305">보호 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="0be87-305">Configure a protection group</span></span>

<span data-ttu-id="0be87-306">System Center Data Protection Manager 또는 Azure Backup Server를 사용해 본 적이 없다면 [디스크 백업 계획](https://technet.microsoft.com/library/hh758026.aspx)을 참조하여 하드웨어 환경을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="0be87-307">적절한 저장소가 있는지 확인한 후 새 보호 그룹 만들기 마법사를 사용하여 VMware Virtual Machines를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="0be87-308">Azure Backup Server 콘솔에서 **보호**를 클릭하고 도구 리본에서 **새로 만들기**를 클릭하여 새 보호 그룹 만들기 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![새 보호 그룹 만들기 마법사 열기](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="0be87-310">**새 보호 그룹 만들기** 마법사 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![새 보호 그룹 만들기 마법사 대화 상자](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="0be87-312">**다음**을 클릭하여 **보호 그룹 형식 선택** 페이지로 넘어갑니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="0be87-313">**보호 그룹 형식 선택** 페이지에서 **서버**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="0be87-314">**그룹 구성원 선택** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="0be87-315">**그룹 구성원 선택** 페이지에 사용 가능한 구성원 및 선택한 구성원이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="0be87-316">보호할 구성원을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![그룹 구성원 선택](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="0be87-318">구성원을 선택할 때 다른 폴더 또는 VM을 포함하는 폴더를 선택하면 포함되는 폴더 및 VM도 함께 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="0be87-319">상위 폴더에 폴더와 VM이 포함되는 것을 폴더 수준 보호라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="0be87-320">폴더 또는 VM을 제거하려면 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="0be87-321">VM 또는 VM을 포함하는 폴더가 이미 Azure에서 보호되는 경우 해당 VM을 다시 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="0be87-322">즉, VM은 한 번 Azure에서 보호되면 다시 보호할 수 없습니다. 이는 하나의 VM에 대해 중복 복구 지점이 생성되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="0be87-323">Azure Backup Server 인스턴스가 이미 구성원을 보호하는지 확인하려는 경우 구성원을 가리켜서 보호하는 서버의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="0be87-324">**데이터 보호 방법 선택** 페이지에서 보호 그룹에 사용할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="0be87-325">단기 보호(디스크) 및 온라인 보호가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="0be87-326">Azure에 온라인 보호를 사용하려면 디스크에 대한 단기 보호를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="0be87-327">**다음**을 클릭하여 단기 보호 범위로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![데이터 보호 방법 선택](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="0be87-329">**단기 목표 지정** 페이지의 **보존 범위**에서 *디스크에 저장된* 복구 지점을 유지할 원하는 일 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="0be87-330">복구 지점을 생성할 때 시간 및 일 수를 변경하려면 **수정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="0be87-331">단기 복구 지점은 전체 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="0be87-332">증분 백업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-332">They are not incremental backups.</span></span> <span data-ttu-id="0be87-333">단기 목표를 충족하는 경우 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![단기 목표 지정](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="0be87-335">**디스크 할당 검토** 페이지에서 필요한 경우 검토하고 VM에 대한 디스크 공간을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="0be87-336">권장되는 디스크 할당은 **단기 목표 지정** 페이지에서 지정한 보존 범위, 워크로드의 형식 및 보호된 데이터의 크기(3단계에서 식별됨)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="0be87-337">**데이터 크기:** 보호 그룹의 데이터 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="0be87-338">**디스크 공간:** 보호 그룹에 권장되는 디스크 공간의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="0be87-339">이 설정을 수정하려는 경우 총 공간을 각 데이터 원본의 예상 확장량보다 약간 더 크게 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="0be87-340">**데이터 공동 배치:** 공동 배치를 사용하는 경우 보호되는 여러 데이터 원본은 단일 복제본 및 복구 지점 볼륨에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="0be87-341">공동 배치는 모든 워크로드에 지원되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="0be87-342">**자동 증가:** 이 설정을 사용하는 경우 보호되는 그룹의 데이터가 초기 할당량을 초과하면 System Center Data Protection Manager가 25%까지 디스크 크기 증가를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="0be87-343">**저장소 풀 세부 정보:** 총 디스크 크기 및 남아 있는 디스크 크기를 포함한 저장소 풀의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![디스크 할당 검토](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="0be87-345">할당된 공간이 만족스러운 경우 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="0be87-346">**복제본 만들기 방법 선택** 페이지에서 초기 복사본 또는 Azure Backup Server에서 보호되는 데이터의 복제본을 생성하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="0be87-347">기본 설정은 **네트워크를 통해 자동으로** 및 **지금**입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="0be87-348">기본값을 사용하는 경우 사용량이 적은 시간을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="0be87-349">**나중에**를 선택하고 날짜와 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="0be87-350">대용량 데이터이거나 네트워크 상태가 최적화되지 않은 경우 이동식 미디어를 사용하여 데이터를 오프라인으로 복제하는 것을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="0be87-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="0be87-351">선택을 완료한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-351">After you have made your choices, click **Next**.</span></span>

    ![복제본 만들기 방법 선택](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="0be87-353">**일관성 확인 옵션** 페이지에서 일관성 확인을 자동화할 방법 및 시기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="0be87-354">복제 데이터가 일관성을 잃은 경우 또는 설정된 일정에 따라 일관성 확인을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="0be87-355">자동 일관성 확인을 구성하지 않으려면 수동 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="0be87-356">Azure Backup Server 콘솔의 보호 영역에서 보호 그룹을 마우스 오른쪽 단추로 클릭한 다음 **일관성 확인 수행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="0be87-357">**다음**을 클릭하여 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="0be87-358">**온라인 보호 데이터 지정** 페이지에서 보호하려는 하나 이상의 데이터 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="0be87-359">구성원을 개별적으로 선택하거나 **모두 선택**을 클릭하여 모든 구성원을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="0be87-360">구성원을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-360">After you choose the members, click **Next**.</span></span>

    ![온라인 보호 데이터 지정](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="0be87-362">**온라인 백업 일정 지정** 페이지에서 디스크 백업에서 복구 지점을 생성하기 위한 일정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="0be87-363">복구 지점이 생성되면 Azure에서 Recovery Services 자격 증명 모음으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="0be87-364">온라인 백업 일정에 만족한다면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![온라인 백업 일정 지정](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="0be87-366">**온라인 보존 정책 지정** 페이지에서 Azure의 백업 데이터를 유지하고자 하는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="0be87-367">정책을 정의한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-367">After the policy is defined, click **Next**.</span></span>

    ![온라인 보존 정책 지정](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="0be87-369">Azure에서 데이터를 유지할 수 있는 기간에 대한 시간 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="0be87-370">Azure에 복구 지점 데이터를 저장하는 경우 보호되는 인스턴스당 9999개 미만의 복구 지점을 사용해야 한다는 점이 유일한 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="0be87-371">이 예제에서 보호되는 인스턴스는 VMware 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="0be87-372">**요약** 페이지에서 보호 그룹 구성원 및 설정에 대한 세부 정보를 검토한 다음 **그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![보호 그룹 구성원 및 설정 요약](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="0be87-374">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0be87-374">Next steps</span></span>
<span data-ttu-id="0be87-375">Azure Backup Server를 사용하여 VMware 워크로드를 보호하고 있다면 Azure Backup Server를 사용하여 [Microsoft Exchange Server](./backup-azure-exchange-mabs.md), [Microsoft SharePoint 팜](./backup-azure-backup-sharepoint-mabs.md) 또는 [SQL Server 데이터베이스](./backup-azure-sql-mabs.md)를 보호하는 것에 관심이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be87-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="0be87-376">에이전트 등록, 보호 그룹 구성 또는 작업 백업 관련 문제에 관한 정보는 [Azure Backup Server 문제 해결](./backup-azure-mabs-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0be87-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
