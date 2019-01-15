# Element Status Events Module for Craft CMS 3

The Element Status Events module provides events that are triggered whenever an element’s status changes. It is intended to be used a helper module for other Craft modules and plugins.

## License

This module is licensed for free under the MIT License.

## Requirements

This module requires Craft CMS 3.0.0 or later.

## Usage

Install the module manually using composer.

    composer require putyourlightson/craft-element-status-events

Then add it to your project’s `config/app.php` file as follows.

    return [
        'modules' => [
            'elementstatusevents' => putyourlightson\elementstatusevents\ElementStatusEvents::class,
        ],
        'bootstrap' => [
            'elementstatusevents',
        ],
    ];
    
The module provides the following events.

### `Element::EVENT_STATUS_CHANGED`

Triggered whenever an element’s status is changed. The element will have a `statusBeforeSave` (string) parameter available to it.

    Event::on(Element::class, ElementStatusBehavior::EVENT_STATUS_CHANGED, function() {
        /** @var Element $element */
        $element = $this->sender;
        
        $oldStatus = $element->statusBeforeSave;
        $newStatus = $element->status;
        $statusChanged = $element->$statusChanged;
    }); 

### `ElementStatusEvents::EVENT_ELEMENT_STATUSES_CHANGED`

Triggered after the response has been prepared if one or more element statused have changed. The element will have a `statusBeforeSave` (string) and `statusChanged` (boolean) parameter available to it.

    Event::on(ElementStatusEvents::class, ElementStatusEvents::EVENT_ELEMENT_STATUSES_CHANGED, 
        function(ElementStatusesEvent $event) {
            foreach ($event->elements as $element) {
                /** @var Element $element */
                $oldStatus = $element->statusBeforeSave;
                $newStatus = $element->status;
                $statusChanged = $element->$statusChanged;
            }
        }
    ); 

<small>Created by [PutYourLightsOn](https://putyourlightson.com/).</small>
