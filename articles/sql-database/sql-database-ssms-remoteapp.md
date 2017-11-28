---
title: "aaaConnect tooSQL SQL Server Management Studio를 사용 하 여 Azure RemoteApp에서 데이터베이스 | Microsoft Docs"
description: "이 자습서 toolearn를 어떻게 사용 하 여 보안과 tooSQL 데이터베이스를 연결할 때 성능에 대 한 Azure RemoteApp에서 SQL Server Management Studio toouse"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="1f7fc-103">Azure RemoteApp tooconnect tooSQL 데이터베이스에서에서 SQL Server Management Studio 사용</span><span class="sxs-lookup"><span data-stu-id="1f7fc-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f7fc-104">Azure RemoteApp은 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="1f7fc-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="1f7fc-106">소개</span><span class="sxs-lookup"><span data-stu-id="1f7fc-106">Introduction</span></span>
<span data-ttu-id="1f7fc-107">이 자습서에서는 Azure RemoteApp tooconnect tooSQL 데이터베이스에서에서 SQL Server Management Studio (SSMS) toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="1f7fc-108">Hello Azure RemoteApp에서 SQL Server Management Studio를 설정 과정을 안내 합니다, hello 이점을 설명 하 고 Azure Active Directory에서 사용할 수 있는 보안 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="1f7fc-109">**예상 시간 toocomplete:** 45 분</span><span class="sxs-lookup"><span data-stu-id="1f7fc-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="1f7fc-110">Azure RemoteApp의 SSMS</span><span class="sxs-lookup"><span data-stu-id="1f7fc-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="1f7fc-111">Azure RemoteApp은 응용 프로그램을 제공하는 Azure의 RDS 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="1f7fc-112">[RemoteApp이란?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="1f7fc-113">Azure RemoteApp은 실행 되는 SSMS SSMS를 로컬로 실행 같은 환경을 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Azure RemoteApp에서 실행되는 SSMS를 보여주는 스크린 샷][1]

## <a name="benefits"></a><span data-ttu-id="1f7fc-115">이점</span><span class="sxs-lookup"><span data-stu-id="1f7fc-115">Benefits</span></span>
<span data-ttu-id="1f7fc-116">많은 이점을 toousing Azure RemoteApp에서 SSMS는 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="1f7fc-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="1f7fc-117">Azure SQL server에서 1433 포트에는 외부에서 (외부 Azure) 노출 toobe 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="1f7fc-118">추가 하 고 hello Azure SQL server 방화벽의 IP 주소를 제거 하지 필요 tookeep 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="1f7fc-119">Azure RemoteApp 연결은 모두 암호화된 원격 데스크톱 프로토콜을 사용하여 포트 443에서 HTTPS를 통해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="1f7fc-120">다중 사용자이며 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="1f7fc-121">Hello에서 SSMS를 설치에서 향상 된 성능이 hello SQL 데이터베이스와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="1f7fc-122">사용자 작업 보고서에는 Azure Active Directory Premium 버전 hello Azure RemoteApp의 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="1f7fc-123">Multi-Factor Authentication(MFA)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="1f7fc-124">액세스 hello를 사용 하 여 경우에 아무 곳 이나 SSMS iOS, Android, Mac, Windows Phone 및 Windows PC의 포함 된 Azure RemoteApp 클라이언트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="1f7fc-125">Hello Azure RemoteApp 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="1f7fc-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="1f7fc-126">다음 단계 toocreate hello SSMS로 Azure RemoteApp 컬렉션은:</span><span class="sxs-lookup"><span data-stu-id="1f7fc-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="1f7fc-127">1. 이미지에서 새 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1f7fc-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="1f7fc-128">새 VM hello hello 갤러리 toomake에서 "Windows Server 원격 데스크톱 세션 호스트 Windows Server 2012 R2" 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="1f7fc-129">2. SQL Express에서 SSMS 설치</span><span class="sxs-lookup"><span data-stu-id="1f7fc-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="1f7fc-130">이동에 새 VM hello 이동한 toothis 다운로드 페이지: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="1f7fc-131">옵션 tooonly 다운로드 SSMS는.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="1f7fc-132">다운로드 hello 설치 디렉터리로 이동한 다음 설치 프로그램 tooinstall SSMS를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="1f7fc-133">SQL Server 2014 서비스 팩 1 tooinstall을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="1f7fc-134">다음에서 다운로드할 수 있습니다. [Microsoft SQL Server 2014 Service Pack 1(SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="1f7fc-135">SQL Server 2014 서비스 팩 1에는 Azure SQL 데이터베이스로 작업하기 위한 중요한 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="1f7fc-136">3. 유효성 검사 스크립트 및 Sysprep 실행</span><span class="sxs-lookup"><span data-stu-id="1f7fc-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="1f7fc-137">Hello hello VM의 데스크톱에는 유효성 검사를 호출 하는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="1f7fc-138">두 번 클릭하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-138">Run this by double-clicking.</span></span> <span data-ttu-id="1f7fc-139">해당 hello VM은 응용 프로그램의 원격 호스트에 사용 되는 준비 toobe 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="1f7fc-140">Toorun sysprep-이름을 묻는 확인 완료 되 면 toorun 선택할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="1f7fc-141">Sysprep이 완료 되 면 hello VM 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="1f7fc-142">Azure RemoteApp 이미지에 대 한 만들기에 대 한 더 toolearn 참조: [Azure에서 toocreate RemoteApp 템플릿 이미지 하는 방법](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="1f7fc-143">4. 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="1f7fc-143">4. Capture image</span></span>
<span data-ttu-id="1f7fc-144">Hello 실행, VM이 중지 되었습니다 hello 현재 포털에서 찾을 하 고 캡처하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="1f7fc-145">이미지 캡처에 대 한 더 toolearn 참조 [hello 클래식 배포 모델을 사용 하 여 만든 Azure Windows 가상 컴퓨터의 이미지 캡처](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="1f7fc-146">5. TooAzure RemoteApp 템플릿 이미지 추가</span><span class="sxs-lookup"><span data-stu-id="1f7fc-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="1f7fc-147">Hello hello 현재 포털의 Azure RemoteApp 섹션, toohello 템플릿 이미지 탭으로 이동 하 고 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="1f7fc-148">Hello 팝업 상자에 "가상 컴퓨터 라이브러리에서 이미지 가져오기"를 선택 하 고 hello 방금 만든 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="1f7fc-149">6. 클라우드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="1f7fc-149">6. Create cloud collection</span></span>
<span data-ttu-id="1f7fc-150">Hello 현재 포털에서 새 Azure RemoteApp 클라우드 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="1f7fc-151">Hello를 설치 하는 SSMS로 방금 가져온 템플릿 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![새 클라우드 컬렉션 만들기][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="1f7fc-153">7. SSMS 게시</span><span class="sxs-lookup"><span data-stu-id="1f7fc-153">7. Publish SSMS</span></span>
<span data-ttu-id="1f7fc-154">Hello 시작 메뉴에서 게시를 선택 하면 새 클라우드 컬렉션의 탭에서 응용 프로그램을 게시 하는 hello 및 SSMS hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![앱 게시][5]

### <a name="8-add-users"></a><span data-ttu-id="1f7fc-156">8. 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="1f7fc-156">8. Add users</span></span>
<span data-ttu-id="1f7fc-157">Hello 사용자 액세스 탭에서 SSMS를만 포함 하는 액세스 toothis Azure RemoteApp 컬렉션에 있는 hello 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![사용자 추가][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="1f7fc-159">9. Hello Azure RemoteApp에 대 한 클라이언트 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="1f7fc-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="1f7fc-160">다음에 Azure RemoteApp 클라이언트를 다운로드하고 설치할 수 있습니다. [다운로드 | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="1f7fc-161">Azure SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="1f7fc-161">Configure Azure SQL server</span></span>
<span data-ttu-id="1f7fc-162">hello는 tooensure Azure 서비스를 제공 하는 필요한 구성 설정 되어 있는 hello 방화벽에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="1f7fc-163">이 솔루션을 사용 하는 경우 다음 불필요 tooadd 모든 IP 주소 tooopen hello 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="1f7fc-164">SQL Server toohello 허용 되는 hello 네트워크 트래픽은 다른 Azure 서비스에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Azure 허용][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="1f7fc-166">Multi-Factor Authentication(MFA)</span><span class="sxs-lookup"><span data-stu-id="1f7fc-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="1f7fc-167">MFA는 이 응용 프로그램에 구체적으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="1f7fc-168">Azure Active Directory의 toohello 응용 프로그램 탭을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="1f7fc-169">Microsoft Azure RemoteApp에 대한 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="1f7fc-170">해당 응용 프로그램을 클릭 한 다음을 구성 하는 경우이 응용 프로그램에 MFA를 사용할 수 있는 hello 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![MFA 사용][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="1f7fc-172">Azure Active Directory Premium으로 사용자 작업 감사</span><span class="sxs-lookup"><span data-stu-id="1f7fc-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="1f7fc-173">Tooturn 해야 Azure AD Premium, 없는 경우 디렉터리의 라이선스 섹션을 hello에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="1f7fc-174">사용 하도록 설정 하는 premium을 toohello Premium 수준 사용자에 게 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="1f7fc-175">Azure Active Directory에서 tooa 사용자를 이동할 때 다음 toohello 활동 탭 toosee 로그인 정보 tooAzure RemoteApp을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f7fc-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f7fc-176">Next steps</span></span>
<span data-ttu-id="1f7fc-177">모든 hello 단계를 완료 한 후 있습니다 수 toorun hello Azure RemoteApp 클라이언트 되며 할당된 된 사용자에 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="1f7fc-178">사용자 응용 프로그램 중 하나로 SSMS로 표시 되 고 tooAzure SQL server 액세스를 사용 하 여 컴퓨터에 설치 되어 있는 것 처럼 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="1f7fc-179">Toomake 연결 tooSQL 데이터베이스 hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [샘플 T-SQL 쿼리를 수행 하 고 SQL Server Management Studio를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-ssms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="1f7fc-180">이게 전부입니다.</span><span class="sxs-lookup"><span data-stu-id="1f7fc-180">That's everything for now.</span></span> <span data-ttu-id="1f7fc-181">마음껏 즐기세요!</span><span class="sxs-lookup"><span data-stu-id="1f7fc-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png