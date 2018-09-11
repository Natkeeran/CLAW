## Islandora Drupal Tests
Islandora’s Drupal modules make use of [Drupal’s testing framework](https://www.drupal.org/docs/8/testing).  Drupal has four types of tests: unit, kernal, functional and javascript tests. It makes use of the phpunit test framework.

Unit tests check individual methods. Kernel tests check against Drupal APIs. Functional tests simulate browser behavior. Javascript tests enables ajax and more complex browser behavior to be tested.

### Executing Tests in Vagrant
* Ensure that the simpletest directory (`/var/www/html/drupal/web/sites/simpletest`) is owned by `www-data` by issuing the following command: `sudo chown -R www-data:www-data simpletest`

* You can run the tests for a particular module with the follwoing command: 
```
sudo -u www-data php /var/www/html/drupal/web/core/scripts/run-tests.sh --suppress-deprecations --url http://localhost:8000 --verbose --php `which php` --module "module_name"
```

Note that suppress-deprecations flag is needed due to deprecated functions in Drupal core test classes.

### Understanding Functional Tests
Functional tests sets up a new core Drupal instance.  This core Drupal instance does not contain any of the contributed modules.  Any modules and dependencies you need for tests need to be specified in the tests `$modules` array.

Additional setup needed for a particular test such as creation of content types with specific fields, nodes etc can go into the setUp method.  

You can go to a url, fill in fields, click buttons, submit forms etc via functional tests.  There are built in functions such as createContentType, createNode, submitForm, pageTextContains that can be used to write functional tests.  Reviewing and using tests from similar modules is a good way to get started with writing tests for your own modules.

### Resources
* [Learning how to write tests for Drupal](https://www.marcdrummond.com/posts/2016/08/14/learning-to-write-tests-for-drupal)
* [Introduction to Testing in Drupal](https://drupalize.me/tutorial/introduction-testing-drupal?p=3056)
* [BrowserTestBase](https://api.drupal.org/api/drupal/core!tests!Drupal!Tests!BrowserTestBase.php/class/BrowserTestBase)
