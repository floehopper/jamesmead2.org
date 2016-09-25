--- 
permalink: adding-a-user-in-osx-on-command-line
created_at: 2011-01-20 18:13:42 +00:00
updated_at: 2011-01-20 18:13:42 +00:00
title: Adding a User in OSX on Command Line
description: OSX equivalent to the Linux useradd & groupadd commands.
keywords: mac osx add create user group dscl useradd groupadd linux
guid: 83030ef8-7cf3-41cb-bc24-b954297d7248
---

Heavily based on answers to this [question](http://serverfault.com/questions/20702/how-do-i-create-user-accounts-from-the-terminal-in-mac-os-x-10-5) on [serverfault.com](http://serverfault.com/).

List existing group IDs in numerical order to choose an unused one for new group :-

    $ dscl . -list /Groups PrimaryGroupID | awk '{print $2}' | sort -n

Create the new group 'newgroup' and assign it an ID :-

    $ sudo dscl . -create /Groups/newgroup
    $ sudo dscl . -create /Groups/newgroup PrimaryGroupID 1000

View the new group :-

    $ dscl . -read /Groups/newgroup
    AppleMetaNodeLocation: /Local/Default
    GeneratedUID: 423AF02C-F053-41E0-ABCD-33127EF9A9CA
    PrimaryGroupID: 1000
    RecordName: newgroup
    RecordType: dsRecTypeStandard:Groups

List existing user IDs in numerical order to choose an unused one for new user :-

    $ dscl . -list /Users UniqueID | awk '{print $2}' | sort -n

Create the new user 'newuser' and assign various attributes :-

    $ sudo dscl . -create /Users/newuser
    $ sudo dscl . -create /Users/newuser UserShell /bin/bash
    $ sudo dscl . -create /Users/newuser RealName "New User"
    $ sudo dscl . -create /Users/newuser UniqueID "1000"
    $ sudo dscl . -create /Users/newuser PrimaryGroupID 1000

View the new user :-

    $ dscl . -read /Users/newuser
    AppleMetaNodeLocation: /Local/Default
    GeneratedUID: 47D6D841-C7F1-4962-9F7E-167E8BFC3A91
    PrimaryGroupID: 1000
    RealName:
     Application
    RecordName: newuser
    RecordType: dsRecTypeStandard:Users
    UniqueID: 1000
    UserShell: /usr/bash
