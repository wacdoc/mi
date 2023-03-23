# Hangaia taau ake tūmau tuku mēra SMTP

## kupu whakataki

Ka taea e SMTP te hoko ratonga mai i nga kaihoko kapua, penei:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali kapua email pana](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Ka taea hoki e koe te hanga i a koe ake tūmau mēra - te tuku mutunga kore, he iti te utu.

Kei raro iho nei, ka whakaatuhia e matou nga taahiraa i te taahiraa me pehea te hanga i a maatau ake tūmau mēra.

## Kōwhiringa tūmau

Ko te tūmau SMTP e manaaki ana i a ia ano e hiahia ana he IP tūmatanui me nga tauranga 25, 456, me te 587 e tuwhera ana.

Ko nga kapua a-iwi e whakamahia nuitia ana kua aukatihia enei tauranga ma te taunoa, a ka taea pea te whakatuwhera ma te tuku i tetahi ota mahi, engari he tino raruraru i muri i nga mea katoa.

Ka tūtohu ahau ki te hoko mai i tetahi kaihautu kua tuwhera enei tauranga me te tautoko ki te whakatu ingoa rohe whakamuri.

I konei, ka tūtohu ahau [ki a Contabo](https://contabo.com) .

Ko Contabo he kaiwhakarato manaaki kei Munich, Tiamana, i hangaia i te 2003 me nga utu tino whakataetae.

Mena ka whiriwhiria e koe te Euro hei moni hoko, ka iti ake te utu (he tūmau me te 8GB te mahara me te 4 CPU te utu mo te 529 yuan ia tau, a ko te utu whakaurunga tuatahi he utu mo te tau kotahi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

I te wa e ota ana, `prefer AMD` , a ka pai ake te mahi a te tūmau me te PTM AMD.

I te whai ake nei, ka tango ahau i te VPS a Contabo hei tauira hei whakaatu me pehea te hanga i to ake tūmau mēra.

## whirihoranga pūnaha Ubuntu

Ko te punaha whakahaere i konei ko Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ki te whakaatu te tūmau i runga i te ssh `Welcome to TinyCore 13!` (penei i te ahua i raro nei), ko te tikanga kaore ano kia whakauruhia te punaha. Tena koa momotuhia te ssh ka tatari mo etahi meneti kia takiuru ano.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ina puta mai `Welcome to Ubuntu 22.04.1 LTS` , kua oti te arawhitinga, ka taea e koe te haere tonu me nga mahi e whai ake nei.

### [Kōwhiringa] Arawhiti te taiao whanaketanga

Ko tenei taahiraa he mea whiriwhiri.

Mo te waatea, ka tukuna e ahau te whakaurunga me te whirihoranga punaha o te rorohiko ubuntu ki [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Whakahaerehia te whakahau e whai ake nei hei whakauru ma te paato kotahi.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Ko nga kaiwhakamahi Hainamana, whakamahia te whakahau e whai ake nei, ka tautuhi aunoatia te reo, rohe wa, aha atu.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Ka taea e Contabo te IPV6

Whakahohehia te IPV6 kia taea hoki e SMTP te tuku imeera me nga wahitau IPV6.

whakatika `/etc/sysctl.conf`

Whakakē, tāpirihia rānei ngā rārangi e whai ake nei

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Whaia [te akoranga contabo: Te taapiri i te hononga IPv6 ki to tūmau](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Whakatikaina `/etc/netplan/01-netcfg.yaml` , taapirihia etahi rarangi e whakaatuhia ana i te ahua i raro nei (Kei a Contabo VPS te konae whirihoranga taunoa enei rarangi, me whakakore noa i a raatau).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Na ka `netplan apply` kia whai mana te whirihoranga whakarereke.

I muri i te angitu o te whirihoranga, ka taea e koe te whakamahi `curl 6.ipw.cn` ki te tiro i te wahitau IPv6 o to whatunga o waho.

## Whakakaohia nga mahi rokiroki whirihoranga

```
git clone https://github.com/wactax/ops.soft.git
```

## Hangaia he tiwhikete SSL koreutu mo to ingoa rohe

Ko te tuku mēra me whai tiwhikete SSL mo te whakamunatanga me te hainatanga.

Ka whakamahia e matou [acme.sh](https://github.com/acmesh-official/acme.sh) ki te whakaputa tiwhikete.

Ko te acme.sh he taputapu hainatanga tiwhikete aunoa puna tuwhera,

Whakauruhia te whare putunga whirihoranga ops.soft, rere `./ssl.sh` , ka hangaia he kōpaki `conf` ki **te raarangi o runga** .

Kimihia to kaiwhakarato DNS mai i [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , whakatika `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Na ka rere `./ssl.sh 123.com` ki te whakaputa `123.com` me `*.123.com` tiwhikete mo to ingoa rohe.

Ko te oma tuatahi ka whakauru aunoa [acme.sh](https://github.com/acmesh-official/acme.sh) me te taapiri i tetahi mahi kua whakaritea mo te whakahou aunoa. Ka taea e koe te kite `crontab -l` , he rarangi penei.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ko te huarahi mo te tiwhikete kua hangaia he rite ki te `/mnt/www/.acme.sh/123.com_ecc。`

Ko te whakahoutanga o te tiwhikete ka karanga `conf/reload/123.com.sh` script, whakatika i tenei tuhinga, ka taea e koe te taapiri i nga whakahau penei i te `nginx -s reload` ki te whakahou i te keteroki tiwhikete o nga tono e pa ana.

## Hangaia te tūmau SMTP me te chasquid

Ko [te chasquid](https://github.com/albertito/chasquid) he tūmau SMTP puna tuwhera i tuhia ki te reo Haere.

Hei whakakapi mo nga kaupapa tūmau mēra tawhito penei i te Postfix me te Sendmail, he ngawari ake te chasquid me te ngawari ki te whakamahi, he maamaa hoki mo te whanaketanga tuarua.

Whakahaerehia `./chasquid/init.sh 123.com` ka whakauru aunoa ma te paato kotahi (whakakapihia te 123.com me to ingoa rohe tuku).

## Whirihorahia te Waitohu Īmēra DKIM

Ka whakamahia te DKIM ki te tuku i nga waitohu imeera hei aukati i nga reta kia kore e kiia he spam.

I muri i te whakahaerenga angitu o te whakahau, ka akiakihia koe ki te whakatakoto i te rekoata DKIM (penei i raro nei).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Taapiri noa he rekoata TXT ki to DNS (e whakaatu ana i raro nei).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Tirohia te mana ratonga me nga raarangi

 `systemctl status chasquid` Tirohia te tūnga ratonga.

Ko te ahua o te mahi noa e whakaatuhia ana i te ahua i raro nei

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` or `journalctl -xeu chasquid` ka taea te tiro i te raarangi hapa.

## Whakamuri te whirihoranga ingoa rohe

Ko te ingoa rohe whakamuri ko te tuku i te wahitau IP kia whakatauhia ki te ingoa rohe e pa ana.

Ka taea e te whakatu i te ingoa rohe whakamuri te aukati i nga imeera mai i te tohu he mokowhiti.

Ina tae mai te mēra, ka mahia e te kaimau tuku te tātari ingoa rohe whakamuri ki te wahitau IP o te tūmau tuku hei whakaū mena he ingoa rohe whakamuri tika to te tūmau tuku.

Mena karekau he ingoa rohe whakamuri te tūmau tuku, ki te kore ranei te ingoa rohe whakamuri e taurite ki te wāhitau IP o te tūmau tuku, ka mohio pea te tūmau e whiwhi ana i te īmēra he pāme, ka whakakorehia rānei.

Tirohia [https://my.contabo.com/rdns](https://my.contabo.com/rdns) ka whirihora kia rite ki te whakaatu i raro nei

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

I muri i te tautuhi i te ingoa rohe whakamuri, mahara ki te whirihora i te whakataunga whakamua o te ingoa rohe ipv4 me ipv6 ki te tūmau.

## Whakatikaina te ingoa rangatira o chasquid.conf

Whakakē `conf/chasquid/chasquid.conf` ki te uara o te ingoa rohe whakamuri.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Na ka whakahaere i `systemctl restart chasquid` ki te whakaara ano i te ratonga.

## Pūrua te conf ki te putunga git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Hei tauira, ka whakahokia e ahau te kōpaki conf ki taku ake tukanga github e whai ake nei

Hangaia he whare putunga motuhake i te tuatahi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Whakauruhia te whaiaronga conf ka tuku ki te whare putunga

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Tāpirihia te kaituku

rere

```
chasquid-util user-add i@wac.tax
```

Ka taea te taapiri i te kaituku

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Manatokohia kua tika te tautuhi i te kupuhipa

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Whai muri i te taapiri i te kaiwhakamahi, ka whakahouhia `chasquid/domains/wac.tax/users` , mahara ki te tuku ki te whare putunga.

## DNS taapiri rekoata SPF

Ko te SPF ( Anga Kaupapa Kaituku ) he hangarau manatoko imeera e whakamahia ana hei aukati i te tinihanga imeera.

Ka whakamanahia te tuakiri o te kaituku mēra ma te tirotiro kei te rite te wahitau IP o te kaituku ki nga rekoata DNS o te ingoa rohe e kii ana ia, hei aukati i te hunga tinihanga ki te tuku imeera tinihanga.

Ko te taapiri i nga rekoata SPF ka taea te aukati i nga imeera kia mohiohia he mokowhiti ka taea.

Ki te kore e tautokohia e to ingoa ingoa rohe te momo SPF, taapirihia he rekoata momo TXT.

Hei tauira, ko te SPF o `wac.tax` e whai ake nei

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF mo `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Kia mahara kua `include:_spf.google.com` i konei, na te mea ka whirihora e ahau `i@wac.tax` hei wahitau tuku i roto i te pouaka mēra a Google i muri mai.

## whirihoranga DNS DMARC

Ko DMARC te whakapotonga o (Te Motuhēhēnga Karere, Pūrongo me te Whakaaetanga).

Ka whakamahia ki te hopu i nga tawhana SPF (kei te hapa whirihoranga, kei te kii mai ranei tetahi atu ko koe hei tuku mokowhiti).

Tāpiri rekooti TXT `_dmarc` ,

Ko nga korero e whai ake nei

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Ko te tikanga o ia tawhā e whai ake nei

### p (Kaupapahere)

E tohu ana me pehea te hapai i nga imeera kaore e taea te whakamana i te SPF (Anga Kaupapahere Kaituku) DKIM ranei (Meera Tautuhi DomainKeys). Ka taea te tautuhi i te tawhā p ki tetahi o nga uara e toru:

* karekau: Karekau he mahi, ko te hua whakamana ka whakahokia ki te kaituku ma te tikanga tuku korero imeera.
* Taratahi: Whakauruhia te mēra kare ano i tukuna te manatoko ki roto i te kōpaki spam, engari kaua e paopao tika i te mēra.
* paopao: Paopao tika i nga imeera kaore e taea te whakamana.

### fo (Kōwhiringa Rahua)

Ka tautuhi i te nui o nga korero i whakahokia mai e te tikanga tuku korero. Ka taea te tautuhi ki tetahi o nga uara e whai ake nei:

* 0: Purongo nga hua whakamana mo nga karere katoa
* 1: Ko nga karere karekau i te manatoko anake
* d: Me whakaatu noa i nga hapa manatoko ingoa rohe
* s: ripoata noa i nga rahunga manatoko SPF
* l: Me whakaatu noa nga rahunga manatoko DKIM

### rua & ruf

* rua (Reporting URI for Aggregate reports): Wāhitau īmēra mō te whiwhi pūrongo whakahiato
* ruf (Ripurongo URI mo nga purongo Forensic): he wahitau imeera hei whiwhi korero taipitopito

## Taapirihia nga rekoata MX hei tuku i nga imeera ki a Google Mail

I te mea karekau au i kite i tetahi pouaka reta rangatōpū kore utu e tautoko ana i nga wahitau o te ao (Catch-All, ka taea e au nga imeera ka tukuna ki tenei ingoa rohe, me te kore e aukati i nga tohu tuatahi), ka whakamahia e ahau te chasquid ki te tuku i nga imeera katoa ki taku pouaka mēra Gmail.

**Mena kei a koe taau ake pouaka putea pakihi utu, kaua e whakarereketia te MX ka pekehia tenei taahiraa.**

Whakatika `conf/chasquid/domains/wac.tax/aliases` , whakaturia te pouaka pouaka whakamua

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` e tohu ana i nga imeera katoa, ko `i` te wahitau imeera o mua o te kaiwhakamahi tuku i hangaia i runga ake nei. Hei tuku i te mēra, me taapiri ia kaiwhakamahi i tetahi raina.

Na ka taapirihia te rekoata MX (Ka tohu tika ahau ki te wahitau o te ingoa rohe whakamuri i konei, penei i te rarangi tuatahi i te ahua i raro nei).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Ka oti te whirihoranga, ka taea e koe te whakamahi i etahi atu wahitau imeera ki te tuku imeera ki `i@wac.tax` me `any123@wac.tax` kia kite mena ka taea e koe te whiwhi imeera i Gmail.

Ki te kore, tirohia te rangitaki chasquid ( `grep chasquid /var/log/syslog` ).

## Tukuna he imeera ki i@wac.tax me Google Mail

Whai muri i te whiwhinga a Google Mail i te mēra, i tumanako ahau ki te whakautu me `i@wac.tax` , kaua ki i.wac.tax@gmail.com.

Tirohia [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) ka paato i te "Taapirihia tetahi atu wahitau imeera".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Na, tomo te waehere whakaū i riro mai i te imeera i tukuna atu ki.

Ka mutu, ka taea te whakarite hei wahitau kaituku taunoa (me te whiringa ki te whakautu me te wahitau kotahi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

I tenei ara, kua oti i a matou te whakatuu i te tūmau mēra SMTP me te whakamahi i te Google Mail ki te tuku me te whiwhi imeera.

## Tukuna he imeera whakamatautau kia tirohia mena kua angitu te whirihoranga

Whakauruhia `ops/chasquid`

`direnv allow` ki te whakauru i nga whakawhirinakitanga (kua whakauruhia te direnv ki te tukanga arawhiti kotahi-matua o mua, kua taapirihia he matau ki te anga)

ka oma

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Ko te tikanga o nga tawhā e whai ake nei

* kaiwhakamahi: ingoa ingoa SMTP
* haere: Kupuhipa SMTP
* ki: kaiwhiwhi

Ka taea e koe te tuku imeera whakamatautau.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

E taunaki ana kia whakamahia a Gmail ki te whiwhi i nga imeera whakamatautau kia tirohia mena kua angitu nga whirihoranga.

### TLS whakamunatanga paerewa

E whakaatu ana i te ahua i raro nei, kei reira tenei kati iti, ko te tikanga kua pai te whakahohe i te tiwhikete SSL.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Na ka paato "Whakaatuhia te Īmēra Taketake"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

E whakaatu ana i te ahua i raro nei, ko te wharangi mēra taketake Gmail e whakaatu ana i te DKIM, ko te tikanga kua angitu te whirihoranga DKIM.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Tirohia te Received in the header of the original email, and you can see that the sender address is IPV6, which means that IPV6 is also successfully configured.
