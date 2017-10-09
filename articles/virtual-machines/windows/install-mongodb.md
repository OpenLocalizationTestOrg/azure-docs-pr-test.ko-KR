---
title: "Azure에서 Windows VM에서 MongoDB aaaInstall | Microsoft Docs"
description: "Windows Server 2012 r 2를 실행 하는 Azure VM에서 MongoDB tooinstall hello 리소스 관리자 배포 모델에 만드는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="6d428-103">Azure에서 Windows VM에 MongoDB를 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="6d428-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="6d428-104">[MongoDB](http://www.mongodb.org)는 인기 있는 오픈 소스 고성능 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="6d428-105">이 문서에서는 Azure에서 Windows Server 2012 R2 VM(가상 컴퓨터)에 MongoDB를 설치 및 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="6d428-106">[Azure에서 Linux VM에 MongoDB를 설치](../linux/install-mongodb.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d428-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d428-107">Prerequisites</span></span>
<span data-ttu-id="6d428-108">설치 및 구성 하기 전에 MongoDB, 있습니다 toocreate VM와 해야 데이터 디스크 tooit 이상적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="6d428-109">Hello 문서 toocreate VM 다음을 참조 하 고 데이터 디스크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="6d428-110">사용 하 여 Windows Server VM 만들기 [Azure 포털 hello](quick-create-portal.md) 또는 [Azure PowerShell](quick-create-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="6d428-111">디스크 tooa Windows Server VM 사용 하 여 데이터 연결 [Azure 포털 hello](attach-managed-disk-portal.md) 또는 [Azure PowerShell](attach-disk-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="6d428-112">설치 및 구성, MongoDB toobegin [tooyour Windows Server VM에 로그온](connect-logon.md) 원격 데스크톱을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="6d428-113">MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="6d428-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d428-114">인증 및 IP 주소 바인딩과 같은 MongoDB 보안 기능은 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="6d428-115">MongoDB tooa 프로덕션 환경에 배포 하기 전에 보안 기능을 활성화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="6d428-116">자세한 내용은 [MongoDB 보안 및 인증](http://www.mongodb.org/display/DOCS/Security+and+Authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d428-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="6d428-117">Tooyour 원격 데스크톱을 사용 하 여 VM을 연결 하 고 나면 hello에서 Internet Explorer를 열고 **시작** hello VM에 대 한 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="6d428-118">Internet Explorer가 처음으로 열리면 **권장 보안, 개인 정보 및 호환성 설정 사용**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="6d428-119">Internet Explorer 향상된 보안 구성이 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="6d428-120">Hello MongoDB 웹 사이트 toohello 목록이 허용 된 사이트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="6d428-121">선택 hello **도구** hello 오른쪽 위 모서리에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="6d428-122">**인터넷 옵션**선택, hello **보안** 탭을 선택한 후 hello **신뢰할 수 있는 사이트** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="6d428-123">Hello 클릭 **사이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-123">Click hello **Sites** button.</span></span> <span data-ttu-id="6d428-124">추가 *https://\*. mongodb.org* 신뢰할 수 있는 사이트와 종가 hello 대화 상자의 toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Internet Explorer 보안 설정 구성](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="6d428-126">Toohello 찾아보기 [MongoDB-다운로드](http://www.mongodb.org/downloads) 페이지 (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="6d428-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="6d428-127">필요에 따라 선택 hello **Community 서버** 버전과 선택 hello 최신 현재 안정판 Windows Server 2008 R2 64 비트 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="6d428-128">toodownload hello 설치 관리자를 클릭 **다운로드 (msi)**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![MongoDB 설치 관리자 다운로드](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="6d428-130">Hello 다운로드가 완료 된 후 hello 설치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="6d428-131">읽기 및 hello 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="6d428-132">메시지가 나타나면 **전체**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="6d428-133">Hello 마지막 화면에서 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="6d428-134">Hello VM 및 MongoDB 구성</span><span class="sxs-lookup"><span data-stu-id="6d428-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="6d428-135">hello 경로 변수 hello MongoDB 설치 프로그램에서 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="6d428-136">Hello MongoDB 없이 `bin` path 변수에 위치 toospecify hello에 대 한 전체 경로 때마다 필요한 MongoDB 실행 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="6d428-137">tooadd hello 위치 tooyour 경로 변수:</span><span class="sxs-lookup"><span data-stu-id="6d428-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="6d428-138">마우스 오른쪽 단추로 클릭 hello **시작** 메뉴에서을 선택 **시스템**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="6d428-139">**고급 시스템 설정**을 클릭한 다음 **환경 변수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="6d428-140">**시스템 변수**에서 **경로**를 선택한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![PATH 변수 구성](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="6d428-142">Hello 경로 tooyour MongoDB 추가 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="6d428-143">일반적으로 MongoDB는 *C:\Program Files\MongoDB*에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="6d428-144">VM에 hello 설치 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="6d428-145">hello 다음 예제에서는 추가 hello 기본 MongoDB 설치 위치 toohello `PATH` 변수:</span><span class="sxs-lookup"><span data-stu-id="6d428-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="6d428-146">있는지 tooadd hello 선행 세미콜론 수 (`;`) 위치 tooyour 추가 하는 tooindicate `PATH` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="6d428-147">데이터 디스크에 MongoDB 데이터 및 로그 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="6d428-148">Hello에서 **시작** 메뉴 선택 **명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="6d428-149">다음 예제는 hello f: 드라이브에 hello 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="6d428-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="6d428-150">다음 명령을, hello 경로 tooyour 데이터 조정 hello MongoDB 인스턴스를 시작 하 고 그에 따라 로그 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="6d428-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="6d428-151">Hello 저널 파일 MongoDB tooallocate 분이 걸릴 하 고 연결에 대 한 수신을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="6d428-152">모든 로그 메시지는 방향이 지정 된 toohello *F:\MongoLogs\mongolog.log* 다른 이름으로 파일 `mongod.exe` 서버 시작 및 저널 파일을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d428-153">명령 프롬프트 hello MongoDB 인스턴스가 실행 되는 동안이 작업에 초점을 맞추고 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="6d428-154">Hello 명령 프롬프트 창을 열고 toocontinue MongoDB 실행 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="6d428-155">또는 MongoDB hello 다음 단계에 설명 된 대로 서비스로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="6d428-156">보다 강력한 MongoDB 경험을 위해 설치 hello `mongod.exe` 서비스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="6d428-157">서비스를 만드는 의미 toouse MongoDB 때마다 실행 된 명령 프롬프트 tooleave 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="6d428-158">서비스를 만들 hello 다음과 같이 hello 경로 tooyour 데이터 및 로그 디렉터리를 적절 하 게 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="6d428-159">hello 앞의 명령은 서비스를 만든 MongoDB, "Mongo DB"에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="6d428-160">hello 매개 변수 뒤도 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="6d428-161">hello `--dbpath` 옵션 hello 데이터 디렉터리의 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="6d428-162">hello `--logpath` 옵션 명령 창 toodisplay 출력 hello 실행 중인 서비스에 없기 때문에 로그 파일을 사용 하는 toospecify 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="6d428-163">hello `--logappend` hello 서비스를 다시 시작 하면 출력 tooappend toohello 기존 로그 파일이 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="6d428-164">toostart hello MongoDB 서비스를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="6d428-165">Hello MongoDB 서비스를 만드는 방법에 대 한 자세한 내용은 참조 [MongoDB에 대 한 Windows 서비스를 구성](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="6d428-166">테스트 hello MongoDB 인스턴스</span><span class="sxs-lookup"><span data-stu-id="6d428-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="6d428-167">MongoDB를 단일 인스턴스로 실행하거나 서비스로 설치했으면, 이제 데이터베이스를 만들어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="6d428-168">toostart hello MongoDB 관리 셸 hello에서 다른 명령 프롬프트 창을 열고 **시작** 메뉴 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="6d428-169">Hello로 hello 데이터베이스를 나열할 수 `db` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="6d428-170">다음과 같이 일부 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="6d428-171">다음과 같이 일부 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="6d428-172">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="6d428-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="6d428-173">종료 hello `mongo` 다음과 같이 콘솔:</span><span class="sxs-lookup"><span data-stu-id="6d428-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="6d428-174">방화벽 및 네트워크 보안 그룹 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="6d428-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="6d428-175">MongoDB 설치 되어 실행 했으므로 tooMongoDB를 원격으로 연결할 수 있도록 Windows 방화벽에서 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="6d428-176">toocreate 새 인바운드 규칙 tooallow TCP 포트 27017, 관리 PowerShell 프롬프트를 열고 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="6d428-177">Hello를 사용 하 여 hello 규칙을 만들 수도 **고급 보안이 포함 된 Windows 방화벽** 그래픽 관리 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="6d428-178">새 인바운드 규칙 tooallow TCP 포트를 27017 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="6d428-179">필요한 경우에 네트워크 보안 그룹 규칙 tooallow 액세스 tooMongoDB에서 hello 기존 Azure 가상 네트워크 서브넷 외부 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="6d428-180">Hello를 사용 하 여 hello 네트워크 보안 그룹 규칙을 만들 수 있습니다 [Azure 포털](nsg-quickstart-portal.md) 또는 [Azure PowerShell](nsg-quickstart-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="6d428-181">Hello Windows 방화벽 규칙에서와 마찬가지로 MongoDB VM의 TCP 포트 27017 toohello 가상 네트워크 인터페이스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="6d428-182">TCP 포트 27017는 MongoDB에서 사용 하는 hello 기본 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="6d428-183">Hello를 사용 하 여이 포트를 변경할 수 있습니다 `--port` 매개 변수를 시작할 때 `mongod.exe` 수동으로 또는 서비스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="6d428-184">Hello 포트를 변경할 경우 hello 이전 단계에서에서 있는지 tooupdate hello Windows 방화벽 및 네트워크 보안 그룹 규칙을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d428-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d428-185">Next steps</span></span>
<span data-ttu-id="6d428-186">이 자습서에서는 방법에 대해 배웠습니다 tooinstall 및 MongoDB Windows VM에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="6d428-187">이제 액세스할 수 있습니다 MongoDB Windows VM에 의해 hello 고급 항목 hello에 다음 [MongoDB 설명서](https://docs.mongodb.com/manual/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d428-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

