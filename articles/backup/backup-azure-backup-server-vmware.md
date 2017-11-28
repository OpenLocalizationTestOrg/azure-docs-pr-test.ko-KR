---
title: "Azure 백업 서버도 VMware 서버를 aaaBack | Microsoft Docs"
description: "Azure 백업 서버 tooback VMware vCenter/ESXi 서버 tooAzure 또는 디스크를 사용 합니다. 이 문서에서는 VMware 워크로드를 백업(또는 보호)하기 위한 단계별 지침을 제공합니다."
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
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="a908c-104">VMware 서버 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="a908c-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="a908c-105">이 문서에서는 Azure 백업 서버 toohelp tooconfigure VMware 서버 작업을 보호 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="a908c-106">이 문서에서는 Azure Backup Server가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="a908c-107">설치 된 Azure 백업 서버를 설정 하지 않은 경우 참조 [tooback Azure 백업 서버를 사용 하 여 워크 로드를 준비](backup-azure-microsoft-azure-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="a908c-108">Azure Backup Server는 VMware vCenter Server 버전 6.5, 6.0 및 5.5를 백업하거나 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="a908c-109">보안 연결 toohello vCenter 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="a908c-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="a908c-110">기본적으로 Azure Backup Server는 HTTPS 채널을 통해 각 vCenter Server와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="a908c-111">hello 보안 통신에 tooturn, Azure 백업 서버에 hello VMware CA (인증 기관) 인증서를 설치 하는 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="a908c-112">보안 통신에 필요 없는 toodisable hello HTTPS 요구 사항이 하려는 경우 참조 [사용 안 함 보안 통신 프로토콜](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="a908c-113">Azure 백업 서버 hello vCenter 서버와 보안 연결 toocreate hello Azure 백업 서버에서 신뢰할 수 있는 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="a908c-114">일반적으로 hello vSphere 웹 클라이언트를 통해 hello Azure 백업 서버 컴퓨터 tooconnect toohello vCenter 서버에서 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="a908c-115">hello hello Azure 백업 서버 브라우저 tooconnect toohello vCenter Server를 사용 하 여 처음으로 hello 연결 보안이 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="a908c-116">다음 이미지는 hello hello 보안 되지 않은 연결을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-116">hello following image shows hello unsecured connection.</span></span>

![보안 되지 않은 연결 tooVMware 서버의 예](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="a908c-118">toofix이 문제를 하 고 보안 연결 hello 신뢰할 수 있는 루트 CA 인증서를 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="a908c-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="a908c-119">Azure 백업 서버 hello 브라우저에서 hello URL toohello vSphere 웹 클라이언트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="a908c-120">hello vSphere 웹 클라이언트 로그인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere Web Client](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="a908c-122">관리자와 개발자에 대 한 hello 정보의 hello 아래쪽 hello 찾을 **신뢰할 수 있는 루트 CA 인증서 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![링크 toodownload hello 신뢰할 수 있는 루트 CA 인증서](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="a908c-124">Hello vSphere 웹 클라이언트 로그인 페이지에 표시 되지 않으면, 브라우저의 프록시 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="a908c-125">**신뢰할 수 있는 루트 CA 인증서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="a908c-126">hello vCenter Server tooyour 로컬 컴퓨터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="a908c-127">hello 파일의 이름이 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-127">hello file's name is named **download**.</span></span> <span data-ttu-id="a908c-128">묻는 메시지가 나타나면 브라우저에 따라 여부 tooopen 또는 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![인증서 다운로드 시 나타나는 다운로드 메시지](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="a908c-130">Azure 백업 서버 hello 파일 tooa 위치를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="a908c-131">Hello 파일을 저장할 때 hello.zip 파일 이름 확장명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="a908c-132">hello 파일은 hello 인증서에 대 한 hello 정보를 포함 하는.zip 파일.</span><span class="sxs-lookup"><span data-stu-id="a908c-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="a908c-133">Hello.zip 확장명을 가진 hello 추출 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="a908c-134">마우스 오른쪽 단추로 클릭 **download.zip**를 선택한 후 **압축 풀기** tooextract hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="a908c-135">hello.zip 파일의 내용을 tooa 폴더 이름이 추출 **인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="a908c-136">두 유형의 파일 hello 인증서 폴더에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="a908c-137">hello 루트 인증서 파일의.0 및.1 시퀀스 번호가 매겨진된로 시작 하는 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="a908c-138">hello CRL 파일의.r0 또는.r1 시퀀스로 시작 하는 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="a908c-139">hello CRL 파일은 한 인증서와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="a908c-140">로컬로 추출된 다운로드 파일</span><span class="sxs-lookup"><span data-stu-id="a908c-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="a908c-141">Hello에 **인증서** 폴더 hello 루트 인증서 파일을 마우스 오른쪽 단추로 클릭 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="a908c-142">루트 인증서 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="a908c-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="a908c-143">확장 too.crt hello 루트 인증서를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="a908c-144">ख ा त toochange hello 확장명 인 경우 클릭 묻는 경우 **예** 또는 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="a908c-145">그렇지 않으면 hello 파일의 기능을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="a908c-146">루트 인증서를 나타내는 hello 파일 변경 내용 tooan 아이콘에 대 한 hello 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="a908c-147">Hello 루트 인증서를 마우스 오른쪽 단추로 클릭 하 고 hello 팝업 메뉴에서 선택 **인증서 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="a908c-148">hello **인증서 가져오기 마법사** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="a908c-149">Hello에 **인증서 가져오기 마법사** 대화 상자에서 **로컬 컴퓨터** hello 인증서 및 클릭 한 다음에 대 한 hello 대상으로 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="a908c-150">인증서 저장소 대상 옵션</span><span class="sxs-lookup"><span data-stu-id="a908c-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="a908c-151">클릭 하 여 원하는 변경 내용을 toohello 컴퓨터 tooallow 묻는 **예** 또는 **확인**, tooall hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="a908c-152">Hello에 **인증서 저장소** 페이지에서 **모든 인증서 저장소를 다음 hello에 저장**, 클릭 하 고 **찾아보기** toochoose hello 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![특정 저장소 위치에 인증서 저장](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="a908c-154">hello **인증서 저장소 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![인증서 저장소 폴더 계층 구조](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="a908c-156">선택 **신뢰할 수 있는 루트 인증 기관** hello 인증서 및 클릭 한 다음에 대 한 hello 대상 폴더로 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![인증서 대상 폴더](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="a908c-158">hello **신뢰할 수 있는 루트 인증 기관** 폴더 hello 인증서 저장소로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="a908c-159">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-159">Click **Next**.</span></span>

    ![인증서 저장소 폴더](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="a908c-161">Hello에 **완료 hello 인증서 가져오기 마법사** 페이지, 해당 hello 인증서 hello 원하는 폴더에 있는지 확인 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![인증서가 hello 적절 한 폴더를 확인 하십시오.](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="a908c-163">대화 상자가 나타나면 hello 성공적인 인증서 가져오기 확인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="a908c-164">사용자 연결이 보호 되는 서버 tooconfirm toohello vCenter에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="a908c-165">Hello 인증서 가져오기 성공 하 고 보안 연결을 설정할 수 없습니다, 경우에 hello VMware vSphere 설명서를 참조 [서버 인증서 얻기](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="a908c-166">보안 경계, 조직 내의 tooturn hello HTTPS 프로토콜에 원하지 프로시저 toodisable hello 보안 통신을 수행 하는 hello를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a908c-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="a908c-167">보안 통신 프로토콜 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="a908c-167">Disable secure communication protocol</span></span>

<span data-ttu-id="a908c-168">조직 hello HTTPS 프로토콜을 요구 하지 않는 단계 toodisable HTTPS 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="a908c-169">toodisable hello 기본 동작을 hello 기본 동작을 무시 하는 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="a908c-170">복사 하 여.txt 파일에 텍스트를 다음 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="a908c-171">Hello 파일 tooyour Azure 백업 서버 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="a908c-172">Hello 파일 이름에 대해 DisableSecureAuthentication.reg를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="a908c-173">Hello 파일 tooactivate hello 레지스트리 항목을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="a908c-174">Hello vCenter Server에서 역할 및 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a908c-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="a908c-175">Hello vCenter Server에서 역할에는 미리 정의 된 권한 집합이.</span><span class="sxs-lookup"><span data-stu-id="a908c-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="a908c-176">VCenter 서버 관리자는 hello 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="a908c-177">tooassign 권한을 관리자에 게 역할을 갖는 사용자 계정 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="a908c-178">tooestablish hello 필요한 사용자 자격 증명 tooback hello vCenter 서버 컴퓨터를 특정 권한을 가진 역할을 만듭니다와 hello 역할 hello 사용자 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="a908c-179">Azure 백업 서버 hello vCenter 서버를 사용자 이름 및 암호 tooauthenticate를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="a908c-180">Azure Backup Server는 이러한 자격 증명을 모든 백업 작업에 대한 인증으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="a908c-181">tooadd vCenter 서버 역할 및 백업 관리자에 대 한 해당 권한을:</span><span class="sxs-lookup"><span data-stu-id="a908c-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="a908c-182">Toohello vCenter 서버를 찾은 다음 hello vCenter Server에서에서 로그인 **탐색기** 에서 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![vCenter Server 탐색기 패널의 관리 옵션](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="a908c-184">**관리** 선택 **역할**, 한 다음 hello **역할** 패널 클릭 hello 역할 아이콘 (hello + 기호)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![역할 추가](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="a908c-186">hello **역할 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-186">hello **Create Role** dialog box appears.</span></span>

    ![역할 만들기](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="a908c-188">Hello에 **Create Role** 대화 상자의 hello **역할 이름** 상자에 입력 *BackupAdminRole*합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="a908c-189">hello 역할 이름이 든 수는 있지만 hello 역할의 용도 대 한 인식할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="a908c-190">Hello, vCenter의 적절 한 버전에 대 한 hello 권한을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="a908c-191">다음 표에서 hello vCenter 6.0 및 5.5 vCenter에 대 한 hello 필요한 권한을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="a908c-192">Hello 권한을 선택 하면 hello 아이콘 다음 toohello 부모 레이블 tooexpand hello 부모 및 보기 hello 자식 권한을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="a908c-193">toogo 해야 tooselect hello VirtualMachine 권한 hello에 여러 개의 수준이 부모 자식 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="a908c-194">부모 권한 내에서 모든 자식 권한을 tooselect을 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![부모 자식 권한 계층 구조](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="a908c-196">클릭 한 후 **확인**, 새 역할 hello hello 역할 패널에 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="a908c-197">vCenter 6.0에 대한 권한</span><span class="sxs-lookup"><span data-stu-id="a908c-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="a908c-198">vCenter 5.5에 대한 권한</span><span class="sxs-lookup"><span data-stu-id="a908c-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="a908c-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a908c-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="a908c-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a908c-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="a908c-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="a908c-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="a908c-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="a908c-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="a908c-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="a908c-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="a908c-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="a908c-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="a908c-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a908c-205">Network.Assign</span></span> |
|<span data-ttu-id="a908c-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a908c-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="a908c-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="a908c-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="a908c-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a908c-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="a908c-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a908c-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="a908c-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="a908c-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="a908c-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="a908c-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="a908c-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a908c-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="a908c-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a908c-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="a908c-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="a908c-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="a908c-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="a908c-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="a908c-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a908c-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="a908c-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a908c-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="a908c-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a908c-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="a908c-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a908c-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="a908c-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a908c-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="a908c-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a908c-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="a908c-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="a908c-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="a908c-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a908c-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="a908c-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a908c-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="a908c-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a908c-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="a908c-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a908c-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="a908c-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a908c-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="a908c-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a908c-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="a908c-229">vCenter Server 사용자 계정 및 사용 권한 만들기</span><span class="sxs-lookup"><span data-stu-id="a908c-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="a908c-230">권한과 함께 hello 역할을 설정한 후에 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="a908c-231">hello 사용자 계정 이름 및 암호 인증에 사용 되는 hello 자격 증명을 제공 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="a908c-232">toocreate hello vCenter 서버에에서 사용자 계정 **탐색기** 에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![사용자 및 그룹 옵션](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="a908c-234">hello **vCenter 사용자 및 그룹** 다음과 같은 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter 사용자 및 그룹 패널](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="a908c-236">Hello에 **vCenter 사용자 및 그룹** 패널, 선택 hello **사용자** 탭을 클릭 한 다음 hello 사용자 아이콘 (hello + 기호)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="a908c-237">hello **새 사용자** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="a908c-238">Hello에 **새 사용자** 대화 상자, hello 사용자 정보를 추가 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="a908c-239">이 절차에서는 hello 사용자 BackupAdmin 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![새 사용자 대화 상자](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="a908c-241">새 사용자 계정을 hello hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="a908c-242">hello 역할 hello에 tooassociate hello 사용자 계정을 **탐색기** 에서 **전역 권한을**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="a908c-243">Hello에 **전역 권한을** 패널, 선택 hello **관리** 탭을 클릭 한 다음 hello (hello + 기호) 아이콘을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![전역 권한 패널](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="a908c-245">hello **전역 권한을 루트-권한 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="a908c-246">Hello에 **전역 권한 루트-권한 추가** 대화 상자를 클릭 **추가** toochoose hello 사용자 또는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![사용자 또는 그룹 선택](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="a908c-248">hello **사용자/그룹 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="a908c-249">Hello에 **사용자/그룹 선택** 대화 상자에서 선택 **BackupAdmin** 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="a908c-250">**사용자**, hello *domain\username* 형식은 hello 사용자 계정에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="a908c-251">다른 도메인 toouse 원한다 면 hello에서 선택 **도메인** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![BackupAdmin 사용자 추가](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="a908c-253">클릭 **확인** tooadd hello 선택 사용자 toohello **권한 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a908c-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="a908c-254">Hello 사용자를 식별 했으면 했으므로 hello 사용자 toohello 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="a908c-255">**역할 할당**, hello 드롭 다운 목록에서 선택 **BackupAdminRole**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![사용자 toorole 할당](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="a908c-257">Hello에 **관리** hello 탭 **전역 권한을** 패널, hello 새 사용자 계정 및 연결 된 hello 역할 hello 목록에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="a908c-258">Azure Backup Server에서 vCenter Server 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="a908c-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="a908c-259">Hello VMware 서버 tooAzure 백업 서버를 추가 하기 전에 설치 [Azure 백업 서버에 대 한 업데이트 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="a908c-260">tooopen Azure 백업 서버 hello hello Azure 백업 서버 바탕 화면 아이콘을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Azure Backup Server 아이콘](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="a908c-262">Hello 아이콘 hello 바탕 화면에서를 찾을 수 없는 경우 설치 된 응용 프로그램의 hello 목록에서 Azure 백업 서버를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="a908c-263">hello Azure 백업 서버 응용 프로그램 이름에는 Microsoft Azure 백업 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="a908c-264">Hello Azure 백업 서버 콘솔에서 클릭 **관리**, 클릭 **프로덕션 서버**, hello 도구 리본에서을 클릭 하 고 **VMware 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Azure Backup Server 콘솔](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="a908c-266">hello **자격 증명 관리** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="a908c-268">Hello에 **자격 증명 관리** 대화 상자를 클릭 **추가** tooopen hello **자격 증명 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a908c-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="a908c-269">Hello에 **자격 증명 추가** 대화 상자에 이름과 hello 새 자격 증명에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="a908c-270">다음 hello 사용자 이름 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-270">Then specify hello username and password.</span></span> <span data-ttu-id="a908c-271">hello 이름 *Contoso Vcenter 자격 증명* 사용 hello 다음 절차에서 tooidentify hello 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="a908c-272">사용 하 여 hello 동일한 사용자 이름 및 암호에 사용 되는 vCenter Server hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="a908c-273">Hello vCenter Server 및 Azure 백업 서버에 없는 경우 동일한 도메인에 hello **사용자 이름**, hello 도메인을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Azure Backup Server 자격 증명 추가 대화 상자](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="a908c-275">클릭 **추가** tooadd hello 새 자격 증명 tooAzure 백업 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="a908c-276">새 자격 증명 hello hello hello 목록에 표시 **자격 증명 관리** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a908c-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="a908c-278">tooclose hello **자격 증명 관리** 대화 상자에서 hello 클릭 **X** hello 오른쪽 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="a908c-279">Hello vCenter 서버 tooAzure 백업 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="a908c-280">프로덕션 서버 추가 마법사가 사용 되는 tooadd hello vCenter 서버 tooAzure 백업 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="a908c-281">tooopen 프로덕션 서버 추가 마법사를 완료 hello 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="a908c-282">Hello Azure 백업 서버 콘솔에서 클릭 **관리**, 클릭 **프로덕션 서버**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![프로덕션 서버 추가 마법사 열기](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="a908c-284">hello **프로덕션 서버 추가 마법사** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![프로덕션 서버 추가 마법사](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="a908c-286">Hello에 **프로덕션 서버 선택 형식** 페이지 **VMware 서버**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="a908c-287">**서버 이름/i P 주소**, hello 정규화 된 도메인 이름 (FQDN) 또는 IP 주소 hello VMware 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="a908c-288">모든 hello ESXi 서버 hello 하 여 관리 되는 경우 동일한 vCenter hello vCenter 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![VMware 서버 FQDN 또는 IP 주소 지정](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="a908c-290">**SSL 포트**를 사용 하는 toocommunicate hello VMware 서버와는 hello 포트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="a908c-291">다른 포트는 필요 하지 않는 한 hello 기본 포트는 포트 443을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="a908c-292">**자격 증명 지정**, 선택 hello 앞에서 만든 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="a908c-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![자격 증명 지정](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="a908c-294">클릭 **추가** tooadd hello VMware 서버 toohello 목록으로 **VMware 서버 추가**, 클릭 하 고 **다음** toomove toohello hello 마법사의 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![VMWare 서버 및 자격 증명 추가](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="a908c-296">Hello에 **요약** 페이지 **추가** tooadd hello VMware 서버 tooAzure 백업 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![VMware server tooAzure 백업 서버를 추가 합니다.](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="a908c-298">hello VMware 서버 백업은 에이전트 없는 백업 이며 새 서버 hello 즉시 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="a908c-299">hello **마침** 페이지 결과 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-299">hello **Finish** page shows you hello results.</span></span>

  ![마침 페이지](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="a908c-301">이 섹션의 단계를 여러 개 vCenter 서버 tooAzure 백업 서버를 이전 반복 hello tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="a908c-302">Hello vCenter 서버 tooAzure 백업 서버를 추가한 후 hello 다음 단계는 toocreate 보호 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="a908c-303">hello 보호 그룹 지정 hello 짧은 또는 장기 보존에 대 한 다양 한 세부 정보는를 정의 하 고 hello 백업 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="a908c-304">hello 백업 정책은 백업 진행 시기 및 백업할 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="a908c-305">보호 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="a908c-305">Configure a protection group</span></span>

<span data-ttu-id="a908c-306">System Center Data Protection Manager 또는 하기 전에 Azure 백업 서버를 사용 하지 않은 경우 참조 [디스크 백업에 대 한 계획](https://technet.microsoft.com/library/hh758026.aspx) tooprepare 하드웨어 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="a908c-307">적절 한 저장소 있는지 확인 한 후에 hello 새 보호 그룹 만들기 마법사 tooadd VMware 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="a908c-308">Hello Azure 백업 서버 콘솔에서 클릭 **보호**, hello 도구 리본에서을 클릭 하 고 **새로** tooopen hello 새 보호 그룹 만들기 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![열기 hello 새 보호 그룹 만들기 마법사](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="a908c-310">hello **새 보호 그룹 만들기** 마법사 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![새 보호 그룹 만들기 마법사 대화 상자](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="a908c-312">클릭 **다음** tooadvance toohello **보호 그룹 종류 선택** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a908c-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="a908c-313">Hello에 **선택 보호 그룹 종류** 페이지 **서버** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="a908c-314">hello **그룹 구성원 선택** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="a908c-315">Hello에 **그룹 구성원 선택** 페이지, 사용 가능한 구성원 hello 및 hello 선택한 멤버를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="a908c-316">Hello 멤버 tooprotect를 원하고 클릭 한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![그룹 구성원 선택](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="a908c-318">구성원을 선택할 때 다른 폴더 또는 VM을 포함하는 폴더를 선택하면 포함되는 폴더 및 VM도 함께 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="a908c-319">hello 폴더 및 hello 상위 폴더에는 Vm의 hello 포함 폴더 수준 보호를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="a908c-320">tooremove 폴더 또는 VM을 선택 취소 hello 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="a908c-321">VM 또는 VM에 포함 된 폴더가 이미 보호 된 tooAzure 인 경우 해당 VM을 다시 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="a908c-322">즉, VM 보호 tooAzure 후 보호할 수 없습니다 다시 중복 된 복구 지점을 하나의 VM에 대 한 만들어지지 않도록 방지 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="a908c-323">Toosee 하려는 경우 멤버, 지점 toohello toosee hello의 이름 서버를 보호 하는 hello Azure 백업 서버 인스턴스를 이미 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="a908c-324">Hello에 **데이터 보호 방법 선택** 페이지 hello 보호 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="a908c-325">단기 보호 (toodisk) 및 온라인 보호 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="a908c-326">Toouse 온라인 보호 (tooAzure) 하려는 경우에 단기 보호 toodisk를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="a908c-327">클릭 **다음** tooproceed toohello 단기 보호 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![데이터 보호 방법 선택](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="a908c-329">Hello에 **단기 목표 지정** 페이지에 대 한 **보존 범위**, hello tooretain 복구 지점에 원하는 일 수가 지정 *toodisk 저장*합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="a908c-330">Toochange hello 시간 및 복구 지점을 수행 되는 경우 일, 클릭 **수정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="a908c-331">hello 단기 복구 지점은 전체 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="a908c-332">증분 백업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-332">They are not incremental backups.</span></span> <span data-ttu-id="a908c-333">클릭 하 여 hello 단기 목표 만족 스 러 우면 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![단기 목표 지정](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="a908c-335">Hello에 **디스크 할당 검토** 페이지를 검토 하 고 필요한 경우, Vm hello에 대 한 hello 디스크 공간을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="a908c-336">hello hello에 지정 된 hello 보존 범위를 기준으로 하는 디스크 할당 권장 **단기 목표 지정** 페이지, 작업, hello 유형 및 hello의 hello 크기 보호 된 데이터 (3 단계에서 식별 됨).</span><span class="sxs-lookup"><span data-stu-id="a908c-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="a908c-337">**데이터 크기:** hello 보호 그룹의 hello 데이터의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="a908c-338">**디스크 공간:** hello hello 보호 그룹에 대 한 디스크 공간의 크기를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="a908c-339">이 설정은 toomodify을 원하는 경우 각 데이터 원본 증가 예측 하는 hello 크기 보다 약간 더 큰 총 공간을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="a908c-340">**데이터 배치:** hello 보호 데이터 원본을 여러 개 tooa 단일 복제본 및 복구 지점 볼륨에 매핑할 수 공동 배치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="a908c-341">공동 배치는 모든 워크로드에 지원되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="a908c-342">**자동 증가:** hello 보호 그룹의 데이터 hello 초기 할당 보다 커지면 경우이 설정 켜기, 하는 경우 System Center Data Protection Manager 25% tooincrease hello 디스크 크기를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="a908c-343">**저장소 풀 세부 정보:** 합계를 포함 하 여 크기 및 남은 디스크 크기 hello 저장소 풀의 hello 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![디스크 할당 검토](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="a908c-345">Hello 공간 할당에 만족 했으면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="a908c-346">Hello에 **복제본 만들기 방법 선택** 페이지에서 원하는 toogenerate hello 초기 복사본, 즉 Azure 백업 서버 hello 보호 된 데이터의 복제본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="a908c-347">hello 기본값은 **hello 네트워크를 통해 자동으로** 및 **이제**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="a908c-348">Hello 기본값을 사용 하는 경우에 사용량이 적은 시간을 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="a908c-349">**나중에**를 선택하고 날짜와 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="a908c-350">대용량 데이터 또는 작음 보다 최적의 네트워크 상태, 이동식 미디어를 사용 하 여 hello 오프 라인으로 데이터를 복제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="a908c-351">선택을 완료한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-351">After you have made your choices, click **Next**.</span></span>

    ![복제본 만들기 방법 선택](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="a908c-353">Hello에 **일관성 확인 옵션** 페이지에서 tooautomate hello 일관성 검사 하는 방법 및 시기.</span><span class="sxs-lookup"><span data-stu-id="a908c-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="a908c-354">복제 데이터가 일관성을 잃은 경우 또는 설정된 일정에 따라 일관성 확인을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="a908c-355">Tooconfigure 자동 일관성 검사를 사용 하지 않으려는 경우에 수동 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="a908c-356">Hello Azure 백업 서버 콘솔의 hello 보호 영역에서 hello 보호 그룹을 마우스 오른쪽 단추로 클릭 한 다음 선택 **일관성 확인 수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="a908c-357">클릭 **다음** toomove toohello 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="a908c-358">Hello에 **온라인 보호 데이터 지정** 페이지에서 원하는 tooprotect 하나 이상의 데이터 원본을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="a908c-359">Hello 멤버를 개별적으로 선택 하거나 클릭 수 **모두 선택** toochoose 모든 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="a908c-360">Hello 멤버를 선택한 후 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-360">After you choose hello members, click **Next**.</span></span>

    ![온라인 보호 데이터 지정](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="a908c-362">Hello에 **온라인 백업 일정 지정** 페이지 hello 디스크 백업에서 hello 일정 toogenerate 복구 지점을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="a908c-363">Hello 복구 지점이 생성 된 후에 Azure 복구 서비스 자격 증명 모음 전송된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="a908c-364">Hello 온라인 백업 일정에 만족 했으면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![온라인 백업 일정 지정](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="a908c-366">Hello에 **온라인 보존 정책 지정** 페이지에서, tooretain hello Azure에서 백업 데이터를 원하는 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="a908c-367">Hello 정책을 정의한 후 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-367">After hello policy is defined, click **Next**.</span></span>

    ![온라인 보존 정책 지정](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="a908c-369">Azure에서 데이터를 유지할 수 있는 기간에 대한 시간 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="a908c-370">Azure에서 복구 지점 데이터를 저장 하는 경우 hello만 제한은 보호 된 인스턴스 당 9999 개 이상의 복구 지점을 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="a908c-371">이 예제에서는 보호 된 인스턴스 hello hello VMware 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="a908c-372">Hello에 **요약** 페이지, 보호 그룹 구성원 및 설정에 대 한 hello 세부 정보를 검토 한 다음 클릭 **그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![보호 그룹 구성원 및 설정 요약](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="a908c-374">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a908c-374">Next steps</span></span>
<span data-ttu-id="a908c-375">Azure 백업 서버 tooprotect VMware 작업을 사용 하면 Azure 백업 서버 toohelp 보호를 사용 하 여에 관심이 있을 수는 [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [Microsoft SharePoint 팜](./backup-azure-backup-sharepoint-mabs.md), 또는 [SQL Server 데이터베이스](./backup-azure-sql-mabs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="a908c-376">Hello 에이전트 등록 하 고 문제에 대 한 내용은 hello 보호 그룹을 구성 하거나 작업, 백업 참조 [Azure 백업 서버 문제를 해결](./backup-azure-mabs-troubleshoot.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908c-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
