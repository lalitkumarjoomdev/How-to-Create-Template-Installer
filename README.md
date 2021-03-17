# Steps

## Note:
Debug should be disabled in the astroid plugin after all CSS work done.

## 01 Hits 0
update prefix_content set hits = 0

## 02 Skip data for Tables 
1. _action_logs
2. _ucm_history
3. _users
4. _user_usergroup_map
5. _acym_configuration

[image1]: images/image1.jpg "Skip data for Tables "
![image1]

## 03 Check the options

1. IF NOT EXISTS (less efficient as indexes will be generated during table creation)
2. Truncate table before insert

[image2]: images/image2.jpg "Check the options"
![image2]


## 04 - First and last line fix.
**First Line**
```
SET FOREIGN_KEY_CHECKS=0;
SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";
```

**Last Line**
```
SET FOREIGN_KEY_CHECKS=1;
```

[image3]: images/image3.jpg "First and last line fix"
![image3]


## 05 Update User ID

Find the below code in database.php file.
```
'#__user_notes'      => array('created_user_id', 'modified_user_id'),
```

And add For JD Builder.
```
'#__jdbuilder_pages'  => array('created_by', 'modified_by'),
```

And add For TZ Portfolio
```
'#__tz_portfolio_plus_categories'      => array('created_user_id', 'modified_user_id'),
'#__tz_portfolio_plus_content'      => array('created_by', 'modified_by'),
```

**Note:** You have to 

**Path:** installation/model/database.php

[image4]: images/image4.jpg "Update User ID"
![image4]

## 06 Rename the Prefix name with (#_)

**E.g.**
Prefix Name = ``` ncwdf ```
Prefix with Table Name = ```ncwdf_acymailing_action```
After Change = ``` #__acymailing_action ```

## 07 Change the File Name and save and delete the files
* Change the file with **sample_templatedata.sql**
* Save in installation\sql\mysql folder
* Delete all .sql files expected **joomla.sql** and **sample_templatedata.sql**

## 08 Changes in language file

```
INSTL_SAMPLE_TEMPLATEDATA_SET="JD Restaurant Sample Data"
INSTL_SAMPLE_TEMPLATEDATA_SET_DESC="JD Restaurant Sample Data"
```
**Path:** \installation\language\en-GB\en-GB.ini

**Note:** Replace JD Restaurant with Current Template Name.

## 09 Add Default value in summary.xml file
Add the default value in **sample_file** field set.
```
default="sample_templatedata.sql"
```
[image5]: images/image5.jpg "Update Default Value"
![image5]

**Path:** \installation\model\forms

## 10 Add max_execution_time in index.php file
Add ```ini_set('max_execution_time', 300);``` in index.php file
[image6]: images/image6.jpg "Execution time"
![image6]
**Path:** installation/index.php

## 11 Install Themeing
* Rename **joomla.png** to **logo.png**
* Add the following code in index.php file below the second **<hr />** tag and change the coloring according to theme.

```
<style>
			.header {background: #fff; border: 0;}
         .btn-primary, .step.active span { background: #002d87;border-color: transparent; }
			.btn-primary:hover ,.btn-primary:focus { background: #002d87;}
         .nav-tabs>.active>a, .nav-tabs>.active>a:hover, .nav-tabs>.active>a:focus {color: #002d87;}
			.links-holder{text-align: center;}.links-holder ul {list-style: none;}.links-holder ul li {display: inline-block;}</style>
			<div class="links-holder">
				<ul>
				<li><a href="https://docs.joomdev.com" target="_blank">Documentation</a></li>
				<li> | </li>
				<li><a href="https://www.joomdev.com/forum" target="_blank">Forum</a></li>
				</ul>
			</div>
			<div style="text-align:center;margin:15px 0;"><a href="https://www.joomdev.com/" target="_blank"><img style="width:200px;" src="<?php echo $this->baseurl; ?>/template/images/joomdev-logo.png"></a></div>
```
* Save **joomdev-logo.png**(Copy from old installer) and **logo.png** (Theme Logo) in **images** older

**Path:** installation\template\
