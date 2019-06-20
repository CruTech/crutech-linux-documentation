# Scripts

{% tabs %}
{% tab title="user-namer.pl" %}
{% hint style="info" %}
**Usage:** bin/user-namer.pl --user-list &lt;specify file path&gt;  --out &lt;specify file path&gt;
{% endhint %}

_--user-list_  
The user list is a text file for the operator to create which contains the first and last name of the user on each line.  
In whatever capitalisation that you put the names into, the script will transform all letters to lowercase \(since Linux is case-sensitive\).  
See \`t/res/test-names.txt\` to use as a reference and working example.

_--word-list_

{% hint style="info" %}
The word-list flag is optional since you can add your own word list dictionary by specifying the path to the file.
{% endhint %}

The word list is a file containing words that are to be used in the process of generating passwords for the users. Each word must be singular and on a separate line.  
With all of the words in the word list, these words will be combined by randomly picking and choosing 2 words. The two words are then joined with a number in between.

_--out_  
The out flag is the file of which to write all of the generated usernames and passwords to.
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

