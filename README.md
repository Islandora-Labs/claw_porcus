## Introduction
This is a demo module for Islandora CLAW. It illustrates the modeling of a content type and creation of a drupal module for CLAW.


## Steps to create claw_porcus
### 1 - Create a new Media bundle
* Go to `/admin/structure/media/add`
* Provide a label to the bundle: PORCUS_TEXT
* Lave the type provier as Generic media
* Go to the Manage fields of the new media bundle: `/admin/structure/media/manage/porcus_text/fields`
* Add a new file field

### 2 - Create a new Fedora Resource type bundle
* Go to `/admin/structure/fedora_resource_type`
* Provide a label to the fedora resource type: Islandora Porcus Object
* Go to Manage fields of the new fedora resource type: `/admin/structure/fedora_resource_type/islandora_porcus_object/edit/fields`
* Add a new description field (Text (plain, long))
* Add a new field Reference type Other
* Chose 'Type of item to reference' as Media
* Select the Default 'Reference method' and PORCUS_TEXT as the 'Bundles' 
* Go to Manage form display: `/admin/structure/fedora_resource_type/islandora_porcus_object/edit/form-display`
* Specify the porcus_text WIDGET as Inline entity form - complex

### 3 - Creating a module using Drupal console
* ssh into the vagrant `vagrant ssh`
* Go to drupal console and execute command to create a module `ubuntu@claw:/var/www/html/drupal$ drupal generate:module`
* Execute the interactive commands as below:
```
ubuntu@claw:/var/www/html/drupal$ drupal generate:module

 // Welcome to the Drupal module generator

 Enter the new module name:
 > Islandora Porcus

 Enter the module machine name [islandora_porcus]:
 > 

 Enter the module Path [/modules/custom]:
 > /modules/contrib 

 Enter module description [My Awesome Module]:
 > Islandora Porcus

 Enter package name [Custom]:
 > 

 Enter Drupal Core version [8.x]:
 > 

 Do you want to generate a .module file (yes/no) [yes]:
 > 

 Define module as feature (yes/no) [no]:
 > 

 Do you want to add a composer.json file to your module (yes/no) [yes]:
 > 

 Would you like to add module dependencies (yes/no) [no]:
 > yes      

 Module dependencies separated by commas (i.e. context, panels):
 > islandora

 Do you want to generate a unit test class (yes/no) [yes]:
 > no

 Do you want to generate a themeable template (yes/no) [yes]:
 > no


 Do you confirm generation? (yes/no) [yes]:
 >    

Generated or updated files

 1 - /var/www/html/drupal/web/modules/contrib/islandora_porcus/islandora_porcus.info.yml
 2 - /var/www/html/drupal/web/modules/contrib/islandora_porcus/islandora_porcus.module
 3 - /var/www/html/drupal/web/modules/contrib/islandora_porcus/composer.json
ubuntu@claw:/var/www/html/drupal$ 
```

### 4 - Create RDF Mapping for the bunldes (islandora_porcus_object and PORCUS_TEXT)
* Adopt and modify an existing RDF Mapping such as `https://github.com/Islandora-CLAW/islandora_image/blob/8.x-1.x/config/install/rdf.mapping.fedora_resource.islandora_image.yml` to create the RDF mapping of the target bundle
* Go to the form to import a single configuration: `/admin/config/development/configuration/single/import`
* Select 'Configuration type' RDF mapping and import the mapping
* Repeat it for the other bundle

### 5 - Exporting and modifing configuration
* Export the following configuration types:
    * Fedora resource type 
    * Media bundle 
    * Field 
    * Field storage 
    * RDF mapping
    * Entity form display
    * Entity view display
* Create a `config/install` folder and copy the above configurations into that folder


