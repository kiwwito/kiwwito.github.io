---
layout: post
title: "Función PHP para validar DNI/NIE español"
description: "Función PHP que comprueba si una cadena de texto es un DNI/NIE español válido"
redirect_from: /articulo/funcion-php-para-validar-dni-nie-espanol/
locale: es
---

Función PHP que comprueba si una cadena de texto es un DNI/NIE español válida:

{% highlight php startinline %}
function is_valid_dni_nie($string) {
    if (strlen($string) != 9 ||
        preg_match('/^[XYZ]?([0-9]{7,8})([A-Z])$/i', $string, $matches) !== 1) {
        return false;
    }

    $map = 'TRWAGMYFPDXBNJZSQVHLCKE';

    list(, $nieLetter, $number, $letter) = $matches;

    if ($nieLetter) {
        $number = str_replace(['X', 'Y', 'Z'], [0, 1, 2], $nieLetter) ."". $number;
    }

    return strtoupper($letter) === $map[((int) $number) % 23];
}
{% endhighlight %}
