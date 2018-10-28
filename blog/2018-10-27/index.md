---
date: "2018-10-27"
title: "Zeit World DNS"
category: "Tools"
---

In letzter Zeit (pun intended) habe ich sehr viel mit verschiedenen Tools, Frameworks und neuen Programmiersprachen herumgespielt. Im Zuge davon musste ich viele DNS Records pflegen. Daher habe ich den DNS Management Service von Zeit ausprobiert.

## Kurz ein Intro zu Zeit

Zeit ist ein Unternehmen, das ein paar coole Produkte hervorgebracht hat. Das Hauptgeschäft ist wohl ihr Serverless Service [Now](https://zeit.co/now). Erst kürzlich veröffentlichten sie eine [Github Integration](https://zeit.co/blog/every-push-now) für ihren Service. So ermöglichen sie pushbasierte deployments und was ich sehr interessant finde eine automatische Testplatform für jeden Pull Request. Was ich schon länger täglich verwende ist [Hyper](https://hyper.is/), ein Terminal emulator. Aber dazu ein eigener Post.

## Zeit DNS

Ich liebe die CLI, daher finde ich es schonmal klasse wenn ich meine DNS Settings für meine Domains im Terminal pflegen kann. Zeit hat das wirklich einfach gemacht.

> Low-Latency global DNS. Now with even less configuration.

Natürlich muss man einmalig die Nameserver umstellen. Ab dann kann man alles im Terminal machen.

Als erstes registriert man die Domain.

```bash
now domain add example.com
```

Die Registrierung ist nur erfolgfreich, sofern die Nameserver von Zeit hinterlegt wurden. Sobald dies aber abgeschlossen ist kann jegliche DNS Einstellung via Terminal vorgenommen werden. Zum Beispiel so:

```bash
now dns add example.com @ A IP
```

Dieser Command würde den A Record der Domain anlegen. Wenn man eine Subdomain hinterlegen möchte einfach den Namen der Subdomain anstatt dem @ austauschen. Im selben Format kann man so auch jeden anderen DNS Eintrag vornehmen.

```bash
now dns add <domain> <name> <record type> <value> [mx_priority]
```
