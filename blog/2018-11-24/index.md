---
date: "2018-11-24"
title: "Bildoptimierung in WP"
category: "Wordpress"
---

Wie man die Bilder in einem WordPress Projekt genügend komprimiert, sodass sogar [Google Insights](https://developers.google.com/speed/pagespeed/insights/) zufriedengestellt ist.

## Problemstellung

Immer wieder steht man vor dem Livegang eines Projektes vor der Herausforderung den bestmöglichen Score auf [Google Insights](https://developers.google.com/speed/pagespeed/insights/) zu bekommen. Einer der wichtigsten Punkte die man dabei zu beachten hat ist die Bildkomprimierung. Dafür bietet das WordPress Ecosystem sehr viele Plugins die sich darum kümmern. Um nur ein paar Beispiele zu nennen:

+ [EWWW Image Optimizer](https://de.wordpress.org/plugins/ewww-image-optimizer/)
+ [Compress JPEG & PNG images](https://de.wordpress.org/plugins/tiny-compress-images/)
+ [Smush](https://de.wordpress.org/plugins/wp-smushit/)

All diese Plugins sind erstens entweder in der Bildoptimierungen limitiert oder zwingen dich durch andere Gründe in ein Premium Abo oder ähnliches. Zusätzlich ist die Komprimierung (soweit ich das getestet habe) nicht optimal.

## Lösung

Meiner Meinung nach ist die wesentlich bessere Variante die Bilder auf Serverebene ohne WP Plugin zu komprimieren. Dazu gibt es mehrere Cli Tools, unter anderem:

+ jpegoptim oder jpegtran für jpg's
+ optipng für png's
+ gifsicle für gif's

Diese Libraries müssen auf dem Server einmalig installiert werden:

```bash
sudo apt-get install libjpeg-progs jpegoptim optipng gifsicle
```

Natürlich könnte man ein manuelles Script schreiben, welches jede Nacht mittels CronJob ausgeführt wird und alle Bilder in dem Projektordner recursive optimiert. Eine elegantere Lösung ist es jedoch eine helper Library zu verwenden. Ich habe [WP Cubi Imagemin](https://github.com/globalis-ms/wp-cubi-imagemin) getestet. Diese Library kann einfach über Composer installiert werden und bietet zum einen eine WP CLI Integration und zum anderen hooked sie sich in die WordPress Events und führt so Komprimierungen für einzelne Bilder bei speziellen Events aus. Dies ermöglicht es einmalig alle Bilder eines Projektes zu komprimieren:

```bash
wp media optimize <directories>
```

Und anschließend kümmert sich die Library um alles weitere. Ein automatisierte Komprimierung erfolgt, sobald ein Bild hochgeladen oder ein Bildzuschnitt neu generiert wird. Mit der Standardeinstellung der Komprimierungsstärke der Tools konnte ich jedes Bild zw 60 und 80% reduzieren ohne nennenswerte Verluste im Bild zu erkennen. So war sogar das unter PM's so beliebte Tool [Google Insights](https://developers.google.com/speed/pagespeed/insights/) zufriedengestellt.
