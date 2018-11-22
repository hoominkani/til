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
