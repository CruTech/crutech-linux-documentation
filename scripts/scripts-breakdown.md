# Script Explanation Breakdown

{% tabs %}
{% tab title="1. user-namer.pl" %}
## user-namer.pl

This script takes a list of campers and leaders and builds an input file for adding new users to the camp server. The output file has a user on each line and lists their username and inital password. This is the first script to run on a clean system \(A new system or after running clean-users.pl!\).

{% hint style="info" %}
**Usage:** `bin/user-namer.pl --user-list <specify file path> --out <specify file path>`
{% endhint %}

### _--user-list_

The user list is a text file for the operator to create which contains the first and last name of the user on each line.  
In whatever capitalisation that you put the names into, the script will transform all letters to lower-case \(since Linux is case-sensitive\).  
See `t/res/test-names.txt` to use as a reference and working example.

### _--word-list_

{% hint style="info" %}
The word-list flag is optional since you can add your own word list dictionary by specifying the path to the file.
{% endhint %}

The word list is a file containing words that are to be used in the process of generating passwords for the users. Each word must be singular and on a separate line.  
With all of the words in the word list, these words will be combined by randomly picking and choosing 2 words. The two words are then joined with a number in between.

### _--out_

The out flag is the filename where all of the generated user names and passwords will be written to.

{% hint style="info" %}
This file is compatible as input for the newusers-fix.pl script.
{% endhint %}

{% hint style="info" %}
User names must be unique although currently no checks are carried out by this generator.
{% endhint %}
{% endtab %}

{% tab title="2. newusers-fix.pl" %}
## **newusers-fix.pl**

This script creates new users on the server, it is the secod step for creating users for camp.

{% hint style="info" %}
**Usage:** `[sudo] in/newusers-fix.pl --user-file <specify file path>`
{% endhint %}

The new users fix script fixes an ongoing issue with the system newusers utility when adding and creating users in bulk. This script avoids the bug by breaking up the input file and calling newusers multiple times.  
This script requires the file path of the text file produced by user-namer.pl.

### _--user-file_

A newusers compatible file.
{% endtab %}

{% tab title="3. setup-users.pl" %}
## **setup-users.pl**

This script fills in a user's desktop shortcuts and other things relating to their home directory. It is the third and last step in setting up new users for camp.

{% hint style="info" %}
**Usage:** __`[sudo] bin/setup-users.pl`
{% endhint %}

The purpose of this script is to set up the user's home directory. The template directory is found in `templates/user-home-template`. The content of the template directory is copied into the user's home and ownership is given to the user.

It is recommended to create a user-home-template for each camp so that you can customise desktop and elective content required for each camp \(maybe have a different scripts directory for each camp?\).

You can rerun this script multiple times but be aware that it will overwrite any changes a user may have made to a file created from the user home template.

N.B. If you need to add a templated file \(one in which it's content changes based on the user\) this can be added via calling the add-template-to-homes.pl script.
{% endtab %}

{% tab title="3.1 add-template-to-homes.pl" %}
## **add-template-to-homes.pl**

{% hint style="info" %}
**Usage:** `[sudo] bin/add-template-to-homes.pl --template <specify file path> --out <specify file path relative to user home>  
  
# Example:  
bin/add-template-to-homes.pl --template templates/gish.desktop.template --out Desktop/gish.desktop`
{% endhint %}

A script for adding a templated files to user homes.   
  
It is not recommended to use this script to add elective files to camp uesrs. Elective files should be added to the template directory used by setup users.

### _**--template**_

The path to a template file to process.

### _**--out**_

The file name to output processed templates to. The output path is relative to the subject user's home directory.

### **Use case**

You can use this script for one off additions, however as this altered file may not be in the user home template, you may need to add it to find-user-files.pl's ignored files list.

If you have a template which is required dureing regular setup, you should add the call as a line in setup-users.pl
{% endtab %}

{% tab title="3.2 setup-on-login-hooks.pl" %}
## **setup-on-login-hooks.pl**

{% hint style="info" %}
**Usage:** `[sudo] bin/setup-on-login-hooks.pl`
{% endhint %}

Adds and appends actions to the user's .profile, which will be executed when the user logs into their profile.  
  
This script is called by setup-users.pl. The script currently adds a symlink to the virtual Starcraft directory to allow saving of replays to the user's home.
{% endtab %}

{% tab title="4. find-user-files.pl" %}
## **find-user-files.pl**

{% hint style="info" %}
**Usage:** `bin/find-user-files.pl [--template <specify directory path>] [--ignore-list <specify file path>] --archive-dir <specify directory path>`
{% endhint %}

The find user files script takes all of the user home directories zips archives the files to the desired location. The user home directories are differentiated against an example template, the files are then collected if they are new or changed.

### _**--template**_

Defaults to 'templates/user-home-template' the user home template directory of setup-users.pl. The user home template will be used to determine which files have been changed or added by a user.

### _**--ignore-list**_

A path to a text file that contains a list of files to be ignored when comparing user home directories, defaults to: 'config/ignore-file-list.txt'.  
The format of the ignore list file is one file path per line and file paths are relative to a user's home directory, e.g. '/home/crutech/Documents/some-big-file' would be 'Documents/some-big/file'.

{% hint style="info" %}
There are currently no wild-card features so all names are literal.
{% endhint %}

### _**--archive-dir**_

A directory were the zipped user home files will be saved to.
{% endtab %}

{% tab title="5. clean-users.pl" %}
## **clean-users.pl**

{% hint style="info" %}
**Usage:** `[sudo] bin/clean-users.pl`
{% endhint %}

The clean users script cleans up all of the users after a camp.

{% hint style="info" %}
**WARNING:** This literally deletes the users directories on the server. 
{% endhint %}

{% hint style="info" %}
Please ensure that you use the find-user-files script first before executing this script.
{% endhint %}
{% endtab %}
{% endtabs %}

