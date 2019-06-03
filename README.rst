## PhpStorm安装方法 github地址：https://github.com/FriendsOfPHP/PHP-CS-Fixer
#### Step 1: 下载并安装工具
```
sudo curl -L http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -o /usr/local/bin/php-cs-fixer
sudo curl -L https://github.com/FriendsOfPHP/PHP-CS-Fixer/releases/download/v2.3.1/php-cs-fixer.phar -o /usr/local/bin/php-cs-fixer
#or
sudo wget http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -O /usr/local/bin/php-cs-fixer
sudo wget https://github.com/FriendsOfPHP/PHP-CS-Fixer/releases/download/v2.3.1/php-cs-fixer.phar -O /usr/local/bin/php-cs-fixer

sudo chmod a+x /usr/local/bin/php-cs-fixer
#update
sudo /usr/local/php/bin/php /usr/local/bin/php-cs-fixer selfupdate
```
#### Step 2: 打开 Settings -> Tools -> External Tools
![github](https://github.com/fupengfei058/PHP-CS-Fixer/tree/2.15/pic/1.png)

#### Step 3:按照下图配置
![github](https://github.com/fupengfei058/PHP-CS-Fixer/tree/2.15/pic/2.jpg)

#### Step 4:创建一个名为.php_cs的配置文件，内容如下，可自行调整
```php
<?php
$header = <<<'EOF'
This file is part of PHP CS Fixer.
(c) fupengfei058@gmail.com <fupengfei058@gmail.com>
This source file is subject to the MIT license that is bundled
with this source code in the file LICENSE.
EOF;
return PhpCsFixer\Config::create()
    ->setRiskyAllowed(true)
    ->setRules([
        '@Symfony' => true,
        '@Symfony:risky' => true,
        'array_syntax' => ['syntax' => 'short'],
        'combine_consecutive_unsets' => true,
        // one should use PHPUnit methods to set up expected exception instead of annotations
        'general_phpdoc_annotation_remove' => ['expectedException', 'expectedExceptionMessage', 'expectedExceptionMessageRegExp'],
        'header_comment' => array('header' => $header),
        'heredoc_to_nowdoc' => true,
        'no_extra_consecutive_blank_lines' => ['break', 'continue', 'extra', 'return', 'throw', 'use', 'parenthesis_brace_block', 'square_brace_block', 'curly_brace_block'],
        'no_unreachable_default_argument_value' => true,
        'no_useless_else' => true,
        'no_useless_return' => true,
        'ordered_class_elements' => true,
        'ordered_imports' => true,
        'php_unit_strict' => true,
        'phpdoc_add_missing_param_annotation' => true,
        'no_trailing_comma_in_singleline_array' => true, //单行数组最后一个元素不添加逗号
        'phpdoc_order' => true,
        'psr4' => true,
        'strict_comparison' => false,
        'strict_param' => false, //如果这里设置为true，发现in_array方法会默认加上第3个参数为true，这使得in_array会对前两个参数值的类型也会做严格的校验，建议设置为false
        'binary_operator_spaces' => ['align_double_arrow' => true, 'align_equals' => true],
        'concat_space' => ['spacing' => 'one'],
        'no_empty_statement' => true,
        'simplified_null_return' => true,
        'no_extra_consecutive_blank_lines' => true,
        'pre_increment' => false, //设置为false，$i++ 不会变成 ++$i
        'increment_style' => false, //设置为false，$i++ 不会变成 ++$i
    'phpdoc_var_without_name' => false,
    'no_useless_else' => false //不设置的话，默认是true，即会删除无用的else，如果if条件中有return或者exit等关键字会直接删除else，特殊情况下会影响代码逻辑，建议设置成false
    ])
    ->setFinder(
        PhpCsFixer\Finder::create()
            ->exclude('vendor')
            ->in(__DIR__)
    )
    ->setUsingCache(false)
;
```
#### Step 5:配置phpStrom快捷键
进入phpStrom-> Settings->Appearance & Behavior -> Keymap

使用查找 php-cs-fixer
![github](https://github.com/fupengfei058/PHP-CS-Fixer/tree/2.15/pic/3.png)
![github](https://github.com/fupengfei058/PHP-CS-Fixer/tree/2.15/pic/4.png)


## Sublime Text安装方法
#### Step 1:下载PHP code sniffer插件安装包 地址:https://github.com/benmatselby/sublime-phpcs;

Use Sublime Text’s Package Control (Preferences -> Package Control -> Install Package -> Phpcs) to install this plugin. This is the recommended installation path.

### Step 2: 下载php-cs-fixer.phar

```
sudo curl -L http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -o /usr/local/bin/php-cs-fixer
sudo curl -L https://github.com/FriendsOfPHP/PHP-CS-Fixer/releases/download/v2.3.1/php-cs-fixer.phar -o /usr/local/bin/php-cs-fixer
#or
sudo wget http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -O /usr/local/bin/php-cs-fixer
sudo wget https://github.com/FriendsOfPHP/PHP-CS-Fixer/releases/download/v2.3.1/php-cs-fixer.phar -O /usr/local/bin/php-cs-fixer

sudo chmod a+x /usr/local/bin/php-cs-fixer
#update
sudo /usr/local/php/bin/php /usr/local/bin/php-cs-fixer selfupdate
```

### Step 3:安装PHP_CodeSniffer http://pear.php.net/package/PHP_CodeSniffer/download 下载地址： http://download.pear.php.net/package/PHP_CodeSniffer-3.0.0RC4.tgz

```
tar zxvf PHP_CodeSniffer-3.0.0RC4.tgz
sudo mv PHP_CodeSniffer-3.0.0RC4 /usr/local

echo "export PATH=/usr/local//usr/local/PHP_CodeSniffer-3.0.0RC4/bin/:$PATH" >> /etc/profile
#
source /etc/profile
```
### Step 4:配置 拷贝PHp Code Sniffer的默认配置到用户自定义配置中： 然后将以下参数调整为对应的目录：

```
"phpcs_php_path": "/usr/local/php/bin/php",
"phpcs_executable_path": "/usr/local/PHP_CodeSniffer-3.0.0RC4/bin/phpcs",
"phpcbf_executable_path": "/usr/local/PHP_CodeSniffer-3.0.0RC4/bin/phpcbf",
"phpmd_executable_path": "",
"php_cs_fixer_executable_path": "/usr/local/bin/php-cs-fixer",
```

快捷键：
```
{ "keys": ["ctrl+alt+l"], "command": "phpcs_fix_this_file", "args": {"tool": "CodeBeautifier"}}
```

配置内容：
```
{
    // PHP-CS-Fixer settings

    // Fix the issues on save
    "php_cs_fixer_on_save": true,

    // Show the quick panel
    "php_cs_fixer_show_quick_panel": false,

    // Path to where you have the php-cs-fixer installed
    "php_cs_fixer_executable_path": "/usr/local/bin/php-cs-fixer",
/usr/local/bin/php-cs-fixer --quiet --verbose --config="/home/qianxun/website/lnmp/.php_cs" fix "$FileDir$/$FileName$"
    // Additional arguments you can specify into the application
    "php_cs_fixer_additional_args": {
        "--config":"/home/qianxun/website/lnmp/.php_cs"
    },
}
```