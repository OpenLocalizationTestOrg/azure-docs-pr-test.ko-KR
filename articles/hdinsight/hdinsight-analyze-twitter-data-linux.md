---
title: "Apache Hive로 Twitter 데이터 분석 - Azure HDInsight | Microsoft Docs"
description: "HDInsight에서 Hive 및 Hadoop을 사용하여 원시 TWitter 데이터를 검색 가능한 Hive 테이블로 변환하는 방법을 알아 봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: b8656123fa9c5158f366872ab050f370080ec18a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="ffa5a-103">HDInsight에서 Hive 및 Hadoop을 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="ffa5a-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="ffa5a-104">Apache Hive를 사용하여 Twitter 데이터를 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-104">Learn how to use Apache Hive to process Twitter data.</span></span> <span data-ttu-id="ffa5a-105">결과는 특정 단어가 포함된 많은 트윗을 보낸 Twitter 사용자의 목록이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffa5a-106">이 문서의 단계는 HDInsight 3.6에서 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-106">The steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="ffa5a-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ffa5a-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-the-data"></a><span data-ttu-id="ffa5a-109">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="ffa5a-109">Get the data</span></span>

<span data-ttu-id="ffa5a-110">Twitter를 사용하여 [각 트윗에 대한 데이터](https://dev.twitter.com/docs/platform-objects/tweets) 를 REST API를 통해 JSON(JavaScript Notation) 개체로서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-110">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="ffa5a-111">[OAuth](http://oauth.net) 는 API에 대한 인증을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-111">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="ffa5a-112">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ffa5a-112">Create a Twitter application</span></span>

1. <span data-ttu-id="ffa5a-113">웹 브라우저에서[https://apps.twitter.com/](https://apps.twitter.com/)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-113">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="ffa5a-114">Twitter 계정이 없는 경우 **지금 로그인** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-114">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="ffa5a-115">**Create New App**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="ffa5a-116">**Name**, **Description**, **Website**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="ffa5a-117">**Website** 필드의 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-117">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="ffa5a-118">다음 표는 사용할 샘플 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-118">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="ffa5a-119">필드</span><span class="sxs-lookup"><span data-stu-id="ffa5a-119">Field</span></span> | <span data-ttu-id="ffa5a-120">값</span><span class="sxs-lookup"><span data-stu-id="ffa5a-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="ffa5a-121">이름</span><span class="sxs-lookup"><span data-stu-id="ffa5a-121">Name</span></span> |<span data-ttu-id="ffa5a-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ffa5a-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="ffa5a-123">설명</span><span class="sxs-lookup"><span data-stu-id="ffa5a-123">Description</span></span> |<span data-ttu-id="ffa5a-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ffa5a-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="ffa5a-125">Website</span><span class="sxs-lookup"><span data-stu-id="ffa5a-125">Website</span></span> |<span data-ttu-id="ffa5a-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="ffa5a-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="ffa5a-127">**Yes, I agree**를 선택한 후 **Create your Twitter application**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="ffa5a-128">**Permissions** 탭을 클릭합니다. 기본 권한은 **Read only**입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-128">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="ffa5a-129">**Keys and Access Tokens** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-129">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="ffa5a-130">**Create my access token**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="ffa5a-131">페이지의 오른쪽 위에서 **Test OAuth** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-131">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="ffa5a-132">**consumer key**, **Consumer secret**, **Access token** 및 **Access token secret**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="ffa5a-133">트윗 다운로드</span><span class="sxs-lookup"><span data-stu-id="ffa5a-133">Download tweets</span></span>

<span data-ttu-id="ffa5a-134">다음 Python 코드는 Twitter에서 10,000개의 트윗을 다운로드하고 **tweets.txt**라는 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-134">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="ffa5a-135">다음 단계는 Python이 이미 설치되어 있으므로 HDInsight 클러스터에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-135">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="ffa5a-136">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-136">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ffa5a-137">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="ffa5a-138">다음 명령을 사용하여 [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2) 및 기타 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-138">Use the following commands to install [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="ffa5a-139">다음 명령을 사용하여 **gettweets.py**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-139">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="ffa5a-140">다음 텍스트를 **gettweets.py** 파일의 콘텐츠로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-140">Use the following text as the contents of the **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="ffa5a-141">다음 항목에 대한 자리 표시자 텍스트를 Twitter 응용 프로그램의 정보로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-141">Replace the placeholder text for the following items with the information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="ffa5a-142">**Ctrl + X**, **Y**를 차례로 사용하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-142">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="ffa5a-143">다음 명령을 사용하여 파일을 실행하고 트윗을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-143">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="ffa5a-144">진행률 표시기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-144">A progress indicator appears.</span></span> <span data-ttu-id="ffa5a-145">진행률 표시기는 트윗이 다운로드되면서 100%까지 올라갑니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-145">It counts up to 100% as the tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ffa5a-146">진행률 표시줄이 앞으로 이동하는 데 시간이 오래 걸리는 경우 추세 항목을 추적하는 필터를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-146">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="ffa5a-147">필터에서 항목에 대한 트윗이 많을 경우 필요하면 10,000개의 트윗을 신속하게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-147">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="ffa5a-148">데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="ffa5a-148">Upload the data</span></span>

<span data-ttu-id="ffa5a-149">HDInsight 저장소로 데이터를 복사하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-149">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="ffa5a-150">이러한 명령은 클러스터의 모든 노드에서 액세스할 수 있는 위치에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-150">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="ffa5a-151">HiveQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ffa5a-151">Run the HiveQL job</span></span>

1. <span data-ttu-id="ffa5a-152">다음 명령을 사용하여 HiveQL 문이 포함 된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-152">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="ffa5a-153">다음 텍스트를 파일의 내용으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-153">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="ffa5a-154">**Ctrl + X**, **Y**를 차례로 누르고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-154">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="ffa5a-155">다음 명령을 사용하여 파일에 포함된 HiveQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-155">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="ffa5a-156">이 명령은 **twitter.hql** 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-156">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="ffa5a-157">쿼리가 완료되면 `jdbc:hive2//localhost:10001/>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-157">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="ffa5a-158">Beeline 프롬프트에서 다음 쿼리를 사용하여 데이터를 가져왔는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-158">From the beeline prompt, use the following query to verify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="ffa5a-159">이 쿼리는 메시지 텍스트에 단어 **Azure**를 포함하는 최대 10개의 트윗을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-159">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa5a-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffa5a-160">Next steps</span></span>

<span data-ttu-id="ffa5a-161">비구조적 JSON 데이터 집합을 구조적 Hive 테이블로 변환하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-161">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="ffa5a-162">HDInsight에서 Hive에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-162">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ffa5a-163">HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="ffa5a-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="ffa5a-164">HDInsight를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="ffa5a-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
