---
title: "Apache Hive 및 Pig를 포함하는 Python UDF - Azure HDInsight | Microsoft Docs"
description: "HDInsight의 Hive 및 Pig에서 Python UDF(사용자 정의 함수)를 사용하는 방법, Azure에서의 Hadoop 기술 스택에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="878c8-103">HDInsight의 Hive 및 Pig에서 Python UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="878c8-104">Azure HDInsight의 Hadoop에서 Apache Hive 및 Pig와 함께 Python UDF(사용자 정의 함수)를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="878c8-105"><a name="python"></a>HDInsight의 Python</span><span class="sxs-lookup"><span data-stu-id="878c8-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="878c8-106">Python2.7은 기본적으로 HDInsight 3.0 이상에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="878c8-107">스트림 처리를 위해 이 버전의 Python에서 Apache Hive를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="878c8-108">스트림 처리는 STDOUT 및 STDIN을 사용하여 Hive와 UDF 간에 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="878c8-109">HDInsight에는 Java로 작성된 Python 구현인 Jython도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="878c8-110">Jython은 Java Virtual Machine에서 직접 실행되며 스트리밍을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="878c8-111">Jython는 Pig와 함께 Python을 사용할 때 권장되는 Python 인터프리터입니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="878c8-112">이 문서의 단계에서는 다음과 같이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="878c8-113">로컬 개발 환경에서 Python 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="878c8-114">로컬 Bash 세션 또는 제공된 PowerShell 스크립트에서 `scp` 명령을 사용하여 스크립트를 HDInsight에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="878c8-115">[Azure Cloud Shell(bash)](https://docs.microsoft.com/azure/cloud-shell/overview) 미리 보기를 사용하여 HDInsight와 작동하려면 다음과 같이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="878c8-116">Cloud Shell 환경 내에서 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="878c8-117">`scp`를 사용하여 Cloud Shell에서 HDInsight로 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="878c8-118">Cloud Shell에서 `ssh`를 사용하여 HDInsight에 연결하고 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="878c8-119"><a name="hivepython"></a>Hive UDF</span><span class="sxs-lookup"><span data-stu-id="878c8-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="878c8-120">Python은 HiveQL `TRANSFORM` 문을 통해 Hive의 UDF로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="878c8-121">예를 들어 다음 HiveQL은 클러스터의 기본 Azure Storage 계정에 저장된 `hiveudf.py` 파일을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="878c8-122">**Linux 기반 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="878c8-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="878c8-123">**Windows 기반 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="878c8-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="878c8-124">Windows 기반 HDInsight 클러스터에서는 `USING` 절에서 python.exe의 전체 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="878c8-125">다음은 이 예제에서 수행하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-125">Here's what this example does:</span></span>

1. <span data-ttu-id="878c8-126">파일의 시작 부분에 있는 `add file` 문이 분산 캐시에 `hiveudf.py` 파일을 추가하므로, 클러스터의 모든 노드에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="878c8-127">`SELECT TRANSFORM ... USING` 문은 `hivesampletable`에서 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="878c8-128">또한 clientid, devicemake 및 devicemodel 값을 `hiveudf.py` 스크립트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="878c8-129">`AS` 절은 `hiveudf.py`에서 반환된 필드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="878c8-130">hiveudf.py 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="878c8-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="878c8-131">개발 환경에서 `hiveudf.py`라는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="878c8-132">이 파일의 내용으로 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-132">Use the following code as the contents of the file:</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="878c8-133">이 스크립트는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="878c8-134">STDIN에서 데이터 줄을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="878c8-135">`string.strip(line, "\n ")`를 사용하여 후행 줄 바꿈 문자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="878c8-136">스트림 처리를 할 때 모든 값과 각 값 사이의 탭 문자가 한 줄에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="878c8-137">따라서 `string.split(line, "\t")` 를 사용하여 각 탭의 입력을 분할하여 필드만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="878c8-138">처리가 완료되면 출력을 단일 행(각 필드 사이에 탭 포함)으로 STDOUT에 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="878c8-139">예: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`</span><span class="sxs-lookup"><span data-stu-id="878c8-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="878c8-140">`while` 루프는 `line`이 읽히지 않을 때까지 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="878c8-141">스크립트 출력은 `devicemake` 및 `devicemodel`의 입력 값과 연결된 값의 해시를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="878c8-142">HDInsight 클러스터에서 이 예제를 실행하는 방법에 대해서는 [예제 실행](#running) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="878c8-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="878c8-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="878c8-144">`GENERATE` 문을 통해 Python 스크립트를 Pig의 UDF로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="878c8-145">Jython 또는 C Python을 사용하여 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="878c8-146">Jython은 JVM에서 실행되고, 기본적으로 Pig에서 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="878c8-147">C Python은 외부 프로세스이므로 JVM에서 Pig의 데이터는 Python 프로세스에서 실행 중인 스크립트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="878c8-148">Python 스크립트의 출력이 Pig로 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="878c8-149">Python 인터프리터를 지정하려면 Python 스크립트를 참조할 때 `register`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="878c8-150">다음 예제에서는 Pig as `myfuncs`를 사용하여 스크립트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="878c8-151">**Jython 사용**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="878c8-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="878c8-152">**C Python 사용**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="878c8-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="878c8-153">Jython을 사용할 경우 pig_jython 파일에 대한 경로는 로컬 경로 또는 WASB:// 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="878c8-154">그러나 C Python을 사용할 경우에는 Pig 작업을 제출하는 데 사용하는 노드의 로컬 파일 시스템에 있는 파일을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="878c8-155">등록하기 전이라면 두 경우에 대한 이 예제의 Pig Latin은 다음과 같이 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="878c8-156">다음은 이 예제에서 수행하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-156">Here's what this example does:</span></span>

1. <span data-ttu-id="878c8-157">첫 번째 줄은 `LOGS`에 `sample.log` 샘플 데이터 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="878c8-158">각 레코드를 `chararray`로도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="878c8-159">다음 줄에서는 모든 Null 값을 필터링하여 `LOG`에 작업 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="878c8-160">그런 다음 `LOG`의 레코드에 대해 반복하고 `GENERATE`를 사용하여 `create_structure` 메서드를 호출합니다. 이 메서드는 `myfuncs`로 로드된 Python/Jython 스크립트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="878c8-161">`LINE`은 현재 레코드를 함수에 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="878c8-162">마지막으로 출력은 `DUMP` 명령을 사용하여 STDOUT로 덤프됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="878c8-163">이 명령은 작업이 완료된 후 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="878c8-164">pigudf.py 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="878c8-164">Create the pigudf.py file</span></span>

<span data-ttu-id="878c8-165">개발 환경에서 `pigudf.py`라는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="878c8-166">이 파일의 내용으로 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="878c8-167">Pig Latin 예제에서는 입력에 대한 일관된 스키마가 없으므로 `LINE` 입력을 chararray로 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="878c8-168">Python 스크립트는 데이터를 출력에 대한 일관된 스키마로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="878c8-169">`@outputSchema` 문은 Pig에 반환되는 데이터의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="878c8-170">이 경우 Pig 데이터 형식은 **데이터 모음**입니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="878c8-171">모음에는 모두 chararray(문자열)인 다음과 같은 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="878c8-172">date - 로그 항목이 생성된 날짜</span><span class="sxs-lookup"><span data-stu-id="878c8-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="878c8-173">time - 로그 항목이 생성된 시간</span><span class="sxs-lookup"><span data-stu-id="878c8-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="878c8-174">classname - 항목이 생성된 클래스 이름</span><span class="sxs-lookup"><span data-stu-id="878c8-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="878c8-175">level - 로그 수준</span><span class="sxs-lookup"><span data-stu-id="878c8-175">level - the log level</span></span>
   * <span data-ttu-id="878c8-176">detail - 로그 항목에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="878c8-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="878c8-177">그런 다음 `def create_structure(input)`가 Pig에서 줄 항목을 전달할 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="878c8-178">예제 데이터인 `sample.log`는 대개 date, time, classname, level 및 detail(반환을 원하는 필드) 스키마를 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="878c8-179">그러나 `*java.lang.Exception*`으로 시작하는 몇 개의 줄이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="878c8-180">이러한 줄은 스키마와 일치하도록 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="878c8-181">`if` 문이 이러한 줄을 확인한 후 `*java.lang.Exception*` 문자열을 끝으로 이동하고, 원하는 출력 스키마에 따라 인라인 데이터를 가져오는 입력 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="878c8-182">그런 다음 `split` 명령을 사용하여 첫 4개 공백 문자에서 데이터를 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="878c8-183">출력은 `date`, `time`, `classname`, `level` 및 `detail`에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="878c8-184">마지막으로 값은 Pig로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="878c8-185">데이터가 Pig로 반환되면 `@outputSchema` 문에 정의된 것과 일관된 스키마를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="878c8-186"><a name="running"></a>예제 업로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="878c8-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="878c8-187">**SSH** 단계는 Linux 기반 HDInsight 클러스터에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="878c8-188">**PowerShell** 단계는 Linux 또는 Windows 기반 HDInsight 클러스터에서 작동하지만 Windows 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="878c8-189">SSH</span><span class="sxs-lookup"><span data-stu-id="878c8-189">SSH</span></span>

<span data-ttu-id="878c8-190">SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="878c8-191">`scp` 를 사용하여 파일을 HDInsight 클러스터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="878c8-192">예를 들어 다음 명령은 **mycluster**라는 클러스터에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="878c8-193">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="878c8-194">SSH 세션에서 이전에 업로드된 python 파일을 클러스터의 WASB 저장소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="878c8-195">파일을 업로드한 후 다음 단계를 사용하여 Hive 및 Pig 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="878c8-196">Hive UDF 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="878c8-197">`hive` 명령을 사용하여 Hive 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="878c8-198">셸이 로드되면 `hive>` 프롬프트가 한 번 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="878c8-199">`hive>` 프롬프트에서 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="878c8-200">마지막 줄을 입력하면 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="878c8-201">작업이 완료되면 다음 예제와 유사한 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="878c8-202">Pig UDF 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="878c8-203">`pig` 명령을 사용하여 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="878c8-204">셸이 로드되면 `grunt>` 프롬프트가 한 번 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="878c8-205">`grunt>` 프롬프트에 다음 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="878c8-206">다음 줄을 입력하면 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="878c8-207">작업이 완료되면 다음 데이터와 유사한 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="878c8-208">`quit`를 사용하여 Grunt 셸을 종료한 후 다음을 사용하여 로컬 파일 시스템에 있는 pigudf.py 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="878c8-209">편집기에서 다음 줄의 시작 부분에 있는 `#` 문자를 제거하여 해당 줄의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="878c8-210">변경했으면 Ctrl+X를 사용하여 편집기를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="878c8-211">Y를 선택한 다음 enter 키를 눌러 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="878c8-212">`pig` 명령을 사용하여 셸을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="878c8-213">`grunt>` 프롬프트에서 다음 문을 사용하여 Jython 인터프리터를 사용하는 Python 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="878c8-214">이 작업이 완료되면 이전에 Jython을 사용하여 스크립트를 실행한 때와 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="878c8-215">PowerShell: 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="878c8-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="878c8-216">PowerShell을 사용하여 HDInsight 서버에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="878c8-217">다음 스크립트를 사용하여 Python 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="878c8-218">이 섹션의 단계에서는 Azure PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="878c8-219">Azure PowerShell 사용에 관한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> <span data-ttu-id="878c8-220">`C:\path\to` 값을 해당 개발 환경의 파일 경로로 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="878c8-221">이 스크립트는 HDInsight 클러스터의 정보를 검색한 후 계정 및 기본 저장소 계정의 키를 추출하고 컨테이너의 루트에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="878c8-222">파일 업로드에 대한 자세한 내용은 [HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="878c8-223">PowerShell: Hive UDF 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="878c8-224">PowerShell을 사용하여 Hive 쿼리를 원격으로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="878c8-225">다음 PowerShell 스크립트를 사용하여 **hiveudf.py** 스크립트를 사용하는 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="878c8-226">실행하기 전에 스크립트에서 HDInsight 클러스터의 HTTPs/관리자 계정 정보를 입력하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="878c8-227">**Hive** 작업의 출력은 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="878c8-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="878c8-228">Pig (Jython)</span></span>

<span data-ttu-id="878c8-229">PowerShell을 사용하여 Pig Latin 작업을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="878c8-230">**pigudf.py** 스크립트를 사용하는 Pig Latin 작업을 실행하려면 다음 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="878c8-231">PowerShell을 사용하는 작업을 원격으로 제출하는 경우 C Python을 인터프리터로사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="878c8-232">**Pig** 작업의 출력은 다음 데이터와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="878c8-233"><a name="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="878c8-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="878c8-234">작업 실행 중 오류 발생</span><span class="sxs-lookup"><span data-stu-id="878c8-234">Errors when running jobs</span></span>

<span data-ttu-id="878c8-235">하이브 작업 실행 중 다음 텍스트와 유사한 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="878c8-236">이 문제는 Python 파일의 줄 끝 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="878c8-237">많은 Windows 편집기에서는 기본적으로 CRLF를 줄 끝으로 사용하지만 Linux 응용 프로그램에서는 보통 LF를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="878c8-238">파일을 HDInsight로 업로드하기 전에 CR 문자를 제거하기 위해 다음 PowerShell 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="878c8-239">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="878c8-239">PowerShell scripts</span></span>

<span data-ttu-id="878c8-240">이 예제를 실행하는 데 사용된 두 가지 예제 PowerShell 스크립트는 작업의 오류 출력을 표시하는 주석 처리된 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="878c8-241">작업의 필요한 출력이 표시되지 않으면 다음 줄의 주석 처리를 제거하고 오류 정보가 문제를 나타내는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="878c8-242">오류 정보(STDERR) 및 작업의 결과(STDOUT)도 HDInsight 저장소에 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="878c8-243">이 작업의 경우</span><span class="sxs-lookup"><span data-stu-id="878c8-243">For this job...</span></span> | <span data-ttu-id="878c8-244">Blob 컨테이너에서 이러한 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="878c8-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="878c8-245">Hive</span><span class="sxs-lookup"><span data-stu-id="878c8-245">Hive</span></span> |<span data-ttu-id="878c8-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="878c8-246">/HivePython/stderr</span></span><p><span data-ttu-id="878c8-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="878c8-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="878c8-248">Pig</span><span class="sxs-lookup"><span data-stu-id="878c8-248">Pig</span></span> |<span data-ttu-id="878c8-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="878c8-249">/PigPython/stderr</span></span><p><span data-ttu-id="878c8-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="878c8-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="878c8-251"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="878c8-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="878c8-252">기본적으로 제공되지 않는 Python 모듈을 로드해야 하는 경우 [Azure HDInsight에 모듈을 배포하는 방법](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="878c8-253">Pig 및 Hive를 사용하고 MapReduce 사용에 대해 배우는 다른 방법은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="878c8-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="878c8-254">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="878c8-255">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="878c8-256">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="878c8-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
