---
title: "Azure Linux 가상 컴퓨터에서 Oracle ASM를 aaaSet | Microsoft Docs"
description: "Azure 환경에서 Oracle ASM을 빠르게 준비하여 실행합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Azure Linux 가상 컴퓨터에 Oracle ASM 설정  

Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다. 이 자습서에서는 hello 설치 및 구성의 Oracle 자동화 된 저장소 관리 (ASM)와 결합 하는 기본 Azure 가상 컴퓨터 배포에 설명 합니다.  다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 만들고 tooan Oracle 데이터베이스 VM 연결
> * Oracle Automated Storage Management 설치 및 구성
> * Oracle Grid 인프라 설치 및 구성
> * Oracle ASM 설치 초기화
> * ASM에서 관리하는 Oracle DB 만들기


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="prepare-hello-environment"></a>Hello 환경 준비

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

리소스 그룹 toocreate hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에 *eastus* 영역입니다.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>VM 만들기

가상 컴퓨터 toocreate hello Oracle 데이터베이스 이미지를 기반 및 toouse Oracle ASM 구성, hello를 사용 하 여 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 

hello 다음 예제에서는 각 50GB의 네 개의 연결 된 데이터 디스크와 Standard_DS2_v2 크기로 사용 되는 myVM 이라는 VM 이미 hello 기본 키 위치에 존재 하지 않습니다, 하는 경우 또한 SSH 키를 만듭니다.  toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Hello VM을 만든 후 Azure CLI 정보 비슷한 toohello를 다음 예제에서는 표시 됩니다. Hello 값을 확인 `publicIpAddress`합니다. VM이 주소 tooaccess hello를 사용 합니다.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Toohello VM 연결

와 SSH 세션 toocreate VM hello, 추가 설정을 구성 하 고 hello 다음 명령을 사용 합니다. Hello로 hello IP 주소를 교체 `publicIpAddress` VM에 대 한 값입니다.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Oracle ASM 설치

tooinstall Oracle ASM, 전체 hello 단계를 수행 합니다. 

Oracle ASM 설치에 대한 자세한 내용은 [Oracle Linux 6에 대한 Oracle ASMLib 다운로드](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html)를 참조하세요.  

1. ASM 설치 순서 toocontinue의 루트로 toologin이 필요합니다.

   ```bash
   sudo su -
   ```
   
2. 이러한 추가 명령을 tooinstall Oracle ASM 구성 요소를 실행 합니다.

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Oracle ASM이 설치되어 있는지 확인합니다.

   ```bash
   rpm -qa |grep oracleasm
   ```

    hello이이 명령의 출력에는 다음과 같은 구성 요소가 hello를 수록 되어야 합니다.

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM 올바르게 순서 toofunction에서 특정 사용자 및 역할 필요합니다. 다음 명령을 hello hello 필수 사용자 계정 및 그룹을 만듭니다. 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. 사용자 및 그룹이 올바르게 생성되었는지 확인합니다.

   ```bash
   id grid
   ```

    hello이 명령의 출력을 나열 해야 hello 다음 사용자 및 그룹:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. 사용자에 대 한 폴더를 만들고 *그리드* hello 소유자를 변경 하 고:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Oracle ASM 설정

이 자습서에서는 hello 기본 사용자가 *그리드* hello 기본 그룹은 및 *asmadmin*합니다. 해당 hello 확인 *oracle* hello asmadmin 그룹의 일부인 사용자입니다. Oracle ASM 설치 단계를 수행 하는 전체 hello tooset:

1. Hello Oracle ASM 라이브러리 드라이버 설정 정의가 포함 됩니다 (표) hello 기본 사용자 및 기본 그룹 (asmadmin) 부팅 시 hello 드라이브 toostart 구성 뿐만 아니라 (y 선택) 및 디스크에서 부팅에 대 한 tooscan (y 선택). 다음 명령을 hello에서 tooanswer hello 프롬프트가 필요 합니다.

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   이 명령의 출력 hello 비슷한 toohello 뒤, 프롬프트 toobe 답변으로 중지 찾아야 합니다.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Hello 디스크 구성 보기:
   ```bash
   cat /proc/partitions
   ```

   이 명령의 hello 출력의 사용 가능한 디스크 목록을 다음 비슷한 toohello 같아야 합니다.

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. 디스크 포맷 */개발/sdc* hello를 실행 하 여 다음 명령 및 hello 응답 프롬프트에:
   - 새 파티션의 경우 *n*
   - 주 파티션의 경우 *p*
   - *1* tooselect hello 첫 번째 파티션
   - 키를 눌러 `enter` 기본 첫 번째 실린더 hello에 대 한
   - 키를 눌러 `enter` 기본 마지막 실린더 hello에 대 한
   - 키를 눌러 *w* toowrite hello 변경 toohello 파티션 테이블  

   ```bash
   fdisk /dev/sdc
   ```
   
   위에 제공 된 hello 답변을 사용 하 여, hello fdisk 명령에 대 한 hello 출력 hello 다음과 같이 표시 됩니다.

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. 반복 hello에 대 한 fdisk 명령 앞 `/dev/sdd`, `/dev/sde`, 및 `/dev/sdf`합니다.

5. Hello 디스크 구성을 확인 하십시오.

   ```bash
   cat /proc/partitions
   ```

   hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Hello Oracle ASM 서비스 상태를 확인 하 고 hello Oracle ASM 서비스를 시작 합니다.

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Oracle ASM 디스크를 만듭니다.

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   hello 명령의 hello 출력 hello 다음과 같이 표시 됩니다.

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Oracle ASM 디스크를 나열합니다.

   ```bash
   service oracleasm listdisks
   ```   

   다음 Oracle ASM 디스크 hello 오프 hello 명령의 hello 출력 수록 되어야 합니다.

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Hello 루트, oracle 및 눈금 사용자에 대 한 hello 암호를 변경 합니다. **이러한 새 암호를 기록** 대로 hello 설치 하는 동안에 나중에 사용 됩니다.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Hello 폴더 사용 권한을 변경 합니다.

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Oracle Grid Infrastructure 다운로드 및 준비

toodownload hello Oracle 그리드 인프라 소프트웨어, 단계를 수행 하는 전체 hello 준비 및:

1. Hello에서 Oracle 그리드 인프라 다운로드 [Oracle ASM 다운로드 페이지](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html)합니다. 

   라는 hello 다운로드 아래 **Oracle Database 12c 릴리스 1 그리드 인프라 (12.1.0.2.0) Linux x86-64에 대 한**, hello 두 개의.zip 파일을 다운로드 합니다.

2. Hello.zip tooyour 클라이언트 컴퓨터 파일을 다운로드 한 후 복사 프로토콜 보안 (SCP) toocopy hello 파일 tooyour VM을 사용할 수 있습니다.

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH는 hello로 순서 toomove hello.zip 파일에는 Azure에서 Oracle VM 스풀링됩니다/폴더를 선택 합니다. Hello 파일의 hello 소유자를 변경 합니다.

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Hello 파일을 압축을 풉니다. (설치 hello Linux의 압축을 푸는 도구가 설치 되어 있지 않은 경우.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. 사용 권한을 변경합니다.
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. 구성된 스왑 공간을 업데이트합니다. Oracle 그리드 구성 6.8 g B 이상의 스왑 공간 tooinstall 눈금 필요 합니다. Azure에서 Oracle Linux 이미지 hello 기본 스왑 파일 크기는 2048MB만 합니다. Tooincrease 해야 `ResourceDisk.SwapSizeMB` hello에 `/etc/waagent.conf` 파일을 업데이트 하는 hello 설정 tootake 효과 대 한 순서 대로 hello WALinuxAgent 서비스를 다시 시작 합니다. 읽기 전용 파일 이기 때문에 toochange 파일 사용 권한을 tooenable 쓰기 액세스 해야 합니다.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   검색할 `ResourceDisk.SwapSizeMB` hello 값도 변경 및**8192**합니다. Toopress 해야 `insert` tooenter 삽입 모드의 hello 값의 형식 **8192** 누릅니다 `esc` tooreturn toocommand 모드. toowrite hello 변경과 quit hello 파일 입력 `:wq` 누릅니다 `enter`합니다.
   
   > [!NOTE]
   > 항상 사용 하는 것이 좋습니다 `WALinuxAgent` tooconfigure 스왑 공간을 hello 로컬 임시 디스크 (임시 디스크에) 최상의 성능을 위해 항상 만들어집니다. 에 대 한 자세한 내용은 참조 하십시오. [tooadd 스왑 Linux Azure 가상 컴퓨터에서 파일을 어떻게](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines)합니다.

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>로컬 클라이언트 및 VM toorun x11 준비
Oracle ASM 구성 그래픽 인터페이스 toocomplete hello 설치 및 구성이 필요 합니다. 사용 하 여 hello x11 프로토콜 toofacilitate이이 설치 됩니다. X11 이미 클라이언트 시스템 (Mac 또는 Linux)를 사용 하는 경우 기능이 사용 하도록 설정 하 고 구성-있습니다이 구성을 건너뛸 단독 tooWindows 컴퓨터를 설정 합니다. 

1. [PuTTY 다운로드](http://www.putty.org/) 및 [Xming 다운로드](https://xming.en.softonic.com/) tooyour Windows 컴퓨터. 계속 하기 전에 hello 기본 값으로 이러한 응용 프로그램의 두 가지 toocomplete hello 설치를 해야 합니다.

2. PuTTY를 설치한 후 명령 프롬프트를 열고, PuTTY 폴더 (예: C:\Program Files\PuTTY) hello로 변경 하 고 실행 `puttygen.exe` 의 순서로 toogenerate 키입니다.

3. PuTTY 키 생성기에서,
   
   1. Hello를 선택 하 여 키를 생성 `Generate` 단추입니다.
   2. Hello 키 (Ctrl + C)의 hello 내용을 복사 합니다.
   3. 선택 hello `Save private key` 단추입니다.
   4. 암호를 사용 하 여 hello 키를 보안에 대 한 hello 경고를 무시 한 다음 선택 `OK`합니다.

   ![PuTTY 키 생성기의 스크린샷](./media/oracle-asm/puttykeygen.png)

4. VM에서 다음 명령을 실행합니다.

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. `authorized_keys`라는 파일을 만듭니다. 이 파일의 hello 키의 내용을 hello를 붙여 넣고 hello 파일을 저장 합니다.

   > [!NOTE]
   > hello 키 hello 문자열을 포함 해야 `ssh-rsa`합니다. 또한 hello 키의 내용을 hello 텍스트 한 줄 이어야 합니다.
   >  

6. 클라이언트 컴퓨터에서 PuTTY를 시작합니다. Hello에 **범주** 창 너무 이동**연결** > **SSH** > **Auth**합니다. Hello에 **인증에 대 한 개인 키 파일** 상자 이전에 생성 toohello 키를 검색 합니다.

   ![Hello SSH 인증 옵션의 스크린 샷](./media/oracle-asm/setprivatekey.png)

7. Hello에 **범주** 창 너무 이동**연결** > **SSH** > **X11**합니다. 선택 hello **사용 X11 전달** 확인란 합니다.

   ![Hello SSH X11의 스크린샷 옵션 전달](./media/oracle-asm/enablex11.png)

8. Hello에 **범주** 창 너무 이동**세션**합니다. Oracle ASM VM 입력 `<publicIPaddress>` hello 호스트 이름 대화 상자에서 새 입력 `Saved Session` 이름을 지정 하 고 클릭 `Save`합니다.  저장 한 후 클릭 `open` tooconnect tooyour Oracle ASM 가상 컴퓨터.  hello 처음 연결 하면 경고가 표시 되도록 hello 원격 시스템 레지스트리에서 캐시 되지 않습니다. 클릭 `yes` tooadd 것 하 고 계속 합니다.

   ![Hello PuTTY 세션 옵션의 스크린 샷](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Oracle Grid Infrastructure 설치

tooinstall Oracle 그리드 인프라 전체 hello 단계를 수행 합니다.

1. **그리드**로 로그인합니다. (암호를 입력 하지 않고에 수 toosign 수 있어야 합니다.) 

   > [!NOTE]
   > Windows를 실행 하는 경우 Xming hello 설치를 시작 하기 전에 시작 해야 합니다.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Oracle Grid Infrastructure 12c 릴리스 1 설치 관리자가 열립니다. (Hello installer toostart 몇 분 정도 걸릴 수 있습니다.)

2. Hello에 **설치 옵션을 선택** 페이지 **설치 및 독립 실행형 서버에 대 한 Oracle 그리드 인프라 구성**합니다.

   ![Hello 설치 관리자의 설치 옵션 선택 페이지의 스크린샷](./media/oracle-asm/install01.png)

3. Hello에 **제품 언어 선택** 페이지 **영어** hello 원하는 언어를 선택 합니다.  `next`을 클릭합니다.

4. Hello에 **ASM 디스크 그룹 만들기** 페이지:
   - Hello 디스크 그룹에 대 한 이름을 입력 합니다.
   - **중복**에서 **외부**를 선택합니다.
   - **할당 단위 크기**에서 **4**를 선택합니다.
   - **디스크 추가**에서 **ORCLASMSP**를 선택합니다.
   - `next`을 클릭합니다.

5. Hello에 **ASM 암호 지정** 페이지, 선택 hello **이러한 계정에 대해 동일한 암호를 사용 하 여** 옵션을 암호를 입력 합니다.

   ![Hello 설치 관리자의 ASM 암호 지정 페이지의 스크린샷](./media/oracle-asm/install04.png)

6. Hello에 **관리 옵션 지정** 페이지 hello 옵션 tooconfigure EM 클라우드 제어 해야 합니다. 이 옵션을 무시-클릭 `next` toocontinue 합니다. 

7. Hello에 **권한 있는 운영 체제 그룹** 페이지에서 hello 기본 설정을 사용 합니다. 클릭 `next` toocontinue 합니다.

8. Hello에 **설치 위치 지정** 페이지에서 hello 기본 설정을 사용 합니다. 클릭 `next` toocontinue 합니다.

9. Hello에 **만들 인벤토리** 페이지, 너무 hello 인벤토리 디렉터리 변경`/u01/app/grid/oraInventory`합니다. 클릭 `next` toocontinue 합니다.

   ![Hello 설치 관리자 만들기 인벤토리 페이지의 스크린샷](./media/oracle-asm/install08.png)

10. Hello에 **루트 스크립트 실행 구성** 페이지, 선택 hello **자동 구성 스크립트를 실행** 확인란 합니다. 그런 다음 선택 하는 hello **"root" 사용자 자격 증명을 사용 하 여** 옵션을 선택한 hello 루트 사용자 암호를 입력 합니다.

    ![Hello 설치 프로그램의 루트 스크립트 실행 구성 페이지의 스크린샷](./media/oracle-asm/install09.png)

11. Hello에 **Prerequisite Checks 수행** 페이지, 오류와 함께 hello 현재 설치에 실패 합니다. 이는 정상적인 동작입니다. `Fix & Check Again`를 선택합니다.

12. Hello에 **픽스업 스크립트** 대화 상자를 클릭 하 여 `OK`합니다.

13. Hello에 **요약** 페이지에서 선택한 설정을 검토 한 다음 클릭 `Install`합니다.

    ![Hello 설치 관리자의 요약 페이지의 스크린샷](./media/oracle-asm/install12.png)

14. 권한 있는 사용자로 실행 toobe 구성 스크립트를 알리는 경고 대화 상자가 나타납니다. 클릭 `Yes` toocontinue 합니다.

15. Hello에 **마침** 페이지 `Close` toofinish hello 설치 합니다.

## <a name="set-up-your-oracle-asm-installation"></a>Oracle ASM 설치 설정

Oracle ASM 설치 단계를 수행 하는 전체 hello tooset:

1. X11 세션에서 **그리드**로 로그인되었는지 확인합니다. Toohit 해야 `enter` toorevive hello 터미널입니다. 다음 Oracle 자동화 된 저장소 관리 Configuration Assistant hello를 시작 합니다.

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Oracle ASM 구성 도우미가 열립니다.

2. Hello에 **ASM 구성: 디스크 그룹** 대화 상자를 클릭 hello `Create` 단추를 선택한 다음 클릭 `Show Advanced Options`합니다.

3. Hello에 **디스크 그룹 만들기** 대화 상자:

   - Hello 디스크 그룹 이름을 입력 **데이터**합니다.
   - **멤버 디스크 선택**에서 **ORCL_DATA** 및 **ORCL_DATA1**을 선택합니다.
   - **할당 단위 크기**에서 **4**를 선택합니다.
   - 클릭 `ok` toocreate hello 디스크 그룹입니다.
   - 클릭 `ok` tooclose hello 확인 창이 있습니다.

   ![Hello 디스크 그룹 만들기 대화 상자의 스크린 샷](./media/oracle-asm/asm02.png)

4. Hello에 **ASM 구성: 디스크 그룹** 대화 상자를 클릭 hello `Create` 단추를 선택한 다음 클릭 `Show Advanced Options`합니다.

5. Hello에 **디스크 그룹 만들기** 대화 상자:

   - Hello 디스크 그룹 이름을 입력 **FRA**합니다.
   - **중복**에서 **외부(없음)**를 선택합니다.
   - **멤버 디스크 선택**에서 **ORCL_FRA**를 선택합니다.
   - **할당 단위 크기**에서 **4**를 선택합니다.
   - 클릭 `ok` toocreate hello 디스크 그룹입니다.
   - 클릭 `ok` tooclose hello 확인 창이 있습니다.

   ![Hello 디스크 그룹 만들기 대화 상자의 스크린 샷](./media/oracle-asm/asm04.png)

6. 선택 **종료** tooclose ASM Configuration Assistant 합니다.

   ![스크린 샷 hello 구성 ASM: 끝내기 단추와 디스크 그룹 대화 상자](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Hello 데이터베이스 만들기

Oracle 데이터베이스 소프트웨어 hello hello Azure 마켓플레이스 이미지에 이미 설치 되었습니다. toocreate 데이터베이스를 전체 hello 단계를 수행 합니다.

1. 사용자가 toohello Oracle superuser 전환한 다음 로깅에 대 한 hello 수신기를 초기화 합니다.

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   데이터베이스 구성 도우미가 열립니다.

2. Hello에 **데이터베이스 작업** 페이지 `Create Database`합니다.

3. Hello에 **생성 모드** 페이지:

   - Hello 데이터베이스에 대 한 이름을 입력 합니다.
   - **저장소 형식**의 경우 **ASM(자동 저장소 관리)**을 선택하도록 합니다.
   - 에 대 한 **데이터베이스 파일 위치**, hello 기본값을 사용 하 여 ASM 제안 위치입니다.
   - 에 대 한 **빠른 복구 영역**, hello 기본값을 사용 하 여 ASM 제안 위치입니다.
   - **관리 암호** 및 **암호 확인**을 입력합니다.
   - `create as container database`를 선택했는지 확인합니다.
   - `pluggable database name` 값을 입력합니다.

4. Hello에 **요약** 페이지에서 선택한 설정을 검토 한 다음 클릭 `Finish` toocreate hello 데이터베이스입니다.

   ![Hello 요약 페이지의 스크린샷](./media/oracle-asm/createdb03.png)

5. hello 데이터베이스 생성 되었습니다. Hello에 **마침** 페이지에서는 hello toounlock 추가 계정을 toouse이이 데이터베이스 옵션 및 hello 암호를 변경할 수 있습니다. Toodo 하므로, 선택 **암호 관리** -그렇지 않으면 클릭 `close`합니다.

## <a name="delete-hello-vm"></a>Hello VM 삭제

저장소 관리를 자동화 하는 Oracle hello Azure Marketplace에서에서 hello Oracle DB 이미지에서 구성 했습니다.  이 VM이 필요 없는 경우 hello 다음 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 사용할 수 없습니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

[자습서: Oracle DataGuard 구성](configure-oracle-dataguard.md)

[자습서: Oracle GoldenGate 구성](Configure-oracle-golden-gate.md)

[Oracle DB 설계](oracle-design.md) 검토
