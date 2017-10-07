---
title: "Azure Linux 가상 컴퓨터에서 데이터베이스를 aaaBack 및 Oracle 데이터베이스 12c 복구 | Microsoft Docs"
description: "Azure 환경에서 데이터베이스를 tooback 및 Oracle 데이터베이스 12c 복구에 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Azure Linux Virtual Machine에서 Oracle Database 12c 데이터베이스 백업 및 복구

Azure CLI toocreate를 사용 하는 명령 프롬프트에서 Azure 리소스 관리 하거나 스크립트를 사용할 수 있습니다. 이 문서에서는 Azure CLI 스크립트 toodeploy Oracle 데이터베이스 12c 데이터베이스를 사용 하 여 Azure 마켓플레이스 갤러리 이미지를 사용합니다.

시작하기 전에 Azure CLI가 설치되어 있는지 확인합니다. 자세한 내용은 참조 hello [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.

## <a name="prepare-hello-environment"></a>Hello 환경 준비

### <a name="step-1-prerequisites"></a>1단계: 필수 조건

*   tooperform hello 백업 및 복구 프로세스를 먼저 만들어야 합니다 Oracle Database 12c의 설치 된 인스턴스에 있는 Linux VM입니다. VM 이름은 toocreate hello를 사용 하면 hello 마켓플레이스 이미지 *Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest*합니다.

    toolearn toocreate Oracle 데이터베이스를 확인 하려면 어떻게 해야 hello [Oracle 데이터베이스 빠른 시작을 만드는](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create)합니다.


### <a name="step-2-connect-toohello-vm"></a>2 단계: toohello VM 연결

*   VM hello로 SSH (보안 셸) 세션 toocreate hello 다음 명령을 사용 합니다. Hello hello IP 주소와 hello 호스트 이름 조합을 바꿉니다 `publicIpAddress` VM에 대 한 값입니다.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>3 단계: hello 데이터베이스 준비

1.  이 단계에서는 *myVM*이라는 VM이 실행되는 Oracle 인스턴스(cdb1)가 있다고 가정합니다.

    Hello 실행 *oracle* superuser 루트 및 초기화 hello 수신기:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  (선택 사항) Hello 데이터베이스가 보관 로그 모드에 있는지 확인 합니다.

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (선택 사항) 테이블 tootest hello 커밋을 만듭니다.

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  확인 또는 hello 백업 파일 위치와 크기를 변경 합니다.

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Hello 데이터베이스를 사용 하 여 Oracle 복구 관리자 (RMAN) tooback:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>4단계: Linux VM의 응용 프로그램 일치 백업

응용 프로그램 일치 백업은 Azure Backup의 새 기능입니다. 만들 수 있으며 이전 및 이후 hello VM 스냅샷 (프리 스냅숏 및 포스트 스냅숏) 스크립트 tooexecute 선택.

1. Hello JSON 파일을 다운로드 합니다.

    https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig에서 VMSnapshotScriptPluginConfig.json을 다운로드합니다. hello 파일 내용을 비슷한 toohello 다음을 확인합니다.

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Hello VM에 hello /etc/azure 폴더를 만듭니다.

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Hello JSON 파일을 복사 합니다.

    VMSnapshotScriptPluginConfig.json toohello /etc/azure 폴더를 복사 합니다.

4. Hello JSON 파일을 편집 합니다.

    Hello VMSnapshotScriptPluginConfig.json 파일 tooinclude hello 편집 `PreScriptLocation` 및 `PostScriptlocation` 매개 변수입니다. 예:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Hello 프리 스냅숏 및 포스트 스냅숏 스크립트 파일을 만듭니다.

    다음은 “콜드 백업”에 대한 사전 스냅숏 및 사후 스냅숏 스크립트의 예(종료 및 다시 시작을 사용하는 오프라인 백업)입니다.

    /etc/azure/pre_script.sh의 경우:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    /etc/azure/post_script.sh의 경우:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    다음은 “핫 백업”에 대한 사전 스냅숏 및 사후 스냅숏 스크립트의 예(온라인 백업)입니다.

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    /etc/azure/post_script.sh의 경우:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    /Etc/azure/pre_script.sql에 대 한 요구 사항에 따라 hello 파일의 hello 내용을 수정 합니다.

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    /Etc/azure/post_script.sql에 대 한 요구 사항에 따라 hello 파일의 hello 내용을 수정 합니다.

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. 파일 사용 권한을 변경합니다.

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Hello 스크립트를 테스트 합니다.

    첫째, tootest hello 스크립트 루트로 로그인합니다. 그런 다음, 오류가 없는지 확인합니다.

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

자세한 내용은 [Linux VM에 대한 응용 프로그램 일치 백업](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/)을 참조하세요.


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>5 단계: 사용 하 여 Azure 복구 서비스 자격 증명 모음 tooback hello VM 구성

1.  Hello Azure 포털에서 검색할 **복구 서비스 자격 증명 모음**합니다.

    ![Recovery Services 자격 증명 모음 페이지](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Hello에 **복구 서비스 자격 증명 모음** 블레이드에서 tooadd 새 자격 증명 모음 클릭 **추가**합니다.

    ![Recovery Services 자격 증명 모음 추가 페이지](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, 클릭 **myVault**합니다.

    ![Recovery Services 자격 증명 모음 세부 정보 페이지](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Hello에 **myVault** 블레이드에서 클릭 **백업**합니다.

    ![Recovery Services 자격 증명 모음 백업 페이지](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Hello에 **백업 목표** 블레이드를 사용 하 여 hello 기본값의 **Azure** 및 **가상 컴퓨터**합니다. **확인**을 클릭합니다.

    ![Recovery Services 자격 증명 모음 세부 정보 페이지](./media/oracle-backup-recovery/recovery_service_05.png)

6.  **백업 정책**의 경우 **DefaultPolicy**를 사용하거나 **정책 새로 만들기**를 선택합니다. **확인**을 클릭합니다.

    ![Recovery Services 자격 증명 모음 백업 정책 세부 정보 페이지](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Hello에 **가상 컴퓨터 선택** 블레이드, 선택 hello **myVM1** 확인란을 선택한 다음 클릭 **확인**합니다. Hello 클릭 **백업 사용** 단추입니다.

    ![복구 서비스 자격 증명 모음 항목 toohello 백업 세부 정보 페이지](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > 클릭 한 후 **백업 사용**, hello 예약 된 시간이 만료 될 때까지 hello 백업 프로세스를 시작 하지 않습니다. 완료는 즉시 백업 tooset hello 다음 단계입니다.

8.  Hello에 **myVault-백업 항목** 블레이드 아래 **백업 항목 수**, hello 백업 항목 수를 선택 합니다.

    ![Recovery Services 자격 증명 모음 myVault 세부 정보 페이지](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Hello에 **백업 항목 (Azure 가상 컴퓨터)** hello 줄임표를 클릭 하 여 hello hello 페이지의 오른쪽에 블레이드 (**...** ) 단추를 선택한 다음 클릭 **지금 백업**합니다.

    ![Recovery Services 자격 증명 모음 지금 백업 명령](./media/oracle-backup-recovery/recovery_service_09.png)

10. Hello 클릭 **백업** 단추입니다. Hello 백업 프로세스 toofinish 될 때까지 기다립니다. 그런 다음 너무 이동[6 단계: hello 데이터베이스 파일을 제거](#step-6-remove-the-database-files)합니다.

    hello 백업 작업의 tooview hello 상태 클릭 **작업**합니다.

    ![Recovery Services 자격 증명 모음 작업 페이지](./media/oracle-backup-recovery/recovery_service_10.png)

    hello 백업 작업의 상태 hello hello 이미지 다음에 나타납니다.

    ![상태가 표시된 Recovery Services 자격 증명 모음 작업 페이지](./media/oracle-backup-recovery/recovery_service_11.png)

11. 응용 프로그램 일치 백업에 대 한 hello 로그 파일에서 오류를 해결 합니다. hello 로그 파일은 /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0에 있습니다.

### <a name="step-6-remove-hello-database-files"></a>6 단계: hello 데이터베이스 파일을 제거 
이 문서의 뒷부분에 나오는 tootest 복구 프로세스를 hello 하는 방법을 설명 합니다. Hello 복구 프로세스를 테스트 하려면 전에 tooremove hello 데이터베이스 파일 해야 합니다.

1.  Hello 테이블 스페이스 및 백업 파일을 제거 합니다.

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (선택 사항) Hello Oracle 인스턴스를 종료 합니다.

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Hello 복구 서비스 자격 증명 모음에서 삭제 하는 hello 파일 복원
다음 단계 완료 hello toorestore 삭제 hello 파일:

1. Hello hello Azure 포털에서에서 검색할 *myVault* 복구 서비스 항목을 자격 증명 모음입니다. Hello에 **개요** 블레이드 아래 **항목 백업**, hello 항목 수를 선택 합니다.

    ![Recovery Services 자격 증명 모음 myVault 백업 항목](./media/oracle-backup-recovery/recovery_service_12.png)

2. 아래 **백업 항목 수**, hello 항목 수를 선택 합니다.

    ![Recovery Services 자격 증명 모음 Azure Virtual Machine 백업 항목 수](./media/oracle-backup-recovery/recovery_service_13.png)

3. Hello에 **myvm1** 블레이드에서 클릭 **(미리 보기)에 대 한 파일 복구**합니다.

    ![Hello 복구 서비스의 스크린 샷 파일 복구 페이지 자격 증명 모음](./media/oracle-backup-recovery/recovery_service_14.png)

4. Hello에 **(미리 보기)에 대 한 파일 복구** 창에서 클릭 **스크립트 다운로드**합니다. 그런 다음 hello 클라이언트 컴퓨터에서 hello 다운로드 (.sh) 파일 tooa 폴더를 저장 합니다.

    ![다운로드한 스크립트 파일 저장 옵션](./media/oracle-backup-recovery/recovery_service_15.png)

5. Hello.sh 파일 toohello VM을 복사 합니다.

    다음 예제는 hello toouse 안전한 복사 (scp) 명령 toomove 파일 toohello VM hello 하는 방법을 보여 줍니다. 또한 복사할 수 있습니다 hello 내용 toohello 클립보드 및 붙여넣기 hello 내용을 hello VM에 설치 되어 있는 새 파일에.

    > [!IMPORTANT]
    > 다음 예제는 hello, hello IP 주소와 폴더 값을 업데이트를 확인 합니다. hello 값 toohello hello 파일 저장 된 폴더를 매핑해야 합니다.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Hello 루트에서 소유 하 고 hello 파일을 변경 합니다.

    다음 예제는 hello, hello 파일 hello 루트에서 소유 하 고 되도록 변경 합니다. 그런 다음, 사용 권한을 변경합니다.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    hello 다음 예제 스크립트 앞에 오는 hello를 실행 한 후 표시 됩니다. 메시지가 면 toocontinue, 입력 **Y**합니다.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. 액세스 toohello 탑재 된 볼륨 확인 되었습니다.

    tooexit, 입력 **q**, 한 hello 탑재 된 볼륨에 대 한 다음 검색 합니다. 볼륨, 명령 프롬프트에서 입력의 hello 목록 추가 toocreate **df-k**합니다.

    ![hello df-k 명령](./media/oracle-backup-recovery/recovery_service_16.png)

8. 다음 스크립트 toocopy hello 누락 사용 하 여 hello 파일 백 toohello 폴더:

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. 다음 스크립트는 hello, RMAN toorecover hello 데이터베이스를 사용 합니다.

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Hello 디스크를 탑재 해제 합니다.

    Hello hello에 Azure 포털에서에서 **(미리 보기)에 대 한 파일 복구** 블레이드에서 클릭 **디스크 분리**합니다.

    ![디스크 분리 명령](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>복원할 전체 VM hello

복원할 수 hello 복구 서비스 자격 증명 모음에서 삭제 하는 hello 파일을 복원 하는 대신 전체 VM hello 합니다.

### <a name="step-1-delete-myvm"></a>1단계: myVM 삭제

*   Hello Azure 포털에서에서 toohello 이동 **myVM1** 자격 증명 모음을 선택한 후 **삭제**합니다.

    ![자격 증명 모음 삭제 명령](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>2 단계: hello VM 복구

1.  너무 이동**복구 서비스 자격 증명 모음**를 선택한 후 **myVault**합니다.

    ![myVault 항목](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Hello에 **개요** 블레이드 아래 **항목 백업**, hello 항목 수를 선택 합니다.

    ![myVault 백업 항목](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Hello에 **백업 항목 (Azure 가상 컴퓨터)** 블레이드를 **myvm1**합니다.

    ![VM 복구 페이지](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Hello에 **myvm1** 블레이드에서 hello 줄임표를 클릭 (**...** ) 단추를 선택한 다음 클릭 **복원 VM**합니다.

    ![VM 복원 명령](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Hello에 **선택 복원 지점** 블레이드, 선택 hello 항목 toorestore를 원하고 클릭 **확인**합니다.

    ![선택 hello 복원 지점](./media/oracle-backup-recovery/recover_vm_06.png)

    응용 프로그램 일치 백업을 사용하는 경우 파란색 세로 막대가 나타납니다.

6.  Hello에 **구성 복원** 블레이드에서 선택 hello 가상 컴퓨터 이름으로 hello 리소스 그룹을 선택 하 고 클릭 **확인**합니다.

    ![복원 구성 값](./media/oracle-backup-recovery/recover_vm_07.png)

7.  VM을 toorestore hello 클릭 hello **복원** 단추입니다.

8.  hello 복원 프로세스의 tooview hello 상태 클릭 **작업**, 클릭 하 고 **백업 작업이**합니다.

    ![백업 작업 상태 명령](./media/oracle-backup-recovery/recover_vm_08.png)

    hello 다음 그림과 hello 복원 프로세스의 hello 상태:

    ![Hello 복원 프로세스의 상태](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>3 단계: hello 공용 IP 주소 설정
복원 된 VM hello, 후 hello 공용 IP 주소를 설정 합니다.

1.  Hello 검색 상자에 입력 **공용 IP 주소**합니다.

    ![공용 IP 주소의 목록](./media/oracle-backup-recovery/create_ip_00.png)

2.  Hello에 **공용 IP 주소** 블레이드에서 클릭 **추가**합니다. Hello에 **공용 IP 주소 만들기** 블레이드에서 대 한 **이름**선택, hello 공용 IP 이름입니다. **리소스 그룹**에 **기존 항목 사용**을 선택합니다. 그런 다음에 **만들기**를 클릭합니다.

    ![IP 주소 만들기](./media/oracle-backup-recovery/create_ip_01.png)

3.  VM hello에 대 한 hello 네트워크 인터페이스가 tooassociate hello 공용 IP 주소 검색 및 선택 **myVMip**합니다. 그런 다음, **연결**을 클릭합니다.

    ![IP 주소 연결](./media/oracle-backup-recovery/create_ip_02.png)

4.  **리소스 종류**의 경우 **네트워크 인터페이스**를 선택합니다. Hello myVM 인스턴스에서 사용 되는 hello 네트워크 인터페이스를 선택한 다음 클릭 **확인**합니다.

    ![리소스 종류 및 NIC 값 선택](./media/oracle-backup-recovery/create_ip_03.png)

5.  검색 하 고 hello 포털에서 이식은 myVM hello 인스턴스를 엽니다. hello VM hello와 연결 된 IP 주소에 나타나는 hello myVM **개요** 블레이드입니다.

    ![IP 주소 값](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>4 단계: toohello VM 연결

*   tooconnect toohello VM을 hello 다음 스크립트를 사용 합니다.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>5 단계: hello 데이터베이스를 액세스할 수 있는지 여부를 테스트합니다
*   tootest 내게 필요한 옵션을 사용 하 여 hello 다음 스크립트:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Hello 데이터베이스 **시작** 명령은 오류, toorecover hello 데이터베이스 생성을 참조 하십시오. [6 단계: 사용 하 여 RMAN toorecover hello 데이터베이스](#step-6-optional-use-rman-to-recover-the-database)합니다.

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>6 단계: (선택 사항) 사용 하 여 RMAN toorecover hello 데이터베이스
*   다음 스크립트는 사용 하 여 hello toorecover hello 데이터베이스:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

이제 Azure Linux VM에서 hello Oracle 데이터베이스 12c 데이터베이스의 hello 백업 및 복구 완료 됩니다.

## <a name="delete-hello-vm"></a>Hello VM 삭제

더 이상 VM hello 필요 hello 명령 tooremove hello 리소스 그룹, VM hello 및 모든 관련된 리소스에 따라 사용할 수 없습니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

[자습서: 고가용성 VM 만들기](../../linux/create-cli-complete.md)

[VM 배포 Azure CLI 샘플 탐색](../../linux/cli-samples.md)



