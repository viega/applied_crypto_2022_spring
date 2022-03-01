# Project Components

This extra submission allows you to test individual components of the project.
Refer to the project documentation for specifications on how to implement all
the components. Refer to `example-input.json` and `example-output.json` for
example input/output you can use for testing.

## Requirements

Upload `fencrypt` executable file.
It must read json input from `stdin` and output its json output to `stdout`
(same as in previous assignments).

## Problems

### Problem 1

Given password string (**NOT** hex encoded) and salt (hex encoded):

```json
{
  "password": "e09f8ed71b715ec29d7c6c4db2efbf6a",
  "salt": "e95af5ec95b703b9fdb119a565df5012"
}
```

Generate the "master" key via PBKDF:

```json
"25340ee53eb54510ac8770f830c7750fa6b850176e35934fce0db56681e0ec4d"
```

### Problem 2

Given master key derived via PBKDF (hex encoded):

```json
"bb80687f3bb2be6c40322944ee145c947adcf8c8e989da60ebe8a1be5e9aa46b"
```

Generate all keys (all hex encoded):

```json
{
  "validator": "7cfbdb5d0bb4de33a0c31a57a8f50a4b",
  "feistel": [
    "fa229054738db8de31881203637a5eeb",
    "2d779e5c90ff180421a072153bd2e830",
    "3dc67b3a09ea7cde33f179fae9806d4d",
    "bd2a0991be66b66622bf5c4ddf39bef7"
  ],
  "mac": "59339365ac8b691c72eeb2c6f99fd6bb",
  "search_terms": "d587bda883addbed8df571f35eafa7fd"
}
```

### Problem 3

Given 16 byte key (hex encoded) as well as binary data (hex encoded):

```json
{
  "key": "f0976dc478d49e3e501a34c1bc0470d2",
  "data": "96812ae4e46f6394056a343cd24eabe9da96f03cf6f5ea697b7ca81db801605d306cebf586b15a2738dc45f0cae54f48c2de358a4afcfb190c8742d02142a69b"
}
```

Run the `data` via AES-CTR PRF Feistel round (refer to project's diagram for
specifics about the round) and return the result hex encoded:

```json
"96812ae4e46f6394056a343cd24eabe9c6dafa64f3c9d18037916f7ccce8442cc15019214cf268a71a749476175a0bca4f2d5bd0b05c38261cbee6a9fb217a6d"
```

### Problem 4

Given 16 byte key (hex encoded) as well as binary data (hex encoded):

```json
{
  "key": "4867eea7e831dba761ff4f6de73a647e",
  "data": "50e7c0a50e029eb6a22f3115d56f0884739fafaa742f1af02d21c3939fab0692af24920356c94376d0af52ae0fd125c915988c2628b22e10dd92ec91e32c41ed"
}
```

Run the `data` via HMAC PRF Feistel round (refer to project's diagram for
specifics about the round) and return the result hex encoded:

```json
"948761299e0ed12bd4ef3a5f6d939c88739fafaa742f1af02d21c3939fab0692af24920356c94376d0af52ae0fd125c915988c2628b22e10dd92ec91e32c41ed"
```

### Problem 5

Given Feistel network keys (each hex encoded) as well as binary plaintext (hex
encoded):

```json
{
  "keys": [
    "ce47fad49f2534b165d214abe17c73b0",
    "f0261ee3e6dc2bcb39fd491e2c9bb4d1",
    "d876c006c46189102caed558c69b7beb",
    "d440c02d720f38ee9190a0c9b4e5450a"
  ],
  "plaintext": "b8dfb1a24b7003a22b82eed984c14cf73d734eca13dcefe4ac52d0e9f02b1b8a1bafbb9d7886b5bacaa9cc0fce5dc88e8a4e7e651418d66297f6b3040ee42815"
}
```

Encrypt the plaintext and return the ciphertext hex encoded:

```json
"5ca7f4fddb04b84b5621f62d52ad1a8a10a5c5c3cf72e60f68b24ffe2e35befcb71ed1534b4158894cd7848f6b65acda08b6492add4657328500fe25491c38a6"
```

### Problem 6

Given Feistel network keys (each hex encoded) as well as binary ciphertext (hex
encoded):

```json
{
  "keys": [
    "6ebc78045155ad5eb412e3f45b42e270",
    "b8355ee3961e1bf498e877d66afbb9a1",
    "3425ce40cbfc5b7767a3a5e3efc36072",
    "9794c61df58c9b00c491b8a83cbd21ea"
  ],
  "ciphertext": "dbef4441512e336aa7790ba6a52d349dc775c131631f89614d7769d50ba8d4a018d9e672b0e7d225ea14b2c625e0fde7403d58bc4ef84fe73d007d55e3c379e6"
}
```

Decrypt the ciphertext and return the plaintext hex encoded:

```json
"9c11cad9de5e16458b36e98de478d59e5f732a90c5cf5633432bcb93a80da3c8c33a5be878346eb10d1ee3cd52d2bba918792932a9c29ef4c213f805593620b3"
```

### Problem 7

Given 16 byte key (hex encoded) as well as binary data (hex encoded):

```json
{
  "key": "bfff3ed5101115977e79be0d4a8d0f3b",
  "data": "3e669d9db69fa81a464d9ffec1ac9c3cf5aeea47e4b92bcddf137e767f45ded0e6c8c66ab4eff14a0952dfa33160e09c4e289f04decdf0f8321b8931c47c84d4"
}
```

Generate HMAC of the data and return the MAC hex encoded:

```json
"e78ace5ce7856ab83953895ba5547e9ee2e95f13f36e4a32818d613f83bf020c"
```

### Problem 8

Given a string of text (will only contain ascii characters):

```json
"CsykTn_ \f^4dX&\f\u000b ^VJTQsosg9YPSnxY\u000b\f{CBw0bDArl$\n\r\f\fwG2BXVobeSs]  \f\r*j6DzKvg~\u000b\fuahmKzMORE\n\u000bEtOkQq\t\t\f\nxb> \u000b\n\f%F1h97\u000b\r\n'DmbixGXadsairl9DQ\r\r\r}XbpBYYheM\fVEdpX- \ttpkt\\\u000b\u000b\fuG\n \u000b"
```

Return a list of searchable words from the text (see project description as to
what words should be searchable):

```json
[
  "CBw0bDArl",
  "CsykTn_",
  "EtOkQq",
  "F1h97",
  "VEdpX",
  "XbpBYYheM",
  "j6DzKvg",
  "tpkt",
  "uahmKzMORE",
  "wG2BXVobeSs"
]
```

### Problem 9

Same as `problem 8` but input will contain unicode characters:

```json
"xl8u5iadsfG\f\r\u000b\n=8OYHayywdu\r\t<y\t\n9Wq71IzvaDd\nᝄw\t_AiudH\rXwb2R\r[TlK8M& \t\nyS4s=\t\f~yM󠄖\nTQc0ѸIѶd‿ⳇlS8\r \u000b|vLqxrNy+\r\t\r\tⳇW`\u000b\t \f-hCuJd7pwfpv* \t\f\f*B\\\u000b\n)NⰊAyiB𝪝ᾛkhtzmd_ $L5OdRgH2Eyyx\u000b\ff\u000b|FừZh꧴ \u000b\tWQV\ffuUETlO9DS\n\f *󠄾\r_Vg3MQ85YEds𝔈Kᾨ+\rmqԷoi\r\u000b\r*Vg\r\nRᾈ45zB\t\n\nWwxbgFjpRALbuGnBwvR\f\u000b\n2F᱁iA\u000b\fdb5+\r\u000b \u000bBUVDꙄ^\n\n\t\n!5𑄻\"\n\f\t\r=𑛁OXx𓇠v\u000bÐѸb[\n\fRn2sXH1XJkfe| \txGj2pw!\t\rῢC_\n \r3dOᾩEᐽD\u000b"
```

Should generate same list of all searchable unicode words in the text:

```json
[
  "2F᱁iA",
  "3dOᾩEᐽD",
  "8OYHayywdu",
  "9Wq71IzvaDd",
  "BUVDꙄ",
  "FừZh꧴",
  "L5OdRgH2Eyyx",
  "Rn2sXH1XJkfe",
  "Rᾈ45zB",
  "TlK8M",
  "Xwb2R",
  "_AiudH",
  "fuUETlO9DS",
  "hCuJd7pwfpv",
  "mqԷoi",
  "vLqxrNy",
  "xGj2pw",
  "xl8u5iadsfG",
  "yS4s",
  "𑛁OXx𓇠v"
]
```

### Problem 10

Given a string of text (will only contain ascii characters):

```json
"&uCZGBPutUem\fsUB0bQioTLfJIPX/\f\f /NaRq5bWk&\u000b\n\nn,\t\n\t\tdnY01z4yvPuX8AWnPZka\r ?Wm0eIcQSVyv\r\u000b,BMPJa5'\r\n\n\rTknbf1KVCzKE`\f\r=a\nK0xcgF\n\n\r=9kxNYik}\u000b6ypx6il0Y.\t\u000b\u000b:m3{\r\u000b `BsG0TSfR*\n>ueeUN6iS\n"
```

Extract and return a list of all search terms which should be MACed as per
project description:

```json
[
  "6ypx*",
  "6ypx6*",
  "6ypx6i*",
  "6ypx6il*",
  "6ypx6il0*",
  "6ypx6il0y",
  "9kxn*",
  "9kxny*",
  "9kxnyi*",
  "9kxnyik",
  "bmpj*",
  "bmpja*",
  "bmpja5",
  "bsg0*",
  "bsg0t*",
  "bsg0ts*",
  "bsg0tsf*",
  "bsg0tsfr",
  "k0xc*",
  "k0xcg*",
  "k0xcgf",
  "narq*",
  "narq5*",
  "narq5b*",
  "narq5bw*",
  "narq5bwk",
  "tknb*",
  "tknbf*",
  "tknbf1*",
  "tknbf1k*",
  "tknbf1kv*",
  "tknbf1kvc*",
  "tknbf1kvcz*",
  "tknbf1kvczk*",
  "tknbf1kvczke",
  "wm0e*",
  "wm0ei*",
  "wm0eic*",
  "wm0eicq*",
  "wm0eicqs*",
  "wm0eicqsv*",
  "wm0eicqsvy*",
  "wm0eicqsvyv",
  "uczg*",
  "uczgb*",
  "uczgbp*",
  "uczgbpu*",
  "uczgbput*",
  "uczgbputu*",
  "uczgbputue*",
  "uczgbputuem",
  "ueeu*",
  "ueeun*",
  "ueeun6*",
  "ueeun6i*",
  "ueeun6is"
]
```

### Problem 11

Same as `problem 10` but input will contain unicode characters:

```json
"$cPDys79\t\r\\b*\u000b\r\n bAFsUS~ \t\t\tSUZ7iYDczrmdZ0j\r00OrMKR1Pc'\r\u000b\u000b Hrgriu5KhdᶻVR𝗳\r \fd4cMQOjc8YPD[\f\u000b\r\fugN00qY\n\n lHxCFxqwg,\t\u000b}idG1M9\u000b\\N9z\r \t\u000bhrnwH)\n |MQ71yjaGTjTOH4v\f \f\u000b\\SsAjwZJtSLoy\t7\f}TssGr7ZbdlaT_\t\nFZX2IzT^\f\t\r -;,<\u000b\f\r<8\f\n PwxSQnJxlrZjh\r/R6N2Vꓸ3u`\u000byozZ2uJyPJo9oK2qe\nI9RCuq| \n\nCjixLmcrzl5EMw\r\u000b_D3xCTvZ5KqY5N5pd+\n\tH󠄖Qot⁀r jQbⰊC)\f ]msꧏ〲໖KE4︳e51\u000b\n\r\fRaB! ~UIJqsTMcqblruhjHU\t\f\n\tsI7q〲K𝖊6ṁ\n\n\n 󠄖ⳇA1aD\n𖿠_\t  ;O0aBZEkzᵈm9O\u000bJ6C5\r,4W[\u000b\t\r "
```

Should generate same list of all unicode search terms:

```json
[
  "00or*",
  "00orm*",
  "00ormk*",
  "00ormkr*",
  "00ormkr1*",
  "00ormkr1p*",
  "00ormkr1pc",
  "fzx2*",
  "fzx2i*",
  "fzx2iz*",
  "fzx2izt",
  "h󠄖qo*",
  "h󠄖qot*",
  "h󠄖qot⁀*",
  "h󠄖qot⁀r",
  "i9rc*",
  "i9rcu*",
  "i9rcuq",
  "j6c5",
  "o0ab*",
  "o0abz*",
  "o0abze*",
  "o0abzek*",
  "o0abzekz*",
  "o0abzekzᵈ*",
  "o0abzekzᵈm*",
  "o0abzekzᵈm9*",
  "o0abzekzᵈm9o",
  "r6n2*",
  "r6n2v*",
  "r6n2vꓸ*",
  "r6n2vꓸ3*",
  "r6n2vꓸ3u",
  "ssaj*",
  "ssajw*",
  "ssajwz*",
  "ssajwzj*",
  "ssajwzjt*",
  "ssajwzjts*",
  "ssajwzjtsl*",
  "ssajwzjtslo*",
  "ssajwzjtsloy",
  "bafs*",
  "bafsu*",
  "bafsus",
  "cpdy*",
  "cpdys*",
  "cpdys7*",
  "cpdys79",
  "d4cm*",
  "d4cmq*",
  "d4cmqo*",
  "d4cmqoj*",
  "d4cmqojc*",
  "d4cmqojc8*",
  "d4cmqojc8y*",
  "d4cmqojc8yp*",
  "d4cmqojc8ypd",
  "hrnw*",
  "hrnwh",
  "idg1*",
  "idg1m*",
  "idg1m9",
  "jqbⰺ*",
  "jqbⰺc",
  "lhxc*",
  "lhxcf*",
  "lhxcfx*",
  "lhxcfxq*",
  "lhxcfxqw*",
  "lhxcfxqwg",
  "msꧏ〲*",
  "msꧏ〲໖*",
  "msꧏ〲໖k*",
  "msꧏ〲໖ke*",
  "msꧏ〲໖ke4*",
  "msꧏ〲໖ke4︳*",
  "msꧏ〲໖ke4︳e*",
  "msꧏ〲໖ke4︳e5*",
  "msꧏ〲໖ke4︳e51",
  "si7q*",
  "si7q〲*",
  "si7q〲k*",
  "si7q〲k𝖊*",
  "si7q〲k𝖊6*",
  "si7q〲k𝖊6ṁ",
  "ugn0*",
  "ugn00*",
  "ugn00q*",
  "ugn00qy",
  "󠄖ⳇa1*",
  "󠄖ⳇa1a*",
  "󠄖ⳇa1ad"
]
```
