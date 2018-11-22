# サーバーのマシンスペックを確認する

## macの場合

 - system_profiler SPHardwareDataType

```bash
$ system_profiler SPHardwareDataType
Hardware:

    Hardware Overview:

      Model Name: MacBook Pro
      Model Identifier: MacBookPro14,3
      Processor Name: Intel Core i7
      Processor Speed: 3.1 GHz
      Number of Processors: 1
      Total Number of Cores: 4
      L2 Cache (per Core): 256 KB
      L3 Cache: 8 MB
      Memory: 16 GB
      Boot ROM Version: XXXXX.XXXX.XXXXXX
      SMC Version (system): y.zzzz
      Serial Number (system): XXXXXXXXXXXXX
      Hardware UUID: XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXX
```

## Linuxの場合

### cpuinfoを確認
- cat /proc/cpuinfo
```bash
$ cat /proc/cpuinfo
processor	: 0 #プロセッサの通し番号
vendor_id	: GenuineIntel #プロセッサを製造したベンダー
cpu family	: 6 #CPUのファミリー番号
model		: 63 #モデル番号
model name	: Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz #プロセッサ名
stepping	: 2 #CPUのステッピングを指す。一般的にはリビジョンのこと
microcode	: 0x36 #マイクロコード。CPUのファームウェアのこと
cpu MHz		: 2400.066 #プロセッサの動作周波数
cache size	: 30720 KB #キャッシュサイズ
physical id	: 0 #物理プロセッサID
siblings	: 1 #物理プロセッサに相乗りしているコア数
core id		: 0 #物理プロセッサ毎のコアの通し番号
cpu cores	: 1 #CPU ごとのコアの数
apicid		: 0 #割り込みコントローラAPICが有効か否か
initial apicid	: 0 #同上
fpu		: yes #数値演算コプロセッサを搭載しているか否か
fpu_exception	: yes #FPU exceptionが有効になっているか否か
cpuid level	: 13 #CPUが持つ固有情報の読み出しレベル
wp		: yes #不明
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt #各パラメータのフラグ
bugs		: #バグ
bogomips	: 4800.13 #ベンチマーク値
clflush size	: 64 #キャッシュラインフラッシュサイズ
cache_alignment	: 64 #キャッシュアライメント
address sizes	: 46 bits physical, 48 bits virtual #アドレス空間がどのくらいあるか
power management: #

```

### meminfoを確認
```bash
cat /proc/meminfo
MemTotal:        1019116 kB #メモリの総容量
MemFree:          292892 kB #メモリの空き容量
MemAvailable:     647568 kB #露葉可能なメモリ
Buffers:          139632 kB #ファイルバッファに使用するメモリ量
Cached:           330024 kB #キャッシュメモリとして使用されるメモリの量
SwapCached:            0 kB #キャッシュメモリとして使用されるスワップ量
Active:           475080 kB #使用中バッファメモリあるいはページキャッシュメモリの容量
Inactive:          94488 kB #利用可能なバッファメモリあるいはページキャッシュメモリの容量
Active(anon):     103148 kB
Inactive(anon):    23656 kB
Active(file):     371932 kB
Inactive(file):    70832 kB
Unevictable:       53000 kB
Mlocked:           53000 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Dirty:                72 kB
Writeback:             0 kB
AnonPages:        151868 kB
Mapped:            81944 kB
Shmem:             23688 kB
Slab:              83080 kB
SReclaimable:      49072 kB
SUnreclaim:        34008 kB
KernelStack:        3312 kB
PageTables:         4160 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      509556 kB
Committed_AS:     945396 kB
VmallocTotal:   34359738367 kB
VmallocUsed:           0 kB
VmallocChunk:          0 kB
AnonHugePages:      8192 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       12288 kB
DirectMap2M:     1036288 kB
```
