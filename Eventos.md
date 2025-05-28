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
### Assert
```php
#[Assert\Callback(callback: 'callback')]|
|public function validateDates(ExecutionContextInterface $context): void|
|{|

|if ($this->startDate && $this->endDate && $this->endDate < $this->startDate) {|

|$context->buildViolation('The end date can´t be earlier than the start date.')|

|->atPath('endDate')|

|->addViolation();|

|}|

}
```
