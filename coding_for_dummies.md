
# Polybius



```python
# message: list[int]
polybius = [list(), list(" ABCDE"), list(" FGHIJ"), list(" KLMNO"), list(" PQRST"), list(" VWXYZ")]
def decode(secret_message):   
    message = ""
    for i in secret_message:
        r = i % 10
        c = i // 10
        message += polybius[r][c]
    return message
def encode(message):
    secret_message = []
    for letter in message:        
        row = next((row for row, l in enumerate(polybius) if letter in l))
        column = polybius[row].index(letter)
        secret_message.append(column * 10 + row)
    return secret_message
```


```python
secret_message = [12,53,34,54,15,43,51,12,11,15,53,34,44,54,32,51,21,53,23,41]
print(decode(secret_message))
```

    FORTVNEFAVORSTHEBOLD
    


```python
secret_message = encode("FORTVNEFAVORSTHEBOLD")
print(secret_message)
```

    [12, 53, 34, 54, 15, 43, 51, 12, 11, 15, 53, 34, 44, 54, 32, 51, 21, 53, 23, 41]
    

# Caesar


```python
alfabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
# message : String, shift : 
def encode_caesar(message, shift):
    secret_message = ""
    for letter in message:
        if letter != ' ':
            index = alfabet.index(letter)
            secret_message += alfabet[(index + shift) % 26]
        else:
            secret_message += ' '
    return secret_message
def decode_caesar(message, shift):
    return encode_caesar(message, -shift)
# create a dictionary of letter counts
def count_letters(message):
    dictionary = {}
    for letter in message:
        if letter != ' ':
            if letter in dictionary:                
                dictionary[letter] += 1
            else:
                dictionary[letter] = 1
    return dictionary
# probeert alle mogelijke sleutels
def crack_caesar(message):
    for i in range(1,27):
        print(decode_caesar(message, i))
    
```


```python
print(decode_caesar("EDG LV D SODQ ZKLFK FDQQRW EHDU D FKDQJH", 3))
```

    BAD IS A PLAN WHICH CANNOT BEAR A CHANGE
    


```python
dictionary = count_letters("ROHXD VDBCK ANJTC QNUJF MXRCC XBNRI NYXFN ARWJU UXCQN ALJBN BXKBN AENRC")
print(dictionary)
```

    {'R': 5, 'O': 1, 'H': 1, 'X': 6, 'D': 2, 'V': 1, 'B': 5, 'C': 6, 'K': 2, 'A': 4, 'N': 9, 'J': 4, 'T': 1, 'Q': 2, 'U': 3, 'F': 2, 'M': 1, 'I': 1, 'Y': 1, 'W': 1, 'L': 1, 'E': 1}
    


```python
ord('N') - ord('E')
```




    9




```python
decode_caesar("ROHXD VDBCK ANJTC QNUJF MXRCC XBNRI NYXFN ARWJU UXCQN ALJBN BXKBN AENRC", 9)
```




    'IFYOU MUSTB REAKT HELAW DOITT OSEIZ EPOWE RINAL LOTHE RCASE SOBSE RVEIT'




```python
crack_caesar("ROHXD VDBCK ANJTC QNUJF MXRCC XBNRI NYXFN ARWJU UXCQN ALJBN BXKBN AENRC")
```

    QNGWC UCABJ ZMISB PMTIE LWQBB WAMQH MXWEM ZQVIT TWBPM ZKIAM AWJAM ZDMQB
    PMFVB TBZAI YLHRA OLSHD KVPAA VZLPG LWVDL YPUHS SVAOL YJHZL ZVIZL YCLPA
    OLEUA SAYZH XKGQZ NKRGC JUOZZ UYKOF KVUCK XOTGR RUZNK XIGYK YUHYK XBKOZ
    NKDTZ RZXYG WJFPY MJQFB ITNYY TXJNE JUTBJ WNSFQ QTYMJ WHFXJ XTGXJ WAJNY
    MJCSY QYWXF VIEOX LIPEA HSMXX SWIMD ITSAI VMREP PSXLI VGEWI WSFWI VZIMX
    LIBRX PXVWE UHDNW KHODZ GRLWW RVHLC HSRZH ULQDO ORWKH UFDVH VREVH UYHLW
    KHAQW OWUVD TGCMV JGNCY FQKVV QUGKB GRQYG TKPCN NQVJG TECUG UQDUG TXGKV
    JGZPV NVTUC SFBLU IFMBX EPJUU PTFJA FQPXF SJOBM MPUIF SDBTF TPCTF SWFJU
    IFYOU MUSTB REAKT HELAW DOITT OSEIZ EPOWE RINAL LOTHE RCASE SOBSE RVEIT
    HEXNT LTRSA QDZJS GDKZV CNHSS NRDHY DONVD QHMZK KNSGD QBZRD RNARD QUDHS
    GDWMS KSQRZ PCYIR FCJYU BMGRR MQCGX CNMUC PGLYJ JMRFC PAYQC QMZQC PTCGR
    FCVLR JRPQY OBXHQ EBIXT ALFQQ LPBFW BMLTB OFKXI ILQEB OZXPB PLYPB OSBFQ
    EBUKQ IQOPX NAWGP DAHWS ZKEPP KOAEV ALKSA NEJWH HKPDA NYWOA OKXOA NRAEP
    DATJP HPNOW MZVFO CZGVR YJDOO JNZDU ZKJRZ MDIVG GJOCZ MXVNZ NJWNZ MQZDO
    CZSIO GOMNV LYUEN BYFUQ XICNN IMYCT YJIQY LCHUF FINBY LWUMY MIVMY LPYCN
    BYRHN FNLMU KXTDM AXETP WHBMM HLXBS XIHPX KBGTE EHMAX KVTLX LHULX KOXBM
    AXQGM EMKLT JWSCL ZWDSO VGALL GKWAR WHGOW JAFSD DGLZW JUSKW KGTKW JNWAL
    ZWPFL DLJKS IVRBK YVCRN UFZKK FJVZQ VGFNV IZERC CFKYV ITRJV JFSJV IMVZK
    YVOEK CKIJR HUQAJ XUBQM TEYJJ EIUYP UFEMU HYDQB BEJXU HSQIU IERIU HLUYJ
    XUNDJ BJHIQ GTPZI WTAPL SDXII DHTXO TEDLT GXCPA ADIWT GRPHT HDQHT GKTXI
    WTMCI AIGHP FSOYH VSZOK RCWHH CGSWN SDCKS FWBOZ ZCHVS FQOGS GCPGS FJSWH
    VSLBH ZHFGO ERNXG URYNJ QBVGG BFRVM RCBJR EVANY YBGUR EPNFR FBOFR EIRVG
    URKAG YGEFN DQMWF TQXMI PAUFF AEQUL QBAIQ DUZMX XAFTQ DOMEQ EANEQ DHQUF
    TQJZF XFDEM CPLVE SPWLH OZTEE ZDPTK PAZHP CTYLW WZESP CNLDP DZMDP CGPTE
    SPIYE WECDL BOKUD ROVKG NYSDD YCOSJ OZYGO BSXKV VYDRO BMKCO CYLCO BFOSD
    ROHXD VDBCK ANJTC QNUJF MXRCC XBNRI NYXFN ARWJU UXCQN ALJBN BXKBN AENRC
    


```python
# message is een string
def scytale_decode(secret_message, shift):
    message = ""
    for start in reversed(range(shift)):
        i = start
        while (i < len(secret_message)):
            message += secret_message[i]
            i += shift
    return message
```


```python
message = "ANACDDEIORSUTWBAOTIRFNSUEELNTFEHRMAIYNE"
scytale_decode(message, 3)
```




    'ADOUBTFULFRIENDISWORSETHANACERTAINENEMY'




```python
# nummer: een getal van 9 cijfers
def controle_getal(nummer):
    controle = 0
    for i in range(1, 10):
        controle += (nummer % 10) * i
        nummer //= 10
    return controle
def elf_proef(nummer):
    return controle_getal(nummer) % 11 == 0
```




    0


