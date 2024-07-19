# 常用指令表

## Detector 量測

    > ct 
    > ct 10

monitor mode 

    > ct -50000

## 馬達移動

    > umv tth 

## 查詢&設定馬達位置

查詢馬達位置

    > wm phi

設定馬達位置

    > set phi 0

設定馬達位置上下限

    > set_lm phi -30 360

## scan 馬達

dscan : 相對位置

    > dscan tth -1  1               20   1
    > dscan tth -1  1  th -0.5 0.5  20   1

ascan : 絕對位置

    > ascan tth  10 20              200  1.5
    > ascan tth  10 20 th  5   10   200  1.5

mesh : 二維掃描, 絕對位置

    > mesh  phi 10 45  40 chi -30 -45  40  1  

## 常用馬達名稱 List

    tth
    th
    chi
    phi

    phiz 
    ftx
    fty

    farcx 
    farcy

# 倒晶格空間計算系統指令

## 查詢目前晶格常數設定與繞射面位置

    > pa

## 設定晶格常數

    > set_lat 

## 設定主要繞射面位置

    > or0 <H> <K> <L>

    > setor0

## 設定次要繞射面位置

    > or1 <H> <K> <L>

    > setor1
  
## 倒晶格空間計算

    > ca <H> <K> <L>
    > ci <tth> <th> <chi> <phi>

### 設定模式

normal mode

    > unfreeze
    > setmode 0

phi fix mode

    > setmode 3
    > freeze

set sector 

    > setsector 0
    > setsector 4

## 倒晶格空間馬達操作

移動

    > ubr <H> <K> <L>

scan

    > hscan <H start> <H end> <steps> <time>
    > kscan <K start> <K end> <steps> <time>
    > lscan <L start> <L end> <steps> <time>

    > hklscan <H start> <H end> <K start> <K end> <L start> <L end> <steps> <time>

    > hklmesh H <H start> <H end> <H steps> K <K start> <K end> <K steps> <time>
    > hklmesh H <H start> <H end> <H steps> L <L start> <L end> <L steps> <time>

