+++
title = "Laravel 學習筆記 Lesson 16"
slug = "laravel-xue-xi-bi-ji-lesson-16"
date = "2014-11-17T13:14:09.000Z"
url = "/2014/11/17/laravel-xue-xi-bi-ji-lesson-16"
draft = true
+++

### 分頁

$allUsers = User::paginate(15);

<?php echo $allUsers->links(); ?>

$allUsers = User::simplePaginate(15);

<?php echo $allUsers->links('pagination::simple'); ?>

<?php
    $presenter = new Illuminate\Pagination\BootstrapPresenter($paginator);

    $trans = $environment->getTranslator();
?>

<?php if ($paginator->getLastPage() > 1): ?>
    <ul class="pager custom">
        <?php
            echo $presenter->getPrevious($trans->trans('pagination.previous'));

            echo $presenter->getNext($trans->trans('pagination.next'));
        ?>
    </ul>
<?php endif; ?>


<?php echo $allUsers->links('pagination.my-links'); ?>