---
notice: 'This file is imported and can be edited at https://github.com/amphp/http-server-static-content/blob/2.x/README.md'
title: 'Static File Serving'
description: "Learn how to serve static files with Amp's HTTP server."
image: undraw/undraw_logistics.svg
permalink: /http-server-static-content
source: 'https://github.com/amphp/http-server-static-content/blob/2.x/README.md'
layout: docs
---
AMPHP is a collection of event-driven libraries for PHP designed with fibers and concurrency in mind. This package provides an [HTTP server](https://amphp.org/http-server) plugin to serve static files like HTML, CSS, JavaScript, and images effortlessly. 

## Installation

This package can be installed as a [Composer](https://getcomposer.org/) dependency.

```bash
composer require amphp/http-server-static-content
```

## Usage

This package provides two `RequestHandler` implementations:
 - **`DocumentRoot`**: Serves all files within a directory.
 - **`StaticResource`**: Serves a single specific file.

The example below combines static file serving and [request routing](https://amphp.org/http-server-router) to demonstrate how they work well together:

```php
<?php

use Amp\Http\Server\DefaultErrorHandler;
use Amp\Http\Server\RequestHandler\ClosureRequestHandler;
use Amp\Http\Server\Response;
use Amp\Http\Server\SocketHttpServer;
use Amp\Http\Server\StaticContent\DocumentRoot;
use Amp\Http\Status;

$router = new Amp\Http\Server\Router;
$router->setFallback(new DocumentRoot(__DIR__ . '/public'));
$router->addRoute('GET', '/', new ClosureRequestHandler(function () {
    return new Response(Status::OK, ['content-type' => 'text/plain'], 'Hello, world!');
}));


$server->start($router, new DefaultErrorHandler());
```

## Contributing

Please read [our rules](https://amphp.org/contributing) for details on our code of conduct, and the process for submitting pull requests to us.

## Security

If you discover any security related issues, please use the private security issue reporter instead of using the public issue tracker.

## License

The MIT License (MIT). Please see [LICENSE](./LICENSE) for more information.
