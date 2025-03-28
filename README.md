# 高速可信协议 Trusted Express Protocol
`Trusted Express Protocol` is a protocol of radio communication.It's abbreviated as `TEP`.

`高速可信协议`是一种无线电通信协议，英文缩写为`TEP`

高速可信协议由此存储库所有者制定，此说明文档和协议具体内容均基于所有者母语`zh-hans-CN`撰写，在转译到其他文字和语言时或会出现若干错误，请以`zh-hans-CN`的内容为准。

The Trusted Express Protocol is developed by the owner of this repository. This description document and the specific content of the protocol are based on the owner's native language `zh-hans-CN`. Some errors may occur when translating to other written words and languages, whichever is `zh hans-CN`.

业余无线电操作者注意

ITU对于业余无线电有规定：

`25.2A	1A)不同国家业余电台之间的传输不应为模糊电文的意思的目的而编码，卫星业余业务中地面控制电台和空间电台之间交换的控制信号除外。（WRC-03）`

业余无线电在应用本协议时应当避免对信息的直接加密，应当使用数据签名实现数据可信。

# 为什么选择TEP？

TEP使用不对称加密算法，拥有鉴权功能，可以保证消息来源真实可靠，不被冒用身份。

TEP数据结构的核心是TLV格式，使得TEP十分灵活高效，可以轻松容纳任何类型和大小的数据。

TEP通过使用长短帧、前向纠错和交织，可以适应低信噪比与突发干扰的恶劣环境。

TEP协议文档完全免费、公开，任何人都可以免费利用TEP协议进行通信（如果你使用的TEP调制解调器是免费的）。

# v1.0
此协议有`TEPp` `TEPC`和`TCSR`三个子协议，分别是封包通信、数字证书和证书请求。

为保证用户使用`TEP`协议时的安全性和通用性，在此规定有关`TEP`的各种标准，作为应用规范，以避免因标准不一造成的冲突。

为防止版本更改过勤，版本分为大版本和小版本两部分，如`v1.0`即第一大版本的初始版本。在应用中只需传输大版本号即可。小版本主要是针对协议规范、标准的增添、删除和修订，对同一大版本兼容，基本不涉及协议的具体定义。


# 模板
| 数字 | 说明 | 数字 | 说明 | 数字 | 说明 | 数字 | 说明 |
|:---:|:---:|:---:|:---:|:---:|:----:|:---:|:---:|
| 00 |  | 40 |  | 80 |  | C0 |  |
| 01 |  | 41 |  | 81 |  | C1 |  |
| 02 |  | 42 |  | 82 |  | C2 |  |
| 03 |  | 43 |  | 83 |  | C3 |  |
| 04 |  | 44 |  | 84 |  | C4 |  |
| 05 |  | 45 |  | 85 |  | C5 |  |
| 06 |  | 46 |  | 86 |  | C6 |  |
| 07 |  | 47 |  | 87 |  | C7 |  |
| 08 |  | 48 |  | 88 |  | C8 |  |
| 09 |  | 49 |  | 89 |  | C9 |  |
| 0A |  | 4A |  | 8A |  | CA |  |
| 0B |  | 4B |  | 8B |  | CB |  |
| 0C |  | 4C |  | 8C |  | CC |  |
| 0D |  | 4D |  | 8D |  | CD |  |
| 0E |  | 4E |  | 8E |  | CE |  |
| 0F |  | 4F |  | 8F |  | CF |  |
| 10 |  | 50 |  | 90 |  | D0 |  |
| 11 |  | 51 |  | 91 |  | D1 |  |
| 12 |  | 52 |  | 92 |  | D2 |  |
| 13 |  | 53 |  | 93 |  | D3 |  |
| 14 |  | 54 |  | 94 |  | D4 |  |
| 15 |  | 55 |  | 95 |  | D5 |  |
| 16 |  | 56 |  | 96 |  | D6 |  |
| 17 |  | 57 |  | 97 |  | D7 |  |
| 18 |  | 58 |  | 98 |  | D8 |  |
| 19 |  | 59 |  | 99 |  | D9 |  |
| 1A |  | 5A |  | 9A |  | DA |  |
| 1B |  | 5B |  | 9B |  | DB |  |
| 1C |  | 5C |  | 9C |  | DC |  |
| 1D |  | 5D |  | 9D |  | DD |  |
| 1E |  | 5E |  | 9E |  | DE |  |
| 1F |  | 5F |  | 9F |  | DF |  |
| 20 |  | 60 |  | A0 |  | E0 |  |
| 21 |  | 61 |  | A1 |  | E1 |  |
| 22 |  | 62 |  | A2 |  | E2 |  |
| 23 |  | 63 |  | A3 |  | E3 |  |
| 24 |  | 64 |  | A4 |  | E4 |  |
| 25 |  | 65 |  | A5 |  | E5 |  |
| 26 |  | 66 |  | A6 |  | E6 |  |
| 27 |  | 67 |  | A7 |  | E7 |  |
| 28 |  | 68 |  | A8 |  | E8 |  |
| 29 |  | 69 |  | A9 |  | E9 |  |
| 2A |  | 6A |  | AA |  | EA |  |
| 2B |  | 6B |  | AB |  | EB |  |
| 2C |  | 6C |  | AC |  | EC |  |
| 2D |  | 6D |  | AD |  | ED |  |
| 2E |  | 6E |  | AE |  | EE |  |
| 2F |  | 6F |  | AF |  | EF |  |
| 30 |  | 70 |  | B0 |  | F0 |  |
| 31 |  | 71 |  | B1 |  | F1 |  |
| 32 |  | 72 |  | B2 |  | F2 |  |
| 33 |  | 73 |  | B3 |  | F3 |  |
| 34 |  | 74 |  | B4 |  | F4 |  |
| 35 |  | 75 |  | B5 |  | F5 |  |
| 36 |  | 76 |  | B6 |  | F6 |  |
| 37 |  | 77 |  | B7 |  | F7 |  |
| 38 |  | 78 |  | B8 |  | F8 |  |
| 39 |  | 79 |  | B9 |  | F9 |  |
| 3A |  | 7A |  | BA |  | FA |  |
| 3B |  | 7B |  | BB |  | FB |  |
| 3C |  | 7C |  | BC |  | FC |  |
| 3D |  | 7D |  | BD |  | FD |  |
| 3E |  | 7E |  | BE |  | FE |  |
| 3F |  | 7F |  | BF |  | FF |  |
