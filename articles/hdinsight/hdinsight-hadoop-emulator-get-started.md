---
title: "Hadoop 샌드박스 사용에 대한 자세한 정보 - 에뮬레이터 - Azure HDInsight | Microsoft Docs"
description: "Hadoop 에코 시스템을 사용하는 방법에 대해 알아보려면 Azure 가상 컴퓨터에서 Hortonworks의 Hadoop 샌드박스를 설정할 수 있습니다. "
keywords: "Hadoop 에뮬레이터, Hadoop 샌드박스"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="04d53-104">가상 컴퓨터의 에뮬레이터인 Hadoop 샌드박스 시작</span><span class="sxs-lookup"><span data-stu-id="04d53-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="04d53-105">Hadoop 에코 시스템에 대해 알아보기 위해 가상 컴퓨터에서 Hortonworks의 Hadoop 샌드박스를 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="04d53-106">이 샌드박스는 Hadoop, HDFS(Hadoop Distributed File System) 및 작업 제출에 대해 알아보는 로컬 개발 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="04d53-107">Hadoop에 익숙해졌으면 HDInsight 클러스터를 만들어 Azure에서 Hadoop 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="04d53-108">시작 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04d53-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04d53-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04d53-109">Prerequisites</span></span>
* <span data-ttu-id="04d53-110">[Oracle VirtualBox](https://www.virtualbox.org/)</span><span class="sxs-lookup"><span data-stu-id="04d53-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="04d53-111">[여기](https://www.virtualbox.org/wiki/Downloads)에서 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="04d53-112">가상 컴퓨터 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="04d53-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="04d53-113">[Hortonworks 다운로드](http://hortonworks.com/downloads/#sandbox)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="04d53-114">**VIRTUALBOX용 다운로드**를 클릭하여 VM 기반 최신 Hortonworks 샌드박스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="04d53-115">다운로드가 시작되기 전에 Hortonworks에 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="04d53-116">네트워크 속도에 따라 다운로드하는 데 1 ~ 2 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![VirtualBox에 대한 Hortonworks Sandbox를 다운로드용 링크 이미지](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="04d53-118">동일한 웹 페이지에서 **Virtual Box에서 가져오기** 링크를 클릭하여 가상 컴퓨터에 대한 설치 지침이 포함된 PDF를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="04d53-119">이전 HDP 버전 샌드박스를 다운로드하려면 보관 저장소를 확장하세요.</span><span class="sxs-lookup"><span data-stu-id="04d53-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Hortonworks 샌드박스 보관](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="04d53-121">가상 컴퓨터 시작합</span><span class="sxs-lookup"><span data-stu-id="04d53-121">Start the virtual machine</span></span>

1. <span data-ttu-id="04d53-122">Open Oracle VM VirtualBox를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="04d53-123">**파일** 메뉴에서 **Import Appliance(어플라이언스 가져오기)**를 클릭한 다음 Hortonworks Sandbox 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="04d53-124">Hortonworks Sandbox를 선택한 다음 **시작**, **일반 시작**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="04d53-125">가상 컴퓨터가 부팅 프로세스를 완료하면 로그인 지침이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![일반 시작](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="04d53-127">웹 브라우저를 열고 표시된 URL로 이동합니다(일반적으로 http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="04d53-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="04d53-128">샌드박스 암호 설정</span><span class="sxs-lookup"><span data-stu-id="04d53-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="04d53-129">Hortonworks Sandbox 페이지의 **시작** 단계에서 **고급 옵션 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="04d53-130">이 페이지의 정보를 사용하여 SSH를 통해 샌드박스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="04d53-131">제공된 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="04d53-132">SSH 클라이언트를 설치하지 않은 경우 **http://localhost:4200/**의 가상 컴퓨터에 제공된 웹 기반 SSH을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="04d53-133">SSH를 통해 처음 연결하는 경우 루트 계정의 암호를 변경하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="04d53-134">새 암호를 입력합니다. 이 암호는 SSH를 사용하여 로그인할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="04d53-135">일단 로그인하면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="04d53-136">대화 상자가 나타나면 Ambari 관리자 계정에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="04d53-137">Ambari 웹 UI에 액세스할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="04d53-138">Hive 명령 사용</span><span class="sxs-lookup"><span data-stu-id="04d53-138">Use Hive commands</span></span>

1. <span data-ttu-id="04d53-139">샌드박스에 대한 SSH 연결에서 다음 명령을 사용하여 Hive 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="04d53-140">셸이 시작되면 다음을 사용하여 샌드박스와 함께 제공되는 테이블을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="04d53-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="04d53-141">다음을 사용하여 `sample_07` 테이블에서 10개의 행을 검색합니다</span><span class="sxs-lookup"><span data-stu-id="04d53-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="04d53-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04d53-142">Next steps</span></span>
* [<span data-ttu-id="04d53-143">Hortonworks Sandbox와 Visual Studio를 사용하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="04d53-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="04d53-144">Hortonworks Sandbox의 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="04d53-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="04d53-145">Hadoop 자습서 - HDP 시작</span><span class="sxs-lookup"><span data-stu-id="04d53-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

