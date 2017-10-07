---
title: "aaaDeploying 대규모 배포"
description: "Toodeploy 대규모 배포를 사용 하 여 Azure Toolkit for Eclipse hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="748a2-103">대규모 배포</span><span class="sxs-lookup"><span data-stu-id="748a2-103">Deploying Large Deployments</span></span>
<span data-ttu-id="748a2-104">배포가 너무 커서 toobe hello 기본 approot 폴더에 포함 된 면으로 사용할 수 있습니다 로컬 저장소 리소스 hello 배포 루트 폴더에 jdk 및 응용 프로그램 서버.</span><span class="sxs-lookup"><span data-stu-id="748a2-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="748a2-105">toouse 대규모 배포에 대 한 hello 배포 루트 폴더와 로컬 저장소 리소스</span><span class="sxs-lookup"><span data-stu-id="748a2-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="748a2-106">새 로컬 저장소 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-106">Create a new local storage resource.</span></span> <span data-ttu-id="748a2-107">hello 리소스의 hello 이름 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="748a2-108">저장소 리소스는 hello 역할 수준에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="748a2-109">hello 가장 빠른 방법은 tooaccess hello 로컬 저장소 구성 대화 상자에서 새 로컬 저장소 리소스를 만들 수 있습니다는 단계를 수행 하는 hello를 사용 하 여: hello에서 마우스 오른쪽 단추로 클릭 hello 역할 **프로젝트 탐색기** 보기 (확장 프로그램 Azure 프로젝트 노드 hello 역할 보이지 않는 경우)를 클릭 하 여 **Azure**, 클릭 하 고 **로컬 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="748a2-110">Hello 내 **로컬 저장소** 대화 상자를 클릭 하 여 **추가** toocreate 새 로컬 저장소 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="748a2-111">집합 hello 원하는 크기 tooat 최소 2048MB (아무 것도 덜 hello 같은 파일 크기에서에서 문제가 발생할 수 발생 하는 것 처럼 hello approot).</span><span class="sxs-lookup"><span data-stu-id="748a2-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="748a2-112">확인 **hello 내용을 hello 역할 인스턴스가 재활용 될 때 정리** 확인란이; 것을 방지할 hello 배포의 시작 논리 hello 리소스의 기존 파일과 충돌을 일으키지에서 때 역할 hello 인스턴스가 재활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="748a2-113">해당 hello 확인 **배포 후 리소스의 디렉터리 경로 hello 환경 변수 저장** 값이 설정 toohello 문자열 **DEPLOYROOT**합니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="748a2-114">로컬 저장소 리소스 대화 상자에는 비슷한 toohello 다음을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="748a2-115">또는 사용 하는 경우 **DEPLOYROOT** hello로 *이름* 로컬 리소스의 바뀌지 않는 hello 자동으로 생성 된 환경 변수 이름 (너무 설정 **DEPLOYROOT_PATH** 경우), 응용 프로그램 뿐이 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="748a2-116">로컬 저장소 리소스를 만드는 방법에 대한 추가 정보는 [로컬 저장소 속성][Local storage properties]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="748a2-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="748a2-117">See Also</span></span>
<span data-ttu-id="748a2-118">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="748a2-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="748a2-119">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="748a2-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="748a2-120">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="748a2-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="748a2-121">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="748a2-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
