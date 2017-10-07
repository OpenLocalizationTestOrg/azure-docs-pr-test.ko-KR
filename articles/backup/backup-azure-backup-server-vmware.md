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
# <a name="back-up-a-vmware-server-tooazure"></a>VMware 서버 tooAzure 백업

이 문서에서는 Azure 백업 서버 toohelp tooconfigure VMware 서버 작업을 보호 하는 방법을 설명 합니다. 이 문서에서는 Azure Backup Server가 이미 설치되어 있다고 가정합니다. 설치 된 Azure 백업 서버를 설정 하지 않은 경우 참조 [tooback Azure 백업 서버를 사용 하 여 워크 로드를 준비](backup-azure-microsoft-azure-backup.md)합니다.

Azure Backup Server는 VMware vCenter Server 버전 6.5, 6.0 및 5.5를 백업하거나 보호할 수 있습니다.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>보안 연결 toohello vCenter 서버 만들기

기본적으로 Azure Backup Server는 HTTPS 채널을 통해 각 vCenter Server와 통신합니다. hello 보안 통신에 tooturn, Azure 백업 서버에 hello VMware CA (인증 기관) 인증서를 설치 하는 두는 것이 좋습니다. 보안 통신에 필요 없는 toodisable hello HTTPS 요구 사항이 하려는 경우 참조 [사용 안 함 보안 통신 프로토콜](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)합니다. Azure 백업 서버 hello vCenter 서버와 보안 연결 toocreate hello Azure 백업 서버에서 신뢰할 수 있는 인증서를 가져옵니다.

일반적으로 hello vSphere 웹 클라이언트를 통해 hello Azure 백업 서버 컴퓨터 tooconnect toohello vCenter 서버에서 브라우저를 사용 합니다. hello hello Azure 백업 서버 브라우저 tooconnect toohello vCenter Server를 사용 하 여 처음으로 hello 연결 보안이 유지 되지 않습니다. 다음 이미지는 hello hello 보안 되지 않은 연결을 나타냅니다.

![보안 되지 않은 연결 tooVMware 서버의 예](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix이 문제를 하 고 보안 연결 hello 신뢰할 수 있는 루트 CA 인증서를 다운로드 하세요.

1. Azure 백업 서버 hello 브라우저에서 hello URL toohello vSphere 웹 클라이언트를 입력 합니다. hello vSphere 웹 클라이언트 로그인 페이지가 표시 됩니다.

    ![vSphere Web Client](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    관리자와 개발자에 대 한 hello 정보의 hello 아래쪽 hello 찾을 **신뢰할 수 있는 루트 CA 인증서 다운로드** 링크 합니다.

    ![링크 toodownload hello 신뢰할 수 있는 루트 CA 인증서](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Hello vSphere 웹 클라이언트 로그인 페이지에 표시 되지 않으면, 브라우저의 프록시 설정을 확인 합니다.

2. **신뢰할 수 있는 루트 CA 인증서 다운로드**를 클릭합니다.

    hello vCenter Server tooyour 로컬 컴퓨터 파일을 다운로드합니다. hello 파일의 이름이 **다운로드**합니다. 묻는 메시지가 나타나면 브라우저에 따라 여부 tooopen 또는 hello 파일을 저장 합니다.

    ![인증서 다운로드 시 나타나는 다운로드 메시지](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Azure 백업 서버 hello 파일 tooa 위치를 저장 합니다. Hello 파일을 저장할 때 hello.zip 파일 이름 확장명을 추가 합니다.

    hello 파일은 hello 인증서에 대 한 hello 정보를 포함 하는.zip 파일. Hello.zip 확장명을 가진 hello 추출 도구를 사용할 수 있습니다.

4. 마우스 오른쪽 단추로 클릭 **download.zip**를 선택한 후 **압축 풀기** tooextract hello 내용입니다.

    hello.zip 파일의 내용을 tooa 폴더 이름이 추출 **인증서**합니다. 두 유형의 파일 hello 인증서 폴더에 나타납니다. hello 루트 인증서 파일의.0 및.1 시퀀스 번호가 매겨진된로 시작 하는 확장명입니다.
    
    hello CRL 파일의.r0 또는.r1 시퀀스로 시작 하는 확장명입니다. hello CRL 파일은 한 인증서와 연결 합니다.

    ![로컬로 추출된 다운로드 파일 ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. Hello에 **인증서** 폴더 hello 루트 인증서 파일을 마우스 오른쪽 단추로 클릭 **이름 바꾸기**합니다.

    ![루트 인증서 이름 바꾸기 ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    확장 too.crt hello 루트 인증서를 변경 합니다. ख ा त toochange hello 확장명 인 경우 클릭 묻는 경우 **예** 또는 **확인**합니다. 그렇지 않으면 hello 파일의 기능을 변경할 수 있습니다. 루트 인증서를 나타내는 hello 파일 변경 내용 tooan 아이콘에 대 한 hello 아이콘입니다.

6. Hello 루트 인증서를 마우스 오른쪽 단추로 클릭 하 고 hello 팝업 메뉴에서 선택 **인증서 설치**합니다.

    hello **인증서 가져오기 마법사** 대화 상자가 나타납니다.

7. Hello에 **인증서 가져오기 마법사** 대화 상자에서 **로컬 컴퓨터** hello 인증서 및 클릭 한 다음에 대 한 hello 대상으로 **다음** toocontinue 합니다.

    ![인증서 저장소 대상 옵션 ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    클릭 하 여 원하는 변경 내용을 toohello 컴퓨터 tooallow 묻는 **예** 또는 **확인**, tooall hello 변경 합니다.

8. Hello에 **인증서 저장소** 페이지에서 **모든 인증서 저장소를 다음 hello에 저장**, 클릭 하 고 **찾아보기** toochoose hello 인증서 저장소입니다.

    ![특정 저장소 위치에 인증서 저장](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    hello **인증서 저장소 선택** 대화 상자가 나타납니다.

    ![인증서 저장소 폴더 계층 구조](./media/backup-azure-backup-server-vmware/cert-store.png)

9. 선택 **신뢰할 수 있는 루트 인증 기관** hello 인증서 및 클릭 한 다음에 대 한 hello 대상 폴더로 **확인**합니다.

    ![인증서 대상 폴더](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    hello **신뢰할 수 있는 루트 인증 기관** 폴더 hello 인증서 저장소로 확인 됩니다. **다음**을 누릅니다.

    ![인증서 저장소 폴더](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Hello에 **완료 hello 인증서 가져오기 마법사** 페이지, 해당 hello 인증서 hello 원하는 폴더에 있는지 확인 한 다음 클릭 **마침**합니다.

    ![인증서가 hello 적절 한 폴더를 확인 하십시오.](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    대화 상자가 나타나면 hello 성공적인 인증서 가져오기 확인 되었습니다.

11. 사용자 연결이 보호 되는 서버 tooconfirm toohello vCenter에 로그인 합니다.

  Hello 인증서 가져오기 성공 하 고 보안 연결을 설정할 수 없습니다, 경우에 hello VMware vSphere 설명서를 참조 [서버 인증서 얻기](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)합니다.

  보안 경계, 조직 내의 tooturn hello HTTPS 프로토콜에 원하지 프로시저 toodisable hello 보안 통신을 수행 하는 hello를 사용 하십시오.

### <a name="disable-secure-communication-protocol"></a>보안 통신 프로토콜 사용 안 함

조직 hello HTTPS 프로토콜을 요구 하지 않는 단계 toodisable HTTPS 다음 hello를 사용 합니다. toodisable hello 기본 동작을 hello 기본 동작을 무시 하는 레지스트리 키를 만듭니다.

1. 복사 하 여.txt 파일에 텍스트를 다음 hello를 붙여 넣습니다.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Hello 파일 tooyour Azure 백업 서버 컴퓨터를 저장 합니다. Hello 파일 이름에 대해 DisableSecureAuthentication.reg를 사용 합니다.

3. Hello 파일 tooactivate hello 레지스트리 항목을 두 번 클릭 합니다.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Hello vCenter Server에서 역할 및 사용자 계정 만들기

Hello vCenter Server에서 역할에는 미리 정의 된 권한 집합이. VCenter 서버 관리자는 hello 역할을 만듭니다. tooassign 권한을 관리자에 게 역할을 갖는 사용자 계정 쌍입니다. tooestablish hello 필요한 사용자 자격 증명 tooback hello vCenter 서버 컴퓨터를 특정 권한을 가진 역할을 만듭니다와 hello 역할 hello 사용자 계정을 연결 합니다.

Azure 백업 서버 hello vCenter 서버를 사용자 이름 및 암호 tooauthenticate를 사용합니다. Azure Backup Server는 이러한 자격 증명을 모든 백업 작업에 대한 인증으로 사용합니다.

tooadd vCenter 서버 역할 및 백업 관리자에 대 한 해당 권한을:

1. Toohello vCenter 서버를 찾은 다음 hello vCenter Server에서에서 로그인 **탐색기** 에서 **관리**합니다.

    ![vCenter Server 탐색기 패널의 관리 옵션](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. **관리** 선택 **역할**, 한 다음 hello **역할** 패널 클릭 hello 역할 아이콘 (hello + 기호)를 추가 합니다.

    ![역할 추가](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    hello **역할 만들기** 대화 상자가 나타납니다.

    ![역할 만들기](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. Hello에 **Create Role** 대화 상자의 hello **역할 이름** 상자에 입력 *BackupAdminRole*합니다. hello 역할 이름이 든 수는 있지만 hello 역할의 용도 대 한 인식할 수 있는 것입니다.

4. Hello, vCenter의 적절 한 버전에 대 한 hello 권한을 선택한 다음 클릭 **확인**합니다. 다음 표에서 hello vCenter 6.0 및 5.5 vCenter에 대 한 hello 필요한 권한을 식별 합니다.

  Hello 권한을 선택 하면 hello 아이콘 다음 toohello 부모 레이블 tooexpand hello 부모 및 보기 hello 자식 권한을 클릭 합니다. toogo 해야 tooselect hello VirtualMachine 권한 hello에 여러 개의 수준이 부모 자식 계층입니다. 부모 권한 내에서 모든 자식 권한을 tooselect을 필요 하지 않습니다.

  ![부모 자식 권한 계층 구조](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  클릭 한 후 **확인**, 새 역할 hello hello 역할 패널에 hello 목록에 나타납니다.

|vCenter 6.0에 대한 권한| vCenter 5.5에 대한 권한|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>vCenter Server 사용자 계정 및 사용 권한 만들기

권한과 함께 hello 역할을 설정한 후에 사용자 계정을 만듭니다. hello 사용자 계정 이름 및 암호 인증에 사용 되는 hello 자격 증명을 제공 하는 있습니다.

1. toocreate hello vCenter 서버에에서 사용자 계정 **탐색기** 에서 **사용자 및 그룹**합니다.

    ![사용자 및 그룹 옵션](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    hello **vCenter 사용자 및 그룹** 다음과 같은 창이 나타납니다.

    ![vCenter 사용자 및 그룹 패널](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. Hello에 **vCenter 사용자 및 그룹** 패널, 선택 hello **사용자** 탭을 클릭 한 다음 hello 사용자 아이콘 (hello + 기호)를 추가 합니다.

    hello **새 사용자** 대화 상자가 나타납니다.

3. Hello에 **새 사용자** 대화 상자, hello 사용자 정보를 추가 하 고 클릭 **확인**합니다. 이 절차에서는 hello 사용자 BackupAdmin 이름은입니다.

    ![새 사용자 대화 상자](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    새 사용자 계정을 hello hello 목록에 나타납니다.

4. hello 역할 hello에 tooassociate hello 사용자 계정을 **탐색기** 에서 **전역 권한을**합니다. Hello에 **전역 권한을** 패널, 선택 hello **관리** 탭을 클릭 한 다음 hello (hello + 기호) 아이콘을 추가 합니다.

    ![전역 권한 패널](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    hello **전역 권한을 루트-권한 추가** 대화 상자가 나타납니다.

5. Hello에 **전역 권한 루트-권한 추가** 대화 상자를 클릭 **추가** toochoose hello 사용자 또는 그룹입니다.

    ![사용자 또는 그룹 선택](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    hello **사용자/그룹 선택** 대화 상자가 나타납니다.

6. Hello에 **사용자/그룹 선택** 대화 상자에서 선택 **BackupAdmin** 클릭 하 고 **추가**합니다.

    **사용자**, hello *domain\username* 형식은 hello 사용자 계정에 사용 됩니다. 다른 도메인 toouse 원한다 면 hello에서 선택 **도메인** 목록입니다.

    ![BackupAdmin 사용자 추가](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    클릭 **확인** tooadd hello 선택 사용자 toohello **권한 추가** 대화 상자.

7. Hello 사용자를 식별 했으면 했으므로 hello 사용자 toohello 역할을 할당 합니다. **역할 할당**, hello 드롭 다운 목록에서 선택 **BackupAdminRole**, 클릭 하 고 **확인**합니다.

    ![사용자 toorole 할당](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Hello에 **관리** hello 탭 **전역 권한을** 패널, hello 새 사용자 계정 및 연결 된 hello 역할 hello 목록에 표시 합니다.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Azure Backup Server에서 vCenter Server 자격 증명 설정

Hello VMware 서버 tooAzure 백업 서버를 추가 하기 전에 설치 [Azure 백업 서버에 대 한 업데이트 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)합니다.

1. tooopen Azure 백업 서버 hello hello Azure 백업 서버 바탕 화면 아이콘을 두 번 클릭 합니다.

    ![Azure Backup Server 아이콘](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Hello 아이콘 hello 바탕 화면에서를 찾을 수 없는 경우 설치 된 응용 프로그램의 hello 목록에서 Azure 백업 서버를 엽니다. hello Azure 백업 서버 응용 프로그램 이름에는 Microsoft Azure 백업 이라고 합니다.

2. Hello Azure 백업 서버 콘솔에서 클릭 **관리**, 클릭 **프로덕션 서버**, hello 도구 리본에서을 클릭 하 고 **VMware 관리**합니다.

    ![Azure Backup Server 콘솔](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    hello **자격 증명 관리** 대화 상자가 나타납니다.

    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. Hello에 **자격 증명 관리** 대화 상자를 클릭 **추가** tooopen hello **자격 증명 추가** 대화 상자.

4. Hello에 **자격 증명 추가** 대화 상자에 이름과 hello 새 자격 증명에 대 한 설명을 입력 합니다. 다음 hello 사용자 이름 및 암호를 지정 합니다. hello 이름 *Contoso Vcenter 자격 증명* 사용 hello 다음 절차에서 tooidentify hello 자격 증명입니다. 사용 하 여 hello 동일한 사용자 이름 및 암호에 사용 되는 vCenter Server hello 합니다. Hello vCenter Server 및 Azure 백업 서버에 없는 경우 동일한 도메인에 hello **사용자 이름**, hello 도메인을 지정 합니다.

    ![Azure Backup Server 자격 증명 추가 대화 상자](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    클릭 **추가** tooadd hello 새 자격 증명 tooAzure 백업 서버입니다. 새 자격 증명 hello hello hello 목록에 표시 **자격 증명 관리** 대화 상자.
    
    ![Azure Backup Server 자격 증명 관리 대화 상자](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. tooclose hello **자격 증명 관리** 대화 상자에서 hello 클릭 **X** hello 오른쪽 위 모퉁이에 있습니다.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Hello vCenter 서버 tooAzure 백업 서버를 추가 합니다.

프로덕션 서버 추가 마법사가 사용 되는 tooadd hello vCenter 서버 tooAzure 백업 서버입니다.

tooopen 프로덕션 서버 추가 마법사를 완료 hello 절차를 수행 합니다.

1. Hello Azure 백업 서버 콘솔에서 클릭 **관리**, 클릭 **프로덕션 서버**, 클릭 하 고 **추가**합니다.

    ![프로덕션 서버 추가 마법사 열기](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    hello **프로덕션 서버 추가 마법사** 대화 상자가 나타납니다.

    ![프로덕션 서버 추가 마법사](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Hello에 **프로덕션 서버 선택 형식** 페이지 **VMware 서버**, 클릭 하 고 **다음**합니다.

3. **서버 이름/i P 주소**, hello 정규화 된 도메인 이름 (FQDN) 또는 IP 주소 hello VMware 서버를 지정 합니다. 모든 hello ESXi 서버 hello 하 여 관리 되는 경우 동일한 vCenter hello vCenter 이름을 사용할 수 있습니다.

    ![VMware 서버 FQDN 또는 IP 주소 지정](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. **SSL 포트**를 사용 하는 toocommunicate hello VMware 서버와는 hello 포트를 입력 합니다. 다른 포트는 필요 하지 않는 한 hello 기본 포트는 포트 443을 사용 합니다.

5. **자격 증명 지정**, 선택 hello 앞에서 만든 자격 증명.

    ![자격 증명 지정](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. 클릭 **추가** tooadd hello VMware 서버 toohello 목록으로 **VMware 서버 추가**, 클릭 하 고 **다음** toomove toohello hello 마법사의 다음 페이지입니다.

    ![VMWare 서버 및 자격 증명 추가](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. Hello에 **요약** 페이지 **추가** tooadd hello VMware 서버 tooAzure 백업 서버를 지정 합니다.

    ![VMware server tooAzure 백업 서버를 추가 합니다.](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  hello VMware 서버 백업은 에이전트 없는 백업 이며 새 서버 hello 즉시 추가 됩니다. hello **마침** 페이지 결과 hello 보여 줍니다.

  ![마침 페이지](./media/backup-azure-backup-server-vmware/summary-screen.png)

  이 섹션의 단계를 여러 개 vCenter 서버 tooAzure 백업 서버를 이전 반복 hello tooadd 합니다.

Hello vCenter 서버 tooAzure 백업 서버를 추가한 후 hello 다음 단계는 toocreate 보호 그룹입니다. hello 보호 그룹 지정 hello 짧은 또는 장기 보존에 대 한 다양 한 세부 정보는를 정의 하 고 hello 백업 정책을 적용 합니다. hello 백업 정책은 백업 진행 시기 및 백업할 hello 일정입니다.


## <a name="configure-a-protection-group"></a>보호 그룹 구성

System Center Data Protection Manager 또는 하기 전에 Azure 백업 서버를 사용 하지 않은 경우 참조 [디스크 백업에 대 한 계획](https://technet.microsoft.com/library/hh758026.aspx) tooprepare 하드웨어 환경입니다. 적절 한 저장소 있는지 확인 한 후에 hello 새 보호 그룹 만들기 마법사 tooadd VMware 가상 컴퓨터를 사용 합니다.

1. Hello Azure 백업 서버 콘솔에서 클릭 **보호**, hello 도구 리본에서을 클릭 하 고 **새로** tooopen hello 새 보호 그룹 만들기 마법사입니다.

    ![열기 hello 새 보호 그룹 만들기 마법사](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    hello **새 보호 그룹 만들기** 마법사 대화 상자가 나타납니다.

    ![새 보호 그룹 만들기 마법사 대화 상자](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    클릭 **다음** tooadvance toohello **보호 그룹 종류 선택** 페이지.

2. Hello에 **선택 보호 그룹 종류** 페이지 **서버** 클릭 하 고 **다음**합니다. hello **그룹 구성원 선택** 페이지가 나타납니다.

3. Hello에 **그룹 구성원 선택** 페이지, 사용 가능한 구성원 hello 및 hello 선택한 멤버를 표시 합니다. Hello 멤버 tooprotect를 원하고 클릭 한 다음 선택 **다음**합니다.

    ![그룹 구성원 선택](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    구성원을 선택할 때 다른 폴더 또는 VM을 포함하는 폴더를 선택하면 포함되는 폴더 및 VM도 함께 선택됩니다. hello 폴더 및 hello 상위 폴더에는 Vm의 hello 포함 폴더 수준 보호를 라고 합니다. tooremove 폴더 또는 VM을 선택 취소 hello 확인란 합니다.

    VM 또는 VM에 포함 된 폴더가 이미 보호 된 tooAzure 인 경우 해당 VM을 다시 선택할 수 없습니다. 즉, VM 보호 tooAzure 후 보호할 수 없습니다 다시 중복 된 복구 지점을 하나의 VM에 대 한 만들어지지 않도록 방지 하는 합니다. Toosee 하려는 경우 멤버, 지점 toohello toosee hello의 이름 서버를 보호 하는 hello Azure 백업 서버 인스턴스를 이미 보호 됩니다.

4. Hello에 **데이터 보호 방법 선택** 페이지 hello 보호 그룹에 대 한 이름을 입력 합니다. 단기 보호 (toodisk) 및 온라인 보호 선택 됩니다. Toouse 온라인 보호 (tooAzure) 하려는 경우에 단기 보호 toodisk를 사용 해야 합니다. 클릭 **다음** tooproceed toohello 단기 보호 범위입니다.

    ![데이터 보호 방법 선택](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Hello에 **단기 목표 지정** 페이지에 대 한 **보존 범위**, hello tooretain 복구 지점에 원하는 일 수가 지정 *toodisk 저장*합니다. Toochange hello 시간 및 복구 지점을 수행 되는 경우 일, 클릭 **수정**합니다. hello 단기 복구 지점은 전체 백업 합니다. 증분 백업하지 않습니다. 클릭 하 여 hello 단기 목표 만족 스 러 우면 **다음**합니다.

    ![단기 목표 지정](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Hello에 **디스크 할당 검토** 페이지를 검토 하 고 필요한 경우, Vm hello에 대 한 hello 디스크 공간을 수정 합니다. hello hello에 지정 된 hello 보존 범위를 기준으로 하는 디스크 할당 권장 **단기 목표 지정** 페이지, 작업, hello 유형 및 hello의 hello 크기 보호 된 데이터 (3 단계에서 식별 됨).  

  - **데이터 크기:** hello 보호 그룹의 hello 데이터의 크기입니다.
  - **디스크 공간:** hello hello 보호 그룹에 대 한 디스크 공간의 크기를 권장 합니다. 이 설정은 toomodify을 원하는 경우 각 데이터 원본 증가 예측 하는 hello 크기 보다 약간 더 큰 총 공간을 할당 해야 합니다.
  - **데이터 배치:** hello 보호 데이터 원본을 여러 개 tooa 단일 복제본 및 복구 지점 볼륨에 매핑할 수 공동 배치를 설정 합니다. 공동 배치는 모든 워크로드에 지원되는 것은 아닙니다.
  - **자동 증가:** hello 보호 그룹의 데이터 hello 초기 할당 보다 커지면 경우이 설정 켜기, 하는 경우 System Center Data Protection Manager 25% tooincrease hello 디스크 크기를 시도 합니다.
  - **저장소 풀 세부 정보:** 합계를 포함 하 여 크기 및 남은 디스크 크기 hello 저장소 풀의 hello 상태를 보여 줍니다.

    ![디스크 할당 검토](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Hello 공간 할당에 만족 했으면 클릭 **다음**합니다.

7. Hello에 **복제본 만들기 방법 선택** 페이지에서 원하는 toogenerate hello 초기 복사본, 즉 Azure 백업 서버 hello 보호 된 데이터의 복제본을 지정 합니다.

    hello 기본값은 **hello 네트워크를 통해 자동으로** 및 **이제**합니다. Hello 기본값을 사용 하는 경우에 사용량이 적은 시간을 지정 하는 것이 좋습니다. **나중에**를 선택하고 날짜와 시간을 지정합니다.

    대용량 데이터 또는 작음 보다 최적의 네트워크 상태, 이동식 미디어를 사용 하 여 hello 오프 라인으로 데이터를 복제 하는 것이 좋습니다.

    선택을 완료한 후 **다음**을 클릭합니다.

    ![복제본 만들기 방법 선택](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Hello에 **일관성 확인 옵션** 페이지에서 tooautomate hello 일관성 검사 하는 방법 및 시기. 복제 데이터가 일관성을 잃은 경우 또는 설정된 일정에 따라 일관성 확인을 실행할 수 있습니다.

    Tooconfigure 자동 일관성 검사를 사용 하지 않으려는 경우에 수동 검사를 실행할 수 있습니다. Hello Azure 백업 서버 콘솔의 hello 보호 영역에서 hello 보호 그룹을 마우스 오른쪽 단추로 클릭 한 다음 선택 **일관성 확인 수행**합니다.

    클릭 **다음** toomove toohello 다음 페이지입니다.

9. Hello에 **온라인 보호 데이터 지정** 페이지에서 원하는 tooprotect 하나 이상의 데이터 원본을 선택 합니다. Hello 멤버를 개별적으로 선택 하거나 클릭 수 **모두 선택** toochoose 모든 멤버입니다. Hello 멤버를 선택한 후 클릭 **다음**합니다.

    ![온라인 보호 데이터 지정](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Hello에 **온라인 백업 일정 지정** 페이지 hello 디스크 백업에서 hello 일정 toogenerate 복구 지점을 지정 합니다. Hello 복구 지점이 생성 된 후에 Azure 복구 서비스 자격 증명 모음 전송된 toohello 됩니다. Hello 온라인 백업 일정에 만족 했으면 클릭 **다음**합니다.

    ![온라인 백업 일정 지정](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Hello에 **온라인 보존 정책 지정** 페이지에서, tooretain hello Azure에서 백업 데이터를 원하는 시간을 표시 합니다. Hello 정책을 정의한 후 클릭 **다음**합니다.

    ![온라인 보존 정책 지정](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Azure에서 데이터를 유지할 수 있는 기간에 대한 시간 제한은 없습니다. Azure에서 복구 지점 데이터를 저장 하는 경우 hello만 제한은 보호 된 인스턴스 당 9999 개 이상의 복구 지점을 사용할 수는 없습니다. 이 예제에서는 보호 된 인스턴스 hello hello VMware 서버입니다.

12. Hello에 **요약** 페이지, 보호 그룹 구성원 및 설정에 대 한 hello 세부 정보를 검토 한 다음 클릭 **그룹 만들기**합니다.

    ![보호 그룹 구성원 및 설정 요약](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>다음 단계
Azure 백업 서버 tooprotect VMware 작업을 사용 하면 Azure 백업 서버 toohelp 보호를 사용 하 여에 관심이 있을 수는 [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [Microsoft SharePoint 팜](./backup-azure-backup-sharepoint-mabs.md), 또는 [SQL Server 데이터베이스](./backup-azure-sql-mabs.md)합니다.

Hello 에이전트 등록 하 고 문제에 대 한 내용은 hello 보호 그룹을 구성 하거나 작업, 백업 참조 [Azure 백업 서버 문제를 해결](./backup-azure-mabs-troubleshoot.md)합니다.
