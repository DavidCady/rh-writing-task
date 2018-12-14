---
title: configuring ownCloud Server
last_updated: 13/12/2016
sidebar: mydoc_sidebar
permalink: configure.html
---

For the Purpose of the Quick Start guide, this topic describes only the configuration required to for the tasks described in the *Using ownCloud* section of this document. For more detailed configuration information see the *ownCloud Server Admin Manual*.

## PHP Configuration

For ownCloud to work successfully, the settings described in this section must be configured correctly. Known settings causing issues are listed here. However, there might be other settings that cause unwanted behavior. Apart from the settings listed here, it is recommended to use the default `php.ini` settings unless there is a specific requirement to change them and you understand what the implications are. 

**Important:** Changes you make to `php.ini` might require you to configure multiple ini files. this is true the date.timezone setting, for example.

### PHP versions in Paths

If you are using PHP 7.0 or higher, you must amend the path for `php.ini` used by the web server and the php-cli. For example, for the apache webserver path you must replace `php_version` with the version number of the installed PHP.    

 `/etc/php/[php_version]/apache2/php.ini`
  
The path for `php.ini`used by php-cli, which is used for ownCloud CRON jobs, must also be changed.    

   `/etc/php/[php_version]/cli/php.ini`
   
### PHP.ini Settings

The following table describes the attributes in a `php.ini` file that you need to verify are set correctly.

| Attribute | Recommended Setting | Issue |
| --------- | ------------------- | ----- |
| `session.auto_start` | 0 | An incorrect settings can result in inability to log in to ownCloud through the web UI. |
| `enable_post_data_reading` | 1 | An incorrect settings can result in inability to log in to ownCloud through the web UI.|
| `post_max_size` | 512M | An incorrect setting can result in memory issues. **Important** The value must be specified as M for megabyte, not MB |
| `realpath_cache_size` | See Determining realpath_cache_size below | The value must be increased on systems where PHP opens many files, to reflect the number of file operations performed. |

### Determining realpath_cache_size

The `realpath_cache_size` attiubute determines the size of the realpath cache used by PHP. You might need to increase the default value in the `php.ini` file depending on how many fies PHP opens at any one time.

To derive a working value, assume that PHP requires 112 bytes per file path needed. Therefore, if the cache is set to 4M, the cache can hold around 37,000 items at any one time.

You can run cloc to obtain the quantity of PHP files. 

**Note:** The cloc Package is available from  Sourceforge. It can be installed by running the following command:    

    `sudo apt-get install cloc`

The following is an example of running the cloc command and the resulting output:

    `sudo cloc /var/www/owncloud --exclude-dir=data --follow-links
    12179 text files.
    11367 unique files.
    73126 files ignored.

    http://cloc.sourceforge.net v 1.60  T=1308.98 s (6.4 files/s, 1283.5 lines/s)
     --------------------------------------------------------------------------------
    Language                      files          blank        comment           code
     --------------------------------------------------------------------------------
    PHP                            4896          96509         285384         558135
  

In the above example, there are 4896 fies open. With 112 bytes required per file, and assuming a factor of three for a symlinked instance, the formula becomes 4896 * 3 * 112 = 1.6MB This result shows that you can run with the PHP setting of 4M on two instances of ownCloud.   