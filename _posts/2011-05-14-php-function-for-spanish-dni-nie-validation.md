---
layout: post
title: "PHP function for spanish DNI/NIE validation"
description: "PHP function which checks if a given string was a valid spanish DNI/NIE"
redirect_from:
    - /article/php-function-for-spanish-dni-validation/
    - /php-function-for-spanish-dni-validation/
locale: en
---

PHP function which checks if a given string was a valid spanish DNI/NIE:

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
