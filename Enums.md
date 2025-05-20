```php
<?php

namespace App\Config;

use Symfony\Contracts\Translation\TranslatableInterface;
use Symfony\Contracts\Translation\TranslatorInterface;

enum TextAlign: string implements TranslatableInterface
{
    case Left = 'Left aligned';
    case Center = 'Center aligned';
    case Right = 'Right aligned';

    public function trans(TranslatorInterface $translator, ?string $locale = null): string
    {
        // Translate enum from name (Left, Center or Right)
        return $translator->trans($this->name, locale: $locale);

        // Translate enum using custom labels
        return match ($this) {
            self::Left  => $translator->trans('text_align.left.label', locale: $locale),
            self::Center => $translator->trans('text_align.center.label', locale: $locale),
            self::Right  => $translator->trans('text_align.right.label', locale: $locale),
        };
    }
}
```



