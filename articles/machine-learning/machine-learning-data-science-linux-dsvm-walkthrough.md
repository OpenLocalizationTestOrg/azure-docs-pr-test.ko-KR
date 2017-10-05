---
title: "Linux 데이터 과학 가상 컴퓨터의 데이터 과학 | Microsoft Docs"
description: "Linux 데이터 과학 VM을 사용하여 몇 가지 일반적인 데이터 과학 작업을 수행하는 방법입니다."
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
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="b4333-103">Linux 데이터 과학 가상 컴퓨터의 데이터 과학</span><span class="sxs-lookup"><span data-stu-id="b4333-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="b4333-104">이 연습에서는 Linux 데이터 과학 VM을 사용하여 몇 가지 일반 데이터 과학 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="b4333-105">Linux DSVM(데이터 과학 가상 컴퓨터)은 데이터 분석 및 기계 학습에 흔히 사용되는 도구 모음과 함께 미리 설치된, Azure에서 사용 가능한 가상 컴퓨터 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="b4333-106">주요 소프트웨어 구성 요소는 [Linux 데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-linux-dsvm-intro.md) 항목에 항목별로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="b4333-107">VM 이미지를 사용하면 각 도구를 개별적으로 설치하고 구성할 필요 없이 몇 분 내에 데이터 과학 작업을 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="b4333-108">필요한 경우 VM을 쉽게 확장하고 사용하지 않을 때 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="b4333-109">따라서 이 리소스는 탄력적이고 비용 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="b4333-110">이 연습에 설명된 데이터 과학 작업은 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="b4333-111">이 프로세스는 데이터 과학자 팀이 지능적인 응용 프로그램을 빌드하는 전체 수명 주기를 효율적으로 공동 작업할 수 있도록 데이터 과학에 대한 체계적인 접근 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="b4333-112">또한 데이터 과학 프로세스는 개별 사용자가 수행할 수 있는 데이터 과학을 위한 반복되는 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="b4333-113">이 연습에서는 [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 데이터 집합을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="b4333-114">이는 스팸 또는 햄(스팸이 아니라는 의미)으로 표시되는 메일 집합이며 메일의 내용에 대한 일부 통계도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="b4333-115">포함되어 있는 통계는 다음 한 섹션에만 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4333-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b4333-116">Prerequisites</span></span>
<span data-ttu-id="b4333-117">Linux 데이터 과학 가상 컴퓨터를 사용하려면 먼저 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="b4333-118">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b4333-118">An **Azure subscription**.</span></span> <span data-ttu-id="b4333-119">아직 없을 경우 [지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b4333-120">[**Linux 데이터 과학 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="b4333-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="b4333-121">이 VM 프로비전에 대한 자세한 내용은 [Linux 데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-linux-dsvm-intro.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="b4333-122">[X2Go](http://wiki.x2go.org/doku.php) .</span><span class="sxs-lookup"><span data-stu-id="b4333-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="b4333-123">**X2Go 클라이언트**설치 및 구성에 대한 자세한 내용은 [X2Go 클라이언트 설치 및 구성](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="b4333-124">**AzureML 계정**.</span><span class="sxs-lookup"><span data-stu-id="b4333-124">An **AzureML account**.</span></span> <span data-ttu-id="b4333-125">아직 없을 경우 [AzureML 홈 페이지](https://studio.azureml.net/)에서 새 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="b4333-126">시작할 수 있도록 무료 사용 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="b4333-127">spambase 데이터 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="b4333-127">Download the spambase dataset</span></span>
<span data-ttu-id="b4333-128">[spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 데이터 집합은 4601개의 예제만 포함하는 비교적 작은 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="b4333-129">이 데이터 집합은 리소스 요구 사항을 적절하게 유지하도록 하므로 데이터 과학 VM의 몇 가지 주요 기능을 보여 줄 때 사용하기 적합한 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-130">이 연습은 D2 v2 크기의 Linux 데이터 과학 가상 컴퓨터에서 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="b4333-131">이 크기의 DSVM은 이 연습의 절차를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="b4333-132">저장소 공간이 더 필요한 경우 추가 디스크를 만들고 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="b4333-133">이러한 디스크는 영구 Azure Storage를 사용하므로 서버가 크기 조정으로 인해 다시 프로비전되거나 종료되는 경우에도 해당 데이터는 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="b4333-134">디스크를 추가하고 VM에 연결하려면 [Linux VM에 디스크 추가](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b4333-135">이러한 단계는 DSVM에 이미 설치되어 있는 Azure CLI(Azure 명령줄 인터페이스)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="b4333-136">따라서 전적으로 VM 자체에서 이 절차를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="b4333-137">저장소를 늘리는 또 다른 옵션은 [Azure Files](../storage/files/storage-how-to-use-files-linux.md)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="b4333-138">데이터를 다운로드하려면 터미널 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="b4333-139">다운로드한 파일은 머리글 행이 없으므로 머리글이 있는 다른 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="b4333-140">다음 명령을 실행하여 적합한 머리글이 있는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="b4333-141">그런 후 다음 명령을 사용하여 두 개의 파일을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="b4333-142">각 메일의 데이터 집합에는 여러 가지 종류의 통계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="b4333-143">***word\_freq\_WORD***와 같은 열은 메일에서 *WORD*와 일치하는 단어의 백분율을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="b4333-144">예를 들어 *word\_freq\_make*가 1인 경우에는 *make*가 메일에 있는 모든 단어의 1%입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="b4333-145">***char\_freq\_CHAR***과 같은 열은 메일에 있는 모든 문자 중 *CHAR* 문자의 백분율을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="b4333-146">***capital\_run\_length\_longest***는 대문자 시퀀스의 가장 긴 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="b4333-147">***capital\_run\_length\_average***는 모든 대문자 시퀀스의 평균 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="b4333-148">***capital\_run\_length\_total***는 모든 대문자 시퀀스의 총 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="b4333-149">***spam*** 은 메일이 스팸으로 간주되는지 여부를 나타냅니다(1 = 스팸, 0 = 스팸이 아님).</span><span class="sxs-lookup"><span data-stu-id="b4333-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="b4333-150">Microsoft R Open을 사용하여 데이터 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="b4333-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="b4333-151">R을 사용하여 데이터를 검사하고 몇 가지 기본 Machine Learning을 수행해 보겠습니다. 데이터 과학 VM은 [Microsoft R Open](https://mran.revolutionanalytics.com/open/)이 미리 설치된 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="b4333-152">이 R 버전의 다중 스레드 수학 라이브러리는 다양한 단일 스레드 버전보다 더 나은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="b4333-153">Microsoft R Open은 CRAN 패키지 리포지토리의 스냅숏을 사용하여 재현 가능성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="b4333-154">이 연습에서 사용하는 코드 샘플의 복사본을 얻으려면 git를 사용하여 VM에 미리 설치된 **Azure-Machine-Learning-Data-Science** 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="b4333-155">Git 명령줄 도구에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="b4333-156">터미널 창을 열고 R 대화형 콘솔을 통해 새 R 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-157">다음 절차에 RStudio를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="b4333-158">RStudio를 설치하려면 터미널에서 다음 명령을 실행합니다. `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="b4333-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="b4333-159">데이터를 가져오고 환경을 설정하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="b4333-160">각 열에 대한 요약 통계를 보려면</span><span class="sxs-lookup"><span data-stu-id="b4333-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="b4333-161">데이터를 다른 보기로 보려면</span><span class="sxs-lookup"><span data-stu-id="b4333-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="b4333-162">이렇게 하면 각 변수 유형과 데이터 집합의 처음 몇 개의 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="b4333-163">*spam* 열은 정수로 읽었지만 실제로는 범주 변수(또는 요소)입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="b4333-164">해당 형식을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="b4333-165">일부 예비 분석을 수행하려면 VM에 이미 설치되어 있는 R에 대한 인기 있는 그래프 작성 라이브러리인 [ggplot2](http://ggplot2.org/) 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="b4333-166">앞에서 표시된 요약 데이터에서 느낌표 문자의 빈도에 대한 요약 통계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="b4333-167">다음 명령을 사용하여 해당 빈도를 도표로 나타내 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b4333-168">0 모음은 도표를 왜곡하기 때문에 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b4333-169">흥미롭게도 1보다 큰 특수한 밀도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="b4333-170">해당 데이터를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b4333-171">스팸과 햄으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="b4333-172">이러한 예제를 통해 다른 열의 비슷한 도표를 작성하여 포함되어 있는 데이터를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="b4333-173">ML 모델 학습 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b4333-173">Train and test an ML model</span></span>
<span data-ttu-id="b4333-174">이제 스팸 또는 햄을 포함하도록 데이터 집합에서 메일을 분류하는 기계 학습 모델을 몇 가지 학습하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="b4333-175">이 섹션에서 의사 결정 트리 모델 및 임의 포리스트 모델을 학습하고 해당 예측의 정확도를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-176">다음 코드에 사용되는 rpart(재귀 분할 및 회귀 트리) 패키지는 이미 데이터 과학 VM에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="b4333-177">먼저 데이터 집합을 학습 및 테스트 집합으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="b4333-178">그런 다음 메일을 분류하는 의사 결정 트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="b4333-179">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="b4333-181">학습 집합에 대해 얼마나 잘 수행하는지를 확인하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="b4333-182">테스트 집합에 대해 얼마나 잘 수행하는지를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="b4333-183">임의 포리스트 모델도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-183">Let's also try a random forest model.</span></span> <span data-ttu-id="b4333-184">임의 포리스트는 다양한 의사 결정 트리를 학습하고 모든 개별 의사 결정 트리의 분류 모드인 클래스를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="b4333-185">학습 데이터 집합에 지나치게 맞추는 의사 결정 트리 모델의 추세를 바로잡음으로써 더 강력한 기계 학습 접근 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="b4333-186">Azure ML에 모델 배포</span><span class="sxs-lookup"><span data-stu-id="b4333-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="b4333-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML)는 예측 분석 모델을 쉽게 빌드하고 배포할 수 있는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="b4333-188">AzureML의 뛰어난 기능 중 하나는 R 함수를 웹 서비스로 게시하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="b4333-189">AzureML R 패키지를 사용하면 DSVM의 R 세션에서 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="b4333-190">이전 섹션의 의사 결정 트리 코드를 배포하려면 Azure Machine Learning Studio에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="b4333-191">로그인할 작업 영역 ID와 권한 부여 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="b4333-192">이러한 값을 찾아 AzureML 변수를 초기화하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="b4333-193">왼쪽 메뉴에서 **설정** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="b4333-194">**작업 영역 ID**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="b4333-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="b4333-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="b4333-196">오버헤드 메뉴에서 **권한 부여 토큰**을 선택하고 **기본 권한 부여 토큰**을 기록해 둡니다.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="b4333-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="b4333-197">**AzureML** 패키지를 로드한 다음 DSVM의 R 세션에서 토큰 및 작업 영역 ID로 변수 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="b4333-198">이 데모를 보다 쉽게 구현할 수 있도록 모델을 단순화해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="b4333-199">의사 결정 트리에서 루트에 가장 가까운 세 개의 변수를 선택하고 이 세 개의 변수를 사용하여 새 트리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="b4333-200">입력으로 기능을 사용하고 예측된 값을 반환 하는 예측 함수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="b4333-201">**publishWebService** 함수를 사용하여 AzureML에 predictSpam 함수를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="b4333-202">이 함수는 **predictSpam** 함수를 가져와서 입력 및 출력이 정의된 **spamWebService**라는 웹 서비스를 만들고 새 끝점에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="b4333-203">다음 명령을 사용하여 API 끝점 및 액세스 키를 포함하여 게시된 웹 서비스의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="b4333-204">테스트 집합의 처음 10개의 행에 대해 작업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="b4333-205">사용 가능한 다른 도구 사용</span><span class="sxs-lookup"><span data-stu-id="b4333-205">Use other tools available</span></span>
<span data-ttu-id="b4333-206">나머지 섹션에서는 Linux 데이터 과학 VM에 설치된 일부 도구의 사용 방법을 보여 줍니다. 설명할 도구 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="b4333-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="b4333-207">XGBoost</span></span>
* <span data-ttu-id="b4333-208">Python</span><span class="sxs-lookup"><span data-stu-id="b4333-208">Python</span></span>
* <span data-ttu-id="b4333-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="b4333-209">Jupyterhub</span></span>
* <span data-ttu-id="b4333-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="b4333-210">Rattle</span></span>
* <span data-ttu-id="b4333-211">PostgreSQL 및 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="b4333-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="b4333-212">SQL Server 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="b4333-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="b4333-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="b4333-213">XGBoost</span></span>
<span data-ttu-id="b4333-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) 는 빠르고 정확하게 향상된 트리 구현을 제공하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="b4333-215">XGBoost는 python 또는 명령줄에서 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="b4333-216">Python</span><span class="sxs-lookup"><span data-stu-id="b4333-216">Python</span></span>
<span data-ttu-id="b4333-217">Python을 사용하여 개발하는 경우를 위해 Anaconda Python 배포 2.7 및 3.5가 DSVM에 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-218">Anaconda 배포에는 다른 버전 및/또는 패키지가 설치된 Python용 사용자 지정 환경을 만드는 데 사용할 수 있는 [Condas](http://conda.pydata.org/docs/index.html)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="b4333-219">spambase 데이터 집합의 일부를 읽고 scikit-learn에서 벡터 컴퓨터를 지원하는 메일을 분류해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="b4333-220">예측하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="b4333-221">AzureML 끝점을 게시하는 방법을 보여 주기 위해 이전에 R 모델을 게시할 때처럼 3개의 변수를 사용하여 더 간단한 모델을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="b4333-222">AzureML에 모델을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="b4333-223">이 작업은 python 2.7에만 사용할 수 있으며 3.5에는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="b4333-224">**/anaconda/bin/python2.7**을 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="b4333-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="b4333-225">Jupyterhub</span></span>
<span data-ttu-id="b4333-226">DSVM에서 Anaconda 배포에는 Jupyter 노트북, Python R을 공유하는 플랫폼 간 환경 또는 Julia 코드 및 분석이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="b4333-227">JupyterHub을 통해 Jupyter Notebook에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="b4333-228">***https://\<VM DNS 이름 또는 IP 주소\>:8000/***에서 로컬 Linux 사용자 이름 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="b4333-229">JupyterHub에 대한 모든 구성 파일은 **/etc/jupyterhub**디렉터리에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="b4333-230">몇 가지 샘플 노트북이 VM에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="b4333-231">샘플 Python 노트북에 대한 내용은 [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="b4333-232">샘플 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 노트북에 대한 내용은 **IntroTutorialinR** 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="b4333-233">다른 샘플 [Python](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) 노트북에 대한 내용은 **IrisClassifierPyMLWebService** 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-234">Julia 언어는 Linux 데이터 과학 VM의 명령줄에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="b4333-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="b4333-235">Rattle</span></span>
<span data-ttu-id="b4333-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R Analytical Tool To Learn Easily)은 데이터 마이닝을 위한 그래픽 R 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="b4333-237">손쉽게 데이터를 로드, 탐색 및 변환하고 모델을 빌드 및 평가할 수 있는 직관적인 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="b4333-238">문서 [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) (Rattle: R에 대한 데이터 마이닝 GUI)은 해당 기능을 보여 주는 연습을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="b4333-239">다음 명령을 사용하여 Rattle을 설치하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="b4333-240">DSVM에는 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="b4333-241">하지만 Rattle을 로드할 때 추가 패키지를 설치하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="b4333-242">Rattle은 탭 기반 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="b4333-243">대부분의 탭은 데이터를 로드하거나 탐색하는 등 [데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)의 단계에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="b4333-244">데이터 과학 프로세스는 탭을 통해 왼쪽에서 오른쪽으로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="b4333-245">하지만 마지막 탭에는 Rattle에서 실행하는 R 명령의 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="b4333-246">데이터 집합을 로드하고 구성하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="b4333-247">파일을 로드하려면 **데이터** 탭을 선택한 다음</span><span class="sxs-lookup"><span data-stu-id="b4333-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="b4333-248">**파일 이름** 옆에 있는 선택기를 선택하고 **spambaseHeaders.data**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="b4333-249">파일을 로드하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-249">To load the file.</span></span> <span data-ttu-id="b4333-250">단추의 맨 위 행에 있는 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="b4333-251">입력, 대상 또는 다른 유형의 변수인지 고유한 값의 수인지 식별된 데이터 형식을 포함하여 각 열에 대한 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="b4333-252">Rattle은 **spam** 열을 대상으로 제대로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="b4333-253">spam 열을 선택한 다음 **대상 데이터 형식**을 **범주**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="b4333-254">데이터를 탐색하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-254">To explore the data:</span></span>

* <span data-ttu-id="b4333-255">**탐색** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="b4333-256">**요약**을 클릭한 다음 **실행**을 클릭하면 변수 형식에 대한 일부 정보 및 일부 요약 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="b4333-257">각 변수에 대한 다른 종류의 통계를 보려면 **설명** 또는 **기본 사항** 등 다른 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="b4333-258">또한 **탐색** 탭을 사용하여 많은 유용한 도표를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="b4333-259">데이터의 히스토그램을 나타내려면</span><span class="sxs-lookup"><span data-stu-id="b4333-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="b4333-260">**배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-260">Select **Distributions**.</span></span>
* <span data-ttu-id="b4333-261">**word_freq_remove** 및 **word_freq_you**에 대해 **히스토그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="b4333-262">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-262">Select **Execute**.</span></span> <span data-ttu-id="b4333-263">두 밀도 도표가 단일 그래프 창에 표시되고 여기서 단어 "you"가 "remove"보다 메일에 훨씬 더 자주 나오는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="b4333-264">상관 관계 도표도 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="b4333-265">상관 관계를 만들려면</span><span class="sxs-lookup"><span data-stu-id="b4333-265">To create one:</span></span>

* <span data-ttu-id="b4333-266">**상관 관계**를 **형식**으로 선택한 다음</span><span class="sxs-lookup"><span data-stu-id="b4333-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="b4333-267">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-267">Select **Execute**.</span></span>
* <span data-ttu-id="b4333-268">권장 최대 변수는 40개라는 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="b4333-269">도표를 보려면 **예** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="b4333-270">여기서 몇 가지 흥미로운 상관 관계를 볼 수 있습니다. 예를 들어 "technology"는 "HP" 및 "labs"와 굉장히 상호 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="b4333-271">데이터 집합 기부자의 지역 번호가 650이기 때문에 "650"과도 아주 밀접하게 상호 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="b4333-272">단어 사이의 상관 관계에 대한 숫자 값은 탐색 창에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="b4333-273">예를 들어 "technology"가 "your" 및 "money"와 부정적으로 상호 관련되어 있다는 점도 흥미로운 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="b4333-274">Rattle은 몇 가지 일반적인 문제를 처리하기 위해 데이터 집합을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="b4333-275">예를 들어 기능 크기 재조정, 누락 값 귀속, 이상값 처리 및 데이터가 누락된 관찰이나 변수를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="b4333-276">Rattle은 관찰 및/또는 변수 간의 연결 규칙을 식별할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="b4333-277">이러한 탭은 이 소개용 연습에 대한 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="b4333-278">Rattle은 클러스터 분석을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="b4333-279">출력을 더 쉽게 읽을 수 있도록 일부 기능을 제외하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="b4333-280">**데이터** 탭에서 다음 10개의 항목을 제외하고 각 변수 옆에 있는 **무시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="b4333-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="b4333-281">word_freq_hp</span></span>
* <span data-ttu-id="b4333-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="b4333-282">word_freq_technology</span></span>
* <span data-ttu-id="b4333-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="b4333-283">word_freq_george</span></span>
* <span data-ttu-id="b4333-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="b4333-284">word_freq_remove</span></span>
* <span data-ttu-id="b4333-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="b4333-285">word_freq_your</span></span>
* <span data-ttu-id="b4333-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="b4333-286">word_freq_dollar</span></span>
* <span data-ttu-id="b4333-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="b4333-287">word_freq_money</span></span>
* <span data-ttu-id="b4333-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="b4333-288">capital_run_length_longest</span></span>
* <span data-ttu-id="b4333-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="b4333-289">word_freq_business</span></span>
* <span data-ttu-id="b4333-290">spam</span><span class="sxs-lookup"><span data-stu-id="b4333-290">spam</span></span>

<span data-ttu-id="b4333-291">**클러스터** 탭으로 돌아가서 **KMeans**를 선택하고 *클러스터 수*를 4로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="b4333-292">그런 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-292">Then **Execute**.</span></span> <span data-ttu-id="b4333-293">결과가 출력 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-293">The results are displayed in the output window.</span></span> <span data-ttu-id="b4333-294">한 클러스터가 "george" 및 "hp"의 빈도가 높고 아마도 합법적인 비즈니스 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="b4333-295">간단한 의사 결정 트리 기계 학습 모델을 빌드하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="b4333-296">**모델** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="b4333-297">**트리**를 **형식**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="b4333-298">**실행** 을 선택하여 출력 창에 텍스트 형식으로 트리를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="b4333-299">**그리기** 단추를 선택하여 그래픽 버전을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="b4333-300">이전에 *rpart*를 사용하여 얻은 트리와 아주 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="b4333-301">Rattle의 뛰어난 기능 중 하나는 여러 기계 학습 방법을 실행하고 신속하게 평가하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="b4333-302">절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-302">Here is the procedure:</span></span>

* <span data-ttu-id="b4333-303">**형식**에 **모두**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="b4333-304">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-304">Select **Execute**.</span></span>
* <span data-ttu-id="b4333-305">완료되면 **SVM** 등의 모든 단일 **형식**을 클릭하여 그 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="b4333-306">**평가** 탭을 사용하여 유효성 검사 집합에서 모델의 성능을 비교할 수도 있습니다. 예를 들어 **오류 매트릭스** 를 선택하면 유효성 검사 집합에서 각 모델에 대한 혼동 행렬, 전체 오류 및 평균 클래스 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="b4333-307">또한 ROC 곡선을 그림으로 나타내고, 민감도 분석을 수행하고, 다른 유형의 모델 평가를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="b4333-308">모델 빌드가 완료된 후 **로그** 탭을 선택하면 세션 동안 Rattle에서 실행한 R 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="b4333-309">**내보내기** 단추를 선택하여 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="b4333-310">현재 릴리스의 Rattle에 버그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="b4333-311">스크립트를 수정하거나 나중에 단계를 반복하여 사용하려면 로그 텍스트의 *Export this log ... * 앞에 # 문자를 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="b4333-312">PostgreSQL 및 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="b4333-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="b4333-313">DSVM은 PostgreSQL이 설치된 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="b4333-314">PostgreSQL은 정교한 오픈 소스 관계형 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="b4333-315">이 섹션에서는 PostgreSQL에 스팸 데이터 집합을 로드한 다음 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="b4333-316">데이터를 로드하기 전에 먼저 localhost에서 암호 인증을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="b4333-317">명령 프롬프트에서:</span><span class="sxs-lookup"><span data-stu-id="b4333-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="b4333-318">구성 파일의 아래쪽 몇 줄은 허용되는 연결을 자세히 설명하는 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="b4333-319">ident 대신 md5를 사용하도록 "IPv4 local connections" 줄을 변경하면 사용자 이름 및 암호를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="b4333-320">Postgres 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="b4333-321">PostgreSQL용 대화형 터미널인 psql을 기본 제공 postgres 사용자로 시작하려면 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="b4333-322">현재 로그인한 Linux 계정과 동일한 사용자 이름을 사용하여 새 사용자 계정을 만들고 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="b4333-323">그런 다음 사용자로 psql에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="b4333-324">새 데이터베이스에 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="b4333-325">이제 JDBC 드라이버를 통해 데이터베이스와 상호 작용할 수 있는 그래픽 도구인 **Squirrel SQL**을 사용하여 데이터를 탐색하고 일부 쿼리를 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="b4333-326">시작하려면 응용 프로그램 메뉴에서 Squirrel SQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="b4333-327">드라이버를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-327">To set up the driver:</span></span>

* <span data-ttu-id="b4333-328">**Windows**를 선택한 다음 **드라이버 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="b4333-329">**PostgreSQL**을 마우스 오른쪽 단추로 클릭하고 **드라이버 수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="b4333-330">**추가 클래스 경로**를 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="b4333-331">**파일 이름**에 ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar***을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="b4333-332">**열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-332">Select **Open**.</span></span>
* <span data-ttu-id="b4333-333">드라이버 목록을 선택한 다음 **클래스 이름**에서 **org.postgresql.Driver**를 선택하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="b4333-334">로컬 서버에 연결을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="b4333-335">**Windows**를 선택한 다음 **별칭 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="b4333-336">**+** 단추를 선택하여 새 별칭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="b4333-337">이름을 *스팸 데이터베이스*라고 지정하고 **드라이버** 드롭다운 목록에서 **PostgreSQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="b4333-338">URL을 *jdbc:postgresql://localhost/spam*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="b4333-339">*사용자 이름* 및 *암호*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="b4333-340">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-340">Click **OK**.</span></span>
* <span data-ttu-id="b4333-341">**연결** 창을 열려면 별칭 ***스팸 데이터베이스***를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="b4333-342">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-342">Select **Connect**.</span></span>

<span data-ttu-id="b4333-343">일부 쿼리를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="b4333-343">To run some queries:</span></span>

* <span data-ttu-id="b4333-344">**SQL** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="b4333-345">SQL 탭의 맨 위에 있는 쿼리 텍스트 상자에 `SELECT * from data;` 와 같이 단순한 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="b4333-346">**Ctrl+Enter** 를 눌러 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="b4333-347">기본적으로 Squirrel SQL은 쿼리에서 처음 100개의 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="b4333-348">이 데이터를 탐색하기 위해 실행할 수 있는 훨씬 많은 쿼리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="b4333-349">예를 들어 스팸과 햄 간에 *make* 라는 단어의 빈도가 얼마나 차이가 있을까요?</span><span class="sxs-lookup"><span data-stu-id="b4333-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="b4333-350">또는 *3d*가 자주 포함되는 메일의 특징은 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="b4333-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="b4333-351">*3d* 가 자주 발생하는 대부분의 메일은 명백하게 스팸이므로 메일을 분류하는 예측 모델을 빌드하기 위한 유용한 기능이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="b4333-352">PostgreSQL 데이터베이스에 저장된 데이터를 사용하여 기계 학습을 수행하려는 경우 [MADlib](http://madlib.incubator.apache.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="b4333-353">SQL Server 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="b4333-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="b4333-354">Azure SQL 데이터 웨어하우스는 거대한 양의 관계형 및 비관계형 데이터를 처리할 수 있는 클라우드 기반 규모 확장 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="b4333-355">자세한 내용은 [Azure SQL Data Warehouse란?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="b4333-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="b4333-356">데이터 웨어하우스에 연결하고 테이블을 만들려면 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="b4333-357">그런 다음 sqlcmd 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="b4333-358">bcp를 사용하여 데이터 복사:</span><span class="sxs-lookup"><span data-stu-id="b4333-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="b4333-359">다운로드한 파일의 줄 끝은 Windows 스타일이지만 bcp에는 UNIX 스타일이 필요하므로 -r 플래그를 사용하여 bcp에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="b4333-360">sqlcmd를 사용하여 쿼리:</span><span class="sxs-lookup"><span data-stu-id="b4333-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="b4333-361">Squirrel SQL을 사용하여 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="b4333-362">***/usr/share/java/jdbcdrivers/sqljdbc42.jar***에 있을 수 있는 Microsoft MSSQL Server JDBC 드라이버를 사용하여 PostgreSQL과 비슷한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4333-363">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4333-363">Next steps</span></span>
<span data-ttu-id="b4333-364">Azure에서 데이터 과학 프로세스를 구성하는 작업을 안내하는 항목에 대한 개요는 [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="b4333-365">특정 시나리오에 대한 팀 데이터 과학 프로세스의 단계를 보여 주는 다른 종단 간 연습에 대한 설명은 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4333-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="b4333-366">또한 이 연습에서는 클라우드 및 온-프레미스 도구와 서비스를 워크플로 또는 파이프라인에 결합하여 지능형 응용 프로그램을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b4333-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
