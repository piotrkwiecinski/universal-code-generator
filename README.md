# Universal Code Generator Tool

This tool can be used as base for creating code generators for specific frameworks

## Usage

0. Create your own generator project:

    * Check an example here: [magento2-code-generator](https://github.com/staempfli/magento2-code-generator)

0. Add this project as dependency

    ```
    composer require "staempfli/universal-code-generator":"~1.0"
    composer update
    ``` 

0. Copy needed default configuration file

    * `$ cp vendor/staempfli/universal-code-generator/config/default-properties.yml.dist config/default-properties.yml`
    
0. You need to create a PHP script to define the console application: 

    * We recommend to do that into the `bin` folder
       
        `cd bin && vim <command_name>`

    * Add the following content to this file:
    ```
    #!/usr/bin/env php
    <?php
    // application.php
    
    require __DIR__ .'/../vendor/autoload.php';
    
    /**
    * Shortcut constant for the project root directory
    */
    define('BP', dirname(__DIR__));
    /**
    * Command name
    */
    define('COMMAND_NAME', basename(__FILE__));
    
    // Init Console Application
    use Staempfli\UniversalGenerator\Application;
    
    $application = new Application('@git-version@');
    
    /**
    * You can add new commands or extend exiting ones to add custom functionality
    * - Check default commands in Staempfli\UniversalGenerator\Application
    * - To add or extend commands you must use the method $application->addGeneratorCommand
    */
    // $application->addGeneratorCommand('template:generate', 'VendorName\ProjectName\Command\TemplateGenerateCommand');
    
    $application->run();
    ```

0. Usually you might want to extend the default `template:generate` command. You can do that as follows:
 
    *  [Extend Template Generate Command](docs/extend-generate-command.md)
    
0. Create the templates that will be generated:

    *  [How to create templates](docs/createTemplates.md)


