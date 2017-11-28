---
title: "Azure RemoteApp에 대 한 사용자 지정 이미지 aaaUpload | Microsoft Docs"
description: "어떻게 tooupload 사용자 지정 이미지를 Azure RemoteApp에 알아봅니다"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="65813-103">Azure RemoteApp에 대한 사용자 지정 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="65813-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="65813-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="65813-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="65813-106">이 변경 내용으로 업데이트 또는 사용자 지정 템플릿 이미지를 만든 해야 tooupload 해당 이미지 tooyour Azure RemoteApp 이미지 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="65813-107">다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="65813-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="65813-108">Before you start</span></span>
1. <span data-ttu-id="65813-109">사용자 지정 이미지 hello 충족 확인 [이미지 요구 사항](remoteapp-imagereqs.md) 및 [응용 프로그램 요구 사항](remoteapp-appreqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="65813-110">Hello 설치 [Azure PowerShell 모듈](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="65813-111">방법에 대해 과정을 단계별로 tooupload 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="65813-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="65813-112">Azure 관리 포털을 열고 toohello RemoteApp 페이지를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="65813-113">Hello에 **템플릿 이미지** 탭을 클릭 **업로드** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="65813-114">이미지에 대 한 이름을 입력 하 고 hello 저장소 계정 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="65813-115">Hello 위치는 hello 확인 RemoteApp 컬렉션이 나 하나 toocreate 저장할 위치와 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="65813-116">메시지가 표시 되 면 다운로드 hello 스크립트 tooyour 로컬 PC입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="65813-117">Hello 명령 매개 변수 hello 텍스트 상자 tooyour 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="65813-118">관리자 권한 Windows PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65813-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="65813-119">관리자 권한 Windows PowerShell 창을 hello에서 toohello 이동 hello 스크립트를 다운로드 하는 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="65813-120">붙여넣기 hello 명령 및 키를 눌러 복사 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="65813-121">hello 업로드 프로세스 시작 되 고 기간 네트워크 속도 hello 이미지의 크기를 비롯 한 여러 요인에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="65813-122">업로드가 성공 하지 못하면 네트워크 중단 또는 작업으로 인해 그렇게 하는 경우 항상 hello 업로드 프로세스를 시작한 재개할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="65813-123">hello 스크립트를 사용 하 여 다시 실행 하는 업로드 tooresume hello 동일 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="65813-124">Hello 업로드 스크립트를 수정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="65813-124">Never modify hello upload script.</span></span> <span data-ttu-id="65813-125">특정 확인 이미지 충족 hello 이미지 요구 사항 및 응용 프로그램 요구 사항 hello 구현된 tooensure 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="65813-126">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="65813-126">Common problems</span></span>
* <span data-ttu-id="65813-127">Azure PowerShell이 아닌 Windows PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="65813-128">Hello 업로드 프로세스 중 특정 모듈에 필요 하기 때문에 필요가 tooinstall hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="65813-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="65813-129">Hello 스크립트 변경해 서는 안, 유효성 검사는 사용자 편의 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="65813-130">Hello vhd 파일 업로드 중 잠겨 가져옵니다 hello 파일을 복사 또는 tooa 새 위치 및 시도 업로드 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="65813-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="65813-131">업로드를 방지하는 일부 Windows 프로세스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65813-131">There might be some Windows process that is preventing upload.</span></span>  

