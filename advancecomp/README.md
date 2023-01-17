<div align="center">
<p> ------------------------------------------------------ advmng ------------------------------------------------------ </p>
<p> ------------------------------------------------------ advancecomp: SEGV via invalid read address ------------------------------------------------------ </p>
</div>

### advancecomp: SEGV via invalid read address
Advancecomp advmng contains a segmentation fault.

### Product link
https://github.com/amadvance/advancecomp

### POC file
https://github.com/JieyongMa/poc/tree/main/advancecomp/poc_segv01_s.dat

### Command to reproduce
`./advmng -z ./poc_segv01_s.dat`

### Product version
```
git log
commit f4fc0677527bdc7d1b78b1cc43974df7fe849d43 (HEAD -> master, tag: v2.4, origin/master, origin/HEAD)
Author: Andrea Mazzoleni <amadvance@gmail.com>
Date:   Tue Nov 22 22:53:13 2022 +0100
```

### Problem Type
SEGV

### Crash Detail
```
AddressSanitizer:DEADLYSIGNAL
=================================================================
==566874==ERROR: AddressSanitizer: SEGV on unknown address 0x63203000091d (pc 0x5555555d4f75 bp 0x7fffffffcc20 sp 0x7fffffffcbb0 T0)
==566874==The signal is caused by a READ memory access.
    #0 0x5555555d4f74 in adv_png_unfilter_8 lib/png.c:277
    #1 0x5555555e6d01 in mng_read_ihdr lib/mng.c:290
    #2 0x5555555ed823 in mng_read lib/mng.c:686
    #3 0x5555555eeba2 in adv_mng_read lib/mng.c:784
    #4 0x55555557bb4f in convert_f_mng(adv_fz_struct*, adv_fz_struct*, unsigned int*, unsigned int*, adv_scroll_info_struct*, bool, bool) /home/fuzz/advancecomp/remng.cc:479
    #5 0x55555557f635 in convert_mng(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&) /home/fuzz/advancecomp/remng.cc:593
    #6 0x5555555802fd in convert_mng_inplace(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&) /home/fuzz/advancecomp/remng.cc:614
    #7 0x55555558be59 in remng_single(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, unsigned long long&, unsigned long long&) /home/fuzz/advancecomp/remng.cc:950
    #8 0x55555558d474 in remng_all(int, char**) /home/fuzz/advancecomp/remng.cc:985
    #9 0x5555555930d5 in process(int, char**) /home/fuzz/advancecomp/remng.cc:1249
    #10 0x555555594b8c in main /home/fuzz/advancecomp/remng.cc:1268
    #11 0x7ffff7027082 in __libc_start_main ../csu/libc-start.c:308
    #12 0x5555555717dd in _start (/home/fuzz/advancecomp/advmng+0x1d7dd)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV lib/png.c:277 in adv_png_unfilter_8
==566874==ABORTING
```

### Crash summary
```
SUMMARY: AddressSanitizer: SEGV lib/png.c:277 in adv_png_unfilter_8

```