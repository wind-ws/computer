
- 1 byte (8 bit): `byte`, `DB`, `RESB`
- 2 bytes (16 bit): `word`, `DW`, `RESW`
- 4 bytes (32 bit): `dword`, `DD`, `RESD`
- 8 bytes (64 bit): `qword`, `DQ`, `RESQ`
- 10 bytes (80 bit): `tword`, `DT`, `REST`
- 16 bytes (128 bit): `oword`, `DO`, `RESO`, `DDQ`, `RESDQ`
- 32 bytes (256 bit): `yword`, `DY`, `RESY`
- 64 bytes (512 bit): `zword`, `DZ`, `RESZ`


`section .data` : 被初始化的数据部分
格式:`<variable_name> <data_type> <initial_value>`
```nasm
section .data
var1 db 10              ; Byte Variable
var2 db "A"             ; String Character
var3 dw 1000            ; 16bit Variable
var4 dd 10, 20, 30      ; 3 Element Array
```

| Declaration | Variable(s)        |
| ----------- | ------------------ |
| `db`        | 8bit               |
| `dw`        | 16bit              |
| `dd`        | 32bit              |
| `dq`        | 64bit              |
| `ddq`       | 128bit ( Integer ) |
| `dt`        | 128bit ( Float )   |

`section .bss` : 未被初始化的数据部分
格式:  `<variable_name> <res_type> <count>`
```nasm
section .bss
array_b resb 10     ; 10 Element byte array
array_w resw 50     ; 50 Element word array
array_d resd 100    ; 100 element double array
array_q resq 200    ; 200 element quad array
```

|Declaration|Variable(s)|
|---|---|
|`resb`|8bit|
|`resw`|16bit|
|`resd`|32bit|
|`resq`|64bit|
|`resdq`|128bit|

`section .text` : 指令部分

```
section .text
	global _start ;声明入口点

_start:
	...
```

### 寻址模式
`[ base_address + ( index_register * scale_value ) + displacement ]`
**base_address** 是寄存器或变量名
index_register **必须是寄存器** 
scale_value **是立即数** ,取值范围为 1、2、4、8
displacement  必须是立即数。
算出来表示一个 64 位地址
# 参考
[Netwide Assembler - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Netwide_Assembler)
[GitHub - zhangjunlei26/NASM-Tutorial-CN: Nasm指南中文 (NASM Tutorial)](https://github.com/zhangjunlei26/NASM-Tutorial-CN)
[NASM - The Netwide Assembler](https://www.nasm.us/doc/)
[GitHub - las-nish/NASM-Assembly-Collection: NASM 64bit Short Note and sample files](https://github.com/las-nish/NASM-Assembly-Collection)
[NASM Assembly Language Tutorials - asmtutor.com](https://asmtutor.com/)
[GitHub - yds12/x64-roadmap: A roadmap to learn x64 assembly using nasm on Linux.](https://github.com/yds12/x64-roadmap)
[x86架构与汇编语言 · Hongzheng Chen](https://chhzh123.github.io/blogs/2019-03-07-x86-asm/)
[NASM Overview | 小白维基](https://wiki.blanc.site/archives/90a7f914.html)
[GitHub - FFmpeg/asm-lessons: FFMPEG Assembly Language Lessons](https://github.com/FFmpeg/asm-lessons/tree/main)