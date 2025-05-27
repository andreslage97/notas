### PreUpdate interesante sobre el cambio de atributo en el evento
```php
  #[ORM\PreUpdate()]
    public function preUpdateState(PreUpdateEventArgs $event): void
    {
        if ($event->hasChangedField('state') && $this->state === self::STATE_APPROVED) {
            $this->setValidatedAt(new \DateTimeImmutable());
        }
    }
```
