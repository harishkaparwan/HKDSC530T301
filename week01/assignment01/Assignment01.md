## Title: Assignment 1
## Subtitle: Computer performance, reliability, and scalability calculation
## Author: Harish Kaparwan
## Date: 06/26/2022

---

### 1.2 Assignment

#### a. Data Sizes

| Data Item                                  | Size per Item | Ref  |
|--------------------------------------------|--------------:|------|
| 128 character message.                     | 128 Bytes     |  1   |
| 1024x768 PNG image                         | 1.5 MB        |  2   |
| 1024x768 RAW image                         | 1.31 MB       |  3   |
| HD (1080p) HEVC Video (15 minutes)         | 2.5 GB        |  4   |
| HD (1080p) Uncompressed Video (15 minutes) | 167.96 GB     |  5   |
| 4K UHD HEVC Video (15 minutes)             | 6.08 GB       |  6   |
| 4k UHD Uncompressed Video (15 minutes)     | 671.85 GB     |  7   |
| Human Genome (Uncompressed)                | 1.5 GB        |  8   |

## Solution Reference:

* 1:- 1 byte = 1 character
* 2:- Most PNG images are 16 bits of bit depth, calculation: 1024*768=786432 * 16 Bit = 12582912/8 = 1572864 Bytes/1024 = 1536 KB /1024 = 1.5 MB
* 3:- RAW images are 12-14 Bits of bit depth, calculation: 1024*768=786432 * 14 bit = 11010048/8 = 1376256 Bytes/1024 = 1344.0 KB/1024 = 1.31 MB
* 4, 5, 6, 7:- 
HD (1080p) HEVC Video (15 minutes) : The below calculator used H.264 codec tto calculate size of file but HEVC is 50% better compressor and reduces 50% size of file, so for this video H.264 takes 5.16 GB space so HEVC would take 1/2 size that is 2.5 GB.
https://toolstud.io/video/filesize.php?width=1920&height=1080&framerate=30&timeduration=15&timeduration_unit=minutes&compression=3482&specificbitrate=100&specificbitrate_unit=1000000
and https://www.circlehd.com/blog/how-to-calculate-video-file-size#:~:text=The%20approximate%20size%20of%20each,150MB%20storage%20space%20per%20second.

* 8:- A real human genome is 6.4 billion letters (base pairs) long, one byte is considered to be 8 bits of data, so it would store 4 base pairs per byte, total 1.6 Billion Bytes which is 1.49 GB
and https://www.veritasgenetics.com/our-thinking/whole-story/

#### b. Scaling

|                                           | Size     | # HD | 
|-------------------------------------------|---------:|-----:|
| Daily Twitter Tweets (Uncompressed)       | 60GB     |  1   |
| Daily Twitter Tweets (Snappy Compressed)  | 40GB     |  1   |
| Daily Instagram Photos                    | 107TB    |  32  |
| Daily YouTube Videos                      | 3038TB   | 911  |
| Yearly Twitter Tweets (Uncompressed)      | 21TB     | 7    |
| Yearly Twitter Tweets (Snappy Compressed) | 14TB     | 5    |
| Yearly Instagram Photos                   | 39055TB  |11716 |
| Yearly YouTube Videos                     | 1108870TB|332661|


## Solution:

* Daily Twitter Tweets (Uncompressed): 500 M tweets per day and 1 tweet of size 128 Bytes, Total 64 Billion Bytes, which is ~ 60 GB. HDFS uses 3 copies of each so total Size: 180 GB. HDFS total Capacity is 10 TB, so 1 HD would be more than enough tto store 1 day tweets data.
* Daily Twitter Tweets (Snappy Compressed): Snappy Compression ratio for plain text is 1.5, so total size would be - total size/1.5 = ~ 40 GB. Should easily fit in 1 HD of 10TB.
* Daily Instagram Photos: 75 Million photos uploadaed daily of size 1.5 MB(based on above data size chart), which is 109863 GB ~ 107 TB. Total 322 TB on HDFS (3 copies of each), need 32 HDs each of size 10 TB.
* Daily YouTube Videos: Based on below calculator , 1 hr video file size is 4.32 GB, 500 hr videos per minute, so 2160 GB per minute and youtube need 3110400 GB space per day,~ 3038 TB per day. HDFS need 9113 TB space (3 copies each) so need 911 HDs.
https://toolstud.io/video/filesize.php?width=1920&height=1080&framerate=30&timeduration=1&timeduration_unit=hours&compression=19290&specificbitrate=100&specificbitrate_unit=1000000
* Yearly Twitter Tweets (Uncompressed): Yearly tweets = 500 M * 365 = 185 Billion, ~ 21756 GB ~ 21 TB for 1 year and ~ 64 TB HDFS space to store 3 copies, we need 6-7 HD each of size 10 TB
* Yearly Twitter Tweets (Snappy Compressed):Considering snappy compression ratio = 1.5, total space for 1 year tweets = 21756/1.5 = 14504 GB ~ 14 TB. We need 42 TB HDFS space and 4-5 HD each of size 10 TB
* Yearly Instagram Photos:daily need 107 TB, year = 107*365 = 39055 TB, 
* Yearly YouTube Videos: 3038 TB is daily, yearly = 3038*365 = 1108870 TB, and need 332661 HDs

#### c. Reliability

|                                    | # HD | # Failures |
|------------------------------------|-----:|-----------:|
| Twitter Tweets (Uncompressed)      | 7    |   0.0707   |
| Twitter Tweets (Snappy Compressed) | 5    |   0.0505   |
| Instagram Photos                   |11716 |   118      |
| YouTube Videos                     |332661|   3360     |

## Solution:
The HD annual failure rate = 1.01%

Below formula is used to calculate # HD failures.

#### #HD Failures = Total Yearly HD * Failure Rate

#### d. Latency

|                           | One Way Latency      |
|---------------------------|---------------------:|
| Los Angeles to Amsterdam  | 133.218 ms           |
| Low Earth Orbit Satellite | 40 ms                |
| Geostationary Satellite   | 600 ms               |
| Earth to the Moon         | 1.29 sec             |
| Earth to Mars             | 16 minutes           | 

## Solution:

* 1: https://wondernetwork.com/pings/Amsterdam/Los+Angeles , this website provides ping data in ms, which is one way latency.
* 2: https://www.omniaccess.com/leo/
* 3: https://www.omniaccess.com/leo/
* 4: The moon is at an average distance of 240,000 miles from Earth. Light, traveling at 186,000 miles per second would make a single trip from Earth to the moon in 1.29 seconds.
* 5: https://interimm.org/comms-latency/en/

## END
