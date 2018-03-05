# OD Komutu Kullanımı ( Print Binary )
Linux komut satırı üzerinde, bir dosyanın farklı formatlarda basılmasını sağlar.
Özellikle binary dosya içeriği olan dosyaların içeriğini görmede işe yarar.
Default olarak Hexadecimal format gösterimi yapar.

Kullanımı :
```bash
od [OPTION]... [FILE]...
```

### 1 - Octal Format : -b option
```bash
$ od -b input
0000000 061 012 062 012 063 012 064 012 065 012 066 012 067 012 070 012
0000020 071 012 061 060 012 061 061 012 061 062 012 061 063 012 061 064
0000040 012 061 065 012 061 066 012 061 067 012 061 070 012 061 071 012
0000060 062 060 012
0000063
```

### 2 - Character Format : -c option
```bash
$ od -c input
0000000   1  \n   2  \n   3  \n   4  \n   5  \n   6  \n   7  \n   8  \n
0000020   9  \n   1   0  \n   1   1  \n   1   2  \n   1   3  \n   1   4
0000040  \n   1   5  \n   1   6  \n   1   7  \n   1   8  \n   1   9  \n
0000060   2   0  \n
0000063
```

### 3 - İlk satırın (byte ofset / Sıra numarası) farklı gösterimleri için : -A option
- Hexadecimal (using **-x** along with -A)
- Octal (using **-o** along with -A) -> **10'luk sistem**
- Decimal (using **-d** along with -A)
### 4 - Ofset olmadan gösterim için -> -An
```bash
$ od -An -c input
   1  \n   2  \n   3  \n   4  \n   5  \n   6  \n   7  \n   8  \n
   9  \n   1   0  \n   1   1  \n   1   2  \n   1   3  \n   1   4
  \n   1   5  \n   1   6  \n   1   7  \n   1   8  \n   1   9  \n
   2   0  \n
```

### 5 - İlk n karakteri atlamak ve sonrasından yazmaya başlamak için : -j option
```bash
$ od -j9 -c input
```

### 6 - Yazılacak byte sayısını limitlemek için : -N option
```bash
$ od -N9 -c input
```

### 7 -  Decimal integers gösterimi için : -i option
```bash
$ od -i input
0000000   171051569   171182643   171313717   171444791
0000020   808520249   170995978   822751793   875629107
0000040   171258122   822752817   942737975   171520266
0000060      667698
0000063
```

### 8 - Hexadecimal 2 byte units gösterim için : -x option
```bash
$ od -x input
0000000 0a31 0a32 0a33 0a34 0a35 0a36 0a37 0a38
0000020 0a39 3031 310a 0a31 3231 310a 0a33 3431
0000040 310a 0a35 3631 310a 0a37 3831 310a 0a39
0000060 3032 000a
0000063
```

### 9 - 2 byte octal units gösterim için : -o option ( Bu kısım default gösterimdir )
```bash
$ od -o input
0000000 005061 005062 005063 005064 005065 005066 005067 005070
0000020 005071 030061 030412 005061 031061 030412 005063 032061
0000040 030412 005065 033061 030412 005067 034061 030412 005071
0000060 030062 000012
0000063
```

### 10 - Yazılacak satır genişliğini ayarlamak için : -w option
```bash
$ od -w1 -c -Ad input
0000000   1
0000001  \n
0000002   2
0000003  \n
0000004   3
0000005  \n
0000006   4
```

### 11 - Gizlenen tekrarlanan karakterlerin gösterinimini sağlamak için : -v option
Normalde tekrarlayan karakterler * işariyle gösterilir. Bunların gösterimini sağlamak için bu parametre kullanılabilir. 
```bash
$ od -v input
```

### 12 - Terminal üzerinden girilecek inputların göstermi için : - option
```bash
$ od -c -
```

`Ctrl + D`tuşlarına bir kaç kez basılıp sonuçların listelenmesi sağlanabilir.











