# Script Explanation Breakdown

{% tabs %}
{% tab title="user-namer.pl" %}
## user-namer.pl

{% hint style="info" %}
**Usage:** `bin/user-namer.pl --user-list <specify file path> --out <specify file path>`
{% endhint %}

### _--user-list_

The user list is a text file for the operator to create which contains the first and last name of the user on each line.  
In whatever capitalisation that you put the names into, the script will transform all letters to lowercase \(since Linux is case-sensitive\).  
See `t/res/test-names.txt` to use as a reference and working example.

### _--word-list_

{% hint style="info" %}
The word-list flag is optional since you can add your own word list dictionary by specifying the path to the file.
{% endhint %}

The word list is a file containing words that are to be used in the process of generating passwords for the users. Each word must be singular and on a separate line.  
With all of the words in the word list, these words will be combined by randomly picking and choosing 2 words. The two words are then joined with a number in between.

### _--out_

The out flag is the file of which to write all of the generated usernames and passwords to.

{% hint style="info" %}
This file is compatible as input for the adduser.pl script.
{% endhint %}

{% hint style="info" %}
Usernames must be unique although currently no checks are carried out by this generator.
{% endhint %}
{% endtab %}

{% tab title="newusers-fix.pl" %}
## **newusers-fix.pl**

{% hint style="info" %}
**Usage:** `bin/newusers-fix.pl --user-file <specify file path>`
{% endhint %}

The new users fix script fixes an ongoing issue with adding and creating users in bulk, which causes the script to give a crash \(segfault\).  
This script requires the file path of the text file produced by user-namer.pl.

### _--user-file_

A newusers compatible file.
{% endtab %}

{% tab title="setup-users.pl" %}
## **setup-users.pl**

{% hint style="info" %}
**Usage:** __`bin/setup-users.pl`
{% endhint %}

The purpose of this script is to setup the user's home directory. The template directory is found in `templates/user-home-template`. Templates can be added via calling the add-template-to-homes.pl script.
{% endtab %}

{% tab title="add-template-to-homes.pl" %}
## **add-template-to-homes.pl**

{% hint style="info" %}
**Usage:** `bin/add-template-to-homes.pl --template <specify directory path> --out <specify directory path>`
{% endhint %}

A script for adding a template file to user homes for a camp. Use this script to add elective files to the desktop of each campers directory.

### _**--template**_

The path to a template file to process.

### _**--out**_

The file name to output processed templates to. The output path is relative to the subject user's home directory.
{% endtab %}

{% tab title="find-user-files.pl" %}
## **find-user-files.pl**

{% hint style="info" %}
**Usage:** `bin/find-user-files.pl --template <specify directory path> --ignore-list <specify file path> --archive-dir <specify directory path>`
{% endhint %}

The find user files script takes all of the user home directories zips archives the files to the desired location. The user home directories are differentiated against an example template, the files are then collected if they are new or changed.

### _**--template**_

A path to a directory to which user homes will be diffed against. The results of this difference calculate and determine which files have been changed or added by the user.

### _**--ignore-list**_

A path to a text file that contains a list of files to be ignored when comparing user home directories.  
The format the ignore list file is one file path per line and file paths are relative to a user's home directory.

{% hint style="info" %}
There are currently no wild-card features so all names are literal.
{% endhint %}

### _**--archive-dir**_

A path or directory for the zipped user home files to be saved to.
{% endtab %}

{% tab title="clean-users.pl" %}
## **clean-users.pl**

{% hint style="info" %}
**Usage:** `bin/clean-users.pl`
{% endhint %}

The clean users script cleans up all of the users after a camp.

{% hint style="info" %}
**WARNING:** This literally deletes the users directories on the server. 
{% endhint %}

{% hint style="info" %}
Please ensure that you use the find-user-files script first before executing this script.
{% endhint %}
{% endtab %}

{% tab title="setup-on-login-hooks.pl" %}
## **setup-on-login-hooks.pl**

{% hint style="info" %}
**Usage:** `bin/setup-on-login-hooks.pl`
{% endhint %}

Adds and appends actions to the user's .profile, which will be executed when the user logs into their profile.
{% endtab %}
{% endtabs %}

