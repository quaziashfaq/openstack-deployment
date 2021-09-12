# KVM Installation

I use ArchLinux. So I check the trusted [wiki](https://wiki.archlinux.org/title/KVM)

First, check hardware support
```
$ LC_ALL=C lscpu
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         39 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  4
  On-line CPU(s) list:   0-3
Vendor ID:               GenuineIntel
  Model name:            Intel(R) Core(TM) i5-5300U CPU @ 2.30GHz
    CPU family:          6
    Model:               61
    Thread(s) per core:  2
    Core(s) per socket:  2
    Socket(s):           1
    Stepping:            4
    CPU max MHz:         2900.0000
    CPU min MHz:         500.0000
    BogoMIPS:            4591.65
    Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm 
                         constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdb
                         g fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb in
                         vpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm rdsee
                         d adx smap intel_pt xsaveopt dtherm ida arat pln pts md_clear flush_l1d
Virtualization features: 
  Virtualization:        VT-x
Caches (sum of all):     
  L1d:                   64 KiB (2 instances)
  L1i:                   64 KiB (2 instances)
  L2:                    512 KiB (2 instances)
  L3:                    3 MiB (1 instance)
NUMA:                    
  NUMA node(s):          1
  NUMA node0 CPU(s):     0-3
Vulnerabilities:         
  Itlb multihit:         KVM: Mitigation: VMX disabled
  L1tf:                  Mitigation; PTE Inversion; VMX conditional cache flushes, SMT vulnerable
  Mds:                   Mitigation; Clear CPU buffers; SMT vulnerable
  Meltdown:              Mitigation; PTI
  Spec store bypass:     Mitigation; Speculative Store Bypass disabled via prctl and seccomp
  Spectre v1:            Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:            Mitigation; Full generic retpoline, IBPB conditional, IBRS_FW, STIBP conditional, RSB filling
  Srbds:                 Mitigation; Microcode
  Tsx async abort:       Mitigation; Clear CPU buffers; SMT vulnerable
```

In short:
```
magpie:~ ash% LC_ALL=C lscpu | grep Virtualization
Virtualization:                  VT-x
```

OK. I have virtualization support. I can install KVM.

Arch Linux kernels provide the required kernel modules to support KVM.

One can check if the necessary modules, kvm and either `kvm_amd` or `kvm_intel`, are available in the kernel with the following command:
```
$ zgrep CONFIG_KVM /proc/config.gz
CONFIG_KVM_GUEST=y
CONFIG_KVM_MMIO=y
CONFIG_KVM_ASYNC_PF=y
CONFIG_KVM_VFIO=y
CONFIG_KVM_GENERIC_DIRTYLOG_READ_PROTECT=y
CONFIG_KVM_COMPAT=y
CONFIG_KVM_XFER_TO_GUEST_WORK=y
CONFIG_KVM=m
CONFIG_KVM_INTEL=m
CONFIG_KVM_AMD=m
CONFIG_KVM_AMD_SEV=y
CONFIG_KVM_XEN=y
CONFIG_KVM_MMU_AUDIT=y
```
The module is available only if it is set to either y or m.





