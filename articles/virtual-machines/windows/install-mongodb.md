---
title: "Azure에서 Windows VM에 MongoDB 설치 | Microsoft Docs"
description: "Windows Server 2012 R2를 실행하는 Azure VM에 Resource Manager 배포 모델을 사용하여 만든 MongoDB를 설치하는 방법을 알아봅니다."
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
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="f8d6b-103">Azure에서 Windows VM에 MongoDB를 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="f8d6b-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="f8d6b-104">[MongoDB](http://www.mongodb.org)는 인기 있는 오픈 소스 고성능 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f8d6b-105">이 문서에서는 Azure에서 Windows Server 2012 R2 VM(가상 컴퓨터)에 MongoDB를 설치 및 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="f8d6b-106">[Azure에서 Linux VM에 MongoDB를 설치](../linux/install-mongodb.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8d6b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8d6b-107">Prerequisites</span></span>
<span data-ttu-id="f8d6b-108">MongoDB를 설치 및 구성하기 전에 VM을 만들고, 데이터 디스크를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="f8d6b-109">다음 문서를 참조하여 VM을 만들고 데이터 디스크를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="f8d6b-110">[Azure Portal](quick-create-portal.md) 또는 [Azure PowerShell](quick-create-powershell.md)을 사용하여 Windows Server VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="f8d6b-111">[Azure Portal](attach-managed-disk-portal.md) 또는 [Azure PowerShell](attach-disk-ps.md)을 사용하여 Windows Server VM에 데이터 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="f8d6b-112">MongoDB 설치 및 구성을 시작하려면 원격 데스크톱을 사용하여 [Windows Server VM에 로그온](connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="f8d6b-113">MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="f8d6b-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8d6b-114">인증 및 IP 주소 바인딩과 같은 MongoDB 보안 기능은 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="f8d6b-115">MongoDB를 프로덕션 환경에 배포하기 전에 보안 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="f8d6b-116">자세한 내용은 [MongoDB 보안 및 인증](http://www.mongodb.org/display/DOCS/Security+and+Authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="f8d6b-117">원격 데스크톱을 사용하여 VM에 연결한 후에는 VM의 **시작** 메뉴에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="f8d6b-118">Internet Explorer가 처음으로 열리면 **권장 보안, 개인 정보 및 호환성 설정 사용**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="f8d6b-119">Internet Explorer 향상된 보안 구성이 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="f8d6b-120">허용되는 사이트 목록에 MongoDB 웹 사이트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="f8d6b-121">오른쪽 위 모퉁이에서 **도구** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="f8d6b-122">**인터넷 옵션**에서 **보안** 탭을 선택한 다음 **신뢰할 수 있는 사이트** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="f8d6b-123">**사이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-123">Click the **Sites** button.</span></span> <span data-ttu-id="f8d6b-124">신뢰할 수 있는 사이트 목록에 *https://\*.mongodb.org*를 추가하고 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Internet Explorer 보안 설정 구성](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="f8d6b-126">[MongoDB - 다운로드](http://www.mongodb.org/downloads) 페이지(http://www.mongodb.org/downloads)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="f8d6b-127">필요한 경우 **커뮤니티 서버** 버전을 선택한 후 Windows Server 2008 R2 64비트 이상의 안정판을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="f8d6b-128">설치 관리자를 다운로드하려면 **다운로드(msi)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![MongoDB 설치 관리자 다운로드](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="f8d6b-130">다운로드가 완료되면 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="f8d6b-131">사용권 계약을 읽고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-131">Read and accept the license agreement.</span></span> <span data-ttu-id="f8d6b-132">메시지가 나타나면 **전체**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="f8d6b-133">마지막 화면에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="f8d6b-134">VM 및 MongoDB 구성</span><span class="sxs-lookup"><span data-stu-id="f8d6b-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="f8d6b-135">path 변수는 MongoDB 설치 관리자를 통해 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="f8d6b-136">path 변수에 MongoDB `bin` 위치가 없으면 MongoDB 실행 파일을 사용할 때마다 전체 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="f8d6b-137">path 변수에 위치를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="f8d6b-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="f8d6b-138">**시작** 메뉴를 마우스 오른쪽 단추로 클릭하고 **시스템**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="f8d6b-139">**고급 시스템 설정**을 클릭한 다음 **환경 변수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="f8d6b-140">**시스템 변수**에서 **경로**를 선택한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![PATH 변수 구성](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="f8d6b-142">MongoDB `bin` 폴더에 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="f8d6b-143">일반적으로 MongoDB는 *C:\Program Files\MongoDB*에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="f8d6b-144">VM의 설치 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="f8d6b-145">다음은 `PATH` 변수에 기본 MongoDB 설치 위치를 추가하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="f8d6b-146">`PATH` 변수에 위치를 추가하는 것을 나타내는 선행 세미콜론(`;`)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="f8d6b-147">데이터 디스크에 MongoDB 데이터 및 로그 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="f8d6b-148">**시작** 메뉴에서 **명령 프롬프트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="f8d6b-149">다음 예에서는 F: 드라이브에 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="f8d6b-150">다음 명령을 사용하여 MongoDB 인스턴스를 시작하 고, 데이터 및 로그 디렉터리를 적절하게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="f8d6b-151">MongoDB가 저널 파일을 할당하고 연결 수신을 시작할 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="f8d6b-152">`mongod.exe` 서버가 시작되어 저널 파일을 할당하면 모든 로그 메시지가 *F:\MongoLogs\mongolog.log* 파일로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8d6b-153">명령 프롬프트는 MongoDB 인스턴스가 실행되는 동안 이 태스크에 계속 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="f8d6b-154">명령 프롬프트 창을 열어 놓고 MongoDB를 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="f8d6b-155">또는 다음 단계에 설명된 대로 MongoDB를 서비스로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="f8d6b-156">보다 강력한 MongoDB 경험을 원한다면 `mongod.exe`를 서비스로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="f8d6b-157">서비스를 만들면 MongoDB를 사용할 때마다 명령 프롬프트를 계속 실행 상태로 둘 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="f8d6b-158">다음과 같이 서비스를 만들고, 데이터 및 로그 디렉터리 경로를 적절하게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="f8d6b-159">앞의 명령은 MongoDB라는 이름의 서비스를 만들고 그에 대한 설명으로 "Mongo DB"를 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="f8d6b-160">다음 매개 변수도 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="f8d6b-161">`--dbpath` 옵션은 데이터 디렉터리의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="f8d6b-162">실행 중인 서비스는 명령 창에 결과가 표시되지 않으므로 `--logpath` 옵션을 사용하여 로그 파일을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="f8d6b-163">`--logappend` 옵션은 서비스를 다시 시작할 때 기존 로그 파일에 출력을 추가하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="f8d6b-164">MongoDB 서비스를 시작하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="f8d6b-165">MongoDB 서비스를 만드는 방법에 대한 자세한 내용은 [MongoDB에 대한 Windows 서비스 구성](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="f8d6b-166">MongoDB 인스턴스 테스트</span><span class="sxs-lookup"><span data-stu-id="f8d6b-166">Test the MongoDB instance</span></span>
<span data-ttu-id="f8d6b-167">MongoDB를 단일 인스턴스로 실행하거나 서비스로 설치했으면, 이제 데이터베이스를 만들어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="f8d6b-168">MongoDB 관리 셸을 시작하려면 **시작** 메뉴에서 명령 프롬프트 창을 하나 더 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="f8d6b-169">`db` 명령으로 데이터베이스를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="f8d6b-170">다음과 같이 일부 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="f8d6b-171">다음과 같이 일부 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="f8d6b-172">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="f8d6b-173">다음과 같이 `mongo` 콘솔을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="f8d6b-174">방화벽 및 네트워크 보안 그룹 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="f8d6b-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="f8d6b-175">MongoDB를 설치하고 실행했으니, 원격으로 MongoDB에 연결할 수 있도록 Windows 방화벽에 있는 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="f8d6b-176">TCP 포트 27017을 허용하는 새 인바운드 규칙을 만들려면 관리 PowerShell 프롬프트를 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="f8d6b-177">**고급 보안이 포함된 Windows 방화벽** 그래픽 관리 도구를 사용하여 규칙을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="f8d6b-178">TCP 포트 27017을 허용하는 새 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="f8d6b-179">필요한 경우 기존 Azure 가상 네트워크 서브넷 외부에서 MongoDB에 액세스하도록 허용하는 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="f8d6b-180">[Azure Portal](nsg-quickstart-portal.md) 또는 [Azure PowerShell](nsg-quickstart-powershell.md)을 사용하여 네트워크 보안 그룹 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="f8d6b-181">Windows 방화벽 규칙과 마찬가지로 MongoDB VM의 가상 네트워크 인터페이스에 TCP 포트 27017을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="f8d6b-182">TCP 포트 27017은 MongoDB가 사용하는 기본 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="f8d6b-183">수동으로 또는 서비스에서 `mongod.exe`를 시작하고 `--port` 매개 변수를 사용하여 이 포트를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="f8d6b-184">포트를 변경하는 경우 이전 단계의 Windows 방화벽 및 네트워크 보안 그룹 규칙을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f8d6b-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8d6b-185">Next steps</span></span>
<span data-ttu-id="f8d6b-186">이 자습서에서는 Windows VM에 MongoDB를 설치하고 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="f8d6b-187">이제 [MongoDB 설명서](https://docs.mongodb.com/manual/)(영문)의 고급 토픽에 따라 Windows VM의 MongoDB에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d6b-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

