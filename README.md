QueueManagerBundle
==================

## How to install

### Step 1: Download using composer:

``` bash
composer.phar require arko/queue-manager-bundle "dev-master"
```
### Step 2: Enable the bundle:

``` php
<?php
// app/AppKernel.php

public function registerBundle() {
    $bundles = array(
        // ...
        new Arko/QueueManagerBundle/ArkoQueueManagerBundle(),
    );
}
```

## How to use

You should be able to get queue manager service from the service container like this:

``` php
$queueManager = $container->get('arko.queue_manager');
```

Or, as usual, you can inject it in your own service definitions using its id: **arko.queue_manager**.

From now you can use it to add different actions to the named queues:

``` php
$queueManager->add(function() {
    // Do something here
}, 'queue_name');

// ...

$queueManager->add(function() {
    // Do something else, maybe somewhere else.
}, 'queue_name');
```
As a first argument to the queue manager add method you can provide any php callable.

Later you will be able to process the queue like this:

``` php
$queueManager->process('queue_name');
```

After the queue is processed, it will be cleared. Generally speaking, it will be cleared just before the queue is 
processed. So, nested queues should work just fine.