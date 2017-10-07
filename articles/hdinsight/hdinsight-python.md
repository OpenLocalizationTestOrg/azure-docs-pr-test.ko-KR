---
title: "Apache Hive 및 Pig-Azure HDInsight UDF aaaPython | Microsoft Docs"
description: "Azure에서 Python UDF 사용자 정의 함수 ()에서 Hive 및 Pig에서 HDInsight Hadoop 기술 hello toouse 스택 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="59e25-103">HDInsight의 Hive 및 Pig에서 Python UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="59e25-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="59e25-104">어떻게 toouse Python 사용자 정의 알아봅니다 Apache Hive 및 Pig Azure HDInsight의 Hadoop에서 사용 하 여 함수 (UDF).</span><span class="sxs-lookup"><span data-stu-id="59e25-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="59e25-105"><a name="python"></a>HDInsight의 Python</span><span class="sxs-lookup"><span data-stu-id="59e25-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="59e25-106">Python2.7은 기본적으로 HDInsight 3.0 이상에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="59e25-107">스트림 처리를 위해 이 버전의 Python에서 Apache Hive를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="59e25-108">Hive 및 UDF hello 간의 STDOUT 및 STDIN toopass 데이터를 사용 하는 스트림 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="59e25-109">HDInsight에는 Java로 작성된 Python 구현인 Jython도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="59e25-110">Jython은 hello Java 가상 컴퓨터에서 직접 실행 되며 스트리밍을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="59e25-111">Jython는 hello Pig에서 Python 사용 때 Python 인터프리터를 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="59e25-112">이 문서의 단계 hello hello 가정을 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="59e25-113">Hello Python 스크립트에 만들면 로컬 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="59e25-114">Hello 중 하나를 사용 하 여 hello 스크립트 tooHDInsight 업로드 `scp` 명령을 로컬 Bash 세션 또는 hello PowerShell 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="59e25-115">Toouse hello를 원하는 경우 [Azure 클라우드 셸 (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) 해야 합니다 toowork HDInsight와 미리 보기:</span><span class="sxs-lookup"><span data-stu-id="59e25-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="59e25-116">Hello 클라우드 셸 환경 내 hello 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="59e25-117">사용 하 여 `scp` hello에서 tooupload hello 파일 셸 tooHDInsight 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="59e25-118">사용 하 여 `ssh` hello 클라우드 셸 tooconnect tooHDInsight 및 실행된 hello 예제에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="59e25-119"><a name="hivepython"></a>Hive UDF</span><span class="sxs-lookup"><span data-stu-id="59e25-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="59e25-120">Python hello HiveQL 통해 Hive에서 UDF로 사용할 수 있습니다 `TRANSFORM` 문.</span><span class="sxs-lookup"><span data-stu-id="59e25-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="59e25-121">HiveQL를 수행 하는 hello hello를 호출 하는 예를 들어 `hiveudf.py` hello 클러스터에 대 한 hello 기본 Azure 저장소 계정에 저장 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="59e25-122">**Linux 기반 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="59e25-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="59e25-123">**Windows 기반 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="59e25-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="59e25-124">Windows 기반 HDInsight 클러스터에서 hello `USING` hello 전체 경로 toopython.exe 절을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="59e25-125">다음은 이 예제에서 수행하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-125">Here's what this example does:</span></span>

1. <span data-ttu-id="59e25-126">hello `add file` hello 파일의 문 hello 시작 부분에 추가 하는 hello `hiveudf.py` 파일 toohello 분산 캐시를 hello 클러스터의 모든 노드에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="59e25-127">hello `SELECT TRANSFORM ... USING` hello에서 데이터를 선택 하는 문을 `hivesampletable`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="59e25-128">Hello clientid, devicemake, 및 devicemodel 값 toohello도 전달 `hiveudf.py` 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="59e25-129">hello `AS` 절에서 반환 하는 hello 필드 설명 `hiveudf.py`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="59e25-130">Hello hiveudf.py 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="59e25-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="59e25-131">개발 환경에서 `hiveudf.py`라는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="59e25-132">Hello 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="59e25-133">이 스크립트는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="59e25-134">STDIN에서 데이터 줄을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="59e25-135">사용 하 여 hello 후행 줄 바꿈 문자가 제거 됩니다 `string.strip(line, "\n ")`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="59e25-136">스트림 처리를 수행할 때 한 줄 각 값 사이 탭 문자를 사용 하 여 모든 hello 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="59e25-137">따라서 `string.split(line, "\t")` 사용된 toosplit hello 방금 hello 필드를 반환 합니다. 각 탭에 입력 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="59e25-138">처리가 완료 되 면 hello 출력은 각 필드 사이 탭을 한 줄으로 tooSTDOUT 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="59e25-139">예: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="59e25-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="59e25-140">hello `while` 아니요 될 때까지 루프 반복 `line` 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="59e25-141">hello 스크립트 출력은 hello에 대 한 입력된 값의 연결을 `devicemake` 및 `devicemodel`, 되었고 hello의 해시 값을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="59e25-142">참조 [hello 예제 실행](#running) 방법에 대 한 toorun HDInsight 클러스터에서이 예제에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="59e25-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="59e25-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="59e25-144">Python 스크립트 hello 통해 Pig에서 UDF로 사용할 수 있습니다 `GENERATE` 문.</span><span class="sxs-lookup"><span data-stu-id="59e25-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="59e25-145">Jython 또는 C Python 중 하나를 사용 하 여 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="59e25-146">Jython은 hello JVM에서 실행 되며 Pig에서 고유 하 게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="59e25-147">C Python 외부 프로세스를 되므로 hello에 hello 데이터로 Pig JVM 전송 되기 toohello 스크립트 Python 프로세스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="59e25-148">hello Python 스크립트의 출력을 hello Pig로 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="59e25-149">toospecify hello Python 인터프리터를 사용 하 여 `register` hello Python 스크립트를 참조 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="59e25-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="59e25-150">hello 다음 예제에서는 스크립트를 등록으로 Pig `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="59e25-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="59e25-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="59e25-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="59e25-152">**C Python toouse**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="59e25-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59e25-153">로컬 경로 또는 WASB hello toohello pig_jython 파일 경로 가능 Jython를 사용할 때는: / / 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="59e25-154">그러나 C Python을 사용 하는 경우에 toosubmit hello Pig 작업을 사용 하는 hello 노드의 hello 로컬 파일 시스템에 파일을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="59e25-155">이 예제에 대 한 hello Pig 라틴 문자, 등록을 지 나 되 면 둘 다에 대해 동일 hello:</span><span class="sxs-lookup"><span data-stu-id="59e25-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="59e25-156">다음은 이 예제에서 수행하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-156">Here's what this example does:</span></span>

1. <span data-ttu-id="59e25-157">hello 샘플 데이터 파일을 로드 하는 첫 번째 줄 hello `sample.log` 에 `LOGS`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="59e25-158">각 레코드를 `chararray`로도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="59e25-159">hello 다음 줄에 hello 연산의 hello 결과 저장 하는 모든 null 값을 필터링 `LOG`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="59e25-160">Hello 레코드에서 반복 하는 다음으로, `LOG` 사용 하 여 `GENERATE` tooinvoke hello `create_structure` 메서드 hello Python/Jython 스크립트에 포함 된 로드 `myfuncs`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="59e25-161">`LINE`사용 되는 toopass hello 현재 레코드 toohello 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="59e25-162">마지막으로, hello 출력은 hello를 사용 하 여 덤프 tooSTDOUT `DUMP` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="59e25-163">이 명령은 hello 작업이 완료 된 후 hello 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="59e25-164">Hello pigudf.py 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="59e25-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="59e25-165">개발 환경에서 `pigudf.py`라는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="59e25-166">Hello 파일의 내용을 hello로 코드를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-166">Use hello following code as hello contents of hello file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="59e25-167">Hello Pig 라틴 예에서 hello 정의 `LINE` hello 입력에 대 한 일관성 있는 스키마가 없습니다 있기 때문에 입력 한 chararray로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="59e25-168">hello 데이터 출력에 대 한 일관성 있는 스키마로 변환 하는 hello Python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="59e25-169">hello `@outputSchema` 문은 tooPig 반환 되는 hello 데이터의 hello 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="59e25-170">이 경우 Pig 데이터 형식은 **데이터 모음**입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="59e25-171">hello 모음 필드는 모두 chararray (문자열)를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="59e25-172">날짜-hello 날짜 hello 로그 항목 생성</span><span class="sxs-lookup"><span data-stu-id="59e25-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="59e25-173">시간-hello 로그 항목이 생성 된 hello 시간</span><span class="sxs-lookup"><span data-stu-id="59e25-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="59e25-174">응용 프로그램 이름-hello 클래스 이름 hello 항목에 대해 만들어진</span><span class="sxs-lookup"><span data-stu-id="59e25-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="59e25-175">수준-hello 로그 수준</span><span class="sxs-lookup"><span data-stu-id="59e25-175">level - hello log level</span></span>
   * <span data-ttu-id="59e25-176">세부 정보-hello에 대 한 자세한 정보 로그 항목</span><span class="sxs-lookup"><span data-stu-id="59e25-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="59e25-177">다음으로 hello `def create_structure(input)` Pig 품목을 전달 하는 hello 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="59e25-178">예제 데이터의 경우 hello `sample.log`, 주로 toohello 날짜, 시간, classname, 수준, 준수 및 tooreturn 원하는 스키마에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="59e25-179">그러나 `*java.lang.Exception*`으로 시작하는 몇 개의 줄이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="59e25-180">이 줄에는 수정 된 toomatch hello 스키마 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="59e25-181">hello `if` 문은를 검사 한 다음 마사지 hello 입력된 데이터 toomove hello `*java.lang.Exception*` 문자열 toohello 끝나도 hello 데이터와 동일한 줄에 예상된 출력 스키마를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="59e25-182">다음으로 hello `split` 명령 hello 처음 4 개의 공백 문자가에서 사용 되는 toosplit hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="59e25-183">hello 출력에 할당 된 `date`, `time`, `classname`, `level`, 및 `detail`합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="59e25-184">마지막으로, tooPig hello 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="59e25-185">Hello에 정의 된 일관성 있는 스키마가 hello 데이터 tooPig 반환 되 면 `@outputSchema` 문.</span><span class="sxs-lookup"><span data-stu-id="59e25-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="59e25-186"><a name="running"></a>업로드 하 고 hello 예 실행</span><span class="sxs-lookup"><span data-stu-id="59e25-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59e25-187">hello **SSH** 단계는 Linux 기반 HDInsight 클러스터와만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="59e25-188">hello **PowerShell** 단계는 Linux 또는 Windows 기반 HDInsight 클러스터를 사용할 수 없지만 Windows 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="59e25-189">SSH</span><span class="sxs-lookup"><span data-stu-id="59e25-189">SSH</span></span>

<span data-ttu-id="59e25-190">SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59e25-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="59e25-191">사용 하 여 `scp` toocopy hello 파일 tooyour HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="59e25-192">예를 들어 다음 명령을 복사 hello 라는 파일 tooa 클러스터 hello **mycluster**합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="59e25-193">SSH tooconnect toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="59e25-194">Hello SSH 세션에서 hello python 파일은 이전에 업로드 hello 클러스터에 대 한 toohello WASB 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="59e25-195">Hello 파일을 업로드 한 후 사용 하 여 hello 다음 toorun hello Hive 및 Pig 작업 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="59e25-196">Hello 하이브 UDF를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59e25-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="59e25-197">사용 하 여 hello `hive` toostart hello 하이브 셸 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="59e25-198">표시 됩니다는 `hive>` hello 셸 로드 되 면 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="59e25-199">다음 쿼리에서 hello에 hello 입력 `hive>` 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="59e25-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="59e25-200">Hello 마지막 줄을 입력 한 후 hello 작업을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="59e25-201">Hello 작업이 완료 되 면 다음 예제 출력 유사한 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="59e25-202">Hello Pig UDF를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59e25-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="59e25-203">사용 하 여 hello `pig` toostart hello 셸 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="59e25-204">표시는 `grunt>` hello 셸 로드 되 면 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="59e25-205">다음 조건에서 hello hello 입력 `grunt>` 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="59e25-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="59e25-206">Hello 다음 줄을 입력 한 후 hello 작업을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="59e25-207">Hello 작업이 완료 되 면 출력 유사한 toohello를 다음 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="59e25-208">사용 하 여 `quit` tooexit Grunt 셸 hello 및 다음 hello 로컬 파일 시스템에 tooedit hello pigudf.py 파일 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="59e25-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="59e25-209">한 번 hello 편집기에서 hello hello를 제거 하 여 다음 줄을 주석 처리 제거 `#` hello 줄의 시작 부분 hello에서에서 문자:</span><span class="sxs-lookup"><span data-stu-id="59e25-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="59e25-210">Hello 변경 된 내용이 되 면 Ctrl + X tooexit hello 편집기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="59e25-211">Y를 선택한 다음 toosave hello 변경 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="59e25-212">사용 하 여 hello `pig` toostart hello 셸 명령을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="59e25-213">Hello 되 면 `grunt>` hello toorun hello Python 스크립트 hello C Python 인터프리터를 사용 하 여 다음을 사용 하 여, 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="59e25-214">이 작업이 완료 되 면 동일한 출력 hello Jython를 사용 하 여 hello 스크립트를 이전에 실행으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="59e25-215">PowerShell: hello 파일을 업로드</span><span class="sxs-lookup"><span data-stu-id="59e25-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="59e25-216">PowerShell tooupload hello 파일 toohello HDInsight 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="59e25-217">다음 스크립트 tooupload hello Python 파일이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="59e25-218">이 섹션의 단계 hello Azure PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="59e25-219">Azure PowerShell을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
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
> <span data-ttu-id="59e25-220">변경 hello `C:\path\to` 개발 환경에서 toohello 경로 toohello 파일 값입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="59e25-221">이 스크립트 HDInsight 클러스터에 대 한 정보를 검색 한 다음 hello 계정 및 hello 기본 저장소 계정에 대 한 키를 추출 하 고 업로드 hello hello 컨테이너의 toohello 루트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="59e25-222">파일 업로드에 대 한 자세한 내용은 참조 hello [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="59e25-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="59e25-223">PowerShell: hello 하이브 UDF를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="59e25-224">PowerShell을 실행 하는 사용 되는 tooremotely 하이브 쿼리 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="59e25-225">다음 PowerShell 스크립트 toorun 사용 하는 하이브 쿼리를 사용 하 여 hello **hiveudf.py** 스크립트:</span><span class="sxs-lookup"><span data-stu-id="59e25-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59e25-226">를 실행 하기 전에 hello 스크립트가 hello HDInsight 클러스터에 대 한 HTTPs/Admin 계정 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
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
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="59e25-227">hello에 대 한 출력 hello **하이브** 작업에는 다음 예제와 비슷한 toohello 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="59e25-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="59e25-228">Pig (Jython)</span></span>

<span data-ttu-id="59e25-229">PowerShell 사용된 toorun Pig 라틴 작업이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="59e25-230">toorun hello를 사용 하는 Pig 라틴 작업 **pigudf.py** 스크립트, PowerShell 스크립트 뒤 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="59e25-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="59e25-231">PowerShell을 사용 하는 작업을 원격으로 제출할 때 아닙니다 가능한 toouse C Python 인터프리터 hello로.</span><span class="sxs-lookup"><span data-stu-id="59e25-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

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

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="59e25-232">hello에 대 한 출력 hello **Pig** 작업 비슷한 toohello 같은 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="59e25-233"><a name="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="59e25-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="59e25-234">작업 실행 중 오류 발생</span><span class="sxs-lookup"><span data-stu-id="59e25-234">Errors when running jobs</span></span>

<span data-ttu-id="59e25-235">Hello 하이브 작업을 실행할 때 텍스트 다음 오류와 비슷한 toohello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="59e25-236">이 문제는 hello Python 파일의 줄 끝에 hello 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="59e25-237">여러 Windows 편집기를 종료 하는 hello 선으로 toousing CRLF 기본 하지만 Linux 응용 프로그램은 일반적으로 LF을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="59e25-238">Hello PowerShell 문을 tooremove hello CR 문자 hello 파일 tooHDInsight 업로드 하기 전에 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="59e25-239">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="59e25-239">PowerShell scripts</span></span>

<span data-ttu-id="59e25-240">모두 toorun hello 예제 PowerShell 스크립트를 사용 하는 hello 예제 hello 작업에 대 한 오류 출력을 표시 하는 주석 처리 된 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="59e25-241">Hello 작업에 대 한 예상 hello 출력이 표시 되지 않는 경우 주석 처리를 제거 hello 다음 줄을 참조 하는 경우 hello 오류 정보에서 문제가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="59e25-242">hello 오류 (STDERR) 정보와 hello 작업 (STDOUT)의 hello 결과로 로깅된 tooyour HDInsight 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="59e25-243">이 작업의 경우</span><span class="sxs-lookup"><span data-stu-id="59e25-243">For this job...</span></span> | <span data-ttu-id="59e25-244">Hello blob 컨테이너에서 이러한 파일을 확인</span><span class="sxs-lookup"><span data-stu-id="59e25-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="59e25-245">Hive</span><span class="sxs-lookup"><span data-stu-id="59e25-245">Hive</span></span> |<span data-ttu-id="59e25-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="59e25-246">/HivePython/stderr</span></span><p><span data-ttu-id="59e25-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="59e25-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="59e25-248">Pig</span><span class="sxs-lookup"><span data-stu-id="59e25-248">Pig</span></span> |<span data-ttu-id="59e25-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="59e25-249">/PigPython/stderr</span></span><p><span data-ttu-id="59e25-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="59e25-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="59e25-251"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="59e25-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="59e25-252">기본적으로 제공 되지 않습니다 tooload Python 모듈 필요한 경우 참조 [어떻게 toodeploy 모듈 tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="59e25-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="59e25-253">다른 방법으로 toouse Pig, Hive, 및 toolearn MapReduce 사용에 대 한 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="59e25-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="59e25-254">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="59e25-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="59e25-255">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="59e25-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="59e25-256">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="59e25-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
