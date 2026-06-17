---
{"dg-publish":true,"permalink":"/解谜/MAY_IENJOLFDPRCT解密/","dgPassFrontmatter":true,"dg-note-properties":{}}
---

1. 用[[线索文件/全日记残页#^rj8\|日记残页8]]给出的字母表：
```
MAY_IENJOLFDPRCT
```
> [!INFO]- 这串字符是指罗德岛标志的左半边小字 
![罗德岛标志的左半边小字.png\|100](/img/user/%E5%9B%BE%E7%89%87/%E8%A7%A3%E5%AF%86%E6%96%87%E4%BB%B6/%E7%BD%97%E5%BE%B7%E5%B2%9B%E6%A0%87%E5%BF%97%E7%9A%84%E5%B7%A6%E5%8D%8A%E8%BE%B9%E5%B0%8F%E5%AD%97.png)

把它当成 16个符号，对应半字节0-F：
```
MAY＿IENJOLFDPRCT
012  3456789ABCDEF
```

2. 用留言板给出的RE45当密钥。
RE45的 ASCIl 十六进制是：
```
R E 4 5
52 45 34 35
```
把每个十六进制数拆成两个“半字节”（也就是留言板4bit回复的8->4 半字节移位）
```
5 2 4 5 3 4 3 5
```
3. 对[[线索文件/全日记残页#^rj7\|日记残页7]]密文逐字符解密。
```
连成一长串：FIOFNONFJTJENINEOYJENINEPFJPNOEELEJFNNE_O_JLNPEEONJDNINROJJRNINFODJREANNO_JJEINJFENYNONF
```
规则是：
```
plain_nibble=(cipher_index-key_nibble) mod 16
```
然后两个半字节合成一个ASCII字符

> [!NOTE]- 以防你看不懂
前8个密文字符 F I O F N O N F
密文	cipher_index	密钥	计算 (mod 16)	plain_nibble
F	10	5	(10-5)=5	5
I	4	2	(4-2)=2	2
O	8	4	(8-4)=4	4
F	10	5	(10-5)=5	5
N	6	3	(6-3)=3	3
O	8	4	(8-4)=4	4
N	6	3	(6-3)=3	3
F	10	5	(10-5)=5	5
得到 8 个半字节：5,2,4,5,3,4,3,5
两两组合：（前一个数×16 + 后一个数）
(5,2) → 5×16+2 = 82 → 'R'
(4,5) → 4×16+5 = 69 → 'E'
(3,4) → 3×16+4 = 52 → '4'
(3,5) → 3×16+5 = 53 → '5'
解密出 RE45，这就是开头

4. 解出来的第一层结果是：
```
RE45-0000000x74 C52.148 4608580598-112 2S-45
```
5. 将其解读为：
```
RE45=身份，迷迭香
0x74 =VECTOR-BREAKOUT 线索
C52.148/C52.142=疑似身份参数或坐标片段
4608580598=很像MGRS坐标数字
2S-45=可能参与拼52S，或仍是未解释参数
```