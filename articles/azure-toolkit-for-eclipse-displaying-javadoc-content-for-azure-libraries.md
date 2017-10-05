---
title: "Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시"
description: "Eclipse에서 Azure 라이브러리의 Javadoc 콘텐츠를 표시하는 방법입니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="5ad4b-103">Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시</span><span class="sxs-lookup"><span data-stu-id="5ad4b-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="5ad4b-104">Javadoc 콘텐츠를 Java용 Azure 라이브러리 패키지에 연결하면 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠를 Eclipse 환경 내에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="5ad4b-105">다음 단계는 Eclipse 내에서 이 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="5ad4b-106">이 절차는 빌드 경로에 Java용 Azure 라이브러리를 이미 추가했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="5ad4b-107">Eclipse에서 Java용 Azure 라이브러리의 Javadoc 콘텐츠를 표시하려면</span><span class="sxs-lookup"><span data-stu-id="5ad4b-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="5ad4b-108">Eclipse의 프로젝트 탐색기에 있는 프로젝트 **참조 라이브러리** 섹션에서 Java JAR용 Azure 라이브러리의 상황에 맞는 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="5ad4b-109">예를 들어 **microsoft windowsazure-api 0.1.0.jar** (버전 번호는 설치한 버전에 따라 다를 수 있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="5ad4b-110">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-110">Click **Properties**.</span></span>

* <span data-ttu-id="5ad4b-111">**속성** 대화 상자의 왼쪽 창에서 **Javadoc 위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="5ad4b-112">**Javadoc Location** (Javadoc 위치) 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="5ad4b-113">**Javadoc URL** 또는 **보관 중인 Javadoc**을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="5ad4b-114">**Javadoc URL**을 지정하도록 선택하는 경우 **http://dl.windowsazure.com/javadoc** 또는 **http://dl.windowsazure.com/storage/javadoc**와 같은 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="5ad4b-115">**Javadoc in archive**(보관 중인 Javadoc)를 사용하도록 선택하는 경우 외부 파일 또는 작업 영역 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="5ad4b-116">필요에 따라 선택하여 찾거나 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="5ad4b-117">다음 예제에서는 Java용 Azure 라이브러리를 **c:\MyAzureJARs**라는 폴더에 로컬로 다운로드된 해당 Javadoc JAR와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="5ad4b-118">*옵션 단계*: **유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="5ad4b-119">Javadoc JAR의 잠재적 문제가 여기에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="5ad4b-120">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-120">Click **OK**.</span></span>

<span data-ttu-id="5ad4b-121">라이브러리에 연결되면 Javadoc 콘텐츠가 Eclipse IDE 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="5ad4b-122">예를 들어 `blob`이 코드에서 `CloudBlockBlob` 형식으로 정의되는 경우 다음은 코드에서 `blob.acquireLease`를 입력했을 때 표시되는 Javadoc 콘텐츠의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="5ad4b-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5ad4b-123">See Also</span></span>
<span data-ttu-id="5ad4b-124">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5ad4b-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="5ad4b-125">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5ad4b-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="5ad4b-126">[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5ad4b-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="5ad4b-127">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
