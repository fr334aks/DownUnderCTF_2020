# 16 Home Runs
![](https://i.imgur.com/jxKZnxt.png)

`RFVDVEZ7MTZfaDBtM19ydW41X20zNG41X3J1bm4xbjZfcDQ1N182NF9iNDUzNX0=`

Looking at the above encoded string, it is obviously encoded in `Base64`. The equal sign at the end makes it evident.

## solution

```
import base64
data = "RFVDVEZ7MTZfaDBtM19ydW41X20zNG41X3J1bm4xbjZfcDQ1N182NF9iNDUzNX0="
print(base64.b64decode(data))
```
## flag

`DUCTF{16_h0m3_run5_m34n5_runn1n6_p457_64_b4535}`
