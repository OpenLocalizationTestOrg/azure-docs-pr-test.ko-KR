---
title: "hello Linux 데이터 과학 가상 컴퓨터에 aaaData 과학 | Microsoft Docs"
description: "방식과 tooperform 몇 가지 일반 데이터 과학 작업 Linux 데이터 과학 VM hello로 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="d822b-103">데이터 과학 hello Linux 데이터 과학 가상 컴퓨터에</span><span class="sxs-lookup"><span data-stu-id="d822b-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="d822b-104">이 연습에서는 어떻게 tooperform 몇 가지 일반 데이터 과학 작업을 Linux 데이터 과학 VM hello로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="d822b-105">hello Linux 데이터 과학 가상 컴퓨터 (DSVM)는 일반적으로 데이터 분석 및 기계 학습에 사용 되는 도구 모음 미리 설치 되어 있는 Azure에서 제공 되는 가상 컴퓨터 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="d822b-106">hello에 hello 핵심 소프트웨어 구성 요소는 항목별로 [Linux 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-linux-dsvm-intro.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="d822b-107">hello VM 이미지를 사용 하면 쉽게 tooget tooinstall 필요 없이 데이터 과학 분 후에 수행을 시작 하 고 각 hello 도구를 개별적으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="d822b-108">필요한 경우 VM hello을 확장 하 고 중지할 수 없으면에서 쉽게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="d822b-109">따라서 이 리소스는 탄력적이고 비용 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="d822b-110">hello이 연습에서 설명 하는 데이터 과학 작업 단계에 따라 hello hello에 설명 된 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="d822b-111">이 프로세스는 데이터 과학자 tooeffectively hello 수명 주기 지능형 응용 프로그램 빌드를 통해 협력 하 여 팀 수 있게 하는 체계적 접근 방법 toodata 과학을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="d822b-112">hello 데이터 과학 프로세스는 또한으로 수행할 수 있는 데이터 과학을 위한 반복 되는 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="d822b-113">Hello 분석 [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 이 연습에서 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="d822b-114">스팸 또는 햄 (스팸 없는 의미), 표시 된 전자 메일의 집합은 또한 hello 전자 메일의 hello 내용에 대 한 일부 통계를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="d822b-115">포함 하는 hello 통계는 한 개의 절 이지만 다음 hello에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d822b-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d822b-116">Prerequisites</span></span>
<span data-ttu-id="d822b-117">Linux 데이터 과학 가상 컴퓨터를 사용 하려면 먼저 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="d822b-118">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="d822b-118">An **Azure subscription**.</span></span> <span data-ttu-id="d822b-119">아직 없을 경우 [지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d822b-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d822b-120">[**Linux 데이터 과학 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="d822b-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="d822b-121">이 VM을 프로 비전에 대 한 정보를 참조 하십시오. [Linux 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-linux-dsvm-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="d822b-122">[X2Go](http://wiki.x2go.org/doku.php) .</span><span class="sxs-lookup"><span data-stu-id="d822b-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="d822b-123">**X2Go 클라이언트**설치 및 구성에 대한 자세한 내용은 [X2Go 클라이언트 설치 및 구성](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d822b-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="d822b-124">**AzureML 계정**.</span><span class="sxs-lookup"><span data-stu-id="d822b-124">An **AzureML account**.</span></span> <span data-ttu-id="d822b-125">아직 없는 새 하나씩 hello에 등록 한 경우 [AzureML 홈 페이지](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="d822b-126">시작 하는 데 사용 가능한 계층 toohelp이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="d822b-127">Hello spambase 데이터 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="d822b-127">Download hello spambase dataset</span></span>
<span data-ttu-id="d822b-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 데이터 집합은 상대적으로 작은 4601 예제를 포함 하는 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="d822b-129">이것이 보여는 hello 그대로 hello 데이터 과학 VM의 주요 기능 중 일부 유지 hello 리소스 요구 사항을 적당 한 때 편리한 크기 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-130">이 연습은 D2 v2 크기의 Linux 데이터 과학 가상 컴퓨터에서 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="d822b-131">이 크기 DSVM는 hello이이 연습의 프로시저에에서 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="d822b-132">더 많은 저장 공간이 필요한 경우 추가 디스크를 만들 수 있으며 tooyour VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="d822b-133">이러한 디스크 사용 영구 Azure 저장소의 데이터는 보존 hello 서버 다시 프로 비전 하는 경우에 due tooresizing 또는 종료 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="d822b-134">디스크 tooadd hello 지침에 따라, tooyour VM을 연결 하 고 [디스크 tooa Linux VM 추가](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d822b-135">이러한 단계는 hello DSVM hello에 이미 설치 되어 Azure 명령줄 인터페이스 (Azure CLI)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="d822b-136">따라서 hello VM 자체에서이 절차를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="d822b-137">다른 옵션 tooincrease 저장소는 toouse [Azure 파일](../storage/files/storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="d822b-138">toodownload hello 데이터 터미널 윈도우를 열고이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="d822b-139">hello 다운로드 한 파일이 머리글 행이 되어, 만들어야 헤더에는 다른 파일 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="d822b-140">Hello 적절 한 헤더와 함께이 명령 toocreate 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="d822b-141">다음 hello hello 명령과 함께 두 개의 파일을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="d822b-142">hello 데이터 집합에 각 전자 메일에서 여러 유형의 통계:</span><span class="sxs-lookup"><span data-stu-id="d822b-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="d822b-143">열 같은 ***단어\_등호\_단어*** 일치 하는 hello 전자 메일에 있는 단어의 hello 백분율을 나타내는 *단어*합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="d822b-144">예를 들어 경우 *단어\_등호\_확인* hello 전자 메일에 있는 모든 단어의 1% 된 다음에 1, *확인*합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="d822b-145">열 같은 ***char\_등호\_CHAR*** hello 전자 메일에 있는 모든 문자가 hello 백분율로 나타내는 *CHAR*합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="d822b-146">***자본\_실행\_길이\_가장 긴*** hello 가장 긴 시퀀스의 대문자로 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="d822b-147">***자본\_실행\_길이\_평균*** hello의 대문자로 모든 시퀀스의 평균 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="d822b-148">***자본\_실행\_길이\_총*** hello의 대문자로 모든 시퀀스의 총 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="d822b-149">***스팸*** 여부 hello 전자 메일 스팸이 간주 되는지를 나타내는 (1 = 스팸, 0 = 스팸이 아닌).</span><span class="sxs-lookup"><span data-stu-id="d822b-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="d822b-150">Microsoft R Open과 hello 데이터 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="d822b-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="d822b-151">보겠습니다 hello 데이터를 검사 하 고 몇 가지 기본 기계 학습 데이터 과학 VM와 함께 제공 되는 오른쪽 hello로 실행 [Microsoft R Open](https://mran.revolutionanalytics.com/open/) 미리 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="d822b-152">hello R의이 버전에서는 다중 스레드 수학 라이브러리 더 나은 성능을 제공 단일 스레드 다양 한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="d822b-153">Microsoft R Open 제공 재현 가능성 hello CRAN 패키지 저장소의 스냅숏을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="d822b-154">hello tooget 복사본 코드 복제 hello이이 연습에서 사용 하는 샘플 **Azure-컴퓨터-학습-데이터-과학** 리포지토리를 사용 하 여 git를 hello VM 미리 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="d822b-155">Hello git 명령줄에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="d822b-156">터미널 창을 열고 R hello 대화형 콘솔을 통해 새 R 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-157">다음 절차를 수행 하는 hello에 대 한 RStudio를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="d822b-158">RStudio, tooinstall 터미널에서이 명령을 실행 합니다.`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="d822b-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="d822b-159">tooimport hello 데이터와 hello 환경 설정 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="d822b-160">각 열에 대 한 요약 통계를 toosee:</span><span class="sxs-lookup"><span data-stu-id="d822b-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="d822b-161">에 대 한 hello 데이터의 다른 보기:</span><span class="sxs-lookup"><span data-stu-id="d822b-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="d822b-162">여기에 각 변수의 형식을 hello 및 hello 데이터 집합에 적은 수의 값을 먼저 hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="d822b-163">hello *스팸* 를 정수로 열 읽은 이지만 실제로 범주 변수 (또는 계수).</span><span class="sxs-lookup"><span data-stu-id="d822b-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="d822b-164">tooset 해당 형식:</span><span class="sxs-lookup"><span data-stu-id="d822b-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="d822b-165">toodo 몇 가지 탐구 분석, 사용 하 여 hello [ggplot2](http://ggplot2.org/) 패키지 하 고, VM hello에 이미 설치 되어 R에 대 한 그래프는 인기 있는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="d822b-166">참고 hello 요약 데이터에서 앞에서 표시 된 hello 주파수 hello 느낌표 문자에 요약 통계 있으며 이러한 시각화는.</span><span class="sxs-lookup"><span data-stu-id="d822b-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="d822b-167">다음 명령을 hello로 여기 해당 주파수를 그릴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="d822b-168">Hello 0 막대는 hello 점도 기울이기 이후 보겠습니다 제거:</span><span class="sxs-lookup"><span data-stu-id="d822b-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="d822b-169">흥미롭게도 1보다 큰 특수한 밀도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="d822b-170">해당 데이터를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="d822b-171">스팸과 햄으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="d822b-172">이 예제에서는 해야 사용 하면 hello toomake 비슷한 차트가 다른 열 tooexplore hello 여기에 포함 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="d822b-173">ML 모델 학습 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d822b-173">Train and test an ML model</span></span>
<span data-ttu-id="d822b-174">이제 학습 기계 학습의 두 hello 데이터 집합의 tooclassify hello 전자 메일을 모델링 하는 보겠습니다 중 하나를 포함 하는 것에 걸쳐 실행 하거나 햄 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="d822b-175">이 섹션에서 의사 결정 트리 모델 및 임의 포리스트 모델을 학습하고 해당 예측의 정확도를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-176">hello 코드 다음에 사용 되는 hello rpart (재귀 분할 및 회귀 트리) 패키지는 데이터 과학 VM hello에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="d822b-177">첫째, 학습 및 테스트 집합으로 hello 데이터 집합을 분할 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="d822b-178">한 다음 전자 메일 의사 결정 트리 tooclassify hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="d822b-179">Hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="d822b-181">hello 교육에 얼마나 잘 수행 toodetermine 설정, 코드 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d822b-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="d822b-182">toodetermine 얼마나 잘 hello 테스트 집합에 대해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="d822b-183">임의 포리스트 모델도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-183">Let's also try a random forest model.</span></span> <span data-ttu-id="d822b-184">임의 포리스트는 다 수의 의사 결정 트리를 학습 및 hello 모드 hello 개별 의사 결정 트리의 모든 hello 분류 하는 클래스를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="d822b-185">의사 결정 트리 모델 toooverfit 학습 데이터 집합의 hello 경향에 대 한 올바른 것으로 접근 방식 학습 더 강력한 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="d822b-186">모델 tooAzure ML 배포</span><span class="sxs-lookup"><span data-stu-id="d822b-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="d822b-187">[Azure 기계 학습 스튜디오](https://studio.azureml.net/) (AzureML)는 쉽게 toobuild를 사용 하면 예측 분석 모델을 배포 하는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="d822b-188">AzureML의 hello 훌륭한 기능 중 하나에 모든 R 웹 서비스로 작동 하는 기능 toopublish입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="d822b-189">hello AzureML R 패키지 선택 하면 배포 쉽게 toodo 우리의 R 세션에서 바로 hello DSVM 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="d822b-190">toodeploy hello 의사 결정 트리 코드 hello 이전 섹션에서 toosign tooAzure 기계 학습 스튜디오에에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="d822b-191">작업 영역 ID와에 권한 부여 토큰 toosign가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="d822b-192">toofind 다음 값과 이러한 초기화 hello AzureML 변수:</span><span class="sxs-lookup"><span data-stu-id="d822b-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="d822b-193">선택 **설정을** hello 왼쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="d822b-194">**작업 영역 ID**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="d822b-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="d822b-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="d822b-196">선택 **권한 부여 토큰** hello 오버 헤드 메뉴 및 메모에서 프로그램 **기본 권한 부여 토큰**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="d822b-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="d822b-197">부하 hello **AzureML** 패키지 하 고 hello DSVM에 R 세션에서의 토큰 및 작업 영역 ID 사용 하 여 hello 변수 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="d822b-198">보겠습니다 hello 모델 toomake이 데모 쉽게 tooimplement을 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="d822b-199">Hello 의사 결정 트리 가장 가까운 toohello 루트에서 hello 세 개의 변수를 선택 하 고 이러한 3 개의 변수를 사용 하 여 새 트리를 만들 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="d822b-200">입력으로 hello 기능을 사용 하는 예측 함수 필요 하 고 반환 hello 예측된 값:</span><span class="sxs-lookup"><span data-stu-id="d822b-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="d822b-201">Hello predictSpam 함수 tooAzureML hello를 사용 하 여 게시 **publishWebService** 함수:</span><span class="sxs-lookup"><span data-stu-id="d822b-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="d822b-202">이 함수는 hello **predictSpam** 함수, 웹 서비스를 만든 **spamWebService** 와 입력 및 출력을 정의 하 고 hello 새 끝점에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="d822b-203">Hello 명령 사용 하 여 해당 API 끝점 및 액세스 키를 포함 하 여 웹 서비스를 게시 하는 hello의 세부 정보 보기:</span><span class="sxs-lookup"><span data-stu-id="d822b-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="d822b-204">tootry hello 테스트 집합의 처음 10 개 행을 hello 하는지에:</span><span class="sxs-lookup"><span data-stu-id="d822b-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="d822b-205">사용 가능한 다른 도구 사용</span><span class="sxs-lookup"><span data-stu-id="d822b-205">Use other tools available</span></span>
<span data-ttu-id="d822b-206">나머지 단원 들을 hello toouse hello 도구 중 일부에 설치 하거나 Linux 데이터 과학 VM hello 하는 방법을 보여 줍니다. 다음은 도구 설명 hello 목록이입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="d822b-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="d822b-207">XGBoost</span></span>
* <span data-ttu-id="d822b-208">Python</span><span class="sxs-lookup"><span data-stu-id="d822b-208">Python</span></span>
* <span data-ttu-id="d822b-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="d822b-209">Jupyterhub</span></span>
* <span data-ttu-id="d822b-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="d822b-210">Rattle</span></span>
* <span data-ttu-id="d822b-211">PostgreSQL 및 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="d822b-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="d822b-212">SQL Server 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d822b-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="d822b-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="d822b-213">XGBoost</span></span>
<span data-ttu-id="d822b-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) 는 빠르고 정확하게 향상된 트리 구현을 제공하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="d822b-215">XGBoost는 python 또는 명령줄에서 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="d822b-216">Python</span><span class="sxs-lookup"><span data-stu-id="d822b-216">Python</span></span>
<span data-ttu-id="d822b-217">Python을 사용 하 여 개발 하는 경우 hello Anaconda Python 분포 2.7 및 3.5 DSVM hello에 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-218">hello Anaconda 배포 포함 [Condas](http://conda.pydata.org/docs/index.html)이며 서로 다른 버전 및/또는 패키지에 설치 되어 있는 Python에 대 한 사용된 toocreate 환경 사용자 지정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="d822b-219">보겠습니다 hello spambase 데이터 집합의 일부 읽기 및 지원 벡터 컴퓨터 scikit와 hello 전자 메일을 분류-에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="d822b-220">toomake 예측:</span><span class="sxs-lookup"><span data-stu-id="d822b-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="d822b-221">tooshow 어떻게 AzureML 끝점 toopublish 보겠습니다 더 간단한 모델 만들기 hello로 3 개의 변수 했던 이전에 hello R 모델을 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="d822b-222">toopublish hello 모델 tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="d822b-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="d822b-223">이 작업은 python 2.7에만 사용할 수 있으며 3.5에는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="d822b-224">**/anaconda/bin/python2.7**을 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="d822b-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="d822b-225">Jupyterhub</span></span>
<span data-ttu-id="d822b-226">hello에 hello Anaconda 배포 DSVM Jupyter 노트북, 플랫폼 간 환경 tooshare Python, R, 또는 Julia 코드 및 분석 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="d822b-227">hello Jupyter 노트북 JupyterHub 통해 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="d822b-228">***https://\<VM DNS 이름 또는 IP 주소\>:8000/***에서 로컬 Linux 사용자 이름 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="d822b-229">JupyterHub에 대한 모든 구성 파일은 **/etc/jupyterhub**디렉터리에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="d822b-230">여러 개의 샘플 전자 필기장 hello VM에 이미 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="d822b-231">Hello 참조 [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) 샘플 Python 전자 필기장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="d822b-232">샘플 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 노트북에 대한 내용은 **IntroTutorialinR** 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d822b-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="d822b-233">Hello 참조 [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) 다른 샘플 **Python** 노트북 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-234">Julia 언어 hello hello Linux 데이터 과학 VM에 hello 명령줄에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="d822b-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="d822b-235">Rattle</span></span>
<span data-ttu-id="d822b-236">[래 틀](https://cran.r-project.org/web/packages/rattle/index.html) (tooLearn R 분석 도구를 쉽게 hello)는 데이터 마이닝을 위한 그래픽 R 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="d822b-237">에 쉽게 tooload 있게 해 주는 직관적인 인터페이스가, 탐색 및 데이터를 변환 하 고 빌드 및 모델 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="d822b-238">hello 문서 [래 틀: A R에 대 한 데이터 마이닝 GUI](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) 해당 기능을 보여 주는 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="d822b-239">설치 하 고 다음 명령을 hello로 래 틀을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="d822b-240">설치는 DSVM hello에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="d822b-241">하지만 래 틀 묻는 메시지를 tooinstall 추가 패키지를 로드할 때.</span><span class="sxs-lookup"><span data-stu-id="d822b-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="d822b-242">Rattle은 탭 기반 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="d822b-243">Toosteps hello에 해당 하는 대부분의 hello 탭 [데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)와 같은 데이터를 로드 하거나 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="d822b-244">hello 데이터 과학 프로세스에서 왼쪽된 tooright hello 탭을 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="d822b-245">하지만 hello 마지막 탭 래 틀 여를 실행 하는 hello R 명령에 대 한 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="d822b-246">tooload hello 데이터 집합을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="d822b-247">tooload hello 파일, 선택 hello **데이터** 탭 한 다음</span><span class="sxs-lookup"><span data-stu-id="d822b-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="d822b-248">너무 hello 선택기를 다음 선택**Filename** 선택 **spambaseHeaders.data**합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="d822b-249">tooload hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-249">tooload hello file.</span></span> <span data-ttu-id="d822b-250">선택 **Execute** hello 단추의 맨 위 행에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="d822b-251">각 열에 입력, 대상 또는 다른 유형의 변수, 고유 값 수가 hello 여부의 확인 된 데이터 형식 등의 요약이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="d822b-252">래 틀에서 hello 제대로 식별 **스팸** hello 대상으로 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="d822b-253">선택 hello 스팸 열에 있으면 집합 hello **대상 데이터 형식** 너무**Categoric**합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="d822b-254">tooexplore hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="d822b-254">tooexplore hello data:</span></span>

* <span data-ttu-id="d822b-255">선택 hello **탐색** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="d822b-256">클릭 **요약**, 다음 **Execute**, toosee hello 변수 형식 및 일부 요약 통계에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="d822b-257">tooview 같은 기타 옵션을 선택 하는 다른 유형의 각 변수에 대 한 통계 **Describe** 또는 **기본 사항**합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="d822b-258">hello **탐색** 탭도 있습니다 toogenerate 통찰력 많은 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="d822b-259">tooplot hello 데이터의 막대 그래프.</span><span class="sxs-lookup"><span data-stu-id="d822b-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="d822b-260">**배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-260">Select **Distributions**.</span></span>
* <span data-ttu-id="d822b-261">**word_freq_remove** 및 **word_freq_you**에 대해 **히스토그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="d822b-262">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-262">Select **Execute**.</span></span> <span data-ttu-id="d822b-263">두 밀도 "제거" 보다 전자 메일에 훨씬 더 자주 나타나는 "있습니다" hello 단어 선택을 취소 하는 단일 그래프 창에 표시 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="d822b-264">hello 상관 관계 플롯 흥미로운도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="d822b-265">toocreate 하나:</span><span class="sxs-lookup"><span data-stu-id="d822b-265">toocreate one:</span></span>

* <span data-ttu-id="d822b-266">선택 **상관 관계** hello로 **형식**, 한 다음</span><span class="sxs-lookup"><span data-stu-id="d822b-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="d822b-267">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-267">Select **Execute**.</span></span>
* <span data-ttu-id="d822b-268">권장 최대 변수는 40개라는 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="d822b-269">선택 **예** tooview hello 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="d822b-270">시작 하는 몇 가지 흥미로운 상관 관계는: "기술" 강한 상관 관계가 너무 "HP" 및 "랩" 예.</span><span class="sxs-lookup"><span data-stu-id="d822b-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="d822b-271">또한 강력한 상관 관계가 있다는 너무 "650", hello dataset 기부자 hello 지역 번호 650 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="d822b-272">단어 사이의 hello 상관 관계에 대 한 hello 숫자 값은 hello 탐색 창에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="d822b-273">예를 들어, "사용자"와 "기술" 연관 부정적인 되어 toonote 흥미롭고 "money" 이며</span><span class="sxs-lookup"><span data-stu-id="d822b-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="d822b-274">래 틀 hello dataset toohandle 몇 가지 일반적인 문제를 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="d822b-275">예를 들어, 있습니다 toorescale 기능, 누락 된 값으로 돌립니다, 그리고 이상 값 처리 및 변수 또는 관찰 누락 된 데이터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="d822b-276">Rattle은 관찰 및/또는 변수 간의 연결 규칙을 식별할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="d822b-277">이러한 탭은 이 소개용 연습에 대한 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="d822b-278">Rattle은 클러스터 분석을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="d822b-279">일부 기능 toomake hello 출력 쉽게 tooread를 제외 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="d822b-280">Hello에 **데이터** 탭에서 선택 **무시** hello 변수 이러한 10 개의 항목 제외 하 고 다음 tooeach:</span><span class="sxs-lookup"><span data-stu-id="d822b-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="d822b-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="d822b-281">word_freq_hp</span></span>
* <span data-ttu-id="d822b-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="d822b-282">word_freq_technology</span></span>
* <span data-ttu-id="d822b-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="d822b-283">word_freq_george</span></span>
* <span data-ttu-id="d822b-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="d822b-284">word_freq_remove</span></span>
* <span data-ttu-id="d822b-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="d822b-285">word_freq_your</span></span>
* <span data-ttu-id="d822b-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="d822b-286">word_freq_dollar</span></span>
* <span data-ttu-id="d822b-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="d822b-287">word_freq_money</span></span>
* <span data-ttu-id="d822b-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="d822b-288">capital_run_length_longest</span></span>
* <span data-ttu-id="d822b-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="d822b-289">word_freq_business</span></span>
* <span data-ttu-id="d822b-290">spam</span><span class="sxs-lookup"><span data-stu-id="d822b-290">spam</span></span>

<span data-ttu-id="d822b-291">이동 하 여 다시 toohello **클러스터** 탭에서 선택 **KMeans**, 및 집합 hello *클러스터 수* too4 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="d822b-292">그런 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-292">Then **Execute**.</span></span> <span data-ttu-id="d822b-293">hello 결과 hello 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="d822b-294">한 클러스터가 "george" 및 "hp"의 빈도가 높고 아마도 합법적인 비즈니스 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="d822b-295">toobuild 간단한 의사 결정 트리 기계 학습 모델:</span><span class="sxs-lookup"><span data-stu-id="d822b-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="d822b-296">선택 hello **모델** 탭</span><span class="sxs-lookup"><span data-stu-id="d822b-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="d822b-297">선택 **트리** hello로 **형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="d822b-298">선택 **Execute** hello에 대 한 텍스트 형태로 toodisplay hello 트리 출력 창.</span><span class="sxs-lookup"><span data-stu-id="d822b-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="d822b-299">선택 hello **그리기** 단추 tooview 그래픽 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="d822b-300">이러한 사용 하 여 이전을 얻 었 toohello 트리를 매우 유사 하 게 *rpart*합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="d822b-301">Hello 래 틀의 훌륭한 기능 중 하나는 해당 기능 toorun 여러 기계 학습 방법 및 신속 하 게 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="d822b-302">Hello 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-302">Here is hello procedure:</span></span>

* <span data-ttu-id="d822b-303">선택 **모든** hello에 대 한 **형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="d822b-304">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-304">Select **Execute**.</span></span>
* <span data-ttu-id="d822b-305">완료 된 후 클릭할 수 있는 단일 **형식**처럼 **SVM**, hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="d822b-306">Hello를 사용 하 여 설정 하는 hello 유효성 검사에 hello 모델의 hello 성능을 비교할 수도 있습니다 **평가** 탭 합니다. 예를 들어 hello **오류 매트릭스** 선택 보면 hello 혼동 행렬, 전체 오류 및 각 모델에 대 한 평균된 클래스 오류 hello 유효성 검사 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="d822b-307">또한 ROC 곡선을 그림으로 나타내고, 민감도 분석을 수행하고, 다른 유형의 모델 평가를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="d822b-308">모델 작성 작업을 완료 되 면 선택 hello **로그** 세션 동안 래 틀에서 실행 한 tooview hello R 코드를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="d822b-309">Hello를 선택할 수 있습니다 **내보내기** 단추 toosave 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="d822b-310">현재 릴리스의 Rattle에 버그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="d822b-311">toomodify 스크립트 hello 또는 toorepeat 사용할 단계를 앞에 # 문자를 삽입 해야 하는 나중 *...이 로그 내보내기 * hello 로그 hello 텍스트에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="d822b-312">PostgreSQL 및 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="d822b-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="d822b-313">hello DSVM 설치 PostgreSQL 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="d822b-314">PostgreSQL은 정교한 오픈 소스 관계형 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="d822b-315">이 섹션에서는 어떻게 tooload 우리의 PostgreSQL에 데이터 집합을 스팸 및 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="d822b-316">Hello 데이터를 로드할 수 있습니다, 전에 hello localhost에서 tooallow 암호 인증을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="d822b-317">명령 프롬프트에서:</span><span class="sxs-lookup"><span data-stu-id="d822b-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="d822b-318">Hello 구성 파일의 hello 아래 근처는 연결을 허용 하는 hello에 자세히 설명 하는 여러 줄:</span><span class="sxs-lookup"><span data-stu-id="d822b-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="d822b-319">사용자 이름 및 암호를 사용 하 여 로그인 할 수 있도록 hello "로컬 연결 IPv4" 줄 toouse md5 ident, 대신 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="d822b-320">고 hello postgres 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="d822b-321">toolaunch psql, PostgreSQL hello 기본 제공 postgres 사용자로는 대화형 터미널 hello 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="d822b-322">새 사용자 계정 만들기, 사용 하 여 hello Linux 계정 이름으로 현재 로그온에 따라 동일한 사용자 이름 hello 및 암호 제공:</span><span class="sxs-lookup"><span data-stu-id="d822b-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="d822b-323">그런 다음 사용자로 toopsql 로그인:</span><span class="sxs-lookup"><span data-stu-id="d822b-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="d822b-324">하 여 새 데이터베이스로 hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="d822b-325">이제 hello 데이터를 탐색 하 고 사용 하 여 일부 쿼리를 실행 하겠습니다 **스 쿼 럴 SQL**, JDBC 드라이버를 통해 데이터베이스와 상호 작용할 수 있게 하는 그래픽 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="d822b-326">tooget 시작, 스 쿼 럴 SQL hello 응용 프로그램 메뉴에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="d822b-327">tooset hello 드라이버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-327">tooset up hello driver:</span></span>

* <span data-ttu-id="d822b-328">**Windows**를 선택한 다음 **드라이버 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="d822b-329">**PostgreSQL**을 마우스 오른쪽 단추로 클릭하고 **드라이버 수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="d822b-330">**추가 클래스 경로**를 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="d822b-331">입력 ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello에 대 한 **파일 이름** 및</span><span class="sxs-lookup"><span data-stu-id="d822b-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="d822b-332">**열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-332">Select **Open**.</span></span>
* <span data-ttu-id="d822b-333">드라이버 목록을 선택한 다음 **클래스 이름**에서 **org.postgresql.Driver**를 선택하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="d822b-334">hello 연결 toohello 로컬 서버를 tooset:</span><span class="sxs-lookup"><span data-stu-id="d822b-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="d822b-335">**Windows**를 선택한 다음 **별칭 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="d822b-336">Hello 선택  **+**  단추 toomake 새 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="d822b-337">이름을 *스팸 데이터베이스*, 선택 **PostgreSQL** hello에 **드라이버** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="d822b-338">너무 hello URL 설정*jdbc:postgresql://localhost/spam*합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="d822b-339">*사용자 이름* 및 *암호*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="d822b-340">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-340">Click **OK**.</span></span>
* <span data-ttu-id="d822b-341">tooopen hello **연결** 창의 hello를 두 번 클릭 ***스팸 데이터베이스*** 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="d822b-342">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-342">Select **Connect**.</span></span>

<span data-ttu-id="d822b-343">toorun 일부 쿼리:</span><span class="sxs-lookup"><span data-stu-id="d822b-343">toorun some queries:</span></span>

* <span data-ttu-id="d822b-344">선택 hello **SQL** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="d822b-345">단순 쿼리를 같은 입력 `SELECT * from data;` hello SQL 탭의 hello 위쪽 hello 쿼리 텍스트 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="d822b-346">키를 눌러 **Ctrl + Enter** toorun 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="d822b-347">기본적으로 스 쿼 럴 SQL hello 처음 100 개 행 반환 쿼리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="d822b-348">많은 더 많은 쿼리가이 데이터 tooexplore를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="d822b-349">예를 들어 hello은 어떻게 hello 단어의 주파수 *확인* 스팸과 햄 차이?</span><span class="sxs-lookup"><span data-stu-id="d822b-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="d822b-350">자주 포함 하는 전자 메일의 hello 특징은 무엇 또는 *3d*?</span><span class="sxs-lookup"><span data-stu-id="d822b-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="d822b-351">상위 항목에 있는 대부분의 전자 메일 *3d* 예측 모델 tooclassify hello 전자 메일을 작성 하기 위한 유용한 기능 수 있도록는 스팸 명백 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="d822b-352">PostgreSQL 데이터베이스에 저장 된 데이터 tooperform 기계 학습을 원하는 경우 사용해 볼 [MADlib](http://madlib.incubator.apache.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="d822b-353">SQL Server 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d822b-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="d822b-354">Azure SQL 데이터 웨어하우스는 거대한 양의 관계형 및 비관계형 데이터를 처리할 수 있는 클라우드 기반 규모 확장 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="d822b-355">자세한 내용은 [Azure SQL Data Warehouse란?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="d822b-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="d822b-356">tooconnect toohello 데이터 웨어하우스 및 명령 프롬프트에서 명령이 실행된 hello 다음 hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="d822b-357">그런 다음 프롬프트 hello sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="d822b-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="d822b-358">bcp를 사용하여 데이터 복사:</span><span class="sxs-lookup"><span data-stu-id="d822b-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="d822b-359">hello 다운로드 한 파일의 줄 끝에 hello Windows 스타일 있지만 bcp와 hello-r 플래그는 tootell bcp 하므로 UNIX 스타일을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="d822b-360">sqlcmd를 사용하여 쿼리:</span><span class="sxs-lookup"><span data-stu-id="d822b-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="d822b-361">Squirrel SQL을 사용하여 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="d822b-362">사용 하 여 hello Microsoft MSSQL Server JDBC 드라이버에서 찾을 수 있는 PostgreSQL에 대 한 비슷한 단계에 따라 ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d822b-363">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d822b-363">Next steps</span></span>
<span data-ttu-id="d822b-364">Azure의 hello 데이터 과학 프로세스를 구성 하는 hello 작업을 안내 하는 항목의 개요를 참조 하십시오. [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="d822b-365">특정 시나리오에 대 한 hello 팀 데이터 과학 프로세스의에서 hello 단계를 보여 주는 다른 종단 간 연습에 대 한 참조 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="d822b-366">hello 연습도 방법을 toocombine 클라우드 및 온-프레미스 도구 및 워크플로 또는 파이프라인 toocreate에 서비스는 지능형 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d822b-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
