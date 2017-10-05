---
title: "Azure HDInsight에서 ScaleR 및 SparkR 사용 | Microsoft Docs"
description: "R Server와 HDInsight에서 ScaleR 및 SparkR을 사용합니다."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 29733f6f6b725dd4735219ed221431805558a5e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="5f7ec-103">HDInsight에서 ScaleR과 SparkR 결합</span><span class="sxs-lookup"><span data-stu-id="5f7ec-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="5f7ec-104">이 문서는 **SparkR**과 조인된 항공기 지연 및 날씨에 대한 데이터에서 **ScaleR** 로지스틱 회귀 모델을 사용하여 항공기 도착 지연을 예측하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-104">This article shows how to predict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="5f7ec-105">이 시나리오에서는 분석을 위해 Microsoft R Server와 함께 사용하는 Spark에서 데이터를 조작하기 위한 ScaleR의 기능을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-105">This scenario demonstrates the capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="5f7ec-106">이러한 기술 조합을 통해 분산 처리에서 최신 기능을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-106">The combination of these technologies enables you to apply the latest capabilities in distributed processing.</span></span>

<span data-ttu-id="5f7ec-107">두 패키지 모두 Hadoop의 Spark 실행 엔진에서 실행되지만 각각 고유한 각 Spark 세션이 필요하므로 메모리 내 데이터 공유에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="5f7ec-108">R Server의 향후 버전에서 이 문제를 해결할 때까지는 겹치지 않는 Spark 세션을 유지하고 중간 파일을 통해 데이터를 교환하는 것이 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-108">Until this issue is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and to exchange data through intermediate files.</span></span> <span data-ttu-id="5f7ec-109">아래 지침은 이러한 요구 사항을 간단하게 달성할 수 있음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-109">The instructions here show that these requirements are straightforward to achieve.</span></span>

<span data-ttu-id="5f7ec-110">여기에서는 Marin Inchiosa와 Roni Burd가 Stratata 2016에서 처음으로 발표했고 [R로 확장 가능한 데이터 과학 플랫폼 구축](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio)(영문) 웹 세미나를 통해 공유한 예제를 사용하겠습니다. 이 예제에서는 SparkR을 사용하여 잘 알려져 있는 항공기 도착 지연 데이터 집합을 출도착 공항 날씨 데이터와 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="5f7ec-111">그런 다음, 조인된 데이터는 항공기 도착 지연 예측을 위한 ScaleR 로지스틱 회귀에 대한 입력으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-111">The data joined is then used as input to a ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="5f7ec-112">안내한 코드는 원래 Azure HDInsight 클러스터의 Spark에서 실행 중인 R Server용으로 작성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-112">The code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="5f7ec-113">하지만 하나의 스크립트에서 SparkR과 ScaleR을 혼합하여 사용하는 개념도 온-프레미스 환경의 컨텍스트에서 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-113">But the concept of mixing the use of SparkR and ScaleR in one script is also valid in the context of on-premises environments.</span></span> <span data-ttu-id="5f7ec-114">다음에 나오는 예제에서는 R 및 R Server의 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) 라이브러리에 대한 중간 수준의 지식을 가정하고,</span><span class="sxs-lookup"><span data-stu-id="5f7ec-114">In the following, we presume an intermediate level of knowledge of R and R the [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="5f7ec-115">이 시나리오를 진행하면서 [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html)을 사용하는 방법도 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="the-airline-and-weather-datasets"></a><span data-ttu-id="5f7ec-116">항공사 및 날씨 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="5f7ec-116">The airline and weather datasets</span></span>

<span data-ttu-id="5f7ec-117">**AirOnTime08to12CSV** 항공사의 공용 데이터 집합에는 1987년 10월부터 2012년 12월까지 미국 내 모든 상용 항공편에 대한 항공편 도착 및 출발 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-117">The **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span></span> <span data-ttu-id="5f7ec-118">이는 총 1억 5천만 개의 레코드를 포함하고 있는 큰 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="5f7ec-119">압축을 풀면 4GB에 해당하는 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="5f7ec-120">[미국 정부 아카이브](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)에서 제공되며,</span><span class="sxs-lookup"><span data-stu-id="5f7ec-120">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="5f7ec-121">[Revolution Analytics 데이터 집합 리포지토리](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)에 있는 303개의 별도 월간 CSV 파일 집합을 포함하는 zip 파일(AirOnTimeCSV.zip)로 더 편리하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="5f7ec-122">항공기 지연에 대한 날씨의 영향을 확인하려면 각 공항의 날씨 데이터도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-122">To see the effects of weather on flight delays, we also need the weather data at each of the airports.</span></span> <span data-ttu-id="5f7ec-123">이 데이터는 [National Oceanic and Atmospheric Administration(미국해양대기관리처) 리포지토리](http://www.ncdc.noaa.gov/orders/qclcd/)에서 월별로 원시 형식의 zip 파일로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-123">This data can be downloaded as zip files in raw form, by month, from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="5f7ec-124">이 예제에서는 2007년 5월부터 2012년 12월까지의 날씨 데이터를 가져와서 68개 월별 zip 파일 각각에 포함된 시간별 데이터 파일을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-124">For the purposes of this example, we pull weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span></span> <span data-ttu-id="5f7ec-125">또한 월별 zip 파일에는 기상 관측소 ID(WBAN), 연결된 공항(CallSign) 및 UTC 공항 표준 시간대 오프셋(TimeZone) 사이의 매핑(YYYYMMstation.txt)도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-125">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport that it is associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="5f7ec-126">항공편 지연과 날씨 데이터를 조인할 때 이 모든 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-126">All of this information is needed when joining with the airline delay and weather data.</span></span>

## <a name="setting-up-the-spark-environment"></a><span data-ttu-id="5f7ec-127">Spark 환경 설정</span><span class="sxs-lookup"><span data-stu-id="5f7ec-127">Setting up the Spark environment</span></span>

<span data-ttu-id="5f7ec-128">첫 번째 단계는 Spark 환경을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-128">The first step is to set up the Spark environment.</span></span> <span data-ttu-id="5f7ec-129">먼저 다음과 같이 입력 데이터 디렉터리를 포함하고 있는 디렉터리를 가리키고, Spark 계산 컨텍스트를 만들고, 정보 로깅을 위한 로깅 함수를 콘솔에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-129">We begin by pointing to the directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session to reduce startup times 
#   (remember to stop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="5f7ec-130">다음으로 SparkR을 사용하고 SparkR 세션을 초기화할 수 있도록 "Spark_Home"을 R 패키지의 검색 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-130">Next we add “Spark_Home” to the search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-the-weather-data"></a><span data-ttu-id="5f7ec-131">날씨 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="5f7ec-131">Preparing the weather data</span></span>

<span data-ttu-id="5f7ec-132">날씨 데이터를 준비하려면 모델링에 필요한 열에 하위 집합으로 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-132">To prepare the weather data, we subset it to the columns needed for modeling:</span></span> 

- <span data-ttu-id="5f7ec-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-133">"Visibility"</span></span>
- <span data-ttu-id="5f7ec-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="5f7ec-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="5f7ec-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="5f7ec-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-137">"WindSpeed"</span></span>
- <span data-ttu-id="5f7ec-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="5f7ec-138">"Altimeter"</span></span>

<span data-ttu-id="5f7ec-139">그런 다음 기상 관측소와 연결된 공항 코드를 추가하고 측정값을 현지 시간에서 UTC로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-139">Then we add an airport code associated with the weather station and convert the measurements from local time to UTC.</span></span>

<span data-ttu-id="5f7ec-140">기상 관측소(WBAN) 정보를 공항 코드에 매핑하는 파일을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-140">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span></span> <span data-ttu-id="5f7ec-141">날씨 데이터에 포함된 매핑 파일에서 이 상관 관계를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-141">We could get this correlation from the mapping file included with the weather data.</span></span> <span data-ttu-id="5f7ec-142">날씨 데이터의 *CallSign*(예: LAX) 필드를 항공사 데이터의 *Origin*에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-142">By mapping the *CallSign* (for example, LAX) field in the weather data file to *Origin* in the airline data.</span></span> <span data-ttu-id="5f7ec-143">그러나 *WBAN*을 *AirportID*(예: LAX의 경우 12892)에 매핑하고 “wban-to-airport-id-tz.CSV”라고 하는 CSV 파일로 저장된 *TimeZone*을 포함한 사용 가능한 다른 매핑이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-143">However, we just happened to have another mapping on hand that maps *WBAN* to *AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="5f7ec-144">예:</span><span class="sxs-lookup"><span data-stu-id="5f7ec-144">For example:</span></span>

| <span data-ttu-id="5f7ec-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="5f7ec-145">AirportID</span></span> | <span data-ttu-id="5f7ec-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="5f7ec-146">WBAN</span></span> | <span data-ttu-id="5f7ec-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="5f7ec-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="5f7ec-148">10685</span><span class="sxs-lookup"><span data-stu-id="5f7ec-148">10685</span></span> | <span data-ttu-id="5f7ec-149">54831</span><span class="sxs-lookup"><span data-stu-id="5f7ec-149">54831</span></span> | <span data-ttu-id="5f7ec-150">-6</span><span class="sxs-lookup"><span data-stu-id="5f7ec-150">-6</span></span>
| <span data-ttu-id="5f7ec-151">14871</span><span class="sxs-lookup"><span data-stu-id="5f7ec-151">14871</span></span> | <span data-ttu-id="5f7ec-152">24232</span><span class="sxs-lookup"><span data-stu-id="5f7ec-152">24232</span></span> | <span data-ttu-id="5f7ec-153">-8</span><span class="sxs-lookup"><span data-stu-id="5f7ec-153">-8</span></span>
| <span data-ttu-id="5f7ec-154">..</span><span class="sxs-lookup"><span data-stu-id="5f7ec-154">..</span></span> | <span data-ttu-id="5f7ec-155">..</span><span class="sxs-lookup"><span data-stu-id="5f7ec-155">..</span></span> | <span data-ttu-id="5f7ec-156">..</span><span class="sxs-lookup"><span data-stu-id="5f7ec-156">..</span></span>

<span data-ttu-id="5f7ec-157">다음 코드는 각 시간별 원시 날씨 데이터 파일을 읽어서 필요한 열에 하위 집합으로 넣고 기상 관측소 매핑 파일을 병합한 다음 측정값의 날씨 시간을 UTC로 조정한 후 파일의 새 버전을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-157">The following code reads each of the hourly raw weather data files, subsets to the columns we need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file:</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-the-airline-and-weather-data-to-spark-dataframes"></a><span data-ttu-id="5f7ec-158">Spark DataFrame으로 항공사 및 날씨 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f7ec-158">Importing the airline and weather data to Spark DataFrames</span></span>

<span data-ttu-id="5f7ec-159">이제 SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) 함수를 사용하여 날씨 및 항공사 데이터를 Spark DataFrame으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-159">Now we use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span></span> <span data-ttu-id="5f7ec-160">이 함수는 다른 많은 Spark 메서드와 마찬가지로 느리게 실행됩니다. 즉 실행 큐에 있지만 필요할 때까지는 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for the airline data

logmsg('create a SparkR DataFrame for the airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for the weather data

logmsg('create a SparkR DataFrame for the weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="5f7ec-161">데이터 정리 및 변환</span><span class="sxs-lookup"><span data-stu-id="5f7ec-161">Data cleansing and transformation</span></span>

<span data-ttu-id="5f7ec-162">다음으로, 열 이름을 변경하기 위해 가져온 항공기 데이터에 대한 일부 정리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-162">Next we do some cleanup on the airline data we’ve imported to rename columns.</span></span> <span data-ttu-id="5f7ec-163">필요한 변수만을 유지하며, 출발 시 최신 날짜와 병합할 수 있도록 예정된 출발 시간을 가장 가까운 시간으로 받아 내립니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-163">We only keep the variables needed, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data at departure:</span></span>

```
logmsg('clean the airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from the flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time to full hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="5f7ec-164">이제 날씨 데이터에 대해 다음과 비슷한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-164">Now we perform similar operations on the weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean the weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-the-weather-and-airline-data"></a><span data-ttu-id="5f7ec-165">날씨 및 항공사 데이터 결합</span><span class="sxs-lookup"><span data-stu-id="5f7ec-165">Joining the weather and airline data</span></span>

<span data-ttu-id="5f7ec-166">SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) 함수를 사용하여 출발 AirportID와 날짜/시간을 기준으로 항공사와 날씨 데이터의 왼쪽 외부 조인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-166">We now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="5f7ec-167">외부 조인을 사용하면 일치하는 날씨 데이터가 없는 경우에도 모든 항공사 데이터 레코드를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-167">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="5f7ec-168">조인에 따라 중복 열 몇 개를 제거하고, 유지 열의 이름을 바꿔 조인에서 도입된 들어오는 DataFrame 접두사를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-168">Following the join, we remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="5f7ec-169">비슷한 방식으로 도착 AirportID와 날짜/시간을 기준으로 날씨와 항공사 데이터를 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-169">In a similar fashion, we join the weather and airline data based on arrival AirportID and datetime:</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-to-csv-for-exchange-with-scaler"></a><span data-ttu-id="5f7ec-170">ScaleR과 교환하기 위해 CSV로 결과 저장</span><span class="sxs-lookup"><span data-stu-id="5f7ec-170">Save results to CSV for exchange with ScaleR</span></span>

<span data-ttu-id="5f7ec-171">이것으로 SparkR을 사용하는 데 필요한 조인이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-171">That completes the joins we need to do with SparkR.</span></span> <span data-ttu-id="5f7ec-172">ScaleR에 입력할 수 있도록 최종적인 "joinedDF5" Spark DataFrame의 데이터를 CSV로 저장한 다음 SparkR 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-172">We save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span></span> <span data-ttu-id="5f7ec-173">80개의 개별 파티션에 결과 CSV를 저장하도록 SparkR에 명시적으로 지시하여 ScaleR 처리에서 병렬로 충분하게 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-173">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output the joined data from Spark to CSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result to directory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down the SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-to-xdf-for-use-by-scaler"></a><span data-ttu-id="5f7ec-174">ScaleR에서 사용할 XDF로 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f7ec-174">Import to XDF for use by ScaleR</span></span>

<span data-ttu-id="5f7ec-175">ScaleR 텍스트 데이터 원본을 통해 모델링하기 위해 조인된 항공사 및 날짜 데이터의 CSV 파일을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-175">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="5f7ec-176">하지만 데이터 집합에서 여러 작업 실행 시 더 효율적이므로 먼저 XDF로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-176">But we import it to XDF first, since it is more efficient when running multiple operations on the dataset:</span></span>

```
logmsg('Import the CSV to compressed, binary XDF format') 

# set the Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="5f7ec-177">학습 및 테스트를 위한 데이터 분할</span><span class="sxs-lookup"><span data-stu-id="5f7ec-177">Splitting data for training and test</span></span>

<span data-ttu-id="5f7ec-178">rxDataStep을 사용하여 테스트를 위해 2012년 데이터를 분할하고, 나머지 데이터는 교육을 위해 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-178">We use rxDataStep to split out the 2012 data for testing and keep the rest for training:</span></span>

```
# split out the training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out the testing data

logmsg('split out the test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="5f7ec-179">로지스틱 회귀 모델 학습 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5f7ec-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="5f7ec-180">이제 모델을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-180">Now we are ready to build a model.</span></span> <span data-ttu-id="5f7ec-181">도착 시간 지연에 날짜 데이터가 미치는 영향을 확인하기 위해 ScaleR의 로지스틱 회귀 루틴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-181">To see the influence of weather data on delay in the arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="5f7ec-182">이 루틴을 사용하여 15분 이상의 도착 지연이 출도착 공항의 날씨 영향을 받는지 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-182">We use it to model whether an arrival delay of greater than 15 minutes is influenced by the weather at the departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use the scalable rxLogit() function but set max iterations to 3 for the purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="5f7ec-183">이제 몇 가지 예측을 수행하고 ROC와 AUC를 살펴봄으로써 테스트 데이터에서 수행하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-183">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over the test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use the scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under the Curve (AUC).

logmsg('calculate the roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="5f7ec-184">다른 곳에서 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="5f7ec-184">Scoring elsewhere</span></span>

<span data-ttu-id="5f7ec-185">또한, 다른 플랫폼의 데이터에 점수를 매기기 위해 이 모델을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-185">We can also use the model for scoring data on another platform.</span></span> <span data-ttu-id="5f7ec-186">RDS 파일로 저장한 다음 전송하여 해당 RDS를 SQL Server R 서비스 등의 대상 점수 매기기 환경으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-186">By saving it to an RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="5f7ec-187">모델이 빌드된 요소 수준과 점수를 매길 데이터의 요소 수준이 일치하는지 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-187">It is important to ensure that the factor levels of the data to be scored match those on which the model was built.</span></span> <span data-ttu-id="5f7ec-188">이러한 일치는 ScaleR의 `rxCreateColInfo()` 함수를 통해 모델링 데이터와 관련된 열 정보를 추출하고 저장한 다음, 해당 열 정보를 입력 데이터 원본에 적용하여 예측함으로써 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-188">That match can be achieved by extracting and saving the column infomation associated with the modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information to the input data source for prediction.</span></span> <span data-ttu-id="5f7ec-189">다음 예제에서는 테스트 데이터 집합의 몇 개 행만 저장하고 예측 스크립트에서 이 샘플의 열 정보를 추출하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-189">In the following we save a few rows of the test dataset and extract and use the column information from this sample in the prediction script:</span></span>

```
# save the model and a sample of the test dataset 

logmsg('save serialized version of the model and a sample of the test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop the spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="5f7ec-190">요약</span><span class="sxs-lookup"><span data-stu-id="5f7ec-190">Summary</span></span>

<span data-ttu-id="5f7ec-191">이 문서에서는 Hadoop Spark에서 모델 개발을 위해 ScaleR과 데이터 조작을 위해 SparkR의 사용을 결합하는 것이 어떻게 가능한지 보여주었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-191">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="5f7ec-192">이 시나리오에서는 한 번에 하나의 세션만 실행하면서 별도의 Spark 세션을 유지하고 CSV 파일을 통해 데이터를 교환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="5f7ec-193">SparkR과 ScaleR에서 Spark 세션을 공유하고 이에 따라 Spark DataFrame을 공유할 수 있는 경우 이 프로세스가 간단하지만 예정된 R Server 릴리스에서 훨씬 더 쉽게 수행될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="5f7ec-194">다음 단계 및 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="5f7ec-194">Next steps and more information</span></span>

- <span data-ttu-id="5f7ec-195">Spark에서 R Server 사용에 대한 자세한 내용은 [MSDN의 시작 가이드](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-195">For more information on use of R Server on Spark, see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="5f7ec-196">R Server에 대한 일반 정보는 [R 시작](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-196">For general information on R Server, see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="5f7ec-197">HDInsight의 R Server에 대한 자세한 내용은 [Azure HDInsight의 R Server 개요](hdinsight-hadoop-r-server-overview.md) 및 [Azure HDInsight의 R Server](hdinsight-hadoop-r-server-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="5f7ec-198">SparkR 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f7ec-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="5f7ec-199">Apache SparkR 문서</span><span class="sxs-lookup"><span data-stu-id="5f7ec-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="5f7ec-200">Databricks의 [SparkR 개요](https://docs.databricks.com/spark/latest/sparkr/overview.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="5f7ec-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
