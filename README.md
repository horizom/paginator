# Horizom Paginator

A simple paginator for PHP

## Installation

Install with composer:

```bash
composer require horizom/paginator
```

## Usage

```php
use Horizom\Paginator\Paginator;

$totalItems = 1000;
$itemsPerPage = 50;
$currentPage = 8;
$urlPattern = '/foo/page/(:num)';

$paginator = new Paginator($totalItems, $itemsPerPage, $currentPage, $urlPattern);
```

Use `$paginator->getPages()`, `$paginator->getNextUrl()`, and `$paginator->getPrevUrl()` to render a pagination control with your own HTML. For example:

```
<ul class="pagination">
    <?php if ($paginator->getPrevUrl()): ?>
        <li><a href="<?php echo $paginator->getPrevUrl(); ?>">&laquo; Previous</a></li>
    <?php endif; ?>

    <?php foreach ($paginator->getPages() as $page): ?>
        <?php if ($page['url']): ?>
            <li <?php echo $page['isCurrent'] ? 'class="active"' : ''; ?>>
                <a href="<?php echo $page['url']; ?>"><?php echo $page['num']; ?></a>
            </li>
        <?php else: ?>
            <li class="disabled"><span><?php echo $page['num']; ?></span></li>
        <?php endif; ?>
    <?php endforeach; ?>

    <?php if ($paginator->getNextUrl()): ?>
        <li><a href="<?php echo $paginator->getNextUrl(); ?>">Next &raquo;</a></li>
    <?php endif; ?>
</ul>

<p>
    <?php echo $paginator->getTotalItems(); ?> found.
    
    Showing 
    <?php echo $paginator->getCurrentPageFirstItem(); ?> 
    - 
    <?php echo $paginator->getCurrentPageLastItem(); ?>.
</p>
```

## License

MIT
