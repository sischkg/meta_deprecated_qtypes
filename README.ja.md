# QTYPEがMETA TYPEやDEPRECATED TYPEであるクエリに対する権威DNSサーバの応答

## 対象権威サーバ

- Bind: 9.11.4-P2
- NSD: 4.1.25
- PowerDNS Authoritative Server 4.1.4
- Knot DNS

## TYPE

権威DNSサーバへ、QTYPEを次の値に指定した問い合わせを送信した時の応答を調査しました。

* TKEY
* TSIG
* OPT
* MAILA
* MAILB

### 例

```
$ dig @127.0.0.1 localhost OPT

; <<>> DiG 9.11.4-P2 <<>> @127.0.0.1 localhost OPT
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: FORMERR, id: 29060
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 2641b2f3273b359cc0f044175bbc085863b83429208eb0a8 (good)
;; QUESTION SECTION:
;localhost.                     IN      OPT

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Oct 09 10:46:00 JST 2018
;; MSG SIZE  rcvd: 66
```


## 調査結果


| QTYPE | BIND 9.11.4-P2 | NSD 4.1.25 | PowerDNS 4.1.4 | Knot DNS 2.7.2 |
|-------|----------------|------------|----------------|----------------|
| TSIG  | FORMERR        | NODATA     | NODATA         | NODATA         |
| TKEY  | FORMERR        | NODATA     | FORMERR        | NODATA         |
| OPT   | FORMERR        | NODATA     | NODATA         | NODATA         |
| MAILA | NOTIMP         | NODATA     | NODATA         | NODATA         |
| MAILB | NOTIMP         | NODATA     | NODATA         | NODATA         |



