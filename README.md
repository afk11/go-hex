# go-hex

[![GoDoc](https://godoc.org/github.com/tmthrgd/go-hex?status.svg)](https://godoc.org/github.com/tmthrgd/go-hex)
[![Build Status](https://travis-ci.org/tmthrgd/go-hex.svg?branch=master)](https://travis-ci.org/tmthrgd/go-hex)

An efficient hexadecimal implementation for Golang.

go-hex provides hex encoding and decoding using SSE/AVX instructions on x86-64.

## Download

```
go get github.com/tmthrgd/go-hex
```

## Benchmark

go-hex:
```
BenchmarkEncode_32-8     	100000000	        11.9 ns/op	2690.43 MB/s
BenchmarkEncode_128-8    	100000000	        21.4 ns/op	5982.92 MB/s
BenchmarkEncode_1k-8     	20000000	        88.5 ns/op	11572.80 MB/s
BenchmarkEncode_16k-8    	 1000000	      1254 ns/op	13058.10 MB/s
BenchmarkEncode_128k-8   	  100000	     12965 ns/op	10109.53 MB/s
BenchmarkEncode_1M-8     	   10000	    119465 ns/op	8777.23 MB/s
BenchmarkEncode_16M-8    	     500	   3530380 ns/op	4752.24 MB/s
BenchmarkEncode_128M-8   	      50	  28001913 ns/op	4793.16 MB/s
BenchmarkDecode_32-8     	100000000	        12.8 ns/op	2496.87 MB/s
BenchmarkDecode_128-8    	50000000	        28.4 ns/op	4507.07 MB/s
BenchmarkDecode_1k-8     	10000000	       172 ns/op	5947.97 MB/s
BenchmarkDecode_16k-8    	  500000	      2682 ns/op	6107.70 MB/s
BenchmarkDecode_128k-8   	  100000	     21429 ns/op	6116.44 MB/s
BenchmarkDecode_1M-8     	   10000	    173972 ns/op	6027.25 MB/s
BenchmarkDecode_16M-8    	     500	   3269415 ns/op	5131.57 MB/s
BenchmarkDecode_128M-8   	      50	  26166829 ns/op	5129.31 MB/s
```

[encoding/hex](https://golang.org/pkg/encoding/hex/):
```
BenchmarkRefEncode_32-8  	20000000	        72.9 ns/op	 439.14 MB/s
BenchmarkRefEncode_128-8 	 5000000	       289 ns/op	 441.54 MB/s
BenchmarkRefEncode_1k-8  	 1000000	      2268 ns/op	 451.49 MB/s
BenchmarkRefEncode_16k-8 	   30000	     39110 ns/op	 418.91 MB/s
BenchmarkRefEncode_128k-8	    5000	    291260 ns/op	 450.02 MB/s
BenchmarkRefEncode_1M-8  	    1000	   2277578 ns/op	 460.39 MB/s
BenchmarkRefEncode_16M-8 	      30	  37087543 ns/op	 452.37 MB/s
BenchmarkRefEncode_128M-8	       5	 293611713 ns/op	 457.13 MB/s
BenchmarkRefDecode_32-8  	10000000	       128 ns/op	 248.44 MB/s
BenchmarkRefDecode_128-8 	 3000000	       481 ns/op	 265.95 MB/s
BenchmarkRefDecode_1k-8  	  300000	      4172 ns/op	 245.43 MB/s
BenchmarkRefDecode_16k-8 	   10000	    111989 ns/op	 146.30 MB/s
BenchmarkRefDecode_128k-8	    2000	    909077 ns/op	 144.18 MB/s
BenchmarkRefDecode_1M-8  	     200	   7275779 ns/op	 144.12 MB/s
BenchmarkRefDecode_16M-8 	      10	 116574839 ns/op	 143.92 MB/s
BenchmarkRefDecode_128M-8	       2	 933871637 ns/op	 143.72 MB/s
```

[encoding/hex](https://golang.org/pkg/encoding/hex/) -> go-hex:
```
benchmark                  old ns/op     new ns/op     delta
BenchmarkEncode_32-8       72.9          11.9          -83.68%
BenchmarkEncode_128-8      289           21.4          -92.60%
BenchmarkEncode_1k-8       2268          88.5          -96.10%
BenchmarkEncode_16k-8      39110         1254          -96.79%
BenchmarkEncode_128k-8     291260        12965         -95.55%
BenchmarkEncode_1M-8       2277578       119465        -94.75%
BenchmarkEncode_16M-8      37087543      3530380       -90.48%
BenchmarkEncode_128M-8     293611713     28001913      -90.46%
BenchmarkDecode_32-8       128           12.8          -90.00%
BenchmarkDecode_128-8      481           28.4          -94.10%
BenchmarkDecode_1k-8       4172          172           -95.88%
BenchmarkDecode_16k-8      111989        2682          -97.61%
BenchmarkDecode_128k-8     909077        21429         -97.64%
BenchmarkDecode_1M-8       7275779       173972        -97.61%
BenchmarkDecode_16M-8      116574839     3269415       -97.20%
BenchmarkDecode_128M-8     933871637     26166829      -97.20%

benchmark                  old MB/s     new MB/s     speedup
BenchmarkEncode_32-8       439.14       2690.43      6.13x
BenchmarkEncode_128-8      441.54       5982.92      13.55x
BenchmarkEncode_1k-8       451.49       11572.80     25.63x
BenchmarkEncode_16k-8      418.91       13058.10     31.17x
BenchmarkEncode_128k-8     450.02       10109.53     22.46x
BenchmarkEncode_1M-8       460.39       8777.23      19.06x
BenchmarkEncode_16M-8      452.37       4752.24      10.51x
BenchmarkEncode_128M-8     457.13       4793.16      10.49x
BenchmarkDecode_32-8       248.44       2496.87      10.05x
BenchmarkDecode_128-8      265.95       4507.07      16.95x
BenchmarkDecode_1k-8       245.43       5947.97      24.23x
BenchmarkDecode_16k-8      146.30       6107.70      41.75x
BenchmarkDecode_128k-8     144.18       6116.44      42.42x
BenchmarkDecode_1M-8       144.12       6027.25      41.82x
BenchmarkDecode_16M-8      143.92       5131.57      35.66x
BenchmarkDecode_128M-8     143.72       5129.31      35.69x
```

## License

Unless otherwise noted, the go-hex source files are distributed under the Modified BSD License
found in the LICENSE file.
